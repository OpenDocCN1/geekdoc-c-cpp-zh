
## Display 19.17 Some Nonmodifying Generic Functions

These functions all work for forward iterators, which means they also work for bidirectional and random-access iterators. (In some cases they even work for other kinds of iterators that we have not covered in any detail.)

```
template <class ForwardIterator, class T>
ForwardIterator find(ForwardIterator first,
ForwardIterator last, const T& target);
//Traverses the range [first, last) and returns an iterator located at
//the first occurrence of target. Returns last if target is not found.
//Time complexity: linear in the size of the range [first, last).
```

```
template <class ForwardIterator, class T>
int count(ForwardIterator first, ForwardIterator last, const T& target);
//Traverse the range [first, last) and returns the number
//of elements equal to target.
//Time complexity: linear in the size of the range [first, last).
```

```
template <class ForwardIterator1, class ForwardIterator2>
bool equal(ForwardIterator1 first1, ForwardIterator1 last1,
ForwardIterator2 first2);
//Returns true if [first1, last1) contains the same elements in the same order as
//the first last1-first1 elements starting at first2. Otherwise, returns false.
//Time complexity: linear in the size of the range [first, last).
```

```
template <class ForwardIterator1, class ForwardIterator2>
ForwardIterator1 search(ForwardIterator1 first1, ForwardIterator1 last1,
ForwardIterator2 first2, ForwardIterator2 last2);
//Checks to see if [first2, last2) is a subrange of [first1, last1).
//If so, it returns an iterator located in [first1, last1) at the start of
//the first match. Returns last1 if a match is not found.
//Time complexity: quadratic in the size of the range [first1, last1).
```

```
template <class ForwardIterator, class T>
bool binary_search(ForwardIterator first, ForwardIterator last, const T& target);
//Precondition: The range [first, last) is sorted into ascending order using <.
//Uses the binary search algorithm to determine if target is in the range [first,
//last). Time complexity: For random access iterators O(log N). For non-random-
//access iterators linear in N, where N is the size of the range [first, last).
```

## RANGE [FIRST, LAST)

The movement from some iterator first, often container.begin(), up to but not including some location last, often container.end(), is so common it has come to have a special name, range [first, last). For example, the following code outputs all elements in the range [c.begin(), c.end()), where c is some container object, such as a vector:

```
for (iterator p = c.begin(); p != c.end(); p++)
    cout << *p << endl;
```

Notice that there are three search functions in Display 19.17: find, search, and binary_search. The function search searches for a subsequence, while the find and binary_search functions search for a single value. How do you decide whether to use find or binary_search when searching for a single element? One function returns an iterator whereas the other returns just a Boolean value, but that is not the biggest difference. The binary_search function requires that the range being searched be sorted (into ascending order using <) and run in time O(log N), whereas the find function does not require that the range be sorted, but only guarantees linear time. If you have or can have the elements in sorted order, you can search for them much more quickly by using binary_search.

Note that with the binary_search function you are guaranteed that the implementation will use the binary search algorithm, which was discussed in Chapter 13. The importance of using the binary search algorithm is that it guarantees a very fast running time, O(log N). If you have not read Chapter 13 and have not otherwise heard of a binary search, just think of it as a very efficient search algorithm that requires that the elements be sorted. Those are the only two points about binary searches that are relevant to the material in this chapter.

## Self-Test Exercises

- 19. Replace all occurrences of the identifier vector with the identifier list in Display 19.16. Compile and run the program.
- 20. Suppose v is an object of the class vector<int>. Use the search generic function (Display 19.17) to write some code to determine whether or not v contains the number 42 immediately followed by 43. You need not give a complete program, but do give all necessary include and using directives. (Hint: It may help to use a second vector.)

## MODIFYING SEQUENCE ALGORITHMS

Display 19.18 contains descriptions of some of the generic functions in the STL that change the contents of a container in some way.

Remember that adding or removing an element to or from a container can affect any of the other iterators. There is no guarantee that the iterators will be located at the same element after an addition or deletion unless the container template class makes such a guarantee. Of the template classes we have seen, list and slist guarantee that their iterators will not be moved by additions or deletions, except of course if the iterator is located at an element that is removed. The template classes vector and deque make no such guarantee. Some of the function templates in Display 19.18 guarantee the values of some specific iterators; you can, of course, count on those guarantees no matter what the container is.

## Self-Test Exercises

- 21. Can you use the random_shuffle template function with a list container?
- 22. Can you use the copy template function with vector containers, even though copy requires forward iterators and vector has random-access iterators?

## SET ALGORITHMS

Display 19.19 shows a sample of the generic set operation functions defined in the STL. Note that generic algorithms assume that the containers store their elements in sorted order. The containers set, map, multiset, and multimap do store their elements in sorted order; therefore, all the functions in Display 19.19 apply to these four template class containers. Other containers, such as vector, do not store their elements in sorted order; these functions should not be used with such containers. The reason for requiring that the elements be sorted is so that the algorithms can be more efficient.

## Self-Test Exercises

- 23. The mathematics course version of a set does not keep its elements in sorted order, and it has a union operator. Why does the set_union template function require that the containers keep their elements in sorted order?

## Display 19.20 Some Generic Sorting Algorithms

```
template <class RandomAccessIterator>
void sort(RandomAccessIterator first, RandomAccessIterator last);
//Sorts the elements in the range [first, last) into ascending order.
//Time complexity: O(N log N), where N is the size of the range [first, last).
```

```
template <class ForwardIterator1, class ForwardIterator2, class ForwardIterator3>
void merge(ForwardIterator1 first1, ForwardIterator1 last1,
    ForwardIterator2 first2, ForwardIterator2 last2,
    ForwardIterator3 result);

//Precondition: The ranges [first1, last1) and [first2, last2) are sorted.
//Action: Merges the two ranges into a sorted range [result, last3) where
//last3 = result + (last1 - first1) + (last2 - first2).
//Time complexity: linear in the size of the range [first1, last1)
//plus the size of [first2, last2).
```

> Sorting uses the < operator, and so the < operator must be defined. There are other versions, not given here, that allow you to provide the ordering relation. "Sorted" means sorted into ascending order.

## Chapter Summary

- An iterator is a generalization of a pointer. Iterators are used to move through the elements in some range of a container. The operations ++, --, and dereferencing * are usually defined for an iterator.
- Container classes with iterators have member functions end() and begin() that return iterator values such that you can process all the data in the container as follows:
  
  ```
  for (p = c.begin(); p != c.end(); p++)
      process *p //*p is the current data item.
  ```
- The main kinds of iterators are as follows.
  Forward iterators: ++ works on the iterator.
  Bidirectional iterators: Both ++ and -- work on the iterator.
  Random-access iterators: ++, --, and random access all work with the iterator.
- With a constant iterator p, the dereferencing operator *p produces a read-only version of the element. With a mutable iterator p, *p can be assigned a value.
- A bidirectional container has reverse iterators that allow your code to cycle through the elements in the container in reverse order.
