
such a way that objects with different data yield different codes. [Table 9.2](#) lists a few examples of hash codes that result from the `hashCode` method of the `String` class.

If you define your own classes, you are responsible for implementing your own `hashCode` method—see [Chapter 5](#) for more information. Your implementation needs to be compatible with the `equals` method. If `a.equals(b)`, then a and b must have the same hash code.

## Table 9.2 Hash Codes Resulting from the `hashCode` Method

| String | Hash Code |
|---|---:|
| "Lee" | 76268 |
| "lee" | 107020 |
| "eel" | 100300 |

What’s important for now is that hash codes can be computed quickly and that the computation depends only on the state of the object that needs to be hashed, not on the other objects in the hash table.

In Java, hash tables are implemented as arrays of linked lists. Each list is called a *bucket* (see [Figure 9.10](#)). To find the place of an object in the table, compute its hash code and reduce it modulo the total number of buckets. The resulting number is the index of the bucket that holds the element. For example, if an object has hash code 76268 and there are 128 buckets, then the object is placed in bucket 108 (because the remainder 76268 % 128 is 108). Perhaps you are lucky and there is no other element in that bucket. Then, you simply insert the element into that bucket. Of course, sometimes you will hit a bucket that is already filled. This is called a *hash collision*. Then, compare the new object with all objects in that bucket to see if it is already present. If the hash codes are reasonably randomly distributed and the number of buckets is large enough, only a few comparisons should be necessary.

![](img/0e7b74ef51a065c077b42cd87b362288_745_0.png)

**Figure 9.10** A hash table

### **NOTE:**

As of Java 8, the buckets change from linked lists into balanced binary trees when they get full. This improves performance if a hash function was poorly chosen and yields many collisions, or if malicious code tries to flood a hash table with many values that have identical hash codes.

### **TIP:**

If at all possible, the keys of a hash table should belong to a class that implements the `Comparable` interface. Then you are guaranteed not to suffer poor performance due to poorly distributed hash codes.

If you want more control over the performance of the hash table, you can specify the initial bucket count. The bucket count gives the number of buckets used to collect objects with identical hash values. If too many elements are inserted into a hash table, the number of collisions increases and retrieval performance suffers.

If you know how many elements, approximately, will eventually be in the table, you can set the bucket count. Typically, you should set it to somewhere between 75% and 150% of the expected element count. Some researchers believe that it is a good idea to make the bucket count a prime number to prevent a clustering of keys. The evidence for this isn’t conclusive, however. The standard library uses bucket counts that are powers of 2, with a default of 16. (Any value you supply for the table size is automatically rounded to the next power of 2.)

Of course, you do not always know how many elements you need to store, or your initial guess may be too low. If the hash table gets too full, it needs to be *rehashed*. To rehash the table, a table with more buckets is created, all elements are inserted into the new table, and the original table is discarded. The *load factor* determines when a hash table is rehashed. For example, if the load factor is 0.75 (which is the default) and the table is more than 75% full, it is automatically rehashed with twice as many buckets. For most applications, it is reasonable to leave the load factor at 0.75.

Hash tables can be used to implement several important data structures. The simplest among them is the *set* type. A set is a collection of elements without duplicates. The add method of a set first tries to find the object to be added, and adds it only if it is not yet present.

The Java collections library supplies a `HashSet` class that implements a set based on a hash table. You add elements with the add method. The contains method is redefined to make a fast lookup to see if an element is already present in the set. It checks only the elements in one bucket and not all elements in the collection.

The hash set iterator visits all buckets in turn. Since hashing scatters the elements around in the table, they are visited in a seemingly random order. You would only use a `HashSet` if you don’t care about the ordering of the elements in the collection.

```java
13     {
14         var words = new HashSet<String>();
15         long totalTime = 0;
16
17         try (var in = new Scanner(System.in))
18         {
19             while (in.hasNext())
20             {
21                 String word = in.next();
22                 long callTime = System.currentTimeMillis();
23                 words.add(word);
24                 callTime = System.currentTimeMillis() - callTime;
25                 totalTime += callTime;
26             }
27         }
28
29         Iterator<String> iter = words.iterator();
30         for (int i = 1; i <= 20 && iter.hasNext(); i++)
31             System.out.println(iter.next());
32         System.out.println(". . .");
33         System.out.println(words.size() + " distinct words. " +
                totalTime + " milliseconds.");
34     }
35 }
```

### `java.util.HashSet<E>` 1.2

- `HashSet()`
  constructs an empty hash set.
- `HashSet(Collection<? extends E> elements)`
  constructs a hash set and adds all elements from a collection.
- `HashSet(int initialCapacity)`
  constructs an empty hash set with the specified capacity (number of buckets).
- `HashSet(int initialCapacity, float loadFactor)`
  constructs an empty hash set with the specified capacity and load factor. If the ratio size/capacity exceeds the load factor, the hash table will be rehashed into a larger one.

### `java.lang.Object` 1.0

- `int hashCode()`
  returns a hash code for this object. A hash code can be any integer, positive or negative. The definitions of `equals` and `hashCode` must be compatible: If `x.equals(y)` is true, then `x.hashCode()` must be the same value as `y.hashCode()`.

### 9.3.4 Tree Sets

The `TreeSet` class is similar to the hash set, with one added improvement. A tree set is a *sorted collection*. You insert elements into the collection in any order. When you iterate through the collection, the values are automatically presented in *sorted order*. For example, suppose you insert three strings and then visit all elements that you added.

```java
var sorter = new TreeSet<String>();
sorter.add("Bob");
sorter.add("Amy");
sorter.add("Carl");
for (String s : sorter) System.out.println(s);
```

Then, the values are printed in sorted order: Amy Bob Carl. As the name of the class suggests, the sorting is accomplished by a tree data structure. (The current implementation uses a *red-black tree*. For a detailed description of red-black trees see, for example, *Introduction to Algorithms* by Thomas Cormen, Charles Leiserson, Ronald Rivest, and Clifford Stein, The MIT Press, 2009.) Every time an element is added to a tree, it is placed into its proper sorting position. Therefore, the iterator always visits the elements in sorted order.

Adding an element to a tree is slower than adding it to a hash table—see [Table 9.3](#table-9-3) for a comparison. But it is still much faster than checking for duplicates in an array or linked list. If the tree contains *n* elements, then an average of log₂ *n* comparisons are required to find the correct position for the new element. For example, if the tree already contains 1,000 elements, adding a new element requires about 10 comparisons.

### **NOTE:**

In order to use a tree set, you must be able to compare the elements. The elements must implement the `Comparable` interface, or you must supply a comparator when constructing the set. (The `Comparable` and `Comparator` interfaces were introduced in [Chapter 6](#chapter-6).)

**Table 9.3** Adding Elements into Hash and Tree Sets

| Document | Total Number of Words | Number of Distinct Words | HashSet | TreeSet |
|---|---:|---:|---:|---:|
| *Alice in Wonderland* | 28195 | 5909 | 5 sec | 7 sec |
| *The Count of Monte Cristo* | 466300 | 37545 | 75 sec | 98 sec |

If you look back at [Table 9.3](#table-9-3), you may well wonder if you should always use a tree set instead of a hash set. After all, adding elements does not seem to take much longer, and the elements are automatically sorted. The answer depends on the data that you are collecting. If you don’t need the data sorted, there is no reason to pay for the sorting overhead. More important, with some data it is much more difficult to come up with a sort order than a hash function. A hash function only needs to do a reasonably good job of scrambling the objects, whereas a comparison function must tell objects apart with complete precision.
