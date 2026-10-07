
以下哪些是合法的？
`YourClass` `anObject`(42, 'A');
`YourClass` `anotherObject`;
`YourClass` `anotherObject`();
`anObject` = `YourClass`(99, 'B');
`anObject` = `YourClass`();
`anObject` = `YourClass`;

- 23. 你将如何修改显示 10.4 中 `DayOfYear` 类的定义，使其具有两个版本的（重载）构造函数？一个版本应该有一个 `int` 形式参数（一个用于月份，一个用于日期），并将私有成员变量设置为代表月份和日期的值。另一个版本应该没有形式参数，并将日期设置为 1 月 1 日。在两个构造函数中都不要使用构造函数初始化部分。

- 24. 重做之前的练习，但这次使用构造函数初始化部分来初始化每个构造函数中的所有成员函数。

# 10.3 抽象数据类型

我们都知道——《纽约时报》都知道——但我们假装不知道。

> 吉尼亚·伍尔夫，周一或周二

## 抽象数据类型

数据类型（例如 `int` 类型）具有某些特定的值，例如 0、1、–2 等。你倾向于将数据类型看作这些值，但对这些值的操作与值本身同样重要。如果没有这些操作，你无法对这些值做任何有意义的事。`int` 类型的操作包括 `+`、`–`、`*`、 `/` 以及其他几个运算符和预定义的库函数。一个数据类型由一组值以及定义在这些值上的 set 基本操作组成。

如果使用该类型的程序员无法访问值和操作如何实现的实现细节，则该数据类型被称为抽象数据类型（缩写为 ADT）。预定义类型（如 `int`）是抽象数据类型（ADT）。你不知道 `int` 类型的操作（如 `+` 和 `*`）是如何实现的。如果你知道，你将不会在任何 C++ 程序中使用这些信息。

程序员定义的类型（例如结构体类型和类类型）并不自动是 ADT。除非它们是以直观的方式定义的，这种方式使得程序员定义的类型易于理解且难以修改。避免这些问题的最佳方法是将你定义的所有数据类型都变为 ADT。在 C++ 中实现这一点的方法是使用类，但并不是每个类都是 ADT。要使类成为 ADT，你必须以特定的方式定义类，这就是下一个小节的主题。

### 用于产生抽象数据类型的类

类是你定义的一种类型，这与已经为你的值定义的类型（如 `int` 和 `char`）相对。类类型的值是其成员变量值的集合。例如，在显示 10.6 中 `double BankAccount` 类类型的值由两个 `double` 类型的值组成。为了方便参考，我们重复类定义（仅省略了注释）：

```cpp
class BankAccount{
public:
    BankAccount(int dollars, int cents, double rate);
    BankAccount(int dollars, double rate);
    BankAccount();
    void set(int dollars, int cents, double rate);
    void update();
    double getBalance();
    double getRate();
    void output(ostream& outs);
private:
    double balance;
    double interestRate;
    double fraction(double percent);
};
```

使用 `BankAccount` 类型的程序员不需要知道你是如何实现 `BankAccount::update` 的定义或任何其他成员函数的。我们使用的使用的成员 `BankAccount::update` 的函数定义如下：

```cpp
void BankAccount::update()
{
    balance = balance + fraction(interestRate) * balance;
}
```

然而，我们可以省去私有函数 `fraction`，并使用以下稍微复杂的实现来实现成员函数 `update`：

```cpp
void BankAccount::update()
{
    balance = balance + (interestRate / 100.0) * balance;
}
```

使用 `BankAccount` 类的程序员不需要担心我们使用哪种 `update` 的实现，因为两种实现的效果相同。

同样，使用 `BankAccount` 类的程序员不需要担心类值是如何实现的。我们选择将值实现为两个 `double` 值。如果 `VacationSavings` 是 `BankAccount` 类型的对象，那么 `VacationSavings` 的值由存储在以下两个成员变量中的两个 `double` 类型的值组成：

`vacationSavings.balance`
`vacationSavings.interestRate`

然而，我们不想把对象 `vacationSavings` 看作两个 `double` 类型的数字，例如 1.3546e + 2 和 4.5。你希望将 `vacationSavings` 的值看作单一条目

| 账户余额 | $135.46 |
| :--- | :--- |
| 利率 | 4.50% |

这就是我们 `BankAccount::output` 的实现，以这种格式写入类值。

## 抽象数据类型

由一个程序员设计并编写 ADT，而由其他程序员使用该 ADT。即使你是项目中运行的程序员，你也将一个较大的任务拆分成了两个较小的任务，这使得你的程序更易于设计和调试。

### 编程示例
类的替代实现

显示 10.7 包含了上一小节中讨论的 ADT 类 `BankAccount` 的变体实现。在这个版本中，银行账户的数据通过三个成员变量来实现：一个用于账户余额的美元部分，一个用于账户余额的角分部分，另一个用于利率。

请注意，显示 10.6 中的实现和显示 10.7 中的实现各有一个名为 `interestRate` 的成员变量，但在这两种实现中存储的值略有不同。如果账户按照 4.7% 的利率支付利息，那么在显示 10.6 的实现中（它与显示 10.5 的实现基本相同），`interestRate` 的值为 4.7。然而，在显示 10.7 的实现中，`interestRate` 的值将是 0.047。这种在显示 10.7 中所示的替代实现将利率存储为分数而非百分比数字。这种新实现的基本区别在于，当设置利率时，该函数立即将速率转换为分数。因此，在这个新的实现中，私有成员函数 `fraction` 被用于构造函数的定义，但在成员函数 `update` 的定义中不再需要，因为成员变量 `interestRate` 中的值已经转换成了分数。在旧的实现中（显示 10.5 和显示 10.6 所示），情况恰恰相反。在旧实现中，私有成员函数 `fraction` 未在构造函数的定义中使用，但在 `update` 的定义中使用。

尽管我们更改了 `BankAccount` 类的成员，但我们没有更改类定义中的任何内容。公共成员函数具有相同的函数声明，并且它们的行为与显示 10.6 中提供的旧版 ADT 类完全相同。例如，虽然这种新实现将如 4.7% 这样的百分比存储为分数 0.047，但成员函数 `getRate` 仍然返回值 4.7，就像显示 10.5 中的旧实现一样。同样，成员函数 `getBalance` 返回一个带有小数点的 `double` 类型单值，就像在显示 10.5 的旧实现中一样。尽管余额现在存储在两个 `int` 类型的成员变量中，而不是一个 `double` 类型的单一成员变量中（如旧版本所示）。

公共接口没有改变

### 显示 10.7 替代 BankAccount 类实现（4 部分中的第 1 部分）

```cpp
// 演示 BankAccount 类的替代实现。
#include <iostream>
#include <cmath>
using namespace std;
// 注意 BankAccount 的公共成员
// 其外观和行为与显示 10.6
// 完全一致
// 银行类：
class BankAccount{
public:
    BankAccount(int dollars, int cents, double rate);
    // 将账户余额初始化为 $dollars.cents 并
    // 将利率初始化为 rate 百分比。
    BankAccount(int dollars, double rate);
    // 将账户余额初始化为 $dollars.00 并
    // 将利率初始化为 rate 百分比。
    BankAccount();
    // 将账户余额初始化为 $0.00 并
    // 将利率初始化为 0.0%。
    void set(int dollars, int cents, double rate);
    // 后置条件：账户余额已设置为 $dollars.cents；
    // 利率已设置为 rate 百分比。
    void set(int dollars, double rate);
    // 后置条件：账户余额已设置为 $dollars.00；
    // 利率已设置为 rate 百分比。
    void update();
    // 后置条件：一年的单利已
    // 添加到账户余额中。
    double getBalance();
    // 返回当前账户余额。
    double getRate();
    // 以百分比形式返回当前的账户利率。
    void output(ostream& outs);
    // 前置条件：如果 outs 是文件输出流，则
    // outs 已经连接到一个文件。
    // 后置条件：账户余额和利率已 
    // 写入到输出流 outs 中。
private:
    int dollarsPart;
    int centsPart;
    double interestRate;
    // 以分数表示，例如，5.7% 对应 0.057
```

### 10.7 替代 BankAccount 类实现（4 部分中的第 2 部分）

```cpp
double fraction(double percent);
// 将百分比转换为分数。例如，fraction(50.3)
// 返回 0.503；
```

```cpp
double percent(double fractionValue);
// 将分数转换为百分比。例如，percent(0.503)
// 返回 50.3；
```

```cpp
int main()
```

```cpp
BankAccount account1(100, 2.3), account2;
cout << "account1 initialized as follows:\n"
account1.output(cout);
cout << "account2 initialized as follows:\n"
account2.output(cout);
```

### 10.7 替代 BankAccount 类实现（4 部分中的第 3 部分）

```cpp
double fraction(double percent) {
    return percent / 100.0;
}
double percent(double fractionValue) {
    return fractionValue * 100.0;
}
void BankAccount::update() {
    double balance = dollarsPart + centsPart / 100.0;
    balance = balance * interestRate;
    dollarsPart = (int)balance;
    centsPart = (int)((balance - dollarsPart) * 100.0);
}
```

### 显示 10.7 替代 BankAccount 类实现（4 部分中的第 4 部分）

```cpp
void BankAccount::set(int dollars, int cents, double rate) {
    if (dollars < 0 || cents < 0 || rate < 0) {
        cout << "Illegal values for money or rate.\n";
        return;
    }
    dollarsPart = dollars;
    centsPart = cents;
    interestRate = fraction(rate);
}
void BankAccount::set(int dollars, double rate) {
    if (dollars < 0 || rate < 0) {
        cout << "Illegal values for money or rate.\n";
        return;
    }
    dollarsPart = dollars;
    interestRate = fraction(rate);
}
```
