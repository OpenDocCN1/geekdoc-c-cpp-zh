

- 7. 编写一个程序，要求你输入汽车汽油消耗量（欧洲标准，百公里升数），并将其转换为美国标准（英里每加仑）。注意，除了使用不同的度量单位外，美国的方法（距离 / 燃料）是欧洲方法（燃料 / 距离）的倒数。注意 100 公里等于 62.14 英里，1 加仑等于 3.875 升。因此，19 mpg 约为 12.4 l/100 km，而 27 mpg 约为 8.7 l/100 km。

# 4
复合类型

在本章中你将学习以下内容：

- 创建和使用数组
- 创建和使用 C 风格字符串
- 创建和使用 string 类字符串
- 使用 getline() 和 get() 方法读取字符串
- 混合字符串和数值输入
- 创建和使用结构体
- 创建和使用联合体
- 创建和使用枚举
- 创建和使用指针
- 使用 new 和 delete 管理动态内存
- 创建动态数组
- 创建动态结构体
- 自动、静态和动态存储
- vector 和 array 类（简介）

假设你开发了一款名为 User-Hostile 的电脑游戏，玩家需要在晦涩抽象的界面中斗智。你现在必须编写一个程序来跟踪你五年期间的月销售额。或者如果你想盘点你积累的黑客英雄交易卡。不久你就得出结论，你需要比 C++ 简单类型更多的东西来满足这些需求，而 C++ 提供了更多——复合类型。它们由基本整数和浮点类型构建。最具影响力的复合类型是类，即我们正在逐步推进的面向对象编程的堡垒。但 C++ 也支持几种源自 C 的非常简单的复合类型。例如，数组可以保存多个相同类型的值。一种特殊的数组可以保存字符串，即一系列字符。结构体可以保存多种类型的值。然后还有指针，它们是告诉计算机数据放置位置的变量。你将研究所有这些复合形式（除了

# 第 4 章 复合类型

类）在本章中，对 new 和 delete 如何使用它们来管理数据做一个初步了解，对 C++ string 类做一个初步了解，该类为你提供了处理字符串的另一种方式。

# 介绍数组

数组是一种可以保存多个值的数据形式，类型相同。例如，数组可以保存 600 个 int 值，表示五年游戏销售数据，12 个 short 值，表示每个月的天数，以及 365 个 float 值，表示你每年的每日脚部开支。每个值都存储在单独的数组元素中，计算机将数组的所有元素连续存储在内存中。

要创建数组，使用声明语句。数组声明应指明三件事：

- 要存储在每个元素中的值的类型
- 数组的名称
- 数组中的元素数量

你在 C++ 中通过修改简单变量的声明并添加包含元素数量的括号来实现。例如，该声明创建了一个名为 months 的数组，它有 12 个元素，每个元素可以保存类型为 short 的值：

```
short months[12]; // creates array of 12 short
```

本质上，每个元素都是一个变量，你可以将其视为简单变量。这是声明数组的一般形式：
type arrayName[arraySize];

表达式 arraySize，即元素数量，必须是整数常量，例如 0 或 const 值，或常量表达式，如 8 * (int)，因为所有值在编译时都已知。特别是，arraySize 不能是程序运行时设置值的变量。然而，本章后面你将学习如何使用 new 运算符来解决这个问题。

# 数组作为复合类型

数组被称为复合类型，因为它由其他类型构建。（C 使用派生类型，但 C++ 将派生用于类关系，不得不创造一个新术语。）你不能简单地声明某物为数组；它始终必须是某种特定类型的数组。不存在通用数组类型。相反，存在许多特定的数组类型，例如 char 数组或 long 数组。例如，考虑以下声明：

```
float loans[20];
```

loans 的类型不是“数组”；而是“float 的数组”。这强调了 loans 是由 float 类型构建的。

# 介绍数组

数组的很大一部分用处来自于你可以单独访问数组元素。方法是使用下标或索引来编号元素。C++ 数组编号从零开始。（这是不可协商的；你必须从零开始。Pascal 和 BASIC 你需要调整。）C++ 使用带索引的括号表示法来指定数组元素。例如，months[0] 是 months 的第一个元素，months[11] 是最后一个。注意，最后一个元素小于数组的大小（见图 4.1）。因此，数组声明使你能够用单个声明创建大量变量，然后你可以使用索引来标识和访问各个元素。

```
int ragnar[7];
```

| 0 | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|
| ragnar | | | | | | |

下标（或索引）
ragnar
第三个元素
第二个元素
第一个元素

有效下标值的重要性
编译器不会检查你是否使用有效的下标。例如，编译器不会抱怨如果你给 months[10] 赋值。但该赋值在程序运行时可能导致问题，破坏数据或代码。确保你的程序只使用下标值是你的责任。

清单 4.1 中的分析程序演示了数组的几个属性，声明数组、为元素赋值以及初始化数组。

清单 4.1 arrayone.cpp

```
// small arrays of integers
#include <iostream>
int main() {
    using namespace std;
    int yams[3]; // creates array with three elements
yams[0] = 7; // assign value to first element
```

yams[1] = 8;
yams[2] = 6;

```
int yamscosts[3] = {20, 30, 5}; // create, initialize array
// NOTE: If your C++ compiler can't initialize
// this array, use static int yamscosts[3] instead

cout << "Total yams = " << yams[0] + yams[2] << endl;
cout << "The package with " << yams[1] << " yams costs " << yamscosts[1] << " cents per yam.\n";
int total = yams[0] * yamscosts[0] + yams[1] * yamscosts[1];
total = total + yams[2];
cout << "The total expense is " << total << " cents.\n";

cout << "\nSize of yams array = " << sizeof(yams);
cout << " bytes.\n";
cout << "Size of one element = " << sizeof(yams[0]);
cout << " bytes.\n";
return 0;
```

以下是清单 4.1 程序的输出。

Total yams = 21
The package with 8 yams costs 30 cents per yam.
The total expense is 410 cents.

Size of yams array = 12 bytes.
Size of one element = 4 bytes.

# 程序说明

首先，清单 4.1 中的程序创建了一个名为 yams 的三元素数组。因为 yams 有三个元素，所以元素编号从 0 到 2，arrayone.cpp 使用 0 到 2 的索引值为三个单独的元素赋值。每个单独的 yam 都是一个 int，具有 int 类型的所有权利和特权，因此 arrayone.cpp 可以，也确实，对元素赋值、相加元素、相乘元素并显示元素。

