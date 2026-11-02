

```cpp
// Fig. 17.11: Time.cpp
// Time class member-function definitions.
#include <stdexcept>
#include "Time.h" // include definition of class Time
using namespace std;

// constructor function to initialize private data; calls member function
// setTime to set variables; default values are 0 (see class definition)
Time::Time( int hr, int min, int sec )
{
    setTime( hr, min, sec );
} // end Time constructor

// set values of hour, minute and second
void Time::setTime( int h, int m, int s )
{
    // validate hour, minute and second
    if ( ( h >= 0 && h < 24 ) && ( m >= 0 && m < 60 ) &&
         ( s >= 0 && s < 60 ) )
    {
        hour = h;
        minute = m;
        second = s;
    } // end if
    else
        throw invalid_argument(
            "hour, minute and/or second was out of range" );
} // end function setTime

// return hour value
unsigned int Time::getHour()
{
    return hour;
} // end function getHour

// poor practice: returning a reference to a private data member.
unsigned int &Time::badSetHour( int hh )
{
    if ( hh >= 0 && hh < 24 )
        hour = hh;
    else
        throw invalid_argument( "hour must be 0-23" );

    return hour; // dangerous reference return
} // end function badSetHour
```

图 17.11 | Time 类成员函数定义。

图 17.12 声明了 Time 对象 t（第 10 行）和引用 hourRef（第 13 行），该引用通过调用 t.badSetHour(20) 返回的引用进行初始化。第 15 行显示别名 hourRef 的值。这说明了 hourRef 如何破坏类的封装性——main 中的语句不应该能够访问类的私有数据。接下来，第 16 行使用别名将 hour 的值设置为 30（一个无效值），第 17 行显示函数 getHour 返回的值，以证明给 hourRef 赋值实际上修改了 Time 对象 t 中的私有数据。最后，第 21 行将 badSetHour 函数调用本身用作*左值*，并向函数返回的引用赋值 74（另一个无效值）。第 26 行再次显示函数 getHour 返回的值，以证明给第 21 行函数调用的结果赋值会修改 Time 对象 t 中的私有数据。

![](img/d0d3b7423c2d9e5650be79209ea1885d_681_0.png)

### 软件工程观察 17.7

> 返回指向私有数据成员的引用或指针会破坏类的封装性，并使客户端代码依赖于类数据的表示方式。在某些情况下这样做是合适的——我们将在第 18.10 节构建客户类时展示一个示例。

```cpp
// Fig. 17.12: fig17_12.cpp
// Demonstrating a public member function that
// returns a reference to a private data member.
#include <iostream>
#include "Time.h" // include definition of class Time
using namespace std;

int main()
{
   Time t; // create Time object

   // initialize hourRef with the reference returned by badSetHour
   int &hourRef = t.badSetHour( 20 ); // 20 is a valid hour

   cout << "Valid hour before modification: " << hourRef;
   hourRef = 30; // use hourRef to set value in Time object t
   cout << "\nInvalid hour after modification: " << t.getHour();

   // Dangerous: Function call that returns
   // a reference can be used as an lvalue!
   t.badSetHour( 12 ) = 74; // assign another invalid value to hour

   cout << "\n\n**********************************************\n"
        << "POOR PROGRAMMING PRACTICE!!!!!!!!!!\n"
        << "t.badSetHour( 12 ) as an lvalue, invalid hour: "
        << t.getHour()
        << "\n**********************************************" << endl;
} // end main
```

```
Valid hour before modification: 20
Invalid hour after modification: 30

**************************************************
POOR PROGRAMMING PRACTICE!!!!!!!!!!
t.badSetHour( 12 ) as an lvalue, invalid hour: 74
**************************************************
```

**图 17.12** — 返回私有数据成员引用的公有成员函数。

## 17.9 默认按成员赋值

赋值运算符（=）可用于给同类的对象赋值。默认情况下，这种赋值是通过按成员赋值（也称为复制赋值）执行的——赋值运算符右侧对象的每个数据成员会被单独赋值给赋值运算符左侧对象中对应的数据成员。图 17.13–17.14 定义了一个 Date 类。图 17.15 的第 18 行使用默认按成员赋值将 Date 对象 date1 的数据成员赋给 Date 对象 date2 中对应的数据成员。在这种情况下，date1 的 month 成员被赋给 date2 的 month 成员，date1 的 day 成员被赋给 date2 的 day 成员，date1 的 year 成员被赋给 date2 的 year 成员。[注意：当类的数据成员包含指向动态分配内存的指针时，按成员赋值可能会导致严重问题；我们将在第 18 章讨论这些问题并说明如何处理。]

```cpp
// Fig. 17.13: Date.h
// Date class declaration. Member functions are defined in Date.cpp.

// prevent multiple inclusions of header
#ifndef DATE_H
#define DATE_H

// class Date definition
class Date
{
public:
    explicit Date( int = 1, int = 1, int = 2000 ); // default constructor
    void print();
private:
    unsigned int month;
    unsigned int day;
    unsigned int year;
}; // end class Date

#endif
```

图 17.13 | Date 类声明。

```cpp
// Fig. 17.14: Date.cpp
// Date class member-function definitions.
#include <iostream>
#include "Date.h" // include definition of class Date from Date.h
using namespace std;

// Date constructor (should do range checking)
Date::Date( int m, int d, int y )
    : month( m ), day( d ), year( y )
{
} // end constructor Date
```

图 17.14 | Date 类成员函数定义。（第 1 部分，共 2 部分。）

~~~cpp
12
13 // print Date in the format mm/dd/yyyy
14 void Date::print()
15 {
16     cout << month << '/' << day << '/' << year;
17 } // end function print
~~~

**图 17.14** | Date 类成员函数定义。（第 2 部分，共 2 部分。）

~~~cpp
1 // Fig. 17.15: fig17_15.cpp
2 // Demonstrating that class objects can be assigned
3 // to each other using default memberwise assignment.
4 #include <iostream>
5 #include "Date.h" // include definition of class Date from Date.h
6 using namespace std;
7
8 int main()
9 {
10    Date date1( 7, 4, 2004 );
11    Date date2; // date2 defaults to 1/1/2000
12
13    cout << "date1 = ";
14    date1.print();
15    cout << "\ndate2 = ";
16    date2.print();
17
18    date2 = date1; // default memberwise assignment
19
20    cout << "\n\nAfter default memberwise assignment, date2 = ";
21    date2.print();
22    cout << endl;
23 } // end main
~~~

~~~
date1 = 7/4/2004
date2 = 1/1/2000

After default memberwise assignment, date2 = 7/4/2004
~~~

**图 17.15** | 类对象可以使用默认按成员赋值相互赋值。

对象可以作为函数参数传递，也可以从函数返回。默认情况下，这种传递和返回是按照传值方式执行的——传递或返回的是对象的副本。在这种情况下，C++ 会创建一个新对象，并使用复制构造函数将原始对象的值复制到新对象中。对于每个类，编译器都会提供一个默认复制构造函数，将原始对象的每个成员复制到新对象的对应成员中。与按成员赋值类似，当类的数据成员包含指向动态分配内存的指针时，复制构造函数可能会导致严重问题。第 18 章将讨论如何定义自定义的复制构造函数，以正确复制包含指向动态分配内存指针的对象。

图 17.16 中的第 20 行会产生编译错误，即使类 `Time` 的成员函数 `printStandard` *没有*修改其调用对象。成员函数不修改对象这一事实*并不*足以避免错误——该函数必须显式声明为 `const`。

## 17.11 组合：对象作为类的成员

AlarmClock（闹钟）对象需要知道什么时候应该响铃，那么为什么不把 Time 对象作为 AlarmClock 类的成员呢？这种能力称为组合（composition），有时也称为*has-a 关系*——一个类可以将其他类的对象作为成员。

> **软件工程观察 17.9**
> 
> *软件复用的一种常见形式是组合，即一个类拥有其他类型对象作为成员。*

![](img/d0d3b7423c2d9e5650be79209ea1885d_686_0.png)

之前，我们看到了如何向在 `main` 中创建的对象的构造函数传递参数。现在，我们展示类的构造函数如何通过成员初始化器向成员对象的构造函数传递参数。

> **软件工程观察 17.10**
> 
> *数据成员的构造顺序是按它们在类定义中声明的顺序（而不是按它们在构造函数的成员初始化列表中列出的顺序），并且先于其所在类的对象（有时称为宿主对象）的构造。*

![](img/d0d3b7423c2d9e5650be79209ea1885d_686_1.png)

下一个程序使用 Date 类（图 17.17–17.18）和 Employee 类（图 17.19–17.20）来演示组合。Employee 类的定义（图 17.19）包含私有数据成员 firstName、lastName、birthDate 和 hireDate。birthDate 和 hireDate 是类 Date 的 const 对象，类 Date 包含私有数据成员 month、day 和 year。Employee 构造函数的头部（图 17.20 第 10–11 行）指定构造函数有四个参数（first、last、dateOfBirth 和 dateOfHire）。前两个参数通过成员初始化器传递给 string 类构造函数，用于初始化 firstName 和 lastName 数据成员。后两个参数通过成员初始化器传递给 Date 类构造函数，用于初始化 birthDate 和 hireDate 数据成员。

```cpp
// Fig. 17.17: Date.h
// Date class definition; Member functions defined in Date.cpp
#ifndef DATE_H
#define DATE_H

class Date
{
public:
   static const unsigned int monthsPerYear = 12; // months in a year
   explicit Date( int = 1, int = 1, int = 1900 ); // default constructor
   void print() const; // print date in month/day/year format
   ~Date(); // provided to confirm destructor order
};
```

**图 17.17** | Date 类定义。（第 1 部分，共 2 部分。）

