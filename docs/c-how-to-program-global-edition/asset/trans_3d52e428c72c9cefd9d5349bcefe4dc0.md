
在 C++11 中，你可以使用列表初始化来初始化动态分配的内置数组的元素，如下所示

```
int *gradesArray = new int[ 10 ]{};
```

这里所示的空花括号表示应为每个元素使用默认初始化——对于基本类型，每个元素都被设置为 0。花括号中也可以包含数组元素的以逗号分隔的初始化列表。

## 使用 delete [] 释放动态分配的内置数组

要释放 gradesArray 指向的内存，请使用以下语句

```
delete [] gradesArray;
```

如果指针指向一个对象内置数组，则该语句首先为数组中的每个对象调用析构函数，然后释放内存。如果前面的语句未包含方括号 [] 且 gradesArray 指向一个对象内置数组，则结果未定义——某些编译器仅为数组中的第一个对象调用析构函数。对空指针使用 delete 或 delete [] 没有任何效果。

![](img/bf54db922e6fa8319cba11069e785521_729_0.png)

## 常见编程错误 18.3

使用 delete 而不是 delete [] 来释放对象内置数组可能导致运行时逻辑错误。为了确保数组中的每个对象都收到析构函数调用，始终使用 operator delete [] 释放作为数组分配的内存。同样，始终使用 operator delete 释放作为单个元素分配的内存——使用 operator delete [] 删除单个对象的结果是未定义的。

## C++11：使用 unique_ptr 管理动态分配的内存

C++11 的新 unique_ptr 是一种用于管理动态分配内存的“智能指针”。当 unique_ptr 超出作用域时，其析构函数会自动将管理的内存返回到自由存储区。在第 22 章中，我们将介绍 unique_ptr 并展示如何使用它来管理动态分配的对象或动态分配的内置数组。

## 18.10 案例研究：Array 类

我们在第 6 章讨论了内置数组。基于指针的数组存在许多问题，包括：

- 程序很容易“走出”内置数组的两端，因为 C++ 不会检查下标是否超出数组范围（尽管你可以显式地这样做）。
- 大小为 n 的内置数组必须将元素编号为 0、…、n – 1；不允许使用替代下标范围。
- 整个内置数组不能一次输入或输出；每个元素必须单独读取或写入（除非该数组是以 null 结尾的 C 字符串）。
- 两个内置数组不能使用相等或关系运算符进行有意义的比较（因为数组名只是指向数组在内存中开始位置的指针，而两个数组总是在不同的内存位置）。
- 当内置数组传递给设计用于处理任意大小数组的通用函数时，数组的大小必须作为额外参数传递。
- 一个内置数组不能使用赋值运算符赋给另一个数组。

类开发是一项有趣、富有创造性且具有智力挑战性的活动——始终以打造有价值的类为目标。使用 C++，你可以通过类和运算符重载实现更强大的数组功能，就像 C++ 标准库中的类模板 array 和 vector 所做的那样。在本节中，我们将开发自己的自定义数组类，其优于内置数组。在本案例研究中，当我们提到“数组”时，我们指的是内置数组。

在此示例中，我们创建一个功能强大的 Array 类，对下标进行范围检查以确保其保持在 Array 的边界内。该类允许使用赋值运算符将一个 Array 对象赋给另一个 Array 对象。Array 对象知道自己的大小，因此不需要将大小单独传递给接收 Array 参数的函数。整个 Array 可以分别使用流提取和流插入运算符进行输入或输出。你可以使用相等运算符 == 和 != 比较 Array。

### 18.10.1 使用 Array 类

图 18.9–18.11 的程序演示了 Array 类及其重载运算符。首先我们逐步介绍 main（图 18.9）和程序的输出，然后考虑类定义（图 18.10）及其每个成员函数定义（图 18.11）。

```
// Fig. 18.9: fig18_09.cpp
// Array class test program.
#include <iostream>
#include <stdexcept>
#include "Array.h"

using namespace std;

int main()
{
    Array integers1( 7 ); // seven-element Array
    Array integers2; // 10-element Array by default

    // print integers1 size and contents
    cout << "Size of Array integers1 is "
        << integers1.getSize()
        << "\nArray after initialization:\n" << integers1;

    // print integers2 size and contents
    cout << "\nSize of Array integers2 is "
        << integers2.getSize()
        << "\nArray after initialization:\n" << integers2;

    // input and print integers1 and integers2
    cout << "\nEnter 17 integers:" << endl;
    cin >> integers1 >> integers2;
```

图 18.9 | 数组类测试程序。（第 1 部分，共 3 部分。）

```
```text
Size of Array integers1 is 7
Array after initialization:
        0               0               0               0
        0               0               0

Size of Array integers2 is 10
Array after initialization:
        0               0               0               0
        0               0               0
        0               0               0

Enter 17 integers:
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17

After input, the Arrays contain:
integers1:
        1               2               3               4
        5               6               7
integers2:
        8               9               10              11
        12              13              14              15
        16              17

Evaluating: integers1 != integers2
integers1 and integers2 are not equal

Size of Array integers3 is 7
Array after initialization:
        1               2               3               4
        5               6               7

Assigning integers2 to integers1:
integers1:
        8               9               10              11
        12              13              14              15
        16              17

integers2:
        8               9               10              11
        12              13              14              15
        16              17

Evaluating: integers1 == integers2
integers1 and integers2 are equal

integers1[5] is 13

Assigning 1000 to integers1[5]
integers1:
        8               9               10              11
        12              1000            14              15
        16              17

Attempt to assign 1000 to integers1[15]
An exception occurred: Subscript out of range
```
```

图 18.9 | 数组类测试程序。（第 3 部分，共 3 部分。）

### 创建数组、输出其大小并显示其内容

程序首先实例化两个 Array 类对象——integers1（图 18.9，第 10 行）包含七个元素，以及 integers2（第 11 行）使用默认 Array 大小——10 个元素（由图 18.10 第 14 行中 Array 默认构造函数的原型指定）。图 18.9 中的第 14–16 行使用成员函数 getSize 确定 integers1 的大小，然后使用 Array 重载的流插入运算符输出 integers1 的内容。示例输出证实构造函数已将 Array 元素正确设置为零。接下来，第 19–21 行输出 Array integers2 的大小，然后使用 Array 重载的流插入运算符输出 integers2 的内容。

### 使用重载的流插入运算符填充数组

第 24 行提示用户输入 17 个整数。第 25 行使用 Array 重载的流提取运算符将前七个值读入 integers1，将剩余的 10 个值读入 integers2。第 27–29 行使用重载的 Array 流插入运算符输出这两个数组，以确认输入已正确执行。

### 使用重载的不等运算符

第 34 行通过求值条件来测试重载的不等运算符

```
integers1 != integers2
```

程序输出显示 Arrays 不相等。

### 使用现有数组的内容初始化新数组

第 39 行实例化第三个 Array，名为 integers3，并用 Array integers1 的副本对其进行初始化。这会调用 Array 类的拷贝构造函数，将 integers1 的元素复制到 integers3 中。我们稍后会讨论拷贝构造函数的细节。拷贝构造函数也可以通过以下方式编写第 39 行来调用：

```
Array integers3 = integers1;
```

前述语句中的等号不是赋值运算符。当等号出现在对象声明中时，它会调用该对象的构造函数。此形式可用于仅向构造函数传递单个参数——具体为 = 符号右侧的值。第 41–43 行输出 integers3 的大小，然后使用 Array 重载的流插入运算符输出 integers3 的内容，以确认 integers3 的元素已由拷贝构造函数正确设置。

### 使用重载的赋值运算符

第 47 行通过将 integers2 赋给 integers1 来测试重载的赋值运算符 (=)。第 49–50 行显示两个 Array 对象的內容，以确认赋值成功。Array integers1 原本包含 7 个整数，但已调整大小以容纳 integers2 中 10 个元素的副本。正如我们将看到的，重载的赋值运算符以对客户端代码透明的方式执行此调整大小操作。

### 使用重载的相等运算符
