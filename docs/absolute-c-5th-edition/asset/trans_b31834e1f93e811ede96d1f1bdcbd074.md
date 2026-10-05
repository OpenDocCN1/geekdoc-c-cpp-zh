

## 显示 7.4 参数修饰符（3 部分中的第3 部分）

```cpp
46 // 如果 account1 中的余额大于 account2 中的
47 // 则返回 true。否则返回 false。
48 bool isLarger(const BankAccount&account1, const BankAccount&account2);
49 void welcome(const BankAccount&accountYour);
50 int main() {
51     
52     BankAccount account1(6543.21, 4.5), account2;
53     welcome(account1);
54     cout << "Enter data for account 2:\n";
55     account2.input();
56     if (isLarger(account1, account2))
57         cout << "account1 is larger.\n";
58     else
59         cout << "account2 is at least as large as account1.\n";
60     return 0;
61 }
62 
63 bool isLarger(const BankAccount&account1, const BankAccount&account2)
64 {
65     return (account1.getBalance() ) > account2.getBalance();
66 }
67 void welcome(const BankAccount&accountYour)
68 
69 
70 
71 
72 
3 // 使用 iostream 和 cstdlib;
74 void BankAccount::output() const
75     <函数定义的其余部分与显示 7.2 相同.>
76 
77     <其他函数定义与显示 7.2 相同，只是在需要的地方添加了 const 
        以匹配函数声明.>
```

欢迎来到我们的银行。
您的账户状态为：
账户余额：$6543.21
利率：4.5%
请输入账户 2 的数据：
输入账户余额 $100.00
输入利率（无须百分比号）: 10
account1 较大。

## 第 7 章 构造函数和其他工具

### const 参数修饰符

如果你在引用传递参数的类型之前放置修饰符，则该参数被称为常量参数。当你添加 `const` 时：你是在告诉编译器该参数不应该被修改。如果你在函数定义中犯错，导致修改了常量参数，编译器将给出错误信息。对于类中不被函数修改的类类型参数，通常应该是常量引用传递参数，而不是值传递参数。

如果一个成员函数不改变其调用对象的值，你就可以通过在函数声明中添加 `const:` 修饰符来标记该函数。如果你在函数定义中犯错，导致修改了调用对象，且该函数被标记为 `const`，计算机将给出错误信息。`const` 位于函数声明的末尾，紧邻最后的分号之前。函数定义的头部也应该有一个 `const:`，以便与函数声明匹配。

## 示例

```cpp
class Sample
{
public:
    Sample();
    void input();
    void output( ) const;
private:
    int stuff;
    double morestuff;
};

int compare(const Sample& s1, const Sample& s2);
```

`const` 修饰符的使用是一个“全有全无”的命题。每当类参数或类的成员函数合适时，你都应该使用 `const` 修饰符。如果你没有在类适用的时候都使用 `const`，那么你就永远不应该为该类使用它。

## 自测题

- 4. 为什么在显示 7.2 中给出的 `BankAccount` 类的成员函数 `input` 的声明中，如接所示所示添加 `const` 修饰符是错误的？

```cpp
class BankAccount
{
public:
    void input( ) const;
...
```

## 自测题（续）

5. 值传递参数与常量引用传递参数之间有什么区别和相似之处？给出说明这些声明。

```cpp
void callByValue(int x);
void callByConstReference(const int& x);
```

6. 考虑以下定义：

```cpp
const int x = 17;
class A
{
public:
    A();
    A(int n);
    int f() const;
    int g(const int& x);
private:
    int i;
};
```

每个 `const` 关键字都是对编译器的承诺，编译器将执行该承诺。在每种情况下，承诺是什么？

## 内联函数

你可以在类的定义内部给出成员函数的完整定义。此类定义被称为内联函数定义。它们通常用于短函数定义。显示 7.5 展示了显示 7.4 中的类用多个内联函数重写后的类。

内联函数不仅仅是我们已经看到的某种表示写法的变体。编译器会以特殊方式处理内联函数。内联函数声明的代码会被插入到调用函数的地方。这节省了函数调用的开销。

在其他条件都相等的情况下，内联函数应该更高效，因此在通常情况下是首选的。然而，其他条件很少是完全相。内联函数的缺点是将接口和实现混合在一起，这违背了封装原则。

人们通常认为，只有短函数定义应该被定义为内联。内联版本实际上可能效率更，因为大段代码被重复。要决定是否使用内联，只需在声明前放置 `inline` 关键字即可。

## 显示 7.5 内联函数定义

```cpp
#include <iostream>
#include <cmath>
#include <cstdlib>
using namespace std;

class BankAccount
{
public:
    BankAccount(double b = 0.0, double r = 0.0) : balance(b), rate(r) {}
    void input() {
        cout << "Enter account balance: ";
        cin >> balance;
        cout << "Enter interest rate (NO percent sign): ";
        cin >> rate;
    }
    void output() const {
        cout << "The status of your account is:\n";
        cout << "Account balance: $" << balance << "\n";
        cout << "Rate: " << rate << "%\n";
    }
    double getBalance() const { return balance; }
private:
    double balance;
    double rate;
};
```

## 自测题

- 7. 重写 7.3 给出的 `DayOfYear` 定义，使得 `getMonthNumber` 和 `getDay` 成为内联函数。

## 静态成员

有时你希望有一个被所有对象共享的变量。例如，你可能希望有一个变量来统计成员函数被调用的次数。这种变量被称为静态变量，类对象可以使用它们进行相互通信或协调动作。静态变量允许使用全局变量的一些优点，而不会引发全局变量所面临的滥用。特别是，静态变量可以是私有的，这样只有类对象可以直接访问它。

如果一个成员函数不访问任何对象的数据，而你希望该函数是类的成员，你可以将其设为静态函数。静态函数可以使用普通方式调用，使用调用对象。然而，使用类名和作用域运算符调用静态函数更为常见且清晰，如下：

```
Server::getTurn()
```

由于静态函数不需要调用对象，静态函数的定义不能使用任何依赖于对象的内容。静态函数定义不能使用任何非静态变量或函数，除非非静态变量或函数在定义中创建了调用对象。如果这句话很难理解，请使用更简单的规则：静态函数的定义不能使用任何依赖于对象的内容。

7.6 是一个同时使用静态变量和静态函数的演示程序。注意静态变量在声明处由 `static` 关键字指示。

```cpp
int Server::turn = 0;
int Server::lastServed = 0;
bool Server::nowOpen = true;
```

初始化静态变量

这种初始化需要一些解释。每个静态变量必须在类定义之外进行初始化。此外，静态变量不能初始化多次。

