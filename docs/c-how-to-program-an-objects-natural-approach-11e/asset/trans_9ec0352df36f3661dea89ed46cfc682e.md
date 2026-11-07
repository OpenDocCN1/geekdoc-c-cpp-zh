
这些消息还提供了更多细节，称

> 注意：因为 `std::basic_string<char>` 不满足 `integral`

并且

> 注意：并且 `std::basic_string<char>` 不满足 `floating_point`

`static_assert` 声明可以选择指定一个字符串作为第二个参数，以便在断言为假时将其包含在错误消息中。

## 15.8 创建自定义算法

我们在第 13 章和第 14 章中看到，标准库分为容器、迭代器和算法。我们展示了通过迭代器对容器元素进行操作的算法。您可以利用这种架构来**定义能够对任何支持该算法迭代器要求的容器进行操作的自定义算法**。图 15.10 定义了一个受约束的 average 算法，其中参数必须满足第 14–17 行中的自定义 `NumericInputRange` 概念，我们将在图后进行描述。

```cpp
// Fig15_10.cpp
// A custom algorithm to calculate the average of
// a numeric input range's elements.
#include <algorithm>
#include <array>
#include <concepts>
#include <iostream>
#include <iterator>
#include <list>
#include <ranges>
#include <vector>

// concept for an input range containing integer or floating-point values
template<typename T>
concept NumericInputRange = std::ranges::input_range<T> &&
    (std::integral<typename T::value_type> ||
     std::floating_point<typename T::value_type>);

// calculate the average of a NumericInputRange's elements
auto average(NumericInputRange auto const& range) {
    long double total{};

    for (auto i{range.begin()}; i != range.end(); ++i) {
        total += *i; // dereference iterator and add value to total
    }

    // divide total by the number of elements in range
    return total / std::ranges::distance(range);
}
```

**图 15.10** 一个用于计算数值输入范围平均值的自定义算法。（第 1 部分，共 2 部分。）

```cpp
int main() {
    std::ostream_iterator<int> outputInt(std::cout, " ");
    const std::array<int> ints{1, 2, 3, 4, 5};
    std::cout << "array ints: ";
    std::ranges::copy(ints, outputInt);
    std::cout << "\naverage of ints: " << average(ints);

    std::ostream_iterator<double> outputDouble(std::cout, " ");
    const std::vector doubles{10.1, 20.2, 35.3};
    std::cout << "\nvector doubles: ";
    std::ranges::copy(doubles, outputDouble);
    std::cout << "\naverage of doubles: " << average(doubles);

    std::ostream_iterator<long double> outputLongDouble(std::cout, " ");
    const std::list longDoubles{10.1, 20.2, 35.3};
    std::cout << "\nlist longDoubles: ";
    std::ranges::copy(longDoubles, outputLongDouble);
    std::cout << "\naverage of doubles: " << average(longDoubles)
              << "\n";
}
```

```text
array ints: 1 2 3 4 5
average of ints: 3

vector doubles: 10.1 20.2 35.3
average of doubles: 21.8667

list longDoubles: 10.1 20.2 35.3
average of doubles: 21.8667
```

**图 15.10** 一个用于计算数值输入范围平均值的自定义算法。（第 2 部分，共 2 部分。）

### 自定义 NumericInputRange 概念

自定义 `NumericInputRange` 概念（第 14–17 行）检查

- 类型是否满足 `input_range` 概念（第 15 行），因此参数至少支持用于读取其元素的输入迭代器，以及
- 范围的元素是否满足 `std::integral` 或 `std::floating_point` 概念（第 16–17 行），因此它们可用于计算。

回想第 13.4.1 节，每个标准容器都有一个嵌套的 `value_type`，它指示容器的元素类型。我们使用它来检查元素类型是否满足此概念的要求。在第 16 和 17 行中，记法 `typename T::value_type` 表示 `T::value_type` 是范围元素类型的别名。

### 自定义 average 算法

第 20–29 行将 average 定义为缩写函数模板。我们使用自定义概念 `NumericInputRange` 约束其范围参数，因此该算法可以对任何数值类型的 `input_range` 进行操作。为了确保 average 能够支持任何内置数值类型，我们使用 `long double`（第 21 行）来存储元素的总和。

第 23–25 行从范围的**开始迭代器**遍历到其**结束迭代器**（但不包括结束迭代器），并将每个元素的值加到总和中。然后第 28 行将总和除以范围中的元素数量，该数量由 `std::ranges::distance` 算法确定。

### 在标准库容器上使用我们的 average 算法

为了表明我们的自定义 average 算法可以处理各种标准库容器，第 33、39 和 45 行分别定义了一个 int 数组、一个 double 向量和一个 long double 列表。第 36、42 和 48 行分别用这些容器调用 average，以计算其元素的平均值。

## 15.9 创建自定义容器和迭代器

第 11 章介绍了我们的 MyArray 类，以演示特殊成员函数和运算符重载。C++ 核心准则建议使用模板来实现任何表示值容器或值范围的类。[72] 因此，在这里，我们将把 MyArray 定义为一个类模板，并使用各种标准库约定来增强它。[73] 我们还将定义自定义迭代器，以便将 MyArray 对象与各种标准库算法一起使用。

我们的目标是让您了解创建类似标准库的容器涉及哪些内容。实现与标准库的完全兼容性以及与先前 C++ 语言版本的向后兼容性，涉及许多超出本书范围的**条件编译指令**。如果您想构建可复用的类似标准库的容器，请研究编译器供应商提供的代码，并查看我们脚注中引用的研究来源。图 15.11 定义了我们的 MyArray 类模板及其自定义迭代器。我们将该图分成几个部分进行讨论。

### 单个头文件

您会注意到与第 11 章 MyArray 类相比的一处变化是，**整个类及其自定义迭代器都定义在单个头文件中**，这是类模板的典型做法。**编译器在模板被用于实例化之处需要完整定义**。此外，在类模板定义内部定义成员函数可以简化语法，因为您不需要为每个成员函数编写模板头。

### MyArray 支持双向迭代器

我们以标准库的 **array** 类模板为模型来构建此示例，它使用编译时分配的、固定大小的内置数组。如第 13.5 节所述，指向此类数组的指针满足随机访问迭代器的所有要求。然而，对于此示例，我们将使用类模板实现自定义双向迭代器。我们使用的迭代器架构受到 **Microsoft 开源 C++ 标准库 array** 实现的启发，[74] 该实现定义了两个迭代器类：

- 一个用于操作 const 对象的迭代器，以及
- 一个用于操作非 const 对象的迭代器。

您可以在以下网址查看 Microsoft 的实现：
https://github.com/microsoft/STL/blob/main/stl/inc/array

我们定义了以下自定义迭代器类：

- 我们的 **ConstIterator** 类表示只读双向迭代器。
- 我们的 **Iterator** 类表示读/写双向迭代器。

GNU 和 Clang 的 array 实现只是为其数组迭代器使用指针。您可以在以下网址查看它们的实现：
https://github.com/gcc-mirror/gcc/blob/master/libstdc%2B%2B-v3/include/std/array
和
https://github.com/llvm/llvm-project/blob/main/libcxx/include/array

### 为什么我们实现双向迭代器而不是随机访问迭代器

回想我们在第 13.5 节中对迭代器的介绍，标准库容器支持不同级别的迭代器。最强大的是连续迭代器，它们是用于保证连续内存的容器的随机访问迭代器。大多数标准库算法对容器元素范围进行操作。只有 12 个算法需要随机访问迭代器——shuffle 和 11 个与排序相关的算法——并且没有算法需要连续迭代器。MyArray 的双向迭代器使大多数标准库算法能够处理 MyArray 对象。随机访问迭代器有许多附加要求[75]，如下表所示。作为练习，您可以使用这些能力增强 MyArray 的自定义迭代器，使其成为随机访问迭代器。

| 随机访问迭代器操作 | 描述 |
| --- | --- |
| `p += i` | 将迭代器 p 增加 i 个位置。 |
| `p -= i` | 将迭代器 p 减少 i 个位置。 |
| `p + i` 或 `i + p` | 结果是一个位于 p 增加 i 个位置处的迭代器。 |
| `p - i` | 结果是一个位于 p 减少 i 个位置处的迭代器。 |
| `p - p1` | 计算同一容器中两个元素之间的距离（即元素数量）。 |
| `p[i]` | 返回对从 p 偏移 i 个位置处元素的引用 |
| `p < p1` | 如果迭代器 p 小于迭代器 p1（即迭代器 p 在容器中位于迭代器 p1 之前），则返回 true；否则返回 false。 |

（续...）

---

### 脚注

72. C++ 核心准则，“T.3：使用模板表达容器和范围。” 访问于 2023 年 4 月 18 日。https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#rt-cont.
73. Jonathan Boccara，“让您的容器遵循 STL 的约定，” 2018 年 4 月 24 日。访问于 2023 年 4 月 18 日。https://www.fluentcpp.com/2018/04/24/following-conventions-stl/.
74. “array 标准头文件。” 最新提交（即文件最后更新时）2021 年 2 月 24 日。访问于 2023 年 4 月 18 日。https://github.com/microsoft/STL/blob/main/stl/inc/array.
