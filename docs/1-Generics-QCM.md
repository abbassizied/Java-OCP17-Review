- Each question includes:
	- Code snippet
	- Multiple-choice options (A–D)
	- Only one correct answer
 
## ✅ Question 1: Upper Bounds in Generic Methods

- What will be the output of the following code? 
```java
import java.util.*;

public class Test {
    public static void main(String[] args) {
        List<Integer> list = Arrays.asList(10, 20, 30);
        printSum(list);
    }

    public static void printSum(List<? extends Number> list) {
        double sum = 0;
        for (Number n : list) {
            sum += n.doubleValue();
        }
        System.out.println("Sum = " + sum);
    }
}
```
- What is the result?
	- A. Sum = 60.0
	- B. Sum = 30.0
	- C. Compilation error
	- D. Runtime exception

## Question 2: Generic Type Restrictions

- What happens when you compile and run the following? 
```java
public class Holder<T> {
    private T value;

    public static void main(String[] args) {
        Holder<String> h = new Holder<>();
        h.print(); 
    }

    public void print() {
        // T obj = new T(); // Line A
        System.out.println("Printing...");
    }
}
```
- What happens if Line A is uncommented?
	- A. Compiles and runs fine
	- B. Compile-time error: cannot instantiate type T
	- C. Runtime error: ClassCastException
	- D. Compile-time error: generic array creation

## Question 3: Wildcard and PECS
  
```java
import java.util.*;

public class Demo {
    public static void addNumbers(List<? super Integer> list) {
        list.add(10);
        list.add(20);
    }

    public static void main(String[] args) {
        List<Number> nums = new ArrayList<>();
        addNumbers(nums);
        System.out.println(nums);
    }
}
```
- What is the output?
	- A. [10, 20]
	- B. []
	- C. Compilation error
	- D. Runtime exception

## Question 4: Generic Method Declaration

- Which of the following correctly declares a generic static method that accepts an array and returns the first element?
- **A:** 
```java
public static <T> T first(T[] array) { return array[0]; }
```
- **B:**   
```java
public <T> static T first(T[] array) { return array[0]; }
```
- **C:**   
```java
public T static <T> first(T[] array) { return array[0]; }
```
- **D:**   
```java
public static T first(T[] array) { return array[0]; }
```

## Question 5: Inheritance and Generics
 
```java
import java.util.*;

public class GenericsTest {
    public static void main(String[] args) {
        List<String> strings = new ArrayList<>();
        List<Object> objects = new ArrayList<>();
        copy(strings, objects);
    }

    public static <T> void copy(List<T> src, List<? super T> dest) {
        for (T t : src) {
            dest.add(t);
        }
    }
}
```
- What is the result?
	- A. Code compiles and runs
	- B. Compilation error on copy(strings, objects);
	- C. Compilation error inside copy() method
	- D. Runtime exception
	
# 🧠 Answers

| Question | Answer | Explanation                                |
| -------- | -------| ------------------------------------------ |
| 1        | C      | Double casting is safe via `doubleValue()` |
| 2        | B      | Cannot instantiate generic type directly   |
| 3        | A      | Lower bound allows `add()`                 |
| 4        | A      | Correct syntax for generic method          |
| 5        | A      | Correct use of `<? super T>`               |
