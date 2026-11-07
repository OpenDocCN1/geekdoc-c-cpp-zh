
```cpp
//named constants
const int HALF_DOLLAR = 50;
const int QUARTER = 25;
const int DIME = 10;
const int NICKEL = 5;

int main()
{
    //declare variable
    int change;

    //Statements: Step 1 - Step 12
    cout << "Enter change in cents: ";                    //Step 1
    cin >> change;                                        //Step 2
    cout << endl;

    cout << "The change you entered is " << change
         << endl;                                         //Step 3

    cout << "The number of half-dollars to be returned "
         << " is " << change / HALF_DOLLAR
         << endl;                                         //Step 4
    change = change % HALF_DOLLAR;                        //Step 5

    cout << "The number of quarters to be returned is "
         << change / QUARTER << endl;                     //Step 6
    change = change % QUARTER;                            //Step 7

    cout << "The number of dimes to be returned is "
         << change / DIME << endl;                        //Step 8
    change = change % DIME;                               //Step 9

    cout << "The number of nickels to be returned is "
         << change / NICKEL << endl;                      //Step 10
    change = change % NICKEL;                             //Step 11

    cout << "The number of pennies to be returned is "
         << change << endl;                               //Step 12

    return 0;
}
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

```
Enter change in cents: 583

The change you entered is 583
The number of half-dollars to be returned is 11
The number of quarters to be returned is 1
The number of dimes to be returned is 0
The number of nickels to be returned is 1
The number of pennies to be returned is 3
```

## 快速复习

- 1. C++ 程序是函数的集合。
- 2. 每个 C++ 程序都有一个名为 `main` 的函数。
- 3. 单行注释以符号对 `//` 开头，可位于该行的任意位置。
- 4. 多行注释括在 `/*` 和 `*/` 之间。
- 5. 编译器会忽略注释。
- 6. 保留字不能用作程序中的标识符。
- 7. C++ 中的所有保留字都由小写字母组成（见附录 A）。
- 8. 在 C++ 中，标识符是事物的名称。
- 9. C++ 标识符由字母、数字和下划线组成，并且必须以字母或下划线开头。
- 10. 空白字符包括空格、制表符和换行符。
- 11. 数据类型是一组值以及一组允许的操作。
- 12. C++ 数据类型分为以下三类：简单、结构化和指针。
- 13. 简单数据有三类：整型、浮点型和枚举。
- 14. 整型数据类型分为以下类别：`char`、`short`、`int`、`long`、`bool`、`unsigned char`、`unsigned short`、`unsigned int`、`unsigned long`、`long long` 和 `unsigned long long`。
- 15. 属于 `int` 数据类型的值是 -2147483648（=−2^31）到 2147483647（=2^31 − 1）。
- 16. 数据类型 `bool` 只有两个值：`true` 和 `false`。
- 17. 最常见的字符集是 ASCII（有 128 个值）和 EBCDIC（有 256 个值）。
- 18. 字符的排序序列是它在字符数据集中的预设编号。
- 19. C++ 提供了三种数据类型来操作十进制数：`float`、`double` 和 `long double`。
- 20. C++ 中使用数据类型 `float` 表示介于 -3.4 * 10^38 和 3.4 * 10^38 之间的任何实数。为 `float` 数据类型的值分配的内存为四字节。
- 21. C++ 中使用数据类型 `double` 表示介于 -1.7 * 10^308 和 1.7 * 10^308 之间的任何实数。为 `double` 数据类型的值分配的内存为八字节。
- 22. C++ 中的算术运算符有加法（+）、减法（-）、乘法（*）、除法（/）和取模（%）。
- 23. 取模运算符 % 只接受整数操作数。
- 24. 算术表达式使用优先级规则和算术运算符的结合性求值。
- 25. 整型表达式或整数表达式中的所有操作数都是整数，浮点表达式中的所有操作数都是十进制数。
- 26. 混合表达式是同时包含整数和十进制数的表达式。
- 27. 在计算表达式中的运算符时，仅当该运算符具有混合操作数时，整数才转换为小数部分为 0 的浮点数。
- 28. 可以使用强制类型转换运算符将值从一种数据类型显式转换为另一种数据类型。
- 29. 字符串是由零个或多个字符组成的序列。
- 30. C++ 中的字符串用双引号括起来。
- 31. 不含任何字符的字符串称为空字符串或空串。
- 32. 字符串中的每个字符在字符串中都有一个相对位置。第一个字符的位置是 0，第二个字符的位置是 1，依此类推。
- 33. 字符串的长度是其中字符的数量。
- 34. 在程序执行期间，命名常量的内容不能更改。
- 35. 命名常量通过使用保留字 `const` 来声明。
- 36. 命名常量在声明时必须初始化。
- 37. 所有变量必须先声明后使用。
- 38. C++ 不会自动初始化变量。
- 39. 每个变量都有一个名称、一个值、一个数据类型和一个大小。
- 40. 当给变量赋新值时，旧值会丢失。
- 41. 只有赋值语句或输入（读取）语句可以更改变量的值。
- 42. 在 C++ 中，`>>` 称为流提取运算符。
- 43. 从标准输入设备输入通过使用 `cin` 和流提取运算符 `>>` 来完成。
- 44. 当在程序中输入数据时，数据项（例如数字）通常由空格、行或制表符分隔。

![](img/b217c421655b51e7494cf3b89bb5432d_152_0.png)

- 45. 在 C++ 中，`<<` 称为流插入运算符。
- 46. 程序向标准输出设备输出通过使用 `cout` 和流插入运算符 `<<` 来完成。
- 47. 操纵符 `endl` 将插入点定位到输出设备下一行的开头。
- 48. 在表达式中输出或访问变量的值不会破坏或修改变量的内容。
- 49. 字符 `\` 称为转义字符。
- 50. 序列 `\n` 称为换行转义序列。
- 51. 所有预处理命令都以符号 `#` 开头。
- 52. 预处理命令在程序进入编译器之前由预处理器处理。
- 53. 预处理命令 `#include <iostream>` 指示预处理器在程序中包含头文件 `iostream`。
- 54. 要使用 `cin` 和 `cout`，程序必须包含头文件 `iostream`，并包含语句 `using namespace std;`，或者将这些标识符称为 `std::cin` 和 `std::cout`。
- 55. 所有 C++ 语句都以分号结尾。C++ 中的分号称为语句终止符。
- 56. 一个 C++ 系统有三个组成部分：环境、语言和标准库。
- 57. 标准库不是 C++ 语言的一部分。它们包含执行操作（如数学运算）的函数。
- 58. 包含 C++ 程序的文件通常以扩展名 `.cpp` 结尾。
- 59. 提示行是告诉用户要做什么的可执行语句。
- 60. 对应于五个算术运算符 `+`、`-`、`*`、`/` 和 `%`，C++ 分别提供了五个复合运算符：`+=`、`-=`、`*=`、`/=` 和 `%=`。

## 练习

练习末尾括号中的数字指的是本章开头列出的学习目标。

- 1. 将下列陈述标记为真或假。
  - a. 标识符必须以字母开头，并且可以是任意字符序列。(1)
  - b. 在 C++ 中，保留字和预定义标识符之间没有区别。(1)
  - c. C++ 标识符不能以数字开头。(1)

