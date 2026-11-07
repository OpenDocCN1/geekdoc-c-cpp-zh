
-   从账户取款
-   显示账户信息

对于 Brass Plus 账户支票计划，Pontoon 国民银行希望具备 Brass 账户的所有功能，以及以下附加信息项：

-   透支保护的上限
-   对透支贷款收取的利率
-   当前欠银行的透支金额

不需要额外的操作，但有两个操作需要以不同方式实现：

-   取款操作必须为 Brass Plus 账户纳入透支保护
-   显示操作必须显示 Brass Plus 账户所需的附加信息

假设你将一个类称为 Brass，第二个类称为 BrassPlus。你应该从 Brass 公开派生 BrassPlus 吗？要回答这个问题，先回答另一个问题：BrassPlus 类是否满足 *is-a* 测试？当然满足。对 Brass 对象成立的一切都适用于 BrassPlus 对象。两者都存储客户姓名、账号和余额。使用两者都可以存款、取款并显示账户信息。注意，*is-a* 关系通常不是对称的。一般来说，水果不是香蕉；同样，Brass 对象不会具备 BrassPlus 对象的全部能力。

### 开发 Brass 和 BrassPlus 类

Brass 账户类的信息相当直接，但银行还没有告诉你关于透支系统如何运作的足够细节。在你请求提供更多信息后，友好的 Pontoon 国民银行代表告诉你以下内容：

-   Brass Plus 账户限制银行借给你用于弥补透支的金额。默认值为 $500，但某些客户可能以不同的限额开始。
-   银行可以更改客户的透支限额。
-   Brass Plus 账户对贷款收取利息。默认值为 11.125%，但某些客户可能以不同的利率开始。
-   银行可以更改客户的利率。
-   该账户跟踪客户欠银行多少钱（透支贷款加利息）。用户不能通过普通存款或从另一个账户转账来还清这笔金额。相反，他或她必须向一位专门的银行职员支付现金；必要时，该职员会找到该客户。债务还清后，账户可以将欠款金额重置为 0。

最后一项特性对银行开展业务来说是一种不寻常的方式，但它有一个幸运的副作用：使编程问题保持更简单。

这个列表表明，新类需要提供账户信息的构造函数，并且这些构造函数应包含默认值为 $500 的债务限额和默认值为 10% 的利率。还应该有用于重置债务限额、利率和当前债务的方法。这些都是要添加到 Brass 类中的内容，它们将在 BrassPlus 类声明中声明。

关于这两个类的信息表明，类声明应类似于清单 13.7 中的声明。

**清单 13.7 brass.h**

```cpp
// brass.h -- bank account classes
#ifndef BRASS_H_
#define BRASS_H_
#include <string>
// Brass Account Class
class Brass
{
private:
    std::string fullName;
    long acctNum;
    double balance;
public:
    Brass(const std::string & s = "Nullbody", long an = -1,
                double bal = 0.0);
    void Deposit(double amt);
    virtual void Withdraw(double amt);
    double Balance() const;
    virtual void ViewAcct() const;
    virtual ~Brass() {}
};

//Brass Plus Account Class
class BrassPlus : public Brass
{
private:
    double maxLoan;
    double rate;
    double owesBank;
public:
    BrassPlus(const std::string & s = "Nullbody", long an = -1,
                double bal = 0.0, double ml = 500,
                double r = 0.11125);
    BrassPlus(const Brass & ba, double ml = 500,
              double r = 0.11125);
    virtual void ViewAcct() const;
    virtual void Withdraw(double amt);
    void ResetMax(double m) { maxLoan = m; }
    void ResetRate(double r) { rate = r; }
    void ResetOwes() { owesBank = 0; }
};

#endif
```

在清单 13.7 中有几点需要注意：

-   BrassPlus 类向 Brass 类添加了三个新的私有数据成员和三个新的公有成员函数。
-   Brass 类和 BrassPlus 类都声明了 `ViewAcct()` 和 `Withdraw()` 方法；对于 BrassPlus 对象，这些方法的行为将与 Brass 对象不同。
-   Brass 类在声明 `ViewAcct()` 和 `Withdraw()` 时使用了新关键字 `virtual`。这些方法现在被称为 *虚方法*。
-   Brass 类还声明了一个虚析构函数，尽管该析构函数什么也不做。

列表中的第一点并不新鲜。RatedPlayer 类在向 TableTennisPlayer 类添加一个新数据成员和两个新方法时也做了类似的事情。列表中的第二点在于，这些声明如何指定方法对派生类有不同行为。两个 `ViewAcct()` 原型表明将有两个单独的方法定义。基类版本的限定名是 `Brass::ViewAcct()`，派生类版本的限定名是 `BrassPlus::ViewAcct()`。程序将使用对象类型来确定使用哪个版本：

```cpp
Brass dom("Dominic Banker", 11224, 4183.45);
BrassPlus dot("Dorothy Banker", 12118, 2592.00);
dom.ViewAcct();       // use Brass::ViewAcct()
dot.ViewAcct();       // use BrassPlus::ViewAcct()
```

同样，将有两个版本的 `Withdraw()`：一个供 Brass 对象使用，一个供 BrassPlus 对象使用。对两个类行为相同的方法（如 `Deposit()` 和 `Balance()`）只在基类中声明。第三点（`virtual` 的使用）比前两点更复杂。它决定当方法通过引用或指针而不是通过对象调用时使用哪个方法。如果不使用关键字 `virtual`，程序将根据引用类型或指针类型选择方法。如果确实使用关键字 `virtual`，

## 类实现

下一步是准备类实现。其中一部分已由头文件中的内联函数定义完成。清单 13.8 提供了其余的方法定义。注意，关键字 `virtual` 只用在类声明的方法原型中，而不用于清单 13.8 中的方法定义。

**清单 13.8 brass.cpp**

```cpp
// brass.cpp - bank account class methods
#include <iostream>
#include "brass.h"
using std::cout;
using std::endl;
using std::string;

// formatting stuff
typedef std::ios_base::fmtflags format;
typedef std::streamsize precis;
format setFormat();
void restore(format f, precis p);

// Brass methods

Brass::Brass(const string & s, long an, double bal)
{
        fullName = s;
        acctNum = an;
        balance = bal;
}

void Brass::Deposit(double amt)
{
        if (amt < 0)
                cout << "Negative deposit not allowed; "
                     << "deposit is cancelled.\n";
        else
                balance += amt;
}

void Brass::Withdraw(double amt)
{
        // set up ###.## format
        format initialState = setFormat();
        precis prec = cout.precision(2);

        if (amt < 0)
                cout << "Withdrawal amount must be positive; "
                     << "Withdrawal canceled.\n";
        else if (amt <= balance)
                balance -= amt;
        else
                cout << "Withdrawal amount of $" << amt
                     << " exceeds your balance.\n"
                     << "Withdrawal canceled.\n";
        restore(initialState, prec);
}
double Brass::Balance() const
{
        return balance;
}

void Brass::ViewAcct() const
{
        // set up ###.## format
        format initialState = setFormat();
        precis prec = cout.precision(2);
        cout << "Client: " << fullName << endl;
        cout << "Account Number: " << acctNum << endl;
        cout << "Balance: $" << balance << endl;
        restore(initialState, prec); // restore original format
}

// BrassPlus Methods
BrassPlus::BrassPlus(const string & s, long an, double bal,
                     double ml, double r) : Brass(s, an, bal)
{
        maxLoan = ml;
        owesBank = 0.0;
        rate = r;
}

BrassPlus::BrassPlus(const Brass & ba, double ml, double r)
        : Brass(ba)    // uses implicit copy constructor
{
        maxLoan = ml;
        owesBank = 0.0;
        rate = r;
}

// redefine how ViewAcct() works
void BrassPlus::ViewAcct() const
{
        // set up ###.## format
        format initialState = setFormat();
```
