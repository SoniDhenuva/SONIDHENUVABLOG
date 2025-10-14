---
title: 1.8 Documentation With Comments
layout: post
type: hacks
comments: true
courses: {csa: {week: 7}}
type: ccc
---

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
 * @param nums the array of integers to check
 * @return the sum of all positive even integers
 * 
 * Preconditions:
 * - nums must not be null
 * - nums can be empty (returns 0)
 * 
 * Postconditions:
 * - Return value >= 0
 * - Original array unchanged
 * 
 * Examples:
 * - doSomething([1, 2, 3, 4]) returns 6
 * - doSomething([-2, -4, 0]) returns 0
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

```java
/**
 * GradeBook - tracks grades and calculates weighted final grades.
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
     * @param category type of assignment
     * @param name assignment name
     * @param score grade received
     */
    public void addAssignment(String category, String name, double score) { }

    /**
     * Sets the weight for a category.
     * 
     * @param category category name
     * @param weight decimal 0.0-1.0 (ex: 0.40 = 40%)
     */
    public void setCategoryWeight(String category, double weight) { }

    /**
     * Calculates final grade using all assignments and weights.
     * 
     * @return final grade as percentage
     */
    public double calculateFinalGrade() { }

    /**
     * Generates grade report by category.
     * 
     * @return formatted grade breakdown
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
In team projects, other people need to understand and use your code without asking you a million questions. Good documentation means your teammates know what your methods do, what to pass in, and what to expect back. In solo projects, you might remember what you wrote, but even then, future you will thank past you for leaving good comments when you come back to the code months later.

<br>
<br>

**2. Give an example of when a method SHOULD be documented and when it SHOULD NOT.**

SHOULD document: A public method like calculateFinalGrade() that other classes use. People need to know what parameters to pass, what it returns, and any special conditions.
SHOULD NOT document: Super obvious private helper methods like private boolean isEven(int n) { return n % 2 == 0; }. The code is literally self-explanatory - documenting it is just extra clutter.