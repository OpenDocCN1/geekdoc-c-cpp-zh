

```cpp
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

// set second value
void Time::setSecond( int s )
{
   if ( s >= 0 && s < 60 )
      second = s;
   else
      throw invalid_argument( "second must be 0-59" );
} // end function setSecond

// return hour value
int Time::getHour() const // get functions should be const
{
   return hour;
} // end function getHour

// return minute value
int Time::getMinute() const
{
   return minute;
} // end function getMinute

// return second value
int Time::getSecond() const
{
   return second;
} // end function getSecond

// print Time in universal-time format (HH:MM:SS)
void Time::printUniversal() const
{
   cout << setfill( '0' ) << setw( 2 ) << hour << ":"
        << setw( 2 ) << minute << ":" << setw( 2 ) << second;
} // end function printUniversal

// print Time in standard-time format (HH:MM:SS AM or PM)
void Time::printStandard() // note lack of const declaration
{
   cout << ( ( hour == 0 || hour == 12 ) ? 12 : hour % 12 )
        << ":" << setfill( '0' ) << setw( 2 ) << minute
        << ":" << setw( 2 ) << second << ( hour < 12 ? "AM" : "PM" );
} // end function printStandard
```

**图10.2** | Time类成员函数定义。

图10.3实例化了两个Time对象——非const对象`wakeUp`（第7行）和const对象`noon`（第8行）。程序尝试在const对象`noon`上调用非const成员函数`setHour`（第13行）和`printStandard`（第20行）。在这两种情况下，编译器都会生成错误消息。程序还演示了对象上另外三种成员函数调用组合——在非const对象上调用非const成员函数（第11行）、在非const对象上调用const成员函数（第15行）以及在const对象上调用const成员函数（第17–18行）。在const对象上调用非const成员函数时生成的错误消息显示在输出窗口中。

```cpp
// Fig. 10.3: fig10_03.cpp
// Attempting to access a const object with non-const member functions.
#include "Time.h" // include Time class definition

int main()
{
   Time wakeUp( 6, 45, 0 ); // non-const object
   const Time noon( 12, 0, 0 ); // constant object

                         // OBJECT        MEMBER FUNCTION
   wakeUp.setHour( 18 ); // non-const    non-const

   noon.setHour( 12 );   // const        non-const

   wakeUp.getHour();     // non-const    const

   noon.getMinute();     // const        const
   noon.printUniversal();// const        const

   noon.printStandard();// const        non-const
} // end of main
```

*Microsoft Visual C++ 编译器错误消息：*

```text
C:\cpphtp8_examples\ch10\Fig10_01_03\fig10_03.cpp(13) : error C2662:
   'Time::setHour' : cannot convert 'this' pointer from 'const Time' to 'Time &'
   Conversion loses qualifiers
C:\cpphtp8_examples\ch10\Fig10_01_03\fig10_03.cpp(20) : error C2662:
   'Time::printStandard' : cannot convert 'this' pointer from 'const Time' to
   'Time &'
   Conversion loses qualifiers
```

**图10.3** | const对象和const成员函数。

构造函数必须是*非const成员函数*（图10.2，第11–14行），但它仍然可以用来初始化const对象（图10.3，第8行）。Time构造函数的定义（图10.2，第11–14行）表明它调用了另一个非const成员函数——`setTime`（第17–22行）——来执行Time对象的初始化。在const对象初始化过程中，从构造函数调用中调用非const成员函数是允许的。对象的“const性”从构造函数完成对象初始化之时起强制执行，直到该对象的析构函数被调用为止。

图10.3中的第20行产生编译错误，即使Time类的成员函数`printStandard`没有修改调用它的对象。成员函数不修改对象这一事实不足以表明该函数是常量函数——函数必须显式声明为const。

## 使用成员初始化器初始化const数据成员

图10.4–10.6中的程序介绍了成员初始化器语法的使用。所有数据成员都可以使用成员初始化器语法进行初始化，但const数据成员和引用类型的数据成员必须使用成员初始化器进行初始化。在本章后面，我们将看到成员对象也必须以这种方式初始化。

```cpp
// Fig. 10.4: Increment.h
// Definition of class Increment.
#ifndef INCREMENT_H
#define INCREMENT_H

class Increment
{
public:
   Increment( int c = 0, int i = 1 ); // default constructor

   // function addIncrement definition
   void addIncrement()
   {
      count += increment;
   } // end function addIncrement

   void print() const; // prints count and increment
private:
   int count;
   const int increment; // const data member
}; // end class Increment

#endif
```

**图10.4** | 包含非const数据成员count和const数据成员increment的*Increment*类定义。

```cpp
// Fig. 10.5: Increment.cpp
// Member-function definitions for class Increment demonstrate using a
// member initializer to initialize a constant of a built-in data type.

#include <iostream>
#include "Increment.h" // include definition of class Increment
using namespace std;

// constructor
Increment::Increment( int c, int i )
   : count( c ),        // initializer for non-const member
     increment( i )     // required initializer for const member
{
   // empty body
} // end constructor Increment

// print count and increment values
void Increment::print() const
{
   cout << "count = " << count << ", increment = " << increment << endl;
} // end function print
```

**图10.5** | 使用成员初始化器初始化内置数据类型的常量。

```cpp
// Fig. 10.6: fig10_06.cpp
// Program to test class Increment.
#include <iostream>
#include "Increment.h" // include definition of class Increment
using namespace std;

int main()
{
   Increment value( 10, 5 );

   cout << "Before incrementing: ";
   value.print();

   for ( int j = 1; j <= 3; ++j )
   {
      value.addIncrement();
      cout << "After increment " << j << ": ";
      value.print();
   } // end for
} // end main
```

```text
Before incrementing: count = 10, increment = 5
After increment 1: count = 15, increment = 5
After increment 2: count = 20, increment = 5
After increment 3: count = 25, increment = 5
```

**图10.6** | 调用Increment对象的print和addIncrement成员函数。

构造函数定义（图10.5，第9–14行）使用成员初始化器列表来初始化类Increment的数据成员——非const整数count和const整数increment（在图10.4的第19–20行声明）。成员初始化器出现在构造函数的参数列表和构造函数体开始的左花括号之间。成员初始化器列表（图10.5，第10–11行）用冒号（:）与参数列表分隔。每个成员初始化器由数据成员名称后跟包含成员初始值的括号组成。在这个例子中，count用构造函数参数c的值初始化，increment用构造函数参数i的值初始化。多个成员初始化器用逗号分隔。此外，成员初始化器列表在构造函数体执行*之前*执行。

> **软件工程观察 10.3**
>
> *const对象不能通过赋值修改，因此必须初始化。当一个类的数据成员被声明为const时，必须使用成员初始化器向构造函数提供该数据成员对该类对象的初始值。引用类型也是如此。*

### *为什么函数print要声明为const？*

函数print（图10.5，第17–20行）被声明为const。将此函数标记为const似乎很奇怪，因为程序可能永远不会有一个const Increment对象。但是，程序可能有对Increment对象的const引用或指向Increment对象的const指针。通常，当Increment类对象作为参数传递给函数或从函数返回时，会出现这种情况。在这些情况下，只能通过引用或指针调用Increment类的const成员函数。因此，将函数print声明为const是合理的——这样做可以防止在将Increment对象视为const对象的情况下出错。

> **错误预防提示 10.1**
>
> *将类中所有不修改其操作对象的成员函数声明为const。有时这可能看起来不合适，因为你可能无意创建该类的const对象，也不会通过const引用或指向const的指针访问该类的对象。然而，将此类成员函数声明为const确实有一个好处：如果该成员函数被无意中编写为修改对象，编译器将发出错误消息。*

### *错误地尝试使用赋值来初始化const数据成员*

图10.7显示了尝试在Increment构造函数体中使用赋值语句而不是成员初始化器来初始化const数据成员increment时所导致的编译错误。

*Microsoft Visual C++ 编译器错误消息：*

```text
C:\cpphtp8_examples\ch10\consterror\Increment.cpp(10) : error C2758:
    'Increment::increment' : must be initialized in constructor base/member
    initializer list
        C:\cpphtp8_examples\ch10\consterror\Increment.h(20) : see
        declaration of 'Increment::increment'
C:\cpphtp8_examples\ch10\consterror\Increment.cpp(12) : error C2166:
    l-value specifies const object
```

**图10.7** | 在构造函数体而不是成员初始化器列表中尝试初始化const数据成员时生成的编译错误。

