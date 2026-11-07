
当类 A 的头文件 #include 类 B 的头文件，而类 B 的头文件又 #include 类 A 的头文件时，就会发生循环 #include。有些预处理器无法解析这样的 #include 指令，从而导致编译错误。例如，如果类 A 只使用对类 B 对象的引用，那么类 A 头文件中的 #include 可以替换为类 B 的前向声明，以防止循环包含。

```cpp
// Fig. 26.6: Withdrawal.h
// Definition of class Withdrawal that represents a withdrawal transaction
#ifndef WITHDRAWAL_H
#define WITHDRAWAL_H

class Screen;        // forward declaration of class Screen
class Keypad;        // forward declaration of class Keypad
class CashDispenser; // forward declaration of class CashDispenser
class BankDatabase;  // forward declaration of class BankDatabase

class Withdrawal
{
private:
   // attributes
   int accountNumber; // account to withdraw funds from
   double amount;     // amount to withdraw

   // references to associated objects
   Screen &screen;             // reference to ATM’s screen
   Keypad &keypad;             // reference to ATM’s keypad
   CashDispenser &cashDispenser; // reference to ATM’s cash dispenser
   BankDatabase &bankDatabase; // reference to the account info database
}; // end class Withdrawal

#endif // WITHDRAWAL_H
```

**图 26.6** | *使用前向声明代替 #include 指令。*

- 5. 使用图 26.1 第三栏中的操作来编写该类成员函数的函数原型。如果我们尚未为某个操作指定返回类型，则将该成员函数声明为返回类型 `void`。参考图 6.22–6.25 的类图来声明任何必要的参数。例如，在类 `Withdrawal` 中添加公共操作 `execute`（其参数列表为空），会得到图 26.7 第 15 行中的原型。*[注意：当我们在第 26.4 节实现完整的 ATM 系统时，会在 .cpp 文件中编写成员函数的定义。]*

![](img/bfd978e7e9b192bab46ec2a89e481263_1152_0.png)

## 软件工程观察 26.1

> *一些 UML 建模工具可以将基于 UML 的设计转换为 C++ 代码，从而显著加快实现过程。有关这些“自动”代码生成器的更多信息，请参阅我们在 www.deitel.com/UML/ 的 UML 资源中心。*

到此结束我们对从 UML 图生成类头文件基础知识的讨论。在第 26.3 节中，我们将演示如何修改头文件以融入面向对象的继承概念。

一个额外的 Transaction 派生类，它用适合新交易类型的版本重写 execute 成员函数。我们只需对系统代码做最小改动，就能允许用户从主菜单中选择新交易类型，并让 ATM 实例化并执行新派生类的对象。ATM 可以使用当前代码执行新类型的交易，因为它以相同方式执行所有交易。

正如你在本章前面所学到的，像 Transaction 这样的抽象类是你从不打算实例化对象的类。抽象类只是为其继承层次中的派生类声明共同的属性和行为。类 Transaction 定义了“交易”这一概念的含义：具有账号并执行。你可能会想，如果 execute 缺少具体实现，我们为什么还要在类 Transaction 中包含私有虚成员函数 execute。从概念上讲，我们包含这个成员函数，因为它是所有交易的定义性行为——执行。从技术上讲，我们必须在基类 Transaction 中包含成员函数 execute，以便 ATM（或任何其他类）可以通过 Transaction 指针或引用多态地调用每个派生类重写的该函数版本。

## Withdrawal 和 Deposit 类的附加属性

派生类 BalanceInquiry、Withdrawal 和 Deposit 从基类 Transaction 继承属性 accountNumber，但类 Withdrawal 和 Deposit 包含附加属性 amount，以区别于类 BalanceInquiry。类 Withdrawal 和 Deposit 需要这个附加属性来存储用户希望取出或存入的金额。类 BalanceInquiry 不需要这样的属性，只需要账号即可执行。尽管三个 Transaction 派生类中有两个共享此属性，我们并不把它放在基类 Transaction 中——我们只把所有派生类共有的特征放在基类中，这样派生类就不会继承不必要的属性（和操作）。

## 融入 Transaction 层次结构的类图

图 26.10 展示了我们模型的更新类图，它融入了继承并引入了类 Transaction。我们对类 ATM 和类 Transaction 之间的关联建模，以表明 ATM 在任何给定时刻要么正在执行交易，要么没有执行交易（即系统中同一时间存在零个或一个 Transaction 类型的对象）。因为 Withdrawal 是 Transaction 的一种类型，所以我们不再直接在类 ATM 和类 Withdrawal 之间绘制关联线——Withdrawal 派生类继承了基类 Transaction 与类 ATM 的关联。派生类 BalanceInquiry 和 Deposit 也继承此关联，这取代了先前省略的类 BalanceInquiry 和 Deposit 与类 ATM 之间的关联。再次注意使用三角形空心箭头来表示类 Transaction 的特化，如图 26.9 所示。

我们还在类 Transaction 和 BankDatabase 之间添加关联（图 26.10）。所有 Transaction 都需要对 BankDatabase 的引用，以便访问和修改账户信息。每个 Transaction 派生类都继承此引用，因此我们不再为类 Withdrawal 和 BankDatabase 之间的关联建模。类 Transaction 和 BankDatabase 之间的关联取代了先前省略的类 BalanceInquiry 和 Deposit 与 BankDatabase 之间的关联。

我们在类 Transaction 和 Screen 之间包含一个关联，因为所有 Transaction 都通过 Screen 向用户显示输出。每个派生类都继承这个

- 1. 如果类 A 是类 B 的泛化，那么类 B 派生自（并且是）类 A 的特化。例如，抽象基类 Transaction 是类 Withdrawal 的泛化。因此，类 Withdrawal 派生自（并且是）类 Transaction 的特化。图 26.12 包含类 Withdrawal 头文件的一部分，其中类定义表明了 Withdrawal 和 Transaction 之间的继承关系（第 9 行）。

```cpp
// Fig. 26.12: Withdrawal.h
// Definition of class Withdrawal that represents a withdrawal transaction
#ifndef WITHDRAWAL_H
#define WITHDRAWAL_H

#include "transaction.h" // Transaction class definition

// class Withdrawal derives from base class Transaction
class Withdrawal : public Transaction
{
}; // end class Withdrawal

#endif // WITHDRAWAL_H
```

**图 26.12** | *派生自 Transaction 的 Withdrawal 类定义。*

- 2. 如果类 A 是抽象类，并且类 B 派生自类 A，那么如果类 B 要成为具体类，就必须实现类 A 的纯虚函数。例如，类 Transaction 包含纯虚函数 execute，因此如果我们想实例化 Withdrawal 对象，类 Withdrawal 就必须实现这个成员函数。图 26.13 包含来自图 26.10 和图 26.11 的类 Withdrawal 的 C++ 头文件。类 Withdrawal 从基类 Transaction 继承数据成员 accountNumber，因此 Withdrawal 不声明这个数据成员。类 Withdrawal 还从其基类 Transaction 继承对 Screen 和 BankDatabase 的引用，因此我们不在代码中包含这些引用。图 26.11 为类 Withdrawal 指定了属性 amount 和操作 execute。图 26.13 的第 19 行声明了属性 amount 的数据成员。第 16 行包含操作 execute 的函数原型。回想一下，要成为具体类，派生类 Withdrawal 必须为基类 Transaction 中的纯虚函数 execute 提供具体实现。第 16 行中的原型表明你打算重写基类的纯虚函数。如果你要在 .cpp 文件中提供实现，就必须提供这个原型。我们将在第 26.4 节中给出这个实现。keypad 和 cashDispenser 引用（第 20–21 行）是派生自图 26.10 中 Withdrawal 关联的数据成员。在第 26.4 节该类的实现中，构造函数会将这些引用初始化为实际对象。再一次，为了能够编译第 20–21 行中的引用声明，我们在第 8–9 行包含了前向声明。

## ATM 案例研究总结

到此结束我们对 ATM 系统的面向对象设计。第 26.4 节中给出了一个用 850 行代码实现的完整 C++ ATM 系统。这个可运行的
