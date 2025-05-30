# Generics

## ✅ What are Generics?

- Think of generics as a way to make your code type-safe and reusable, like a reusable container that only accepts a certain type of item.
- **Pre-Generics Disaster (Runtime crash!):**
```java
List names = new ArrayList(); // old and unsafe
names.add("Alice");
names.add(123); // Oops, this will not be caught at compile time!
```
- **Solution: Generics add compile-time type safet:**
```java
List<String> names = new ArrayList<>();
names.add("Alice");
// names.add(123); // Compile-time error – safer!
```

## 🧱 Generic Classes and Methods

### 📌 Generic Class

- ✅ T is a type placeholder (like a variable for types)
```java
public class Box<T> {
    private T value;

    public void set(T value) { this.value = value; }
    public T get() { return value; }
}
```

```java
Box<String> box = new Box<>();
box.set("hello");
String val = box.get(); // No cast needed
```  

### 📌 Generic Method

- ✅ Notice <T> comes before the return type (void here). That declares this method as generic.
```java
public <T> void printArray(T[] array) {
    for (T item : array) {
        System.out.println(item);
    }
}
```

## 🌀 Wildcards: ?, ? extends, ? super:

- Use cases for wildcards:
| Form            | Meaning         | Use When                  |
| --------------- | --------------- | ------------------------- |
| `<?>`           | Unknown type    | You just want to **read** |
| `<? extends T>` | T or subclass   | You **read**, not write   |
| `<? super T>`   | T or superclass | You **write**, maybe read |


- 💡 Mnemonic: PECS(Producer Extends, Consumer Super)
	- If it produces values (you read), use extends.
	- If it consumes values (you write), use super. 
```java
List<? extends Number> numbers = List.of(1, 2, 3);
// numbers.add(5); ❌ Can’t add - read-only

List<? super Integer> nums = new ArrayList<>();
nums.add(10); ✅ Safe to add
```

### 🧰 Real-Life Analogy

- 🎁 Generic Box
	- Think of Box<Apple> as a crate labeled "Apple". You can only put apples in, and when you take something out, you know it’s an apple.
	- If we used Box<?>, it’s a crate with no label — you don’t know what’s inside, so you can only look (not put in).
```java
Box<Apple> appleBox = new Box<>();
```

## ⛓️ Type Bounds – Controlling What Types Are Allowed


- 🔼 Upper Bound (extends)
```java
// Upper Bound: "Only accept Numbers or their children"
public <T extends Number> double sum(T a, T b) {
    return a.doubleValue() + b.doubleValue(); 
}

// sum(5, 10) ✅ (Integer extends Number)
// sum(3.14, 2.71) ✅ (Double extends Number)
// sum("a", "b") ❌ Compile error!
```
- 🔽 Lower Bound (? super T)
```java
// Lower Bound: "Accept List of Integer or its PARENTS"
void addNumbers(List<? super Integer> list) {
    list.add(42);
}

// List<Number> ✅ (Number is Integer's parent)
// List<Object> ✅
// List<Double> ❌ (Double isn't Integer's parent)
```
- Unbounded Wildcards (?)
```java
void printAll(List<?> list) { // Accept ANY type
    for (Object item : list) System.out.println(item);
}
```

## ⚠️ Generics Restrictions (Golden Rules!)

- No Primitive Types:  
```java
List<int> ❌ → Use List<Integer> ✅
List<int> list = new ArrayList<>(); // ❌ Invalid
```
- Cannot Instantiate:  
```java
new T() ❌ (Type erasure removes T at runtime)
```
- Static Fields Can't Use Generics:
```java
private static T value; // ❌ Invalid

class Box<T> {
    static T item; ❌ // Illegal!
}
```
- Cannot throw exceptions of a type parameter 
```java
catch (T ex) { } // ❌ Not allowed
```
- No Arrays of Generic Types: 
```java
List<String>[] arr = new List<>[10]; ❌ 
```

- Memory Trick: **P**rimitives, **I**nstantiation, **S**tatics, **A**rrays → **PISA** Leaning Tower (they fall down!).
