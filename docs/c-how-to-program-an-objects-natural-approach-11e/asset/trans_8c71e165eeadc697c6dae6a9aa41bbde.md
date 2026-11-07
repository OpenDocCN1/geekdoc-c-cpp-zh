
## 隐式创建 span 并将其传递给函数

第46行以 `values1` 为实参调用 `displaySpan`。该函数的形参声明为

```cpp
std::span<const int>
```

因此 C++ 会创建一个 span，其中包含一个指向数组首元素的 `const int*`，以及一个表示数组大小的 `size_t`，编译器从 `values1` 的声明（第34行）中获取该大小。由于 span 可以查看任意连续的元素序列，你也可以将 `int` 的 `std::array` 或 `std::vector` 传递给 `displaySpan`（第50行和第52行）。C++ 会创建一个适当的 span，表示指向容器首元素的指针和大小。这使得 `displaySpan` 比 `displayArray` 更灵活，后者在此示例中只能接收内置数组。

```cpp
// compiler knows values1's size and automatically creates a span
// representing &values1[0] and the array's length
std::cout << "\nvalues1 via displaySpan: ";
displaySpan(values1);

// compiler also can create spans from std::arrays and std::vectors
std::cout << "\nvalues2 via displaySpan: ";
displaySpan(values2);
std::cout << "\nvalues3 via displaySpan: ";
displaySpan(values3);
```

```text
values1 via displaySpan: 1 2 3 4 5
values2 via displaySpan: 6 7 8 9 10
values3 via displaySpan: 11 12 13 14 15
```

## 修改 span 的元素会修改原始数据

正如我们提到的，函数 `times2` 将其 span 的元素乘以 2。第55行以 `values1` 为实参调用 `times2`。该函数的形参声明为

```cpp
std::span<int>
```

因此 C++ 会创建一个 span，其中包含一个指向数组首元素的 `int*`，以及一个表示数组大小的 `size_t`，编译器从 `values1` 的声明（第34行）中获取该大小。为了证明 `times2` 修改了原始数组的数据，第57行显示 `values1` 更新后的值。与 `displaySpan` 一样，`times2` 也可以用此程序的 `std::array` 或 `std::vector` 调用。

```cpp
// changing a span’s contents modifies the original data
times2(values1);
std::cout << "\nvalues1 after times2 modifies its span argument: ";
displaySpan(values1);
```

```text
values1 after times2 modifies its span argument: 2 4 6 8 10
```

## 手动创建 span 并与之交互

你可以显式创建 span 并与之交互。第60行创建一个 `span<int>`，用于查看 `values1` 中的数据——编译器使用 CTAD 从 `values1` 的元素推断出元素类型 `int`。第61–62行演示了 span 的 `front` 和 `back` 成员函数，它们分别返回视图的第一个和最后一个元素——因此也就是 `values1` 的第一个和最后一个元素。

```cpp
// spans have various array-and-vector-like capabilities
std::span mySpan{values1}; // span<int>
std::cout << "\nmySpan's first element: " << mySpan.front()
          << "\nmySpan's last element: " << mySpan.back();
```

```text
mySpan's first element: 2
mySpan's last element: 10
```

> C++ Core Guidelines 的一个理念是“优先选择编译期检查而非运行期检查。”[^22] 这使编译器能够在编译期发现并报告错误，而不是由你编写代码来帮助防止运行时错误。在第60行，编译器根据第34行中 `values1` 的声明确定 span 的大小（5）。你可以显式说明 span 的类型和大小，如下所示：
>
> ```cpp
> span<int, 5> mySpan{values1};
> ```
>
> 在这种情况下，编译器会确保 span 声明的大小与 `values1` 的大小匹配；否则会发生编译错误。

## 将 span 与标准库的 accumulate 算法配合使用

正如你在此示例中所见，span 是可迭代的。这意味着你还可以对 span 使用 `begin` 和 `end` 函数，将它们传递给 C++ 标准库算法，例如 `accumulate`（第66行）或 `sort`。我们将在第14章深入讨论标准库算法。

```cpp
// spans can be used with standard library algorithms
std::cout << "\nSum of mySpan's elements: "
          << std::accumulate(std::begin(mySpan), std::end(mySpan), 0);
```

```text
Sum of mySpan's elements: 30
```

## 创建子视图

有时，你可能想处理 span 的子集。span 的 `first`、`last` 和 `subspan` 成员函数可以创建子视图。第70行和第72行使用 `first` 和 `last` 分别获取表示 `values1` 前三个元素和后三个元素的 span。第74行使用 `subspan` 获取一个查看从索引1开始的3个元素的 span。在每种情况下，我们都会将子视图传递给 `displaySpan`，以确认该子视图表示什么。

```cpp
68    // spans can be used to create subviews of a container
69    std::cout << "\n\nFirst three elements of mySpan: ";
70    displaySpan(mySpan.first(3));
71    std::cout << "\nLast three elements of mySpan: ";
72    displaySpan(mySpan.last(3));
73    std::cout << "\nMiddle three elements of mySpan: ";
74    displaySpan(mySpan.subspan(1, 3));
75
```

```text
First three elements of mySpan: 2 4 6
Last three elements of mySpan: 6 8 10
Middle three elements of mySpan: 4 6 8
```

## 修改子视图的元素会修改原始数据

非 const 数据的子视图可以修改该数据。第77行创建一个 span，查看 `values1` 中从索引1开始的3个元素，然后将其传递给函数 `times2`。第79行显示更新后的 `values1` 元素以确认结果。

```cpp
76    // changing a subview's contents modifies the original data
77    times2(mySpan.subspan(1, 3));
78    std::cout << "\n\nvalues1 after modifying elements via span: ";
79    displaySpan(values1);
80
```

```text
values1 after modifying elements via span: 2 8 12 16 10
```

## 通过 [] 运算符访问视图的元素

与内置数组、`std::array` 和 `std::vector` 一样，你可以通过 `[]` 运算符访问和修改 span 元素，该运算符不提供范围检查。第82行显示索引2处的元素。[^23]

```cpp
81    // access a span element via []
82    std::cout << "\n\nThe element at index 2 is: " << mySpan[2];
83 }
```

```text
The element at index 2 is: 12
```

![](img/7b5e2088e71c7f78681d4ddbcf104c06_397_0.png)

## 检查点

- 1. （正确/错误）span（头文件 `<span>`）使程序能够查看容器中的连续元素，例如内置数组、`std::array` 或 `std::vector`。span 是对容器的“视图”。它“看到”容器的元素，但没有这些元素自己的副本。
  - **答案：** 正确。
- 2. （填空）span 同时封装一个指针和一个表示元素数量的 `______`。
  - **答案：** `size_t`
- 3. （正确/错误）因为 span 是对现有容器的视图，所以修改 span 的元素会修改容器的原始数据。
  - **答案：** 正确。

## 7.11 基于指针的字符串简介

我们已经使用 C++ 标准库的 string 类将字符串表示为成熟的对象。第8章详细介绍了 `std::string` 类。本节介绍从 C 编程语言继承而来的基于指针的字符串。这里，我们将它们称为 C 字符串或字符串，并在指代 C++ 标准库的 string 类时使用 `std::string`。

首选 `std::string`，因为它消除了由操作 C 字符串引起的许多安全问题和错误。但是，在某些情况下需要 C 字符串，例如处理命令行参数时。此外，如果你处理遗留的 C 和 C++ 程序，很可能会遇到基于指针的字符串。

### 字符和字符常量

字符是 C++ 源程序的基本构建块。每个程序都由字符组成——当这些字符按有意义的方式分组时，编译器会将其解释为用于完成任务的指令和数据。程序可以包含字符常量，每个字符常量都是一个整数值，表示为单引号中的字符。字符常量的值是该字符在机器字符集中的整数值。例如，`'z'` 表示字母 z 的整数值（在 ASCII 字符集中为 122；请参阅 https://deitel.com/cpphtp11 上的字符集附录），类型为 char。类似地，`'\n'` 表示换行符的整数值（在 ASCII 字符集中为 10）。

### 基于指针的字符串

C 字符串是一个内置字符数组，以空字符（`'\0'`）结尾，该空字符标记字符串在内存中终止的位置。C 字符串通过指向其第一个字符的指针来访问（无论字符串有多长）。

### 字符串字面量作为初始化器

字符串字面量可以用作内置 char 数组或 `const char*` 类型变量的初始化器。以下每个声明都将一个变量初始化为字符串 `"blue"`：

```cpp
char color[] {"blue"};
const char* colorPtr{"blue"};
```

第一个声明创建一个包含五个元素的内置数组 `color`，其中包含字符 `'b'`、`'l'`、`'u'`、`'e'` 和 `'\0'`。第二个声明创建指针变量 `colorPtr`，指向内存中某处字符串 `"blue"`（以 `'\0'` 结尾）中的字母 `b`。上面的第一个声明也可以使用单个字符的初始化列表来实现，其中你手动包含终止符 `'\0'`，如下所示：

```cpp
char color[] {'b', 'l', 'u', 'e', '\0'};
```

[^22]: C++ Core Guidelines，“P.5：优先选择编译期检查而非运行期检查。”访问于2023年4月14日。https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rp-compile-time。

[^23]: `std::span` 不提供带范围检查的 `at` 成员函数，但将来可能会提供。
