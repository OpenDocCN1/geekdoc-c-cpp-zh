
A checked view can detect this problem. Define a safe list as follows:

```java
List<String> safeStrings = Collections.checkedList(strings, String.class);
```

The view’s add method checks that the inserted object belongs to the given class and immediately throws a ClassCastException if it does not. The advantage is that the error is reported at the correct location:

```java
ArrayList rawList = safeStrings;
rawList.add(new Date()); // checked list throws ClassCastException
```

> **CAUTION:** The checked views are limited by the runtime checks that the virtual machine can carry out. For example, if you have an ArrayList<Pair<String>>, you cannot protect it from inserting a Pair<Date> since the virtual machine has a single "raw" Pair class.

## 9.5.6 A Note on Optional Operations

A view usually has some restriction—it may be read-only, it may not be able to change the size, or it may support removal but not insertion (as is the case for the key view of a map). A restricted view throws an UnsupportedOperationException if you attempt an inappropriate operation.

In the API documentation for the collection and iterator interfaces, many methods are described as “optional operations.” This seems to be in conflict with the notion of an interface. After all, isn’t the purpose of an interface to lay out the methods that a class *must* implement? Indeed, this arrangement is unsatisfactory from a theoretical perspective. A better solution might have been to design separate interfaces for read-only views and views that can’t change the size of a collection. However, that would have tripled the number of interfaces, which the designers of the library found unacceptable.

Should you extend the technique of “optional” methods to your own designs? We think not. Even though collections are used frequently, the coding style for implementing them is not typical for other problem domains. The designers of a collection class library have to resolve a particularly brutal set of conflicting requirements. Users want the library to be easy to learn, convenient to use, completely generic, idiot-proof, and at the same time as efficient as hand-coded algorithms. It is plainly impossible to achieve all these goals simultaneously, or even to come close. But in your own programming problems, you will rarely encounter such an extreme set of constraints. You should be able to find solutions that do not rely on the extreme measure of “optional” interface operations.

## java.util.List 1.2

- `static <E> List<E> of()` 9
- `static <E> List<E> of(E e1)` 9
- ...
- `static <E> List<E> of(E e1, E e2, E e3, E e4, E e5, E e6, E e7, E e8, E e9, E e10)` 9
- `static <E> List<E> of(E... elements)` 9

yields an immutable list of the given elements, which must not be null.

## java.util.Set 1.2

- `static <E> Set<E> of()` 9
- `static <E> Set<E> of(E e1)` 9
- ...
- `static <E> Set<E> of(E e1, E e2, E e3, E e4, E e5, E e6, E e7, E e8, E e9, E e10)` 9
- `static <E> Set<E> of(E... elements)` 9

yields an immutable set of the given elements, which must not be null.

## java.util.Map 1.2

- `static <K, V> Map<K, V> of()` 9
- `static <K, V> Map<K, V> of(K k1, V v1)` 9
- ...
- `static <K, V> Map<K, V> of(K k1, V v1, K k2, V v2, K k3, V v3, K k4, V v4, K k5, V v5, K k6, V v6, K k7, V v7, K k8, V v8, K k9, V v9, K k10, V v10)` 9

yields an immutable map of the given keys and values, which must not be null.

- `static <K, V> Map.Entry<K, V> entry(K k, V v)` 9

yields an immutable map entry of the given key and value, which must not be null.

- `static <K, V> Map<K, V> ofEntries(Map.Entry<? extends K, ? extends V>... entries)` 9

yields an immutable map of the given entries.

## java.util.Collections 1.2

| 方法/描述 | 版本 |
|---|---|
| `static <E> Collection unmodifiableCollection(Collection<E> c)` | |
| `static <E> List unmodifiableList(List<E> c)` | |
| `static <E> Set unmodifiableSet(Set<E> c)` | |
| `static <E> SortedSet unmodifiableSortedSet(SortedSet<E> c)` | |
| `static <E> SortedSet unmodifiableNavigableSet(NavigableSet<E> c)` | 8 |
| `static <K, V> Map unmodifiableMap(Map<K, V> c)` | |
| `static <K, V> SortedMap unmodifiableSortedMap(SortedMap<K, V> c)` | |
| `static <K, V> SortedMap unmodifiableNavigableMap(NavigableMap<K, V> c)` | 8 |
| Constructs a view of the collection; the view’s mutator methods throw an UnsupportedOperationException. | |
| `static <E> Collection<E> synchronizedCollection(Collection<E> c)` | |
| `static <E> List synchronizedList(List<E> c)` | |
| `static <E> Set synchronizedSet(Set<E> c)` | |
| `static <E> SortedSet synchronizedSortedSet(SortedSet<E> c)` | |
| `static <E> NavigableSet synchronizedNavigableSet(NavigableSet<E> c)` | 8 |
| `static <K, V> Map<K, V> synchronizedMap(Map<K, V> c)` | |
| `static <K, V> SortedMap<K, V> synchronizedSortedMap(SortedMap<K, V> c)` | |
| `static <K, V> NavigableMap<K, V> synchronizedNavigableMap(NavigableMap<K, V> c)` | 8 |
| Constructs a view of the collection; the view’s methods are synchronized. | |
| `static <E> Collection<E> checkedCollection(Collection<E> c, Class<E> elementType)` | |
| `static <E> List<E> checkedList(List<E> c, Class<E> elementType)` | |
| `static <E> Set<E> checkedSet(Set<E> c, Class<E> elementType)` | |
| `static <E> SortedSet<E> checkedSortedSet(SortedSet<E> c, Class<E> elementType)` | |
| `static <E> NavigableSet<E> checkedNavigableSet(NavigableSet<E> c, Class<E> elementType)` | 8 |
| `static <K, V> Map<K, V> checkedMap(Map<K, V> c, Class<K> keyType, Class<V> valueType)` | |
| `static <K, V> SortedMap<K, V> checkedSortedMap(SortedMap<K, V> c, Class<K> keyType, Class<V> valueType)` | |
| `static <K, V> NavigableMap<K, V> checkedNavigableMap(NavigableMap<K, V> c, Class<K> keyType, Class<V> valueType)` | 8 |
| `static <E> Queue<E> checkedQueue(Queue<E> queue, Class<E> elementType)` | 8 |
| Constructs a view of the collection; the view’s methods throw a ClassCastException if an element of the wrong type is inserted. | |
| `static <E> List<E> nCopies(int n, E value)` | |
| Yields an unmodifiable list with n identical values. | |

```java
for (int i = 1; i < a.length; i++)
   if (largest.compareTo(a[i]) < 0)
      largest = a[i];
```

Of course, to find the maximum of an array list, you would write the code slightly differently.

```java
if (v.size() == 0) throw new NoSuchElementException();
T largest = v.get(0);
for (int i = 1; i < v.size(); i++)
   if (largest.compareTo(v.get(i)) < 0)
      largest = v.get(i);
```

What about a linked list? You don't have efficient random access in a linked list, but you can use an iterator.

```java
if (l.isEmpty()) throw new NoSuchElementException();
Iterator<T> iter = l.iterator();
T largest = iter.next();
while (iter.hasNext())
{
   T next = iter.next();
   if (largest.compareTo(next) < 0)
      largest = next;
}
```

These loops are tedious to write, and just a bit error-prone. Is there an off-by-one error? Do the loops work correctly for empty containers? For containers with only one element? You don't want to test and debug this code every time, but you also don't want to implement a whole slew of methods, such as these:

```java
static <T extends Comparable> T max(T[] a)
static <T extends Comparable> T max(ArrayList<T> v)
static <T extends Comparable> T max(LinkedList<T> l)
```

That's where the collection interfaces come in. Think of the minimal collection interface that you need to efficiently carry out the algorithm. Random access with get and set comes higher in the food chain than simple iteration. As you have seen in the computation of the maximum element in a linked list, random access is not required for this task. Computing the maximum can be done simply by iterating through the elements. Therefore, you can implement the max method to take any object that implements the Collection interface.

```java
public static <T extends Comparable> T max(Collection<T> c)
{
   if (c.isEmpty()) throw new NoSuchElementException();
   Iterator<T> iter = c.iterator();
   T largest = iter.next();
   ...
```
