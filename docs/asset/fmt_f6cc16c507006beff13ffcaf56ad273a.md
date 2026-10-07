
# 第 10 章 / 定义类

```
BankAccount account1, account2; //问题--但可以修复

account1.BankAccount(10, 50, 2.0); //非常非法 account2.

BankAccount(500, 0, 4.5); //非常非法
```

正如注释所示，你不能在程序中这样放置这三行代码。第一行可以修改为可接受的形式，但两次对 `BankAccount` 构造函数的调用都是非法的。构造函数不能像调用普通成员函数那样被调用。尽管如此，我们很清楚在声明这三行代码时想要发生什么，而每当你按照如下方式声明对象 `account1` 和 `account2` 时，这一切会自动发生：

```
BankAccount account1(10, 50, 2.0), account2(500, 0, 4.5);
```

构造函数的定义方式与任何其他成员函数相同。例如，如果你通过添加上述描述的构造函数来修改类 `BankAccount` 的类的定义，你需要添加以下构造函数的定义：

```
BankAccount::BankAccount(int dollars, int cents, double rate)
{
    if ((dollars < 0) || (cents < 0) || (rate < 0))
    {
        cout << "非法的金额或利率值。\n";
    }
    balance = dollars + 0.01*cents;
    interestRate = rate;
}
```

由于类和构造函数的名称相同，`BankAccount` 名字在函数头中出现了两次：作用域运算符 `::` 之前的 `BankAccount` 是类名，而作用域运算符 `::` 之后的 `BankAccount` 是构造函数名。还要注意，在构造函数定义的头部中没有指定返回类型，而不是 `void` 类型。除了这些点外，构造函数可以像普通成员函数一样定义。

你可以重载像 `BankAccount::BankAccount` 这样的构造函数名，就像你可以重载任何其他函数名一样，例如我们在显示 10.5 中对 `BankAccount::set` 所做的那样。事实上，构造函数通常会被重载，以便对象可以用多种方式进行初始化。例如，在显示 10.6 中，我们重新定义了 `BankAccount` 类，使其拥有三个版本的构造函数。这种重新定义重载了构造函数名 `BankAccount`，使其可以有三个参数（正如我们刚刚讨论的）、两个参数或无参数。

例如，假设你在声明一个 `BankAccount` 类型的对象时只给出两个参数，如下例所示：

```
BankAccount account1(100, 2.3);
```

## 10.2 类

那么对象 `account1` 将被初始化，使得它代表一个余额为 $100.00、利率为 2.3% 的账户。

另一方面，如果在下例中没有提供任何参数，如下所示：
`BankAccount account2;`

那么该对象被初始化为代表一个余额为 $0.00、利率为 0.0% 的账户。注意，当构造函数没有参数时，在对象声明中不包含任何括号。以下是错误的：

```
BankAccount account2(); // 错误！不要这样做！
```

在某些情况下，一旦你拥有了一组良好的构造函数定义，就可以省略像 `set` 这样的成员函数。你可以使用显示 10.6 中的重载构造函数 `BankAccount` 来创建一个带有你选择的值的新 `BankAccount`。然而，调用构造函数会创建一个新对象，因此如果你想更改对象中的现有成员变量，应该使用修改函数。

## 显示 10.6 带有构造函数的类（3 部分中的 1 部分）

```cpp
//演示 BankAccount 类的程序。
#include <iostream>
using namespace std;
//银行账户类：
class BankAccount
{
public:
BankAccount(int dollars, int cents, double rate);
//初始化账户余额为 $dollars.cents 并
// 将利率设置为 rate 百比。
BankAccount(int dollars, int cents, double rate);
// 初始化账户余额为 $dollars.00 并
// 将利率设置为 rate 百比。
BankAccount();
// 将账户余额设置为 $0.00
// 并将利率设置为 rate 百比。
void set(int dollars, int cents, double rate);
// 后置条件：账户余额已设置为 $dollars.cents；
// 利率已设置为 rate 百比。
void set(int dollars, int cents, double rate);
// 后置条件：账户余额已设置为 $dollars.00。
// 利率已设置为 rate 百比。
void update(); // (续)
```

> 该 `BankAccount` 的定义是 10.5 中给出类的改进版本。

## 显示 10.6 带有构造函数的类（3 部分中的 2 部分）

```cpp
//后置条件：一年的单利已添加到
// 账户余额中。
double getBalance();
//返回当前余额。
double getRate();
//返回以百分比表示的当前利率。
void output(ostream& outs);
//前置条件：如果 outs 是文件流，那么
// outs 已经连接到文件。
//后置条件：账户余额和利率
// 已写入流 outs 中。
private:
double balance;
double interestRate;
double fraction(double percent);
int main() {
    // (此处由于提供的原始文本后续乱序重复，已翻译至逻辑结束点)
}
```

## 10.2 类

## 617

## 示例

```cpp
BankAccount::BankAccount(int dollars, int cents,
    double rate)
{
    if ((dollars < 0) || (cents < 0) || (rate < 0))
    {
        cout << "Illegal values for money or interest rate.\n";
        exit(1);
    }
}
```

注意，初始化值可以通过构造函数参数提供。

## 调用构造函数

在声明对象时，构造函数会被调用，但你在声明对象时必须为构造函数提供参数。也可以显式调用构造函数来为类变量创建一个新对象。

## 语法（当有构造函数时的对象声明）

```
ClassName ObjectName(ArgumentsForConstructor);
```

## 示例

```cpp
BankAccount account1(100, 2.3);
```

## 语法（用于显式构造函数调用）

```
Object = ConstructorName(ArgumentsForConstructor);
```

## 示例

```cpp
account1 = BankAccount(200, 3.5);
```

构造函数的名称必须与其所属类的名称相同。因此，在上述语法中，`ClassName` 和 `ConstructorName` 是同一个标识符。

如果对象是作为动态变量创建，也可以指定初始化器。

```cpp
BankAccount *myAcct; myAcct = BankAccount (300, 4.2);
```

## 第 10 章 / 定义类

每当你声明一个类类型的对象时，构造函数就会自动调用，但在对象声明之后也可以再次调用它。这允许你方便地设置对象的所有成员。技术细节如下：调用构造函数会创建一个带有新值的匿名对象。匿名对象是指尚未被任何变量命名的对象。该匿名对象可以赋值给具名对象（即类变量）。例如，下面这行代码调用了构造函数 `BankAccount`，创建了一个余额为 $999.99 且利率为 5% 的匿名对象。该匿名对象被赋值给对象 `account1`，使其代表一个余额为 $999.99 且利率为 5.9% 的账户。

```cpp
account1 = BankAccount(99, 99, 5, 5);
```

正如你从符号中推测的那样，构造函数的行为就像一个返回其类类型对象的函数。然而，由于调用构造函数总是创建一个新对象，而调用 `set` 函数仅仅是更改现有成员变量的值，因此调用 `set` 可能是比调用构造函数更改成员变量更有效的方法。因此，出于效率考虑，或者如果你需要在不创建新对象的情况下更改成员变量的值，你可能希望在类定义中同时拥有 `set` 成员函数和构造函数。

## 编程提示 始终包含默认构造函数

C++ 并不总是为你定义的类生成默认构造函数。如果你没有提供构造函数，编译器将生成一个无所事事的默认构造函数。相反，如果你为类提供了至少一个构造函数，那么 C++ 编译器将不再生成其他构造函数。每当你声明该类型的对象时，C++ 都会寻找合适的构造函数来使用。如果你在不使用构造函数参数的情况下声明对象，C++ 将寻找默认构造函数，如果你没有定义默认构造函数，则将无可用。

例如，假设你定义了如下类：

```cpp
class SampleClass {
public:
    SampleClass(int parameter1, double parameter2);
    void do_stuff();
private:
    int data1;
    double data2;
};
```

## 10.2 类

你应该能识别出以下声明 `SampleClass` 类型对象并调用该类构造函数的合法方法：

`SampleClass myObject(7, 7.77);`

然而，你可能会惊讶地发现以下内容是非合法的：
`SampleClass yourObject;`

编译器将其解释为包含一个对无参数构造函数的调用。你必须在 `yourObject` 的声明中添加两个参数，或者为无无参数调用的构造函数添加一个构造函数定义。

可以使用无参数调用的构造函数是默认构造函数，因为它适用于你不指定任何参数的情况下声明对象的默认情况。由于你很可能在不提供任何构造函数参数的情况下声明对象，因此你应该始终包含一个默认构造函数。以下修改后的 `SampleClass` 版本包含了默认构造函数：

```cpp
class SampleClass {
public:
    SampleClass(int parameter1, double parameter2);
    SampleClass() ← 默认构造函数
    void doStuff();
private:
    int data1;
    double data2;
};
```

如果你以这种方式精炼 `SampleClass` 类，那么之前的 `yourObject` 声明将是合法的。

如果你不希望构造函数初始化任何成员变量，你可以在实现它时只需给它一个空体。以下构造函数定义是完全合法的。它在调用时什么都不做，以让编译器满意：

```cpp
SampleClass::SampleClass() {
    // 什么都不做
}
```

注意，如果使用 `new` 运算符将类创建为动态变量，则调用默认构造函数。

## 陷阱 无参数构造函数

如果名为 `BankAccount` 的类的构造函数有两个形式参数，你如下所示声明对象并调用构造函数：

```cpp
BankAccount account1(100, 2.3);
```

## 第 10 章 / 定义类

每当你声明一个类类型的对象时，构造函数就会自动调用，但在对象声明之后也可以再次调用它。这允许你方便地设置对象的所有成员。技术细节如下：调用构造函数会创建一个带有新值的匿名对象。匿名对象是指尚未被任何变量命名的对象。该匿名对象可以赋值给具名对象（即类变量）。例如，下面这行代码调用了构造函数 `BankAccount`，创建了一个余额为 $999.99 且利率为 5% 的匿名对象。该匿名对象被赋值给对象 `account1`，使其代表一个余额为 $999.99 且利率为 5.9% 的账户。

```cpp
account1 = BankAccount(99, 99, 5, 5);
```

正如你从符号中推测的那样，构造函数的行为就像一个返回其类类型对象的函数。然而，由于调用构造函数总是创建一个新对象，而调用 `set` 函数仅仅是更改现有成员变量的值，因此调用 `set` 可能是比调用构造函数更改成员变量更有效的方法。因此，出于效率考虑，或者如果你需要在不创建新对象的情况下更改成员变量的值，你可能希望在类定义中同时拥有 `set` 成员函数和构造函数。

## 无参数构造函数

如果名为 `BankAccount` 的类的构造函数有两个形式参数，你如下所示声明对象并调用构造函数：

```cpp
BankAccount account1(100, 2.3);
```

然而，如果你想使用无参数构造函数，如下所示声明对象：

```cpp
BankAccount account1;
```

（问题是这种语法声明了一个名为 `account1` 的返回 `BankAccount` 对象的函数。）

## C++11 中的成员初始化和构造函数委托

C++11 支持一种在大多数面向对象语言中存在的成员初始化功能。该功能允许你为成员变量设置默认值。当创建对象时，成员变量会自动初始化为指定值。考虑以下 `Coordinate` 类的定义和实现：

```cpp
class Coordinate {
public:
    Coordinate();
    Coordinate(int x);
    Coordinate(int x, int y);
    int getX();
    int getY();
private:
    int x=1;
    int y=2;
};
Coordinate::Coordinate() {}
Coordinate::Coordinate(int xVal) : x(xVal) {}
Coordinate::Coordinate(int xVal, int yVal) : x(xVal), y(yVal) {}
int Coordinate::getX() {
    return x;
}
int Coordinate::getY() {
    return y;
}
```

如果我们创建一个 `Coordinate` 对象，成员变量 `x` 将默认被设置为 1，成员变量 `y` 将默认设置为 2。如果我们调用显式设置变量的构造函数，这些值可以被覆盖。在下面的代码段中，`c1` 的 `x` 和 `y` 默认值被设置，但对于 `c2`，只设置了 `y` 的默认值因为 `x` 被设置为输入参数：

```cpp
Coordinate c1, c2(120);
cout << c1.getX() << " " << c1.getY() << endl; // 输出 1 2
cout << c2.getX() << " " << c2.getY() << endl; // 输出 120 2
```

C++11 的一个相关功能是构造函数委托。简单来说，这允许一个构造函数调用另一个构造函数。例如，我们可以修改默认构造函数的实现，使其调用带有两个参数的构造函数：

```cpp
Coordinate::Coordinate() : Coordinate(99,99) {}
```

由 `Coordinate c1` 定义的对象将调用默认构造函数，该构造函数转而调用将 `x` 设置为 99 且 `y` 设置为 99 的构造函数。

## 自测练习

- 22. 假设你的程序包含以下类定义（以及成员函数的定义）：

```cpp
class YourClass {
public:
    YourClass(int newInfo, char moreNewInfo);
    YourClass();
    void doStuff();
private:
    int information;
    char moreInformation;
};
```
