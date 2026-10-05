

## 第 8 章运算符重载、友元与引用

显示 8.4 << 作为一个运算符

等同于

```
(cout << "I have") << amount << " in my purse.\n";
```

并且求值如下：

首先求值 (cout << "I have")，它返回 cout：
((cout << "I have") << amount) << " in my purse.\n";
输出字符串 "I have"。

```
(cout << amount) << " in my purse.\n";
```

然后求值 (cout << amount)，它返回 cout：

```
(cout << amount) << " in my purse.\n";
输出 amount 的值。
```

```]

一旦我们重载了插入（输出）运算符 `<<`，我们就不再需要成员函数 `output` 了。重载运算符 `<<` 的定义与成员函数 `output` 非常相似。在形式上，重载运算符的定义如下所示：

```cpp
ostream& operator << (ostream& outputStream, const Money&)
{
    /* 这部分与显示 8.1 中给出的 Money::output 函数体相同
    （除了将 dollars 替换为 amount
    并将 cents 替换为 amount。） */
    return outputStream;
}
```

<< 和 >> 返回引用

提取运算符 `>>` 的重载方式与我们对插入运算符 `<<` 的描述是类似的（类比的）。然而，对于提取（输入）运算符 `>>`，第二个参数是接收输入值的对象，因此第二个参数必须是一个普通的引用传递参数。重载提取运算符 `>>` 的定义如下：

```cpp
istream& operator >> (istream& inputStream, Money& amount)
{
    /* 这部分与显示 8.1 中给出的 Money::input 函数体相同
    （除了将 dollars 替换为 amount
    并将 cents 替换为 amount。） */
    return inputStream;
}
```

重载运算符 `<<` 和 `>>` 的完整定义在显示 8.5 中，在其中我们重写了类，使得运算符 `<<` 和 `>>` 被重载，从而允许我们对 `Money` 类型使用这些运算符。请注意，在实际上你无法将 `>>` 或 `<<` 重载为成员函数。如果我们希望 `<<` 和 `>>` 按照我们想要的方式工作，那么第一个操作数（第一个参数）必须是 `cout` 或 `cin`（或某些 I/O 流）。但如果我们想将这些运算符重载为例如 `Money` 类的成员，那么第一个操作数将不得不是调用对象，这将导致你无法定义让 `>>` 和 `<<` 以正常方式行为的运算符。

### 显示 8.5 重载 << >> (第 1/3 部分)

```cpp
#include <iostream>
#include <cstdlib>
#include <cmath>
using namespace std;

// 用于美元金额的类
class Money
{
public:
    Money();
    Money(double amount);
    Money(int dollars, int cents);
    Money(int dollars);
    double getAmount() const;
    int getDollars() const;
    int getCents() const;
```

### 显示 8.5 重载 << >> (第 2/3 部分)

```cpp
friend const operator +(const Money& amount1, const Money& amount2);
friend const operator -(const Money& amount1, const Money& amount2);
friend bool operator==(const Money& amount1, const Money& amount2);
friend const Money operator << (ostream& outputStream, const Money& amount);
friend ostream& operator >> (istream& inputStream, Money&);

private:
    // 负数金额表示为负的美元和负的分分。
    // 负 $4.50 表示为 -4 和 -50。
    int dollars, cents;
    int dollarsPart(double amount) const;
    int centsPart(double amount) const;
    int round(double number) const;

int main() {
    Money yourAmount, myAmount(10, 9);
    cout << "Enter an amount of money: ";
    cin >> yourAmount;
    cout << "Your amount is " << yourAmount << endl;
    cout << "My amount is " << myAmount << endl;
    if (yourAmount == myAmount)
        cout << "We have the same amounts.\n";
    else
        cout << "One of us is richer.\n";
    Money diffAmount = yourAmount - myAmount;
    cout << yourAmount << " - " << myAmount << " equals " << diffAmount << endl;

    return 0;
}
```

<其他成员函数的定义在显示 8.1 中。其他重载运算符的定义在显示 8.3 中。>

### 显示 8.5 重载 << >> (第 3/3 部分)

```cpp
ostream& operator << (ostream& outputStream, const Money& amount)
{
    int absDollars = abs(amount.dollars);
    int absCents = abs(amount.cents);
    if (amount.dollars < 0 || amount.cents < 0)
        // 考虑到 dollars == 0 或 cents == 0
        outputStream << "$";
    else
        outputStream << '$';
    outputStream << absDollars;
    if (absCents >= 10)
        outputStream << '.' << absCents;
    else
        outputStream << ".00" << absCents;
    return outputStream;
}
```

```cpp
// 使用 iostream 和 cstdlib
istream& operator >> (istream& inputStream, Money& amount)
{
    char dollarSign;
    inputStream >> dollarSign; // 希望如此
    if (dollarSign != '$')
    {
        cout << "No dollar sign in Money input.\n";
        exit(1);
    }
    double amountAsDouble;
    inputStream >> amountAsDouble;
    amount.dollars = amount.dollarsPart(amountAsDouble);
    amount.cents = amount.centsPart(amountAsDouble);
    return inputStream;
}
```

示例对话

Enter an amount of money: $123.45
Your amount is $123.45
My amount is $10.09.
One of us is richer.
$123.45 - $10.09 equals $113.36

