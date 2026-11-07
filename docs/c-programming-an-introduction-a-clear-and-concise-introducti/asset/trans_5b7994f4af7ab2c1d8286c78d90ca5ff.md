
## 组合示例：Employee 类

定义一名员工有许多属性，例如他或她的姓名、年龄、性别、受雇日期等。其中一些属性可以单独作为类存在，例如姓名和受雇日期。在本节中，我们将构建一个 Employee 类，它由 Name 类和 Date 类的对象组合而成。

我们已经定义了一个 Name 类，因此这里可以直接使用该类的简化版本。在展示 Employee 类的全部代码时，我们会再次列出它。不过，我们还没有 Date 类，所以现在就来定义它。

Date 类的成员肯定包括日、月和年。还有许多其他可能的成员，但我们将定义限制为这三个成员。

这里我们将定义的 Date 类方法仅包括一个构造函数和一个以 mm/dd/yyyy 格式显示日期的方法。我们还可以包含许多其他方法，但这两个方法足以演示如何在类组合示例中使用该类。

以下是 Date 类的代码：

```cpp
class Date
{
private:
    int month, day, year;

public:
    Date()
    {
        month = 0;
        day = 0;
        year = 0;
    }

    Date(int m, int d, int y)
    {
        month = m;
        day = d;
        year = y;
    }

    void setDate(int m, int d, int y)
    {
        month = m;
        day = d;
        year = y;
    }

    string getDate()
    {
        stringstream dt;
        dt << month << "/" << day << "/" << year;
        return dt.str();
    }
};
```

上面的 getDate() 方法需要一些解释。C++ 语言在组合字符串和整数方面做得并不好。编写 getDate() 函数的简单方式是：

```cpp
return month + "/" + day + "/" + year;
```

但这种方法无法编译。最简单的解决方案是使用一种特殊的数据类型 stringstream，它允许你将数据流赋给一个变量，就像将数据流写到控制台一样。然后，你可以将包含月、日和年并用斜杠分隔的数据流写入该变量，再以字符串形式显示 stringstream 变量的值。

现在，我们准备好使用 Date 类和 Name 类来构建 Employee 类了。以下是代码：

```cpp
class Employee
{
private:
    Name empName;
    Date hireDate;

public:
    Employee(string first, string middle,
             string last, int m, int d, int y)
    {
        empName.setName(first, middle, last);
        hireDate.setDate(m, d, y);
    }

    string getEmployee()
    {
        return empName.getName() + "\n" +
               hireDate.getDate() + "\n";
    }
};
```

数据成员由两个对象组成——一个 Name 对象和一个 Date 对象。构造函数必须分别调用 setName 和 setDate 方法，将数据放入这两个数据成员，因为此时无法调用构造函数。getEmployee() 方法只是分别调用 Name 和 Date 对象的相应 get 方法，并加入换行符，使输出更易读。

在面向对象编程中，你会遇到的许多问题，使用组合而不是继承可以更轻松、更高效地解决。组合以与继承大致相同的方式利用代码复用，但不会像继承那样导致令人困惑、低效且可能不正确的代码。还有许多问题也更适合采用组合方案，而不是使用继承的解决方案。

## 练习

- 1. 设计一个 DateBook 类，它由 Name 类和 Date 类组成。编写一个程序来测试该类。确保创建一整套构造函数以及 get 和 set 方法。
- 2. 创建一个 DateTime 类，它组合 Date 类和 Time 类，使得当时间从 23:59 变为 00:00 时，对应的日期增加 1。确保包含构造函数以及 get 和 set 方法。

## 附录 A

### 错误与错误消息

程序中出现错误是不可避免的。初学 C++ 的程序员尤其会在程序中遇到许多错误，但同样真实的是，专家级 C++ 程序员每天也会经历代码中的错误。编程太复杂了，程序员不可能期望不必处理错误。在本附录中，我们讨论你开始学习 C++ 时会遇到的一些常见错误。更重要的是，我们讨论如何解释编译器在代码中发现错误时你将收到的错误消息。

#### 语法错误

你刚开始学习 C++ 编程时最常犯的错误是*语法错误*。语法错误意味着你没有正确地构成 C++ 语句。一种常见语法错误的例子是在语句末尾漏掉分号。下面是一个 C++ 程序，其中一条语句漏掉了分号：

```cpp
// ErrorHandling.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    cout << "Hello, World!" << endl
    Console::ReadKey();
    return 0;
}
```

运行此程序时，首先会弹出一个消息框，内容为：“存在生成错误。是否要继续并运行上一次成功生成？” 对这个问题你应该回答“否”。

现在查看 Visual C++ Express 底部的“输出”窗口。你将看到以下消息：

```text
1>------ Build started: Project: ErrorHandling.cpp, Configuration: Debug Win32 ------
1>ErrorHandling.cpp
1>ErrorHandling.cpp(12): error C2143: Syntax error: missing ';' before System::Console::ReadKey
====== Build: 0 succeeded, 1 failed, 0 up-to-date, 0 skipped ======
```

输出消息非常清楚地告诉你漏掉了分号，并且给出了编译器最终判定发生错误的行号。它无法告诉你错误在第 11 行，因为它必须等到发现第 12 行的后续代码，才能确定确实需要在第 11 行末尾放置分号。然而，Console::ReadKey() 不能跟在 cout << "Hello, World!" << endl 之后而没有在 endl 后加分号，所以报告了该错误。

另一种常见语法错误是拼错变量名。下面的程序演示了当你错误输入变量名时会发生什么：

```cpp
// ErrorHandling.cpp : main project file.

#include "stdafx.h"
using namespace System;

#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    int number1, number2, number3;
    number1 = 12;
    number2 = 23;
    numbre3 = number1 + number2;
    cout << "The sum is: " << number3 << endl;
    Console::ReadKey();
    return 0;
}
```

你可以看到变量 number3 在第 14 行被拼错了。产生的错误消息是：

```text
1>------ Build started: Project: ErrorHandling, Configuration: Debug Win32 ------
1>ErrorHandling.cpp
1>ErrorHandling.cpp(14): error C2065: 'numbre3': undeclared identifier
1>------ Build: 0 succeeded, 1 failed, 0 up-to-date, 0 skipped ------
```

这条错误消息更加用户友好，因为它准确报告了拼写错误发生在哪一行以及拼写错误是什么。你只需回到程序并修正错误。

另一种常见语法错误是遗漏——在预处理指令中漏掉一个库。下面的程序忘记包含 <iostream> 库：

```cpp
// ErrorHandling.cpp : main project file.

#include "stdafx.h"
using namespace System;

int main(array<System::String ^> ^args)
{
    cout << "Hello, World!" << endl;
    Console::ReadKey();
    return 0;
}
```

编译此程序时得到的错误消息是：

```text
1>----- Build started: Project: ErrorHandling, Configuration: Debug Win32 ------
1>ErrorHandling.cpp
1>ErrorHandling.cpp(8): error C2065: 'cout' : undeclared identifier
1>ErrorHandling.cpp(8): error C2065: 'endl' : undeclared identifier
=========== Build: 0 succeeded, 1 failed, 0 up-to-date, 0 skipped ===========
```

这条错误消息比上一条用处稍小，因为它没有告诉你你做了什么，只是让你知道它无法识别 cout 和 endl。不过，每当你看到这条错误消息，并且错误消息中提到的标识符是系统对象（例如 cout 和 endl）时，你就可以确定自己忘记包含那些对象所在的库了。

当你尝试在程序中使用一个尚未声明的变量时，会出现类似的错误消息：

```cpp
// ErrorHandling.cpp : main project file.

#include "stdafx.h"
using namespace System;
#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    int number1, number2;
    number1 = 12;
    number2 = 23;
```
