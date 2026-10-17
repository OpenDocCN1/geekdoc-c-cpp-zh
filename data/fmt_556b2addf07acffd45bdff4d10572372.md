
```
// poor practice: returning a reference to a private data member.
unsigned int& Time::badSetHour(int hh) {
    if (hh >= 0 && hh < 24) {
        hour = hh;
    }
    else {
        throw invalid_argument("hour must be 0-23");
    }
    return hour; // dangerous reference
}
```

图 9.12 `Time`类成员函数定义。

9.13 声明 `Time`对象（第 9 行）和引用 `hourRef`，该引用由调用 `badHour(20)`返回的引用初始化。第 14 行显示别名 `hourRef`的值。这显示了 `hourRef`如何破坏类的封装——`states in main`可能无法访问类的私有数据。接下来，第 15 行使用别名将 `hour`的值设置为 30（无效值），第 16 行显示 `getHour`返回的值，以显示将值分配给 `hourRef`实际上修改了 `Time`对象中的私有数据。最后，第 20 行使用 `badHour`函数本身

# 9.10 默认逐成员赋值

`as I value and assigns 74` (another invalid value) to the reference returned by the function.
Line 25 assigns the value returned by function `getHour` to show that assigning a value to the result of the function call in line 20 modifies the private data in the Object `t`.

# 软件工程观察 9.7

返回对私有数据成员的引用或指针会破坏类的封装性，并使客户端代码依赖于类的表示。在某些情况下这是合适的——我们将在第 10.10 节中展示我们在构建自定义 `Array`类时使用它的示例。

![](img/06ca63376760c659af4aa0e9c282068d_451_0.png)

```
// Fig. 9.13: fig09_13.cpp
// Demonstrating a public member function that
// returns a reference to a private data member.
#include <iostream>
#include "time.h" // include definition of class Time
using namespace std;
int main() {
    Time t; // Create Time object
    initialize hourRef with the reference returned by badHour
unsigned int& hourRef(t.setHour(20)); // 20 is a valid hour
    cout << "Valid before modification: " << hourRef;
    hourRef = 30; // use hourRef to set invalid value in Time object
    cout << "\nInvalid hour after modification: " << t.getHour();
    // Dangerous: Function call that returns
// a reference can be used as an lvalue!
t.setHour(12) = 74; // assign another invalid value to hour
    cout << "\n==================================================\n"
         << "POOR PROGRAMMING PRACTICE!!!!!!!!\n"
         << t.setHour(12) as an lvalue, invalid hour: "
         << t.getHour();
    cout << "\n==================================================\n" << endl;
}
```

Valid hour before modification: 20
Invalid hour after modification: 30

****************************************************
POOR PROGRAMMING PRACTICE!!!!!!!
t.setHour(12) as an lvalue, invalid hour: 74
****************************************************

Fig. 9.13 | public member function that returns a reference to a private data member.

# 9.10 默认逐成员赋值

赋值运算符 (`=`) 可用于将一个对象赋给同一类的另一个对象。默认情况下，此类赋值是通过逐成员赋值执行的，也称为复制赋值——赋值运算符右侧对象的每个数据成员

![](img/06ca63376760c659af4aa0e9c282068d_451_1.png)

# 452 第 9 章 类：更深入的探讨

运算符单独赋给赋值运算符左侧对象中的相同数据成员。图 9.14–9.15 定义了一个 `Date`类。第 9.16 行 15 使用默认逐成员赋值将 `Date`对象 `date1`的数据成员赋给 `Date`对象 `date2`的对应数据成员。在这种情况下，`date1`的 `month`成员被赋给 `date2`的 `month`成员，`date1`的 `day`成员被赋给 `date2`的 `day`成员，`date1`的 `year`成员被赋给 `date2`的 `year`成员。[注意：当与数据成员包含指向动态分配内存的指针的类一起使用时，逐成员赋值可能会导致严重问题；我们在第 10 章中讨论这些问题并展示如何处理它们。]

// Fig. 9.14: Date.h
// Class declaration. Member functions are defined in Date.cpp.
#include <string>
// prevent multiple inclusions of header
#ifndef DATE_H
#define DATE_H
// Class Date definition
class Date {
public:
    explicit Date(unsigned int = 1, unsigned int = 1, unsigned int = 2000);
    std::string toString() const;
private:
    unsigned int month;
    unsigned int day;
    unsigned int year;
};
#endif
```

**Fig. 9.14** | `Date` class declaration.

```
// Fig. 9.15: Date.cpp
// Date class member-function definitions.
#include <sstream>
#include <string>
#include "Date.h" // inclusion of class Date from Date.h
using namespace std;
// Date constructor (should do range checking)
Date::Date(unsigned int m, unsigned int d, unsigned int y)
    : month(m), day(d), year(y) {}
// print Date in the format mm/dd/yyyy
string Date::toString() const {
    ostringstream output;
    output << month << "/" << day << "/" << year;
    return output.str();
}
```

**Fig. 9.15** | `Date` class member-function definitions.

# 9.11 const 对象和 const 成员函数 453

```
// Fig. 9.16: fig09_16.cpp
// Demonstrating that class objects can be assigned
// to each other using default memberwise assignment
#include <iostream>
#include "Date.h" // include definition of class from Date.h
using namespace std;
int main() {
Date date1(7, 4, 2004);
Date date2; // date2 defaults to 1/1/2000
cout << "date1 = " << date1.toString() << "\n\n"
<< "ndate2 = " << date2.toString() << "\n\n"
date2 = date1; // default memberwise assignment
cout << "After memberwise assignment, date2 = "
<< date2.toString() << endl;
}
```

date1 = 7/4/2004
date2 = 1/1/2000
After default memberwise assignment, date2 = 7/4/2004

> **Fig. 9.16** Class objects can be assigned to each other using default memberwise assignment.

对象可以作为函数参数传递，也可以从函数返回。这种传递和返回默认情况下使用按值传递——对象的副本被传递或返回。在这种情况下，C++ 创建一个新对象并使用拷贝构造函数将原始对象的值复制到新对象中。对于每个类，编译器都提供一个默认的拷贝构造函数，该构造函数将原始对象的每个成员复制到新对象的对应成员中。与逐成员赋值一样，拷贝构造函数在使用数据成员指向动态分配内存的类时也会导致严重问题。第 10 章讨论了如何定义自定义构造函数以正确复制对象。

# 9.11 const 对象和 const 成员函数

让我们看看最小权限原则如何应用于对象。有些对象需要被修改，有些则不需要。你可以使用 `const` 指定对象不可修改，任何尝试修改对象的操作都应导致编译错误。语句

```
const Time noon{12, 0, 0};
```

声明了一个 `Time`类的 `const`对象并将其初始化为 12 点中午。可以实例化同一类的 `const`和非 `const`对象。

> 错误预防提示 9.5
尝试修改 `const`对象的操作在编译时被捕获，而不是导致执行时错误。

# 性能提示 9.3

> 在适当时声明变量和对象为 `const`可以提高性能——编译器对不能对非 `const`变量执行的常量进行优化。

C++ 声明对 `const`对象的成员函数调用，除非成员函数本身也被声明为 `const`。这对于不修改对象的 `get`成员函数也是如此。这也是我们声明所有不修改其调用对象的成员函数为 `const`的关键原因之一。

# 常见编程错误 9.3

> 定义一个 `const`成员函数，该函数在同一对象上调用类的非 `const`成员函数是编译错误。

# 常见编程错误 9.4

> 在 `const`对象上调用非 `const`成员函数是编译错误。

对于构造函数和析构函数会出现一个有趣的问题，每个构造函数和析构函数通常都会修改对象。构造函数必须被允许修改对象，以便析构构能够在系统的内存被回收之前执行其终止清理工作。尝试将构造函数或析构函数声明为 `const`是编译错误。`const`对象的“constness”从 `const`完成对象初始化的那一刻起被强制执行，直到对象被销毁。

# 使用 const 和非 const 成员函数

图 9.17 中的程序使用图 9.5–9.6 中的 `Time`类，但移除了函数 `toString()`原型和定义的 `const`，以便我们可以展示编译错误。我们创建了两个对象——非 `const`的 `wakeup`（第 6 行）和 `const`的 `noon`（第 7 行）。程序尝试在 `const`对象 `noon`上调用非 `const`成员函数 `sethour`（第 11 行）和 `toString`（第 15 行）。在每种情况下，编译器都会生成错误。消息说明了对象上的另外三种成员函数调用——非 `const`对象上的非 `const`成员函数（第 10 行）、非 `const`对象上的 `const`成员函数（第 12 行）和 `const`对象上的 `const`成员函数（第 13–14 行）。对 `const`对象调用非 `const`成员函数时生成的错误消息显示在输出窗口中。

```
// Fig. 9.17.cpp
// const objects and const member functions.
#include "Time.h" // include Time class definition
\int main() {
    Time wakeup{6, 45, 0}; // non-const object
    const Time noon{12, 0, 0}; // const object
```

Fig.9.17 | const objects and const member functions. (Part I of 2).

# 9.12 组合：类成员对象

```
// wakeup.setHour(18); // OBJECT MEMBER FUNCTION
// // non-const non-const
// noon.setHour(12); // const non-const
// wakeup.getHour(); // const non-const const
// noon.getMinute(); // const const
// noon.toUniversalString(); // const const
// noon.toStandardString(); // const non-const
//
```

Visual C++ compiler errors:

```
C:\examples\ch09\fig09_17.cpp(fig09_17.cpp:11): error C2662:
// void Time::setHour(int): cannot convert 'this' pointer from 'const Time
// to 'Time &'
C:\examples\ch09\fig09_17.cpp(fig09_17.cpp:11): note: Conversion losses
C:\examples\ch09\fig09_17.cpp(fig09_17.cpp:15): error C2662:
// std::string Time::toStandardString(void): cannot convert 'this' pointer
from 'const Time' to 'Time &'
C:\examples\ch09\fig09_17.cpp(fig09_17.cpp:15): note: Conversion losses
```
