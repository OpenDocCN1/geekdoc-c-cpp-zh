
```
namespace Chrono { // facilities for dealing with time
class Date { /* ... */ };
int diff(Date a, Date b);
bool is_leapyear(int y);
bool is_date(int d, Month m, int y);
const Date& default_date();
Date next_weekday(Date d);
Date next_saturday(Date d);
// ...
}
```

`Chrono` 命名空间自然也会包含相关的类，例如 `Time` 和 `Stopwatch`，以及它们的辅助函数。使用命名空间来容纳单个类通常是一种过度设计，会导致不便。

自然地，辅助函数必须在某处定义：

```
bool Chrono::is_date(int d, Month m, int y)
{
    int ndays;
    switch (m) {
        case Month::feb:
            ndays = 28+is_leapyear(y);
            break;
        case Month::apr: case Month::jun: case Month::sep: case Month::nov:
            ndays = 30;
            break;
        case Month::jan: case Month::mar: case Month::may: case Month::jul: case Month::aug: case Month::oct: case Month::dec:
            ndays = 31;
            break;
        default:
            return false;
    }
    return 1<=d && d<=ndays;
}
```

我在这里故意有点偏执。`Month` 不应超出 `jan` 到 `dec` 范围，但这是可能的（有人可能在强制转换时粗心），所以我进行了检查。

麻烦的 `default_date` 最后变成：

```
const Date& Chrono::default_date()
{
    static Date d {1,Month::jan,1970}; return d;
}
```

# 16.3.3 重载运算符

添加函数以实现惯用记法通常很有用。例如，`operator==()` 定义相等运算符 `==` 使其适用于 `Dates`：

```
inline bool operator==(Date a, Date b) // equality
{
    return a.day()==b.day() && a.month()==b.month() && a.year()==b.year();
}
```

其他明显候选是：

```
bool operator!=(Date, Date);
bool operator<(Date, Date);
bool operator>(Date, Date);
// inequality
// less than
// greater than
// …
Date& operator++(Date& d) { return d.add_day(1); } Date& operator--(Date& d) {
    return d.add_day(-1); }
// increase Date by one day // decrease Date by one day
```

```
Date& operator+=(Date& d, int n) { return d.add_day(n); } Date& operator-=(Date& d, int n) { return d.add_day(-n); }
// add n days
// subtract n days
```

```
Date operator+(Date d, int n) { return d+=n; } Date operator-(Date d, int n) { return d+=n; }
// add n days
// subtract n days
```

```
ostream& operator<<(ostream&, Date d); istream& operator>>(istream&, Date& d);
// output d // read into d
```

这些运算符与 `Date` 一起定义在 `Chrono` 中，以避免重载问题并受益于参数依赖查找（§14.2.4）。

对于 `Date`，这些运算符可以看作是便利设施。然而，对于许多类型 —— 例如复数（§18.3）、向量（§4.4.1）和类函数对象（§3.4.3，§19.2.2）—— 使用惯用运算符已根深蒂固，以至于其定义几乎是强制性的。运算符重载在第 18 章讨论。

对于 `Date`，我曾想过将 `+=` 和 `-=` 作为成员函数提供而不是 `add_day()`。如果我这样做，我会遵循一个常见习惯用法（§3.2.1.1）。请注意赋值和拷贝初始化默认提供（§16.3，§17.3.3）。

# 16.3.4 具体类的意义

我称像 `Date` 这样的简单用户定义类型为具体类型，以将其与抽象类（§3.2.2）和类层次结构（§20.4）区分开来，并强调它们与内置类型如 `int` 和 `char` 的相似性。具体类像内置类型一样使用。具体类型也被称为值类型，其使用被称为值导向编程。它们的使用模型和设计背后的“哲学”与通常所说的面向对象编程（§3.2.4，第 21 章）大不相同。

具体类型的意图是做好一件相对简单的事情，并且高效。它通常不以向用户提供修改具体类型行为的设施为目标。特别是，具体类型不打算显示运行时多态行为（参见§3.2.3，§20.3.2）。

如果你不喜欢具体类型的某个细节，你就构建一个具有期望行为的新类型。如果你想“重用”一个具体类型，你就在新类型的实现中使用它，就像使用 `int` 一样。例如：

```
class Date_and_time {
private:
    Date d;
    Time t;
public:
    Date_and_time(Date d, Time t);
    Date_and_time(int d, Date::Month m, int y, Time t);
    // ...
};
```

另外，第20章中讨论的派生类机制也可以用来通过描述所需的不同之处，从一个具体类定义新的类型。`Vec` 从 `vector` (§4.4.1.2) 的定义就是一个例子。然而，由于缺乏虚函数和运行时类型信息（§17.5.1.4，第22章），从具体类派生应谨慎进行且仅在很少情况下使用。

使用一个足够好的编译器，像 `Date` 这样的具体类在时间和空间上不会产生任何隐藏开销。特别是，访问具体类的对象不需要通过指针进行间接访问，并且具体类的对象中不存储“维护”数据。具体类型的大小在编译时已知，因此对象可以分配在运行时栈上（即，无需自由存储操作）。对象的布局在编译时已知，因此操作的内联可以轻易实现。同样，与 C 和 Fortran 等其他语言的布局兼容性无需特殊努力即可实现。

一套良好的此类类型可以为应用程序提供基础。特别是，它们可用于使接口更具体且不易出错。例如：

```
Month do_something(Date d);
```

这比以下情况更不可能被误解或误用：

```
int do_something(int d);
```

缺乏具体类型可能导致晦涩的程序，以及浪费时间让每个程序员编写代码直接操作表示为内置类型简单聚合的“简单且频繁使用”的数据结构。或者，应用程序中缺乏合适的“小型高效类型”可能导致使用过于通用且昂贵的类时出现严重的运行时和空间效率低下。

# 16.4 建议

- [1] 将概念表示为类；§16.1。
- [2] 将类的接口与其实现分离；§16.1。
- [3] 仅当它确实只是数据且数据成员没有有意义的不变量时才使用公共数据（`struct`）；§16.2.4。
- [4] 定义构造函数来处理对象的初始化；§16.2.5。
- [5] 默认情况下将单参数构造函数声明为 `explicit`；§16.2.6。
- [6] 声明一个不修改其对象状态的成员函数为 `const`；§16.2.9。
- [7] 具体类型是最简单的类类型。在适用时，优先使用具体类型而不是更复杂的类和纯数据结构；§16.3。
- [8] 仅当函数需要直接访问表示时才将其设为成员

# 17 构造、清理、拷贝和移动

> 无知比知识更常产生自信。
> —— 查尔斯·达尔文

- 引言
- 构造函数和析构函数
  - 构造函数与不变量；析构函数与资源；基类和成员析构函数；调用构造函数和析构函数；虚析构函数
- 类对象初始化
  - 无构造函数初始化；使用构造函数初始化；默认构造函数；初始化列表构造函数
- 成员和基类初始化
  - 成员初始化；基类初始化器；委托构造函数；在类中初始化器；静态成员初始化
- 拷贝和移动
  - 拷贝；移动
- 生成默认操作
  - 显式默认值；默认操作；使用默认操作；已删除函数
- 建议

## 17.1 引言

本章重点关注对象“生命周期”的技术方面：我们如何创建对象，如何拷贝它，如何移动它，以及当它消失时如何清理它？“拷贝”和“移动”的正确定义是什么？例如：

```
string ident(string arg) {
    // string passed by value (copied into arg)
    return arg;
}
// return string (move the value of arg out of ident() to a caller)

int main() {
    string s1 {"Adams"};
    s1 = ident(s1);
    string s2 {"Pratchett"};
    s1 = s2;
    // initialize string (construct in s1).
    // copy s1 into ident()
    // move the result of ident(s1) into s1; // s1’s value is “Adams”.
    // initialize string (construct in s2)
    // copy the value of s2 into s1
    // both s1 and s2 have the value “Pratchett”.
}
```

显然，在调用 `ident()` 之后，`s1` 的值应该是“Adams”。我们将 `s1` 的值拷贝到参数 `arg` 中，然后将 `arg` 的值从函数调用中移出（并）移回 `s1`。接下来，我们用值“Pratchett”构造 `s2` 并将其拷贝到 `s1`。最后，在退出 `main()` 时我们销毁变量 `s1` 和 `s2`。拷贝和移动的区别在于，拷贝后两个对象必须具有相同的值，而移动后源对象不需要保留其原始值。移动可用于源对象将不再被使用的情况。它们对于实现资源移动的概念特别有用（§3.2.1.2，§5.2）。

这里使用了几个函数：

- 用字符串字面量初始化字符串的构造函数（用于 `s1` 和 `s2`）
- 拷贝字符串的拷贝构造函数（拷贝到函数参数 `arg`）
- 移动字符串值的移动构造函数（从 `arg` 移出 `ident()` 到保存 `ident(s1)` 结果的临时变量）
- 移动字符串值的移动赋值（从保存 `ident(s1)` 结果的临时变量移动到 `s1`）
- 拷贝字符串的拷贝赋值（从 `s2` 拷贝到 `s1`）
- 释放 `s1`、`s2` 以及保存 `ident(s1)` 结果的临时变量所拥有的资源的析构函数

优化器可以消除其中一些工作。例如，在这个简单示例中，临时变量通常会被消除。然而，从原则上讲，这些操作会被执行。构造函数、拷贝和移动赋值操作以及析构函数直接支持生命周期和资源管理的视图。对象在其构造函数完成后被视为其类型的对象，并且在其析构函数开始执行之前一直保持为其类型的对象。对象生命周期与错误之间的交互在 §13.2 和 §13.3 中进一步探讨。特别是，本章不讨论半构造和半销毁对象的问题。

对象的构造在许多设计中起关键作用。这种广泛的使用反映在支持初始化的语言特性的范围和灵活性中。类型的构造函数、析构函数以及拷贝和移动操作在逻辑上不是分离的。我们必须将它们作为匹配的集合来定义，否则会遭受逻辑或性能问题。如果类 `X` 有一个执行非平凡任务的析构函数，例如自由存储释放或锁释放，该类很可能需要完整的函数集合：

```
class X {
    X(Sometype); // “ordinary constructor”: create an object
    X(); // default constructor
    X(const X&); // copy constructor
    X(X&&); // move constructor
    X& operator=(const X&); // copy assignment: clean up target and copy
    X& operator=(X&&); // move assignment: clean up target and move
    ~X(); // destructor: clean up
    // ...
};
```

对象被拷贝或移动的情况有五种：

- 作为赋值的源
- 作为对象初始化器
- 作为函数参数
- 作为函数返回值
- 作为异常

在所有情况下，拷贝或移动构造函数将被应用（除非可以优化掉）。除了命名对象和自由存储上的对象的初始化外，构造函数还用于初始化临时对象（§6.4.2）并实现显式类型转换（§11.5）。除了“普通构造函数”之外，这些特殊成员函数可以由编译器生成；参见 §17.6。

本章充满了规则和技术细节。这些对于全面理解是必要的，但大多数人只是从示例中学习一般规则。

## 17.2 构造函数和析构函数

我们可以通过定义构造函数来指定类的对象应如何初始化（§16.2.5，§17.3）。为了补充构造函数，我们可以定义析构函数以确保在对象销毁时进行“清理”（例如，当它超出作用域时）。C++ 中许多最有效的资源管理技术都依赖于构造函数/析构函数对。同样，依赖于一对操作的其它技术，例如 do/undo、start/stop、before/after 等也如此。例如：

```
struct Tracer {
    string mess;
    Tracer(const string& s) :mess{s} { clog << mess; }
    ~Tracer() {clog << "~" << mess; }
};

void f(const vector<int>& v) {
    Tracer tr {"in f()\n"};
    for (auto x : v) {
        Tracer tr {string{"v loop "}+to<string>(x)+"\n"}; // §25.2.5.1
        // ...
    }
}
```

我们可以尝试一个调用：

```
f({2,3,5});
```

这将打印到日志流：

```
in f()
v loop 2
~v loop 2
```

### 17.2.1 构造函数和不变量

与类同名的成员称为构造函数。例如：

```
class Vector {
public:
    Vector(int s);
    // ...
};
```

构造函数声明指定参数列表（与函数完全相同），但没有返回类型。类名在类内不能用于普通成员函数、数据成员、成员类型等。例如：

```
struct S {
    S(); // fine
    void S(int); // error :no type can be specified for a constructor
    int S; // error :the class name must denote a constructor
    enum S { foo, bar }; // error :the class name must denote a constructor
};
```

构造函数的任务是初始化其类的对象。通常，这种初始化必须建立类不变量，即在调用成员函数（来自类外）时必须成立的东西。考虑：

```
class Vector {
public:
    Vector(int s);
    // ...
private:
    double* elem; // elem points to an array of sz doubles
    int sz; // sz is non-negative
};
```

这里（通常如此），不变量以注释形式陈述：“`elem` 指向一个包含 `sz` 个 `double` 的数组”以及“`sz` 为非负数”。构造函数必须使其为真。例如：

```
Vector::Vector(int s) {
    if (s<0) throw Bad_size{s};
    sz = s;
    elem = new double[s];
}
```
