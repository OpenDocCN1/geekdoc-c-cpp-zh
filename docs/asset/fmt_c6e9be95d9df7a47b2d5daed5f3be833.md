
# BasePlusCommissionEmployee 类代码示例

```cpp
// print BasePlusCommissionEmployee object

void BasePlusCommissionEmployee::print() const

{

    cout << "base-salaried commission employee: " << firstName << ' '

        << lastName << "\nsocial security number: " << socialSecurityNumber

        << "\ngross sales: " << grossSales

        << "\ncommission rate: " << commissionRate

        << "\nbase salary: " << baseSalary;

} // end function print
```

Fig. 12.8 | `BasePlusCommissionEmployee` 类表示除佣金外还领取基本工资的员工。 (第 3 部分，共 3 部分。)

```cpp
// Fig. 12.9: fig12_09.cpp
// Testing class BasePlusCommissionEmployee.

#include <iostream>

using std::cout;

using std::endl;

using std::fixed;

#include <iomanip>

using std::setprecision;

// BasePlusCommissionEmployee class definition

#include "BasePlusCommissionEmployee.h"

int main()

{

    // instantiate BasePlusCommissionEmployee object
    BasePlusCommissionEmployee

        employee( "Bob", "Lewis", "333-33-3333", 5000, .04, 300 );

    // set floating-point output formatting
    cout << fixed << setprecision( 2 );

    // get commission employee data
    cout << "Employee information obtained by get functions: \n"
        << "\nFirst name is " << employee.getFirstName()
        << "\nLast name is " << employee.getLastName()
        << "\nSocial security number is "
        << employee.getSocialSecurityNumber()
        << "\nGross sales is " << employee.getGrossSales()
        << "\nCommission rate is " << employee.getCommissionRate()
        << "\nBase salary is " << employee.getBaseSalary() << endl;

    employee.setBaseSalary( 1000 ); // set base salary

    cout << "\nUpdated employee information output by print function: \n"
        << endl;

    employee.print(); // display the new employee information
```

Fig. 12.9 | `BasePlusCommissionEmployee` 类测试程序。 (第 1 部分，共 2 部分。)

```cpp
// display the employee's earnings
cout << "\n\nEmployee's earnings: $" << employee.earnings() << endl;
return 0;
} // end main
```

通过 `get` 函数获得的员工信息：

名字是 Bob
姓氏是 Lewis
社会安全号码是 333-33-3333
毛销售额是 5000.00
佣金率是 0.04
基本工资是 300.00

由 `print` 函数输出的更新后的员工信息：

base-salaried commission employee: Bob Lewis
social security number: 333-33-3333
gross sales: 5000.00
commission rate: 0.04
base salary: 1000.00

员工收入：$1200.00

Fig. 12.9 | `BasePlusCommissionEmployee` 类测试程序。 (第 2 部分，共 2 部分。)

## 探索类 `BasePlusCommissionEmployee` 与类 `CommissionEmployee` 之间的相似性

请注意，类 `BasePlusCommissionEmployee` 的大部分代码（图 12.7–12.8）与类 `CommissionEmployee` 的代码（图 12.4–12.5）相似，如果不是完全相同的话。例如，在类 `BasePlusCommissionEmployee` 中，私有数据成员 `firstName` 和 `lastName` 以及成员函数 `setFirstName`、`getFirstName`、`setLastName` 和 `getLastName` 与类 `CommissionEmployee` 完全相同。类 `CommissionEmployee` 和 `BasePlusCommissionEmployee` 都包含私有数据成员 `socialSecurityNumber`、`commissionRate` 和 `grossSales`，以及用于操作这些成员的 `get` 和 `set` 函数。此外，`BasePlusCommissionEmployee` 构造函数几乎与类 `CommissionEmployee` 的构造函数相同，只是 `BasePlusCommissionEmployee` 的构造函数还设置了 `baseSalary`。类 `BasePlusCommissionEmployee` 的其他新增内容是私有数据成员 `baseSalary` 以及成员函数 `setBaseSalary` 和 `getBaseSalary`。类 `BasePlusCommissionEmployee` 的 `print` 成员函数几乎与类 `CommissionEmployee` 的相同，只是 `BasePlusCommissionEmployee` 的 `print` 还输出数据成员 `baseSalary` 的值。

我们 literally 从类 `CommissionEmployee` 复制代码并粘贴到类 `BasePlusCommissionEmployee` 中，然后修改类 `BasePlusCommissionEmployee` 以包含基本工资和操作基本工资的成员函数。这种“复制粘贴”方法容易出错且耗时。更糟糕的是，它可能在整个系统中传播同一代码的多个物理副本，造成代码维护的噩梦。有没有办法“吸收”一个类的 数据成员和成员函数，使其成为另一个类的组成部分，而无需重复代码？在接下来的几个示例中，我们正是这样做的，使用继承。

## 软件工程观察 12.3

从一个类复制并粘贴代码到另一个类可能会在多个源代码文件中传播错误。为了避免重复代码（以及可能的错误），在希望一个类“吸收”另一个类的数据成员和成员函数的情况下，应使用继承，而不是“复制粘贴”方法。

## 软件工程观察 12.4

使用继承时，所有类层次结构中共同的数据成员和成员函数都在基类中声明。当需要对这些通用功能进行更改时，您只需在基类中进行更改——派生类随后继承这些更改。没有继承，就需要在包含所讨论代码副本的所有源代码文件中进行更改。

## 12.4.3 创建 `CommissionEmployee`-`BasePlusCommissionEmployee` 继承层次结构

现在我们创建并测试一个新的 `BasePlusCommissionEmployee` 类（图 12.10–12.11），它派生自类 `CommissionEmployee`（图 12.4–12.5）。在这个示例中，`BasePlusCommissionEmployee` 对象是 `CommissionEmployee`（因为继承传递了类 `CommissionEmployee` 的功能），但类 `BasePlusCommissionEmployee`

```cpp
// Fig. 12.10: BasePlusCommissionEmployee.h
// BasePlusCommissionEmployee class derived from class
// CommissionEmployee.

#ifndef BASEPLUS_H
#define BASEPLUS_H

#include <string> // C++ standard string class

using std::string;

#include "CommissionEmployee.h" // CommissionEmployee class declaration

class BasePlusCommissionEmployee : public CommissionEmployee
{

public:
    BasePlusCommissionEmployee( const string &, const string &,
        const string &, double = 0.0, double = 0.0, double = 0.0 );
    void setBaseSalary( double ); // set base salary
    double getBaseSalary() const; // return base salary
    double earnings() const; // calculate earnings
    void print() const; // print BasePlusCommissionEmployee object
private:
    double baseSalary; // base salary
}; // end class BasePlusCommissionEmployee

#endif
```

Fig. 12.10 | `BasePlusCommissionEmployee` 类定义表明与类 `CommissionEmployee` 的继承关系。

```cpp
19 // set base salary
20 void BasePlusCommissionEmployee::setBaseSalary( double salary )
21 {
22     baseSalary = ( salary < 0.0 ) ? 0.0 : salary;
23 } // end function setBaseSalary
24
25 // return base salary
26 double BasePlusCommissionEmployee::getBaseSalary() const
27 {
28     return baseSalary;
29 } // end function getBaseSalary
30
31 // calculate earnings
32 double BasePlusCommissionEmployee::earnings() const
33 {
34     // derived class cannot access the base class's private data
35     return baseSalary + ( commissionRate * grossSales );
36 } // end function earnings
37
38 // print BasePlusCommissionEmployee object
39 void BasePlusCommissionEmployee::print() const
40 {
41     // derived class cannot access the base class's private data
42     cout << "base-salaried commission employee: " << firstName << ' '
43         << lastName << "\nsocial security number: " << socialSecurityNumber
44         << "\ngross sales: " << grossSales
45         << "\ncommission rate: " << commissionRate
46         << "\nbase salary: " << baseSalary;
47 } // end function print
```

`C:\cppfp_examples\ch12\Fig12_10_11\BasePlusCommissionEmployee.cpp(35)` :
error C2248: '`CommissionEmployee::commissionRate`' :
    cannot access private member declared in class '`CommissionEmployee`'
    `C:\cppfp_examples\ch12\Fig12_10_11\CommissionEmployee.h(37)` :
    see declaration of '`CommissionEmployee::commissionRate`'
    `C:\cppfp_examples\ch12\Fig12_10_11\CommissionEmployee.h(10)` :
    see declaration of '`CommissionEmployee`'

`C:\cppfp_examples\ch12\Fig12_10_11\BasePlusCommissionEmployee.cpp(35)` :
error C2248: '`CommissionEmployee::grossSales`' :
    cannot access private member declared in class '`CommissionEmployee`'
    `C:\cppfp_examples\ch12\Fig12_10_11\CommissionEmployee.h(36)` :
    see declaration of '`CommissionEmployee::grossSales`'
    `C:\cppfp_examples\ch12\Fig12_10_11\CommissionEmployee.h(10)` :
    see declaration of '`CommissionEmployee`'

`C:\cppfp_examples\ch12\Fig12_10_11\BasePlusCommissionEmployee.cpp(42)` :
error C2248: '`CommissionEmployee::firstName`' :
    cannot access private member declared in class '`CommissionEmployee`'
    `C:\cppfp_examples\ch12\Fig12_10_11\CommissionEmployee.h(33)` :
    see declaration of '`CommissionEmployee::firstName`'
    `C:\cppfp_examples\ch12\Fig12_10_11\CommissionEmployee.h(10)` :
    see declaration of '`CommissionEmployee`'

Fig. 12.11 | `BasePlusCommissionEmployee` implementation file: private base-class data cannot be accessed from derived class. (Part 2 of 3.)

```cpp
C:\cppfp_examples\ch12\Fig12_10_11\BasePlusCommissionEmployee.cpp(43) :

error C2248: 'CommissionEmployee::lastName' :

    cannot access private member declared in class 'CommissionEmployee'

    C:\cppfp_examples\ch12\Fig12_10_11\CommissionEmployee.h(34) :

    see declaration of 'CommissionEmployee::lastName'

    C:\cppfp_examples\ch12\Fig12_10_11\CommissionEmployee.h(10) :

    see declaration of 'CommissionEmployee'

C:\cppfp_examples\ch12\Fig12_10_11\BasePlusCommissionEmployee.cpp(43) :

error C2248: 'CommissionEmployee::socialSecurityNumber' :

    cannot access private member declared in class 'CommissionEmployee'
```
