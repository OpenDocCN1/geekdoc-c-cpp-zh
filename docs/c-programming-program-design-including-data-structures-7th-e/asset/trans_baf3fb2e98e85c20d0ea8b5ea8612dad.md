
### 表 6-1 预定义函数（续）

| 函数 | 头文件 | 用途 | 参数类型 | 结果 |
|---|---|---|---|---|
| `floor(x)` | `<cmath>` | 返回不大于 x 的最大整数：`floor(45.67) = 45.00` | `double` | `double` |
| `islower(x)` | `<cctype>` | 如果 x 是小写字母，则返回 1（真）；否则返回 0（假）；`islower('h')` 为 1（真） | `int` | `int` |
| `isupper(x)` | `<cctype>` | 如果 x 是大写字母，则返回 1（真）；否则返回 0（假）；`isupper('K')` 为 1（真） | `int` | `int` |
| `pow(x, y)` | `<cmath>` | 返回 x<sup>y</sup>；如果 x 为负数，则 y 必须是整数：`pow(0.16, 0.5) = 0.4` | `double` | `double` |
| `sqrt(x)` | `<cmath>` | 返回 x 的非负平方根；x 必须非负：`sqrt(4.0) = 2.0` | `double` | `double` |
| `tolower(x)` | `<cctype>` | 如果 x 是大写字母，则返回 x 的小写值；否则返回 x | `int` | `int` |
| `toupper(x)` | `<cctype>` | 如果 x 是小写字母，则返回 x 的大写值；否则返回 x | `int` | `int` |

要在程序中使用预定义函数，必须通过 include 语句包含含有该函数说明的头文件。例如，要使用函数 pow，程序必须包含：

```cpp
#include <cmath>
```

示例 6-1 展示了如何使用一些预定义函数。

### 示例 6-1

```cpp
// How to use predefined functions.
#include <iostream>                                      //Line 1
#include <cmath>                                         //Line 2
#include <cctype>                                        //Line 3
#include <iomanip>                                       //Line 4

using namespace std;                                     //Line 5

int main()                                               //Line 6
{
    int num;                                              //Line 7
    double firstNum, secondNum;                           //Line 8
    char ch = 'T';                                        //Line 9

    cout << fixed << showpoint << setprecision (2)        //Line 10
         << endl;                                         //Line 11

    cout << "Line 12: Is " << ch
         << " a lowercase letter? "
         << islower(ch) << endl;                          //Line 12
    cout << "Line 13: Uppercase a is "
         << static_cast<char>(toupper('a')) << endl;     //Line 13

    cout << "Line 14: 4.5 to the power 6.0 = "
         << pow(4.5, 6.0) << endl;                       //Line 14

    cout << "Line 15: Enter two decimal numbers: ";      //Line 15
    cin >> firstNum >> secondNum;                         //Line 16
    cout << endl;                                         //Line 17

    cout << "Line 18: " << firstNum
         << " to the power of " << secondNum
         << " = " << pow(firstNum, secondNum) << endl;   //Line 18

    cout << "Line 19: 5.0 to the power of 4 = "
         << pow(5.0, 4) << endl;                         //Line 19

    firstNum = firstNum + pow(3.5, 7.2);                  //Line 20
    cout << "Line 21: firstNum = " << firstNum << endl;   //Line 21

    num = -32;                                            //Line 22
    cout << "Line 23: Absolute value of " << num
         << " = " << abs(num) << endl;                   //Line 23

    cout << "Line 24: Square root of 28.00 = "
         << sqrt(28.00) << endl;                         //Line 24

    return 0;                                              //Line 25
}                                                        //Line 26
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

```
Line 12: Is T a lowercase letter? 0
Line 13: Uppercase a is A
Line 14: 4.5 to the power 6.0 = 8303.77
Line 15: Enter two decimal numbers: 24.7 3.8

Line 18: 24.7 to the power of 3.80 = 195996.55
Line 19: 5.0 to the power of 4 = 625.00
Line 21: firstNum = 8290.60
Line 23: Absolute value of −32 = 32
Line 24: Square root of 28.00 = 5.29
```

该程序的工作方式如下。第 1 行到第 4 行的语句包含了使用程序中函数所需的头文件。第 7 行到第 9 行的语句声明了程序中使用的变量。第 10 行的语句将十进制数的输出设置为带两位小数的定点小数格式。第 12 行的语句使用函数 islower 判断并输出 ch 是否为小写字母。第 13 行的语句使用函数 toupper 输出与 'a' 对应的大写字母，即 A。注意，函数 toupper 返回一个 int 值。因此，表达式 toupper('a') 的值为 65，即 'A' 的 ASCII 值。要打印字符 A 而不是值 65，需要像第 13 行语句所示应用强制类型转换运算符。第 14 行的语句使用函数 pow 输出 4.5<sup>6.0</sup>。在 C++ 术语中，称为以参数 4.5 和 6.0 调用函数 pow。第 15 行到第 17 行的语句提示用户输入两个十进制数，并将用户输入的数存储到变量 firstNum 和 secondNum 中。在第 18 行的语句中，使用函数 pow 输出 firstNum<sup>secondNum</sup>。在这种情况下，以参数 firstNum 和 secondNum 调用函数 pow，并将 firstNum 和 secondNum 的值传递给函数 pow。其他语句含义类似。再次注意，程序包含头文件 cctype 和 cmath，因为它使用了这些头文件中的函数 islower、toupper、pow、abs 和 sqrt。

## 用户自定义函数

如示例 6-1 所示，在程序中使用函数极大地增强了程序的可读性，因为它降低了 main 函数的复杂性。此外，一旦你编写并正确调试了一个函数，就可以在程序（或不同程序）中反复使用它，而不必重复重写相同的代码。例如，在示例 6-1 中，函数 pow 被多次使用。

因为 C++ 并不提供你将来可能需要的每一个函数，而且设计者不可能知道用户的具体需求，所以你必须学会编写自己的函数。

C++ 中的用户自定义函数分为两类：

- **有返回值函数**——具有返回类型的函数。这些函数使用 `return` 语句返回特定数据类型的值，我们稍后将对此进行解释。注意，在我们迄今见到的每个程序中，函数 `main` 都使用了 `return` 语句返回值 0。
- **无返回值函数**——不具有返回类型的函数。这些函数*不*使用 `return` 语句返回值。

我们将首先讨论有返回值函数。关于有返回值函数讨论的许多概念也适用于无返回值函数。

## 有返回值函数

上一节介绍了一些预定义的 C++ 函数，例如 pow、abs、islower 和 toupper。这些都是有返回值函数的示例。要在程序中使用这些函数，你必须知道包含函数说明的头文件的名称。你需要使用 include 语句在程序中包含该头文件，并知道以下各项：

- 1. 函数名称
- 2. **参数**（如果有）
- 3. 每个参数的数据类型
- 4. 函数计算出的值（即函数返回的值）的数据类型，称为函数的类型

由于有返回值函数只返回一个值，你自然会以以下方式之一使用该值：

- 保存该值以供进一步计算。例如，`x = pow(3.0, 2.5);`
- 在某种计算中使用该值。例如，`area = PI * pow(radius, 2.0);`
- 打印该值。例如，`cout << abs(-5) << endl;`

这表明有返回值函数用于：

- 在赋值语句中。
- 作为函数调用中的参数。
- 在输出语句中。

也就是说，有返回值函数在表达式中使用（调用）。

在我们查看用户自定义有返回值函数的语法之前，先考虑与此类函数相关的事项。除了前面描述的四个属性外，函数（有返回值函数和无返回值函数）还关联一个事项：

- 5. 完成任务所需的代码

前四个属性构成所谓的函数**首部**（也称为**函数头**）；第五个属性称为函数**体**。这些合在一起，

![](img/d0be7fc6d804b63484835c6c8bc67a07_401_0.png)

