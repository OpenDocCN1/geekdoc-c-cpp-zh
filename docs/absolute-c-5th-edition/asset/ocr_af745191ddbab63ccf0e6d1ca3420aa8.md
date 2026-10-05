# CHAPTER 19 Standard Template Library

Display 19.19 Some Modifying Generic Functions (part 2 of 2)

```
//Removes those elements equal to target the range [first, last).
//The size of the container is not changed. The removed values equal to
//target are moved to the end of the range [first, last). There is then
//an iterator i in this range such that all the values not equal to
//target are in [first, i). This is returned. Time complexity: linear
//in the size of the range [first, last).
```

```
template <class BidirectionalIterator>
void reverse(BidirectionalIterator first, BidirectionalIterator last);
//Reverses the order of the elements in the range [first, last).
//Time complexity: linear in the size of the range [first, last].
```

```
template <class RandomAccessIterator>
void random_shuffle(RandomAccessIterator first,
RandomAccessIterator last);
//Uses a pseudorandom number generator to randomly reorder the elements
//in the range [first, last).
//Time complexity: linear in the size of the range [first, last].
```

![](bbox=[0.072, 0.558, 0.196, 0.577])

# Self-Test Exercises

+   22. You can use the random_shuffle template function with a list container.
23. You can use the copy template function with vector containers, even though
copy requires forward iterators and vector has random-access iterators?

# Set Algorithms

Display 19.20 show a sample of the generic operation functions defined in the
STL. Note that generic algorithms assume that the containers store their elements
in sorted order. The containers set, map, multiset, and multimap do store their
elements in sorted order; therefore, all the functions in Display 19.20 apply to these
four template class containers. Other containers, such as vector, do not store their
elements in sorted order; these functions should not be used with such containers.
The reason for requiring that the elements be sorted is so that the algorithms can be\more efficient.