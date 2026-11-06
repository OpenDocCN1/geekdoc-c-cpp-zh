

```cpp
37
38 // return last name
39 string BasePlusCommissionEmployee::getLastName() const
40 {
41    return lastName;
42 } // end function getLastName
43
44 // set social security number
45 void BasePlusCommissionEmployee::setSocialSecurityNumber(
46    const string &ssn )
47 {
48    socialSecurityNumber = ssn; // should validate
49 } // end function setSocialSecurityNumber
50
51 // return social security number
52 string BasePlusCommissionEmployee::getSocialSecurityNumber() const
53 {
54    return socialSecurityNumber;
55 } // end function getSocialSecurityNumber
56
57 // set gross sales amount
58 void BasePlusCommissionEmployee::setGrossSales( double sales )
59 {
60    grossSales = ( sales < 0.0 ) ? 0.0 : sales;
61 } // end function setGrossSales
62
63 // return gross sales amount
64 double BasePlusCommissionEmployee::getGrossSales() const
65 {
66    return grossSales;
67 } // end function getGrossSales
68
69 // set commission rate
70 void BasePlusCommissionEmployee::setCommissionRate( double rate )
71 {
72    commissionRate = ( rate > 0.0 && rate < 1.0 ) ? rate : 0.0;
73 } // end function setCommissionRate
74
75 // return commission rate
76 double BasePlusCommissionEmployee::getCommissionRate() const
77 {
78    return commissionRate;
79 } // end function getCommissionRate
80
81 // set base salary
82 void BasePlusCommissionEmployee::setBaseSalary( double salary )
83 {
84    baseSalary = ( salary < 0.0 ) ? 0.0 : salary;
85 } // end function setBaseSalary
86
```

**图 12.8** | BasePlusCommissionEmployee 类表示除佣金外还领取基本工资的员工。（第 2 部分，共 3 部分）

```cpp
// return base salary
double BasePlusCommissionEmployee::getBaseSalary() const
{
   return baseSalary;
} // end function getBaseSalary

// calculate earnings
double BasePlusCommissionEmployee::earnings() const
{
   return baseSalary + ( commissionRate * grossSales );
} // end function earnings

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

**图 12.8** | BasePlusCommissionEmployee 类表示除佣金外还领取基本工资的员工。（第 3 部分，共 3 部分）

## 定义 BasePlusCommissionEmployee 类

BasePlusCommissionEmployee 头文件（图 12.7）指定了 BasePlusCommissionEmployee 类的公有服务，包括 BasePlusCommissionEmployee 构造函数（第 13–14 行）以及成员函数 earnings（第 34 行）和 print（第 35 行）。第 16–32 行为类的私有数据成员（在第 37–42 行声明）firstName、lastName、socialSecurityNumber、grossSales、commissionRate 和 baseSalary 声明了公有的 get 和 set 函数。这些变量和成员函数封装了带基本工资的佣金员工的所有必要特性。请注意该类与 CommissionEmployee（图 12.4–12.5）之间的相似性。在本例中，我们还不会利用这种相似性。

BasePlusCommissionEmployee 类的 earnings 成员函数（在图 12.8 的第 94–97 行定义）计算带基本工资的佣金员工的收入。第 96 行返回将员工的基本工资与佣金率和员工总销售额的乘积相加的结果。

## 测试 BasePlusCommissionEmployee 类

图 12.9 测试 BasePlusCommissionEmployee 类。第 1–12 行实例化了 BasePlusCommissionEmployee 类的 employee 对象，分别将 "Bob"、"Lewis"、"333-33-3333"、5000、.04 和 300 作为名字、姓氏、社会安全号码、总销售额、佣金率和基本工资传给构造函数。第 19–25 行使用 BasePlusCommissionEmployee 的 get 函数获取对象的数据成员值以进行输出。第 27 行调用对象的 setBaseSalary 成员函数来更改基本工资。成员函数 setBaseSalary（图 12.8，第 82–85 行）确保不会为数据成员 baseSalary 分配负值，因为员工的基本工资不能为负。图 12.9 的第 31 行调用对象的 print 成员函数以输出更新后的 BasePlusCommissionEmployee 信息，第 34 行调用成员函数 earnings 以显示 BasePlusCommissionEmployee 的收入。

```cpp
// Fig. 12.9: fig12_09.cpp
// Testing class BasePlusCommissionEmployee.
#include <iostream>
#include <iomanip>
#include "BasePlusCommissionEmployee.h"
using namespace std;

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

   employee.setBaseSalary( 1000 );  // set base salary

   cout << "\nUpdated employee information output by print function: \n"
        << endl;
   employee.print(); // display the new employee information

   // display the employee's earnings
   cout << "\nEmployee's earnings: $" << employee.earnings() << endl;
} // end main
```

```
Employee information obtained by get functions:

First name is Bob
Last name is Lewis
Social security number is 333-33-3333
Gross sales is 5000.00
Commission rate is 0.04
Base salary is 300.00

Updated employee information output by print function:

base-salaried commission employee: Bob Lewis
social security number: 333-33-3333
gross sales: 5000.00
commission rate: 0.04
base salary: 1000.00

Employee's earnings: $1200.00
```

**图 12.9** | `BasePlusCommissionEmployee` 类测试程序。

## *探索 BasePlusCommissionEmployee 类与 CommissionEmployee 类之间的相似性*

BasePlusCommissionEmployee 类（图 12.7–12.8）的大部分代码与 CommissionEmployee 类（图 12.4–12.5）的代码相似，即使不完全相同。例如，在 BasePlusCommissionEmployee 类中，私有数据成员 firstName 和 lastName 以及成员函数 setFirstName、getFirstName、setLastName 和 getLastName 与 CommissionEmployee 类完全相同。CommissionEmployee 类和 BasePlusCommissionEmployee 类也都包含私有数据成员 socialSecurityNumber、commissionRate 和 grossSales，以及用于操作这些成员的 get 和 set 函数。此外，BasePlusCommissionEmployee 构造函数几乎与 CommissionEmployee 类的构造函数相同，只是 BasePlusCommissionEmployee 的构造函数还设置了 baseSalary。BasePlusCommissionEmployee 类的其他新增内容为私有数据成员 baseSalary 以及成员函数 setBaseSalary 和 getBaseSalary。BasePlusCommissionEmployee 类的 print 成员函数与 CommissionEmployee 类的 print 成员函数几乎相同，只是 BasePlusCommissionEmployee 的 print 还会输出数据成员 baseSalary 的值。

我们确实从 CommissionEmployee 类复制了代码并粘贴到 BasePlusCommissionEmployee 类中，然后修改了 BasePlusCommissionEmployee 类以包含基本工资和操作基本工资的成员函数。这种“复制粘贴”方法容易出错且耗时。更糟的是，它会在整个系统中散布同一份代码的许多物理副本，造成代码维护的噩梦。有没有一种方法可以“吸收”一个类的数据成员和成员函数，使它们成为另一个类的一部分，而无需重复代码？在接下来的几个示例中，我们将使用继承来做到这一点。

![](img/023f159fdd47d944d48e08843cea732d_573_0.png)

> **软件工程观察 12.3**
> *从一个类向另一个类复制粘贴代码可能会将错误扩展到多个源代码文件。为了避免重复代码（并可能避免错误），在希望一个类“吸收”另一个类的数据成员和成员函数的情况下，我们使用继承，而不是“复制粘贴”方法。*

> **软件工程观察 12.4**
> *使用继承时，层次结构中所有类的公共数据成员和成员函数都在基类中声明。当这些公共特性需要更改时，只需在基类中进行更改——派生类随后会继承这些更改。如果没有继承，则需要修改所有包含相关代码副本的源代码文件。*

### 12.4.3 创建 CommissionEmployee–BasePlusCommissionEmployee 继承层次结构

现在我们创建并测试一个新的 BasePlusCommissionEmployee 类（图 12.10–12.11），它派生自 CommissionEmployee 类（图 12.4–12.5）。在本例中，BasePlusCommissionEmployee 对象是一个 CommissionEmployee（因为继承

