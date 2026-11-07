

### 示例 2-8

| 混合表达式 | 求值 | 应用的规则 |
|---|---|---|
| `3 / 2 + 5.5` | `= 1 + 5.5`<br>`= 6.5` | `3 / 2 = 1`（整数除法；规则 1(a)）<br>`1 + 5.5 = 1.0 + 5.5`（规则 1(b)）<br>`= 6.5` |
| `15.6 / 2 + 5` | `= 7.8 + 5`<br>`= 12.8` | `15.6 / 2`<br>`= 15.6 / 2.0`（规则 1(b)）<br>`= 7.8`<br>`7.8 + 5`<br>`= 7.8 + 5.0`（规则 1(b)）<br>`= 12.8` |
| `4 + 5 / 2.0` | `= 4 + 2.5`<br>`= 6.5` | `5 / 2.0 = 5.0 / 2.0`（规则 1(b)）<br>`= 2.5`<br>`4 + 2.5 = 4.0 + 2.5`（规则 1(b)）<br>`= 6.5` |
| `4 * 3 + 7 / 5 - 25.5` | `= 12 + 7 / 5 - 25.5`<br>`= 12 + 1 - 25.5`<br>`= 13 - 25.5`<br>`= -12.5` | `4 * 3 = 12;`（规则 1(a)）<br>`7 / 5 = 1`（整数除法；规则 1(a)）<br>`12 + 1 = 13;`（规则 1(a)）<br>`13 - 25.5 = 13.0 - 25.5`（规则 1(b)）<br>`= -12.5` |

以下 C++ 程序对前面的表达式求值：

```cpp
// This program illustrates how mixed expressions are evaluated.

#include <iostream>

using namespace std;

int main()
{
    cout << "3 / 2 + 5.5 = " << 3 / 2 + 5.5 << endl;
    cout << "15.6 / 2 + 5 = " << 15.6 / 2 + 5 << endl;
    cout << "4 + 5 / 2.0 = " << 4 + 5 / 2.0 << endl;
    cout << "4 * 3 + 7 / 5 - 25.5 = "
         << 4 * 3 + 7 / 5 - 25.5
         << endl;

    return 0;
}
```

**示例运行：**

```text
3 / 2 + 5.5 = 6.5
15.6 / 2 + 5 = 12.8
4 + 5 / 2.0 = 6.5
4 * 3 + 7 / 5 - 25.5 = -12.5
```

这些示例说明，除非要运算的运算符有一个整数操作数和一个浮点操作数，否则整数不会转换为浮点数。

## 类型转换（强制类型转换）

在上一节中，你了解到，在对算术表达式求值时，如果运算符具有混合操作数，则整数值会转换为小数部分为零的浮点值。当一种数据类型的值自动转换为另一种数据类型时，就说发生了**隐式类型强制转换**。正如上一节中的示例所示，如果不注意数据类型，隐式类型强制转换可能会产生意外结果。

为避免隐式类型强制转换，C++ 通过使用强制转换运算符来提供显式类型转换。**强制转换运算符**，也称为**类型转换**或**类型强制转换**，采用以下形式：

```cpp
static_cast<dataTypeName>(expression)
```

首先，对表达式求值。然后，将其值转换为由 `dataTypeName` 指定的类型的值。在 C++ 中，`static_cast` 是保留字。

使用强制转换运算符将浮点（十进制）数转换为整数时，只需去掉浮点数的小数部分。也就是说，浮点数被截断。示例 2-9 展示了强制转换运算符如何工作。请务必理解最后两个表达式为何得到那样的求值结果。

### 示例 2-9

| 表达式 | 求值结果 |
| :--- | :--- |
| `static_cast<int>(7.9)` | `7` |
| `static_cast<int>(3.3)` | `3` |
| `static_cast<double>(25)` | `25.0` |
| `static_cast<double>(5 + 3)` | `= static_cast<double>(8) = 8.0` |
| `static_cast<double>(15) / 2` | `= 15.0 / 2`<br>`(because static_cast<double>(15) = 15.0)`<br>`= 15.0 / 2.0 = 7.5` |
| `static_cast<double>(15 / 2)` | `= static_cast<double>(7)`<br>`(because 15 / 2 = 7)`<br>`= 7.0` |
| `static_cast<int>(7.8 + static_cast<double>(15) / 2)` | `= static_cast<int>(7.8 + 7.5)`<br>`= static_cast<int>(15.3)`<br>`= 15` |
| `static_cast<int>(7.8 + static_cast<double>(15 / 2))` | `= static_cast<int>(7.8 + 7.0)`<br>`= static_cast<int>(14.8)`<br>`= 14` |

以下 C++ 程序对前面的表达式求值：

```cpp
// This program illustrates how explicit type conversion works.

#include <iostream>

using namespace std;

int main()
{
    cout << "static_cast<int>(7.9) = "
         << static_cast<int>(7.9)
         << endl;
    cout << "static_cast<int>(3.3) = "
         << static_cast<int>(3.3)
         << endl;
    cout << "static_cast<double>(25) = "
         << static_cast<double>(25)
         << endl;
    cout << "static_cast<double>(5 + 3) = "
         << static_cast<double>(5 + 3)
         << endl;
    cout << "static_cast<double>(15) / 2 = "
         << static_cast<double>(15) / 2
         << endl;
    cout << "static_cast<double>(15 / 2) = "
         << static_cast<double>(15 / 2)
         << endl;
    cout << "static_cast<int>(7.8 + static_cast<double>(15) / 2) = "
         << static_cast<int>(7.8 + static_cast<double>(15) / 2)
         << endl;
    cout << "static_cast<int>(7.8 + static_cast<double>(15 / 2)) = "
         << static_cast<int>(7.8 + static_cast<double>(15 / 2))
         << endl;

    return 0;
}
```

**示例运行：**

```text
static_cast<int>(7.9) = 7
static_cast<int>(3.3) = 3
static_cast<double>(25) = 25
static_cast<double>(5 + 3) = 8
static_cast<double>(15) / 2 = 7.5
static_cast<double>(15 / 2) = 7
static_cast<int>(7.8 + static_cast<double>(15) / 2) = 15
static_cast<int>(7.8 + static_cast<double>(15 / 2)) = 14
```

注意，表达式 `static_cast<double>(25)` 的值是 25.0。但是，它输出为 25 而不是 25.0。这是因为我们尚未讨论如何输出小数部分为 0 的十进制数，以显示小数点和末尾的零。第 3 章解释了如何以所需格式输出十进制数。类似地，其他小数部分为零的十进制数在输出时也不带小数点和为 0 的小数部分。

> **注意** 在 C++ 中，强制转换运算符也可以采用 `dataType(expression)` 形式。这种形式称为类 C 强制转换。例如，`double(5) = 5.0` 和 `int(17.6) = 17`。但是，`static_cast` 比类 C 强制转换更稳定。

还可以使用强制转换运算符将 `char` 数据值显式转换为 `int` 数据值，并将 `int` 数据值转换为 `char` 数据值。要将 `char` 数据值转换为 `int` 数据值，需使用排序序列。例如，在 ASCII 字符集中，`static_cast<int>('A')` 为 65，`static_cast<int>('8')` 为 56。类似地，`static_cast<char>(65)` 为 'A'，`static_cast<char>(56)` 为 '8'。

本章前面你已经学习了 C++ 中算术表达式是如何形成和求值的。如果想在一个表达式中使用另一个表达式的值，首先必须保存该表达式的值。保存表达式值的原因有很多。有些表达式很复杂，求值可能需要相当多的计算机时间。通过计算一次值并将其保存以供进一步使用，你不仅可以节省计算机时间并创建执行更快的程序，还可以避免可能的录入错误。在 C++ 中，表达式会被求值，如果值未被保存，它就会丢失。也就是说，除非保存它，否则表达式的值不能用于后续计算。下一节中，你将学习如何保存表达式的值并在后续计算中使用它。

在结束数据类型的讨论之前，我们再讨论一种数据类型——string。

## string 类型

数据类型 `string` 是一种程序员定义的数据类型。它不像前面讨论的简单数据类型那样可以直接在程序中使用。要使用此数据类型，需要访问库中的程序组件，本章后面将讨论这一点。数据类型 `string` 是 ANSI/ISO 标准 C++ 的一项特性。

> **注意** 在 ANSI/ISO C++ 语言标准之前，标准 C++ 库不提供字符串数据类型。编译器供应商通常提供自己的程序员定义的字符串类型，并且字符串操作的语法和语义常常因供应商而异。

字符串是零个或多个字符的序列。C++ 中的字符串用双引号括起来。不含任何字符的字符串称为 null 字符串或空字符串。以下是字符串的示例。注意 "" 是空字符串。

```text
"William Jacob"
"Mickey"
""
```

字符串中的每个字符在该字符串中都有一个相对位置。第一个字符的位置是 0，第二个字符的位置是 1，依此类推。字符串的长度是其中字符的数量。

![](img/f97f778697507bb6fdd80c5991210cba_90_0.png)

