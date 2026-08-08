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

Here is a slightly richer example that combines a loop with the modulo (`%`) and ternary (`? :`) operators — printing each number and labelling it as even or odd:

```java
for (int i = 1; i <= 10; i++) {
  String type = (i % 2 == 0) ? "even" : "odd";
  System.out.println(i + " is " + type);
}
```

### 👨‍💻 Activity — FizzBuzz
Print the numbers 1 to 20. For each number, print:
- `"FizzBuzz"` if it is divisible by both 3 and 5
- `"Fizz"` if it is divisible by 3
- `"Buzz"` if it is divisible by 5
- otherwise, just the number

*(Tip: check the "divisible by both" condition first — remember, in an `if-else if` ladder the first true condition wins.)*

---

### Jump Statements: `break` and `continue`

These statements change the normal flow inside a loop:
- **`break`** exits the loop immediately, skipping any remaining iterations.
- **`continue`** skips only the rest of the current iteration and moves on to the next one.

The example below processes a list of order amounts. It skips any invalid entries (zero or negative) with `continue`, and stops processing entirely once it hits an oversized order (over 1000) with `break`:

```java
int[] amounts = {50, 120, -5, 300, 2000, 80};

for (int amount : amounts) {
  if (amount <= 0) continue;   // skip invalid entries
  if (amount > 1000) break;    // stop at the first oversized order
  System.out.println("Processing: " + amount);
}
```

Here, `-5` is skipped by `continue`, and the loop stops completely when it reaches `2000` — so `80` is never processed, even though it comes after.


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
A switch can also be used as an **expression**, returning a value that you assign directly to a variable. The arrows (`->`) return each value, and when a case needs more than one line of logic before returning, you use the `yield` keyword inside a block:

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

Here, the simple cases return their value directly with `->`, while the `default` case uses a block with `yield` to build and return a custom message.

**Which data types can switch use?** `byte`, `short`, `char`, `int` (and their wrapper classes), `String`, and `enum` types. It does **not** work with `long`, `float`, `double`, or `boolean`. The return type of a switch *expression*, however, can be anything — `int`, `boolean`, a custom object, whatever the situation needs — the return type is completely independent of what you're switching on.


### 👨‍💻 Activity
Write a switch expression that takes a month name and returns its quarter (Q1–Q4).

---

## Pattern Matching in `switch` (Java 21)

Pattern matching lets a switch check the **type** of an object, not just a fixed value — something a plain switch cannot do (plain switch cannot take custom objects at all; pattern matching is what makes that possible).

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

Each `case` checks "is this object actually an `Integer`? A `String`?" — and if it matches, Java automatically gives you a properly-typed variable to use immediately, with no manual casting required. `case null ->` also lets you handle `null` explicitly as its own case.

**Important distinction:** the example above only checks **type** — it does not check any particular value within that type. To check both type *and* value together in the same case, add a `when` clause:

```java
static String describe(Object obj) {
  return switch (obj) {
    case Integer i when i < 0 -> "Negative integer: " + i;
    case Integer i when i == 0 -> "Zero";
    case Integer i -> "Positive integer: " + i;
    case String s when s.isEmpty() -> "Empty string";
    case String s -> "String: " + s.toUpperCase();
    case null -> "null";
    default -> "Unknown type";
  };
}
```

Here, `case Integer i when i < 0` checks both **type** (is it an `Integer`?) and **value** (is it negative?) before matching. Without a `when` clause, pattern matching only checks type.

A few things worth noting:
- This works the same whether it's inside a `static` method, an instance method, or directly inside `main` — there's no required structure; the examples above just use a separate reusable method as good practice.
- The return type can be anything, same as any switch expression — not limited to `String`.
- Case order matters, same as `if-else if` — Java checks top to bottom and stops at the first match, so put more specific types/conditions above more general ones.

---

## Part 2: Enums in Control Flow

An **enum** defines a fixed set of named constants — useful whenever a value should only ever be one of a known, limited set of options (days of the week, statuses, directions). Enums are more type-safe than using `String` or `int` for the same purpose, because the compiler won't let you assign anything outside the defined set.

An enum is a custom (user-defined) reference type — under the hood, it's actually a class the compiler generates for you. Each constant (`Direction.N`, `Direction.S`, etc.) is a real, singleton object, which is why enums are reference types, not primitives.

```java
enum Direction { N, S, E, W }

Direction dir = Direction.N;
System.out.println("Direction: " + dir);
```

Enum constants can also carry fixed values, using a field and constructor:

```java
enum StatusCode {
  OK(200), NOT_FOUND(404), SERVER_ERROR(500);

  private final int code;

  StatusCode(int code) {
    this.code = code;
  }

  public int getCode() {
    return code;
  }
}
```
`StatusCode.OK.getCode()` returns `200` — each constant carries its own fixed value, set once via the constructor.

**Comparing enums:** unlike Strings, `==` is safe and conventional for comparing enum values, since each constant is a single guaranteed instance.

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

**Important:** a static method can only be called directly (with no class-name prefix) from *within the same class*. When calling a static method from a **different** class, you must prefix it with the class name — e.g. `BonusCalculator.calcBonus(5000)`, not just `calcBonus(5000)`. Leaving out the class name is one of the most common early errors — it produces a "cannot find symbol" error because Java looks for the method inside the *calling* class instead.

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

**Setting this up in code:** define these overloaded `calcBonus` methods inside a class named `BonusCalculator` (not inside `MyApp`). Since they are `static` methods, calling them from `MyApp` (or any other class) requires the class name prefix:

```java
System.out.println("Employee bonus:" + BonusCalculator.calcBonus(5000));
System.out.println("Staff Bonus: " + BonusCalculator.calcBonus(5000, 0.2));
System.out.println("CEO Bonus: " + BonusCalculator.calcBonus(20000, 1.5));
```

You can format decimal output cleanly with `printf`:

```java
System.out.printf("Staff Bonus: $%.2f\n", BonusCalculator.calcBonus(5000, 0.2));
System.out.printf("CEO Bonus: $%.2f\n", BonusCalculator.calcBonus(20000, 1.5));
```

*Note: Java also supports `static import` (e.g. `import static BonusCalculator.calcBonus;`), which would let you call `calcBonus(5000)` with no class prefix at all. This works, but is generally discouraged for your own custom classes, since it hides which class a method actually comes from when someone else reads your code. Stick with the explicit `ClassName.method()` form shown above.*

### 👨‍💻 Activity — Calculate Bonus by Position
Create an overloaded `calcBonus` method in `BonusCalculator` that takes a salary and an `enum Position { STAFF, MANAGER, CEO }`:
- Staff: 10% of salary
- Manager: 20% of salary
- CEO: 300% of salary

---

## Practice Exercises

Work through these on your own to reinforce today's concepts:

1. Ask the user for their marks and print `"Excellent"` (marks > 85), `"Good"` (70–85), or `"Needs Improvement"` (otherwise).
2. Ask the user for their favorite fruit — print `"Healthy choice!"` if it's `"apple"`, otherwise print `"Nice fruit!"`.
3. Create an overloaded method that takes an array of salaries and calculates a bonus based on the average salary — only paying a bonus if the worker has at least 6 months of data.
4. *(Optional)* Write a program that uses pattern matching in `switch` (with a `when` clause) to check whether a number is positive, negative, or zero, and whether a string is empty or not.

### 👨‍💻 Activity — Vending Machine

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