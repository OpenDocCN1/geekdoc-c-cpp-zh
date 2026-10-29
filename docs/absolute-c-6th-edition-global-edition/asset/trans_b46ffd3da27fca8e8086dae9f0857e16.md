

设置和更改姓名和社会安全号码对薪资员工和小时工来说是相同的。

在 C++ 中，你可以定义一个名为 Employee 的类，其中包含所有员工，无论是薪资还是小时工，然后使用该类来定义小时工类和薪资员工类。

类 Employee 还将包含操作类 Employee 数据字段的成员函数。显示 14.1 和 14.2 显示了类 Employee 的一种可能定义。

## Display 14.1 Interface for the Base Class Employee

```
//This is the header file employee.h.
//This is the interface for the class Employee.
//This is primarily intended to be used as a base class to derive
//classes for different kinds of employees.
#ifndef EMPLOYEE_H
#define EMPLOYEE_H

#include <string>
using std::string;

namespace SavitchEmployees
{

class Employee
{
public:
Employee();
Employee(const string& theName, const string& theSsn);
string getName() const;
string getSsn() const;
double getNetPay() const;
void setName(const string& newName);
void setSsn(const string& newSsn);
void setNetPay(double newNetPay);
void printCheck() const;
private:
string name;
string ssn;
double netPay;
};

};//SavitchEmployees

#endif //EMPLOYEE_H
```

## Display 14.2 Implementation for the Base Class Employee (part 1 of 2)

```
//This is the file employee.cpp.
//This is the implementation for the class Employee.
//The interface for the class Employee is in the header file employee.h.
#include <string>
#include <cstdlib>
#include <iostream>
#include "employee.h"
using std::string;
using std::cout;

namespace SavitchEmployees
{
    Employee::Employee() : name("No name yet"), ssn("No number yet"), netPay(0)
    {
        //deliberately empty
    }

    Employee::Employee(const string& theName, const string& theNumber)
        : name(theName), ssn(theNumber), netPay(0)
    {
        //deliberately empty
    }

    string Employee::getName() const
    {
        return name;
    }

    string Employee::getSsn() const
    {
        return ssn;
    }

    double Employee::getNetPay() const
    {
        return netPay;
    }

    void Employee::setName(const string& newName)
    {
        name = newName;
    }

    void Employee::setSsn(const string& newSsn)
```

## Display 14.2 Implementation for the Base Class Employee (part 2 of 2)

```
{
    ssn = newSsn;
}

void Employee::setNetPay (double newNetPay)
{
    netPay = newNetPay;
}

void Employee::printCheck( ) const
{
    cout << "\nERROR: printCheck FUNCTION CALLED FOR AN \n"
         << "UNDIFFERENTIATED EMPLOYEE. Aborting the program.\n"
         << "Check with the author of the program about this bug.\n";
    exit(1);
}
}//SavitchEmployees
```

你可以有一个（未区分的）Employee 对象，但我们定义类 Employee 的原因是为了能够为不同种类的员工定义派生类。特别是，函数 printCheck 将始终在派生类中更改其定义，以便不同种类的员工可以有不同种类的支票。这在类 Employee 的函数 printCheck 的定义中有所体现（显示 14.2）。为这种（未区分的）Employee 打印支票意义不大。我们对该员工一无所知。因此，我们实现了类 Employee 的函数 printCheck，以便如果为基类 Employee 对象调用 printCheck，程序将以错误消息停止。正如你将看到的，派生类将拥有足够的信息来重新定义函数 printCheck 以生成有意义的员工支票。

派生自类 Employee 的类将自动拥有类 Employee 的所有成员变量（name、ssn 和 netPay）。派生自类 Employee 的类还将拥有类 Employee 的所有成员函数，例如 printCheck、getName、setName 和显示 14.1 中列出的其他成员函数。这通常被表述为派生类继承成员变量和成员函数。

类 Employee 的两个派生类的接口文件在显示 14.3（HourlyEmployee）和显示 14.4（SalariedEmployee）中给出。我们将类 Employee 和两个派生类放在同一个命名空间中。C++ 不要求它们在同一个命名空间中，但由于它们是相关的类，将它们放在同一个命名空间中是有意义的。我们将首先讨论派生类 HourlyEmployee，给出在显示 14.3 中。

## Display 14.3 Interface for the Derived Class HourlyEmployee

```
//This is the header file hourlyemployee.h.
//This is the interface for the class HourlyEmployee.
#ifndef HOURLYEMPLOYEE_H
#define HOURLYEMPLOYEE_H

#include <string>
#include "employee.h"

using std::string;

namespace SavitchEmployees
{

class HourlyEmployee : public Employee
{
public:
    HourlyEmployee();
    HourlyEmployee(const string& theName, const string& theSsn, double theWageRate, double theHours);
    void setRate(double newWageRate);
    double getRate() const;
    void setHours(double hoursWorked);
    double getHours() const;
    void printCheck();
private:
    double wageRate;
    double hours;
};

}//SavitchEmployees

#endif //HOURLYEMPLOYEE_H
```

请注意，派生类的定义与任何其他类定义开始相同，但在类定义的第一个行添加冒号、保留字 public 和基类名，如以下（来自显示 14.3）所示：

```
class HourlyEmployee : public Employee
{
```

派生类（如 HourlyEmployee）自动接收基类（如 Employee）的所有成员变量和成员函数，并且可以添加额外的成员变量和成员函数。

类 HourlyEmployee 的定义没有提到成员变量 name、ssn 和 netPay，但类 HourlyEmployee 的每个对象都有

> 如果你想更改函数的定义，则只列出继承的成员函数的声明。

## Display 14.4 Interface for the Derived Class SalariedEmployee

```
//This is the header file salariedemployee.h.
//This is the interface for the class SalariedEmployee.
#ifndef SALARIEDEMPLOYEE_H
#define SALARIEDEMPLOYEE_H

#include <string>
#include "employee.h"

using std::string;

namespace SavitchEmployees
{

class SalariedEmployee : public Employee
{
public:
    SalariedEmployee();
    SalariedEmployee(const string& theName, const string& theSsn,
                    double theWeeklySalary);
    double getSalary() const;
    void setSalary(double newSalary);
    void printCheck();
private:
    double salary;//weekly
};
}//SavitchEmployees

#endif //SALARIEDEMPLOYEE_H
```

成员变量名为 name、ssn 和 netPay。成员变量 name、ssn 和 netPay 是从类 Employee 继承的。类 HourlyEmployee 声明了两个额外的成员变量名为 wageRate 和 hours。因此，类 HourlyEmployee 的每个对象都有五个成员变量名为 name、ssn、netPay、wageRate 和 hours。请注意，派生类（如 HourlyEmployee）的定义仅列出添加的成员变量。基类中定义的成员变量不会被提及。它们会自动提供给派生类。

正如它继承类 Employee 的成员变量一样，类 HourlyEmployee 也继承了类 Employee 的所有成员函数。因此，类 HourlyEmployee 继承了成员函数 getName、getSsn、getNetPay、setName、setSsn、setNetPay 和 printCheck 来自类 Employee。

## Inherited Members

派生类自动拥有基类的所有成员变量和所有普通成员函数。（正如本章后面讨论的那样，有一些专门的成员函数，如构造函数，并不是自动继承的。）这些来自基类的成员被称为继承。这些继承的成员函数和继承的成员变量，除了一个例外外，在派生类的定义中没有提及，但自动成为派生类的成员。如文中所述，如果你想更改继承的成员函数的定义，则在派生类的定义中提及该继承的成员函数。

除了继承的成员变量和成员函数外，派生类还可以添加新的成员变量和新的成员函数。新的成员变量和新成员函数的声明列在类定义中。例如，派生类 HourlyEmployee 添加了两个成员变量 wageRate 和 hours，并添加了新的成员函数 setRate、getRate、setHours 和 getHours。这在显示 14.3 中显示。请注意，除非你想更改这些定义，否则不会给出继承的成员函数的声明，这一点我们稍后会讨论。现在，不要担心派生类构造函数定义的细节。我们将在下一小节讨论构造函数。

在派生类的实现文件中，例如显示 14.5 中 HourlyEmployee 的实现，给出所有添加的成员函数的定义。请注意，除非在派生类中更改了成员函数的定义，否则不会给出继承的成员函数的定义，我们接下来讨论这一点。

## Parent and Child Classes

在讨论派生类时，常用来自家庭关系的术语。一个基类通常被称为父类。派生类则被称为子类。这使得继承的语言非常流畅。例如，我们可以说子类从其父类继承成员变量和成员函数。这种类比通常会更进一步。一个类的父类的父类（或其他任意次数的“父类”迭代）通常被称为祖先类。如果类 A 是类 B 的祖先，则类 B 通常被称为类 A 的后代。

继承的成员函数的定义可以在派生类的定义中更改，以便在派生类中具有与基类中不同的含义。这称为重新定义继承的成员函数。例如，成员函数 printCheck() 在派生类 HourlyEmployee 的定义中被重新定义。要重新定义成员函数定义，只需

