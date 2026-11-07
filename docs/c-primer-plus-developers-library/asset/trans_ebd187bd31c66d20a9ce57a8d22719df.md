
然而，类型意味着程序在销毁 `sum` 之前构造它的一个副本，而调用函数得到的是该副本。

> **注意**
> 
> 不要返回对局部变量或其他临时对象的引用。当函数终止且局部变量或临时对象消失时，该引用就会变成对不存在数据的引用。

最后，程序清单11.3测试Time类的时间求和部分。

### 程序清单11.3 `usetime0.cpp`

```cpp
// usetime0.cpp -- using the first draft of the Time class
// compile usetime0.cpp and mytime0.cpp together
#include <iostream>
#include "mytime0.h"

int main()
{
    using std::cout;
    using std::endl;
    Time planning;
    Time coding(2, 40);
    Time fixing(5, 55);
    Time total;

    cout << "planning time = ";
    planning.Show();
    cout << endl;

    cout << "coding time = ";
    coding.Show();
    cout << endl;

    cout << "fixing time = ";
    fixing.Show();
    cout << endl;

    total = coding.Sum(fixing);
    cout << "coding.Sum(fixing) = ";
    total.Show();
    cout << endl;

    return 0;
}
```

以下是程序清单11.1、11.2和11.3中程序的输出：

```text
planning time = 0 hours, 0 minutes
coding time = 2 hours, 40 minutes
fixing time = 5 hours, 55 minutes
coding.Sum(fixing) = 8 hours, 35 minutes
```

## 添加加法运算符

将Time类改为使用重载加法运算符很简单。只需将Sum()的名称改为看起来奇怪的名称operator+()。没错：只需将运算符符号（本例中为+）追加到operator末尾，并将结果用作方法名。这是标识符名称中可以使用字母、数字或下划线以外字符的一个地方。程序清单11.4和11.5反映了这一小改动。

### 程序清单11.4 `mytime1.h`

```cpp
// mytime1.h -- Time class before operator overloading
#ifndef MYTIME1_H_
#define MYTIME1_H_

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
    void Show() const;
};
#endif
```

### 程序清单11.5 `mytime1.cpp`

```cpp
// mytime1.cpp -- implementing Time methods
#include <iostream>
#include "mytime1.h"

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

void Time::Show() const
{
    std::cout << hours << " hours, " << minutes << " minutes";
}
```

与Sum()一样，operator+()由Time对象调用，接受第二个Time对象作为参数，并返回一个Time对象。因此，可以使用与Sum()相同的语法调用operator+()方法：

```cpp
total = coding.operator+(fixing);    // function notation
```

但是，将方法命名为`operator+()`还允许你使用运算符表示法：

```cpp
total = coding + fixing;        // operator notation
```

两种表示法都会调用`operator+()`方法。注意，使用运算符表示法时，运算符左侧的对象（本例中为coding）是调用对象，而右侧的对象（本例中为fixing）是作为参数传递的对象。程序清单11.6说明了这一点。

### 程序清单11.6 `usetime1.cpp`

```cpp
// usetime1.cpp -- using the second draft of the Time class
// compile usetime1.cpp and mytime1.cpp together
#include <iostream>
#include "mytime1.h"

int main()
{
    using std::cout;
    using std::endl;
    Time planning;
    Time coding(2, 40);
    Time fixing(5, 55);
    Time total;

    cout << "planning time = ";
    planning.Show();
    cout << endl;

    cout << "coding time = ";
    coding.Show();
    cout << endl;

    cout << "fixing time = ";
    fixing.Show();
    cout << endl;

    total = coding + fixing;
    // operator notation
    cout << "coding + fixing = ";
    total.Show();
    cout << endl;

    Time morefixing(3, 28);
    cout << "more fixing time = ";
    morefixing.Show();
    cout << endl;
    total = morefixing.operator+(total);
    // function notation
    cout << "morefixing.operator+(total) = ";
    total.Show();
    cout << endl;

    return 0;
}
```

以下是程序清单11.4、11.5和11.6中程序的输出：

```text
planning time = 0 hours, 0 minutes
coding time = 2 hours, 40 minutes
fixing time = 5 hours, 55 minutes
coding + fixing = 8 hours, 35 minutes
more fixing time = 3 hours, 28 minutes
morefixing.operator+(total) = 12 hours, 3 minutes
```

简而言之，`operator+()`函数的名称允许使用函数表示法或运算符表示法来调用它。编译器使用操作数类型来确定要做什么：

```cpp
int a, b, c;
Time A, B, C;
c = a + b;       // use int addition
C = A + B;       // use addition as defined for Time objects
```

能相加多于两个对象吗？例如，如果`t1`、`t2`、`t3`和`t4`都是Time对象，可以执行以下操作吗？

```cpp
t4 = t1 + t2 + t3;                    // valid?
```

回答这个问题的方法是考虑该语句如何转换为函数调用。因为加法是从左到右的运算符，所以该语句首先转换为：

```cpp
t4 = t1.operator+(t2 + t3);             // valid?
```

然后，函数参数本身又被转换为函数调用，如下所示：

```cpp
t4 = t1.operator+(t2.operator+(t3));   // valid? YES
```

这有效吗？是的，有效。函数调用`t2.operator+(t3)`返回一个Time对象，表示`t2`和`t3`的和。然后这个对象成为`t1.operator+()`函数调用的对象，该调用返回`t1`与表示`t2`和`t3`之和的Time对象之和。简而言之，最终返回值是`t1`、`t2`和`t3`的和，正如所愿。

## 重载限制

大多数C++运算符（见表11.1）可以按照上一节所述的方式进行重载。重载运算符（有一些例外）不一定必须是成员函数。但是，至少有一个操作数必须是用户定义的类型。让我们更仔细地看看C++对用户定义运算符重载施加的限制：

- 重载运算符必须至少有一个操作数是用户定义的类型。这可以防止你为标准类型重载运算符。因此，不能重新定义减号运算符（`-`），使其产生两个double值之和而不是它们的差。这一限制保持了程序的健全性，尽管它可能会妨碍创造性会计。
- 不能以违反原运算符语法规则的方式使用运算符。例如，不能重载求模运算符（`%`），使其可用于单个操作数：

```cpp
int x;
Time shiva;
% x;      // invalid for modulus operator
% shiva;  // invalid for overloaded operator
```

同样，不能改变运算符优先级。因此，如果重载加法运算符以便将两个类相加，新运算符具有与普通加法相同的优先级。

- 不能创建新的运算符符号。例如，不能定义`operator**()`函数来表示求幂。
- 不能重载以下运算符：

| 运算符 | 描述 |
|---|---|
| `sizeof` | sizeof运算符 |
| `.` | 成员运算符 |
| `.*` | 指向成员的指针运算符 |
| `::` | 作用域解析运算符 |
| `?:` | 条件运算符 |
| `typeid` | RTTI运算符 |
| `const_cast` | 类型转换运算符 |
| `dynamic_cast` | 类型转换运算符 |
| `reinterpret_cast` | 类型转换运算符 |
| `static_cast` | 类型转换运算符 |

这仍然使表11.1中的所有运算符可用于重载。
