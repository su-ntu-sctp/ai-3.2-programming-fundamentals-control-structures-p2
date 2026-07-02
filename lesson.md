# 3.2 Programming Fundamentals and Control Structures (Part 2)

## Lesson Overview

This lesson introduces Java's control flow mechanisms — how programs make decisions and execute tasks repeatedly. You will also learn how to organize code using packages and create reusable blocks of logic through methods. Together, these topics form the foundation for building structured, modular Java applications.

**Duration:** 3 hours
**Module:** 3.2
**Prerequisites:** Basic Java syntax, variables, and operators

---

## Lesson Objectives

By the end of this lesson, you will be able to:

1. **Implement control flow constructs** (if-else, loops, switch, Scanner) to create dynamic Java programs that make decisions and handle repetitive tasks.
2. **Organize Java code using packages and methods** to build modular, maintainable applications.
3. **Apply method overloading and access modifiers** to create flexible, reusable, properly encapsulated code.

---

## Part 1: Control Flow Statements

Control flow statements determine the order in which statements execute. Instead of running top to bottom every time, Java lets you make decisions, repeat actions, or skip sections based on conditions — which is what makes a program dynamic rather than a fixed script.

Java's control flow falls into three categories:

1. **Decision Making** — `if-else`, `switch`
2. **Loops** — `for`, `while` / `do-while`
3. **Jump/Branching** — `break`, `continue`

### Creating the Class

```java
public class LearnControlFlow {
  public static void main(String[] args) {
    int budget = 1000;
    int expense = 90;
  }
}
```

---

### Decision-Making: `if`, `if-else`, and `if-else if`

The `if` statement runs a block of code only when a condition evaluates to `true`. An `else` block runs when it's `false`. When you have more than two possibilities, you chain conditions using `if-else if` — Java checks each condition top to bottom and runs the block for the **first** one that's `true`; once a match is found, the rest are skipped.

```java
int score = 75;

if (score > 90) {
  System.out.println("A");
} else if (score > 80) {
  System.out.println("B");
} else if (score > 70) {
  System.out.println("C");
} else {
  System.out.println("D or below");
}
```

---

### Comparing Strings

In Java, strings are objects, not primitive data types. This matters because the `==` operator compares **object references** (whether two variables point to the same memory location), while `.equals()` compares **actual content**.

```java
String fruit1 = "apple";
String fruit2 = new String("apple");

System.out.println(fruit1 == fruit2);       // false
System.out.println(fruit1.equals(fruit2));  // true
```

`fruit1` and `fruit2` hold the same text, but they are different objects in memory, so `==` returns `false`. **Always use `.equals()` when comparing string values** — this is a common bug source in real applications.

---

### Loops: `for` and `while`

Loops let you repeat a block of code without writing it out multiple times.

Use a **`for` loop** when you know the number of iterations in advance:

```java
for (int i = 1; i <= 5; i++) {
  System.out.println("i = " + i);
}
```
`int i = 1` initializes the counter, `i <= 5` is checked before every iteration, and `i++` increments the counter after each loop.

Use a **`while` loop** when the number of iterations depends on a condition that isn't known ahead of time:

```java
int i = 1;
while (i <= 5) {
  System.out.println(i);
  i++;
}
```
The condition is checked *before* each iteration — if it's `false` from the start, the loop body never runs.

### 👨‍💻 Activity
Write a program to print numbers from 1 to 10 using both a `for` loop and a `while` loop.

---

### Jump Statements: `break` and `continue`

These statements change the normal flow inside a loop:
- **`break`** exits the loop immediately, skipping any remaining iterations.
- **`continue`** skips only the rest of the current iteration and moves on to the next one.

```java
for (int i = 1; i <= 10; i++) {
  if (i == 3) continue; // skip printing 3, but keep looping
  if (i == 8) break;    // stop the loop entirely once i reaches 8
  System.out.println(i);
}
```

---

## Switch Statements

When multiple conditions all depend on the same variable, a chain of `if-else` statements gets verbose. The `switch` statement handles this more cleanly by matching a variable against a list of possible values.

### Traditional `switch`
```java
String direction = "N";

switch (direction) {
  case "N":
    System.out.println("North");
    break;
  case "E":
    System.out.println("East");
    break;
  default:
    System.out.println("Invalid input");
}
```
Each `case` needs a `break`, otherwise execution "falls through" into the next case — a classic source of bugs in older Java code.

### Enhanced `switch` (Java 17+)

The enhanced switch uses `->` instead of `case:`/`break`, removing the fall-through problem entirely. It can also return a value directly using `yield`.

```java
String direction = "E";

switch (direction) {
  case "N" -> System.out.println("North");
  case "E" -> System.out.println("East");
  case "S" -> System.out.println("South");
  default -> System.out.println("Invalid input");
}
```

Cases can be combined with a comma:

```java
switch (direction) {
  case "N", "E", "W", "S" -> System.out.println("You have chosen a valid direction");
  default -> System.out.println("Invalid input");
}
```

A switch can also be used as an **expression**, returning a value that you assign directly to a variable:

```java
String quarter = switch (month) {
  case "January", "February", "March" -> "Q1";
  case "April", "May", "June" -> "Q2";
  case "July", "August", "September" -> "Q3";
  case "October", "November", "December" -> "Q4";
  default -> "Unknown";
};

System.out.println("quarter: " + quarter);
```

When a case needs more than one line of logic before returning a value, use `yield` inside a block:

```java
int rating = 5;

String feedback = switch (rating) {
  case 1, 2, 3 -> "Poor";
  case 4 -> "Good";
  case 5 -> "Excellent";
  default -> {
    yield "Invalid rating: " + rating;
  }
};

System.out.println(feedback);
```

### 👨‍💻 Activity
Write a switch expression that takes a month name and returns its quarter (Q1–Q4).

---

## Pattern Matching in `switch` (Java 21) — *optional, time permitting*

Pattern matching lets a switch check both the **type** and the **value** of an object in one compact block, instead of writing separate `instanceof` checks.

```java
static String format(Object obj) {
  return switch (obj) {
    case Integer i -> "Integer: " + i;
    case String s -> "String: " + s.toUpperCase();
    case null -> "null";
    default -> "Unknown type";
  };
}
```

---

## Part 2: Enums in Control Flow

An **enum** defines a fixed set of named constants — useful whenever a value should only ever be one of a known, limited set of options (days of the week, statuses, directions). Enums are more type-safe than using `String` or `int` for the same purpose, because the compiler won't let you assign anything outside the defined set.

```java
enum Direction { N, S, E, W }

Direction dir = Direction.N;
System.out.println("Direction: " + dir);
```

### 👨‍💻 Activity
Create an enum `TrafficLight` with constants `RED`, `YELLOW`, and `GREEN`, and print the corresponding action for each (e.g. `RED` → "Stop").

### Switch with Enums

Enums work naturally with switch expressions — no quotes needed, and the compiler can warn you if you miss a case:

```java
Direction d = Direction.W;

switch (d) {
  case N -> System.out.println("North");
  case E -> System.out.println("East");
  case W -> System.out.println("West");
  case S -> System.out.println("South");
}
```

---

## Part 3: Packages

A **package** is a collection of related classes and interfaces — similar to a folder that groups related files. Packages help organize large codebases and, importantly, prevent naming conflicts: two classes with the same name can coexist as long as they live in different packages.

There are two types:
- **Built-in packages**, such as `java.util` (contains `Scanner`, `ArrayList`) and `java.lang` (contains `String`, and is automatically imported into every Java program — that's why you can use `String` without an import statement). Java's own packages begin with `java` or `javax`.
- **User-defined packages**, which you create yourself to organize your own code.

### Creating a Package

The `package` declaration must be the first line in the file:

```java
package mypackage;

public class HelloWorld {
  public static void main(String[] args) {
    System.out.println("Hello from mypackage!");
  }
}
```

To compile and run from the terminal, you need to be in the parent directory of `mypackage` and reference the fully qualified class name:

```bash
javac HelloWorld.java
java mypackage.HelloWorld
```

If you remove the `package mypackage;` line, the class no longer belongs to that package and running it with the qualified name will fail — a good way to see why the declaration matters.

### Importing Packages

To use a class from another package, import it — either the specific class, or every class in the package using `*`:

```java
import java.util.Scanner;
import java.util.*;
```

**Package naming convention (self-study):** it's common to use your organization's reverse domain name — e.g. `companyname.com` becomes package `com.companyname`, matching folder structure `com/companyname`. Package names are all lowercase; use underscores to separate words if needed (`com.companyname.project_name`).

### 👨‍💻 Activity
Create a `mypackage` folder, add `HelloWorld.java` inside it, and run it. Then remove the `package` line and observe what happens.

---

## Part 4: Methods

A **method** is a named, reusable block of code that can be invoked, optionally accepting input (parameters) and optionally returning a value. Methods reduce repetition and make code easier to maintain and test.

Java also provides many **predefined methods** (`System.out.println`, `Math.max`) alongside the **user-defined methods** you write yourself.

> Note: "method" and "function" are often used interchangeably, but strictly speaking, a **function** is a static method that belongs to the class itself, while a **method** is a non-static (instance) method that belongs to an object. `Arrays.toString()` is technically a function; `myString.toUpperCase()` is technically a method.

```java
public static void addNumbers(int a, int b) {
  System.out.println(a + b);
}
```
Called from `main` as:
```java
addNumbers(5, 10);
```

### Method Structure

```java
<access modifier> <return type> <method name>(<parameters>) {
  // method body
}
```
```java
public static int add(int a, int b) {
  return a + b;
}
```
- **Access modifier** — controls where the method can be called from.
- **Return type** — the data type of the value the method sends back (`void` means it returns nothing).
- **Parameters** — variables declared in the method signature that receive input. If a method needs no input, the parentheses stay empty.

Note the distinction: **parameters** are the variables declared in the method definition; **arguments** are the actual values you pass in when calling it.

---

### Static vs Instance Methods

A **static** method belongs to the class itself, not to any particular object — you can call it directly on the class, without creating an instance. An **instance** method belongs to an object, so you must create an instance of the class first before calling it.

```java
public class Car {
  public static void aboutCar() {
    System.out.println("Cars have 4 wheels.");
  }

  public void drive() {
    System.out.println("Car is moving.");
  }
}
```

```java
public class MyApp {
  public static void main(String[] args) {
    Car.aboutCar();          // static — called on the class
    Car car = new Car();
    car.drive();             // instance — called on an object
  }
}
```

Calling `Car.drive()` directly (without creating an instance) will not compile — `drive()` needs an object to act on, since instance methods typically work with instance-specific data.

### 👨‍💻 Activity
Extend the `Car` class with one more static method and one more instance method of your choice, and call both correctly from `MyApp`.

---

### Access Modifiers

An **access modifier** controls where a method (or field) can be accessed from. Java has four:

| Modifier | Scope |
|-----------|--------|
| `public` | Accessible everywhere |
| `private` | Only within the same class |
| `protected` | Within the same class and its subclasses |
| (default, no keyword) | Within the same package |

Restricting access matters when you don't want other classes reaching in and modifying internal data or calling internal steps directly. For example, in a `Car` class, some setup steps shouldn't be triggered independently — only as part of starting the engine:

```java
private void startAircon() {
  System.out.println("💨 Aircon started!");
}

private void startRadio() {
  System.out.println("📻 Radio started!");
}

private void checkSeatBelts() {
  System.out.println("🪑 Seat belts checked!");
}

public void startEngine() {
  System.out.println("🚗 Starting engine...");
  System.out.println("✅ Engine started!");
  startAircon();
  startRadio();
  checkSeatBelts();
}
```

Here, `startEngine()` is the only public entry point; the three private methods can only be called from within the class. This is a first look at **encapsulation** — hiding internal details and exposing only what's necessary — which is covered in more depth in the next lesson.

---

### Method Overloading

**Method overloading** means defining two or more methods in the same class with the same name but different parameter lists, so each version handles a different set of inputs. Java decides which version to run based on the arguments passed at the call site.

```java
public static double calcBonus(double salary) {
  return salary * 0.1;
}

public static double calcBonus(double salary, double rate) {
  return salary * rate;
}
```

**Rules for overloading:**
1. The method name must be identical.
2. The parameter list must differ — in number of parameters, or in type.

The **method signature** is the method name plus its parameter list; the return type is *not* part of the signature, so you can't overload two methods that differ only in return type.

```java
public static void myFn(int a)
public static void myFn(int a, float b)   // ✅ different parameter list
public static void myFn(float a)          // ✅ different parameter type
public static void myFn(int b)            // ❌ same signature as the first — won't compile
```

```java
System.out.println("Employee bonus:" + calcBonus(5000));
System.out.println("Staff Bonus: " + calcBonus(5000, 0.2));
System.out.println("CEO Bonus: " + calcBonus(20000, 1.5));
```

You can format decimal output cleanly with `printf`:

```java
System.out.printf("Staff Bonus: $%.2f\n", calcBonus(5000, 0.2));
System.out.printf("CEO Bonus: $%.2f\n", calcBonus(20000, 1.5));
```

### 👨‍💻 Activity — Calculate Bonus by Position
Create an overloaded `calcBonus` method that takes a salary and an `enum Position { STAFF, MANAGER, CEO }`:
- Staff: 10% of salary
- Manager: 20% of salary
- CEO: 300% of salary

---

## Practice Exercises

Work through these on your own to reinforce today's concepts:

1. Ask the user for their marks and print `"Excellent"` (marks > 85), `"Good"` (70–85), or `"Needs Improvement"` (otherwise).
2. Ask the user for their favorite fruit — print `"Healthy choice!"` if it's `"apple"`, otherwise print `"Nice fruit!"`.
3. Create a `mypackage` folder with `HelloWorld.java`, run it in VS Code, then remove the `package` line and observe the compilation error.
4. Create an overloaded method that takes an array of salaries and calculates a bonus based on the average salary — only paying a bonus if the worker has at least 6 months of data.
5. *(Optional)* Write a program that uses pattern matching in `switch` to check whether an object is a number, a string, or null.

### 👨‍💻 Optional / Bonus — Vending Machine

```java
enum EPayment {
  PAYNOW, GRABPAY, FAVEPAY
}
```

Create a `VendingMachine` class with an overloaded `makePayment` method:
- One version takes a `double` amount (cash) and prints that payment was accepted.
- One version takes an `EPayment` enum and calls a corresponding private method (`connectPayNow()`, `connectGrabPay()`, `connectFavePay()`), each returning `true`/`false` to simulate payment status.

```java
VendingMachine myVendingMachine = new VendingMachine();
myVendingMachine.makePayment(10.0);
myVendingMachine.makePayment(EPayment.GRABPAY);
myVendingMachine.makePayment(EPayment.FAVEPAY);
myVendingMachine.makePayment(EPayment.PAYNOW);
```

---

## Lesson Summary

**Key Takeaways:**
- Control flow statements (if-else, loops, switch) enable dynamic program execution
- Scanner allows interactive user input
- Packages organize code and prevent naming conflicts
- Methods promote code reusability and modularity
- Method overloading provides flexibility with the same method name
- Access modifiers control visibility and encapsulation

**Next Steps:**
- Complete the practice exercises above
- Review the self-study notes (package naming conventions)
- Practice with additional exercises as needed

---

END