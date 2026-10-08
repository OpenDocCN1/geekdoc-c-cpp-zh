
**图 9.23** | 友元可以访问类的私成员。

## 9.14 使用 this 指针

重载友函数
可以将重载函数指定为类的友元。每个打算作为友元的函数都必须在类定义中显式声明为该类的友元。

- **软件工程观察 9.10**：尽管友元函数的原型出现在类定义中，但友元并不是成员函数。
- **软件工程观察 9.11**：私有、受保护和公共的概念与友元声明无关，因此友元声明可以放置在类定义中的任何位置。
- **良好的编程实践 9.3**：在类定义的体内部将声明放在前面，并且不要在它们之前添加任何访问修饰符。

每个类的功能只有一份拷贝，但一个类可以有很多个对象，那么成员函数如何知道要操作哪一个对象的数据成员呢？每个对象都通过一个名为 `this` 的指针（一个 C++ 关键字）来访问其本身。该指针不是对象本身——也就是说，该指针所占的内存不会反映在对象的大小中。然而，该指针（由编译器传递）作为对象的非静态成员函数的隐式参数传递。第 9.15 节介绍了静态成员，并解释了为什么该指针不会隐式传递给静态成员函数。

### 使用 this 指针避免命名冲突
成员函数隐式地（正如我们一直所做的）或显式使用指针来引用对象的数据成员和其他成员函数。`this` 指针的一个常见用途是避免类数据成员与成员参数（或其他局部变量）之间的命名冲突。如果一个成员函数包含一个同名的局部变量和数据成员，如下函数所示：

```cpp
// 设置小时值
void Time::setHour(int hour) {
    if (this->hour >= 0 && hour < 24) {
        this->hour = hour; // 使用 this-> 访问数据成员
    } else {
        throw invalid_argument("hour must be 0-23");
    }
}
```

局部变量被视为隐藏或遮蔽（shadow）了数据成员——在成员函数体中使用变量名指的是局部变量而非数据成员。然而，你可以通过用 `this->` 限定其名称来访问数据成员。因此，以下语句将参数的值赋值给数据成员 `hour`：

```cpp
this->hour = hour; // 使用 this-> 访问数据成员
```

### 良好的编程实践 9.4
一种广泛接受的减少标识符名称泛滥的做法是：对设置函数的参数和它的数据成员使用相同的名称，并在设置函数体内通过 `this->` 引用该数据成员。

### this 指针的类型
该指针的类型取决于对象的类型以及声明它的成员函数是否为 `const`：

- 在 `Employee` 类的非 const 成员函数中，指针类型为 `Employee*`——一个指向非常量 `Employee` 的常量指针。
- 在 const 成员函数中，`this` 的类型为 `const Employee*`——一个指向常量 `Employee` 的常量指针。

## 9.14.1 隐式和显式地使用 this 指针访问对象的数据成员

图 9.24 展示了隐式和显式使用 `this` 指针，使 `Test` 类的成员函数能够打印 `Test` 对象的私有数据。在示例和第 10 章中，我们展示了一些使用这种技巧的实质且微妙的示例。

```cpp
// 图 9.24: fig09_24.cpp
// 使用 this 指针引用对象成员。
#include <iostream>
using namespace std;
class Test {
public:
    explicit Test(int);
    void print() const;
private:
    int x;
};
// 构造函数
Test::Test(int value) : x{value} {}
// 使用隐式后显式的 this 指针打印 x；
// * 号周围的括号是必要的
void Test::print() const {
    // 隐式使用 this 指针访问成员 x
    cout << "" << x << endl;
    // 显式使用 this 指针和箭头运算符
    // 访问成员 x
    cout << "\n" << this->x << " " << this->x;
    // 显式使用解引的 this 指针和
    // 点运算符访问成员 x
    cout << "\n" << (*this).x << " " << (*this) << endl;
}
int main() {
    Test setObject{12};
    testObject.print();
}
```

**图 9.24** | 使用 this 指针引用对象成员。（第 I 部分，共 2）

为了说明起，成员函数 `print`（第 19–30 行）首先通过隐式使用 `this` 指针（第 21 行）打印 x——只指定了成员的数据。然后 `print` 使用两种表示法通过 `this` 指针访问 x：通过 `this` 指针使用箭头运算符 (`->`)（第 25 行）以及通过解引的 `this` 指针使用点运算符 (`.`)（第 29 行）。注意在使用成员选择运算符 (`.`) 时，`*this`（第 29 行）需要括号。括号是必要的，因为点运算符的优先级高于星号 `*`。如果没有括号，`*this.x` 将被解析为 `*(this.x)`。

## 9.14 使用 `this` 指针实现链式调用

另一种用法是使用 `this` 指针来实现链式调用（chained method calls）。通过让成员函数返回 `*this` 指针，允许在一行代码中调用多个成员函数。

```cpp
// 图 9.25: Time.h
#ifndef TIME_H
#define TIME_H
#include <string>
#include <sstream>
#include <stdexcept>
#include <iostream>
class Time {
public:
    explicit Time(int hour = 0, int min = 0, int sec = 0);
    Time& setHour(int hour);
    Time& setMinute(int min);
    Time& setSecond(int sec);
    void print() const;
    std::string UniversalString() const;
private:
    int hour;
    int minute;
    int sec;
};
#endif
```

```cpp
// 图 9.25: Time.cpp
#include "Time.h"
using namespace std;
Time::Time(int hour, int min, int sec) {
    setHour(hour);
    setMinute(min);
    setSecond(sec);
}
Time& Time::setHour(int hour) {
    if (hour >= 0 && hour < 24) {
        hour = hour;
    } else {
        throw invalid_argument("hour must be 0-23");
    }
    return *this;
}
Time& Time::setMinute(int min) {
    if (min >= 0 && min < 60) {
        minute = min;
    } else {
        throw invalid_argument("minute must be 0-59");
    }
    return *this;
}
Time& Time::setSecond(int sec) {
    if (sec >= 0 && sec < 60) {
        sec = sec;
    } else {
        throw invalid_argument("second must be 0-59");
    }
    return *this;
}
void Time::print() const {
    cout << hour << ":" << minute << ":" << sec << endl;
}
string Time::UniversalString() const {
    ostringstream output;
    output << fill('0') << setw(2) << hour() << ":"
           << setw(2) << minute() << ":" << setw(2) << sec;
    return output.str();
}
int main() {
    Time t;
    t.setHour(10).setMinute(30).setSecond(45);
    t.print();
    return 0;
}
```

**图 9.25** | Time 类修改以支持链式成员调用。（第 I 部分，共 2）

# 468 第 9 章 类：深入探究

```cpp
// 以标准时间格式（HH:MM:SS AM 或 PM）返回时间
string Time::toStandardString() const {
  ostream& out;
  out << ((getHour() == 0 || getHour() == 12) ? 12 : getHour() % 12)
  << ":" << setfill('0') << setw(2) << getMinute() << ":" << setw(2)
  << ((getHour() < 12) ? " AM" : " PM");
  return out.str();
}
```

**图 9.26** 修改后的 Time 类成员函数定义，以启用级联成员函数调用（部分共 3 部分）

图 9.27 中的程序创建了对象 `t`（第 8 行），然后在级联成员函数调用中使用它（第 10 行和第 18 行）。为什么返回 `*this` 引用的技术有效？点运算符（`.`）从左到右操作，因此第 10 行

```cpp
t.setHour(18).setMinute(30).setSecond(22);
```

首先评估 `t.setHour(18)`，然后返回（进一步更新的）对象的引用作为该函数调用的值。

```cpp
// 图 9.27: fig09_27.cpp
// 使用 this 指针的级联成员函数调用
#include <iostream>
#include "Time.h"
using namespace std;
int main() {
    Time t;
    t.setHour(18).setMinute(30).setSecond(22);
    cout << "Universal time: " << t.toStandardString();
    cout << "\nstandard time: " << t.toStandardString();
    cout << "\nNew standard time: "
         << t.setTime(20, 20, 20).toStandardString() << endl;
}
```
