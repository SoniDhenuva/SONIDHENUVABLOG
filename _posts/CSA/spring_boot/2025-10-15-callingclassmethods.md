---
title: 1.10 Calling Class Methods
layout: post
type: hacks
comments: true
courses: {csa: {week: 7}}
type: ccc
---

## Popcorn hacks
<br>
- Fix the below code

You’ve learned that static methods belong to the class and instance methods belong to the object.

Look at the code below and decide which lines will work — and which will cause an error.
Then fix the wrong ones.
<br>

```java
class Bro {
    String name;
    static String catchphrase = "Sup bro?";

    public Bro(String name) {
        this.name = name;
    }

    public void sayHi() {
        System.out.println("Hey, I'm " + name);
    }

    public static void sayCatchphrase() {
        System.out.println(catchphrase);
    }

    public static void main(String[] args) {
        // Will this work?
        sayCatchphrase();

        // What about this one?
        sayHi();

        Bro alex = new Bro("Alex");
        alex.sayHi();
        alex.sayCatchphrase();
    }
}
```
## Fixed Code Below

```java
class Bro {
    String name;
    static String catchphrase = "Sup bro?";

    public Bro(String name) {
        this.name = name;
    }

    public void sayHi() {
        System.out.println("Hey, I'm " + name);
    }

    public static void sayCatchphrase() {
        System.out.println(catchphrase);
    }

    public static void main(String[] args) {
        // Static method - OK
        sayCatchphrase();

        // Instance method - needs an object
        Bro alex = new Bro("Alex");

        // Works correctly
        alex.sayHi();

        // works (but better to write Bro.sayCatchphrase())
        Bro.sayCatchphrase();
    }
}

```

```
Sup bro?
Hey, I'm Alex
Sup bro?
```
<br>

## Homeowrk
<br>
-You are programming a game where 2 objects of your choosing (e.g., Robots, Dinosaurs, People) battle. Each object has health and power.
<br>

```java
class Robot {
    String name;
    int power;
    int health;
    static double fightDuration = 3.5; // in minutes

    // Constructor
    public Robot(String name, int power, int health) {
        this.name = name;
        this.power = power;
        this.health = health;
    }

    // Instance method: attack another robot
    public void attack(Robot enemy) {
        System.out.println(name + " attacks " + enemy.name + " for " + power + " damage!");
        enemy.health -= power;
        if (enemy.health < 0) {
            enemy.health = 0;
        }
    }

    // Instance method: print current status
    public void printStatus() {
        System.out.println(name + " → Power: " + power + ", Health: " + health);
    }

    // Static method: find the stronger fighter
    public static Robot strongerFighter(Robot r1, Robot r2) {
        if (r1.power > r2.power) {
            return r1;
        } else if (r2.power > r1.power) {
            return r2;
        } else {
            return null; // same strength
        }
    }

    // Static method: begin battle
    public static void beginBattle() {
        System.out.println("The ultimate robot battle begins!");
        System.out.println("This fight will last about " + fightDuration + " minutes!");
    }

    // Main method
    public static void main(String[] args) {
        Robot soni = new Robot("Soni", 30, 100);
        Robot nora = new Robot("Nora", 25, 100);

        beginBattle();

        soni.printStatus();
        nora.printStatus();

        soni.attack(nora);
        nora.attack(soni);

        soni.printStatus();
        nora.printStatus();

        Robot stronger = strongerFighter(soni, nora);
        if (stronger != null) {
            System.out.println("Stronger fighter: " + stronger.name);
        } else {
            System.out.println("It's a tie!");
        }

        System.out.println("Battle Over!");
    }
}
```

```
The ultimate robot battle begins!
This fight will last about 3.5 minutes!
soni → Power: 30, Health: 100
nora → Power: 25, Health: 100
soni attacks Beta for 30 damage!
nora attacks Alpha for 25 damage!
soni → Power: 30, Health: 75
nora → Power: 25, Health: 70
Stronger fighter: soni
Battle Over!
```



