
实用函数的一种做法是将一些公共代码放到一个函数中，否则这些代码会在其他多个成员函数中重复。

## 9.6 `Time` 类案例研究：带默认实参的构造函数

**图 9.5–9.7** 中的程序增强了 `Time` 类，以演示如何隐式地将实参传递给构造函数。

### 9.6.1 带默认实参的构造函数

与其他函数一样，构造函数可以指定*默认实参*。[图 9.5] 的第 13 行声明了一个带默认实参的 `Time` 构造函数，为传递给构造函数的每个实参指定默认值零。该构造函数被声明为 `explicit`，因为它可以用一个实参调用。我们将在[第 10.13 节]详细讨论 `explicit` 构造函数。

```cpp
// Fig. 9.5: Time.h
// Time class containing a constructor with default arguments.
// Member functions defined in Time.cpp.
#include <string>

// prevent multiple inclusions of header
#ifndef TIME_H
#define TIME_H

// Time class definition
class Time {
public:
    explicit Time(int = 0, int = 0, int = 0); // default constructor

    // set functions
    void setTime(int, int, int); // set hour, minute, second
    void setHour(int); // set hour (after validation)
    void setMinute(int); // set minute (after validation)
    void setSecond(int); // set second (after validation)

    // get functions
    unsigned int getHour() const; // return hour
    unsigned int getMinute() const; // return minute
    unsigned int getSecond() const; // return second

    std::string toUniversalString() const; // 24-hour time format string
    std::string toStandardString() const; // 12-hour time format string
private:
    unsigned int hour{0}; // 0 - 23 (24-hour clock format)
    unsigned int minute{0}; // 0 - 59
    unsigned int second{0}; // 0 - 59
};

#endif
```

**图 9.5** 包含带默认实参构造函数的 `Time` 类。

在**图 9.6**中，第 11–13 行定义了 `Time` 构造函数，它接收形参 `hour`、`minute` 和 `second` 的值，这些值将分别用于初始化 `private` 数据成员 `hour`、`minute` 和 `second`。*将所有实参都设为默认值的构造函数也是默认构造函数——也就是说，是可以在不传实参的情况下调用的构造函数。* 每个类最多只能有一个默认构造函数。本示例中 `Time` 类的版本为每个数据成员提供 *set* 和 *get* 函数。现在 `Time` 构造函数调用 `setTime`，后者调用 `setHour`、`setMinute` 和 `setSecond` 函数来验证并给数据成员赋值。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1190_0.png)

### 软件工程观察 9.4

> *对函数默认实参值的任何更改都要求重新编译客户端代码（以确保程序仍能正确运行）。*

```cpp
// Fig. 9.6: Time.cpp
// Member-function definitions for class Time.
#include <iomanip>
#include <stdexcept>
#include <iostream>
#include <string>
#include "Time.h" // include definition of class Time from Time.h
using namespace std;

// Time constructor initializes each data member
Time::Time(int hour, int minute, int second) {
   setTime(hour, minute, second); // validate and set time
}

// set new Time value using universal time
void Time::setTime(int h, int m, int s) {
   setHour(h); // set private field hour
   setMinute(m); // set private field minute
   setSecond(s); // set private field second
}

// set hour value
void Time::setHour(int h) {
   if (h >= 0 && h < 24) {
      hour = h;
   }
   else {
      throw invalid_argument("hour must be 0-23");
   }
}

// set minute value
void Time::setMinute(int m) {
    if (m >= 0 && m < 60) {
        minute = m;
    }
    else {
        throw invalid_argument("minute must be 0-59");
    }
}

// set second value
void Time::setSecond(int s) {
    if (s >= 0 && s < 60) {
        second = s;
    }
    else {
        throw invalid_argument("second must be 0-59");
    }
}

// return hour value
unsigned int Time::getHour() const {return hour;}

// return minute value
unsigned int Time::getMinute() const {return minute;}

// return second value
unsigned int Time::getSecond() const {return second;}

// return Time as a string in universal-time format (HH:MM:SS)
string Time::toUniversalString() const {
    ostringstream output;
    output << setfill('0') << setw(2) << getHour() << ":"
        << setw(2) << getMinute() << ":" << setw(2) << getSecond();
    return output.str();
}

// return Time as a string in standard-time format (HH:MM:SS AM or PM)
string Time::toStandardString() const {
    ostringstream output;
    output << ((getHour() == 0 || getHour() == 12) ? 12 : getHour() % 12)
        << ":" << setfill('0') << setw(2) << getMinute() << ":" << setw(2)
        << getSecond() << (getHour() < 12 ? " AM" : " PM");
    return output.str();
}
```

图 9.6 类 `Time` 的成员函数定义。

在**图 9.6**中，构造函数的第 12 行用传递给构造函数的值（或默认值）调用成员函数 `setTime`。函数 `setTime` 调用 `setHour` 以确保为 `hour` 提供的值在 0–23 范围内，然后调用 `setMinute` 和 `setSecond` 以确保 `minute` 和 `second` 的值各自在 0–59 范围内。函数 `setHour`（第 23–30 行）、`setMinute`（第 33–40 行）和 `setSecond`（第 43–50 行）在收到超出范围的实参时都会抛出异常。

**图 9.7**中的函数 `main` 初始化五个 `Time` 对象——一个在隐式构造函数调用中三个实参全部默认（第 15 行），一个指定一个实参（第 16 行），一个指定两个实参（第 17 行），一个指定三个实参（第 18 行），以及一个指定三个无效实参（第 28 行）。每个显式构造函数调用（第 16–18 行和第 28 行）都使用 C++11 列表初始化器语法。程序以通用时间格式和标准时间格式显示每个对象。对于 `Time` 对象 `t5`（第 28 行），程序显示错误消息，因为构造函数实参超出范围。

```cpp
// Fig. 9.7: Fig09_07.cpp
// Constructor with default arguments.
#include <iostream>
#include <stdexcept>
#include "Time.h" // include definition of class Time from Time.h
using namespace std;

// displays a Time in 24-hour and 12-hour formats
void displayTime(const string& message, const Time& time) {
   cout << message << "\nUniversal time: " << time.toUniversalString()
      << "\nStandard time: " << time.toStandardString() << "\n\n";
}

int main() {
   Time t1; // all arguments defaulted
   Time t2{2}; // hour specified; minute and second defaulted
   Time t3{21, 34}; // hour and minute specified; second defaulted
   Time t4{12, 25, 42}; // hour, minute and second specified

   cout << "Constructed with:\n\n";
   displayTime("t1: all arguments defaulted", t1);
   displayTime("t2: hour specified; minute and second defaulted", t2);
   displayTime("t3: hour and minute specified; second defaulted", t3);
   displayTime("t4: hour, minute and second specified", t4);

   // attempt to initialize t5 with invalid values
   try {
      Time t5{27, 74, 99}; // all bad values specified
   }
   catch (invalid_argument& e) {
      cerr << "Exception while initializing t5: " << e.what() << endl;
   }
}
```

```
Constructed with:

t1: all arguments defaulted
Universal time: 00:00:00
Standard time: 12:00:00 AM

t2: hour specified; minute and second defaulted
Universal time: 02:00:00
Standard time: 2:00:00 AM

t3: hour and minute specified; second defaulted
Universal time: 21:34:00
Standard time: 9:34:00 PM

t4: hour, minute and second specified
Universal time: 12:25:42
Standard time: 12:25:42 PM

Exception while initializing t5: hour must be 0-23
```

图 9.7 带默认实参的构造函数。

## 关于类 `Time` 的 Set 和 Get 函数以及构造函数的说明

`Time` 的 set 和 get 函数在整个类体中被调用。具体来说，函数 `setTime`（**图 9.6** 的第 16–20 行）调用函数 `setHour`、`setMinute` 和 `setSecond`，而函数 `toUniversalString` 和 `toStandardString` 在第 64–65 行和第 72–74 行调用函数 `getHour`、`getMinute` 和 `getSecond`。

在每种情况下，这些函数本来可以直接访问类的 `private` 数据。然而，考虑将时间的表示从三个 `int` 值（在 `int` 为四字节的系统上需要 12 字节内存）改为一个 `int` 值，表示自午夜以来经过的总秒数（只需要四字节内存）。如果我们做出这样的更改，只有直接访问 `private` 数据的函数体需要更改——特别是 `hour`、`minute` 和 `second` 各自的 set 和 get 函数。无需修改函数 `setTime`、`toUniversalString` 或 `toStandardString` 的函数体，因为它们*不*直接访问数据。

同样，`Time` 构造函数可以编写为包含函数 `setTime` 中相应语句的副本。这样做可能稍微更高效，因为消除了对 `setTime` 的额外调用。
