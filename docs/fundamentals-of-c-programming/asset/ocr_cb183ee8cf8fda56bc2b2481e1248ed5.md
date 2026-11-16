```
int main() {
    std::vector<int> nums { 4, 7, 2, 3, 7, 9, 0, 1, 8 };
    std::cout << "Original vector: " << nums << '\n';

    // Find the first occurrence of 7
    auto del = std::find(std::begin(nums), std::end(nums), 7);
    if (del != nums.end())
        nums.erase(del); // Remove it if we found it

    std::cout << "Vector with 7 removed: " << nums << '\n';
}
```

The following output of Listing 20.25 (removefirst.cpp) shows the first occurrence of 7 absent after the std::find/std::vector::erase combination.

```
Original vector:    {4, 7, 2, 3, 7, 9, 0, 1, 8}
Vector with 7 removed: {4, 2, 3, 7, 9, 0, 1, 8}
```

**std::sort.** In Listing 20.14 (genericlogicalflexiblesort.cpp) we implemented a generic, flexible sorting function named selection_sort. While doing so expanded our development experience and provided insights into C++ generic programming techniques, if we just need to sort a container, we can do so without going to the trouble of writing our own sort function. The STL offers a standard sorting function named std::sort that provides an interface to callers similar to our selection_sort function. The std::sort function is overloaded, and here we will concentrate on two of its overloads. One version accepts two iterators specifying a range within a container, and another specifies the two iterators plus a comparer function that specifies how the elements should be ordered. Listing 20.26 (stdsort.cpp) exercises the std::sort function.

# Listing 20.26: stdsort.cpp

```
#include <iostream>
#include <vector>
#include <algorithm>
#include "vectorprint.h"

/*
 * less_than(a, b)
 *
 * Returns true if a < b; otherwise, returns
 * false.
 */
template <typename T>
bool less_than(const T& a, const T& b) {
    return a < b;
}

/*
 * greater_than(a, b)
 *
 * Returns true if a > b; otherwise, returns
 * false.
 */
template <typename T>
bool greater_than(const T& a, const T& b) {
    return a > b;
}
```