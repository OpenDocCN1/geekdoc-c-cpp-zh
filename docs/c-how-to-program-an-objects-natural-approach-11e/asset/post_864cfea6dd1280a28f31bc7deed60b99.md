
```text
Found 16 at index: 4
100 not found
```

### find_if Algorithm

The C++20 `std::ranges::find_if` algorithm (line 35) performs an *O(n)* linear search to locate the first value in its input range argument (values) for which a unary predicate function (`isGreaterThan10` from line 32) returns true. The algorithm returns an iterator positioned at the first element containing a value for which the predicate function returns true; otherwise, it returns the range’s sentinel.

```cpp
// create variable to store lambda for reuse later
auto isGreaterThan10([](auto x){return x > 10;});

// locate first occurrence of value greater than 10 in values
auto loc3(std::ranges::find_if(values, isGreaterThan10));

if (loc3 != values.cend()) { // found value greater than 10
    std::cout << "\n\nFirst value greater than 10: " << *loc3
              << "\nfound at index: " << (loc3 - values.cbegin());
} else { // value greater than 10 not found
    std::cout << "\n\nNo values greater than 10 were found";
}
```

```text
First value greater than 10: 17
found at index: 3
```

### sort Algorithm

The C++20 `std::ranges::sort` algorithm (line 46) performs an *O(n log n)* sort that arranges the elements in its argument values into ascending order. The argument must be a `random_access_range`, which supports `random_access_iterators` and thus can be used with the containers array, vector or deque (and with built-in arrays). This algorithm also can receive a binary predicate function taking two arguments and returning a bool indicating the sorting order. The predicate compares two values from the sequence being sorted. If the binary predicate returns true, the two elements are already in sorted order; otherwise, the two elements need to be reordered in the sequence.

```cpp
// sort elements of values
std::ranges::sort(values);
std::cout << "\n\nvalues after sort: ";
std::ranges::copy(values, output);
```

```text
values after sort: 2 5 7 8 10 11 13 16 17 20
```

### binary_search Algorithm

The C++20 `std::ranges::binary_search` algorithm (line 51) performs an `O(log n)` binary search to determine whether the value 13 is in the `forward_range` argument (values). The range must be sorted in ascending order. The algorithm returns a `bool` indicating whether the value was found in the sequence. Line 59 demonstrates a call to `binary_search` for which the value is not found. This algorithm also can receive a binary predicate function that takes two arguments and returns a `bool`. The function should return `true` if the two elements being compared are in sorted order. If you need to know the search key's location in the container, use the `lower_bound` or `find` algorithms rather than `binary_search`.

```cpp
// use binary_search to check whether 13 exists in values
if (std::ranges::binary_search(values, 13)) {
    std::cout << "\n13 was found in values";
}
else {
    std::cout << "\n13 was not found in values";
}

// use binary_search to check whether 100 exists in values
if (std::ranges::binary_search(values, 100)) {
    std::cout << "\n100 was found in values";
}
else {
    std::cout << "\n100 was not found in values";
}
```

```text
13 was found in values
100 was not found in values
```

### all_of Algorithm

The C++20 `std::ranges::all_of` algorithm (line 67) performs an `O(n)` linear search to determine whether the unary predicate function in its second argument (in this case, the lambda `isGreaterThan10`) returns `true` for all of the elements in its `input_range` argument (values). If so, `all_of` returns `true`; otherwise, it returns `false`.

```cpp
// determine whether all of values' elements are greater than 10
if (std::ranges::all_of(values, isGreaterThan10)) {
    std::cout << "\nAll values elements are greater than 10";
}
else {
    std::cout << "\nSome values elements are not greater than 10";
}
```

```text
Some values elements are not greater than 10
```

### any_of Algorithm

The C++20 `std::ranges::any_of` algorithm (line 75) performs an *O(n)* linear search to determine whether the unary predicate function in its second argument (in this case, the lambda `isGreaterThan10`) returns true for at least one element in its `input_range` argument (values). If so, `any_of` returns true; otherwise, it returns false.

```cpp
// determine whether any of values' elements are greater than 10
if (std::ranges::any_of(values, isGreaterThan10)) {
    std::cout << "\n\nSome values elements are greater than 10";
}
else {
    std::cout << "\n\nNo values elements are greater than 10";
}
```

```text
Some values elements are greater than 10
```

### none_of Algorithm

The C++20 `std::ranges::none_of` algorithm (line 83) performs an *O(n)* linear search to determine whether the unary predicate function in its second argument (in this case, the lambda `isGreaterThan10`) returns false for all of the elements in its `input_range` argument (values). If so, `none_of` returns true; otherwise, it returns false.

```cpp
// determine whether none of values' elements are greater than 10
if (std::ranges::none_of(values, isGreaterThan10)) {
    std::cout << "\n\nNo values elements are greater than 10";
}
else {
    std::cout << "\n\nSome values elements are greater than 10";
}
```

```text
Some values elements are greater than 10
```

### find_if_not Algorithm

The C++20 `std::ranges::find_if_not` algorithm (line 91) performs an *O(n)* linear search to locate the first value in its `input_range` argument (values) for which a unary predicate function (the lambda `isGreaterThan10`) returns false. The algorithm returns an iterator that’s positioned at the first element containing a value for which the predicate function returns false; otherwise, it returns the range’s sentinel.

```cpp
// locate first occurrence of value that is not greater than 10
auto loc4{std::ranges::find_if_not(values, isGreaterThan10)};

if (loc4 != values.cend()) { // found a value less than or equal to 10
    std::cout << "\n\nFirst value not greater than 10: " << *loc4
              << "\nfound at index: " << (loc4 - values.begin());
}
else { // no values less than or equal to 10 were found
    std::cout << "\n\nOnly values greater than 10 were found";
}

std::cout << "\n";
}
```

```text
First value not greater than 10: 2
found at index: 0
```

## 14.4.7 swap, iter_swap and swap_ranges

Figure 14.8 demonstrates algorithms for swapping elements—**swap** and **iter_swap** from the std namespace and algorithm **swap_ranges** from C++20’s **std::ranges** namespace.

```cpp
// fig14_08.cpp
// Algorithms swap, iter_swap and swap_ranges.
#include <algorithm>
#include <array>
#include <iostream>
#include <iterator>

int main() {
    std::array values{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    std::ostream_iterator<int> output{std::cout, " "};

    std::cout << "values contains: ";
    std::ranges::copy(values, output);
```

```text
values contains: 1 2 3 4 5 6 7 8 9 10
```

**Fig. 14.8** | Algorithms swap, iter_swap and swap_ranges.

### swap Algorithm

Line 15 uses the `std::swap` algorithm to exchange its two arguments’ values—this is not a range or common-range algorithm. The function receives references to the two values being exchanged. In this case, we pass references to the array’s first and second elements.

```cpp
std::swap(values[0], values[1]); // swap elements at index 0 and 1

std::cout << "\nafter std::swap of values[0] and values[1]: ";
std::ranges::copy(values, output);
```

```text
after std::swap of values[0] and values[1]: 2 1 3 4 5 6 7 8 9 10
```

### iter_swap Algorithm

Line 21 uses the `std::iter_swap` algorithm to exchange the two elements specified by its **common-range forward iterator** arguments. The iterators can refer to any two elements of the same type.

```cpp
// use iterators to swap elements at locations 0 and 1
std::iter_swap(values.begin(), values.begin() + 1);
std::cout << "\n\nAfter std::iter_swap of values[0] and values[1]: ";
std::ranges::copy(values, output);
```

```text
after std::iter_swap of values[0] and values[1]: 1 2 3 4 5 6 7 8 9 10
```

### swap_ranges Algorithm

Line 31 uses the C++20 `std::ranges::swap_ranges` algorithm to exchange the elements of its two **input_range** arguments. If the ranges are not the same length, the algorithm swaps the shorter sequence with the corresponding elements in the longer sequence. The **ranges** also must support **indirectly_swappable iterators**, so the algorithm can dereference the iterators to swap to the corresponding elements in each range.

```cpp
// swap values and values2
std::array values2{10, 9, 8, 7, 6, 5, 4, 3, 2, 1};
std::cout << "\n\nBefore swap_ranges\nvalues contains: ";
std::ranges::copy(values, output);
std::cout << "\nvalues2 contains: ";
std::ranges::copy(values2, output);
std::ranges::swap_ranges(values, values2);
std::cout << "\n\nAfter swap_ranges\nvalues contains: ";
std::ranges::copy(values, output);
std::cout << "\nvalues2 contains: ";
std::ranges::copy(values2, output);
```

```text
Before swap_ranges
values contains: 1 2 3 4 5 6 7 8 9 10
values2 contains: 10 9 8 7 6 5 4 3 2 1

After swap_ranges
values contains: 10 9 8 7 6 5 4 3 2 1
values2 contains: 1 2 3 4 5 6 7 8 9 10
```

Lines 38–39 call the C++20 `std::ranges::swap_ranges` overload specifying the portions of two **input_ranges** to swap. Here, we swap the first five elements of values with the first five elements of values2, indicating the two ranges to swap as **iterator pairs**:

- `values.begin()` and `values.begin() + 5` specify the first five elements in values.
- `values2.begin()` and `values2.begin() + 5` specify values2’s first five elements.
