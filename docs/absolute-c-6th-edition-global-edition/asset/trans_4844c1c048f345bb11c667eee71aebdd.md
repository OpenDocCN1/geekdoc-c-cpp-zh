

# 2020年杭州市区 各类高中招生 集中统一第一、二批招生录取学校分数线

| 序号 | 学校名称 | 第一批分数线 | 第二批分数线 |
|------|----------|-------------|-------------|
| 1 | 杭州第二中学（滨江校区） | 540 | - |
| 2 | 杭州学军中学（西溪校区） | 538 | - |
| 3 | 杭州高级中学（贡院校区） | 533 | - |
| 4 | 杭州第十四中学（凤起校区） | 530 | - |
| 5 | 杭州第四中学（下沙校区） | 524 | - |
| 6 | 萧山中学 | 521 | - |
| 7 | 浙江大学附属中学（玉泉校区） | 519 | - |
| 8 | 杭州师范大学附属中学 | 516 | - |
| 9 | 富阳中学 | 513 | - |
| 10 | 长河高级中学 | 510 | - |
| 11 | 杭州学军中学（紫金港校区） | 508 | - |
| 12 | 杭州第二中学（东河校区） | 505 | - |
| 13 | 杭州第十四中学（康桥校区） | 502 | - |
| 14 | 杭州高级中学（钱江校区） | 500 | - |
| 15 | 杭州第四中学（吴山校区） | 497 | - |
| 16 | 源清中学 | 494 | - |
| 17 | 杭州第七中学 | 491 | - |
| 18 | 西湖高级中学 | 488 | - |
| 19 | 余杭第二高级中学 | 485 | - |
| 20 | 临安中学 | 482 | - |

# 显示 8.2 将运算符重载为成员（第 2 部分，共 2 部分）

```
22 private;
23     int dollars; //A negative amount is represented as negative
                   //dollars and
24     int cents;   //negative cents. Negative $4.50 is represented as
                   //-4 and -50.
25
26     int dollarsPart(double amount) const;
27     int centsPart(double amount) const;
28     int round(double number) const;
29 };

29 int main( )
30 {
31     <If the main function is the same as in Display 8.1, then the screen dialogue
32     will be the same as shown in Display 8.1.>
33 }

34 const Money Money::operator +(const Money& secondOperand) const
35 {
36     int allCents1 = cents + dollars * 100;
37     int allCents2 = secondOperand.cents + secondOperand.dollars * 100;
38     int sumAllCents = allCents1 + allCents2;
39     int absAllCents = abs(sumAllCents); //Money can be negative.
40     int finalDollars = absAllCents / 100;
41     int finalCents = absAllCents % 100;
42     if (sumAllCents < 0)
43     {
44         finalDollars = -finalDollars;
45         finalCents = -finalCents;
46     }
47     return Money(finalDollars, finalCents);
48 }

49 const Money Money::operator -(const Money& secondOperand) const
50     <The rest of this definition is Self-Test Exercise 5.>

51 bool Money::operator ==(const Money& secondOperand) const
52 {
53     return ((dollars == secondOperand.dollars)
54         && (cents == secondOperand.cents));
55 }

56 const Money Money::operator -() const
57 {
58     return Money(-dollars, -cents);
59 }

60     <Definitions of all other member functions are the same as in Display 8.1.>
```

# 提示：类可以访问其所有对象

在定义成员函数或运算符时，您可以访问调用对象的任何私有成员变量（或函数）。然而，您被允许的比这更多。您可以访问正在定义的类中任何对象的任何私有成员变量（或私有成员函数）。

例如，考虑以下几行，它们开始了在显示 8.2 中为类 Money 定义加法运算符：

```
const Money Money::operator+ (const Money& secondOperand) const
{
    int allCents1 = cents + dollars*100;
    int allCents2 = secondOperand.cents + secondOperand.dollars
                    * 100;
}
```

在这种情况下，加法运算符被定义为成员运算符，因此函数体第一行的变量 cents 和 dollars 是调用对象的成员变量（碰巧是第一个操作数）。然而，按名称访问对象 secondOperand 的成员变量也是合法的，如以下行所示：

```
int allCents2 = secondOperand.cents + secondOperand.dollars * 100;
```

这是合法的，因为 secondOperand 是类 Money 的一个对象，并且这一行位于类 Money 的成员运算符的定义中。许多初学者错误地认为他们只能直接访问调用对象的私有成员，而没有意识到他们可以直接访问正在定义的类的所有对象。

# 自测练习

+   5. 完成显示 8.2 中成员二元运算符的定义。

# 重载函数应用 ( )

函数调用运算符 ( ) 必须作为成员函数重载。它允许您将类的对象用作函数。如果类 AClass 重载了函数应用运算符使其有一个类型为 int 的参数，并且 anObject 是 AClass 的一个对象，那么 anObject(42) 将调用重载的函数应用运算符 ( )，调用对象为 anObject，参数为 42。返回的类型可以是 void 或任何其他类型。

函数调用运算符 ( ) 的不寻常之处在于它允许任意数量的参数。因此，您可以定义函数调用运算符 ( ) 的多个重载版本。

# 陷阱：重载 &&、|| 和逗号运算符

为类型 bool 预定义的 && 和 || 版本使用短路求值。然而，当被重载时，这些运算符会执行完全求值。这与大多数程序员的预期完全相反，不可避免地会导致问题。最好根本不要重载这两个运算符。

逗号运算符也存在问题。在其正常使用中，逗号运算符保证从左到右求值。当被重载时则不保证这种顺序。逗号运算符是另一个最好避免重载的运算符。

# 8.2 友元函数和自动类型转换

> 相信你的朋友。

常见建议

友元函数是非成员函数，但具有成员函数的全部特权。在详细讨论友元函数之前，我们先讨论通过构造函数进行的自动类型转换，因为这有助于解释将运算符（或其他函数）重载为友元函数的一个优势。

# 用于自动类型转换的构造函数

如果您的类定义包含适当的构造函数，系统将自动执行某些类型转换。例如，如果您的程序包含类 Money 的定义，如显示 8.1 中给出或如显示 8.2 中给出，您可以在程序中使用以下内容：

```
Money baseAmount(100, 60), fullAmount;
fullAmount = baseAmount + 25;
fullAmount.output( );
```

输出将是

$125.60

系统知道 25 表示 $25.00 的原因是我们包含了一个接受单个 int 类型参数的构造函数。当系统看到表达式

```
baseAmount + 25
```

时，它首先检查运算符 + 是否已为 Money 类型的值和整数的组合重载。由于没有这样的重载，系统接下来会查看是否存在接受单个整数参数的构造函数。如果找到接受单个整数参数的构造函数，它就会使用该构造函数将整数 25 转换为 Money 类型的值。单参数构造函数说明 25 应转换为一个 Money 类型的对象，其成员变量 dollars 等于 25，其成员变量 cents 等于 0。换句话说，构造函数将 25 转换为表示 $25.00 的 Money 类型对象。 （构造函数的定义在显示 8.1 中。）

请注意，除非存在合适的构造函数，否则这种类型转换将无法工作。如果类 Money 不包含一个参数类型为 int（或其他数字类型，如 long 或 double）的构造函数，那么表达式

```
baseAmount + 25
```

将产生错误信息。

这些自动类型转换（由构造函数产生）在重载的数值运算符如 + 和 - 中似乎最常见且最有说服力。然而，这些自动转换以完全相同的方式适用于普通函数的参数、成员函数的参数以及其他重载运算符的参数。

# 陷阱：成员运算符和自动类型转换

当您将二元运算符重载为成员运算符时，两个参数不再对称。一个是调用对象，只有第二个“参数”才是真正的参数。这不仅不美观，而且也有非常实际的缺点。任何自动类型转换只适用于第二个参数。因此，例如，正如我们在前一小节中指出的，以下内容是合法的：

```
Money baseAmount(100, 60), fullAmount;
fullAmount = baseAmount + 25;
```

这是因为 Money 有一个参数类型为 int 的构造函数，因此值 25 将被视为 int 值并自动转换为 Money 类型的值。

然而，如果您将 + 重载为成员运算符（如显示 8.2 中），那么您就不能交换 + 的两个参数。以下内容是非法的：

```
fullAmount = 25 + baseAmount;
```

因为 25 不能是调用对象。int 值到 Money 类型的转换适用于参数，但不适用于调用对象。

