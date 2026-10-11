
```
//main.cpp
#include "file1.h"
#include "file2.h"
int main() 
{
  ...
}

//file1.h
#include "head.h"
...

//file2.cpp
#include "head.h"
...

//head.h
...
class Point
{
}
```

由于 `#include` 指令的嵌套使用，头文件 `head.h` 被包含了两次，然后系统会在编译和定义类 `Point` 时指示错误。如何避免这种错误？我们需要在可能被多次包含的头文件中使用条件编译指令。我们可以使用一个互斥标识符来标记文件是否已经编译：如果它已经编译过，那么这个程序段就不应该被重复包含，编译器将不再重新编译重复的部分。因此，`head.h` 可以重写为：

```
//head.h
#ifndef HEAD_H
#define HEAD_H
...
class Point
{
#endif
```

在这个头文件中，编译器首先需要判断标识符 `HEAD_H` 是否已经定义。如果它未定义，则说明头文件还没有被编译，编译器将宏定义标识符 `HEAD_H` 并编译以下程序段。定义的标识符标记该文件已经编译；如果标识符已定义，则说明文件应该已经编译过，编译器将不再重新编译以下程序段。这样，我们就可以避免类 `Point` 的重复定义。

## 5.7 示例 – 人员信息管理程序

我们在第 4 章中使用一个小型公司的人员信息管理程序作为示例来解释类和成员函数的设计与使用。在本节中，我们将对上一章示例 4.5 进行以下改进：

- 1. 我们在 5.2.1 和 5.3.1 中引入了静态数据成员。在示例中，我们将利用静态数据成员具有静态生命期的特性专注于数据成员——员工人数。这一新功能是：在 `employee` 中添加一个静态数据成员来存储当前最大的员工编号，当添加新员工时，当前最大值会自动增加。通过这种方式，我们可以避免频繁调用成员函数 `IncreaseEmpNo(int steps)`。

- 2. 我们在 5.6.1 中引入了 C++ 程序的通用结构。在这里我们将根据上一章示例 4,5 调整程序结构：我们将类的定义部分和实现部分分为两个文件。

此示例中的类设计与示例 4.5 中的几乎相同。预计我们在基类 `employee` 中添加一个静态数据成员 `static employeeNo` 来存储当前最大的员工编号；我们还删除了成员函数

| employee |
| :--- |
| # individualEmpNo : int |
| # grade : int |
| # accumPay : float |
| # employeeNo : int = 1000 |
| + employee() |
| ~employee() |
| + promote(int) : void void |
| + SetaccumPay(pe : float) : void |
| GetIndividualEmpNo() : int |
| + Grade() : int |
| + GetaccumPay() : float |

> 图 5.9：人员信息管理程序的 UML 图。

## 5.7 示例 – 人员信息管理程序

`IncreaseEmpNo(int steps)` 是一个通过构造函数实现的函数。该类设计的 UML 图如图 5.9 所示。

**示例 5.11:** 人员信息管理程序。

整个程序分为三个文件：类定义头文件 `employee.h`、类实现文件 `employee.cpp` 和主函数文件 `5_11.cpp`。编译后，我们需要将 `5_11.cpp` 和 `employee.cpp` 链接在一起。如果我们使用 VC++ 环境，则应该将 `5_11.cpp` 和 `employee.cpp` 放在同一个项目中。

```cpp
//employee.h
class employee
{
protected:
    int individualEmpNo;        //个人编号
    int grade;                  //级别
    float accumPay();           //工资
    static int employeeNo;     //当前最大员工编号
public:
    employee();                  //构造函数
    ~employee();                 //析构函数
    void promote(int);          //晋升函数
    void SetAccumPay(float pa); //设置工资函数
    int GetIndividualEmpNo();   //获取编号函数
    int GetGrade();             //获取级别函数
    float GetAccumPay();        //获取工资函数
};
```

```cpp
//employee.cpp
#include<iostream>
#include "employee.h"
using namespace std;
int employee::employeeNo=1000; //员工编号的初始值

employee::employee() {
    individualEmpNo=employeeNo++; //新添加的员工编号为
    grade=1;                      //当前最大员工编号加1
    accumPay=0.0;                 //级别的初始值为 1
} //工资的初始值为 0

void employee::promote(int increment) //晋升，晋升的级别由
    grade+=increment;             //增量决定
}
```

```cpp
void employee::SetAccumPay(float pa)
{ 
    accumPay=pa; 
} //设置工资
```

```cpp
int employee::GetIndividualEmpNo()
{ 
    return individualEmpNo; 
} //获取成员编号
```

```cpp
int employee::Getgrade()
{ 
    return grade; 
} //获取级别
```

```cpp
float employee::GetAccumPay()
{ 
    return accumPay; 
} //设置工资
```

```cpp
//5_11.cpp
#include<iostream>
#include"employee.h"
using namespace std;
int main()
{
    employee m1;
    employee t1;
    employee sm1;
    employee s1;
    cout<<"请输入员工的月工资：";
    float pa;
    cin>>pa;
    m1.promote(3); //将 m1 晋升 3 级
    m1.SetAccumPay(pa); //设置 m1 的月工资
    cout<<"请输入员工的月工资:"\n";
    cin>>pa;
    t1.promote(2); //将 t1 晋升 2 级
    t1.SetAccumPay(pa); //设置 t1 的月工资
    cout<<"请输入员工的月工资:"\n";
    cin>>pa;
    sm1.promote(2); //将 s1 晋升 2 级（注：此处代码逻辑为sm1）
    sm1.SetAccumPay(pa); //设置 sm1 的月工资
    cout<<"请输入员工的月工资:"\n;
    cin >>pa;
    s1.SetAccumPay(pa); //设置 s1 的月工资
}
```

```cpp
//显示 m1 的信息
cout<<"编号："%(<<m1.GetindividualEmpNo()
    <<"级别："%(<<m1.Getgrade()<<", 本月工资："
""<<m1.GetaccumPay()]<<endl;
```

```cpp
//显示 t1 的信息
cout<<"编号："%(<<t1.GetindividualEmpNo()
    <<"级别："%(<<t1.Getgrade()<<", 本月工资："
""<<t1.GetaccumPay()]<<endl;
```

```cpp
//显示 s1 的信息
cout<<"编号："%(<<s1.GetindividualEmpNo()
    <<"级别："%(<<s1.Getgrade()<<", 本月工资："
""<<s1.GetaccumPay()]<<endl;
}
```

结果：

| 输入/输出 |
| :--- |
| 请输入员工的月工资：8000 |
| 请输入员工的月工资：4000 |
| 请输入员工的月工资：7000 |
| 请输入员工的月工资：1600 |
| 编号:1000 级别:4，本月工资：8000 |
| 编号:1001 级别:3，本月工资：4000 |
| 编号:1002 级别:3，本月工资：7000 |
| 编号:1003 级别:1，本月工资：1600 |

我们可以发现这个示例的结果与示例 4.5 的结果相同。然而，`employee` 类中静态成员的使用使得该类的所有对象共享此静态数据。通过这种方式，每当创建一个对象时，构造函数都会自动生成员工编号。

此外，我们在 5.6.2 节中引入了条件编译指令。通过使用条件编译指令，我们可以避免重复包含 `employee` 类导致的编译错误。读者可以参考 5.6.2 节在 `employee.h` 中添加条件编译指令。

## 5.8 总结

数据共享和数据保护机制是 C++ 中非常重要的特性。它们包括标识符的作用域、可见性和生命周期，通过类的静态成员实现同类不同对象之间的数据共享和操作共享，并使用常量成员设置成员的保护属性。

## 练习题

- 5.1 什么是作用域？C++ 中有什么种作用域？
- 5.2 什么是可见性？可见性的通用规则是什么？
- 5.3 运行以下程序的运行是什么？运行它看看是否如你想的一样。

```cpp
#include <iostream>
using namespace std;
void myFunction();
int x = 5, y = 7;
int main() {
    cout << "main 函数中的 x: " << x << "\n";
    cout << "main 函数中的 y: " << y << "\n";
    myFunction();
    cout << "从 myFunction 返回！\n";
    cout << "main 函数中的 x: " << x << "\n";
    cout << "main 函数中的 y: " << y << "\n";
}
void myFunction() {
    int y = 10;
    cout << "myFunction 中的 x: " << x << "\n";
    cout << "myFunction 中的 y: " << y << "\n";
}
```

- 5.4 假设有两个独立的类——`Engine`（引擎）和 `Fuel`（燃料），如何让 `Fuel` 的成员访问 `Engine` 的私有和保护成员？
- 5.5 什么是静态数据成员？它的特性是什么？
- 5.6 什么是静态成员函数？它的特性是什么？
- 5.7 定义一个类 `Cat`：它有一个静态数据成员 `HowManyCats` 用于统计猫的数量；静态成员函数 `GetHowMany()` 用于……
- 5.8 什么是静态数据成员？
- 5.9 如果类 `A` 是……的友元
- 5.10 静态变量可以是私有的吗？
- 5.11 在 `main()` 中定义一个静态变量。
- 5.12 在 `main()` 中定义一个静态变量。
- 5.13 定义类 `X`, `Y`, `Z`...
- 5.14 定义类 `Boat`（船）和 `Car`（汽车）...

### 6.1.1 数组的声明与使用

### 1. 数组的声明

数组是一种用户定义的数据类型，在使用之前需要进行声明。数组的声明应由以下部分组成：

- a) 定义数组的名称；
- b) 定义元素的类型；
- c) 定义数组的结构（例如数组的维度、每个维的大小等）

声明数组的通用形式如下：

```
Data type Identifier[Constant expression 1]
[ Constant expression 1]...;
```

数组中元素的类型由“Data type”指定。该数据类型可以是基本类型（如 `int`、`float`），也可以是用户定义的类型（如结构体 `struct` 和类 `class`）。
数组名指定为“Identifier”。**数组名是一个常量，代表数组元素在内存中的起始地址。**

诸如“Constant Expression 1”、“Constant Expression 2”等表达式被称为下标表达式。它们必须是无符号整数类型（unsigned int）。数组的下标用于限制数组中元素的数量，并指定每个元素在数组中的顺序和位置。在 C语言中，n 维数组的元素实际上是一个 (n-1) 维数组。因此，C 中 n 维数组的声明为数组名加上下标表达式，其中每个下标表达式的值表示每个维度的大小（注意，这并不是该维度上下标的上界）。数组元素的数量可以通过乘以数组声明中所有下标表达式的值来计算。例如：

```
int b[10];
```

表示 `b` 是一个 `int` 类型的数组，它有 10 个元素：`b[0]`...`b[9]`。它可以用于存储一个包含 10 个元素的整数数组。

```cpp
int a[5][3];
```

表示 `a` 是一个 `int` 类型的二维数组。其第一维的长度为 5（下标从 0 到 4），第二维的长度为 3（下标从 0 到 2）。因此，`a` 的元素总数为 15 个。它可以用于存储一个 `int` 类型的表格，有五行三列。值得注意的是，数组下标的值从 0 开始。对于上述声明的数组 `a`，第一个元素是 `a[0][0]`，最后一个元素是 `a[4][2]`。换句话说，每个维度的下标都从 0 开始。

### 2. 数组的使用

在使用数组时，我们可以分别操作它的元素。数组元素通过下标表示。对于已声明的数组，我们可以这样引用它的元素：

```
Array name[Subscript expression 1][Subscript expression 2] ... ;
```

这里，下标表达式的数量取决于数组的维度。对于一个 N 维数组，它的每个元素都必须由 N 个表达式表示。

数组的每个元素等同于对应类型的变量。我们可以在允许该类型变量的地方使用数组元素。例如，我们可以像使用整数变量一样使用整数数组元素。同样，类类型数组的每个元素都可以作为该类的普通对象使用。

- a) 数组元素的下标表达式可以是任何算术表达式，只要表达式的值是整数。
- b) 数组元素某一维的下标值不能超过原始声明数组中该维度的上下界。否则，在运行时可能会发生“数组越界”（Array is out of range）的错误。

示例 6.1：数组的声明与使用。

```cpp
//6_1.cpp
#include <iostream>
using namespace std;
int main()
{
    int A[10],B[10];
    int i;
    for(i=0;i<10;i++)
    {
        A[i]=i*2-1;
        B[10-i-1]=A[i];
    }
    for(i=0;i<10;i++)
    {
        cout<<"A["<<i<<"]="<<A[i];
        cout<<"B["<<i<<"]="<<B[i]<<endl;
    }
}
```

在这个程序中，我们声明了两个各包含 10 个元素的一维数组 `A` 和 `B`。我们使用 `for` 循环为它们的元素赋值。在引用 `B` 的元素时，我们使用算术表达式作为下标。运行程序后，0, 1, ..., 9 分别被赋值给 `A` 的元素：`A[0]`, `A[1]`, ..., `A[9]`。`B` 的元素是 `A` 元素的倒序排列。

如果我们重写两个循环语句 `(i=0; i<10; i++)` 和 `(i=1; i<=10)`，编译过程中不会产生任何错误。但在运行过程中，我们可能无法得到正确的结果，而是遇到意料之外的错误。这是一个典型的“数组越界”错误。

### 6.1.2 数组的存储与初始化

#### 1. 数组的存储

数组元素在内存中连续有序地存储。它们占据内存中一组连续的位置。逻辑上相邻的元素在物理上也是相邻的。数组名代表数组元素的起始地址。一维数组的元素简单地根据其下标顺序连续排列。多维数组的元素也是连续排列的，且存储顺序的规则非常重要。数组元素的存储顺序与我们操作数组元素时采用何种顺序有关。在 C++ 中，一维数组可以看作是一个向量，其元素按照下标存储在内存中，如下所示。例如，如下语句：

```cpp
int ay[5];
```

声明了一个包含 5 个元素的 `int` 类型一维数组。该数组可以看作是一个向量 `[ay[0], ay[1], ay[2], ay[3], ay[4]]`。二维数组可以看作是一个矩阵，其第一维下标称为行下标，第二维下标称为列下标。例如，如下语句：

```cpp
int M[2][3];
```
