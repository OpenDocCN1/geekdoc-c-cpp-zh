
`Brass` 类设计使得 `Deposit()` 和 `Withdraw()` 接口成为修改 `balance` 的唯一手段。`Reset()` 方法对于 `BrassPlus` 对象而言，本质上使 `balance` 变成了一个公共变量，忽略了 `Withdraw()` 中的保护措施。

> **注意**
对于类数据成员，你应该优先使用私有（private）而非保护（protected）访问控制，你应该使用基类方法为派生类提供基类数据。

然而，保护访问控制对于成员函数可能非常有用，它允许派生类访问无法公开的内部函数。

# 抽象基类

你已经看到了简单的继承和更复杂的多态继承。增加复杂性的下一步是抽象基类（ABC）。让我们来看一些为 ABC 提供背景的编程场景。

有时，应用“是一个（is-a）”规则并不像表面上看起来那么简单。例如，假设你正在开发一个图形程序，该程序应该代表圆和椭圆等。圆是椭圆的一种特殊情况：它是长轴等于短轴的椭圆。因此，所有的圆都是椭圆，从 `Ellipse` 类派生出一个 `Circle` 类似乎是很有诱惑力的。但当你涉及到细节时，你可能会发现问题。

为了理解这一点，首先考虑你可能作为 `Ellipse` 类的一部分包含的内容。数据成员可以包括椭圆圆心的坐标、长轴（直径的一半）、短轴（短直径的一半）以及一个从水平坐标轴到长轴的方位方向角。此外，该类还可以包含移动椭圆、返回椭圆面积、旋转椭圆以及缩放长轴和短轴的方法：

```cpp
class Ellipse
{
private:
    double x;      // 椭圆中心的 x 坐标
    double y;      // 椭圆中心的 y 坐标
    double a;      // 长轴
    double b;      // 短轴
    double angle; // 以度为单位的方位角
```

```cpp
public:
    void Move(int nx, int ny) { x = nx; y = ny; }
    virtual double Area() const { return 3.14159 * a * b; }
    virtual void Rotate(double angle) { angle += angle; }
    virtual void Scale(double sa, double sb) { a *= sa; b *= sb; }
```

现在你从 `Ellipse` 类派生出一个 `Circle` 类：

```cpp
class Circle : public Ellipse
{
};
```

虽然圆是椭圆，但这种派生关系很笨拙。例如，圆只需要一个值（半径）来描述其尺寸和形状，而不是拥有长轴（a）和短轴（b）。`Circle` 构造函数可以通过给 `a` 和 `b` 成员分配相同的值来处理，但这样就会对相同信息产生冗余表示。`angle` 参数和 `Rotate()` 方法对圆来说没有意义，而 `Scale()` 方法按目前的设计，可以通过不同地缩放两个轴来将圆变成非圆。你可以尝试用技巧来修复这些，例如在 `Circle` 类的私有部分放置一个重新定义的 `Rotate()` 方法，以便：

```cpp
class BaseEllipse            // 抽象基类
{
private:
    double x;                   // 中心 x 坐标
    double y;                   // 中心 y 坐标
    ...
public:
    BaseEllipse(double x0, double y0 = 0) : x(x0),y(y0) {}
    virtual ~BaseEllipse() {};
    void Move(int nx, int ny) { x = nx; y = ny; }
    virtual double Area() const = 0; // 一个纯虚函数
    ...
```

## 抽象基类

当类声明包含一个虚函数时，你就无法创建该类的对象。其想法是，带有纯虚函数的类仅为了作为基类而存在。对于一个类要成为真正的 ABC，它必须至少有一个纯虚函数。原型中的 `= 0` 使得虚函数变成纯虚函数。在没有定义的 `Area()` 方法的类中，C++ 甚至允许纯虚函数也有定义。也许所有的基类方法都像 `Move()` 一样，它们可以在基类中定义，但你仍然需要将它们变为抽象。你可以让原型变为虚：

```cpp
void Move(int nx, int ny) = 0;
```

这使得基类成为抽象类。但你仍然可以在实现文件中提供定义：

```cpp
void BaseEllipse::Move(int nx, int ny) { x = nx; y = ny; }
```

简而言之，原型中的 `0` 表示该类是抽象基类，且该类并不一定实现该函数。

现在你可以从 `Ellipse` 类派生出 `Circle` 类，由于原型中的 `0` 表示该类是抽象基类，且该类并不一定实现该函数。需要注意的是，`Circle` 类总是表示圆，而 `Ellipse` 类表示椭圆。

使用 `EllipseEllipse` 对象的程序可以管理 `Ellipse` 数组，但无法创建 `Ellipse` 实例。

## 应用概念

你可能想看到 ABC 的完整示例，因此我们将该概念应用到表示 `BrassPlus` 账户，从一个名为 `ActABC` 的 ABC 开始。该类应该包含 `BrassPlus` 类共有的方法和数据。对于 `BrassPlus` 不同的方法应声明为虚函数。至少一个虚函数应该是纯虚函数，以便使 `ActABC` 类成为抽象类。为了方便派生类访问基类数据，`ActABC` 提供了一些保护方法。记住保护方法是派生类可以调用的，但不是派生类对象的公共接口的一部分。`ActABC` 还提供了一个处理格式的保护成员函数。

```cpp
//BrassPlus Account Class
class BrassPlus : public AcctABC
{
private:
    double maxLoan;
    double rate;
    double owesBank;
public:
    BrassPlus(const std::string & s = "Nullbody", long an = -1,
        double bal = 0.0, double ml = 500,
        double r = 0.10);
    BrassPlus(const Brass & ba, double ml = 500, double r = 0.1);
    virtual void getView()const;
    virtual void Withdraw(double amt);
    void ResetMax(double m) { maxLoan = m; }
    void ResetRate(double r) { rate = r; }
    void ResetOwes() { owesBank = 0; }
};
#endif
```

下一步是实现那些还没有内联定义的方法。列表 13.12 就实现了这些。

### 列表 13.12 acctabc.cpp

```cpp
// acctabc.cpp -- 银行账户类方法
#include <iostream>
#include "acctabc.h"
using std::cout;
using std::ios_base;
using std::endl;
using std::string;
// 抽象基类
AcctABC::AcctABC(const std::string & s, long an, double bal)
{
    fullName = s;
    acctNum = an;
    balance = bal;
}
void AcctABC::Deposit(double amt)
{
    if (amt < 0)
        cout << "不允许负存款; "
            << "存款已取消。\n";
else
    balance += amt;
}
```

```cpp
void AcctABC::Withdraw(double amt)
{
    balance -= amt;
}
```

```cpp
// 用于格式化的保护方法
AcctABC::Formatting AcctABC::SetFormat() const
{
    // 设置 ###.## 格式
    Formatting f;
    f.flag = cout.setf(ios_base::fixed, ios_base::floatfield);
    f.pr = cout.precision(2);
    return f;
}
```

```cpp
void AcctABC::Restore(Formatting & f) const
{
    cout.setf(f.flag, ios_base::floatfield);
    cout.precision(f.pr);
}
```

```cpp
void Brass::ViewAcct() const
{
    Formatting f = SetFormat();
    cout << "Brass Client: " << FullName() << endl;
    cout << "Account Number: " << AcctNum() << endl;
}
```

```cpp
cout << "Balance: " << Balance() << endl;
Restore(f);
}
```

```cpp
// BrassPlus 方法
BrassPlus::BrassPlus(const std::string & s, long an, double bal,
    double ml, double r) : AcctABC(s, an, bal)
{
    maxLoan = ml;
    owesBank = 0.0;
    rate = r;
}
```

```cpp
BrassPlus::BrassPlus(const Brass & ba, double ml, double r)
    : AcctABC(ba) // 使用隐式拷贝构造函数
{
    maxLoan = ml;
    owesBank = 0.0;
    rate = r;
}
```

```cpp
void BrassPlus::ViewAcct() const
{
    Formatting f = SetFormat();
    cout << "BrassPlus Client: " << FullName() << endl;
    cout << "Account Number: " << AcctNum() << endl;
    cout << "Balance: " << Balance() << endl;
    cout << "Maximum loan: " << maxLoan << endl;
    cout << "Owed to bank: " << owesBank << endl;
    cout.precision(3);
    cout << "Loan Rate: " << 100 * rate << "\n";
    Restore(f);
}
```

```cpp
void BrassPlus::Withdraw(double amt)
{
    Formatting f = SetFormat();
    double bal = Balance();
    if (amt <= bal)
        AcctABC::Withdraw(amt);
    else if (amt <= bal + maxLoan)
    {
        double advance = amt;
        owesBank += advance * (1.0 + rate);
        cout << "Bank advance: $" << advance << endl;
        cout << "Finance charge: $" << advance * rate << endl;
        AcctABC::Withdraw(amt);
    }
    else
    {
        cout << "Credit limit exceeded. Transaction cancelled.\n";
        Restore(f);
    }
}
```

# 第 13 章 类继承

`Name()` 和 `AcctNum()` 保护方法为 `fullName` 和 `acctNum` 成员提供了只读访问，并允许为每个派生类更独立地定制 `ViewAcct()`。此版本在格式化的实现上做了一些改进。之前的版本使用了两个函数调用来设置和恢复格式：

```cpp
format = setFormat();
cout.precision(2);
restore(initialState, prec); // 恢复原始格式
```

新版本定义了一个结构来存储格式化值，并使用该结构通过两次函数调用来设置和恢复格式：

```cpp
struct Formatting
{
    std::ios_base::fmt flag;
    std::streamsize pr;
};
Formatting f = SetFormat();
Restore(f);
```

`Name()` 和 `AcctNum()` 保护方法为 `fullName` 和 `acctNum` 成员提供了只读访问，并允许为每个派生类更独立地定制 `ViewAcct()`。此版本在格式化的实现上做了一些改进。之前的版本使用了两个函数调用来设置和恢复格式：

```cpp
format = setFormat();
cout.precision(2);
restore(initialState, prec); // 恢复原始格式
```

新版本定义了一个结构来存储格式化值，并使用该结构通过两次函数调用来设置和恢复格式：

```cpp
struct Formatting
{
    std::ios_base::fmt flag;
    std::streamsize pr;
};
Formatting f = SetFormat();
Restore(f);
```
