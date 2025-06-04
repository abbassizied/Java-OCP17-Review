# Java Core 

---

## 🌱 **Phase 1: Building Blocks of Java**

### 🔹 Topics Covered:

1. What is Java? (JVM, JRE, JDK)
2. Java Program Structure (classes, `main()` method)
3. Data Types and Variables
4. Naming Conventions and Syntax Rules
5. Type Conversion and Casting
6. `var` keyword (Java 10+)

### ✅ Goal:

* Understand how a Java program is structured.
* Know the difference between primitive and reference types.
* Be confident with type conversions and assignments.

---

## 🔧 **Phase 2: Operators and Expressions**

### 🔹 Topics Covered:

1. Arithmetic Operators
2. Relational and Logical Operators
3. Assignment Operators
4. Unary and Ternary Operators
5. Operator Precedence and Associativity
6. Short-circuit Evaluation

### ✅ Goal:

* Master combining expressions.
* Evaluate and predict results of complex statements.

---

## 🔀 **Phase 3: Making Decisions (Control Flow)**

### 🔹 Topics Covered:

1. `if`, `else if`, `else`
2. `switch` (traditional and enhanced, Java 12+)
3. `while`, `do-while`, and `for` loops
4. `break`, `continue`, and labels
5. Loop nesting and common patterns (e.g., factorial, prime check)

### ✅ Goal:

* Write efficient decision-making code.
* Choose the right loop for the task.

---

## 🧰 **Phase 4: Methods**

### 🔹 Topics Covered:

1. Declaring and Calling Methods
2. Parameters and Return Types
3. Method Overloading
4. Pass-by-value (especially for objects)
5. Varargs
6. Recursion (basic and tail-recursive forms)

### ✅ Goal:

* Understand the call stack.
* Write reusable, modular code with proper method structure.

---

## 🏗️ **Phase 5: Class Design**

### 🔹 Topics Covered:

1. Defining Classes and Objects
2. `this` keyword
3. Constructors (default, parameterized, chaining)
4. Encapsulation (private fields + getters/setters)
5. Static Variables and Methods
6. Access Modifiers (`public`, `private`, `protected`, default)
7. `final`, `static`, and initialization blocks

### ✅ Goal:

* Design classes with clean encapsulation.
* Understand the object lifecycle and memory model.

---

## 🔍 **Phase 6: Beyond Classes (Advanced OOP and Design)**

### 🔹 Topics Covered:

1. Inheritance and Composition
2. Overriding vs Overloading
3. `super` keyword
4. `Object` class and its methods (`equals`, `hashCode`, `toString`)
5. `abstract` classes and `interfaces`
6. Polymorphism and Dynamic Dispatch
7. Sealed Classes (Java 15+)
8. Records (Java 14+)
9. Nested Classes: Static, Non-static, Local, Anonymous

### ✅ Goal:

* Apply principles like SOLID, DRY, and Liskov Substitution.
* Use abstraction effectively in real-world designs.

---

### 🎯 Teaching Format:

For each phase, I’ll provide:

* 📖 **Concept Explanation**
* 🧠 **Memory Tricks & Analogies**
* ✍️ **Practice Exercises**
* ✅ **Quizzes**
* 💡 **Common Interview Questions**

---

# 🌱 Phase 1: Building Blocks of Java

---

## 🔹 1. What is Java?

### Java is:

* **High-level**: Easier to read/write than machine-level code.
* **Object-Oriented**: Based on classes and objects.
* **Platform-independent**: *“Write once, run anywhere”* — thanks to the JVM.

### Java Runtime Architecture:

| Term                               | Meaning                                                                       |
| ---------------------------------- | ----------------------------------------------------------------------------- |
| **JDK** (Java Development Kit)     | Full toolkit including compiler (`javac`) and libraries to develop Java apps. |
| **JRE** (Java Runtime Environment) | Tools to run Java programs (includes JVM + libraries).                        |
| **JVM** (Java Virtual Machine)     | Runs `.class` files. Converts bytecode to machine code.                       |

---

## 🔹 2. Java Program Structure

Here’s the most basic Java program:

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, Java!");
    }
}
```

### Breakdown:

* `public class HelloWorld`: Every Java app must have at least one class.
* `main(String[] args)`: Entry point of any Java application.
* `System.out.println(...)`: Prints text to the console.

🧠 **Memory Hook**: Think of the `main()` method as the *front door* where the JVM knocks and says, “Let’s run this!”

---

## 🔹 3. Data Types and Variables

### 🔸 Primitive Types:

| Type      | Size   | Example              |
| --------- | ------ | -------------------- |
| `byte`    | 8-bit  | `byte b = 10;`       |
| `short`   | 16-bit | `short s = 200;`     |
| `int`     | 32-bit | `int i = 1000;`      |
| `long`    | 64-bit | `long l = 123456L;`  |
| `float`   | 32-bit | `float f = 12.3f;`   |
| `double`  | 64-bit | `double d = 123.45;` |
| `char`    | 16-bit | `char c = 'A';`      |
| `boolean` | 1-bit  | `boolean b = true;`  |

🧠 **Tip**: Use `L` for long literals, and `f` for float literals.

### 🔸 Reference Types:

* Objects (like `String`, arrays, user-defined classes).

```java
String name = "Alice";
int[] nums = {1, 2, 3};
```

---

## 🔹 4. Naming Conventions and Syntax Rules

✅ **Valid Identifiers**:

* Start with letter, `$`, or `_`.
* Can’t start with digits or use keywords.

✅ **Best Practices**:

* `camelCase` for variables/methods
* `PascalCase` for classes
* ALL\_CAPS for constants

🧠 **Memory Hook**: *Camel has humps* → `camelCase` for methods and variables!

---

## 🔹 5. Type Conversion and Casting

### 🔸 Implicit (Widening):

```java
int i = 100;
long l = i; // OK
```

### 🔸 Explicit (Narrowing):

```java
double d = 123.45;
int i = (int) d; // Needs casting
```

⚠️ Be careful — narrowing may lose data!

---

## 🔹 6. `var` Keyword (Java 10+)

```java
var name = "John";   // Compiler infers String
var age = 25;        // Compiler infers int
```

📌 You can’t assign `null` or change type later.

🧠 **Use when**:

* Type is obvious
* Improves readability

---

## ✍️ Practice Exercises

### 🧪 Exercise 1: Write a Java class called `Student` that:

* Declares `name` (String), `age` (int), and `grade` (char) variables
* Assigns values to them and prints them out

<details>
<summary>✅ Solution</summary>

```java
public class Student {
    public static void main(String[] args) {
        String name = "Emily";
        int age = 20;
        char grade = 'A';

        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
        System.out.println("Grade: " + grade);
    }
}
```

</details>

---

## ✅ Quick Quiz

1. What is the difference between JDK and JVM?
2. What is the default value of a boolean variable?
3. Is the following valid? `var x = null;`
4. What is the result of this cast? `int x = (int) 5.9;`
5. Which is larger in size: `int` or `float`?

---

# 🔧 Phase 2: Operators and Expressions

---

## 🔹 1. **Arithmetic Operators**

Used for basic mathematical operations.

```java
int a = 10, b = 3;

System.out.println(a + b);  // Addition → 13
System.out.println(a - b);  // Subtraction → 7
System.out.println(a * b);  // Multiplication → 30
System.out.println(a / b);  // Integer Division → 3
System.out.println(a % b);  // Remainder → 1
```

🧠 **Tip**: `a / b` for integers truncates the decimal!

---

## 🔹 2. **Relational (Comparison) Operators**

Returns `true` or `false`.

```java
a > b     // true
a < b     // false
a >= b    // true
a <= b    // false
a == b    // false
a != b    // true
```

🧠 **Tip**: `==` compares values, **not objects** (we’ll revisit this in object comparisons).

---

## 🔹 3. **Logical Operators**

Used to combine boolean conditions.

| Operator | Meaning     | Example          |            |         |   |         |
| -------- | ----------- | ---------------- | ---------- | ------- | - | ------- |
| `&&`     | Logical AND | `a > 0 && b < 5` |            |         |   |         |
| \`       |             | \`               | Logical OR | \`a > 0 |   | b < 5\` |
| `!`      | Logical NOT | `!(a > 0)`       |            |         |   |         |

📌 **Short-circuiting**:

* `&&` stops if the first condition is false.
* `||` stops if the first condition is true.

```java
int x = 0;
if (x != 0 && 10 / x > 1) { } // Safe, short-circuit avoids division by zero
```

---

## 🔹 4. **Assignment Operators**

```java
int x = 10;
x += 5;   // x = x + 5 → 15
x -= 3;   // x = x - 3 → 12
x *= 2;   // x = x * 2 → 24
x /= 6;   // x = x / 6 → 4
x %= 3;   // x = x % 3 → 1
```

---

## 🔹 5. **Unary Operators**

| Operator | Description                |
| -------- | -------------------------- |
| `+`      | Unary plus                 |
| `-`      | Unary minus                |
| `++`     | Increment                  |
| `--`     | Decrement                  |
| `!`      | Logical negation (boolean) |

```java
int a = 5;
System.out.println(++a); // pre-increment: a becomes 6, prints 6
System.out.println(a++); // post-increment: prints 6, then a becomes 7
```

---

## 🔹 6. **Ternary Operator**

Shortcut for simple `if-else`.

```java
int age = 18;
String result = (age >= 18) ? "Adult" : "Minor";
System.out.println(result); // Adult
```

📌 **Form**: `(condition) ? valueIfTrue : valueIfFalse`

---

## 🔹 7. **Operator Precedence & Associativity**

When multiple operators are used, Java follows **precedence rules**.

| Precedence (High → Low) | Operators                    |   |    |
| ----------------------- | ---------------------------- | - | -- |
| 1                       | `()` (parentheses)           |   |    |
| 2                       | `++`, `--`, `+`, `-` (unary) |   |    |
| 3                       | `*`, `/`, `%`                |   |    |
| 4                       | `+`, `-`                     |   |    |
| 5                       | `<`, `>`, `<=`, `>=`         |   |    |
| 6                       | `==`, `!=`                   |   |    |
| 7                       | `&&`                         |   |    |
| 8                       | \`                           |   | \` |
| 9                       | `=`, `+=`, `-=`, `*=`, etc.  |   |    |

🧠 **Rule of Thumb**: Use parentheses `()` to make precedence explicit and code readable.

---

## ✍️ Practice Exercises

### 🧪 Exercise 1: Predict the output

```java
int a = 4, b = 5;
System.out.println(++a * b--);
System.out.println("a = " + a);
System.out.println("b = " + b);
```

<details>
<summary>✅ Solution</summary>

1. `++a` → `a` becomes 5
2. `b--` → uses 5, then `b` becomes 4
3. Result → `5 * 5 = 25`
4. Final values: `a = 5`, `b = 4`

</details>

---

### 🧪 Exercise 2: Use a ternary operator

Write a Java program that:

* Accepts a number
* Prints "Even" or "Odd" using the ternary operator

<details>
<summary>✅ Solution</summary>

```java
public class EvenOdd {
    public static void main(String[] args) {
        int num = 7;
        String result = (num % 2 == 0) ? "Even" : "Odd";
        System.out.println(result);
    }
}
```

</details>

---

## ✅ Quick Quiz

1. What’s the output? `System.out.println(10 + 20 + "Java");`
2. What’s the result of `true || false && false`?
3. What’s the difference between `a++` and `++a`?
4. What does the `%` operator return?
5. When is the ternary operator useful?

---

## 🔍 Common Interview Traps

* **Order of evaluation**: `System.out.println("Result: " + 1 + 2);` → prints `"Result: 12"` not `"3"`.
* **Short-circuiting**: Can protect against exceptions.
* **Post vs pre increment** in loops and conditions.

---

# 🔀 Phase 3: Making Decisions (Control Flow)

---

## 🔹 1. `if`, `else if`, and `else`

```java
int age = 18;

if (age < 18) {
    System.out.println("Minor");
} else if (age == 18) {
    System.out.println("Just became adult");
} else {
    System.out.println("Adult");
}
```

🧠 **Execution Flow**:

* Conditions are checked in order.
* First true block is executed.
* Others are skipped.

---

## 🔹 2. `switch` Statement

When checking a single variable against many values, `switch` is clearer than many `if`s.

```java
int day = 2;

switch (day) {
    case 1: System.out.println("Monday"); break;
    case 2: System.out.println("Tuesday"); break;
    default: System.out.println("Other day");
}
```

✅ Supports:

* `byte`, `short`, `int`, `char`, `String`, and `enum` (Java 7+)

🧠 **Tip**: `break` is essential to prevent *fall-through*!

---

## 🔹 3. Modern `switch` Expression (Java 14+)

More concise and safer:

```java
int day = 3;
String result = switch (day) {
    case 1 -> "Monday";
    case 2 -> "Tuesday";
    default -> "Other";
};
System.out.println(result);
```

📌 **Benefits**:

* No need for `break`
* Can return values

---

## 🔹 4. Nested `if` Statements

```java
int score = 85;

if (score >= 50) {
    if (score >= 80) {
        System.out.println("Distinction");
    } else {
        System.out.println("Pass");
    }
} else {
    System.out.println("Fail");
}
```

🧠 Use nesting *carefully*. Overuse → unreadable code.

---

## 🔹 5. Logical Flow Summary

| Syntax Type    | Use When                                         |
| -------------- | ------------------------------------------------ |
| `if-else`      | Simple yes/no or multiple condition checks       |
| `switch`       | Single variable against multiple constant values |
| Ternary (`?:`) | Simple 1-liner decisions                         |
| `if` nesting   | You need step-wise, layered decisions            |

---

## ✍️ Practice Exercises

### 🧪 Exercise 1: Grade Evaluator

Write a Java program that:

* Takes a `score` (int)
* Prints grade:

  * `90+` → "A"
  * `80+` → "B"
  * `70+` → "C"
  * Below 70 → "F"

<details>
<summary>✅ Solution</summary>

```java
public class GradeEvaluator {
    public static void main(String[] args) {
        int score = 85;

        if (score >= 90) {
            System.out.println("Grade A");
        } else if (score >= 80) {
            System.out.println("Grade B");
        } else if (score >= 70) {
            System.out.println("Grade C");
        } else {
            System.out.println("Grade F");
        }
    }
}
```

</details>

---

### 🧪 Exercise 2: Switch on Month

Print the number of days in a month using `switch`. Assume February has 28 days.

<details>
<summary>✅ Solution</summary>

```java
public class MonthDays {
    public static void main(String[] args) {
        String month = "February";

        switch (month) {
            case "January", "March", "May", "July", "August", "October", "December" ->
                System.out.println("31 days");
            case "April", "June", "September", "November" ->
                System.out.println("30 days");
            case "February" ->
                System.out.println("28 days");
            default ->
                System.out.println("Invalid month");
        }
    }
}
```

</details>

---

## ✅ Quick Quiz

1. What happens if you omit `break` in a `switch` case?
2. Which version of Java introduced `switch` as an expression?
3. Can `switch` work with `String`?
4. What is the output?

   ```java
   int x = 10;
   if (x > 5)
       if (x < 15)
           System.out.println("A");
       else
           System.out.println("B");
   ```

---

## 🧠 Gotchas

* `switch` without `break` → fall-through
* Always cover the **default** case in `switch`
* Avoid **deep nesting** of `if`s unless necessary

---

# 🧩 Phase 4: Methods in Java

---

## 🔹 1. What is a Method?

A **method** is a block of code that performs a specific task.

🔹 **Benefits:**

* Avoids code duplication
* Makes code modular and readable
* Enables reuse and testing

---

## 🔹 2. Method Structure

```java
<access_modifier> <return_type> <method_name>(<parameters>) {
    // method body
    return value; // if return_type is not void
}
```

---

## 🔹 3. Method Examples

### Example 1: A simple method

```java
public static void greet() {
    System.out.println("Hello, world!");
}
```

Call it with:

```java
greet(); // prints: Hello, world!
```

---

### Example 2: Method with parameters

```java
public static void greetUser(String name) {
    System.out.println("Hello, " + name + "!");
}
```

```java
greetUser("Alice"); // Hello, Alice!
```

---

### Example 3: Method with return value

```java
public static int add(int a, int b) {
    return a + b;
}
```

```java
int sum = add(5, 3); // sum = 8
```

---

## 🔹 4. Key Concepts

### a. **Return Type**

* `void` → no return
* `int`, `String`, `double`, etc. → must return a value

### b. **Parameters and Arguments**

* **Parameters**: variables defined in method declaration
* **Arguments**: values passed during the call

---

## 🔹 5. Method Overloading

**Same name**, different parameter list (number or types of parameters).

```java
public static int square(int x) {
    return x * x;
}

public static double square(double x) {
    return x * x;
}
```

Java decides which version to call based on the arguments passed.

---

## 🔹 6. `main()` Method

Entry point of every Java program:

```java
public static void main(String[] args) {
    // program starts here
}
```

* `static`: can run without an instance
* `String[] args`: allows passing command-line arguments

---

## 🔹 7. Method Calling Rules

* Methods in the **same class** can be called directly if `static`.
* Non-static methods need an **object** to be called.

```java
public class Calculator {
    public int add(int x, int y) {
        return x + y;
    }

    public static void main(String[] args) {
        Calculator calc = new Calculator();
        int result = calc.add(2, 3);
        System.out.println(result); // 5
    }
}
```

---

## ✍️ Practice Exercises

### 🧪 Exercise 1: Max of two numbers

Write a method `max(int a, int b)` that returns the larger value.

<details>
<summary>✅ Solution</summary>

```java
public static int max(int a, int b) {
    return (a > b) ? a : b;
}
```

</details>

---

### 🧪 Exercise 2: Prime Checker

Write a method `isPrime(int n)` that returns `true` if `n` is prime.

<details>
<summary>✅ Solution</summary>

```java
public static boolean isPrime(int n) {
    if (n <= 1) return false;
    for (int i = 2; i <= Math.sqrt(n); i++) {
        if (n % i == 0) return false;
    }
    return true;
}
```

</details>

---

### 🧪 Exercise 3: Method Overloading

Create multiple `multiply()` methods:

* one for `int a, int b`
* one for `double a, double b`

---

## ✅ Quick Quiz

1. What is the difference between parameters and arguments?
2. Can a method return multiple values in Java?
3. What is method overloading and how does Java resolve it?
4. What happens if a method with return type doesn’t use `return`?

---

## 🧠 Gotchas & Tips

* Always match method **return type** and **actual return value**.
* Avoid excessive method length: aim for **single responsibility**.
* Prefer **descriptive names** like `calculateTax()` over vague ones like `doIt()`.

---

## 🧠 Optional Challenge

Write a calculator app with methods for:

* `add(int, int)`
* `subtract(int, int)`
* `multiply(int, int)`
* `divide(int, int)` (return `double`, handle divide by 0) 

---

# 🏗️ Phase 5: Class Design

---

## 🔹 1. What is a Class?

A **class** is a *blueprint* for creating **objects**.

```java
public class Car {
    String color;
    int speed;

    void drive() {
        System.out.println("Car is driving");
    }
}
```

> Think of a class as a template and an object as an actual instance of it.

---

## 🔹 2. Creating an Object

```java
Car myCar = new Car();
myCar.color = "Red";
myCar.speed = 100;
myCar.drive();
```

---

## 🔹 3. Instance Variables and Methods

* **Instance variables** (fields) belong to the object.
* **Instance methods** operate on those variables.

```java
public class Person {
    String name;

    void sayHello() {
        System.out.println("Hello, my name is " + name);
    }
}
```

---

## 🔹 4. `this` Keyword

`this` refers to the **current object**.

```java
public class Student {
    String name;

    Student(String name) {
        this.name = name;
    }
}
```

---

## 🔹 5. Constructors

Special methods used to **initialize objects**.

```java
public class Book {
    String title;

    // Constructor
    public Book(String t) {
        title = t;
    }
}
```

If you don’t define any, Java adds a **default constructor**.

You can **overload constructors**:

```java
public class Rectangle {
    int length, width;

    Rectangle() {
        length = 1; width = 1;
    }

    Rectangle(int l, int w) {
        length = l; width = w;
    }
}
```

---

## 🔹 6. Access Modifiers

| Modifier    | Accessible From          |
| ----------- | ------------------------ |
| `public`    | Everywhere               |
| `private`   | Within the same class    |
| `protected` | Same package or subclass |
| *(default)* | Same package only        |

Encapsulation uses **`private` fields + public getters/setters**.

---

## 🔹 7. Encapsulation

**Bundle data + methods**, restrict direct access.

```java
public class BankAccount {
    private double balance;

    public void deposit(double amount) {
        balance += amount;
    }

    public double getBalance() {
        return balance;
    }
}
```

---

## 🔹 8. Static Members

* Belong to **class**, not individual objects.
* Called via class name.

```java
public class MathUtils {
    public static int square(int x) {
        return x * x;
    }
}
```

```java
int result = MathUtils.square(5); // 25
```

---

## 🔹 9. `toString()` Method

Overrides the default object representation.

```java
public class User {
    String name;
    int age;

    public String toString() {
        return name + " (" + age + ")";
    }
}
```

---

## 🔹 10. `equals()` and `hashCode()`

To compare objects meaningfully:

```java
public boolean equals(Object o) {
    if (this == o) return true;
    if (!(o instanceof User)) return false;
    User other = (User) o;
    return this.name.equals(other.name);
}
```

---

## ✍️ Practice Exercises

### 🧪 Exercise 1: Create a `Laptop` class

With fields:

* `brand`, `price`
* constructor, `toString()` method

<details>
<summary>✅ Solution</summary>

```java
public class Laptop {
    String brand;
    double price;

    public Laptop(String brand, double price) {
        this.brand = brand;
        this.price = price;
    }

    public String toString() {
        return brand + ": $" + price;
    }
}
```

</details>

---

### 🧪 Exercise 2: BankAccount with Encapsulation

Fields:

* `private double balance`

Methods:

* `public void deposit(double)`
* `public void withdraw(double)`
* `public double getBalance()`

---

## ✅ Quick Quiz

1. What is the difference between a constructor and a method?
2. What is the purpose of `this`?
3. What happens if no constructor is defined?
4. What’s the difference between instance and static members?
5. What does `toString()` do?

---

## 🧠 Tips & Gotchas

* Always make fields `private` for **encapsulation**
* Use constructors to avoid object misconfiguration
* Avoid creating too many public setters (immutability is better)
* Override `toString()` for better debugging

---

# Beyond Classes: Advanced OOP and Design in Java

## Part 1: Core OOP Foundations

### 1. The Four Pillars of OOP

**Encapsulation**
```java
public class BankAccount {
    private double balance;  // Data hiding
    
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        }
    }
    
    public double getBalance() {
        return balance;
    }
}
```

**Inheritance**
```java
class Vehicle {
    void move() {
        System.out.println("Vehicle is moving");
    }
}

class Car extends Vehicle {
    @Override
    void move() {
        System.out.println("Car is driving");
    }
}
```

**Polymorphism**
```java
interface Shape {
    double area();
}

class Circle implements Shape {
    private double radius;
    
    @Override
    public double area() {
        return Math.PI * radius * radius;
    }
}

class Square implements Shape {
    private double side;
    
    @Override
    public double area() {
        return side * side;
    }
}
```

**Abstraction**
```java
abstract class Database {
    abstract void connect();
    
    void disconnect() {
        System.out.println("Disconnecting from database");
    }
}

class MySQLDatabase extends Database {
    @Override
    void connect() {
        System.out.println("Connecting to MySQL");
    }
}
```

## Part 2: Advanced Class Design

### 2. Composition Over Inheritance

```java
// Prefer this:
class Engine {
    void start() { /* ... */ }
}

class Car {
    private Engine engine;
    
    void start() {
        engine.start();
    }
}

// Over this:
class Car extends Engine { /* ... */ }
```

### 3. The Liskov Substitution Principle (LSP)

```java
class Bird {
    void fly() { /* ... */ }
}

// Violates LSP:
class Penguin extends Bird {
    @Override
    void fly() {
        throw new UnsupportedOperationException("Penguins can't fly!");
    }
}

// Better approach:
interface Flyable {
    void fly();
}

class Sparrow implements Flyable { /* ... */ }
class Penguin implements Bird { /* ... */ }
```

## Part 3: Design Patterns Fundamentals

### 4. Singleton Pattern

```java
public class DatabaseConnection {
    private static volatile DatabaseConnection instance;
    
    private DatabaseConnection() {}
    
    public static DatabaseConnection getInstance() {
        if (instance == null) {
            synchronized (DatabaseConnection.class) {
                if (instance == null) {
                    instance = new DatabaseConnection();
                }
            }
        }
        return instance;
    }
}
```

### 5. Factory Pattern

```java
interface PaymentProcessor {
    void processPayment(double amount);
}

class CreditCardProcessor implements PaymentProcessor {
    @Override
    public void processPayment(double amount) { /* ... */ }
}

class PayPalProcessor implements PaymentProcessor {
    @Override
    public void processPayment(double amount) { /* ... */ }
}

class PaymentProcessorFactory {
    public static PaymentProcessor getProcessor(String type) {
        return switch (type.toLowerCase()) {
            case "creditcard" -> new CreditCardProcessor();
            case "paypal" -> new PayPalProcessor();
            default -> throw new IllegalArgumentException("Unknown processor");
        };
    }
}
```

## Part 4: SOLID Principles Deep Dive

### 6. Single Responsibility Principle (SRP)

```java
// Violation:
class User {
    void saveToDatabase() { /* ... */ }
    void sendEmail() { /* ... */ }
    void validate() { /* ... */ }
}

// Compliant:
class User {
    // Only user-related properties
}

class UserRepository {
    void save(User user) { /* ... */ }
}

class EmailService {
    void sendEmail(User user) { /* ... */ }
}

class UserValidator {
    boolean validate(User user) { /* ... */ }
}
```

### 7. Open/Closed Principle (OCP)

```java
interface DiscountStrategy {
    double applyDiscount(double price);
}

class RegularDiscount implements DiscountStrategy {
    @Override
    public double applyDiscount(double price) {
        return price * 0.9;
    }
}

class PremiumDiscount implements DiscountStrategy {
    @Override
    public double applyDiscount(double price) {
        return price * 0.7;
    }
}

class DiscountCalculator {
    private DiscountStrategy strategy;
    
    public DiscountCalculator(DiscountStrategy strategy) {
        this.strategy = strategy;
    }
    
    public double calculate(double price) {
        return strategy.applyDiscount(price);
    }
}
```

## Part 5: Advanced Design Patterns

### 8. Strategy Pattern

```java
interface CompressionStrategy {
    void compress(String file);
}

class ZipCompression implements CompressionStrategy {
    @Override
    public void compress(String file) {
        System.out.println("Compressing " + file + " using ZIP");
    }
}

class RarCompression implements CompressionStrategy {
    @Override
    public void compress(String file) {
        System.out.println("Compressing " + file + " using RAR");
    }
}

class CompressionContext {
    private CompressionStrategy strategy;
    
    public void setStrategy(CompressionStrategy strategy) {
        this.strategy = strategy;
    }
    
    public void createArchive(String file) {
        strategy.compress(file);
    }
}
```

### 9. Observer Pattern

```java
interface Observer {
    void update(String message);
}

interface Subject {
    void register(Observer observer);
    void unregister(Observer observer);
    void notifyObservers();
}

class NewsAgency implements Subject {
    private List<Observer> observers = new ArrayList<>();
    private String news;
    
    @Override
    public void register(Observer observer) {
        observers.add(observer);
    }
    
    @Override
    public void unregister(Observer observer) {
        observers.remove(observer);
    }
    
    @Override
    public void notifyObservers() {
        observers.forEach(observer -> observer.update(news));
    }
    
    public void setNews(String news) {
        this.news = news;
        notifyObservers();
    }
}

class NewsChannel implements Observer {
    private String news;
    
    @Override
    public void update(String news) {
        this.news = news;
        display();
    }
    
    public void display() {
        System.out.println("Breaking News: " + news);
    }
}
```

## Part 6: Java-Specific Advanced Features

### 10. Generics and Type Safety

```java
class Box<T> {
    private T content;
    
    public void setContent(T content) {
        this.content = content;
    }
    
    public T getContent() {
        return content;
    }
}

// Bounded type parameter
class NumberBox<T extends Number> {
    private T number;
    
    public double square() {
        return number.doubleValue() * number.doubleValue();
    }
}
```

### 11. Effective Java Practices

**Item 17: Minimize mutability**
```java
public final class ImmutablePoint {
    private final double x;
    private final double y;
    
    public ImmutablePoint(double x, double y) {
        this.x = x;
        this.y = y;
    }
    
    public double getX() { return x; }
    public double getY() { return y; }
    
    public ImmutablePoint translate(double dx, double dy) {
        return new ImmutablePoint(x + dx, y + dy);
    }
}
```

## Part 7: Architectural Considerations

### 12. Dependency Injection

```java
interface MessageService {
    void sendMessage(String msg, String recipient);
}

class EmailService implements MessageService {
    @Override
    public void sendMessage(String msg, String recipient) {
        // Email sending logic
    }
}

class SMSService implements MessageService {
    @Override
    public void sendMessage(String msg, String recipient) {
        // SMS sending logic
    }
}

class NotificationService {
    private final MessageService service;
    
    // Constructor injection
    public NotificationService(MessageService service) {
        this.service = service;
    }
    
    public void notifyUser(String msg, String recipient) {
        service.sendMessage(msg, recipient);
    }
}
```

### 13. Domain-Driven Design Basics

```java
// Value Object
public final class Address {
    private final String street;
    private final String city;
    private final String zipCode;
    
    public Address(String street, String city, String zipCode) {
        this.street = street;
        this.city = city;
        this.zipCode = zipCode;
    }
    
    // No setters, immutable
    // equals() and hashCode() implementations
}

// Aggregate Root
public class Order {
    private OrderId id;
    private List<OrderItem> items;
    private Customer customer;
    
    public void addItem(Product product, int quantity) {
        // Domain logic
    }
    
    public void complete() {
        // Domain logic
    }
}
```

## Part 8: Integration with Design Patterns and Best Practices

### 14. Adapter Pattern for Legacy Systems

The **Adapter Pattern** is useful when integrating new systems with legacy code or third-party libraries that don’t follow the same interface. Here's an example of adapting a legacy payment gateway to work with a modern system:

```java
interface ModernPaymentGateway {
    void makePayment(double amount);
}

// Legacy system with different API
class LegacyPaymentSystem {
    public void payWithLegacyAPI(int amountInCents) {
        System.out.println("Processing $" + (amountInCents / 100.0) + " via legacy system");
    }
}

// Adapter
class LegacyPaymentAdapter implements ModernPaymentGateway {
    private LegacyPaymentSystem legacySystem;

    public LegacyPaymentAdapter(LegacyPaymentSystem legacySystem) {
        this.legacySystem = legacySystem;
    }

    @Override
    public void makePayment(double amount) {
        int cents = (int)(amount * 100);
        legacySystem.payWithLegacyAPI(cents);
    }
}
```

This allows developers to integrate legacy systems into modern applications without modifying the existing codebase .

### 15. Template Method Pattern for Code Reuse

The **Template Method Pattern** defines the skeleton of an algorithm in a method, deferring some steps to subclasses. It’s ideal for situations where you want to enforce a common structure but allow customization in specific parts:

```java
abstract class Game {
    abstract void initialize();
    abstract void startPlay();
    abstract void endPlay();

    // Template method
    public final void play() {
        initialize();
        startPlay();
        endPlay();
    }
}

class Cricket extends Game {
    @Override
    void initialize() {
        System.out.println("Cricket Game Initialized");
    }

    @Override
    void startPlay() {
        System.out.println("Cricket Game Started");
    }

    @Override
    void endPlay() {
        System.out.println("Cricket Game Finished");
    }
}

class Football extends Game {
    @Override
    void initialize() {
        System.out.println("Football Game Initialized");
    }

    @Override
    void startPlay() {
        System.out.println("Football Game Started");
    }

    @Override
    void endPlay() {
        System.out.println("Football Game Finished");
    }
}
```

This pattern helps reduce code duplication by defining a consistent flow while allowing flexibility in implementation .

### 16. Builder Pattern for Complex Object Construction

The **Builder Pattern** is particularly useful when constructing complex objects with many optional parameters. It separates the construction of an object from its representation:

```java
class Pizza {
    private String dough;
    private String sauce;
    private String toppings;

    public void setDough(String dough) {
        this.dough = dough;
    }

    public void setSauce(String sauce) {
        this.sauce = sauce;
    }

    public void setToppings(String toppings) {
        this.toppings = toppings;
    }

    @Override
    public String toString() {
        return "Pizza [dough=" + dough + ", sauce=" + sauce + ", toppings=" + toppings + "]";
    }
}

class PizzaBuilder {
    private Pizza pizza = new Pizza();

    public PizzaBuilder setDough(String dough) {
        pizza.setDough(dough);
        return this;
    }

    public PizzaBuilder setSauce(String sauce) {
        pizza.setSauce(sauce);
        return this;
    }

    public PizzaBuilder setToppings(String toppings) {
        pizza.setToppings(toppings);
        return this;
    }

    public Pizza build() {
        return pizza;
    }
}

// Usage
Pizza myPizza = new PizzaBuilder()
    .setDough("thin")
    .setSauce("tomato")
    .setToppings("cheese, ham")
    .build();
```

This pattern improves readability and maintainability when creating complex objects . 

### 17. Facade Pattern for Simplified Interfaces

The **Facade Pattern** provides a simplified interface to a complex subsystem. This pattern is helpful when dealing with large APIs or multiple classes that need to be coordinated:

```java
// Subsystems
class DVDPlayer {
    public void on() {
        System.out.println("DVD Player On");
    }

    public void play(String movie) {
        System.out.println("Playing " + movie);
    }

    public void off() {
        System.out.println("DVD Player Off");
    }
}

class Projector {
    public void on() {
        System.out.println("Projector On");
    }

    public void wideScreenMode() {
        System.out.println("Set to Wide Screen Mode");
    }

    public void off() {
        System.out.println("Projector Off");
    }
}

// Facade
class HomeTheaterFacade {
    private DVDPlayer dvd;
    private Projector projector;

    public HomeTheaterFacade(DVDPlayer dvd, Projector projector) {
        this.dvd = dvd;
        this.projector = projector;
    }

    public void watchMovie(String movie) {
        projector.on();
        projector.wideScreenMode();
        dvd.on();
        dvd.play(movie);
    }

    public void endMovie() {
        projector.off();
        dvd.stop();
        dvd.off();
    }
}
```

By encapsulating the complexity of interacting with multiple components, the facade makes the system easier to use and reduces coupling between clients and subsystems .

### 18. Decorator Pattern for Dynamic Behavior Addition

The **Decorator Pattern** allows behavior to be added to individual objects dynamically, without affecting the behavior of other objects from the same class. It is often used in scenarios like adding features to streams or GUI components:

```java
interface Coffee {
    double cost();
    String description();
}

class SimpleCoffee implements Coffee {
    @Override
    public double cost() {
        return 2.0;
    }

    @Override
    public String description() {
        return "Simple Coffee";
    }
}

abstract class CoffeeDecorator implements Coffee {
    protected Coffee decoratedCoffee;

    public CoffeeDecorator(Coffee decoratedCoffee) {
        this.decoratedCoffee = decoratedCoffee;
    }

    @Override
    public double cost() {
        return decoratedCoffee.cost();
    }

    @Override
    public String description() {
        return decoratedCoffee.description();
    }
}

class MilkDecorator extends CoffeeDecorator {
    public MilkDecorator(Coffee decoratedCoffee) {
        super(decoratedCoffee);
    }

    @Override
    public double cost() {
        return super.cost() + 0.5;
    }

    @Override
    public String description() {
        return super.description() + ", Milk";
    }
}

class SugarDecorator extends CoffeeDecorator {
    public SugarDecorator(Coffee decoratedCoffee) {
        super(decoratedCoffee);
    }

    @Override
    public double cost() {
        return super.cost() + 0.2;
    }

    @Override
    public String description() {
        return super.description() + ", Sugar";
    }
}

// Usage
Coffee coffee = new SimpleCoffee();
coffee = new MilkDecorator(coffee);
coffee = new SugarDecorator(coffee);

System.out.println("Cost: $" + coffee.cost());
System.out.println("Description: " + coffee.description());
```

This pattern enables flexible extension of functionality at runtime, avoiding the need for subclassing for every possible combination .

### 19. Chain of Responsibility Pattern for Decoupled Processing

The **Chain of Responsibility Pattern** allows requests to be passed through a chain of handlers until one of them handles it. It decouples the sender of a request from its receiver:

```java
abstract class RequestHandler {
    protected RequestHandler nextHandler;

    public void setNextHandler(RequestHandler nextHandler) {
        this.nextHandler = nextHandler;
    }

    public abstract void handleRequest(Request request);
}

class Manager extends RequestHandler {
    @Override
    public void handleRequest(Request request) {
        if (request.getAmount() <= 1000) {
            System.out.println("Manager approved the request of $" + request.getAmount());
        } else if (nextHandler != null) {
            nextHandler.handleRequest(request);
        }
    }
}

class Director extends RequestHandler {
    @Override
    public void handleRequest(Request request) {
        if (request.getAmount() <= 5000) {
            System.out.println("Director approved the request of $" + request.getAmount());
        } else if (nextHandler != null) {
            nextHandler.handleRequest(request);
        }
    }
}

class President extends RequestHandler {
    @Override
    public void handleRequest(Request request) {
        System.out.println("President approved the request of $" + request.getAmount());
    }
}

class Request {
    private double amount;

    public Request(double amount) {
        this.amount = amount;
    }

    public double getAmount() {
        return amount;
    }
}

// Usage
RequestHandler manager = new Manager();
RequestHandler director = new Director();
RequestHandler president = new President();

manager.setNextHandler(director);
director.setNextHandler(president);

Request request1 = new Request(800);
Request request2 = new Request(3000);
Request request3 = new Request(7000);

manager.handleRequest(request1);
manager.handleRequest(request2);
manager.handleRequest(request3);
```

This pattern is especially useful in scenarios like logging, validation, or workflow management, where multiple layers of processing are required .
