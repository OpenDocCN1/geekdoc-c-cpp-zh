
请注意虚函数 `print`（图 13.14，第 54–58 行）提供了一个实现，该实现将在每个派生类中被重写。然而，这些函数中的每一个都将使用抽象类的 `print` 版本来打印 `Employee` 层次结构中所有类共有的信息。

## 13.6.2 创建具体派生类 SalariedEmployee

类 `SalariedEmployee`（图 13.15–13.16）派生自类 `Employee`（图 13.15 第 8 行）。公共函数包括一个构造函数，该构造函数以 first name、last name、social security number 和 weekly salary 作为参数（第 11–12 行）；一个 set 函数，用于将数据成员 `weeklySalary` 分配为新的非负值（第 14 行）；一个 get 函数，用于返回 `weeklySalary` 的值（第 15 行）；一个计算 `SalariedEmployee` earnings 的虚函数 `earnings`（第 18 行）和一个输出员工类型，即 "salaried employee: " 后跟由基类 `Employee` 的 `print` 函数和 `SalariedEmployee` 的 `getWeeklySalary` 函数生成的员工特定信息的虚函数 `print`（第 19 行）。

图 13.16 包含 `SalariedEmployee` 的成员函数实现。该类的构造函数将 first name、last name 和 social security number 传递给 `Employee` 构造函数（第 11 行），以初始化从基类继承但在派生类中不可访问的私有数据成员。函数 `earnings`（第 30–33 行）重写 `Employee` 中的纯虚函数 `earnings`，以提供返回 `SalariedEmployee` 的 weekly salary 的具体实现。如果我们没有实现 `earnings`，类 `SalariedEmployee` 将是一个抽象类，任何尝试实例化该类的对象的尝试都会导致编译错误（当然，我们希望 `SalariedEmployee` 在这里是一个具体类）。请注意，在类 `SalariedEmployee` 的头文件中，我们将成员函数 `earnings` 和 `print` 声明为 `virtual`（图 13.15 第 18–19 行）——实际上，在这些成员函数前放置 `virtual` 关键字是多余的。我们已在基类 `Employee` 中将它们定义为 `virtual`，因此它们在整个类层次结构中仍然是虚函数。回想一下 Good Programming Practice 13.1，明确地在层次结构的每个级别声明此类函数为 `virtual` 可以提高程序的清晰度。

```cpp
25     return weeklySalary;

26 } // end function getWeeklySalary

27

28 // calculate earnings;

29 // override pure virtual function earnings in Employee

30 double SalariedEmployee::earnings() const

31 {

32     return getWeeklySalary();

33 } // end function earnings

34

35 // print SalariedEmployee's information

36 void SalariedEmployee::print() const

37 {

38     cout << "salaried employee: ";

39     Employee::print(); // reuse abstract base-class print function

40     cout << "\nweekly salary: " << getWeeklySalary();

41 } // end function print

```

**图 13.16 | SalariedEmployee 类实现文件。（第 2 部分，共 2 部分。）**

类 `SalariedEmployee` 的 `print` 函数（图 13.16 第 36–41 行）重写 `Employee` 的 `print` 函数。如果类 `SalariedEmployee` 没有重写 `print`，`SalariedEmployee` 将继承 `Employee` 版本的 `print`。在这种情况下，`SalariedEmployee` 的 `print` 函数将仅返回员工的 full name 和 social security number，这不足以代表 `SalariedEmployee`。为了打印 `SalariedEmployee` 的完整信息，派生类的 `print` 函数输出 "salaried employee: " 后跟通过使用作用域解析运算符调用基类的 `print` 函数打印的基类 `Employee` 特定信息（即 first name、last name 和 social security number）（第 39 行）——这是一个很好的代码重用示例。`SalariedEmployee` 的 `print` 函数产生的输出包含通过调用类的 `getWeeklySalary` 函数获得的员工的 weekly salary。

## 13.6.3 创建具体派生类 HourlyEmployee

类 `HourlyEmployee`（图 13.17–13.18）也派生自类 `Employee`（图 13.17 第 8 行）。公共成员函数包括一个构造函数（第 11–12 行），该构造函数以 first name、last name、social security number、hourly wage 和工作小时数作为参数；设置数据成员 `wage` 和 `hours` 的 set 函数（分别第 14 行和第 17 行）；返回 `wage` 和 `hours` 值的 get 函数（分别第 15 行和第 18 行）；一个计算 `HourlyEmployee` earnings 的虚函数 `earnings`（第 21 行）和一个输出员工类型，即 "hourly employee: " 和员工特定信息的虚函数 `print`（第 22 行）。

```cpp
// Fig. 13.17: HourlyEmployee.h
// HourlyEmployee class definition.
#ifndef HOURLY_H
#define HOURLY_H

#include "Employee.h" // Employee class definition

class HourlyEmployee : public Employee
{
public:
    HourlyEmployee( const string &, const string &,
        const string &, double = 0.0, double = 0.0 );

    void setWage( double ); // set hourly wage
    double getWage() const; // return hourly wage

    void setHours( double ); // set hours worked
    double getHours() const; // return hours worked

    // keyword virtual signals intent to override
    virtual double earnings() const; // calculate earnings
    virtual void print() const; // print HourlyEmployee object
private:
    double wage; // wage per hour
    double hours; // hours worked for week
}; // end class HourlyEmployee

#endif // HOURLY_H
```

**图 13.17 | HourlyEmployee 类头文件。**

```cpp
// Fig. 13.18: HourlyEmployee.cpp
// HourlyEmployee class member-function definitions.
#include <iostream>
using std::cout;

#include "HourlyEmployee.h" // HourlyEmployee class definition

// constructor
HourlyEmployee::HourlyEmployee( const string &first, const string &last,
    const string &ssn, double hourlyWage, double hoursWorked )
    : Employee( first, last, ssn )
{
    setWage( hourlyWage ); // validate hourly wage
    setHours( hoursWorked ); // validate hours worked
} // end HourlyEmployee constructor

// set wage
void HourlyEmployee::setWage( double hourlyWage )
{
    wage = ( hourlyWage < 0.0 ? 0.0 : hourlyWage );
} // end function setWage
```

**图 13.18 | HourlyEmployee 类实现文件。（第 1 部分，共 2 部分。）**

```cpp
// return wage

double HourlyEmployee::getWage() const

{

   return wage;

} // end function getWage

// set hours worked

void HourlyEmployee::setHours( double hoursWorked )

{

   hours = ( ( ( hoursWorked >= 0.0 ) && ( hoursWorked <= 168.0 ) ) ?

      hoursWorked : 0.0 );

} // end function setHours

// return hours worked

double HourlyEmployee::getHours() const

{

   return hours;

} // end function getHours

// calculate earnings;

// override pure virtual function earnings in Employee

double HourlyEmployee::earnings() const

{

   if ( getHours() <= 40 ) // no overtime

      return getWage() * getHours();

   else

      return 40 * getWage() + ( ( getHours() - 40 ) * getWage() * 1.5 );

} // end function earnings

// print HourlyEmployee's information

void HourlyEmployee::print() const

{

   cout << "hourly employee: ";

   Employee::print(); // code reuse

   cout << "\nhourly wage: " << getWage() <<

      "; hours worked: " << getHours();

} // end function print
```

图 13.18 包含了 `HourlyEmployee` 类的成员函数实现。第18–21行和第30–34行分别定义了为数据成员 `wage` 和 `hours` 赋予新值的 set 函数。`setWage` 函数（第18–21行）确保 `wage` 非负，`setHours` 函数（第30–34行）确保数据成员 `hours` 在 0 到 168（一周的总小时数）之间。`HourlyEmployee` 类的 get 函数实现在第24–27行和第37–40行。我们没有将这些函数声明为 `virtual`，因此从 `HourlyEmployee` 类派生的类不能覆盖它们（尽管派生类当然可以重新定义它们）。注意，`HourlyEmployee` 构造函数与 `SalariedEmployee` 构造函数类似，将名、姓和社会安全号码传给基类 `Employee` 构造函数（第11行），以初始化继承自基类中声明的私有数据成员。此外，`HourlyEmployee` 的 `print` 函数调用基类函数 `print`（第56行）来输出 `Employee` 特有的信息（即名、姓和社会安全号码）——这是另一个很好的代码复用示例。

## 13.6.4 创建具体派生类 CommissionEmployee

类 `CommissionEmployee`（图13.19–13.20）派生自类 `Employee`（图13.19的第8行）。其成员函数实现（图13.20）包括一个构造函数（第9–15行），该构造函数接受名、姓、社会安全号码、销售额和佣金率；set 函数（第18–21行和第30–33行）分别给数据成员 `commissionRate` 和 `grossSales` 赋新值；get 函数（第24–27行和第36–39行）检索这些数据成员的值；函数 `earnings`（第43–46行）计算 `CommissionEmployee` 的工资；函数 `print`（第49–55行）输出员工类型，即 "commission employee: " 以及员工特有信息。`CommissionEmployee` 的构造函数也将名、姓和社会安全号码传给 `Employee` 构造函数（第11行），以初始化 `Employee` 的私有数据成员。

```cpp
// Fig. 13.19: CommissionEmployee.h

// CommissionEmployee class derived from Employee.

#ifndef COMMISSION_H

#define COMMISSION_H

#include "Employee.h" // Employee class definition

class CommissionEmployee : public Employee

{

public:

    CommissionEmployee( const string &, const string &,

       const string &, double = 0.0, double = 0.0 );

    void setCommissionRate( double ); // set commission rate

    double getCommissionRate() const;  // return commission rate

    void setGrossSales( double ); // set gross sales amount

    double getGrossSales() const; // return gross sales amount

    // keyword virtual signals intent to override

    virtual double earnings() const; // calculate earnings

    virtual void print() const; // print CommissionEmployee object

private:

    double grossSales; // gross weekly sales

    double commissionRate; // commission percentage

}; // end class CommissionEmployee

#endif // COMMISSION_H
```

**图 13.19 | CommissionEmployee 类头文件。**

```cpp
// Fig. 13.20: CommissionEmployee.cpp

// CommissionEmployee class member-function definitions.

#include <iostream>
```

