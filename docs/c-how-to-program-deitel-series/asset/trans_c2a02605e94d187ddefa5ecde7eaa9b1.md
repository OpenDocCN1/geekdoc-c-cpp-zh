
```cpp
// utility function to confirm proper day value based on
// month and year; handles leap years, too
unsigned int Date::checkDay( int testDay ) const
{
    static const array< int, monthsPerYear + 1 > daysPerMonth =
       { 0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31 };

    // determines if testDay is valid for specified month
    if ( testDay > 0 && testDay <= daysPerMonth[ month ] )
        return testDay;

    // February 29 check for leap year
    if ( month == 2 && testDay == 29 && ( year % 400 == 0 ||
       ( year % 4 == 0 && year % 100 != 0 ) ) )
        return testDay;

    throw invalid_argument( "Invalid day for current month and year" );
} // end function checkDay
```

**图 9.18** | Date 类成员函数定义。（第 2 部分，共 2 部分。）

```cpp
// Fig. 9.19: Employee.h
// Employee class definition showing composition.
// Member functions defined in Employee.cpp.
#ifndef EMPLOYEE_H
#define EMPLOYEE_H

#include <string>
#include "Date.h" // include Date class definition

class Employee
{
public:
    Employee( const std::string &, const std::string &,
       const Date &, const Date & );
    void print() const;
    ~Employee(); // provided for custom destruction order
private:
    std::string firstName; // composition: member object
    std::string lastName; // composition: member object
    const Date birthDate; // composition: member object
    const Date hireDate; // composition: member object
}; // end class Employee

#endif
```

**图 9.19** | 展示组合的 Employee 类定义。

```cpp
// Fig. 9.20: Employee.cpp
// Employee class member-function definitions.
#include <iostream>
#include "Employee.h" // Employee class definition
#include "Date.h" // Date class definition
using namespace std;

// constructor uses member initializer list to pass initializer
// values to constructors of member objects
Employee::Employee( const string &first, const string &last,
    const Date &dateOfBirth, const Date &dateOfHire )
    : firstName( first ), // initialize firstName
      lastName( last ), // initialize lastName
      birthDate( dateOfBirth ), // initialize birthDate
      hireDate( dateOfHire ) // initialize hireDate
{
    // output Employee object to show when constructor is called
    cout << "Employee object constructor: "
         << firstName << ' ' << lastName << endl;
} // end Employee constructor

// print Employee object
void Employee::print() const
{
    cout << lastName << ", " << firstName << " Hired: ";
    hireDate.print();
    cout << " Birthday: ";
    birthDate.print();
    cout << endl;
} // end function print

// output Employee object to show when its destructor is called
Employee::~Employee()
{
    cout << "Employee object destructor: "
         << lastName << ", " << firstName << endl;
} // end ~Employee destructor
```

**图 9.20** | Employee 类成员函数定义。

### Employee 构造函数的成员初始化列表

构造函数头部（图 9.20 第 12 行）后面的冒号（:）开始 *成员初始化列表*。成员初始化器指定传递给 string 和 Date 数据成员构造函数的 Employee 构造函数参数。参数 first、last、dateOfBirth 和 dateOfHire 分别传递给对象 firstName（第 12 行）、lastName（第 13 行）、birthDate（第 14 行）和 hireDate（第 15 行）的构造函数。同样，成员初始化器用逗号分隔。成员初始化器的顺序无关紧要。它们按照成员对象在类 Employee 中声明的顺序执行。

![](img/b42ba5cd262b1358d16610173f975e4d_442_0.png)

### 良好编程实践 9.3

为清晰起见，请按类中数据成员的声明顺序列出成员初始化器。

### Date 类的默认拷贝构造函数

在学习 Date 类（图 9.17）时，请注意该类并未提供接收 Date 类型参数的构造函数。那么，为什么 Employee 构造函数的成员初始化列表可以通过将 Date 对象传递给它们的 Date 构造函数来初始化 birthDate 和 hireDate 对象呢？正如我们在 9.9 节中提到的，编译器为每个类提供一个默认拷贝构造函数，该构造函数将构造函数参数对象的每个数据成员复制到正在初始化的对象的对应成员中。第 10 章将讨论如何定义自定义拷贝构造函数。

### 测试 Date 和 Employee 类

图 9.21 创建了两个 Date 对象（第 10-11 行），并将它们作为参数传递给第 12 行创建的 Employee 对象的构造函数。第 15 行输出 Employee 对象的数据。在第 10-11 行创建每个 Date 对象时，图 9.18 第 11-25 行定义的 Date 构造函数会显示一行输出，以表明构造函数被调用了（参见示例输出的前两行）。[注意：图 9.21 的第 12 行导致另外两次 Date 构造函数调用，但这两次调用并未出现在程序输出中。当 Employee 的每个 Date 成员对象在 Employee 构造函数的成员初始化列表（图 9.20 第 14-15 行）中被初始化时，会调用 Date 类的默认拷贝构造函数。由于该构造函数是由编译器隐式定义的，它不包含任何用于演示何时被调用的输出语句。]

```cpp
// Fig. 9.21: fig09_21.cpp
// Demonstrating composition—an object with member objects.
#include <iostream>
#include "Date.h" // Date class definition
#include "Employee.h" // Employee class definition
using namespace std;

int main()
{
    Date birth( 7, 24, 1949 );
    Date hire( 3, 12, 1988 );
    Employee manager( "Bob", "Blue", birth, hire );

    cout << endl;
    manager.print();
} // end main
```

![](img/b42ba5cd262b1358d16610173f975e4d_443_0.png)

**图 9.21** | 演示组合——一个包含成员对象的对象。

## 9.12 友元函数和友元类

类的 *友元函数* 是一种非成员函数，它有权访问类的公有和非公有成员。独立函数、整个类或其他类的成员函数都可以被声明为另一个类的 *友元*。

本节展示了一个说明友元函数如何工作的机械示例。在第 10 章中，我们将展示用于类对象的重载运算符的友元函数——您将看到，有时成员函数无法用于某些重载运算符。

### 声明友元

要将函数声明为类的友元，请在类定义中的函数原型前加上关键字 friend。要将类 ClassTwo 的所有成员函数声明为类 ClassOne 的友元，请放置如下形式的声明：

```cpp
friend class ClassTwo;
```

在类 ClassOne 的定义中。

友谊是 *授予的，而非索取的*——要使类 B 成为类 A 的友元，类 A 必须 *显式* 声明类 B 是其友元。友谊不是 *对称的*——如果类 A 是类 B 的友元，你不能推断出类 B 是类 A 的友元。友谊不是 *可传递的*——如果类 A 是类 B 的友元，且类 B 是类 C 的友元，你不能推断出类 A 是类 C 的友元。

### 使用友元函数修改类的私有数据

图 9.22 是一个机械示例，其中我们定义了友元函数 setX 来设置类 Count 的私有数据成员 x。按照惯例，我们将友元声明（第 9 行）放在类定义中的 *最前面*，甚至在 *公有* 成员函数声明之前。同样，这个友元声明可以出现在类中的 *任何地方*。

函数 setX（第 29-32 行）是一个独立（全局）函数——它不是类 Count 的成员函数。因此，当为对象 counter 调用 setX 时，第 41 行将 counter 作为参数传递给 setX，而不是使用句柄（例如对象名）来调用函数。

```cpp
counter.setX( 9 ); // error: setX not a member function
```

如果删除第 9 行的友元声明，您将收到错误消息，指出函数 setX 无法修改类 Count 的私有数据成员 x。

```cpp
// Fig. 9.22: fig09_22.cpp
// Friends can access private members of a class.
#include <iostream>
using namespace std;

// Count class definition
class Count
{
    friend void setX( Count &, int ); // friend declaration
```

**图 9.22** | 友元可以访问类的私有成员。（第 1 部分，共 2 部分。）

