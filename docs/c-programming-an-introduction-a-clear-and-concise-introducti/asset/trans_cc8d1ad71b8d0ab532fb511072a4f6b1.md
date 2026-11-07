
## 代码中的继承示例

为了演示 C++ 中继承的工作原理，我们将开发一组类，模拟公司中不同类型员工之间的关系。

出于演示目的，我们将定义公司中的三种员工类型——普通员工、主管和经理。我们将让 Employee 类作为基类，Supervisor 类和 Manager 类将作为派生类。

首先，让我们定义 Employee 类。为了避免事情变得过于复杂，我们将所有类定义在同一个程序中。我们不提倡在“真实世界”的程序中这样做，但如果所有类定义都在同一个地方，会让我们的讨论更容易理解。

以下是对 Employee 类进行定义以及测试该实现的测试程序的初步尝试：

```cpp
// EmployeeClass.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <string>
using namespace std;

class Employee
{
private:
        string empName;
        double pay;

public:
        Employee(string name, double payRate)
        {
                empName = name;
                pay = payRate;
        }

        string getName()
        {
            return empName;
        }

        double getPay()
        {
            return pay;
        }

        double grossPay(int hours)
        {
            return pay * hours;
        }
};

int main(array<System::String ^> ^args)
{
    Employee emp1("Mary Smith", 15.0);
    cout << "Employee name: " << emp1.getName() << endl;
    cout << "Pay rate: " << emp1.getPay() << endl;
    cout << "Gross pay: " << emp1.grossPay(40) << endl;
    Console::ReadKey();
    return 0;
}
```

该程序的输出是：

```
Employee name: Mary Smith
Pay rate: 15
Gross pay: 600
```

现在我们可以从 Employee 类派生 Manager 类了。当我们从基类派生一个类时，我们只想实现派生类中出现的不同成员和方法，并复用基类中与派生类共享的成员和方法。这意味着我们希望继续在 Manager 类中使用 Employee 类的数据成员，并添加任何不同的属性，例如经理通常是领薪员工而不是计时员工这一事实。我们可以通过包含一个布尔变量 isSalaried 将此事实添加到 Manager 类中，然后调整 grossPay() 方法：如果对象是经理，则返回薪金；如果对象是普通员工，则返回薪金乘以工作小时数。

我们几乎准备好实现 Manager 类了，但有一个主要问题。Employee 类的数据成员是私有成员，这意味着它们的值只能在类定义内部访问。我们可以为基类使用一种访问修饰符，使类的成员和方法可被派生类访问：protected。这种访问修饰符允许派生类访问基类的成员和方法，但不允许任何其他代码（例如测试程序）访问。

一旦我们将基类的成员和方法设为受保护，就必须告诉编译器派生类正在从基类继承成员和方法。为此，在派生类定义的第一行同一行中，写一个冒号，后跟关键字 public 和基类名称，以包含对基类的引用，如下所示：

```cpp
class Manager : public Employee
```

现在我们可以重新定义 Employee 类并定义 Manager 类了。以下是完整程序：

```cpp
// EmployeeClass.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
#include <string>
using namespace std;

class Employee
{
protected:
    string empName;
    double pay;

public:
    Employee(string name, double payRate)
    {
        empName = name;
        pay = payRate;
    }

    string getName()
    {
        return empName;
    }

    double getPay()
    {
        return pay;
    }

    double grossPay(int hours)
    {
        return pay * hours;
    }
};

class Manager : public Employee
{
protected:
    bool salaried;

public:
    Manager(string name, double payRate,
            bool isSalaried)
        : Employee(name, payRate)
    {
        salaried = isSalaried;
    }

    bool getSalaried()
    {
        return salaried;
    }

    double grossPay(double hours)
    {
        if (salaried)
            return pay;
        else
            return Employee::grossPay(hours);
    }
};

int main(array<System::String ^> ^args)
{
    Employee emp1("Mary Smith", 15.0);
    cout << "Employee name: " << emp1.getName()
         << endl;
    cout << "Pay rate: " << emp1.getPay() << endl;
    cout << "Gross pay: " << emp1.grossPay(40)
         << endl;
    Manager emp2("Liz Warren", 1500, true);
    cout << "Employee name: " << emp2.getName()
         << endl;
    cout << "Pay rate: " << emp2.getPay() << endl;
    cout << "Gross pay: " << emp2.grossPay(40)
         << endl;
    Console::ReadKey();
    return 0;
}
```

我们做的第一个更改是将 Employee 类数据成员的访问修饰符从 private 改为 protected。以下是该部分代码：

```cpp
class Employee
{
protected:
    string empName;
    double pay;
```

必须进行此更改，以便 Manager 类可以访问 Employee 类的数据成员。因此，我们不必在 Manager 类中重新声明 Employee 类的数据成员。

Manager 类的构造函数也利用了继承，它使用 Employee 类定义中的成员赋值来设置员工姓名和员工薪金。让我们只关注构造函数，看看它是如何工作的：

```cpp
Manager(string name, double payRate,
        bool isSalaried)
    : Employee(name, payRate)
{
    salaried = isSalaried;
}
```

构造函数的参数列表包括所有数据成员的参数。然而，在列表之后，有一个冒号，后跟对 Employee 类基类构造函数的调用。可以把它看作函数调用。在代码中的这一点，编译器将控制权转移到为 Employee 类构造函数定义的代码。这是代码复用的经典示例，也是继承最重要的特性之一。没有理由包含以下语句：

```
empName = name;
pay = payRate;
```

因为我们已经在基类中编写了它们。

构造函数体的其余部分将最后一个参数赋给 Manager 类的新数据成员，即布尔数据成员 salaried。

另一段需要解释的代码是 grossPay() 方法。以下是其定义：

```cpp
double grossPay(double hours)
{
    if (salaried)
        return pay;
    else
        return Employee::grossPay(hours);
}
```

此方法首先通过测试 salaried 变量来检查员工是否领取薪金。如果是，该方法只返回 pay 中的值。如果员工不领薪金，则该方法计算总工资。由于我们已经在 Employee 类中执行了此计算，因此没有理由在 Manager 类中重复它。相反，我们只需像这样调用 Employee 类中的该方法：

`Employee::grossPay(hours)`

如果我们只写：

`grossPay(hours)`

编译器会感到困惑并再次调用同一个方法，导致永无止境的递归调用，最终使程序崩溃。此示例演示了在 C++ 中使用继承如何帮助减少必须编写的代码量，从而使代码更易于使用和调试。

### 组合

继承是在派生类中复用基类的代码。*组合* 是在一个类的定义中使用其他类。组合用于描述 *“有一个”* 关系。一条线有一个点（准确地说，是两个点）；一个圆有一个半径；一辆汽车有一个发动机。这些都是一个对象由其他对象组成的例子。

许多看似适合用继承解决的编程问题，实际上用组合解决更好。继承，尤其是涉及长链派生类时，众所周知很难正确实现。
