
![](img/d0d3b7423c2d9e5650be79209ea1885d_701_0.png)

## 性能提示 17.5

当类中所有对象共用一份数据副本就足够时，使用 static 数据成员来节省存储空间。

## static 数据成员的作用域和初始化

类的 static 数据成员具有类作用域。static 数据成员必须恰好初始化一次。基本类型的 static 数据成员默认初始化为 0。在 C++11 之前，int 或枚举类型的 static const 数据成员可以在类定义中的声明处初始化，而所有其他 static 数据成员必须在全局命名空间作用域（即类定义体之外）定义并初始化。同样，C++11 的类内初始化器也允许在类定义中声明这些变量的地方初始化它们。如果 static 数据成员是提供默认构造函数的类的对象，则该 static 数据成员无需初始化，因为将调用其默认构造函数。

## 访问 static 数据成员

类的 private 和 protected static 成员通常通过类的 public 成员函数或友元访问。即使该类的对象不存在，类的 static 成员也存在。当类的对象不存在时，要访问 public static 类成员，只需在数据成员名称前加上类名和作用域解析运算符 (::)。例如，如果前面提到的变量 martianCount 是 public，则即使没有 Martian 对象，也可以用表达式 Martian::martianCount 访问它。（当然，不鼓励使用 public 数据。）

当类的对象不存在时，要访问 private 或 protected static 类成员，请提供一个 public static 成员函数，并在调用该函数时在其名称前加上类名和作用域解析运算符。static 成员函数是类提供的服务，而不是类的特定对象提供的服务。

![](img/d0d3b7423c2d9e5650be79209ea1885d_701_1.png)

![](img/d0d3b7423c2d9e5650be79209ea1885d_701_2.png)

## 软件工程观察 17.14

即使尚未实例化该类的任何对象，类的 static 数据成员和 static 成员函数也存在并且可以使用。

## 演示 static 数据成员

图 17.27–17.29 的程序演示了一个名为 count 的 private static 数据成员（图 17.27 第 24 行）和一个名为 getCount 的 public static 成员函数（图 17.27 第 18 行）。在图 17.28 中，第 8 行在全局命名空间作用域定义数据成员 count 并将其初始化为零，第 12–15 行定义 static 成员函数 getCount。注意，第 8 行和第 12 行都不包含关键字 static，但这两行都定义 static 类成员。static 关键字不能用于出现在类定义之外的成员定义。数据成员 count 维护已实例化的 Employee 类对象数量的计数。当 Employee 类的对象存在时，可以通过 Employee 对象的任何成员函数引用成员 count——在图 17.28 中，构造函数中的第 22 行和析构函数中的第 32 行都引用了 count。

```
// Fig. 17.27: Employee.h
// Employee class definition with a static data member to
// track the number of Employee objects in memory
#ifndef EMPLOYEE_H
#define EMPLOYEE_H

#include <string>

class Employee
{
public:
Employee( const std::string &, const std::string & ); // constructor
~Employee(); // destructor
std::string getFirstName() const; // return first name
std::string getLastName() const; // return last name

// static member function
static unsigned int getCount(); // return # of objects instantiated
private:
std::string firstName;
std::string lastName;

// static data
static unsigned int count; // number of objects instantiated
}; // end class Employee

#endif
```

图 17.27 | 带有 static 数据成员的 Employee 类定义，用于跟踪内存中 Employee 对象的数量。

```
// Fig. 17.28: Employee.cpp
// Employee class member-function definitions.
#include <iostream>
#include "Employee.h" // Employee class definition
using namespace std;

// define and initialize static data member at global namespace scope
unsigned int Employee::count = 0; // cannot include keyword static

// define static member function that returns number of
// Employee objects instantiated (declared static in Employee.h)
unsigned int Employee::getCount()
{
return count;
} // end static function getCount

// constructor initializes non-static data members and
// increments static data member count
Employee::Employee( const string &first, const string &last )
: firstName( first ), lastName( last )
{
```

图 17.28 | Employee 类成员函数定义。（第 1 部分，共 2 部分。）

```
13
14 // the following scope creates and destroys
15 // Employee objects before main terminates
16 {
17     Employee e1("Susan", "Baker");
18     Employee e2("Robert", "Jones");
19
20     // two objects exist; call static member function getCount again
21     // using the class name and the scope resolution operator
22     cout << "Number of employees after objects are instantiated is "
23         << Employee::getCount();
24
25     cout << "\n\nEmployee 1: "
26         << e1.getFirstName() << " " << e1.getLastName()
27         << "\nEmployee 2: "
28         << e2.getFirstName() << " " << e2.getLastName() << "\n\n";
29 } // end nested scope in main
30
31 // no objects exist, so call static member function getCount again
32 // using the class name and the scope resolution operator
33 cout << "\nNumber of employees after objects are deleted is "
34     << Employee::getCount() << endl;
35 } // end main
```

```
Number of employees before instantiation of any objects is 0
Employee constructor for Susan Baker called.
Employee constructor for Robert Jones called.
Number of employees after objects are instantiated is 2
Employee 1: Susan Baker
Employee 2: Robert Jones
~Employee() called for Robert Jones
~Employee() called for Susan Baker
Number of employees after objects are deleted is 0
```

图 17.29 | 跟踪某个类的对象数量的 static 数据成员。（第 2 部分，共 2 部分。）

如果成员函数不访问类的非 static 数据成员或非 static 成员函数，则应将其声明为 static。与非 static 成员函数不同，static 成员函数没有 this 指针，因为 static 数据成员和 static 成员函数独立于类的任何对象而存在。this 指针必须指向类的特定对象，而调用 static 成员函数时，内存中可能没有任何该类的对象。

**常见编程错误 17.6**
在 static 成员函数中使用 this 指针是编译错误。

**常见编程错误 17.7**
将 static 成员函数声明为 const 是编译错误。const 限定符表示函数不能修改其操作对象的内容，但 static 成员函数独立于类的任何对象而存在和操作。

## 17.15 小结

本章加深了对类的讲解，并通过 Time 类案例研究介绍了若干新特性。我们使用包含防护来防止头文件（.h）中的代码在同一源代码（.cpp）文件中被多次包含。你学习了如何使用箭头运算符通过对象类类型的指针访问对象的成员。你学习了成员函数具有类作用域——除非类的客户端通过对象名、对类对象的引用、指向类对象的指针或作用域解析运算符来引用成员函数名，否则该名称只对该类的其他成员可见。我们还讨论了访问函数（通常用于获取数据成员的值或测试条件的真伪）和工具函数（支持类的 public 成员函数操作的 private 成员函数）。

你学习了构造函数可以指定默认实参，使其能够以多种方式被调用。你还学习了任何可以在不带参数的情况下调用的构造函数都是默认构造函数，并且每个类最多只能有一个默认构造函数。我们讨论了用于在类的对象被销毁之前对该对象执行终止清理的构造函数，并演示了对象的构造函数和析构函数的调用顺序。

我们演示了当成员函数返回对 private 数据成员的引用或指针时可能发生的问题，这会破坏类的封装。我们还展示了同一类型的对象可以使用默认的逐成员赋值相互赋值——在第 18 章中，我们将讨论当对象包含指针成员时这如何导致问题。

你学习了如何指定 const 对象和 const 成员函数以防止修改对象，从而实施最小权限原则。你还学习了通过组合，一个类可以将其他类的对象作为成员。我们演示了如何使用友元函数。

你学习了 this 指针作为隐式实参传递给类的每个非 static 成员函数，使它们能够访问正确对象的数据成员和其他非 static 成员函数。我们显式使用 this 指针访问类的成员并支持级联成员函数调用。我们说明了 static 数据成员和成员函数的概念，并演示了如何在自己的类中声明和使用它们。

在第 18 章中，我们将通过展示如何使 C++ 的运算符能够处理类类型对象来继续学习类和对象——这一过程称为运算符重载。例如，你将看到如何重载 << 运算符，使其可用于输出完整数组，而无需显式使用重复语句。

## 总结

*17.2 节 Time 类案例研究*

### 17.2 节 Time 类案例研究
- 预处理指令 #ifndef（意为“如果未定义”；第 662 页）和 #endif（第 662 页）用于防止头文件被多次包含。如果这些指令之间的代码之前尚未包含在应用程序中，则 #define（第 662 页）定义一个可用于防止将来再次包含的名称，并且该代码会被包含到源代码文件中。
- C++11 之前，只有 static const int 数据成员可以在类体内的声明处初始化。因此，数据成员通常应由类的

