
```text
Found 16 at index: 4
100 not found
```

### find_if 算法

C++20 `std::ranges::find_if` 算法（第35行）执行 *O(n)* 线性搜索，在其输入范围参数（values）中定位第一个使一元谓词函数（第32行的 `isGreaterThan10`）返回 true 的值。该算法返回一个迭代器，指向第一个包含使谓词函数返回 true 的值的元素；否则，返回该范围的哨兵。

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

### sort 算法

C++20 `std::ranges::sort` 算法（第46行）执行 *O(n log n)* 排序，将其参数 values 中的元素按升序排列。该参数必须是 `random_access_range`，它支持 `random_access_iterators`，因此可与容器 array、vector 或 deque（以及内置数组）一起使用。该算法还可以接收一个二元谓词函数，该函数接受两个参数并返回一个表示排序顺序的 bool。谓词比较正在排序的序列中的两个值。如果二元谓词返回 true，则这两个元素已按排序顺序排列；否则，这两个元素需要在序列中重新排序。

```cpp
// sort elements of values
std::ranges::sort(values);
std::cout << "\n\nvalues after sort: ";
std::ranges::copy(values, output);
```

```text
values after sort: 2 5 7 8 10 11 13 16 17 20
```

### binary_search 算法

C++20 `std::ranges::binary_search` 算法（第51行）执行 `O(log n)` 二分搜索，以确定值 13 是否在 `forward_range` 参数（values）中。该范围必须按升序排序。该算法返回一个 `bool`，表示是否在序列中找到该值。第59行演示了一次未找到该值的 `binary_search` 调用。该算法还可以接收一个二元谓词函数，该函数接受两个参数并返回一个 `bool`。如果要比较的两个元素按排序顺序排列，则该函数应返回 `true`。如果你需要知道搜索键在容器中的位置，请使用 `lower_bound` 或 `find` 算法，而不是 `binary_search`。

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

### all_of 算法

C++20 `std::ranges::all_of` 算法（第67行）执行 `O(n)` 线性搜索，以确定其第二个参数中的一元谓词函数（在本例中为 lambda `isGreaterThan10`）是否对其 `input_range` 参数（values）中的所有元素都返回 `true`。如果是，则 `all_of` 返回 `true`；否则，返回 `false`。

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

### any_of 算法

C++20 `std::ranges::any_of` 算法（第75行）执行 *O(n)* 线性搜索，以确定其第二个参数中的一元谓词函数（在本例中为 lambda `isGreaterThan10`）是否对其 `input_range` 参数（values）中的至少一个元素返回 true。如果是，则 `any_of` 返回 true；否则，返回 false。

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

### none_of 算法

C++20 `std::ranges::none_of` 算法（第83行）执行 *O(n)* 线性搜索，以确定其第二个参数中的一元谓词函数（在本例中为 lambda `isGreaterThan10`）是否对其 `input_range` 参数（values）中的所有元素都返回 false。如果是，则 `none_of` 返回 true；否则，返回 false。

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

### find_if_not 算法

C++20 `std::ranges::find_if_not` 算法（第91行）执行 *O(n)* 线性搜索，以在其 `input_range` 参数（values）中定位第一个使一元谓词函数（lambda `isGreaterThan10`）返回 false 的值。该算法返回一个迭代器，指向第一个包含使谓词函数返回 false 的值的元素；否则，返回该范围的哨兵。

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

## 14.4.7 swap、iter_swap 和 swap_ranges

图14.8演示了用于交换元素的算法——来自 std 命名空间的 **swap** 和 **iter_swap**，以及来自 C++20 的 **std::ranges** 命名空间的算法 **swap_ranges**。

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

**图 14.8** | swap、iter_swap 和 swap_ranges 算法。

### swap 算法

第15行使用 `std::swap` 算法交换其两个参数的值——这不是范围算法或公共范围算法。该函数接收对被交换的两个值的引用。在本例中，我们传入对该数组第一个和第二个元素的引用。

```cpp
std::swap(values[0], values[1]); // swap elements at index 0 and 1

std::cout << "\nafter std::swap of values[0] and values[1]: ";
std::ranges::copy(values, output);
```

```text
after std::swap of values[0] and values[1]: 2 1 3 4 5 6 7 8 9 10
```

### iter_swap 算法

第21行使用 `std::iter_swap` 算法交换其 **公共范围前向迭代器** 参数指定的两个元素。这些迭代器可以指向同一类型的任意两个元素。

```cpp
// use iterators to swap elements at locations 0 and 1
std::iter_swap(values.begin(), values.begin() + 1);
std::cout << "\n\nAfter std::iter_swap of values[0] and values[1]: ";
std::ranges::copy(values, output);
```

```text
after std::iter_swap of values[0] and values[1]: 1 2 3 4 5 6 7 8 9 10
```

### swap_ranges 算法

第31行使用 C++20 `std::ranges::swap_ranges` 算法交换其两个 **input_range** 参数的元素。如果两个范围长度不同，该算法会将较短的序列与较长序列中的对应元素交换。这些 **范围** 还必须支持 **indirectly_swappable 迭代器**，以便该算法可以解引用迭代器，与每个范围中的对应元素进行交换。

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

第38–39行调用 C++20 `std::ranges::swap_ranges` 重载，指定要交换的两个 **input_ranges** 的部分。在这里，我们将 values 的前五个元素与 values2 的前五个元素交换，并将要交换的两个范围表示为 **迭代器对**：

- `values.begin()` 和 `values.begin() + 5` 指定 values 中的前五个元素。
- `values2.begin()` 和 `values2.begin() + 5` 指定 values2 的前五个元素。

