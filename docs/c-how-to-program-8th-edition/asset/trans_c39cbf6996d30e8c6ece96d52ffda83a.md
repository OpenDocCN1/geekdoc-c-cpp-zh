
```cpp
// test for a leap year
if ( ( month == 2 && leapYear( year ) && dd >= 1 && dd <= 29 ) ||
     ( dd >= 1 && dd <= days[ month ] ) )
   day = dd;
else
   throw invalid_argument(
      "Day is out of range for current month and year" );
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
   for ( int i = 0; i < additionalDays; ++i )
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
      ++day; // increment day
   else
      if ( month < 12 ) // day is end of month and month < 12
      {
         ++month; // increment month
         day = 1; // first day of new month
      } // end if
      else // last day of year
      {
         ++year; // increment year
         month = 1; // first month of new year
         day = 1; // first day of new month
      } // end of else
} // end function helpIncrement

// overloaded output operator
ostream &operator<<( ostream &output, const Date &d )
{
   static string monthName[ 13 ] = { "", "January", "February",
      "March", "April", "May", "June", "July", "August",
      "September", "October", "November", "December" };
   output << monthName[ d.month ] << " " << d.day << ", " << d.year;
   return output; // enables cascading
} // end of function operator<<
```

图 11.7 | Date 类的成员函数和友元函数定义。（第2部分，共3部分。）

图 11.7 | Date 类的成员函数和友元函数定义。（第3部分，共3部分。）

```cpp
// Fig. 11.8: fig11_08.cpp
// Date class test program.
#include <iostream>
#include "Date.h" // Date class definition
using namespace std;

int main()
{
   Date d1( 12, 27, 2010 ); // December 27, 2010
   Date d2; // defaults to January 1, 1900

   cout << "d1 is " << d1 << "\nd2 is " << d2;
   cout << "\n\nd1 += 7 is " << ( d1 += 7 );

   d2.setDate( 2, 28, 2008 );
   cout << "\n\n d2 is " << d2;
   cout << "\n++d2 is " << ++d2 << " (leap year allows 29th)";

   Date d3( 7, 13, 2010 );

   cout << "\nTesting the prefix increment operator:\n"
        << "  d3 is " << d3 << endl;
   cout << "++d3 is " << ++d3 << endl;
   cout << "     d3 is " << d3;

   cout << "\nTesting the postfix increment operator:\n"
        << "  d3 is " << d3 << endl;
   cout << "d3++ is " << d3++ << endl;
   cout << "     d3 is " << d3 << endl;
} // end main
```

图 11.8 | Date 类测试程序。（第1部分，共2部分。）

```text
d1 is December 27, 2010
d2 is January 1, 1900

d1 += 7 is January 3, 2011

  d2 is February 28, 2008
++d2 is February 29, 2008 (leap year allows 29th)
Testing the prefix increment operator:
  d3 is July 13, 2010
++d3 is July 14, 2010
  d3 is July 14, 2010

Testing the postfix increment operator:
  d3 is July 14, 2010
d3++ is July 14, 2010
  d3 is July 15, 2010
```

*图 11.8* | Date 类测试程序。（第2部分，共2部分。）

函数 main（图 11.8）创建两个 Date 对象（第9—10行）——d1 初始化为2010年12月27日，d2 默认初始化为1900年1月1日。Date 构造函数（定义于图 11.7 第13—16行）调用 setDate（定义于图 11.7 第19—38行）来验证指定的月、日、年。为月、日或年指定无效值会导致 invalid_argument 异常。

main 的第12行使用重载的流插入运算符（定义于图 11.7 第107—114行）输出每个 Date 对象。main 的第13行使用重载的 += 运算符（定义于图 11.7 第59—65行）向 d1 加7天。第15行使用函数 setDate 将 d2 设置为2008年2月28日，该年是闰年。然后，第17行对 d2 进行前缀自增，以表明日期正确递增到2月29日。接着，第19行创建 Date 对象 d3，并用日期2010年7月13日初始化。然后第23行使用重载的前缀自增运算符将 d3 递增1。第21—24行在前缀自增操作前后输出 d3，以确认其工作正常。最后，第28行使用重载的后缀自增运算符递增 d3。第26—29行在后缀自增操作前后输出 d3，以确认其工作正常。

## Date 类的前缀自增运算符

重载前缀自增运算符很直接。前缀自增运算符（定义于图 11.7 第41—45行）调用工具函数 helpIncrement（定义于

## 11.10.1 使用 Array 类

图 11.9—11.11 的程序演示了 Array 类及其重载运算符。首先我们逐步分析 main（图 11.9）和程序的输出，然后考虑类定义（图 11.10）及其每个成员函数定义（图 11.11）。

```cpp
// Fig. 11.9: fig11_09.cpp
// Array class test program.
#include <iostream>
#include "Array.h"
using namespace std;

int main()
{
    Array integers1( 7 ); // seven-element Array
    Array integers2; // 10-element Array by default

    // print integers1 size and contents
    cout << "Size of Array integers1 is "
         << integers1.getSize()
         << "\nArray after initialization:\n" << integers1;

    // print integers2 size and contents
    cout << "\nSize of Array integers2 is "
         << integers2.getSize()
         << "\nArray after initialization:\n" << integers2;

    // input and print integers1 and integers2
    cout << "\nEnter 17 integers:" << endl;
    cin >> integers1 >> integers2;

    cout << "\nAfter input, the Arrays contain:\n"
         << "integers1:\n" << integers1
         << "integers2:\n" << integers2;

    // use overloaded inequality (!=) operator
    cout << "\nEvaluating: integers1 != integers2" << endl;

    if ( integers1 != integers2 )
        cout << "integers1 and integers2 are not equal" << endl;

    // create Array integers3 using integers1 as an
    // initializer; print size and contents
    Array integers3( integers1 ); // invokes copy constructor

    cout << "\nSize of Array integers3 is "
         << integers3.getSize()
         << "\nArray after initialization:\n" << integers3;

    // use overloaded assignment (=) operator
    cout << "\nAssigning integers2 to integers1:" << endl;
    integers1 = integers2; // note target Array is smaller
```

图 11.9 | Array 类测试程序。（第1部分，共3部分。）

```text
Evaluating: integers1 != integers2
integers1 and integers2 are not equal

Size of Array integers3 is 7
Array after initialization:
        1           2           3           4
        5           6           7

Assigning integers2 to integers1:
integers1:
        8           9           10          11
        12          13          14          15
        16          17

integers2:
        8           9           10          11
        12          13          14          15
        16          17

Evaluating: integers1 == integers2
integers1 and integers2 are equal

integers1[5] is 13

Assigning 1000 to integers1[5]
integers1:
        8           9           10          11
        12          1000        14          15
        16          17

Attempt to assign 1000 to integers1[15]
An exception occurred: Subscript out of range
```

**图 11.9** | Array 类测试程序。（第3部分，共3部分。）

### 创建数组、输出其大小并显示其内容

程序首先实例化两个 Array 类对象——integers1（图 11.9 第9行）含七个元素，integers2（第10行）使用默认 Array 大小——10个元素（由图 11.10 第14行中 Array 默认构造函数的原型指定）。第13—15行使用成员函数 getSize 确定 integers1 的大小，然后使用 Array 重载的流插入运算符输出 integers1 的内容。示例输出确认构造函数已正确地将 Array 元素设置为零。接着，第18—20行输出 Array integers2 的大小，然后使用 Array 重载的流插入运算符输出 integers2 的内容。

### 使用重载的流提取运算符填充数组

第23行提示用户输入17个整数。第24行使用 Array 重载的流提取运算符将前七个值读入 integers1，其余10个值读入 integers2。第26—28行使用重载的 Array 流插入运算符输出这两个数组，以确认输入执行正确。

### 使用重载的不等运算符

第33行通过求值以下条件来测试重载的不等运算符

```text
integers1 != integers2
```

程序输出表明这些 Array 不相等。

