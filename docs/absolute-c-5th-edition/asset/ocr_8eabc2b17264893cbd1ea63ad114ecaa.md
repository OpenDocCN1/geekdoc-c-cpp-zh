# Self-Test Exercises

20. Replace all occurrences of the identifier vector with the identifier list in Display 19.17. Compile and run the program.

21. Suppose v is an object of the class vector<int>. Use the search generic function (Display 19.18) to write some code to determine whether or not v contains the number 42 immediately followed by 43. You need not give a complete program, but do all necessary include and using directives. (Hint: It may help you to use a second vector.)

# Generic Sequence Algorithms

Display 19.19 contains descriptions of some of the generic functions in the STL that change the contents of a container in some way. Remember that adding or removing an element to or from a container can affect any of the other iterators. There is no guarantee that the iterators will be located at the same element after deletion unless the template class makes a guarantee. Of the template classes we have seen, list and enlist guarantee that their iterators will not be moved by additions or deletions, except in case of the iterator is located at an element that is removed. The template classes vector and deque make no guarantee. Some of the function templates in Display 19.19 guarantee the values of some specific iterators; you can, of course, count on those guarantees no what the container is.

Display 19.19 Some Generic Functions (part 1 of 2)

```
template<class T>
void swap(T& variable1, T& variable2);
//Interchanges the values of variable1 and variable2.
```

> The type of iterator parameter tells the kind of iterator for which the function works. Remember that these are minimum iterator requirements. For example, ForwardIterator works for forward iterators, bidirectional, and random-access iterators.

```
template<class ForwardIterator1, class ForwardIterator2>
ForwardIterator2 copy(ForwardIterator1 first1, ForwardIterator1 last1,
//last2 is such that the range [first1, last1) and (first2, last2) is
the same size.
//Action: Copies the elements at locations [first1, last1) to
//locations [first2, last2). Returns last2.
//Time complexity: linear in the size of the range [first1, last1].
template<class ForwardIterator, class T>
ForwardIterator remove(ForwardIterator first,
const T& target);
```

(continued)