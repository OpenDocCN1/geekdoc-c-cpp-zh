
![](img/127bccebb2cfadea3f02579edaad63c3_554_0.png)

**Figure 9.11** A linked hash table

```
157-62-7935
456-62-5527
```

and `staff.values().iterator()` enumerates the values in this order:

```
Amy Lee
Harry Hacker
Gary Cooper
Francesca Cruz
```

A linked hash map can alternatively use *access order*, not insertion order, to iterate through the map entries. Every time you call `get` or `put`, the affected entry is removed from its current position and placed at the *end* of the linked list of entries. (Only the position in the linked list of entries is affected, not the hash table bucket. An entry always stays in the bucket that corresponds to the hash code of the key.) To construct such a hash map, call

```java
new LinkedHashMap<K, V>(initialCapacity, loadFactor, true)
```

Access order is useful for implementing a “least recently used” discipline for a cache. For example, you may want to keep frequently accessed entries in memory and read less frequently accessed objects from a database. When you don't find an entry in the table, and the table is already pretty full, you can get an iterator into the table and remove the first few elements that it enumerates. Those entries were the least recently used ones.

You can even automate that process. Form a subclass of `LinkedHashMap` and override the method

```java
protected boolean removeEldestEntry(Map.Entry<K, V> eldest)
```

Adding a new entry then causes the eldest entry to be removed whenever your method returns true. For example, the following cache is kept at a size of at most 100 elements:

```java
var cache = new LinkedHashMap<K, V>(128, 0.75F, true)
{
    protected boolean removeEldestEntry(Map.Entry<K, V> eldest)
    {
        return size() > 100;
    }
};
```

Alternatively, you can consider the eldest entry to decide whether to remove it. For example, you may want to check a time stamp stored with the entry.

### 9.4.6 Enumeration Sets and Maps

The EnumSet is an efficient set implementation with elements that belong to an enumerated type. Since an enumerated type has a finite number of instances, the EnumSet is internally implemented simply as a sequence of bits. A bit is turned on if the corresponding value is present in the set.

The EnumSet class has no public constructors. Use a static factory method to construct the set:

```java
enum Weekday { MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY };
EnumSet<Weekday> always = EnumSet.allOf(Weekday.class);
EnumSet<Weekday> never = EnumSet.noneOf(Weekday.class);
EnumSet<Weekday> workday = EnumSet.range(Weekday.MONDAY, Weekday.FRIDAY);
EnumSet<Weekday> mwf = EnumSet.of(Weekday.MONDAY, Weekday.WEDNESDAY, Weekday.FRIDAY);
```

You can use the usual methods of the Set interface to modify an EnumSet.

An EnumMap is a map with keys that belong to an enumerated type. It is simply and efficiently implemented as an array of values. You need to specify the key type in the constructor:

```java
var personInCharge = new EnumMap<Weekday, Employee>(Weekday.class);
```

> NOTE: In the API documentation for EnumSet, you will see odd-looking type parameters of the form `E extends Enum<E>`. This simply means “E is an enumerated type.” All enumerated types extend the generic Enum class. For example, `Weekday extends Enum<Weekday>`.

### 9.4.7 Identity Hash Maps

The IdentityHashMap has a quite specialized purpose. Here, the hash values for the keys should not be computed by the hashCode method but by the System.identityHashCode method. That's the method that Object.hashCode uses to compute a hash code from the object's memory address. Also, for comparison of objects, the IdentityHashMap uses ==, not equals.

In other words, different key objects are considered distinct even if they have equal contents. This class is useful for implementing object traversal algorithms, such as object serialization, in which you want to keep track of which objects have already been traversed.

| `java.util.WeakHashMap<K, V>` 1.2 |
|---|
| • `WeakHashMap()`<br>• `WeakHashMap(int initialCapacity)`<br>• `WeakHashMap(int initialCapacity, float loadFactor)`<br>  constructs an empty hash map with the specified capacity and load factor. |

| `java.util.LinkedHashSet<E>` 1.4 |
|---|
| • `LinkedHashSet()`<br>• `LinkedHashSet(int initialCapacity)`<br>• `LinkedHashSet(int initialCapacity, float loadFactor)`<br>  constructs an empty linked hash set with the specified capacity and load factor. |

| `java.util.LinkedHashMap<K, V>` 1.4 |
|---|
| • `LinkedHashMap()`<br>• `LinkedHashMap(int initialCapacity)`<br>• `LinkedHashMap(int initialCapacity, float loadFactor)`<br>• `LinkedHashMap(int initialCapacity, float loadFactor, boolean accessOrder)`<br>  constructs an empty linked hash map with the specified capacity, load factor, and ordering. The accessOrder parameter is true for access order, false for insertion order.<br>• `protected boolean removeEldestEntry(Map.Entry<K, V> eldest)`<br>  should be overridden to return true if you want the eldest entry to be removed. The eldest parameter is the entry whose removal is being contemplated. This method is called after an entry has been added to the map. The default implementation returns false—old elements are not removed by default. However, you can redefine this method to selectively return true—for example, if the eldest entry fits a certain condition or if the map exceeds a certain size. |

| `java.util.EnumSet<E extends Enum<E>>` 5 |
|---|
| • `static <E extends Enum<E>> EnumSet<E> allOf(Class<E> enumType)`<br>  returns a mutable set that contains all values of the given enumerated type.<br>• `static <E extends Enum<E>> EnumSet<E> noneOf(Class<E> enumType)`<br>  returns a mutable set that is initially empty.<br>• `static <E extends Enum<E>> EnumSet<E> range(E from, E to)`<br>  returns a mutable set that contains all values between from and to (inclusive).<br>• `static <E extends Enum<E>> EnumSet<E> of(E e)`<br>  ...<br>• `static <E extends Enum<E>> EnumSet<E> of(E e1, E e2, E e3, E e4, E e5)`<br>• `static <E extends Enum<E>> EnumSet<E> of(E first, E... rest)`<br>  returns a mutable set containing the given elements which must not be null. |

| `java.util.EnumMap<K extends Enum<K>, V>` 5 |
|---|
| • `EnumMap(Class<K> keyType)`<br>  constructs an empty mutable map whose keys have the given type. |

| `java.util.IdentityHashMap<K, V>` 1.4 |
|---|
| • `IdentityHashMap()`<br>• `IdentityHashMap(int expectedMaxSize)`<br>  constructs an empty identity hash map whose capacity is the smallest power of 2 exceeding 1.5 × expectedMaxSize. (The default for expectedMaxSize is 21.) |

| `java.lang.System` | 1.0 |
|---|---|
| • `static int identityHashCode(Object obj)` 1.1 | returns the same hash code (derived from the object’s memory address) that `Object.hashCode` computes, even if the class to which obj belongs has redefined the `hashCode` method. |

## 9.5 Views and Wrappers

If you look at Figures 9.4 and 9.5, you might think it is overkill to have lots of interfaces and abstract classes to implement a modest number of concrete collection classes. However, these figures don’t tell the whole story. By using *views*, you can obtain other objects that implement the Collection or Map interfaces. You saw one example of this with the keySet method of the map classes. At first glance, it appears as if the method creates a new set, fills it with all the keys of the map, and returns it. However, that is not the case. Instead, the keySet method returns an object of a class that implements the Set interface and whose methods manipulate the original map. Such a collection is called a *view*.

The technique of views has a number of useful applications in the collections framework. We will discuss these applications in the following sections.

### 9.5.1 Small Collections

Java 9 introduces static methods yielding a set or list with given elements, and a map with given key/value pairs.

For example,

```java
List<String> names = List.of("Peter", "Paul", "Mary");
Set<Integer> numbers = Set.of(2, 3, 5);
```

yield a list and a set with three elements. For a map, you specify the keys and values, like this:

```java
Map<String, Integer> scores = Map.of("Peter", 2, "Paul", 3, "Mary", 5);
```

The elements, keys, or values may not be null.

The List and Set interfaces have eleven methods with zero to ten arguments, and an of method with a variable number of arguments. The specializations are provided for efficiency.
