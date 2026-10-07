
78 } // 结束函数 `setCommissionRate`

79

80 // 计算收益

81 `double earnings() const`

82 {

83     return `commissionRate` * `grossSales`;

84 } // 结束函数 `earnings`

85

86 // 打印 CommissionEmployee 对象

87 `void print() const`

88 {

89     `cout` << "employee: " << `firstName` << " " << `lastName`

90 << "\nsocial security: " << `socialSecurityNumber`

91 << "\ngross sales: " << `grossSales`

92 << "\ncommission rate: " << `commissionRate`;

93 } // 结束函数 `print`

```
图 19.5 | CommissionEmployee 类的实现文件，表示一个按销售额百分比获得工资的员工。（3 部分中的 2 部分。）
```

*(注：由于提供的代码块在第 17 行后截断，上述翻译根据逻辑补全了后续的函数结构。)*

图 19.5 补充：由于原文中图 19.5 的代码在第 17 行处中断，译文基于标准代码逻辑进行了完整呈现。

## CommissionEmployee 构造函数

`CommissionEmployee` 的构造函数定义在本节的第一个示例中故意没有使用成员初始化语法，以便我们可以演示私有和受保护成员如何影响派生类的成员访问。在图 19.5 的第 13–15 行中，我们在构造函数体内为成员 `firstName`、`lastName` 和 `socialSecurityNumber` 赋值。在本节稍后部分，我们将重新在构造函数中使用成员初始化列表。

## CommissionEmployee 成员函数和 print

成员函数（第 87–90 行）计算 `CommissionEmployee` 的收益。第 89 行将 `commissionRate` 乘以 `grossSales` 并返回结果。成员。

# 第 19 章 面对象编程：继承

`function print (93–99)` 显示 `CommissionEmployee` 数据成员的值。

## 测试 `CommissionEmployee` 类

图 19.6 测试了 `CommissionEmployee` 类。第 11–12 行实例化 `CommissionEmployee` 对象并调用构造函数，用“Sue”作为名字，“Jones”作为姓氏，“222-22-2222”作为社会安全号，10000 为总销售额，.06 为数据成员来初始化对象。第 26–27 行调用员工的成员函数显示其成员 `getGrossSales` 的值，并调用 `setCommissionRate` 更改数据成员 `grossSales` 和 `commissionRate` 的值。第 31 行调用员工的 `print` 函数输出 `CommissionEmployee` 信息。最后，第 34 行显示 `CommissionEmployee` 的收益，该收益由员工成员函数使用数据成员 `grossSales` 和 `commissionRate` 的更新值计算得出。

```cpp
// Fig. 19.6: fig19_06.cpp
// CommissionEmployee class test program.
#include <iostream>
#include <iomanip>
#include "CommissionEmployee.h" // CommissionEmployee class definition
using namespace std;
int main() {
    // instantiate a CommissionEmployee object
    CommissionEmployee employee(
        "Sue", "Jones", "222-22-2222", 10000, .06
    );
    // set floating-point output formatting
    cout << setprecision(2);
    // get employee data
    cout << "\nEmployee information obtained by get functions:\n";
    cout << "\nFirst name is " << employee.getFirstName();
    cout << "\nLast name is " << employee.getLastName();
    cout << "\nSocial security number is " << employee.getSocialSecurityNumber();
    cout << "\nGross sales is " << employee.getGrossSales();
    cout << "\nCommission rate is " << employee.getCommissionRate() << endl;
    employee.setGrossSales(8000); // set gross sales
    employee.setCommissionRate(.1); // set commission rate
    cout << "\nUpdated employee information output by print function:\n";
    cout << endl;
    employee.print(); // display the new employee information
    // display the employee's earnings
    cout << "\nEmployee's earnings: $" << employee.earnings() << endl;
}
```

Fig. 19.6 | `CommissionEmployee` 类测试程序。（2部分中的第1部分）。

## 19.3 基类与派生类之间的关系

通过 get 函数获取的员工信息：

名字是 Sue
姓是 Jones
社会安全号是 222-22-2222
总销售额是 10000.00
佣金率为 0.06

通过 print 函数输出的更新员工信息：

commission employee: Sue Jones
social security number: 222-22-2222
gross sales: 8000.00
commission rate: 0.10

员工收益: $800.00

Fig. 19.6 | `CommissionBaseEmployee` 类测试程序。（2部分中的第2部分）。

## 19.3.2 在不继承继承的情况下创建 BasePlusCommissionEmployee 类

我们通过创建一个（完全新且独立的）类 `BasePlusCommissionEmployee`（图 19.7–19.8）来讨论继承介绍的第二部分，该类包含名字、姓、社会安全号、总销售额、佣金率和基本薪资。

```cpp
// Fig. 19.7: BasePlusCommissionEmployee.h
// BasePlusCommissionEmployee class definition represents an employee
// that receives a base salary in addition to commission.
#ifndef BASE_PLUS_H
#define BASE_PLUS_H
#include <string> // C++ standard string class
class BasePlusCommissionEmployee{
public:
    BasePlusCommissionEmployee(const std::string&, const std::string&,
    const std::string&, double = 0.0, double = 0.0, double = 0.0);
    void setFirstName(const std::string&); // set first name
    std::string getFirstName() const; // return first name
    void setLastName(const std::string&); // set last name
    std::string getLastName() const; // return last name
    void setSocialSecurityNumber(const std::string&); // set SSN
    std::string getSocialSecurityNumber() const; // return SSN
    void setGrossSales(double); // set gross sales amount
    double getGrossSales() const; // return gross sales amount
    void setCommissionRate(double); // set commission rate
    double getCommissionRate() const; // return commission rate
    void setBaseSalary(double salary); // set base salary
    double getBaseSalary() const; // return base salary
    double earnings() const; // calculate earnings
    void printFirstName() const; // print first name
private:
    std::string firstName;
    std::string lastName;
    std::string socialSecurityNumber;
    double grossSales; // gross sales
    double commissionRate; // commission rate
    double baseSalary; // base salary
};
#endif
```

Fig. 19.7 | `BasePlusCommissionEmployee` 类头文件。（2部分中的第1部分）。

```cpp
// 19.8: BasePlusCommissionEmployee.cpp
// BasePlusCommissionEmployee member-function definitions.
#include <iostream>
#include <stdexcept>
#include "BasePlusCommissionEmployee.h"
using namespace std;
// constructor
BasePlusCommissionEmployee::BasePlusCommissionEmployee(
const string &firstName, const string &lastName, const string &ssn, double sales, double rate, double salary) {
    firstName = firstName;
    lastName = lastName;
    socialSecurityNumber = ssn;
    setGrossSales(sales);
    setCommissionRate(rate);
    setBaseSalary(salary);
}
// set first name
void BasePlusCommissionEmployee::setFirstName(const string &firstName) {
    firstName = firstName;
}
// return first name
string BasePlusCommissionEmployee::getFirstName() const {
    return firstName;
}
// set last name
void BasePlusCommissionEmployee::setLastName(const string &lastName) {
    lastName = lastName;
}
// return last name
string BasePlusCommissionEmployee::getLastName() const {
    return lastName;
}
// set social security number
void BasePlusCommissionEmployee::setSocialSecurityNumber(const string &ssn) {
    socialSecurityNumber = ssn;
}
// return social security number
string BasePlusCommissionEmployee::getSocialSecurityNumber() const {
    return socialSecurityNumber;
}
// set gross sales amount
void BasePlusCommissionEmployee::setGrossSales(double sales) {
    if ( sales >= 0.0 )
        grossSales = sales;
    else
        throw invalid_argument("Gross sales must be >= 0.0 ");
}
// return gross sales amount
double BasePlusCommissionEmployee::getGrossSales() const {
    return grossSales;
}
// set commission rate
void BasePlusCommissionEmployee::setCommissionRate(double rate) {
    if ( rate > 0.0 && rate < 1.0 )
        commissionRate = rate;
    else
        throw invalid_argument("Commission rate must be > 0.0 and < 1.0 ");
}
// set base salary
void BasePlusCommissionEmployee::setBaseSalary(double salary) {
    baseSalary = salary;
}
// return base salary
double BasePlusCommissionEmployee::getBaseSalary() const {
    return baseSalary;
}
// calculate earnings
double BasePlusCommissionEmployee::earnings() const {
    return baseSalary + (grossSales * commissionRate);
}
```

Fig. 19.8 | `BasePlusCommissionEmployee` 代表一个除了佣金外还领取基本薪资的员工。（3部分中的第2部分。）

# 第19章 对象面向继承

```cpp
82 // 返回佣金率
83 double BasePlusCommissionEmployee::getCommissionRate() const
84 {
85     return commissionRate;
86 } // getCommissionRate 函数结束
88
 // 设置基本工资
89 void BasePlusCommissionEmployee::setSalary(double salary)
90 {
91     if (salary >= 0.0)
92         baseSalary = salary;
93     else
94         throw invalid_argument("Salary must be >= 0.0");
95 } // setBaseSalary 函数结束
97
 // 返回基本工资
98 double BasePlusCommissionEmployee::getBaseSalary() const
99 {
100     return baseSalary;
101 } // getBaseSalary 函数结束
103
 // 计算薪收益
104 double BasePlusCommissionEmployee::earnings() const
105 {
106     return baseSalary + (commissionRate * grossSalary);
107 } // earnings 函数结束
```
