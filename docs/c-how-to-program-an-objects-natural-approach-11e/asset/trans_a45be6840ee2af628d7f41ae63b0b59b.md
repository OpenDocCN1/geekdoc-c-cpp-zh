
## 建筑师说明——无障碍设计

除通用说明和结构说明外，以下无障碍设计事项应无条件予以考虑：

- 1. 入口通道和入口区域应设计为无台阶，并可无障碍通行。
- 2. 门系统应设计为自动滑动门或自动平开门。
- 3. 所有楼梯均应增设尺寸足够的坡道或无障碍电梯。本要求不适用于仅作为辅助逃生路线的楼梯。

所有所需图纸均应按照 DIN 18040-1 编制。

红色图纸：初步规划阶段的变更。

```text
a1: 1 2 3 4 5 6 7 8 9 10
```

**图 14.6** | 标准库中的数学算法。（第 2 部分，共 2 部分。）

## Shuffle 算法

第 18 行调用 C++20 的 `std::ranges::shuffle` 算法，随机重排 a1 的元素。这要求使用带有 `random_access_iterators` 的 `random_access_range`，因此可用于容器 `array`、`vector` 和 `deque`（以及内置数组）。该算法的声明表明，范围的迭代器必须是 `permutable`，这允许交换和移动元素等操作。非 const 数组的迭代器允许此类操作。`shuffle` 算法的第二个参数是随机数生成器引擎（第 5.8 节）。第 20 行显示重排后的结果。

```cpp
// create random-number engine and use it to help shuffle a1
std::default_random_engine randomEngine{std::random_device()()};
std::ranges::shuffle(a1, randomEngine); // randomly order elements
std::cout << "\na1 shuffled: ";
std::ranges::copy(a1, output);
```

```text
a1 shuffled: 5 4 7 6 3 9 1 8 10 2
```

## Count 算法

第 27 行调用 C++20 的 `std::ranges::count` 算法，统计 a2 中具有特定值（此处为 8）的元素个数。第一个参数必须是 `input_range`，以便 `count` 能读取范围内的元素。

```cpp
std::array a2{100, 2, 8, 1, 50, 3, 8, 8, 9, 10};
std::cout << "\na2: ";
std::ranges::copy(a2, output);

// count number of elements in a2 with value 8
auto result1{std::ranges::count(a2, 8)};
std::cout << "\nCount of 8s in a2: " << result1;
```

```text
a2: 100 2 8 1 50 3 8 8 9 10
Count of 8s in a2: 3
```

## count_if 算法

第 31 行调用 C++20 的 `std::ranges::count_if` 算法，在其 `input_range` 参数 a2 中统计一元谓词函数返回 true 的元素个数。这里我们再次使用 lambda 定义一元谓词，对大于 9 的值返回 true。

```cpp
// count number of elements in a2 that are greater than 9
auto result2{std::ranges::count_if(a2, [](auto x){return x > 9;})};
std::cout << "\nCount of elements of a2 that are greater than 9: " << result2;
```

```text
Count of elements of a2 that are greater than 9: 3
```

### min_element 算法

第 35 行调用 C++20 的 `std::ranges::min_element` 算法，在其 **前向范围**参数 `a2` 中定位最小元素。此类范围支持 **前向迭代器**，使 `min_element` 能够读取范围内的元素。该算法返回一个迭代器，指向范围中最小元素的首次出现位置；如果范围为空，则返回其哨兵。与许多比较元素的算法一样，你可以提供自定义二元谓词函数，指定如何比较两个元素，并在第一个元素应被视为小于第二个元素时返回 true。在解引用可能表示范围哨兵的迭代器之前，应检查它是否不等于哨兵，如第 35 行所示。

C++ 概念

Err X

```cpp
34      // locate minimum element in a2
35      if (auto result{std::ranges::min_element(a2)}; result != a2.end()) {
36          std::cout << "\na2 minimum element: " << *result;
37      }
38
```

```text
a2 minimum element: 1
```

### max_element 算法

第 40 行调用 C++20 的 `std::ranges::max_element` 算法，在其 **前向范围**参数 `a2` 中定位最大元素。此类范围支持 **前向迭代器**，使 `max_element` 能够读取范围内的元素。该算法返回一个迭代器，指向范围中最大元素的首次出现位置；如果范围为空，则返回其哨兵。同样，你可以提供自定义二元谓词函数，指定如何比较元素。

C++ 概念

```cpp
39      // locate maximum element in a2
40      if (auto result{std::ranges::max_element(a2)}; result != a2.end()) {
41          std::cout << "\na2 maximum element: " << *result;
42      }
43
```

```text
a2 maximum element: 100
```

### minmax_element 算法

第 45 行调用 C++20 的 `std::ranges::minmax_element` 算法，在其 **前向范围**参数 `a2` 中定位最小和最大元素。该算法返回一个 `std::ranges::minmax_element_result`，其中包含名为 `min` 和 `max` 的迭代器，分别指向最小和最大元素：

- 如果有重复的最小元素，第一个迭代器位于最小值的第一个位置。
- 如果有重复的最大元素，第二个迭代器位于最大值的最后一个位置——注意，这与 `max_element` 的工作方式不同。

你可以提供自定义二元谓词函数，指定如何比较元素。

```cpp
// locate minimum and maximum elements in a2
auto [min, max]{std::ranges::minmax_element(a2)};
std::cout << "a2 minimum and maximum elements: "
          << *min << " and " << *max;
```

```text
a2 minimum and maximum elements: 1 and 100
```

## 结构化绑定

第 45 行使用 **minmax_element** 返回的 **minmax_element_result**，通过结构化绑定声明初始化变量 `min` 和 `max`。^18,19 这有时称为解包元素，可用于将内置数组、`std::array` 对象、`std::pair` 或 `std::tuple`（每个的大小在编译时已知）的元素提取到各个变量中。结构化绑定还可用于解包结构体或类对象的可访问数据成员。在第 13 章的每个示例中，如果函数返回 `std::pair`，我们也可以使用结构化绑定来解包其成员。

## transform 算法

第 51–52 行使用 C++20 的 **std::ranges::transform** 算法，将其 **输入范围** a1 的元素转换为新值。每个新值写入该算法第二个参数指定的范围，该参数必须是输出迭代器，并且可以指向与 **输入范围** 相同的容器或不同容器。作为 **transform** 第三个参数提供的函数接收一个值并返回一个新值。无法保证该函数对范围内元素的调用顺序，因此它不应修改 **输入范围** 的元素。若要修改原始范围的元素，请使用 **std::foreach** 算法。^20

```cpp
// calculate cube of each element in a1; place results in cubes
std::array<int, a1.size()> cubes{};
std::ranges::transform(a1, cubes.begin(),
    [](auto& x) { return x * x * x; });
std::cout << "\na1 values cubed: ";
std::ranges::copy(cubes, output);
std::cout << "\n";
}
```

```text
a1 values cubed: 125 64 343 216 27 729 1 512 1000 8
```

**transform** 的一个重载接受两个 **输入范围**、一个输出迭代器，以及一个接受两个参数并返回结果的函数。此版本的 **transform** 将每个 `input_range` 中的对应元素传递给其函数参数，然后通过 `output iterator` 输出函数结果。

- 18. “结构化绑定声明”。访问日期：2023 年 4 月 18 日。https://en.cppreference.com/w/cpp/language/structured_binding.
- 19. Dominik Berner，“使用结构化绑定在 C++ 中快速轻松地解包”。2018 年 5 月 24 日。访问日期：2023 年 4 月 18 日。https://dominikk.com/structured-bindings/.
- 20. “算法库——修改序列操作——Transform”。访问日期：2023 年 4 月 18 日。https://timsong-cpp.github.io/cppwp/n4861/alg.transform.

## 14.4.6 搜索与排序算法

图 14.7 演示了一些基本的搜索和排序算法，包括 C++20 `std::ranges` 命名空间中的 `find`、`find_if`、`sort`、`binary_search`、`all_of`、`any_of`、`none_of` 和 `find_if_not`。

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

```text
values contains: 10 2 17 5 16 8 13 11 20 7
```

**图 14.7** | 标准库搜索和排序算法。

## find 算法

C++20 的 `std::ranges::find` 算法（第 16 行）执行 O(n) 线性搜索，在其 `input_range` 参数（`values`）中查找值（16）。该算法返回指向第一个包含该值的元素的迭代器；否则返回范围的哨兵（第 24–29 行演示了这一点）。我们在第 17 行使用返回的迭代器计算找到该值的索引位置。

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
