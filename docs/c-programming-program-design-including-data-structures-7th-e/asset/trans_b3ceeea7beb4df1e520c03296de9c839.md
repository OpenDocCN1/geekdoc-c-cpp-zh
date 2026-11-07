
考虑以下语句：

- 1. `num = 78;`
- 2. `p = &num;`
- 3. `*p = 24;`

下面显示了每条语句执行后变量的值。

| 执行语句后 | 变量的值 | 说明 |
|---|---|---|
| 1 | `p` = 1200；`num` = 1800；`num` 的内存位置包含 `78` | 语句 `num = 78;` 将 78 存入 `num`。 |
| 2 | `p` = 1800；`num` = 1800；`num` 的内存位置包含 `78` | 语句 `p = &num;` 将 `num` 的地址（即 1800）存入 `p`。 |
| 3 | `p` = 1800；`num` = 1800；`num` 的内存位置包含 `24` | 语句 `*p = 24;` 将 24 存入 `p` 所指向的内存位置。因为 `p` 的值为 1800，所以语句 3 将 24 存入内存位置 1800。注意，`num` 的值也发生了变化。 |

让我们总结前面的讨论。

- 1. 诸如 `int *p;` 这样的声明只为 `p` 分配内存，而不为 `*p` 分配内存。稍后，你将学习如何为 `*p` 分配内存。
- 2. `p` 的内容只指向一个 `int` 类型的内存位置。
- 3. `&p`、`p` 和 `*p` 的含义各不相同。
- 4. `&p` 表示 `p` 的地址——即 1200（在图 12-1 中）。
- 5. `p` 表示 `p` 的内容，在语句 `p = &num;` 执行后为 1800。
- 6. `*p` 表示 `p` 所指向的内存位置的内容。注意，在语句 `p = &num;` 执行后，`*p` 的值为 78；在语句 `*p = 24;` 执行后，`*p` 的值为 24。

### 例 12-2

考虑以下语句：

```cpp
int *p;
int x;
```

假设 p 和 x 的内存分配如图 12-2 所示。

![](img/d0be7fc6d804b63484835c6c8bc67a07_867_0.png)

**图 12-2** 变量 p 和 x

`&p`、`p`、`*p`、`&x` 和 `x` 的值如下：

| 表达式 | 值 |
|---|---|
| &p | 1400 |
| p | ?（未知） |
| *p | 不存在（未定义） |
| &x | 1750 |
| x | ?（未知） |

假设以下语句按给定顺序执行：

```cpp
x = 50;
p = &x;
*p = 38;
```

在每条语句执行后，`&p`、`p`、`*p`、`&x` 和 `x` 的值如下所示。

在语句 `x = 50;` 执行后，`&p`、`p`、`*p`、`&x` 和 `x` 的值如下：

| 表达式 | 值 |
|---|---|
| &p | 1400 |
| p | ?（未知） |
| *p | 不存在（未定义） |
| &x | 1750 |
| x | 50 |

在语句 `p = &x;` 执行后，`&p`、`p`、`*p`、`&x` 和 `x` 的值如下：

| 表达式 | 值 |
|---|---|
| &p | 1400 |
| p | 1750 |
| *p | 50 |
| &x | 1750 |
| x | 50 |

在语句 `*p = 38;` 执行后，`&p`、`p`、`*p`、`&x` 和 `x` 的值如下。（因为 `*p` 和 `x` 引用同一内存空间，所以 `x` 的值也变为 38。）

| 表达式 | 值 |
|---|---|
| &p | 1400 |
| p | 1750 |
| *p | 38 |
| &x | 1750 |
| x | 38 |

让我们注意以下几点：

- 1. `p` 是一个指针变量。
- 2. `p` 的内容只指向一个 `int` 类型的内存位置。
- 3. 内存位置 `x` 存在且类型为 `int`。因此，赋值语句：

       p = &x;

   是合法的。执行此赋值语句后，`*p` 有效且有意义。

例 12-3 中的程序进一步说明了指针变量如何工作。

### 例 12-3

以下程序说明了指针变量如何工作：

```cpp
//Chapter 12: Example 12-3

#include <iostream>                                          //Line 1
#include <iomanip>                                           //Line 2

using namespace std;                                         //Line 3

const double PI = 3.1416;                                    //Line 4

int main()                                                   //Line 5
{                                                            //Line 6
    double radius;                                           //Line 7
    double *radiusPtr;                                       //Line 8

    cout << fixed << showpoint << setprecision(2);           //Line 9

    radius = 2.5;                                            //Line 10
    radiusPtr = &radius;                                     //Line 11

    cout << "Line 12: Radius = " << radius
         << ", area = " << PI * radius * radius << endl;     //Line 12

    cout << "Line 13: Radius = " << *radiusPtr
         << ", area = "
         << PI * (*radiusPtr) * (*radiusPtr) << endl;        //Line 13

    cout << "Line 14: Enter the radius: ";                   //Line 14
    cin >> *radiusPtr;                                       //Line 15
    cout << endl;                                            //Line 16

    cout << "Line 17: Radius = " << radius << ", area = "
         << PI * radius * radius << endl;                  //Line 17
    cout << "Line 18: Radius = " << *radiusPtr
         << ", area = "
         << PI * (*radiusPtr) * (*radiusPtr) << endl
         << endl;                                          //Line 18

    cout << "Line 19: Address of radiusPtr: "
         << &radiusPtr << endl;                            //Line 19
    cout << "Line 20: Value stored in radiusPtr: "
         << radiusPtr << endl;                              //Line 20
    cout << "Line 21: Address of radius: "
         << &radius << endl;                                //Line 21
    cout << "Line 22: Value stored in radius: "
         << radius << endl;                                 //Line 22

    return 0;                                               //Line 23
}                                                           //Line 24
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

```text
Line 12: Radius = 2.50, area = 19.64
Line 13: Radius = 2.50, area = 19.64
Line 14: Enter the radius: 4.90

Line 17: Radius = 4.90, area = 75.43
Line 18: Radius = 4.90, area = 75.43

Line 19: Address of radiusPtr: 0012FF50
Line 20: Value stored in radiusPtr: 0012FF5C
Line 21: Address of radius: 0012FF5C
Line 22: Value stored in radius: 4.90
```

前面的程序按如下方式工作。第 7 行中的语句将 radius 声明为 **double** 类型的变量，第 8 行中的语句将 radiusPtr 声明为 **double** 类型的指针变量。第 10 行中的语句将 2.5 存入 radius，第 11 行中的语句将 radius 的地址存入 radiusPtr。第 12 行中的语句使用内存位置 radius 中存储的值输出圆的半径和面积。第 13 行中的语句使用 radiusPtr 所指向的内存位置中存储的值输出圆的半径和面积。注意，第 12 行和第 13 行中语句的输出相同，因为 radiusPtr 指向 radius。接下来，第 14 行中的语句提示用户输入半径，第 15 行中的语句将半径存入 radiusPtr 所指向的内存位置。接下来，与第 12 行和第 13 行中的语句类似，第 17 行和第 18 行中的语句使用变量 radius 和 radiusPtr 输出半径和面积。第 19 行至第 22 行中的语句输出 radiusPtr 的地址、radiusPtr 中存储的值、radius 的地址以及 radius 中存储的值。

从第 20 行和第 21 行中语句的输出可知，radiusPtr 存储的是变量 radius 的地址。（注意，第 19、20 和 21 行的输出分别显示的 radiusPtr 的地址、radiusPtr 的值和 radius 的地址依赖于机器。当你在自己的机器上运行此程序时，很可能会得到不同的值。此外，指针值（即地址）默认以十六进制打印。）

## 类、结构体和指针变量

在上一节中，你学习了如何声明和操作简单数据类型（如 int 和 char）的指针。你也可以声明指向其他数据类型（如类）的指针。现在你将学习如何声明和操作指向类和结构体的指针。（回想一下，类和结构体具有相同的能力。类和结构体之间的唯一区别是，默认情况下，类的所有成员都是 private，而默认情况下，结构体的所有成员都是 public。因此，以下讨论对两者都适用。）

考虑以下结构体声明：

```cpp
struct studentType
{
    char name[26];
    double gpa;
    int sID;
    char grade;
};

studentType student;
studentType *studentPtr;
```

在前面的声明中，student 是 studentType 类型的对象，studentPtr 是 studentType 类型的指针变量。以下语句将 student 的地址存入 studentPtr：

```cpp
studentPtr = &student;
```

以下语句将 3.9 存入对象 student 的成员 gpa：

```cpp
(*studentPtr).gpa = 3.9;
```

表达式 `(*studentPtr).gpa` 是指针解引用和类成员选择的混合。在 C++ 中，点运算符 `.` 的优先级高于解引用运算符。

让我们对此稍作说明。在表达式 `(*studentPtr).gpa` 中，运算符 `*` 首先求值，因此表达式 `*studentPtr` 首先求值。因为 `studentPtr` 是 `studentType` 类型的指针变量，所以 `*studentPtr` 指的是一个类型为
