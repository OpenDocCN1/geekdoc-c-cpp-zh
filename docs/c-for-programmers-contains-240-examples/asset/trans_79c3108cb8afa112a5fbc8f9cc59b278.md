

## 错误预防提示 10.1

将类的所有不修改其操作对象的成员函数声明为 const。有时这可能显得并不合适，因为你并不打算创建该类的 const 对象，也不想通过 const 引用或指向 const 的指针来访问该类的对象。不过，将这类成员函数声明为 const 确实有一个好处：如果成员函数被无意中编写成会修改该对象，编译器就会发出错误信息。

```
// Fig. 10.8: Increment.cpp
// Erroneous attempt to initialize a constant of a built-in data
// type by assignment.
#include <iostream>
using std::cout;
using std::endl;

#include "Increment.h" // include definition of class Increment

// constructor; constant member 'increment' is not initialized
Increment::Increment( int c, int i )
{
   count = c; // allowed because count is not constant
   increment = i; // ERROR: Cannot modify a const object
} // end constructor Increment

// print count and increment values
void Increment::print() const
{
   cout << "count = " << count << ", increment = " << increment << endl;
} // end function print
```

**图 10.8** | 通过赋值初始化内置数据类型常量的错误尝试。

```
// Fig. 10.9: fig10_09.cpp
// Program to test class Increment.
#include <iostream>
using std::cout;

#include "Increment.h" // include definition of class Increment

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
```

**图 10.9** | 测试类 `Increment` 的程序会产生编译错误。（第 1 部分，共 2 部分。）

```
21
22    return 0;
23 } // end main
```

*Borland C++ 命令行编译器错误信息：*

```
Error E2024 Increment.cpp 14: Cannot modify a const object in function
    Increment::Increment(int,int)
```

*Microsoft Visual C++ 2005 编译器错误信息：*

```
C:\cppfp_examples\ch10\Fig10_07_09\Increment.cpp(12) : error C2758:
    'Increment::increment' : must be initialized in constructor
    base/member initializer list
        C:\cppfp_examples\ch10\Fig10_07_09\Increment.h(20) :
            see declaration of 'Increment::increment'
C:\cppfp_examples\ch10\Fig10_07_09\Increment.cpp(14) : error C2166:
    l-value specifies const object
```

*GNU C++ 编译器错误信息：*

```
Increment.cpp:12: error: uninitialized member 'Increment::increment' with
    'const' type 'const int'
Increment.cpp:14: error: assignment of read-only data-member
    `Increment::increment'
```

**图 10.9** | 测试类 Increment 的程序会产生编译错误。（第 2 部分，共 2 部分。）

## 10.3 组合：对象作为类的成员

AlarmClock 对象需要知道应该在什么时候响铃，那么为什么不将一个 Time 对象作为 AlarmClock 类的成员呢？这种能力称为*组合*，有时也称为*has-a 关系*——一个类可以将其他类的对象作为成员。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_433_0.png)

**软件工程观察 10.5**

*软件复用的一种常见形式是组合，即一个类拥有其他类的对象作为成员。*

创建对象时，会自动调用其构造函数。之前，我们看到了如何向在 main 中创建的对象的构造函数传递实参。本节展示对象的构造函数如何向成员对象的构造函数传递实参，这是通过成员初始化器完成的。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_433_1.png)

**软件工程观察 10.6**

*成员对象按照它们在类定义中声明的顺序构造（而不是按照它们在构造函数的成员初始化列表中列出的顺序），并且在其外围类对象（有时称为宿主对象）构造之前构造。*

图 10.10–图 10.14 的程序使用类 Date（图 10.10–图 10.11）和类 Employee（图 10.12–图 10.13）来演示对象作为其他对象的成员。类 `Employee` 的定义（图 10.12）包含私有数据成员 `firstName`、`lastName`、`birthDate` 和 `hireDate`。成员 `birthDate` 和 `hireDate` 是类 `Date` 的 const 对象，类 `Date` 包含私有数据成员 month、day 和 year。`Employee` 构造函数的头部（图 10.13，第 18–21 行）指定该构造函数有四个参数（`first`、`last`、`dateOfBirth` 和 `dateOfHire`）。前两个参数在构造函数体中用于初始化字符数组 `firstName` 和 `lastName`。后两个参数通过成员初始化器传递给类 `Date` 的构造函数。头部中的冒号（`:`）将成员初始化器与参数列表分隔开。成员初始化器指定的是要传递给成员 `Date` 对象构造函数的 `Employee` 构造函数参数。参数 `dateOfBirth` 被传递给对象 `birthDate` 的构造函数（图 10.13，第 20 行），参数 `dateOfHire` 被传递给对象 `hireDate` 的构造函数（图 10.13，第 21 行）。同样，成员初始化器之间用逗号分隔。在学习类 `Date`（图 10.10）时，请注意该类没有提供接收 `Date` 类型参数的构造函数。那么，`Employee` 构造函数中的成员初始化列表如何能够通过将 Date 对象传递给它们的 Date 构造函数来初始化 `birthDate` 和 `hireDate` 对象呢？正如第 9 章提到的，编译器为每个类提供一个默认复制构造函数，它会将构造函数实参对象的每个数据成员复制到正在初始化的对象的相应成员中。第 11 章将讨论如何定义定制的复制构造函数。

图 10.14 创建了两个 Date 对象（第 11–12 行），并将它们作为实参传递给第 13 行创建的 Employee 对象的构造函数。第 16 行输出 Employee 对象的数据。当在第 11–12 行创建每个 Date 对象时，图 10.11 第 11–28 行定义的 Date 构造函数会显示一行输出，以表明该构造函数已被调用（参见示例输出的前两行）。[**注意：** 图 10.14 的第 13 行会导致另外两次 Date 构造函数调用，但这两次调用不会出现在程序输出中。当 Employee 的每个 Date 成员对象在 Employee 构造函数的成员初始化列表（图 10.13，第 21–21 行）中被初始化时，都会调用类 Date 的默认复制构造函数。该构造函数由编译器隐式定义，不包含任何用于显示其调用时机的输出语句。我们将在第 11 章详细讨论复制构造函数和默认复制构造函数。]

```
// Fig. 10.10: Date.h
// Date class definition; Member functions defined in Date.cpp
#ifndef DATE_H
#define DATE_H

class Date
{
public:
   Date( int = 1, int = 1, int = 1900 ); // default constructor
   void print() const; // print date in month/day/year format
   ~Date(); // provided to confirm destruction order
private:
   int month; // 1-12 (January-December)
   int day; // 1-31 based on month
   int year; // any year

   // utility function to check if day is proper for month and year
   int checkDay( int ) const;
}; // end class Date

#endif
```

## 图 10.10 | Date 类定义。

```
// Fig. 10.11: Date.cpp
// Date class member-function definitions.
#include <iostream>
using std::cout;
using std::endl;

#include "Date.h" // include Date class definition

// constructor confirms proper value for month; calls
// utility function checkDay to confirm proper value for day
Date::Date( int mn, int dy, int yr )
{
    if ( mn > 0 && mn <= 12 ) // validate the month
        month = mn;
    else
    {
        month = 1; // invalid month set to 1
        cout << "Invalid month (" << mn << ") set to 1.\n";
    } // end else

    year = yr; // could validate yr
    day = checkDay( dy ); // validate the day

    // output Date object to show when its constructor is called
    cout << "Date object constructor for date ";
    print();
    cout << endl;
} // end Date constructor

// print Date object in form month/day/year
void Date::print() const
{
    cout << month << '/' << day << '/' << year;
} // end function print

// output Date object to show when its destructor is called
Date::~Date()
{
    cout << "Date object destructor for date ";
    print();
    cout << endl;
} // end ~Date destructor

// utility function to confirm proper day value based on
// month and year; handles leap years, too
int Date::checkDay( int testDay ) const
{
```

图 10.11 | Date 类成员函数定义。（第 1 部分，共 2 部分。）

