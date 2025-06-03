# Streams

---

## ## 🧠 **Lesson 1: Introduction to Java Streams – Foundations**

---

### 🔹 1. What Is a Stream?

A **Stream** is a sequence of elements that supports **functional-style operations** on collections. It's **not a data structure** but a **view** of a data source (usually a `Collection`, array, or I/O).

```java
List<String> names = List.of("Alice", "Bob", "Charlie");
Stream<String> stream = names.stream();
```

---

### 🔹 2. Core Features of Streams

| Feature                 | Description                                      |
| ----------------------- | ------------------------------------------------ |
| Declarative             | Focus on *what* to do, not *how*                 |
| Functional              | Use lambdas and higher-order functions           |
| Lazy                    | Execution is deferred until a terminal operation |
| Pipeline                | Chained transformations                          |
| Possibly Parallelizable | Easily parallelized with `.parallelStream()`     |

---

### 🔹 3. Stream Pipeline Structure

Every stream pipeline has three parts:

```
Source → Intermediate Operations → Terminal Operation
```

Example:

```java
List<String> result = names.stream()
    .filter(name -> name.startsWith("A"))
    .map(String::toUpperCase)
    .collect(Collectors.toList());
```

---

### 🔹 4. Stream Creation Methods

#### From Collections

```java
List<String> list = List.of("a", "b", "c");
Stream<String> stream = list.stream();
```

#### From Arrays

```java
Stream<Integer> numbers = Arrays.stream(new Integer[]{1, 2, 3});
```

#### From Static Methods

```java
Stream<String> s = Stream.of("x", "y", "z");
Stream<Integer> range = IntStream.range(1, 5); // 1, 2, 3, 4
```

---

### 🔹 5. Common Intermediate Operations

| Operation    | Description               |
| ------------ | ------------------------- |
| `filter()`   | Exclude elements          |
| `map()`      | Transform elements        |
| `flatMap()`  | Flatten nested structures |
| `distinct()` | Remove duplicates         |
| `sorted()`   | Sort elements             |
| `limit()`    | Limit result size         |
| `skip()`     | Skip elements             |

Example:

```java
List<String> upper = names.stream()
    .filter(n -> n.length() > 3)
    .map(String::toUpperCase)
    .toList();
```

---

### 🔹 6. Common Terminal Operations

| Operation     | Description                       |
| ------------- | --------------------------------- |
| `collect()`   | Reduce to a collection or summary |
| `forEach()`   | Perform an action                 |
| `count()`     | Count elements                    |
| `anyMatch()`  | Check if any match a predicate    |
| `allMatch()`  | Check if all match                |
| `noneMatch()` | Check if none match               |
| `reduce()`    | Combine elements                  |
| `findFirst()` | Get first element (if any)        |

---

### 🔹 7. Key Property: Streams Are Lazy

```java
Stream<String> s = Stream.of("one", "two", "three")
    .filter(e -> {
        System.out.println("filter: " + e);
        return true;
    }); // Nothing is printed yet!

s.forEach(System.out::println); // Now the pipeline runs
```

---

### 🔹 8. Streams Are One-Time Use

```java
Stream<String> s = Stream.of("a", "b", "c");
s.forEach(System.out::println);
s.forEach(System.out::println); // ❌ IllegalStateException
```

---

## 🧠 Lesson 2: **Deep Dive into Intermediate Stream Operations**

---

### 🔹 1. `map()` – Element Transformation

Transforms each element using a **mapping function**:

```java
List<String> words = List.of("java", "stream");

List<Integer> lengths = words.stream()
    .map(String::length)
    .toList(); // [4, 6]
```

* Always 1-to-1 mapping (input → output)
* Preserves stream size

---

### 🔹 2. `flatMap()` – Flattening Nested Structures

Used when the mapper function returns a `Stream<T>` instead of a `T`. Flattens nested streams.

#### Compare:

```java
Stream.of("a b", "c d")
    .map(s -> s.split(" "))           // Stream<String[]>
    .forEach(System.out::println);    // prints array references

Stream.of("a b", "c d")
    .flatMap(s -> Arrays.stream(s.split(" "))) // Stream<String>
    .forEach(System.out::println);             // a b c d
```

**Use Case**: Flattening a stream of collections

```java
List<List<String>> data = List.of(List.of("A", "B"), List.of("C"));
List<String> flat = data.stream()
    .flatMap(List::stream)
    .toList(); // [A, B, C]
```

---

### 🔹 3. `peek()` – For Debugging Only

Allows inspecting elements at any stage of the pipeline without modifying them.

```java
List<String> result = List.of("one", "two", "three").stream()
    .peek(s -> System.out.println("Before filter: " + s))
    .filter(s -> s.length() > 3)
    .peek(s -> System.out.println("After filter: " + s))
    .toList();
```

> 🧠 Never use `peek()` for business logic or side effects.

---

### 🔹 4. `sorted()` – Sorting Elements

#### Natural Order:

```java
List<String> sorted = List.of("banana", "apple", "pear").stream()
    .sorted()
    .toList(); // [apple, banana, pear]
```

#### Custom Comparator:

```java
List<String> sortedByLength = List.of("java", "streams", "are", "fun").stream()
    .sorted(Comparator.comparingInt(String::length).reversed())
    .toList(); // [streams, java, fun, are]
```

---

### 🔹 5. `filter()` – Conditional Inclusion

```java
List<String> filtered = List.of("java", "js", "python").stream()
    .filter(s -> s.length() > 3)
    .toList(); // [java, python]
```

You can combine multiple conditions:

```java
.filter(s -> s.startsWith("j") && s.length() > 2)
```

---

### 🔹 6. `distinct()` – Remove Duplicates

```java
Stream.of(1, 2, 2, 3, 3, 3)
    .distinct()
    .toList(); // [1, 2, 3]
```

Uses `equals()` and `hashCode()`

---

### 🔹 7. `limit()` and `skip()`

Control size of the result stream:

```java
Stream.of("A", "B", "C", "D")
    .limit(2)
    .toList(); // [A, B]

Stream.of("A", "B", "C", "D")
    .skip(2)
    .toList(); // [C, D]
```

Can be used for pagination.

---

## 🧠 Lesson 3: **Terminal Operations – Reduction, Collection, Matching, and More**

---

### 🔹 1. `collect()` – Gathering the Results

Most powerful and flexible terminal operation. Uses **Collectors** to produce lists, sets, maps, etc.

#### a. To List/Set

```java
List<String> list = Stream.of("a", "b", "c").collect(Collectors.toList());
Set<String> set = Stream.of("a", "b", "a").collect(Collectors.toSet());
```

#### b. Joining Strings

```java
String joined = Stream.of("a", "b", "c").collect(Collectors.joining(", ")); // "a, b, c"
```

#### c. To Map

```java
Map<String, Integer> map = Stream.of("apple", "banana")
    .collect(Collectors.toMap(
        s -> s,
        String::length
    ));
```

#### d. Grouping

```java
Map<Integer, List<String>> byLength = Stream.of("java", "kotlin", "go")
    .collect(Collectors.groupingBy(String::length));
```

---

### 🔹 2. `reduce()` – Combining Elements into One

Signature:

```java
Optional<T> reduce(BinaryOperator<T> accumulator)
T reduce(T identity, BinaryOperator<T> accumulator)
```

#### Example 1: Sum all numbers

```java
int sum = Stream.of(1, 2, 3, 4).reduce(0, Integer::sum);
```

#### Example 2: Concatenate strings

```java
String result = Stream.of("a", "b", "c").reduce("", String::concat);
```

---

### 🔹 3. `forEach()` – Performing Side Effects

```java
Stream.of("a", "b", "c").forEach(System.out::println);
```

**Caution**: This is **not parallel-safe**. For parallel streams, use `forEachOrdered()` for predictable order.

---

### 🔹 4. `count()` – Count Elements

```java
long count = Stream.of("a", "b", "c").count(); // 3
```

---

### 🔹 5. Matching Operations

All return boolean:

| Method        | Description                           |
| ------------- | ------------------------------------- |
| `anyMatch()`  | True if any element matches predicate |
| `allMatch()`  | True if all elements match predicate  |
| `noneMatch()` | True if no element matches predicate  |

Example:

```java
boolean hasEmpty = Stream.of("hi", "").anyMatch(String::isEmpty); // true
```

---

### 🔹 6. `findFirst()` vs `findAny()`

* `findFirst()` returns first element (ordered)
* `findAny()` returns any element (possibly faster for parallel streams)

```java
Optional<String> any = Stream.of("a", "b", "c").findAny();
Optional<String> first = Stream.of("a", "b", "c").findFirst();
```

---

### 🔹 7. Terminal Operations Are **Eager** and **Consume the Stream**

Once you run a terminal operation, the stream is **closed**.

```java
Stream<String> s = Stream.of("a", "b");
s.forEach(System.out::println);
// s.count(); // ❌ IllegalStateException
```

---

## 🧠 Lesson 4: **Primitive Streams – `IntStream`, `LongStream`, `DoubleStream`**

---

### 🔹 1. Why Use Primitive Streams?

Regular streams like `Stream<Integer>` involve **autoboxing**, which introduces memory and CPU overhead.

Instead, Java provides:

| Type     | Stream Class   |
| -------- | -------------- |
| `int`    | `IntStream`    |
| `long`   | `LongStream`   |
| `double` | `DoubleStream` |

These are optimized for **primitive operations**, support **ranges**, and offer **statistical methods**.

---

### 🔹 2. Creating Primitive Streams

#### a. From Ranges

```java
IntStream.range(1, 5)       // 1, 2, 3, 4
IntStream.rangeClosed(1, 5) // 1, 2, 3, 4, 5
```

#### b. From Arrays

```java
int[] nums = {1, 2, 3};
IntStream s = Arrays.stream(nums);
```

#### c. Using Static Methods

```java
IntStream.of(1, 2, 3)
LongStream.of(100L, 200L)
DoubleStream.of(3.14, 2.71)
```

---

### 🔹 3. Common Operations on Primitive Streams

#### a. `sum()`, `average()`, `min()`, `max()`

```java
int total = IntStream.rangeClosed(1, 5).sum();         // 15
OptionalDouble avg = IntStream.of(3, 6, 9).average();   // 6.0
OptionalInt min = IntStream.of(3, 6, 1).min();          // 1
```

#### b. `boxed()` – Converting to `Stream<T>`

```java
List<Integer> list = IntStream.range(1, 4)
    .boxed()
    .collect(Collectors.toList()); // [1, 2, 3]
```

#### c. `mapToObj()` – Primitive → Object

```java
Stream<String> names = IntStream.range(1, 4)
    .mapToObj(i -> "Item" + i); // "Item1", "Item2", "Item3"
```

---

### 🔹 4. `summaryStatistics()` – Quick Summary

```java
IntSummaryStatistics stats = IntStream.of(1, 2, 3, 4, 5)
    .summaryStatistics();

System.out.println(stats.getAverage()); // 3.0
System.out.println(stats.getMax());     // 5
System.out.println(stats.getMin());     // 1
System.out.println(stats.getSum());     // 15
```

Also available on `LongStream` and `DoubleStream`.

---

### 🔹 5. Infinite Primitive Streams

```java
IntStream.iterate(1, i -> i + 2)  // 1, 3, 5, ...
    .limit(5)
    .forEach(System.out::println);
```

---

## 🧠 Lesson 5: **Advanced Collectors in Java Streams**

---

### 🔹 1. `groupingBy()` – Classify and Aggregate

Groups stream elements by a **classifier function**, returning a `Map<K, List<T>>`.

#### Basic Grouping

```java
Map<Integer, List<String>> grouped = Stream.of("java", "go", "python", "c")
    .collect(Collectors.groupingBy(String::length));

// Result: {1=[c], 2=[go], 4=[java], 6=[python]}
```

#### Group and Count

```java
Map<Integer, Long> countByLength = Stream.of("hi", "hello", "hey")
    .collect(Collectors.groupingBy(String::length, Collectors.counting()));
```

#### Group and Map

```java
Map<Integer, List<Character>> byLength = Stream.of("hi", "hello", "hey")
    .collect(Collectors.groupingBy(
        String::length,
        Collectors.mapping(s -> s.charAt(0), Collectors.toList())
    ));
```

---

### 🔹 2. `partitioningBy()` – Boolean Classifier

Partitions stream into two groups based on a predicate: `true` and `false`.

```java
Map<Boolean, List<String>> partitioned = Stream.of("java", "go", "c++", "ruby")
    .collect(Collectors.partitioningBy(s -> s.length() > 3));

// true  → ["java", "ruby"]
// false → ["go", "c++"]
```

---

### 🔹 3. `toMap()` – Building a Map

```java
Map<String, Integer> wordLengths = Stream.of("java", "python")
    .collect(Collectors.toMap(
        s -> s,
        String::length
    ));
```

#### Handle Key Collisions:

```java
Map<Integer, String> firstLetters = Stream.of("cat", "cup", "dog")
    .collect(Collectors.toMap(
        String::length,
        s -> s,
        (s1, s2) -> s1 + "," + s2
    ));
```

---

### 🔹 4. `mapping()` and `flatMapping()` – Nested Collectors

Useful when collecting **inside** a `groupingBy()`.

```java
Map<Integer, Set<Character>> initials = Stream.of("hi", "hello", "hey")
    .collect(Collectors.groupingBy(
        String::length,
        Collectors.mapping(s -> s.charAt(0), Collectors.toSet())
    ));
```

Java 9+ supports `flatMapping()`:

```java
Map<Integer, Set<Character>> allCharsByLength = Stream.of("hi", "ho")
    .collect(Collectors.groupingBy(
        String::length,
        Collectors.flatMapping(
            s -> s.chars().mapToObj(c -> (char) c),
            Collectors.toSet()
        )
    ));
```

---

### 🔹 5. Immutable Collectors

Java 10+ introduced:

```java
Collectors.toUnmodifiableList()
Collectors.toUnmodifiableSet()
Collectors.toUnmodifiableMap()
```

```java
List<String> immutable = Stream.of("a", "b")
    .collect(Collectors.toUnmodifiableList());
```

Attempting to modify throws `UnsupportedOperationException`.

---

### 🔹 6. Custom Collector (Advanced)

You can define your own collector using:

```java
Collector.of(supplier, accumulator, combiner, finisher)
```

For example, a collector to concatenate uppercase strings:

```java
Collector<String, StringBuilder, String> upperConcat =
    Collector.of(
        StringBuilder::new,
        (sb, s) -> sb.append(s.toUpperCase()),
        StringBuilder::append,
        StringBuilder::toString
    );

String result = Stream.of("a", "b", "c").collect(upperConcat); // "ABC"
```

---

## 🧠 Lesson 6: **Parallel Streams in Java**

---

### 🚦 1. What Are Parallel Streams?

A **parallel stream** splits the data into multiple chunks and **processes them concurrently** using the **Fork/Join framework** under the hood.

```java
List<Integer> nums = List.of(1, 2, 3, 4, 5);

nums.parallelStream()
    .map(n -> n * n)
    .forEach(System.out::println);
```

Each operation may be run on a **different thread**, so the order is **not guaranteed**.

---

### 🛠 2. How to Create a Parallel Stream

You can make a stream parallel in 3 ways:

```java
list.parallelStream();                // From collection
stream.parallel();                   // Convert sequential stream
stream.sequential();                 // Convert back to sequential
```

---

### ⛓ 3. How It Works Internally

* Uses **ForkJoinPool.commonPool()**
* Default parallelism = **# of CPU cores**
* Recursive **divide-and-conquer** strategy

```java
System.out.println(ForkJoinPool.commonPool().getParallelism());
```

To customize the pool, you must **manually submit tasks** to a custom pool (advanced topic).

---

### ⚠️ 4. When **Not** to Use Parallel Streams

Avoid in these cases:

* Small data sets (parallel overhead is high)
* Stream operations with **side effects** (e.g., `forEach`)
* Stateful or synchronized operations
* Need for **predictable order** (use `forEachOrdered`)
* In **web apps** or **shared environments** where CPU is shared

---

### ✅ 5. When Parallel Streams Shine

Use when:

* Large datasets (10,000+ items)
* Pure functions (no side effects)
* CPU-bound operations
* Order doesn't matter

---

### 📊 6. Benchmark Example

```java
long start = System.nanoTime();

IntStream.range(1, 1_000_000)
    .parallel()
    .map(i -> i * i)
    .sum();

long time = System.nanoTime() - start;
System.out.println("Time: " + (time / 1_000_000) + " ms");
```

Compare `.stream()` vs `.parallelStream()` for performance impact.

---

## 🧠 Lesson 7: **Stream Best Practices, Gotchas, and Debugging**

This lesson focuses on **clean, efficient, and correct** use of streams. Even seasoned developers can run into trouble if these principles are overlooked.

---

### ✅ 1. **Streams Are One-Time Use**

Once a stream has been consumed, it **cannot be reused**.

```java
Stream<String> s = Stream.of("a", "b", "c");
s.forEach(System.out::println);
s.forEach(System.out::println); // ❌ IllegalStateException
```

✅ **Fix**: Use a supplier or regenerate the stream.

```java
Supplier<Stream<String>> supplier = () -> Stream.of("a", "b", "c");
```

---

### ⚠️ 2. **Avoid Side Effects**

Streams are designed for **functional-style programming**. Avoid modifying external or shared state.

```java
List<String> results = new ArrayList<>();

// ❌ Not recommended: shared mutable state
list.stream().forEach(results::add);

// ✅ Preferred: use collectors
List<String> results = list.stream().collect(Collectors.toList());
```

---

### 🧪 3. **Use `peek()` Only for Debugging**

```java
Stream.of("a", "b", "c")
    .peek(s -> System.out.println("Processing: " + s))
    .map(String::toUpperCase)
    .forEach(System.out::println);
```

`peek()` should never be used to **modify** state — only for debugging or tracing.

---

### 🔍 4. **Short-Circuiting with `limit()` and `anyMatch()`**

```java
list.stream()
    .filter(s -> s.startsWith("J"))
    .limit(5)              // stops after 5 matches
    .forEach(System.out::println);

boolean found = list.stream()
    .anyMatch(s -> s.length() > 10); // returns as soon as a match is found
```

These improve **performance** in large datasets.

---

### 🧱 5. **Flatten Nested Streams Safely**

Common pitfall: not using `flatMap()` when required.

```java
List<List<String>> nested = List.of(List.of("a", "b"), List.of("c"));

// ❌ Wrong: creates Stream<Stream<String>>
nested.stream().map(List::stream);

// ✅ Right
nested.stream().flatMap(List::stream).forEach(System.out::println);
```

---

### 🧹 6. **Don't Abuse Streams for Control Flow**

Streams are not replacements for traditional **looping or branching**.

```java
// ❌ Avoid
if (list.stream().anyMatch(x -> x == null)) {
    throw new IllegalArgumentException();
}

// ✅ Use Optional or traditional control logic when clarity matters
```

---

### 🔄 7. **Avoid Mixing Stream Pipelines and Loops**

```java
for (String name : names) {
    // ❌ Don't call stream inside loop
    if (otherList.stream().anyMatch(name::equals)) {
        ...
    }
}
```

✅ Instead, **convert to sets** or **use intermediate structures**.

---

### ✅ 8. Prefer `collect()` over `forEach() + add()`

```java
List<String> upper = new ArrayList<>();

// ❌ Inefficient and error-prone
list.stream().map(String::toUpperCase).forEach(upper::add);

// ✅ Better
List<String> upper = list.stream().map(String::toUpperCase).collect(Collectors.toList());
```

---

### 🧠 Summary: Stream Do’s and Don’ts

| ✅ Do                           | ❌ Don’t                    |
| ------------------------------ | -------------------------- |
| Use pure functions             | Modify external state      |
| Use collectors                 | Mix streams with loops     |
| Use flatMap for nested streams | Forget streams are one-use |
| Use peek only for debugging    | Use for side effects       |

---
