
“`0`” 是一个纯限定符。纯虚函数不提供实现。每个派生类都必须用实现重写基类的所有的纯虚函数；否则，该派生类也是抽象的。

虚函数和纯虚函数之间的区别在于，虚函数有实现，并赋予派生类重写它的选项；而纯虚函数没有实现，并要求派生类重写该函数以便该派生类成为具体的；否则，派生类将保持为抽象类。

当基类拥有函数的实现没有意义，但你又想强制所有派生类实现该函数时，就会使用纯虚函数。回到我们之前关于空间对象的例子，基类 `GameObject` 具有 `draw` 函数实现是没有意义的（因为在没有关于正在绘制的什么类型对象的特定信息的情况下，无法画出一个通用对象）。一个可以定义为虚（或非纯虚）的函数示例是需要对象名称的函数。我们可以为通用的 `GameObject` 命名（例如，“空间对象”），为该函数提供一个简单的实现，该函数不需要是纯虚的。该函数仍然声明为虚函数，因为预计派生类将重写此函数以为派生类对象提供更具体的名称。

> 软件工程观察 12.8
抽象类为类层次结构中派生自它的各种类定义了一个公共接口。抽象类包含一个或多个派生类必须重写的纯虚函数。

> 常见编程错误 12.2
在派生类中未能重写纯虚函数会导致该类成为抽象类。尝试实例化抽象类的对象会导致编译错误。

> 软件工程观察 12.9
抽象类至少包含一个纯虚函数。抽象类还可以拥有数据成员和具体函数，这些成员遵循通常的继承规则。

## 12.6.2 设备驱动程序：操作系统中的多态

多态在实现分层系统时特别有效。例如，在操作系统中，每种设备运行方式可能与其它不同。尽管如此，对设备读取或写入数据的命令可能具有某种统一性。发送到设备的写入消息需要在该设备的语文中进行解释。操作系统可以使用抽象基类为所有设备提供适当的接口。然后，通过继承抽象类，形成了运行类似的派生类。设备驱动程序的能力（即公共函数）在派生类中作为虚函数提供。这种架构还允许方便地添加新设备。用户只需插入并安装新设备即可。操作系统通过设备驱动程序与新设备通信，驱动程序具有与所有驱动程序相同的公共函数——这些函数定义在抽象基类中。

## 12.7 研究：使用多态工资系统

本节重新检查了我们在 11.3 节中探讨的 `CommissionEmployee-BaseEmployee` 层次结构。在这个例子中，我们使用抽象类和多态来根据员工类型执行计算。我们创建一个增强的员工层次结构来解决问题：

一家公司向员工发放工资。员工有三种：薪制员工无论工作小时多少都获得固定的周薪；佣金员工根据其销售额的比例获得工资；底薪加佣金员工根据其销售额获得底薪比例。在本期内，公司决定通过为底薪加佣金员工增加 10% 的底薪来奖励他们。公司想要实现一个多态地执行工资计算的 C++ 程序。

我们使用抽象类来表示员工的通用概念。直接派自 `Employee` 的类有 `SalariedEmployee` 和 `CommissionEmployee`。`BaseEmployee` 类派自 `CommissionEmployee` 并代表最后类型。12.7 节中的 UML 类图显示了我们多态员工程序的继承层次结构。根据 UML 约定，抽象类 `Employee` 使用斜体。

抽象基类声明了层次结构的“接口”——即程序可以在所有 `Employee` 对象上调用的成员函数集。无论计算方式如何，每个员工都有一个名字和一个

# 590 第 12 章 对象面向编程：多态

![](img/d9ae0ed4c13d4f57e9ae2c92e9fdf0b7_590_0.png)

图 12.7 | 员工层级结构的 UML 类图。

抽象基类 `Employee` 中的私有数据成员 `firstName`、`lastName`（姓）和 `socialSecurityNumber`（社会安全号）。

# 软件工程观察 12.10

派生类可以继承和/或实现基类。为继承设计的层次结构其功能通常位于层次结构的较高位置，每个派生类从基类继承一个或多个成员，并且派生类使用基类的定义。为接口设计的层次结构其功能通常位于层次结构的较低位置——基类指定每个派生类应该定义的一个或多个函数，但具体的派生类提供这些函数各自的实现。

# 12.7.1 创建抽象基类 Employee

`Employee` 类（图 12.9–12.10，将在后续详细讨论）提供了 `earnings` 和 `toString` 函数，以便改变操作 `Employee` 数据的 get 和 set 函数。`earnings` 函数通常适用于所有员工，但每个计算取决于员工的类。我们在基类 `Employee` 中将 `earnings` 声明为纯虚函数（pure virtual），因为该函数没有默认实现意义意义——没有足够的信息来确定 `earnings` 返回什么。

每个派生类都用相应的实现来重写该函数。为了计算员工的工资，程序将员工对象的地址分配给基类 `Employee` 指针，然后并在该对象上调用 `earnings` 函数。

测试程序维护了一个 `Employee` 指针的向量（`vector`），每个指针都指向一个 `Employee` 对象。当然，不能有 `Employee` 对象，因为 `Employee` 是一个抽象类——尽管如此，通过继承，`Employee` 的派生类的所有对象都可以被视为 `Employee` 对象。程序遍历向量并对每个 `Employee` 对象调用 `earnings` 函数。C++ 以多态态的方式处理这些函数调用。

# 12.7 案例研究：使用多态的薪资系统 591

将 `earnings` 作为纯虚函数包含在 `Employee` 中，迫使每个希望成为类的 `Employee` 派生类都重写 `earnings`。

`Employee` 类中的函数 `toString` 返回一个包含员工名、姓和社会安全号的字符串。正如我们看到的，`Employee` 的每个派生类都重写了 `toString` 以输出员工的类型（例如“薪制员工”），随后是员工的其他信息。每个派生类的 `toString` 也可以调用 `earnings`，即使 `earnings` 是 `Employee` 中的纯虚函数，因为每个类都保证拥有 `earnings` 的实现。由于这个原因，即使是 `Employee` 的 `toString` 也可以调用 `earnings`——在运行时，当你对 `Employee` 指针或引用调用 `toString` 时，你始终是在一个派生类对象上调用它。

12.8 中的图表显示了层次结构中四个类中的每一个，左侧是类，顶部是 `earnings` 和 `toString`。对于每个类，图表显示了每个函数的预期结果。斜体文本表示特定对象的值何在 `earnings` 和 `toString` 函数中被使用。类 `Employee` 为函数 `earnings` 指定了 "0"，以表示它是一个虚函数，因此没有实现。我们没有列出基类 `Employee` 的 get 和 set 函数，因为它们在任何派生类中都没有被重写——这些每一个每一个都都被派生类继承并“原样”使用。

| earnings | toString |
|---|---|
| Employee | 0 | firstName lastName social security number: SSN |
| Salaried-Employee | weeklySalary | salaried employee: firstName lastName social security number: SSN weekly salary: weeklySalary |
| Commission-Employee | commissionRate * grossSales | commission employee: firstName lastName social security number: SSN gross sales: grossSales commission rate: commissionRate |
| BasePlus-Commission-Employee | (commissionRate * grossSales) + baseSalary | base-salaried commission employee: firstName lastName social security number: SSN gross sales: grossSales commission rate: commissionRate base salary: baseSalary |

**图 12.8** `Employee` 层次结构类类的多态接口。

# Employee 类头文件

让我们考虑 `Employee` 的头文件（图 12.9）。公共成员函数包括一个以名、姓和社会安全号作为参数的构造函数（第 10 行）；编译器生成的 C++11 默认析构函数（第 11 行）；

设置名、姓和社会安全号的函数（分别为第 13、16 和 19 行）；返回名、姓和社会安全号的 get 函数（分别为第 14、17 和 20 行）；纯虚函数 `earnings`（第 23 行）和虚函数 `toString`（第 24 行）。

```
// Fig.12.9: Employee.h

// Employee 抽象基类。

#ifndef EMPLOYEE_H

#define EMPLOYEE_H

#include <string> // C++ 标准字符串类

class Employee {

public:

    Employee(const std::string&, const std::string&, const std::string&);

    virtual ~Employee() = default; // 默认析构函数

    void setFirstName(const std::string&); // 设置名

    std::string getFirstName(); // 返回名

    void setLastName(const std::string&); // 设置姓

    std::string getUsername() const; // 返回姓

    void setSocialSecurityNumber(const std::string&); // 设置号

    std::string getSocialSecurityNumber() const; // 返回号

    virtual double earnings() const = 0; // 纯虚

    virtual std::string toString() const; // 虚

private:

    std::string firstName;

    std::string lastName;

    std::string socialSecurityNumber;

};

#endif // EMPLOYEE_H
```

图12.9 | `Employee` 抽象基类。

记得我们将 `earnings` 声明为纯虚函数，因为必须知道具体的 `Employee` 类型才能确定相应的工资计算。将此函数声明为纯虚表示每个派生类必须提供 `earnings` 实现，并且程序可以使用基类 `Employee` 指针（或引用）以多态方式调用。

# Employee 类成员函数定义

图 12.10 包含了 `Employee` 类的成员函数定义。虚函数没有提供实现。`Employee` 构造函数（第 9–11 行）没有验证社会安全号。通常应该提供这种验证。

# 12.7 案例研究：使用多态的薪资系统 593

```
// Fig.12.10: Employee.cpp

// 抽象类的成员函数定义。

// 注意：纯虚函数没有定义。

#include <iostream>

#include "Employee.h" // Employee 类定义

using namespace std;

// 构造函数

Employee::Employee(const string& first, const string& last,

    const string& ssn)

    : firstName(first), lastName(last), socialSecurityNumber(ssn) {}

// 设置名

void Employee::setFirstName(const string& first) { firstName = first; }

// 返回名

string Employee::getFirstName() { return firstName; }

// 设置姓

void Employee::setLastName(const string& last) { lastName = last; }

// 返回姓

string Employee::getUsername() const { return lastName; }

// 设置号

void Employee::setSocialSecurityNumber(const string& ssn) {

    socialSecurityNumber = ssn; // 应验证

}

// 返回号

string Employee::getSocialSecurityNumber() const {

    return socialSecurityNumber;

}

// toString 的信息（虚，但不是纯虚）

string Employee::toString() const {

    return getFirstName() + " " + getLastName() +

        " social security number: " + getSocialSecurityNumber();

}
```

**图 12.10** | `Employee` 类实现。

虚函数 `toString`（第 36–39 行）提供了一个将在派生类中重写的实现。这些函数中的每一个都将使用 `Employee` 类的 `toString` 版本来获取包含 `Employee` 层次结构中所有类共同信息的字符串。

# 12.7.2 创建派生类 SalariedEmployee

`SalariedEmployee` 类（图 12.11–12.12）派自 `Employee` 类（图 12.11 的第 9 行）。公共成员函数包括一个以名、姓、社会安全号和每周工资作为参数的构造函数（第 11-12 行）；C++11 默认虚析构函数（第 13 行）；一个用于分配新非负

数据成员 `weeklySalary`（第 15 行）；一个返回 `weeklySalary` 值的函数（第 16 行）；一个虚拟函数 `earnings` 计算 `SalariedEmployee` 的收益（第 19 行），以及一个虚拟函数 `toString`（第 20 行），用于输出员工的类型、名称、“salaried employee: ”，以及由基类 `Employee` 的 `toString` 函数和 `SalariedEmployee::WeeklySalary` 函数生成的员工特定信息。

```
// Fig. 12.11 SalariedEmployee.h

// 继承自 Employee 的 SalariedEmployee 类

#ifndef SALARIED_H

#define SALARIED_H

#include <string> // C++ 标准字符串类

#include "Employee.h" // Employee 类定义

class SalariedEmployee : public Employee {

public:

    SalariedEmployee(const std::string&, const std::string&,

                     const std::string&, double = 0.0);

    virtual ~SalariedEmployee() = default; // 虚析构函数

    void setWeeklySalary(double); // 设置周薪

    double getWeeklySalary() const; // 返回周薪

    // virtual 出重写意图

    virtual double earnings() const override; // 计算收益

    virtual std::string toString() const override; // 字符串表示

private:

    double weeklySalary; // 每周工资

};

#endif // SALARIED_H
```

图 12.11 | `SalariedEmployee` 类头文件。

## SalariedEmployee 类成员函数定义

图 12 包含了 `SalariedEmployee` 的成员函数定义。该类的构造函数将名、姓和社会安全号传递给 `Employee` 构造函数（第 12 行），以初始化继承自基类的私有数据成员，这些成员在派生类中无法直接访问。`earnings` 函数（第 30 行）重写了 `Employee` 中的虚函数，提供了一个返回月薪薪资的具体实现。如果我们不定义 `earnings`，`SalariedEmployee` 将成为一个抽象类，尝试实例化 `SalariedEmployee` 对象将导致编译错误。在 `SalariedEmployee` 的头文件中，我们声明了成员函数 `earnings` 和 `toString`（图 12.11 的第 19–20 行）实际上，在这些成员函数之前放置 `virtual` 关键字是多余的。由于我们在基类 `Employee` 中已将其定义为虚，它们在类层次结构中一直保持虚函数。在层次结构的每一层显式声明此类虚函数可以提高清晰度。不将 `earnings` 声明为纯虚表示了我们在具体类中提供实现的意图。

## 12.7 案例研究：使用多态的薪资系统

```
// Fig. 12.12: SalariedEmployee.cpp

// SalariedEmployee 类成员函数定义。

#include <iostream>
```
