
```cpp
#include <stdexcept>

#include <string>

#include "SalariedEmployee.h" // SalariedEmployee 类定义

using namespace std;

// 构造函数

SalariedEmployee::SalariedEmployee(const string& first,

    const string& last, const string& ssn, double salary)

    : Employee(first, last, ssn),

    setWeeklySalary(salary);

// 设置周薪

void SalariedEmployee::setWeeklySalary(double salary) {

    if (salary < 0.0) {

        throw invalid_argument("Weekly salary must be >= 0.0");

    }

    weeklySalary = salary;

}

// 返回薪资

double SalariedEmployee::getWeeklySalary() const { return weeklySalary; }

// 计算收益：

// 重写 SalariedEmployee 中的虚函数 earnings

double SalariedEmployee::earnings() const { return getWeeklySalary(); }

// 返回 SalariedEmployee 信息的字符串表示

string SalariedEmployee::toString() const {

    ostringstream output;

    output << "Salaried employee: "

    output << "weekly salary: " << getWeeklySalary();

    return output.str();

}
```

**图 12.12** | `SalariedEmployee` 类实现文件。

`SalariedEmployee` 类的 `toString` 函数（图 12.12 的第 33–40 行）重写了 `Employee` 的 `toString` 函数。如果 `SalariedEmployee` 类没有重写 `toString`，则 `SalariedEmployee` 将继承员工版本的 `toString`。在这种情况下，`SalariedEmployee` 的 `toString` 将仅仅返回员工的全名和社会安全号，这不能充分表示一个 `SalariedEmployee`。为了创建 `SalariedEmployee` 完整字符串表示，派生类的 `toString` 函数通过使用作用域解析运算符（第 37 行）调用基类的 `toString` 函数，返回基类特定的员工信息（即名、姓和社会安全号），并在其前面加上“salaried employee: ”。如果没有 `Employee::`，`toString` 将导致无限递归。`SalariedEmployee::toString` 函数生成的字符串还包含通过调用类的 `getWeeklySalary` 函数获取的员工周薪。

## 12.7.3 创建派生类 CommissionEmployee

`CommissionEmployee` 类（图 12.13-12.14）派自 `Employee`（图 12.3，第 9 行）。图 12.14 中的成员函数实现包含一个构造函数（第 10–15 行），该函数接收名、姓、社会安全号、销售额和佣金率；set 函数（第 18–24 行和 30–36 行）用于分配新值；get 函数（第 27–39 行）用于检索这些值；函数（第 44–56 行）用于输出员工类型，即“commission employee: ”以及员工特定信息。构造函数将名、姓和社会安全号传递给 `Employee` 构造函数（第 12 行）以初始化私有数据成员。`toString` 函数调用基类以获取 `CommissionEmployee` 的字符串表示。

```cpp
// Fig. 12.13: CommissionEmployee.h
// 继承自 Employee 的 CommissionEmployee 类
#ifndef COMMISSION_H
#define COMMISSION_H

#include <string> // C++ 标准字符串类
#include "Employee.h" // Employee 类定义

class CommissionEmployee : public Employee {
public:
    CommissionEmployee(const std::string&, const std::string&,
                       const std::string&, double = 0.0);
    virtual ~CommissionEmployee() = default; // 虚析构函数
    void setCommissionRate(double); // 设置佣金率
    double getCommissionRate() const; // 返回佣金率
    void setGrossSales(double); // 设置销售额
    double getGrossSales() const; // 返回销售额
    // virtual 出重写意图
    virtual double earnings() const override; // 计算收益
    virtual std::string toString() const override; // 字符串表示
private:
    double grossSales; // 销售额
    double commissionRate; // 佣金百分比
};
#endif // COMMISSION_H
```

图 12.13 | `CommissionEmployee` 类头文件。

```cpp
// Fig. 12.14: CommissionEmployee.cpp
// CommissionEmployee 类成员函数定义。
#include <iostream>
#include <stdexcept>
#include <string>
#include "CommissionEmployee.h" // CommissionEmployee 类定义
using namespace std;

// 构造函数
CommissionEmployee::CommissionEmployee(const string& first,
    const string& last, const string& ssn, double sales, double rate)
    : Employee(first, last, ssn) {
    setGrossSales(sales);
    setCommissionRate(rate);
}

// 设置佣金率
void CommissionEmployee::setCommissionRate(double rate) {
    if (rate < 0.0 || rate > 1.0) {
        throw invalid_argument("Commission rate must be > 0.0 and < 1.0");
    }
    commissionRate = rate;
}

// 返回佣金率
double CommissionEmployee::getCommissionRate() const {
    return commissionRate;
}

// 设置销售额
void CommissionEmployee::setGrossSales(double sales) {
    if (sales < 0.0) {
        throw invalid_argument("Gross sales must be >= 0.0");
    }
    grossSales = sales;
}

// 返回销售额
double CommissionEmployee::getGrossSales() const {
    return grossSales;
}

// 计算收益：
// 重写 Employee 中的纯虚函数 earnings
double CommissionEmployee::earnings() const {
    return getCommissionRate() * grossSales();
}

// 返回 CommissionEmployee 信息的字符串表示
string CommissionEmployee::toString() const {
    ostringstream output;
    output << fixed << setprecision(2);
    output << "commission employee: ";
    output << "sales: " << getGrossSales();
    output << ", rate: " << getCommissionRate();
    output << ", " << Employee::toString();
    return output.str();
}
```

图 12.14 | `CommissionEmployee` 类实现文件。

## 第 12 章 对象面向编程：多态

```cpp
52 output << "commission employee: " << Employee::toString()
53 << "\ngross sales: " << getSales()
54 << " commission rate: " << getCommissionRate();
55 return out.str();
56 }
```

图 12.14 | `CommissionEmployee` 类实现。（2 部分中的第 2 部分。）

### 12.7. 创建间接具体派生类 BasePlusCommissionEmployee

`BasePlusCommissionEmployee`（图 12.15–12.16）直接继承自 `CommissionEmployee` 类（图 12.15 的第 9 行），并且是 `Employee` 类的间接派生类。图 12.16 中 `BasePlusCommissionEmployee` 的成员函数实现包含一个构造函数（第 10-15 行），其参数接收名字、姓、安全号、销售金额、佣金率和基本薪水。然后，它将名字、姓、销售金额和佣金率传递给 `CommissionEmployee` 构造函数（第 13 行）以初始化继承的成员。`BasePlusCommissionEmployee` 还包含一个 set 函数（第 27–29 行）用于为成员 `baseSalary` 分配新值，以及一个返回 `baseSalary` 值的 get 函数。`earnings` 函数（第 33–35 行）计算 `BasePlusCommissionEmployee` 的收益。`CommissionEmployee` 类中的第 34 行计算了员工收益中基于佣金的部分。`BasePlusCommissionEmployee` 的 `toString` 函数（第 38–44 行）返回“salary-based”，随后是基类 `CommissionEmployee` 的 `toString` 函数的结果，紧接着是 `BasePlusCommissionEmployee` 的信息。记住，`CommissionEmployee` 的 `toString` 通过调用其基类（即 `Employee`）的 `toString` 函数返回一个包含员工名字、姓和社会安全号的字符串。`BasePlusCommissionEmployee` 的 `toString` 启动了一个跨越 `Employee` 层次结构三层的函数调用链。

```cpp
// 图 12.15: BasePlusCommissionEmployee.h
// BasePlusCommissionEmployee 类派生自 CommissionEmployee。
#ifndef BASE_PLUS_H
#define BASE_PLUS_H

#include <string> // C++ 标准字符串类
#include "CommissionEmployee.h" // CommissionEmployee 类定义

class BasePlusCommissionEmployee : public CommissionEmployee {
public:
    BasePlusCommissionEmployee(const std::string&, const std::string&,
    const std::string&, double = 0.0, double = 0.0, double = 0.0);
    virtual ~BasePlusCommissionEmployee() = default; // 虚析构函数
    void setBaseSalary(double); // 设置基本薪水
    double getBaseSalary() const; // 返回基本薪水
```

图 12.15 | `BasePlusCommissionEmployee` 类头文件。（2 部分中的第 1 部分。）

### 12.7 案例研究：使用多态的工资系统

```cpp
17 // 关键字 virtual 表示重写意图
18 virtual double earnings() const override; // 计算收益
20 virtual std::string toString() const override; // 字符串表示
21 private:
23 double baseSalary; // 每个键的基本薪水
24 };
26 #endif // BASE_PLUS_H
```

**图 12.15 | `BasePlusCommissionEmployee` 类头文件。（2 部分中的第 2 部分。）**

```cpp
1 // 图 12.16: BasePlusCommissionEmployee.cpp
2 // BasePlusCommissionEmployee 成员函数定义。
3 #include <iostream>
4 #include <stdexcept>
5 #include <iostream>
6 #include "BasePlusCommissionEmployee.h"
7 using namespace std;

9 // 构造函数
10 BasePlusCommissionEmployee::BasePlusCommissionEmployee(
11 const string& first, const string& last, const string& ssn,
12 double sales, double rate, double salary)
13 : CommissionEmployee(first, last, ssn, sales, rate) {
14 setBaseSalary(salary); // 校验并存储基本薪水
15 }

17 // 设置基本薪水
18 void BasePlusCommissionEmployee::setBaseSalary(double salary) {
19 if (salary < 0.0) {
20 throw invalid_argument("Salary must be >= 0.0");
21 }
23 baseSalary = salary;
24 }

26 // 返回基本薪水
27 double BasePlusCommissionEmployee::getBaseSalary() const {
28 return baseSalary;
29 }

31 // 计算收益：
// 重写 CommissionEmployee 中的虚函数 earnings：
33 double BasePlusCommissionEmployee::earnings() const {
34 return getSalary() + CommissionEmployee::earnings();
35 }

37 // 返回 BasePlusCommissionEmployee 的字符串表示
38 string BasePlusCommissionEmployee::toString() const {
39 ostream output;
40 output << fixed << setprecision(2);
```

**图 12.16 | `BasePlusCommissionEmployee` 类实现文件。（2 部分中的第 1 部分。）**

```cpp
41 output << "base-salaried " << CommissionEmployee::toString()
42 << " base salary: " << getBaseSalary();
43 return output.str();
44 }
```
