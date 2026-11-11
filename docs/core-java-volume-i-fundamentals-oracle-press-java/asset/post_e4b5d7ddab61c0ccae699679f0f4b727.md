
- `static <E extends Enum<E>> EnumSet<E> noneOf(Class<E> enumType)` returns a mutable set that is initially empty.
- `static <E extends Enum<E>> EnumSet<E> range(E from, E to)` returns a mutable set that contains all values between `from` and `to` (inclusive).
- `static <E extends Enum<E>> EnumSet<E> of(E e)`
  . . .
- `static <E extends Enum<E>> EnumSet<E> of(E e1, E e2, E e3, E e4, E e5)`
- `static <E extends Enum<E>> EnumSet<E> of(E first, E... rest)` returns a mutable set containing the given elements which must not be null.
- `public static <E extends Enum<E>> EnumSet<E> copyOf(EnumSet<E> s)`  
  `public static <E extends Enum<E>> EnumSet<E> copyOf(Collection<E> c)`  
  creates a mutable set initially containing the given elements. In the second method, `c` must either be an `EnumSet` or be nonempty (in order to determine the element type).

### `java.util.EnumMap<K extends Enum<K>, V>` 5

- `EnumMap(Class<K> keyType)` constructs an empty mutable map whose keys have the given type.

### `java.util.IdentityHashMap<K, V>` 1.4

- `IdentityHashMap()`
- `IdentityHashMap(int expectedMaxSize)` constructs an empty identity hash map whose capacity is the smallest power of 2 exceeding 1.5 × `expectedMaxSize`. (The default for `expectedMaxSize` is 21.)

### **java.lang.System** 1.0

- `static int identityHashCode(Object obj)` 1.1 returns the same hash code (derived from the object’s memory address) that `Object.hashCode` computes, even if the class to which `obj` belongs has redefined the `hashCode` method.

## 9.5 Copies and Views

If you look at Figures 9.4 and 9.5, you might think it is overkill to have lots of interfaces and abstract classes to implement a modest number of concrete collection classes. However, these figures don’t tell the whole story. By using *views*, you can obtain other objects that implement the Collection or Map interfaces. You saw one example of this with the keySet method of the map class. At first glance, it appears as if the method creates a new set, fills it with all the keys of the map, and returns it. However, that is not the case. Instead, the keySet method returns an object of a class that implements the Set interface and whose methods manipulate the original map. Such a collection is called a *view*.

The technique of views has a number of useful applications in the collections framework. We will discuss these applications in the following sections.

### 9.5.1 Small Collections

Java 9 introduces static methods yielding a set or list with given elements, and a map with given key/value pairs. For example,

```java
List<String> names = List.of("Peter", "Paul", "Mary");
Set<Integer> numbers = Set.of(2, 3, 5);
```

yield a list and a set with three elements. For a map, you specify the keys and values, like this:

```java
Map<String, Integer> scores = Map.of("Peter", 2, "Paul", 3, "Mary", 5);
```

The elements, keys, or values may not be null. Set and map keys may not be duplicated:

```java
numbers = Set.of(13, null); // Error—null element
scores = Map.of("Peter", 4, "Peter", 2); // Error—duplicate key
```

![](img/0e7b74ef51a065c077b42cd87b362288_778_0.png)

**CAUTION:**

No guarantee is made about the iteration order of these sets and maps. In fact, the order is deliberately scrambled with a seed that is randomized at each virtual machine startup. Look at these two jshell runs:

```text
$ jshell -q
jshell> Set.of("Peter", "Paul", "Mary")
$1 ==> [Peter, Mary, Paul]
jshell> /exit
$ jshell -q
jshell> Set.of("Peter", "Paul", "Mary")
$1 ==> [Paul, Mary, Peter]
```

Some Java programmers write programs whose correctness depends on the assumption that implementation details will never change. That can make it very difficult for the library implementors to make useful implementation changes. In this case, the message is clear—don't write programs that assume anything about the element order.

The `List` and `Set` interfaces have eleven `of` methods with zero to ten arguments, and an `of` method with a variable number of arguments. The specializations are provided for efficiency.

For the `Map` interface, it is not possible to provide a version with variable arguments since the argument types alternate between the key and value types. There is a static method `ofEntries` that accepts an arbitrary number of `Map.Entry<K, V>` objects, which you can create with the static `entry` method. For example,

```java
import static java.util.Map.*;
. . .
Map<String, Integer> scores = ofEntries(
    entry("Peter", 2),
    entry("Paul", 3),
    entry("Mary", 5));
```

The `of` and `ofEntries` methods produce objects of classes that have an instance variable for each element, or that are backed by an array.

These collection objects are *unmodifiable*. Any attempt to change their contents results in an `UnsupportedOperationException`.

If you want a mutable collection, you can pass the unmodifiable collection to the constructor:

```java
var names = new ArrayList<>(List.of("Peter", "Paul", "Mary"));
// A mutable list of names
```

The method call `Collections.nCopies(n, anObject)` returns an immutable object that implements the `List` interface and gives the illusion of having n elements, each of which appears as an `Object`.

For example, the following call creates a `List` containing 100 strings, all set to `"DEFAULT"`:

```java
List<String> settings = Collections.nCopies(100, "DEFAULT");
```

There is very little storage cost—the object is stored only once.

![](img/0e7b74ef51a065c077b42cd87b362288_780_0.png)

> **NOTE:**
>
> The of methods were introduced in Java 9. Previously, there was a static `Arrays.asList` method that returns a list that is mutable but not resizable. That is, you can call `set` but not add or remove on the list. There are also legacy methods `Collections.emptySet` and `Collections.singleton`.

![](img/0e7b74ef51a065c077b42cd87b362288_780_1.png)

> **NOTE:**
>
> The `Collections` class contains a number of utility methods with parameters or return values that are collections. Do not confuse it with the `Collection` interface.

![](img/0e7b74ef51a065c077b42cd87b362288_780_2.png)

> **TIP:**
>
> Java doesn’t have a pair class, and some programmers use a `Map.Entry` as a poor man’s pair. Before Java 9, this was painful—you had to construct a new `AbstractMap.SimpleImmutableEntry<>(first, second)`. Nowadays, you can call `Map.entry(first, second)`.

### 9.5.2 Unmodifiable Copies and Views

To make an *unmodifiable copy* of a collection, use the `copyOf` method of the collection type:

```java
ArrayList<String> names = . . .;
Set<String> nameSet = Set.copyOf(names); // The names as an unmodifiable set
List<String> nameList = List.copyOf(names); // The names as an unmodifiable list
```

Each `copyOf` method makes a copy of the collection. If the original collection is modified, the copy is not affected.

If the original collection happens to be unmodifiable and of the correct type, then `copyOf` simply returns it:

```java
Set<String> names = Set.of("Peter", "Paul", "Mary");
Set<String> nameSet = Set.copyOf(names); // No need to make a copy: names == nameSet
```

The `Collections` class has methods that produce *unmodifiable views* of collections. These views add a runtime check to an existing collection. If an attempt to modify the unmodifiable collection is detected, an exception is thrown.

However, if the original collection changes, the view reflects those changes. That is what makes views different from copies.

You obtain unmodifiable views by eight methods:

```java
Collections.unmodifiableCollection
Collections.unmodifiableList
Collections.unmodifiableSet
Collections.unmodifiableSortedSet
Collections.unmodifiableNavigableSet
Collections.unmodifiableMap
Collections.unmodifiableSortedMap
Collections.unmodifiableNavigableMap
```
