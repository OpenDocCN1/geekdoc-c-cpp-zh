
```cpp
class Date {
public:
// ...
int day() const; // const 成员：不能修改对象
Month month() const; // const 成员：不能修改对象
int year() const; // const 成员：不能修改对象

void add_day(int n); // 非 const 成员：可以修改对象
void add_month(int n); // 非 const 成员：可以修改对象
void add_year(int n); // 非 const 成员：可以修改对象

private:
int y; // 年份
Month m;
int d; // 月份中的天数
};

Date d <2000, Month::jan, 20>;
const Date cd <2001, Month::feb, 21>;

cout << d.day() << " " << cd.day() << '\n'; // OK
d.add_day(1); // OK
cd.add_day(1); // 错误：cd 是 const
```

我们在成员函数声明的参数列表后紧跟着使用 `const` 来表示该成员函数可以针对 `const` 对象调用。一旦我们将成员函数声明为 `const`，编译器就会监督我们遵守不修改对象的承诺。例如：

```cpp
int Date::day() const
{
    ++d;    // 错误：尝试从 const 成员函数中改变对象
    return d;
}
```

自然，我们通常不会试图以这种方式“作弊”。编译器为类实现者提供的首先是保护免受意外，这对更复杂的代码特别有用。

### 9.7.5 成员和“辅助函数”

当我们设计接口以使其最小化（尽管是完整的）时，我们必须排除许多仅仅是有用的操作。如果一个函数可以简单、优雅且高效地实现为独立函数（即作为非成员函数），它应该在类外实现。这样，该函数中的 bug 不能直接破坏类对象中的数据。不访问表示很重要，因为通常的调试技术是“围捕惯常嫌疑人”；也就是说，当一个类出现问题时，我们首先查看直接访问表示的函数：其中几乎肯定有一个是罪魁祸首。如果有十几个这样的函数，我们会比有 50 个时更满意。

`Date` 类有五十个函数！你一定会怀疑我们在开玩笑。我们没有：几年前我调查了许多商业使用的 `Date` 库，发现它们充满了像 `next_Sunday()`, `next_workday()` 等函数。对于旨在为用户方便而非易理解、易实现和易维护而设计的类来说，五十并不是一个不合理的数字。

还请注意，如果表示改变，只有直接访问表示的函数需要重写。这是保持接口最小的另一个强有力的实际原因。在我们的 `Date` 示例中，我们可能会决定，一个代表自 1900 年 1 月 1 日起天数的整数，比 `year, month, day` 是适合我们用途的更好的表示。只有成员函数需要改变。

这里有一些*辅助函数*的例子：

```cpp
Date next_Sunday(const Date& d)
{
    // 使用 d.day(), d.month(), 和 d.year() 访问 d
    // 制作新的 Date 以返回
}
```

辅助函数也被称为*便利函数*、*辅助函数*以及许多其他名称。这些函数与其他非成员函数之间的区别是逻辑上的；也就是说，“辅助函数”是一个设计概念，而不是编程语言概念。辅助函数通常接受它们是辅助对象的类的参数作为参数。不过也有例外；请注意 `leapyear()`。通常，我们使用命名空间来标识一组辅助函数；参见§8.7：

```cpp
namespace Chrono {
    enum class Month { /* . . . */ };
    class Date { /* . . . */ };
    bool is_date(int y, Month m, int d);         // true for valid date
    Date next_Sunday(const Date& d) { /* . . . */ }
    Date next_weekday(const Date& d) { /* . . . */ }
    bool leapyear(int y) { /* . . . */ }            // see exercise 10
    bool operator==(const Date& a, const Date& b) { /* . . . */ }
    // . . . 
}
```

请注意，`==` 和 `!=` 运算符是函数。它们是典型的辅助函数。对于许多类，`==` 和 `!=` 显然有意义，但由于它们并不适用于所有类，编译器无法像编写拷贝构造函数的拷贝赋值那样为你编写它们。

还请注意，我们引入了辅助函数 `is_date()`。该函数取代了 `Date::is_valid()`，因为检查日期是否有效在很大程度上独立于 `Date` 的表示方式。例如，我们不需要知道 `Date` 对象是如何表示的，就能知道“2008年1月30日”是有效日期，而“2008年2月30日”不是。仍然可能有日期的某些方面取决于表示方式（例如，我们能表示“1066年1月30日”吗？），但（如果需要）`Date` 的构造函数可以处理这些问题。

## 9.8 Date 类

那么，让我们把所有内容整合起来，看看当我们结合所有的想法/关注点时，`Date` 类可能是什么样的。如果一个函数体只是 ... 注释，那么实际实现是很棘手的（请暂时不要尝试编写这些）。首先，我们将声明放在头文件 `Chrono.h` 中：

```cpp
// file Chrono.h

namespace Chrono {

enum class Month {
    jan=1, feb, mar, apr, may, jun, jul, aug, sep, oct, nov, dec
};

class Date {
public:
    class Invalid { };        // to throw as exception

    Date(int y, Month m, int d);    // check for valid date and initialize
    Date();                          // default constructor
    // the default copy operations are fine

    // nonmodifying operations:
    int day() const { return d; }
    Month month() const { return m; }
    int year() const { return y; }

    // modifying operations:
    void add_day(int n);
    void add_month(int n);
    void add_year(int n);
private:
    int y;
    Month m;
    int d;
};

bool is_date(int y, Month m, int d);    // true for valid date
bool leapyear(int y);                // true if y is a leap year

bool operator==(const Date& a, const Date& b);
bool operator!=(const Date& a, const Date& b);

ostream& operator<<(ostream& os, const Date& d);
istream& operator>>(istream& is, Date& dd);

Day day_of_week(const Date& d);      // day of week of d
Date next_Sunday(const Date& d);     // next Sunday after d
Date next_weekday(const Date& d);     // next weekday after d
}
                              // Chrono
```

定义放在文件 `Chrono.cpp` 中：

```cpp
// Chrono.cpp
#include "Chrono.h"

namespace Chrono {
// member function definitions:

Date::Date(int yy, Month mm, int dd)
           : y(yy), m(mm), d(dd)
{
    if(!is_date(yy,mm,dd)) throw Invalid{};
}

const Date& default_date()
{
    static Date dd {2001,Month::jan,1};  // start of 21st century
    return dd;
}

Date::Date()
     :y(default_date().year()),
      m(default_date().month()),
      d(default_date().day())
{
}

void Date:: add_day(int n)
{
    // ...
}

void Date::add_month(int n)
{
// ...
}

void Date::add_year(int n)
{
if (m==Month::feb && d==29 && !leapyear(y+n)) { // beware of leap years!
m = Month::mar; // use March 1 instead of February 29
d = 1;
}
y+=n;
}

// helper functions:
bool is_date(int y, Month m, int d)
{
// assume that y is valid
if (d<=0) return false; // d must be positive
if (m<Month::jan || Month::dec<m) return false;
int days_in_month = 31; // most months have 31 days
switch (m) {
case Month::feb: // the length of February varies
days_in_month = (leapyear(y))?29:28;
break;
case Month::apr: case Month::jun: case Month::sep: case Month::nov:
days_in_month = 30; // the rest have 30 days
break;
}
if (days_in_month<d) return false;
return true;
}

bool leapyear(int y)
{
// see exercise 10
}

bool operator==(const Date& a, const Date& b)
{
    return a.year()==b.year()
        && a.month()==b.month()
        && a.day()==b.day();
}

bool operator!=(const Date& a, const Date& b)
{
    return !(a==b);
}

ostream& operator<<(ostream& os, const Date& d)
{
    return os << '(' << d.year()
        << ',' << int(d.month())
        << ',' << d.day() << ')';
}

istream& operator>>(istream& is, Date& dd)
{
    int y, m, d;
    char ch1, ch2, ch3, ch4;
    is >> ch1 >> y >> ch2 >> m >> ch3 >> d >> ch4;
    if (!is) return is;
    if (ch1!='(' || ch2!=',' || ch3!=',' || ch4!=')') {   // oops: format error
        is.clear(ios_base::failbit);  // set the fail bit
        return is;
    }
    dd = Date(y, Month(m),d);    // update dd

    return is;
}

enum class Day {
    sunday, monday, tuesday, wednesday, thursday, friday, saturday
};

Day day_of_week(const Date& d)
{
    // . . .
}

Date next_Sunday(const Date& d)
{
// ...
}
Date next_weekday(const Date& d)
{
// ...
}
} // Chrono
```

为 `Date` 实现 `>>` 和 `<<` 的函数将在§10.8 和§10.9 中详细解释。

## 练习

此练习仅涉及让 `Date` 的各个版本能够运行。对于每个版本，定义一个名为 `today` 的 `Date`，初始化为1978年6月25日。然后，定义一个名为 `tomorrow` 的 `Date`，通过将 `today` 复制给它并增加其天数（使用 `add_day()`）来赋予它一个值。最后，使用§9.8中定义的 `<<` 输出 `today` 和 `tomorrow`。

您对有效日期的检查可以非常简单。可以随意忽略闰年。但是，不要接受不在 [1,12] 范围内的月份或不在 [1,31] 范围内的日期。每个版本至少测试一个无效日期（例如，2004年13月-5日）。

- §9.4.1 中的版本

- §9.4.2 中的版本

- §9.4.3 中的版本

- §9.7.1 中的版本

- §9.7.4 中的版本

## 复习

- 本章中描述的类的两个组成部分是什么？

- 类中接口和实现之间有什么区别？

- 章节中创建的原始 `Date struct` 有什么限制和问题？

- 为什么使用构造函数而不是 `init_day()` 函数来处理 Date 类型？

- 什么是不变量？举例说明。

- 什么时候应该将函数放在类定义中，什么时候应该在类外定义？为什么？

- 什么时候应该在程序中使用运算符重载？列出你可能想要重载的运算符（每个都带有理由）。

- 为什么类的公共接口应该尽可能小？

- 给成员函数添加 `const` 会有什么效果？

- 为什么“辅助函数”最好放在类定义之外？

## 术语

- 内置类型

- 类

- `const`

- 构造函数

- 析构函数

- 枚举

- 枚举类型

- 枚举器

- 辅助函数

- 实现

- 类内初始化器

- 内联

- 接口

- 不变量

- 表示

- 结构体

- 结构

- 用户定义类型

- 有效状态

## 练习题

- 列出§9.1中现实世界对象示例（如烤面包机）的合理操作集合。

- 设计和实现一个 `Name_pairs` 类，保存 `(name, age)` 对，其中 `name` 是字符串，`age` 是双精度浮点数。将其表示为 `vector<string>`（名为 `name`）和 `vector<double>`（名为 `age`）成员。提供一个输入操作 `read_names()`，读取一系列姓名。提供一个 `read_ages()` 操作，提示用户为每个姓名输入年龄。提供一个 `print()` 操作，按 `name` 向量确定的顺序打印 `(name[i], age[i])` 对（每行一个）。提供一个 `sort()` 操作，按字母顺序对 `name` 向量进行排序，并重新组织 `age` 向量以匹配。将所有“操作”实现为成员函数。测试该类（当然：尽早且经常测试）。

- 用（全局）`operator <<` 替换 `Name_pair::print()`，并为 `Name_pairs` 定义 `==` 和 `!=`。

- 查看§8.4中令人头痛的最后一个例子。正确缩进并解释每个构造的含义。注意，该示例并没有做任何有意义的事情；它是纯粹的混淆。

- 此练习及接下来的几个练习要求你设计和实现一个 `Book` 类，例如作为图书馆软件的一部分。Class

6. 为 `Book` 类添加运算符。让 `==` 运算符检查两本书的 ISBN 号是否相同。让 `!=` 也比较 ISBN 号。让 `<<` 运算符在单独的行上打印出标题、作者和 ISBN。

7. 为 `Book` 类创建一个名为 `Genre` 的枚举类型。类型包括 `fiction`（小说）、`nonfiction`（非小说）、`periodical`（期刊）、`biography`（传记）和 `children`（儿童）。为每本书指定一个 `Genre`，并对 `Book` 构造函数的成员函数进行适当修改。

8. 为图书馆创建一个 `Patron` 类。该类将包含用户的姓名、借书证号以及拖欠的图书馆费用（如果有）。提供访问这些数据的函数，以及一个设置用户费用的函数。编写一个辅助函数，根据用户是否拖欠费用返回一个布尔值（`bool`）。
