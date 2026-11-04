
## 第3章 • Raspberry Pi 的 C 编程

### 3.1 • 概述

本章将介绍使用 C 编程的基本原理。关于使用 C 编程的书籍、教程和应用笔记有数百种，因此本章并不打算详细教授 C 编程。

### 3.2 • C 语言

#### 3.2.1 • 变量

C 语言支持以下变量类型：

| 类型 | 描述 |
|---|---|
| `char` | 单个字符或 8 位变量（-128 到 +127） |
| `unsigned char` | 8 位无符号数（0 到 +255） |
| `int` | 32 位有符号整数（-2147483648 到 +2147483647） |
| `long` | 32 位有符号整数（-2147483648 到 +2147483647） |
| `unsigned int` | 32 位无符号整数（0 到 +4294967295） |
| `unsigned long` | 32 位无符号整数（0 到 +4294967295） |
| `short` | 16 位有符号整数（-32768 到 +32767） |
| `unsigned short` | 16 位无符号数（0 到 +65535） |
| `float` | 浮点数（±3.402823x10^38） |
| `double` | 双精度数（±1.7×10^308） |

#### 3.2.2 • 屏幕输出和键盘输入

如前所述，`printf` 用于在屏幕上显示数据和文本。可以使用 `scanf` 语句从键盘输入数据。下面给出一个示例。

#### 示例 3.1

编写一个程序，读取三角形的底和高，然后计算并显示其面积。

#### 解答 3.1

所需程序清单（程序：TriangleArea.c）如图 3.1 所示。

```c
/*--------------------------------------------

            AREA OF A TRIANGLE
            ====================

This program calculates the area of a triangle, given its
base and height

Author: Dogan Ibrahim
File : TriangleArea.c
Date : December 2020
---------------------------------------------*/
#include <stdio.h>

int main(void)
{
    float Base, Height, Area;
    printf("\nArea of a Triangle\n\n");
    printf("Enter base: ");
    scanf("%f", &Base);
    printf("Enter Height: ");
    scanf("%f", &Height);
    Area = Base * Height / 2.0;
    printf("Area = %f\n", Area);
    return 0;
}
```

图 3.1 程序：TriangleArea.c

程序开始时，变量 Base、Height 和 Area 被声明为浮点变量。然后程序显示标题 Area of a Triangle。在显示此标题前后会打印换行。显示文本 Enter base:，并请求用户输入三角形的底，该值存储在变量 Base 中。请注意，`scanf` 需要变量的内存地址来存储数据。然后请求用户输入高。计算三角形的面积并显示在屏幕上。图 3.2 显示了该程序的一次示例运行。

```text
pi@raspberrypi:~ $ gcc -o Area TriangleArea.c
pi@raspberrypi:~ $ ./Area

Area of a Triangle

Enter base: 12.0
Enter Height: 10.4
Area = 62.399998
pi@raspberrypi:~ $
```

图 3.2 程序的一次示例运行

我们可以使用 `%f` 语句更改小数位数。该语句的一般格式为：

`%n.df` —— 其中 n 是要显示的数字总长度，d 是小数点后的位数。

例如，要显示小数点后一位的面积，我们可以使用以下语句：

```c
printf("Area = %4.1f\n", Area);
```

这会将图 3.2 中的结果显示为 **62.4**。

其他一些示例输出格式如下（假设要显示的数字为 62.0）：

| 格式 | 输出 |
|---|---|
| `%4.2f` | 62.40 |
| `%5.2f` | 62.40 |
| `%6.3f` | 62.400 |

要读取或显示其他变量，我们可以使用：

- `%c` —— 字符
- `%d` —— 整数
- `%s` —— 字符串
- `%u` —— 无符号十进制整数
- `%lu` —— 无符号十进制长整数
- `%o` —— 八进制数
- `%x`, `%X` —— 十六进制数
- `%e` —— 指数数

#### 示例 3.2

在此示例中，我们将再次计算三角形的面积，但其底和高将在同一行输入。

#### 解答 3.2

所需程序清单（程序：**TriangleArea2.c**）如图 3.3 所示。

```c
/*-----------------------------
        AREA OF A TRIANGLE
        =================

This program calculates the area of a triangle, given its
base and height. The base and height are entered on the same line

Author: Dogan Ibrahim
File : TriangleArea2.c
Date : December 2020
-----------------------------*/
#include <stdio.h>

int main(void)
{
    float Base, Height, Area;
    printf("\nArea of a Triangle\n\n");
    printf("Enter base and height: ");
    scanf("%f %f", &Base, &Height);
    Area = Base * Height / 2.0;
    printf("Area = %6.3f\n", Area);
    return 0;
}
```

图 3.3 程序：TriangleArea2.c

该程序与示例 3.1 中提供的程序非常相似，但使用 `scanf` 读取三角形的底和高，两个输入项之间用空格分隔。图 3.4 显示了该程序的一次示例运行。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_38_0.png)

图 3.4 程序的一次示例运行

#### 3.2.3 比较

我们可以在程序中使用以下比较运算符：

- `>` —— 大于
- `<` —— 小于
- `==` —— 等于
- `!=` —— 不等于
- `>=` —— 大于或等于
- `<=` —— 小于或等于

#### 3.2.4 运算符

| 运算符 | 描述 |
|---|---|
| `x + y` | 加法 |
| `x - y` | 减法 |
| `x * y` | 乘法 |
| `x / y` | 除法 |
| `x % y` | x/y 的余数 |
| `x & y` | 按位与 |
| x \| y | 按位或 |
| `x ^ y` | 按位异或 |
| `~x` | 按位取反 |
| `!x` | 逻辑非 |
| `x << y` | 左移 |
| `x >> y` | 右移 |

#### 3.2.5 • 自动递增/递减运算符

| 运算符 | 描述 |
|---|---|
| `x++` | 将 x 递增 1（后置） |
| `x--` | 将 x 递减 1（后置） |
| `++x` | 将 x 递增 1（前置） |
| `--x` | 将 x 递减 1（前置） |
| `x += y` | 将 x 增加 y（等同于 x = x + y） |
| `x -= y` | 将 x 减少 y（等同于 x = x - y） |
| `x *= y` | 将 x 乘以 y（等同于 x = x * y） |
| `x /= y` | 将 x 除以 y（等同于 x = x / y） |
| `x &= y` | 将 x 与 y 按位与（等同于 x = x & y） |
| x \|= y | 将 x 与 y 按位或（等同于 x = x \| y） |
| `x ^= y` | 将 x 与 y 按位异或（等同于 x = x ^ y） |

#### 3.2.6 • 逻辑运算符

| 运算符 | 描述 |
|---|---|
| `&&` | 逻辑与（用于条件测试） |
| \|\| | 逻辑或（用于条件测试） |
| `!` | 逻辑非 |

#### 3.2.7 • 流程控制

流程控制语句是所有编程语言中非常重要的语句。这些语句使程序员能够形成条件执行、选择和迭代（循环）。

#### 条件语句

#### if...else

`if...else` 语句块是主要的条件语句。if...else 块的一般格式为：

```c
if (condition is true)
{
    execute these statements
    ----------------
    ....................
}
else
{
    execute these statements
    ......................
    ......................
}
```

如果 `if` 块内只有一条语句，则无需使用花括号：

```c
if (condition is true)
    execute a single statement;
```

或者，`if (condition is true) execute a single statement;`

#### 示例 3.3

编写一个程序，从键盘读取两个数并计算它们的平均值。如果平均值大于 10，显示 **平均值大于 10。** 另一方面，如果平均值小于 10，显示 **平均值小于 10。** 另一方面，如果平均值等于 10，显示 **平均值是 10。**

#### 解答 3.3

图 3.5 显示了程序清单（程序：**Average.c**）。该程序读取两个浮点数到变量 **no1** 和 **no2**。计算平均值并存储在变量 **average** 中。然后根据平均值等于 10、大于 10 还是小于 10 显示一条消息。图 3.6 显示了该程序的一次示例运行。

```c
/*------------------------------------------------------------
                    AVERAGE OF 2 NUMBERS
                    ====================

This program calculates the average of two numbers read from
the keyboard and compares it with 10

Author: Dogan Ibrahim
File  : Average.c
Date  : December 2020
-------------------------------------------------------------*/
#include <stdio.h>

int main(void)
{
    float no1, no2, average;
    printf("\nAverage of two numbers\n\n");
    printf("Enter two numbers: ");
