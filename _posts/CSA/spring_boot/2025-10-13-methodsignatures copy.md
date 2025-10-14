---
title: 1.8 Documentation With Comments
layout: post
type: hacks
comments: true
courses: {csa: {week: 7}}
type: ccc
---

## Lesson Hack 1 - Fix the Documentation
<br>
Task: The following code has poor documentation. Rewrite it with proper Javadoc comments including preconditions and postconditions.

```java
/**
 * Calculates the sum of all positive even numbers in an array.
 * 
 * This method goes through each number in the array and adds it to the total
 * if it's both positive AND even. Pretty straightforward once you break it down!
 * 
 * @param nums the array of integers to check (can include negative, positive, odd, or even numbers)
 * @return the sum of all positive even integers found in the array
 * 
 * Preconditions:
 * - nums must not be null (otherwise you'll get a NullPointerException - not fun)
 * - nums can be empty (that's totally fine, you'll just get 0 back)
 * 
 * Postconditions:
 * - The return value will be >= 0 (since we're only adding positive numbers)
 * - The original array is NOT modified (we're just reading, not changing anything)
 * - If there are no positive even numbers, returns 0
 * 
 * Examples:
 * - doSomething([1, 2, 3, 4]) returns 6 (because 2 + 4 = 6)
 * - doSomething([-2, -4, 0]) returns 0 (negatives don't count, and 0 isn't positive)
 * - doSomething([1, 3, 5]) returns 0 (all odd numbers)
 * - doSomething([]) returns 0 (empty array, nothing to add)
 */
public int doSomething(int[] nums) {
    int result = 0;
    for (int i = 0; i < nums.length; i++) {
        if (nums[i] > 0 && nums[i] % 2 == 0) {
            result += nums[i];
        }
    }
    return result;
}
```

## Popcorn Hack 2: Write Class Documentation
<br>
Your Mission: Add Javadoc comments to document this GradeBook class!

What to include:

What does this class do? (purpose)
What are the main features? (key methods)
How would someone use it? (example)
Tags: @author, @version, @since ```java // TODO: Add your class-level Javadoc here! // Hint: Start with /** and end with */
public class GradeBook { private HashMap<String, Double> assignments; private HashMap<String, Double> categoryWeights; private double extraCredit;

```java
/**
 * GradeBook - tracks your grades and does the math so you don't have to.
 * 
 * Keeps all your assignments, weights categories (tests, homework, etc.),
 * and calculates your final grade. Super useful for "what do I need on the final?" moments.
 * 
 * Example:
 * <pre>
 * GradeBook myGrades = new GradeBook();
 * myGrades.setCategoryWeight("Tests", 0.50);
 * myGrades.addAssignment("Tests", "Midterm", 88.5);
 * double grade = myGrades.calculateFinalGrade();
 * </pre>
 * 
 * @author Sonika Dhenuva Konda
 * @version 1.0
 * @since 2025-10-14
 */
public class GradeBook {
    private HashMap<String, Double> assignments;
    private HashMap<String, Double> categoryWeights;
    private double extraCredit;

    /**
     * Adds an assignment to the gradebook.
     * 
     * @param category type of assignment ("Tests", "Homework", etc.)
     * @param name assignment name
     * @param score the grade you got
     * 
     * Preconditions: category and name can't be null, score should be valid
     * Postconditions: assignment is saved in the gradebook
     */
    public void addAssignment(String category, String name, double score) { }

    /**
     * Sets the weight for a category (how much it counts toward final grade).
     * 
     * @param category which category
     * @param weight decimal between 0.0 and 1.0 (ex: 0.40 = 40%)
     * 
     * Preconditions: category not null, weight between 0 and 1
     * Postconditions: category weight is set/updated
     */
    public void setCategoryWeight(String category, double weight) { }

    /**
     * Calculates your final grade using all assignments and weights.
     * 
     * @return final grade as a percentage
     * 
     * Preconditions: should have assignments and weights set
     * Postconditions: returns calculated grade, nothing gets changed
     */
    public double calculateFinalGrade() { }

    /**
     * Makes a report showing all your grades by category.
     * 
     * @return formatted string with grade breakdown
     * 
     * Preconditions: none
     * Postconditions: returns report string, gradebook unchanged
     */
    public String generateReport() { }
}
```

## Homework
<br>

### Part 1
```java
/**
 * Calculator class that adds two numbers together.
 * 
 * @author [Your Name]
 * @version 1.0
 */
public class Calculator {
    
    /**
     * Main method that demonstrates addition.
     * 
     * @param args command line arguments (not used)
     */
    public static void main(String args[]) {
        int x = 5;
        int y = 10;
        int z = add(x, y);
        System.out.println("Answer is " + z);
    }
    
    /**
     * Adds two integers together.
     * 
     * @param a first number
     * @param b second number
     * @return sum of a and b
     * 
     * Preconditions: none
     * Postconditions: returns a + b, inputs unchanged
     */
    static int add(int a, int b) {
        return a + b;
    }
}

```

### Part 2
<br>

```java
/**
 * Enrolls a student in a course if they meet all requirements.
 * 
 * Checks if the student exists, course exists, course isn't full,
 * no schedule conflicts, has prerequisites, and won't exceed 18 credit hours.
 * If everything passes, adds the student to the course.
 * 
 * @param studentId the ID of the student trying to enroll
 * @param courseCode the code of the course (like "CS101")
 * @param semester which semester to enroll for
 * @return true if enrollment succeeded, false if it failed any check
 * 
 * Preconditions:
 * - studentId should be valid
 * - courseCode should be valid
 * - semester should be a valid semester number
 * 
 * Postconditions:
 * - If returns true: student is enrolled, course roster updated, transaction recorded
 * - If returns false: nothing changes, enrollment failed
 * - Student can't exceed 18 credit hours total
 */
public boolean enrollStudent(String studentId, String courseCode, int semester) {
    Student student = findStudentById(studentId);
    if (student == null) return false;
    
    Course course = findCourseByCode(courseCode);
    if (course == null) return false;
    
    if (course.isFull()) return false;
    if (student.hasScheduleConflict(course)) return false;
    if (!student.hasPrerequisites(course)) return false;
    if (student.getCreditHours() + course.getCreditHours() > 18) return false;
    
    student.addCourse(course);
    course.addStudent(student);
    recordEnrollmentTransaction(studentId, courseCode, semester);
    return true;
}

```
### Part 3

**1. Why is documentation more important in team projects than solo projects?**
- In team projects, other people need to understand and use your code without asking you a million questions. Good documentation means your teammates know what your methods do, what to pass in, and what to expect back. In solo projects, you might remember what you wrote, but even then, future you will thank past you for leaving good comments when you come back to the code months later.

<br>
<br>

**2. Give an example of when a method SHOULD be documented and when it SHOULD NOT.**

SHOULD document: A public method like calculateFinalGrade() that other classes use. People need to know what parameters to pass, what it returns, and any special conditions.
SHOULD NOT document: Super obvious private helper methods like private boolean isEven(int n) { return n % 2 == 0; }. The code is literally self-explanatory - documenting it is just extra clutter.