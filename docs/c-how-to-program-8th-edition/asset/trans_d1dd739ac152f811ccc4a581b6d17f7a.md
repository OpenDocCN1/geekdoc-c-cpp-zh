

### SalariedEmployee 类成员函数定义

图 13.12 包含了 SalariedEmployee 的成员函数实现。该类的构造函数将名字、姓氏和社会安全号码传递给 Employee 构造函数（第 10 行），以初始化从基类继承但无法在派生类中直接访问的私有数据成员。函数 earnings（第 32–35 行）重写了 Employee 中的纯虚函数 earnings，提供了一个具体实现，返回 SalariedEmployee 的周薪。如果我们不实现 earnings，那么 SalariedEmployee 类将是抽象类，任何尝试实例化该类的对象都会导致编译错误（当然，这里我们希望 SalariedEmployee 是一个具体类）。在 SalariedEmployee 类的头文件中，我们将成员函数 earnings 和 print 声明为 virtual（图 13.11 第 18–19 行）——实际上，在这些成员函数前加上 virtual 关键字是多余的。我们在基类 Employee 中已经将它们定义为 virtual，因此它们在类层次结构中始终是虚函数。在层次结构的每一层显式声明这样的函数为 virtual 可以提高清晰度。不将 earnings 声明为纯虚函数表明我们打算在这个具体类中提供实现。

```cpp
// Fig. 13.12: SalariedEmployee.cpp
// SalariedEmployee class member-function definitions.
#include <iostream>
#include "SalariedEmployee.h" // SalariedEmployee class definition
using namespace std;

// constructor
SalariedEmployee::SalariedEmployee( const string &first,
    const string &last, const string &ssn, double salary )
    : Employee( first, last, ssn )
{
    setWeeklySalary( salary );
} // end SalariedEmployee constructor

// set salary
void SalariedEmployee::setWeeklySalary( double salary )
{
    if ( salary >= 0.0 )
        weeklySalary = salary;
    else
        throw invalid_argument( "Weekly salary must be >= 0.0" );
} // end function setWeeklySalary

// return salary
double SalariedEmployee::getWeeklySalary() const
{
    return weeklySalary;
} // end function getWeeklySalary

// calculate earnings;
// override pure virtual function earnings in Employee
double SalariedEmployee::earnings() const
{
    return getWeeklySalary();
} // end function earnings

// print SalariedEmployee's information
void SalariedEmployee::print() const
{
    cout << "salaried employee: ";
    Employee::print(); // abstract base-class print function
    cout << "weekly salary: " << getWeeklySalary();
} // end function print
```

**图 13.12** | SalariedEmployee 类实现文件。（共 2 部分，此为第 1 和 2 部分。）

SalariedEmployee 类的函数 print（图 13.12 第 38–43 行）重写了 Employee 的 print 函数。如果 SalariedEmployee 类没有重写 print，那么 SalariedEmployee 将继承 Employee 版本的 print。在这种情况下，SalariedEmployee 的 print 函数只会返回雇员的全名和社会安全号码，这不足以表示一个 SalariedEmployee。为了打印 SalariedEmployee 的完整信息，派生类的 print 函数输出“salaried employee:”，后跟通过使用作用域解析运算符（第 41 行）调用基类的 print 函数所打印的基类 Employee 特有信息（即名字、姓氏和社会安全号码）——这是一个很好的代码复用示例。如果没有作用域解析运算符，print 调用将导致无限递归。SalariedEmployee 的 print 函数产生的输出包含通过调用该类的 getWeeklySalary 函数获得的雇员周薪。

### 13.6.3 创建具体派生类 CommissionEmployee

类 CommissionEmployee（图 13.13–13.14）派生自 Employee（图 13.13 第 8 行）。其成员函数实现（图 13.14）包括一个构造函数（第 8–14 行），该构造函数接受名字、姓氏、社会安全号码、销售额和佣金率；set 函数（第 17–23 行和第 32–38 行）分别用于为数据成员 commissionRate 和 grossSales 赋值；get 函数（第 26–29 行和第 41–44 行）用于获取这些值；函数 earnings（第 47–50 行）用于计算 CommissionEmployee 的收入；函数 print（第 53–59 行）用于输出雇员类型，即“commission employee:”以及雇员特有信息。构造函数将名字、姓氏和社会安全号码传递给 Employee 构造函数（第 10 行），以初始化 Employee 的私有数据成员。函数 print 调用基类的 print 函数（第 56 行）来显示 Employee 特有的信息。

```cpp
// Fig. 13.13: CommissionEmployee.h
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
   double getCommissionRate() const; // return commission rate

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

**图 13.13** | CommissionEmployee 类头文件。（共 2 部分，此为第 1 和 2 部分。）

```cpp
// Fig. 13.14: CommissionEmployee.cpp
// CommissionEmployee class member-function definitions.
#include <iostream>
#include "CommissionEmployee.h" // CommissionEmployee class definition
using namespace std;

// constructor
CommissionEmployee::CommissionEmployee( const string &first,
   const string &last, const string &ssn, double sales, double rate )
   : Employee( first, last, ssn )
{
   setGrossSales( sales );
   setCommissionRate( rate );
} // end CommissionEmployee constructor

// set gross sales amount
void CommissionEmployee::setGrossSales( double sales )
{
   if ( sales >= 0.0 )
      grossSales = sales;
   else
      throw invalid_argument( "Gross sales must be >= 0.0" );
} // end function setGrossSales

// return gross sales amount
double CommissionEmployee::getGrossSales() const
{
   return grossSales;
} // end function getGrossSales

// set commission rate
void CommissionEmployee::setCommissionRate( double rate )
{
   if ( rate > 0.0 && rate < 1.0 )
      commissionRate = rate;
   else
      throw invalid_argument( "Commission rate must be > 0.0 and < 1.0" );
} // end function setCommissionRate

// return commission rate
double CommissionEmployee::getCommissionRate() const
{
   return commissionRate;
} // end function getCommissionRate

// calculate earnings; override pure virtual function earnings in Employee
double CommissionEmployee::earnings() const
{
   return getCommissionRate() * getGrossSales();
} // end function earnings

// print CommissionEmployee's information
void CommissionEmployee::print() const
{
   cout << "commission employee: ";
   Employee::print(); // code reuse
   cout << "\ngross sales: " << getGrossSales()
        << "\ncommission rate: " << getCommissionRate();
} // end function print
```

**图 13.14** | CommissionEmployee 类实现文件。（共 2 部分，此为第 1 和 2 部分。）

### 13.6.4 创建间接具体派生类 BasePlusCommissionEmployee

类 BasePlusCommissionEmployee（图 13.15–13.16）直接继承自类 CommissionEmployee（图 13.15 第 8 行），因此是 Employee 的间接派生类。BasePlusCommissionEmployee 类的成员函数实现包括一个构造函数（图 13.16 第 8–14 行），该构造函数接受名字、姓氏、社会安全号码、销售额、佣金率和基本工资作为参数。然后它将名字、姓氏、社会安全号码、销售额和佣金率传递给 CommissionEmployee 构造函数（第 11 行），以初始化继承的成员。BasePlusCommissionEmployee 还包含一个 set 函数（第 17–23 行）用于为数据成员 baseSalary 赋值，以及一个 get 函数（第 26–29 行）用于返回 baseSalary 的值。函数 earnings（第 33–36 行）计算 BasePlusCommissionEmployee 的收入。函数 earnings 中的第 35 行调用基类 CommissionEmployee 的 earnings 函数来计算雇员收入中基于佣金的部分。这是另一个很好的代码复用示例。BasePlusCommissionEmployee 的 print 函数（第 39–44 行）输出“base-salaried”，后接基类 CommissionEmployee 的

