
```cpp
if (s.empty()) {
    // do something because the string s is empty
}
```

在 C++20 中，string 的 empty 函数使用 `[[nodiscard]]` 属性声明——如果调用者不使用返回值，编译器会发出警告。³³ 自 C++17 起，许多库函数已通过 `[[nodiscard]]` 得到增强，以帮助你编写正确的代码。

## `[[nodiscard("with reason")]]` 属性

你可以包含一条描述性消息，编译器会将其作为警告消息的一部分显示，如下所示：

```cpp
[[nodiscard("Insight goes here")]]
```

你也可以在自己的函数定义上使用此属性。图 20.31 展示了一个使用 `[[nodiscard]]` 声明的 cube 函数。你将属性放在返回类型之前——通常为了可读性单独占一行（第 4 行）。第 10 行调用 cube，但没有使用返回值。三个输出分别显示了来自 Visual C++、clang++ 和 g++ 的编译器警告。这些只是警告，因此程序仍会编译并运行。本示例的主要目的是演示 `[[nodiscard]]` 产生的编译器警告消息。该程序运行时不会产生任何输出，因为它在不应忽略 cube 返回值时忽略了它。

```cpp
// fig20_31.cpp
// [[nodiscard]] attribute.

[[nodiscard("Do not ignore! Otherwise, you won't know the cube of x")]]
int cube(int x) {
    return x * x * x;
}

int main() {
    cube(10); // generates a compiler warning
}
```

```text
C:\Users\pauldeitel\examples\ch20\fig20_31.cpp(10,8): warning C4858: discarding return value. Do not ignore! Otherwise, you won't know the cube of x.
```

```text
fig20_31.cpp:10:4: warning: ignoring return value of function declared with
'nodiscard' attribute: Do not ignore! Otherwise, you won't know the cube of
x. [-Wunused-result]
    cube(10); // generates a compiler warning
    ^~~~
1 warning generated.
```

```text
fig20_31.cpp: In function 'int main()':
fig20_31.cpp:10:8: warning: ignoring return value of 'int cube(int)', declared with attribute 'nodiscard' [-Wunused-result]. Otherwise, you won't know the cube of x.
   10 |     cube(10); // generates a compiler warning
      |     ~~~~^~~~
fig20_31.cpp:5:5: note: declared here
    5 | int cube(int x) {
      |     ^~~~
```

**图 20.31** | `[[nodiscard]]` 属性。

33. “C++ [dcl.attr.nodiscard]。”访问于 2023 年 4 月 18 日。https://timsong-cpp.github.io/cppwp/n4861/dcl.attr.nodiscard.

## 20.15 一些关键的 C++23 特性

在我们完成本书时，C++23 标准已接近完成，且编译器支持很少，因此本节的代码片段和示例输出是虚构的，尚未经过测试。在这里，我们概述几个关键的 C++23 特性。³⁴,³⁵,³⁶ 之前，我们提到了一些 C++23 特性以及一些可能的未来 C++ 特性，包括

- `std::mdarray` 容器（第 6.13 节），
- 契约（第 12.13 节），
- ranges 增强（第 14.10 节），
- 模块化标准库（第 16.12 节），
- 并发数据结构（第 17.15 节），
- 并行 ranges 算法（第 17.15 节）以及
- 执行器（第 18.5 和 18.8 节）。

cppreference.com 上展示 C++23 编译器支持的表格（https://en.cppreference.com/w/cpp/compiler_support/23）列出了 120 多个条目，其中一些涵盖了许多新特性。其中许多在 https://en.wikipedia.org/wiki/C%2B%2B23 上进行了总结。

C++23 是与 C++20 不同的一种更新，C++20 有四个主要新特性——ranges、concepts、modules 和协程。

有 25 个新的 C++23 条目被归类为“缺陷报告”（defect report）改进（在编译器支持表中标记为 DR）——它们是针对现有特性的缺陷修复的组合。其他条目是新特性或对现有特性的增强，例如新的 ranges 和 views 能力，提供额外的函数式编程能力。

34. “C++23。”Wikipedia。Wikimedia Foundation。访问于 2023 年 4 月 18 日。https://en.wikipedia.org/wiki/C%2B%2B23.

35. “C++23 的编译器支持。”访问于 2023 年 4 月 18 日。https://en.cppreference.com/w/cpp/compiler_support/23.

36. Bryce Adelstein Lelbach、Fabio Fracassi、Ben Craig、Billy Baker、Nevin Liber、Ville Voutilainen 和 Inbal Levi，“完成 C++23 的库演化计划”，2021 年 11 月 9 日。访问于 2023 年 4 月 18 日。https://wg21.link/p2489.

### C++23 格式化输出

我们在本书中通篇使用 C++20 的 `std::format` 函数进行文本格式化，第 19 章介绍了更多 C++20 文本格式化特性。C++23 的 `<print>` 头文件提供了函数 `std::print` 和 `std::println`（“打印行”），它们默认将格式化字符串直接输出到标准输出流。它们还提供了将格式化文本写入其他流的重载。`std::println` 在输出其参数后自动输出一个换行符。

假设存在 `int` 变量 `total` 且其值为 385。使用新的格式化输出函数，像这样的语句

```cpp
std::cout << std::format("Sum is {}\n", total);
```

可以用 `std::print` 更简洁地写为

```cpp
std::print("Sum is {}\n", total);
```

或者用 `std::println` 写为

```cpp
std::println("Sum is {}", total);
```

上述每个语句都会产生以下输出，并将输出光标移到下一行的开头：

```text
Sum is 385
```

有关 `std::print` 和 `std::println` 的更多信息，请参见 https://en.cppreference.com/w/cpp/header/print。

### C++23 ranges 增强

C++20 的 ranges 和 views 已通过 11 个新的 `std::ranges` 算法和 14 个新的 `std::views` 函数式编程能力得到增强。一些关键的新特性包括：

- `ranges::to` 使你能够将范围转换为元素容器，从而方便地存储每个函数式操作管道的结果。例如，给定 lambda 表达式 `isEven`（第 1 行），如果其参数能被 2 整除，则返回 `true`，第 3-6 行中的管道从 0 开始生成整数（第 3 行），仅保留 `isEven` 返回 `true` 的整数（第 4 行），取这些偶数中的前五个（第 5 行），并将管道的结果收集到一个 `vector` 中（第 6 行）。此代码执行后，变量 `results` 是一个 `vector<int>`，包含 0、2、4、6 和 8。

```cpp
1  auto isEven = [](int x) {return x % 2 == 0;};
2  auto results{
3      std::views::iota(0)
4      | std::views::filter(isEven)
5      | std::views::take(5)
6      | std::ranges::to<std::vector>()
7  };
```

- 用于在范围中搜索项目的算法，例如 `ranges::contains`、`ranges::contains_subrange`、`ranges::find_last`、`ranges::find_last_if`、`ranges::find_last_if_not`、`ranges::starts_with` 和 `ranges::ends_with`。

- 视图操作 `views::zip` 和 `views::zip_transform`，用于处理元素的并行范围。例如，以下代码片段使用 `views::zip` 生成包含来自 `studentNames` 和 `gradePointAverages` 向量的对应元素的元组，然后显示这些元组的元素：

```cpp
std::vector studentNames{"Meriem", "Pierre", "Sierra"};
std::vector gradePointAverages{3.9, 3.5, 4.0};

for (std::tuple<std::string&, double&> student :
     std::views::zip(studentNames, gradePointAverages)) {
  std::println("{}: {}",
     std::get<0>(student), std::get<1>(student));
}
```

```text
Meriem: 3.9
Pierre: 3.5
Sierra: 4.0
```

- 视图操作 `views::enumerate` 提供了一种便捷机制，用于访问范围中元素的索引和值。例如，以下代码遍历向量 `colors`，显示每个元素的索引和值，而无需可变的计数器变量：

```cpp
std::vector colors{"red", "orange", "yellow"};

for (const auto& [i, color] : std::views::enumerate(colors)) {
  std::println("{}: {}", i, color);
}
```

```text
0: red
1: orange
2: yellow
```

有关 C++23 ranges 和 views 增强的更多信息，请参见 https://en.cppreference.com/w/cpp/header/ranges 中标记为 C++23 的条目。

### C++23 生成器协程

在第 18.4 节中，我们使用 Sy Brand 的 `std::generator` 库创建了一个生成器协程。C++23 现在提供了 `std::generator`，因此你无需第三方库即可创建生成器协程。`std::generator` 应该可以一对一替换图 18.1 中的 `tl::generator`。有关 `std::generator` 的更多信息，请参见：³⁷

37. 以 https://wg21.link 开头的链接会带你前往描述新特性的 C++ 标准委员会论文的最新版本。
