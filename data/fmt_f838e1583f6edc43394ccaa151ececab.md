
图 9.9 | `CreateDestroy` 成员函数定义。

图 9.10 定义了全局作用范围内的第一行（第10行）。它的构造函数实际上在 `main` 中任何语句执行之前被调用，其析构函数在所有自动生存对象的析构函数运行后的终止时被调用。

```cpp

// 9.10: fig09_10.cpp

// 构造函数和析构函数的调用顺序。

#include <iostream>

#include "CreateDestroy.h" // 包含 CreateDestroy 类定义

using namespace std;

void create(); // 声明

```
图 9.10 | 构造函数和析构函数的调用顺序。（部分 I）。

```cpp

CreateDestroy first(1, "global before main"); // 全局对象

int main() {

    cout << "\nMAIN FUNCTION: EXECUTION BEGINS" << endl;

    CreateDestroy second(2, "local in main");

    static CreateDestroy third(3, "local static in main");

    create(); // 调用创建对象

    cout << "\nMAIN FUNCTION: EXECUTION RESUMES" << endl;

    CreateDestroy fourth(4, "local in main");

    cout << "\nMAIN FUNCTION: EXECUTION ENDS" << endl;

}

// 调用创建对象

void create() {

    cout << "\nCREATE FUNCTION: EXECUTION BEGINS" << endl;

    CreateDestroy fifth(5, "local in create");

    static CreateDestroy sixth(6, "local static in create");

    CreateDestroy seventh(7, "local in create");

    cout << "\nCREATE FUNCTION: EXECUTION ENDS" << endl;

}

```

| Object 1 runs (global before main) |
| MAIN FUNCTION: EXECUTION BEGINS |
| Object 2 runs (local in main) |
| Object 3 runs (local static in main) |
| CREATE FUNCTION: EXECUTION BEGINS |
| Object 5 runs (local in create) |
| Object 6 runs (local static in create) |
| Object 7 runs (local in create) |
| CREATE FUNCTION: EXECUTION ENDS |
| Object 4 runs (local in main) |
| MAIN FUNCTION: EXECUTION RESUMES |
| MAIN FUNCTION: EXECUTION ENDS |

```cpp

unsigned int minute{0};

unsigned int second{0};

}

#endif

```

# 图 9.11 Time 类声明。（2 部分中的第 2 部分）

```cpp

// Fig 9.12: Time.cpp

// Time 类成员函数定义。

#include <stdexcept>

#include "Time.h" // 包含 Time 类的定义

using namespace std;

// n 设置小时、分、秒的值

void Time::setTime(int h, int m, int s) {

    if ((h > 0 && h < 24) && (m >= 0 && m < 60) && (s >= 0 && s < 60)) {

        hour = h;

        minute = m;

        second = s;

    } else {

        throw invalid_argument("hour, minute and/or second is out of range");

    }

}

// 返回

unsigned int Time::getHour() const { return hour; };

// 糟糕的做法：返回私有数据成员的引用。

unsigned int Time::setHour(int hh) {

    if (hh > 0 && hh < 24) {

        hour = hh;

    } else {

        throw invalid_argument("hour must be 0-23");

    }

    return hour; // 危险的引用返回

}

```

# 图 9.2 Time 类成员函数定义。

9.13 声明了 `Time` 对象（第 9 行）和引用 `hourRef`（第 12 行），它通过调用 `badHour(0)` 返回的引用进行初始化。第 14 行显示了别名 `hourRef` 的值。这展示了 `hourRef` 如何破坏类的封装——`main` 函数中的状态应该有访问该类对象中私有数据的权限。接下来，第 15 行使用该别名将 `hour` 的值设置为 30（无效值），第 16 行显示了函数 `getHour` 返回的值，这说明给 `hourRef` 赋值实际上修改了 `Time` 对象中的私有数据。最后，第 20 行将 `badHour` 函数调用本身本身一个值，并将 74（另一个无效值）赋值给函数返回的引用。第 25 行显示了函数 `getHour` 返回的值，说明给第 20 行调用的结果赋值修改了对象 `t` 中的私有数据。

![](img/09cee61886647f0b1e06dc44c0065a38_451_0.png)

> 软件工程观察 9.7
> 返回私有数据成员的引用或指针会破坏类的封装，并使客户端代码依赖于类数据的表示。在某些情况下，这样做是恰当的——我们将在第 10.10 节构建自定义 `Array` 类时展示这样一个例子。

```cpp

// Fig 9.13: fig013.cpp

// 演示一个返回私有数据成员引用的

// 公有成员函数。

#include <iostream>

#include "time.h" // 包含 Time 类的定义

using namespace std;

int main() {

    Time t; // 创建 Time 对象

    // 使用 badSetHour 返回的引用初始化 hourRef

    unsigned int& hourRef(t.badSetHour(20)); // 20 是有效值

    cout << "Valid before modification: " << hourRef;

    hourRef = 30; // 使用 hourRef 设置 Time 对象 t 中的无效值

    cout << "Invalid hour after modification: " << t.getHour();

    // 危险：返回引用的函数调用

    // 可以作为左值！

    t.badSetHour(12) = 74; // 给 hour 赋值另一个无效值

    cout << "\n============================================\n";

    cout << "POOR PROGRAMMING PRACTICE!!!\n";

    cout << t.badSetHour(12) as an lvalue, invalid hour: ";

    cout << t.getHour();

    cout << "\n============================================\n" << endl;

}

```

Valid before modification: 20
Invalid hour after modification: 30

********************************************
POOR PROGRAMMING PRACTICE!!!!!!
t.badSetHour(12) as an lvalue, invalid hour: 74
********************************************

**图 9.13 | 返回私有数据成员引用的公有成员函数。**

# 9.10 默认成员级赋值

赋值运算符 (`=`) 可用于将一个对象赋值给同类类的另一个对象。默认情况下，赋值是通过成员级赋值（也称为拷贝赋值）完成的——赋值运算符右侧对象的每个数据成员都被单独赋值给赋值运算符左侧对象的相同数据成员。图 9.14–9.15 定义了一个 `Date` 类。9.16 的第 15 行使用默认成员级赋值将 `Date` 对象 `date1` 的数据成员赋值给 `Date` 对象 `date2` 的对应数据成员。在这种情况下，`date1` 的 `month` 成员被赋值给 `date2` 的 `day` 成员，[注意：当类的数据成员包含指向动态分配内存的指针时，使用成员级赋值可能会导致严重问题；我们将在第 10 章讨论这些问题以及如何处理它们。]

```cpp

// Fig 9.14: Date.h

// Date 类声明。成员函数在 Date.cpp 中定义。

#include <string>

// 防止头文件重复包含

#ifndef DATE

#define DATE

// 类定义

class Date {

public:

    explicit Date(int month = 1, int day = 1, int year = 2000);

    std::string toString() const;

private:

    int month;

    int day;

    int year;

};

#endif

```
**图 9.14 | Date 类声明。**

```cpp

// Fig 9.15: Date.cpp

// Date 类成员函数定义。

#include <iostream>

#include <string>

#include "Date.h"

using namespace std;

// Date 构造函数（带范围检查）

Date::Date(int m, int d, int y)

    : month(m), day(d), year(y) {}

// 以 mm/dd/yyyy 格式打印 Date

string Date::toString() const {

    stringstream output;

    output << month << "/" << day << "/" << year;

    return output.str();

}

```
**15 | 成员函数定义。**

```cpp

// Fig 9.16: fig016.cpp

// 演示对象可以通过成员级赋值

// 进行赋值。

#include <iostream>

#include "Date.h"

using namespace std;

int main() {

    Date date1(7, 15, 2004);

    Date date2;

    date2 = date1; // 使用默认成员级赋值

    cout << "date1: " << date1.toString() << endl;

    cout << "date2: " << date2.toString() << endl;

    date2.day = 20; // 修改 date2

    cout << "date1 after modification: " << date1.toString() << endl;

    cout << "date2 after modification: " << date2.toString() << endl;

}

```

date1: 7/15/2004
date2: 7/15/2004
date1 after modification: 7/15/2004
date2 after modification: 7/20/2004

**图 9.16 | 成员级赋值。**

# 9.11 const 对象与成员函数

让我们看看最小权限原则如何应用于对象。有些对象需要是修改的。使用 `const` 可以指定对象是不可修改的。

```cpp

const Time noon{12, 0, 0};

```

声明了一个 `Time` 的 `const` 对象并将其初始化为 12 点。

![](img/09cee61886647f0b1e06dc44c0065a38_453_0.png)

# 性能提示 9.3

在适当的情况下将变量和对象声明为 `const` 可以提高性能——编译器对常量进行优化，而对非 const 变量不能。

C++ 允许 `const` 对象调用成员函数，只要这些成员函数本身被声明为 `const`。这也是我们为不修改对象的成员函数声明 `const` 的关键原因。

# 常见错误 9.3

在成员函数中调用该对象的非 const 成员函数会导致编译错误。

# 常见错误 9.4

在 `const` 对象上调用非 const 成员函数会导致编译错误。

一个有趣的问题出现在构造函数和析构函数中，每个通常都会修改对象。构造函数必须允许修改对象以便初始化对象。析构函数必须能够在对象内存被系统回收之前执行清理工作。尝试将构造函数或析构函数声明为 `const` 是编译错误。`const` 对象的“常量性”从对象初始化完成一直到该对象被销毁。

## 9.12 组合：对象作为类的成员

```cpp

// 对象成员函数

wakeup.setHour(18);      // 非 const 非 const

noon.setHour(12);       // const 非 const

wakeup.getHour();        // 非 const const

noon.getMinute();       // const const

noon.toUniversalString(); // const const

noon.toStandardString(); // const 非 const

```

Microsoft Visual C++ 编译器错误信息：

```

C:\examples\ch09_fig09_17.cppfig09_17.cpp(11): error C2662:

'void Time::setTime(int): cannot convert 'this' pointer from 'const Time'

to 'Time'

C:\examples\ch09_fig09_17.cppfig09_17.cpp(11): note: Conversion loses qualifiers

C:\examples\ch09_fig09_17.cppfig09_17.cpp(15): error C2662:

'std::string Time::toStandardString(void): cannot convert 'this' pointer

from 'const Time' to 'Time'

C:\examples\ch09_fig09_17.cppfig09_17.cpp(15): note: Conversion loses qualifiers
