# Display 19.18 Some Nonmodifying Generic Functions (part 2 of 2)

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

# Self-Test Exercises

+   20. Replace all occurrences of the identifier vector with the identifier list in Display 19.17. Compile and run the program.

+   21. Suppose v is an object of the class vector<int>. Use the search generic function (Display 19.18) to write some code to determine whether or not v contains the number 42 immediately followed by 43. You need not give a complete program, but do give all necessary include and using directives.
+   (Hint: It may help to use a second vector.)

# Modifying Sequence Algorithms

Display 19.19 contains descriptions of some of the generic functions in the STL that change the contents of a container in some way.

Remember that adding or removing an element to or from a container can affect any of the other iterators. There is no guarantee that the iterators will be located at the same element after an addition or deletion unless the container template class makes such a guarantee. Of the template classes we have seen, list and slist guarantee that their iterators will not be moved by additions or deletions, except of course if the iterator is located at an element that is removed. The template classes vector and deque make no such guarantee. Some of the function templates in Display 19.19 guarantee the values of some specific iterators; you can, of course, count on those guarantees no matter what the container is.