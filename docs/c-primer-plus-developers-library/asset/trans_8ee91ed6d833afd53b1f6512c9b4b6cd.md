
表 11.1 中的大多数运算符都可以通过成员函数或非成员函数进行重载。但是，下列运算符*只能*使用成员函数进行重载：

| 运算符 | 描述 |
|---|---|
| `=` | 赋值运算符 |
| `()` | 函数调用运算符 |
| `[]` | 下标运算符 |
| `->` | 通过指针访问类成员的运算符 |

> **注意**
>
> 本章并未涵盖限制列表或表 11.1 中提到的每一个运算符。不过，附录 E“其他运算符”总结了本书正文未涵盖的运算符。

**表 11.1 可重载的运算符**

|  |  |  |  |  |  |
|---|---|---|---|---|---|
| `+` | `-` | `*` | `/` | `%` | `^` |
| `&` | `\|` | `~` | `!` | `=` | `<` |
| `>` | `+=` | `-=` | `*=` | `/=` | `%=` |
| `^=` | `&=` | `\|=` | `<<` | `>>` | `>>=` |
| `<<=` | `==` | `!=` | `<=` | `>=` | `&&` |
| `\|\|` | `++` | `--` | `,` | `->*` | `->` |
| `()` | `[]` | `new` | `delete` | `new []` | `delete []` |

除了这些形式上的限制之外，在重载运算符时还应保持合理的克制。例如，你不应重载 `*` 运算符来实现交换两个 Time 对象的数据成员。这种表示法本身无法表明该运算符做了什么，因此最好定义一个具有说明性名称的类方法，例如 `swap()`。

## 更多重载运算符

还有一些其他操作对 Time 类也有意义。例如，你可能想从一个时间中减去另一个时间，或将一个时间乘以一个因子。这意味着需要重载减法和乘法运算符。其技术与加法运算符相同：创建 `operator-()` 和 `operator*()` 方法。也就是说，将下列原型添加到类声明中：

```cpp
Time operator-(const Time & t) const;
Time operator*(double n) const;
```

程序清单 11.7 展示了新的头文件。

### 程序清单 11.7 mytime2.h

```cpp
// mytime2.h -- Time class after operator overloading
#ifndef MYTIME2_H
#define MYTIME2_H

class Time
{
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
    void Show() const;
};
#endif
```

然后，将新方法的定义添加到实现文件中，如程序清单 11.8 所示。

### 程序清单 11.8 mytime2.cpp

```cpp
// mytime2.cpp -- implementing Time methods
#include <iostream>
#include "mytime2.h"

Time::Time()
{
    hours = minutes = 0;
}

Time::Time(int h, int m)
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

void Time::AddHr(int h)
{
    hours += h;
}

void Time::Reset(int h, int m)
{
    hours = h;
    minutes = m;
}

Time Time::operator+(const Time & t) const
{
    Time sum;
    sum.minutes = minutes + t.minutes;
    sum.hours = hours + t.hours + sum.minutes / 60;
    sum.minutes %= 60;
    return sum;
}

Time Time::operator-(const Time & t) const
{
    Time diff;
    int tot1, tot2;
    tot1 = t.minutes + 60 * t.hours;
    tot2 = minutes + 60 * hours;
    diff.minutes = (tot2 - tot1) % 60;
    diff.hours = (tot2 - tot1) / 60;
    return diff;
}

Time Time::operator*(double mult) const
{
    Time result;
    long totalminutes = hours * mult * 60 + minutes * mult;
    result.hours = totalminutes / 60;
    result.minutes = totalminutes % 60;
    return result;
}

void Time::Show() const
{
    std::cout << hours << " hours, " << minutes << " minutes";
}
```

完成这些修改后，可以使用程序清单 11.9 中所示的代码测试这些新定义。

### 程序清单 11.9 usetime2.cpp

```cpp
// usetime2.cpp -- using the third draft of the Time class
// compile usetime2.cpp and mytime2.cpp together
#include <iostream>
#include "mytime2.h"

int main()
{
    using std::cout;
    using std::endl;
    Time weeding(4, 35);
    Time waxing(2, 47);
    Time total;
    Time diff;
    Time adjusted;

    cout << "weeding time = ";
    weeding.Show();
    cout << endl;

    cout << "waxing time = ";
    waxing.Show();
    cout << endl;

    cout << "total work time = ";
    total = weeding + waxing;   // use operator+()
    total.Show();
    cout << endl;

    diff = weeding - waxing;    // use operator-()
    cout << "weeding time - waxing time = ";
    diff.Show();
    cout << endl;

    adjusted = total * 1.5;     // use operator*()
    cout << "adjusted work time = ";
    adjusted.Show();
    cout << endl;

    return 0;
}
```

程序清单 11.7、11.8 和 11.9 中程序的输出如下：

```text
weeding time = 4 hours, 35 minutes
waxing time = 2 hours, 47 minutes
total work time = 7 hours, 22 minutes
weeding time - waxing time = 1 hours, 48 minutes
adjusted work time = 11 hours, 3 minutes
```

## 引入友元

如你所见，C++ 控制对类对象私有部分的访问。通常，公有类方法是唯一的访问途径，但有时这种限制过于严格，不适合特定的编程问题。在这种情况下，C++ 提供了另一种访问形式：*友元*。友元有三种：

- 友元函数
- 友元类
- 友元成员函数

通过让一个函数成为某个类的友元，你允许该函数拥有与该类成员函数相同的访问权限。现在我们将研究友元函数，而将另外两种留到第 15 章“友元、异常及其他”中讨论。

在了解如何创建友元之前，我们先来看看为什么可能需要友元。通常，为类重载二元运算符（即带有两个参数的运算符）会产生对友元的需求。将一个 Time 对象乘以一个实数恰好提供了这样一种情形，因此我们来研究该案例。

在前面的 Time 类示例中，重载的乘法运算符与其他两个重载运算符不同，因为它组合了两种不同的类型。也就是说，加法和减法运算符各自组合两个 Time 值，而乘法运算符将一个 Time 值与一个 double 值组合。这限制了该运算符的使用方式。记住，左操作数是调用对象。也就是说，

```cpp
A = B * 2.75;
```

会转换为以下成员函数调用：

```cpp
A = B.operator*(2.75);
```

但下面这条语句呢？

```cpp
A = 2.75 * B;    // cannot correspond to a member function
```

从概念上讲，2.75 * B 应该与 B * 2.75 相同，但第一个表达式无法对应于成员函数，因为 2.75 不是 Time 类型的对象。记住，左操作数是调用对象，但 2.75 不是对象。因此编译器无法将该表达式替换为成员函数调用。

```cpp
result.minutes = totalminutes % 60;
return result;
}
```

有了这个声明和定义，语句

```cpp
A = 2.75 * B;
```

会转换为以下内容，并调用刚刚定义的非成员友元函数：

```cpp
A = operator*(2.75, B);
```

简而言之，类的友元函数是一个非成员函数，它具有与成员函数相同的访问权限。

### 友元是否违背 OOP？

乍一看，友元似乎违背了 OOP 的数据隐藏原则，因为友元机制允许非成员函数访问私有数据。然而，这是一种过于狭隘的观点。相反，你应该将友元函数视为类的扩展接口的一部分。例如，从概念上看，将一个 `double` 乘以一个 `Time` 值，与将一个 `Time` 值乘以一个 `double` 几乎相同。前者需要友元函数，而后者可以用成员函数完成，这是 C++ 语法的结果，而不是深刻的概念差异。通过同时使用友元函数和类方法，你可以用相同的用户界面表达任一操作。还要记住，只有类声明才能决定哪些函数是友元，因此类声明仍然控制着哪些函数可以访问私有数据。简而言之，类方法和友元只是表达类接口的两种不同机制。

实际上，你可以通过修改定义，使乘法中哪个值在前发生交换，从而将这个特定的友元函数写成非友元函数：

```cpp
Time operator*(double m, const Time & t)
{
    return t * m;    // use t.operator*(m)
}
```

原始版本显式访问了 `t.minutes` 和 `t.hours`，因此它必须是一个友元。这个版本只将 `Time` 对象 `t` 作为一个整体使用，让成员函数处理私有值，因此这个版本不必是友元。尽管如此，仍有理由将这个版本也设为友元。最重要的是，它将该函数作为正式类接口的一部分绑定进来。其次，如果你后来发现该函数需要直接访问私有数据，只需修改函数定义，而不必修改类原型。

### 提示

如果你想为类重载一个运算符，并且希望将该运算符与非类项作为第一个操作数一起使用，可以使用友元函数来反转操作数顺序。
