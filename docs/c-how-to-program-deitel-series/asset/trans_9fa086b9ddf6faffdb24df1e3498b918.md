
```cpp
#include <string> // C++ standard string class

class CommissionEmployee
{
public:
   CommissionEmployee( const std::string &, const std::string &,
      const std::string &, double = 0.0, double = 0.0 );

   void setFirstName( const std::string & ); // set first name
   std::string getFirstName() const; // return first name

   void setLastName( const std::string & ); // set last name
   std::string getLastName() const; // return last name

   void setSocialSecurityNumber( const std::string & ); // set SSN
   std::string getSocialSecurityNumber() const; // return SSN

   void setGrossSales( double ); // set gross sales amount
   double getGrossSales() const; // return gross sales amount

   void setCommissionRate( double ); // set commission rate
   double getCommissionRate() const; // return commission rate

   double earnings() const; // calculate earnings
   void print() const; // print CommissionEmployee object
protected:
   std::string firstName;
   std::string lastName;
   std::string socialSecurityNumber;
   double grossSales; // gross weekly sales
   double commissionRate; // commission percentage
}; // end class CommissionEmployee

#endif
```

**图 11.12 |** *CommissionEmployee* 类定义，声明了受保护的数据，以允许派生类访问。（第 2 部分，共 2 部分。）

## BasePlusCommissionEmployee 类

图 11.10–11.11 中 BasePlusCommissionEmployee 类的定义保持*不变*，因此我们这里不再展示。现在 BasePlusCommissionEmployee 继承自更新后的 CommissionEmployee 类（图 11.12），BasePlusCommissionEmployee 对象可以访问在 CommissionEmployee 类中声明为 protected 的继承数据成员（即数据成员 firstName、lastName、socialSecurityNumber、grossSales 和 commissionRate）。因此，当编译器编译图 11.11 中 BasePlusCommissionEmployee 的 earnings 和 print 成员函数定义（分别为第 34–38 行和第 41–49 行）时，不会产生错误。这显示了派生类被授予访问基类 protected 数据成员的特殊权限。派生类的对象还可以访问该派生类的*任何**间接*基类中的 protected 成员。

BasePlusCommissionEmployee 类不继承 CommissionEmployee 类的构造函数。但是，BasePlusCommissionEmployee 类的构造函数（图 11.11，第 9–16 行）通过成员初始化列表显式调用 CommissionEmployee 类的构造函数。

直接操作数据成员的 get 和 set 成员函数的实现将需要更改。这些更改仅发生在基类内部——不需要对派生类进行任何更改。像这样将更改的影响局部化是一种良好的软件工程实践。

```cpp
// Fig. 11.14: CommissionEmployee.cpp
// Class CommissionEmployee member-function definitions.
#include <iostream>
#include <stdexcept>
#include "CommissionEmployee.h" // CommissionEmployee class definition
using namespace std;

// constructor
CommissionEmployee::CommissionEmployee(
   const string &first, const string &last, const string &ssn,
   double sales, double rate )
   : firstName( first ), lastName( last ), socialSecurityNumber( ssn )
{
   setGrossSales( sales ); // validate and store gross sales
   setCommissionRate( rate ); // validate and store commission rate
} // end CommissionEmployee constructor

// set first name
void CommissionEmployee::setFirstName( const string &first )
{
   firstName = first; // should validate
} // end function setFirstName

// return first name
string CommissionEmployee::getFirstName() const
{
   return firstName;
} // end function getFirstName

// set last name
void CommissionEmployee::setLastName( const string &last )
{
   lastName = last; // should validate
} // end function setLastName

// return last name
string CommissionEmployee::getLastName() const
{
   return lastName;
} // end function getLastName

// set social security number
void CommissionEmployee::setSocialSecurityNumber( const string &ssn )
{
   socialSecurityNumber = ssn; // should validate
} // end function setSocialSecurityNumber
```

图 11.14 | CommissionEmployee 类实现文件：CommissionEmployee 类使用成员函数操作其私有数据。（第 1 部分，共 2 部分。）

```cpp
// return social security number
string CommissionEmployee::getSocialSecurityNumber() const
{
    return socialSecurityNumber;
} // end function getSocialSecurityNumber

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

// calculate earnings
double CommissionEmployee::earnings() const
{
    return getCommissionRate() * getGrossSales();
} // end function earnings

// print CommissionEmployee object
void CommissionEmployee::print() const
{
    cout << "commission employee: "
         << getFirstName() << " " << getLastName()
         << "\nsocial security number: " << getSocialSecurityNumber()
         << "\ngross sales: " << getGrossSales()
         << "\ncommission rate: " << getCommissionRate();
} // end function print
```

图 11.14 | CommissionEmployee 类实现文件：CommissionEmployee 类使用成员函数操作其私有数据。（第 2 部分，共 2 部分。）

![](img/b42ba5cd262b1358d16610173f975e4d_542_0.png)

### 性能提示 11.2

> 使用成员函数访问数据成员的值可能比直接访问数据稍慢。然而，当今的优化编译器经过精心设计，可以隐式执行许多优化（例如内联以及 get 和成员函数调用）。你应该编写遵循良好软件工程原则的代码，把优化留给编译器。一条好的规则是：“不要猜测编译器的意图。”

### 对 BasePlusCommissionEmployee 类成员函数定义的更改

BasePlusCommissionEmployee 类继承 CommissionEmployee 的公有成员函数，并可以通过继承的成员函数访问基类的私有成员。该类的头文件与图 11.10 相比保持不变。该类的成员函数实现有几处更改（图 11.15），这些更改使其区别于该类的旧版本（图 11.10–11.11）。成员函数 earnings（图 11.15，第 34–37 行）和 print（第 40–48 行）都调用成员函数 getBaseSalary 来获取基本工资值，而不是直接访问 baseSalary。这使 earnings 和 print 免受数据成员 baseSalary 实现可能发生的变化的影响。例如，如果我们决定重命名数据成员 baseSalary 或更改其类型，只需要更改成员函数 setBaseSalary 和 getBaseSalary。

```cpp
// Fig. 11.15: BasePlusCommissionEmployee.cpp
// Class BasePlusCommissionEmployee member-function definitions.
#include <iostream>
#include <stdexcept>
#include "BasePlusCommissionEmployee.h"
using namespace std;

// constructor
BasePlusCommissionEmployee::BasePlusCommissionEmployee(
   const string &first, const string &last, const string &ssn,
   double sales, double rate, double salary )
   // explicitly call base-class constructor
   : CommissionEmployee( first, last, ssn, sales, rate )
{
   setBaseSalary( salary ); // validate and store base salary
} // end BasePlusCommissionEmployee constructor

// set base salary
void BasePlusCommissionEmployee::setBaseSalary( double salary )
{
   if ( salary >= 0.0 )
      baseSalary = salary;
   else
      throw invalid_argument( "Salary must be >= 0.0" );
} // end function setBaseSalary

// return base salary
double BasePlusCommissionEmployee::getBaseSalary() const
{
```

**图 11.15** | 继承自 CommissionEmployee 类但不能直接访问该类私有数据的 BasePlusCommissionEmployee 类。（第 1 部分，共 2 部分。）

