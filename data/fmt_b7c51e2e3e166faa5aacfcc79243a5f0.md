
#ifndef name

#define name

...

#endif

```

的指令称为 __________ 指令。

5. 前述指令的用途是什么？

### EXERCISES

## Section 14.3

对于练习 1–3，将函数成员添加到类 `Temperature` 以实现指定的操作。你应该用驱动程序对其进行测试，如编程问题 1 和 2 所要求的那样。

- 1. 将 `Temperature` 值转换为 (a) 摄氏度 (b) 开尔文。

- 2. 重载类 `Temperature` 的 `operator+`，以便像 `temp + 3.6` 这样的表达式可以用来将 `Temperature` 值增加一个以相同刻度表示的 `double` 数量的度数。

3. 重载类 `Temperature` 的 `operator-`，以便像 `temp - 3.6` 这样的表达式可以用来将 `Temperature` 值增加一个以相同刻度表示的 `double` 数量的度数。

对于练习 4–12，定义一个类来模拟给定的项目。它应具有适当的构造器、访问器、用于更改数据成员的变异器、输入和输出操作，以及问题中给出的额外操作。

4. 平面中的一条线，由其在笛卡尔坐标 `(x, y)` 中的一点和其斜率指定；额外操作：(a) 确定给定的点是否在线上；(b) 求其方程——斜率为 `m` 且通过坐标为 `(x₁, y₁)` 的点 `P` 的线的点斜式方程为 `y − y₁ = m(x − x₁)`；(c) 求其 `x` 截距和 `y` 截距（如果存在）。

5. 平面中的一条线段，由其端点在笛卡尔坐标 `(x, y)` 中指定；额外操作：(a) 求其长度；(b) 求其中点；(c) 求其方程；(d) 求其垂直平分线的方程。

6. 由其圆心和半径指定的圆；额外操作：(a) 求其面积；(b) 求其周长。

7. 由其三个顶点指定的三角形；额外操作：(a) 确定它是否为 (i) 直角三角形，(ii) 等腰三角形，(iii) 等边三角形；(b) 求其周长；(c) 求其面积。（对于面积，你可以使用海伦公式：面积 = √(`s·(s−a)·(s−b)·(s−c)`)，其中 `a`、`b` 和 `c` 是其边，`s` 是其周长的一半。）

8. 由小时、分钟、秒和 AM/PM 指示符指定的时间；额外操作：(a) 更改为/从夏令时；(b) 两个时间之间的差；(c) 等效的军用时间。

9. 由月份名称、日期数字和年份组成的日期；额外操作：(a) 两个日期之间的差；(b) 确定年份是否为闰年；(c) 求月份中的天数。

10. 电话号码作为区号、本地交换、号码以及拥有该号码的人的名字。

11. 天气统计：日期；城市和州、省或国家；一天中的时间；温度；气压；天气状况（晴朗、局部多云、多云、暴风雨）。

12. 关于一个人的信息：姓名、生日、年龄、性别、社会安全号码、身高、体重、头发颜色、眼睛颜色和婚姻状况。

对于练习 13 和 14，编写适当的类声明来描述指定文件中的信息。参见第 11 章末尾对这些文件的描述。

## PROGRAMMING PROBLEMS

Sections 14.3

- 1. 编写一个驱动程序来测试练习 1 的温度转换方法。
- 2. 编写一个驱动程序来测试练习 2 和 3 的方法 `operator+()` 和 `operator-()`。
- 3. 编写一个驱动程序来测试练习 4 的线类。
- 4. 编写一个驱动程序来测试练习 5 的线段类。
- 5. 编写一个驱动程序来测试练习 6 的圆类。
- 6. 编写一个驱动程序来测试练习 7 的三角形类。
- 7. 编写一个驱动程序来测试练习 8 的时间类。
- 8. 编写一个驱动程序来测试练习 9 的日期类。
- 9. 编写一个驱动程序来测试练习 10 的电话号码类。
- 10. 编写一个驱动程序来测试练习 11 的天气统计类。
- 11. 编写一个驱动程序来测试练习 12 的个人信息类。

12. 有理数是形如 `a/b` 的数，其中 `a` 和 `b` 是整数且 `b ≠ 0`。编写一个程序来进行有理数运算，将每个有理数表示为一个类，该类具有分子和分母数据成员。程序应以 `a/b` 的格式读取和显示所有有理数，如果分母为 1 则仅显示 `a`。以下示例说明了用户应被允许输入的命令菜单：

| Input | Output | Comments |
|---|---|---|
| `3/8 + 1/6` | `13/24` | `a/b + c/d = (ad + bc)/bd` 化为最低项 |
| `3/8 - 1/6` | `5/24` | `a/b - c/d = (ad - bc)/bd` 化为最低项 |
| `3/8 * 1/6` | `1/16` | `a/b * c/d = ac/bd` 化为最低项 |
| `3/8 / 1/6` | `9/4` | `a/b / c/d = ad/bc` 化为最低项 |
| `3/8 I` | `8/3` | 求 `a/b` 的倒数 |
| `8/3 M` | `2 + 2/3` | 将 `a/b` 写成带分数 |
| `6/8 R` | `3/4` | 将 `a/b` 化为最低项 |
| `6/8 G` | `2` | 分子分母的最大公约数 |
| `1/6 L 3/8` | `24` | `a/b` 和 `c/d` 的最小公分母 |
| `1/6 < 3/8` | `true` | `a/b < c/d`？ |
| `1/6 <= 3/8` | `true` | `a/b ≤ c/d`？ |
| `1/6 > 3/8` | `false` | `a/b > c/d`？ |
| `1/6 >= 3/8` | `false` | `a/b ≥ c/d`？ |
| `3/8 == 9/24` | `true` | `a/b = c/d`？ |
| `2/3 X + 2 = 4/5` | `X = -9/5` | 线性方程 `(a/b)X + c/d = e/f` 的解 |

## Pointers and Linked Structures

## CONTENTS

- 15.1 Pointers and Indirection 594
- 15.2 Run-Time Arrays 605
- 15.3 Introduction to Linked Lists 610
- 15.4 The STL `list<T>` Class Template 613
- 15.5 Pointers and Command-Line Arguments 620
- Chapter Summary 625
- Test Yourself 628
- Exercises 630
- Programming Problems 634

> [Pointers] are like jumps, leaping wildly from one part of a data structure to another. Their introduction into high-level languages has been a step backward from which we may never recover.
> 
> C. A. R. HOARE

> He’s making a list,
> And checking it twice;
> Gonna’ find out who’s naughty or nice.
> 
> "SANTA CLAUS IS COMING TO TOWN"

> It is a mistake to try to look too far ahead. The chain of destiny can only be grasped one link at a time.
> 
> SIR WINSTON CHURCHILL

> ... is the sort of person who keeps a list of all of his lists.
> 
> ANONYMOUS

在第 12 章中，我们看到了 C++ 提供的两种用于存储值序列的数据结构：数组和 `vector<T>`。这两个对象之间一个显著的区别是它们被定义的方式。对于我们考虑的那种数组，它们的容量必须在编译时指定，如以下对 `anArray` 的声明所示：

`const int CAPACITY = 50;`

`int anArray[CAPACITY];`

虽然 `vector<T>` 对象可以以类似的方式定义，

`const int CAPACITY = 50;`

`vector<int> aVector(CAPACITY);`

它的容量也可以在运行时指定

`cout << "Enter the number of values to be stored: ";`

`int capacity;`

`cin >> capacity;`

`vector<int> aVector(capacity);`

这是两种对象之间的一个基本区别：数组的存储在程序编译时确定（并且固定），但 `vector<T>` 对象的存储在程序执行时确定（并且可以改变）。`string` 类与 `vector<T>` 类似，因为 `string` 对象的存储会自动调整为存储的字符数。

为了构建容量可以在运行时指定的数组以及存储可以在执行期间增长（和缩小）的其他结构，C++ 提供了在程序执行期间请求和返回内存的方法。为了理解此功能以及如何使用它，我们必须首先研究指针和间接。

通常，我们从一个程序开始——示例 15.1 中的程序——来介绍指针和间接的基础知识。它无意展示指针在程序中通常如何使用。¹

```
/* indirection.cpp illustrates indirection and pointer variables.

Output: addresses of memory locations and the integers stored there */

#include <iostream>

using namespace std;

```

```cpp

int main()

{

    int i = 11,

        j = 22,

        k = 33;

    int * iPtr = &i;

    int * jPtr = &j;

    int * kPtr = &k;

    cout << "\nAt address " << iPtr

         << ", the value " << *iPtr << " is stored.\n"

         << "\nAt address " << jPtr

         << ", the value " << *jPtr << " is stored.\n"

         << "\nAt address " << kPtr

         << ", the value " << *kPtr << " is stored.\n";

}

```

## SAMPLE RUN:

`At address 0xbffff970, the value 11 is stored.`

`At address 0xbffff96c, the value 22 is stored.`

`At address 0xbffff968, the value 33 is stored.`

## 15.1.1 声明和初始化指针

我们从示例 15.1 中程序的第二组声明开始：

```cpp

int * iPtr = &i;

int * jPtr = &j;

int * kPtr = &k;

```

这些语句中有两项新内容：

- 1. `*`在形如*

      ```cpp

      type * variableName;

      ```

      的声明中跟在类型名之后的一个星号 (`*`)，*

      声明 `variableName` 可以存储一个存储指定 `Type` 值 的内存位置的地址。这类变量通常称为 **指针变量**，或简称为指针。因此，声明

      ```cpp

      int * iPtr;

      int * jPtr;

      int * kPtr;

      ```

  声明 `iPtr`、`jPtr` 和 `kPtr` 为指针变量，每个都可以存储一个存储 `int` 的内存位置的地址。这三个变量的类型均为 `int *`。

2. 取地址运算符（`&`）可作为变量名上的前缀一元运算符使用，

```

&variableName

```

返回与 `variableName` 关联的地址，因此 `&` 被称为取地址运算符。因此，表达式 `&i`、`&j` 和 `&k` 分别返回与变量 `i`、`j` 和 `k` 关联的地址（或引用³）。

将这两条信息结合起来，我们看到声明

```

int * iPtr = &i;

int * jPtr = &j;

int * kPtr = &k;

```

将 `iPtr`、`jPtr` 和 `kPtr` 声明为指针变量，每个都可以存储包含 `int` 的内存位置的地址，并且它们将 `iPtr` 初始化为变量 `i` 的地址，`jPtr` 初始化为变量 `j` 的地址，`kPtr` 初始化为变量 `k` 的地址。在示例 15.1 的示例运行中，与变量 `i` 关联的地址是十六进制值 `0xbffff970`，`j` 的地址是 `0xbffff96c`，`k` 的地址是 `0xbffff968`。我们可以按如下方式可视化程序数据的内存布局：⁴

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_611_0.png)

必须记住，在声明中，星号运算符 `*` 必须位于要作为指针的每个标识符之前。因此，

```

double * ptr1,

    * ptr2;

```

是正确地将 `ptr1` 和 `ptr2` 声明为指向 `double` 的指针的声明。如果我们写成

```

double * ptr1,

    ptr2;

```

则只有 `ptr1` 是指针变量；`ptr2` 将是一个普通的 `double` 变量。为了避免犯此错误，我们通常会对每个指针变量使用单独的声明：

```

double * ptr1;

double * ptr2;

```

### 15.1.1.1 使用 `typedef` 提高可读性

一种不需要在指针声明中重复使用星号的替代记法是使用 `typedef` 重命名类型。例如，我们可以在示例 15.1 中首先声明

```

typedef int * IntPointer;

```

然后使用 `IntPointer` 声明指针：

```

IntPointer iPtr = &i,

    jPtr = &j,

    kPtr = &k;

```

此类声明提高了指针声明的可读性，尤其是在声明指针参数时。

## 15.1.2 基本指针操作

C++ 支持对指针的多种操作，包括初始化、解引用、I/O、赋值、比较和算术。我们依次检查这些操作。

### 15.1.2.1 初始化

当指针变量被初始化为一个地址时，如

```

int * iPtr = &i;

```

该地址必须是其类型与指针指向的类型相同的对象的地址。指针据说已绑定到该类型。例如，声明

```

double doubleVar;

int * iPtr = &doubleVar; // ERROR

```

将导致编译器错误，因为整数指针只能存储整数对象的地址。

一个重要的例外是 `0` 可以赋给任何指针变量。由此得到的值称为该类型的空指针值，而 `0` 通常称为空地址。因此，声明

```

char * cPtr = 0;

int * iPtr = 0;

double * dPtr = 0;

```

都是使用空地址的有效初始化。
空地址还可以在布尔表达式中用来指示指针是否指向任何东西：

```

if (dPtr == 0)

    // dPtr 当前未指向任何东西

else

    // dPtr 指向一个内存位置

```

正如我们将看到的，当指针用于存储执行期间分配的内存块的地址时，此类比较尤其重要。

### 15.1.2.2 间接寻址和解引用

指针变量不仅存储地址，还提供对存储在这些地址处的值的访问。形如

```

*pointerVariable

```

的表达式可用于访问存储在 `pointerVariable` 中的地址处的值。它可以被认为是在 `pointerVariable` 中存储的引用（地址）处转到并访问存储在该地址处的值。为了说明，在示例 15.1 的示例运行中，表达式

```

iPtr

```

的值为 `0xbffff970`，而表达式

```

*iPtr
