
让我们注意以下几点：

- p 是指针变量。
- p 的内容仅指向一个 int 类型的内存位置。
- 内存位置 x 存在，且类型为 int。因此，赋值语句：

```cpp
p = &x;
```

是合法的。执行此赋值语句后，*p 是有效且有意义的。

示例 12-3 中的程序进一步说明了指针变量如何工作。

### 示例 12-3

以下程序说明了指针变量如何工作：

```cpp
//Chapter 12: Example 12-3

#include <iostream>                                   //Line 1
#include <iomanip>                                    //Line 2

using namespace std;                                  //Line 3

const double PI = 3.1416;                             //Line 4

int main()                                            //Line 5
{                                                     //Line 6
    double radius;                                    //Line 7
    double *radiusPtr;                                //Line 8

    cout << fixed << showpoint << setprecision(2);    //Line 9

    radius = 2.5;                                     //Line 10
    radiusPtr = &radius;                              //Line 11

    cout << "Line 12: Radius = " << radius            //Line 12
         << ", area = " << PI * radius * radius
         << endl;

    cout << "Line 13: Radius = " << *radiusPtr        //Line 13
         << ", area = "
         << PI * (*radiusPtr) * (*radiusPtr)
         << endl;

    cout << "Line 14: Enter the radius: ";            //Line 14
    cin >> *radiusPtr;                                //Line 15
    cout << endl;                                     //Line 16

    cout << "Line 17: Radius = " << radius << ", area = "
         << PI * radius * radius << endl;                    //Line 17
    cout << "Line 18: Radius = " << *radiusPtr
         << ", area = "
         << PI * (*radiusPtr) * (*radiusPtr) << endl;         //Line 18

    cout << "Line 19: Address of radiusPtr: "
         << &radiusPtr << endl;                              //Line 19
    cout << "Line 20: Value stored in radiusPtr: "
         << radiusPtr << endl;                                //Line 20
    cout << "Line 21: Address of radius: "
         << &radius << endl;                                  //Line 21
    cout << "Line 22: Value stored in radius: "
         << radius << endl;                                   //Line 22

    return 0;                                                  //Line 23
}                                                         //Line 24
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

```text
Line 12: Radius = 2.50, area = 19.64
Line 13: Radius = 2.50, area = 19.64
Line 14: Enter the radius: 4.90

Line 17: Radius = 4.90, area = 75.43
Line 18: Radius = 4.90, area = 75.43

Line 19: Address of radiusPtr: 013EFDA4
Line 20: Value stored in radiusPtr: 013EFDB0
Line 21: Address of radius: 013EFD80
Line 22: Value stored in radius: 4.90
```

前面的程序按如下方式工作。第 7 行的语句将 `radius` 声明为 double 类型的变量，第 8 行的语句将 `radiusPtr` 声明为 double 类型的指针变量。第 10 行的语句将 2.5 存储到 `radius` 中，第 11 行的语句将 `radius` 的地址存储到 `radiusPtr` 中。第 12 行的语句使用存储在内存位置 `radius` 中的值输出圆的半径和面积。第 13 行的语句使用 `radiusPtr` 所指向的内存位置中存储的值输出圆的半径和面积。注意，第 12 行和第 13 行语句的输出相同，因为 `radiusPtr` 指向 `radius`。接下来，第 14 行的语句提示用户输入半径，第 15 行的语句将半径存储到 `radiusPtr` 所指向的内存位置中。接下来，与第 12 行和第 13 行的语句类似，第 17 行和第 18 行的语句使用变量 `radius` 和 `radiusPtr` 输出半径和面积。第 19 行至第 22 行的语句输出 `radiusPtr` 的地址、存储在 `radiusPtr` 中的值、`radius` 的地址以及存储在 `radius` 中的值。

从第 20 行和第 21 行语句的输出可知，`radiusPtr` 存储的是变量 `radius` 的地址。（注意，第 19、20 和 21 行的输出分别显示的 `radiusPtr` 的地址、`radiusPtr` 的值以及 `radius` 的地址依赖于机器。当你在自己的机器上运行此程序时，很可能会得到不同的值。此外，指针值（即地址）默认以十六进制打印。）

## 类、结构体和指针变量

在上一节中，你学习了如何声明和操作简单数据类型的指针，例如 `int` 和 `char`。你也可以声明指向其他数据类型的指针，例如类。现在你将学习如何声明和操作指向类和结构体的指针。（回顾一下，类和结构体具有相同的能力。类和结构体之间的唯一区别是：默认情况下，类的所有成员都是 `private`，而默认情况下，`struct` 的所有成员都是 `public`。因此，以下讨论对两者都适用。）

考虑以下 `struct` 的声明：

```cpp
struct studentType
{
    char name[26];
    double gpa;
    int sID;
    char grade;
};

studentType student;
studentType* studentPtr;
```

在前面的声明中，`student` 是 `studentType` 类型的对象，`studentPtr` 是 `studentType` 类型的指针变量。以下语句将 `student` 的地址存储到 `studentPtr` 中：

```cpp
studentPtr = &student;
```

以下语句将 3.9 存储到对象 `student` 的成员 `gpa` 中：

```cpp
(*studentPtr).gpa = 3.9;
```

表达式 `(*studentPtr).gpa` 是指针解引用和类成员选择的混合。在 C++ 中，点运算符 `.` 的优先级高于解引用运算符。

让我们稍作详细说明。在表达式 `(*studentPtr).gpa` 中，运算符 `*` 首先求值，因此表达式 `*studentPtr` 首先求值。因为 `studentPtr` 是 `studentType` 类型的指针变量，所以 `*studentPtr` 指的是 `studentType` 类型的内存空间，而 `studentType` 是一个 `struct`。因此，`(*studentPtr).gpa` 指的是该 `struct` 的成员 `gpa`。

考虑表达式 `*studentPtr.gpa`。让我们看看这个表达式如何求值。因为 `.`（点）的优先级高于 `*`，所以表达式 `studentPtr.gpa` 首先求值。表达式 `studentPtr.gpa` 会导致语法错误，因为 `studentPtr` 不是 `struct` 变量，所以它没有 `gpa` 这样的成员。

如你所见，在表达式 `(*studentPtr).gpa` 中，括号很重要。然而，拼写错误可能会带来问题。因此，为了简化通过指针访问 `class` 或 `struct` 成员的操作，C++ 提供了另一个运算符，称为成员访问运算符箭头 `->`。运算符 `->` 由两个连续符号组成：一个连字符和“大于”号。

使用运算符 `->` 访问 `class`（`struct`）成员的语法是：

```cpp
pointerVariableName->classMemberName
```

因此，语句：

```cpp
(*studentPtr).gpa = 3.9;
```

等价于语句：

```cpp
studentPtr->gpa = 3.9;
```

因此，使用运算符 `->` 通过指针访问 `class`（`struct`）成员，消除了对括号和解引用运算符的使用。由于拼写错误不可避免，而缺少括号可能导致程序异常终止或错误结果，因此在通过指针访问 `class`（`struct`）成员时，本书使用箭头表示法。

示例 12-4 说明了指针如何与类成员函数一起工作。

### 示例 12-4

考虑以下类：

```cpp
class classExample
{
public:
    void setX(int a);
        //Function to set the value of x
        //Postcondition: x = a;
    void print() const;
        //Function to output the value of x

private:
    int x;
};
```

![](img/b217c421655b51e7494cf3b89bb5432d_876_0.png)
