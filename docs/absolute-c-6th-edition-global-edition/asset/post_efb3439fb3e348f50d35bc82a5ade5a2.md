
## Display 19.18 Some Nonmodifying Generic Functions (part 2 of 2)

```
template <class ForwardIterator1, class ForwardIterator2>
ForwardIterator1 search(ForwardIterator1 first1, ForwardIterator1 last1,
    ForwardIterator2 first2, ForwardIterator2 last2);
//Checks to see if [first2, last2) is a subrange of [first1, last1).
//If so, it returns an iterator located in [first1, last1) at the start
//of the first match. Returns last1 if a match is not found.
//Time complexity: quadratic in the size of the range [first1, last1).
```

```
template <class ForwardIterator, class T>
bool binary_search(ForwardIterator first, ForwardIterator last,
    const T& target);
//Precondition: The range [first, last) is sorted into ascending order
//using <.
//Uses the binary search algorithm to determine if target is in the
//range [first, last).
//Time complexity: For random-access iterators O(log N). For nonrandom-
//access iterators linear in N, where N is the size of the range [first,
//last).
```

## Self-Test Exercises

- 20. Replace all occurrences of the identifier vector with the identifier list in Display 19.17. Compile and run the program.
- 21. Suppose v is an object of the class vector<int>. Use the search generic function (Display 19.18) to write some code to determine whether or not v contains the number 42 immediately followed by 43. You need not give a complete program, but do give all necessary include and using directives.
+   (Hint: It may help to use a second vector.)

## Modifying Sequence Algorithms

Display 19.19 contains descriptions of some of the generic functions in the STL that change the contents of a container in some way.

Remember that adding or removing an element to or from a container can affect any of the other iterators. There is no guarantee that the iterators will be located at the same element after an addition or deletion unless the container template class makes such a guarantee. Of the template classes we have seen, list and slist guarantee that their iterators will not be moved by additions or deletions, except of course if the iterator is located at an element that is removed. The template classes vector and deque make no such guarantee. Some of the function templates in Display 19.19 guarantee the values of some specific iterators; you can, of course, count on those guarantees no matter what the container is.

## Display 19.19 Some Modifying Generic Functions

```
template <class T>
void swap(T& variable1, T& variable2);
//Interchanges the values of variable1 and variable2.
```

The name of the iterator type parameter tells the kind of iterator for which the function works. Remember that these are minimum iterator requirements. For example, ForwardIterator works for forward iterators, bidirectional iterators, and random-access iterators.

```
template <class ForwardIterator1, class ForwardIterator2>
ForwardIterator2 copy(ForwardIterator1 first1, ForwardIterator1 last1,
ForwardIterator2 first2);
//last2 is such that the ranges [first1, last1) and [first2, last2) are
//the same size.
//Action: Copies the elements at locations [first1, last1) to
//locations [first2, last2). Returns last2.
//Time complexity: linear in the size of the range [first1, last1].
```

```
template <class ForwardIterator, class T>
ForwardIterator remove(ForwardIterator first, ForwardIterator last,
const T& target);
//Removes those elements equal to target from the range [first, last).
//The size of the container is not changed. The removed values equal to
//target are moved to the end of the range [first, last). There is then
//an iterator i in this range such that all the values not equal to
//target are in [first, i). This i is returned. Time complexity: linear
//in the size of the range [first, last).
```

```
template <class BidirectionalIterator>
void reverse(BidirectionalIterator first, BidirectionalIterator last);
//Reverses the order of the elements in the range [first, last).
//Time complexity: linear in the size of the range [first, last).
```

```
template <class RandomAccessIterator>
void random_shuffle(RandomAccessIterator first,
RandomAccessIterator last);
//Use a pseudorandom number generator to randomly reorder the elements
//in the range [first, last).
//Time complexity: linear in the size of the range [first, last).
```

## Self-Test Exercises

- 22. Can you use the random_shuffle template function with a list container?
- 23. Can you use the copy template function with vector containers, even though copy requires forward iterators and vector has random-access iterators?

## Display 19.20 Set Operations (part 2 of 2)

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

## Self-Test Exercise

24. The mathematics course version of a set does not keep its elements in sorted order, and it has a union operator. Why does the set_union template function require that the containers keep their elements in sorted order?

## Sorting Algorithms

Display 19.21 gives the declarations and documentation for two template functions: one to sort a range of elements and one to merge two sorted ranges of elements. Note that the sorting function sort guarantees a running time of O(N log N). Although it is beyond the scope of this book, it can be shown that you cannot write a sorting algorithm that is faster than O(N log N). So, this function guarantees that the sorting algorithm is as fast as possible, up to a constant multiple.

## Display 19.21 Some Generic Sorting Algorithms

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

## Chapter Summary

- An *iterator* is a generalization of a pointer. Iterators are used to move through the elements in some range of a container. The operations ++, --, and dereferencing * are usually defined for an iterator.
- *Container classes* with iterators have member functions `end()` and `begin()` that return iterator values such that you can process all the data in the container as follows:
  
  ```
  for (p = c.begin(); p != c.end(); p++)
      process *p //*p is the current data item.
  ```
- The main kinds of iterators are as follows:
  Forward iterators: ++ works on the iterator.
  Bidirectional iterators: Both ++ and -- work on the iterator.
  Random-access iterators: ++, --, and random access all work with the iterator.
- With a *constant iterator* p, the dereferencing operator *p produces a read-only version of the element. With a *mutable iterator* p, *p can be assigned a value.
- A bidirectional container has reverse iterators that allow your code to cycle through the elements in the container in reverse order.
- The main container template classes in the STL are `list`, which has mutable bidirectional iterators; and the template classes `vector` and `deque`, both of which have mutable random-access iterators.
- `stack` and `queue` are container adapter classes, which means they are built on top of other container classes. A `stack` is a last-in/first-out container. A `queue` is a first-in/first-out container.
- The `set`, `map`, `multiset`, and `multimap` container template classes store their elements in sorted order for efficiency of search algorithms. A `set` is a simple collection of elements. A `map` allows storing and retrieving by key values. The `multiset` class allows repetitions of entries. The `multimap` class allows a single key to be associated with multiple data items.
- The STL includes template functions to implement generic algorithms with guarantees on their maximum running time.

## Answers to Self-Test Exercises

- 1. `v.begin()` returns an iterator located at the first element of v. `v.end()` returns a value that serves as a sentinel value at the end of all the elements of v.
- 2. *p is the dereferencing operator applied to p. *p is a reference to the element at location p.
