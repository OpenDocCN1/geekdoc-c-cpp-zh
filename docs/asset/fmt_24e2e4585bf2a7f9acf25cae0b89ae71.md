
![](img/09cee61886647f0b1e06dc44c0065a38_460_0.png)

**图 9.22** 演示组合——一个包含成员对象的对象。

`Date`类和`Employee`类都包含一个析构函数（分别见图 9.19 的第 30–32 行和图 9.21 的第 31–34 行）。这使我们能够在输出中确认对象是从*内部*构造的，并按照*反*序从外部向内部销毁（即`Date`成员对象在它们所包含的`Employee`对象之后被销毁）。

注意图 9.22 输出中的四行。最后几行是`Date`析构函数运行在`Date`对象（第 10 行）和`birth`（第 9 行）上的输出。输出确认了在`main`中创建的三个`Date`对象是按照它们构造顺序的*反*序被销毁的。`Employee`析构函数的输出位于倒数五行，显示了`Employee`的成员对象`hireDate`（图 9.20，第 22 行）和`birthDate`（第 21 行）的析构函数。输出的最后两行对应于图 9.22 第 10 行和第 9 行创建的`Date`对象。

这些输出确认了`Employee`对象是从内部向外部销毁的——即`Employee`析构函数首先运行（从输出窗口底部），然后成员对象按照它们构造的反向顺序被销毁。`string`析构函数不包含输出语句，因此我们没有看到`firstName`和`lastName`对象被销毁。同样，图 9.22 的输出没有显示成员对象`birthDate`和`hireDate`的构造函数运行，因为这些对象是用编译器提供的*默认*`Date`类构造函数初始化的。

## 9.13 友函数和友元类

### 当你不使用成员初始化列表会发生什么？
如果成员没有通过成员初始化列表初始化，则会隐式调用成员对象的默认构造函数。默认构造函数建立的值（如果有的话）可以通过`set`函数覆盖。然而，对于复杂的初始化，这种方法可能需要大量工作和时间。

![](img/09cee61886647f0b1e06dc44c0065a38_461_0.png)

**性能提示 9.4**
通过成员初始化器显式地初始化成员对象。这消除了“双重初始化”对象的开销——一次是在成员对象的默认构造函数被调用时，另是在构造函数体（或之后）调用`set`函数来初始化成员对象时。

![](img/09cee61886647f0b1e06dc44c0065a38_461_1.png)

**常见编程错误 9.5**
如果成员对象没有通过成员初始化器初始化，且成员对象的类没有提供默认构造函数，则会发生编译错误（即成员对象的类定义了一个或多个构造函数，但没有一个是默认构造函数）。

![](img/09cee61886647f0b1e06dc44c0065a38_461_2.png)

**软件工程观察 9.9**
如果数据成员是另一个类，将该成员对象设为公共并不违反该成员对象私有成员的封装和隐藏。但是，它违反了外层类实现的封装和隐藏，因此类类型的成员对象仍应为私有。

类的友函数是一个具有访问公共和非公有成员类权限的非函数。独立函数、整个类或其他类的成员函数都可以声明为另一个类的友元。

本节介绍了一个关于友函数如何工作的机械性示例。第 10 章将展示重载运算符以用于类对象的友函数——你会发现，有时成员函数无法用于某些重载运算符。

### 声明友元
要将非成员函数声明为类的友元，请将函数原型放在类中并用`friend`关键字进行定义。要将`ClassTwo`的所有成员函数声明为`ClassOne`的友元，请在`ClassOne`的定义中放置如下形式的声明：

```cpp
friend class ClassTwo;
```

友元声明出现在类的任何地方，且不受访问说明符`public`、`private`（或`protected`，我们在第 11 章中讨论）的影响。

友元关系是授予的，而不是要求的——要让类`B`成为类`A`的友元，类`A`必须显式声明类`B`是类`A`的友元。友元关系不是对称的——如果类`A`是类`B`的友元，你不能推导出类`B`是类`A`的友元。

## 第 9 章 类：深入观察

### 修改类
图 9.23：
`Date`类和`Employee`类包含一个析构函数（分别见图 9.19 的第 30–32 行和图 9.21 的第 31–34 行）。这使我们能够在输出中确认对象是从*内部*构造的，并按照*反*序从外部向内部销毁（即`Date`成员对象在它们所包含的`Employee`对象之后被销毁）。

```cpp
// 图 9.22: fig09_22.cpp
// 演示组合——一个包含成员对象的对象。
#include <iostream>
#include "Date.h" // Date 类定义
#include "Employee.h" // Employee 类定义
using namespace std;
int main() {
    Date birth(7, 24, 1949);
    Date hire(3, 12, 1983);
    Employee manager("Bob", "Blue", birth, hire);
    cout << "\n" << manager.toString() << endl;
}
```

![](img/09cee61886647f0b1e06dc44c0065a38_460_0.png)

**图 9.22** 演示组合——一个包含成员对象的对象。

注意图 9.22 输出中的四行。最后几行是`Date`析构函数运行在`Date`对象（第 10 行）和`birth`（第 9 行）上的输出。输出确认了在`main`中创建的三个`Date`对象是按照它们构造顺序的*反*序被销毁的。`Employee`析构函数的输出位于倒数五行，显示了`Employee`的成员对象`hireDate`（图 9.20，第 22 行）和`birthDate`（第 21 行）的析构函数。输出的最后两行对应于图 9.22 第 10 行和第 9 行创建的`Date`对象。

这些输出确认了`Employee`对象是从内部向外部销毁的——即`Employee`析构函数首先运行（从输出窗口底部），然后成员对象按照它们构造的反向顺序被销毁。`string`析构函数不包含输出语句，因此我们没有看到`firstName`和`lastName`对象被销毁。同样，图 9.22 的输出没有显示成员对象`birthDate`和`hireDate`的构造函数运行，因为这些对象是用编译器提供的*默认*`Date`类构造函数初始化的。

## 9.14 使用 this 指针

每个类的功能只有一个副本，但一个类可以有很多对象，那么成员函数如何知道操作哪个对象的数据成员呢？每个对象都通过一个名为`this`（C++ 关键字）的指针来访问自己。这个指针不是对象的一部分——即该指针占据的内存不会反映在对象的`sizeof`中。然而，这个指针由编译器作为对象非静态成员函数的隐式参数传递。第 9.15 节引入了静态类成员，并解释了为什么该指针不会隐式传递给静态成员函数。

### 使用 this 指针避免命名冲突
成员函数隐式地（如我们所做的那样）或显式地使用`this`指针来引用对象的数据成员和其他成员函数。`this`指针的一个常见用途是避免类数据成员与成员函数（或其他局部变量）之间的命名冲突。如果成员函数包含与同名的局部变量和数据成员，如下函数所示：

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

局部变量被称为隐藏或遮蔽了数据成员——在成员函数体内使用变量名指的是局部变量而不是数据成员。然而，你可以通过`this->`修饰其名称来访问数据成员。因此，以下语句将参数`hour`的值赋值给数据成员`hour`：

```cpp
this->hour = hour; // 使用 this-> 访问数据成员
```

# 良好的编程实践 9.4

一种广泛接受的减少标识符名称泛滥的方法是：为设置函数的参数和它设置的数据成员使用相同的名称，并在设置函数的体中通过`this->`引用该数据成员。

## this 指针的类型

`this`指针的类型取决于对象的类型以及使用它的成员函数是否被声明为`const`：

- 在`Employee`类的非`const`成员函数中，指针的类型为`Employee const`——一个指向非`const` `Employee`的常量指针。
- 在`const`成员函数中，`this`的类型为`const Employee const`——一个指向常量`Employee`的常量指针。

## 9.14. 隐式和显式使用 this 指针访问对象的数据成员

图 9.24 展示了`this`指针的隐式和显式使用，以使`Test`类的成员函数能够打印`Test`对象的数据`x`。在示例和第 10 章中，我们展示了一些使用这种技巧的实质性且微妙的示例。

```cpp
// Fig. 9.24: fig09_24.cpp
// 使用 this 指针引用对象成员。
#include <iostream>
using namespace std;
class Test {
public:
    explicit Test(int);
    void print() const;
private:
    int x[0];
};
// 构造函数
Test::Test(int value) : x{value} {} // 将 x 初始化为 value
// 隐式后显式使用 this 指针打印；
// *this 外围的括号是必要的
void Test::print() const {
    // 隐式使用 this 指针来访问成员 x
    cout << x << endl;
    // 显式使用 this 指针和箭头运算符
    // 来访问成员 x
    cout << "\n" << this->x << " " << this->x << endl;
}
```

**9.24** | 使用 this 指针引用对象成员。（第 2 部分的第一）。

```cpp
// 27 显式使用解引用后的 this 指针和
// 28 点运算符来访问成员 x
29 cout << "\n" << (*this).x << " " << (*this) << endl;
30 }
32 int main() {
33 Test testObject{12}; // 实例化并初始化 testObject
34 testObject.print();
35 }
37 x = 12
38 this->x = 12
39 (*this).x = 12
```

![](img/09cee61886647f0b1e06dc44c0065a38_465_0.png)

为了说明，成员函数`print`（第 19–30 行）通过隐式使用`this`指针（第 21 行）打印`x`——仅指定了数据成员。然后`print`使用两种不同的符号通过`this`指针访问`x`——箭头运算符 (`->`) `this`指针（第 25 行）和点运算符 (`.`) 解引用后的`this`指针（第 29 行）。注意在与成员选择运算符 `()` 使用时，括号 `*this`（第 29 行）是必要的。之所以需要括号，是因为点运算符的优先级高于 `*` 运算符。如果没有括号，表达式 `*this.x` 的求值将等同于带括号的 `*(this.x)`，这会导致编译错误，因为点运算符不能与指针一起。

`this`指针的一个有趣用途是防止对象被赋值给自己。正如我们在第 10 章中看到的，当对象包含指向动态分配存储的指针时，自赋值会导致严重的错误。

## 9.14.2. 使用 this 指针实现级联函数调用

`this`指针的另一个用途是实现级联成员函数调用——即在同一个语句中调用多个函数（见图 9.27 的第 10 行）。图 9.25–9.27 的程序修改了`Time`类的`setTime`、`setHour`、`setMinute`和`setSecond`，这些函数每个都返回所用的`Time`对象的引用，以实现级联成员函数调用。注意图 9.26 中，这些成员函数体中的最后一个状态返回`*this`（第 21, 33, 45 和 57 行），返回类型为`Time`。

```cpp
// Fig. 9.25: Time.h
// 修改后的 Time 类以实现级联成员函数调用。
#include <string>
// Time 类定义。
// 在 Time.cpp 中定义的成员函数。
#ifndef TIME_H
#define TIME_H
```

![](img/09cee61886647f0b1e06dc44c0065a38_465_1.png)

# 第 9 章 类：深入观察

```cpp
class Time {
public:
    explicit Time(int = 0, int = 0, int = 0); // 构造函数
    // 设置函数（Time& 返回类型实现了级联）
    setTime(int, int, int); // 设置小时、分、秒
    setHour(int); // 设置小时
    setMinute(int); // 设置分
    setSecond(int); // 设置秒
    unsigned getHour() const; // 返回小时
    unsigned getMinute() const; // 返回分钟
    unsigned    unsigned getSecond() const; // 返回秒
    std::string toUniversalString() const; // 24小时格式
    std::string toString() const; // 12小时格式
private:
    unsigned hour; // 24小时
    unsigned minute; // 24小时
    unsigned second; // 24小时
};
#endif
```

图 9.25 | 修改后的 Time 类以实现级联成员函数调用。

```cpp
// Fig 9.26: Time.cpp
// 成员函数定义以
级联函数调用。
#include <iomanip>
#include <sstream>
#include <except>
#include "Time.h" // Time 类定义
using namespace std;
// 构造函数初始化变量;
// 默认值用于 Time（定义）
Time(int hr, int min, int sec) {
    setTime(hr, min, sec);
}
// 设置小时、分、秒
Time& setTime(int h, int m, int sec) {
    hour = h;
    minute =;;
    return;
;
```
