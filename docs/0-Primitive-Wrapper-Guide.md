# Java Primitive Types vs. Wrapper Classes: A Comprehensive Guide

## 🧠 1. Primitive Types in Java (The Foundation)
 
- Java has **8 primitive types**, which are **not objects**, directly hold their value in memory, and are **very efficient**.

| Type      | Size          | Default Value | Example Values        | Notes                           |
| --------- | ------------- | ------------- | --------------------- | ------------------------------- |
| `byte`    | 8-bit         | `0`           | `-128` to `127`       | Smallest integer                |
| `short`   | 16-bit        | `0`           | `-32,768` to `32,767` |                                 |
| `int`     | 32-bit        | `0`           | `-2^31` to `2^31-1`   | Most commonly used integer      |
| `long`    | 64-bit        | `0L`          | `-2^63` to `2^63-1`   | Suffix `L` is required          |
| `float`   | 32-bit        | `0.0f`        | \~7 decimal digits    | Suffix `f` is required          |
| `double`  | 64-bit        | `0.0d`        | \~15 decimal digits   | Default for decimals            |
| `char`    | 16-bit        | `\u0000`      | Unicode characters    | Enclosed in single quotes `'A'` |
| `boolean` | JVM dependent | `false`       | `true`, `false`       | No numerical representation     |

- When to Use Primitives?
	- ✔ Performance-critical applications (faster, no object overhead).
	- ✔ Storing large amounts of data (e.g., arrays in numerical computations).
	- ✔ When null is not needed (primitives cannot be null).
 
### 🔄 Conversions Between Primitive Types 

- Java supports two broad categories of primitive conversions: **widening** (implicit, safe) and **narrowing** (explicit, potentially lossy).

#### 1 Widening Conversions (Implicit)

- You can assign a smaller-range primitive to a larger-range primitive without an explicit cast.
- No data loss, since the target can represent all values of the source.

| From → To                                              | Example                                  |
| ------------------------------------------------------ | ---------------------------------------- |
| `byte` → `short` → `int` → `long` → `float` → `double` | `int i = 42; long L = i; double d = L;`  |
| `char` → `int` → `long` → `float` → `double`           | `char c = 'A'; int x = c; double y = x;` |
 
```java
byte b = 10;
int i = b;             // implicit, no cast needed
double d = i;           // implicit, no cast needed
char ch = 'Z';
int code = ch;          // 'Z' → 90
float f = ch;           // 'Z' → 90.0f
```
- **OCP Insight**: Widening char → int is allowed (because char is unsigned 0..65535 and fits in an int).

#### 2 Narrowing Conversions (Explicit)

- Converting a “larger” type to a “smaller” type (or from floating-point to integer) can lose information (rounding or overflow).
- Requires an explicit cast using parentheses.

| From → To                                                | Example                                       |
| -------------------------------------------------------- | --------------------------------------------- |
| `double` → `float` → `long` → `int` → `short` → `byte`   | `double d = 9.99; int i = (int) d;`           |
| `double` → `short` (direct) or `double → char` (if cast) | `char c = (char) 65.5; // c == 'A'`           |
| `long` → `int`, `int` → `short`, etc.                    | `int i = 200; byte b = (byte) i; // overflow` |
  
```java
double d = 9.99;
int i = (int) d;       // i == 9 (fraction truncated)

long L = 100_000L;
int x = (int) L;       // possible overflow if L > Integer.MAX_VALUE

int val = 130;
byte bb = (byte) val;  // bb == -126 (130 mod 256 = 130, then interpreted as signed)
```

#### ⚠️ Common Pitfall: Precision Loss & Overflow

- Floating → Integer
	- The fractional part is dropped (not rounded)
	- E.g., ```(int) 3.99 == 3, (int) -3.99 == -3```.
- Integer Overflow
	- If the original value is outside the target’s range, you get wraparound/truncation.
	- E.g., ```(byte) 130 == -126 because 130 − 256 = -126```. 
  
## 📦 2. Wrapper Classes (The Object Counterparts)
 
- **Primitive** types are **not objects**, so they **cannot** be used in:
	- Collections (e.g., List, Set)
	- Generics
	- Object-required contexts (e.g., reflection, method return types)
- So Java provides **Wrapper Classes** in the **java.lang** package:

| Primitive | Wrapper Class |
| --------- | ------------- |
| `byte`    | `Byte`        |
| `short`   | `Short`       |
| `int`     | `Integer`     |
| `long`    | `Long`        |
| `float`   | `Float`       |
| `double`  | `Double`      |
| `char`    | `Character`   |
| `boolean` | `Boolean`     |
 
- These are **immutable objects** that wrap the primitive values. 
- When to Use Wrapper Classes?
	- ✔ Collections (e.g., List<Integer>): Generics require objects, not primitives.
	- ✔ Nullable values: Wrappers can be null, primitives cannot.
	- ✔ Working with APIs (e.g., Hibernate, Jackson) that expect objects.
	- ✔ Reflection & Method calls (e.g., Integer.parseInt()).
	
### 🏷️ Primitive ↔ Wrapper Conversions (Autoboxing & Unboxing)

- Java provides automatic boxing (primitive → wrapper) and automatic unboxing (wrapper → primitive) since Java 5. However, this convenience can introduce subtle pitfalls.

#### 1 Autoboxing (Primitive → Wrapper)

- Implicit creation of a wrapper object from a primitive value.
- Internally calls methods like Integer.valueOf(int), which may cache small values (–128 to 127).
```java
int primitiveInt = 100;
Integer wrappedInt = primitiveInt;   // Autoboxing: Integer.valueOf(100)
Boolean wrappedBool = true;          // Autoboxing: Boolean.valueOf(true)
```

#### 2 Unboxing (Wrapper → Primitive)

- Implicit extraction of the primitive value from its wrapper.
- Equivalent to calling methods like wrappedInt.intValue().
```java
Integer wrapped = Integer.valueOf(42);
int prim = wrapped;     // Unboxing: wrapped.intValue()

Double dObj = Double.valueOf(3.14);
double dPrim = dObj;    // Unboxing: dObj.doubleValue()
```	 

#### ⚠️ Common Pitfall: NullPointerException on Unboxing

```java
Integer maybeNull = null;
int primitive = maybeNull; // Throws NullPointerException
```
- Always ensure wrapper references are not null before unboxing. 

### 📦 String ↔ Primitive/Wrapper Conversions

- In real-world applications you often need to convert between **String** and **numeric types**. The two most common directions:
	- **String → Primitive/Wrapper (Parsing)**
	- **Primitive/Wrapper → String (Formatting)**

#### 1 Parsing Strings to Primitives (and Wrappers)
 
- Use static methods in wrapper classes (e.g., Integer.parseInt(), Double.parseDouble(), Boolean.parseBoolean()). 
```java
String s1 = "123";
int i1 = Integer.parseInt(s1);                   // i1 == 123

String s2 = "3.14159";
double d1 = Double.parseDouble(s2);               // d1 == 3.14159

String boolStr = "true";
boolean flag = Boolean.parseBoolean(boolStr);      // flag == true
```
- NumberFormatException
	- Thrown if the string is not a valid representation of the number.
	- E.g., ```Integer.parseInt("12A") → NumberFormatException```.
- NullPointerException on Passing null
	- E.g., ```Integer.parseInt(null) → NullPointerException```.
- 🔑 Best Practice: Pre-Validate or Catch Exceptions 
```java
try {
    int safe = Integer.parseInt(userInput);
} catch (NumberFormatException e) {
    // Handle invalid input gracefully
}
```

#### 2 Formatting Primitives/Wrappers to Strings

- Concatenation 
```java
int x = 42;
String s = "" + x; // "42"
```
- String.valueOf(...)
```java
double pi = 3.14;
String s2 = String.valueOf(pi);   // "3.14"
```
- Wrapper’s toString() 
```java
Integer w = Integer.valueOf(7);
String s3 = w.toString();       // "7"
```

## 🧰 3. When to Use What?

| Situation                                                 | Use Primitive | Use Wrapper |
| --------------------------------------------------------- | ------------- | ----------- |
| Arithmetic, performance-sensitive code                    | ✅            | ❌          |
| Collections (`List<Integer>`)                             | ❌            | ✅          |
| Reflection / annotations / frameworks (Spring, Hibernate) | ❌            | ✅          |
| Generic method parameters                                 | ❌            | ✅          |
| You need `null` (e.g., not-yet-set state)                 | ❌            | ✅          |

- 🔍 OCP Tip: Java **autoboxes (primitive → wrapper)** and **unboxes (wrapper → primitive)** automatically: 
```java
int a = 5;
Integer obj = a; // autoboxing
int b = obj;     // unboxing
```

## ⚠️ 4. Common Mistakes and Gotchas

### Mistake 1: ❌ Comparing Wrapper Objects with ==
 
```java
Integer a = 127;
Integer b = 127;
System.out.println(a == b); // true (cached)

Integer c = 128;
Integer d = 128;
System.out.println(c == d); // false (outside cache range)
```
- ✅ Fix: Always use **.equals()** to compare wrappers for value equality.

### Mistake 2: ⚠️ NullPointerException on Unboxing
 
```java
Integer x = null;
int y = x; // ❌ Throws NullPointerException
``` 
- ✅ Fix: Check for null before unboxing.

### Mistake 3: ❗ Precision Loss
 
```java
float f = 1.123456789f;
System.out.println(f); // 1.1234568 (rounded)
```
- ✅ Always choose double unless you explicitly need lower precision.

### Mistake 4: Memory Overhead with Wrappers
   
```java
List<Integer> numbers = new ArrayList<>(); // Each Integer is an object (~16-24 bytes)  
```
- ✅ Fix: For large datasets, consider int[] instead.

## 📚 5. Best Practices (Academic + OCP Advice)

- Use primitives by default for performance.
- Use wrappers when necessary (e.g., collections, nullability).
- Use Integer.valueOf(String) instead of new Integer(String) (deprecated).
- Avoid == on wrappers — use .equals() unless identity is what you’re checking.
- Watch for NullPointerException when unboxing wrappers.
