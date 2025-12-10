# **Self-Study Preparation Guide**

**⏳ Estimated Prep Time:** 60–80 minutes

Welcome to our flipped-classroom session, where you'll review foundational concepts beforehand to maximize our time for hands-on coding and debugging. This pre-study focuses on the essential building blocks of Java programming: **Control Flow Statements**, **Packages**, and **Methods**. 

By mastering these concepts now, you will be better equipped to write dynamic programs that make decisions, repeat tasks efficiently, and organize code in a modular and maintainable way during our live session.

---

## ⚡ Your Self-Study Tasks

Please complete the following activities before our session.

### 📝 Task 1: Control Flow Fundamentals (25 Minutes)

**Activity:** 

Watch the video titled [**"Java Control Flow - If Statements, Switch & Loops"**](https://youtu.be/eIrMbAQSU34?t=5923).

[![video](https://img.youtube.com/vi/eIrMbAQSU34/default.jpg)](https://youtu.be/eIrMbAQSU34?t=5923)

Review the following concepts from the [`lesson.md`](./lesson.md) file:
- **Decision-Making Statements** (`if`, `if-else`, `if-else if` ladder)
- **Looping Constructs** (`for` loop, `while` loop)
- **Jump Statements** (`break`, `continue`)
- **String Comparison** (`.equals()` vs `==`)

Pay close attention to the syntax and how conditions control program execution.

**Guiding Questions:**
* **If Statements:** What happens if you forget the `else` block in an `if-else` statement? Will your code still compile?
* **String Comparison:** Why does Java require `.equals()` for comparing string content instead of `==`? What does `==` actually compare?
* **Loops:** How would you decide between using a `for` loop versus a `while` loop for a given task?
* **Break vs Continue:** In a loop printing numbers 1-10, what's the difference between using `break` at 5 versus `continue` at 5?

---

### 📝 Task 2: Enhanced Switch and User Input (20 Minutes)

**Activity:** 

Watch the video titled [**"Java Switch Statements"**](https://youtu.be/ldYLYRNaucM).

[![video](https://img.youtube.com/vi/ldYLYRNaucM/default.jpg)](https://youtu.be/ldYLYRNaucM)

Review the following sections from the [`lesson.md`](./lesson.md) file:
- **Traditional Switch Statements**
- **Enhanced Switch (Java 17+)** with arrow syntax and `yield`
- **Pattern Matching in Switch (Java 21)**
- **Scanner Class** for reading user input

Examine the differences between traditional switch (with `break`) and enhanced switch (with `->` arrow syntax).

**Guiding Questions:**
* **Switch Evolution:** What advantages does the enhanced switch (`->` syntax) provide over the traditional switch with `break` statements?
* **Switch Expressions:** How does returning a value from a switch expression (using `yield`) differ from a traditional switch statement?
* **Pattern Matching:** Why is pattern matching in switch statements (Java 21) considered a powerful feature? How does it improve type checking?
* **Scanner Input:** What's the difference between `nextLine()`, `nextInt()`, and `next()` methods in the Scanner class? When would you use each?

---

### 📝 Task 3: Code Organization - Packages and Methods (25 Minutes)

**Activity:** 

Watch the video titled [**"Java Methods Tutorial"**](https://youtu.be/cCgOESMQe44).

[![video](https://img.youtube.com/vi/cCgOESMQe44/default.jpg)](https://youtu.be/cCgOESMQe44)

Review the following sections from the [`lesson.md`](./lesson.md) file:
- **Packages** (built-in vs user-defined, package naming conventions)
- **Methods** (structure, parameters, return types)
- **Static vs Instance Methods**
- **Access Modifiers** (`public`, `private`, `protected`, default)
- **Method Overloading**

Pay attention to how packages organize code and how methods promote code reusability.

**Guiding Questions:**
* **Packages:** Why do Java packages use reverse domain naming conventions (e.g., `com.companyname.projectname`)? How does this prevent naming conflicts?
* **Static Methods:** Why can you call `Car.aboutCar()` without creating a `Car` object, but you need to create an object to call `myCar.drive()`?
* **Access Modifiers:** In the `Car` example with private methods like `startAircon()`, why would we want to hide certain methods from public access? What principle does this demonstrate?
* **Method Overloading:** How does Java determine which overloaded method to call when multiple methods have the same name? What aspects of the method signature must differ?

---

## 🙌🏻 Active Engagement Strategies

To deepen your retention, try one of the following while you review:

* **"Code Tracing":** Pick a code example with nested if-else or loops and trace the execution flow line by line. Predict the output before running the code mentally.
* **"Syntax Comparison":** Create a side-by-side comparison of traditional switch vs enhanced switch syntax. List the pros and cons of each approach.
* **"Real-World Application":** Think of a real-world scenario where you would need to use loops (e.g., processing a list of student grades, validating user login attempts). How would control flow statements help solve this problem?
* **"Method Design":** Before looking at the method overloading examples, try to design your own overloaded methods. What parameters would differ? How would you name them clearly?

---

## 📖 Additional Reading Material

**Java Control Flow:**
- [Oracle Java Tutorial - Control Flow Statements](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/flow.html)
- [W3Schools - Java If...Else](https://www.w3schools.com/java/java_conditions.asp)
- [W3Schools - Java Switch](https://www.w3schools.com/java/java_switch.asp)

**Java Methods and Packages:**
- [Oracle Java Tutorial - Methods](https://docs.oracle.com/javase/tutorial/java/javaOO/methods.html)
- [Oracle Java Tutorial - Packages](https://docs.oracle.com/javase/tutorial/java/package/packages.html)
- [GeeksforGeeks - Method Overloading in Java](https://www.geeksforgeeks.org/method-overloading-in-java/)

**Modern Java Features:**
- [Java 17 Enhanced Switch](https://openjdk.org/jeps/406)
- [Java 21 Pattern Matching for Switch](https://openjdk.org/jeps/441)

---

### 🙋🏻‍♂️ See you in the session!
