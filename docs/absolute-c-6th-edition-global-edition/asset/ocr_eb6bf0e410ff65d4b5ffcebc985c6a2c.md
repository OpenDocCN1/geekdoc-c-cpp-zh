# Display 19.20 Set Operations (part 2 of 2)

```
template <class ForwardIterator1, class ForwardIterator2,
class ForwardIterator3>
void set_difference(ForwardIterator1 first1, ForwardIterator1 last1,
ForwardIterator2 first2, ForwardIterator2 last2,
ForwardIterator3 result);
//Creates a sorted set difference of the two ranges [first1, last1) and
//[first2, last2). The difference consists of the elements in the first
//range that are not in the second. The result is stored starting at
//result. Time complexity: linear in the size of [first1, last1) plus
//[first2, last2).
```

# Self-Test Exercise

24. The mathematics course version of a set does not keep its elements in sorted order, and it has a union operator. Why does the set_union template function require that the containers keep their elements in sorted order?

# Sorting Algorithms

Display 19.21 gives the declarations and documentation for two template functions: one to sort a range of elements and one to merge two sorted ranges of elements. Note that the sorting function sort guarantees a running time of O(N log N). Although it is beyond the scope of this book, it can be shown that you cannot write a sorting algorithm that is faster than O(N log N). So, this function guarantees that the sorting algorithm is as fast as possible, up to a constant multiple.

# Display 19.21 Some Generic Sorting Algorithms

```
template <class RandomAccessIterator>
void sort(RandomAccessIterator first, RandomAccessIterator last);
//Sorts the elements in the range [first, last) into ascending order.
//Time complexity: O(N log N), where N is the size of the range [first,
//last).
```

```
template <class ForwardIterator1, class ForwardIterator2,
class ForwardIterator3>
void merge(ForwardIterator1 first1, ForwardIterator1 last1,
ForwardIterator2 first2, ForwardIterator2 last2,
ForwardIterator3 result);
//Precondition: The ranges [first1, last1) and [first2, last2) are
//sorted.
//Action: Merges the two ranges into a sorted range [result, last3)
//where last3 = result + (last1 - first1) + (last2 - first2).
//Time complexity: linear in the size of the range [first1, last1)
//plus the size of [first2, last2).
Sorting uses the < operator, and so the < operator must be defined.
There are other versions, not given here, that allow you to provide the ordering relation.
"Sorted" means sorted into ascending order.
```