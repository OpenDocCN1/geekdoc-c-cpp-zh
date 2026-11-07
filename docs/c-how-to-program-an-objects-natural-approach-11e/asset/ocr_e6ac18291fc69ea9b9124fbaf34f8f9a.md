# reverse_copy Algorithm

Line 30 calls the C++20 `std::ranges::reverse_copy` algorithm to make a reversed copy of its first argument, `bidirectional_range`. The output iterator supplied as the second argument specifies where to place the copied elements—in this case, the `back_inserter` adds new elements to the vector `results2`, growing it as necessary.

```
```cpp
// copy elements of a1 into results2 in reverse order
std::vector<int> results2{};
std::ranges::reverse_copy(a1, std::back_inserter(results2));
std::cout << "\nAfter reverse_copy, results2 contains: ";
std::ranges::copy(results2, output);
std::cout << "\n";
}
```
```

> After reverse_copy, results2 contains: 9 9 7 7 5 5 3 3 1 1

# 14.4.10 Set Operations

Figure 14.11 demonstrates the C++20 `std::ranges` namespace’s set-manipulation algorithms includes, `set_difference`, `set_intersection`, `set_symmetric_difference` and `set_union`. In addition to the capabilities we show, you can customize each algorithm’s element comparisons by passing a binary predicate function that receives two elements and returns true if the first should be considered less than the second.

```
```cpp
// figure 14.11.cpp
// Algorithms includes, set_difference, set_intersection,
// set_symmetric_difference and set_union.
#include <array>
#include <algorithm>
#include <format>
#include <iostream>
#include <iterator>
#include <vector>

int main() {
    std::array a1{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    std::array a2{4, 5, 6, 7, 8};
    std::array a3{4, 5, 6, 11, 15};
    std::ostream_iterator<int> output{std::cout, " "};

    std::cout << "a1 contains: ";
    std::ranges::copy(a1, output); // display array a1
    std::cout << "\na2 contains: ";
    std::ranges::copy(a2, output); // display array a2
    std::cout << "\na3 contains: ";
    std::ranges::copy(a3, output); // display array a3
}
```
```

**Fig. 14.11** | Algorithms includes, set_difference, set_intersection, set_symmetric_difference and set_union. (Part 1 of 2.)