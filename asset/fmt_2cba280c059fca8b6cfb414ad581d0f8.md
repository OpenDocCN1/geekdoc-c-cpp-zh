
`<< "\nbase salary: " << baseSalary;`

`return output.str();`

```
}
```

图 11.11 | `BasePlusCommissionEmployee` 实现：派生类无法访问基类的私有数据。

分别拥有数据成员 `firstName`、`lastName`、`socialNumber`、`grossSales` 和 `commissionRate`。如果 `BasePlusCommissionEmployee` 的构造函数没有显式调用 `CommissionEmployee` 的构造函数，编译器将引发错误——在这种情况下，C++ 尝试隐式调用 `CommissionEmployee` 类的默认构造函数，但该类没有构造函数。回顾第 3 章，对于任何没有显式包含构造函数的类，编译器都会提供一个无参数的默认构造函数。然而，`CommissionEmployee` 显式包含了一个构造函数，因此不再提供默认构造函数。

![](img/09cee61886647f0b1e06dc44c0065a38_554_0.png)

## 常见编程错误 II-1

当派生类构造函数调用基类构造函数时，传递给基类构造函数的参数必须与基类构造函数指定的参数数量和类型一致；否则会发生编译错误。

![](img/09cee61886647f0b1e06dc44c0065a38_554_1.png)

## 性能提示 II-1

在派生类构造函数中通过成员初始化列表中显式调用基类构造函数并初始化成员对象，可以防止重复初始化（重复初始化是指先调用默认构造函数，然后在派生类构造函数体中再次修改数据成员）。

### 访问基类私有成员导致的编译错误
编译器为 11.11 中的第 35 行生成错误，因为 `BasePlusCommissionEmployee` 的数据成员 `commissionRate` 和 `grossSales` 是私有的——由于相同的原因，派生类 `BasePlusCommissionEmployee` 在 `BasePlusCommissionEmployee` 的 `toString` 成员函数的第 44–47 行产生了额外的错误。如所示，C++ 严格执行访问私有数据成员限制，因此即使是派生类（与其基类相关）也无法访问基类的私有数据。

### 防止 BasePlusCommissionEmployee 中的错误
我们在 11.11 中使用的错误代码是为了强调派生类的成员函数无法访问类的私有数据。通过使用从 `CommissionEmployee` 继承的 `get` 成员函数，已经防止了 `BasePlusCommissionEmployee` 中的错误。例如，第 35 行本可以通过 `commissionRate` 和 `grossSales` 来访问 `CommissionEmployee` 的私有数据成员。同样，第 44–47 行可以使用适当的成员函数来获取基类成员的值。在下一个示例中，我们将展示如何通过使用 `protected` 数据来避免在本示例中遇到的错误。

### 使用 #include 在派生类头文件中包含基类头文件
注意我们在派生类头文件中 `#include` 了基类头文件（11.10 的第 8 行）。出于三个原因：首先，为了让派生类在第 10 行使用基类的名称，我们需要告诉编译器基类的存在——即 `CommissionEmployee.h` 中的类定义正是此作用。

## 11.3 基类与派生类之间的关系

第二个原因是编译器使用类定义来确定该类对象的大小（正如我们在 9.3 节中讨论过的）。创建类对象的客户端程序包含了类定义，以便编译器为对象分配适当的内存。当使用继承时，派生类的大小取决于其类定义中显式声明的数据成员以及从其直接和间接类继承的数据成员。在图 11 的第 8 行包含基类定义，允许编译器确定基类数据成员的内存需求，这些成员成为派生类对象的一部分并贡献于其总大小。

第 8 行的最后一个原因是允许编译器确定派生类是否正确地使用了基类继承的成员。例如，在图 10-11 的程序中，客户端使用基类头文件来确定派生类访问的数据成员在基类中是私有的。由于这些成员对派生类不可见，编译器产生错误。编译器还使用基类的函数原型来验证派生类的调用。

## 继承层次中的链接过程

在 9.3 节中，我们讨论了创建可执行程序的链接过程。链接过程对于使用继承的应用程序类似。假设客户端创建一个 `BasePlusCommissionEmployee` 对象，该类派自 `CommissionEmployee`。在这种情况下，客户端的代码必须与 `CommissionEmployee` 类的代码链接。这是因为链接器需要看到基类的完整定义，以解析对其成员函数的调用。

## 11.3.4 CommissionEmployee——使用数据

使用 `protected` 访问提供了 public 和 private 之间的中间级别保护。为了让 `BasePlusEmployee` 直接访问 `CommissionEmployee` 数据成员，我们可以在基类中将这些成员声明为 `protected`。

### 定义带有保护数据的基类 CommissionEmployee
`Employee`（图 11.12）现在将 `firstName`、`lastName`、`socialNumber`、`grossSales` 和 `commissionRate` 声明为 `protected`（30–35 行）而不是 private。成员函数的实现与图 11.5 相同，此处 own `CommissionEmployee.cpp`。

```
// Fig 11.12: CommissionEmployee.h
// 保护数据的 CommissionEmployee 类定义
#ifndef COMMISSION_H
#define COMMISSION_H
#include <string> // C++ 标准类
class CommissionEmployee {
public:
    CommissionEmployee(const std::string&, const std::string&, const std::string&, double = 0.0, double = 0.0);
    void setFirstName(const std::string&);
    std::string getFirstName() const;
    void setLastName(const std::string&);
    std::string getLastName() const;
    void setSecurityNumber(const std::string&);
    std::string getSecurityNumber() const;
    void setGrossSales(double);
    double getGrossSales() const;
    void setCommissionRate(double);
    double getCommissionRate() const;
    double earnings() const;
    std::string toString() const;
protected:
    std::string firstName;
    std::string lastName;
    std::string socialSecurityNumber;
    double grossSales;
    double commissionRate;
};
#endif
```

图 11.12 | `CommissionEmployee` 类定义，声明了保护数据供派生类访问。

# 11.3 基类与派生类之间的关系

## BasePlusCommissionEmployee
图 11.10–11.11 中 `BasePlusCommissionEmployee` 类的定义保持不变，因此我们不再显示。由于 `BasePlusCommissionEmployee` 继承自更新后的 `CommissionEmployee` 类（图 11.12），`BasePlusCommissionEmployee` 可以访问在 `CommissionEmployee` 类中声明为 `protected` 的数据（即数据成员 `firstName`、`lastName`、`socialSecurityNumber`、`grossSales` 和 `commissionRate`）。因此，在编译 11.11 中 `BasePlusCommissionEmployee` 的 `earnings` 和 `toString` 成员函数定义（分别为 33–36 行和 39–50 行）时，编译器不会产生错误。这显示了赋予派生类访问 `protected` 基类数据成员的权限。派生类的对象可以访问该派生类任何直接类中的 `protected` 成员。

`BasePlusCommissionEmployee` 没有继承 `CommissionEmployee` 的构造函数。然而，`BasePlusCommissionEmployee` 的构造函数（图 11.11，第 10–14 行）使用成员初始化语法（第 14 行）显式调用了 `BasePlusCommissionEmployee` 的构造函数。记住，`BasePlusCommissionEmployee` 的构造函数必须显式调用 `CommissionEmployee` 类的构造函数，因为 `CommissionEmployee` 不包含可以调用的默认构造函数。

### 测试修改后的 BasePlusCommissionEmployee 类
为了测试类层次结构，我们重用了图 11.9 中的测试程序。如图 11.13 所示，输出结果与图 11.9 相同。

通过 `get` 函数获取的员工信息：

- 名字是 Bob
- 姓是 Lewis
- 社会安全号是 333-33-3333
- 总销售额为 $5000.00
- 佣金率为 0.04
- 基本薪水为 300.00

来自 `toString` 函数更新的员工信息：

- 带底薪的佣金员工：Bob Lewis
- 社会安全号：333-33-3333
- 总销售额：$5000.00
- 佣金率：0.04
- 基本薪水：1000.00

员工收入：$1200.00

> 图 11.13 | 从派生类可以访问保护的基类数据。

我们最初在没有使用继承的情况下创建了 `BasePlusCommissionEmployee` 类，然后使用继承创建了此版本的 `BasePlusCommissionEmployee`；然而，这两个类提供了相同的功能。派生类 `BasePlusCommissionEmployee` 的代码（即头文件和实现文件）比非继承版本的类代码要短得多，因为继承版本吸收了来自 `CommissionEmployee` 的大部分功能，而非继承版本没有吸收任何功能。此外，现在 `CommissionEmployee` 类中仅有一份声明和定义的 `Commission-Employee` 功能副本。这使得源代码更易维护和调试，因为与 `CommissionEmployee` 相关的源代码仅存在于 `CommissionEmployee.h` 和 `CommissionEmployee.cpp` 文件中。

## 使用保护 数据的注意事项
在本示例中，我们将基类数据成员声明为 `protected`，以便派生类可以修改这些数据。继承 `protected` 数据会稍微提高性能，因为我们可以直接访问成员，而无需承担调用 `get` 成员函数的开销。

## 软件工程观察 11.3
![](img/09cee61886647f0b1e06dc44c0065a38_558_0.png)

在某些情况下，使用 `private` 数据成员以鼓励良好的软件工程，并将代码优化留给编译器。你的代码将更易维护和调试。

使用 `protected` 数据成员会产生两个问题。首先，派生类对象没有设置基类数据成员数值的成员函数。无效的值可以很容易地分配给 `protected` 数据成员，导致对象处于不一致状态——例如，正如 `CommissionEmployee` 中声明的 `groupSales` 数据组，派生类对象可以给 `groupSales` 分配一个负值。使用 `protected` 数据的第二个问题是，派生类的成员函数更容易被写成依赖于基类的实现。派生类应该只依赖于基类服务（即非 `private` 成员函数），而不依赖于基类的实现。如果基类中使用 `protected` 数据成员，如果基类实现发生变化，我们可能需要修改所有数据成员名称（从 `firstName` 和 `lastName` 改为 `first` 和 `last`），然后我们必须对所有派生类直接引用这些基类数据成员的地方进行修改。这种软件是脆弱或易碎的，因为基类的微小变化就会“弄坏”派生类的实现。你应该能够在更改基类实现的同时，仍向派生类提供相同的服务。当然，如果基类服务发生变化，我们必须重新实现派生类——良好的面向对象设计试图防止这种情况。

![](img/09cee61886647f0b1e06dc44c0065a38_558_1.png)

## 软件工程观察 11.4
当基类应仅向派生类和朋友提供服务（即非 `private` 成员函数）时，使用 `protected` 访问限定符是合适的。

## 软件工程观察 11.5
将基类数据成员声明为 `private`（而不是声明为 `protected`）可以让你。

## 11.3 基类与派生类之间的关系
### 基类与派生类
我们再次审视了该层次结构，这次使用了软件工程实践。派生类 `BasePlusCommissionEmployee` 的代码（即头文件和实现文件）比非继承版本的类代码要短得多，因为继承版本吸收了来自 `CommissionEmployee` 的大部分功能，而非继承版本没有吸收任何功能。此外，现在 `CommissionEmployee` 类中仅有一份声明和定义的 `Commission-Employee` 功能副本。这使得源代码更易维护和调试，因为与 `CommissionEmployee` 相关的源代码仅存在于 `CommissionEmployee.h` 和 `CommissionEmployee.cpp` 文件中。

## CommissionEmployee 实现
```cpp
#include <iostream>
#include <string>
#include <stdexcept>
#include <sstream>
#include <iomanip>
using namespace std;
class CommissionEmployee {
private:
    string firstName;
    string lastName;
    string socialSecurityNumber;
    double grossSales;
    double commissionRate;
public:
    CommissionEmployee(const string& first, const string& last, const string& ssn, double sales, double rate)
        : firstName(first), lastName(last), socialSecurityNumber(ssn) {
        setSales(sales);
        setRate(rate);
    }
    string getFirstName() const { return firstName; }
    string getLastName() const { return lastName; }
    string getSocialSecurityNumber() const { return socialSecurityNumber; }
    double getGrossSales() const { return grossSales; }
    double getCommissionRate() const { return commissionRate; }
    void setFirstName(const string& first) { firstName = first; }
    void setLastName(const string& last) { lastName = last; }
    void setSocialSecurityNumber(const string& ssn) { socialSecurityNumber = ssn; }
    void setSales(double sales) {
        if (sales < 0.0) {
            throw invalid_argument("Gross sales must be >= 0.0");
        }
        grossSales = sales;
    }
    void setRate(double rate) {
        if (rate < 0.0 || rate > 1.0) {
            throw invalid_argument("Commission rate must be between 0.0 and 1.0");
        }
        commissionRate = rate;
    }
    double earnings() const {
```
