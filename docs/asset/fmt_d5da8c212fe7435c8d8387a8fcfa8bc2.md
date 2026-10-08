
`Database`类使用标准库中的`std::vector`类来存储`Employee`对象。

## Database.h

由于数据库将负责自动为新员工分配员工编号，因此用一个常量定义编号的起始位置。

```cpp
#pragma once
#include <iostream>
#include <vector>
#include "Employee.h"

namespace Records {
    const int kFirstEmployeeNumber = 1000;
}
```

数据库提供了一种简单的方法通过提供姓和名来添加新员工。为了方便起见，该方法返回新员工的引用。外部代码也可以通过调用`getEmployee()`方法获取员工引用。该方法声明了两个版本。一个允许检索员工编号。另一个需要姓和名。

```cpp
class Database {
public:
    Database();
    Employee& addEmployee(const std::string& firstName, const std::string& lastName);
    Employee& getEmployee(int employeeNumber);
    Employee& getEmployee(const std::string& firstName, const std::string& lastName);

    void displayAll() const;
    void displayCurrent() const;
    void displayFormer() const;

private:
    std::vector<Employee> mEmployees;
    int mNextEmployeeNumber;
};
```

## Database.cpp

构造函数负责初始化下一个员工编号数据成员为其起始值。

```cpp
#include <iostream>
#include <stdexcept>
#include "Database.h"
using namespace std;

namespace Records {
    Database::Database() : mNextEmployeeNumber(kFirstEmployeeNumber) {}
}
```

`addEmployee()`方法创建一个新的`Employee`对象，填充其信息并将其添加到`vector`中。注意`mNextEmployeeNumber`数据成员在使用后会递增，这样下一个员工将获得一个新的编号。

```cpp
Employee& Database::addEmployee(const string& firstName, const string& lastName)
{
    Employee employee;
    employee.setFirstName(firstName);
    employee.setLastName(lastName);
    employee.setEmployeeNumber(mNextEmployeeNumber++);
    employee.hire();
    mEmployees.push_back(employee);
    return mEmployees[mEmployees.size() - 1];
}
```

只显示了一个`getEmployee()`版本。两个版本的工作方式相似。这些方法使用基于范围的循环遍历`mEmployees`中的所有员工，并检查每个`Employee`是否与提供给方法的信息匹配。如果没有找到匹配项，则抛出一个异常。

```cpp
Employee& Database::getEmployee(int employeeNumber)
{
    for (auto& employee : mEmployees) {
        if (employee.getEmployeeNumber() == employeeNumber) {
            return employee;
        }
    }
    throw runtime_error("Employee not found.");
}

Employee& Database::getEmployee(const std::string& firstName, const std::string& lastName)
{
    for (auto& employee : mEmployees) {
        if (employee.getFirstName() == firstName && employee.getLastName() == lastName) {
            return employee;
        }
    }
    throw runtime_error("Employee not found.");
}

// 注意：此处原文代码逻辑似乎有错位或错误，已根据上下文修正翻译逻辑
void Database::displayAll() const
{
    for (auto& employee : mEmployees) {
        // 显示所有员工
    }
}

void Database::displayCurrent() const
{
    for (auto& employee : mEmployees) {
        if (employee.cHired) {
            // 显示当前员工
        }
    }
}

void Database::displayFormer() const
{
    for (auto& employee : mEmployees) {
        if (!employee.cHired) {
            // 显示之前的员工
        }
    }
}
```

### DatabaseTest.cpp

对数据库基础功能的简单测试：

```cpp
#include <iostream>
#include "Database.h"
using namespace std;
using namespace Records;

int main() {
    Database myDB;
    myDB.addEmployee("Greg", "Wallis");
    myDB.addEmployee("Marc", "Gregoire");
    myDB.addEmployee("John", "Doe");

    cout << "All employees: " << endl;
    myDB.displayAll();

    cout << "Current employees: " << endl;
    myDB.displayCurrent();

    cout << "Former employees: " << endl;
    myDB.displayFormer();

    return 0;
}
```

## 用户界面

程序的最后部分是一个基于菜单的用户界面，使用户能够与员工数据库交互。

## UserInterface.cpp

`main()`函数是一个循环，显示菜单、执行选择的操作，然后再次执行。对于大多数操作，定义了单独函数。对于较简单的操作（如显示员工），将实际代码放在相应的分支中。

```cpp
#include <iostream>
#include <stdexcept>
#include <exception>
#include "Database.h"
using namespace std;
using namespace Records;

int displayMenu();
void doHire(Database& db);
void doFire(Database& db);
void doPromote(Database& db);
void doDemote(Database& db);

int main() {
    Database employeeDB;
    bool done = false;
    while (!done) {
        int selection = displayMenu();
        switch (selection) {
            case 1:
                doHire(employeeDB);
                break;
            case 2:
                doFire(employeeDB);
                break;
            case 3:
                doPromote(employeeDB);
                break;
            case 4:
                employeeDB.displayAll();
                break;
            case 5:
                employeeDB.displayCurrent();
                break;
            case 6:
                employeeDB.displayFormer();
                break;
            case 0:
                done = true;
                break;
            default:
                cout << "Unknown command." << endl;
        }
    }
    return 0;
}
```

```cpp
break;
}
return 0;
}
```

`displayMenu()`函数输出菜单并获取用户输入。一个重要的注记是，这段代码假设用户会“听话”，并且在要求输入数字时输入数字。当你在第12章学习 I/O 时，你将学习到如何防止错误的输入。

```cpp
int displayMenu()
{
    int selection;
    cout << endl;
    cout << "Employee Database" << endl;
    cout << "--------------------" << endl;
    cout << "1) Hire a new employee" << endl;
    cout << "2) Fire an employee" << endl;
    cout << "3) Promote an employee" << endl;
    cout << "4) List all employees" << endl;
    cout << "5) List current employees" << endl;
    cout << "6) List all former employees" << endl;
    cout << "0) Quit" << endl;
    cout << endl;
    cout << "---------";
    cin >> selection;
    return selection;
}
```

`doHire()`函数从用户处获取新员工的名字并告诉数据库添加该员工。它通过输出消息并继续执行来优雅地处理错误。

```cpp
void doHire(Database &db)
{
    string firstName;
    string lastName;
    cout << "First name? ";
    cin >> firstName;
    cout << "Last name? ";
    cin >> lastName;
    try {
        db.addEmployee(firstName, lastName);
    } catch (std::exception& exception) {
        cerr << "Unable to add new employee: " << exception.what() << endl;
    }
}
```

`doFire()`和`doPromote()`根据员工编号向数据库查询员工，并使用`Employee`对象的公共方法进行修改。

```cpp
void doFire(Database &db)
{
    int employeeNumber;
    cout << "----Employee number? ";
    cin >> employeeNumber;
    try {
        Employee& emp = db.getEmployee(employeeNumber);
        emp.fire();
        cout << "Employee " << employeeNumber << " terminated." << endl;
    } catch (const std::exception& exception) {
        cerr << "Unable to terminate employee: " << exception.what() << endl;
    }
}
```

```cpp
void doPromote(Database& db)
{
    int employeeNumber;
    int raiseAmount;
    cout << "Employee number? ";
    cin >> employeeNumber;
    cout << "How much of a raise? ";
    cin >> raiseAmount;
    try {
        Employee& emp = db.getEmployee(employeeNumber);
        emp.promote(raiseAmount);
    } catch (const std::exception& exception) {
        cerr << "Unable to promote employee: " << exception.what() << endl;
    }
}
```

## 评估程序

前面的程序涵盖了从非常简单到复杂的多个主题。你有许多方法可以扩展这个程序。例如，用户界面并没有暴露`Database`或`Employee`类的所有功能。你可以修改 UI 以包含这些特性。你还可以修改`Database`类，从`mEmployees`中移除被解雇的员工。

如果这个程序中有某些部分不理解，请考虑回顾之前的章节以复习那些主题。如果某些地方仍然不清楚，学习最好的方法是玩玩代码并尝试。例如，如果你不确定如何使用条件运算符，可以写一个短的`main()`函数来尝试一下。

## 总结

现在你已经掌握了 C++ 的基础知识，你准备好成为一名专业的 C++ 程序员了。当你书中后面开始深入学习 C++ 语言时，请参考本章来复习你可能需要回顾的语言部分。回到本章中的一些代码示例，可以将遗忘的概念带回脑海。

## 处理字符串

本章包含什么？

- C 风格字符串与 C++ 字符串的区别
- C++ `string`类的细节
- 什么是原始字面量（raw literals）

WROX.COM 下载资源

请注意，本章所有的代码示例都可以在网站 www.wrox.com/downloads/chapter2 获取。

你编写的每个程序都会使用某种类型的字符串。在旧的 C 语言中，使用空字符结尾的字符数组来表示字符串。遗憾的是，这样做会导致很多问题，例如缓冲区溢出。本章详细讨论了字符串。从讨论旧风格字符串开始，解释了它们的缺点、C++ `string`类以及原始字面量。

## 动态字符串

在将字符串作为类对象的语言中，字符串具有许多特性，例如可以扩展到任何大小，或者提取或替换子字符串。在 C 等语言中，字符串几乎是事后考虑的；没有真正良好的 "string" 类型，只有固定大小的数组。C++ 提供了安全易用的`string`类。

## C 风格字符串

在 C 语言中，字符串表示为字符数组。字符串的最后一个字符是空字符（`\0`），以便处理字符串的代码判断其何时结束。这个空字符被称为 NULL，这与指针不同。C++ 提供了更好的抽象，但在 C++ 编程中仍然需要理解字符串的技术。长远来看，程序员处理字符串时最常见的错误是忘记为`\0`字符分配空间。例如，字符串 "hello" 看起来是五个字符，但存储它需要六个字符的空间，如图 2-1 所示。

![](img/5a77830a2588ca56d95_0.png) 图2-1

C++ 包含了几个来自 C 语言的处理字符串的函数。这些函数定义在`<cstring>`头文件中。作为一个通用规则，这些函数不处理内存分配。例如，`strcpy()`取两个字符串作为参数并将第二个字符串拷贝到第一个，无论其是否容纳。下面的代码尝试构建`strcpy()`的封装，分配正确的内存并返回结果，而不是接收一个字符串。调用者负责释放`copyString()`分配的内存。

```cpp
char* copyString(const char* str)
{
    char* result = new char[strlen(str)]; // 错误！差了一个！
    strcpy(result, str);
    return result;
}
```
