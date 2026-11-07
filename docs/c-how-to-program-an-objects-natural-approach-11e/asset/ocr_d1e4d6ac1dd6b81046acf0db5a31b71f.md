```
set_union of al and a3 is: 1 2 3 4 6 7 8 9 10 11 15
```

# 14.4.1 lower_bound, upper_bound and equal_range

Figure 14.12 demonstrates the algorithms **lower_bound**, **upper_bound** and **equal_range** from C++20’s `std::ranges` namespace. In addition to the capabilities we show, you can customize each algorithm’s element comparisons by passing a binary predicate function that receives two elements and returns true if the first should be considered less than the second.

```
```cpp
// fig14_12.cpp
// Algorithms lower_bound, upper_bound and
// equal_range for a sorted sequence of values.
#include <algorithm>
#include <array>
#include <iostream>
#include <iterator>

int main() {
   std::array values{2, 2, 4, 4, 4, 6, 6, 6, 8};
   std::ostream_iterator<int> output{std::cout, " "};
   std::cout << "values contains: ";
   std::ranges::copy(values, output);
}
```
```

```
values contains: 2 2 4 4 4 6 6 6 8
```

**Fig. 14.12** | Algorithms lower_bound, upper_bound and equal_range for a sorted sequence of values.

# lower_bound Algorithm

Line 17 calls the C++20 `std::ranges::lower_bound` algorithm to find in a sorted forward_range the first location at which the second argument could be inserted such that the range would still be sorted in ascending order. The algorithm returns an iterator pointing to that location.

Concepts

```
```cpp
// determine lower-bound insertion point for 6 in values
auto lower{std::ranges::lower_bound(values, 6)};
std::cout << "\nLower bound of 6 is index:"
   << (lower - values.begin());
```
```

```
Lower bound of 6 is index: 5
```