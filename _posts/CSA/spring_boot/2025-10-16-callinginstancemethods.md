---
title: 1.14 Calling Instance Methods
layout: post
type: hacks
comments: true
courses: {csa: {week: 8}}
type: ccc
---

## Popcorn Hack 1
<br>
- Add another property to the dog class for breed.
- Add another method to the dog class that prints “My dog name is a breed!”
- Create a new object of this class and call the method.

```java
// Work by Soni Dhenuva
public class Dog {

    String name;
    String breed;

    public Dog(String name, String breed) {
        this.name = name;
        this.breed = breed;
    }

    public void printInfo() {
        System.out.println("My dog " + name + " is a " + breed + "!");
    }

    public static void main(String[] args) {
        Dog myDog = new Dog("Buddy", "Golden Retriever");
        myDog.printInfo();
    }
}
```
```
My dog Buddy is a Golden Retriever
```


## Popcorn Hack #2
<br>
-Add on to the previous counter class and add three more methods for subtraction, multiplication, and division.
-Call all five methods outside of the class.

```java
// Work by Soni Dhenuva

public class Counter {
    private int count;

    public void add(int x) {
        count += x;
    }

    public void subtract(int x) {
        count -= x;
    }

    public void multiply(int x) {
        count *= x;
    }

    public void divide(int x) {
        if (x != 0) {
            count /= x;
        } else {
            System.out.println("no divide 0");
        }
    }

    public int getCount() {
        return count;
    }
}

// Use it:
public class Main {
    public static void main(String[] args) {
        Counter c = new Counter();

        c.add(10);
        System.out.println(c.getCount());

        c.subtract(3);
        System.out.println(c.getCount());

        c.multiply(4);
        System.out.println(c.getCount());

        c.divide(2);
        System.out.println(c.getCount());

        c.divide(0); // test divide by zero
    }
}
```
```
10
7
28
14
no divide 0
```

## Homework

```java
// Work by Soni Dhenuva
// StudentGradeTracker.java

public class Student {
    // Instance variables
    private String name;
    private int totalPoints;
    private int numAssignments;

    // Constructor gives name and sets totals to 0
    public Student(String name) {
        this.name = name;
        this.totalPoints = 0;
        this.numAssignments = 0;
    }

    // addGrade void method that updates totals
    public void addGrade(int points) {
        totalPoints += points;
        numAssignments++;
    }

    // getAverage returns current avg as a double
    public double getAverage() {
        if (numAssignments == 0) return 0.0;
        return (double) totalPoints / numAssignments;
    }

    // getLetterGrade returns letter grade based on the avg
    public String getLetterGrade() {
        double avg = getAverage();
        if (avg >= 90.0) return "A";
        if (avg >= 80.0) return "B";
        if (avg >= 70.0) return "C";
        if (avg >= 60.0) return "D";
        return "F";
    }

    // printReport void method to show a report
    public void printReport() {
        double avg = getAverage();
        String avgFormatted = String.format("%.2f", avg);
        String letter = getLetterGrade();
        String status;
        switch (letter) {
            case "A": status = "Excellent work!"; break;
            case "B": status = "Great job!"; break;
            case "C": status = "Keep working hard!"; break;
            case "D": status = "Needs improvement."; break;
            default:  status = "Significant improvement needed.";
        }

        System.out.println();
        System.out.println("--- " + name + "'s Grade Report ---");
        System.out.println("Student Name: " + name);
        System.out.println("Total Points: " + totalPoints);
        System.out.println("Assignments Completed: " + numAssignments);
        System.out.println("Current Average: " + avgFormatted);
        System.out.println("Letter Grade: " + letter);
        System.out.println("Status: " + status);
        System.out.println();
        System.out.println("========================================");
    }
}

// Separate class with main to shwo usage
class StudentGradeTracker {
    public static void main(String[] args) {
        System.out.println("=== Student Grade Tracker System ===");

        // Creating student Emma
        System.out.println();
        System.out.println("Creating student: Soni Dhenuva");
        Student soni = new Student("Soni Dhenuva");
        System.out.println("Student created successfully!");

        System.out.println();
        System.out.println("--- Adding Grades for Soni ---");
        System.out.println("Adding grade: 95 points");
        soni.addGrade(95);
        System.out.println("Adding grade: 88 points");
        soni.addGrade(88);
        System.out.println("Adding grade: 92 points");
        soni.addGrade(92);
        System.out.println("Adding grade: 85 points");
        soni.addGrade(85);

        soni.printReport(); // prints Soni's full report

        // Creating student Nora
        System.out.println();
        System.out.println("Creating student: Nora Ahadian");
        Student nora = new Student("Nora Ahadian");
        System.out.println("Student created successfully!");

        System.out.println();
        System.out.println("--- Adding Grades for Nora ---");
        System.out.println("Adding grade: 78 points");
        nora.addGrade(78);
        System.out.println("Adding grade: 82 points");
        nora.addGrade(82);
        System.out.println("Adding grade: 75 points");
        nora.addGrade(75);

        nora.printReport(); // prints Nora's full report

        // Final summary (shosw calling getAverage and getLetterGrade ouside the class)
        System.out.println();
        System.out.println("Final Summary:");
        System.out.printf("%s - Average: %.2f (%s)%n",
                "Soni Dhenuva", emma.getAverage(), emma.getLetterGrade());
        System.out.printf("%s - Average: %.2f (%s)%n",
                "Nora Ahadian", james.getAverage(), james.getLetterGrade());
    }
}
```
```
=== Student Grade Tracker System ===

Creating student: Soni Dhenuva
Student created successfully!

--- Adding Grades for Soni ---
Adding grade: 95 points
Adding grade: 88 points
Adding grade: 92 points
Adding grade: 85 points

--- Soni Dhenuva's Grade Report ---
Student Name: Soni Rodriguez
Total Points: 360
Assignments Completed: 4
Current Average: 90.00
Letter Grade: A
Status: Excellent work!

========================================


Creating student: Nora Ahadian
Student created successfully!

--- Adding Grades for Nora ---
Adding grade: 78 points
Adding grade: 82 points
Adding grade: 75 points

--- Nora Ahadian's Grade Report ---
Student Name: Nora Ahadian
Total Points: 235
Assignments Completed: 3
Current Average: 78.33
Letter Grade: C
Status: Keep working hard!

========================================

Final Summary:
Soni Dhenuva - Average: 90.00 (A)
Nora Ahadian - Average: 78.33 (C)
```