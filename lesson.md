# 3.2 Programming Fundamentals and Control Structures (Part 2)

## Lesson Overview

This lesson introduces students to Java's control flow mechanisms, demonstrating how programs make decisions and execute tasks repeatedly. Students will also learn how to organize code using packages and create reusable blocks of logic through methods. Together, these topics form the foundation for building structured and modular Java applications.

**Duration:** 3 hours  
**Module:** 3.2  
**Prerequisites:** Basic Java syntax, variables, and operators  

---

## Lesson Objectives

By the end of this lesson, learners will be able to:

1. **Implement control flow constructs** (if-else, loops, switch, Scanner) to create dynamic Java programs that make decisions and handle repetitive tasks based on conditions.

2. **Organize Java code using packages and methods** to build modular, maintainable applications following professional development practices.

3. **Apply method overloading and access modifiers** to create flexible, reusable code while properly encapsulating functionality within classes.

---

## Part 1: Control Flow Statements [70 minutes]

Control flow statements determine the order in which individual statements, instructions, or functions are executed in a program. Instead of executing code sequentially from top to bottom, Java allows you to make decisions, repeat actions, or skip sections based on conditions. This makes programs dynamic and responsive to input or logic.

Java's control flow can be divided into three main categories:

1. Decision Making Statements
   - if else
   - switch

2. Loop Statements
   - for
   - while / do while

3. Jump/Branching Statements
   - break
   - continue

### Creating the Class

Let's start by creating a class named `LearnControlFlow.java` where we'll experiment with different control flow constructs.

```java
public class LearnControlFlow {
  public static void main(String[] args) {
    int budget = 1000;
    int expense = 90;
  }
}
```

---

### Decision-Making Statements [25 minutes]

#### `if` and `if-else` Statements

Decision-making is a core concept in programming. The `if` statement allows a block of code to run only when a specific condition evaluates to `true`. The optional `else` block executes when the condition is `false`.

```java
if (budget > expense) {
  System.out.println("You are within budget");
} else {
  System.out.println("You are over budget");
}
```

**Explanation:**  
The expression inside parentheses `(budget > expense)` is evaluated first.  
- If `true`, the statement inside the `if` block executes.  
- If `false`, the statement inside the `else` block executes.  

### 👨‍💻 Activity **(10 minutes)**
Ask the user for their marks and print:  
- `"Excellent"` if marks > 85  
- `"Good"` if marks are between 70–85  
- `"Needs Improvement"` otherwise  

---

#### `if-else if` Ladder

When multiple conditions need to be checked, Java provides the `if-else if` ladder. It evaluates conditions sequentially from top to bottom and executes the block corresponding to the first `true` condition.

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

Each condition is mutually exclusive — once a match is found, subsequent checks are skipped.

---

#### Comparing Strings

In Java, strings are objects, not primitive data types.  
The `==` operator compares **object references** (memory locations), whereas `.equals()` compares **actual content**.

```java
String fruit1 = "apple";
String fruit2 = new String("apple");

System.out.println(fruit1 == fruit2);       // false
System.out.println(fruit1.equals(fruit2));  // true
```

**Key takeaway:** Always use `.equals()` to compare string values.

### 👨‍💻 Activity **(8 minutes)**
Ask the user for their favorite fruit.  
If it's `"apple"`, print `"Healthy choice!"`; otherwise print `"Nice fruit!"`.

---

### Looping Constructs **(~20 minutes)**

Loops allow repetitive execution of a block of code until a condition is met. They are useful for iterating over data, performing repeated calculations, or waiting for specific conditions.

#### `for` Loop

Use a `for` loop when the number of iterations is known.

```java
for (int i = 1; i <= 5; i++) {
  System.out.println("i = " + i);
}
```

**Explanation:**  
- `int i = 1` initializes the counter.  
- `i <= 5` is the condition checked before every iteration.  
- `i++` increments the counter after each loop.  

---

#### `while` Loop

Use a `while` loop when you do not know the exact number of iterations beforehand.

```java
int i = 1;
while (i <= 5) {
  System.out.println(i);
  i++;
}
```

The condition is evaluated before each iteration; if false initially, the loop may not execute at all.

---

### 👨‍💻 Activity **(12 minutes)**
Write a program to print numbers from 1 to 10 using both `for` and `while` loops.

---

### Jump Statements **(~15 minutes)**

#### `break` and `continue`

These statements alter the normal flow inside loops.

- **`break`** exits the loop immediately.  
- **`continue`** skips the remaining code in the loop for that iteration and proceeds to the next one.

```java
for (int i = 1; i <= 10; i++) {
  if (i == 5) break; // exit loop
  System.out.println(i);
}
```

```java
for (int i = 1; i <= 10; i++) {
  if (i == 3) continue; // skip 3
  System.out.println(i);
}
```

### 👨‍💻 Activity [8 minutes]
Print numbers from 1 to 10, skipping 3 and stopping completely at 8.

---

#### Reading User Input — `Scanner`

Reading input dynamically allows programs to interact with users.  
The `Scanner` class (from `java.util`) provides methods to read text, integers, and other types.

```java
import java.util.Scanner;

public class UserInputActivity {
  public static void main(String[] args) {
    Scanner sc = new Scanner(System.in);
    System.out.print("Enter your username: ");
    String userName = sc.nextLine();

    if (userName.equals("admin")) {
      System.out.println("Welcome Admin!");
    } else {
      System.out.println("Unauthorized user!");
    }
    sc.close();
  }
}
```

### 👨‍💻 Activity [10 minutes]
Ask for a password. Keep prompting until the user enters `"java123"`.

---

### Switch Statements [25 minutes]

When multiple conditions depend on the same variable, using multiple `if-else` statements becomes verbose.  
The `switch` statement provides a cleaner approach.

#### Traditional `switch`
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

---

#### Enhanced `switch` (Java 17+)

The enhanced switch introduced modern syntax and eliminated `break` statements. It can also return a value using `yield`.

```java
String direction = "E";

switch (direction) {
  case "N" -> System.out.println("North");
  case "E" -> System.out.println("East");
  case "S" -> System.out.println("South");
  default -> System.out.println("Invalid input");
}
```
As with the traditional switch statement, cases can be combined as well.

```java
switch (direction) {
  case "N", "E", "W", "S" -> System.out.println("You have chosen a valid direction");
  default -> System.out.println("Invalid input");
}
```

The `switch` expression can return the value directly as well. Using the month example:

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

### To customize our return value, we can use the `yield` keyword.
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

### 👨‍💻 Activity [10 minutes]
Write a switch expression that takes a month name and returns its quarter (Q1–Q4).

---

##  Pattern Matching in `switch` (Java 21) [OPTIONAL]

Pattern Matching in modern Java allows checking both **type** and **value** in one compact switch block.

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

### 👨‍💻 Activity
Write a program that checks whether an object is a number, a string, or null using pattern matching.

---

## Part 2: Enums in Control Flow [12 minutes]

Java provides a special data type called `enum` to support enumeration. It is used to define a collection of constants. Enums are useful to represent a fixed set of values, such as days of the week, months of the year, etc.
Enums represent a fixed set of named constants, it is more type safe than using `String` or `int` variables.

```java
enum Direction { N, S, E, W }

Direction dir = Direction.N;
System.out.println("Direction: " + dir);
```

### 👨‍💻 Activity [8 minutes]
Create an enum `TrafficLight` with constants `RED`, `YELLOW`, and `GREEN` and print corresponding actions.

---

#### Switch with Enums

Enums integrate seamlessly with switch expressions.

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

## Part 3: Packages [28 minutes]

### What is a Package?

A **package** is a collection of related classes and interfaces, similar to folders organizing files on your computer.  
They help group logically related code, avoid naming conflicts, and make large projects easier to manage.

### Why Use Packages?

Packages help us to organize our code. It also helps to prevent naming conflicts. For example, if we have two classes with the same name, we can place them in different packages to avoid naming conflicts.

There are two types of packages in Java: **built-in packages** and **user-defined packages**.

### Types of Packages

-  **Built-in packages** in Java such as `java.lang`, `java.util`, etc. For example, the `java.util` package contains the `Scanner` and `ArrayList` classes. 
The `java.lang` package is automatically imported into every Java program. As it contains the `String` class, this is why we can use the `String` class without importing it.

As you may have noticed, packages in the Java language begin with `java` or `javax`.
 
- **User-defined packages** created by developers.
We can also create our own packages to organize our code.

###  Package Naming Conventions [SELF-STUDY]

The package declaration should be the first line of code in a Java source file. It is declared using the `package` keyword followed by the package name.

It is common to use the reverse domain name of the organization to name the package. For example, if the organization's domain name is `companyname.com`, then the package name should be `com.companyname`. In this case, the folder structure should be `com/companyname`.

The naming convention for packages is to use all lowercase letters. If the package name contains multiple words, we can use underscores to separate the words. For example, `com.companyname.project_name` is a valid package name.

---

### Creating a Package

We can try creating a new folder called `mypackage` and adding a new file called `HelloWorld.java` with the following code:

```java
package mypackage;

public class HelloWorld {
  public static void main(String[] args) {
    System.out.println("Hello from mypackage!");
  }
}
```
To compile and run the code, we can use the "Run Java" button in VS Code.

Alternatively, we can compile and run it in the terminal:

```bash
javac HelloWorld.java
```

To run the file, we need to be in the parent directory of the package. In this case, we need to be in the parent directory of `mypackage` and we need to specify the fully qualified name of the class:

```bash
java mypackage.HelloWorld
```

Try removing the line `package mypackage;` and see what happens when you try to compile the code.

### Importing Packages

To use a class or interface from a package, we need to import the package. We can also import all the classes and interfaces in a package using the `*` wildcard. The syntax for importing a package is:

```java
import java.util.Scanner;
import java.util.*;
```

These allow you to use classes defined in other packages.

### 👨‍💻 Activity [10 minutes]
Create a `mypackage` folder, add `HelloWorld.java`, and run it in VS Code.  
Observe that removing the package line leads to compilation issues.

---

## Part 4: Methods [55 minutes]

### What Are Methods?

A method is a block of executable code which can be invoked. You can pass an optional set of arguments to the method. It may also optionally return data.

Methods promote modularity, reduce redundancy, and make code easier to maintain.

### Predefined vs User-defined Methods

- **Predefined methods:** Provided by Java (e.g., `System.out.println`, `Math.max`).  
- **User-defined methods:** Written by developers for specific needs.

Let's add a method `addNumbers` into our `MyApp.java` file. This should be within the class but outside the `main` method.

Example:
```java
public static void addNumbers(int a, int b) {
  System.out.println(a + b);
}
```
Inside the `main` method, we can call our method by using the method name and passing in the arguments.
Call it using:
```java
addNumbers(5, 10);
```

In Java, the terms **method** and **function** are sometimes used interchangeably but there are a few differences between the two.

- functions are static methods that belong to a class
- methods are usually non-static (instance) methods that belong to an object (instance of a class)

For example, `Arrays.toString()` can be considered a function because it is a static method that belongs to the Arrays class. On the other hand, `myString.toUpperCase()` is a method because it is a non-static method that belongs to the String class.

---

### Method Structure

```java
<access modifier> <return type> <method name>(<parameters>) {
  // method body
}
```

Example:
```java
public static int add(int a, int b) {
  return a + b;
}
```

- **Access Modifier:** Defines where the method is accessible (`public`, `private`, etc.)  
- **Return Type:** Data type of value returned (`void` means no return).  
- **Parameters:** Variables used to pass data into the method. If the method does not require any parameters, we can leave the parentheses empty.

We may sometimes use the terms **parameters** and **arguments** interchangeably but there is a difference between the two. **Parameters** are the variables that are declared in the method signature. **Arguments** are the actual values that are passed into the method.

---

### Static vs Instance Methods

- **Static methods** 
The `static` keyword is used to declare a static method. A static method belongs to the class and not to the object (instance of the class). This means that we can call a static method without creating an object of the class.

- **Instance methods** 
An instance method belongs to an object (instance of a class). This means that we need to create an object of the class before we can call an instance method.

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

We can call these methods in the `main` method of the `MyApp` class.

```java
public class MyApp {
  public static void main(String[] args) {
    Car.aboutCar();
    Car car = new Car();
    car.drive();
  }
}
```

Try to call the `drive()` method without creating an object of the `Car` class and see what happens.

```java
Car.drive();
```

Usage:
```java
Car.aboutCar(); // static
Car myCar = new Car();
myCar.drive();  // instance
```

---

### Access Modifiers

An **access modifier** is a keyword that determines the accessibility of a method. There are four access modifiers in Java: `public`, `private`, `protected`, and `default`.

| Modifier | Scope |
|-----------|--------|
| `public` | Accessible everywhere |
| `private` | Only within the same class |
| `protected` | Within same class + subclasses |
| (default) | Within same package |

We may not always want our methods to be public. For example, we may want to restrict access to certain methods to prevent other classes from modifying the data in our class. In this case, we can use the `private` access modifier.

In our `Car` example, we want to restrict some of these methods because they should not be controlled directly. Let's change these 3 methods to be `private`.

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
```

Now if you try to call these methods in the `main` method of another class, say `MyApp` class, you will get an error. This is correct, because we should not be able to call these methods directly but only from within the class.

In this case, we want `startEngine()` to be the only method that can be called directly, which will in turn call these `private` methods.

```java
public void startEngine() {
  System.out.println("🚗 Starting engine...");
  System.out.println("✅ Engine started!");
  startAircon();
  startRadio();
  checkSeatBelts();
}
```

Our public method `startEngine()` will now call these private methods. We have now hidden some methods from public access. This is a concept called **encapsulation**, which we will cover in more detail in the next lesson.

---

### Method Overloading

A class can have multiple methods with the same name but declared with different parameters. This is called **method overloading**, which means providing 2 or more separate methods in a class with the same name but different parameters. This allows us to have different implementations of the same method.

Java can resolve which method it needs to execute, based on the arguments being passed.

```java
public static double calcBonus(double salary) {
  return salary * 0.1;
}

public static double calcBonus(double salary, double rate) {
  return salary * rate;
}
```

**Rules for overloading:**
1. Method name must be identical.  
2. Parameter list must differ (in number or type).  

###  Valid vs Invalid Overloaded Method Signatures [SELF-STUDY]

The **method signature** consists of the method name and the parameter list. The return type is not part of the method signature.

```java
1 public static void myFn(int a)
2 public static void myFn(int b) // ❌ same parameter type as 1
3 public static void myFn(float a) // ✅
4 public static void myFn(double a) // ✅
5 public static void myFn(int a, int b) // ✅
6 public static void myFn(int b, int a) // ❌ same parameter types as 5
7 public static void myFn(int a, float b) // ✅
8 public static void myFn(int a, int b, int c) // ✅
9 public static int myFn(int a, int b, int c) // ❌ same parameter types as 8
```

**In class:** Show a quick example of valid vs invalid overloading (2-3 examples max).

---

### Method Overloading Example

Create a `LearnMethods.java` file and code along.

Let's create a method `calcBonus()` that calculates the bonus based on a salary.

```java
public static double calcBonus(double salary) {
  return salary * 0.1;
}
```

We can call this method in the `main` method.

```java
System.out.println("Employee bonus:" + calcBonus(5000));
```

Now let's create an overloaded method `calcBonus()` that calculates the bonus based on the salary and the bonus rate.

```java
public static double calcBonus(double salary, double bonusRate) {
  return salary * bonusRate;
}
```

We can call same method name with different parameters.

```java
System.out.println("Staff Bonus: " + calcBonus(5000, 0.2));
System.out.println("CEO Bonus: " + calcBonus(20000, 1.5));
```

Sidenote: we can use `printf` to format the decimal output.
https://www.theserverside.com/blog/Coffee-Talk-Java-News-Stories-and-Opinions/Format-double-Java-printf-example

```java
System.out.printf("Staff Bonus: $%.2f\n", calcBonus(5000, 0.2));
System.out.printf("CEO Bonus: $%.2f\n", calcBonus(20000, 1.5));
```

### 👨‍💻 Activity 1 - Calculate Bonus [12 minutes]

Create another overloaded method for `calcBonus` that takes in the salary as well as an `enum` `Position` with the following values: `STAFF`, `MANAGER`, `CEO`.

The bonuses should be calculated as follows:

- Staff: 10% of salary
- Manager: 20% of salary
- CEO: 300% of salary

### 👨‍💻 Activity 2 - Calculate Bonus for Variable Wage Worker [10 minutes]

Now we have a variable wage worker, and we store his salary in an array. We want to calculate his bonus based on his monthly average salary. The worker should only get a bonus if he has worked for at least 6 months.

Create an overloaded method that takes in an array of salaries and calculates the bonus based on the average salary.

###  👨‍💻 Activity 3 - Vending Machine [OPTIONAL]

Create a new class `VendingMachine`. You may do it in the same file or create a new file.

This vending machine will have a `makePayment` method that takes in a `double` amount and outputs to the console that the payment was accepted.

It should also have another overloaded method that takes in an `enum` `EPayment`.

```java
enum EPayment {
  PAYNOW, GRABPAY, FAVEPAY
}
```

This overloaded `makePayment` method will accept the enum and call the respective `private` method i.e. `connectPayNow()`, `connectGrabPay()`, `connectFavePay()`. You can just return `true` or `false` in these methods for simulating the payment status.

Test code:

```java
VendingMachine myVendingMachine = new VendingMachine();
myVendingMachine.makePayment(10.0); // cash
myVendingMachine.makePayment(EPayment.GRABPAY); // cashless, no amount needed
myVendingMachine.makePayment(EPayment.FAVEPAY);
myVendingMachine.makePayment(EPayment.PAYNOW);
```

---

## Lesson Summary [10 minutes]

**Key Takeaways:**
- Control flow statements (if-else, loops, switch) enable dynamic program execution
- Scanner class allows interactive user input
- Packages organize code and prevent naming conflicts
- Methods promote code reusability and modularity
- Method overloading provides flexibility with same method names
- Access modifiers control visibility and encapsulation

**Next Steps:**
- Complete the assignment
- Review self-study materials for deeper understanding
- Practice with additional exercises

---

END
