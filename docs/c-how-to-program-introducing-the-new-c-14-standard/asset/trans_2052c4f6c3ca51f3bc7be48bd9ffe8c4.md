

## 9.8.4 演示构造函数和析构函数何时被调用

**图 9.8–9.10** 中的程序演示了全局、局部和局部 `static` 的 `CreateAndDestroy` 类对象（**图 9.8** 和**图 9.9**）构造函数与析构函数的调用顺序。`CreateAndDestroy` 类的每个对象包含一个整数（`objectID`）和一个 `string`（`message`），用于在程序输出中标识该对象（**图 9.8**，第 14–15 行）。这个机械化的示例纯粹出于教学目的。因此，**图 9.9** 中析构函数的第 17 行会判断被销毁对象的 `objectID` 是否为 `1` 或 `6`，如果是，就输出一个换行符。这一行使得程序输出更易于阅读。

```cpp
// Fig. 9.8: CreateAndDestroy.h
// CreateAndDestroy class definition.
// Member functions defined in CreateAndDestroy.cpp.
#include <string>

#ifndef CREATE_H
#define CREATE_H

class CreateAndDestroy {
public:
    CreateAndDestroy(int, std::string); // constructor
    ~CreateAndDestroy(); // destructor
private:
    int objectID; // ID number for object
    std::string message; // message describing object
};

#endif
```

图 9.8 **CreateAndDestroy** 类定义。

```cpp
// Fig. 9.9: CreateAndDestroy.cpp
// CreateAndDestroy class member-function definitions.
#include <iostream>
#include "CreateAndDestroy.h" // include CreateAndDestroy class definition
using namespace std;

// constructor sets object's ID number and descriptive message
CreateAndDestroy::CreateAndDestroy(int ID, string messageString)
    : objectID{ID}, message{messageString} {
    cout << "Object " << objectID << " constructor runs  "
         << message << endl;
}

// destructor
CreateAndDestroy::~CreateAndDestroy() {
    // output newline for certain objects; helps readability
    cout << (objectID == 1 || objectID == 6 ? "\n" : "");

    cout << "Object " << objectID << " destructor runs  "
         << message << endl;
}
```

图 9.9 **CreateAndDestroy** 类成员函数定义。

图 9.10 在全局作用域中定义了对象 `first`（第 10 行）。它的构造函数实际上在 `main` 中的任何语句执行*之前*就被调用，而它的析构函数则在程序终止时、所有具有自动存储期对象的析构函数运行*之后*才被调用。

```cpp
// Fig. 9.10: fig09_10.cpp
// Order in which constructors and
// destructors are called.
#include <iostream>
#include "CreateAndDestroy.h" // include CreateAndDestroy class definition
using namespace std;

void create(); // prototype

CreateAndDestroy first{1, "(global before main)"}; // global object

int main() {
   cout << "\nMAIN FUNCTION: EXECUTION BEGINS" << endl;
   CreateAndDestroy second{2, "(local in main)"};
   static CreateAndDestroy third{3, "(local static in main)"};

   create(); // call function to create objects

   cout << "\nMAIN FUNCTION: EXECUTION RESUMES" << endl;
   CreateAndDestroy fourth{4, "(local in main)"};
   cout << "\nMAIN FUNCTION: EXECUTION ENDS" << endl;
}
```

```cpp
// function to create objects
void create() {
    cout << "\nCREATE FUNCTION: EXECUTION BEGINS" << endl;
    CreateAndDestroy fifth(5, "(local in create)");
    static CreateAndDestroy sixth(6, "(local static in create)");
    CreateAndDestroy seventh(7, "(local in create)");
    cout << "\nCREATE FUNCTION: EXECUTION ENDS" << endl;
}
```

```text
Object 1  constructor runs    (global before main)

MAIN FUNCTION: EXECUTION BEGINS
Object 2  constructor runs    (local in main)
Object 3  constructor runs    (local static in main)

CREATE FUNCTION: EXECUTION BEGINS
Object 5  constructor runs    (local in create)
Object 6  constructor runs    (local static in create)
Object 7  constructor runs    (local in create)

CREATE FUNCTION: EXECUTION ENDS
Object 7  destructor runs     (local in create)
Object 5  destructor runs     (local in create)

MAIN FUNCTION: EXECUTION RESUMES
Object 4  constructor runs    (local in main)

MAIN FUNCTION: EXECUTION ENDS
Object 4  destructor runs     (local in main)
Object 2  destructor runs     (local in main)

Object 6  destructor runs     (local static in create)
Object 3  destructor runs     (local static in main)

Object 1  destructor runs     (global before main)
```

图 9.10 构造函数和析构函数的调用顺序。

函数 `main`（第 12–22 行）声明了三个对象。对象 `second`（第 14 行）和 `fourth`（第 20 行）是局部对象，对象 `third`（第 15 行）是一个*静态*局部对象。每个对象的构造函数在程序执行到该对象声明处时被调用。当执行到达 `main` 的末尾时，析构函数按构造函数调用顺序的*逆序*被调用——先 `fourth` 后 `second`。由于对象 `third` 是 `static` 的，它将一直存在到程序终止。对象 `third` 的析构函数在全局对象 `first` 的析构函数*之前*、但在所有其他对象销毁*之后*被调用。

函数 `create`（第 25–31 行）声明了三个对象——`fifth`（第 27 行）和 `seventh`（第 29 行）为局部自动对象，`sixth`（第 28 行）为一个 `static` 局部对象。当 `create` 终止时，析构函数按构造函数调用顺序的*逆序*被调用——先 `seventh` 后 `fifth`。因为 `sixth` 是 `static` 的，它将一直存在到程序终止。`sixth` 的析构函数在 `third` 和 `first` 的析构函数*之前*、但在所有其他对象销毁*之后*被调用。

## 9.9 `Time` 类案例研究：一个潜在的陷阱——返回对 `private` 数据成员的引用或指针

对象的引用是该对象名称的别名，因此可以用在赋值语句的左侧。在这种上下文中，该引用是一个完全可接受的 *lvalue*，可以接收值。

成员函数可以返回对该类 `private` 数据成员的引用。如果引用返回类型声明为 `const`，则该引用是不可修改的 *lvalue*，不能用来修改数据。然而，如果引用返回类型未声明为 `const`，就可能发生微妙的错误。

图 9.11–9.13 中的程序使用一个简化的 `Time` 类（图 9.11 和图 9.12）来演示通过成员函数 `badSetHour`（在图 9.11 第 13 行声明，图 9.12 第 25–34 行定义）返回对 `private` 数据成员的引用。这样的引用返回实际上使对成员函数 `badSetHour` 的调用成为 `private` 数据成员 `hour` 的别名！该函数调用可以像使用该 `private` 数据成员一样被使用，包括作为赋值语句中的 *lvalue*，从而*使类的客户能够随意篡改类的 `private` 数据！* 如果函数返回指向 `private` 数据的指针，也会出现类似的问题。

```cpp
// Fig. 9.11: Time.h
// Time class declaration.
// Member functions defined in Time.cpp

// prevent multiple inclusions of header
#ifndef TIME_H
#define TIME_H

class Time {
public:
    void setTime(int, int, int);
    unsigned int getHour() const;
    unsigned int& badSetHour(int); // dangerous reference return
private:
    unsigned int hour{};
    unsigned int minute{};
    unsigned int second{};
};

#endif
```

**图 9.11** `Time` 类声明。

```cpp
// Fig. 9.12: Time.cpp
// Time class member-function definitions.
#include <stdexcept>
#include "Time.h" // include definition of class Time
using namespace std;

// set values of hour, minute and second
void Time::setTime(int h, int m, int s) {
    // validate hour, minute and second
    if ((h >= 0 && h < 24) && (m >= 0 && m < 60) && (s >= 0 && s < 60)) {
        hour = h;
        minute = m;
        second = s;
    }
    else {
        throw invalid_argument(
            "hour, minute and/or second was out of range");
    }
}

// return hour value
unsigned int Time::getHour() const { return hour;}

// your practice: returning a reference to a private data member.
unsigned int& Time::badSetHour(int hh)
{
    if (hh >= 0 && hh < 24) {
        hour = hh;
    }
    else {
        throw invalid_argument("hour must be 0-23");
    }

    return hour; // dangerous reference return
}
```

**图 9.12** `Time` 类成员函数定义。

**图 9.13** 声明了 `Time` 对象 `t`（第 9 行）和引用 `hourRef`（第 12 行），该引用用调用 `t.badSetHour(20)` 返回的引用进行初始化。第 14 行显示别名 `hourRef` 的值。这显示了 `hourRef` 如何*破坏了类的封装性*——`main` 中的语句不应能访问类的对象中的 `private` 数据。接下来，第 15 行使用该别名来设置 `hour` 的值。
