

# 表 11.1 可供类使用的运算符

| Operator | Description |
|---|---|
| () | Function call (see Section 11.4) |
| [] | Array element (see Section 11.4) |
| -> | Structure member pointer reference |
| new | Dynamic allocation of memory |
| delete | Dynamic deallocation of memory |
| ++ | Increment |
| -- | Decrement |
| - | Unary minus |
| ! | Logical negation |
| ~ | Ones complement |
| * | Indirection |
| * | Multiplication |
| / | Division |
| % | Modulus (remainder) |
| + | Addition |
| - | Subtraction |
| << | Left shift |
| >> | Right shift |
| < | Less than |
| <= | Less than or equal to |
| > | Greater than |
| >= | Greater than or equal to |
| == | Equal to |
| != | Not equal to |
| && | Logical AND |
| || | Logical OR |
| & | Bit-by-bit AND |
| ^ | Bit-by-bit exclusive OR |
| | | Bit-by-bit inclusive OR |
| = | Assignment |
| += -= *= /= %= &= ^= |= <<= >>= |  |
| , | Comma |

为类提供表 11.1 中的运算符的第一步是决定哪些操作对该类有意义以及应如何定义它们。作为示例，您将继续在第 10 章中引入的 Date 类的基础上进行构建。

## 创建类运算符

显然，两个日期的相加是没有意义的。然而，日期与整数的相加是有意义的，如果该整数被视为要加到日期上的天数。同样，从日期中减去一个整数也是有意义的。此外，两个日期的相减是有意义的，如果您将差值定义为两个日期之间的天数。同样，比较两个日期并确定日期是否相等或一个日期发生在另一个日期之前或之后也是有意义的。现在看看其中两个运算符 == 和 + 如何适用于 Date 类。

使用 C++ 内置运算符符号对类对象进行的操作被称为 **operator functions**。Operator functions 的声明和实现方式与所有成员函数相同，只有一个例外：函数名必须使用 *operator<symbol>* 的形式，其中 *<symbol>* 是表 11.1 中的一个运算符符号。例如，函数名 *operator+* 是类加法函数的名称，而函数名 *operator==* 是类比较函数的名称。必须理解，operator function 可以被重新定义为执行 *任何* 操作。然而，良好的编程实践规定，编写的函数应实际执行函数名所暗示的操作。

在选择函数名之后，编写函数的过程仅仅是使其接受输入并产生正确的返回值。例如，要比较两个 Date 对象是否相等，您选择 C++ 的相等运算符（==），函数名变为 operator==。对于 Date 类，此比较操作应接受两个 Date 对象，对它们进行比较，并返回一个布尔值以指示比较结果：相等时为 true，不相等时为 false。此 operator function 的合适原型如下：

```
bool operator==(const Date&);  //pass a reference to a Date object
```

此原型表示函数名为 operator==，它返回一个布尔值，并接受一个 Date 对象的引用。¹ 使用引用参数并非偶然。C++ 中引用的主要原因之一是便于构建重载运算符。原因在于引用使函数中的记法比使用指针时更自然。包含 const 关键字可确保传递的引用不能被函数更改。此原型必须包含在 Date 类的声明部分中。

现在看看如何为包含在类实现部分中的运算符编写函数定义。对于 Date 类，以下定义是合适的：

```
bool Date::operator==(const Date& date2)
{
    if (day == date2.day && month == date2.month && year == date2.year)
        return true;
    else
        return false;
}
```

定义此函数后，它可以通过使用关系表达式 a == b 或 a.operator==(b) 来调用，前提是 a 和 b 都是 Date 对象。更典型的是，它用于条件表达式中，例如 if (a == b)。程序 11.1 包含了此 if 语句和 operator function 的上下文中的完整程序。阴影线指示与 operator function 相关的语句。

### 程序 11.1

```
#include <iostream>
using namespace std;

// class declaration section
class Date
{
private:
    int month;
    int day;
    int year;
public:
    Date(int = 7, int = 4, int = 2012); // constructor
    bool operator==(Date&); // prototype for the operator== function
};

// class implementation section
Date::Date(int mm, int dd, int yyyy)
{
    month = mm;
    day = dd;
    year = yyyy;
}

bool Date::operator==(Date& date2)
{
    if(day == date2.day && month == date2.month && year == date2.year)
        return true;
    else
        return false;
}

int main()
{
    Date a(4,1,2012), b(12,18,2010), c(4,1,2012); // declare 3 objects
```

```
if (a == b)
    cout << "Dates a and b are the same." << endl;
else
    cout << "Dates a and b are not the same." << endl;
if (a == c)
    cout << "Dates a and c are the same." << endl;
else
    cout << "Dates a and c are not the same." << endl;
return 0;
}
```

程序 11.1 产生的输出如下：

```
Dates a and b are not the same.
Dates a and c are the same.
```

程序 11.1 中显示的第一个新特性是 operator== 函数的声明和实现。除了名称外，此 operator function 的构造方式与任何其他类方法相同：它在类声明部分中声明，并在类实现部分中定义。

第二个新特性是函数如何被调用。Operator functions 可以使用其关联的符号来调用。然而，由于 operator functions 是真正的函数，因此也可以使用传统的调用方法——指定函数名并包含适当的自变量。因此，在程序 11.1 中，除了使用表达式 a == b 调用之外，也可以使用 a.operator==(b) 进行调用。

现在看看如何为 Date 类创建另一个运算符——加法运算符。与之前一样，创建此运算符需要指定三项：

- Operator function 的名称
- 函数应执行的处理
- 函数应返回的数据类型（如果有）

显然，对于加法，您将使用加法符号作为 operator function 名称：operator+。在选择了函数名之后，您必须确定此函数对 Date 对象想要做什么。如前所述，加两个日期是没有意义的。然而，将整数加到日期上是有意义的，当整数表示给定日期之前或之后的日期数时。整数与 Date 对象的和只是一个新的 Date 对象，应由加法操作返回。因此，以下原型适用于加法函数：

```
Date operator+(int);
```

此原型包含在类声明部分中，指定将整数加到类对象上并返回一个 Date 对象。因此，如果 a 是一个 Date 对象，则函数调用 a.operator+(284)，或其更常见的替代形式 a + 284，应导致 284 正确地加到 a 的日期值上。

接下来，您必须构建函数以完成此任务，这首先需要选择一个日历约定。为简单起见，采用金融日期约定，即每个月包含 30 天，每年包含 360 天。使用此约定，函数将整数天数加到 Date 对象的 day 值上，然后调整 resulting day 值使其落在 1 到 30 的范围内，并将 month 值调整为落在 1 到 12 的范围内。以下函数完成了这些任务：

```
Date Date::operator+(int days)
{
    Date temp;  // a temporary Date to store the result

    temp.day = day + days;   // add the days
    temp.month = month;
    temp.year = year;

    while (temp.day > 30)   // adjust the months
    {
        temp.month++;
        temp.day -= 30;
    }
    while (temp.month > 12)  // adjust the years
    {
        temp.year++;
        temp.month -= 12;
    }

    return temp;     // the values in temp are returned
}
```

需要注意的重要特性是 temp 对象的用法。其目的是确保函数不会更改赋值语句右侧的对象。为了理解这一点，请考虑使用此 operator function 的语句，例如 newDate = oldDate + 284; newDate 和 oldDate 都是 Date 对象。此语句绝不应修改 oldDate 的值，而函数可以访问该值。2 相反，表达式 oldDate + 284 应产生一个新日期值，然后将其赋给 newDate。此新的 Date 对象在 operator function 中命名为 temp，并成为 operator+() 函数返回的 Date 对象，然后将其赋给 newDate。程序 11.2 在完整程序的上下文中使用了此函数。与 operator function 相关的语句已被着色。

