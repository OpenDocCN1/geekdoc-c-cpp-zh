
- `default boolean removeIf(Predicate<? super E> filter)` 8 removes all matching elements.

**`java.util.List<E>` 1.2**

- `default void replaceAll(UnaryOperator<E> op)` 8 applies the operation to all elements of this list.

### 9.6.5 Bulk Operations

There are several operations that copy or remove elements “in bulk.” The call

```java
coll1.removeAll(coll2);
```

removes all elements from `coll1` that are present in `coll2`. Conversely,

```java
coll1.retainAll(coll2);
```

removes all elements from `coll1` that are *not* present in `coll2`. Here is a typical application.

Suppose you want to find the *intersection* of two sets—the elements that two sets have in common. First, make a new set to hold the result.

```java
var result = new HashSet<String>(firstSet);
```

Here, we use the fact that every collection has a constructor whose parameter is another collection that holds the initialization values.

Now, use the `retainAll` method:

```java
result.retainAll(secondSet);
```

It retains all elements that occur in both sets. You have formed the intersection without programming a loop.

You can carry this idea further and apply a bulk operation to a view. For example, suppose you have a map that maps employee IDs to employee objects and you have a set of the IDs of all employees that are to be terminated.

```java
Map<String, Employee> staffMap = . . .;
Set<String> terminatedIDs = . . .;
```

Simply form the key set and remove all IDs of terminated employees.

```java
staffMap.keySet().removeAll(terminatedIDs);
```

Since the key set is a view into the map, the keys and associated employee names are automatically removed from the map.

By using a subrange view, you can restrict bulk operations to sublists and subsets. For example, suppose you want to add the first ten elements of a list to another container. Form a sublist to pick out the first ten:

```java
relocated.addAll(staff.subList(0, 10));
```

The subrange can also be a target of a mutating operation.

```java
staff.subList(0, 10).clear();
```

### 9.6.6 Converting between Collections and Arrays

Large portions of the Java platform API were designed before the collections framework was created. As a result, you will occasionally need to translate between traditional arrays and the more modern collections.

If you have an array that you need to turn into a collection, the `List.of` method serves this purpose. For example:

```java
String[] names = . . .;
List<String> staff = List.of(names);
```

Obtaining an array from a collection is a bit trickier. You can use the `toArray` method:

```java
Object[] names = staff.toArray();
```

But the result is an array of *objects*. Even if you know that your collection contained objects of a specific type, you cannot use a cast:

```java
String[] names = (String[]) staff.toArray(); // ERROR
```

The array returned by the `toArray` method was created as an `Object[]` array, and you cannot change its type. Instead, pass an array constructor expression to the `toArray` method. The returned array is then created *as the correct array type*:

```java
String[] values = staff.toArray(String[]::new);
```

![](img/0e7b74ef51a065c077b42cd87b362288_805_0.png)

**NOTE:**

Prior to JDK 11, you had to use another form of the `toArray` method, passing an array of the correct type:

```java
String[] values = staff.toArray(new String[0]);
```

This `toArray` method constructs another array of the same type. Or, if the array has sufficient length, it is reused:

```java
staff.toArray(new String[staff.size()]);
```

**TIP:**

In this case, you can do even better by accepting an `Iterable<Item>`. The `Iterable` interface has a single abstract method `iterator` which the enhanced `for` loop uses behind the scenes. The `Collection` interface extends `Iterable`.

Conversely, if your method returns multiple elements, you don’t want to constrain yourself against future improvements. For example, consider

```java
public ArrayList<Item> lookupItems(. . .)
{
    var result = new ArrayList<Item>();
    . . .
    return result;
}
```

This method promises to return an `ArrayList`, even though the caller almost certainly doesn’t care what kind of list it is. If instead you return a `List`, you can at any time add a branch that returns an empty or singleton list by calling `List.of`.

**NOTE:**

If it is such a good idea to use collection interfaces as parameter and return type, why doesn’t the Java library follow this rule consistently? For example, the `JComboBox` class has two constructors:

```java
JComboBox(Object[] items)
JComboBox(Vector<?> items)
```

The reason is simply timing. The Swing library was created before the collections library.

## 9.7 Legacy Collections

A number of “legacy” container classes have been present since the first release of Java, before there was a collections framework.

They have been integrated into the collections framework—see Figure 9.12. I will briefly introduce them in the following sections.

![](img/0e7b74ef51a065c077b42cd87b362288_808_0.png)

**Figure 9.12** Legacy classes in the collections framework

### 9.7.1 The Hashtable Class

The classic `Hashtable` class serves the same purpose as the `HashMap` class and has essentially the same interface. Just like methods of the `Vector` class, the `Hashtable` methods are synchronized. If you do not require compatibility with legacy code, you should use a `HashMap` instead. If you need concurrent access, use a `ConcurrentHashMap`—see [Chapter 12](#).

### 9.7.2 Enumerations

The legacy collections use the `Enumeration` interface for traversing sequences of elements. The `Enumeration` interface has two methods, `hasMoreElements` and `nextElement`. These are entirely analogous to the `hasNext` and `next` methods of the `Iterator` interface.

If you find this interface with legacy classes, you can use `Collections.list` to collect the elements in an `ArrayList`. For example, the `LogManager` class is only willing to reveal logger names as an `Enumeration`. Here is how you can get them all:

```java
ArrayList<String> loggerNames = Collections.list(LogManager.getLoggerNames());
```

Alternatively, as of Java 9, you can turn an enumeration into an iterator:

```java
LogManager.getLoggerNames().asIterator().forEachRemaining(n -> { ... });
```

You will occasionally encounter a legacy method that expects an enumeration parameter. The static method `Collections.enumeration` yields an enumeration object that enumerates the elements in the collection. For example:

```java
List<InputStream> streams = ...;
var in = new SequenceInputStream(Collections.enumeration(streams));
// the SequenceInputStream constructor expects an enumeration
```

**NOTE:**

In C++, it is quite common to use iterators as parameters. Fortunately, on the Java platform, very few programmers use this idiom. It is much smarter to pass around the collection than to pass an iterator. The collection object is more useful. The recipients can always obtain the iterator from the collection when they need to do so, plus they have all the collection methods at their disposal. However, you will find enumerations in some legacy code because they were the only available mechanism for generic collections until the collections framework appeared in Java 1.2.

**`java.util.Enumeration<E>` 1.0**

- `boolean hasMoreElements()` returns true if there are more elements yet to be inspected.
- `E nextElement()` returns the next element to be inspected. Do not call this method if `hasMoreElements()` returned `false`.
- `default Iterator<E> asIterator()` 9 yields an iterator that iterates over the enumerated elements.

**`java.util.Collections` 1.2**

- `static <T> Enumeration<T> enumeration(Collection<T> c)` returns an enumeration that enumerates the elements of c.
- `public static <T> ArrayList<T> list(Enumeration<T> e)` returns an array list containing the elements enumerated by e.
