
图10.3实例化两个Time对象——非const对象wakeUp（第7行）和const对象noon（第8行）。程序尝试在const对象noon上调用非const成员函数setHour（第13行）和printStandard（第20行）。每种情况下，编译器都会生成错误消息。程序还演示了对象上的另外三种成员函数调用组合——非const对象上的非const成员函数（第11行）、非const对象上的const成员函数（第15行）以及const对象上的const成员函数（第17–18行）。在const对象上调用非const成员函数生成的错误消息显示在输出窗口中。

```cpp
// Fig. 10.3: fig10_03.cpp
// Attempting to access a const object with non-const member functions.
#include "Time.h" // include Time class definition

int main()
{
   Time wakeUp( 6, 45, 0 ); // non-constant object
   const Time noon( 12, 0, 0 ); // constant object

                         // OBJECT        MEMBER FUNCTION
   wakeUp.setHour( 18 ); // non-const     non-const
   noon.setHour( 12 );   // const         non-const

   wakeUp.getHour();     // non-const     const
   noon.getHour();       // const         const

   noon.getMinute();     // const         const
   noon.printUniversal(); // const        const

   noon.printStandard(); // const         non-const
} // end main
```

*Microsoft Visual C++ 编译器错误消息：*

```text
C:\cpphtp7_examples\ch10\Fig10_01_03\fig10_03.cpp(13) : error C2662:
   'Time::setHour' : cannot convert 'this' pointer from 'const Time' to
   'Time &'
      Conversion loses qualifiers
C:\cpphtp7_examples\ch10\Fig10_01_03\fig10_03.cpp(20) : error C2662:
   'Time::printStandard' : cannot convert 'this' pointer from 'const Time' to
   'Time &'
      Conversion loses qualifiers
```

*GNU C++ 编译器错误消息：*

```text
fig10_03.cpp:13: error: passing 'const Time' as 'this' argument of
   'void Time::setHour(int)' discards qualifiers
fig10_03.cpp:20: error: passing 'const Time' as 'this' argument of
   'void Time::printStandard()' discards qualifiers
```

**图10.3** | const对象与const成员函数。

构造函数必须是非const成员函数（图10.2，第11–14行），但它仍然可以用于初始化const对象（图10.3，第8行）。Time构造函数的定义（图10.2，第11–14行）表明它调用了另一个非const成员函数——setTime（第17–22行）——来执行Time对象的初始化。在const对象初始化过程中，通过构造函数调用非const成员函数是允许的。const对象的“常量性”从构造函数完成对象初始化之时起，一直持续到该对象的析构函数被调用为止。

此外，图10.3中的第20行会产生编译错误，即使Time类的成员函数printStandard并不修改调用它的对象。成员函数不修改对象这一事实并不足以表明该函数是const的——该函数必须显式声明为const。

## 用成员初始化器初始化const数据成员

图10.4–10.6中的程序介绍了成员初始化器语法。所有数据成员都可以使用成员初始化器语法进行初始化，但const数据成员和引用类型的数据成员必须使用成员初始化器进行初始化。在本章后面，我们将看到成员对象也必须以这种方式初始化。

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

**图10.4** | Increment类定义，包含非const数据成员count和const数据成员increment。

```cpp
// Fig. 10.5: Increment.cpp
// Member-function definitions for class Increment demonstrate using a
// member initializer to initialize a constant of a built-in data type.
```

**图10.5** | 用于初始化内置数据类型常量的成员初始化器。（第1部分，共2部分）

```cpp
#include <iostream>
#include "Increment.h" // include definition of class Increment
using namespace std;

// constructor
Increment::Increment( int c, int i )
    : count( c ),       // initializer for non-const member
      increment( i )    // required for initializer for const member
{
    // empty body
} // end constructor Increment

// print count and increment values
void Increment::print() const
{
    cout << "count = " << count << ", increment = " << increment << endl;
} // end function print
```

**图10.5** | 用于初始化内置数据类型常量的成员初始化器。（第2部分，共2部分）

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

    for ( int j = 1; j <= 3; j++ )
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

构造函数定义（图10.5，第9–14行）使用成员初始化列表来初始化类Increment的数据成员——count和increment——非const整数count和const整数increment（在图10.4的第19–20行中声明）。成员初始化器出现在构造函数的参数列表和构造函数体的左花括号之间。成员初始化列表（图10.5，第10–11行）用冒号（:）与参数列表分隔。每个成员初始化器由数据成员名称后跟包含该成员初始值的括号组成。在此示例中，count使用构造函数参数c的值初始化。多个成员初始化器用逗号分隔。此外，成员初始化列表在构造函数体执行之前执行。

> **软件工程观察 10.3**
> 
> *const对象不能通过赋值来修改，因此必须对其进行初始化。当类的数据成员被声明为const时，必须使用成员初始化器向构造函数提供该数据成员对于类对象的初始值。引用也是如此。*

## 错误地尝试用赋值初始化const数据成员

图10.7–10.9中的程序说明了由尝试在Increment构造函数体中使用赋值语句（图10.8，第12行）而不是使用成员初始化器来初始化const数据成员increment所引起的编译错误。图10.8中的第11行不会产生编译错误，因为count没有被声明为const。

> **常见编程错误 10.5**
> 
> *不为const数据成员提供成员初始化器是编译错误。*

> **软件工程观察 10.4**
> 
> *常量数据成员（const对象和const变量）以及声明为引用的数据成员必须使用成员初始化器语法进行初始化；不允许在构造函数体中对这些类型的数据进行赋值。*

```cpp
// Fig. 10.7: Increment.h
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
   int increment;
```

**图10.7** | Increment类定义，包含非const数据成员count和非const数据成员increment。（第1部分，共2部分）

