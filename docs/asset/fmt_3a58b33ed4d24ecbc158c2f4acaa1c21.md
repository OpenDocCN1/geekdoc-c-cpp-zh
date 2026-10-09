
Fig. 11.14 | `CommissionEmployee` 类实现使用成员函数操作其私有数据。 (第 2 部分，共 2 部分。)

## 11.3 基类与派生类之间的关系 561

在构造函数的函数体中以及成员函数 `earnings` (图 11.14，第 70–72 行) 和 `toString` (第 75–84 行) 的函数体中，我们调用 `get` 和 `set` 成员函数来访问类的私有数据成员。如果我们决定更改数据名称，`earnings` 和 `toString` 的定义将不需要修改——只有直接操作数据成员的 `get` 和 `set` 成员函数的定义需要更改。这些更改仅发生在基类中——派生类无需进行任何更改。使更改的影响局部化是一种良好的软件工程实践。

### Performance Tip 11.2

使用成员函数访问数据成员值可能比直接访问数据稍慢一些。然而，今天的优化编译器会执行优化 (例如内联和 `get` 成员函数调用)，这些优化遵循正确的软件工程原则，并将优化留给编译器。 一个好的规则是，“不要猜测编译器。”

Changes to Class BasePlusCommissionEmployee::Member-Function Definitions
类 `BasePlusCommissionEmployee` 继承 `Employee` 的公共成员函数，并且可以通过继承的成员函数访问私有基类成员。该类的头文件自图 11.11 以来发生了变化。该类的成员函数实现有若干更改 (图 11.15)，使其与该类的先前版本 (图 11.10–11.11) 不同。成员函数 `earnings` (图 11.15，第 32–34 行) 和 `toString` (第 37–42 行) 调用成员函数 `getBaseSalary` 来获取基本工资值，而不是直接访问 `baseSalary`。 这将 `earnings` 和 `toString` 与数据成员 `baseSalary` 的实现潜在更改隔离开来。 例如，如果我们决定重命名数据成员 `baseSalary` 或更改其类型，则只有成员函数 `setBaseSalary` 和 `getBaseSalary` 需要更改。

```
// Fig. 11.15: BasePlusCommissionEmployee.cpp
// Class BasePlusCommissionEmployee member-function definitions.
#include <stdexcept>
#include <iostream>
#include "BasePlusCommissionEmployee.h"
using namespace std;
// constructor
BasePlusCommissionEmployee::BasePlusCommissionEmployee(
const string& first, const string& last, const string& ssn,
double sales, double rate, double salary)
// explicitly call base-class constructor
: CommissionEmployee(first, last, ssn, rate) {
setBaseSalary(salary); // validate and store base salary
}
```

Fig. 11.15 | `BasePlusCommissionEmployee` 类继承自 `Employee` 类但不能直接访问该类的私有数据。 (第 I 部分，共 2 部分。)

```
// set base salary
void BasePlusCommissionEmployee::setBaseSalary(double salary) {
    if (salary < 0.0) {
        throw invalid_argument("Salary must be >= 0.0");
    }
    baseSalary = salary;
}
// return base salary
double BasePlusCommissionEmployee::getBaseSalary() const {
    return baseSalary;
}
// calculate earnings
double BasePlusCommissionEmployee::earnings() const {
    return getBaseSalary() + CommissionEmployee::earnings();
}
// return string representation of BasePlusCommissionEmployee
string BasePlusCommissionEmployee::toString() const {
    ostringstream output;
    output << "base-salaried " << CommissionEmployee::toString();
    output << "\nsalary: " << getBaseSalary();
    return output.str();
}
```

**Fig. 11.15** | `BasePlusCommissionEmployee` 类继承但不能访问类的私有数据。 (第 2 部分，共 2 部分。)

### BasePlusCommissionEmployee 成员函数 earnings

类 `BasePlusCommissionEmployee` 的 `earnings` 函数 (图 11.15，第 32–34 行) 重新定义了类 `BasePlusCommissionEmployee` 的 `earnings` 成员函数 (图 11.14，第 70–72 行)，以计算 `BasePlusCommissionEmployee` 的收益。类 `BasePlusCommissionEmployee` 的 `earnings` 版本通过使用表达式 `CommissionEmployee::earnings()` 如图 11.15 第 33 行所示调用 `CommissionEmployee` 的 `earnings` 函数来获取仅基于佣金的收益部分。`BasePlusCommissionEmployee` 然后将基本工资加到此值上以计算员工的总收益。注意用于从派生类调用重新定义的基类成员函数的语法——在基类成员函数之前放置类名和作用域解析运算符 (`::`)。 此成员函数调用是一种良好的软件工程实践； 回顾第 9 章，如果对象的成员函数执行另一个对象所需的动作，我们应该拥有该成员函数而不是复制其代码体。通过让 `BasePlusCommissionEmployee` 的 `earnings` 函数调用 `CommissionEmployee` 的 `earnings` 函数来计算 `BasePlusCommissionEmployee` 对象收益的一部分，我们避免了代码重复并减少了代码维护问题。

## 11.4 派生类中的构造函数和析构函数

![](img/06ca63376760c659af4aa0e9c282068d_563_0.png)

### Common Programming Error 11.2

当基类成员函数在派生类中被重新定义时，派生类版本通常会调用基类版本来执行工作。 在引用基类成员函数时未能使用以基类名称为前缀的 `::` 运算符会导致无限递归，因为派生类成员函数将调用自身。

### BasePlusCommissionEmployee 成员函数 toString

同样，`BasePlusCommissionEmployee` 的 `toString` 函数 (图 11.15，第 37–42 行) 定义了类 `CommissionEmployee` 的 `toString` 函数 (图 11.14，第 75–84 行) 以输出适当的基本工资佣金员工信息。 新版本显示 "base-salary" 后跟通过调用 `CommissionEmployee::toString` (图 11.15，第 39 行) 返回的 `BasePlusCommissionEmployee` 对象信息的一部分——这返回一个包含 "commission employee" 和 `CommissionEmployee` 私有数据成员值的字符串。`BasePlusCommissionEmployee` 的 `toString` 函数然后输出 `BasePlusCommissionEmployee` 对象信息的其余部分 (即类 `BasePlusCommissionEmployee` 的基本工资值前面加上 "base salary:")。

### Testing the Modified Class Hierarchy

再次，这个示例使用了图 11.9 中的 `BasePlusCommissionEmployee` 测试程序并产生相同的输出。 尽管每个“基本工资佣金员工”行为相同，但这里的版本是最好的工程设计。 通过使用继承并调用隐藏数据并确保一致性的成员函数，我们高效有效地构建了一个设计良好的类。

### Summary of the CommissionEmployee–BasePlusCommissionEmployee Examples

在本节中，您看到了一个旨在教授继承良好软件工程关键能力的演进示例集。我们学习了如何使用继承创建派生类，如何使用受保护的基类成员使派生类能够访问继承的数据成员，以及如何重新定义基类函数以提供更适合派生类的版本。 此外，我们学习了如何应用第 9 章和本章的软件工程技术来创建易于维护、修改和调试的类。

## 11.4 派生类中的构造函数和析构函数

实例化派生类对象会开始一系列构造函数调用，其中派生类构造函数在执行其任务时显式 (通过基类成员初始化器) 或隐式 (调用基类构造函数) 调用其直接基类的构造函数。 同样，如果基类派生自另一个类，则基类构造函数需要调用层次结构中下一个上层的构造函数，依此类推。 此链中最后调用的构造函数是层次结构基部的类之一，它实际上最先完成执行。 最派生类构造函数的函数体最后完成执行。 每个基类构造函数初始化基类数据

## 第11章 面向对象编程：继承

在我们一直在研究的 `CommissionEmployee`-`BasePlusCommissionEmployee` 继承层次结构中，派生类对象继承的成员，当程序创建一个 `BasePlusCommissionEmployee` 对象时，`CommissionEmployee` 构造函数会被调用。由于类 `CommissionEmployee` 位于层次结构的顶端，其构造函数会初始化作为 `BasePlusCommissionEmployee` 对象一部分的私有 `CommissionEmployee` 数据成员。当 `CommissionEmployee` 的构造函数执行完毕后，它将控制权返回给 `BasePlusCommissionEmployee` 的构造函数，后者初始化 `BasePlusCommissionEmployee` 对象的薪水。

![](img/06ca63376760c659af4aa0e9c282068d_564_0.png)

### 软件工程观察 1.6

当程序创建一个派生类对象时，派生类构造函数会立即调用基类构造函数，基类构造函数的体执行，然后派生类的成员初始化器执行，最后派生类构造函数的体执行。如果层次结构包含超过两层，此过程会向上调用层次结构。

当派生类对象被销毁时，程序会调用该对象的析构函数。这会开始一个析构函数调用的链（或级联），其中派生类析构函数以及直接和间接基类成员的析构函数会以与构造函数执行顺序相反的顺序执行。当派生类对象的析构函数被调用时，析构函数执行其任务，然后调用层次结构中下一个基类的析构函数。此过程重复，直到最终基类的析构函数位于层次结构的顶端。然后它被从内存中移除。

![](img/06ca63376760c659af4aa0e9c282068d_564_1.png)

### 软件工程观察 1.7

假设我们创建一个派生类的对象，其中基类和派生类都通过组合包含其他类。当该派生类的对象被创建时，基类成员对象的构造函数执行，然后基类构造函数体执行，然后派生类成员对象的构造函数执行，然后派生类构造函数的体执行。派生类对象的析构函数调用顺序与它们构造函数的调用顺序相反。

默认情况下，基类构造函数、析构函数和重载赋值运算符（第10章）不会被派生类继承。派生类构造函数、析构函数和重载赋值运算符 however，可以调用基类版本。

## 11 C++11：继承基类构造函数

有时派生类构造函数只是指定与基类构造函数相同的参数并简单地将构造函数传递给基类构造。对于这种情况，C++11 允许你指定派生类应继承基类的构造函数。为此，在派生类定义中的任何位置显式使用如下形式的 `using` 声明

```
using BaseClass ::BaseClass;
```

在前述声明中，`BaseClass` 是基类的名称。在少数例外情况（如下列出）下，对于基类中的每个构造函数，编译器会生成一个调用基类构造函数的派生类构造函数。每个生成的构造函数具有与派生类相同的名称。生成的构造函数仅对派生类的额外数据成员执行默认初始化。

当你继承构造函数时：

- 每个继承的构造函数具有与其对应的基类构造函数相同的访问说明符（public、protected 或 private）。
- 默认、拷贝和移动构造函数不会被继承。
- 如果基类中通过在其原型中放置 = delete 删除了某个构造函数，则派生类中的构造函数也会被删除。
- 如果派生类没有显式定义构造函数，编译器将在派生类中生成默认构造函数。
- 基类构造函数不会被派生类中你显式定义且具有相同参数列表的构造函数所继承。相反，编译器将在派生类中生成重载的构造函数。例如，如果基类声明构造函数

```
BaseClass(int = 0, double = 0.0);
```
