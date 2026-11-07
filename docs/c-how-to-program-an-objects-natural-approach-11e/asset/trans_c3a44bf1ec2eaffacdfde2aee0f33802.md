

```cpp
int main() {
    std::array a1{1, 3, 5, 7, 9, 1, 3, 5, 7, 9};
    std::ostream_iterator<int> output(std::cout, " ");

    std::cout << "array a1 contains: ";
    std::ranges::copy(a1, output);
}
```

```text
array a1 contains: 1 3 5 7 9 1 3 5 7 9
```

**图 14.10** | 算法 inplace_merge、unique_copy 和 reverse_copy。（第 2 部分，共 2 部分。）

### inplace_merge 算法

第 18 行调用 C++20 的 `std::ranges::inplace_merge` 算法，以合并其 **双向范围** 参数中的两个已排序元素范围。此示例处理范围 a1（第一个参数），将 a1.begin() 到（但不包括）a1.begin() + 5（第二个参数）的元素，与从 a1.begin() + 5（第二个参数）开始到（但不包括）范围末尾的元素合并。还可以传入一个 **二元谓词函数**，它比较两个子范围中的元素，并在第一个元素应被视为小于第二个元素时返回 true。

```cpp
// merge first half of a1 with second half of a1 such that
// a1 contains sorted set of elements after merge
std::ranges::inplace_merge(a1, a1.begin() + 5);
std::cout << "\nAfter inplace_merge, a1 contains: ";
std::ranges::copy(a1, output);
```

```text
After inplace_merge, a1 contains: 1 1 3 3 5 5 7 7 9 9
```

### unique_copy 算法

第 24 行调用 C++20 的 `std::ranges::unique_copy` 算法，复制其第一个参数的已排序 **输入范围** 中的唯一元素——重复项会被忽略。作为第二个参数提供的输出迭代器指定复制元素的位置——在本例中，**back_inserter** 会将新元素添加到 vector results1 中，并根据需要扩展它。还可以传入一个 **二元谓词函数**，指定如何比较元素是否相等。

```cpp
// copy only unique elements of a1 into results1
std::vector<int> results1{};
std::ranges::unique_copy(a1, std::back_inserter(results1));
std::cout << "\nAfter unique_copy, results1 contains: ";
std::ranges::copy(results1, output);
```

```text
After unique_copy, results1 contains: 1 3 5 7 9
```

### reverse_copy 算法

第 30 行调用 C++20 的 `std::ranges::reverse_copy` 算法，创建其第一个参数 `bidirectional_range` 的反向副本。作为第二个参数提供的输出迭代器指定复制元素的位置——在本例中，`back_inserter` 会将新元素添加到 vector `results2` 中，并根据需要扩展它。

```cpp
// copy elements of a1 into results2 in reverse order
std::vector<int> results2{};
std::ranges::reverse_copy(a1, std::back_inserter(results2));
std::cout << "\nAfter reverse_copy, results2 contains: ";
std::ranges::copy(results2, output);
std::cout << "\n";
}
```

```text
After reverse_copy, results2 contains: 9 9 7 7 5 5 3 3 1 1
```

## 14.4.10 集合操作

图 14.11 演示了 C++20 `std::ranges` 命名空间的集合操作算法：includes、`set_difference`、`set_intersection`、`set_symmetric_difference` 和 `set_union`。除了我们展示的功能外，还可以通过传入一个二元谓词函数来自定义每个算法的元素比较；该函数接收两个元素，并在第一个元素应被视为小于第二个元素时返回 true。

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

**图 14.11** | 算法 includes、set_difference、set_intersection、set_symmetric_difference 和 set_union。（第 1 部分，共 2 部分。）

```text
a1 contains: 1 2 3 4 5 6 7 8 9 10
a2 contains: 4 5 6 7 8
a3 contains: 4 5 6 11 15
```

**图 14.11** | 算法 includes、set_difference、set_intersection、set_symmetric_difference 和 set_union。（第 2 部分，共 2 部分。）

### includes 算法

第 26 行和第 30 行分别调用 C++20 的 `std::ranges::includes` 算法，比较两个已排序的 **输入范围**，并判断第二个范围中的每个元素是否都在第一个范围中。这些范围必须使用相同的比较函数进行排序。如果第二个范围的所有元素都在第一个范围中，该算法返回 true；否则返回 false。第 26 行中，a2 的元素全都在 a1 中，因此 includes 返回 true。第 30 行中，a3 的元素并非全都在 a1 中，因此 includes 返回 false。

```cpp
24    // determine whether a2 is completely contained in a1
25    std::cout << std::format("\n\na1 {} a2",
26        std::ranges::includes(a1, a2) ? "includes" : "does not include");
27
28    // determine whether a3 is completely contained in a1
29    std::cout << std::format("\n\na1 {} a3",
30        std::ranges::includes(a1, a3) ? "includes" : "does not include");
```

```text
a1 includes a2

a1 does not include a3
```

### set_difference 算法

第 34 行调用 C++20 的 `std::ranges::set_difference` 算法，找出第一个已排序 **输入范围** 中不在第二个已排序 **输入范围** 中的元素。这些范围必须使用相同的比较函数进行排序。不同的元素会被复制到第三个参数的 **输出迭代器** 所指定的位置——在本例中，**back_inserter** 会将它们添加到 vector difference 中。

```cpp
32    // determine elements of a1 not in a2
33    std::vector<int> difference{};
34    std::ranges::set_difference(a1, a2, std::back_inserter(difference));
35    std::cout << "\n\nset_difference of a1 and a2 is: ";
36    std::ranges::copy(difference, output);
```

```text
set_difference of a1 and a2 is: 1 2 3 9 10
```

### set_intersection 算法

第 40–41 行调用 C++20 的 `std::ranges::set_intersection` 算法，确定第一个已排序 **输入范围** 中位于第二个已排序 **输入范围** 中的元素。这些范围必须使用相同的比较函数进行排序。两个范围共有的元素会被复制到第三个参数的输出迭代器所指定的位置——在本例中，`back_inserter` 会将它们添加到 vector intersection 中。

```cpp
// determine elements in both a1 and a2
std::vector<int> intersection{};
std::ranges::set_intersection(a1, a2,
    std::back_inserter(intersection));
std::cout << "\n\nset_intersection of a1 and a2 is: ";
std::ranges::copy(intersection, output);
```

```text
set_intersection of a1 and a2 is: 4 5 6 7 8
```

### set_symmetric_difference 算法

第 48–49 行调用 C++20 的 `std::ranges::set_symmetric_difference` 算法，确定第一个已排序 `input_range` 中不在第二个 `input_range` 中的元素，以及第二个范围中不在第一个范围中的元素。这些范围必须使用相同的比较函数进行排序。每个 `input_range` 中不同的元素会被复制到第三个参数的输出迭代器所指定的位置——在本例中，`back_inserter` 会将它们添加到 `symmetricDifference` 中。

```cpp
// determine elements of a1 that are not in a3 and
// elements of a3 that are not in a1
std::vector<int> symmetricDifference{};
std::ranges::set_symmetric_difference(a1, a3,
    std::back_inserter(symmetricDifference));
std::cout << "\n\nset_symmetric_difference of a1 and a3 is: ";
std::ranges::copy(symmetricDifference, output);
```

```text
set_symmetric_difference of a1 and a3 is: 1 2 3 7 8 9 10 11 15
```

### set_union 算法

第 55 行调用 C++20 的 `std::ranges::set_union` 算法，创建由其两个已排序 `input_ranges` 中任一范围或两个范围所包含元素组成的集合；这些范围必须使用相同的比较函数进行排序。元素会被复制到第三个参数的输出迭代器所指定的位置——在本例中，`back_inserter` 会将它们添加到 `unionSet`。同时出现在两个集合中的元素只从第一个集合复制。

```cpp
// determine elements that are in either or both sets
std::vector<int> unionSet{};
std::ranges::set_union(a1, a3, std::back_inserter(unionSet));
std::cout << "\n\nset_union of a1 and a3 is: ";
std::ranges::copy(unionSet, output);
std::cout << "\n";
}
```

