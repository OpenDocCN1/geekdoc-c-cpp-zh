

## C 遗留代码主题

![](img/bfd978e7e9b192bab46ec2a89e481263_1196_0.png)

> 我们将使用一种我尝试过、发现影响深远且容易喊出的信号。哇呼！
> ——赞恩·格雷
>
> 这是一个相当费三斗烟的问题。
> ——阿瑟·柯南·道尔爵士
>
> 然而在分离中仍有结合。
> ——威廉·莎士比亚

### 目标

在本附录中，你将学习

- 将键盘输入重定向为来自文件，并将屏幕输出重定向到文件。
- 编写使用可变长度参数列表的函数。
- 处理命令行参数。
- 处理程序内的意外事件。
- 使用 C 风格动态内存分配为数组动态分配内存。
- 调整使用 C 风格动态内存分配所动态分配的内存大小。

- F.1 引言
- F.2 在 UNIX/Linux/Mac OS X 和 Windows 系统上重定向输入/输出
- F.3 可变长度参数列表
- F.4 使用命令行参数
- F.5 关于编译多源文件程序的说明
- F.6 使用 `exit` 和 `atexit` 终止程序
- F.7 类型限定符 `volatile`
- F.8 整型和浮点常量的后缀
- F.9 信号处理
- F.10 使用 `calloc` 和 `realloc` 动态分配内存
- F.11 无条件分支：`goto`
- F.12 联合体
- F.13 链接规范
- F.14 小结

*小结 | 自测练习 | 自测练习答案 | 练习*

### F.1 引言

本章介绍若干通常在入门课程中不会涉及的主题。这里讨论的许多能力特定于某些操作系统，尤其是 UNIX/Linux/Mac OS X 和/或 Windows。许多材料是为了帮助那些需要处理较旧 C 遗留代码的 C++ 程序员。

### F.2 在 UNIX/Linux/Mac OS X 和 Windows 系统上重定向输入/输出

通常，程序的输入来自键盘（标准输入），程序的输出显示在屏幕上（标准输出）。在大多数计算机系统上——尤其是 UNIX、LINUX、Mac OS X 和 Windows 系统——可以将输入重定向为来自文件，并将输出重定向到文件中。两种重定向形式都可以在不使用标准库文件处理能力的情况下完成。

有几种方法可以从 UNIX 命令行重定向输入和输出。考虑可执行文件 sum，它一次输入一个整数，持续累计这些值，直到设置文件结束指示符，然后打印结果。通常，用户从键盘输入整数，并输入文件结束键组合以表示不再输入更多值。使用输入重定向时，输入可以存储在文件中。例如，如果数据存储在文件 input 中，则命令行

```text
$ sum < input
```

会使程序 sum 被执行；重定向输入符号 (<) 表示文件 input 中的数据（而不是键盘）将用作程序的输入。在 Windows 命令提示符中重定向输入的执行方式完全相同。

注意 $ 表示 UNIX 命令行提示符。（UNIX 提示符因系统而异，同一系统上的不同 shell 之间也会不同。）重定向是操作系统功能，而不是另一个 C++ 特性。

第二种重定向输入的方法是管道。管道 (|) 使一个程序的输出重定向为另一个程序的输入。假设程序 random 输出一系列随机整数；使用 UNIX 命令行，random 的输出可以直接“管道”到程序 sum

```text
$ random | sum
```

这会计算 random 产生的整数之和。管道可以在 UNIX、LINUX、Mac OS X 和 Windows 中执行。

可以使用**重定向输出符号 (>)**将程序输出重定向到文件。（UNIX、LINUX、Mac OS X 和 Windows 使用相同的符号。）例如，要将程序 random 的输出重定向到名为 out 的新文件，请使用

```text
$ random > out
```

最后，可以使用**追加输出符号 (>>)**将程序输出追加到现有文件的末尾。（UNIX、LINUX、Mac OS X 和 Windows 使用相同的符号。）例如，要将程序 random 的输出追加到前一条命令行中创建的文件 out 的末尾，请使用以下命令行

```text
$ random >> out
```

### F.3 可变长度参数列表

可以创建接收未指定数量参数的函数。函数原型中的省略号 (…) 表示该函数接收任意类型的可变数量参数。¹ 注意，省略号必须始终放在参数列表末尾，并且省略号之前至少有一个参数。**可变参数头文件 <cstdarg>**（图 F.1）的宏和定义提供了构建具有可变长度参数列表的函数所需的能力。

| 标识符 | 描述 |
|---|---|
| `va_list` | 一种适合保存宏 `va_start`、`va_arg` 和 `va_end` 所需信息的类型。要访问可变长度参数列表中的参数，必须声明一个 `va_list` 类型的对象。 |
| `va_start` | 一个宏，在访问可变长度参数列表的参数之前调用。该宏初始化用 `va_list` 声明的对象，以供 `va_arg` 和 `va_end` 宏使用。 |
| `va_arg` | 一个宏，展开为可变长度参数列表中下一个参数的值和类型的表达式。每次调用 `va_arg` 都会修改用 `va_list` 声明的对象，使该对象指向列表中的下一个参数。 |
| `va_end` | 一个宏，在函数中执行终止清理工作，该函数的可变长度参数列表曾由 `va_start` 宏引用。 |

**图 F.1** | 头文件 `<cstdarg>` 中定义的类型和宏。

1. 在 C++ 中，程序员使用函数重载来完成 C 程序员用可变长度参数列表完成的许多工作。

图 F.2 演示了接收可变数量参数的函数 average。average 的第一个参数始终是要取平均值的数量，其余参数必须都是 double 类型。

函数 average 使用头文件 `<cstdarg>` 的所有定义和宏。类型为 `va_list` 的对象 list 由宏 `va_start`、`va_arg` 和 `va_end` 使用，以处理函数 average 的可变长度参数列表。

```cpp
// Fig. F.2: figF_02.cpp
// Using variable-length argument lists.
#include <iostream>
#include <iomanip>
#include <cstdarg>
using namespace std;

double average( int, ... );

int main()
{
   double double1 = 37.5;
   double double2 = 22.5;
   double double3 = 17.7;
   double double4 = 10.2;

   cout << fixed << setprecision( 1 ) << "double1 = "
        << double1 << "\ndouble2 = " << double2 << "\ndouble3 = "
        << double3 << "\ndouble4 = " << double4 << endl
        << setprecision( 3 )
        << "\nThe average of double1 and double2 is "
        << average( 2, double1, double2 )
        << "\nThe average of double1, double2, and double3 is "
        << average( 3, double1, double2, double3 )
        << "\nThe average of double1, double2, double3, and double4 is "
        << average( 4, double1, double2, double3, double4 )
        << endl;
}
// end main

// calculate average
double average( int count, ... )
{
   double total = 0;
   va_list list; // for storing information needed by va_start

   va_start( list, count );

   // process variable-length argument list
   for ( int i = 1; i <= count; i++ )
      total += va_arg( list, double );

   va_end( list ); // end the va_start
   return total / count;
} // end function average
```

**图 F.2** | 使用可变长度参数列表。（第 1 部分，共 2 部分。）

```text
double1 = 37.5
double2 = 22.5
double3 = 1.7
double4 = 10.2

The average of double1 and double2 is 30.000
The average of double1, double2, and double3 is 20.567
The average of double1, double2, double3 and double4 is 17.975
```

**图 F.2** | 使用可变长度参数列表。（第 2 部分，共 2 部分。）

该函数调用 `va_start` 初始化对象 list，以供 `va_arg` 和 `va_end` 使用。该宏接收两个参数——对象 list 和省略号之前参数列表中最右侧参数的标识符——在本例中是 count（`va_start` 在此使用 count 来确定可变长度参数列表从何处开始）。

接下来，函数 average 反复将可变长度参数列表中的参数加到 total 中。要加到 total 的值通过调用宏 `va_arg` 从参数列表中取得。宏 `va_arg` 接收两个参数——对象 list 和参数列表中预期值的类型（本例中为 double）——并返回该参数的值。函数 average 在返回之前以对象 list 作为参数调用宏 `va_end`。最后，计算平均值并将其返回给 `main`。注意，我们仅对参数列表的可变长度部分使用了 double 参数。

可变长度参数列表会将 float 类型的变量提升为 double 类型。这些参数列表还会将小于 int 的整型变量提升为 int 类型（int、unsigned、long 和 unsigned long 类型的变量保持不变）。

> **软件工程观察 F.1**
>
> *可变长度参数列表只能用于基本类型参数，以及不包含 C++ 特有特性（如虚函数、构造函数、析构函数、引用、const 数据成员和虚基类）的结构体类型参数。*

> **常见编程错误 F.1**
>
> *将省略号放在函数参数列表中间是语法错误。省略号只能放在参数列表末尾。*

### F.4 使用命令行参数

在许多系统上，可以通过在 `main` 的参数列表中包含参数 `int argc` 和 `char *argv[]`，从命令行向 `main` 传递参数。参数 `argc` 接收命令行参数的数量。参数 `argv` 是一个 `char *` 数组，指向存储实际命令行参数的字符串。命令行参数的常见用途包括打印参数、向程序传递选项以及向程序传递文件名。

图 F.3 一次一个字符地将一个文件复制到另一个文件。该程序的可执行文件名为 copyFile（即该文件的可执行名称）。在 UNIX 系统上，copyFile 程序的典型命令行是

```text
$ copyFile input output
```

