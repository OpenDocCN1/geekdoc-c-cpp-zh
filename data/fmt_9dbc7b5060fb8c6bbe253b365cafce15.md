
**Fig. E.14** | `BankDatabase` class member-function definitions. (Part 3 of 3.)

`Account` 构造函数有四个参数——账号、分配给账号的 PIN、初始可用余额和初始总余额。

请回顾类 `BankDatabase` 在类 `ATM` 与实际包含用户账户信息的 `Account` 对象之间充当中间人。因此，类 `BankDatabase` 的成员函数只不过是调用当前 `ATM` 用户所属 `Account` 对象的相应成员函数。

我们包含私有工具函数 `getAccount`（第 18–29 行），以允许 `BankDatabase` 获取指向 `vector` `accounts` 中特定 `Account` 的指针。为了定位用户的 `Account`，`BankDatabase` 将 `accounts` 中每个元素的成员函数 `getAccountNumber` 返回的值与指定的账号进行比较，直到找到匹配项。第 21–26 行遍历 `accounts` 向量。如果当前 `Account`（即 `accounts[ i ]`）的账号等于参数 `accountNumber` 的值，则该成员函数立即返回当前 `Account` 的地址（即指向当前 `Account` 的指针）。如果没有账号与给定的账号匹配，则第 28 行返回 `NULL`。请注意，该成员函数必须返回指针而不是引用，因为返回值可能为 `NULL`——引用不能为 `NULL`，但指针可以。

请注意，向量函数 `size`（在第 21 行的循环继续条件中调用）以类型 `size_t` 的值返回向量中的元素个数（通常为 `unsigned int`）。因此，我们也将控制变量 `i` 声明为类型 `size_t`。在某些编译器上，将 `i` 声明为 `int` 会导致编译器发出警告消息，因为循环继续条件会比较有符号值（即 `int`）和无符号值（即类型为 `size_t` 的值）。

成员函数 `authenticateUser`（第 33–44 行）证明或否定 `ATM` 用户的身份。此函数以用户指定的账号和用户指定的 PIN 作为参数，并指示它们是否与数据库中某个 `Account` 的账号和 PIN 匹配。第 37 行调用工具函数 `getAccount`，该函数返回指向账号为 `userAccountNumber` 的 `Account` 的指针，或返回 `NULL` 以指示 `userAccountNumber` 无效。我们将 `userAccountPtr` 声明为 `const` 指针，因为一旦该成员函数将此指针指向用户的 `Account`，指针就不应再改变。如果 `getAccount` 返回指向 `Account` 对象的指针，第 41 行返回该对象 `validatePIN` 成员函数返回的 `bool` 值。请注意，`BankDatabase` 的 `authenticateUser` 成员函数本身并不执行 PIN 比较——而是将其转发给 `Account` 对象的 `validatePIN` 成员函数执行。`Account` 成员函数 `validatePIN` 返回的值指示用户指定的 PIN 是否与用户 `Account` 的 PIN 匹配，因此成员函数 `authenticateUser` 只是将此值返回给类的客户端（即 `ATM`）。

`BankDatabase` 信任 `ATM` 在允许用户执行交易之前调用成员函数 `authenticateUser` 并收到 `true` 的返回值。`BankDatabase` 还信任 `ATM` 创建的每个 `Transaction` 对象都包含当前已认证用户的有效账号，并且该账号作为参数 `userAccountNumber` 传递给剩余的 `BankDatabase` 成员函数。因此，成员函数 `getAvailableBalance`（第 47–51 行）、`getTotalBalance`（第 54–58 行）、`credit`（第 61–65 行）和 `debit`（第 68–72 行）只需使用工具函数 `getAccount` 获取指向用户 `Account` 对象的指针，然后使用此指针在用户的 `Account` 对象上调用适当的 `Account` 成员函数。我们知道这些成员函数中对 `getAccount` 的调用永远不会返回 `NULL`，因为 `userAccountNumber` 必须引用一个已存在的 `Account`。请注意，`getAvailableBalance` 和 `getTotalBalance` 返回相应 `Account` 成员函数返回的值。另请注意，`credit` 和 `debit` 只是将参数 `amount` 转发给它们调用的 `Account` 成员函数。

## E.9 Class `Transaction`

类 `Transaction`（图 E.15–E.16）是一个抽象基类，表示 `ATM` 交易的概念。它包含派生类 `BalanceInquiry`、`Withdrawal` 和 `Deposit` 的共同特征。图 E.15 扩展了在第 13.10 节中首次开发的 `Transaction` 头文件。第 13、17–19 行和第 22 行包含类的构造函数和四个成员函数的函数原型，我们稍后会讨论。第 15 行定义了一个空体的虚析构函数——这使得所有派生类析构函数都变为虚函数（即使由编译器隐式定义），并确保通过基类指针删除时动态分配的派生类对象能被正确销毁。第 24–26 行声明类的私有数据成员。请回顾图 13.29 的类图，类 `Transaction` 包含一个属性 `accountNumber`（在第 24 行实现），它指示 `Transaction` 涉及的账号。我们从图 13.28 中建模的类 `Transaction` 的关联派生出数据成员 `screen`（第 25 行）和 `bankDatabase`（第 26 行）——所有交易都需要访问 `ATM` 的屏幕和银行的数据库，因此我们将对 `Screen` 和 `BankDatabase` 的引用作为类 `Transaction` 的数据成员包含在内。正如你很快会看到的，`Transaction` 的构造函数初始化这些引用。请注意，第 6–7 行的前向声明表示头文件包含对类 `Screen` 和 `BankDatabase` 对象的引用，但这些类的定义位于头文件之外。

```cpp
// Transaction.h
// Transaction abstract base class definition.
#ifndef TRANSACTION_H
#define TRANSACTION_H
class Screen; // forward declaration of class Screen
class BankDatabase; // forward declaration of class BankDatabase
```

**Fig. E.15** | `Transaction` class definition. (Part 1 of 2.)

```cpp
class Transaction
{
public:
    // constructor initializes common features of all Transactions
    Transaction( int, Screen &, BankDatabase & );
    virtual ~Transaction() { } // virtual destructor with empty body
    int getAccountNumber() const; // return account number
    Screen &getScreen() const; // return reference to screen
    BankDatabase &getBankDatabase() const; // return reference to database
    // pure virtual function to perform the transaction
    virtual void execute() = 0; // overridden in derived classes
private:
    int accountNumber; // indicates account involved
    Screen &screen; // reference to the screen of the ATM
    BankDatabase &bankDatabase; // reference to the account info database
}; // end class Transaction
#endif // TRANSACTION_H
```

**Fig. E.15** | `Transaction` class definition. (Part 2 of 2.)

```cpp
// Transaction.cpp
// Member-function definitions for class Transaction.
#include "Transaction.h" // Transaction class definition
#include "Screen.h" // Screen class definition
#include "BankDatabase.h" // BankDatabase class definition
// constructor initializes common features of all Transactions
Transaction::Transaction( int userAccountNumber, Screen &atmScreen,
    BankDatabase &atmBankDatabase )
    : accountNumber( userAccountNumber ),
      screen( atmScreen ),
      bankDatabase( atmBankDatabase )
{
    // empty body
} // end Transaction constructor
// return account number
int Transaction::getAccountNumber() const
{
    return accountNumber;
} // end function getAccountNumber
// return reference to screen
Screen &Transaction::getScreen() const
{
    return screen;
} // end function getScreen
```

**Fig. E.16** | `Transaction` class member-function definitions. (Part 1 of 2.)

```cpp
// return reference to bank database
BankDatabase &Transaction::getBankDatabase() const
{
    return bankDatabase;
} // end function getBankDatabase
```

**图 E.16** | `Transaction` 类成员函数定义。（第 2 部分，共 2 部分。）

类 `Transaction` 有一个构造函数（在图 E.15 的第 13 行声明，并在图 E.16 的第 8–15 行定义），它接受当前用户的账号以及对 `ATM` 屏幕和银行数据库的引用作为参数。因为 `Transaction` 是一个抽象类，所以这个构造函数永远不会被直接调用来实例化 `Transaction` 对象。相反，`Transaction` 派生类的构造函数将使用基类初始化器语法调用此构造函数。

类 `Transaction` 有三个公共的 `get` 函数——`getAccountNumber`（在图 E.15 的第 17 行声明，并在图 E.16 的第 18–21 行定义）、`getScreen`（在图 E.15 的第 18 行声明，并在图 E.16 的第 24–27 行定义）以及 `getBankDatabase`（在图 E.15 的第 19 行声明，并在图 E.16 的第 30–33 行定义）。`Transaction` 派生类从 `Transaction` 继承这些成员函数，并使用它们来访问类 `Transaction` 的私有数据成员。

类 `Transaction` 还声明了一个纯虚函数 `execute`（图 E.15 的第 22 行）。为此成员函数提供实现没有意义，因为通用事务无法执行。因此，我们将此成员函数声明为纯虚函数，并强制每个 `Transaction` 派生类提供自己的具体实现来执行该特定类型的事务。

## E.10 类 `BalanceInquiry`

类 `BalanceInquiry`（图 E.17–E.18）派生自抽象基类 `Transaction`，表示余额查询 `ATM` 事务。`BalanceInquiry` 本身没有数据成员，但它继承了 `Transaction` 数据成员 `accountNumber`、`screen` 和 `bankDatabase`，这些数据成员可通过 `Transaction` 的公共 `get` 函数访问。请注意，第 6 行 `#include` 了基类 `Transaction` 的定义。`BalanceInquiry` 构造函数（在图 E.17 的第 11 行声明，并在图 E.18 的第 8–13 行定义）接受与 `Transaction` 数据成员对应的参数，并简单地使用基类初始化器语法（图 E.18 的第 10 行）将它们转发给 `Transaction` 的构造函数。图 E.17 的第 12 行包含成员函数 `execute` 的函数原型，这需要表明有意重写基类同名纯虚函数。

类 `BalanceInquiry` 重写 `Transaction` 的纯虚函数 `execute` 以提供具体实现（图 E.18 的第 16–37 行），该实现执行余额查询所涉及的步骤。第 19–20 行通过调用从基类 `Transaction` 继承的成员函数获取对银行数据库和 `ATM` 屏幕的引用。第 23–24 行通过调用 `bankDatabase` 的成员函数 `getAvailableBalance` 获取所涉及账户的可用余额。请注意，第 24 行使用继承的成员函数 `getAccountNumber` 获取当前用户的账号，然后将其传递给 `getAvailableBalance`。第 27–28 行检索当前用户账户的总余额。第 31–36 行在 `ATM` 屏幕上显示余额信息。请回忆 `displayDollarAmount` 接受一个 `double` 参数并将其格式化为美元金额输出到屏幕。例如，如果用户的 `availableBalance` 为 700.5，第 33 行输出 `$700.50`。请注意，第 36 行插入一个空行输出，以将余额信息与后续输出（即类 `ATM` 在执行 `BalanceInquiry` 后重复的主菜单）分隔开。

```cpp
// BalanceInquiry.h
// BalanceInquiry class definition. Represents a balance inquiry.
#ifndef BALANCE_INQUIRY_H
#define BALANCE_INQUIRY_H
#include "Transaction.h" // Transaction class definition
class BalanceInquiry : public Transaction
{
public:
    BalanceInquiry( int, Screen &, BankDatabase & ); // constructor
    virtual void execute(); // perform the transaction
}; // end class BalanceInquiry
#endif // BALANCE_INQUIRY_H
```

**图 E.17** | `BalanceInquiry` 类定义。

```cpp
// BalanceInquiry.cpp
// Member-function definitions for class BalanceInquiry.
#include "BalanceInquiry.h" // BalanceInquiry class definition
#include "Screen.h" // Screen class definition
#include "BankDatabase.h" // BankDatabase class definition
// BalanceInquiry constructor initializes base-class data members
BalanceInquiry::BalanceInquiry( int userAccountNumber, Screen &atmScreen,
    BankDatabase &atmBankDatabase )
    : Transaction( userAccountNumber, atmScreen, atmBankDatabase )
{
    // empty body
} // end BalanceInquiry constructor
// performs transaction; overrides Transaction's pure virtual function
void BalanceInquiry::execute()
{
    // get references to bank database and screen
    BankDatabase &bankDatabase = getBankDatabase();
    Screen &screen = getScreen();
    // get the available balance for the current user's Account
    double availableBalance =
```
