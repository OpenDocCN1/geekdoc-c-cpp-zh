
> **错误预防提示 17.4**
>
> *为了使代码更清晰、更易维护，并避免错误，切勿用局部变量名隐藏数据成员。*

### *this* 指针的类型

*this* 指针的类型取决于对象的类型，以及使用 *this* 的成员函数是否声明为 const。例如，在类 `Employee` 的非 const 成员函数中，*this* 指针的类型为 `Employee *`。在 const 成员函数中，*this* 指针的类型为 `const Employee *`。

### 隐式和显式使用 *this* 指针访问对象的数据成员

图 17.23 演示了隐式和显式使用 *this* 指针，使类 `Test` 的成员函数能够打印 `Test` 对象的私有数据 `x`。在下一个示例和第 18 章中，我们将展示一些使用 *this* 的重要且微妙的示例。

```cpp
1  // Fig. 17.23: fig17_23.cpp
2  // Using the this pointer to refer to object members.
3  #include <iostream>
4  using namespace std;
5
6  class Test
7  {
8  public:
9      explicit Test( int = 0 ); // default constructor
10     void print() const;
11 private:
12     int x;
13 }; // end class Test
14
15 // constructor
16 Test::Test( int value )
17     : x( value ) // initialize x to value
18 {
19     // empty body
20 } // end constructor Test
21
22 // print x using implicit and explicit this pointers;
23 // the parentheses around *this are required
24 void Test::print() const
25 {
26     // implicitly use the this pointer to access the member x
27     cout << "    x = " << x;
28
29     // explicitly use the this pointer and the arrow operator
30     // to access the member x
31     cout << "\n  this->x = " << this->x;
32
33     // explicitly use the dereferenced this pointer and
34     // the dot operator to access the member x
35     cout << "\n(*this).x = " << (*this).x << endl;
36 } // end of function print
37
38 int main()
39 {
40     Test testObject( 12 ); // instantiate and initialize testObject
41
42     testObject.print();
43 } // end main
```

```text
        x = 12
    this->x = 12
  (*this).x = 12
```

**图 17.23** | 使用 *this* 指针引用对象成员。（第 1 和第 2 部分，共 2 部分。）

为便于说明，成员函数 `print`（第 24—36 行）首先通过隐式使用 *this* 指针打印 `x`（第 27 行）——只指定数据成员的名称。然后 `print` 使用两种不同的表示法通过 *this* 指针访问 `x`——在 *this* 指针上使用箭头运算符（`->`）（第 31 行），以及在解引用的 *this* 指针上使用点运算符（`.`）（第 35 行）。注意第 35 行中，当 *this* 与点成员选择运算符（`.`）一起使用时，其周围的括号。这些括号是必需的，因为点运算符的优先级高于 `*` 运算符。没有括号时，表达式 `*this.x` 的求值会像是被加上括号的 `*(this.x)`，这会导致 *编译错误*，因为点运算符不能用于指针。

*this* 指针的一个有趣用途是防止对象被赋值给自身。正如我们将在第 18 章看到的，当对象包含指向动态分配存储区的指针时，*自赋值* 可能导致严重错误。

### 使用 *this* 指针实现级联函数调用

*this* 指针的另一个用途是实现级联成员函数调用——也就是说，在同一条语句中调用多个函数（如图 17.26 第 12 行所示）。图 17.24—17.26 的程序修改了类 `Time` 的设置函数 `setHour`、`setMinute` 和 `setSecond`，使每个函数都返回一个 `Time` 对象的引用，以实现级联成员函数调用。注意图 17.25 中，这些成员函数函数体中的最后一条语句都返回 *this*（第 23、34、45 和 56 行），返回类型为 `Time&`。

图 17.26 的程序创建 `Time` 对象 `t`（第 9 行），然后在级联成员函数调用中使用它（第 12 和 24 行）。为什么要求以引用形式返回 *this* 能够奏效？点运算符（`.`）从左到右结合，因此第 12 行首先计算 `t.setHour(18)`，然后返回对象 `t` 的引用作为该函数调用的值。剩余表达式随后被解释为

```cpp
t.setMinute( 30 ).setSecond( 22 );
```

`t.setMinute(30)` 调用执行并返回对象 `t` 的引用。剩余表达式被解释为

```cpp
t.setSecond( 22 );
```

```cpp
// Fig. 17.24: Time.h
// Cascading member function calls.

// Time class definition.
// Member functions defined in Time.cpp.
#ifndef TIME_H
#define TIME_H

class Time
{
public:
   explicit Time( int = 0, int = 0, int = 0 ); // default constructor

   // set functions (the Time class uses set functions to enable cascading)
   Time &setTime( int, int, int ); // set hour, minute, second
   Time &setHour( int ); // set hour
   Time &setMinute( int ); // set minute
   Time &setSecond( int ); // set second

   // get functions (normally declared const)
   unsigned int getHour() const; // return hour
   unsigned int getMinute() const; // return minute
   unsigned int getSecond() const; // return second

   // print functions (normally declared const)
   void printUniversal() const; // print universal time
   void printStandard() const; // print standard time
private:
   unsigned int hour; // 0 - 23 (24-hour clock format)
   unsigned int minute; // 0 - 59
   unsigned int second; // 0 - 59
}; // end class Time

#endif
```

**图 17.24** | 为支持级联成员函数调用而修改的 Time 类。

```cpp
1  // Fig. 17.25: Time.cpp
2  // Time class member-function definitions.
3  #include <iostream>
4  #include <iomanip>
5  #include <stdexcept>
6  #include "Time.h" // Time class definition
7  using namespace std;
8
9  // constructor function to initialize private data;
10 // calls member function setTime to set variables;
11 // default values are 0 (see class definition)
12 Time::Time( int hr, int min, int sec )
13 {
14     setTime( hr, min, sec );
15 } // end Time constructor
16
17 // set values of hour, minute, and second
18 Time &Time::setTime( int h, int m, int s ) // note Time & return
19 {
20     setHour( h );
21     setMinute( m );
22     setSecond( s );
23     return *this; // enables cascading
24 } // end function setTime
25
26 // set hour value
27 Time &Time::setHour( int h ) // note Time & return
28 {
29     if ( h >= 0 && h < 24 )
30         hour = h;
31     else
32         throw invalid_argument( "hour must be 0-23" );
33
34     return *this; // enables cascading
35 } // end function setHour
36
37 // set minute value
38 Time &Time::setMinute( int m ) // note Time & return
39 {
40     if ( m >= 0 && m < 60 )
41         minute = m;
42     else
43         throw invalid_argument( "minute must be 0-59" );
44
45     return *this; // enables cascading
46 } // end function setMinute
47
48 // set second value
49 Time &Time::setSecond( int s ) // note Time & return
50 {
51     if ( s >= 0 && s < 60 )
52         second = s;
53     else
54         throw invalid_argument( "second must be 0-59" );
55
56     return *this; // enables cascading
57 } // end function setSecond
58
59 // get hour value
60 unsigned int Time::getHour() const
61 {
62     return hour;
63 } // end function getHour
64
65 // get minute value
66 unsigned int Time::getMinute() const
67 {
68     return minute;
69 } // end function getMinute
70
71 // get second value
72 unsigned int Time::getSecond() const
73 {
74     return second;
75 } // end function getSecond
76
77 // print Time in universal-time format (HH:MM:SS)
78 void Time::printUniversal() const
79 {
80     cout << setfill('0') << setw(2) << hour << ":"
81         << setw(2) << minute << ":" << setw(2) << second;
82 } // end function printUniversal
83
84 // print Time in standard-time format (HH:MM:SS AM or PM)
85 void Time::printStandard() const
86 {
87     cout << ( ( hour == 0 || hour == 12 ) ? 12 : hour % 12 )
88         << ":" << setfill('0') << setw(2) << minute
89         << ":" << setw(2) << second << ( hour < 12 ? " AM" : " PM" );
90 } // end function printStandard
```

**图 17.25** | 为支持级联成员函数调用而修改的 Time 类成员函数定义。（第 1—3 部分，共 3 部分。）

第 24 行（图 17.26）也使用了级联。注意，这里不能在 `printStandard` 之后继续链式调用另一个成员函数，因为 `printStandard` 不返回 `t` 的引用。在第 24 行中，将对 `printStandard` 的调用放在对 `setTime` 的调用之前会导致编译错误。第 18 章给出了几个使用级联函数调用的实际示例。其中一个示例使用多个 `<<` 运算符与 `cout`，在一条语句中输出多个值。

```cpp
1  // Fig. 17.26: fig17_26.cpp
2  // Cascading member-function calls with the this pointer.
3  #include <iostream>
4  #include "Time.h" // Time class definition
5  using namespace std;
6
7  int main()
8  {
9      Time t; // create Time object
10
11     // cascaded function calls
12     t.setHour( 18 ).setMinute( 30 ).setSecond( 22 );
```

**图 17.26** | 使用 *this* 指针进行级联成员函数调用。（第 1 部分，共 2 部分。）

