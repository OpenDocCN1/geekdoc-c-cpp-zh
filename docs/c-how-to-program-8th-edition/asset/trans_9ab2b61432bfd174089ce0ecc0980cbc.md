

```cpp
// Fig. 26.13: Withdrawal.h
// Definition of class Withdrawal that represents a withdrawal transaction
#ifndef WITHDRAWAL_H
#define WITHDRAWAL_H

#include "Transaction.h" // Transaction class definition

class Keypad; // forward declaration of class Keypad
class CashDispenser; // forward declaration of class CashDispenser

// class Withdrawal derives from base class Transaction
class Withdrawal : public Transaction
{
public:
   // member function overriding execute in base class Transaction
   virtual void execute(); // perform the transaction
private:
   // attributes
   double amount; // amount to withdraw
   Keypad &keypad; // reference to ATM's keypad
   CashDispenser &cashDispenser; // reference to ATM's cash dispenser
}; // end class Withdrawal

#endif // WITHDRAWAL_H
```

图 26.13 | 基于图 26.10 和图 26.11 的 Withdrawal 类头文件。

该实现使用了关键的编程概念，包括类、对象、封装、可见性、组合、继承和多态。代码注释充分，并符合你已学过的编码实践。掌握这段代码将是一次绝佳的综合实践体验。

## 26.3 节的自测练习题

- 26.4 UML 使用带 ________ 的箭头来表示泛化关系。
  - a) 实心填充箭头
  - b) 三角形空心箭头
  - c) 菱形空心箭头
  - d) 棍状箭头
- 26.5 判断以下陈述是否正确；如果错误，请解释原因：UML 要求为抽象类名和操作名加下划线。
- 26.6 编写一个 C++ 头文件，开始实现图 26.10 和图 26.11 中指定的 Transaction 类设计。确保根据 Transaction 类的关联关系包含私有引用。还要确保为派生类执行任务时必须访问的任何私有数据成员包含 public get 函数。

## 26.4 ATM 案例研究实现

本节展示我们在第 25 章和本章设计的 ATM 系统的完整可运行实现。我们按照第 25.4 节中识别这些类的顺序来考虑它们：

- ATM
- Screen
- Keypad
- CashDispenser
- DepositSlot
- Account
- BankDatabase
- Transaction
- BalanceInquiry
- Withdrawal
- Deposit

我们应用第 26.2 节和第 26.3 节中讨论的指导原则，根据我们在图 26.10 和图 26.11 的 UML 类图中对这些类建模的方式来编写这些类。为了开发类成员函数的定义，我们参考第 25.6 节中的活动图以及第 25.8 节中的通信图和顺序图。请注意，我们的 ATM 设计并未规定所有程序逻辑，也可能没有规定完成 ATM 实现所需的所有属性和操作。这是面向对象设计过程中的正常部分。在实现系统时，我们完善程序逻辑，并根据需要添加属性和行为，以构建第 25.3 节需求规范所指定的 ATM 系统。

最后，我们展示一个 C++ 程序（ATMCaseStudy.cpp），它启动 ATM 并让系统中的其他类投入使用。回想一下，我们正在开发 ATM 系统的第一个版本，它在个人计算机上运行，并使用计算机的键盘和显示器来模拟 ATM 的键盘和屏幕。我们也只模拟 ATM 出钞口和存款槽的动作。不过，我们尝试以实现该系统的方式，使得这些设备的真实硬件版本可以在代码无需重大更改的情况下集成。

### 26.4.1：类 ATM

类 ATM（图 26.14–26.15）表示整个 ATM。图 26.14 包含 ATM 类定义，它被包裹在 #ifndef、#define 和 #endif 预处理指令中，以确保该定义在程序中只被包含一次。我们稍后讨论第 6–11 行。第 16–17 行包含该类 public 成员函数的函数原型。图 26.11 的类图没有为类 ATM 列出任何操作，但我们现在在类 ATM 中声明一个 public 成员函数 run（第 17 行），它允许该类的外部客户（即 ATMCaseStudy.cpp）告诉 ATM 运行。我们还包含一个默认构造函数的函数原型（第 16 行），我们稍后讨论它。

```cpp
// ATM.h
// ATM class definition. Represents an automated teller machine.
#ifndef ATM_H
#define ATM_H

#include "Screen.h" // Screen class definition
#include "Keypad.h" // Keypad class definition
#include "CashDispenser.h" // CashDispenser class definition
#include "DepositSlot.h" // DepositSlot class definition
#include "BankDatabase.h" // BankDatabase class definition
class Transaction; // forward declaration of class Transaction

class ATM
{
public:
    ATM(); // constructor initializes data members
    void run(); // start the ATM
private:
    bool userAuthenticated; // whether user is authenticated
    int currentAccountNumber; // current user's account number
    Screen screen; // ATM's screen
    Keypad keypad; // ATM's keypad
    CashDispenser cashDispenser; // ATM's cash dispenser
    DepositSlot depositSlot; // ATM's deposit slot
    BankDatabase bankDatabase; // account information database

    // private utility functions
    void authenticateUser(); // attempts to authenticate user
    void performTransactions(); // performs transactions
    int displayMainMenu() const; // displays main menu

    // return object of specified Transaction derived class
    Transaction *createTransaction( int );
}; // end class ATM

#endif // ATM_H
```

![](img/bfd978e7e9b192bab46ec2a89e481263_1161_0.png)

**图 26.14 |** 类 ATM 的定义，它表示 ATM。（第 2 部分，共 2 部分。）

图 26.14 的第 19–25 行将该类的属性实现为私有数据成员。除了一个属性外，其余属性都由我们根据图 26.10–26.11 的类图确定。我们将图 26.11 中的 UML 布尔属性 userAuthenticated 实现为 C++ 中的 bool 数据成员（第 19 行）。第 20 行声明了一个在我们的 UML 设计中未出现的数据成员——一个 int currentAccountNumber，用于跟踪当前已认证用户的账号。我们很快会看到该类如何使用这个数据成员。

第 21–24 行创建对象来表示 ATM 的各个部分。回想图 26.10 的类图，类 ATM 与类 Screen、Keypad、CashDispenser 和 DepositSlot 具有组合关系，因此类 ATM 负责创建它们。第 25 行创建一个 BankDatabase，ATM 与之交互以访问和操作银行账户信息。[注意：如果这是一个真实的 ATM 系统，ATM 类将接收银行创建的现有数据库对象的引用。然而，在本实现中，我们只是模拟银行的数据库，因此类 ATM 创建与其交互的 BankDatabase 对象。] 第 6–10 行 #include 了 Screen、Keypad、CashDispenser、DepositSlot 和 BankDatabase 的类定义，以便 ATM 可以存储这些类的对象。

第 28–30 行和第 33 行包含该类用于执行任务的私有工具函数的函数原型。我们很快会看到这些函数如何为该类服务。成员函数 createTransaction（第 33 行）返回一个 Transaction 指针。为了在该文件中包含类名 Transaction，我们至少必须包含类 Transaction 的前向声明（第 11 行）。回想一下，前向声明告诉编译器某个类存在，但该类在别处定义。这里前向声明就足够了，因为我们使用 Transaction 指针作为返回类型——如果我们要创建或返回实际的 Transaction 对象，就需要 #include 完整的 Transaction 头文件。

### ATM 类成员函数定义

图 26.15 包含类 ATM 的成员函数定义。第 3–7 行 #include 了实现文件 ATM.cpp 所需的头文件。包含 ATM 头文件可让编译器确保该类的成员函数定义正确。这也允许成员函数使用该类的数据成员。

```cpp
 1   // ATM.cpp
 2   // Member-function definitions for class ATM.
 3   #include "ATM.h" // ATM class definition
 4   #include "Transaction.h" // Transaction class definition
 5   #include "BalanceInquiry.h" // BalanceInquiry class definition
 6   #include "Withdrawal.h" // Withdrawal class definition
 7   #include "Deposit.h" // Deposit class definition
 8
 9   // enumeration constants represent main menu options
10   enum MenuOption { BALANCE_INQUIRY = 1, WITHDRAWAL, DEPOSIT, EXIT };
11
12   // ATM default constructor initializes data members
13   ATM::ATM()
14      : userAuthenticated( false ), // user is not authenticated to start
15        currentAccountNumber( 0 ) // current account number to start
16   {
17      // empty body
18   } // end ATM default constructor
19
20   // start ATM
21   void ATM::run()
22   {
23      // welcome and authenticate user; perform transactions
24      while ( true )
25      {
26         // loop while user is not yet authenticated
27         while ( !userAuthenticated )
28         {
29            screen.displayMessageLine( "\nWelcome!" );
30            authenticateUser(); // authenticate user
31         } // end while
32   }
```

图 26.15 | ATM 类成员函数定义。（第 1 部分，共 4 部分。）

