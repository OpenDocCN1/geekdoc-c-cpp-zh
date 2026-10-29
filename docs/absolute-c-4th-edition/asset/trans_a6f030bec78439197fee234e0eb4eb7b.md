

# 显示 7.4 const 参数修饰符（第 2 部分，共 3 部分）

```
40  int dollarsPart(double amount) const;
41  int centsPart(double amount) const;
42  int round(double number) const;
43
44  double fraction(double percent) const;
45  //Converts a percentage to a fraction. For example, fraction(50.3) returns 0.503.
46  };
```

```
46  //Returns true if the balance in account1 is greater than that
47  //in account2. Otherwise returns false.
48  bool isLarger(const BankAccount& account1, const BankAccount& account2);
```

```
49  void welcome(const BankAccount& yourAccount);
```

```
50  int main()
51  {
52      BankAccount account1(6543.21, 4.5), account2;
53      welcome(account1);
54      cout << "Enter data for account 2:\n";
55      account2.input();
56      if (isLarger(account1, account2))
57          cout << "account1 is larger\n";
58      else
59          cout << "account2 is at least as large as account1.\n";
60
61      return 0;
62  }
```

```
63  bool isLarger(const BankAccount& account1, const BankAccount& account2)
64  {
65      return(account1.getBalance() > account2.getBalance());
66  }
```

```
67  void welcome(const BankAccount& yourAccount)
68  {
69      cout << "Welcome to our bank.\n"
70           << "The status of your account is:\n";
71      yourAccount.output();
72  }
```

```
73  //Uses iostream and cstdlib:
74  void BankAccount::output() const
75  <The rest of the function definition is the same as in Display 7.2.>
```

<Other function definitions are the same as in Display 7.2, except that const is added where needed to match the function declaration.>

# 显示 7.4 const 参数修饰符（第 3 部分，共 3 部分）

## 示例对话

```
Welcome to our bank.
The status of your account is:
Account balance: $6543.21
Rate: 4.5%
Enter data for account 2:
Enter account balance $100.00
Enter interest rate (NO percent sign): 10
account1 is larger.
```

## 内联函数

你可以在类的定义内给出成员函数的完整定义。这种定义称为内联函数定义。这些内联定义通常用于非常短的函数定义。显示 7.5 显示了显示 7.4 中的类重写为多个内联函数。

内联函数不仅仅是我们已经见过的那种成员函数定义的记法变体。编译器以特殊方式处理内联函数。内联函数声明的每个调用位置都会插入其代码。这节省了函数调用的开销。

在其他条件相同的情况下，内联函数应该更高效，因此通常比以通常方式定义的函数更可取。然而，其他条件很少，如果有的话，总是相等。内联函数的缺点是混合了类的接口和实现，因此违背了封装的原则。而且，正如通常的争论来回进行一样。

一般认为，只有非常短的函数定义才应定义为内联。对于长函数定义，内联版本实际上可能效率更低，因为大段代码会被频繁重复。除此一般规则外，你需要自行决定是否使用内联函数。

任何函数都可以定义为内联函数。要将非成员函数定义为内联，只需在函数声明和函数定义前放置关键字 inline。我们在本书中不会使用，也不会进一步讨论内联非成员函数。

## 自测练习

- 7. 重写显示 7.3 中给出的类 DayOfYear 的定义，使函数 getMonthNumber 和 getDay 以内联方式定义。

# 显示 7.5 内联函数定义

这是使用内联成员函数重写的显示 7.4。

```
```cpp
#include <iostream>
#include <cmath>
#include <cstdlib>
using namespace std;

class BankAccount
{
public:
    BankAccount(double balance, double rate);
    BankAccount(int dollars, int cents, double rate);
    BankAccount(int dollars, double rate);
    BankAccount();
    void update();
    void input();
    void output() const;

    double getBalance() const { return (accountDollars + accountCents*0.01); }
    int getDollars() const { return accountDollars; }
    int getCents() const { return accountCents; }
    double getRate() const { return rate; }

    void setBalance(double balance);
    void setBalance(int dollars, int cents);
    void setRate(double newRate);
private:
    int accountDollars; //of balance
    int accountCents; //of balance
    double rate;//as a percentage

    int dollarsPart(double amount) const { return static_cast<int>(amount); }
    int centsPart(double amount) const;
    int round(double number) const
    { return static_cast<int>(floor(number + 0.5)); }
    double fraction(double percent) const { return (percent/100.0); }
};
```
```

*内联函数没有进一步的定义。其他函数定义与显示 7.4 相同。*

![](img/9505fd46e120aa9c1406715936ff6251_282_0.png)

# 静态成员

有时你希望有一个变量被类的所有对象共享。例如，你可能希望有一个变量来计数特定成员函数被类的所有对象调用的次数。这种变量称为静态变量，可以用于对象之间通信或协调其行为。这种变量允许使用全局变量的一些优点，而不会打开真正的全局变量所带来的所有滥用大门。特别是，静态变量可以是私有的，这样只有类的对象可以直接访问它。

如果一个函数不访问任何对象的数据，但你希望该函数是类的成员，你可以使其成为静态函数。静态函数可以用通常的方式使用类的调用对象进行调用。然而，更常见且更清晰的做法是使用类名和作用域解析运算符调用静态函数，如以下示例：

```
Server::getTurn()
```

由于静态函数不需要调用对象，静态函数的定义不能使用任何依赖于调用对象的东西。静态函数定义不能使用任何非静态变量或非静态成员函数，除非该非静态变量或函数具有在定义中作为局部变量或以其他方式创建的对象作为调用对象。如果上一句话听起来难以理解，只需使用更简单的规则：静态函数的定义不能使用任何依赖于调用对象的东西。

显示 7.6 是一个演示程序，使用了静态变量和静态函数。请注意，静态变量由其声明开头的限定关键字 static 指示。还请注意，所有静态变量都按如下方式初始化：

```
int Server::turn = 0;
int Server::lastServed = 0;
bool Server::nowOpen = true;
```

这种初始化需要一点解释。每个静态变量都必须在类定义之外初始化。此外，静态变量不能被初始化超过一次。如显示 7.6 中所示，私有静态变量——事实上，所有静态变量——都在类之外初始化。这似乎与私有概念相矛盾。然而，类的作者预计会进行初始化，通常在与类定义相同的文件中。在这种情况下，使用类的任何程序员都不能初始化静态变量，因为静态变量不能被第二次初始化。

请注意，关键字 static 用于成员函数声明中，但在成员函数定义中未使用。

static variable

initializing
static
member
variables

# 显示 7.6 静态成员（第 1 部分，共 2 部分）

```
#include <iostream>
using namespace std;

class Server
{
public:
    Server(char letterName);
    static int getTurn();
    void serveOne();
    static bool stillOpen();
private:
    static int turn;
    static int lastServed;
    static bool nowOpen;
    char name;
};

int Server::turn = 0;
int Server::lastServed = 0;
bool Server::nowOpen = true;

int main()
{
    Server s1('A'), s2('B');
    int number, count;
    do
    {
        cout << "How many in your group? ";
        cin >> number;
        cout << "Your turns are: ";
        for (count = 0; count < number; count++)
            cout << Server::getTurn() << ' ';
        cout << endl;
        s1.serveOne();
        s2.serveOne();
    } while (Server::stillOpen());
    cout << "Now closing service.\n";
    return 0;
}

Server::Server(char letterName) : name(letterName)
{/*Intentionally empty*/}

int Server::getTurn()
{
    turn++;
    return turn;
}
```

Since getTurn is static, only static members can be referenced in here.

