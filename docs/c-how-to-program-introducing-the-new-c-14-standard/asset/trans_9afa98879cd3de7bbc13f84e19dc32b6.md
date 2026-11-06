

## 12.7 案例研究：使用多态性的工资系统

本节重新审视我们在 **第11.3节** 中探讨的 `CommissionEmployee—BasePlusCommissionEmployee` 继承体系。在本例中，我们使用抽象类和多态性根据员工类型执行工资计算。我们创建了一个增强的员工继承体系来解决以下问题：

> 公司每周向员工支付工资。员工有三种类型：受薪员工无论工作多少小时都获得固定的周薪；佣金员工按销售额的一定百分比获得报酬；底薪加佣金员工获得基本工资加上销售额的一定百分比。对于当前支付周期，公司决定通过将底薪加佣金员工的基本工资提高10%来奖励他们。公司希望实现一个 C++ 程序，以多态方式执行其工资计算。

我们使用抽象类 `Employee` 来表示员工的一般概念。直接从 `Employee` 派生的类是 `SalariedEmployee` 和 `CommissionEmployee`。类 `BasePlusCommissionEmployee` 派生自 `CommissionEmployee`，代表最后一种员工类型。**图 12.7** 中的 UML 类图显示了我们的多态员工工资应用程序的继承层次结构。按照 UML 的约定，抽象类名 `Employee` 以*斜体*显示。

抽象基类 `Employee` 声明了该层次结构的“接口”——即程序可以对*所有* `Employee` 对象调用的一组成员函数。无论每位员工的收入如何计算，每位员工都有名字、姓氏和社会安全号码，因此 `private` 数据成员 `firstName`、`lastName` 和 `socialSecurityNumber` 出现在抽象基类 `Employee` 中。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1590_0.png)

**图 12.7** `Employee` 层次结构 UML 类图。

*派生类可以从基类继承接口和/或实现。为**实现继承**设计的层次结构往往将其功能放在层次结构的高层——每个派生类从基类继承一个或多个成员函数，并且派生类使用基类的定义。为**接口继承**设计的层次结构往往将其功能放在层次结构的较低层——基类指定一个或多个应由每个派生类定义的函数，但各个派生类提供自己的函数实现。*

以下各节实现 `Employee` 类层次结构。前四节分别实现抽象类或具体类之一。最后一节实现一个测试程序，该程序构建具体类的对象并以多态方式处理这些对象。

### 12.7.1 创建抽象基类 `Employee`

类 `Employee`（**图 12.9–12.10**，稍后将详细讨论）提供了函数 `earnings` 和 `toString`，以及操作 `Employee` 数据成员的各种 *get* 和 *set* 函数。`earnings` 函数当然普遍适用于所有员工，但每次收入计算都取决于员工的类别。因此，我们在基类 `Employee` 中将 `earnings` 声明为纯 `virtual` 函数，因为*该函数的默认实现没有意义*——没有足够的信息来确定 `earnings` 应该返回的金额。

每个派生类都使用适当的实现*覆盖* `earnings`。为了计算员工的收入，程序将员工对象的地址分配给基类 `Employee` *指针*，然后对该对象调用 `earnings` 函数。

测试程序维护一个 `Employee` 指针的 `vector`，每个指针都指向一个 `Employee` 对象。*当然，不可能存在 `Employee` 对象，因为 `Employee` 是一个抽象类——但通过继承，`Employee` 的所有具体派生类的所有对象仍然可以被视为 `Employee` 对象。* 程序遍历 `vector` 并为每个 `Employee` 对象调用函数 `earnings`。C++ 以*多态*方式处理这些函数调用。将 `earnings` 作为 `Employee` 中的纯 `virtual` 函数，迫使 `Employee` 的每个希望成为*具体*类的直接派生类都必须覆盖 `earnings`。

类 `Employee` 中的函数 `toString` 返回一个 `string`，其中包含员工的名字、姓氏和社会安全号码。我们将看到，`Employee` 的每个派生类都覆盖函数 `toString`，以输出员工类型（例如，`"salaried employee:"`），后跟员工信息的其余部分。每个派生类的 `toString` 也可以调用 `earnings`，即使 `earnings` 是基类 `Employee` 中的纯 `virtual` 函数，因为每个*具体*类都保证有 `earnings` 的实现。因此，即使类 `Employee` 的 `toString` 函数也可以调用 `earnings`——在运行时，当你通过 `Employee` 指针或引用调用 `toString` 时，你总是在*具体*派生类的对象上调用它。

**图 12.8** 中的图表在左侧显示了层次结构中的四个类，在顶部显示了函数 `earnings` 和 `toString`。对于每个类，图表显示了每个函数的期望结果。斜体文本表示 *`earnings` 和 `toString` 函数中使用的特定对象的值*。类 `Employee` 为函数 `earnings` 指定了“`=0`”，以表明它是一个纯 `virtual` 函数，因此*没有*实现。每个派生类都覆盖此函数以提供适当的实现。我们没有列出基类 `Employee` 的 *get* 和 *set* 函数，因为它们在任何派生类中*未被覆盖*——这些函数中的每一个都被每个派生类继承并“原样”使用。

| 类 | earnings | toString |
|---|---|---|
| Employee | =0 | *firstName lastName*<br>social security number: SSN |
| SalariedEmployee | *weeklySalary* | salaried employee: *firstName lastName*<br>social security number: *SSN*<br>weekly salary: *weeklySalary* |
| CommissionEmployee | *commissionRate × grossSales* | commission employee: *firstName lastName*<br>social security number: *SSN*<br>gross sales: *grossSales*<br>commission rate: *commissionRate* |
| BasePlusCommissionEmployee | (*commissionRate × grossSales*) + *baseSalary* | base-salaried commission employee: *firstName lastName*<br>social security number: *SSN*<br>gross sales: *grossSales*<br>commission rate: *commissionRate*<br>base salary: *baseSalary* |

**图 12.8** `Employee` 层次结构类的多态接口。

### Employee 类头文件

让我们考虑类 `Employee` 的头文件（**图 12.9**）。**public** 成员函数包括一个构造函数，该构造函数将名字、姓氏和社会安全号码作为参数（第 10 行）；一个由编译器生成的 C++11 默认 `virtual` 析构函数（第 11 行）；设置名字、姓氏和社会安全号码的 `set` 函数（分别为第 13、16 和 19 行）；返回名字、姓氏和社会安全号码的 `get` 函数（分别为第 14、17 和 20 行）；纯 `virtual` 函数 `earnings`（第 23 行）和 `virtual` 函数 `toString`（第 24 行）。

```cpp
// Fig. 12.9: Employee.h
// Employee abstract base class.
#ifndef EMPLOYEE_H
#define EMPLOYEE_H

#include <string> // C++ standard string class

class Employee {
public:
    Employee(const std::string&, const std::string&, const std::string&);
    virtual ~Employee() = default; // compiler generates virtual destructor

    void setFirstName(const std::string&); // set first name
    std::string getFirstName() const; // return first name

    void setLastName(const std::string&); // set last name
    std::string getLastName() const; // return last name

    void setSocialSecurityNumber(const std::string&); // set SSN
    std::string getSocialSecurityNumber() const; // return SSN

    // pure virtual function makes Employee an abstract base class
    virtual double earnings() const = 0; // pure virtual
    virtual std::string toString() const; // virtual
private:
    std::string firstName;
    std::string lastName;
    std::string socialSecurityNumber;
};

#endif // EMPLOYEE_H
```

**图 12.9** *Employee* 抽象基类。

