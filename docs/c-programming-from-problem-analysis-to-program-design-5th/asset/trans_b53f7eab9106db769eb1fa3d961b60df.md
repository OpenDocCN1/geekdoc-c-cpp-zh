
**示例运行 2：**

```
Line 2: Enter the dividend: 24
Line 5: Enter the divisor: 0
Assertion failed: divisor !=0, file c:\chapter 16 source code\ch16_exp3.cpp,
line 20
```

在示例运行 1 中，除数的值非零，因此不会发生异常。程序计算并输出商，然后正常终止。

在示例运行 2 中，为除数输入的值是 0。在第 8 行，函数 assert 检查除数是否非零。由于除数为 0，assert 语句中的表达式求值为 false，函数 assert 以输出中第三行所示的错误消息终止程序。

## C++ 异常处理机制

示例 16-1 至 16-3 展示了程序中发生异常且未被处理时会出现什么情况。本节介绍如何在程序中包含处理异常所需的代码。

### try/catch 块

可能产生异常的语句放在 try 块中。try 块还包含在发生异常时不应执行的语句。try 块后面跟着一个或多个 catch 块。catch 块指定它能捕获的异常类型，并包含一个异常处理程序。

try/catch 块的一般语法是：

```
try
{
    //statements
}
catch (dataType identifier)
{
    //exception-handling code
}
.
.
.
catch (dataType identifier)
{
    //exception-handling code
}
.
.
.
catch (...)
{
    //exception-handling code
}
```

假设有一条可能产生异常的语句，例如除以 0。通常，在执行这样的语句之前，我们会检查是否满足某些条件。例如，在执行除法之前，我们会检查除数是否非零。如果不满足条件，我们通常会生成一个异常，在 C++ 术语中这称为抛出异常。这通常使用 `throw` 语句完成，我们很快会解释它。我们将展示通常会抛出什么来生成异常。

现在让我们注意以下关于 `try`/`catch` 块的要点。

- 如果 `try` 块中没有抛出异常，那么与该 `try` 块关联的所有 `catch` 块都会被忽略，程序执行会从最后一个 `catch` 块之后继续。
- 如果 `try` 块中抛出了异常，该 `try` 块中剩余的语句会被忽略。程序会按照 `catch` 块在 `try` 块之后出现的顺序搜索这些 `catch` 块，寻找合适的异常处理程序。如果抛出的异常类型与某个 `catch` 块中的参数类型匹配，则执行该 `catch` 块的代码，并且该 `catch` 块之后剩余的 `catch` 块会被忽略。
- 最后一个带有省略号（三个点）的 `catch` 块用于捕获任何类型的异常。

考虑下面的 `catch` 块：

```
catch (int x)
{
    //exception-handling code
}
```

在这个 `catch` 块中：

- 标识符 `x` 充当参数。实际上，它被称为 `catch` 块参数。
- 数据类型 `int` 指定这个 `catch` 块可以捕获 `int` 类型的异常。
- 一个 `catch` 块*至多*可以有一个 `catch` 块参数。

本质上，`catch` 块参数会成为所抛出值的占位符。在这种情况下，`x` 成为任何 `int` 类型抛出值的占位符。换句话说，如果抛出的值被这个 `catch` 块捕获，那么该抛出值会存储在 `catch` 块参数中。这样，如果异常处理代码想对该值执行某些操作，就可以通过 `catch` 块参数访问它。

假设在 `catch` 块头部只指定了数据类型，也就是说没有 `catch` 块参数。那么，在 `catch` 块的异常处理代码中可能无法访问所抛出的值。

### 抛出异常

为了让异常在 `try` 块中发生并被 `catch` 块捕获，必须在 `try` 块中抛出该异常。抛出异常的一般语法是：

```
throw expression;
```

其中 **表达式** 是常量值、变量或对象。被抛出的对象可以是特定对象，也可以是匿名对象。由此可知，在 C++ 中，*异常是一个值。*

在 C++ 中，**throw** 是保留字。

示例 16-4 说明如何使用 **throw** 语句。

### 示例 16-4

假设有如下声明：

```
int num = 5;
string str = "Something is wrong!!!";
```

| throw 表达式 | 效果 |
|---|---|
| `throw 4;` | 抛出常量值 4。 |
| `throw x;` | 抛出变量 x 的值。 |
| `throw str;` | 抛出对象 str。 |
| `throw string("Exception found!");` | 抛出一个匿名 string 对象，其字符串为 "Exception found!"。 |

### catch 块的顺序

**catch** 块既可以捕获某一特定类型的所有异常，也可以捕获所有类型的异常。**catch** 块的头部指定它处理的异常类型。如前所述，带有省略号（三个点）的 **catch** 块用于捕获任何类型的异常。因此，如果我们把这个 **catch** 块放在最前面，那么这个 **catch** 块就能捕获所有类型的异常。

假设在 **try** 块中发生异常，并被某个 **catch** 块捕获。那么，与该 **try** 块关联的其余 **catch** 块会被忽略。因此，应当注意在 **try** 块之后列出 **catch** 块的顺序。例如，考虑下面这组 **try/catch** 块：

```
try                         //Line 1
{
    //statements
}
catch (...)                  //Line 2
{
    //statements
}
catch (int x)                //Line 3
{
    //statements
}
```

假设在 `try` 块中抛出了异常。由于第 2 行的 `catch` 块可以捕获所有类型的异常，第 3 行的 `catch` 块无法到达。对于这组 `try`/`catch` 块，某些编译器实际上可能会给出语法错误（请查阅编译器的文档）。

在一组 `try`/`catch` 块中，如果需要带有省略号（在头部）的 `catch` 块，那么它应该是该组中的最后一个 `catch` 块。

### 在程序中使用 `try`/`catch` 块

接下来，我们提供一些示例，说明 `try`/`catch` 块在程序中可能如何出现。

执行数值计算时可能发生的一个常见错误是整数除以零。如果在程序执行期间发生整数除以零且程序未处理，程序可能会以错误消息终止，或者可能只是挂起。示例 16-5 展示如何处理除零异常。

### 示例 16-5

本示例说明如何捕获和处理除以零异常。它还展示 `try`/`catch` 块在程序中可能如何出现。

```cpp
// Handling division by zero exception.

#include <iostream>

using namespace std;

int main()
{
    int dividend, divisor, quotient;                 //Line 1

    try                                           //Line 2
    {
        cout << "Line 3: Enter the dividend: ";    //Line 3
        cin >> dividend;                           //Line 4
        cout << endl;                              //Line 5

        cout << "Line 6: Enter the divisor: ";     //Line 6
        cin >> divisor;                            //Line 7
        cout << endl;                              //Line 8

        if (divisor == 0)                          //Line 9
            throw 0;                               //Line 10

        quotient = dividend / divisor;             //Line 11

        cout << "Line 12: Quotient = " << quotient
             << endl;                              //Line 12
    }
    catch (int)                                    //Line 13
```

**示例运行 1：** 在此示例运行中，用户输入以底纹显示。

第 4 行：输入被除数：**23**

第 7 行：输入除数：**6**

第 17 行：商 = 3

**示例运行 2：** 在此示例运行中，用户输入以底纹显示。

第 4 行：输入被除数：**34**

第 7 行：输入除数：**-6**

第 21 行：除数为负。

**示例运行 3：** 在此示例运行中，用户输入以底纹显示。

第 4 行：输入被除数：**34**

第 7 行：输入除数：**g**

第 21 行：输入流处于失败状态。

在这个程序中，第 1 行和第 2 行的语句声明了程序中使用的变量。注意，string 对象 inpStr 也被初始化。

第 4 行至第 9 行的语句将数据输入到变量 dividend 和 divisor 中。第 10 行的语句检查 divisor 是否为 0；第 12 行的语句检查 divisor 是否为负；第 14 行的语句检查标准输入流是否处于失败状态。

第 11 行的语句抛出变量 divisor；第 13 行的语句抛出一个匿名 string 对象，其字符串为 "Negative divisor."；第 15 行的语句抛出对象 inpStr。

第 18 行的 catch 块捕获 int 类型的异常，第 20 行的 catch 块捕获 string 类型的异常。如果异常由第 11 行的语句抛出，则由第 18 行的 catch 块捕获并处理。如果异常由第 13 行或第 15 行的语句抛出，则由第 20 行的 catch 块捕获并处理。

在示例运行 1 中，程序没有遇到任何问题。在示例运行 2 中，发生了除以负数的情况。在示例运行 3 中，标准输入流进入失败状态。

## 使用 C++ 异常类

C++ 通过类层次结构提供处理异常的支持。类 exception 是用于处理异常的类的基类。除其他内容外，该类还包含函数 what。函数 what 返回一个字符串，其中包含一个
