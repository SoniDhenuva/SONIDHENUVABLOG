---
title: 1.9 Method Signatures
layout: post
type: hacks
comments: true
courses: {csa: {week: 6}}
type: ccc
---

## Popcorn Hack 1 - Maximum Values
<br>

```java
public class MaxUtility {

    // Max of two integers
    public static int maxIntValue(int num1, int num2) {
        return (num1 >= num2) ? num1 : num2;
    }

    // Max of two doubles
    public static double maxDoubleValue(double num1, double num2) {
        return (num1 >= num2) ? num1 : num2;
    }

    public static void main(String[] args) {
        System.out.println(maxIntValue(3, 9));      // 9
        System.out.println(maxIntValue(-2, -7));    // -2
        System.out.println(maxDoubleValue(3.5, 2.9)); // 3.5
        System.out.println(maxDoubleValue(2, 2.0));   // 2.0
    }
}
```

## Popcorn Hack 2
<br>

```java
public class PrintUtility {

    static void printData(int value) {
        System.out.println("int:" + value);
    }

    static void printData(String value) {
        System.out.println("str:" + value);
    }

    public static void main(String[] args) {
        printData(42);           // int:42
        printData("hello");      // str:hello
        printData('A' + "!");    // str:A!
    }
}
```

## FRQ 
<br>

```java
public class FRQUtilities {

    // --- FRQ 1: Calculate the sum of all integers in a range (inclusive) ---
    public static int sumRange(int start, int end) {
        if (start > end) return 0;
        int sum = 0;
        for (int i = start; i <= end; i++) {
            sum += i;
        }
        return sum;
    }

    // --- FRQ 2: Overloaded methods to find area ---
    // Circle area
    public static double area(double radius) {
        return Math.PI * Math.pow(radius, 2);
    }

    // Rectangle area
    public static int area(int width, int height) {
        return width * height;
    }

    // --- FRQ 3: Overloaded methods to format scores ---
    // Format as "earned/total"
    public static String formatScore(int earned, int total) {
        return earned + "/" + total;
    }

    // Format as "percent%"
    public static String formatScore(double percent) {
        return String.format("%.1f%%", percent);
    }

    // --- Main Method: Test all methods ---
    public static void main(String[] args) {
        System.out.println(sumRange(1, 5));        // Output: 15
        System.out.println(area(3.0));             // Output: ~28.2743
        System.out.println(area(3, 4));            // Output: 12
        System.out.println(formatScore(45, 50));   // Output: 45/50
        System.out.println(formatScore(92.35));    // Output: 92.4%
    }
}
```

## HOMEWORK: coding task
<br>

```java
public class OverloadExamples {

    // --- 1. Overloads of abs ---
    static int abs(int x) {
        return (x < 0) ? -x : x;
    }

    static double abs(double x) {
        return (x < 0) ? -x : x;
    }

    static long abs(long x) {
        return (x < 0) ? -x : x;
    }

    // --- 2. Overloads of concat ---
    static String concat(String str1, String str2) {
        return str1 + str2;
    }

    static String concat(String str, int times) {
        String result = "";
        for (int i = 0; i < times; i++) {
            result += str;
        }
        return result;
    }

    // --- 3. Overloads of show ---
    static void show(int x) {
        System.out.println("int");
    }

    static void show(double x) {
        System.out.println("double");
    }

    static void show(long x) {
        System.out.println("long");
    }

    // --- Main method to test all overloads ---
    public static void main(String[] args) {
        // Testing abs overloads
        System.out.println("abs(-5): " + abs(-5));
        System.out.println("abs(-5.5): " + abs(-5.5));
        System.out.println("abs(-5000000000L): " + abs(-5000000000L));

        System.out.println();

        // Testing concat overloads
        System.out.println("concat(\"Hi\", \"There\"): " + concat("Hi", "There"));
        System.out.println("concat(\"Go\", 3): " + concat("Go", 3));

        System.out.println();

        // Testing show overloads
        show(7);     // int literal
        show(7L);    // long literal
        show(7.0);   // double literal
    }
}

// Run it
OverloadExamples.main(null);
```
- The abs method picks the right version depending on the type of number you give it. So if you do abs(-5), it uses the int version because -5 is an integer. If you do abs(-5.5), it uses the double version since -5.5 is a double. And abs(-5000000000L) uses the long version because of the long number. For concat, concat("Hi", "There") just sticks the two strings together, but concat("Go", 3) repeats "Go" three times. The show method prints what type of number you gave it: show(7) prints "int", show(7L) prints "long", and show(7.0) prints "double".

## Homework 2

```java
public class FRQOverloadsRewritten {

    // FRQ 1: findCharIndex
    // Assumes:
    // - str is not null
    // - search is case sensitive
    // - returns -1 if char not found
    static int findCharIndex(char targetChar, String str) {
        for (int i = 0; i < str.length(); i++) {
            if (str.charAt(i) == targetChar) {
                return i;
            }
        }
        return -1;
    }

    // FRQ 1: findSubstringIndex
    // Assumes:
    // - str and subStr are not null
    // - subStr is non-empty
    // - returns -1 if substring not found
    static int findSubstringIndex(String subStr, String str) {
        int subLen = subStr.length();
        int strLen = str.length();

        for (int i = 0; i <= strLen - subLen; i++) {
            boolean isMatch = true;
            for (int j = 0; j < subLen; j++) {
                if (str.charAt(i + j) != subStr.charAt(j)) {
                    isMatch = false;
                    break;
                }
            }
            if (isMatch) return i;
        }
        return -1;
    }

    // FRQ 2: limitRange for int
    // Swaps low and high if they are in wrong order
    static int limitRange(int value, int low, int high) {
        if (low > high) {
            int temp = low;
            low = high;
            high = temp;
        }
        if (value < low) return low;
        if (value > high) return high;
        return value;
    }

    // FRQ 2: limitRange for double
    static double limitRange(double value, double low, double high) {
        if (low > high) {
            double temp = low;
            low = high;
            high = temp;
        }
        if (value < low) return low;
        if (value > high) return high;
        return value;
    }

    // Main test
    public static void main(String[] args) {
        // Test findCharIndex
        System.out.println(findCharIndex('a', "banana"));   // 1
        System.out.println(findCharIndex('z', "banana"));   // -1
        // Test findSubstringIndex
        System.out.println(findSubstringIndex("ana", "banana"));  // 1
        System.out.println(findSubstringIndex("nana", "banana")); // 2
        System.out.println(findSubstringIndex("zzz", "banana"));  // -1

        System.out.println();

        // Test limitRange for int
        System.out.println(limitRange(5, 1, 10));     // 5
        System.out.println(limitRange(-5, 1, 10));    // 1
        System.out.println(limitRange(15, 1, 10));    // 10
        System.out.println(limitRange(5, 10, 1));     // 5 (swap handled)

        // Test limitRange for double
        System.out.println(limitRange(3.5, 2.0, 5.0));  // 3.5
        System.out.println(limitRange(1.0, 2.0, 5.0));  // 2.0
        System.out.println(limitRange(8.0, 2.0, 5.0));  // 5.0
        System.out.println(limitRange(4.0, 7.0, 2.0));  // 4.0 (swap handled)
    }
}

```