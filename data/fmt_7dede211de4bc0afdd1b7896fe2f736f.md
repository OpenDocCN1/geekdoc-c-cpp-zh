
原始版本显式访问了 `t.minutes` 和 `t.hours`，所以它必须是友元。这个版本只使用整个 `Time` 对象，让成员函数处理私有值，因此这个版本不需要是友元。尽管如此，使其友元是有理由的。

提示：如果你想访问私有数据，该函数必须是友元。

## 一种常见的友元：重载 `<<`

类的一个非常实用的特性是你可以重载 `<<` 运算符向屏幕输出数据。为了教类如何使用它，请使用以下定义：

```cpp
void operator<<(ostream & os, const Time & t)
{
    os << t.hours << " " << t.minutes << " minutes";
}
```

这允许你按照以下格式打印数据：
4 hours, 23 minutes

## 是友元还是非友元？

刚刚提出的实现有一个问题。像这样的语句运行良好：
`cout << trip;`

但该实现不允许你将重定义的 `<<` 运算符与 `cout` 使用的运算符结合起来：
`cout << "Trip time: " << trip << " (Tuesday)\n"; // 无法做到`

为了理解为什么这不起通以及必须做什么才能使其生效，你首先需要更多关于 `cout` 如何运作的信息。考虑以下语句：

# 介绍友元

```cpp
int x = 5;
int y = 8;
cout << x << y;
```

`C++` 从左到右读取输出语句，这意味着它等同于以下代码：

```
(cout << x) << y;
```

`<<` 运算符在 `iostream` 中定义，它在左侧接收一个 `ostream` 对象。显然，表达式 `cout << x` 满足这一要求，因为 `cout` 是一个 `ostream` 对象。但输出语句还要求整个表达式 `(cout << x)` 是一个 `ostream` 类型对象，因为它位于 `y` 的左侧。因此，`ostream` 类实现了 `operator<<()` 函数，以便它返回一个 `ostream` 对象的引用。特别是，它返回了调用对象——`cout` 的引用，在这种情况下，表达式 `(cout << x)` 本身就是 `ostream` 对象，它可以被用在运算符的左侧。

你可以对友元函数采取相同的方法。你只需要修改 `operator<<()` 函数，使其返回一个 `ostream` 对象的引用即可：

```cpp
ostream & operator<<(ostream & os, const Time &t)
{
    os << t.hours << " hours, " << t.minutes << " minutes";
    return os;
}
```

注意返回类型是 `ostream &`。回想，这意味着函数返回一个 `ostream` 对象的引用。由于程序最初就将对象引用传递给函数，其最终效果是函数的返回值就是传递给它的对象。也就是说，语句

```
cout << trip;
operator<< (cout, trip);
```

该调用返回了 `cout` 对象。现在接下来的语句可以运行：

```cpp
cout << "Trip time: " << trip << " (Tuesday)\n"; // 可以执行
```

让我们将其拆分为不同的步骤来查看它是如何工作的。首先，以下代码调用了特定的 `ostream::<<` 定义，它显示字符串并返回当时的 `cout` 对象：

```cpp
cout << "Trip time:
```

因此，表达式 `<< "Trip time: "` 显示了字符串，然后被它的返回值 `cout` 替换。这使得原始语句简化为如下内容：

```cpp
cout << trip << "Tuesday)\n";
```

# 第11章 类操作

接下来，程序使用 `Time` 类的 `<<` 来显示行程值并再次返回 `cout` 对象。这使得语句简化为：

```cpp
cout << *(Tuesday)\n";
```

程序通过使用字符串的 `ostream::<<` 定义来显示字符串并结束。

有趣的一点是，这个版本的 `operator<<()` 也可以用于文件输出：

```cpp
#include <fstream>
ofstream fout;
fout.open("savtime.txt");
Time trip(12, 40);
fout << trip;
```

最后一条语句变为：

```cpp
operator<< (fout, trip);
```

正如第8章所示，类继承的属性允许 `ostream` 引用指向 `ostream` 对象，也可以指向 `ofstream` 对象。

> 提示
> 通常情况下，要重载 `<<` 运算符来显示类 `c_name` 的对象，你使用定义如下形式的友元函数：

```cpp
ostream& operator<<(ostream & os, const c_name & obj)
{
os << ...; // 显示对象内容
return os;
}
```

列表 11.10 显示了修改后的类定义，包含了两个友元函数 `operator*()` 和 `operator<<()`。由于代码非常短，我们将其中第一个实现为内联函数。（当定义同时也是原型声明时，在此情况下，你将使用 `friend` 前缀。）

> 注意
> 你仅在类声明中的原型函数中使用 `friend` 关键字。除非该定义本身也是原型，否则你不在函数定义中使用它。

# 列表 11.10 mytime3.h

```cpp
// mytime3.h -- 带有友元的 Time 类
#ifndef MYTIME3_H_
#define MYTIME3_H_
#include <iostream>
class Time
{}
```
```cpp
private:
int hours;
int minutes;
public:
Time();
Time(int h, int m = 0);
void AddMin(int m);
void AddHr(int h);
void Reset(int h = 0, int m = 0);
Time operator+(const Time & t) const;
Time operator-(const Time & t) const;
Time operator*(double n) const;
friend Time operator*(double m, const Time & t)
    { return t * m; } // 内联定义
friend std::ostream& operator<<(std::ostream& os, const Time & t);
#endif
```

列表 11.11 显示了修改后的定义集。再次注意，方法使用了 `Time::` 限定符，而友元函数没有。同样注意，由于 `mytime3.h` 包含了 `iostream` 并提供了 `std::ostream` 的声明，在 `mytime3.cpp` 中包含 `mytime3.h` 会为实现文件提供 `ostream` 的支持。

# 列表 11.11 mytime3.cpp

```cpp
// mytime3.cpp -- 实现 Time3.h
#include "mytime3.h"
Time::Time()
{
hours = minutes = 0;
}
Time::Time(int h, int m )
{
hours = h;
minutes = m;
}
void Time::AddMin(int m)
{
minutes += m;
hours += minutes / 60;
minutes %= 60;
}
```
```cpp
void Time::AddHr(int h)
{
    hours += h;
}
```
```cpp
void Time::Reset(int h, int m)
{
    hours = h;
    minutes = m;
}
```
```cpp
Time Time::operator+(const Time & t) const
{
    Time sum;
    sum.minutes = minutes + t.minutes;
    sum.hours = hours + sum.minutes / 60;
    sum.minutes %= 60;
    return sum;
}
```
```cpp
Time Time::operator-(const Time & t) const
{
    Time diff;
    int tot1, tot2;
    tot1 = t.minutes + 60;
    tot2 = minutes + 60;
    diff.minutes = (tot2 - tot1) % 60;
    diff.hours = (tot2 - tot1) / 60;
    return diff;
}
```
```cpp
Time Time::operator*(double mult) const
{
    Time result;
    long totalminutes = hours * mult + 60;
    result.hours = totalminutes / 60;
    result.minutes = totalminutes % 60;
    return result;
}
```
```cpp
std::ostream & operator<<(std::ostream & os, const Time & t)
{
    os << t.hours << " hours, " << t.minutes << " minutes";
    return os;
}
```

# 重载运算符：成员与非成员

列表 11.12 显示了一个示例程序。技术上，`mytime3.cpp` 不需要包含 `iostream`，`mytime3.h` 已经包含了。作为 `Time` 类的用户，你并不一定知道包含了哪些文件，因此你需要负责声明那些文件。

列表 11.12 mytime3.cpp

```cpp
// mytime3.cpp -- 使用 Time 类
// 一起编译 mytime3.cpp 和 mytime3.cpp
#include <iostream>
#include "mytime3.h"
int main()
{
    using std::cout;
    using std::endl;
    Time aida(3, 35);
    Time tosca(2, 48);
    Time temp;
    cout << "Aida and Tosca:\n";
    cout << "aida: " << tosca << endl;
    temp = aida + tosca; // operator+
    cout << "Aida + Tosca: " << temp << endl;
    temp = aida * 1.1; // operator*
    cout << "Aida * 1.1: " << temp << endl;
    cout << "10.0 * tosca: " << tosca << endl;
    return 0;
}
```

这是列表 11.10、11.11 和 11.12 中程序的输出：

Aida and Tosca:
3 hours, 35 minutes; 2 hours, 48 minutes
Aida + Tosca: 6 hours, 23 minutes
Aida * 1.1: 4 hours, 11 minutes
10.0 * Tosca: 28 hours, 0 minutes

# 重载运算符：成员函数与非成员函数

对于许多运算符，你可以选择成员函数或非成员函数来实现运算符重载。通常，非成员版本是友元函数，以便它可以直接访问类的私有数据。例如，考虑 `Time` 类的加运算符。它在 `Time` 类声明中具有如下原型：

相反，类可以使用以下原型：

```cpp
// 非成员版本
friend Time operator+(const Time & t1, const Time & t2);
```

加运算符需要两个操作数。对于成员函数版本，一个通过 `this` 指针隐式传递，第二个作为函数参数式传递。对于友元版本，两者都作为参数传递。

> 注意
> 重载运算符函数的非成员版本所需的形式参数与运算符的数量相同。相同运算符的成员版本需要的少一个参数，因为一个操作数作为调用对象隐式传递的。

这两个原型中的每一个都匹配 `T2 + T3` 表达式，其中 `T2` 和 `T3` 是类型对象。编译器可以将语句

```
T1 = T2 + T3;
```

转换为以下任一种情况：

```cpp
T1 = T2.operator+(T3);      // 成员函数
T1 = operator+(T2, T3);     // 非成员函数
```
