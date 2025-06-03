# Functional Programming (FP) in Java

---

## 🧠 Lesson 1: Foundations of Functional Programming in Java

- **Java's Path to FP:** Java is an object-oriented language, but since Java 8, it's been evolving to support functional constructs:

| Feature               | Version | Description                          |
| --------------------- | ------- | ------------------------------------ |
| Lambda expressions    | 8       | Anonymous functions                  |
| Functional interfaces | 8       | Single abstract method interfaces    |
| Streams API           | 8       | Declarative collection processing    |
| Method references     | 8       | Compact lambda syntax                |
| Optional<T>           | 8       | Functional null handling             |
| var keyword           | 10      | Type inference (useful in FP)        |
| Pattern matching      | 14+     | Cleaner conditions and destructuring |

### 🔸 Functional Interfaces

- A **functional interface** is **an interface with a single abstract method (SAM)**.
- 🧪 Example: Custom Functional Interface:
```java
@FunctionalInterface
interface MyFunction<T, R> {
    R apply(T t);
}
``` 
- Built-in functional interfaces in java.util.function:

| Interface          | Signature           | Example Usage                   |
| ------------------ | ------------------- | ------------------------------- |
| `Function<T, R>`   | `R apply(T t)`      | Mapping types                   |
| `Predicate<T>`     | `boolean test(T t)` | Filtering                       |
| `Consumer<T>`      | `void accept(T t)`  | Performing side effects         |
| `Supplier<T>`      | `T get()`           | Lazily producing values         |
| `UnaryOperator<T>` | `T apply(T t)`      | Transformation of the same type |

- 🧪 Usage:
```java
Function<String, Integer> lengthFunc = s -> s.length();
System.out.println(lengthFunc.apply("Java")); // 4
```

### 🔸 Lambda Expressions

- A **lambda expression** is a **shorthand** for **implementing a functional interface**.
- Use them anywhere a functional interface is expected:
```java
(String s) -> s.length()         // With parameter type
s -> s.length()                  // Type inference
() -> 42                         // No parameters
x -> { return x * 2; }           // Block with return
```
 
### Method References

- A **method reference** is a **shorthand** for **lambdas that call a single method**. 
```java
String::toLowerCase        // Equivalent to s -> s.toLowerCase()
System.out::println        // Equivalent to x -> System.out.println(x)
Integer::parseInt          // Equivalent to s -> Integer.parseInt(s)
```

---
 
## 🧠 Lesson 2: Streams API Deep Dive — Functional Data Processing in Java 

- A **Stream** is a sequence of elements supporting **sequential and parallel** aggregate operations.

### 🔸 Creating Streams

#### 🧪 From a Collection 
 
```java
List<String> list = List.of("Java", "Python", "Kotlin");
Stream<String> stream = list.stream();
```

#### 🧪 From values or arrays 
 
```java
Stream<String> s1 = Stream.of("A", "B", "C");
IntStream intStream = IntStream.of(1, 2, 3);
```

#### 🧪 Infinite Streams (careful!) 

- Use **.limit(n)** to bound infinite streams.
```java
Stream<Double> randoms = Stream.generate(Math::random);
Stream<Integer> countUp = Stream.iterate(0, n -> n + 1);
```

### 🔸 Stream Operations 
 
| Type         | Operation Examples                                     |
| ------------ | ------------------------------------------------------ |
| Intermediate | `filter`, `map`, `distinct`, `sorted`, `limit`, `peek` |
| Terminal     | `forEach`, `collect`, `reduce`, `count`, `anyMatch`    |

- Operations are **lazy**: nothing executes until **a terminal operation** is called. 

### 🔸 Functional Pipeline Example 
 
```java
List<String> words = List.of("Java", "Python", "JavaScript", "Ruby");

int total = words.stream()
	// Predicate (keeps elements that match)
    .filter(w -> w.startsWith("J"))      // Keep: "Java", "JavaScript"
	// Function (transforms each element)
    .map(String::length)                 // → [4, 10]
	// Combines elements into a single result
    .reduce(0, Integer::sum);            // 4 + 10 = 14

System.out.println(total);              // Output: 14
```
### 🔸 Stream Laziness

- Intermediate ops like map, filter are **lazy**. They're only evaluated when a terminal op triggers them.
```java
List<String> names = List.of("Alice", "Bob", "Charlie");

names.stream()
     .filter(s -> {
         System.out.println("Filtering: " + s);
         return s.length() > 3;
     })
     .map(s -> {
         System.out.println("Mapping: " + s);
         return s.toUpperCase();
     })
     .findFirst();  // Only processes until first match is found
```
- Only one element is processed! 

### 🔸 Collecting Results
 
- Use **Collectors** to gather results: 
```java
List<String> filtered = names.stream()
    .filter(n -> n.startsWith("A"))
    .collect(Collectors.toList());
```
- More **Collectors**:
	- **toList()**, **toSet()**, **toMap()** 
	- **joining()**, **groupingBy()**, **partitioningBy()**, **summarizingInt()**
 
### 🔬 Advanced: Custom Collector (Preview)

- You can even define your own collector: 
```java
Collector<String, StringBuilder, String> customCollector =
    Collector.of(
        StringBuilder::new,
        StringBuilder::append,
        StringBuilder::append,
        StringBuilder::toString
    );

String result = Stream.of("J", "a", "v", "a")
                      .collect(customCollector); // → "Java"
```

---

## 🧠 Lesson 3: Functional Transformations – map() vs flatMap(), Nested Structures, Optionals, and Primitives

### 🔹 map() vs flatMap()

- ```🔸 map()``` is **1-to-1 transformation**. Each element becomes exactly one new element:
```java
Stream<String> names = Stream.of("Java", "Python");
Stream<Integer> lengths = names.map(String::length); // Stream<Integer>
```
- ```🔸 flatMap()``` is **1-to-many flattening**. When each element maps to a stream or collection, flatMap() flattens them.: 
```java
List<String> phrases = List.of("Java is cool", "Streams are powerful");

List<String> words = phrases.stream()
    .flatMap(phrase -> Arrays.stream(phrase.split(" "))) // Stream<Stream<String>> → Stream<String>
    .toList();

// Output: [Java, is, cool, Streams, are, powerful]
```
- Think of:
	- ```map()``` → ```Stream<Stream<T>>```
	- ```flatMap()``` → ```Stream<T>```

### 🔹 Optional<T> with flatMap()

- **Functional null-safety!**
- **map()** vs **flatMap()** on Optional: 
```java
Optional<String> name = Optional.of("Java");

// map() returns Optional<Optional<Integer>>
Optional<Optional<Integer>> lengthWrapped = name.map(s -> Optional.of(s.length()));

// flatMap() flattens the nested Optional
Optional<Integer> length = name.flatMap(s -> Optional.of(s.length()));
```

### 🔹 Flattening Nested Collections 

```java
List<List<Integer>> matrix = List.of(
    List.of(1, 2),
    List.of(3, 4),
    List.of(5, 6)
);

List<Integer> flat = matrix.stream()
    .flatMap(List::stream)
    .toList(); // [1, 2, 3, 4, 5, 6]
```

### 🔹 Primitive Streams 

- Java offers primitive specializations for performance:

| Type           | Description  |
| -------------- | ------------ |
| `IntStream`    | For `int`    |
| `LongStream`   | For `long`   |
| `DoubleStream` | For `double` |
 
- Avoids boxing/unboxing. 
```java
int sum = IntStream.range(1, 5) // [1, 2, 3, 4]
                   .map(i -> i * i)
                   .sum(); // 1² + 2² + 3² + 4² = 30
```
- To go back to a boxed stream:
```java
IntStream.range(1, 5)
         .boxed()
         .collect(Collectors.toList());
```

### 🔸 Bonus: flatMapToInt(), mapToObj()  

- Useful for bridging between stream types:
```java
List<String> lines = List.of("abc", "de");

IntStream charCodes = lines.stream()
    .flatMapToInt(str -> str.chars()); // chars() → IntStream

charCodes.forEach(System.out::println); // ASCII codes
```

---

## 🧠 Lesson 4: Declarative Data Aggregation — Collectors, Grouping, Partitioning, and Custom Reduction

### 🔹 collect() Terminal Operation

- The **collect()** method is used to:
	- Gather elements into containers (lists, maps, sets, strings)
	- Perform reductions with aggregation logic
- It works with **Collectors** from **java.util.stream.Collectors**.

### 🔹 Common Built-in Collectors 

| Collector             | Purpose                            |
| --------------------- | ---------------------------------- |
| `toList()`, `toSet()` | Collect into `List`, `Set`         |
| `toMap()`             | Collect into `Map<K, V>`           |
| `joining(delimiter)`  | Concatenate strings                |
| `counting()`          | Count elements                     |
| `summarizingInt()`    | Summary statistics for numbers     |
| `groupingBy()`        | Group by classifier function       |
| `partitioningBy()`    | Group into two groups by predicate |
 
### 🔹 Aggregation Examples 

- 📦 ```toList()```, ```toSet()```, ```joining()```
```java
List<String> names = List.of("Alice", "Bob", "Charlie");

String result = names.stream()
    .map(String::toUpperCase)
    .collect(Collectors.joining(", "));  // "ALICE, BOB, CHARLIE"
```

### 🔹 Grouping with groupingBy() 

- 🧪 Example: Grouping Strings by Length 
```java
List<String> names = List.of("Anna", "Bob", "Clara", "David");

Map<Integer, List<String>> byLength = names.stream()
    .collect(Collectors.groupingBy(String::length));

System.out.println(byLength);
// Output: {3=[Bob], 4=[Anna], 5=[Clara, David]}
```

### 🔹 Partitioning with partitioningBy() 

- Divides into two groups based on a boolean predicate.
```java
Map<Boolean, List<String>> partitioned = names.stream()
    .collect(Collectors.partitioningBy(name -> name.length() > 3));
```

### 🔹 Downstream Collectors 

- You can combine collectors for nested aggregations: 🧪 Count how many names per length:
```java
Map<Integer, Long> countByLength = names.stream()
    .collect(Collectors.groupingBy(
        String::length,
        Collectors.counting()
    ));
```

### 🔹 Summary Statistics 

- For numeric streams:
```java
IntSummaryStatistics stats = names.stream()
    .mapToInt(String::length)
    .summaryStatistics();

System.out.println(stats.getAverage());  // Mean length
System.out.println(stats.getMax());      // Max length
System.out.println(stats.getSum());      // Total characters
```

### 🔹 Custom Collectors with Collector.of() 

- Build your own: 
```java
Collector<String, StringBuilder, String> reverseConcat = Collector.of(
    StringBuilder::new,
    (sb, s) -> sb.insert(0, s),    // Reversed append
    StringBuilder::append,
    StringBuilder::toString
);

String result = Stream.of("a", "b", "c").collect(reverseConcat);  // "cba"
```

---

## 🧠 Lesson 5: Advanced Functional Patterns in Java Streams

### 🔹 peek() — Debugging Inside Pipelines 

- Use peek() to inspect elements mid-stream. It’s like map(), but for side effects.
```java
Stream.of("Java", "Python", "Kotlin")
    .filter(s -> s.length() > 4)
    .peek(s -> System.out.println("Filtered: " + s))
    .map(String::toUpperCase)
    .peek(s -> System.out.println("Mapped: " + s))
    .toList();
```
- ✅ Great for debugging. ❌ Not for mutation in production logic.

### 🔹 Composing Predicate, Function, and Comparator 

- You can compose functional interfaces using default methods:
- 🧪 Composing Predicates
```java
Predicate<String> startsWithA = s -> s.startsWith("A");
Predicate<String> endsWithZ = s -> s.endsWith("Z");

Predicate<String> complex = startsWithA.and(endsWithZ);

System.out.println(complex.test("AMAZ")); // true
```  
- Other methods: ```and()```, ```or()```, ```negate()```

- 🧪 Composing Functions
```java
Function<String, String> trim = String::trim;
Function<String, String> toUpper = String::toUpperCase;

Function<String, String> pipeline = trim.andThen(toUpper);

System.out.println(pipeline.apply("  java ")); // "JAVA"
```
- 🧪 Composing Comparators
```java
List<String> langs = List.of("Java", "Python", "Go", "C");

langs.stream()
    .sorted(Comparator.comparingInt(String::length)
        .thenComparing(Comparator.naturalOrder()))
    .forEach(System.out::println);
```

### 🔹 Custom Sorting Strategies  

- You can write expressive custom sorts using lambda comparators. 
```java
List<String> names = List.of("Anna", "Alex", "Bob", "Alice");

names.stream()
    .sorted((a, b) -> {
        int cmp = Integer.compare(a.length(), b.length());
        return cmp != 0 ? cmp : a.compareTo(b);
    })
    .forEach(System.out::println);
```

### 🔹 Parallel Streams  

- Streams can be parallelized for concurrency: 
```java
List<String> list = List.of("a", "b", "c", "d", "e");

list.parallelStream()
    .map(s -> s.toUpperCase())
    .forEach(System.out::println);
```
- Use parallelStream() or stream().parallel()
- Be cautious with:
	- **Shared mutable state**
	- **Order-sensitive operations**
	- **IO or thread-unsafe logic**
 
### 🔹 Functional Design Patterns in Java 

- 1. Pipeline Pattern (Fluent interface via chained functions)
```java
Function<String, String> processor = 
    String::trim
    .andThen(String::toLowerCase)
    .andThen(s -> s.replace(" ", "_"));

String result = processor.apply("  Hello World  "); // "hello_world"
```
- 2. Command Pattern with lambdas 
```java
Map<String, Runnable> commands = Map.of(
    "start", () -> System.out.println("Starting..."),
    "stop",  () -> System.out.println("Stopping...")
);

commands.getOrDefault("start", () -> {}).run();
```
- 3. Filter-Map-Reduce idiom
```java
List<String> langs = List.of("Java", "C#", "JavaScript");

int totalJLength = langs.stream()
    .filter(s -> s.startsWith("J"))
    .mapToInt(String::length)
    .sum();
```
 
---

## 🧠 Lesson 6: Mastering Optional and Functional Error Handling

- An ```Optional<T>``` is a container object that may or may not hold a non-null value.
```java
Optional<String> maybeName = Optional.of("Alice");
Optional<String> empty = Optional.empty();
```
-  Why Use Optional?
	- ✅ Avoid NullPointerException
	- ✅ Replace null-checking boilerplate
	- ✅ Chain fallback logic functionally
	- ✅ Improve API clarity (explicit return types) 
 
### 🔹 Creating Optionals 

```java
Optional<String> opt1 = Optional.of("Hi");      // Must be non-null
Optional<String> opt2 = Optional.ofNullable(null);  // Safe with null
Optional<String> opt3 = Optional.empty();       // Empty container
```

### 🔹 Working with Optionals  
 
- 🔹 isPresent() / isEmpty()
```java
if (opt1.isPresent()) {
    System.out.println(opt1.get()); // use get() only when present
}
```
- ⚠️ Avoid get() unless you’re sure. Use safer methods below.

- 🔹 ifPresent() / ifPresentOrElse() 
```java
opt1.ifPresent(System.out::println); // print if exists

opt2.ifPresentOrElse(
    v -> System.out.println("Value: " + v),
    () -> System.out.println("Empty")
);
```
- 🔹 map() and flatMap()  
```java
Optional<String> upper = Optional.of("java")
    .map(String::toUpperCase); // Optional[JAVA]
```
- Use ```flatMap()``` if the mapper returns an ```Optional<T>```
```java
Optional<String> getTitle(User user) {
    return Optional.ofNullable(user.getProfile())
                   .flatMap(Profile::getTitle); // avoids nested optionals
}
```
- 🔹 orElse, orElseGet, orElseThrow 
```java
String result = Optional.ofNullable(null)
    .orElse("default");

String result2 = Optional.ofNullable(null)
    .orElseGet(() -> computeExpensiveDefault());

String result3 = Optional.ofNullable(null)
    .orElseThrow(() -> new IllegalArgumentException("Missing!"));
```
 
### 🔹 Optional in Stream Pipelines  

- Filter out nulls safely:
```java
Stream.of("Java", null, "Kotlin")
    .filter(Objects::nonNull)
    .map(String::toUpperCase)
    .forEach(System.out::println);
```
- OR use flatMap with Optionals: 
```java
Stream.of("Java", null, "Go")
    .map(Optional::ofNullable)
    .flatMap(Optional::stream)
    .map(String::toUpperCase)
    .forEach(System.out::println);
```

### 🔹 Functional Error Wrapping Pattern  

- Use Optional<T> as a poor man's Try-catch: 
```java
Optional<String> safeDivide(int a, int b) {
    return b == 0 ? Optional.empty() : Optional.of(String.valueOf(a / b));
}
```

---

## 🧠 Lesson 7: Custom Functional Interfaces, Higher-Order Functions, and Currying 

### 🔹 Why Create Your Own Functional Interfaces? 

- Java has many built-ins (Function, Predicate, Supplier, etc.), but sometimes:
	- You need custom parameter combinations
	- You want stronger type names for readability
	- You’re working with domain-specific logic
 
### 🔹 Defining a Custom Functional Interface  
  
```java
@FunctionalInterface
interface Transformer<T, R> {
    R apply(T input);
}

// Usage:
Transformer<String, Integer> length = String::length;
System.out.println(length.apply("Hello")); // 5
```
- ✔ A single abstract method
- ✔ Optional: add default or static methods
 
### 🔹 Higher-Order Functions in Java 

- A higher-order function is a function that:
	- Accepts other functions as arguments
	- Or returns a function as a result
- ✅ Accepting a function 
```java
static <T> void repeat(int times, Consumer<T> action, T value) {
    for (int i = 0; i < times; i++) action.accept(value);
}

// Usage:
repeat(3, System.out::println, "Hi!");
```
- ✅ Returning a function (Function Factory) 
```java
static Function<Integer, Integer> multiplier(int factor) {
    return x -> x * factor;
}

Function<Integer, Integer> triple = multiplier(3);
System.out.println(triple.apply(10)); // 30
```

### 🔹 Currying in Java 

- **Currying**: Converting a function with multiple arguments into a chain of functions each taking one argument.
```java
BiFunction<Integer, Integer, Integer> add = Integer::sum;

// Curried version:
Function<Integer, Function<Integer, Integer>> curriedAdd =
    a -> b -> a + b;

Function<Integer, Integer> add5 = curriedAdd.apply(5);
System.out.println(add5.apply(10)); // 15
```

### 🔹 Partial Application (Closely Related to Currying)  

- Lock in some arguments, leave others open:
```java
static <A, B, R> Function<B, R> partial(BiFunction<A, B, R> biFn, A fixedA) {
    return b -> biFn.apply(fixedA, b);
}

BiFunction<Integer, Integer, Integer> multiply = (a, b) -> a * b;

Function<Integer, Integer> doubleIt = partial(multiply, 2);

System.out.println(doubleIt.apply(8)); // 16
```

### 🔹 Real-World Example: Validator DSL  

- 
```java
@FunctionalInterface
interface Validator<T> {
    boolean validate(T input);

    default Validator<T> and(Validator<T> other) {
        return t -> this.validate(t) && other.validate(t);
    }
}

// Use it like this:
Validator<String> notEmpty = s -> !s.isEmpty();
Validator<String> hasUppercase = s -> s.chars().anyMatch(Character::isUpperCase);

Validator<String> passwordValidator = notEmpty.and(hasUppercase);
```

### 🔹 Bonus (Java 21+): Sealed Interfaces for ADTs 

- Use sealed types to model Either, Result, Try, etc. 
```java
sealed interface Result<T> permits Success, Failure {}

record Success<T>(T value) implements Result<T> {}
record Failure<T>(String error) implements Result<T> {}

// Then write: 
Result<String> output = divide(10, 2); // Success or Failure
```

---
