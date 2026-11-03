
可与对其他 PhoneNumber 对象或其他数据类型的输入操作级联。例如，程序可以在一条语句中输入两个 PhoneNumber 对象，如下所示：

```cpp
cin >> phone1 >> phone2;
```

首先，表达式 cin >> phone1 通过进行非成员函数调用来执行

```cpp
operator>>( cin, phone1 );
```

此调用随后将 cin 的引用作为 cin >> phone1 的值返回，因此表达式的剩余部分被简单解释为 cin >> phone2。这通过进行非成员函数调用来执行

```cpp
operator>>( cin, phone2 );
```

### 良好的编程实践 18.1

重载运算符应模仿其内置对应项的功能——例如，+ 运算符应执行加法，而不是减法。避免过度或不一致地使用运算符重载，因为这会使程序晦涩难懂且难以阅读。

### 重载流插入 (<<) 运算符

流插入运算符函数（图 18.4，第 11–16 行）接受一个 ostream 引用（output）和一个 const PhoneNumber 引用（number）作为参数，并返回一个 ostream 引用。函数 operator<< 显示 PhoneNumber 类型的对象。当编译器看到表达式

```cpp
cout << phone
```

在图 18.5 的第 22 行，编译器生成非成员函数调用

```cpp
operator<<( cout, phone );
```

函数 operator<< 将电话号码的各部分作为字符串显示，因为它们以字符串对象的形式存储。

### 将运算符重载为非成员友元函数

函数 operator>> 和 operator<< 在 PhoneNumber 中声明为非成员友元函数（图 18.3，第 11–12 行）。它们是非成员函数，因为 PhoneNumber 类的对象必须是运算符的右操作数。如果这些是 PhoneNumber 成员函数，则输出和输入 PhoneNumber 时必须使用以下笨拙的语句：

```cpp
phone << cout;
phone >> cin;
```

这样的语句会让大多数 C++ 程序员感到困惑，他们习惯于 cout 和 cin 分别作为 << 和 >> 的左操作数出现。

函数 operator>> 的参数列表（第 21 行）是非 const 的，因为 PhoneNumber 对象必须被修改以将输入的电话号码存储在对象中。

### 软件工程观察 18.2

> *为用户定义类型添加新的输入/输出功能，而无需修改标准输入/输出库类。这是 C++ 可扩展性的另一个例子。*

### 为什么将流插入和流提取运算符重载为非成员函数

重载的流插入运算符（<<）用于左操作数类型为 ostream & 的表达式中，如 cout << classObject。要在右操作数为用户定义类对象时以这种方式使用运算符，它必须作为非成员函数重载。要成为成员函数，operator<< 必须成为类 ostream 的成员。对于用户定义类来说这是不可能的，因为我们不允许修改 C++ 标准库类。同样，重载的流提取运算符（>>）用于左操作数类型为 istream & 的表达式中，如 cin >> classObject，右操作数是用户定义类对象，因此它也必须是非成员函数。此外，这些重载运算符函数可能需要访问正在输出或输入的类对象的私有数据成员，因此这些重载运算符函数可以作为类的友元函数以提高性能。

## 18.6 重载一元运算符

类的一个一元运算符可以作为没有参数的非静态成员函数重载，也可作为有一个参数的非成员函数重载，该参数必须是该类的对象（或对象引用）。实现重载运算符的成员函数必须是 non-static，以便它们可以访问每个对象中的非静态数据。

### 一元重载运算符作为成员函数

考虑重载一元运算符 ! 来测试你自己的 String 类的对象是否为空。这样的函数将返回一个 bool 结果。当一元运算符如 ! 被重载为没有参数的成员函数并且编译器看到表达式 !s（其中 s 是 String 类的对象）时，编译器会生成函数调用 s.operator!()。操作数 s 是 String 类成员函数 operator! 被调用的 String 对象。该函数声明如下：

```cpp
class String
{
public:
   bool operator!() const;
   ...
}; // end class String
```

### 一元重载运算符作为非成员函数

一元运算符如 ! 可以作为有一个参数的非成员函数重载。如果 s 是 String 类对象（或 String 类对象的引用），则 !s 被视为已编写调用 operator!(s)，从而调用声明如下的非成员 operator! 函数：

```cpp
bool operator!( const String & );
```

```cpp
24
25    static const std::array< unsigned int, 13 > days; // days per month
26    void helpIncrement(); // utility function for incrementing date
27  }; // end class Date
28
29 #endif
```

图 18.6 | 日期类定义，其中重载了增量运算符。（第 2 部分，共 2 部分。）

```cpp
1 // Fig. 18.7: Date.cpp
2 // Date class member- and friend-function definitions.
3 #include <iostream>
4 #include <string>
5 #include "Date.h"
6 using namespace std;
7
8 // initialize static member; one classwide copy
9 const array< unsigned int, 13 > Date::days =
10    { 0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31 };
11
12 // Date constructor
13 Date::Date( int month, int day, int year )
14 {
15    setDate( month, day, year );
16 } // end Date constructor
17
18 // set month, day and year
19 void Date::setDate( int mm, int dd, int yy )
20 {
21    if ( mm >= 1 && mm <= 12 )
22       month = mm;
23    else
24       throw invalid_argument( "Month must be 1-12" );
25
26    if ( yy >= 1900 && yy <= 2100 )
27       year = yy;
28    else
29       throw invalid_argument( "Year must be >= 1900 and <= 2100" );
30
31    // test for a leap year
32    if ( ( month == 2 && leapYear( year ) && dd >= 1 && dd <= 29 ) ||
33         ( dd >= 1 && dd <= days[ month ] ) )
34       day = dd;
35    else
36       throw invalid_argument(
37          "Day is out of range for current month and year" );
38 } // end function setDate
39
40 // overloaded prefix increment operator
41 Date &Date::operator++()
42 {
```

**图 18.7** | 日期类成员和友元函数定义。（第 1 部分，共 3 部分。）

```cpp
        day = 1; // first day of new month
    } // end if
    else // last day of year
    {
        ++year; // increment year
        month = 1; // first month of new year
        day = 1; // first day of new month
    } // end else
} // end function helpIncrement

// overloaded output operator
ostream& operator<<( ostream &output, const Date &d )
{
    static string monthName[ 13 ] = { "", "January", "February",
        "March", "April", "May", "June", "July", "August",
        "September", "October", "November", "December" };
    output << monthName[ d.month ] << '/' << d.day << '/' << d.year;
    return output; // enables cascading
} // end function operator<<
```

**图 18.7** | 日期类成员和友元函数定义。（第 3 部分，共 3 部分。）

```cpp
// Fig. 18.8: fig18_08.cpp
// Date class test program.
#include <iostream>
#include "Date.h" // Date class definition
using namespace std;

int main()
{
    Date d1( 12, 27, 2010 ); // December 27, 2010
    Date d2; // defaults to January 1, 1900

    cout << "d1 is " << d1 << "\nd2 is " << d2;
    cout << "\n\nDate d1 + 7 is " << ( d1 + 7 );

    d2.setDate( 2, 28, 2008 );
    cout << "\n\nd2 is " << d2;
    cout << "\n\nd2 + 1 is " << ++d2 << " (Leap year allows 29th)";

    Date d3( 7, 13, 2010 );

    cout << "\n\nTesting the prefix increment operator:\n"
         << "  d3 is " << d3 << endl;
    cout << "++d3 is " << ++d3 << endl;
    cout << "  d3 is " << d3;

    cout << "\n\nTesting the postfix increment operator:\n"
         << "  d3 is " << d3 << endl;
    cout << "d3++ is " << d3++ << endl;
    cout << "  d3 is " << d3 << endl;
} // end main
```

**图 18.8** | 日期类测试程序。（第 1 部分，共 2 部分。）
