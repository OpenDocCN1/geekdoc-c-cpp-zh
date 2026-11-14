yielding the same results as map. If desired, a user-defined hash function can be provided.

Further reading: All containers provide a customizable allocator that allows us to implement our own memory management or to use platform-specific memory. The allocator interface is given, for instance, in [40], [62].

# 4.1.4 Algorithms

General-purpose STL algorithms are defined in the header <algorithm> and those primarily for number crunching in <numeric>.

# 4.1.4.1 Non-modifying Sequence Operations

find takes three arguments: two iterators that define the right-open interval of the search space, and a value to search for in that range. Each entry referred to by first is compared with value. When a match is found, the iterator pointing to it is returned; otherwise the iterator is incremented. If the value is not contained in the sequence, an iterator equal to last is returned. Thus, the caller can test whether the search was successful by comparing its result with last. This is actually not a particularly difficult task and we could implement this by ourselves:

Click here to view code image

```
template <typename InputIterator, typename T>
InputIterator find(InputIterator first, InputIterator last,
                   const T& value)
{
    while (first != last && *first != value)
        ++first;
    return first;
}
```

This program snippet is indeed the standard way find is realized whereas specialized overloads for special iterators may exist.

```
=> c++11/find_test.cpp
```

As a demonstration we consider a sequence of integer values containing the number 7 twice. We want to write the sub-sequence that starts with the first and ends with the second 7. In other words, we have to find the two