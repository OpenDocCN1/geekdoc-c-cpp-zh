
## 显示 11.6 重载一元运算符

```cpp
//Class for amounts of money in U.S. currency.
class Money
{
public:
    friend Money operator +(const Money& amount1, const Money& amount2);

    friend Money operator -(const Money& amount1, const Money& amount2);
    //Precondition: amount1 and amount2 have been given values.
    //Returns amount1 minus amount2.

    friend Money operator -(const Money& amount);
    //Precondition: amount has been given a value.
    //Returns the negative of the value of amount.

    friend bool operator ==(const Money& amount1, const Money& amount2);

    Money(long dollars, int cents);
    Money(long dollars);
    Money( );
    double getValue( ) const;
    void input(istream& ins);
    void output(ostream& outs) const;
private:
    long allCents;
};
```

<此处放置任何其他函数声明以及程序的主部分。>

```cpp
Money operator -(const Money& amount1, const Money& amount2)
{
    Money temp;
    temp.allCents = amount1.allCents - amount2.allCents;
    return temp;
}
```

```cpp
Money operator -(const Money& amount)
{
    Money temp;
    temp.allCents = -amount.allCents;
    return temp;
}
```

<其他函数定义与显示 11.5 中的相同。>

> 这是对显示 11.5 中给出的 Money 类的改进版本。

> 我们省略了 include 指令和一些注释，但你应该在程序中包含它们。

这个表达式中的两个操作数是 cout 和 amount，对表达式求值应将 amount 的值写到屏幕上。但如果 << 是一个像 + 或 * 这样的运算符，那么上述表达式也应该返回某个值。毕竟，带有其他操作数的表达式，如 n1 + n2，会返回值。但是 cout << amount 返回什么呢？为了得到这个问题的答案，我们需要考察一个更复杂的涉及 << 的表达式。

让我们考虑下面的表达式，它涉及使用 << 对表达式链进行求值：

```cpp
cout << "I have " << amount << " in my purse.\n";
```

如果你将运算符 << 视为与其他运算符（如 +）类似，那么上述表达式应该（实际上也确实是）等价于以下形式：

```cpp
((cout << "I have ") << amount) << " in my purse.\n";
```

为了使这个表达式有意义，<< 应该返回什么值？首先被求值的是子表达式：

```cpp
(cout << "I have ")
```

如果要让一切顺利工作，那么子表达式最好返回 cout，这样计算可以继续如下：

```cpp
(cout << amount) << " in my purse.\n";
```

而且如果要继续顺利工作，(cout << amount) 也最好返回 cout，这样计算可以继续如下：

```cpp
cout << " in my purse.\n";
```

这一点在显示 11.7 中进行了说明。运算符 << 应返回其第一个参数，即一个类型为 ostream 的流。

因此，重载运算符 <<（用于 Money 类）的声明应如下所示：

```cpp
class Money
{
public:
    ...
    friend ostream& operator<<(ostream& outs, const Money& amount);
    //Precondition: If outs is a file output stream, then outs
    //has already been connected to a file.
    //Postcondition: A dollar sign and the amount of money
    //recorded in the calling object have been sent to the output
    //stream outs.
    ...
```

一旦我们重载了插入（输出）运算符 <<，我们将不再需要成员函数 output，因此可以从

<< 的链式调用

<< 返回一个流

## 显示 11.7  << 作为运算符

```text
1  cout << "I have " << amount << " in my purse.\n";

3  means the same as

5  ((cout << "I have ") << amount) << " in my purse.\n";

7  and is evaluated as follows:

9  First evaluate (cout << "I have "), which returns cout:
10 ((cout << "I have ") << amount) << " in my purse.\n";

14 (cout << amount) << " in my purse.\n";

17 Then evaluate (cout << amount), which returns cout:
19 (cout << amount) << " in my purse.\n";

23 cout << " in my purse.\n";

26 Then evaluate cout << " in my purse.\n", which returns cout:
28 cout << " in my purse.\n";

32 cout;
```

我们的 Money 类定义。重载运算符 << 的定义与成员函数 output 非常相似。用概要形式表示，重载运算符的定义如下：

```cpp
ostream& operator <<(ostream& outs, const Money& amount)
{
    <This part is the same as the body of Money::output
     that is given in Display 11.3 (except that allCents
     is replaced with amount.allCents).>

    return outs;
}
```

<< 和 >> 返回引用

在之前关于重载运算符 << 的函数声明和定义中，还有一件事需要解释。返回类型 ostream& 中的 & 是什么意思？最简单的回答是：当一个运算符（或函数）返回流时，你必须在返回类型名称的末尾加上一个 &。这条简单规则允许你重载运算符 << 和 >>。然而，尽管这是一条有效的实用规则，能让你写出自己的类定义和程序，但它并不令人满意。你不需要知道 & 的真正含义，但如果我们解释一下，就会消除那条要求你添加 & 的规则中的一些神秘感。

返回引用

当你给返回类型的名称添加一个 & 时，你是在表示该运算符（或函数）返回一个引用。到目前为止我们看到的所有函数和运算符都返回值。然而，如果返回类型是流，你不能简单地返回流的值。对于流来说，流的值是整个文件或键盘或屏幕，返回这些东西可能没有意义。因此，你只想返回流本身，而不是流的值。当你给返回类型的名称添加一个 & 时，你是在表示该运算符（或函数）返回一个引用，这意味着你返回的是对象本身，而不是对象的值。

提取运算符 >> 的重载方式与我们为插入运算符 << 描述的方式类似。但是，对于提取（输入）运算符 >>，第二个参数将是接收输入值的对象，因此第二个参数必须是普通的按引用调用参数。用概要形式表示，重载提取运算符 >> 的定义如下：

```cpp
istream& operator >>(istream& ins, Money& amount)
{
    <This part is the same as the body of
    Money::input given in Display 11.3 (except that
    allCents is replaced with amount.allCents).>
    return ins;
}
```

重载运算符 << 和 >> 的完整定义在显示 11.8 中给出，我们再次重写了 Money 类。这一次我们重写类是为了重载运算符 << 和 >>，使我们能够将这些运算符用于 Money 类型的值。

## 重载 >> 和 <<

输入和输出运算符 >> 和 << 可以像任何其他运算符一样被重载。返回的值必须是流。返回值的类型必须在类型名称的末尾添加 & 符号。函数声明和函数定义的开头如下一页所示。有关示例，请参见显示 11.8。

```cpp
FUNCTION DECLARATIONS

class ClassName
{
public:
    ...

    friend istream& operator >>(istream& Parameter_1,
                                 ClassName& Parameter_2);

    friend ostream& operator <<(ostream& Parameter_3,
                                 const ClassName&
                                 Parameter_4);
    ...

DEFINITIONS

istream& operator >>(istream& Parameter_1,
                     ClassName& Parameter_2)
{
    ...
}
ostream& operator <<(ostream& Parameter_3,
                      const ClassName& Parameter_4)
{
    ...
```

## 显示 11.8  重载 << 和 >> *（第 1 部分，共 4 部分）*

```cpp
//Program to demonstrate the class Money
#include <iostream>
#include <fstream>
#include <cstdlib>
#include <cctype>
using namespace std;

//Class for amounts of money in U.S. currency.
class Money
{
public:
    friend Money operator +(const Money& amount1, const Money& amount2);
    friend Money operator -(const Money& amount1, const Money& amount2);
    friend Money operator -(const Money& amount);
```

> 这是我们在显示 11.6 中给出的 Money 类的改进版本。

> 尽管我们省略了显示 11.5 和 11.6 中的一些注释，但你应该将它们包含在程序中。

