

| 数据类型 | `printf` 转换说明符 | `scanf` 转换说明符 |
|---|---|---|
| *整数类型* |  |  |
| `unsigned long long int` | `%llu` | `%llu` |
| `long long int` | `%lld` | `%lld` |
| `unsigned long int` | `%lu` | `%lu` |
| `long int` | `%ld` | `%ld` |
| `unsigned int` | `%u` | `%u` |
| `int` | `%d` | `%d` |
| `unsigned short` | `%hu` | `%hu` |
| `short` | `%hd` | `%hd` |
| `char` | `%c` | `%c` |

**图 5.5** 算术数据类型及其转换说明符。 (第 2 部分，共 2 部分。)

一个值只能通过显式地将该值赋给较低类型的变量或使用 *强制转换* 运算符来转换为 *较低类型*。函数调用中的参数会根据函数原型中指定的参数类型进行转换，就好像参数被直接赋给这些类型的变量一样。如果我们的 square 函数使用 int 参数（图 5.3）被调用时传入浮点参数，则参数会被转换为 int（一种较低类型），并且 square 通常会返回错误的值。例如，`square(4.5)` 返回 16，而不是 20.25。

> **常见编程错误 5.6**
> 
> *在提升层级中从较高数据类型转换为较低类型可能会改变数据值。许多编译器在这种情况下会发出警告。*

如果函数没有函数原型，编译器会使用函数的第一次出现——函数定义或函数调用——来形成自己的函数原型。这通常会导致警告或错误，具体取决于编译器。

> **错误预防提示 5.3**
> 
> *始终为程序中定义或使用的函数包含函数原型，以帮助防止编译错误和警告。*

> **软件工程观察 5.9**
> 
> *放置在任何函数定义之外的函数原型适用于文件中的函数原型之后出现的所有函数调用。放置在函数体内的函数原型仅适用于该函数中进行的调用。*

### 5.7 函数调用栈和栈帧

要了解 C 如何执行函数调用，我们首先需要考虑一种称为 *栈* 的数据结构（即相关数据项的集合）。把栈想象成类似于一个

操作系统（即，转移到返回地址 R1）并包含 main 的自动变量（即 a，其初始化为 10）的空间。

```c
1 // Fig. 5.6: fig05_06.c
2 // Demonstrating the function call stack
3 // and stack frames using a function square.
4 #include <stdio.h>
5
6 int square(int); // prototype for function square
7
8 int main()
9 {
10     int a = 10; // value to square (local automatic variable in main)
11
12     printf("%d squared: %d\n", a, square(a)); // display a squared
13 }
14
15 // returns the square of an integer
16 int square(int x) // x is a local variable
17 {
18     return x * x; // calculate square and return result
19 }
```

10 的平方：100

**图 5.6** 使用 square 函数演示函数调用栈和栈帧。

### 步骤 1：操作系统调用 main 执行应用程序

![](img/bf54db922e6fa8319cba11069e785521_196_0.png)

**图 5.7** 操作系统调用 main 执行程序后的函数调用栈。

函数 main——在返回操作系统之前——现在在图 5.6 的第 12 行调用函数 square。这会导致 square 的栈帧（第 16–19 行）被压入函数调用栈（图 5.8）。该栈帧包含 square 需要返回到 main 的返回地址（即 R2）以及 square 的自动变量（即 x）的内存。

### 步骤 2：main 调用函数 square 执行计算

```c
int main()
{
    int a = 10;
    printf("%d squared: %d\n", a, square(a));
}
```

```c
int square(int x)
{
    return x * x;
}
```

![](img/bf54db922e6fa8319cba11069e785521_197_0.png)

**图 5.8** main 调用 square 执行计算后的函数调用栈。

在 square 计算其参数的平方后，它需要返回到 main——并且不再需要其自动变量 x 的内存。因此栈被弹出——给 square main 中的返回位置（即 R2）并丢失 square 的自动变量。图 5.9 显示了在 square 的栈帧被弹出后函数调用栈。函数 main 现在显示调用 square 的结果（图 5.6 中的第 12 行）。到达 main 的闭合右大括号会导致其栈帧从栈中弹出，给 main 它返回到操作系统的地址（即图 5.7 中的 R1）并导致 main 的自动变量（即 a）的内存变得不可用。你现在已经看到了栈数据结构在实现支持程序执行的关键机制方面的价值。数据结构在计算机科学中有许多重要的应用。我们在第 12 章中讨论栈、队列、列表、树和其他数据结构。

| 标头 | 说明 |
|---|---|
| `<math.h>` | 包含数学库函数的函数原型。 |
| `<setjmp.h>` | 包含允许绕过通常的函数调用和返回序列的函数的函数原型。 |
| `<signal.h>` | 包含处理程序执行期间可能出现的各种条件的函数原型和宏。 |
| `<stdarg.h>` | 定义用于处理参数数量和类型未知的函数的参数列表的宏。 |
| `<stddef.h>` | 包含 C 用于执行计算的常用类型定义。 |
| `<stdio.h>` | 包含标准输入/输出库函数的函数原型以及它们使用到的信息。 |
| `<stdlib.h>` | 包含数字到文本和文本到数字的转换、内存分配、随机数和其他实用函数的函数原型。 |
| `<string.h>` | 包含字符串处理函数的函数原型。 |
| `<time.h>` | 包含用于操作时间和日期的函数原型和类型。 |

**图 5.10** 一些标准库头文件。 (第 2 部分，共 2 部分。)

你可以创建自定义头文件。程序员定义的头文件也应使用 .h 文件名扩展名。程序员定义的头文件可以通过使用 #include 预处理器指令来包含。例如，如果我们的 square 函数的原型位于头文件 square.h 中，我们将通过在程序顶部使用以下指令来包含该头文件：

```c
#include "square.h"
```

第 13.2 节介绍了有关包含头文件的其他信息，例如为什么程序员定义的头文件用引号 (" ) 而不是尖括号 (<>) 括起来。

### 5.9 按值传递参数和按引用传递参数

在许多编程语言中，有两种传递参数的方式——按值传递和按引用传递。当参数按值传递时，参数值的副本会被制作并传递给被调用函数。对副本的更改不会影响调用方中原始变量的值。当参数按引用传递时，调用方允许被调用函数修改原始变量的值。

按值传递应在被调用函数不需要修改调用方原始变量值时使用。这可以防止那些极大地阻碍正确可靠软件系统开发的意外副作用（变量修改）。按引用传递应仅与需要修改原始变量的可信被调用函数一起使用。

在 C 中，所有参数都是按值传递的。正如我们将在第 7 章 C 指针中看到的那样，可以通过使用地址运算符和间接运算符来实现按引用传递。在第 6 章中，我们将看到出于性能原因，数组参数会自动按引用传递。我们将在第 7 章看到这并不是矛盾的。现在，我们集中讨论按值传递。

|   |   |   |   |   |
|---|---|---|---|---|
| 6 | 6 | 5 | 5 | 6 |
| 6 | 1 | 1 | 5 | 3 |
| 6 | 6 | 2 | 4 | 2 |
| 6 | 2 | 3 | 4 | 1 |

**图 5.11** 由 `1 + rand() % 6` 产生的平移、缩放随机整数。 (第 2 部分，共 2 部分。)

函数 `rand` 的函数原型在 `<stdlib.h>` 中。我们使用余数运算符 (`%`) 与 `rand` 结合使用如下

```c
rand() % 6
```

以产生 0 到 5 范围内的整数。这称为缩放。数字 6 称为缩放因子。然后我们通过将 1 加到之前的结果来平移产生数字的范围。输出证实结果在 1 到 6 的范围内——实际选择的随机值可能会因编译器而异。

### 掷六面骰子 60,000,000 次

为了表明这些数字大致以相等的可能性出现，让我们使用图 5.12 的程序模拟掷骰子 60,000,000 次。每个 1 到 6 的整数应大约出现 10,000,000 次。

```c
 1  // Fig. 5.12: fig05_12.c
 2  // Rolling a six-sided die 60,000,000 times.
 3  #include <stdio.h>
 4  #include <stdlib.h>
 5
 6  int main(void)
 7  {
 8      unsigned int frequency1 = 0; // rolled 1 counter
 9      unsigned int frequency2 = 0; // rolled 2 counter
10      unsigned int frequency3 = 0; // rolled 3 counter
11      unsigned int frequency4 = 0; // rolled 4 counter
12      unsigned int frequency5 = 0; // rolled 5 counter
13      unsigned int frequency6 = 0; // rolled 6 counter
14
15      // loop 60000000 times and summarize results
16      for (unsigned int roll = 1; roll <= 60000000; ++roll) {
17          int face = 1 + rand() % 6; // random number from 1 to 6
18
19          // determine face value and increment appropriate counter
20          switch (face) {
21
22              case 1: // rolled 1
23                  ++frequency1;
24                  break;
25
26              case 2: // rolled 2
27                  ++frequency2;
28                  break;
```

**图 5.12** 掷六面骰子 60,000,000 次。 (第 1 部分，共 2 部分。)

