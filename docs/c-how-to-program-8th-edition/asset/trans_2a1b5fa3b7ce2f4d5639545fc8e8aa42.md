
```cpp
#include "Time.h" // include definition of class Time from Time.h

using namespace std;

// Time constructor initializes each data member to zero.
Time::Time()
{
   hour = minute = second = 0;
} // end Time constructor

// set new Time value using universal time
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
   {
      throw invalid_argument(
         "hour, minute and/or second was out of range" );
   }
} // end function setTime

// print Time in universal-time format (HH:MM:SS)
void Time::printUniversal()
{
   cout << setfill( '0' ) << setw( 2 ) << hour << ":"
        << setw( 2 ) << minute << ":" << setw( 2 ) << second;
} // end function printUniversal

// print Time in standard-time format (HH:MM:SS AM or PM)
void Time::printStandard()
{
   cout << ( ( hour == 0 || hour == 12 ) ? 12 : hour % 12 ) << ":"
        << setfill( '0' ) << setw( 2 ) << minute << ":"
        << setw( 2 ) << second << ( hour < 12 ? " AM" : " PM" );
} // end function printStandard
```

**图 9.2** | Time 类成员函数定义。（第 2 部分，共 2 部分。）

除了静态 const int 数据成员（你在第 7 章已经见过）之外，类的数据成员只能在类体中声明它们的位置进行初始化——不过下一版 C++ 标准将允许这样做。强烈建议由类的构造函数初始化这些数据成员，因为基本类型的数据成员没有默认初始化。数据成员也可以通过 Time 的 set 函数赋值。

![](img/bfd978e7e9b192bab46ec2a89e481263_416_0.png)

> **常见编程错误 9.1**
>
> 试图在类定义中显式初始化类的非静态数据成员属于语法错误。

## Time 类成员函数 `setTime` 与抛出异常

函数 `setTime`（第 17—30 行）是一个公有函数，它声明三个 int 参数并用这些参数设置时间。第 20—21 行测试每个实参以确定其值是否在范围内；如果在范围内，第 23—25 行将这些值赋给 hour、minute 和 second 数据成员。hour 值必须大于或等于 0 且小于 24，因为通用时间格式将小时表示为 0 到 23 的整数（例如，下午 1 点是 13 时，晚上 11 点是 23 时；午夜是 0 时，中午是 12 时）。类似地，minute 和 second 都必须大于或等于 0 且小于 60。对于超出这些范围的值，`setTime` 抛出类型为 `invalid_argument` 的异常（第 28—29 行），它通知客户端代码收到了无效实参。正如你在 7.11 节所学，可以使用 `try...catch` 捕获异常并尝试从中恢复，我们将在图 9.3 中这样做。`throw` 语句（第 28—29 行）创建一个 `invalid_argument` 类型的新对象。该类名后的圆括号表示调用 `invalid_argument` 构造函数，允许我们指定自定义错误消息字符串。异常对象创建后，`throw` 语句立即终止函数 `setTime`，并将异常返回给尝试设置时间的代码。*[注意：为避免 GNU C++ 编译错误，你可能需要包含头文件 `<stdexcept>` 才能使用类 `invalid_argument`。]*

> **错误预防提示 9.2**
>
> 每个粘性设置（例如填充字符或浮点精度）在不再需要时都应恢复为之前的设置。否则可能导致程序后面输出格式不正确。第 15 章“流输入/输出”讨论了如何重置填充字符和精度。

![](img/bfd978e7e9b192bab46ec2a89e481263_417_0.png)

## Time 类成员函数 `printUniversal`

函数 `printUniversal`（图 9.2 的第 33—37 行）不接受实参，并以通用时间格式输出时间，该格式由三对用冒号分隔的、分别表示小时、分钟和秒的数字组成。例如，如果时间为下午 1:30:07，函数 `printUniversal` 将显示 13:30:07。第 35 行使用参数化流操纵符 `setfill` 指定当整数在比其数字位数更宽的字段中输出时显示的填充字符。默认情况下，填充字符出现在数字的左侧。在本例中，如果 minute 值为 2，它将显示为 02，因为填充字符被设置为零（'0'）。如果要输出的数字填满了指定字段，则不会显示填充字符。一旦使用 `setfill` 指定了填充字符，它就会应用于后续所有在比所显示值更宽的字段中显示的值（也就是说，`setfill` 是“粘性”设置）。这与 `setw` 相反，后者只应用于下一个显示的值（`setw` 是“非粘性”设置）。

## Time 类成员函数 `printStandard`

函数 `printStandard`（第 40—45 行）不接受实参，并以标准时间格式输出时间，该格式由用冒号分隔的小时、分钟和秒值组成，后面跟 AM 或 PM 指示符（例如，1:27:06 PM）。与函数 `printUniversal` 一样，函数 `printStandard` 使用 `setfill('0')` 将 minute 和 second 格式化为必要时带前导零的两位数值。第 42 行使用条件运算符 (?:) 确定要显示的小时值——如果小时为 0 或 12（AM 或 PM），则显示为 12；否则，小时显示为 1 到 11 的值。第 44 行中的条件运算符确定将显示 AM 还是 PM。

## 在类定义之外定义成员函数；类作用域

即使成员函数在类定义中声明，也可以在该类定义之外定义（并通过作用域解析运算符“绑定”到类），该成员函数仍然处于该类的类作用域中——也就是说，除非被隐藏，否则它的名字对该类的其他成员是已知的。我们稍后将进一步讨论类作用域。

如果成员函数在类定义的主体中定义，则该成员函数被隐式声明为内联。请记住，编译器保留不对任何函数进行内联的权利。

![](img/bfd978e7e9b192bab46ec2a89e481263_418_0.png)

> **性能提示 9.1**
>
> 在类定义内部定义成员函数会使该成员函数内联（如果编译器选择这样做）。这可以提高性能。

![](img/bfd978e7e9b192bab46ec2a89e481263_418_1.png)

> **软件工程观察 9.2**
>
> 在类定义内部定义小型成员函数并不有助于实现最佳的软件工程，因为该类的客户端将能够看到函数的实现，而且如果函数定义发生更改，客户端代码必须重新编译。

![](img/bfd978e7e9b192bab46ec2a89e481263_418_2.png)

> **软件工程观察 9.3**
>
> 只应在类头文件中定义最简单、最稳定的成员函数（即其实现不太可能更改的成员函数）。

## 成员函数与全局函数

`printUniversal` 和 `printStandard` 成员函数不接受实参，因为这些成员函数隐式地知道要打印的是调用它们的那个特定 Time 对象的数据成员。这使得成员函数调用比过程式编程中的传统函数调用更简洁。

![](img/bfd978e7e9b192bab46ec2a89e481263_418_3.png)

> **软件工程观察 9.4**
>
> 使用面向对象编程方法通常通过减少参数数量来简化函数调用。面向对象编程的这一优点源于以下事实：将数据成员和成员函数封装在对象中，使成员函数有权访问数据成员。

![](img/bfd978e7e9b192bab46ec2a89e481263_418_4.png)

> **软件工程观察 9.5**
>
> 成员函数通常比非面向对象程序中的函数更短，因为数据成员中存储的数据理想情况下已由构造函数或存储新数据的成员函数验证过。由于数据已经在对象中，成员函数调用通常没有实参，或者比非面向对象语言中的函数调用具有更少的实参。因此，调用、函数定义和函数原型都更短。这改善了程序开发的许多方面。

![](img/bfd978e7e9b192bab46ec2a89e481263_418_5.png)

> **错误预防提示 9.3**
>
> 成员函数调用通常不接受实参，或者比非面向对象语言中的传统函数调用接受少得多的实参，这一事实降低了传递错误实参、错误类型实参或错误数量实参的可能性。

