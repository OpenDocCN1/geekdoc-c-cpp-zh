
`myCat = 19.6;` // 如果 `Stonew` (double) 被声明为 `explicit`，则无效

`mycat = Stonew(19.6);` // 好的，一个显式转换

`mycat = (Stonew) 19.6;` // 好的，显式类型转换的老形式

# 注意

一个包含一个参数的 C++ 构造函数定义了从参数到类类型的转换。如果该构造函数带有 `explicit` 关键字，则它仅用于显式转换；否则，用于隐式转换。

编译器何时使用 `Stonew(double)` 函数？如果在声明中使用了 `explicit` 关键字，它仅用于显式类型转换；否则，也用于隐式转换：

- 当你初始化一个 `Stonew` 对象为双 `double` 值时
- 当将 `double` 值赋值给 `Stonew` 对象时
- 当将 `double` 值传递给期望 `Stonew` 参数的函数时
- 当函数返回 `Stonew` 值时

让我们详细看看在上述任何一种情况下，如果内置类型无法转换为 `double`，构造函数匹配过程都会让 `Stonew(double)` 构造函数作为其他类型的转换。也就是说，以下语句通过将 `int` 转换为 `double` 并使用 `Stonew(double)` 构造函数来工作：

```cpp
Stonew Jumbo(7); // 使用 Stonew(double), 将 int 转换为 double
```

然而，这种两步转换只有在选择唯一的情况下才有效。也就是说，如果类还定义了 `Stonew(long)` 构造函数，编译器将拒绝这些语句，因为 `int` 可以转换为 `long` 或 `double`，所以调用是歧义的。列表11.18 使用构造函数初始化 `Stonew` 对象并处理类型转换。确保编译列表11.17 以及列表11.18。

# 列表 11.18 stone.cpp

```cpp
// stone.cpp -- 用户定义的转换
// 使用 stonew.cpp
#include <iostream>
using std::cout;
#include "stonew.h"
void display(const Stonew & st, int n);
int main()
{
    Stonew incognito = 275; // 使用构造函数初始化
    Stonew wolfe(285.7); // 等于 wolfe = 285.7;
    Stonew taft(2, 8);
    cout << "The celebrity weighed ";
    incognito.show_stn();
    cout << "The detective weighed ";
    wolfe.show_stn();
    cout << "The President weighed ";
    taft.show_lbs();
    incognito = 276.8; // 使用构造函数进行转换
    taft = 325; // 等于 Stonew(325)
    cout << "The celebrity weighed ";
    incognito.show_stn();
    cout << "The President weighed ";
    taft.show_lbs();
    display(taft, 2);
    cout << "The wrestler weighed more.\n";
    display(422, 2);
    cout << "No stone left\n";
    return 0;
}
void display(const Stonew & st, int n)
{
    for (int i = 0; i < n; i++)
    {
        cout << "Wow! ";
        st.show_stn();
    }
}
```

这是列表11.18中程序的输出：

The celebrity weighed 19 stone, 9 pounds
The detective weighed 20 stone, 5.7 pounds
The President weighed 30 pounds
After dinner, the celebrity weighed 19 stone, 10.8 pounds
After dinner, the President weighed 325 pounds
Wow! 23 stone, 3 pounds
Wow! 23 stone, 3 pounds
The wrestler weighed even more.
Wow! 30 stone, 2 pounds
Wow! 30 stone, 2 pounds
No stone left

## 程序说明

注意，当构造函数有一个参数时，你可以在初始化类对象时使用以下形式：

```cpp
// 使用带有一个参数的构造函数初始化类的语法
Stonew incognito = 275;
```

这等于之前显示的两种形式：

```cpp
// 初始化类对象的标准语法
Stonew incognito = 275;
Stonew incognito = Stonew(275);
```

然而，后两种形式也可以用于具有多个参数的构造函数。

接下来，注意列表11.18中的两个赋值：

```cpp
incognito = 276.8;
taft = 325;
```

这些赋值中的第一个使用带 `double` 类型参数的构造函数将 276.8 转换为 `Stonew` 值。这将 `incognito` 的 `pounds` 成员设置为 276.8。由于使用了构造函数，该赋值还设置了类的 `stone` 和 `pds_left`。第二个赋值将 `int` 类型值转换为 `double`，然后使用 `Stonew(double)` 在过程中设置所有三个成员值。

最后，注意以下函数调用：

```cpp
display(422, 2); // 将 double转换为 double，再转换为 Stonew
```

`display()` 的原型表明其第一个参数应该是 `Stonew` 对象。无论是 `Stonew &` 形式参数……面对一个 `int` 参数，编译器会寻找 `Stonew(int)` 构造函数来将 `int` 转换为所需的 `Stonew` 类型。如果没有找到该构造函数，编译器会寻找具有某种 `int` 可以转换的类型内置类型的构造函数。`Stonew(double)` 构造函数符合要求。编译器将 `int` 转换为 `double`，然后使用 `Stonew(double)` 将结果转换为 `Stonew` 对象。

# 转换函数

列表11.18 将数字转换为 `Stonew` 对象。你可以反过来做吗？也就是说，你可以将 `Stonew` 对象转换为 `double` 值，如下所示：

```cpp
Stonew wolfe (285.5);
double host = wolfe; // ?? 可能 ??
```

答案是你可以这样做——但不是通过使用构造函数。构造函数只提供将另一种类型转换为类。要反过来操作，你必须使用一种特殊形式的 C++ 运算符函数，称为转换函数。

# 类的 613 自动转换与类型转换

转换函数是用户定义的类型转换，你可以像使用类型转换符一样使用它们。例如，如果你定义了一个 `Stonew` 到 `double` 的转换函数，你可以使用以下转换：

```
Stonew(285.7);
double host = double(wolfe); // 语法 #1
double thinker = (double) wolfe; // 语法 #2
```

或者，你可以让编译器推断出：
`Stonew wells(20,3);`
`double star = wells;` // 隐式使用转换函数

编译器注意到右侧是 `Stonew` 类型而左侧是 `double` 类型，它会查找你是否定义了符合此描述的转换函数。（如果它找不到这样的定义，编译器将生成一条错误信息，说明它无法将 `Stonew` 赋值给 `double`。）

那么，如何创建转换函数呢？要转换类型 `typeName`，你使用如下形式的转换函数：
`operator typeName();`

注意以下几点：

- 转换函数必须是一个类方法。
- 转换函数不能指定返回类型。
- 转换函数不能有任何参数。

例如，一个转换类型 `double` 的函数原型将是：
`operator double();`

`typeName` 部分（在此处 `typeName` 是 `double`）告诉了要转换到的目标类型，因此不需要返回类型。类方法的这种特性意味着它由特定的类对象进行调用，并告诉了函数要转换哪个值。因此，该函数不需要参数。

要添加将 `stone_wt` 对象转换为 `int` 和 `double` 类型的函数，需要在类声明中添加以下原型：

```
operator int();
operator double();
```

列表 11.19 显示了修改后的类声明。

# 列表 11.19 stonew1.h

```
// stonew1.h 修改后的 Stonew 类定义
#ifndef STONEWT1_H_
#define STONEWT1_H_
class Stonew
{
private:
enum { Lbs_per_stn = 14 };      // 每英石 14 磅
int stone;                               // 整数石
double pds_left;                         // 小数磅
double pounds;                           // 磅的总重量
public:
Stonew(double lbs);                    // 从 double pounds 构造
Stonew(int stn, double lbs);           // 从 stone, lbs 构造
Stonew();                                // 默认构造函数
~Stonew();
void show_lbs(const) const;               // 以磅格式显示重量
void show_stn(const) const;               // 以石格式显示重量
// 转换函数
operator int() const;
operator double() const;
};
#endif
```

列表 11.20 显示了 11.18 的修改，包含了这两个转换函数的定义。请注意，每个函数都返回了预期的值，尽管没有声明返回类型。还要注意，`int` 转换是舍入到最近的整数而不是截断。例如，如果 `pounds` 是 114.4，那么 `pounds + 0.5` 是 114.9，而 `int (114.9)` 是 114。但如果 `pounds` 是 114.6，`pounds + 0.5` 是 115.1，而 `int (115.1)` 是 115。

# 列表 11.20 stonew1.cpp

```
// stonew1.cpp -- Stonew 类方法 + 转换函数
#include <iostream>
using std::cout;
#include "stonew1.h"
// 从 double 值构造 Stonew 对象
Stonew::Stonew(double lbs)
{
    stone = int(lbs) / Lbs_per_stn;      // 整数除法
    pds_left = int(lbs);
}
// 从 stone, lbs 构造 Stonew 对象
Stonew::Stonew(int stn, double lbs)
{
    stone = stn;
    pds_left = lbs;
}
// 默认构造函数
Stonew::Stonew()
{
    stone = 0;
    pds_left = 0;
}
// 析构函数
Stonew::~Stonew()
}
void Stonew::show_lbs(const) const
{
    cout << stone * Lbs_per_stn + pds_left << " pounds\n";
}
void Stonew::show_stn(const) const
{
    cout << stone << " stone " << pds_left / Lbs_per_stn << " lbs\n";
}
// 转换函数
int Stonew::operator int() const
{
    return int(stone * Lbs_per_stn + pds_left + 0.5);
}
double Stonew::operator double() const
{
    return stone * Lbs_per_stn + pds_left;
}
```

*(注：由于原文代码块在 11.20 处存在部分逻辑断层和重复，翻译时已根据上下文保持了代码结构的完整性。)*

## 第 11 章 类的操作

如果你确实需要进行转换，它允许以下操作：

```
int plb = poppins.Stone_to_Int();
```

## 注意事项

你应该谨慎地避免使用隐式转换函数。通常，一个只能显式调用的函数是最佳选择。

总结来说，C++ 为类提供了以下类型转换：

- 具有单个参数的类构造函数充当将参数类型的值转换为类类型的转换指令。例如，当你将一个 `int` 类型赋值给 `Stonew` 对象时，带有 `int` 类型参数的 `Stonew` 类构造函数会被调用。然而，在构造函数声明中使用 `explicit` 可以消除隐式转换，并仅允许显式转换。
- 一种称为转换函数的特殊类成员运算符函数，充当将类对象转换为某种其他类型的转换指令。该转换函数是类的成员函数，没有声明的返回类型，没有参数，并且通过 `operator typeName()` 调用，其中 `typeName` 是对象要转换到的类型。当你将类对象赋值给该类型的变量，或使用强制类型转换符转换为该类型时，该转换函数会被调用。

## 转换与友元

让我们开始为 `Stonew` 类添加内容。正如在 `Time` 类讨论中所提到的，你可以使用成员函数或友元函数来重载加法。（为了简化，假设没有定义 `operator double()` 的转换函数）。你可以使用以下成员函数实现加法：

```
Stonew::operator+(const Stonew & st) const
{
double pds = pounds + st.pounds;
Stonew sum(pds);
return sum;
}
```

或者你可以这样作为友元函数实现加法：

```
{
double pds = st1.pounds + st2.pounds;
Stonew sum(pds);
return sum;
}
```

记住，你可以提供方法定义或友元定义，但不能兼者。任一种形式都能让你执行以下操作：

## 类的自动转换与类型强制转换

```
Stonew jennySt(9, 12);
Stonew bennySt(12, 8);
Stonew total;
total = jennySt + bennySt;
```

考虑到给出的 `Stonew (double)` 构造函数，每种形式让你执行以下操作：

```
Stonew jennySt(9, 12);
double jennyD = 176.0;
Stonew total;
total = jennySt + jennyD;
```

但只有友元函数让你执行此操作：

```
Stonew jennySt(9, 12);
double bennyD = 146.0;
Stonew total;
total = pennyD + jennySt;
```

为了理解为什么，你可以将每个加法翻译为相应的函数调用。首先，

```
total = jennySt + bennySt;
```

在任何情况下，实际类型都与形式参数匹配。此外，`Stonew` 对象按要求调用了成员函数。

```
total = jennySt.operator+(bennySt); // 成员函数
total = operator+(jennySt, bennySt); // 友元函数
```

```
total = jennySt + jennyD;
```

```
total = jennySt.operator+(jennyD); // 成员函数
total = operator+(jennySt, jennyD); // 友元函数
```

再次，`Stonew` 对象按要求调用了成员函数。这次，在每个情况下，一个参数（`jennyD`）类型为 `double`，这会调用 `Stonew(double)` 构造函数将参数转换为 `Stonew` 对象。

顺便说一下，此时定义 `operator double()` 成员函数会产生混惑，因为这将产生另一种解释选项。编译器不是将 `jennyD` 转换为 `double` 并执行 `Stonew` 加法，而是将 `jennySt` 转换为 `double` 并执行 `double` 加法。过多的转换函数会导致歧义。

最后。

```
total = pennyD + jennySt;
变为
total = operator+(pennyD, jennySt); // 友元函数
```
