
### Employee 抽象基类

```cpp
public:
    Employee(const std::string&, const std::string&, const std::string&);
    virtual ~Employee() = default; // 生成析构
    void setFirstName(const std::string&); // 设置名字
    std::string getFirstName() const; // 返回名字
    void setLastName(const std::string&); // 设置姓
    std::string getLastName() const; // 返回姓
    void setSocialSecurityNumber(const std::string&); // 设置 SSN
    std::string getSocialSecurityNumber() const; // 返回 SSN
    // 纯虚函数使 Employee 成为抽象基类
    virtual double earnings() const = 0; // 纯虚
    virtual std::string toString() const; // 虚
private:
    std::string firstName;
    std::string lastName;
    std::string socialSecurityNumber;
};
#endif // EMPLOYEE_H
```

图 12.9 | `Employee` 抽象基类。

### Employee 成员函数定义

图 12.10 包含了 `Employee` 类的成员函数定义。虚函数 `earnings` 没有提供实现。`Employee` 构造函数（第 9–11 行）没有验证社会安全号。通常，应该提供这种验证。

## 12.7 案例研究：使用多态的工资系统

```cpp
// Fig. 12.10: Employee.cpp
// 抽象类 Employee 的成员函数定义。
// 注意：纯虚函数没有提供定义。
#include <iostream>
#include "Employee.h" // Employee 类定义
using namespace std;
// 构造函数
Employee::Employee(const string& first, const string& last,
    const string& ssn)
    : firstName(first), lastName(last), socialSecurityNumber(ssn) {}
// 设置名字
void Employee::setFirstName(const string& first) { firstName = first; }
// 返回名字
string Employee::getFirstName() { return firstName; }
// 设置姓
void Employee::setLastName(const string& last) { lastName = last; }
// 返回姓
string Employee::getLastName() const { return lastName; }
// 设置社会安全号
void Employee::setSecurityNumber(const string& ssn) {
    socialSecurityNumber = ssn; // 应进行有效验证
}
// 返回社会安全号
string Employee::getSecurityNumber() const {
    return socialSecurityNumber;
}
// toString 的信息（虚函数，但不是纯虚函数）
string Employee::toString() const {
    return getFirstName() + " " + getLastName() + 
        " \n security number: " + getSecurityNumber();
}
```

**图 12.10** | `Employee` 类实现。

虚函数 `toString`（第 36–39 行）提供了一个将在派生类中重写的实现。这些函数中的每一个将使用 `Employee` 版本的 `toString` 来获取包含 `Employee` 层次体系中所有类共同信息的字符串。

### 12.7.2 创建派生类 SalariedEmployee

`SalariedEmployee`（图 12.11-12.12）派自 `Employee` 类（图 12.11 的第 9 行）。公共成员函数包括：一个接受名字、姓氏、社会安全号和每周工资作为参数的构造函数（第 11-12 行）；一个 C++ 默认虚析构函数（第 13 行）；一个为数据成员 `weeklySalary` 分配新非负值的设置函数（第 15 行）；一个返回 `weeklySalary` 值的获取函数（第 16 行）；一个计算 `SalariedEmployee` 收益的虚函数 `earnings`（第 19 行），以及一个虚函数 `toString`（第 20 行），用于输出员工的类型、“salaried employee: ” 跟着由基类 `Employee` 的 `toString` 函数和 `SalariedEmployee` 的 `getWeeklySalary` 函数生成的员工特定信息。

```cpp
// Fig. 12.11: SalariedEmployee.h
// 派自 Employee 的 SalariedEmployee 类。
#ifndef SALARIED_H
#define SALARIED_H
#include <string>
#include "Employee.h" // Employee 类定义
class SalariedEmployee : public Employee {
public:
    SalariedEmployee(const std::string&, const std::string&,
                     const std::string&, double = 0.0);
    virtual ~SalariedEmployee() = default; // 虚析构函数
    void setWeeklySalary(double); // 设置每周工资
    double getWeeklySalary() const; // 返回每周工资
    virtual double earnings() const override; // 计算收益
    virtual std::string toString() const override; // 字符串表示
private:
    double getWeeklySalary; // 每周工资
};
#endif // SALARIED_H
```

图 12.11 | `SalariedEmployee` 类头文件。

#### SalariedEmployee 类成员函数定义

图 12 包含了 `SalariedEmployee` 的成员函数定义。该类的构造函数将名字、姓氏和社会安全号传递给 `Employee` 构造函数（第 12 行），以初始化继承自基类的私有数据成员，这些成员在派生类中无法直接访问。`earnings`（第 30 行）重写了 `Employee` 中的虚函数 `earnings`，以提供一个返回 `SalariedEmployee` 工资的具体实现。如果我们没有定义 `earnings`，`SalariedEmployee` 将成为一个抽象类，尝试实例化 `SalariedEmployee` 对象将导致编译错误。在 `SalariedEmployee` 的头文件中，我们声明了成员函数 `earnings` 和 `toString`（图 12.11 的第 19–20 行）——实际上，在这些成员函数之前放置 `virtual` 关键字是多余的。当在基类 `Employee` 中定义为虚函数时，它们在整个类层次结构中一直保持为虚函数。在层次结构的每一级显式声明此类虚函数可以提高清晰度。不将 `earnings` 声明为纯虚函数表示我们的意图在这个具体类中提供实现。

```cpp
// Fig.12.12: SalariedEmployee.cpp
// SalariedEmployee 类成员函数定义。
#include <iostream>
#include <stdexcept>
#include <string>
#include "SalariedEmployee.h" // SalariedEmployee 类定义
using namespace std;
// 构造函数
SalariedEmployee::SalariedEmployee(const string& first,
    const string& last, const string& ssn, double salary)
    : Employee(first, last, ssn) {
    setWeeklySalary(salary);
}
// 设置工资
void SalariedEmployee::setWeeklySalary(double salary) {
    if (salary < 0.0)
        throw invalid_argument("Weekly salary must be >= 0.0");
    weeklySalary = salary;
}
// 返回工资
double SalariedEmployee::getWeeklySalary() const { return weeklySalary; }
// 计算收益：
double SalariedEmployee::earnings() const {
    return getWeeklySalary() * taxRate;
}
// 返回字符串表示
string SalariedEmployee::toString() const {
    ostringstream output;
    output << "salaried employee: "
        << "weekly salary: " << getWeeklySalary();
    return output.str();
}
```

图 12.12 | `SalariedEmployee` 类实现。

虚函数 `toString`（第 36–39 行）提供了一个将在派生类中重写的实现。这些函数中的每一个将使用 `Employee` 版本的 `toString` 来获取包含 `Employee` 层次体系中所有类共同信息的字符串。

### 12.7 创建派生类 CommissionEmployee

`CommissionEmployee` 类（图 12.13-12.14）派自 `Employee`（图 12.13 的第 9 行）。图 12 中的成员函数实现包括：一个构造函数（第 10–15 行），接受名字、姓氏、社会安全号、销售金额和佣金率；设置函数（第 18–24 行和 30–36 行）分别为 `grossSales` 和 `commissionRate` 分配新值；获取函数（第 27–41 行）计算 `CommissionEmployee` 的收益；以及 `toString` 函数（第 49–56 行），输出员工的类型，即“commission employee: ” 以及员工特定信息。构造函数将名字、姓氏和社会安全号传递给 `Employee` 构造函数（第 12 行），以初始化 `Employee` 的私有成员。`toString` 基（第 52 行）获取员工特定信息的字符串表示。

```cpp
// Fig.12.13: CommissionEmployee.h
// 派自 Employee 的 CommissionEmployee 类。
#ifndef COMMISSION_H
#define COMMISSION_H
#include <string>
#include "Employee.h" // Employee 类定义
#include <sstream> // cpp 中需要的 ostring
class CommissionEmployee : public Employee {
public:
    CommissionEmployee(const std::string&, const std::string&,
        const std::string&, double = 0.0);
    virtual ~CommissionEmployee() = default; // 虚析构函数
    void setCommissionRate(double); // 设置佣金率
    double getCommissionRate() const; // 返回佣金率
    void setGrossSales(double); // 设置总销售额
    double getGrossSales() const; // 返回总销售额
    virtual double earnings() const override; // 计算收益
    virtual std::string toString() const override; // 字符串表示
private:
    double grossSales; // 每周销售
    double commissionRate; // 佣金百分比
};
#endif // COMMISSION_H
```

## 12.7 案例研究：使用多态的工资系统

```cpp
// Fig. 12.14: CommissionEmployee.cpp
// CommissionEmployee 类成员函数定义。
#include <iomanip>
#include <stdexcept>
#include <iostream>
// "CommissionEmployee.h" // CommissionEmployee 类定义
using namespace std;
// 构造函数
CommissionEmployee::CommissionEmployee(const string&first,
    const string &last, const string &ssn, double sales, double rate)
    : Employee(first, last, ssn) {
    setGrossSales(sales);
    setCommissionRate(rate);
}
// 设置总销售额
void CommissionEmployee::setGrossSales(double sales) {
    if (sales < 0.0) {
        throw invalid_argument("Gross sales must be >= 0.0");
    }
    grossSales = sales;
}
// 返回总销售额
double CommissionEmployee::getGrossSales() const {return grossSales;}
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
// 计算收益；重写 Employee 中的纯虚函数 earnings
double CommissionEmployee::earnings() const {
    return getCommissionRate() * getGrossSales();
}
// 返回 CommissionEmployee 信息的字符串表示
string CommissionEmployee::toString() const {
    ostringstream output;
    output << fixed << setprecision(2);
    output << "commission employee: " << Employee::toString() 
        << "gross sales: " << getSales()
        << " commission rate: " << getCommissionRate();
    return output.str();
}
```
