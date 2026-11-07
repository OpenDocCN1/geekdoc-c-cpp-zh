

## 9.5 Time 类案例研究：带默认参数的构造函数

图 9.4–9.6 中的程序增强了 Time 类，以演示参数如何隐式传递给构造函数。图 9.2 中定义的构造函数将 hour、minute 和 second 初始化为 0（即通用时间的午夜）。与其他函数一样，构造函数可以指定*默认参数*。图 9.4 的第 13 行声明 Time 构造函数包含默认参数，为传递给构造函数的每个参数指定默认值 0。该构造函数被声明为 `explicit`，因为它可以用一个参数调用。我们将在 10.13 节详细讨论显式构造函数。

```cpp
// Fig. 9.4: Time.h
// Time class containing a constructor with default arguments.
// Member functions defined in Time.cpp.

// prevent multiple inclusions of header
#ifndef TIME_H
#define TIME_H

// Time class definition
class Time
{
public:
   explicit Time( int = 0, int = 0, int = 0 ); // default constructor

   // set functions
   void setTime( int, int, int ); // set hour, minute, second
   void setHour( int ); // set hour (after validation)
   void setMinute( int ); // set minute (after validation)
   void setSecond( int ); // set second (after validation)

   // get functions
   unsigned int getHour() const; // return hour
   unsigned int getMinute() const; // return minute
   unsigned int getSecond() const; // return second

   void printUniversal() const; // output time in universal-time format
   void printStandard() const; // output time in standard-time format
private:
   unsigned int hour; // 0 - 23 (24-hour clock format)
   unsigned int minute; // 0 - 59
   unsigned int second; // 0 - 59
}; // end class Time

#endif
```

**图 9.4** | 包含带默认参数的构造函数的 Time 类。

在图 9.5 中，第 10–13 行定义了 Time 构造函数的新版本，它接收参数 hour、minute 和 second 的值，这些值将分别用于初始化私有数据成员 hour、minute 和 second。构造函数的默认参数确保即使在构造函数调用中未提供任何值，构造函数仍会初始化数据成员。将所有参数都设置为默认值的构造函数也是默认构造函数——也就是说，它可以在不提供任何参数的情况下被调用。每个类最多只能有一个默认构造函数。本例中的 Time 类版本为每个数据成员提供了 set 和 get 函数。Time 构造函数现在调用 setTime，而 setTime 又调用 setHour、setMinute 和 setSecond 函数来验证数据成员并为其赋值。

> **软件工程观察 9.5**
>
> *对函数默认参数值的任何更改都需要重新编译客户端代码（以确保程序仍能正常运行）。*

```cpp
// Fig. 9.5: Time.cpp
// Member-function definitions for class Time.
#include <iostream>
#include <iomanip>
#include <stdexcept>
#include "Time.h" // include definition of class Time from Time.h
using namespace std;

// Time constructor initializes each data member
Time::Time( int hour, int minute, int second )
{
   setTime( hour, minute, second ); // validate and set time
} // end Time constructor

// set new Time value using universal time
void Time::setTime( int h, int m, int s )
{
   setHour( h ); // set private field hour
   setMinute( m ); // set private field minute
   setSecond( s ); // set private field second
} // end function setTime

// set hour value
void Time::setHour( int h )
{
   if ( h >= 0 && h < 24 )
      hour = h;
   else
      throw invalid_argument( "hour must be 0-23" );
} // end function setHour

// set minute value
void Time::setMinute( int m )
{
   if ( m >= 0 && m < 60 )
      minute = m;
   else
      throw invalid_argument( "minute must be 0-59" );
} // end function setMinute
```

**图 9.5** | Time 类的成员函数定义。（第 1 部分，共 2 部分。）

```text
Constructed with:

t1: all arguments defaulted
  00:00:00
  12:00:00 AM

t2: hour specified; minute and second defaulted
  02:00:00
  2:00:00 AM

t3: hour and minute specified; second defaulted
  21:34:00
  9:34:00 PM

t4: hour, minute and second specified
  12:25:42
  12:25:42 PM

Exception while initializing t5: hour must be 0-23
```

**图 9.6** | 带默认参数的构造函数。（第 2 部分，共 2 部分。）

### 关于 Time 类的 Set 和 Get 函数及构造函数的说明

Time 的 set 和 get 函数在类的整个主体中都会被调用。特别是，setTime 函数（图 9.5 的第 16–21 行）调用 setHour、setMinute 和 setSecond 函数，而 printUniversal 和 printStandard 函数在第 71–72 行和第 78–80 行调用 getHour、getMinute 和 getSecond 函数。在每种情况下，这些函数本可以直接访问类的私有数据。然而，请考虑将时间的表示从三个 int 值（在 int 占四个字节的系统上需要 12 字节内存）改为一个表示自午夜以来经过的总秒数的 int 值（只需四字节内存）。如果我们进行这样的更改，只有直接访问私有数据的函数体需要修改——特别是针对 hour、minute 和 second 的各个 set 和 get 函数。而 setTime、printUniversal 或 printStandard 的函数体则无需修改，因为它们不直接访问数据。以这种方式设计类，在更改类的实现时可以减少编程错误发生的可能性。

类似地，Time 构造函数也可以写成包含 setTime 函数中相应语句的副本。这样做可能会稍微高效一些，因为省去了对 setTime 的额外调用。但是，在多个函数或构造函数中重复语句会使更改类的内部数据表示变得更加困难。让 Time 构造函数调用 setTime，并让 setTime 调用 setHour、setMinute 和 setSecond，可以将验证 hour、minute 或 second 的代码更改限制在相应的 set 函数中。这降低了更改类的实现时出错的可能性。

![](img/b42ba5cd262b1358d16610173f975e4d_426_0.png)

> **软件工程观察 9.6**
>
> 如果类的某个成员函数已经提供了类的构造函数（或其他成员函数）所需的全部或部分功能，请从构造函数（或其他成员函数）中调用该成员函数。这简化了代码的维护，并且在代码实现被修改时降低了出错的可能性。一般规则：避免重复代码。

```cpp
Time::Time( int hour )
    : Time( hour, 0, 0 ) // delegate to Time( int, int, int )
{
} // end constructor with one argument
Time::Time( int hour, int minute )
    : Time( hour, minute, 0 ) // delegate to Time( int, int, int )
{
} // end constructor with two arguments
```

## 9.6 析构函数

**析构函数**是另一种特殊类型的成员函数。类的析构函数的名称是**波浪号字符（~）**后跟类名。这种命名约定具有直观的吸引力，因为正如我们将在后面的章节中看到的，波浪号运算符是按位取反运算符，而且在某种意义上，析构函数就是构造函数的取反。析构函数不能指定参数或返回类型。

当对象被销毁时，类的析构函数会被*隐式*调用。例如，当程序执行离开实例化该对象的作用域时，对象即被销毁。*析构函数本身实际上并不释放对象的内存*——它会在对象的内存被回收之前执行**终止清理**工作，以便该内存可以被重新用于容纳新的对象。

尽管目前呈现的类都还没有定义析构函数，但*每个类都有一个析构函数*。如果你没有*显式*定义析构函数，编译器会定义一个“空”析构函数。[*注：我们将看到，这种隐式创建的析构函数实际上会对通过组合*（9.11 节）*和继承*（第 11 章）*创建的类类型对象执行重要的操作。*] 在第 10 章中，我们将为对象包含动态分配内存（例如数组和字符串）或使用其他系统资源（例如磁盘上的文件，我们将在第 14 章中学习）的类构建合适的析构函数。我们将在第 10 章讨论如何动态分配和释放内存。

## 9.7 构造函数和析构函数的调用时机

构造函数和析构函数由编译器*隐式*调用。这些函数调用的发生顺序取决于执行进入和离开实例化对象的范围的顺序。通常，析构函数的调用顺序与相应的构造函数调用顺序*相反*，但正如我们将在图 9.7–9.9 中看到的，对象的存储类别可以改变析构函数的调用顺序。

### 全局作用域中对象的构造函数和析构函数

在全局作用域（也称为全局命名空间作用域）中定义的对象，其构造函数会在该程序中任何其他函数（包括 main）开始执行*之前*被调用（尽管不同文件之间全局对象构造函数的执行顺序*无法保证*）。相应的析构函数在 main 终止时被调用。函数 **exit** 强制程序立即终止，并且*不*执行局部对象的析构函数。当发生致命的不可恢复错误时，通常使用 exit 函数来终止程序。函数 **abort** 的功能与 exit 函数类似，但强制程序*立即*终止，不允许调用任何对象的析构函数。函数

