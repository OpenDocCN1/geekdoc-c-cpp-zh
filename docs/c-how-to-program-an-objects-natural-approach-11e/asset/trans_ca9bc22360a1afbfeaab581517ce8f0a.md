
基于范围的 for 语句使用内部迭代，向你隐藏迭代细节。你指定基于范围的 for 应处理哪个数组，它知道如何从数组中获取每个值，并在没有更多值时停止迭代。

### 检查点

- 1. *（判断正误）* 处理数组的所有元素时，应使用基于范围的 for 语句，因为它确保你的代码不会“越出”数组边界。

  **答案：** 正确。

- 2. *（判断正误）* 在基于范围的 for 的初始化器中定义的变量在循环终止后仍然存在。

  **答案：** 错误。实际上，在基于范围的 for 的初始化器中定义的变量只在循环终止前存在。

- 3. *（代码）* 下面的计数器控制的 for 语句输出数组 grades 中的 int 整数。

  ```cpp
  for (int counter{0}; counter < grades.size(); ++counter) {
      std::cout << std::format("{}", grades[counter]);
  }
  ```

  将这个计数器控制的 for 语句转换为基于范围的 for 语句。

  **答案：**

  ```cpp
  for (const int& grade : grades) {
      std::cout << std::format("{}", grade);
  }
  ```

## 6.7 计算数组元素值以及 constexpr 简介

图 6.4 将名为 values 的 5 元素数组的元素设置为偶数整数 2、4、6、8 和 10（第 13—15 行），并打印该数组（第 18—20 行）。第 14 行通过将循环计数器 i 的每个连续值乘以 2 再加 2 来生成值。

```cpp
// fig06_04.cpp
// Set array values to the even integers from 2 to 10.
#include <format>
#include <iostream>
#include <array>

int main() {
    // constant can be used to specify array size
    constexpr size_t arraySize{5}; // must initialize in declaration

    std::array<int, arraySize> values{}; // array values has 5 elements

    for (int i{0}; i < values.size(); ++i) { // set the values
        values.at(i) = 2 + 2 * i;
    }
```

**图 6.4** | 将数组元素设置为从 2 到 10 的偶数整数。（第 1 部分，共 2 部分。）

```cpp
// output contents of array values in tabular format
for (const int& value : values) {
    std::cout << std::format("{} ", value);
}

std::cout << '\n';
}
```

```text
2  4  6  8  10
```

**图 6.4** | 将数组元素设置为从 2 到 10 的偶数整数。（第 2 部分，共 2 部分。）

### 常量

在第 5 章中，我们使用 const 限定符来表示变量的值在初始化后不再改变。有时，编译器会通过在编译期初始化 const 变量来优化代码以获得更好的性能；但这并不保证。constexpr 限定符也可用于声明常量变量。这样的变量隐式地是 const，并且显式地在编译期初始化，从而消除了运行时初始化的可能性。

将数组的大小定义为常量而不是字面量值，可以使程序更清晰、更易于更新。这种技术消除了魔法数——即没有上下文帮助你理解其含义的字面数值。使用常量可以为字面量值提供名称，并有助于解释该值在程序中的用途。

### 初始化后不能修改 constexpr 变量

第 9 行使用 constexpr 声明值为 5 的常量 arraySize。在 arraySize 初始化后尝试修改它，如下所示：

```cpp
arraySize = 7;
```

会导致编译错误。⁶

- Visual C++:

  ```text
  error C3892:
      that is const
  ```

- g++:

  ```text
  error: assignment of read-only variable
  ```

- clang++:

  ```text
  error: cannot assign to variable
  const-qualified type
  ```

6. 在错误消息中，一些编译器将 const 基本类型变量称为“const 对象”。C++ 标准将“对象”定义为任何“存储区域”。与类对象一样，基本类型变量也占用内存空间，因此它们通常被称为“对象”。

### 现代 C++：在编译期做更多事

现代 C++ 的一个主题是在编译期做更多事，以获得更好的运行时性能。**constexpr** 是我们将要介绍的若干特性之一，这些特性可消除运行时开销并提高性能。自 C++11 以来的每个 C++ 标准都扩展了 constexpr 的用途。

在第 15.13 节中，你将看到 constexpr 可以应用于函数。当你使用 constexpr 实参调用这样的函数时，编译器可以确定该调用的最终结果，并用常量替换该调用，从而消除运行时函数调用开销并提高性能。现在，C++ 标准库中的许多函数都声明为 constexpr，以利用这种优化。

今后，我们将把每个值可在编译期确定的变量定义为 constexpr。当我们在第 15.13 节介绍构造函数时，我们将演示 constexpr 函数调用的编译期求值。

![](img/7b5e2088e71c7f78681d4ddbcf104c06_329_0.png)

### ✓ 检查点

- 1. *（填空）* ______ 限定符使你能够声明可在编译期求值并得到常量的变量。

  **答案：** constexpr。

- 2. *（判断正误）* const 变量必须在编译期初始化，但 constexpr 变量可以在执行期初始化。

  **答案：** 错误。实际上，constexpr 变量必须在编译期初始化，但 const 变量可以在执行期初始化。

## 6.8 对数组元素求和

通常，数组元素表示用于计算的一系列值。例如，如果数组的元素表示考试成绩，教授可能希望先将数组元素求和，然后计算该考试的班级平均分。将一组值处理为单个值称为归约——正如我们在第 6.14 节中讨论的，这是一种常见的函数式编程操作。图 6.5 使用基于范围的 for 语句（第 12—14 行）对包含四个 int 元素的数组中的值求和。第 6.14 节展示了如何使用 C++ 标准库的 accumulate 函数执行此计算。

```cpp
// fig06_05.cpp
// Compute the sum of an array
#include <format>
#include <iostream>
#include <array>

int main() {
    std::array items{10, 20, 30, 40}; // type inferred as array<int, 4>
    int total{0};
```

**图 6.5** | 计算数组元素之和（第 1 部分，共 2 部分。）

- 第 8 行使用 `constexpr` 声明该数组，因为程序从不修改 frequencies，并且其值在编译期已知。

- 为了标记每个条形，第 15—21 行根据 `i` 的当前值输出一个成绩范围（例如 "70-79: "）。在第 16—17 行中，格式说明符 `:02d` 表示整数（由 `d` 表示）应使用字段宽度 2 进行格式化，如果整数少于两位，则使用前导 0。在第 20 行中，格式说明符 `:>5d` 表示整数应在字段宽度 5 中右对齐（`>`）。

- 嵌套的 `for` 语句（第 26—28 行）输出当前条形的星号。第 26 行中的循环继续条件（`stars < frequency`）使内层循环从 0 计数到 frequency。因此，frequencies 中的一个值决定要显示的星号数量。在此示例中，frequencies 元素 0—5 包含零，因为没有学生成绩低于 60。因此，程序在前六个成绩范围旁边不显示星号。

```cpp
// fig06_06.cpp
// Printing a student grade distribution as a primitive bar chart.
#include <format>
#include <iostream>
#include <array>

int main() {
    constexpr std::array frequencies{0, 0, 0, 0, 0, 0, 1, 2, 4, 2, 1};

    std::cout << "Grade distribution:\n";

    // for each element of frequencies, output a bar of the chart
    for (int i{0}; const int& frequency : frequencies) {
        // output bar labels ("00-09", ... , "90-99", "100")
        if (i < 10) {
            std::cout << std::format("{:02d}-{:02d}: ",
                i * 10, (i * 10) + 9);
        }
        else {
            std::cout << std::format("{:>5d}: ", 100);
        }

        ++i;

        // print bar of asterisks
        for (int stars{0}; stars < frequency; ++stars) {
            std::cout << '*';
        }

        std::cout << '\n'; // start a new line of output
    }
}
```

**图 6.6** | 将学生成绩分布打印为原始条形图。（第 1 部分，共 2 部分。）
