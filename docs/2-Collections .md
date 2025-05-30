# Collections
 
## 🎯 GOAL: Master Java Collections

- By the end of this, you will:
	- Understand the main Collection interfaces and their relationships.
	- Know how to use bounds with collections (?, ? extends, ? super).
	- Recognize the most used methods and their behavior.
	- Master iteration, sorting, and searching techniques.
	- Know how to compare different collection types.

## 🏗️ Main Interfaces in the Collections Framework

| Interface       | Description                     | Examples                              |
| --------------- | ------------------------------- | ------------------------------------- |
| `Collection<E>` | Root of everything except maps  | `List`, `Set`, `Queue`                |
| `List<E>`       | Ordered, can contain duplicates | `ArrayList`, `LinkedList`             |
| `Set<E>`        | No duplicates                   | `HashSet`, `TreeSet`, `LinkedHashSet` |
| `Queue<E>`      | For FIFO or LIFO processing     | `LinkedList`, `PriorityQueue`         |
| `Map<K, V>`     | Key-value pairs                 | `HashMap`, `TreeMap`, `LinkedHashMap` |

- "List = Ordered, Set = Unique, Map = Key-Value"
- **The Java Collections Framework (JCF) — Big Picture**
```
              Iterable
                 |
             Collection
          /        |       \
     List        Set       Queue
      |            |          \
 ArrayList    HashSet      PriorityQueue
 LinkedList   TreeSet      ArrayDeque
 ```
- **Map** is **not a Collection** but part of the framework. 
- **Iterable**: Defines **forEach** and allows **for-each** loop.
- **Collection**: **Root interface** for **List**, **Set**, and **Queue**.

## Main Interfaces: Features and Use Cases

### ✅ List (Ordered, allows duplicates)

- Common Classes:
	- **ArrayList**: Fast reads, slow inserts/removals in middle.
	- **LinkedList**: Fast inserts/removals, slower reads.
- 📌 Key Methods:
```
add(E e),
add(int index, E e)
get(int index)
set(int index, E e)
remove(int index)
indexOf(E e)
subList(from, to)
contains(E e)
```

### ✅ Set (No duplicates)

- Unordered or sorted depending on implementation.
- Common Classes:
	- **HashSet**: Fast, no ordering.
	- **LinkedHashSet**: Preserves insertion order.
	- **TreeSet**: Sorted based on natural/comparator order.
- 📌 Key Methods: 
```
add(E e)
contains(E e)
remove(E e)
first()
last() // TreeSet
```

### ✅ Queue / Deque (FIFO or LIFO)

- Think of real-world queues (like lines or stacks).
- Common Classes:
	- **PriorityQueue**: Automatically sorts elements by priority.
	- **ArrayDeque**: Double-ended queue (efficient stack/queue).
- 📌 Key Methods: 
``` 
offer(E e)
poll()
peek()
push()
pop() // Deque
```
 
## Iteration: How to Traverse a Collection

- **3 Ways to Iterate** 
```java
// 1. Enhanced For Loop
for (String s : list) { System.out.println(s); }

// 2. Iterator
Iterator<String> it = list.iterator();
while (it.hasNext()) { System.out.println(it.next()); }

// 3. forEach with Lambda
list.forEach(s -> System.out.println(s));
```
- 🔐 Fail-fast behavior: Modifying a collection during iteration using non-iterator methods causes **ConcurrentModificationException**.

## Sorting and Searching

- **Sorting:**
```java
List<String> list = Arrays.asList("banana", "apple", "pear");
Collections.sort(list); // natural order
list.sort(Comparator.reverseOrder()); // reverse
```
- **Searching:**
```java
Collections.binarySearch(list, "apple"); // list MUST be sorted
```

## 🧠 Comparing Collection Types

| Collection Type | Allows Duplicates | Ordered? | Sorted? | Access Time | Use Case |
|------------------|-------------------|----------|---------|--------------|-----------|
| `ArrayList`      | ✅ Yes             | ✅ Yes    | ❌ No    | O(1)         | Fast access |
| `LinkedList`     | ✅ Yes             | ✅ Yes    | ❌ No    | O(n)         | Frequent inserts/removes |
| `HashSet`        | ❌ No              | ❌ No    | ❌ No    | O(1) average | Unique elements |
| `TreeSet`        | ❌ No              | ❌ No    | ✅ Yes (natural order) | O(log n) | Sorted unique elements |
| `HashMap`        | Keys: ❌ Values: ✅ | ❌ No    | ❌ No    | O(1) average | Fast key lookup |
| `TreeMap`        | Keys: ❌ Values: ✅ | ❌ No    | ✅ Yes (by key) | O(log n) | Sorted map |

## Recap

| Concept            | Key Takeaway                                                |
| ------------------ | ----------------------------------------------------------- |
| Interfaces         | `List`, `Set`, `Queue` — each with unique behaviors         |
| Wildcards          | Use PECS: Producer = extends, Consumer = super              |
| Iteration          | 3 ways: for-each, `Iterator`, `forEach()`                   |
| Common operations  | `add`, `remove`, `get`, `contains`, `sort`, `binarySearch`  |
| Collection classes | Know when to use `ArrayList`, `LinkedList`, `HashSet`, etc. |

- **Generics** = **Type safety** + **Reusability**.
- Type erasure = Java removes type info at runtime → no new T()!
- Sorting/Searching = Only work on ordered collections!

