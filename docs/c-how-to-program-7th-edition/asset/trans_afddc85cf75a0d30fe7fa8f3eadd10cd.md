
能够确定意图使用的是哪个版本的 ++。前缀版本的重载方式与任何其他前缀一元运算符完全相同。

## 重载前缀自增运算符

例如，假设我们希望将 Date 对象 d1 中的日期加 1。当编译器看到前置自增表达式 ++d1 时，编译器会生成成员函数调用

```cpp
d1.operator++()
```

该运算符函数的原型将为

```cpp
Date &operator++();
```

如果前缀自增运算符实现为全局函数，那么当编译器看到表达式 ++d1 时，编译器会生成函数调用

```cpp
operator++( d1 )
```

该运算符函数的原型将在 Date 类中声明为

```cpp
Date &operator++( Date & );
```

## 重载后缀自增运算符

重载后缀自增运算符会带来一个挑战，因为编译器必须能够区分重载的前缀自增运算符函数与后缀自增运算符函数的签名。C++ 采用的约定是：当编译器看到后置自增表达式 d1++ 时，它会生成成员函数调用

```cpp
d1.operator++( 0 )
```

该函数的原型为

```cpp
Date operator++( int )
```

参数 0 严格来说是一个“哑值”，它使编译器能够区分前缀和后缀自增运算符函数。同样的语法也用于区分前缀和后缀自减运算符函数。

如果后缀自增实现为全局函数，那么当编译器看到表达式 d1++ 时，编译器会生成函数调用

```cpp
operator++( d1, 0 )
```

该函数的原型将为

```cpp
Date operator++( Date &, int );
```

同样，0 参数由编译器用来区分实现为全局函数的前缀和后缀自增运算符。请注意，后缀自增运算符按值返回 Date 对象，而前缀自增运算符按引用返回 Date 对象，因为后缀自增运算符通常返回一个临时对象，其中包含自增发生之前该对象的原始值。C++ 将此类对象视为右值，不能用于赋值语句的左侧。前缀自增运算符返回实际自增后的对象及其新值。这样的对象可以在连续表达式中用作左值。

### 性能提示 11.2

*后缀自增（或自减）运算符创建的额外对象可能导致显著的性能问题——尤其是当该运算符用于循环中时。因此，只有当程序的逻辑需要后置自增（或后置自减）时，才应使用后缀自增（或自减）运算符。*

本节中关于重载前缀和后缀自增运算符的所有说明，同样适用于重载前缀和后缀自减运算符。接下来，我们考察一个带有重载前缀和后缀自增运算符的 Date 类。

### 11.13 案例研究：Date 类

图 11.9–11.11 中的程序演示了一个 Date 类，它使用重载的前缀和后缀自增运算符将 Date 对象中的日期加 1，并在必要时对月份和年份进行相应的递增。Date 头文件（图 11.9）指明，Date 的公共接口包括一个重载的流插入运算符（第 11 行）、一个默认构造函数（第 13 行）、一个 setDate 函数（第 14 行）、一个重载的前缀自增运算符（第 15 行）、一个重载的后缀自增运算符（第 16 行）、一个重载的 += 加法赋值运算符（第 17 行）、一个用于测试闰年的函数（第 18 行）以及一个用于判断某天是否为该月最后一天的函数（第 19 行）。

```cpp
 1  // Fig. 11.9: Date.h
 2  // Date class definition with overloaded increment operators.
 3  #ifndef DATE_H
 4  #define DATE_H
 5
 6  #include <iostream>
 7  using namespace std;
 8
 9  class Date
10  {
11    friend ostream &operator<<( ostream &, const Date & );
12  public:
13    Date( int m = 1, int d = 1, int y = 1900 ); // default constructor
14    void setDate( int, int, int ); // set month, day, year
15    Date &operator++(); // prefix increment operator
16    Date operator++( int ); // postfix increment operator
17    const Date &operator+=( int ); // add days, modify object
18    static bool leapYear( int ); // is date in a leap year?
19    bool endOfMonth( int ) const; // is date at the end of month?
20  private:
21    int month;
22    int day;
23    int year;
24
25    static const int days[]; // array of days per month
26    void helpIncrement(); // utility function for incrementing date
27  }; // end class Date
28
29  #endif
```

*图 11.9 | 带重载自增运算符的 Date 类定义。*

```cpp
// Fig. 11.10: Date.cpp
// Date class member- and friend-function definitions.
#include <iostream>
#include <string>
#include "Date.h"

using namespace std;

// initialize static member; one classwide copy
const int Date::days[] =
   { 0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31 };

// Date constructor
Date::Date( int m, int d, int y )
{
   setDate( m, d, y );
} // end Date constructor

// set month, day and year
void Date::setDate( int mm, int dd, int yy )
{
   month = ( mm >= 1 && mm <= 12 ) ? mm : 1;
   year = ( yy >= 1900 && yy <= 2100 ) ? yy : 1900;

   // test for a leap year
   if ( month == 2 && leapYear( year ) )
      day = ( dd >= 1 && dd <= 29 ) ? dd : 1;
   else
      day = ( dd >= 1 && dd <= days[ month ] ) ? dd : 1;
} // end function setDate

// overloaded prefix increment operator
Date &Date::operator++()
{
   helpIncrement(); // increment date
   return *this; // reference return to create an lvalue
} // end function operator++

// overloaded postfix increment operator; note that the
// dummy integer parameter does not have a parameter name
Date Date::operator++( int )
{
   Date temp = *this; // hold current state of object
   helpIncrement();

   // return unincremented, saved, temporary object
   return temp; // value return; not a reference return
} // end function operator++

// add specified number of days to date
const Date &Date::operator+=( int additionalDays )
{
   for ( int i = 0; i < additionalDays; i++ )
      helpIncrement();

   return *this; // enables cascading
} // end function operator+=

// if the year is a leap year, return true; otherwise, return false
bool Date::leapYear( int testYear )
{
   if ( testYear % 400 == 0 ||
        ( testYear % 100 != 0 && testYear % 4 == 0 ) )
      return true; // a leap year
   else
      return false; // not a leap year
} // end function leapYear

// determine whether the day is the last day of the month
bool Date::endOfMonth( int testDay ) const
{
   if ( month == 2 && leapYear( year ) )
      return testDay == 29; // last day of Feb. in leap year
   else
      return testDay == days[ month ];
} // end function endOfMonth

// function to help increment the date
void Date::helpIncrement()
{
   // day is not end of month
   if ( !endOfMonth( day ) )
      day++; // increment day
   else
      if ( month < 12 ) // day is end of month and month < 12
      {
         month++; // increment month
         day = 1; // first day of new month
      } // end if
      else // last day of year
      {
         year++; // increment year
         month = 1; // first month of new year
         day = 1; // first day of new month
      } // end else
} // end function helpIncrement

// overloaded output operator
ostream &operator<<( ostream &output, const Date &d )
{
   static string monthName[ 13 ] = { "", "January", "February",
      "March", "April", "May", "June", "July", "August",
      "September", "October", "November", "December" };
   output << monthName[ d.month ] << " " << d.day << ", " << d.year;
   return output; // enables cascading
} // end function operator<<
```

*图 11.10 | Date 类的成员函数和友元函数定义。（第 2 部分，共 2 部分。）*
