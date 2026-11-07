

```cpp
#include "Employee.h"

// constructor performs "constructor injection" to initialize
// the CompensationModel pointer to a CompensationModel implementation
Employee::Employee(std::string_view name, CompensationModel* modelPtr)
    : m_name{name}, m_modelPtr{modelPtr} {}

// set function performs "property injection" to change the
// CompensationModel pointer to a new CompensationModel implementation
void Employee::setCompensationModel(CompensationModel* modelPtr) {
    m_modelPtr = modelPtr;
}

// use the CompensationModel to calculate the Employee's earnings
double Employee::earnings() const {
    return m_modelPtr->earnings();
}

// return string representation of Employee object
std::string Employee::toString() const {
    return std::format("{}\n{}", m_name, m_modelPtr->toString());
}
```

**图 10.21** | 类 `Employee` 的成员函数定义。（第 2 部分，共 2 部分。）

## 10.11.3 CompensationModel 实现

接下来，让我们定义 CompensationModel 的实现。这些类的对象将被注入到 Employee 对象中，以指定如何计算其收入。

### CompensationModel 的 Salaried 派生类

受薪薪酬模型（图 10.22–10.23）定义如何向领取固定薪水的 Employee 支付报酬。该类包含一个 m_salary 数据成员，并重写接口 CompensationModel 的 earnings 和 toString 成员函数。**Salaried 被声明为 final**（第 7 行），因此它是 **CompensationModel** 层次结构中的叶节点。它不能用作基类。

```cpp
// Fig. 10.22: Salaried.h
// Salaried implements the CompensationModel interface.
#pragma once
#include <string>
#include "CompensationModel.h" // CompensationModel definition

class Salaried final : public CompensationModel {
public:
    explicit Salaried(double salary);
    double earnings() const override;
    std::string toString() const override;
private:
    double m_salary{0.0};
};
```

**图 10.22** | Salaried 实现 CompensationModel 接口。

```cpp
// Fig. 10.23: Salaried.cpp
// Salaried compensation model member-function definitions.
#include <format>
#include <stdexcept>
#include "Salaried.h" // class definition

// constructor
Salaried::Salaried(double salary) : m_salary{salary} {
    if (m_salary < 0.0) {
        throw std::invalid_argument("Weekly salary must be >= 0.0");
    }
}

// override CompensationModel pure virtual function earnings
double Salaried::earnings() const { return m_salary; }

// override CompensationModel pure virtual function toString
std::string Salaried::toString() const {
    return std::format("salary: ${:.2f}", m_salary);
}
```

**图 10.23** | Salaried 薪酬模型的成员函数定义。

### CompensationModel 的 Commission 派生类

佣金薪酬模型（图 10.24–10.25）定义如何根据总销售额向 Employee 支付佣金。该类包含数据成员 m_grossSales 和 m_commissionRate，并重写接口 CompensationModel 的 earnings 和 toString 成员函数。与类 Salaried 一样，类 Commission 被声明为 final（第 7 行），因此它是 CompensationModel 层次结构中的叶节点。它不能用作基类。

```cpp
// Fig. 10.24: Commission.h
// Commission implements the CompensationModel interface.
#pragma once
#include <string>
#include "CompensationModel.h" // CompensationModel definition

class Commission final : public CompensationModel {
public:
    Commission(double grossSales, double commissionRate);
    double earnings() const override;
    std::string toString() const override;
private:
    double m_grossSales{0.0};
    double m_commissionRate{0.0};
};
```

**图 10.24** | Commission 实现 CompensationModel 接口。

```cpp
// Fig. 10.25: Commission.cpp
// Commission member-function definitions.
#include <format>
#include <stdexcept>
#include "Commission.h" // class definition

// constructor
Commission::Commission(double grossSales, double commissionRate)
   : m_grossSales{grossSales}, m_commissionRate{commissionRate} {

   if (m_grossSales < 0.0) {
      throw std::invalid_argument("Gross sales must be >= 0.0");
   }

   if (m_commissionRate <= 0.0 || m_commissionRate >= 1.0) {
      throw std::invalid_argument(
         "Commission rate must be > 0.0 and < 1.0");
   }
}

// override CompensationModel pure virtual function earnings
double Commission::earnings() const {
   return m_grossSales * m_commissionRate;
}

// override CompensationModel pure virtual function toString
std::string Commission::toString() const {
   return std::format("gross sales: ${:.2f}; commission rate: {:.2f}",
      m_grossSales, m_commissionRate);
}
```

**图 10.25** | Commission 成员函数定义。

## 10.11.4 测试新层次结构

我们已经创建了 CompensationModel 接口以及定义 Employee 如何获得报酬的派生类实现。现在，让我们创建 Employee 对象，并用合适的具体 CompensationModel 实现来初始化每个对象（图 10.26）。

```cpp
// fig_10_26.cpp
// Processing Employees with various CompensationModels.
#include <format>
#include <iostream>
#include <vector>
#include "Employee.h"
#include "Salaried.h"
#include "Commission.h"
```

**图 10.26** | 使用各种 CompensationModel 处理 Employee 对象。（第 1 部分，共 2 部分。）

```cpp
int main() {
    // create CompensationModels and Employees
    Salaried salaried{800.0};
    Employee salariedEmployee{"Pierre Simon", &salaried};

    Commission commission{10000, .06};
    Employee commissionEmployee{"Sierra Dembo", &commission};

    // create and initialize vector of Employees
    std::vector<Employee> employees{salariedEmployee, commissionEmployee};

    // print each Employee's information and earnings
    for (const Employee& employee : employees) {
        std::cout << std::format("{}\nearned: ${:.2f}\n\n",
            employee.toString(), employee.earnings());
    }
}
```

```
Pierre Simon
salary: $800.00
earned: $800.00

Sierra Dembo
gross sales: $10000.00; commission rate: 0.06
earned: $600.00
```

**图 10.26** | 使用各种 CompensationModel 处理 Employee 对象。（第 2 部分，共 2 部分。）

第 12 行创建一个 Salaried 薪酬模型对象（salaried）。第 13 行创建 Employee 对象 salariedEmployee，并注入其 CompensationModel，将指向 salaried 的指针作为第二个构造函数参数传入。第 15 行创建一个 Commission 薪酬模型对象（commission）。第 16 行创建 Employee 对象 commissionEmployee，并注入其 CompensationModel，将指向 commission 的指针作为第二个构造函数参数传入。<sup>27</sup> 第 19 行创建一个 Employee 对象的 vector，并用 salariedEmployee 和 commissionEmployee 对象初始化它。最后，第 22–25 行遍历该 vector，显示每个 Employee 的字符串表示和收入。

## 10.11.5 依赖注入设计的好处

### 如果 CompensationModel 发生变化时的灵活性

将 CompensationModel 声明为实现同一接口的独立类，为未来的变化提供了灵活性。假设公司增加了新的员工薪酬支付方式。我们只需定义一个带有适当 earnings 函数的新 CompensationModel 派生类即可。

27. 在本例中，两个 CompensationModel 的生存期都将长于其对应的 Employee 对象，因此本例不存在脚注 25 中提到的运行时逻辑错误的可能性。

### 如果 Employee 被晋升时的灵活性

本例中使用的基于接口、组合和依赖注入的方法比 10.9 节的类层次结构更灵活。在 10.9 节中，如果某个 Employee 被晋升，你需要通过创建适当 Employee 派生类的新对象，然后将数据移入新对象，来改变其对象类型。**使用依赖注入，你可以调用 Employee 的 setCompensationModel 成员函数，并注入一个指向不同 CompensationModel 的指针来替换现有的指针。**

### 如果 Employee 获得新能力时的灵活性

基于接口的组合和依赖注入方法在增强 Employee 类时也更灵活。如果我们决定支持退休计划（例如 401(k) 和 IRA），我们可以说每个 Employee 都有一个 RetirementPlan。首先，我们会定义一个带有 makeRetirementPlan 成员函数的 RetirementPlan 接口，并提供适当的派生类实现。

如本例所示，使用基于接口的组合和依赖注入，只需对 Employee 类做少量修改即可支持 RetirementPlan：

- 一个指向 RetirementPlan 的数据成员，
- 一个额外的构造函数参数，用于初始化 RetirementPlan 指针，以及
- 一个 setRetirementPlan 成员函数，在需要更改 RetirementPlan 时可以调用。

## 检查点

- 1. *（判断题）* 实现继承会创建紧耦合的类，其中基类的数据成员和成员函数被继承到派生类中。**答案：** 正确。
- 2. *（讨论题）* 描述你会如何在 C++ 中定义接口。**答案：** 定义一个只包含纯虚函数的类。这样的类称为纯抽象类。
- 3. *（填空题）* 通过 ________，类包含一个指向对象的指针，该对象提供该类对象所需的行为。**答案：** 依赖注入。

## 10.12 小结

本章继续了我们对面向对象编程（OOP）的讨论，介绍了继承和运行时多态。你创建了继承基类能力的派生类，然后对它们进行自定义或增强。我们区分了 has-a 组合关系和 is-a 继承关系。

我们通过继承层次结构解释并演示了运行时多态。你编写了处理同一类层次结构中各个类的对象的程序，就像它们都是该层次结构基类的对象一样。你通过基类指针和引用来操作这些对象。

我们解释了运行时多态有助于你设计和实现更易于扩展的系统，使你能够添加新类，而只需很少或无需修改现有代码。

