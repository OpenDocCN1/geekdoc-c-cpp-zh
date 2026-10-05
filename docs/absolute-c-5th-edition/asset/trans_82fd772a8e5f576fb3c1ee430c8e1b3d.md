
# 继承基础

在类定义中列出它并赋予其新的定义，就像你在派生类中添加成员函数时所做的那样。这通过 `HourlyEmployee` 类重新定义的函数 `printCheck()` 显示（显示 14.3 和 14.5）。

图 14.5 派生类 HourlyEmployee 的实现（部分 1/2）

```cpp
// 这是 hourlyemployee.cpp 文件。
// 这是 HourlyEmployee 类的实现代码。
// HourlyEmployee 类的接口定义在
// 头文件 hourlyemployee.h 中。
#include <string>
#include <iostream>
#include "hourlyemployee.h"
using std::string;
using std::cout;
using std::endl;

namespace SwitchEmployees
{
    HourlyEmployee::HourlyEmployee() : Employee(), wageRate(0), hours(0)
    {
        // 刻意留
    }

    HourlyEmployee::HourlyEmployee(const string& theName,
                                   double string theNumber, double theWageRate,
                                   double theHours)
                                   : Employee(theName, theNumber), wageRate(theWageRate),
                                     hours(theHours)
    {
        // 刻意留空
    }

    void HourlyEmployee::setRate(double newWageRate)
    {
        wageRate = newWageRate;
    }

    double HourlyEmployee::get() const
    {
        return wageRate;
    }

    void HourlyEmployee::setHours(double hoursWorked)
    {
        hours = hoursWorked;
    }
}
```

图 14.5 派生类 HourlyEmployee 的实现（部分 2/2）

```cpp
35 
36 double HourlyEmployee::getHours( ) const
37 {
38     return hours;           我们选择将 setNetPay 作为
                                     printCheck 函数的一部分，
                                     在调用时使用。在任何情况下，这是一个
                                     会计问题，而不是一个编程
                                     问题。
39 }

40 void HourlyEmployee::printCheck( )
41 {                               但请注意，C++ 允许我们在
                                     在派生类中重定义 printCheck 时
                                     去掉 const 修饰符。
42     setNetPay (hours * wageRate);

43     cout << "\n";
44     cout << "Pay to the order of " << getName() << endl;
45     cout << "The sum of " << getNetPay() << " Dollars:"
46     cout << "\n";
47     cout << "Check Stub: NOT NEGOTIABLE\n";
48     cout << "Employee Number: " << getSsn() << endl;
49     cout << " HourlyEmployee. nHours worked: " << hours
50     cout << " Rate: " << wageRate << " Pay: " << getNetPay() << endl
51     endl;
52     cout << "\n";
53 }
```

`SalariedEmployee` 是 `Employee` 类的另一个派生类示例。`SalariedEmployee` 类的接口见图 14.4，其实现见图 14.6。声明一个 `SalariedEmployee` 类型的对象具有所有 `Employee` 变量的所有成员和函数，加上 `SalariedEmployee` 类定义中给出的新成员。尽管 `SalariedEmployee` 类没有列出任何继承的变量，并且只列出了 `Employee` 类的一个函数——即 `printCheck` 函数（该函数在 `SalariedEmployee` 中更改了定义），尽管如此，`SalariedEmployee` 类仍然拥有成员变量 `name`、`ssn` 和 `netPay`，以及成员变量 `salary`。注意，你不需要为了让 `SalariedEmployee` 拥有这些成员而声明 `Employee` 类的变量和函数（例如 `name` 和 `setName`）。`SalariedEmployee` 类会自动获取这些成员，无需程序员进行任何操作。

注意，`Employee` 类包含了 `HourlyEmployee` 和 `SalariedEmployee` 两个类共同的代码。这避免了重复编写相同代码的麻烦：为 `HourlyEmployee` 类写一次，为 `SalariedEmployee` 类写一次。继承允许你重用 `Employee` 类中的代码。

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_651_0.png)

# 继承基础

图 14.6 派生类 SalariedEmployee 的实现（部分 1/2）

```cpp
// 这是 salariedemployee.cpp 文件
// 这是 SalariedEmployee 类的实现代码。
// SalariedEmployee 类的接口定义在
// 头文件 salariedemployee.h 中。
#include <iostream>
#include <string>
#include "salariedemployee.h"
using std::string;
using std::cout;
using std::endl;

namespace SavitchEmployees
{
    SalariedEmployee::SalariedEmployee() : Employee( ), salary(0)
    {
        // 刻意留空
    }

    SalariedEmployee::SalariedEmployee(const string& theName, const string& theNumber, double theWeeklyPay)
        : Employee(theName, theNumber), salary(theWeeklyPay)

    double SalariedEmployee::get() const
    {
        return salary;
    }

    void SalariedEmployee::setSalary(double newSalary)
    {
        salary = newSalary;
    }

    void SalariedEmployee::printCheck()
    {
        cout << "\n";
        cout << "Pay to the order of " << getName() << endl;
        cout << "The sum of " << getPay() << " Dollars\n";
        cout << "\n";
        cout << "Check Stub NOT NEGOTIABLE \n";
        cout << "Employee Number: " << getSsn() << endl;
}
```

图 14.6 派生类 SalariedEmployee 的实现（部分 2/2）

```cpp
42 cout << "Salaried Employee. Regular Pay: "
43 cout << salary << endl;
44 cout << "\n";
45 }
46 ///SavitchEmployees
```

# 派生类中的构造函数

基类中的构造函数不会被派生类继承，但你可以在派生构造函数的定义中调用基类的构造函数，这通常就是你需要的。派生类的构造函数以特殊的方式使用基类的构造函数。基类的构造函数会初始化从基类继承的所有数据。（此处由于原文存在大量重复的 OCR 错误文本，已根据逻辑整理为：基类的构造函数用于初始化所有从基类继承的数据，因此，派生类的构造函数以特殊的方式使用基类的构造函数。）

