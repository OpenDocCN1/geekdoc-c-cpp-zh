

```cpp
18    // output x
19    void print() const
20    {
21        cout << x << endl;
22    } // end function print
23    private:
24        int x; // data member
25    }; // end class Count

27    // function setX can modify private data of Count
28    // because setX is declared as a friend of Count (line 9)
29    void setX( Count &c, int val )
30    {
31        c.x = val; // allowed because setX is a friend of Count
32    } // end function setX

34    int main()
35    {
36        Count counter; // create Count object

38        cout << "counter.x after instantiation: ";
39        counter.print();

41        setX( counter, 8 ); // set x using a friend function
42        cout << "counter.x after call to setX friend function: ";
43        counter.print();
44    } // end main
```

```
counter.x after instantiation: 0
counter.x after call to setX friend function: 8
```

图 10.15 | 友元可以访问类的私有成员。（共 2 部分，第 2 部分。）

函数 setX（第 29–32 行）是一个 C 风格的独立函数，并不是类 Count 的成员函数。因此，在针对对象 counter 调用 setX 时，第 41 行将 counter 作为参数传递给 setX，而不是像下面这样使用句柄（例如对象的名称）调用函数：

```cpp
counter.setX( 8 );
```

如果删除第 9 行中的友元声明，将收到错误消息，指出函数 setX 无法修改类 Count 的私有数据成员 x。

正如我们所提到的，图 10.15 是使用 friend 构造的一 个机械式示例。通常，应将函数 setX 定义为类 Count 的成员函数。此外，通常还应将图 10.15 中的程序拆分为三个文件：

- 1. 头文件（例如 Count.h），其中包含 Count 类的定义，而该定义中又包含友元函数 setX 的原型
- 2. 实现文件（例如 Count.cpp），其中包含 Count 类成员函数的定义以及友元函数 setX 的定义
- 3. 测试程序（例如 Fig10_15.cpp），其中包含 main。

### 重载的友元函数

可以将重载函数指定为某个类的友元。每个要成为友元的函数都必须在类定义中显式声明为该类的友元。

## 10.5 使用 *this* 指针

我们已经了解到，对象的成员函数可以操作对象的数据。那么，成员函数如何知道要操作*哪个*对象的数据成员呢？每个对象都可以通过一个名为 *this* 的指针访问自身的地址（*this* 是 C++ 关键字）。*this* 指针本身并不是对象的一部分——也就是说，*this* 指针所占用的内存不会反映在对对象执行 `sizeof` 操作的结果中。相反，编译器会将 *this* 指针作为隐式参数传递给对象的每个非-*static* 成员函数。第 10.6 节将介绍 *static* 类成员，并解释为什么 *this* 指针不会隐式传递给 *static* 成员函数。

对象可以隐式地（正如我们目前所做的那样）或显式地使用 *this* 指针来引用其数据成员和成员函数。*this* 指针的类型取决于对象的类型，以及使用 *this* 的成员函数是否声明为 `const`。例如，在类 `Employee` 的非常量成员函数中，*this* 指针的类型为 `Employee * const`（指向非常量 `Employee` 对象的常量指针）。在类 `Employee` 的常量成员函数中，*this* 指针的数据类型为 `const Employee * const`（指向常量 `Employee` 对象的常量指针）。

下一个示例展示了 *this* 指针的隐式和显式用法；在本章后面的内容以及第 11 章中，我们还将展示一些使用 *this* 的重要且细微的示例。

### 隐式和显式使用 *this* 指针访问对象的数据成员

图 10.16 展示了如何隐式和显式使用 *this* 指针，使类 `Test` 的成员函数能够打印 `Test` 对象的私有数据 `x`。

```cpp
    1  // Fig. 10.16: fig10_16.cpp
    2  // Using the this pointer to refer to object members.
    3  #include <iostream>
    4  using namespace std;
    5
    6  class Test
    7  {
    8  public:
    9      Test( int = 0 ); // default constructor
    10     void print() const;
    11 private:
    12     int x;
    13 }; // end class Test
    14
    15 // constructor
    16 Test::Test( int value )
    17     : x( value ) // initialize x to value
    18 {
    19     // empty body
    20 } // end constructor Test
```

**图 10.16** | *this* 指针隐式和显式地访问对象的成员。（共 2 部分，第 1 部分。）

```cpp
    21     
    22     // print x using implicit and explicit this pointers;
    23     // the parentheses around *this are required
    24     void Test::print() const
    25     {
    26       // implicitly use the this pointer to access the member x
    27       cout << "x = " << x << endl;
    28
    29       // explicitly use the this pointer and the arrow operator
    30       // to access the member x
    31       cout << "this->x = " << this->x << endl;
    32
    33       // explicitly use the dereferenced this pointer and
    34       // the dot operator to access the member
    35       cout << "\n(*this).x = " << (*this).x << endl;
    36     } // end function print
    37
    38     int main()
    39     {
    40       Test testObject( 12 ); // instantiate and initialize testObject
    41
    42       testObject.print();
    43     } // end main
```

```
     x = 12
     this->x = 12
     (*this).x = 12
```

**图 10.16** | *this* 指针隐式和显式地访问对象的成员。（共 2 部分，第 2 部分。）

为便于说明，成员函数 `print`（第 24–36 行）首先通过隐式使用 `this` 指针来打印 x（第 27 行）——这里只指定了数据成员的名称。然后，`print` 使用两种不同的表示法，通过 `this` 指针访问 x：一种是使用 `this` 指针上的箭头运算符（`->`）（第 31 行），另一种是使用解引用后的 `this` 指针上的点运算符（`.`）（第 35 行）。请注意，在使用点成员选择运算符（`.`）时，`*this` 两侧的括号（第 35 行）是必需的。这是因为点运算符的优先级高于 `*` 运算符。如果没有括号，表达式 `*this.x` 将按照添加括号后的 `*(this.x)` 进行求值，这会导致编译错误，因为点运算符不能与指针一起使用。

> **常见编程错误 10.7**
>
> *尝试将成员选择运算符（.）与指向对象的指针一起使用会导致编译错误——点成员选择运算符只能与左值一起使用，例如对象的名称、对象的引用或指向对象的指针解引用后的结果。*

`this` 指针的一个有趣用途是防止对象被赋值给自身。正如我们将在第 11 章中看到的那样，当对象包含指向动态分配存储空间的指针时，自赋值可能会导致严重错误。

### 使用 *this* 指针实现链式函数调用

*this* 指针的另一个用途是实现链式成员函数调用，也就是在同一条语句中调用多个函数（如图 10.19 第 12 行所示）。图 10.17–10.19 中的程序修改了类 Time 的设置函数 setTime、setHour、setMinute 和 setSecond，使每个函数都返回一个 Time 对象的引用，从而实现链式成员函数调用。请注意，在图 10.18 中，这些成员函数各自函数体中的最后一条语句都将 `*this`（第 22、29、36 和 43 行）返回到 `Time &` 返回类型中。

```cpp
// Fig. 10.17: Time.h
// Cascading member function calls.

// Time class definition.
// Member functions defined in Time.cpp.
#ifndef TIME_H
#define TIME_H

class Time
{
public:
    Time( int = 0, int = 0, int = 0 ); // default constructor

    // set functions (the Time & return types enable cascading)
    Time &setTime( int, int, int ); // set hour, minute, second
    Time &setHour( int );            // set hour
    Time &setMinute( int );          // set minute
    Time &setSecond( int );          // set second

    // get functions (normally declared const)
    int getHour() const;   // return hour
    int getMinute() const; // return minute
    int getSecond() const; // return second

    // print functions (normally declared const)
    void printUniversal() const; // print universal time
    void printStandard() const;  // print standard time
private:
    int hour;   // 0 - 23 (24-hour clock format)
    int minute; // 0 - 59
    int second; // 0 - 59
}; // end class Time

#endif
```

**图 10.17** | 修改后的 Time 类定义，用于实现链式成员函数调用。

```cpp
// Fig. 10.18: Time.cpp
// Time class member-function definitions.
#include <iostream>
#include <iomanip>
#include "Time.h" // Time class definition
using namespace std;
```

**图 10.18** | 修改后的 Time 类成员函数定义，用于实现链式成员函数调用。（共 3 部分，第 1 部分。）

