
这些规则是有意义的。例如，考虑拥有指向派生对象的基类引用产生。在这种情况下，你可以使用基类引用来调用派生类对象的基类方法。由于派生类继承了基类的方法和数据成员，这不会产生任何问题。现在考虑一下，如果可以将基类对象赋值给派生类引用会发生什么。派生类引用将能够对基类对象调用派生类方法，这可能会导致问题。例如，对 `TableTennisPlayer` 应用 `RatedPlayer::Rating()` 方法是没有意义的，因为 `TableTennisPlayer` 对象并没有评分。

基类引用和指针可以指向派生类对象，这一事实产生了一些后果。其之一是使用基类引用或指针参数定义的函数可以用于基类对象也可以用于派生类对象。例如：

```cpp
void Show(const TableTennisPlayer & rt)
{
	std::cout << "Name: " << rt.Name();
	std::cout << "Table: ";
	if (rt.HasTable())
		std::cout << "yes\n";
	else
		std::cout << "no\n";
}
```

形式参数 `rt` 是指向基类的引用，因此它可以指向基类对象或派生类对象。因此，你可以对 `TableTennisPlayer` 或 `RatedPlayer` 类型的参数使用 `Show()` 函数：

```cpp
TableTennisPlayer player1("Tara", "Boom", false);
RatedPlayer player2("Mallory", "Duck", true);
Show(player1); // 对 TableTennisPlayer 参数有效
Show(player2); // 对 RatedPlayer 参数有效
```

对于指向基类的指针形式参数，也具有类似的关系；它可以使用基类对象的地址或派生类对象的地址作为参数：

```cpp
void Show(const TableTennisPlayer * pt); // 使用指针参数的函数
TableTennisPlayer player1("Tara", "Boom", false);
RatedPlayer player2("Mallory", "Duck", true);
Show(&player1); // 对 TableTennisPlayer * 参数有效
Show(&player2); // 对 RatedPlayer * 参数有效
```

引用兼容性还允许你无意中从派生类对象初始化基类对象。假设你有以下代码：

```cpp
RatedPlayer player1("Olaf", "Loaf", true);
TableTennisPlayer player2(player1);
```

初始化 `player2` 的精确匹配将是一个原型如下的构造函数：

```cpp
TableTennisPlayer(const RatedPlayer &); // 不存在
```

类定义没有包含此构造函数，但存在一个隐式拷贝构造函数：

```cpp
// 隐式拷贝构造函数
TableTennisPlayer(const TableTennisPlayer &);
```

形式参数是基类型的引用，因此它可以指向派生类型。因此，使用此构造函数将 `player2` 初始化为 `player1` 会拷贝 `firstname`、`lastname` 和 `hasTable` 成员。换句话说，它将 `player2` 初始化为 `RatedPlayer` 对象中嵌入的 `TableTennisPlayer` 对象。同样，你可以将派生类对象赋值给基类：

```cpp
RatedPlayer player1("Olaf", "Loaf", true);
TableTennisPlayer winner;
winner = player1; // 将派生类赋值给基类对象
```

在这种情况下，程序使用了隐式的重载赋值运算符：

```cpp
TableTennisPlayer &operator=(const TableTennisPlayer&) const;
```

## 继承：“是”的关系

基类引用和指针可以指向派生类对象，这一事实产生了一些后果……（此处省略原文中重复的段落，直接进入新主题）

为了澄清“是”的关系，让我们来看一些不符合模型的例子。公共继承并不建模“拥有”关系。例如，午餐可能包含水果。但通常情况下，午餐并不是水果。因此，你不应该通过从 `Fruit` 类派生 `Lunch` 类来尝试将水果放入午餐。处理放入水果的正确方法将其视为“拥有”关系：午餐拥有水果。

![](img/cd111a87c1db9aff4db4b18834327463_735_0.png)

图 13.3 “是”和“拥有”关系。

公共继承并不建模“像”的关系——也就是说，它不代表微笑。有人指出律师像鲨鱼。但从字面上讲，律师并不是鲨鱼。因此，你不应该从 `Shark` 类派生 `Lawyer` 类。

## 第13 章 类继承

公共继承并不建模“实现为”的关系。例如，你可以使用数组来实现栈。然而，从 `Array` 类派生 `Stack` 类是不妥妥的。栈并不是数组。例如，栈可以通过其他方式实现，例如链表。一种正确的方法是通过给栈提供一个私有的 `Array` 对象来隐藏数组实现。

## 多态公继承 723

- 从账户中取钱
- 显示账户信息

对于 Brass Plus 支票账户计划，Pontoon 国家银行希望拥有 Brass 账户的所有功能，以及以下额外信息项：

- 透支保护的上限
- 透支贷款的收取的利率
- 当前欠银行的透支金额

不需要额外的操作，但有两个操作需要以不同的实现：

- 取钱操作必须为 Brass Plus 账户整合透支保护
- 显示操作必须显示 Brass Plus 账户所需的额外信息

假设你调用第一个类为 Brass，第二个类为 BrassPlus。你应该将 BrassPlus 公地派自 Brass 吗？要回答这个问题，首先回答：BrassPlus 类是否满足“是一个”（is-a）测试？任何是 Brass 对象的东西对于 BrassPlus 对象来说都成立。存储一个客户名称、账号号码和余额。对于这两者，你都可以进行存款、取款和显示账户信息。请注意，“是一个”关系通常不是对称的。水果，通常来说不是香蕉；同样，一个 Brass 对象并不具备一个 BrassPlus 对象的所有能力。

## 开发 Brass 和 BrassPlus 类

Brass 账户类的信息非常直接，但银行还没有告诉你足够关于透支系统如何运作的细节。针对你对进一步信息的请求，友好的 Pontoon 国家银行代表告知你以下内容：

- Brass Plus 账户限制了银行借给你以覆盖透支的金额。默认值为 $500，但某些客户可能从不同的限额开始。
- 银行可能会更改客户的透支限额。
- Brass Plus 账户对贷款收取利。默认值为 11.125%，但某些客户可能从不同的费率开始。
- 银行可能会更改客户的利率。
- 账户记录客户欠银行的金额（透支贷款加利息）。用户无法通过从另一个账户转账的常规存款来偿还这笔金额。相反，他或她必须向特定的银行官员支付现金，该官员在必要时会寻找客户。当债务被偿还后，账户可以将欠款金额重置为 0。

最后一个功能是银行业务的一种不寻常方式，但它具有幸运的副作用，即让编程问题保持简单。这表明新的类构造函数应该提供账户信息，并包含一个默认值为 $500 的债务限制以及一个默认值为 10% 的利率。此外，还应该有重置债务限制、利率和当前债务的方法。这些都将添加到 Brass 类中，并将在 BrassPlus 声明中声明。

这两个类之间的信息表明，类声明可能如列表 13.7 所示。

### 列表 13.7 brass.h

```cpp
// brass.h -- 银行账户类
#ifndef BRASS_H_
#define BRASS_H_
#include <string>
// Brass 账户类
class Brass {
private:
    std::string fullName;
    long acctNum;
    double balance;
public:
    Brass(const std::string& s = "Nullbody", long an = -1,
         double bal = 0.0);
    void Deposit(double amt);
    virtual void Withdraw(double amt);
    double Balance() const;
    virtual void ViewAcct() const;
    virtual ~Brass() {}
};
// BrassPlus 账户类
class BrassPlus : public Brass {
private:
    double maxLoan;
    double rate;
    double owesBank;
public:
    BrassPlus(const std::string& s = "Nullbody", long an = -1,
         double bal = 0.0, double ml = 500,
```

## 多态公继承 725

```cpp
double r = 0.11125;
BrassPlus(const Brass &ba, double ml = 500,
double r = 0.11125);
virtual void ViewAcct();
virtual void Withdraw(double amt);
void ResetMax(double m) { maxLoan = m; }
void ResetRate(double r) { rate = r; }
void ResetOwes() { owesBank = 0; }
#endif
```

列表 13.7 中有几点需要注意：

- Brass 类为类添加了三个新的私有数据成员和三个新的公共成员函数。
- Brass 类和 BrassPlus 类都声明了 `ViewAcct()` 和 `Withdraw()` 方法；这些方法对于 BrassPlus 对象的行为与对于 Brass 对象的不同。
- Brass 类在使用新的 `virtual` 关键字在声明 `ViewAcct()` 和 `Withdraw()` 时。这些方法现在被称为虚方法。
- Brass 类声明了虚析构函数，尽管该析构函数什么都没做。

列表中的第一点是接下来的。RatedClass 在为 `TableTennisPlayer` 类添加一个新数据成员和两个新方法时也做过类似的事情。列表中的第二点是声明如何指定哪些方法在派生类中将有不同的行为。两个 `ViewAcct()` 原型表明将有两个独立的方法。基类版本的限定名称为 `Brass::ViewAcct()`，而派生类版本的限定名称为 `BrassPlus::ViewAcct()`。程序将使用对象类型来决定使用哪个版本。

```cpp
Brass dom("Dominic", 11224, 4183.45);
BrassPlus dot("Dorothy Banker", 12118, 2500);
```

## 多态公继承

## 类实现

下一步是准备类的实现。这部分工作已经在头文件中的内联函数定义中完成。列表 13.8 提供了剩余的方法定义。注意，`virtual` 关键字仅在类声明中的方法原型中使用，而没有在列表 13.8 的方法定义中使用。

*列表 13.8 `brass.cpp`*

```cpp
// brass.cpp -- 银行账户类方法
#include <iostream>
#include "brass.h"
using std::cout;
using std::endl;
using std::string;
// 格式处理
typedef std::ios_base::fmtflags format;
typedef std::streamsize precision;
format setFormat();
void restore(format f, precis p);
```

```cpp
// Brass 方法
Brass::Brass(const string & s, long an, double bal)
{
    fullName = s;
    acctNum = an;
    balance = bal;
}
```

```cpp
void Brass::Deposit(double amt)
{
    if (amt < 0)
        cout << "Negative deposit not allowed; "
             << "deposit is cancelled.\n";
    else
        balance += amt;
}
```

```cpp
void Brass::Withdrawal(double amt)
{
    // 设置 ###.## 格式
    format initialState = setFormat();
    precis prec = cout.precision(2);
    if (amt < 0)
        cout << "Withdrawal amount must be positive; "
             << "withdrawal canceled.\n";
    else if (amt <= balance)
        balance = amt;
    else
        cout << "Withdrawal amount of $" << amt
             << " exceeds your balance.\n"
             << "Withdrawal canceled.\n";
    restore(initialState, prec);
}
```

```cpp
double Brass::Balance() const
{
    return balance;
}
void Brass::ViewAcct() const
{
    // 设置 ###.### 格式
    format initialState = setFormat();
    precis prec = cout.precision(2);
    cout << "Client: " << fullName << endl;
    cout << "Account Number: " << acctNum << endl;
    cout << "Balance: $" << balance << endl;
    restore(initialState, prec); // 还原原始格式
}
```

```cpp
// BrassPlus 方法
BrassPlus::BrassPlus(const string & s, long an, double bal,
    double ml, double r) : Brass(s, an, bal)
{
    maxLoan = ml;
    owesBank = 0.0;
    rate = r;
}
```

```cpp
BrassPlus::BrassPlus(const Brass & ba, double ml, double r)
{
    Brass(ba) // 使用隐式拷贝构造函数
    maxLoan = ml;
    owesBank = 0.0;
    rate = r;
}
```

```cpp
// 重新定义 ViewAcct()的行为
void BrassPlus::ViewAcct() const
{
    // 设置 ###.### 格式
    format initialState = setFormat();
    precis prec = cout.precision(2);
    Brass::ViewAcct(); // 显示基类部分
    cout << "Maximum loan: $" << maxLoan << endl;
    cout << "Owed to bank: $" << owesBank << endl;
    cout << "Loan Rate: " << rate << "\n";
}
```

```cpp
// 重新定义 Withdraw()的行为
void BrassPlus::Withdraw(double amt)
{
    // 设置 ###.### 格式
    format initialState = setFormat();
    precis prec = cout.precision(2);
    double bal = Balance();
    if (amt <= bal)
        Brass::Withdraw(amt);
    else if (amt <= bal + maxLoan - owesBank)
    {
        double advance = amt - bal;
        owesBank += advance * (1.0 + rate);
        cout << "Bank advance: $" << advance << endl;
    }
    else
        cout << "Credit limit exceeded. Transaction cancelled.\n";
    restore(initialState, prec);
}
```
