

```cpp
std::map<int, int, decltype(([](int x, int y) { return x > y; })> map;
```

如你所见，现在可以在 map 容器内部指定 lambda。它可以被用作比较仿函数对象。此类“未求值上下文”（unevaluated contexts）对于高级模板元编程特别有用。例如，在该特性的提案中，作者提到了使用 lambda 谓词在编译时对 tuple 对象进行排序。

更多推理请参阅 P0315R2。

# Lambda 与 constexpr 算法

如果你还记得上一章，自 C++17 起，我们可以使用带有 constexpr 的 lambda。通过此功能，你可以将 lambda 传递给编译时求值的函数。在 C++20 中，大多数标准算法现在都标记了 `constexpr` 关键字，这使得 constexpr lambda 变得更加方便！

让我们来看几个例子。

下面你可以找到在数组上运行 `std::accumulate` 的代码，并使用了自定义的 lambda：

> 使用自定义的 constexpr lambda 使用 std::accumulate。在线代码 @Compiler Explorer
#include <array>
#include <numeric>

```cpp
int main() {
    constexpr std::array arr{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    // 使用 constexpr lambda
    static_assert(std::accumulate(begin(arr), end(arr), 0,
        [](auto a, auto b) noexcept {
            return a + b;
        }) == 55);
    return arr[0];
}
```

在 `std::accumulate` 的示例中，我们使用了 lambda，它实际上是 `std::plus` 操作。

在下一个示例中，有一个 constexpr 函数接收用于 `count_if` 算法的比较器/谓词：

将 constexpr lambda 传递给自定义函数。在线代码 @Compiler Explorer

```cpp
#include <array>
#include <algorithm>

constexpr auto CountValues (auto container, auto cmp) {
    return std::count_if(begin(container), end(container), cmp);
}

int main () {
    constexpr auto minVal = CountValues(std::array{-10, 6, 8, 4, -5, 2, 4, 6},
        [](auto a) { return a >= 0; }
    );
    return minVal;
}
```

- 哪些标准算法是 constexpr 的？`<algorithm>`、`<utility>` 和头文件中的所有算法现在都标记为 constexpr，除了 `shuffle`、`sample`、`stable_sort`、`stable_partition`、`inplace_merge` 以及接受执行策略（Execution Policy）参数的重载。更多信息请阅读论文 P0202 和 P1645。

# C++20 对重载模式（Overloaded Pattern）的更新

在上一章中，你学习了如何继承多个 lambda 表达式并通过重载模式将其暴露出来。这种技术对于 `std::variant` 访问非常有用。

得益于 C++20 类模板参数推导（CTAD）的更新，我们现在可以拥有更短的语法！

为什么？

因为在 C++20 中 CTAD 有了扩展，并且聚合体会被自动处理。这意味着不需要编写自定义推导指南。

对于简单类型：

```cpp
template < typename T, typename U, typename V>
struct Triple { T t; U u; V v; };
```

在 C++20 中你可以写：

```cpp
Triple ttt{ 10.0f , 90 , std::string{"hello"} };
```

并且 `t` 将被推导为 `float`，`u` 为 `int`，`v` 为 `std::string`。

C++20 中的重载模式现在只需为：

```cpp
template < class... > struct overload: Ts... { using Ts::operator (().); };
```

该特性的提案可用于 P1021 以及 P1816（措辞）。

> GCC10 未能实现此提案，但它对于带有继承的高级情况无效，因此我们必须等待完全符合标准。

# 总结

在本章中，我们回顾了 C++20 带来的变化。

首先，我们有一些澄清和改进：例如对 `this` 的捕获、捕获结构化绑定，以及能够默认构造无状态 lambda 的能力。此外，还有更重要的新增！现在一个显著的特性是模板 lambda 和概念（concepts）——这让你对泛型 lambda 拥有更多的控制权。

总之，有了 C++20 及其所有特性，lambda 变得更加强大的工具！

# 附录 A - 技术列表

下面你可以找到贯穿全书的技术和模式：

## C++11 章节

- 计算调用次数 - 一个对默认仿函数进行插桩以扩展其额外功能的示例。
- 继承自 lambda - 一种基本技术，允许你封装闭包类型并扩展其额外功能。
- IIFE - 立即调用函数表达式 - 一种高效计算 `const` 变量值的方法，该方法需要复杂的初始化，而无需创建额外的函数。
- 传递 C++：将无捕获 lambda 作为函数指针传递给 C 风格 API 函数。
- 如何在容器中存储 lambda - 我们可以使用一个小技巧，并存储封装在 `std::function` 中的 lambda。

## C++14 章节

- 替换 `std::bind1`、`std::bind2nd` - 如何使用现代 C++ 替换已弃用的功能。
- 得益于带初始化器的捕获的优化。

## C++17 章节

- IIFE - 立即调用函数表达式 - 一种高效计算 `const` 变量值的方法，该方法需要复杂的初始化，而无需创建额外的函数。
- 传递 C++：将无捕获 lambda 作为函数指针传递给 C 风格 API 函数。
- 如何在容器中存储 lambda - 我们可以使用一个小技巧，并存储封装在 `std::function` 中的 lambda。

## C++20 章节

- 替换 `std::bind1`、`std::bind2nd` - 如何使用现代 C++ 替换已弃用的功能。
- 得益于带初始化器的捕获的优化。

