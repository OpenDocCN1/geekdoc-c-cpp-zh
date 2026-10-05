always output. The loop from 0 to 3 performs this experiment multiple times.

The output (on my system, by chance) is this:

```
abcfg
abcde
bdfgh
abefg
```

As you can see, sample ensures that the elements of the sample retain their order.

| 25.6.5 | Algorithms for Partitions | division of a range into two |

subranges based on a predicate. Everything in the left subrange matches the predicate; everything in the right range does not match the predicate. The point between the two is the *partition point*.

The standard library provides a modest selection of algorithms related to partitions. These algorithms are useful in a variety of contexts and can be used to implement highly efficient sorting algorithms in a general manner. The algorithms require that the iterators originate from a container with bidirectional iterators, not necessarily random-access iterators. In fact, a simple form of *quicksort* can be implemented with this type of partition:

+   * is_partitioned
  Usage: occasional; iterators: in
  Checks if a range is already neatly partitioned based on a predicate.