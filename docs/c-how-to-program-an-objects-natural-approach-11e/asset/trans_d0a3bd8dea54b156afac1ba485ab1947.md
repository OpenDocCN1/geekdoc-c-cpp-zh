
### 检查点

1. **（填空）** runtime_error 的典型派生类只定义了一个 ________。
   **答案：** 将错误消息字符串传递给基类构造函数的构造函数。
2. **（填空）** 通常，应从 ________ 派生自定义异常类，并选择一个能清楚表明发生了什么问题的名称。
   **答案：** C++ 标准库异常类。

## 12.2.2 演示异常处理

图 12.2 使用异常处理来包装可能抛出 DivideByZeroException 的代码，并在发生该异常时处理它。quotient 函数接收两个 double 值，用第一个除以第二个并返回 double 结果。该函数将所有除以零的尝试都视为错误。如果第二个实参为零，它会抛出 DivideByZeroException（第 13 行），以向调用者表明此问题。throw 操作数可以是任何可复制构造类型的对象，而不仅是 exception 及其派生类型。之所以要求可复制构造类型，是因为异常机制会把异常复制到一个临时异常对象中。^15

```cpp
// fig12_02.cpp
// Example that throws an exception on
// an attempt to divide by zero.
#include <format>
#include <iostream>
#include "DivideByZeroException.h" // DivideByZeroException class

// performs division only if the denominator is not zero;
// otherwise, throws DivideByZeroException object
double quotient(double numerator, double denominator) {
    // throw DivideByZeroException if trying to divide by zero
    if (denominator == 0.0) {
        throw DivideByZeroException{};
    }

    // return division result
    return numerator / denominator;
}

int main() {
    int number1{}; // user-specified numerator
    int number2{}; // user-specified denominator

    std::cout << "Enter two integers (end-of-file to end): ";

    // enable user to enter two integers to divide
    while (std::cin >> number1 >> number2) {
       // try block contains code that might throw exception
       // and code that will not execute if an exception occurs
       try {
          double result{quotient(number1, number2)};
          std::cout << std::format("The quotient is: {:.2f}\n", result);
       }
       catch (const DivideByZeroException& divideByZeroException) {
          std::cout << std::format("Exception occurred: {}\n",
             divideByZeroException.what());
       }

       std::cout << "\nEnter two integers (end-of-file to end): ";
    }

    std::cout << '\n';
}
```

**图 12.2** | 在尝试除以零时抛出异常的示例。（第 1 部分，共 2 部分。）

**图 12.2** | 在尝试除以零时抛出异常的示例。（第 2 部分，共 2 部分。）

![](img/7b5e2088e71c7f78681d4ddbcf104c06_718_0.png)

假设用户没有将 0 指定为除法的分母，`quotient` 会返回除法结果。如果用户为分母输入 0，`quotient` 会抛出异常。在这种情况下，main 会处理该异常，然后在再次调用 `quotient` 之前要求用户输入两个新值。这样，即使输入不当，程序也能继续执行，使程序更健壮。在示例输出中，前两行显示一次成功计算，接下来两行显示因尝试除以零而导致的失败。讨论完代码后，我们将考虑产生图 12.3 所示输出的用户输入和控制流。

### 检查点

- **（填空）** throw 的操作数可以是任何 ______ 类型，而不仅是直接或间接派生自 exception 的类型的对象。
  
  **答案：** 可复制构造

## 12.2.3 将代码包含在 try 块中

程序提示用户输入两个整数，然后在 while 循环的条件中（第 27 行）输入它们。第 31 行将这些值传递给 `quotient`（第 10–18 行），该函数要么对整数进行除法并返回结果，要么在用户尝试除以零时抛出异常。

`quotient` 中的第 13 行称为抛出点。异常处理适用于检测到错误的函数无法执行其任务的情况。¹⁶

第 30–33 行的 try 块执行两条语句：

- 对 `quotient` 函数的调用（第 31 行），它可能抛出异常，以及
- 显示除法结果的语句（第 32 行）。

仅当 `quotient` 成功返回结果时，第 32 行才会执行。

## 12.2.4 为 DivideByZeroException 定义 catch 处理程序

每个 try 块后必须立即至少有一个 catch 处理程序（第 34–37 行）。**异常参数应声明为对要处理的异常类型的 const 引用**——在本例中，即对 DivideByZeroException 的 const 引用。这有两个关键好处：

- 它防止在 catch 操作过程中复制异常。
- 它使得能够捕获派生类异常而不会发生切片（见下文）。

### 按引用捕获可避免切片

当 try 块中发生异常时，C++ 会执行**第一个 catch 处理程序**，其参数类型与所抛出异常的类型相同，或者是该类型的基类类型。如果基类 catch 处理程序**按值**捕获派生类异常对象，则只会将派生类异常对象的基类部分复制到异常参数中。这种逻辑错误称为切片，当派生类对象被复制或赋值给基类对象时就会发生。始终按**引用捕获异常以防止切片**。

### catch 参数名

包含*可选*参数名的异常参数（如第 34 行）使 catch 处理程序能够与被捕获的异常交互。第 36 行调用其 `what` 成员函数以获取异常的错误消息。

### catch 处理程序中执行的任务

catch 处理程序执行的典型任务包括

- 将错误记录到文件中，供开发人员研究以进行调试，
- 优雅地终止程序，
- 尝试替代策略以完成失败的任务，
- 将异常重新抛给当前函数的调用者，或
- 抛出不同的异常类型。

为演示目的，本示例的 catch 处理程序仅报告用户试图除以零。

16. C++ 核心准则，“E.2：抛出异常以表明函数无法执行其分配的任务。”访问于 2023 年 4 月 18 日。https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#e-throw.

### 定义 catch 处理程序时的常见错误

刚接触异常处理的程序员应注意几种常见的编码错误：

- 在 try 块与其对应的 catch 处理程序之间，或在各 catch 处理程序之间放置代码，属于语法错误。
- 每个 catch 处理程序只能有一个参数——指定以逗号分隔的异常参数列表属于语法错误。
- 在单个 try 块后的多个 catch 处理程序中捕获相同类型，属于编译错误。
- 在派生类异常之前捕获基类异常，属于逻辑错误——发生这种情况时，编译器通常会警告你。

### 检查点

1. **（填空）** 将每个异常参数声明为 ________，以防止复制异常对象并能够捕获派生类异常。
   **答案：** 对要处理的异常类型的 const 引用。
2. **（填空）** 当 try 块中发生异常时，C++ 执行第一个 catch 处理程序，其参数类型与所抛出异常的类型相同，或者是该类型的 ________。
   **答案：** 基类类型
3. **（填空）** 当派生类对象被复制到基类对象中或赋值给基类对象时，会发生称为 ________ 的逻辑错误。
   **答案：** 切片。

## 12.2.5 异常处理的终止模型

如果 try 块中没有发生异常，程序控制会继续执行该 try 块后最后一个 catch 之后的第一个语句。如果确实发生异常，try 块会立即终止——该块中定义的任何局部变量都会离开作用域。这是异常处理的一个优势。try 块局部变量的析构函数保证会运行，使程序能够避免资源泄漏。¹⁷ 接下来，程序会搜索并执行第一个匹配的 catch 处理程序。如果执行到达该 catch 处理程序的右花括号 (})，则认为异常已处理。catch 处理程序中的任何局部变量（包括 catch 参数）都会离开作用域。

C++ 使用异常处理的终止模型，在这种模型中，程序控制不能返回到抛出点。相反，控制会从 try 块最后一个 catch 处理程序之后的第一个语句（第 39 行）继续。

如果函数中发生异常且未在该函数中捕获，该函数会立即终止。程序会尝试在调用函数中定位一个外围 try 块。这一过程称为栈展开，将在第 12.5 节讨论。

17. “C++ 性能技术报告”，2006 年 2 月 15 日。访问于 2023 年 4 月 18 日。http://www.open-std.org/jtc1/sc22/wg21/docs/TR18015.pdf（第 34 页）。
