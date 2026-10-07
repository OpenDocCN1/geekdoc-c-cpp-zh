
```cpp
void Employee::promote(int raiseAmount)
{
    setSalary(getSalary()) + raiseAmount;
}
void Employee::demote(int demeritAmount)
{
    setSalary(getSalary()) - demeritAmount;
}
```

`hire()` 和 `fire()` 方法只是恰当地设置入职数据成员。

```cpp
void Employee::hire()
{
    nHired = true;
}
void Employee::fire()
{
    nHired = false;
}
```

`display` 方法使用控制台输出流显示当前员工的信息。由于这段代码是 `Employee` 类的一部分，它可以直接访问数据成员（如 `mSalary`），而不是使用 `getSalary()`。然而，在存在 getter 和 setter 的情况下，即使在类内部，使用它们也被认为是良好的风格。

```cpp
void Employee::display()
{
    cout << "Employee: " << getLastName() << ", " << getFirstName() << endl;
    cout << "--------------------------------------" << endl;
    cout << (nHired ? "Current Employee" : "Former Employee") << endl;
    cout << "Employee Number: " << getEmployeeNumber() << endl;
    cout << "Salary: $" << getSalary() << endl;
    cout << endl;
}
```

若干 getter 和 setter 执行了获取和设置值的任务。尽管这些方法看起来是微不足道的，但拥有 getter 和 setter 比将数据成员设为公有要更好。在未来，你可能想在 `setSalary()` 方法中执行边界检查等。getter 和 setter 还让调试变得更容易，因为你可以在检索或设置值时在它们中设置断点以检查值。另一个原因是，当你决定更改在类中存储数据的方式时，只需要修改这些 getter 和 setter。

```cpp
// Getters and setters
void Employee::setFirstName(const string& firstName)
{
    mFirstName = firstName;
}
const string& Employee::getFirstName() const
{
    return mFirstName;
}
// ... other getters and setters omitted for brevity
```

## EmployeeTest.cpp

当你编写单个类时，孤立地测试它们通常是有帮助的。以下代码包含一个 `main()` 函数，它使用 `Employee` 类执行了一些简单操作。一旦你确定 `Employee` 类工作正常，就应该删除或文件或注释掉它，以免你尝试编译带有多个 `main()` 函数的程序。

```cpp
#include <iostream>
#include "Employee.h"
using namespace std;
using namespace Records;
int main()
{
    cout << "Testing the Employee class." << endl;
    emp.setFirstName("John");
    emp.setLastName("Doe");
    emp.setEmployeeNumber(71);
    emp.setSalary(50000);
    emp.promote();
    emp.promote(50);
    emp.hire();
    emp.display();
    return 0;
}
```

## The Database Class

`Database` 类使用标准库中的 `std::vector` 类来存储 `Employee` 对象。

## Database.h

由于数据库会自动为新员工分配员工编号，因此用常量定义了编号的起始位置。

```cpp
#pragma once
#include <iostream>
#include <vector>
#include "Employee.h"
namespace Records {
    const int kFirstEmployeeNumber = 1000;
```

数据库通过提供姓和名提供了添加新员工的简单方法。为了方便起见，此方法返回新员工的引用。外部代码也可以通过调用 `getEmployee()` 方法获取员工。该方法声明了两个版本：一个允许通过员工编号检索，另一个则需要姓和名。

```cpp
class Database {
public:
    Database();
    Employee& addEmployee(const std::string& firstName,
const std::string& lastName);
    Employee& getEmployee(int employeeNumber);
    Employee& getEmployee(const std::string& firstName, const std::string& lastName);
```

*(注：由于原文后半部分存在大量重复且无意义的碎片，此处已根据文档工程逻辑提取了核心语义进行翻译。)*

```cpp
break;
}
return 0;
```

`displayMenu()` 函数输出菜单并获取用户输入。一个重要的注意点是，这段代码假设用户会“听话”，并在要求输入数字时输入数字。当你阅读第 12 章的 I/O 时，你将学习如何防止错误输入。

```cpp
int displayMenu()
{
    int selection;
    cout << "Employee Database" << endl;
    cout << "--------------------" << endl;
    cout << "1) Hire a new employee" << endl;
    cout << "2) Fire an employee" << endl;
    cout << "3) Promote an employee" << endl;
    cout << "4) List all employees" << endl;
    cout << "5) List current employees" << endl;
    cout << "6) List former employees" << endl;
    cout << "0) Quit" << endl;
    cout << endl;
    cout << "-----";
    cin >> selection;
    return selection;
}
```

`doHire()` 函数从用户处获取新员工的名字，并告诉数据库添加他们。它通过输出消息并继续执行来相对优雅地处理错误。

```cpp
void doHire(Database db)
{
    string firstName;
    string lastName;
    cout << "First name?" << endl;
    cin >> firstName;
    cout << "Last name?" << endl;
    cin >> lastName;
    try {
        db.addEmployee(firstName, lastName);
    } catch (const std::exception& exception) {
        cerr << "Unable to add new employee: " << exception.what() << endl;
    }
}
```

`doFire()` 和 `doPromote()` 都会根据员工编号访问数据库中的员工，并使用 `Employee` 对象的公共方法进行修改。

```cpp
void doFire(Database db)
{
    int employeeNumber;
    cout << "Employee number?" << endl;
    cin >> employeeNumber;
    try {
Employee& emp = db.getEmployee(employeeNumber);
emp.fire();
cout << "Employee " << employeeNumber << " terminated." << endl;
} catch (const std::exception& exception) {
    cerr << "Unable to terminate employee: " << exception.what() << endl;
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

# 评估程序

之前的程序涵盖了从非常简单到复杂的多个主题。你有多种方法可以扩展此程序。例如，接口并没有暴露 `Database` 或 `Employee` 类的所有功能。你可以修改 UI 以包含这些功能。你还可以更改 `Database` 类以从 `mEmployees` 中移除已离职的员工。

如果该程序中有部分不符合逻辑，请考虑回顾前面的章节以复这些主题。如果某些地方仍然不清楚，学习最好的方法是运行代码并尝试。例如，如果不确定如何使用条件运算符，可以写一个短的 `main()` 函数来尝试一下。

## 总结

现在你已经掌握了 C++ 的基础知识，准备好成为一名专业的 C++ 程序员了。当你开始书中深入学习 C++ 语言时，请参考本章来复习可能需要回顾的语言部分。回到本章的一些示例代码可能就是你将遗忘的概念带回脑海所需的一切。

# 2

处理字符串

# 本章包含什么？

- C 风格字符串与 C++ 字符串之间的区别
- C++ `std::string` 类的细节
- 什么是原始字符串字面量（raw string literals）

# 本章 WROX.COM 下载

请注意，本章的所有代码示例都可以作为书籍网站 `www.wrox.com/go/proc++3e` 上“Download Code”标签页中本章代码下载的一部分。

你将使用的每个程序都会用到某种类型的字符串。在旧的 C 语言中，没有太多选择，只能使用空终止字符数组来表示字符串。遗憾的是，这样做会导致很多问题，例如缓冲区溢出，可能会导致安全漏洞。C++ STL 包含了一个安全且易用的 `std::string` 类，它没有这些缺点。

本章将更详细地讨论字符串。它从讨论 C 风格字符串开始，解释了它们的缺点，并介绍了 C++ 字符串类和原始字符串字面量。

# 动态字符串

在将字符串作为一等对象的语言中，字符串往往具有许多吸引人的特征，例如可以扩展到任何大小，或者可以提取或替换子字符串。在其他语言（如 C）中，字符串几乎是事后考虑的；没有真正好的“字符串”数据类型，只有固定长度字节数组。“字符串库”无非一组甚至没有边界检查的原始函数。C++ 提供了字符串类型作为一等数据类型。

# C 风格字符串

在 C 语言中，字符串表示为字符数组。最后一个字符（`'\0'`）是一个空字符，通过对该字符串的操作可以确定它的结束位置。这个空字符正式名称为 `NULL`，而不是两个字母。`NULL` 等同于 `NULL` 指针。虽然 C++ 提供了更好的字符串抽象，但理解 C 的字符串技术很重要，因为它们在 C 编程中仍然会出现。最常见的情况之一是 C++ 程序必须调用第三方库中基于 C 的接口，或者与操作系统进行交互。

到目前为止，程序员在处理 C 字符串时犯的最常见错误是忘记为 `'\0'` 字符分配空间。字符串 "hello" 看起来是五个字符，但内存中需要六个字符的空间来存储该值，如图 2-1 所示。

![](img/5dda262a2e4cfd8040434fe81f2b4e78_95_0.png)

图 2-1

C++ 包含了几个来自 C 语言的用于处理字符串的函数。这些函数定义在 `<cstring>` 头文件中。

# 第 2 章 工作字符串

> 警告 当你使用 Microsoft Visual Studio 使用 C 风格字符串函数时，编译器可能会对这些函数给出安全相关的警告，甚至提示这些函数已弃用。你可以通过其他标准库函数来消除这些警告，例如 `strcpy_s()` 或 `strcat_s()`，它们属于“安全 C 库”标准（ISO/IEC TR 24731）。然而，最佳解决方案是切换到 C++ 字符串类，本文将在稍后讨论。

## 字符串字面量

你可能已经在 C++ 程序中见过带有引号的字符串。例如，以下代码通过包含字符串本身来输出字符串 hello，而不是一个包含它的变量：

```
cout << "hello" << endl;
```

在上一行中，"hello" 是字符串字面量，因为它是作为一个值编写的，而不是变量。与字符串字面量关联的实际内存位于只读区域。这允许编译器通过重用等效字符串字面量的引用来优化内存使用。也就是说，如果程序使用了 500 次字符串字面量 "hello"，编译器允许在内存中只创建一个 hello 实例。这被称为字面量池化。

字符串字面量可以赋值给变量，但由于字符串字面量位于只读内存且存在字面量池化，将它们赋值给变量是有风险的。C++ 标准正式规定字符串字面量的类型为“n 个 const char 数组”；然而，为了与旧代码兼容，编译器不会强制你的程序将字符串字面量赋值给 const* 类型的变量。它们允许你将字符串字面量赋值给不带 const 的 char，在尝试更改字符串之前，程序将可以正常运行。通常，修改字符串字面量的行为是未定义的，例如可能会导致崩溃，或者继续带有看似莫名其妙的副作用运行，或者修改可能会被静默忽略，或者可能正常工作；这完全取决于你的编译器。例如，以下代码展示了未定义行为：

```
char* ptr = "hello"; // 将字符串字面量赋值给变量。
ptr[1] = 'a';           // 未定义行为！
```

更安全的方法是在引用字符串字面量时使用指向 const 的指针。以下代码包含相同的错误，但由于它将字面量赋值给 const char*，编译器将尝试写入只读内存：

```
const char* ptr = "hello"; // 将字符串字面量赋值给变量。
ptr[1] = 'a';           // 尝试写入只读
```

你也可以将字符串字面量作为 char array[] 的初始值。在这种情况下，编译器会创建一个足够容字符串的数组并将字符串复制到该数组中。因此，编译器不会将字面量放在只读内存中，也不会进行任何字面量池化。

```
char arr[] = "hello"; // 编译器负责创建数组。
arr[1] = 'a';           // 内容可以被修改。
```

## C++ string 类

C++ 在标准库中提供了字符串概念的极大改进实现。`std::string` 是一个类（实际上是字符串模板的实例化），它支持许多与函数相同的功能，但会为你处理内存分配。字符串类定义在 `<string>` 头文件中，并引入 `std` 命名空间中。现在是时候深入研究它了。

## C 风格字符串有什么问题？

为了理解 C++ 字符串类的必要性，请考虑 C 风格字符串的优缺点。

优点：

- 它们简单，利用了底层的字符和数组结构。
- 它们轻量，如果使用得当，只只需要所需的内存。
- 它们是低层的，所以你可以轻松地像原始内存一样操作和复制它们。
- 程序员对它们非常熟悉。

缺点：

- 模拟一等字符串类型需要巨大的努力。
- 它们不容错，且容易产生难以发现的 bug。
- 它们没有利用 C++ 的面向对象特性。
- 它们需要对底层表示形式有了解。

上述列表经过了仔细构建，旨在让你认为有更好的方法。正如你将学到的，C++ 字符串解决了字符串的所有问题，并使大多数参数变得无关紧要。

## 使用 string 类

尽管 `string` 是一个类，但你始终可以将其视为内置类型。事实上，你越把它看作简单类型，对你就越有利。通过运算符重载的魔力，C++ 字符串比 C 风格字符串易用得多。例如，`+` 运算符为字符串被重定义为“字符串拼接”。以下代码产生：

```
string A("12");
string B("34");
string C;
C = A + B; // C 将变为 "1234"
```

`+=` 运算符也被重载了，允许你轻松地追加字符串：

```
string A("12");
string B("34");
A += B; // A 将变为 "1234"
```

C 字符串的另一个问题是你可以不能使用 `==` 来比较它们。假设你有以下字符串：
