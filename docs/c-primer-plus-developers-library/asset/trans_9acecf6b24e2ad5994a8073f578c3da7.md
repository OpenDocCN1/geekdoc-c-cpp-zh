
```cpp
    return s;                 // argument object
else
    return *this;            // invoking object
}
```

![](img/9afc44517b591d64e2e19f623c9308ef_555_0.png)

图10.3 使用成员函数访问两个对象。

这里 `s.total_val` 是作为实参传入的对象的总价值，而 `total_val` 是消息发送到的对象的总价值。如果 `s.total_val` 大于 `total_val`，函数返回 `s` 的引用。否则，它返回用于调用该方法的对象的引用。（用面向对象编程的话说，就是 `topval` 消息发送到的对象。）问题来了：那个对象该叫什么？如果你调用 `stock1.topval(stock2)`，那么 `s` 是 `stock2` 的引用（即 `stock2` 的别名），但 `stock1` 没有别名。

C++ 解决这个问题的方法是使用一个称为 `this` 的特殊指针。`this` 指针指向用于调用成员函数的对象。（基本上，它是作为隐藏参数传递给该方法的。）因此，函数调用 `stock1.topval(stock2)` 将 `this` 设置为 `stock1` 对象的地址，并使该指针可供 `topval()` 方法使用。类似地，函数调用 `stock2.topval(stock1)` 将 `this` 设置为 `stock2` 对象的地址。一般来说，所有类方法都有一个 `this` 指针，它被设置为调用该方法的对象的地址。实际上，`topval()` 中的 `total_val` 只是 `this->total_val` 的简写表示法。（回想第4章“复合类型”，你使用 `->` 运算符通过指针访问结构成员。类成员也是如此。）（见图10.4。）

![](img/9afc44517b591d64e2e19f623c9308ef_556_0.png)

图10.4 this 指向调用对象。

> **注意**
>
> 每个成员函数（包括构造函数和析构函数）都有一个 `this` 指针。`this` 指针的特殊之处在于它指向调用对象。如果某个方法需要将调用对象作为一个整体来引用，它可以使用表达式 `*this`。在函数参数括号后使用 `const` 限定符会将 `this` 限定为指向 `const` 的指针；在这种情况下，你不能使用 `this` 来改变对象的值。

然而，你想要返回的并不是 `this`，因为 `this` 是对象的地址。你想返回对象本身，而对象本身用 `*this` 表示。（回想一下，对指针应用解引用运算符 `*` 会得到该指针所指向的值。）现在你可以使用 `*this` 作为调用对象的别名来完成方法定义。

```cpp
const Stock & Stock::topval(const Stock & s) const
{
    if (s.total_val > total_val)
        return s;             // argument object
    else
        return *this;         // invoking object
}
```

返回类型是引用这一事实意味着返回的对象是调用对象本身，而不是通过返回机制传递的副本。清单10.7给出了新的头文件。

## 清单10.7 stock20.h

```cpp
// stock20.h -- augmented version
#ifndef STOCK20_H_
#define STOCK20_H_
#include <string>

class Stock
{
private:
    std::string company;
    int shares;
    double share_val;
    double total_val;
    void set_tot() { total_val = shares * share_val; }
public:
    Stock();              // default constructor
    Stock(const std::string & co, long n = 0, double pr = 0.0);
    ~Stock();             // do-nothing destructor
    void buy(long num, double price);
    void sell(long num, double price);
    void update(double price);
    void show()const;
    const Stock & topval(const Stock & s) const;
};

#endif
```

清单10.8给出了修订后的类方法文件。它包含了新的 `topval()` 方法。另外，既然你已经了解了构造函数和析构函数如何工作，清单10.8用静默版本替换了它们。

## 清单10.8 stock20.cpp

```cpp
// stock20.cpp -- augmented version
#include <iostream>
#include "stock20.h"

// constructors
Stock::Stock()        // default constructor
{
    company = "no name";
    shares = 0;
    share_val = 0.0;
    total_val = 0.0;
}

Stock::Stock(const std::string & co, long n, double pr)
{
    company = co;

    if (n < 0)
    {
        std::cout << "Number of shares can't be negative; "
                  << company << " shares set to 0.\n";
        shares = 0;
    }
    else
        shares = n;
    share_val = pr;
    set_tot();
}

// class destructor
Stock::~Stock()        // quiet class destructor
{
}

// other methods
void Stock::buy(long num, double price)
{
    if (num < 0)
    {
        std::cout << "Number of shares purchased can't be negative. "
                  << "Transaction is aborted.\n";
    }
    else
    {
        shares += num;
        share_val = price;
        set_tot();
    }
}

void Stock::sell(long num, double price)
{
    using std::cout;
    if (num < 0)
    {
        cout << "Number of shares sold can't be negative. "
             << "Transaction is aborted.\n";
    }
    else if (num > shares)
    {
        cout << "You can't sell more than you have! "
             << "Transaction is aborted.\n";
    }
    else
    {
        shares -= num;
        share_val = price;
        set_tot();
    }
}

void Stock::update(double price)
{
    share_val = price;
    set_tot();
}

void Stock::show() const
{
    using std::cout;
    using std::ios_base;
    // set format to #.###
    ios_base::fmtflags orig =
        cout.setf(ios_base::fixed, ios_base::floatfield);
    std::streamsize prec = cout.precision(3);

    cout << "Company: " << company
         << " Shares: " << shares << '\n';
    cout << " Share Price: $" << share_val;
    // set format to #.##
    cout.precision(2);
    cout << " Total Worth: $" << total_val << '\n';

    // restore original format
    cout.setf(orig, ios_base::floatfield);
    cout.precision(prec);
}

const Stock & Stock::topval(const Stock & s) const
{
    if (s.total_val > total_val)
```

值。如果类有多个构造函数，你可以为不同的元素使用不同的构造函数：

```cpp
const int STKS = 10;
Stock stocks[STKS] = {
    Stock("NanoSmart", 12.5, 20),
    Stock(),
    Stock("Monolithic Obelisks", 130, 3.25),
};
```

这会使用 Stock(const string & co, long n, double pr) 构造函数初始化 stocks[0] 和 stocks[2]，并使用 Stock() 构造函数初始化 stocks[1]。由于此声明只部分初始化了数组，其余七个成员将使用默认构造函数初始化。

清单10.9将这些原则应用到一个简短程序中，该程序初始化四个数组元素，显示它们的内容，并测试这些元素以找出总价值最高的那个。由于 `topval()` 一次只检查两个对象，程序使用 `for` 循环检查整个数组。它还使用一个指向 Stock 的指针来跟踪哪个元素具有最高价值。此清单使用清单10.7的头文件和清单10.8的方法文件。

## 清单10.9 usestok2.cpp

```cpp
// usestok2.cpp -- using the Stock class
// compile with stock20.cpp
#include <iostream>
#include "stock20.h"

const int STKS = 4;
int main()
{
// create an array of initialized objects
    Stock stocks[STKS] = {
        Stock("NanoSmart", 12, 20.0),
        Stock("Boffo Objects", 200, 2.0),
        Stock("Monolithic Obelisks", 130, 3.25),
        Stock("Fleep Enterprises", 60, 6.5)
        };

    std::cout << "Stock holdings:\n";
    int st;
    for (st = 0; st < STKS; st++)
        stocks[st].show();

// set pointer to first element
    const Stock * top = &stocks[0];
    for (st = 1; st < STKS; st++)
        top = &top->topval(stocks[st]);

// now top points to the most valuable holding
    std::cout << "\nMost valuable holding:\n";
    top->show();
    return 0;
}
```

下面是清单10.9中程序的输出：

```
Stock holdings:
Company: NanoSmart  Shares: 12
    Share Price: $20.00  Total Worth: $240.00
Company: Boffo Objects  Shares: 200
    Share Price: $2.00  Total Worth: $400.00
Company: Monolithic Obelisks  Shares: 130
    Share Price: $3.250  Total Worth: $422.50
Company: Fleep Enterprises  Shares: 60
    Share Price: $6.500  Total Worth: $390.00

Most valuable holding:
Company: Monolithic Obelisks  Shares: 130
    Share Price: $3.250  Total Worth: $422.50
```

关于清单10.9需要注意的一点是，大部分工作都花在设计类上。完成之后，编写程序本身相当简单。

顺便说一句，了解 `this` 指针可以更容易地理解 C++ 在底层是如何工作的。例如，最初的 Unix 实现使用一个 C++ 前端将 C++ 程序转换为 C 程序。为了处理方法定义，它只需将这样的 C++ 方法定义

```cpp
void Stock::show() const
{
    cout << "Company: " << company
         << "  Shares: " << shares << '\n'
         << "  Share Price: $" << share_val
         << "  Total Worth: $" << total_val << '\n';
}
```

转换为以下 C 风格定义：

```cpp
void show(const Stock * this)
{
    cout << "Company: " << this->company
         << "  Shares: " << this->shares << '\n'
         << "  Share Price: $" << this->share_val
         << "  Total Worth: $" << this->total_val << '\n';
}
```
