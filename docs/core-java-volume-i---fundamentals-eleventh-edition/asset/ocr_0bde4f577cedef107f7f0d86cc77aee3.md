Of course, if you have an existing map, the keySet method yields the set of keys. That set is mutable. If you remove the set’s elements, the keys (and their values) are removed from the map. But it doesn’t make sense to add elements to the key set, because there would be no corresponding values to add. There is a second keySet method to ConcurrentHashMap, with a default value, to be used when adding elements to the set:

```
```java
Set<String> words = map.keySet(1L);
words.add("Java");
```
```

If "Java" wasn’t already present in words, it now has a value of one.

# ### 12.5.6 Copy on Write Arrays

The CopyOnWriteArrayList and CopyOnWriteArraySet are thread-safe collections in which all mutators make a copy of the underlying array. This arrangement is useful if the threads that iterate over the collection greatly outnumber the threads that mutate it. When you construct an iterator, it contains a reference to the current array. If the array is later mutated, the iterator still has the old array, but the collection’s array is replaced. As a consequence, the older iterator has a consistent (but potentially outdated) view that it can access without any synchronization expense.

# ### 12.5.7 Parallel Array Algorithms

The Arrays class has a number of parallelized operations. The static Arrays.parallelSort method can sort an array of primitive values or objects. For example,

```
```java
var contents = new String(Files.readAllBytes(
      Path.of("alice.txt")), StandardCharsets.UTF_8); // read file into string
String[] words = contents.split("[\\P{L}]+"); // split along nonletters
Arrays.parallelSort(words);
```
```

When you sort objects, you can supply a Comparator.

```
```java
Arrays.parallelSort(words, Comparator.comparing(String::length));
```
```

With all methods, you can supply the bounds of a range, such as

```
```java
Arrays.parallelSort(words.length / 2, words.length); // sort the upper half
```
```

> > **NOTE:** At first glance, it seems a bit odd that these methods have parallel in their name, since the user shouldn’t care how the sorting happens. However, the API designers wanted to make it clear that the sorting is parallelized. That way, users are on notice to avoid comparators with side effects.