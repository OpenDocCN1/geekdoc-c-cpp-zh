

将 30（一个无效值）赋给它，第 16 行显示函数 `getHour` 返回的值，以证明给 `hourRef` 赋值实际上修改了 `Time` 对象 `t` 中的 `private` 数据。最后，第 20 行将 `badSetHour` 函数调用本身用作 *左值*，并给函数返回的引用赋值为 74（另一个无效值）。第 25 行再次显示函数 `getHour` 返回的值，以证明对第 20 行函数调用的结果赋值会修改 `Time` 对象 `t` 中的 `private` 数据。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1214_0.png)

## 软件工程

### 观察 9.7

> 返回对 `private` 数据成员的引用或指针会破坏类的封装，并使客户端代码依赖于类数据的表示方式。在某些情况下这样做是合适的——我们将在**第 10.10 节**构建自定义 `Array` 类时展示一个这样的例子。

```cpp
// Fig. 9.13: fig09_13.cpp
// Demonstrating a public member function that
// returns a reference to a private data member.
#include <iostream>
#include "Time.h" // include definition of class Time
using namespace std;

int main() {
   Time t; // create Time object

   // initialize hourRef with the reference returned by badSetHour
   unsigned int& hourRef{t.badSetHour(20)}; // 20 is a valid hour

   cout << "Valid hour before modification: " << hourRef;
   hourRef = 30; // use hourRef to set invalid value in Time object t
   cout << "\nInvalid hour after modification: " << t.getHour();

   // Dangerous: function call that returns
   // a reference can be used as an lvalue!
   t.badSetHour(12) = 74; // assign another invalid value to hour

   cout << "\n\n**************************************************\n"
        << "POOR PROGRAMMING PRACTICE!!!!!!\n"
        << "t.badSetHour(12) as an lvalue, invalid hour: "
        << t.getHour()
        << "\n**************************************************" << endl;
}
```

```text
Valid hour before modification: 20
Invalid hour after modification: 30

**************************************************
POOR PROGRAMMING PRACTICE!!!!!!
t.badSetHour(12) as an lvalue, invalid hour: 74
**************************************************
```

**图 9.13** 返回对**私有**数据成员的引用的**公有**成员函数。

## 9.10 默认逐成员赋值

赋值运算符（`=`）可用于将一个对象赋值给同一个类的另一个对象。默认情况下，这种赋值通过**逐成员赋值**（也称为*复制赋值*）执行——赋值运算符右侧对象的每个数据成员被逐个赋值给赋值运算符左侧对象中*相同*的数据成员。**图 9.14–图 9.15** 定义了一个 `Date` 类。**图 9.16** 中的第 15 行使用**默认逐成员赋值**将 `Date` 对象 `date1` 的数据成员赋值给 `Date` 对象 `date2` 的对应数据成员。在这种情况下，`date1` 的 `month` 成员被赋值给 `date2` 的 `month` 成员，`date1` 的 `day` 成员被赋值给 `date2` 的 `day` 成员，`date1` 的 `year` 成员被赋值给 `date2` 的 `year` 成员。[*注意：* 当类的数据成员包含指向动态分配内存的指针时，逐成员赋值可能会导致严重问题；我们将在**第 10 章**讨论这些问题并说明如何处理它们。]

```cpp
// Fig. 9.14: Date.h
// Date class declaration. Member functions are defined in Date.cpp.
#include <string>

// prevent multiple inclusions of header
#ifndef DATE_H
#define DATE_H

// class Date definition
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

**图 9.14** `Date` 类声明。

```cpp
// Fig. 9.15: Date.cpp
// Date class member-function definitions.
#include <sstream>
#include <string>
#include "Date.h" // include definition of class Date from Date.h
using namespace std;

// Date constructor (should do range checking)
Date::Date(unsigned int m, unsigned int d, unsigned int y)
   : month{m}, day{d}, year{y} {}

// print Date in the format mm/dd/yyyy
string Date::toString() const {
   ostringstream output;
   output << month << '/' << day << '/' << year;
   return output.str();
}
```

**图 9.15** `Date` 类成员函数定义。

```cpp
// Fig. 9.16: fig09_16.cpp
// Demonstrating that class objects can be assigned
// to each other using default memberwise assignment.
#include <iostream>
#include "Date.h" // include definition of class Date from Date.h
using namespace std;

int main() {
   Date date1{7, 4, 2004};
   Date date2; // date2 defaults to 1/1/2000

   cout << "date1 = " << date1.toString()
      << "\ndate2 = " << date2.toString() << "\n\n";

   date2 = date1; // default memberwise assignment

   cout << "After default memberwise assignment, date2 = "
      << date2.toString() << endl;
}
```

```text
date1 = 7/4/2004
date2 = 1/1/2000

After default memberwise assignment, date2 = 7/4/2004
```

**图 9.16** 类对象可以使用默认逐成员赋值相互赋值。

对象可以作为函数参数传递，也可以从函数返回。这种传递和返回默认按值进行——传递或返回的是对象的*副本*。在这种情况下，C++ 会创建一个新对象，并使用**复制构造函数**将原始对象的值复制到新对象中。对于每个类，编译器都提供一个默认复制构造函数，将原始对象的每个成员复制到新对象的对应成员中。与逐成员赋值一样，当类的数据成员包含指向动态分配内存的指针时，复制构造函数也可能导致严重问题。**第 10 章**将讨论如何定义自定义复制构造函数来正确复制此类对象。

## 9.11 `const` 对象和 `const` 成员函数

让我们看看最小权限原则如何应用于对象。有些对象需要可修改，有些则不需要。您可以使用 `const` 指定对象*不可*修改，并且任何修改该对象的尝试都应导致编译错误。以下语句

```cpp
const Time noon{12, 0, 0};
```

声明了一个 `Time` 类的 `const` 对象 `noon`，并将其初始化为中午 12 点。可以实例化同一个类的 `const` 对象和非 `const` 对象。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1219_0.png)

### 错误预防提示 9.5

> *修改 `const` 对象的尝试会在编译时被捕获，而不是导致运行时错误。*

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1220_0.png)

### 性能提示 9.3

> *适当地将变量和对象声明为 `const` 可以提高性能——编译器可以对常量执行无法对非 `const` 变量执行的优化。*

*C++ 不允许对 `const` 对象调用成员函数，除非这些成员函数本身也声明为 `const`。即使是不会修改对象的 get 成员函数也是如此。这也是我们将所有不修改调用对象的成员函数声明为 `const` 的关键原因。*

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1220_1.png)

### 常见编程错误 9.3

> *将一个调用同一个对象上的非 `const` 成员函数的成员函数定义为 `const` 是编译错误。*

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1220_2.png)

### 常见编程错误 9.4

> *在 `const` 对象上调用非 `const` 成员函数是编译错误。*

构造函数和析构函数会出现一个有趣的问题，因为它们通常会修改对象。构造函数*必须*允许修改对象，以便对象可以被初始化。析构函数必须能够在系统回收对象的内存之前执行其终止清理工作。试图将构造函数或析构函数声明为 `const` 是编译错误。`const` 对象的“`const` 性”从构造函数*完成*对象初始化时开始，一直持续到该对象的析构函数被调用为止。

### 使用 `const` 和非 `const` 成员函数

[图 9.17] 中的程序使用了 [图 9.5–图 9.6] 中的 `Time` 类，但移除了函数 `toStandardString` 原型和定义中的 `const`，以便我们展示编译错误。我们创建了两个 `Time` 对象——非 `const` 对象 `wakeUp`（第 6 行）和 `const` 对象 `noon`（第 7 行）。程序试图在 `const` 对象 `noon` 上调用非 `const` 成员函数 `setHour`（第 11 行）和 `toStandardString`（第 15 行）。在每种情况下，编译器都会生成错误消息。程序还演示了另外三种成员函数调用

