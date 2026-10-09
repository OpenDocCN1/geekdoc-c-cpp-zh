
```cpp
struct A {
  A(int = 0); // 通常有两个是个坏主意
  A(double); // 从算术类型的转换
  operator int() const; // 通常有两个是个坏主意
  operator double() const; // 到算术类型的转换
  // 其他成员
};
```

```cpp
void f2(long double);
A a;
f2(a); // 错误：歧义：f(A::operator int())
// 或 f(A::operator double())
long lg;
A a2(lg); // 错误：歧义：A::A(int) 或 A::operator double()
```

在调用 `f2` 时，哪种转换都不是 `long double` 的精确匹配。然而，可以使用任何一种转换，然后通过标准转换转换为 `long double`。因此，没有哪种转换优于另一种；调用是歧义的。

当我们从 `long` 初始化 `a2` 时遇到了相同的问题。每个构造函数都是 `long` 的精确匹配。每个构造函数都需要在使用构造函数之前对参数进行转换：

- 标准 `long` 到 `double` 的转换，随后 `A(double)`

- 标准 `long` 到 `int` 的转换，随后 `A(int)`

这些转换序列是无法区分的，因此调用是歧义的。

对 `f2` 的调用和 `a2` 的初始化是歧义的，是因为所需的标准转换具有相同的秩（§ 6.6.1，第 245 页）。当使用用户定义的转换时，标准转换的秩（如果有）被用于选择最佳匹配。

```cpp
short s = 42;
A a3(s); // 将 short 提升为 int 比转换为 double 好
```

# 重载函数与转换构造函数

当调用重载函数时，在多个转换之间选择变得更加复杂。如果两个或多个转换提供了可行的匹配，则这些转换被认为是等好的。

例如，当重载函数通过定义相同构造函数的类类型进行区分时，可能会产生歧义问题：

[点击此处查看代码图像](#)

```cpp
struct C {
  C(int);
  // 其他成员
};
struct D {
  D(int);
  // 其他成员
};
void manip(const C&);
void manip(const D&);
manip(10); // 错误：歧义：manip(C(10)) 或 manip(D(10))
```

# C++ Primer, 第五版

这里 `C` 和 `D` 都有接受 `int` 的构造函数。任何构造函数都可以用于匹配 `manip`。因此，调用是歧义的：它可以将 `int` 转换为 `C` 并调用第一个版本，或者可以将 `int` 转换为 `D` 并调用第二个版本。

调用者可以通过显式构造正确的类型来消除歧义：

[点击此处查看代码图像](#)

```cpp
manip(C(10)); // OK：调用 manip(const C&)
```

> 警告

> 在重载函数的调用中使用构造函数或类型转换来转换参数，经常可能是设计不良的信号。

# 重载函数与用户定义转换

在调用重载函数时，如果两个（或多个）用户定义的转换提供了可行的匹配，则这些转换被认为是等好的。可能或不考虑的标准转换的秩不被考虑。内置转换是否也仅在可以使用相同的转换函数匹配重载集时才被考虑。

例如，即使其中一个类定义了对参数需要标准转换的构造函数，我们对 `manip` 的调用可能是歧义的：

[点击此处查看代码图像](#)

```cpp
struct E {
  E(double);
  // 其他成员
};

void manip2(const C&);
void manip2(const E&);
manip2(10); // 错误：歧义：manip2(C(10)) 或 manip2(E(double(10)))
```

在这种情况下，`C` 有从 `int` 的转换，`E` 有从 `double` 的转换。对于调用 `manip2(10)`，两个 `manip2` 函数都是可行的：

- `manip2(const C&)` 是可行的，因为 `C` 有一个接受 `int` 的转换构造函数。该构造函数是参数的精确匹配。

- `manip2(const E&)` 是可行的，因为 `E` 有一个接受 `double` 的转换构造函数，我们可以使用标准转换转换 `int` 参数以便使用该转换构造函数。

由于对重载函数的调用需要彼此不同的用户定义转换，因此此调用是歧义的。特别是，尽管其中一个调用需要标准转换，而另一个是精确匹配，编译器仍然会将此调用标记为错误。

> 注意

> 在对重载函数进行调用时，额外的标准转换（如果有的话）的秩仅在可行函数需要相同的用户定义转换时才重要。如果需要不同的用户定义转换，则该调用是歧义的。

### 14.9.3. 函数匹配与重载运算符

重载运算符是重载函数。普通函数匹配（见第 233 页第 6.4 节）用于用于确定在给定的表达式上应该应用哪种运算符（内置的或重载的）。然而，当表达式中使用比那更宽泛的运算符时，候选函数集会增加。如果 `a` 具有类类型，表达式 `a sym b` 可能会调用使用调用运算符的函数。

点击此处查看代码

```
a.operatorsym(b); // a 有 operatorsym 成员函数
operatorsym(a, b); // operatorsym 是一个普通函数
```

与函数调用不同，我们无法通过调用的形式来区分我们调用的是非成员函数还是成员函数。

### 练习题章节 14.9.2

练习 14.50：显示 `ex1` 和 `ex2` 初始化时可能的类类型转换序列。解释这些初始化是否合法。

点击此处查看代码

```
struct LongDouble {
    LongDouble(double = 0.0);
    operator double();
    operator float();
}
LongDouble l1dobj;
int ex1 = l1dobj;
float ex2 = l1dobj;
```

练习 14.51：显示调用每个版本的 `calc` 所需的转换序列（如果有），并解释为什么选择最佳可行函数。

点击此处查看代码

```
void calc(int);
void calc(LongDouble);
double dval;
calc(dval); // 调用哪一个 calc?
```

当我们对类类型的操作数使用重载运算符时，候选函数包括该运算符的普通成员版本，以及该运算符的内置版本。此外，如果左侧操作数具有类类型，则该类定义的运算符重载版本（如果有）也会被包含在内。

当我们调用具名函数时，同名的成员函数和非成员函数不会产生相互重载。这里没有重载，因为调用具名函数的语法区分了成员函数和非成员函数。当通过类类型对象调用（通过对该对象的引用或指针）时，只考虑该类的成员函数。当我们在表达式中使用重载运算符时，没有任何可以表明我们正在使用成员函数或非成员函数。因此，成员和非成员版本都必须被考虑。

> 注意

表达式中使用的运算符的候选函数集可以同时包含非成员和成员函数。

作为一个示例，我们将为 `SmallInt` 类定义一个加法运算符：

点击此处查看代码

```
class SmallInt {
    friend
    SmallInt operator+(const SmallInt&, const SmallInt&);
public:
    SmallInt(int i = 0); // 从 int 转换
    operator(int) const { return val; } //  int
private:
    std::size_t val;
};
```

我们可以使用该类加上两个 `SmallInt`，但如果我们尝试执行混合模式算术，将会遇到歧义问题：

点击此处查看代码

SmallInt s1, s2;

SmallInt s3 = s1 + s2; // 使用重载运算符+

int i = s3 + 0; // 错误：歧义

第一次加法使用了接受两个 `SmallInt` 值的重载 `+` 版本。

第二次加法是歧义的，因为需要将 `s3` 转换为 `int`，或者使用内置的运算符。

> 警告

对于表达式中使用的运算符，同时提供 `SmallInt` 类型的转换函数和 `int` 类型的重载运算符可能会导致歧义。

## 练习题章节 14.9.3

练习 14.52：对于每个加法表达式，使用了哪个运算符 `+`？列出所需的候选函数：

点击此处查看代码

```
struct LongDouble {
    // operator+ 通常是非成员
    LongDouble operator+(const SmallInt&);
    // 见第 587 页 14.9
}
LongDouble operator+(LongDouble&);
SmallInt si;
LongDouble ld;
ld + si;
```

练习 14.53：根据第 588 页的 `SmallInt` 定义，判断以下加法表达式是否合法。如果是，使用了哪种运算符？如果不是，你如何修改代码使其合法？

```
SmallInt s1;
double d = s1 + 14;
```

## 章节总结

重载运算符要么是类的成员，要么至少一个操作数具有类类型。重载运算符在应用于内置类型时，与相应的运算符的操作数、优先级相同。当运算符定义为成员时，其 `this` 指针绑定到第一个操作数。赋值、下标、函数调用和箭头运算符必须是成员。

类可以定义自动使用的其类型转换。非显式构造函数通过单个参数定义从参数类型到类的转换；非显式转换运算符定义从类类型到类型的转换。Lambda 表达式是定义简单函数对象的简洁方式。

## 定义

- **调用签名 (call signature)**：表示可调用对象的接口。调用签名包括返回类型和括号内的逗号分隔参数列表。

- **类类型转换 (class-type conversion)**：到或类的转换分别由构造函数和转换运算符定义。非显式构造函数通过单个参数定义从参数类型到类的转换。转换运算符定义从类类型到指定类型的转换。

- **转换运算符 (conversion operator)**：位于 `explicit` 关键字之前的转换运算符。

- **显式转换运算符 (explicit conversion operator)**：带有 `explicit` 关键字的转换运算符，用于防止非意外的隐式转换。

- **函数对象 (function object)**：定义了运算符的类对象。

- **函数表 (function table)**：存储值的容器，通常是 map 或 vector。

- **函数模板 (function template)**：可以表示任何可调用对象的模板。

- **重载运算符 (overloaded operator)**：重新定义内置运算符含义的函数。重载运算符的名称后跟被定义的符号。重载运算符必须至少有一个操作数具有类类型。

- **用户定义转换 (user-defined conversion)**：类类型转换的同义词。

面向对象编程的核心思想是数据抽象、继承和动态绑定。通过数据抽象，我们可以定义将接口与实现分离开来的类（见第 7 章）。通过继承，我们可以定义模拟相似类型之间关系的类。通过动态绑定，我们可以使用这些类型的对象，而忽略它们之间差异的细节。

## 继承

通过继承关系相关的类形成了一个层次结构。通常情况下，在层次结构的根部有一个基类，其他类直接或间接地继承自基类。这些继承的类被称为派生类。基类定义了层次结构中所有类型共有的成员。每个派生类定义了派生类本身特有的成员。

为了建模我们的定价策略，我们将定义一个名为 `Quote` 的类，它将作为我们层次结构的基类。一个 `Quote` 对象将代表折扣书籍。我们将从 `Quote` 继承第二个类，名为 `Bulk_quote`，代表可以按数量折扣出售的书籍。

这些类将具有以下两个成员函数：

- *isbn()*，它将返回 ISBN。此操作不依赖于被继承类的具体实现；它只在 `Quote` 类中定义。

- *net_price(size_t)*，它将返回购买指定数量书籍的价格。此操作是类型特定的；`Quote` 和 `Bulk_quote` 都会定义它们自己的该函数版本。

在 C++ 中，基类会将依赖于类型的函数与它期望派生类在不改变的情况下继承的函数区分开来。基类定义了它期望派生类为自己实现的虚函数。利用这些知识，我们可以开始编写 `Quote` 类：

点击此处查看代码图像

```cpp
class Quote {
public:
    std::string isbn(const) const;
    virtual double net_price(std::size_t n) const;
};
```

派生类必须指定它意图继承的类。它在类派生列表中这样做，该列表是一个冒号，后面跟一个由逗号分隔的基类列表，每个基类可以有一个可选的访问限定符：

点击此处查看代码图像

```cpp
class Bulk_quote : public Quote { // Bulk_quote 继承自 Quote
public:
    double net_price(std::size_t) const override;
};
```

由于 `Bulk_quote` 在其派生列表中使用了 `public`，我们可以像使用 `Quote` 对象一样使用 `Bulk_quote` 类型的对象。

派生类必须在自己的正体中包含它意图为自己定义的所有虚函数的声明。派生类可以在这些函数上包含 `virtual` 关键字，但不是强制要求的。由于我们将在 § 15.3（第 606 页）中解释的原因，新标准允许派生类显式地指出其成员函数意图重写它所继承的虚函数。它通过在参数列表后指定 `override` 来实现。

## 动态绑定

通过动态绑定，我们可以相同的代码交替处理 `Quote` 或 `Bulk_quote` 任意类型的对象。例如，以下函数打印了购买指定数量书籍的总价：

点击此处查看代码图像

```cpp
// 计算指定数量书籍的价格，应用折扣
double print_total(ostream cout,
    const Quote &item, size_t n)
{
    // 取决于绑定到 item 参数的对象类型
    // 调用 Quote::net_price 或 Bulk_quote::net_price
    double ret = item.net_price(n);
    os << "ISBN: " << item.isbn // 调用 Quote::isbn()
         << " # sold: " << n << " total due: " << ret << endl;
    return ret;
}
```

该函数简单地打印总额，并返回通过对其参数调用 `net_price` 计算的值。

尽管如此，该函数有两个有趣的地方：由于我们将在 § 15.2.3（第 601 页）中解释的原因，因为 `item` 参数是 `Quote` 的引用，我们可以在 `Quote` 对象或 `Bulk_quote` 对象上调用此函数。而且，由于我们将在 § 15.2.1（第 594 页）中解释的原因，由于 `net_price` 是一个虚函数，由于 `print_total` 通过引用调用了 `net_price`，运行的 `net_price` 版本取决于传递给 `print_total` 的对象的类型：

点击此处查看代码图像

```cpp
// basic 类型为 Quote; bulk 类型为 Bulk_quote
print_total(cout, basic, 20); // 调用 Quote 版本的 net_price
print_total(cout, bulk, 20); // 调用 Bulk_quote 版本的 net_price
```

第一次调用将一个 `Quote` 对象传递给 `print_total`。当 `print_total` 调用 `net_price` 时，将运行 `Quote` 版本。在下一次调用中，参数是一个

![](img/3a7e14b77396239ca7166fc2adb32975_333_0.png)

`Bulk_quote`，因此运行 `Bulk_quote` 版本的 `net_price`。由于我们将在 § 15.2.3（第 601 页）中解释的原因，因为 `item` 参数是 `Quote` 的引用，我们可以在 `Quote` 对象或 `Bulk_quote` 对象上调用此函数。而且，由于我们将在 § 15.2.1（第 594 页）中解释的原因，由于 `net_price` 是一个虚函数，由于 `print_total` 通过引用调用了 `net_price`，运行的 `net_price` 版本取决于传递给 `print_total` 的对象的类型：

> 注意：当通过引用调用虚函数时，会发生动态绑定。基类通常应该定义虚构函数。

## 定义基类和派生类

在许多情况下，并不是所有通过继承定义的类都定义虚构函数。在本节中，我们将涵盖用于继承的类的其他方式。

### 15.2.1 定义基类

我们将通过完成 `Quote` 类的定义来开始定义基类：

```cpp
class Quote {
public:
    Quote() = default; // 见 7.1（第 264 页）
    Quote(const std::string &book, double sales_price):
        bookNo(book), price(sales_price) {}
    std::string isbn() const { return bookNo; } // 返回 ISBN
    // 派生类可以覆盖
    virtual double net_price(size_t n) const
        return price * n; }
    virtual ~Quote() = default; // 构函数的动态绑定
private:
    std::string bookNo; // 项目
protected:
    double price = 0.0; // 正常价格
};
```
