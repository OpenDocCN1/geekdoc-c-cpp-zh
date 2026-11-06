

### 探索类 `BasePlusCommissionEmployee` 与类 `CommissionEmployee` 之间的相似性

类 `BasePlusCommissionEmployee`（图11.7–11.8）的大部分代码与类 `CommissionEmployee`（图11.4–11.5）的代码*相似，即使不完全相同*。例如，在类 `BasePlusCommissionEmployee` 中，*私有*数据成员 `firstName` 和 `lastName` 以及成员函数 `setFirstName`、`getFirstName`、`setLastName` 和 `getLastName` 与类 `CommissionEmployee` 中的完全一致。类 `CommissionEmployee` 和 `BasePlusCommissionEmployee` 还都包含*私有*数据成员 `socialSecurityNumber`、`commissionRate` 和 `grossSales`，以及用于操作这些成员的*获取*和*设置*函数。此外，`BasePlusCommissionEmployee` 的构造函数与类 `CommissionEmployee` 的构造函数*几乎*相同，只是 `BasePlusCommissionEmployee` 的构造函数还设置了 `baseSalary`。类 `BasePlusCommissionEmployee` 的其他新增内容是*私有*数据成员 `baseSalary` 以及成员函数 `setBaseSalary` 和 `getBaseSalary`。类 `BasePlusCommissionEmployee` 的 `toString` 成员函数与类 `CommissionEmployee` 的*几乎相同*，只是 `BasePlusCommissionEmployee` 的 `toString` 还输出了数据成员 `baseSalary` 的值。

我们真的从类 `CommissionEmployee` 中*复制*了代码，并将其*粘贴*到类 `BasePlusCommissionEmployee` 中，然后*修改*了类 `BasePlusCommissionEmployee`，使其包含基本工资和操作基本工资的成员函数。这种*复制粘贴方法*容易出错且耗时。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1483_0.png)

### 软件工程观察 11.1

*将一个类的代码复制并粘贴到另一个类中会传播同一代码的许多物理副本，并可能在整个系统中传播错误，从而造成代码维护的噩梦。为了避免重复代码（以及可能的错误），当你希望一个类“吸收”另一个类的数据成员和成员函数时，应使用继承，而不是“复制粘贴”方法。*

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1483_1.png)

### 软件工程观察 11.2

*使用继承时，层次结构中所有类的公共数据成员和成员函数都声明在一个基类中。当这些公共特性需要更改时，只需在基类中进行更改——派生类随后会继承这些更改。如果没有继承，则需要对所有包含相关代码副本的源文件进行修改。*

### 11.3.3 创建 `CommissionEmployee-BasePlusCommissionEmployee` 继承层次结构

现在，我们创建并测试一个*派生自*类 `CommissionEmployee`（图11.4–11.5）的新类 `BasePlusCommissionEmployee`（**图11.10–11.11**）。在本例中，一个 `BasePlusCommissionEmployee` 对象*是一个* `CommissionEmployee`（因为继承传递了类 `CommissionEmployee` 的能力），但类 `BasePlusCommissionEmployee` *还*具有数据成员 `baseSalary`（**图11.10**，第21行）。类定义第10行中的冒号（`:`）表示继承。关键字 `public` 表示继承的*类型*。作为派生类（通过 `public` 继承形成），`BasePlusCommissionEmployee` 继承类 `CommissionEmployee` 的*所有*成员，但构造函数除外——每个类都提供其*自己的*构造函数，这些构造函数特定于该类。（析构函数也不会被继承。）因此，`BasePlusCommissionEmployee` 的 `public` 服务包括其构造函数（第12–13行）以及从类 `CommissionEmployee` 继承的 `public` 成员函数——*虽然我们无法在* `BasePlusCommissionEmployee` 的源代码中看到这些继承的成员函数，但它们仍然是派生类 `BasePlusCommissionEmployee` 的一部分。派生类的 `public` 服务还包括成员函数 `setBaseSalary`、`getBaseSalary`、`earnings` 和 `toString`（第15–19行）。

```cpp
// Fig. 11.10: BasePlusCommissionEmployee.h
// BasePlusCommissionEmployee class derived from class
// CommissionEmployee.
#ifndef BASEPLUS_H
#define BASEPLUS_H

#include <string> // C++ standard string class
#include "CommissionEmployee.h" // CommissionEmployee class declaration

class BasePlusCommissionEmployee : public CommissionEmployee {
public:
    BasePlusCommissionEmployee(const std::string&, const std::string&,
        const std::string&, double = 0.0, double = 0.0, double = 0.0);

    void setBaseSalary(double); // set base salary
    double getBaseSalary() const; // return base salary

    double earnings() const; // calculate earnings
    std::string toString() const; // create string representation
private:
    double baseSalary; // base salary
};

#endif
```

**图11.10** `BasePlusCommissionEmployee` 类定义，表示与类 `CommissionEmployee` 的继承关系。

```cpp
// Fig. 11.11: BasePlusCommissionEmployee.cpp
// Class BasePlusCommissionEmployee member-function definitions.
#include <iomanip>
#include <iostream>
#include <sstream>
#include <stdexcept>
#include "BasePlusCommissionEmployee.h"
using namespace std;

// constructor
BasePlusCommissionEmployee::BasePlusCommissionEmployee(
    const string& first, const string& last, const string& ssn,
    double sales, double rate, double salary)
    // explicitly call base-class constructor
    : CommissionEmployee(first, last, ssn, sales, rate) {
    setBaseSalary(salary); // validate and store base salary
}

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
    // derived class cannot access the base class's private data
    return baseSalary + (commissionRate * grossSales);
}

// returns string representation of BasePlusCommissionEmployee object
string BasePlusCommissionEmployee::toString() const {
    ostringstream output;
    output << fixed << setprecision(2); // two digits of precision

    // derived class cannot access the base class's private data
    output << "base salaried commission employee: " << firstName
           << " " << lastName
           << "\nsocial security number: " << socialSecurityNumber
           << "\ngross sales: " << grossSales
           << "\ncommission rate: " << commissionRate
           << "\nbase salary: " << baseSalary;

    return output.str();
}
```

### Xcode 7.2 中 Clang/LLVM 编译器产生的编译错误

```text
BasePlusCommissionEmployee.cpp:34:25:
    'commissionRate' is a private member of 'CommissionEmployee'
BasePlusCommissionEmployee.cpp:34:42:
    'grossSales' is a private member of 'CommissionEmployee'
BasePlusCommissionEmployee.cpp:42:55:
    'firstName' is a private member of 'CommissionEmployee'
BasePlusCommissionEmployee.cpp:43:10:
    'lastName' is a private member of 'CommissionEmployee'
BasePlusCommissionEmployee.cpp:43:54:
    'socialSecurityNumber' is a private member of 'CommissionEmployee'
BasePlusCommissionEmployee.cpp:44:31:
    'grossSales' is a private member of 'CommissionEmployee'
BasePlusCommissionEmployee.cpp:45:35:
    'commissionRate' is a private member of 'CommissionEmployee'
```

**图11.11** `BasePlusCommissionEmployee` 实现文件：*基类的私有数据不能从派生类访问。*

**图11.11** 展示了 `BasePlusCommissionEmployee` 的成员函数实现。构造函数（第10–16行）引入了**基类初始化器语法**（第14行），它使用成员初始化器将参数传递给基类（`CommissionEmployee`）构造函数。C++ 要求派生类构造函数调用其基类构造函数，以初始化继承到派生类中的基类数据成员。第14行通过名称*显式*调用 `CommissionEmployee` 构造函数来实现这一点，将构造函数的参数 `first`、`last`、`ssn`、`sales` 和 `rate` 作为实参，分别初始化基类数据成员 `firstName`、`lastName`、`socialSecurityNumber`、`grossSales` 和 `commissionRate`。如果 `BasePlusCommissionEmployee` 的构造函数*没有*调用类 `CommissionEmployee` 的构造函数，编译器将发出错误。

