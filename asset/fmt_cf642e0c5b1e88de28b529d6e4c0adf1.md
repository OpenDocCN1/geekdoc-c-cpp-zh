
## 11.5 public, protected and private 继承

继承类型决定了基类成员在派生类中的可访问性。

- `public` 继承：基类的 `public` 成员在派生类中仍为 `public`，`protected` 成员仍为 `protected`。
- `protected` 继承：基类的 `public` 和 `protected` 成员在派生类中都变为 `protected`。
- `private` 继承：基类的 `public` 和 `protected` 成员在派生类中都变为 `private`。

## 11.3 基类与派生类的关系

这是一个公继承的示例，它是最常用的形式。我们还将讨论私有继承和受保护继承（第 11.5 节）。在所有继承形式中，基类的私有成员无法从该类的派生类直接访问，但这些私有基类成员仍然被继承了（即它们被视为派生类的一部分）。通过公继承，所有其他基类成员在成为派生类的成员时，会保留其原始的成员访问权限（例如，基类的公共成员将成为派生类的公共成员，正如我们将会看到的，基类的受保护成员将成为派生类的受保护成员）。通过继承的基类成员，派生类可以操作基类的私有成员（前提是这些继承的成员函数在基类中提供了此类功能）。

继承并不适用于所有的类关系。在某些情况下，“包含关系”（has-relationship，组合）更为合适。例如，给定类 `Employee`（员工）、`BirthDate`（出生日期）和 `TelephoneNumber`（电话号码），说一个 `Employee` 是一个 `BirthDate` 或者说 `Employee` 是一个 `TelephoneNumber` 是不妥的。然而，说一个 `Employee` 拥有 `BirthDate` 且一个 `Employee` 拥有 `TelephoneNumber` 是合适的。

可以相似地对待基类对象和派生类对象；它们的共同点体现在基类的成员中。在第 12 章中，我们将考虑许多利用这种关系的示例。

在本节中，我们使用一个包含某公司/薪资应用程序中各种员工类型的继承层次结构，来讨论基类与派生类之间的关系。佣金员工（将用基类对象表示）按销售额的百分比获得工资，而底薪加佣金员工（将用派生类对象表示）获得底薪加销售额的百分比工资。我们将佣金员工与底薪加佣金员工之间关系的划分分为一系列精心设计的示例。

### 11.3.1 创建和使用 CommissionEmployee 类

让我们检查 `CommissionEmployee` 的类定义（图 11.4–11.5）。`CommissionEmployee` 头文件 (11.4) 规定了 `CommissionEmployee` 的公共服务，包括一个构造函数（第 10–11 行）和一个转换为 `String` 的成员函数（第 28 行和 29 行）。第 13–26 行定义了公共的 `get` 和 `set` 函数，用于操作类的数据成员（声明在第 31–35 行）：`firstName`、`lastName`、`SecurityNumber`、`grossSales` 和 `commissionRate`。例如，成员函数 `getSales`（在图 11.5 第 46–52 行）和 `setCommissionRate`（定义在图 11.5 第 58–64 行）在将值分配给数据成员 `grossSales` 和 `commissionRate` 之前，会对其参数进行验证。

```cpp
// Fig 11.4: CommissionEmployee.h
// CommissionEmployee 类定义表示一个佣金员工。
#ifndef COMMISSION_H
#define COMMISSION_H
```

图 11.4 | `CommissionEmployee` 类定义表示一个佣金员工。（2 部分中的第 1 部分）

```cpp
#include <string> // C++ 标准字符串类
class CommissionEmployee {
public:
    CommissionEmployee(const std::string&, const std::string&,
                        const std::string&, double = 0.0, double = 0.0);
    void setFirstName(const std::string&); // 设置名字
    std::string getFirstName() const; // 返回名字
    void setLastName(const std::string&); // 设置姓
    std::string getLastName() const; // 返回姓
    void setSocialSecurityNumber(const std::string&); // 设置 SSN
    std::string getSocialSecurityNumber() const; // 返回 SSN
    void setGrossSales(double); // 设置总销售额
    double getGrossSales() const; // 返回总销售额
    void setCommissionRate(double); // 设置佣金率（百分比）
    double getCommissionRate() const; // 返回佣金率
    double getEarnings() const; // 计算收益
    std::string toString() const; // 创建字符串表示
private:
    std::string firstName;
    std::string lastName;
    std::string socialSecurityNumber;
    double grossSales;
    double commissionRate;
};
#endif
```

图 11.4 | `CommissionEmployee` 类定义表示一个佣金员工。（2 部分中的第 2 部分）

```cpp
// CommissionEmployee.cpp
// CommissionEmployee 成员定义。
#include <iostream>
#include <iomanip>
#include <string>
#include <sstream>
using namespace std;
// 构造函数
CommissionEmployee::CommissionEmployee(const string& first, const string& last,
                                       const string& ssn, double sales, double rate) {
    firstName = first;
    lastName = last;
    socialSecurityNumber = ssn;
    grossSales = sales;
    commissionRate = rate;
}
// 设置名字
void CommissionEmployee::setFirstName(const string& first) {
    firstName = first;
}
// 返回名字
string CommissionEmployee::getFirstName() const {
    return firstName;
}
// 设置姓
void CommissionEmployee::setLastName(const string& last) {
    lastName = last;
}
// 返回姓
string CommissionEmployee::getLastName() const {
    return lastName;
}
// 设置社会安全号码
void CommissionEmployee::setSocialSecurityNumber(const string& ssn) {
    socialSecurityNumber = ssn;
}
// 返回社会安全号码
string CommissionEmployee::getSocialSecurityNumber() const {
    return socialSecurityNumber;
}
// 设置总销售额
void CommissionEmployee::setGrossSales(double sales) {
    if (sales < 0.0) {
        throw invalid_argument("总销售额不能为负数");
    }
    grossSales = sales;
}
// 返回总销售额
double CommissionEmployee::getGrossSales() const {
    return grossSales;
}
// 设置佣金率
void CommissionEmployee::setCommissionRate(double rate) {
    if (rate < 0.0 || rate > 1.0) {
        throw invalid_argument("佣金率必须在 0.0 到 1.0 之间");
    }
    commissionRate = rate;
}
// 计算收益
double CommissionEmployee::getEarnings() const {
    return commissionRate * grossSales;
}
// CommissionEmployee 的字符串表示
string CommissionEmployee::toString() const {
    ostringstream output;
    output << setprecision(2);
    output << "commission employee: " << firstName << " " << lastName
            << "\nsocial security number: " << socialSecurityNumber
            << "\ngross sales: " << grossSales;
    return output.str();
}
```

图 11.5 | 按销售额百分比计薪的 `CommissionEmployee` 实现文件（3 部分中的第 1 部分）

#### CommissionEmployee 构造函数

`CommissionEmployee` 构造函数在本文几个示例中故意没有使用成员初始化语法。这将允许我们演示私有和受保护成员对派生类访问的影响。在图 11.5 第 12–14 行，我们在构造函数体内为数据成员 `firstName`、`lastName` 和 `socialSecurityNumber` 赋值。在本文之后，我们将重新使用成员初始化列表。

我们没有在将构造函数的参数赋值给数据成员之前进行验证。我们可以对名字和姓进行验证——例如确保它们的长度合理。同样，可以对社会安全号码进行验证以确保它包含九位数字，或者不带连字符（例如 123-45-6789 或 123456789）。

#### CommissionEmployee 成员函数 earnings 和 toString

成员函数 `earnings`（第 72–74 行）计算 `CommissionEmployee` 的收益。第 73 行将 `commissionRate` 乘以 `grossSales` 并返回结果。成员函数 `toString`（第 77–85 行）显示 `CommissionEmployee` 对象数据成员的值。

#### 测试 CommissionEmployee 类

图 11.6 测试 `CommissionEmployee` 类。第 10 行实例化 `CommissionEmployee` 派生员工，并调用构造函数初始化对象，使用 "Sue" 为名字，“Jones” 为姓，“222-22-2222”为社会安全号码，100000 为总销售额，06 为佣金率。第 14–20 行使用员工的 `get` 函数显示其数据成员的值。第 22–26 行调用对象的成员函数。

`setGrossSales` 和 `setCommissionRate` 分别用于更改数据成员 `grossSales` 和 `commissionRate` 的值。第 24–25 行修改了员工的 `toll` 函数以返回更新后的 `CommissionEmployee` 函数输出。最后，第 28 行显示了 `CommissionEmployee` 的收入，该收入是通过员工成员函数使用更新后的数据成员 `grossSales` 和 `commissionRate` 值计算出的。

通过 `get` 函数获取的员工信息：

- 名字：Sue
- 姓：Jones
- 社会安全号：222-22-2222
- 总销售额：10000.00
- 佣金率：0.06

通过 `toString` 更新的员工信息：

- 佣金员工：Sue Jones
- 社会安全号：222-22-2222
- 总销售额：8000.00
- 佣金率：0.10

员工收入：$800.00

图 11.6 | `CommissionEmployee` 类测试程序。

## 第二章 对象面向编程：继承

### 11.3.2 在不使用继承的情况下创建 BasePlusCommissionEmployee 类

我们现在通过创建并测试一个完全且独立的 `BasePlusCommissionEmployee`（图 11.7–11.8）来讨论继承介绍的第二部分，它包含名字、姓、社会安全号、总销售额金额、佣金率和基本工资。

```cpp
// 图 11.7: BasePlusCommissionEmployee.h
// BasePlusCommissionEmployee 类定义表示一个除了
// 佣金外还领取基本工资的员工。
#ifndef BASEPLUS_H
#define BASEPLUS_H
#include <string> // C++ 标准字符串类
class BasePlusCommissionEmployee {
public:
    BasePlusCommissionEmployee(const std::string&, const std::string&,
                               std::string&, double = 0.0, double = 0.0);
    void setFirstName(const std::string&); // 设置名字
    std::string getFirstName() const; // 返回名字
    void setLastName(const std::string&); // 设置姓
    std::string getLastName() const; // 返回姓
    void setSocialSecurityNumber(const std::string&); // 设置 SSN
    std::string getSocialSecurityNumber() const; // 返回 SSN
    void setGrossSales(double); // 设置总销售额
    double getGrossSales() const; // 返回总销售额金额
    void setCommissionRate(double); // 设置佣金率
    double getCommissionRate() const; // 返回佣金率
    void setBaseSalary(double); // 设置基本工资
    double getBaseSalary() const; // 返回基本工资
    double earnings() const; // 计算收入
    std::string toString() const; // 创建字符串表示
private:
    std::string firstName;
    std::string lastName;
    std::string socialSecurityNumber;
    double grossSales; // 每周总销售额
    double commissionRate; // 佣金比例
    double baseSalary; // 基本工资
};
#endif
```

图 11.7 | `BasePlusCommissionEmployee` 类头文件。

```cpp
// 图 11.8: BasePlusCommissionEmployee.cpp
// 类 BasePlusCommissionEmployee 的成员函数定义。
#include <iostream>
#include <stdexcept>
#include <string>
#include "BasePlusCommissionEmployee.h"
using namespace std;
BasePlusCommissionEmployee::BasePlusCommissionEmployee(
    const string& first, const string& last, const string& ssn,
    double sales, double rate, double salary) {
    firstName = first; // 应该验证
    lastName = last; // 应该验证
```
