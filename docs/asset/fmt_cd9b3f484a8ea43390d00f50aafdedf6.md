
> Fig. 9.17 | const objects and const member functions. (Part 2 of 2 )

构造函数必须是 `non-const` 成员函数，但它仍然可以用来初始化 `const` 对象（图 9.17，Recall）。从 9.6 可知 `Time` 构造函数的定义调用了另一个 `non-const` 成员函数——`setTime` 来执行 `Time` 对象的初始化。在 `const` 对象初始化过程中从构造函数调用 `non-const` 成员函数是允许的。

图 9.17 中的第 15 行显示了一个编译错误，即使类 `Time` 的成员函数 `toStandardString` 在其被调用的对象上不修改对象。成员函数不修改对象这一事实是不够的——该函数必须声明为 `const`。

## 9.12 组合：类成员对象

`AlarmClock` 对象需要知道何时响铃，为什么不将 `Time` 对象作为 `AlarmClock` 类的成员包含在内？这种软件能力称为组合（聚合），有时也被称为 `has-relationship`——一个类可以拥有其他类的对象作为成员。⁵

你实际上从第 3 章就开始使用组合了。在该章的示例中，类 `Account` 包含一个 `string` 对象作为数据成员。

之前，我们看到如何在 `main` 中创建对象时向其构造函数传递参数。现在我们展示类的构造函数如何通过成员初始化器向成员对象构造函数传递参数。

⁵ 正如你在第 11 章中看到的，类也可以从提供新类可用的属性和行为的其他类派生——这称为继承。

## 软件工程观察 9.8

数据成员是按照它们在类定义中声明的顺序构造的（而不是按照它们在构造函数成员初始化器列表中列出的顺序），并且在封闭类对象构造之前完成。

下一个程序使用类 `Date`（图 9.18-9.19）和 `Employee`（图 9.20-9.21）来演示组合。类 `Employee` 的定义（图 20）包含私有数据成员 `firstName`、`lastName`、`birthDate` 和 `hireDate`。成员 `birthDate` 和 `hireDate` 是类 `Date` 的 `const`，类 `Date` 包含私有数据成员 `day` 和 `year`。`Employee` 构造函数的原型（图 9.20，第 14–15 行）指定构造函数有四个参数（`first`、`last`、`date0Birth` 和 `date0Hire`）。前两个参数通过成员初始化器传递给 `string` 类构造函数以用于 `firstName` 和 `lastName` 数据成员。后两个参数通过成员初始化器传递给 `Date` 类构造函数以用于 `birthDate` 和 `hireDate` 数据成员。

![](img/06ca63376760c659af4aa0e9c282068d_456_0.png)

```cpp
// Fig. 9.18: Date.h
// Class definition; Member functions defined in Date.cpp
#include <string>
#ifndef DATE_H
#define DATE_H
class Date {
public:
    static const unsigned int monthsYear = 12; // months in a year
    explicit Date(unsigned int month = 1, unsigned int day = 1, unsigned int year = 1900);
    std::string toString() const; // date in month/day/year format
    ~Date(); // provided to confirm destruction order
private:
    unsigned int month; // 1-12 (January-December)
    unsigned int day; // 1-31 based on month
    unsigned int year; // any year
    // utility function to check if day is proper for month and year
    unsigned int checkDay(int) const;
};
#endif
```

图 9.18 | `Date` 类定义。

```cpp
// Fig. 9.19: Date.cpp
// Date class member-function definitions.
#include <array>
#include <iostream>
#include <sstream>
#include <stdexcept>
#include "Date.h" // Include Date class definition
using namespace std;
```

图 9.19 | `Date` 类成员函数定义。（第 1 部分，共 2 部分）。

## 9.12 组合：类成员对象 457

```cpp
// constructor confirms proper value for month; calls
// utility checkDay to confirm proper value for day
Date::Date(unsigned int mn, unsigned int dy, unsigned int yr)
: month(mn), day(checkDay(dy)), year(yr) {
if (mn < 1 || mn > monthsYear) // validate the month
throw invalid_argument("must be 1-12");
}
// Output Date object to show when constructor is called
cout << "Date object constructor for date " << toString() << endl;
}
// print Date object in form month/day/year
string Date::toString() const {
ostringstream output;
output << month << '/' << day << '/' << year;
return output.str();
}
// Output Date to show when its destructor is called
Date::~Date() {
cout << "Date object destructor of date " << toString() << endl;
}
// utility function to confirm proper value based on
// month and year; handles leap year, too
unsigned int Date::checkDay(int testDay) const {
static const int daysPerMonth[] = {0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 31};
// determine whether testDay is valid for specified month
if (testDay > 0 && testDay <= daysPerMonth[month]) {
return testDay;
}
// February 29 check for leap year
if (month == 2 && testDay == 29 && (year % 400 == 0 ||
(year % 4 == 0 && year % 100 != 0))) {
return testDay;
}
throw invalid_argument("Invalid day for current month and year");
}
```

图 9.19 | `Date` 类成员函数定义。（第 2 部分，共 2 部分。）

```cpp
// Fig. 9.20: Employee.h
// Employee class definition showing composition.
// Member functions defined in Employee.cpp.
#include <string>
```

图 9.20 | `Employee` 类定义显示组合。（第 1 部分，共 2 部分。）

## 第 9 章 类：更深入的探讨

```cpp
#ifndef EMPLOYEE_H
#define EMPLOYEE_H
#include <string>
#include "Date.h" // include Date class definition
class Employee {
public:
Employee(const std::string&, const std::string&,
const Date&, const Date&);
std::string toString() const;
~Employee(); // provided to confirm destruction order
private:
std::string firstName; // composition: member object
std::string lastName; // composition: member object
const Date birthDate; // composition: member object
const Date hireDate; // composition: member object
};
#endif
```

图 9.20 | `Employee` 类定义显示组合。（第 2 部分，共 2 部分）

```cpp
// 9.21: Employee.cpp
// Employee class member-function definitions.
#include <iostream>
#include <sstream>
#include "Employee.h" // Employee class definition
#include "Date.h" // Date class definition
using namespace std;
// constructor use member initializer list to pass initializer
// values to constructors of member objects
Employee::Employee(const string& firstName, const string& lastName,
const Date& dateOfBirth, const Date& dateOfHire)
: firstName(firstName), // initialize firstName
lastName(lastName), // initialize lastName
birthDate(dateOfBirth), // initialize birthDate
hireDate(dateOfHire) {} // initialize hireDate
// output Employee object to show when constructor is called
cout << "Employee object constructor: "
<< firstName << " " << lastName << endl;
```

```cpp
}
// print object
string Employee::toString() const {
ostringstream output;
output << lastName << ", " << firstName << " Hired: "
<< hireDate.toString() << " Birthday: " << birthDate.toString();
return output.str();
}
```

图 9.21 | `Employee` 类成员函数定义。（第 1 部分，共 2 部分）

# 9.12 组合：类成员对象 459

```cpp
// output Employee object to show when its destructor is called
Employee::Employee() {
cout << "Employee destructor: "
<< lastName << ", << firstName << endl;
}
```

图 9.21 `Employee` 构造函数的成员初始化列表（第 2 部分，共 2 部分）

`Employee` 构造函数的成员初始化列表
冒号 (`:`) 位于构造函数头之后（图 9.21，第 13 行）开始成员初始化列表。成员初始化器指定传递给 `string` 和 `date` 成员的构造函数的 `Employee` 构造函数参数。参数 `first`、`last`、`dateBirth` 和 `dateHire` 分别传递给 `firstName`、`lastName`、`birthDate` 和 `hireDate` 的构造函数。成员初始化器的顺序无关紧要。它们按在 `Employee` 类中声明成员对象的顺序执行。

## 良好的编程实践 9.2

为清晰起见，按类的数据成员声明的顺序列出成员初始化器。

![](img/06ca63376760c659af4aa0e9c282068d_459_0.png)

`Date` 类的默认拷贝构造函数
在研究类（图 9.18）时，请注意该类未提供接收 `Date` 类型参数的构造函数。那么，为什么 `Employee` 构造函数的成员初始化列表不通过向其 `Date` 构造函数传递 `Date` 来初始化 `birthDate` 和 `hireDate` 呢？正如我们在第 10 节中提到的，编译器为每个类提供一个默认拷贝构造函数，该构造函数将构造函数参数对象的每个数据成员复制到正在初始化的对象中的对应成员中。第 10 章讨论了如何定义自定义拷贝构造函数。

测试类 `Date` 和 `Employee`
图 9.22 创建了两个 `Date` 对象（第 9–10 行）并将它们作为参数传递给第 11 行创建的 `Employee` 对象的构造函数。实际上，在构造 `Employee` 时共有五次构造函数调用：

- 两次调用 `string` 类的构造函数（图 9.21 第 13–14 行），
- 两次调用 `Date` 类的默认拷贝构造函数（图 9.21 第 15–16 行），
- 一次调用 `Employee` 类的构造函数。

第 13 行输出 `Employee` 的对象数据。当在第 9–10 行创建每个 `Date` 对象时，第 9.19 图第 12–20 行定义的构造函数会显示一行输出，以表明构造函数已被调用（参见输出的前两行）。请注意，图 9.22 第 11 行导致了两个 `Date` 调用，这些调用不会出现在该程序的输出中。当在 `Employee` 的成员初始化列表中初始化 `Employee` 的每个 `Date` 成员对象时（图 9.21，第 15–16 行），会调用类的默认拷贝构造函数。由于该构造函数是由编译器隐式定义的，因此它不包含任何输出语句来演示何时被调用。

# 第 9 章 类：更深入的探讨

```cpp
// Fig. 9.22: fig09_22.cpp
// Demonstrating composition--an object with member objects.
#include <iostream>
#include "Date.h" // Date class definition
#include "Employee.h" // Employee class definition
using namespace std;
int main() {
    Date birth(7, 24, 1949);
    Date hire(3, 12, 1983);
    Employee manager("Bob", "Blue", birth, hire);
    cout << "\n" << manager.toString() << endl;
}
```
