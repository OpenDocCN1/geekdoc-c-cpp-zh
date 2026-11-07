```
```cpp
// determine which argument is the min and which is the max
auto [smaller, larger]{std::minmax(12, 7)};
std::cout << "\nMinimum of 12 and 7 is: " << smaller
          << "\nMaximum of 12 and 7 is: " << larger;
```
```

```
```
Minimum of 12 and 7 is: 7
Maximum of 12 and 7 is: 12
```
```

# ### minmax Algorithm for C++20 Ranges

The C++20 **std::ranges::minmax** algorithm (line 25) returns a pair of values containing the minimum and maximum items in its **input_range** or **initializer_list** argument. Again, we used structured bindings to unpack these values into **smallest** and **largest**, respectively. You also can pass as a second argument a binary predicate function for comparing elements to determine whether the first should be considered less than the second.

```
```cpp
std::array items{3, 100, 52, 77, 22, 31, 98, 13, 40};
std::ostream_iterator<int> output{std::cout, " "};

std::cout << "\nitems: ";
std::ranges::copy(items, output);

auto [smallest, largest]{std::ranges::minmax(items)};
std::cout << "\nMinimum value in items: " << smallest
          << "\nMaximum value in items is: " << largest << "\n";
```
```

```
```
items: 3 100 52 77 22 31 98 13 40
Minimum value in items: 1
Maximum value in items is: 100
```
```

# ## 14.4.13 Algorithms gcd, lcm, iota, reduce and partial_sum from Header <numeric>

Section 8.19.2 introduced the **accumulate** algorithm (header **<numeric>**). Figure 14.14 demonstrates **<numeric>** algorithms **gcd**, **lcm**, **iota**, **reduce** and **partial_sum**. This header’s algorithms require common ranges and are expected to have ranges overloads in C++23.

# ### gcd Algorithm

The gcd algorithm (lines 14 and 15) receives two integer arguments and returns their **greatest common divisor**.