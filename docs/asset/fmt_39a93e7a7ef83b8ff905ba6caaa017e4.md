
`double weeklySalary; // salary per week`

};

#endif // `SALARIED_H`

```
图 12.11 | SalariedEmployee 类头文件。
```

## SalariedEmployee 类成员函数定义

图12.12 包含 `SalariedEmployee` 的成员函数定义。该类的构造函数将名字、姓氏和社会安全号码传递给 `Employee`（第12行）以初始化从基类继承的私有数据成员，但在派生类中不能直接访问。函数 `earnings`（第30行）覆盖 `Employee` 中的虚函数 `earnings`，提供返回 `SalariedEmployee` 薪水的具体实现。如果我们没有定义 `earnings`，`SalariedEmployee` 将是一个抽象类，尝试实例化 `SalariedEmployee` 对象将导致编译错误。在 `SalariedEmployee` 的头文件中，我们将成员 `earnings` 和 `toString` 定义为（图12.11 第19-20行）——实际上，在这些成员函数前放置 `virtual` 关键字是多余的。我们已在基类 `Employee` 中将它们定义为 `virtual`，因此它们在整个类层次结构中保持为虚函数。在层次结构的每个级别上显式声明此类 `virtual` 有助于提高程序清晰度。不将 `earnings` 声明为纯虚表示我们打算在此类中提供实现。

# 12.7 案例研究：使用多态的工资系统 595

```
// Fig. 12.12: SalariedEmployee.cpp

// SalariedEmployee class member-function definitions.

#include <iomanip>

#include <stdexcept>

#include <iostream>

#include "SalariedEmployee.h" // SalariedEmployee class definition

using namespace std;

// constructor

SalariedEmployee::SalariedEmployee(const string& first,

    const string& last, const string& ssn, double salary)

    : Employee(first, last, ssn) {

    setWeeklySalary(salary);

}

// set salary

void SalariedEmployee::setWeeklySalary(double salary) {

    if (salary < 0.0)

        throw invalid_argument("Weekly salary must be >= 0.0");

    weeklySalary = salary;

}

// return salary

double SalariedEmployee::getWeeklySalary() const { return weeklySalary; }

// calculate earnings

// override pure virtual function earnings in Employee

double SalariedEmployee::earnings() const { return getWeeklySalary(); }

// return a string representation of SalariedEmployee's information

string SalariedEmployee::toString() const {

    ostringstream output;

    output << fixed << setprecision(2);

    output << "Salaried employee: " << Employee::toString(); // reuse base-class function

    output << "\nweekly salary: " << getWeeklySalary();

    return output.str();

}
```

图 12.12 | `SalariedEmployee` 类实现文件。

类 `SalariedEmployee` 的 `toString` 函数（图12.12 第33-40行）覆盖了 `Employee` 的 `toString` 函数。如果类 `SalariedEmployee` 没有覆盖 `toString`，`SalariedEmployee` 将继承 `Employee` 版本的 `toString`。这将返回全名和社会安全号码，这不足以代表 `SalariedEmployee`。为了创建 `SalariedEmployee` 完整信息的字符串表示，派生类的 `toString` 函数返回 `"salaried employee: "` 后跟基类特定信息（即名字、姓氏和社会安全号码），该信息是通过使用作用域解析运算符调用基类的 `toString` 函数获得的

## 第12章 面向对象编程：多态

(line 37)。如果没有 `Employee::`，`toString` 将会导致无限递归。`SalariedEmployee::toString` 函数产生的字符串也包含通过重写类的 `weekly` 函数获得的员工周薪。

### 12.7.3 创建派生类 CommissionEmployee

`CommissionEmployee`（图 12.13-12.14）派生自 `Employee`（图 12，第 9 行）。图 12.14 中的成员函数实现包括一个构造函数（第 10–15 行），它接收名字、姓氏、社会安全号码、销售额和佣金率；设置函数（第 18–24 行和第 30–36 行）用于为成员 `grossSales` 和 `commissionRate` 分配新值；获取函数（第 27 行和第 39–41 行）用于检索其值；函数 `earnings`（第 44–46 行）用于计算 `Employee` 的收入；以及函数 `toString`（第 49–50 行）用于输出员工的类型，即 `"commission employee:"` 以及员工特定信息。构造函数将名字、姓氏和社会安全号码传递给 `Employee` 构造函数（第 12 行）以初始化 `Employee` 私有成员。function `toString`(line 52) 用于获取 `Employee` 特定信息的字符串表示。

```
// Fig. 12.13: CommissionEmployee.h

// CommissionEmployee class derived from Employee.

#ifndef COMMISSION_H

#define COMMISSION_H

#include <string> // C++ standard string class

#include "Employee.h" // Employee class definition

class CommissionEmployee : public Employee {

public:

CommissionEmployee(const std::string&, const std::string&,

const std::string&, double = 0.0);

virtual ~CommissionEmployee() = default; // virtual destructor

void setCommissionRate(double); // set commission rate

double getCommissionRate() const; // return rate

void setGrossSales(double); // set gross sales amount

double getGrossSales() const; // return gross sales amount

// keyword double earnings() const override; // calculate earnings

virtual std::string toString() const override; // string representation

private:

double grossSales; // gross weekly sales

double commissionRate; // commission percentage

};

#endif // COMMISSION_H
```

图 12.13 | `CommissionEmployee` 类头文件。

### 12.7 案例研究：使用多态的工资系统 597

```
// Fig.12.14: CommissionEmployee.cpp

// CommissionEmployee class member-function definitions.

#include <iostream>

#include <stdexcept>

#include <sstream>

#include "CommissionEmployee.h" // CommissionEmployee class definition

namespace std;

// constructor

CommissionEmployee::CommissionEmployee(const string& first,

    const string& last, const string& ssn, double sales, double rate)

    : Employee(first, last, ssn) {

    setGrossSales(sales);

    setCommissionRate(rate);

}

// set gross sales amount

void CommissionEmployee::setGrossSales(double sales) {

    if (sales < 0.0) {

        throw invalid_argument("Gross sales must be >= 0.0");

    }

    grossSales = sales;

}

double CommissionEmployee::getGrossSales() const { return grossSales; }

// set commission rate

void CommissionEmployee::setCommissionRate(double rate) {

    if (rate < 0.0 || rate > 1.0) {

        throw invalid_argument("Commission rate must be > 0.0 and < 1.0");

    }

    commissionRate = rate;

}

// return commission rate

double CommissionEmployee::getCommissionRate() const {

    return commissionRate;

}

// calculate earnings; override pure virtual earnings in Employee

double CommissionEmployee::earnings() const {

    return getCommissionRate() * getGrossSales();

}

// return a string representation of CommissionEmployee's information

string CommissionEmployee::toString() const {

    ostringstream output;

    output << fixed << setprecision(2);

}
```

图 12.14 | `CommissionEmployee` 类实现文件。（第 1 部分，共 2 部分。）

## 598 第12章 面向对象编程：多态

| 52 | output << "commission employee: " << Employee::toString() |
| 53 | << "\ngross sales: " << getGrossSales() |
| 54 | << "; commission rate: " << getCommissionRate(); |
| 55 | return output.str(); |

图 12.14 | `CommissionEmployee` 类实现。（第 2 部分，共 2 部分。）

### 12.7.4 创建直接派生类 BasePlusCommissionEmployee

`BasePlusCommissionEmployee`（图 12.15–12.16）直接继承自类 `CommissionEmployee`（12.15 的第 9 行），因此是类 `Employee` 的派生类。图 12.16 中 `BasePlusCommissionEmployee` 的成员函数实现包括一个构造函数（第 10-15 行），它接收名字、姓氏、社会安全号码、销售额、佣金率和薪水作为参数。它将名字、姓氏、销售额和佣金率传递给 `CommissionEmployee` 构造函数（第 13 行）以初始化继承的成员。`BasePlusCommissionEmployee` 还包含一个设置函数（第 18–24 行）用于为成员 `baseSalary` 分配值，以及一个获取函数（第 27–29 行）用于返回 `baseSalary` 的值。函数 `earnings`（第 33–35 行）计算 `BasePlusCommissionEmployee` 的收入。第 34 行的函数调用类 `Employee` 的 `earnings` 以计算员工收入中基于佣金的部分。`BasePlusCommissionEmployee` 的 `toString` 函数（第 38–44 行）返回 `"base-salaried"`，随后返回基类 `CommissionEmployee` 的 `toString` 函数的结果，然后是基本工资。 resulting 字符串以 `"base-salaried commission employee: "` 开头，后跟 `BasePlusCommissionEmployee` 信息的返回。回想一下，`CommissionEmployee` 的 `toString` 通过调用其基类（即 `Employee`）的 `toString` 函数来获取包含员工名字、姓氏和社会安全号码的字符串。`BasePlusCommissionEmployee` 的 `toString` 启动了一系列跨越 `Employee` 层次结构三个层级的函数调用。

```
// Fig. 12.15: BasePlusCommissionEmployee.h

// BasePlusCommissionEmployee class derived from CommissionEmployee.

#ifndef BASE_PLUS_H

#define BASE_PLUS_H

#include <string> // C++ standard string class

#include "CommissionEmployee.h" // CommissionEmployee class definition

class BasePlusCommissionEmployee : public CommissionEmployee {

public:

    BasePlusCommissionEmployee(const std::string&, const std::string&,

    const std::string&, double = 0.0, double = 0.0, double = 0.0);

    virtual ~BasePlusCommissionEmployee() = default; // virtual destructor

    void setBaseSalary(double); // set base salary

    double getBaseSalary() const; // return base salary
```

图 12.15 | `BasePlusCommissionEmployee` 类头文件。（第 1 部分，共 2 部分。）

### 12.7 案例研究：使用多态的工资系统 599

```
// keyword virtual signals intent to override

virtual double earnings() const override; // calculate earnings

virtual std::string toString() const override; // string representation

private:

    double baseSalary; // base salary per week

};

#endif // BASEPLUS_H
```

图 12.15 | `BasePlusCommissionEmployee` 类头文件。（第 2 部分，共 2 部分。）

```
// Fig. BasePlusCommissionEmployee.cpp

// BasePlusCommissionEmployee member-function definitions.

#include <iostream>

#include <stdexcept>

#include <iostream>

#include "BasePlusCommissionEmployee.h"

using namespace std;

constructor()

BasePlusCommissionEmployee::BasePlusCommissionEmployee(
