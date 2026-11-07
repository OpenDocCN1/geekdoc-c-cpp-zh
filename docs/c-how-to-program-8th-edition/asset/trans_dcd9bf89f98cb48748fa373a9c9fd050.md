
将 counter 作为参数传递给 `setX`，而不是使用句柄（例如对象名）来调用该函数，如下所示：

```
counter.setX( 8 );
```

如果删除第 9 行的 friend 声明，你将收到错误消息，指出函数 `setX` 无法修改类 Count 的私有数据成员 `x`。

正如我们提到的，图 10.13 是使用友元结构的一个机械示例。通常更适合将函数 `setX` 定义为类 Count 的成员函数。通常也适合将图 10.13 的程序分成三个文件：

- 1. 一个头文件（例如 `Count.h`），包含 Count 类定义，其中又包含友元函数 `setX` 的原型
- 2. 一个实现文件（例如 `Count.cpp`），包含 Count 类的成员函数定义以及友元函数 `setX` 的定义
- 3. 一个测试程序（例如 `fig10_13.cpp`），其中包含 `main`。

## 重载友元函数

可以将重载函数指定为类的友元。每个打算成为友元的函数都必须在类定义中显式声明为该类的友元。

## 10.5 使用 this 指针

我们已经看到，对象的成员函数可以操作对象的数据。成员函数如何知道要操作哪个对象的数据成员？每个对象都可以通过一个名为 `this` 的指针（C++ 关键字）访问自己的地址。`this` 指针不是对象本身的一部分——也就是说，`this` 指针占用的内存不会反映在对对象执行 `sizeof` 运算的结果中。相反，`this` 指针（由编译器）作为隐式参数传递给对象的每个非静态成员函数。10.6 节介绍静态类成员，并解释为什么 `this` 指针不会隐式传递给静态成员函数。

对象会隐式地（正如我们到目前为止所做的那样）或显式地使用 `this` 指针来引用其数据成员和成员函数。`this` 指针的类型取决于对象的类型，以及使用 `this` 的成员函数是否声明为 `const`。例如，在类 Employee 的非 const 成员函数中，`this` 指针的类型为 `Employee * const`（指向非 const Employee 对象的常量指针）。在类 Employee 的 const 成员函数中，`this` 指针的数据类型为 `const Employee * const`（指向 const Employee 对象的常量指针）。

下一个示例展示 `this` 指针的隐式和显式使用；本章后面以及第 11 章中，我们将展示一些重要而微妙的 `this` 使用示例。

### 隐式和显式使用 `this` 指针访问对象的数据成员

图 10.14 演示了隐式和显式使用 `this` 指针，使类 Test 的成员函数能够打印 Test 对象的私有数据 `x`。

为便于说明，成员函数 `print`（第 24—36 行）首先隐式使用 `this` 指针打印 `x`（第 27 行）——只指定数据成员的名称。然后，`print` 使用两种不同的记法通过 `this` 指针访问 `x`——通过 `this` 指针使用箭头运算符（`->`）（第 31 行），以及通过对解引用后的 `this` 指针使用点运算符（`.`）（第 35 行）。

```cpp
// Fig. 10.14: fig10_14.cpp
// Using the this pointer to refer to object members.
#include <iostream>
using namespace std;

class Test
{
public:
   Test( int = 0 ); // default constructor
   void print() const;
private:
   int x;
}; // end class Test

// constructor
Test::Test( int value )
   : x( value ) // initialize x to value
{
   // empty body
} // end constructor Test

// print x using implicit and explicit this pointers;
// the parentheses around *this are required
void Test::print() const
{
   // implicitly use the this pointer to access the member x
   cout << "        x = " << x;

   // explicitly use the this pointer and the arrow operator
   // to access the member x
   cout << "\n this->x = " << this->x;

   // explicitly use the dereferenced this pointer and
   // the dot operator to access the member x
   cout << "\n(*this).x = " << (*this).x << endl;
} // end function print

int main()
{
   Test testObject( 12 ); // instantiate and initialize testObject

   testObject.print();
} // end main
```

```
x = 12
this->x = 12
(*this).x = 12
```

**图 10.14** | 使用 `this` 指针引用对象成员。

注意第 35 行中 `*this` 与点成员选择运算符（`.`）一起使用时外面的括号。这些括号是必需的，因为点运算符的优先级高于 `*` 运算符。如果没有括号，表达式 `*this.x` 将被按 `*(this.x)` 加括号的方式求值，这会导致编译错误，因为点运算符不能用于指针。

> **常见编程错误 10.7**
>
> *尝试对指向对象的指针使用成员选择运算符（`.`）会导致编译错误——点成员选择运算符只能用于左值，例如对象名、对象的引用或解引用后的对象指针。*

![](img/bfd978e7e9b192bab46ec2a89e481263_466_0.png)

`this` 指针的一个有趣用途是防止对象被赋值给自身。正如我们将在第 11 章看到的，当对象包含指向动态分配存储的指针时，*自赋值*可能导致严重错误。

### 使用 `this` 指针实现级联函数调用

`this` 指针的另一个用途是实现级联成员函数调用——即，在同一条语句中调用多个函数（如图 10.17 第 12 行）。图 10.15—10.17 的程序修改了类 Time 的设置函数 `setTime`、`setHour`、`setMinute` 和 `setSecond`，使每个函数都返回一个 Time 对象的引用，以实现级联成员函数调用。注意，在图 10.16 中，这些成员函数各自函数体中的最后一条语句都返回 `*this`（第 22、33、44 和 55 行），返回类型为 `Time &`。

```cpp
// Fig. 10.15: Time.h
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
   int getHour() const;             // return hour
   int getMinute() const;           // return minute
   int getSecond() const;           // return second

   // print functions (normally declared const)
   void printUniversal() const;     // print universal time
   void printStandard() const;      // print standard time
private:
   int hour;                        // 0 - 23 (24-hour clock format)
   int minute;                      // 0 - 59
   int second;                      // 0 - 59
}; // end class Time

#endif
```

**图 10.15** | 为启用级联成员函数调用而修改的 Time 类。

```cpp
// Fig. 10.16: Time.cpp
// Time class member-function definitions.
#include <iostream>
#include <iomanip>
#include "Time.h" // Time class definition
using namespace std;

// constructor function to initialize private data;
// calls member function setTime to set variables;
// default values are 0 (see class definition)
Time::Time( int hr, int min, int sec )
{
   setTime( hr, min, sec );
} // end Time constructor

// set values of hour, minute, and second
Time &Time::setTime( int h, int m, int s ) // note Time & return
{
   setHour( h );
   setMinute( m );
   setSecond( s );
   return *this; // enables cascading
} // end of function setTime

// set hour value
Time &Time::setHour( int h ) // note Time & return
{
   if ( h >= 0 && h < 24 )
      hour = h;
   else
      throw invalid_argument( "hour must be 0-23" );

   return *this; // enables cascading
} // end of function setHour

// set minute value
Time &Time::setMinute( int m ) // note Time & return
{
   if ( m >= 0 && m < 60 )
      minute = m;
   else
      throw invalid_argument( "minute must be 0-59" );
```

**图 10.16** | 为启用级联成员函数调用而修改的 Time 类成员函数定义。（第 1 部分，共 2 部分。）
