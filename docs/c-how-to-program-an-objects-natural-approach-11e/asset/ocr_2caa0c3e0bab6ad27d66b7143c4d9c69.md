sponding elements from each `input_range` to its function argument, then outputs the function's result via the `output iterator`.

# 14.4.6 Searching and Sorting Algorithms

Figure 14.7 demonstrates some basic searching and sorting algorithms, including `find`, `find_if`, `sort`, `binary_search`, `all_of`, `any_of`, `none_of` and `find_if_not` from C++20’s `std::ranges` namespace.

```
```cpp
// fig14_07.cpp
// Standard library search and sort algorithms.
#include <algorithm> // algorithm definitions
#include <array> // array class-template definition
#include <iostream>
#include <iterator>

int main() {
    std::array values{10, 2, 17, 5, 16, 8, 13, 11, 20, 7};
    std::ostream_iterator<int> output{std::cout, " "};

    std::cout << "values contains: ";
    std::ranges::copy(values, output); // display output vector
}
```
```

`values contains: 10 2 17 5 16 8 13 11 20 7`

**Fig. 14.7** | Standard library search and sort algorithms.

# Find Algorithm

The C++20 `std::ranges::find` algorithm (line 16) performs an O(n) linear search to find a value (16) in its `input_range` argument (`values`). The algorithm returns an iterator positioned at the first element containing the value; otherwise, it returns the range’s sentinel (demonstrated by lines 24–29). We use the returned iterator in line 17 to calculate the index position at which the value was found.

```
```cpp
// locate first occurrence of 16 in values
if (auto loc1{std::ranges::find(values, 16)}; loc1 != values.cend()) {
    std::cout << "\nFound 16 at index: " << (loc1 - values.cbegin());
}
else { // 16 not found
    std::cout << "\n16 not found";
}

// locate first occurrence of 100 in values
if (auto loc2{std::ranges::find(values, 100)}; loc2 != values.cend()) {
    std::cout << "\nFound 100 at index: " << (loc2 - values.cbegin());
}
else { // 100 not found
    std::cout << "\n100 not found";
}
```
```