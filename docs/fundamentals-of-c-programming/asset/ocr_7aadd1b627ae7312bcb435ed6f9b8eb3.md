```
// Is it possible to avoid iterators?
for_each(vec, [&sum](int x) { sum += x; });
```

rather than

```
for_each(std::begin(vec), std::end(vec), [&sum](int x) { sum += x; });
```

Why did the creators of the STL design the algorithms in this way? Iterators make the algorithms more flexible. What if you wish to double the elements in just the first half of a vector of integers and leave the elements in the second half of the vector unchanged? Listing 20.21 (doublefirsthalf.cpp) shows how this can be done.

# Listing 20.21: doublefirsthalf.cpp

```
#include <iostream>
#include <vector>
#include <algorithm>
#include "vectprint.h"

void twice(int& n) {
    n *= 2;
}

int main() {
    std::vector<int> vec { 10, 20, 30, 40, 50, 60, 70, 80 };
    std::cout << "Before: " << vec << '\n';
    // Only double the elements in the first half of the vector
    std::for_each(std::begin(vec), std::begin(vec) + vec.size()/2, twice);
    std::cout << "After: " << vec << '\n';
}
```

Listing 20.21 (doublefirsthalf.cpp) prints the following:

```
Before: {10, 20, 30, 40, 50, 60, 70, 80}
After: {20, 40, 60, 80, 50, 60, 70, 80}
```

Most often programmers will apply an STL algorithm to all the contents of the container, but the iterator interface enables programmers to reduce the algorithm's application to a smaller range of elements if the problem at hand requires it.

The other reason for using iterators is that the algorithm developer can treat an iterator like a primitive pointer variable within the algorithm's function. The * operator applied to an iterator object accesses the current element which the iterator references, and the ++ operator applied to an iterator moves the iterator to the next element in the container. For the purposes of writing the function, it is not necessary to know if the sequence actually is a std::vector, std::list, or primitive statically allocated array. To demonstrate, consider the following function:

```
template <typename Iter>
void ten_times(Iter begin, Iter end) {
    auto cursor = begin;
    while (cursor != end) {
        *cursor *= 10;
        cursor++;
    }
}
```