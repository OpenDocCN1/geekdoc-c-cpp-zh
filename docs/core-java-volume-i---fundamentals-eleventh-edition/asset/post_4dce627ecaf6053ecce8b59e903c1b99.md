
**`java.util.concurrent.ArrayBlockingQueue<E>`** 5

- `ArrayBlockingQueue(int capacity)`
- `ArrayBlockingQueue(int capacity, boolean fair)`

constructs a blocking queue with the given capacity and fairness settings. The queue is implemented as a circular array.

**`java.util.concurrent.LinkedBlockingQueue<E>`** 5  
**`java.util.concurrent.LinkedBlockingDeque<E>`** 6

- `LinkedBlockingQueue()`
- `LinkedBlockingDeque()`

constructs an unbounded blocking queue or deque, implemented as a linked list.

- `LinkedBlockingQueue(int capacity)`
- `LinkedBlockingDeque(int capacity)`

constructs a bounded blocking queue or deque with the given capacity, implemented as a linked list.

**`java.util.concurrent.DelayQueue<E extends Delayed>`** 5

- `DelayQueue()`

constructs an unbounded blocking queue of delayed elements. Only elements whose delay has expired can be removed from the queue.

**`java.util.concurrent.Delayed`** 5

- `long getDelay(TimeUnit unit)`

gets the delay for this object, measured in the given time unit.

**`java.util.concurrent.PriorityBlockingQueue<E>`** 5

- `PriorityBlockingQueue()`
- `PriorityBlockingQueue(int initialCapacity)`
- `PriorityBlockingQueue(int initialCapacity, Comparator<? super E> comparator)`

constructs an unbounded blocking priority queue implemented as a heap. The default for the initial capacity is 11. If the comparator is not specified, the elements must implement the `Comparable` interface.

| API | Since | Method | Description |
|---|---|---|---|
| `java.util.concurrent.BlockingQueue<E>` | 5 | `void put(E element)` | adds the element, blocking if necessary. |
| `java.util.concurrent.BlockingQueue<E>` | 5 | `E take()` | removes and returns the head element, blocking if necessary. |
| `java.util.concurrent.BlockingQueue<E>` | 5 | `boolean offer(E element, long time, TimeUnit unit)` | adds the given element and returns true if successful, blocking if necessary until the element has been added or the time has elapsed. |
| `java.util.concurrent.BlockingQueue<E>` | 5 | `E poll(long time, TimeUnit unit)` | removes and returns the head element, blocking if necessary until an element is available or the time has elapsed. Returns null upon failure. |
| `java.util.concurrent.BlockingDeque<E>` | 6 | `void putFirst(E element)`<br>`void putLast(E element)` | adds the element, blocking if necessary. |
| `java.util.concurrent.BlockingDeque<E>` | 6 | `E takeFirst()`<br>`E takeLast()` | removes and returns the head or tail element, blocking if necessary. |
| `java.util.concurrent.BlockingDeque<E>` | 6 | `boolean offerFirst(E element, long time, TimeUnit unit)`<br>`boolean offerLast(E element, long time, TimeUnit unit)` | adds the given element and returns true if successful, blocking if necessary until the element has been added or the time has elapsed. |
| `java.util.concurrent.BlockingDeque<E>` | 6 | `E pollFirst(long time, TimeUnit unit)`<br>`E pollLast(long time, TimeUnit unit)` | removes and returns the head or tail element, blocking if necessary until an element is available or the time has elapsed. Returns null upon failure. |
| `java.util.concurrent.TransferQueue<E>` | 7 | `void transfer(E element)`<br>`boolean tryTransfer(E element, long time, TimeUnit unit)` | transfers a value, or tries transferring it with a given timeout, blocking until another thread has removed the item. The second method returns true if successful. |

### 12.5.2 Efficient Maps, Sets, and Queues

The `java.util.concurrent` package supplies efficient implementations for maps, sorted sets, and queues: `ConcurrentHashMap`, `ConcurrentSkipListMap`, `ConcurrentSkipListSet`, and `ConcurrentLinkedQueue`.

These collections use sophisticated algorithms that minimize contention by allowing concurrent access to different parts of the data structure.

Unlike most collections, the `size` method of these classes does not necessarily operate in constant time. Determining the current size of one of these collections usually requires traversal.

> **NOTE:** Some applications use humongous concurrent hash maps, so large that the `size` method is insufficient because it returns an int. What is one to do with a map that has over two billion entries? The `mappingCount` method returns the size as a long.

The collections return *weakly consistent* iterators. That means that the iterators may or may not reflect all modifications that are made after they were constructed, but they will not return a value twice and they will not throw a `ConcurrentModificationException`.

> **NOTE:** In contrast, an iterator of a collection in the `java.util` package throws a `ConcurrentModificationException` when the collection has been modified after construction of the iterator.

The concurrent hash map can efficiently support a large number of readers and a bounded number of writers.

> **NOTE:** A hash map keeps all entries with the same hash code in the same “bucket.” Some applications use poor hash functions, and as a result all entries end up in a small number of buckets, severely degrading performance. Even generally reasonable hash functions, such as that of the `String` class, can be problematic. For example, an attacker can slow down a program by crafting a large number of strings that hash to the same value. In recent Java versions, the concurrent hash map organizes the buckets as trees, not lists, when the key type implements `Comparable`, guaranteeing **O(log n)** performance.

| API | Since | Description |
|---|---|---|
| `java.util.concurrent.ConcurrentLinkedQueue<E>` | 5 | `ConcurrentLinkedQueue<E>()`<br>constructs an unbounded, nonblocking queue that can be safely accessed by multiple threads. |
| `java.util.concurrent.ConcurrentSkipListSet<E>` | 6 | `ConcurrentSkipListSet<E>()`<br>`ConcurrentSkipListSet<E>(Comparator<? super E> comp)`<br>constructs a sorted set that can be safely accessed by multiple threads. The first constructor requires that the elements implement the `Comparable` interface. |
| `java.util.concurrent.ConcurrentHashMap<K,V>` | 5 | `ConcurrentHashMap<K,V>()`<br>`ConcurrentHashMap<K,V>(int initialCapacity)`<br>`ConcurrentHashMap<K,V>(int initialCapacity, float loadFactor, int concurrencyLevel)`<br>constructs a hash map that can be safely accessed by multiple threads. The default for the initial capacity is 16. If the average load per bucket exceeds the load factor, the table is resized. The default is 0.75. The concurrency level is the estimated number of concurrent writer threads. |
| `java.util.concurrent.ConcurrentSkipListMap<K,V>` | 6 | `ConcurrentSkipListMap<K,V>()`<br>`ConcurrentSkipListMap<K,V>(Comparator<? super K> comp)`<br>constructs a sorted map that can be safely accessed by multiple threads. The first constructor requires that the keys implement the `Comparable` interface. |

### 12.5.3 Atomic Update of Map Entries

The original version of `ConcurrentHashMap` only had a few methods for atomic updates, which made for somewhat awkward programming. Suppose we want to count how often certain features are observed. As a simple example, suppose multiple threads encounter words, and we want to count their frequencies.

Can we use a `ConcurrentHashMap<String, Long>`? Consider the code for incrementing a count. Obviously, the following is not thread-safe:

```java
Long oldValue = map.get(word);
Long newValue = oldValue == null ? 1 : oldValue + 1;
map.put(word, newValue); // ERROR--might not replace oldValue
```

Another thread might be updating the exact same count at the same time.

> **NOTE:** Some programmers are surprised that a supposedly thread-safe data structure permits operations that are not thread-safe. But there are two entirely different considerations. If multiple threads modify a plain `HashMap`, they can destroy the internal structure (an array of linked lists). Some of the links may go missing, or even go in circles, rendering the data structure unusable. That will never happen with a `ConcurrentHashMap`. In the example above, the code for `get` and `put` will never corrupt the data structure. But, since the sequence of operations is not atomic, the result is not predictable.

In old versions of Java, it was necessary to use the `replace` method, which atomically replaces an old value with a new one, provided that no other thread has come before and replaced the old value with something else. You had to keep doing it until the attempt succeeded:

```java
do
{
    oldValue = map.get(word);
    newValue = oldValue == null ? 1 : oldValue + 1;
}
while (!map.replace(word, oldValue, newValue));
```

An alternative was to use a `ConcurrentHashMap<String, AtomicLong>` and the following update code:

```java
map.putIfAbsent(word, new AtomicLong());
map.get(word).incrementAndGet();
```

Unfortunately, a new `AtomicLong` is constructed for each increment, whether or not it is needed.

Nowadays, the Java API provides methods that make atomic updates more convenient. The `compute` method is called with a key and a function to compute the new value. That function receives the key and the associated value, or null if there is none, and it computes the new value. For example, here is how we can update a map of integer counters:

```java
map.compute(word, (k, v) -> v == null ? 1 : v + 1);
```
