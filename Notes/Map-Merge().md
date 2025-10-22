# `V Map.merge(K key, V value, BiFunction<V, V, V> remappingFunction)` method

* the `Map.merge(K key, V value, BiFunction<V, V, V> remappingFunction)` method is a **Java 8 feature** that merges a new value into the map.

It works like this:

* If the key **does not exist**, it simply **inserts** the key-value pair.
* If the key **exists**, it **applies the given function** to the existing and new values, and the result replaces the old value.
* If the function returns `null`, the key is **removed** from the map.

Here’s a **clear, working example** using your `strMap`:

```java
package ch2_collections;

import java.util.*;

public class MapMergeExample {

    public static void main(String[] args) {

        Map<Integer, String> strMap = new TreeMap<>();

        strMap.put(0, "a");
        strMap.put(1, "b");
        strMap.put(2, "c");
        strMap.put(3, "d");
        strMap.put(4, "e");

        System.out.println("Before merge: " + strMap);

        // Example 1: Key exists -> merge combines old and new values
        strMap.merge(2, "X", (oldVal, newVal) -> oldVal + newVal);
        // This will replace value at key 2 ("c") with "cX"

        // Example 2: Key does not exist -> new key/value added
        strMap.merge(5, "f", (oldVal, newVal) -> oldVal + newVal);
        // Since key 5 doesn't exist, it just adds 5="f"

        // Example 3: Using a function that removes an entry if result is null
        strMap.merge(1, "REMOVE", (oldVal, newVal) -> null);
        // This removes key 1 from the map

        System.out.println("After merge: " + strMap);
    }
}
```

### 💡 Output:

```
Before merge: {0=a, 1=b, 2=c, 3=d, 4=e}
After merge: {0=a, 2=cX, 3=d, 4=e, 5=f}
```

### 🧠 Summary of how `merge()` works:

| Case                 | Condition                                                 | Behavior |
| -------------------- | --------------------------------------------------------- | -------- |
| Key doesn’t exist    | Inserts `(key, value)`                                    |          |
| Key exists           | Replaces old value with result of `f(oldValue, newValue)` |          |
| `f()` returns `null` | Removes the key from map                                  |          |

