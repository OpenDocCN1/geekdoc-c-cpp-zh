
### 26.
编写一个完整的程序来测试示例 5-25 中的代码。

### 27. 锥形杯问题
你收到一份制作可以装水的小锥杯的合同。这些杯将由半径为 4 英寸的圆形蜡纸制成，只需去掉长度为 `$x$` 的扇形（见图 5-4）。通过闭合圆形的剩余部分形成锥形杯。你的目标是去掉这个扇形，使得杯子的体积最大。

![](img/d998292a174f7bfd8a26bfbada3d454e_394_0.png)

图 5-4 锥形纸杯

编写一个程序，提示用户输入圆形蜡纸的半径。程序应输出被去掉的扇形的长度，使得生成的杯子体积最大。计算你的答案并保留两位。

### 28. 公寓问题
一家房地产中介管理着 50 套公寓。当租金为每月 `$600` 时，所有公寓都已租出。然而，租金每增加 `$40`，就会有一套公寓空出。此外，每个出租公寓每月平均需要 `$27` 的维护费用。应该出租多少套公寓才能利润最大？

编写一个程序，提示用户输入：

a. 总单元数。
b. 租满所有公寓的租金。
c. 导致公寓空出的租金增加额。
d. 出租公寓的维护费用。

### 29.
令 `$n$` 为非负整数。`$n$` 的阶乘 `$n!$` 定义为：`$0! = 1$`，当 `$n \ge 1$`，`$n! = 1\cdot2\cdot3\dots n$`。例如，`$4! = 1\cdot2\cdot3\cdot4 = 24$`。编写一个程序，提示用户输入一个非负整数并输出该数的阶乘。

### 30.
令 `$n$` 为一个整数。表达式 `$\lim_{n\to\infty}(1+\frac{1}{n})^n$` 的值写作 `$e$`。这个数字 `$e$` 出现在数学的很多地方。它是一个无理数。`$e$` 的九位小数值为 2.718281828。编写一个程序计算表达式 `$\lim_{n\to\infty}(1+\frac{1}{n})^n$` 在特定 `$n$` 值范围内的值，并将这些值与 `$e$` 进行比较。例如，你可以计算 100 到 10,000 之间步长为 100 的值，或者计算 1,000 到 1,000,000 之间步长为 1,000 的值。

## 预定义函数

一些预定义的数学函数包括 `pow(x, y)`、`sqrt(x)` 和 `floor(x)`。

平方根函数 `sqrt(x)` 计算 `x >= 0.0` 时 `x` 的非平方根。例如，`sqrt(2.25) = 1.5`。函数 `sqrt` 的类型为 `double`，且只有一个参数。

取整函数 `floor(x)` 计算小于或等于 `x` 的最大整数。例如，`floor(48.79) = 48.0`。函数 `floor` 的类型为 `double`，且只有一个参数。

在 C++ 中，预定义函数被组织在不同的库中。例如，头文件 `cmath` 包含输入输出函数，而头文件 `cline` 包含数学函数。表 6-1 列出了一些最常用的预定义函数，可以在每个函数规范中找到对应的头文件名称、参数的数据类型以及函数类型。函数类型是函数返回的值的类型。（更多预定义函数列表，请参见附录 E。）

### 表 6-1 预定义函数

| 函数 | 头文件 | 目的 | 参数 | 结果 |
|---|---|---|---|---|
| `abs(x)` | `<cmath>` | 返回其参数的绝对值：`abs (-7) = 7` | `int (double)` | `int (double)` |
| `ceil(x)` | `<cmath>` | 返回小于 `x` 的最小整数：`ceil(56.34) = 57.0` | `double` | `double` |
| `cos(x)` | `<cmath>` | 返回角度 `x` 的余弦：`cos(0.0) = 1.0` | `double` (弧度) | `double` |
| `exp(x)` | `<cmath>` | 返回 `$e^*$`，其中 `$e = 2.718$`：`exp(1.0) = 2.7182` | `double` | `double` |

### 表 6-1 预定义函数（续）

| 函数 | 头文件 | 目的 | 参数类型 | 结果 |
|---|---|---|---|---|
| `fabs (x)` | `<cmath>` | 返回其参数的绝对值：`fabs (-5.67) = 5.67` | `double` | `double` |
| `floor (x)` | `<cmath>` | 返回不大于 `x` 的最大整数：`floor(45.67) = 45.00` | `double` | `double` |
| `islower (x)` | `<ctype>` | 如果 `x` 是小写字母则返回 true；否则返回 false；`islower('h')` 为 true | `int` | `int` |
| `isupper (x)` | `<ctype>` | 如果 `x` 是大写字母则返回 true；否则返回 false；`isupper('K')` 为 true | `int` | `int` |
| `pow(x, y)` | `<cmath>` | 返回 `$x^y$`；如果 `y` 为负数，则 `y` 必须是整数：`pow(0.16, 0.5) = 0.4` | `double` | `double` |
| `sqrt (x)` | `<cmath>` | 返回 `x` 的非平方根；`x` 必须是非负数：`sqrt(4.0) = 2.0` | `double` | `double` |
| `towlower (x)` | `<ctype>` | 如果 `x` 是大写字母则返回其小写值；否则返回 `x` | `int` | `int` |
| `toupper (x)` | `<ctype>` | 如果 `x` 是小写字母则返回其大写值；否则返回 `x` | `int` | `int` |

要在程序中使用预定义函数，必须通过 `include` 语句包含该函数规范的头文件。例如，要使用函数 `pow`，你的程序需要包含：

```cpp
#include <cmath>
```

示例 6-1 展示了如何使用其中一些预定义函数。

### 示例 6-1

```cpp
// 如何使用预定义函数。
#include <iostream>
#include <cmath>
#include <cctype>
#include <iomanip>

using namespace std;

int main() {
    int num;
    double firstName, secondNum;
    char ch = 'T';

    cout << fixed << showpoint << setprecision(2);

    cout << "Line 12: Is " << ch << " a lowercase" << endl;
    cout << "Line 13: Uppercase is a " << static_cast<char>(toupper('a')) << endl;

    cout << "Line 14: 4.5 to the power of 6.0 = " << pow(4.5, 6.0) << endl;

    cout << "Line 15: Enter two decimal numbers: ";
    cin >> firstName >> secondNum;

    cout << "Line 18: " << firstName << " to the power of " << secondNum << " = " << pow(firstName, secondNum) << endl;

    cout << "Line 19: 5.0 to the power of 4 = " << pow(5.0, 4) << endl;

    firstNum = firstName + pow(3.5, 7);
    cout << "Line 21: firstNum = " << firstNum << endl;

    num = -3;
    cout << "Line 23: Absolute value of " << num << " = " << abs(num) << endl;

    cout << "Line 24: Square root of 2.0 = " << sqrt(2.0) << endl;

    return 0;
}
```

**示例运行：** 在此示例运行中，用户输入

```
Line 12: Is T a lowercase letter?
Line 13: Uppercase is a A
Line 14: 4.5 to the power of 6.0 = 8303.77
Line 15: Enter two decimal numbers: 5.5 7.0
Line 18: 5.5 to the power of 7.0 = 15243.52
Line 19: 5.0 to the power of 4 = 625.00
Line 21: firstNum = 73.50
Line 23: Absolute value of -3 = 3
Line 24: Square root of 2.0 = 1.41
```

该程序的工作如下：第 1 到 4 语句包含了程序中使用函数所需的头文件。第 8 到 10 语句声明了程序中使用的变量。第 11 语句以固定格式和两位小数设置数字输出。第 12 语句使用 `islower` 函数判断输出是否为小写字母。第 13 语句使用 `toupper` 函数输出对应于 `'a'` 的大写字母。注意 `toupper` 函数返回 `int` 值。因此，表达式 `toupper('a')` 的值为 65，即 `'a'` 的 ASCII 值。要打印字符，需要像第 13 语句所示应用转换运算符。第 14 语句使用函数 `pow` 输出 4.5。在 C++ 术语中，可以说函数 `pow` 被带有参数 4.5 和 6.0 调用。第 15 到 17 语句提示用户输入两个小数，并将用户输入的数字存储在变量 `firstName` 和 `secondNum` 中。第 18 语句使用函数 `pow` 输出 `firstName` 和 `secondNum`。在这种情况下，函数 `pow` 被带有参数 `firstName` 和 `secondNum` 调用`firstName` 和 `secondNum` 的值传递给函数 `pow`。其他语句含义相似。再次注意，程序包含了 `ctype` 和 `cmath` 头文件，因为它使用了这些头文件中的 `islower`、`toupper`、`pow`、`abs` 和 `sqrt` 函数。

## 自定义函数

示例 6-1 说明，在程序中使用函数可以大大提高程序的可读性，因为它降低了 `main` 函数的复杂度。此外，一旦你编写并调试了一个函数，就可以反复在程序（或不同的程序）中使用它，而无需重复编写相同的代码。例如，在示例 6-1 中，`pow` 函数被使用了多次。

由于 C++ 不会提供你可能需要的每一个函数，且设计者无法预测用户的需求，你必须学习编写自己的函数。

C++ 中的自定义函数分为两类：

- **返回值的函数**：具有返回类型的函数。这些函数使用 `return` 语句返回特定数据类型的值，我们稍后会解释。注意到为止的每个程序中 `main` 函数都使用 `return` 语句返回值 0。
- **void 函数**：没有返回类型的函数。这些函数不使用 `return` 语句返回值。

我们将首先讨论返回值的函数。关于返回值的函数的许多概念也适用于 void 函数。

## 返回值的函数

上一节介绍了一些预定义的 C++ 函数，如 `pow`、`abs`、`islower` 和 `toupper`。这些都是返回值的函数示例。要在你的程序中使用这些函数，你必须知道需要包含的头文件（并通过 `include` 语句在程序中包含该头文件），并知道：

1. 函数的名称
2. 参数（如果有）
3. 每个参数的数据类型
4. 函数计算的值（即返回的值）的数据类型，称为函数类型

前四个属性构成了函数的头部（也称为函数头）；第五个属性被称为函数的体体。这五个属性共同构成了所谓的函数定义。例如，对于函数 `abs`，其头部可能如下所示：

```
int abs(int number)
```

同样，函数 `abs` 可能具有以下定义：

```
{
if (number < 0)
number = -number;
return number;
}
```

在函数 `abs` 头部中声明的变量被称为函数 `abs` 的**形式参数**。因此，`abs` 的形式参数是 `number`。

示例 6-1 中的程序包含多个使用 `pow` 函数的语句。也就是说，在 C++ 术语中，函数 `pow` 被调用了多次。在本章的后面，我们将发现当函数被调用时会发生什么。

假设函数 `pow` 的头部为：

```
double pow(double base, double exponent)
```

从函数 `pow` 的头部可以看出，`pow` 的形式参数是 `base` 和 `exponent`。考虑以下语句：

```
double u = 2.5;
double v = 3.0;
x, y;
```

```
x = pow(u, v); // Line 1
y = pow(2.0, 3.2) + 5.1; // Line 2
cout << u << " to the power of 7 = " << pow(u, 7) << endl; // Line 3
```

在第 1 行，使用参数 `u` 和 `v` 调用了函数 `pow`。在这种情况下，`u` 和 `v` 的值被传递给函数 `pow`。事实上，`u` 的值被复制到函数 `pow` 的调用中，`v` 的值被复制到 `exponent`。第 1 行调用中变量 `u` 和 `v` 是调用的**实际参数**。在第 2 行，使用参数 `2.0` 和 `3.2` 调用了函数 `pow`。在这种情况下，值 `2.0` 被复制到 `base`，`3.2` 被复制到 `exponent`。此外，在这次函数 `pow` 的调用中，实际参数分别为 `2.0` 和 `3.2`。同样，在第 3 行，函数 `pow` 的实际参数是 `u` 和 `7`；`u` 的值被复制到 `base`，`7.0` 被复制到 `exponent`。

我们现在给出两个定义：

- 形式参数（Formal Parameter）：在函数头部中声明的变量。
- 实际参数（Actual Parameter）：在函数调用中列出的变量或表达式。

对于预定义函数，你只需要关注前四个属性。通常情况下，软件公司不会提供实际源代码（即函数的体）。

## 语法：返回值函数

返回值函数的语法为：

```
functionType functionName (formal parameter list)
{
    statements
}
```

其中 `statements` 通常是声明语句和/或可执行语句。在这种语法中，`functionType` 是函数返回的值的类型。`functionType` 也称为返回值函数的**数据类型**或**返回类型**。此外，封装在花括号之间的语句构成了函数体。

## 语法：形式参数列表

形式参数列表的语法为：

```
dataType identifier, dataType identifier, ...
```

考虑本章之前给出的函数 `abs` 定义。图 6-1 标识了该函数的各个部分。

![](img/d998292a174f7bfd8a26bfbada3d454e_404_0.png)

图 6-1 函数 abs 的各个部分

## 函数调用

调用返回值函数的语法为：

```
functionName (actual parameter list)
```

例如，在表达式 `x = abs (-5);` 中，调用了 `abs` 函数。

## 语法：实际参数列表

实际参数列表的语法为：

```
expression or variable, expression or variable, ...
```

因此，要调用一个返回值函数，你使用它的名称，并在括号中带有实际参数（如果有的话）。

函数的形式参数列表可以是空的。但是，如果形式参数列表为空，返回值函数的头部将采取以下形式：

```
functionType functionName()
```

如果返回值函数的形式参数列表为空，则在函数调用中的实际参数也是空的。在这种情况下（即形式参数列表为空），仍然需要空括号。因此，带有空参数列表的返回值函数的调用为：

```
functionName()
```

在函数调用中，实际参数的数量及其数据类型必须按照给定的顺序与形式参数匹配。

## return 语句

一旦返回值函数计算出值，该函数将通过 `return` 语句返回该值。

## 语法：return 语句

`return` 语句的语法如下：

```
return expr;
```

其中 `expr` 是变量、常量或表达式。`expr` 的数据类型必须匹配函数类型。

## 返回值函数

在 C++ 中，`return` 是关键字。当函数执行 `return` 语句时，函数立即终止并返回调用函数。此外，`return` 语句将此值传递到外部。

为了使这些讨论生效，让我们编写一个确定两个数字较大值的函数。因为数字的数据类型是 `double`，你可以这样写函数：

```
double larger(double x, double y)
{
double max;
if (x >= y)
    max = x;
else
    max = y;
return max;
}
```

函数 `larger` 使用了一个额外的变量（称为局部声明）。图 6-2 描述了函数 `larger` 的各个部分。

![](img/d998292a174f7bfd8a26bfbada3d454e_406_0.png)

图 6-2 函数 larger 的各个部分

# 354 | 第6章：用户定义函数
