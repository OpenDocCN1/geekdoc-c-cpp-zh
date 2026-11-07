
-   派生类成员函数更可能被编写为依赖基类的数据。派生类应只依赖非私有基类成员函数。如果我们更改某个基类受保护数据成员的名称，就需要修改每个直接引用该数据的派生类。这样的软件被称为脆弱或易碎的。基类中的一个小改动就可能“破坏”派生类。这被称为脆弱基类问题 16，也是 C++ Core Guidelines 建议避免使用受保护数据的关键原因。17 你应当能够更改基类而无需更改其派生类。

使用私有数据成员更有利于良好的软件工程。将基类数据成员声明为私有，可以让你更改基类实现而无需更改派生类实现。这使代码更易于维护、修改和调试。

派生类只能通过继承到派生类中的非私有基类成员函数来更改私有基类数据成员的状态。如果派生类能够访问其基类的私有数据成员，那么从该派生类继承的类也能访问这些数据成员，信息隐藏的好处就会丧失。

### 受保护的基类成员函数

protected 的一种用途是定义不应暴露给客户端代码但应可在派生类中访问的基类成员函数。一个用例是使派生类能够重写基类的受保护虚函数，并从派生类的实现中调用原始基类版本。18 我们在下一节中使用了这一能力。

## 20.5 非虚接口（NVI）惯用法

非虚接口（NVI）惯用法 19,20——由 Herb Sutter（ISO C++ 标准委员会召集人）在其“Virtuality”论文 21 中首次提出——是使用类层次结构实现运行时多态的另一种方式。该惯用法侧重于将类的接口与其实现分离的良好软件工程实践。在第 10 章的运行时多态示例中，每个公有虚函数实际上服务于两个目的：

1.  它描述了类接口的一部分，指明客户端代码如何与该类的对象交互，并且
2.  它描述了类实现的一部分，使派生类能够通过重写该虚函数来自定义行为（一个实现细节）。

因此，每个公有虚函数既是类接口的一部分，也是其实现的一部分。

因此，Sutter 说每个函数应只服务于这两个目的之一。有趣的是，派生类可以重写其基类的**私有虚函数**。因此，他推荐以下在类层次结构中实现成员函数的方法：

-   **将每个虚函数设为私有**，这样它就是实现细节，而不是类公有接口的一部分。这样做可确保其唯一目的是让派生类通过重写该虚函数来自定义基类行为。如果每个派生类都需要在其重写函数定义中调用基类虚函数，则可以将该虚函数设为 protected。
-   **在基类中使用公有非虚函数来调用该虚函数。** 这个公有非虚函数将被所有派生类继承，且不能被重写，因此它只服务于一个目的——供客户端代码调用来执行任务。当在派生类对象上调用该公有非虚函数时，它会在内部调用派生类重写后的基类虚函数版本。

### 为 NVI 惯用法重构 Employee 类

按照 Sutter 的准则，我们来重构 Employee 类（图 10.11–10.12）。大部分代码相同，因此我们重点关注图 20.14 中的以下关键更改：

-   Employee 的公有 earnings（第 15 行）和 toString（第 16 行）成员函数不再声明为虚函数，而且如你将看到的，earnings 将有一个实现。函数 earnings 和 toString 现在各自只服务于一个目的——分别允许客户端代码获取 Employee 的收益和字符串表示。它们原先的第二个目的——**派生类的定制点**——现在将通过新的成员函数实现。
-   我们添加了**受保护的虚函数 getString（第 18 行）作为派生类的定制点。** 该函数由非虚函数 toString 调用。基类的**受保护成员可被其派生类访问。** 如你将看到的，我们派生类的 getString 函数将重写并调用 Employee 类的 getString。
-   我们添加了**私有纯虚函数 getPay（第 21 行）作为派生类的定制点。** 该函数由非虚函数 earnings 调用。派生类重写 getPay 以指定自定义收益计算。

```cpp
// Fig. 20.14: Employee.h
// Employee abstract base class.
#pragma once // prevent multiple inclusions of header
#include <string>
#include <string_view>

class Employee {
public:
    Employee(std::string_view name);
    virtual ~Employee() = default;

    void setName(std::string_view name);
    std::string getName() const;

    double earnings() const; // not virtual
    std::string toString() const; // not virtual
protected:
    virtual std::string getString() const; // virtual
private:
    std::string m_name;
    virtual double getPay() const = 0; // pure virtual
};
```

**图 20.14** | Employee 抽象基类。

图 20.15 包含 Employee 类成员函数实现中的几项关键更改：

-   成员函数 `earnings`（第 17 行）现在提供一个具体实现，返回调用私有纯虚函数 `getPay` 的结果。即使 `getPay` 尚未实现，也允许此调用，因为在执行时，earnings 将在 Employee 的具体派生类对象上被调用。
-   成员函数 `toString`（第 20 行）现在返回调用受保护虚函数 `getString` 的结果。
-   我们现在定义新的受保护成员函数 `getString`（第 23–25 行），用于指定 Employee 的默认字符串表示，其中包含 Employee 的名称。该函数是受保护的，以便派生类可以重写它并调用它来获取派生类字符串表示中的基类部分。

```cpp
// Fig. 20.15: Employee.cpp
// Abstract-base-class Employee member-function definitions.
// Note: No definitions are given for pure virtual functions.
#include <format>
#include "Employee.h" // Employee class definition

// constructor
Employee::Employee(std::string_view name) : m_name{name} {} // empty body
```

**图 20.15** | 抽象基类 Employee 的成员函数定义。（第 1 部分，共 2 部分。）

```cpp
// set name
void Employee::setName(std::string_view name) {m_name = name;}

// get name
std::string Employee::getName() const {return m_name;}

// public non-virtual function; returns Employee's earnings
double Employee::earnings() const {return getPay();}

// public non-virtual function; returns Employee's string representation
std::string Employee::toString() const {return getString();}

// protected virtual function that derived classes can override and call
std::string Employee::getString() const {
    return std::format("name {}", getName());
}
```

**图 20.15** | 抽象基类 `Employee` 的成员函数定义。（第 2 部分，共 2 部分。）

### 更新后的 SalariedEmployee 类

我们重构后的 `SalariedEmployee` 类（图 20.16–20.17）有几项关键更改：

-   该类的头文件（图 20.16）不再包含 `earnings` 和 `toString` 成员函数的原型。这些**公有非虚**基类函数现在继承自 `Employee`。
-   该类的私有部分现在声明对基类的私有纯虚函数 `getPay` 和受保护虚函数 `getString` 的重写（图 20.16，第 19–20 行）。函数 `getString` 在 `SalariedEmployee` 中是私有的，因为该类是 final 的，所以没有其他类可以从它派生。
-   该类的成员函数实现（图 20.17）现在包括重写函数 `getPay`（第 27 行）以返回薪水，以及重写函数 `getString`（第 30–33 行）以获取 `SalariedEmployee` 的字符串表示。注意，`SalariedEmployee` 的 `getString` 调用 `Employee` 的受保护 `getString` 来获取字符串表示的一部分。

```cpp
// Fig. 20.16: SalariedEmployee.h
// SalariedEmployee class derived from Employee.
#pragma once
#include <string> // C++ standard string class
#include <string_view>
#include "Employee.h" // Employee class definition

class SalariedEmployee final : public Employee {
public:
    SalariedEmployee(std::string_view name, double salary);
    virtual ~SalariedEmployee() = default; // virtual destructor

    void setSalary(double salary);
    double getSalary() const;
```

**图 20.16** | 从 `Employee` 派生的 `SalariedEmployee` 类。（第 1 部分，共 2 部分。）
