

## 使用 delete 释放动态内存

要销毁动态分配的对象并释放该对象占用的空间，请使用 `delete` 运算符，如下所示：

```cpp
delete timePtr;
```

这条语句首先*调用 timePtr 所指向对象的析构函数，然后释放与该对象关联的内存，并将内存归还给自由存储区*。

> **常见编程错误10.2**
> *当不再需要动态分配的内存时若不及时释放，可能会导致系统过早耗尽内存。这种情况有时被称为“内存泄漏”。*

![](img/b42ba5cd262b1358d16610173f975e4d_487_0.png)

> **错误预防提示10.1**
> *不要删除不是由 new 分配的内存。这样做会导致未定义的行为。*

![](img/b42ba5cd262b1358d16610173f975e4d_487_1.png)

> **错误预防提示10.2**
> *删除一块动态分配的内存后，务必不要再次删除同一块内存。防范这一点的一种方法是立即将指针设置为 nullptr。删除 nullptr 没有任何效果。*

![](img/b42ba5cd262b1358d16610173f975e4d_487_2.png)

## 初始化动态内存

你可以为新创建的基础类型变量提供初始化器，例如：

```cpp
double *ptr = new double(3.14159);
```

这将新创建的 double 变量初始化为 3.14159，并将生成的指针赋给 ptr。同样的语法可用于指定传递给对象构造函数的逗号分隔的参数列表。例如，

```cpp
Time *timePtr = new Time(12, 45, 0);
```

将新的 Time 对象初始化为下午 12:45，并将生成的指针赋给 timePtr。

## 使用 new [] 动态分配内置数组

你也可以使用 new 运算符动态分配内置数组。例如，可以按如下方式分配一个包含 10 个元素的整型数组并将其赋给 gradesArray：

```cpp
int *gradesArray = new int[10]();
```

这行代码声明了 int *gradesArray，并将一个指向动态分配的 10 元素 int 数组首元素的指针赋给它。`new int[10]` 后面的圆括号会对数组的元素进行值初始化——基础数值类型被设置为 0，bool 被设置为 false，指针被设置为 nullptr，类对象由其默认构造函数初始化。在编译时创建的数组大小必须使用整型常量表达式指定；然而，动态分配数组的大小可以使用任何在执行时可求值的非负整型表达式来指定。

## C++11：将列表初始化器用于动态分配的内置数组

![](img/b42ba5cd262b1358d16610173f975e4d_487_3.png)

在 C++11 之前，当动态分配对象的内置数组时，你*无法*向每个对象的构造函数传递参数——每个对象都由其*默认构造函数*初始化。

- 当内置数组传递给设计用于处理任意大小数组的通用函数时，必须将数组的**大小**作为额外参数传递。
- 一个内置数组不能通过赋值运算符*赋值*给另一个内置数组。

类开发是一项有趣、富有创造性且具有智力挑战性的活动——其目标始终是*打造有价值的类*。使用 C++，你可以通过类和运算符重载实现更强大的数组功能，正如 C++ 标准库中的类模板 `array` 和 `vector` 所做的那样。在本节中，我们将开发一个自定义的 Array 类，它比内置数组更可取。在本案例研究中，当我们提到“数组”时，指的是内置数组。

在此示例中，我们创建一个功能强大的 `Array` 类，它执行范围检查以确保下标始终在 `Array` 的边界内。该类允许使用赋值运算符将一个 `Array` 对象赋给另一个 `Array` 对象。`Array` 对象知道自己的大小，因此无需将大小单独传递给接收 `Array` 参数的函数。整个 `Array` 可以分别使用流提取运算符和流插入运算符进行输入或输出。你可以使用相等运算符 `==` 和 `!=` 比较 `Array`。

## 10.10.1 使用 Array 类

图 10.9–10.11 的程序演示了 `Array` 类及其重载运算符。首先我们浏览 `main`（图 10.9）和程序的输出，然后考察类定义（图 10.10）及其每个成员函数定义（图 10.11）。

```cpp
// Fig. 10.9: fig10_09.cpp
// Array class test program.
#include <iostream>
#include <stdexcept>
#include "Array.h"
using namespace std;

int main()
{
    Array<int> integers1( 7 ); // seven-element Array
    Array<int> integers2; // 10-element Array by default

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

**图 10.9** | Array 类测试程序。（第 1 部分，共 3 部分。）

```text
Size of Array integers1 is 7
Array after initialization:
             0          0          0          0
             0          0          0


Size of Array integers2 is 10
Array after initialization:
             0          0          0          0
             0          0          0          0
             0          0          0

Enter 17 integers:
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17

After input, the Arrays contain:
integers1:
             1          2          3          4
             5          6          7
integers2:
             8          9          10         11
             12         13         14         15
             16         17

Evaluating: integers1 != integers2
integers1 and integers2 are not equal

Size of Array integers3 is 7
Array after initialization:
             1          2          3          4
             5          6          7

Assigning integers2 to integers1:
integers1:
             8          9          10         11
             12         13         14         15
             16         17

integers2:
             8          9          10         11
             12         13         14         15
             16         17

Evaluating: integers1 == integers2
integers1 and integers2 are equal

integers1[5] is 13

Assigning 1000 to integers1[5]
integers1:
             8          9          10         11
             12         1000       14         15
             16         17

Attempt to assign 1000 to integers1[15]
An exception occurred: Subscript out of range
```

**图 10.9** | Array 类测试程序。（第 3 部分，共 3 部分。）

### 创建数组、输出其大小并显示其内容

程序首先实例化 Array 类的两个对象——integers1（图 10.9 第 10 行）包含 7 个元素，以及 integers2（第 11 行）使用默认的 Array 大小——10 个元素（由图 10.10 第 14 行的 Array 默认构造函数原型指定）。图 10.9 第 14–16 行使用成员函数 getSize 确定 integers1 的大小，然后使用 Array 重载的流插入运算符输出 integers1 的内容。示例输出确认构造函数将 Array 元素正确设置为零。接下来，第 19–21 行输出 Array integers2 的大小，然后使用 Array 重载的流插入运算符输出 integers2 的内容。

### 使用重载的流提取运算符填充数组

第 24 行提示用户输入 17 个整数。第 25 行使用 Array 重载的流提取运算符将前 7 个值读入 integers1，将剩余 10 个值读入 integers2。第 27–29 行使用重载的 Array 流插入运算符输出这两个数组，以确认输入正确执行。

### 使用重载的不等于运算符

第 34 行通过计算以下条件来测试重载的不等于运算符：

```cpp
integers1 != integers2
```

程序输出显示这两个 Array 不相等。

### 使用现有 Array 内容的副本初始化新 Array

第 39 行实例化名为 integers3 的第三个 Array，并使用 Array integers1 的副本对其进行初始化。这将调用类 Array 的复制构造函数，将 integers1 的元素复制到 integers3 中。稍后我们将讨论复制构造函数的细节。也可以通过将第 39 行写为以下形式来调用复制构造函数：

```cpp
Array<int> integers3 = integers1;
```

上述语句中的等号不是赋值运算符。当等号出现在对象的声明中时，它会调用该对象的构造函数。这种形式只能向构造函数传递单个参数——具体来说，就是 = 符号右侧的值。

第 41–43 行输出 integers3 的大小，然后使用 Array 重载的流插入运算符输出 integers3 的内容，以确认 integers3 的元素已由复制构造函数正确设置。

### 使用重载的赋值运算符

第 47 行通过将 integers2 赋给 integers1 来测试重载的赋值运算符（=）。第 49–50 行显示两个 Array 对象的内容以确认赋值成功。Array integers1 最初包含 7 个整数，但已被调整为包含 integers2 中 10 个元素的副本。我们将在后面看到，重载的赋值运算符以对客户端代码透明的方式执行此调整大小操作。

### 使用重载的相等运算符

第 55 行使用重载的相等运算符（==）确认在完成第 47 行的赋值后，对象 integers1 和 integers2 确实相同。

