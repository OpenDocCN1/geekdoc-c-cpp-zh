
在前面的代码片段中，可以看到除枚举 Tuesday 外，days（枚举）的名称没有分配任何值。分配给枚举 Tuesday 的值为 5。编译器按递增顺序为枚举赋值，从 Sunday 的 0 开始。数值序列的赋值从 Tuesday 开始改变，这意味着编译器根据枚举 Tuesday 的值，为 Tuesday 之后的枚举赋值。这就是编译器将 0 赋给 Sunday、1 赋给 Monday、5 赋给 Tuesday、6 赋给 Wednesday、7 赋给 Thursday、8 赋给 Friday、9 赋给 Saturday 的原因。

## 测试你的知识

Q4. 编写一个程序来实现枚举的概念。

答案。

```cpp
#include <iostream.h>
int main()
{
enum month {
    Jan,
    Feb,
    Mar,
    Apr,
    May,
    Jun,
    Jul,
    Aug,
    Sep,
    Oct,
    Nov,
    Dec
};

enum month summer = Jun;
if (summer == May || summer == Jun || summer == Jul)
{
cout << "It is summer " << endl;
}
return 0;

}
```

输出：

```text
It is summer
```

![](img/8a6886c00caa6a1651a6c0e62bff341f_49_0.png)

写一篇关于枚举数据类型（孟买大学，2009 年 5 月）的简短说明。

## 派生数据类型

由现有数据类型创建的数据类型称为派生数据类型。以下是 C++ 中可用的派生数据类型：

- 数组
- 指针

### 数组

数组是数据存储位置的集合，其中每个位置保存相同类型的数据。那么问题来了：为什么我们需要这种复杂的结构？可能存在需要为大量数据项存储相似类型值的情况。基本数据类型在用于存储单个数据时没有问题，但如果要存储的数据更复杂呢？例如，假设你想存储 50 名学生的姓名。你可以通过声明 50 个变量来实现，每个变量存储一个姓名。然而，这并不是正确的方法。想象一下，仅仅为了存储学生姓名就要编写 50 条语句。这个问题的解决方案在于使用数组。使用数组，你可以声明一个能够存储所有这 50 个姓名的变量。使用数组的优点是，它们通过用一两条语句替换多条语句来简化编程。在 C++ 中声明数组的语法是：

```cpp
datatype array_name [array_size];
```

在前面的语法中，

- `datatype`：指合法的 C++ 数据类型
- `array_name`：指用于标识数组的任何标识符
- `array_size`：指一个整数值，表示数组可以存储的元素总数

声明数组的代码片段是：

```cpp
int  item [10];
```

在前面的代码片段中，声明了 int 类型的 item 数组。该数组最多可以存储 10 个元素。

![](img/8a6886c00caa6a1651a6c0e62bff341f_50_0.png)

在第 3 章*《使用数组和函数》*中会更详细地讨论数组。

### 指针

C++ 中的指针被定义为存储另一个变量内存地址的变量。指针与 C++ 中的其他变量类似，在使用前需要声明。指针的声明方式与其他变量相同。指针存储特定数据类型的地址，例如 int、char 和 float。声明指针的语法是：

```cpp
datatype *point_name;
```

在前面的语法中，

- **datatype：** 指任何合法的 C++ 基本数据类型或用户定义的数据类型。
- **point_name：** 指任何变量名。* 告知编译器变量 point_name 是一个指针变量。

![](img/8a6886c00caa6a1651a6c0e62bff341f_51_0.png)

> 第 4 章《指针》将更详细地讨论指针。

在讨论了内置数据类型、用户定义数据类型和派生数据类型之后，我们来学习如何将一种数据类型的变量转换为另一种数据类型。

## C++ 中的类型转换和类型强制转换

在 C++ 中，将整型变量转换为浮点型的概念称为类型转换。清单 10 展示了整型变量如何自动转换为浮点型（你可以在 CD 的 code/chapter1 文件夹中找到 IntTypeEx.cpp 文件：

### 清单 10：将整型变量转换为浮点型

```cpp
#include <iostream.h>
int main()
{
    int a = 10;
    float b = 22.7;
    b = b + a;
    cout << "The value of the b variable is:" <<b;
    return 0;
}
```

**输出：**

```text
The value of the b variable is:32.700001
```

在清单 10 中，int 类型变量 a 被赋值为 10，在变量 a 和 b 的值相加期间，它会自动转换为 10.0。在清单 10 中，你会注意到从 int 到 float 的自动类型转换。然而，如果你想将 double 类型变量转换为 int 类型，则需要为此显式提供代码。将一个数据类型变量显式转换为另一种数据类型的概念称为类型强制转换。清单 11 展示了如何将 double 类型变量强制转换为 int 类型（你可以在 CD 的 code/chapter1 文件夹中找到 DoubleTypeEx.cpp 文件）：

### 清单 11：将 double 类型变量强制转换为 int 类型

```cpp
#include <iostream.h>
int main()
{
double a = 2134.56;
int b;
b = int(a);
cout << "The value of the b variable is:" <<b;
return 0;
}
```

输出：

The value of the b variable is:2134

在清单 11 中，一个 double 类型变量被强制转换为 int 类型变量 b。在讨论了类型强制转换和类型转换的概念之后，现在我们来学习预处理器指令，它们可帮助你在 C++ 程序中包含文件并定义宏。

## 预处理器指令

预处理器指令在代码传递给 C++ 编译器之前处理。编译器包含一个预处理器，它在 C++ 编译过程开始之前处理预处理器指令。预处理器指令可帮助你执行操作，例如在 C++ 程序中包含头文件，以便你可以使用头文件中存储的函数，以及定义常量。C++ 中的预处理指令如下：

- `#define`：定义宏/标记
- `#elif`：表示 else-if 指令，其工作方式类似于 else-if 语句
- `#else`：表示 else 指令，其工作方式类似于 else 语句
- `#error`：生成编译时错误消息
- `#if`：表示 if 指令，其工作方式类似于 if 语句
- `#ifdef`：表示 if-defined 指令，用于测试宏是否存在
- `#ifndef`：表示 if-not-defined 指令
- `#include`：在 C++ 程序中包含文件
- `#line`：表示当前行指令
- `#pragma`：表示在代码之前运行的特殊功能
- `#undef`：取消定义已定义的宏

你可以将这些预处理器指令与预定义标记一起使用，例如 `_cplusplus`，如果当前程序是 C++，则定义该标记，否则不定义。你可以使用 `ifdef` 指令检查标记是否已定义，该指令以 `#ifdef` 关键字开始，以 `#endif` 关键字结束。以下代码片段检查程序是否在 C++ 中创建：

```cpp
#ifdef _cplusplus
cout << "This is a C++ program." << endl;
#endif
```

你可以在代码中使用的一些预定义标记如下：

- `_cplusplus`：如果当前程序是 C++，则定义
- `_STDC_`：如果当前程序是标准 C，则定义
- `__LINE__`：保存当前行号
- `__FILE__`：保存当前文件名
- `__DATE__`：保存程序的编译日期
- `__TIME__`：保存程序的编译时间

预处理器指令还支持*宏*，宏是预定义代码的片段。这些宏会连同宏中存储的值一起被预处理器替换。所有预处理器指令将在以下各节中详细讨论：

- #define 指令
- #undef 指令
- #include 指令
- 条件编译中使用的指令

### #define 指令

#define 指令是一种预处理器指令，用于为 C++ 程序中的常量赋予有意义的名称，然后该常量在程序中用作宏。#define 指令有以下两种使用方式：

- 定义保存常量值的变量
- 定义函数常量

使用 #define 指令的两种语法是：

```cpp
#define <macro/constant name> < value> // defining constant variable/macro
#define < func_name () > < func_val> // function constant/macro
```

在第一种语法中，宏/常量名可以是任何逻辑变量名，以用作常量或宏，值可以是赋给该变量的任何逻辑值。这方面的一个示例是 #define PI 3.14。在这种情况下，程序中所有出现的 PI 都将替换为值 3.14。

在第二种语法中，func_name() 是要为其创建宏的函数名，func_val 是要赋给函数中传递的参数的值。例如，在 #define radius (a) (PI *a*a) 中，a 将被替换为 C++ 程序传入函数 radius 的参数。现在，考虑以下代码片段，以更好地理解函数宏的概念：

```cpp
result = radius (a);
```
