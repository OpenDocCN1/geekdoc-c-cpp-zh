
10. 首先，完成编程项目 6.12。用循环修改 `main` 函数，让用户决定创建多少个 `BoxProduce` 对象。每个盒子应包含三捆从列表中随机选择的水果或蔬菜：酸茄（tomatillo）、西兰花、番茄、奇异果和羽甘蓝。添加一个菜单让用户决定何时停止创建盒子。菜单允许用户对盒子中的随机物品进行替换。

如果盒子里包含酸茄，你希望赠送一份免费的绿色莎酱食谱。总共只有 5 张食谱。在 `BoxProduce` 类中添加一个静态成员变量来计算剩余食谱的数量，并将其初始化为 5。还要添加一个成员变量来指示盒子是否包含食谱，并修改输出函数，如果盒子包含食谱，则也打印“salsa verde recipe”。最后，在类内部添加逻辑，使得盒子如果包含至少一个酸茄，它就能自动获得一份食谱，直到所有食谱用完为止。注意，即使盒子里有多个酸茄，一个盒子也只能获得一份食谱。

通过从菜单创建包含酸茄的盒子来测试你的类，直到所有食谱用完。

# 运算符重载、友元与引用

## 8.1 运算符重载 322

- 重载基础 323
- 提示：构造函数可以返回一个对象 328
- 由 const 返回 329
- 重载一元运算符 332
- 作为成员函数的重载 332
- 提示：类对其所有对象的访问 335
- 重载函数调用 () 335

## 8.2 友元与自动转换 336

## 8.3 引用及更多 343

## 324 第8章 运算符重载、友元与引用

### 显示 8.1 运算符重载（部分 1/5）

```cpp
#include <iostream>
#include <cstdlib>
#include <cmath>
using namespace std;

// 用于处理美元货币账户的类
class Money {
public:
    Money();
    Money(double amount);
    Money(int dollars, int cents);
    Money(int dollars);
    double getAmount() const;
    int getDollars() const;
    int getCents() const;
    void input(); // 读取美元符号以及金额。
    void output() const;
private:
    int dollars; // 负数金额用负美元
                  // 来表示
    int cents; // 负分钱。负的 $4.50 表示为
                // -4 和 -50；

const Money operator +(const Money& amount1, const Money& amount2);
const Money operator =(const Money& amount1, const Money& amount2);

int main() {
    Money yourAmount, myAmount(10, 9);
    cout << "Enter an amount of money: ";
    yourAmount.input();
    cout << "Your amount is ";
    yourAmount.output() << endl;
    cout << "My amount is ";
    myAmount.output() << endl;
    cout << endl;

}
```

> 这是一个一元运算符，将在“重载一元运算符”小节中讨论。

> 关于返回类型中的 const 的解释，请参阅“按常量值返回”小节。

## 基础运算符重载 325

### 显示 8.1 运算符重载（部分 2/5）

```cpp
40  if (yourAmount == myAmount)
41      cout << "We have the same amounts.\n"
42  else
43      cout << "One of us is richer.\n";
```

```cpp
44  Money ourAmount = yourAmount + myAmount;
45      yourAmount.output(); cout << " + " + myAmount.output();
46      cout << " equals " + ourAmount.output(); cout << endl;
```

```cpp
47  Money diffAmount = yourAmount - myAmount;
48      yourAmount.output(); cout << " - " + myAmount.output();
49      cout << " equals " + diffAmount.output(); cout << endl;
```

注意我们需要使用访问器函数（accessor）和修改器函数（mutator）。

```cpp
52 const Money operator+(const Money& amount1, const Money& amount2)
53 {
54     int intCents1 = amount1.getCents() + amount1.getDollars() * 100;
55     int intCents2 = amount2.getCents() + amount2.getDollars() * 100;
56     int sumAllCents = intCents1 + intCents2;
57     int absAllCents = abs(sumAllCents); // Money 可以负数。
58     int finalDollars = absAllCents / 100;
59     int finalCents = absAllCents % 100;
```

```cpp
60 if (sumAllCents < 0)
61 {
62     finalDollars = -finalDollars;
63     finalCents = -finalCents;
64 }
```

> 如果对返回语句感到困惑，请查看“构造函数可以返回对象”。

```cpp
65 return Money(finalDollars, finalCents);
66 }
```

```cpp
67 // 使用 stdlib.h
68 const Money operator-(const Money& amount1, const Money& amount2)
69 {
70     int intCents1 = amount1.getCents() + amount1.getDollars() * 100;
71     int intCents2 = amount2.getCents() + amount2.getDollars() * 100;
72     int diffAllCents = intCents1 - intCents2;
73     int absAllCents = abs(diffAllCents);
74     int finalDollars = absAllCents / 100;
75     int finalCents = absAllCents % 100;
```

```cpp
76 if (diffAllCents < 0)
77 {
78     finalDollars = -finalDollars;
```

（续）

## 326 第8章 运算符重载、友元与引用

### 显示 8.1 运算符重载（部分 3/5）

| 行号 | 代码 |
| :--- | :--- |
| 79 | finalCents = -finalCents; |
| 80 | } |
| 81 | return Money(finalDollars, finalCents); |
| 82 | |

```cpp
bool operator ==(const Money& amount1, const Money& amount2)
{
    return (amount1.getDollars() == amount2.getDollars())
    && (amount1.getCents() == amount2.getCents());
}
```

```cpp
const Money operator-(const Money& amount)
{
    return Money(-amount.getDollars(), -amount.getCents());
}
```

```cpp
Money::Money() : dollars(0), cents(0){/* 函数体为空.*/}
```

```cpp
Money::Money(double amount) : dollars(dollarsPart(amount)), cents(centsPart(amount))/* 函数体为空*/
```

```cpp
Money::Money(int dollars) : dollars(dollars), cents(0){/* 函数体为空*/}
```

```cpp
// 使用 cstdlib
Money::Money(int dollars, int cents)
if ((dollars < 0 && cents > 0) || (dollars > 0 && cents < 0))
{
    cout << "Inconsistent data.\n";
    exit(1);
}
dollars = dollars;
cents = cents;
```

```cpp
double Money::getAmount() const
{
    return (dollars + cents * 0.01);
}
```

## 327 基础运算符重载

### 显示 8.1 运算符重载（部分 4/5）

```cpp
116 int Money::getDollars() const
117     return dollars;
```

```cpp
120 int Money::getCents() const
121     return cents;
```

```cpp
124 // 使用 iostream 和 cstdlib
125 void Money::output() const
126 {
127     int absDollars = abs(dollars);
128     int absCents = abs(cents);
129     if (dollars < 0 || cents < 0) // 处理 dollars == 0 或 cents == 0
130         cout << "$";
131     else
132         cout << '-';
133     cout << absDollars;
134
135     if (absCents >= 10)
136         cout << '.' << absCents;
137     else
138         cout << '0' << absCents;
140 // 使用 iostream 和 cstdlib
141 void Money::input()
142 {
    char dollarSign;
143     cin >> dollarSign; //
144     if (dollarSign != '$')
145         cout << "No dollar sign in input.\n";
146         exit(1);
150 double amountDouble;
151     cin >> amountDouble;
152     dollars = dollarsPart(amountDouble);
153     cents = centsPart(amountDouble);
154 }
```

```cpp
155 int Money::dollarsPart(double amount) const
// 定义的其余部分与显示7.2中的 BankAccount::dollarsPart 相同。
```

> 如需了解输入函数的更好定义，请参阅第7章的自测练习题3。

## 328 第8章 运算符重载、友元与引用

### 显示 8.1 运算符重载（部分 5/5）

```cpp
int Money::dollarsPart(double amount) const
// 定义的其余部分与显示7.2中的 BankAccount::dollarsPart 相同。
```

## 329 基础运算符重载

### 自测练习

- 1. 二元运算符与函数之间有什么区别？
- 2. 假设你希望重载运算符以使其适用于显示8.1中定义的 `Money` 类型。你需要在显示8.1中 `Money` 的定义中添加什么？
- 3. 是否可能使用运算符重载来改变整数的 `+` 行为？为什么或为什么不？

## 按常量引用

注意显示8.1中 `Money` 类重载运算符声明中的返回类型。例如，以下是显示8.1中重载运算符的声明：

```cpp
const Money operator+(const Money& amount1,
const Money& amount2);
```

本节解释了行头的 const。但在讨论第一个 const 之前，让我们确保理解了返回值的所有其他细节。因此，让我们先考虑重载运算符的声明或定义中都没有出现 const 的情况。假设声明如下：

```cpp
Money operator+(const Money& amount1, const Money& amount2);
```

# 330 第 8 章 运算符重载、友元与引用

当对象被返回时，例如 `(m1 + m2)`，其中 `m1` 和 `m2` 可能被用于调用成员函数，该成员函数可能会或不会改变对象 `(m1 + m2)` 中成员变量的值。例如：

```
(m1 + m2).output();
```

这是完全合法的。在这种情况下，它没有改变对象 `(m1 + m2)` 返回的类型。然而，如果我们在加运算符返回的类型之前省略 `const`，那么下面的代码将是合法的并且会改变对象 `(m1 + m2)` 成员变量的值：

```
(m1 + m2).input();
```

因此，对象是可以改变的，即使它们没有与任何变量关联。实现这一点的一种方法是注意对象具有成员变量，因此具有某些可以被更改的变量。

现在让我们假设一切都如显示 8.1 所示；也就是说，每个返回 `Money` 类型对象的运算符的返回类型之前都有 `const`。例如，这里是显示 8.1 中重载的加运算符的声明：

```
const Money operator+(const Money& amount1, const& amount2);
```

该行的第一个 `const` 是 `const` 修饰符的新用法。这被称为按常量值返回（或按 const 值返回或按常量值返回）。在这种情况下，`const` 修饰符意味着返回的对象不能被更改。例如，考虑以下代码：

```
Money m1(10.99), m2(23.57);
(m1 + m2).output();
```

调用 `output` 是完全合法的，因为它没有改变对象 `(m1 + m2)`。然而，在返回类型之前有 `const`，下面的代码将产生编译器错误信息：

```
(m1 + m2).input();
```

为什么你想要按常量值返回？它提供了一种自动的错误检查。当你构造 `(m1 + m2)` 时，你通常不想无意中改变它。在这种情况下，改变对象 `(m1 + m2)` 可能无关紧要，但如果返回的对象是现有对象的引用，这就会导致问题。引用在第 8.3 节中介绍。

起初，这种对改变对象的保护似乎保护过度了，因为你可以：

```
Money m3;
m3 = (m1 + m2);
```

并且你可能想改变 `m3`。没问题——以下内容是完全合法的：

```
m3 = (m1 + m2);
m3.input();
```

返回常量值

# 运算符重载

`m3` 和 `(m1 + m2)` 的值是两个不同的对象。赋值运算符并没有让 `m3` 等于 `(m1 + m2)`。相反，它将 `(m1 + m2)` 成员变量的值复制到 `m3` 的成员变量中。对于类对象，默认赋值运算符不会让两个对象变成同一个对象，它只是将成员变量的值从一个对象拷贝到另一个对象。

这种区别微妙但很重要。如果你能记住类变量和类类型的对象不是一件事，这可能帮助你理解细节。对象是类类型的一个值，可以存储在类类型的变量中，但变量和对象不是同一种东西。在代码中：

```
m3 = (m1 + m2);
```

变量 `m3` 及其它的值 `(m1 + m2)` 是不同的东西，就像 `n` 和 `5` 在以下代码中是不同的一样：

```
int n = 5;
```

或者

```
int n = (2 + 3);
```
