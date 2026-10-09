
```cpp
        return commissionRate * grossSales;

    }

    string toString() const {

        ostream outputstream;

        outputstream << fixed << setprecision(2);

        outputstream << "commission employee: "

            << getFirstName() << " " << getLastName()

            << "\nsocial security number: " << getSocialSecurityNumber()

            << "\ngross sales: " << getGrossSales()

            << "\ncommission rate: " << getCommissionRate();

        return outputstream.str();

    }

};

class BasePlusCommissionEmployee : public CommissionEmployee {

protected:

    double baseSalary;

public:

    BasePlusCommissionEmployee(const string& first, const string& last, const string& ssn, double sales, double rate, double base)

        : CommissionEmployee(first, last, ssn, sales, rate), baseSalary(base) {}

    double getBaseSalary() const { return baseSalary; }

    void setBaseSalary(double base) { baseSalary = base; }

    double earnings() const {

        return CommissionEmployee::earnings() + baseSalary;

    }

    string toString() const {

        ostream outputstream;

        outputstream << fixed << setprecision(2);

        outputstream << "base-salaried commission employee: "

            << getFirstName() << " " << getLastName()

            << "\nsocial security number: " << getSocialSecurityNumber()

            << "\ngross sales: " << getGrossSales()

            << "\ncommission rate: " << getCommissionRate()

            << "\nbase salary: " << getBaseSalary();

        return outputstream.str();

    }

};
```

*(注：提供的原始代码块严重碎片化并与页面文本交织。我根据源材料中的描述对其进行了逻辑重构。)*

> 图 11.14 | `CommissionEmployee` 类实现：操作其私有数据的 `CommissionEmployee` 类成员函数。（第 2 部分，共 2 部分。）

## 11.3 基类与派生类之间的关系

在构造函数以及成员函数 `earnings`（图 11.14，70–72行）和 `toString`（75–84行）的体内，我们调用了类的私有数据成员。如果我们决定更改数据成员的名称，`earnings` 和 `toString` 的定义不需要修改——只有直接操作数据数据的 get 和 set 成员函数的定义需要更改。这些更改完全发生在基类内部——不需要对派生类进行任何更改。这种将更改影响局部化的是一种良好的软件工程实践。

## 性能提示 11.2

使用成员函数访问数据成员的值可能比直接访问数据稍慢。然而，如今的优化编译器会隐式地执行优化（例如内联和 get 成员函数调用）。您应该编写符合良好软件工程原则的代码，并将优化交给编译器。一个好的规则是：“不要猜疑编译器”。

![](img/09cee61886647f0b1e06dc44c0065a38_561_0.png)

### 类 `BasePlusCommissionEmployee` 的成员函数定义

类 `BasePlusCommissionEmployee` 继承了它的公共成员函数，并通过继承的成员函数访问基类的私有成员。该类的头文件与图 11.10 不变。该类在成员函数实现上有几处更改（图 11.15），这与该类的之前的版本（图 11.10–11.11）不同。成员函数 `earnings`（图 11.15，32–34行）和 `toString`（37–42行）分别调用成员函数 `getBaseSalary` 来获取基本工资值，而不是直接访问 `baseSalary`。这使得 `earnings` 和 `toString` 受到数据成员 `baseSalary` 实现可能变化的影响。如果我们决定重命名数据成员 `baseSalary` 或更改其类型，则只需要更改成员函数 `setBaseSalary` 和 `getBaseSalary`。

```cpp
// Fig.11.15: BasePlusCommissionEmployee.cpp
// 类 BasePlusCommissionEmployee 成员函数定义.
#include <stdexcept>
#include <iostream>
#include "BasePlusCommissionEmployee.h"
using namespace std;
// 构造函数
BasePlusCommissionEmployee::BasePlusCommissionEmployee(
const string& first, const string& last, const string& ssn,
double sales, double rate, double salary)
// 显式调用基类构造函数
: CommissionEmployee(first, last, ssn, rate) {
  setBaseSalary(salary); // 验证并存储基本工资
}
```

**图 11.15 | 继承自 `BasePlusCommissionEmployee` 类的 `BasePlusCommissionEmployee` 类无法直接访问类的私有数据。（2部分的1部分）**

```cpp
17 // 设置基本工资
18 void BasePlusCommissionEmployee::setBaseSalary(double salary) {
19   if (salary < 0.0) {
20     throw invalid_argument("Salary must be >= 0.0");
21   }
23
24
   baseSalary = salary;
25 }
26
27 // 返回基本工资
28 double BasePlusCommissionEmployee::getBaseSalary() const {
29   return baseSalary;
30 }
31
32 // 计算收益
33 double BasePlusCommissionEmployee::earnings() const {
34   return getBaseSalary() + CommissionEmployee::earnings();
35 }
36
37 // 返回 BasePlusCommissionEmployee 的字符串表示
38 string BasePlusCommissionEmployee::toString() const {
39   ostream output;
40   output << "base-salaried " << CommissionEmployee::toString();
41   output << "\nsalary: " << getBaseSalary();
42   return output.str();
43 }
```

**图 11.15** | 继承自 `CommissionEmployee` 类的 `BasePlusCommissionEmployee` 类无法直接访问类的数据。（2部分的2部分）

### `BasePlusCommissionEmployee` 成员函数 `earnings`

类 `BasePlusCommissionEmployee` 的 `earnings` 函数（图 11.15，32–34行）重写了 `CommissionEmployee` 类的 `earnings` 成员函数（图 11.14，70–72行），以计算 `BasePlusCommissionEmployee` 的收益。`BasePlusCommissionEmployee` 版本的 `earnings` 通过通过调用基类 `CommissionEmployee` 的函数来获取仅基于佣金的收益部分，如 11.15 第 33 行所示的表达式 `CommissionEmployee::earnings()`。`BasePlusCommissionEmployee` 的 `earnings` 函数将基本工资加到该值上，以计算员工的总收益。注意从派生类中调用重定义的基类成员函数的语法——在基类成员函数之前放置类名和作用域解析运算符 (`::`)。这种函数调用是一种良好的软件工程实践；回想第 9 章的内容，如果一个对象的成员函数执行了另一个对象所需的操作，我们应该调用该成员函数，而不是重复其代码体。通过让 `BasePlusCommissionEmployee` 的 `earnings` 函数调用 `CommissionEmployee` 的 `earnings` 函数来计算 `BasePlusCommissionEmployee` 对象的部分收益，我们避免了代码重复并减少了代码维护问题。

## 11.4 派生类中的构造函数和析构函数

![](img/09cee61886647f0b1e06dc44c0065a38_563_0.png)

## 常见编程错误 11.2

当在派生类中重定义基类成员函数时，派生类版本通常会调用基类版本来完成额外工作。在引用基类成员函数时未使用基类名的 `::` 运算符会导致无限递归，因为派生类成员函数将调用它自己。

### `BasePlusCommissionEmployee` 成员函数 `toString`

同样，`BasePlusCommissionEmployee` 的 `toString` 函数（图 11.15，37–42行）定义了 `BasePlusCommissionEmployee` 的 `toString` 函数（图 11.14，75–84行），以输出正确的带薪佣金员工信息。新版本显示“base-salaried”，随后是通过使用限定名 `CommissionEmployee::toString`（图 11.15 第39行）调用 `CommissionEmployee` 的 `toString` 成员函数返回的信息——这将返回一个包含“commission employee”和 `CommissionEmployee` 私有数据成员值的字符串。然后 `BasePlusCommissionEmployee` 的 `toString` 函数输出 `BasePlusCommissionEmployee` 对象的剩余部分（即类 `BasePlusCommissionEmployee` 的基本工资值）。

### 测试修改后的类层次结构

再次，此示例使用了图 11.9 中的 `BasePlusCommissionEmployee` 测试程序并产生相同的输出。每个“带薪员工”类都经过了良好的设计。通过使用继承并调用隐藏数据且确保一致性的成员函数，我们高效且有效地构建了一个工程良好的类。

### `CommissionEmployee`–`BasePlusCommissionEmployee` 示例总结

在本节中，你看到了一组演进的示例，这些示例旨在测试使用继承进行良好软件工程的关键能力。你学习了如何使用继承创建派生类，如何保护基类成员，以及如何重定义基类函数以提供更适合派生类对象的版本。此外，你还学习了如何应用第 9 章和本的软件工程技术来创建易于维护、修改和调试的类。

派生类对象继承的成员。在我们一直在研究的 `CommissionEmployee-Base-PlusCommissionEmployee` 层次结构中，当程序创建一个 `BasePlusCommissionEmployee` 对象时，会调用 `CommissionEmployee` 的构造函数。由于 `CommissionEmployee` 类位于该层次结构的顶端，它的构造函数负责初始化作为 `Base-Plus-CommissionEmployee` 对象一部分的私有 `CommissionEmployee` 数据成员。当 `CommissionEmployee` 的构造函数执行完毕后，它会将控制权交还给 `BasePlusCommissionEmployee` 的构造函数，后者负责初始化 `BasePlusCommissionEmployee` 对象的工资。

## 软件工程观察 11.6

当程序创建一个派生类对象时，派生类构造函数会立即调用基类构造函数，接着执行基类构造函数的体体，然后执行派生类的成员初始化器，最后执行派生类构造函数的体体。如果层次结构包含两个以上的级别，这一过程将沿层次结构向上级联。

当派生类对象被销毁时，程序会调用该对象的析构函数。当派生类对象被析构时，会开始一个析构函数调用链（或级联），其中派生类析构函数以及基类和间接基类成员的析构函数按照构造函数执行顺序的反序执行。当派生类对象的析构函数被调用时，析构函数执行其任务，并调用层次结构上下一个基类的析构函数。这一过程不断重复，直到层次结构顶端的最终基类的析构函数从内存中移除。

## 软件工程观察 11.7

假设我们创建一个派生类对象，其中基类和派生类都（通过组合）包含了其他类的对象。当该派生类的对象被创建时，首先执行基类成员对象的构造函数，然后执行基类构造函数的体体，接着执行派生类成员对象的构造函数，最后执行派生类构造函数的体体。派生类对象的析构函数调用顺序与其相应的构造函数调用的顺序相反。

默认情况下，基类的构造函数、析构函数和重载赋值运算符（第 10 章）不被派生类继承。然而，派生类的构造函数、析构函数和重载赋值运算符可以调用基类的版本。

## 11.4 C++11：继承基类构造函数

有时，派生类构造函数仅指定与基类构造函数相同的参数，并简单将构造函数传递给基类构造函数。对于此类情况，C++11 允许你指定派生类应该继承基类的构造函数。要实现这一点，可以在派生类定义的任何地方显式使用如下形式的 `using` 声明

```
using BaseClass::BaseClass;
```

在前面的声明中，`BaseClass` 是基类的名称。除少数例外外（见下文），对于基类中的每个构造函数，编译器都会生成一个派生类构造函数，该函数调用相应的基类构造函数。每个生成的构造函数都与派生类同名。生成的构造函数仅对派生类的额外数据成员执行默认初始化。

当你继承构造函数时：

- 每个生成的构造函数与其对应的基类构造函数具有相同的访问修符（public、protected 和 private）。
- 默认构造函数、拷贝构造函数和移动构造函数不被继承。
- 如果基类通过在原型中放置 `= delete` 删除了构造函数，则派生类中的该构造函数也会被删除。
- 如果派生类没有显式定义构造函数，编译器将在派生类中生成一个默认构造函数。
- 在派生类参数列表中显式定义的构造函数不会继承基类构造函数。
- 基类构造函数的默认参数不被继承。相反，编译器会在派生类中生成重载构造函数。例如，如果基类声明了构造函数

```
BaseClass(int = 0, double = 0.0);
```

编译器将生成以下两个没有默认参数的派生类构造函数

```
DerivedClass();
DerivedClass(int);
DerivedClass(int, double);
```

## 11.5 公有、保护和私有继承

假设我们创建一个派生类对象，其中基类和派生类都（通过组合）包含了其他类的对象。当该派生类的对象被创建时，首先执行基类成员对象的构造函数，然后执行基类构造函数的体体，接着执行派生类成员对象的构造函数，最后执行派生类构造函数的体体。派生类对象的析构函数调用顺序与其相应的构造函数调用的顺序相反。

在默认情况下，基类的构造函数、析构函数和重载赋值运算符（第 10 章）不被派生类继承。然而，派生类的构造函数、析构函数和重载赋值运算符可以调用基类的版本。

## 11.4 C++11：继承基类构造函数

有时，派生类构造函数仅指定与基类构造函数相同的参数，并简单将构造函数传递给基类构造函数。对于此类情况，C++11 允许你指定派生类应该继承基类的构造函数。要实现这一点，可以在派生类定义的任何地方显式使用如下形式的 `using` 声明

```
using BaseClass::BaseClass;
```
