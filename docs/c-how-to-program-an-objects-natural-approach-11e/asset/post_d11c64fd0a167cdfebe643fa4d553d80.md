
```text
set_union of a1 and a3 is: 1 2 3 4 6 7 8 9 10 11 15
```

## 14.4.1 lower_bound, upper_bound and equal_range

Figure 14.12 demonstrates the algorithms **lower_bound**, **upper_bound** and **equal_range** from C++20’s `std::ranges` namespace. In addition to the capabilities we show, you can customize each algorithm’s element comparisons by passing a binary predicate function that receives two elements and returns true if the first should be considered less than the second.

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

```text
values contains: 2 2 4 4 4 6 6 6 8
```

**Fig. 14.12** | Algorithms lower_bound, upper_bound and equal_range for a sorted sequence of values.

### lower_bound Algorithm

Line 17 calls the C++20 `std::ranges::lower_bound` algorithm to find in a sorted forward_range the first location at which the second argument could be inserted such that the range would still be sorted in ascending order. The algorithm returns an iterator pointing to that location.

Concepts

```cpp
// determine lower-bound insertion point for 6 in values
auto lower{std::ranges::lower_bound(values, 6)};
std::cout << "\nLower bound of 6 is index:"
   << (lower - values.begin());
```

```text
Lower bound of 6 is index: 5
```

### upper_bound Algorithm

Line 22 calls the C++20 **std::ranges::upper_bound** algorithm to find in a sorted **forward_range** the last location at which the second argument could be inserted so the range would still be sorted. The algorithm returns an iterator pointing to that location.

```cpp
// determine upper-bound insertion point for 6 in values
auto upper{std::ranges::upper_bound(values, 6)};
std::cout << "\nUpper bound of 6 is index: "
          << (upper - values.begin());
```

```text
Upper bound of 6 is index: 9
```

### equal_range Algorithm

The C++20 **std::ranges::equal_range** algorithm (line 27) performs the **lower_bound** and **upper_bound** operations, then returns their results as a **std::ranges::subrange**, which we unpack into variables first and last.

```cpp
// use equal_range to determine the lower and upper bound of 6
auto [first, last]{std::ranges::equal_range(values, 6)};
std::cout << "\nUsing equal_range:\n Lower bound of 6 is index: "
          << (first - values.begin());
std::cout << "\n Upper bound of 6 is index: "
          << (last - values.begin());
```

```text
Using equal_range:
  Lower bound of 6 is index: 5
  Upper bound of 6 is index: 9
```

### Locating Insertion Points in Sorted Sequences

Algorithms **lower_bound**, **upper_bound** and **equal_range** are often used to locate a new value’s insertion point in a sorted sequence. Line 36 uses **lower_bound** to locate the first position where 3 can be inserted in order in values. Line 43 uses **upper_bound** to locate the last position where 7 can be inserted in order in values.

```cpp
// determine lower-bound insertion point for 3 in values
std::cout << "\nLower bound to locate the first point "
          << "at which 3 can be inserted in order";
lower = std::ranges::lower_bound(values, 3);
std::cout << "\n  Lower bound of 3 is index: "
          << (lower - values.begin());

// determine upper-bound insertion point for 7 in values
std::cout << "\n\nUse upper_bound to locate the last point "
          << "at which 7 can be inserted in order";
upper = std::ranges::upper_bound(values, 7);
std::cout << "\n  Upper bound of 7 is index: "
          << (upper - values.begin()) << "\n";
}
```

```text
Use `lower_bound` to locate the first point at which 3 can be inserted in order
Lower bound of 3 is index: 2

Use `upper_bound` to locate the last point at which 7 can be inserted in order
Upper bound of 7 is index: 9
```

## 14.4.12 min, max and minmax

Figure 14.13 demonstrates algorithms `min`, `max` and `minmax` from the `std` namespace and the `minmax` overload from C++20's `std::ranges` namespace. Unlike the algorithms we presented in Section 14.4.5, which operated on ranges, the `std` namespace's `min`, `max` and `minmax` algorithms operate on two values passed as arguments. The `std::ranges::minmax` algorithm returns the minimum and maximum values in a range.

### Algorithms `min` and `max` with Two Parameters

The `min` and `max` algorithms (lines 8–12) each receive two arguments and return the minimum or maximum value. Each algorithm also has an overload that takes as a third argument a binary predicate function for custom comparisons determining whether the first argument should be considered less than the second.

```cpp
    1  // fig14_13.cpp
    2  // Algorithms min, max and minmax.
    3  #include <array>
    4  #include <algorithm>
    5  #include <iostream>

    7  int main() {
    8      std::cout << "Minimum of 12 and 7 is: " << std::min(12, 7)
    9          << "\nMaximum of 12 and 7 is: " << std::max(12, 7)
    10         << "\nMinimum of 'G' and 'Z' is: " << std::min('G', 'Z') << '\n'
    11         << "\nMaximum of 'G' and 'Z' is: " << std::max('G', 'Z') << '\n'
    12         << "\nMinimum of 'z' and 'Z' is: " << std::min('z', 'Z') << '\n';
    13 }
```

```text
    Minimum of 12 and 7 is: 7
    Maximum of 12 and 7 is: 12
    Minimum of 'G' and 'Z' is: 'G'
    Maximum of 'G' and 'Z' is: 'Z'
    Minimum of 'z' and 'Z' is: 'Z'
```

**Fig. 14.13** | Algorithms `min`, `max` and `minmax`.

### `minmax` Algorithm with Two Arguments

The two-argument `minmax` algorithm (line 15) returns a pair of values containing the smaller and larger items, respectively. Here we used structured bindings to unpack the values into smaller and larger. A second version of `minmax` takes as a third argument a binary predicate function for a custom comparison determining whether the first argument should be considered less than the second.

```cpp
// determine which argument is the min and which is the max
auto [smaller, larger]{std::minmax(12, 7)};
std::cout << "\nMinimum of 12 and 7 is: " << smaller
          << "\nMaximum of 12 and 7 is: " << larger;
```

```text
Minimum of 12 and 7 is: 7
Maximum of 12 and 7 is: 12
```

### minmax Algorithm for C++20 Ranges

The C++20 **std::ranges::minmax** algorithm (line 25) returns a pair of values containing the minimum and maximum items in its **input_range** or **initializer_list** argument. Again, we used structured bindings to unpack these values into **smallest** and **largest**, respectively. You also can pass as a second argument a binary predicate function for comparing elements to determine whether the first should be considered less than the second.

```cpp
std::array items{3, 100, 52, 77, 22, 31, 98, 13, 40};
std::ostream_iterator<int> output{std::cout, " "};

std::cout << "\nitems: ";
std::ranges::copy(items, output);

auto [smallest, largest]{std::ranges::minmax(items)};
std::cout << "\nMinimum value in items: " << smallest
          << "\nMaximum value in items is: " << largest << "\n";
```

```text
items: 3 100 52 77 22 31 98 13 40
Minimum value in items: 3
Maximum value in items is: 100
```

## 14.4.13 Algorithms gcd, lcm, iota, reduce and partial_sum from Header <numeric>

Section 8.19.2 introduced the **accumulate** algorithm (header **<numeric>**). Figure 14.14 demonstrates **<numeric>** algorithms **gcd**, **lcm**, **iota**, **reduce** and **partial_sum**. This header’s algorithms require common ranges and are expected to have ranges overloads in C++23.

### gcd Algorithm

The gcd algorithm (lines 14 and 15) receives two integer arguments and returns their **greatest common divisor**.

```cpp
// Fig14_14.cpp
// Demonstrating algorithms gcd, lcm, iota, reduce and partial_sum.
#include <array>
#include <algorithm>
#include <functional>
#include <iostream>
#include <iterator>
#include <numeric>

int main() {
    std::ostream_iterator<int> output{std::cout, " "};

    // calculate the greatest common divisor of two integers
    std::cout << "std::gcd(75, 20): " << std::gcd(75, 20)
              << "\nstd::gcd(17, 13): " << std::gcd(17, 13);
}
```

```text
std::gcd(75, 20): 5
std::gcd(17, 13): 1
```

**Fig. 14.14** | Demonstrating algorithms gcd, lcm, iota, reduce and partial_sum.

### lcm Algorithm

The lcm algorithm (lines 18 and 19) receives two integer arguments and returns their least common multiple.

```cpp
// calculate the least common multiple of two integers
std::cout << "\nstd::lcm(3, 5): " << std::lcm(3, 5)
          << "\nstd::lcm(12, 9): " << std::lcm(12, 9);
```

```text
std::lcm(3, 5): 15
std::lcm(12, 9): 36
```

### iota Algorithm

The iota algorithm (line 23) fills a common range with a sequence of values starting with the value in the third argument. The first two arguments must be forward iterators representing a common range to fill. The last argument's type must support the ++ operator.

```cpp
// fill an array with integers using the std::iota algorithm
std::array<int, 5> ints{};
std::iota(ints.begin(), ints.end(), 1);
std::cout << "\nints: ";
std::ranges::copy(ints, output);
```

```text
ints: 1 2 3 4 5
```
