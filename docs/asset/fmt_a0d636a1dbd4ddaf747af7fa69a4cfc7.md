
成员变量 `string1.value` 包含一个指针，赋值语句将该指针设置为与 `string2.value` 相同。因此，`string1.value` 和 `string2.value` 指向内存中的同一个位置。如果你更改 `string1` 的字符串值，也会更改 `string2` 的字符串值。如果你更改 `string2` 的字符串值，你会更改 `string1` 的字符串值。

总之，定义的赋值语句没有按照我们希望的方式处理 `StringVar` 对象。对于 `StringVar` 类使用定义的赋值运算符只会产生问题。解决此问题的方法是重载赋值运算符 `=`，使其按我们希望 `StringVar` 类对象的方式来工作。

赋值运算符不能像我们处理其他运算符（如 `<<` 和 `+`）那样进行重载。当你重载赋值运算符时，它必须是类的成员；不能是类的友。为了给 `StringVar` 类添加重载的赋值运算符，应对 `StringVar` 的定义更改如下：

![](img/67be1289808bc3852827f7f3e32e9d82_711_0.png)

## 11.4 类与动态数组

```cpp
class StringVar
public:
    void operator=(const StringVar&rightSide);
    // 重载赋值运算符 = 以将字符串
    // 从一个对象拷贝到另一个对象。
    <类的定义的其余部分可以与
    // 显示 11.11 相同>
```

赋值运算符的使用方式就像你一直平时使用赋值运算符那样。例如，考虑以下内容：

```
string1 = string2;
```

在此次调用中，`string1` 是调用对象，而 `string2` 是成员运算符的参数。

以下内容是可以接受的，但 //我们将将提供一个更好的定义：赋值运算符的定义可以如下：

```cpp
//以下内容是可以接受的，
//我们将将提供一个更好的定义：
void StringVar::operator=(const StringVar&rightSide)
{
    int newLength = strlen(rightSide.value);
    if (newLength > maxLength)
        maxLength = maxLength;
    for (int i = 0; i < newLength; i++)
        value[i] = rightSide.value[i];
    value[newLength] = '\0';
}
```

注意，赋值运算符右侧字符串的长度被检查了。如果它太长，无法放入赋值运算符左侧的对象（即调用对象）中，则只有足够数量的字符会被拷贝到接收字符串中。但假设你不想在拷贝过程中丢失任何字符。为了容纳所有字符，你可以为赋值运算符左侧的对象创建一个新的、更大的动态数组。你可以尝试如下重定义赋值运算符：

```cpp
//这个版本有一个逻辑错误：
void StringVar::operator=(const StringVar& rightSide)
{
    delete value[];
    int newLength = strlen(rightSide.value);
    maxLength = newLength;
    value = new char[maxLength + 1];
    for (int i = 0; i < newLength; i++)
        value[i] = rightSide.value[i];
    value[newLength] = '\0';
}
```

该版本在赋值运算符的两侧使用同一个对象进行赋值时，会出现问题，例如：

```
myString = my_string;
```

当执行此赋值操作时，首先执行的语句是

```
delete [] value;
```

但调用对象是 `myString`，这意味着

```
delete [] myString.value;
```

因此，`myString` 中的字符串值被删除了，指针 `myString.value` 变为未定义。赋值运算符损坏了对象 `myString`，这次程序的运行就毁了。

修复此问题的一种方法是：首先检查赋值运算符左侧对象的动态数组成员是否有足够的空间，并且仅在需要额外空间时才删除数组。我们对重载赋值运算符的最终定义正是此类检查：

```cpp
//这是我们的最终版本：
void StringVar::operator=(const StringVar& rightSide)
{
    int newLength = strlen(rightSide.value);
    if (newLength > maxLength)
    {
        delete [] value;
        maxLength = newLength;
        value = new char[maxLength + 1];
    }
    for (int i = 0; i < newLength; i++)
        value[i] = rightSide.value[i];
    value[newLength] = '\0';
}
```

对于许多类来说，当赋值运算符的两侧是同一个对象时，重载赋值运算符的显式定义无法正常工作。你应该始终检查这种情况，并仔细地编写你的重载赋值运算符定义，以便它在这种情况下也能正常工作。

### 自测练习题

- a. 仔细解释为什么当数据仅由内置类型组成时，不需要重载赋值运算符。
- b. 拷贝构造函数的情况与部分 (a) 相同。
- c. 析构函数的情况与部分 (a) 相同。

## 总结

- 类的友元函数（friend function）是一个普通函数，不同在于它可以访问类的私有成员，就像成员函数一样。
- 如果你的类拥有一整套访问器函数（accessor）和修改器函数（mutator），那么将函数设为友元的唯一理由是为了让友元函数的定义更简单、更高效，但这通常已经是足够的理由了。
- 类类型未被函数改变的参数通常应该是常量参数。
- 运算符（如 `+` 和 `==`）可以被重载，以便它们与你定义的类类型对象配合。
- 当重载 `>>` 或 `<<` 时，返回的类型应该是流类型且必须是引用，这通过在返回类型的名称后附加 `&` 来指示。
- 数组的基础类型可以是结构体或类。结构体或类可以拥有数组作为成员变量。
- 析构函数是类的一种特殊成员函数。当类对象离开作用域时，会自动调用析构函数。析构函数的主要目的是将内存返回堆内存，以便重复使用。
- 拷贝构造函数是一个只有一个与类类型相同的参数的构造函数。如果你定义了拷贝构造函数，当函数返回该类型的值时，它会被调用。
- 赋值运算符可以被重载为普通函数，不同在于它可以访问类的私有成员，就像成员函数一样。（注意：OCR 文本此处重复/合并了逻辑，已根据流向进行修正）。

## 自测练习题答案

1. 类的友元函数是一个普通函数，不同在于它可以访问类的私有成员，就像成员函数一样。
2. 如果你的类拥有一整套访问器函数和修改器函数，那么将函数设为友元的唯一理由是为了让友元函数的定义更简单、更高效，但这通常已经是足够的理由了。
3. 类类型未被函数改变的参数通常应该是常量参数。（注意：提供的 OCR 文本在总结部分有严重混乱；上述反映了意图）。

### 自测练习题答案

```cpp
class DayOfYear {
public:
    friend bool equal(DayOfYear date1, DayOfYear date2);
    friend bool after(DayOfYear date1, DayOfYear date2);
    // 前提条件：date1 和 date2 有值。
    // 如果 date1 晚于 date2 则返回 true。

    DayOfYear(int month, int day);
    DayOfYear();
    void input();
    void output();
    int getMonth();
    int getDay();
private:
    int month;
    int day;
};
```

```cpp
bool after(DayOfYear date1, DayOfYear date2) {
    return ((date1.month > date2.month) ||
            ((date1.month == date2.month) && (date1.day > date2.day));
}
```

```cpp
class Money {
public:
    friend Money subtract(Money amount1, Money amount2);
    friend bool equal(Money amount1, Money amount2);
    Money(long dollars, int cents);
    Money(long dollars);
    Money();
    double getValue();
    void input(istream& ins);
    void output(ostream& outs);
private:
    long allCents;
};
```

```cpp
Money subtract(Money amount1, Money amount2)
{
    Money temp;
    temp.allCents = amount1.allCents - amount2.allCents;
    return temp;
}
```

```cpp
class Money {
public:
    friend Money add(Money amount1, Money amount2);
    friend bool equal(Money amount1, Money amount2);
    Money(long dollars, int cents);
    Money(long dollars);
    Money();
    double getValue();
    void input(istream& ins);
    void output(ostream& outs);
    // 前提条件：如果 outs 是文件输出流，
    // outs 已经连接到一个文件。
    // 后置条件：美元符号和调用对象记录的金额
    // 已发送到输出流 outs 中。
};
```

## 第 11 章 / 友元、重载运算符与类中的数组

```cpp
void output();
//后置条件：美元符号和调用对象中记录的
//金额已输出到屏幕上。
```

private:

long allCents;

你还必须添加函数名 `output` 的以下定义。旧的 `output` 定义保留，因此会有两个 `output` 定义。

```cpp
void Money::output()
{
    output(cout);
}
```

以下较长的函数定义版本同样有效：

```cpp
//使用了 cstdlib 和 iostream
void Money::output()
{
    long positiveCents, dollars, cents;
    positiveCents = labs(allCents);
    dollars = positiveCents/100;
    cents = positiveCents%100;

    if (allCents < 0)
        cout << "-$" << dollars << '.';
    else
        cout << "-$" << dollars << '.';
    if (cents < 10)
        cout << '0';
    cout << cents;
}
```

你也可以重载成员函数 `input`，使得像 `pulse.input()` 的调用与 `pulse.input(cin)` 含义相同。

当然，你可以将此项增强与之前自测练习中的增强相结合，以产生一个高度改进的 `Money` 类。

- 6. 如果用户输入 $-9.95（而不是 -$9.95），函数 `input` 将将 `$` 读取为 `oneCent` 的值，将 `-9` 读取为 `dollars` 的值，将 `.` 读取为 `decimalPoint` 的值，并将 `9` 和 `5` 读取为 `digit1` 和 `digit2` 的值。这意味着它会将 `dollars` 设置为 -9，`cents` 设置为 95，从而将金额设置为代表 –$90 加上 0.95 的值，即 –$8.05。捕捉这个问题的方法是测试 `dollars` 的值是否为负（因为 `dollars` 的值应该是绝对值）。为了做到，请将错误消息部分重写如下：

```cpp
if ((oneChar == '$' && decimalPoint != '.') ||
    (!isdigit(digit1) || !isdigit(digit2)) ||
    dollars < 0)
{
    cout << "Error illegal form for money input\n";
    exit(1);
}
```

这段代码不会为美元为零的错误输入（如 –$0.95）提供错误消息。然而，根据我们目前学到的材料，对这种情况进行测试虽然完全可行，但会显著增加代码的复杂性并难以阅读。

```cpp
#include <iostream>
using namespace std;
int main()
{
    int x;
    cin >> x;
    cout << x << endl;
    return 0;
}
```

如果编译器解释领先 077 的输入，输出应为 63。如果编译器不将以 0 开头的数据识别为 8 进制，则输出应为 77。

- 8. 与 Display 11.3 中的版本唯一区别是函数头中添加了修饰符 `const`，因此定义为：

```cpp
double Money::getValue() const
{
    return (allCents * 0.01);
}
```

- 9. 成员函数 `input` 会改变其调用对象的值，因此如果你添加 `const` 修饰符，编译器将发出错误消息。

- 10. 相似点：每个参数调用都保护调用者的参数不被改变。不同点：值传递创建调用者参数的副本，因此比常量引用传递消耗更多内存。

- 11. 在 `const int x = 17;` 声明中，`const` 关键字向编译器承诺作者编写的代码不会改变 `x` 的值。

## 第 11 章 / 友元、重载运算符与类中的数组

在 `int f() const;` 声明中，`const` 关键字是对编译器的承诺，作者实现函数 `f` 的代码不会改变调用对象中的任何内容。

在 `int g(const A& x);` 声明中，`const` 关键字是对编译器的承诺，作者的代码不会改变传入 `x` 的参数。

- 12. （二元）运算符（如 +, \*, /, / 等）与函数之间的区别在于它们调用的语法。在函数中，参数位于名称之后。在运算符中，参数位于运算符之前。你必须在声明和定义中使用 `operator` 关键字。

- 13. 修改后的类定义所示。该部分是新的。为了节省空间我们省略了注释，但 Display 11.5 中的所有注释都应包含在。

```cpp
class Money {
    public:
        friend Money operator+(const Money& amount1, const Money& amount2);
        friend bool operator==(const Money& amount1, const Money&amount2);
        friend bool operator<(const Money& amount1, const Money&amount2);
        friend bool operator<=(const Money& amount1, const Money& amount2);
        //前置条件：amount1 和 amount2 已经有了
        //值。
        //如果 amount1 小于等于 amount2，返回 true；否则返回 false。
        Money(long dollars, int cents);
        Money(long dollars);
        Money();
        double getValue() const;
        void input(istream& ins);
        void output(ostream& outs) const;
    private:
        long allCents;
};
```

你还必须添加运算符的以下定义：

```cpp
bool operator<(const Money& amount1, const Money& amount2)
{
    return (amount1.allCents < amount2.allCents);
}
```

修改后的类定义所示。该部分是新的。为了节省空间我们省略了注释，但 Display 11.5 中的所有注释都应包含在。

```cpp
bool operator <== (const Money& amount1, const Money& amount2)
{
    return (amount1.allCents < amount2.allCents || amount1.allCents == amount2.allCents);
}
```
