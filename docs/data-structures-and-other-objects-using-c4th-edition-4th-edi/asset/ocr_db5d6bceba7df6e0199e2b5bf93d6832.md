At this point, we can find the first occurrence of "dog" and the first item after all the dogs, like this:

```
vector<string>::iterator first_dog =
    = lower_bound(pets.begin( ), pets.end( ), "dog");
vector<string>::iterator after_dog =
    = upper_bound(pets.begin( ), pets.end( ), "dog");
```

At this point in the code, *first_dog will be the first occurrence of "dog" and *after_dog will be "fish".

By the way, the only time that lower_bound and upper_bound return the same iterator is when the target does not appear in the sorted range. The technique used by both of these functions is a binary search, so their behavior is guaranteed to be logarithmic in the size of the range.

# Functions for Unsorted Ranges

The STL find and count functions work with any STL sequence class that has an iterator, regardless of whether the sequence is sorted. Note that some containers, such as set and map, implement their own versions of the find and count functions. The prototypes for these functions are

```
difference_type count
(Iterator first, Iterator last, const Item& target);
iterator find
(Iterator first, Iterator last, const Item& target);
```

The count function's return type is a special integer type that allows the computer to store integers that might be too large for an int. The return value of the count function is the number of times that the target value appears in the range [first..last). It uses the == operator of the Item type to determine whether an item is equal to the target.

The find function returns an iterator that refers to the first occurrence of the target. If the target is not found, the last iterator is returned. The find and count functions may be used with any of the STL container classes or with arrays. Even the STL string class can be searched with these functions, as shown in Figure 12.3.

# The STL search Function

An STL function called search can be used to determine whether a copy of one sequence (determined by two iterators, [target_first..target_last)) occurs as a contiguous piece somewhere within a second sequence (determined by two other iterators, [first..last)). The prototype is shown here: