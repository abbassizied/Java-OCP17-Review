# Exceptions in Java

---

## 🧠 **Lesson 1: Introduction to Exceptions in Java**

---

### 📌 What Are Exceptions?

An **exception** is an **event** that disrupts the normal flow of a program's execution. Java provides a powerful mechanism to **detect**, **handle**, and **recover** from errors at runtime.

---

### 🔷 1. **Throwable Hierarchy**

```
           Throwable
           /       \
      Error        Exception
                    /     \
       Checked     Unchecked (RuntimeException)
```

* **Error**: Critical issues (e.g., `OutOfMemoryError`) — should not be caught.
* **Checked Exceptions**: Must be handled or declared (`IOException`, `SQLException`)
* **Unchecked Exceptions**: Can be avoided if your code is correct (`NullPointerException`, `IllegalArgumentException`)

---

### 🔷 2. **Basic Exception Syntax**

```java
try {
    // code that may throw an exception
} catch (ExceptionType name) {
    // handle exception
} finally {
    // optional: always executed
}
```

---

### 🔷 3. **Example: ArithmeticException**

```java
public class Demo {
    public static void main(String[] args) {
        try {
            int result = 10 / 0; // ❌
        } catch (ArithmeticException e) {
            System.out.println("Cannot divide by zero!");
        } finally {
            System.out.println("Done!");
        }
    }
}
```

Output:

```
Cannot divide by zero!
Done!
```

---

### 🔷 4. **Common Runtime Exceptions**

| Exception                        | Cause                              |
| -------------------------------- | ---------------------------------- |
| `NullPointerException`           | Accessing an object that is `null` |
| `ArrayIndexOutOfBoundsException` | Invalid array index                |
| `IllegalArgumentException`       | Invalid method arguments           |
| `ArithmeticException`            | Division by zero                   |

---

### 🔷 5. **Multiple Catch Blocks**

```java
try {
    // risky code
} catch (IOException e) {
    // file error
} catch (SQLException e) {
    // db error
}
```

### 🔷 6. **Multi-Catch (Java 7+)**

```java
catch (IOException | SQLException e) {
    // handle both
}
```

---

### 🔷 7. **The `finally` Block**

Always runs — even if an exception is thrown or `return` is called.

Use it for **cleanup** (closing files, releasing resources).

```java
try {
    // risky
} finally {
    // always runs
}
```

---

### 📌 Best Practices

* Handle only what you can **recover** from.
* Don’t catch `Exception` or `Throwable` unless necessary.
* Log or rethrow critical exceptions.
* Always close resources — preferably using **try-with-resources** (covered later).

---

## 🧠 **Lesson 2: Checked Exceptions, `throws`, and Propagation**

---

### 🔷 1. **What Are Checked Exceptions?**

Checked exceptions are **checked at compile time**. If a method can throw one, the compiler enforces you to **handle it or declare it**.

Examples:

* `IOException`
* `SQLException`
* `FileNotFoundException`
* `ParseException`

---

### 🔷 2. **Declaring Exceptions with `throws`**

If a method can throw a checked exception but **doesn't handle it**, it must declare it:

```java
public void readFile(String path) throws IOException {
    Files.readAllLines(Path.of(path)); // throws IOException
}
```

---

### 🔷 3. **Handling vs Propagating**

You have two choices:

**Option A: Handle it (try-catch)**

```java
try {
    readFile("data.txt");
} catch (IOException e) {
    e.printStackTrace();
}
```

**Option B: Propagate it (rethrow)**

```java
public static void main(String[] args) throws IOException {
    readFile("data.txt"); // declared, so no try-catch needed here
}
```

---

### 🔷 4. **The Golden Rule**

> **You must either handle the exception (`try-catch`) or declare it (`throws`) — never ignore it.**

Unchecked exceptions (RuntimeExceptions) **do not require** this.

---

### 🔷 5. **Multi-Level Propagation**

If `methodA()` calls `methodB()` which calls `methodC()` — and `methodC()` throws `IOException`, all three must either handle or declare it.

```java
void methodC() throws IOException { ... }

void methodB() throws IOException {
    methodC();
}

void methodA() throws IOException {
    methodB();
}
```

---

### 🔷 6. **Checked vs Unchecked Exceptions**

| Feature             | Checked Exception             | Unchecked Exception (Runtime)                      |
| ------------------- | ----------------------------- | -------------------------------------------------- |
| Checked by compiler | ✅ Yes                         | ❌ No                                               |
| Must be declared    | ✅ Yes                         | ❌ No                                               |
| Can be caught       | ✅ Yes                         | ✅ Yes                                              |
| Represents          | Recoverable issues            | Programming errors                                 |
| Examples            | `IOException`, `SQLException` | `NullPointerException`, `IllegalArgumentException` |

---

### 📌 Best Practices

* Use checked exceptions for **recoverable** conditions (file not found, network timeout).
* Use unchecked for **programming errors** (nulls, invalid args).
* Don’t overuse `throws` in public APIs — design exception-safe interfaces.

---

## 🧠 Lesson 3: **Creating Custom Exceptions in Java**

Sometimes built-in exceptions like `IllegalArgumentException` or `IOException` aren't specific enough. For **clearer intent**, you can define **custom exceptions** that match your domain.

---

### 🔷 1. **Why Custom Exceptions?**

Use custom exceptions to:

* Make your code more **readable** and **self-documenting**
* Express **domain-specific problems**
* Separate business logic errors from system errors

---

### 🔷 2. **How to Define a Custom Exception**

You can extend either:

* `Exception` → makes it a **checked** exception
* `RuntimeException` → makes it **unchecked**

#### ✅ Checked Example

```java
public class InvalidUserException extends Exception {
    public InvalidUserException(String message) {
        super(message);
    }
}
```

#### ✅ Unchecked Example

```java
public class InvalidInputException extends RuntimeException {
    public InvalidInputException(String message) {
        super(message);
    }
}
```

---

### 🔷 3. **Throwing a Custom Exception**

```java
public void registerUser(String username) throws InvalidUserException {
    if (username == null || username.isBlank()) {
        throw new InvalidUserException("Username cannot be blank");
    }
}
```

---

### 🔷 4. **Catching a Custom Exception**

```java
try {
    registerUser(" ");
} catch (InvalidUserException e) {
    System.out.println("Error: " + e.getMessage());
}
```

---

### 🔷 5. **Checked vs Unchecked – Use Guidelines**

| Use Case                       | Exception Type | Example                                                 |
| ------------------------------ | -------------- | ------------------------------------------------------- |
| User enters invalid data       | ✅ Checked      | `InvalidUserException`                                  |
| Programming error (null input) | ✅ Unchecked    | `NullPointerException` or custom `BadApiUsageException` |

---

### 🔷 6. **Adding Fields to Custom Exceptions**

Custom exceptions can have extra context:

```java
public class OutOfStockException extends Exception {
    private final String productId;

    public OutOfStockException(String productId) {
        super("Product out of stock: " + productId);
        this.productId = productId;
    }

    public String getProductId() {
        return productId;
    }
}
```

---

### 🔷 7. **Best Practices**

✅ **Do**:

* Name exceptions clearly (`InvalidOrderException`, `PermissionDeniedException`)
* Extend `RuntimeException` for programmer errors
* Extend `Exception` for recoverable, user-facing problems

❌ **Don't**:

* Create unnecessary custom exceptions (if `IllegalArgumentException` is enough, use it)
* Catch exceptions you can't handle meaningfully

---

## 🧠 Lesson 4: **Exception Chaining, Rethrowing, and Logging**

---

As a seasoned developer or architect, you’ll often need to **wrap**, **preserve**, or **log** exceptions. Java provides powerful tools for this.

---

### 🔷 1. **What is Exception Chaining?**

**Chaining** is when one exception is caused by another — letting you **preserve the root cause** while **rethrowing or wrapping** it.

#### ✅ Example:

```java
public void loadData() throws DataLoadException {
    try {
        // some IO code
        Files.readAllLines(Path.of("data.txt"));
    } catch (IOException e) {
        throw new DataLoadException("Failed to load data", e);
    }
}
```

---

### 🔷 2. **Constructors That Support Chaining**

Java exception classes support two key constructors:

```java
public CustomException(String message);
public CustomException(String message, Throwable cause);
```

This allows:

```java
throw new CustomException("Custom message", originalException);
```

And you can retrieve the cause:

```java
Throwable rootCause = e.getCause();
```

---

### 🔷 3. **Rethrowing Exceptions**

You can catch, log, and then **rethrow**:

```java
try {
    doWork();
} catch (IOException e) {
    logger.error("I/O error", e);
    throw e; // rethrowing
}
```

If you **modify the exception**, chain it:

```java
catch (SQLException e) {
    throw new DataAccessException("DB query failed", e);
}
```

---

### 🔷 4. **Custom Exception With Cause**

You can define this in your own exceptions:

```java
public class DataLoadException extends Exception {
    public DataLoadException(String message, Throwable cause) {
        super(message, cause);
    }
}
```

---

### 🔷 5. **Logging Exceptions**

For debugging or operations, log exceptions properly.

#### Using `printStackTrace()` (not recommended in production)

```java
e.printStackTrace();
```

#### Preferred: Use SLF4J / Log4j / Java Logger

```java
logger.error("Could not complete operation", e);
```

Logging libraries let you:

* Print stack traces
* Include thread info, timestamps
* Log to files, syslogs, alerts

---

### 🔷 6. **Never Swallow Exceptions Silently**

```java
try {
    // risky
} catch (Exception e) {
    // ❌ wrong: nothing here!
}
```

✅ **Always** log, rethrow, or handle meaningfully.

---

### 🔷 7. **Best Practices for Exception Design**

| Goal                | Practice                                          |
| ------------------- | ------------------------------------------------- |
| Preserve root cause | Use `Throwable cause` in constructors             |
| Improve debugging   | Include full context in messages                  |
| Avoid stack loss    | Never create `new Exception(e.getMessage())`      |
| Keep API clean      | Wrap low-level exceptions in domain-specific ones |

---

### 🔷 BONUS: `addSuppressed()` for try-with-resources

Java 7+ tracks suppressed exceptions automatically:

```java
try (InputStream in = new FileInputStream("file.txt")) {
    // read...
} catch (IOException e) {
    Throwable[] suppressed = e.getSuppressed();
}
```

---

## 🧠 Lesson 5: `try-with-resources` and `AutoCloseable`

---

### 🔷 1. **Motivation: Why `try-with-resources`?**

Before Java 7, resource management (e.g., closing files, DB connections) was error-prone:

```java
BufferedReader reader = null;
try {
    reader = new BufferedReader(new FileReader("file.txt"));
    // read...
} catch (IOException e) {
    e.printStackTrace();
} finally {
    if (reader != null) {
        try { reader.close(); } catch (IOException e) { e.printStackTrace(); }
    }
}
```

✅ This is verbose and easy to mess up.

---

### 🔷 2. **`try-with-resources` (Java 7+)**

This syntax **automatically closes** resources that implement `AutoCloseable`:

```java
try (BufferedReader reader = new BufferedReader(new FileReader("file.txt"))) {
    String line = reader.readLine();
    System.out.println(line);
} catch (IOException e) {
    e.printStackTrace();
}
```

👉 The `reader` is **automatically closed**, even if an exception is thrown.

---

### 🔷 3. **What is `AutoCloseable`?**

It's a simple interface:

```java
public interface AutoCloseable {
    void close() throws Exception;
}
```

Most I/O classes (like `InputStream`, `OutputStream`, `Reader`, `Writer`, JDBC `Connection`) implement it.

---

### 🔷 4. **Creating a Custom Resource**

```java
public class MyResource implements AutoCloseable {
    public void doSomething() {
        System.out.println("Doing something...");
    }

    @Override
    public void close() throws Exception {
        System.out.println("Closing resource");
    }
}
```

Use it like this:

```java
try (MyResource res = new MyResource()) {
    res.doSomething();
}
```

---

### 🔷 5. **Suppressed Exceptions**

If an exception is thrown inside the `try`, and **another is thrown during `close()`**, the latter is **suppressed** but not lost:

```java
try (MyResource res = new MyResource()) {
    throw new RuntimeException("Primary");
}
```

To inspect:

```java
catch (RuntimeException e) {
    for (Throwable suppressed : e.getSuppressed()) {
        System.out.println("Suppressed: " + suppressed);
    }
}
```

✅ This helps **debug multiple errors** from `try` and `close()` simultaneously.

---

### 🔷 6. **Multiple Resources**

You can manage multiple resources in the same `try` block:

```java
try (
    BufferedReader br = new BufferedReader(new FileReader("file1.txt"));
    PrintWriter pw = new PrintWriter("output.txt")
) {
    pw.println(br.readLine());
}
```

Resources are **closed in reverse order**.

---

### 🔷 7. **Common Pitfalls**

* The variable declared in `try(...)` must be **final or effectively final**
* You **cannot** reassign it inside the block
* `close()` is **guaranteed** to be called — no need for `finally`

---

## 🧠 Lesson 6: Exception Hierarchy and Best Practices

---

### 🔷 1. **Java's Exception Class Hierarchy**

All exceptions stem from:

```
java.lang.Object
  └── java.lang.Throwable
        ├── Error
        └── Exception
              ├── RuntimeException
              └── (Checked Exceptions)
```

#### ⚠️ `Throwable` has two direct children:

* **`Error`** — serious issues you shouldn't catch (e.g., `OutOfMemoryError`)
* **`Exception`** — represents recoverable problems

---

### 🔷 2. **Checked vs Unchecked Exceptions Recap**

| Feature                     | Checked                          | Unchecked                                          |
| --------------------------- | -------------------------------- | -------------------------------------------------- |
| Subclass of                 | `Exception`                      | `RuntimeException`                                 |
| Needs `throws` declaration? | ✅ Yes                            | ❌ No                                               |
| Compiler enforces handling? | ✅ Yes                            | ❌ No                                               |
| Examples                    | `IOException`, `SQLException`    | `NullPointerException`, `IllegalArgumentException` |
| Use case                    | External, recoverable conditions | Programming errors or validation issues            |

---

### 🔷 3. **When to Use Checked Exceptions**

Use **checked exceptions** when:

* The caller is expected to handle or recover from the exception
* The error represents an external problem (I/O, network, DB)

```java
public void readFile() throws IOException
```

---

### 🔷 4. **When to Use Unchecked Exceptions**

Use **unchecked exceptions** when:

* It’s a programming error (e.g., null inputs, precondition violations)
* You want cleaner APIs (let callers decide whether to catch)

```java
public void setAge(int age) {
    if (age < 0) throw new IllegalArgumentException("Age must be positive");
}
```

---

### 🔷 5. **When NOT to Use Exceptions**

Avoid using exceptions for:

* **Flow control** (e.g., looping)
* **Performance-sensitive code** — exception handling is relatively costly

```java
// ❌ Bad practice:
try {
    return list.get(index);
} catch (IndexOutOfBoundsException e) {
    return null;
}
```

Use bounds checking instead.

---

### 🔷 6. **Wrapping and Propagation Strategies**

* **Wrap low-level exceptions** with domain-specific ones:

```java
try {
    db.query();
} catch (SQLException e) {
    throw new DataAccessException("DB failure", e);
}
```

* **Avoid leaking implementation details** through APIs (e.g., don't throw `SQLException` from your service layer)

---

### 🔷 7. **Top Best Practices Summary**

✅ **Do:**

* Be precise with exception names (`InvalidOrderException`, not just `Exception`)
* Document thrown exceptions in method Javadoc
* Fail fast on invalid arguments (`Objects.requireNonNull`, `IllegalArgumentException`)
* Use `try-with-resources` for anything that implements `AutoCloseable`
* Log exceptions **with full stack traces**

❌ **Don’t:**

* Catch `Exception` or `Throwable` unless at app boundaries
* Use exceptions for control flow
* Swallow exceptions silently
* Leak low-level exceptions (like `IOException`) into higher-level APIs

---

### 🔷 8. **Advanced: Functional Exception Handling (Optional)**

For functional code (like Streams, lambdas), checked exceptions can be awkward.

Solutions:

* Use utility wrappers like:

```java
@FunctionalInterface
public interface CheckedFunction<T, R> {
    R apply(T t) throws Exception;
}
```

* Or use libraries like [Vavr](https://www.vavr.io/) that support `Try`, `Either`, etc.

---