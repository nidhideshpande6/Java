# Java Collections: Detailed Explanation with Examples

## Overview of Collections Framework

The Java Collections Framework provides a set of interfaces and classes to handle groups of objects. It includes various data structures such as `List`, `Set`, and `Map` that allow efficient data manipulation.

### Key Differences Between List and Set

| Feature                  | List                         | Set                          |
|--------------------------|------------------------------|------------------------------|
| Allows Duplicates        | Yes                          | No                           |
| Index-Based Access       | Yes                          | No                           |
| Underlying Mechanism     | Array or Linked List         | Hashing or Tree structure    |
| Frequent Access          | Better for frequent access   | Not optimized for frequent access |

---

## List

A `List` is an ordered collection that allows duplicate elements and provides index-based access.

### Implementations of List

#### ArrayList
- Backed by a dynamic array.
- Fast for storing and accessing data.
- Slower for insertion and deletion due to memory shifting.

#### LinkedList
- Backed by a doubly linked list (DLL).
- Better for manipulation (insertion and deletion).
- Slower for random access.

### Comparison: ArrayList vs LinkedList

| Feature                     | ArrayList                        | LinkedList                      |
|-----------------------------|-----------------------------------|---------------------------------|
| Underlying Mechanism        | Dynamic Array                   | Doubly Linked List (DLL)        |
| Manipulation (Insertion/Deletion) | Slow (memory shifting required) | Easy (no memory shifting)       |
| Storage and Access          | Better for storing and accessing | Better for manipulation         |

### Example: Creating a List
```java
// Tightly Coupled
List<String> list1 = new ArrayList<>();

// Loosely Coupled
ArrayList<String> list2 = new ArrayList<>();

// Declaring List with Final Keyword
final List<String> list3 = new ArrayList<>();
list3.add("A"); // Works
// list3 = new ArrayList<>(); // Error: Cannot reassign final reference
```

### Custom ArrayList to Prevent Duplicates
```java
import java.util.ArrayList;

class CustomArrayList extends ArrayList<Object> {
    @Override
    public boolean add(Object o) {
        if (this.contains(o)) {
            return false;
        } else {
            return super.add(o);
        }
    }

    public static void main(String[] args) {
        CustomArrayList list = new CustomArrayList();
        list.add(1);
        list.add(1);
        System.out.println(list); // Output: [1]
    }
}
```

---

## Set

A `Set` is an unordered collection that does not allow duplicate elements.

### Implementations of Set

#### HashSet
- Backed by a `HashMap`.
- Does not maintain any order.

#### LinkedHashSet
- Maintains insertion order.

#### TreeSet
- Maintains elements in sorted order.

### Why Set Does Not Allow Duplicates
- Internally uses a `HashMap`.
- Elements are stored as keys, and duplicate keys are not allowed.

### Example: Behavior with Custom Objects
```java
import java.util.HashSet;

class Student {
    int id;
    String name;

    Student(int id, String name) {
        this.id = id;
        this.name = name;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Student student = (Student) o;
        return id == student.id && name.equals(student.name);
    }

    @Override
    public int hashCode() {
        return id;
    }
}

public class Main {
    public static void main(String[] args) {
        HashSet<Student> set = new HashSet<>();
        Student s1 = new Student(1, "ABC");
        Student s2 = new Student(1, "ABC");
        set.add(s1);
        set.add(s2);
        System.out.println(set.size()); // Output: 1
    }
}
```

### Does Set Always Prevent Duplicates?
When using custom objects in a `Set`, duplicates may still be added unless the `equals` and `hashCode` methods are properly overridden. For example:

```java
Student s1 = new Student(1, "ABC");
Student s2 = new Student(1, "ABC");
HashSet<Student> set = new HashSet<>();
set.add(s1);
set.add(s2);
System.out.println(set.size()); // Output: 2 (without overriding equals and hashCode)
```

---

## Map

A `Map` is a collection of key-value pairs. Keys are unique, but values can be duplicated.

### Implementations of Map

#### HashMap
- No guaranteed order.

#### LinkedHashMap
- Maintains insertion order.

#### TreeMap
- Maintains keys in sorted order.

### Example: Using a Map
```java
import java.util.HashMap;

public class Main {
    public static void main(String[] args) {
        HashMap<Integer, String> map = new HashMap<>();
        map.put(1, "A");
        map.put(2, "B");
        map.put(1, "C"); // Overwrites value for key 1
        System.out.println(map); // Output: {1=C, 2=B}
    }
}
```

---

## Comparable vs Comparator

| Feature                   | Comparable                      | Comparator                   |
|---------------------------|----------------------------------|------------------------------|
| Sorting Sequence          | Single                          | Multiple                     |
| Affects Original Class    | Yes                             | No                           |
| Method                    | `compareTo()`                   | `compare()`                  |
| Package                   | `java.lang`                     | `java.util`                  |
| Usage                     | `Collections.sort(list)`         | `Collections.sort(list, cmp)`|

### Example: Comparable
```java
class Student implements Comparable<Student> {
    int id;

    Student(int id) {
        this.id = id;
    }

    @Override
    public int compareTo(Student s) {
        return Integer.compare(this.id, s.id);
    }
}
```

### Example: Comparator
```java
import java.util.Comparator;

class StudentComparatorByName implements Comparator<Student> {
    @Override
    public int compare(Student s1, Student s2) {
        return s1.name.compareTo(s2.name);
    }
}

class StudentComparatorById implements Comparator<Student> {
    @Override
    public int compare(Student s1, Student s2) {
        return Integer.compare(s1.id, s2.id);
    }
}
```

### Multi-Level Sorting
```java
class StudentComparatorByIdAndName implements Comparator<Student> {
    @Override
    public int compare(Student s1, Student s2) {
        if (s1.id == s2.id) {
            return s1.name.compareTo(s2.name);
        } else {
            return Integer.compare(s1.id, s2.id);
        }
    }
}
```

---

### Key Differences Between List and Set

| Feature                  | List                         | Set                          |
|--------------------------|------------------------------|------------------------------|
| Allows Duplicates        | Yes                          | No                           |
| Index-Based Access       | Yes                          | No                           |
| Underlying Mechanism     | Array or Linked List         | Hashing or Tree structure    |
| Frequent Access          | Better for frequent access   | Not optimized for frequent access |

---

## List

A `List` is an ordered collection that allows duplicate elements and provides index-based access.

### Implementations of List

#### ArrayList
- Backed by a dynamic array.
- Fast for storing and accessing data.
- Slower for insertion and deletion due to memory shifting.

#### LinkedList
- Backed by a doubly linked list (DLL).
- Better for manipulation (insertion and deletion).
- Slower for random access.

### Comparison: ArrayList vs LinkedList

| Feature                     | ArrayList                        | LinkedList                      |
|-----------------------------|-----------------------------------|---------------------------------|
| Underlying Mechanism        | Dynamic Array                   | Doubly Linked List (DLL)        |
| Manipulation (Insertion/Deletion) | Slow (memory shifting required) | Easy (no memory shifting)       |
| Storage and Access          | Better for storing and accessing | Better for manipulation         |

### Example: Creating a List
```java
// Tightly Coupled
List<String> list1 = new ArrayList<>();

// Loosely Coupled
ArrayList<String> list2 = new ArrayList<>();

// Declaring List with Final Keyword
final List<String> list3 = new ArrayList<>();
list3.add("A"); // Works
// list3 = new ArrayList<>(); // Error: Cannot reassign final reference
```

### Custom ArrayList to Prevent Duplicates
```java
import java.util.ArrayList;

class CustomArrayList extends ArrayList<Object> {
    @Override
    public boolean add(Object o) {
        if (this.contains(o)) {
            return false;
        } else {
            return super.add(o);
        }
    }

    public static void main(String[] args) {
        CustomArrayList list = new CustomArrayList();
        list.add(1);
        list.add(1);
        System.out.println(list); // Output: [1]
    }
}
```

---

## Set

A `Set` is an unordered collection that does not allow duplicate elements.

### Implementations of Set

#### HashSet
- Backed by a `HashMap`.
- Does not maintain any order.

#### LinkedHashSet
- Maintains insertion order.

#### TreeSet
- Maintains elements in sorted order.

### Why Set Does Not Allow Duplicates
- Internally uses a `HashMap`.
- Elements are stored as keys, and duplicate keys are not allowed.

### Example: Behavior with Custom Objects
```java
import java.util.HashSet;

class Student {
    int id;
    String name;

    Student(int id, String name) {
        this.id = id;
        this.name = name;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Student student = (Student) o;
        return id == student.id && name.equals(student.name);
    }

    @Override
    public int hashCode() {
        return id;
    }
}

public class Main {
    public static void main(String[] args) {
        HashSet<Student> set = new HashSet<>();
        Student s1 = new Student(1, "ABC");
        Student s2 = new Student(1, "ABC");
        set.add(s1);
        set.add(s2);
        System.out.println(set.size()); // Output: 1
    }
}
```

### Does Set Always Prevent Duplicates?
When using custom objects in a `Set`, duplicates may still be added unless the `equals` and `hashCode` methods are properly overridden. For example:

```java
Student s1 = new Student(1, "ABC");
Student s2 = new Student(1, "ABC");
HashSet<Student> set = new HashSet<>();
set.add(s1);
set.add(s2);
System.out.println(set.size()); // Output: 2 (without overriding equals and hashCode)
```

---

## Map

A `Map` is a collection of key-value pairs. Keys are unique, but values can be duplicated.

### Implementations of Map

#### HashMap
- No guaranteed order.

#### LinkedHashMap
- Maintains insertion order.

#### TreeMap
- Maintains keys in sorted order.

### Example: Using a Map
```java
import java.util.HashMap;

public class Main {
    public static void main(String[] args) {
        HashMap<Integer, String> map = new HashMap<>();
        map.put(1, "A");
        map.put(2, "B");
        map.put(1, "C"); // Overwrites value for key 1
        System.out.println(map); // Output: {1=C, 2=B}
    }
}
```

---

## Comparable vs Comparator

| Feature                   | Comparable                      | Comparator                   |
|---------------------------|----------------------------------|------------------------------|
| Sorting Sequence          | Single                          | Multiple                     |
| Affects Original Class    | Yes                             | No                           |
| Method                    | `compareTo()`                   | `compare()`                  |
| Package                   | `java.lang`                     | `java.util`                  |
| Usage                     | `Collections.sort(list)`         | `Collections.sort(list, cmp)`|

### Example: Comparable
```java
class Student implements Comparable<Student> {
    int id;

    Student(int id) {
        this.id = id;
    }

    @Override
    public int compareTo(Student s) {
        return Integer.compare(this.id, s.id);
    }
}
```

### Example: Comparator
```java
import java.util.Comparator;

class StudentComparatorByName implements Comparator<Student> {
    @Override
    public int compare(Student s1, Student s2) {
        return s1.name.compareTo(s2.name);
    }
}

class StudentComparatorById implements Comparator<Student> {
    @Override
    public int compare(Student s1, Student s2) {
        return Integer.compare(s1.id, s2.id);
    }
}
```

### Multi-Level Sorting
```java
class StudentComparatorByIdAndName implements Comparator<Student> {
    @Override
    public int compare(Student s1, Student s2) {
        if (s1.id == s2.id) {
            return s1.name.compareTo(s2.name);
        } else {
            return Integer.compare(s1.id, s2.id);
        }
    }
}
```

---

# Multi-Level Comparison Using Comparator

When sorting objects based on multiple criteria, the `Comparator` interface is preferred. Below is a detailed explanation and example.

### Example: Multi-Level Sorting

#### Scenario
Sort a list of `Student` objects by:
1. `id` (ascending order).
2. If `id` is the same, sort by `name` (alphabetical order).

#### Implementation
```java
import java.util.*;

class Student {
    int id;
    String name;

    Student(int id, String name) {
        this.id = id;
        this.name = name;
    }

    @Override
    public String toString() {
        return "Student{id=" + id + ", name='" + name + "'}";
    }
}

class StudentComparatorByIdAndName implements Comparator<Student> {
    @Override
    public int compare(Student s1, Student s2) {
        if (s1.id == s2.id) {
            return s1.name.compareTo(s2.name);
        } else {
            return Integer.compare(s1.id, s2.id);
        }
    }
}

public class MultiLevelSorting {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student(1, "Alice"));
        students.add(new Student(2, "Bob"));
        students.add(new Student(1, "Charlie"));

        Collections.sort(students, new StudentComparatorByIdAndName());

        System.out.println(students);
        // Output: [Student{id=1, name='Alice'}, Student{id=1, name='Charlie'}, Student{id=2, name='Bob'}]
    }
}
```

---

# Fail-Fast vs Fail-Safe Iteration

### Fail-Fast Iteration
- Occurs when a collection is structurally modified during iteration.
- Throws `ConcurrentModificationException`.
- Examples: `ArrayList`, `HashMap`.

#### Internal Mechanism: `modCount`
- Tracks structural modifications.
- On iteration, the expected `modCount` is compared with the actual `modCount`.
- If a mismatch is detected, a `ConcurrentModificationException` is thrown.

#### Example: Fail-Fast Behavior
```java
import java.util.*;

public class FailFastExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("A");
        list.add("B");

        for (String s : list) {
            list.add("C"); // Throws ConcurrentModificationException
        }
    }
}
```

### Fail-Safe Iteration
- Works on a clone of the collection.
- Does not throw `ConcurrentModificationException`.
- Examples: `CopyOnWriteArrayList`, `ConcurrentHashMap`.

#### Example: Fail-Safe Behavior
```java
import java.util.concurrent.*;

public class FailSafeExample {
    public static void main(String[] args) {
        CopyOnWriteArrayList<String> list = new CopyOnWriteArrayList<>();
        list.add("A");
        list.add("B");

        for (String s : list) {
            list.add("C"); // No exception
        }

        System.out.println(list); // Output: [A, B, C, C]
    }
}
```

---

# ConcurrentHashMap vs HashMap

| Feature                     | HashMap                         | ConcurrentHashMap             |
|-----------------------------|----------------------------------|--------------------------------|
| Synchronization             | Not synchronized                | Synchronized                  |
| Thread Safety               | Not thread-safe                 | Thread-safe                   |
| Fail-Fast Behavior          | Yes                             | No                            |
| Null Keys/Values            | Allows null keys and values     | Does not allow null keys/values |
| Performance                 | Faster                          | Slower (due to thread safety) |

### Why ConcurrentHashMap is Needed
- `HashMap` is not thread-safe.
- Synchronizing a `HashMap` locks the entire map, reducing performance.
- `ConcurrentHashMap` allows segment-level locking for better concurrency.

#### Example: ConcurrentHashMap
```java
import java.util.concurrent.*;

public class ConcurrentHashMapExample {
    public static void main(String[] args) {
        ConcurrentHashMap<Integer, String> map = new ConcurrentHashMap<>();
        map.put(1, "A");
        map.put(2, "B");

        map.putIfAbsent(3, "C");
        System.out.println(map); // Output: {1=A, 2=B, 3=C}
    }
}
```

---

# Why ConcurrentHashMap Over Synchronized HashMap?

### Synchronized HashMap
- Achieved using `Collections.synchronizedMap()`.
- Locks the entire map for any operation.

### ConcurrentHashMap
- Uses segment-level locking.
- Allows multiple threads to modify the map concurrently without locking the entire structure.

#### Example: Synchronized HashMap
```java
import java.util.*;

public class SynchronizedHashMapExample {
    public static void main(String[] args) {
        Map<Integer, String> map = Collections.synchronizedMap(new HashMap<>());
        map.put(1, "A");
        map.put(2, "B");

        synchronized (map) {
            for (Map.Entry<Integer, String> entry : map.entrySet()) {
                System.out.println(entry.getKey() + " -> " + entry.getValue());
            }
        }
    }
}
```

---

# Null Handling in HashMap and ConcurrentHashMap

### HashMap
- Allows `null` keys and values.
```java
HashMap<Integer, String> map = new HashMap<>();
map.put(null, null);
System.out.println(map); // Output: {null=null}
```

### ConcurrentHashMap
- Does not allow `null` keys or values.
```java
ConcurrentHashMap<Integer, String> map = new ConcurrentHashMap<>();
map.put(null, "A"); // Throws NullPointerException
```

---

# How HashMap Internally Works

### Overview
A `HashMap` in Java stores key-value pairs in buckets. Each bucket corresponds to an index in an internal array, calculated using the hash of the key.

### Key Concepts
1. **Initial Capacity**: Default is 16 buckets (0 to 15).
2. **Hashing**: A key's hash code determines its bucket index.
3. **Collision Handling**: Uses linked lists or trees (Java 8+).
4. **Null Key**: Always stored in bucket 0.

### Example Code
```java
import java.util.*;

class Employee {
    int id;
    String name;

    Employee(int id, String name) {
        this.id = id;
        this.name = name;
    }

    @Override
    public int hashCode() {
        return Objects.hash(id, name);
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Employee employee = (Employee) o;
        return id == employee.id && Objects.equals(name, employee.name);
    }
}

public class HashMapExample {
    public static void main(String[] args) {
        Map<Employee, String> map = new HashMap<>();
        Employee e1 = new Employee(1, "John");
        Employee e2 = new Employee(2, "Jane");
        Employee e3 = new Employee(3, "Jack");

        map.put(e1, "Dev");
        map.put(e2, "QA");
        map.put(e3, "UI");

        System.out.println(map);
    }
}
```

### Diagram: HashMap Workflow

```plaintext
PUT Operation Workflow:

  1. Key: Employee e1
  2. Compute hash: hash(e1) -> 1011
  3. Calculate index: index = hash & (n-1) -> index = 6
  4. Check bucket:
      - If empty, store key-value pair in bucket.
      - If collision (another key already exists):
          - Compare using equals().
          - If equals() returns true, replace value.
          - Otherwise, add to linked list (or tree).
```

#### Diagram: Collision Handling
```plaintext
Bucket Array (Initial Capacity: 16)

Index 0: [null key, value]
Index 6: [e1, "Dev"] -> [e3, "UI"]
Index 7: [e4, "UI"]
Index 9: [e2, "QA"]

Collision at index 6:
    - e3 added as the next node in the linked list.

Java 8+ Enhancement:
    - If linked list exceeds threshold (e.g., 8 nodes), convert to a balanced tree for faster lookup.
```

---

# How TreeMap Internally Works

### Overview
A `TreeMap` stores key-value pairs in a Red-Black Tree, maintaining keys in sorted order.

### Key Concepts
1. **Sorting Order**: Keys are sorted based on natural ordering or a custom comparator.
2. **Red-Black Tree**: A self-balancing binary search tree.
3. **Comparison**: Keys are compared using the `compareTo()` method.

### Example Code
```java
import java.util.*;

public class TreeMapExample {
    public static void main(String[] args) {
        Map<String, String> map = new TreeMap<>();
        map.put("a", "Xyz");
        map.put("d", "ksg");
        map.put("b", "abc");

        System.out.println(map); // Output: {a=Xyz, b=abc, d=ksg}
    }
}
```

### Diagram: TreeMap Workflow

```plaintext
INSERT Operation Workflow:

  1. Key: "d"
  2. Compare with root ("a"):
      - "d".compareTo("a") -> +1 (greater)
      - Add "d" as the right child of "a".

  3. Key: "b"
  4. Compare with root ("a"):
      - "b".compareTo("a") -> +1 (greater)
      - Compare with right child ("d"):
          - "b".compareTo("d") -> -1 (lesser)
          - Add "b" as the left child of "d".

Tree Structure:
      a
       \
        d
       /
      b

Output (in-order traversal): {a=Xyz, b=abc, d=ksg}
```

---

# Key Differences: HashMap vs TreeMap

| Feature           | HashMap                     | TreeMap                     |
|-------------------|-----------------------------|-----------------------------|
| Ordering          | No specific order           | Sorted order (keys)         |
| Implementation    | Hash table + linked list    | Red-Black Tree              |
| Null Keys         | Allows one null key         | Does not allow null keys    |
| Performance       | O(1) for get/put            | O(log n) for get/put        |

# Additional Important Topics in Java Collections for Interviews

## 1. Differences Between Key Collection Interfaces

| Feature       | List                         | Set                          | Map                         |
|---------------|------------------------------|------------------------------|-----------------------------|
| Duplicates    | Allows                      | Does not allow              | Keys: No, Values: Yes      |
| Null Elements | Allows multiple null values | Allows one null element      | Allows one null key        |
| Ordering      | Maintains insertion order (e.g., ArrayList) | Depends on implementation (e.g., LinkedHashSet maintains order) | Depends on implementation (e.g., TreeMap sorts keys) |

---

## 2. Differences Between Key Implementations

### ArrayList vs Vector

| Feature               | ArrayList                  | Vector                      |
|-----------------------|----------------------------|-----------------------------|
| Synchronization       | Not synchronized          | Synchronized                |
| Performance           | Faster                    | Slower due to synchronization |
| Capacity Increment    | 50% of current size       | Doubles current size        |

### HashSet vs LinkedHashSet vs TreeSet

| Feature               | HashSet                   | LinkedHashSet              | TreeSet                    |
|-----------------------|---------------------------|-----------------------------|-----------------------------|
| Ordering              | No ordering              | Maintains insertion order  | Sorted order (natural/comparator) |
| Null Elements         | Allows one null element  | Allows one null element    | Does not allow null        |
| Performance           | O(1) for basic operations| Slightly slower than HashSet | O(log n) for basic operations |

### HashMap vs Hashtable

| Feature               | HashMap                   | Hashtable                   |
|-----------------------|---------------------------|-----------------------------|
| Synchronization       | Not synchronized         | Synchronized                |
| Null Keys/Values      | Allows one null key, multiple null values | Does not allow null keys or values |
| Performance           | Faster                   | Slower                      |

---

## 3. Thread-Safe Collections

| Type                     | Example Classes       | Key Features                                              |
|--------------------------|-----------------------|----------------------------------------------------------|
| Synchronized Wrappers    | `Collections.synchronizedList`, `Collections.synchronizedMap` | Entire collection is synchronized, slower due to locking |
| Concurrent Collections   | `CopyOnWriteArrayList`, `ConcurrentHashMap` | Segment-level locking or cloning for better performance |

### CopyOnWriteArrayList
- **Use Case**: Best for scenarios with more reads than writes.
- **How It Works**: Creates a copy of the list for every modification.
- **Example**:
```java
import java.util.concurrent.CopyOnWriteArrayList;

public class Example {
    public static void main(String[] args) {
        CopyOnWriteArrayList<String> list = new CopyOnWriteArrayList<>();
        list.add("A");
        list.add("B");

        for (String s : list) {
            list.add("C"); // No ConcurrentModificationException
        }

        System.out.println(list);
    }
}
```

### ConcurrentHashMap
- **Use Case**: Best for high-concurrency scenarios.
- **How It Works**: Divides map into segments for thread-safe access.
- **Example**:
```java
import java.util.concurrent.ConcurrentHashMap;

public class Example {
    public static void main(String[] args) {
        ConcurrentHashMap<Integer, String> map = new ConcurrentHashMap<>();
        map.put(1, "A");
        map.put(2, "B");

        map.forEach((key, value) -> map.put(3, "C")); // No ConcurrentModificationException

        System.out.println(map);
    }
}
```

---

## 4. PriorityQueue

### Overview
- A `PriorityQueue` is used to process elements based on priority.
- Internally uses a binary heap.

### Example
```java
import java.util.PriorityQueue;

public class Example {
    public static void main(String[] args) {
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        pq.add(10);
        pq.add(5);
        pq.add(20);

        while (!pq.isEmpty()) {
            System.out.println(pq.poll()); // Prints in ascending order: 5, 10, 20
        }
    }
}
```

---

## 5. Deque (Double-Ended Queue)

### Overview
- Allows insertion and removal from both ends.
- Implementations: `ArrayDeque`, `LinkedList`.

### Example
```java
import java.util.ArrayDeque;

public class Example {
    public static void main(String[] args) {
        ArrayDeque<String> deque = new ArrayDeque<>();
        deque.addFirst("A");
        deque.addLast("B");
        deque.addFirst("C");

        System.out.println(deque); // Output: [C, A, B]
    }
}
```

---

## 6. Immutable Collections

### Overview
- Immutable collections are read-only.
- Use `List.of()`, `Set.of()`, `Map.of()` (Java 9+).

### Example
```java
import java.util.List;

public class Example {
    public static void main(String[] args) {
        List<String> list = List.of("A", "B", "C");
        // list.add("D"); // Throws UnsupportedOperationException
        System.out.println(list);
    }
}
```

---

## 7. Common Interview Questions

1. **What is the difference between HashMap and ConcurrentHashMap?**
2. **Explain fail-fast vs fail-safe iterators.**
3. **How does a HashSet ensure uniqueness?**
4. **What is the load factor in HashMap?**
5. **Why is a LinkedHashMap useful?**
6. **How does a PriorityQueue work internally?**

