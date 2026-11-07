
以下 C++ 程序对前面的表达式进行求值：

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

### 示例运行：

```text
3 / 2 + 5.5 = 6.5
15.6 / 2 + 5 = 12.8
4 + 5 / 2.0 = 6.5
4 * 3 + 7 / 5 - 25.5 = -12.5
```

这些示例表明，除非要运算的运算符有一个整数操作数和一个浮点数操作数，否则整数不会转换为浮点数。

## 类型转换（强制类型转换）

在上一节中，你了解到：在计算算术表达式时，如果运算符具有混合操作数，则整数值会转换为带小数部分的浮点值。当一个数据类型的值自动更改为另一个数据类型时，就称发生了**隐式类型强制转换**。正如上一节中的示例所示，如果不注意数据类型，隐式类型强制转换可能会产生意想不到的结果。

为避免隐式类型强制转换，C++ 提供了通过使用**强制类型转换运算符**进行显式类型转换的方式。强制类型转换运算符也称为**类型转换**或**类型强制转换**，采用以下形式：

```cpp
static_cast<dataTypeName>(expression)
```

首先，对表达式求值。然后，将其值转换为 `dataTypeName` 指定的类型值。在 C++ 中，`static_cast` 是保留字。

使用强制类型转换运算符将浮点数（小数）转换为整数时，只需去掉浮点数的小数部分。也就是说，浮点数被截断。示例 2-9 展示了强制类型转换运算符的工作方式。请务必理解最后两个表达式为何得到那样的求值结果。

### 示例 2-9

| 表达式 | 求值结果 |
|---|---|
| `static_cast<int>(7.9)` | `7` |
| `static_cast<int>(3.3)` | `3` |
| `static_cast<double>(25)` | `25.0` |
| `static_cast<double>(5 + 3)` | `= static_cast<double>(8) = 8.0` |
| `static_cast<double>(15) / 2` | `= 15.0 / 2`（因为 `static_cast<double>(15) = 15.0`）<br>`= 15.0 / 2.0 = 7.5` |
| `static_cast<double>(15 / 2)` | `= static_cast<double>(7)`（因为 `15 / 2 = 7`）<br>`= 7.0` |
| `static_cast<int>(7.8 + static_cast<double>(15) / 2)` | `= static_cast<int>(7.8 + 7.5)`<br>`= static_cast<int>(15.3)`<br>`= 15` |
| `static_cast<int>(7.8 + static_cast<double>(15 / 2))` | `= static_cast<int>(7.8 + 7.0)`<br>`= static_cast<int>(14.8)`<br>`= 14` |

以下 C++ 程序对前面的表达式进行求值：

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

### 示例运行：

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

请注意，表达式 `static_cast<double>(25)` 的值是 25.0。然而，它输出为 25，而不是 25.0。这是因为我们尚未讨论如何输出小数部分为 0 的十进制数，以显示小数点和末尾的零。第 3 章解释了如何以所需格式输出十进制数。同样，其他小数部分为零的十进制数的输出也不带小数点和 0 小数部分。

> **注意**
>
> 在 C++ 中，强制类型转换运算符也可以采用 `dataType(expression)` 形式。这种形式称为 C 风格强制类型转换。例如，`double(5) = 5.0`，`int(17.6) = 17`。然而，`static_cast` 比 C 风格强制类型转换更稳定。

你也可以使用强制类型转换运算符将 `char` 数据值显式转换为 `int` 数据值，以及将 `int` 数据值转换为 `char` 数据值。要将 `char` 数据值转换为 `int` 数据值，需要使用排序序列。例如，在 ASCII 字符集中，`static_cast<int>('A')` 为 65，`static_cast<int>('8')` 为 56。类似地，`static_cast<char>(65)` 为 'A'，`static_cast<char>(56)` 为 '8'。

在本章前面，你学习了 C++ 中算术表达式是如何形成和求值的。如果要在另一个表达式中使用某个表达式的值，首先必须保存该表达式的值。保存表达式值的原因有很多。有些表达式很复杂，可能需要大量计算机时间进行求值。通过只计算一次值并将其保存以供后续使用，不仅可以节省计算机时间、创建执行更快的程序，还可以避免可能的排版错误。在 C++ 中，表达式会被求值，如果值未被保存，就会丢失。也就是说，除非保存该值，否则表达式的值不能在后续计算中使用。在本章后面，你将学习如何保存表达式的值并在后续计算中使用它。

在结束数据类型讨论之前，我们再讨论一种数据类型——string。

## string 类型

数据类型 **string** 是程序员定义的数据类型。它不像前面讨论的简单数据类型那样可以直接在程序中使用。要使用此数据类型，需要从库中访问程序组件，这将在本章后面讨论。数据类型 **string** 是 ANSI/ISO 标准 C++ 的特性。

> **注意**
>
> 在 ANSI/ISO C++ 语言标准之前，标准 C++ 库不提供 **string** 数据类型。编译器供应商通常提供自己的程序员定义的 **string** 类型，而字符串操作的语法和语义往往因供应商而异。

**string** 是零个或多个字符的序列。C++ 中的字符串用双引号括起来。不包含任何字符的字符串称为 **null** 或**空**字符串。以下是字符串的示例。注意 **""** 是空字符串。

```text
"William Jacob"
"Mickey"
""
```

字符串中的每个字符在字符串中都有一个相对位置。第一个字符的位置是 0，第二个字符的位置是 1，依此类推。字符串的长度是其中字符的数量。确定字符串长度时，还必须计入字符串中的任何空格。

### 示例 2-10

| 字符串 | 字符在字符串中的位置 | 字符串长度 |
|---|---|---|
| **"William Jacob"** | 'W' 的位置是 0。<br>第一个 'i' 的位置是 1。<br>' '（空格）的位置是 7。<br>'J' 的位置是 8。<br>'b' 的位置是 12。 | 13 |
| **"Mickey"** | 'M' 的位置是 0。<br>'i' 的位置是 1。<br>'c' 的位置是 2。<br>'k' 的位置是 3。<br>'e' 的位置是 4。<br>'y' 的位置是 5。 | 6 |

以下字符串的长度是 22。

```text
"It is a beautiful day."
```
