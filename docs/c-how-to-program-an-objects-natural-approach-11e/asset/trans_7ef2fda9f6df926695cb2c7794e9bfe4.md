
```cpp
// initialize elements of array values to 0
for (size_t i{0}; i < values.size(); ++i) {
   values[i] = 0; // set element at location i to 0
}

std::cout << std::format("{:>7}{:>10}\n", "Element", "Value");

// output each array element
for (size_t i{0}; i < values.size(); ++i) {
   std::cout << std::format("{:>7}{:>10}\n", i, values[i]);
}

std::cout << std::format("\n{:>7}{:>10}\n", "Element", "Value");

// access elements via the at member function
for (size_t i{0}; i < values.size(); ++i) {
   std::cout << std::format("{:>7}{:>10}\n", i, values.at(i));
}

// accessing an element outside the array
values.at(10); // throws an exception
}
```

| 元素 | 值 |
| ---: | ---: |
| 0 | 0 |
| 1 | 0 |
| 2 | 0 |
| 3 | 0 |
| 4 | 0 |

| 元素 | 值 |
| ---: | ---: |
| 0 | 0 |
| 1 | 0 |
| 2 | 0 |
| 3 | 0 |
| 4 | 0 |

```text
terminate called after throwing an instance of
  what():  array::at: __n (which is 10) >= _Nm (which is 5)
Aborted
```

**图 6.1** | 将数组元素初始化为零并打印该数组。（第 2 部分，共 2 部分。）

### 在循环中为数组元素赋值

第 11–13 行使用 for 语句将 0 赋给每个数组元素。与其他非静态局部变量一样，数组元素不会被隐式初始化为零，但静态数组的元素会。在处理数组元素的循环中，要确保循环条件能防止访问数组边界之外的元素。6.6 节介绍基于范围的 for 语句，它提供了一种更安全的方式来处理数组的每个元素。

### 类型 `size_t`

第 11、18 和 25 行将每个循环的控制变量声明为 `size_t` 类型。C++ 标准规定，`size_t` 是一种无符号整型，能够表示任何对象的大小。<sup>2</sup> 对于表示数组大小或下标的任何变量，请使用此类型。类型 `size_t` 定义在 `std` 命名空间中，位于头文件 `<cstddef>` 中；使用 `size_t` 的其他标准库头文件通常会为你包含该头文件。如果你编译程序时收到错误，指出 `size_t` 未定义，请在程序中添加 `#include <cstddef>`。

### 显示数组元素

第一条输出语句（第 15 行）显示后续 for 语句（第 18–20 行）所打印各行的列标题。这些输出语句使用 4.6 节介绍的 C++20 文本格式化功能，以表格形式输出数组。

### 避免安全漏洞：数组下标的边界检查

当你使用 `[]` 运算符访问数组元素时（如第 11–13 行和第 18–20 行所示），C++ **不提供自动数组边界检查**来防止你引用**不存在的元素**。因此，正在执行的程序可能在没有警告的情况下“越界访问”数组的任一端。然而，类模板 `array` 的 `at` 成员函数会执行边界检查。第 25–27 行演示了通过 `at` 成员函数访问元素的值。你也可以在赋值号左侧使用 `at` 为数组元素赋值，如下所示

```cpp
values.at(0) = 10;
```

第 30 行试图访问数组边界之外的元素。**当成员函数 `at` 遇到越界下标时，它会生成一种称为异常的运行时错误。** 在本程序中（我们使用 GNU g++ 编译并在 Linux 上运行），第 30 行导致以下运行时错误消息，随后程序终止：

```text
terminate called after throwing an instance of
  what():  array::at: __n (which is 10) >= _Nm (which is 5)
Aborted
```

此错误消息表明，`at` 成员函数（`array::at`）检查名为 `__n` 的变量（其值为 10）是否大于或等于名为 `_Nm` 的变量（其值为 5）。在本例中，下标越界。在 GNU 对 `array` 的 `at` 成员函数的实现中，`__n` 表示元素的下标，`_Nm` 表示数组的大小。6.15 节介绍如何使用异常处理来处理运行时错误。第 12 章深入讨论异常处理。

**允许程序读写数组边界之外的数组元素是常见的安全缺陷。** 从越界数组元素读取可能导致程序崩溃，甚至可能在使用错误数据的情况下看似正确执行。写入越界元素（称为缓冲区溢出³）可能破坏程序在内存中的数据并导致程序崩溃。攻击者有时可以通过用恶意代码覆盖程序的可执行代码来利用缓冲区溢出。

- 2. C++ 标准，“17.2.4 大小、对齐和偏移。”访问于 2023 年 4 月 14 日。https://timsong-cpp.github.io/cppwp/n4861/support.types#layout-3。
- 3. 有关缓冲区溢出的更多信息，请参见 http://en.wikipedia.org/wiki/Buffer_overflow。

![](img/7b5e2088e71c7f78681d4ddbcf104c06_323_0.png)

### 检查点

- 1. *（正/误）* C++ 提供自动数组边界检查，以防止你引用不存在的数组元素。因此，正在执行的程序不能在无警告的情况下“越界访问”数组的任一端。
  
  **答案：** 错误。实际上，C++ 不提供自动数组边界检查来防止你引用不存在的元素。因此，正在执行的程序可能在没有警告的情况下“越界访问”数组的任一端。
- 2. *（代码）* 假设数组 numbers 存在并包含 int 值。以下代码做什么？
  
  ```cpp
  for (size_t i{0}; i < numbers.size(); ++i) {
      numbers[i] = 1; // set element at location i to 1
  }
  ```
  
  **答案：** 该代码将 numbers 的每个元素设置为 1。

## 6.5 使用初始化列表初始化数组

数组元素也可以在数组声明中初始化：在数组名后跟一个用花括号限定、以逗号分隔的初始化器列表。图 6.2 中的程序使用初始化列表将一个 int 数组初始化为五个值（第 8 行），并将一个 double 数组初始化为四个值（第 18 行），然后显示每个数组的内容：

- 第 8 行显式告诉编译器数组的元素类型（`int`）和大小（5）。
- 第 18 行让编译器根据初始化列表中的值确定数组的元素类型（`double`），并根据初始化器的数量确定数组的大小（4）。这种能力称为类模板实参推导（CTAD）⁴，当你事先知道容器的初始元素值时，它可以简化代码。

```cpp
// fig06_02.cpp
// Initializing an array in a declaration.
#include <format>
#include <iostream>
#include <array>

int main() {
    std::array<int, 5> values{32, 27, 64, 18, 95}; // braced initializer

    // output each array element
    for (size_t i{0}; i < values.size(); ++i) {
        std::cout << std::format("{} ", values.at(i));
    }

    std::cout << "\n\n";
}
```

**图 6.2** 在声明中初始化数组。（第 1 部分，共 2 部分。）

- 4. “类模板实参推导（CTAD）。”访问于 2023 年 4 月 14 日。https://en.cppreference.com/w/cpp/language/class_template_argument_deduction。

## 6.6 基于范围的 for 语句

处理数组的所有元素是很常见的。基于范围的 for 语句允许你在不使用计数器的情况下做到这一点。在处理数组的所有元素时，请使用基于范围的 for 语句，以确保你的代码不会“越出”数组边界。本节末尾，我们将比较计数器控制的 for 语句和基于范围的语句。图 6.3 使用基于范围的 for 显示数组内容（第 12–14 行和第 23–25 行），并将每个元素的值乘以 2（第 17–19 行）。

```cpp
// fig06_03.cpp
// Using range-based for.
#include <format>
#include <iostream>
#include <array>

int main() {
    std::array items{1, 2, 3, 4, 5}; // type inferred as array<int, 5>

    // display items before modification
    std::cout << "items before modification: ";
    for (const int& item : items) { // item is a reference to a const int
        std::cout << std::format("{} ", item);
    }

    // multiply the elements of items by 2
    for (int& item : items) { // item is a reference to an int
        item *= 2;
    }

    // display items after modification
    std::cout << "\nitems after modification: ";
    for (const int& item : items) {
        std::cout << std::format("{} ", item);
    }

    // sum elements of items using range-based for with initialization
    std::cout << "\n\ncalculating a running total of items";
    for (int runningTotal{0}; const int& item : items) {
        runningTotal += item;
        std::cout << std::format("item: {}; running total: {}\n",
            item, runningTotal);
    }
}
```

```text
items before modification: 1 2 3 4 5
items after modification: 2 4 6 8 10

calculating a running total of items
item: 2; running total: 2
item: 4; running total: 6
item: 6; running total: 12
item: 8; running total: 20
item: 10; running total: 30
```

**图 6.3** | 使用基于范围的 for。

