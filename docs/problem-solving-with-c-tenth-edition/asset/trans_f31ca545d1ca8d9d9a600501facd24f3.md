

# 本章小结

- 类的友元函数是一种普通函数，但它可以像成员函数一样访问类的私有成员。
- 如果你的每个类都有一整套访问器和修改器函数，那么让某个函数成为友元的唯一理由就是使友元函数的定义更简单、更高效，但这往往已经是一个足够的理由了。
- 不会被函数改变的类类型参数通常应该是常量参数。
- 运算符（如 `+` 和 `==`）可以被重载，以便用于你所定义的类类型的对象。
- 重载 `>>` 或 `<<` 运算符时，返回的类型应为流类型，并且必须是引用，这通过在返回类型名后附加 `&` 来表示。
- 数组的基类型可以是结构体类型或类类型。结构体或类可以将数组作为成员变量。
- **析构函数**是类的一种特殊成员函数。当类的对象超出作用域时，析构函数会被自动调用。析构函数的主要用途是将内存归还给自由存储区，以便该内存可以被重新使用。
- **复制构造函数**是一种构造函数，它只有一个参数，且该参数的类型与类相同。如果你定义了复制构造函数，那么每当函数返回类类型的值，以及每当参数被“代入”类类型的按值调用参数时，它都会被自动调用。任何使用指针和 `new` 运算符的类都应该有一个复制构造函数。
- 赋值运算符 `=` 可以为类重载，使其按你希望的方式对该类起作用。但是，它必须作为类的成员重载，不能作为友元函数重载。任何使用指针和 `new` 运算符的类都应该重载赋值运算符，以供该类使用。

## 自测练习答案

```
1. `bool before(DayOfYear date1, DayOfYear date2)
   {
       return ((date1.getMonth() < date2.getMonth())
            || (date1.getMonth() == date2.getMonth()
                && date1.getDay() < date2.getDay()));
   }`
```

```
class Money
{
public:
    friend Money subtract(Money amount1, Money amount2);
    //Precondition: amount1 and amount2 have values.
    //Returns amount1 minus amount2.
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

你还必须添加下面这个函数 subtract 的定义：

```
Money subtract(Money amount1, Money amount2)
{
    Money temp;
    temp.allCents = amount1.allCents
                 - amount2.allCents;
    return temp;
}
```

5. 这里显示的是类 Money 的修改后的定义。颜色标记的部分是新增的。为了节省篇幅，我们省略了一些注释，但程序清单 11.3 中显示的所有注释都应包含在这个定义中。

```
class Money
{
public:
    friend Money add(Money amount1, Money amount2);
    friend bool equal(Money amount1, Money amount2);
    Money(long dollars, int cents);
    Money(long dollars);
    Money();
    double getValue();
    void input(istream& ins);
    void output(ostream& outs);
    //Precondition: If outs is a file output stream, then
    //outs has already been connected to a file.
    //Postcondition: A dollar sign and the amount of money
    //recorded in the calling object has been sent to the
    //output stream outs.
```

```
void output();
//Postcondition: A dollar sign and the amount of money
//recorded in the calling object has been output to the
//screen.
```

```
private:
    long allCents;
};
```

你还必须添加下面这个名为 output 的函数的定义。（原来的 output 定义仍然保留，因此会有两个 output 的定义。）

```
void Money::output()
{
    output(cout);
}
```

下面这个更长的函数定义版本也同样有效：

```
//Uses cstdlib and iostream
void Money::output()
{
    long positiveCents, dollars, cents;
    positiveCents = labs(allCents);
    dollars = positiveCents/100;
    cents = positiveCents%100;

    if (allCents < 0)
        cout << "-$" << dollars << '.';
    else
        cout << "$" << dollars << '.';
    if (cents < 10)
        cout << '0';
    cout << cents;
}
```

你也可以重载成员函数 input，使得类似

```
purse.input();
```

的调用与

```
purse.input(cin);
```

含义相同。

当然，你还可以将这个增强功能与之前自测练习中的增强功能结合起来，得到一个高度改进的类 Money。

6. 如果用户输入 $-9.95（而不是 -$9.95），函数 input 会把“$”读作 oneChar 的值，把 -9 读作 dollars 的值，把“.”读作 decimalPoint 的值，把“9”和“5”分别读作 digit1 和 digit2 的值。这意味着它会将 dollars 设为 -9，将 cents 设为 95，因此所设金额相当于 −$9.00 加 0.95，即 −$8.05。发现这个问题的一种方法是检查 dollars 的值是否为负（因为 dollars 的值应当是一个绝对值）。为此，请将错误消息部分改写如下：

```
if (oneChar != '$' || decimalPoint != '.'
    || !isdigit(digit1) || !isdigit(digit2)
    || dollars < 0)  New
{
    cout << "Error illegal form for money input\n";
    exit(1);
}
```

这段代码对于 $−0.95 这种零美元的错误输入仍不会给出错误消息。然而，就我们目前所学的内容而言，对这种情况进行测试虽然肯定是可能的，但会显著使代码复杂化，并使其更难阅读。

7. #include <iostream>
using namespace std;
int main()
{
    int x;
    cin >> x;
    cout << x << endl;
    return 0;
}

如果编译器将带有前导 0 的输入解释为八进制数，那么对于输入数据 077，输出应为 63；如果编译器不将带有前导 0 的数据解释为八进制，则输出应为 77。

8. 与程序清单 11.3 中给出的版本相比，唯一的变化是在函数头部添加了 const 修饰符，因此定义如下：

```
double Money::getValue() const
{
    return (allCents * 0.01);
}
```

9. 成员函数 input 会改变其调用对象的值，因此如果你添加 const 修饰符，编译器将发出错误消息。

10. 相似之处：每次参数调用都会保护调用者的实参不被修改。不同之处：按值调用会复制调用者的实参，因此它比按常量引用调用占用更多内存。

11. 在 `const int x = 17;` 声明中，const 关键字向编译器保证，作者编写的代码不会改变 x 的值。

在 `int f() const;` 声明中，const 关键字向编译器保证，作者为实现函数 f 而编写的代码不会改变调用对象中的任何内容。

在 `int g(const A& x);` 声明中，const 关键字向编译器保证，类作者编写的代码不会改变为 x 传入的实参。

12. （二元）运算符（如 +、*、/ 等）与函数之间的区别在于它们的调用语法。在函数调用中，实参写在函数名后面的括号内；对于运算符，实参分别写在运算符的两侧。另外，在重载运算符的声明和定义中，必须使用保留字 operator。

13. 这里显示的是类 Money 的修改后的定义。颜色标记的部分是新增的。为了节省篇幅，我们省略了一些注释，但程序清单 11.5 中显示的所有注释都应包含在这个定义中。

```
class Money
{
public:
    friend Money operator +(const Money& amount1,
        const Money& amount2);
    friend bool operator ==(const Money& amount1,
        const Money& amount2);
    friend bool operator <(const Money& amount1,
        const Money& amount2);
    //Precondition: amount1 and amount2 have been given
    //values.
    //Returns true if amount1 is less than amount2;
    //otherwise, returns false.
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

你还必须添加下面这个重载运算符 < 的定义：

```
bool operator <(const Money& amount1,
    const Money& amount2)
{
    return (amount1.allCents < amount2.allCents);
}
```

