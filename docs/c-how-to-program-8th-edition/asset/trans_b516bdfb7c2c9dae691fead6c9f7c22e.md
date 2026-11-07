

```cpp
setSales( i, salesFigure );
} // end for
} // end function getSalesFromUser

// set one of the 12 monthly sales figures; function subtracts
// one from month value for proper subscript in sales array
void SalesPerson::setSales( int month, double amount )
{
    // test for valid month and amount values
    if ( month >= 1 && month <= monthsPerYear && amount > 0 )
        sales[ month - 1 ] = amount; // adjust for subscripts 0-11
    else // invalid month or amount value
        cout << "Invalid month or sales figure" << endl;
} // end function setSales

// print total annual sales (with the help of utility function)
void SalesPerson::printAnnualSales()
{
    cout << setprecision( 2 ) << fixed
         << "\nThe total annual sales are: $"
         << totalAnnualSales() << endl; // call utility function
} // end function printAnnualSales

// private utility function to total annual sales
double SalesPerson::totalAnnualSales()
{
    double total = 0.0; // initialize total

    for ( int i = 0; i < monthsPerYear; ++i ) // summarize sales results
        total += sales[ i ]; // add month i sales to total

    return total;
} // end function totalAnnualSales
```

**图 9.6** | SalesPerson 类的成员函数定义。（第 2 部分，共 2 部分。）

在图 9.7 中，请注意，应用程序的 main 函数只包含一系列简单的成员函数调用——没有控制语句。操作 sales 数组的逻辑完全封装在 SalesPerson 类的成员函数中。

> **软件工程观察 9.8**
>
> 面向对象编程的一个现象是：一旦定义了类，创建和操作该类的对象通常只需发出一系列简单的成员函数调用——需要的控制语句很少，甚至没有。相比之下，在类成员函数的实现中通常会有控制语句。

```cpp
// Fig. 9.7: fig09_07.cpp
// Utility function demonstration.
// Compile this program with SalesPerson.cpp

// include SalesPerson class definition from SalesPerson.h
#include "SalesPerson.h"

int main()
{
    SalesPerson s; // create SalesPerson object s

    s.getSalesFromUser(); // note simple sequential code; there are
    s.printAnnualSales(); // no control statements in main
} // end main
```

**图 9.7** | 实用函数演示。（第 1 部分，共 2 部分。）

```text
Enter sales amount for month 1: 5314.76
Enter sales amount for month 2: 4292.38
Enter sales amount for month 3: 4589.83
Enter sales amount for month 4: 5534.03
Enter sales amount for month 5: 4376.34
Enter sales amount for month 6: 5698.45
Enter sales amount for month 7: 4439.22
Enter sales amount for month 8: 5893.57
Enter sales amount for month 9: 4909.67
Enter sales amount for month 10: 5123.45
Enter sales amount for month 11: 4024.97
Enter sales amount for month 12: 5923.92

The total annual sales are: $60120.59
```

**图 9.7** | 实用函数演示。（第 2 部分，共 2 部分。）

## 9.6 Time 类案例研究：带默认实参的构造函数

图 9.8–9.10 中的程序增强了 Time 类，以演示实参如何隐式传递给构造函数。图 9.2 中定义的构造函数将 hour、minute 和 second 初始化为 0（即通用时间午夜）。与其他函数一样，构造函数可以指定默认实参。图 9.8 的第 13 行声明 Time 构造函数包含默认实参，为传递给构造函数的每个实参指定默认值零。在图 9.9 中，第 10–13 行定义了 Time 构造函数的新版本，它接收参数 hour、minute 和 second 的值，这些值将分别用于初始化私有数据成员 hour、minute 和 second。Time 类为每个数据成员提供 set 和 get 函数。Time 构造函数现在调用 setTime，后者调用 setHour、setMinute 和 setSecond 函数来验证并实际将数据设置到数据成员中。构造函数的默认实参确保：即使在构造函数调用中未提供任何值，构造函数仍会初始化数据成员。将其所有实参都设为默认值的构造函数也是默认构造函数——也就是说，是可以在不带实参的情况下调用的构造函数。每个类最多只能有一个默认构造函数。

> **软件工程观察 9.9。**
>
> 对函数默认实参值的任何更改都要求重新编译客户端代码（以确保程序仍能正确运行）。

```cpp
// Fig. 9.8: Time.h
// Time class containing a constructor with default arguments.
// Member functions defined in Time.cpp.

// prevent multiple inclusions of header
#ifndef TIME_H
#define TIME_H

// Time abstract data type definition
class Time
{
public:
   Time( int = 0, int = 0, int = 0 ); // default constructor

   // set functions
   void setTime( int, int, int ); // set hour, minute, second
   void setHour( int ); // set hour (after validation)
   void setMinute( int ); // set minute (after validation)
   void setSecond( int ); // set second (after validation)

   // get functions
   int getHour(); // return hour
   int getMinute(); // return minute
   int getSecond(); // return second

   void printUniversal(); // output time in universal-time format
   void printStandard(); // output time in standard-time format
private:
   int hour; // 0 - 23 (24-hour clock format)
   int minute; // 0 - 59
   int second; // 0 - 59
}; // end class Time

#endif
```

**图 9.8** | 包含带默认实参构造函数的 Time 类。

在图 9.9 中，构造函数的第 12 行使用传递给构造函数的值（或默认值）调用成员函数 setTime。函数 setTime 调用 setHour 以确保为 hour 提供的值在 0–23 范围内，然后调用 setMinute 和 setSecond 以确保 minute 和 second 的值分别在 0–59 范围内。函数 setHour（第 24–30 行）、setMinute（第 33–39 行）和 setSecond（第 42–48 行）在接收到超出范围的实参时都会抛出异常。

```cpp
// Fig. 9.9: Time.cpp
// Member-function definitions for class Time.
#include <iostream>
#include <iomanip>
```

**图 9.9** | Time 类的成员函数定义，包括一个接收实参的构造函数。（第 1 部分，共 3 部分。）

```cpp
// return minute value
int Time::getMinute()
{
   return minute;
} // end function getMinute

// return second value
int Time::getSecond()
{
   return second;
} // end function getSecond

// print Time in universal-time format (HH:MM:SS)
void Time::printUniversal()
{
   cout << setfill( '0' ) << setw( 2 ) << getHour() << ":"
        << setw( 2 ) << getMinute() << ":" << setw( 2 ) << getSecond();
} // end function printUniversal

// print Time in standard-time format (HH:MM:SS AM or PM)
void Time::printStandard()
{
   cout << ( ( getHour() == 0 || getHour() == 12 ) ? 12 : getHour() % 12 )
        << ":" << setfill( '0' ) << setw( 2 ) << getMinute()
        << ( hour < 12 ? " AM" : " PM" );
} // end function printStandard
```

**图 9.9** | Time 类的成员函数定义，包括一个接收实参的构造函数。（第 3 部分，共 3 部分。）

图 9.10 中的函数 main 初始化五个 Time 对象——一个在隐式构造函数调用中三个实参全部采用默认值（第 10 行），一个指定一个实参（第 11 行），一个指定两个实参（第 12 行），一个指定三个实参（第 13 行），还有一个指定三个无效实参（第 38 行）。程序以通用时间格式和标准时间格式显示每个对象。对于 Time 对象 t5（第 38 行），程序显示错误消息，因为构造函数实参超出范围。

```cpp
// Fig. 9.10: fig09_10.cpp
// Demonstrating a default constructor for class Time.
#include <iostream>
#include <stdexcept>
#include "Time.h" // include definition of class Time from Time.h
using namespace std;

int main()
{
   Time t1;             // all arguments defaulted
   Time t2( 2 );        // hour specified; minute and second defaulted
   Time t3( 22, 34 );   // hour and minute specified; second defaulted
   Time t4( 12, 25, 42 ); // hour, minute and second specified
```

**图 9.10** | 带默认实参的构造函数。（第 1 部分，共 2 部分。）

