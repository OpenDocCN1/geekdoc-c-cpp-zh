
## 第5章：让类承担责任

### 本章内容

- 通过访问控制让类保护自身
- 介绍属性，一种特殊的方法
- 允许对象通过构造函数初始化自身
- 为同一个类定义多个构造函数
- 构造静态成员或类成员

类必须对其行为负责。就像微波炉不应因为你按错键就燃起火焰一样，类也不应在遇到错误数据时任由自己崩溃并失效。

为了让类对其行为负责，类必须确保其初始状态正确，然后控制其后续状态以使其保持有效。C# 提供了这两种能力。

### 限制对类成员的访问

简单类将其所有成员都定义为 `public`。考虑一个 `BankAccount` 程序，它维护一个 `balance` 数据成员来保存每个账户的余额。将该数据成员设为 `public`，就等于让所有人都处于自觉遵守规则的状态。

我不知道你的银行怎样，但我的银行远不会那么大方，留下一堆钱和一本登记簿，让我每次往那堆钱里加钱或取钱时都自己登记。毕竟，我可能会忘记在登记簿上标记取款。

控制访问可以避免小错误，例如偶尔忘记标记一笔取款，并且还能避免一些真正重大的取款错误。

我完全知道你们这些面向过程的家伙在想什么：“只要制定一条规则，让其他类不能直接访问 `balance` 数据成员，就这样。”这种方法在理论上也许行得通，但在实践中从来不行。人们一开始都怀着良好的意图（就像我打算每天锻炼一样），但这些良好意图在把产品交付出去的时间进度压力下被压得粉碎。说到体重……

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_286_0.png)

### 一个 public BankAccount 的公开示例

下面的 BankAccount 类示例将其所有方法声明为 public，但将其数据成员（包括 _accountNumber 和 _balance）声明为 private。请注意，我故意让它处于不正确的状态，以说明一个要点。下面的代码块目前还不能正确编译：

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_287_0.png)

```csharp
// BankAccount -- Create a bank account using a double variable
// to store the account balance (keep the balance in a private
// variable to hide its implementation from the outside world).
// Note: Until you correct it, this program fails to compile
// because Main() refers to a private member of class BankAccount.
using System;
namespace BankAccount
{
 public class Program
 {
 public static void Main(string[] args)
 {
 Console.WriteLine("This program doesn't compile in its present state.");
 // Open a bank account.
 Console.WriteLine("Create a bank account object");
 BankAccount ba = new BankAccount();
 ba.InitBankAccount();
 // Accessing the balance via the Deposit() method is okay --
 // Deposit() has access to all the data members.
 ba.Deposit(10);
 // Accessing the data member directly is a compile-time error.
 Console.WriteLine("Just in case you get this far the following is "
 + "supposed to generate a compile error");
 ba._balance += 10;
 // Wait for user to acknowledge the results.
 Console.WriteLine("Press Enter to terminate...");
 Console.Read();
 }
 }

 // BankAccount -- Define a class that represents a simple account.
public class BankAccount
{
 private static int _nextAccountNumber = 1000;
 private int _accountNumber;
 // Maintain the balance as a double variable.
 private double _balance;
 // Init -- Initialize a bank account with the next
 // account id and a balance of 0.
 public void InitBankAccount()
 {
 _accountNumber = ++_nextAccountNumber;
 _balance = 0.0;
 }
 // GetBalance -- Return the current balance.
 public double GetBalance()
 {
 return _balance;
 }
}
```

```
// AccountNumber
public int GetAccountNumber()
{
    return _accountNumber;
}
public void SetAccountNumber(int accountNumber)
{
    this._accountNumber = accountNumber;
}
// Deposit -- Any positive deposit is allowed.
public void Deposit(double amount)
{
    if (amount > 0.0)
    {
        _balance += amount;
    }
}
// Withdraw -- You can withdraw any amount up to the
// balance. Return the amount withdrawn.
public double Withdraw(double withdrawal)
{
    if (_balance <= withdrawal)
    {
        withdrawal = _balance;
    }
    _balance -= withdrawal;
    return withdrawal;
}
// GetString -- Return the account data as a string.
public string GetString()
{
    string s = String.Format("{0} {1:C}", GetAccountNumber(), GetBalance());
    return s;
}
}
```

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_288_0.png)

在这个代码示例中，_balance -= withdrawal 与 _balance = _balance - withdrawal 相同。（C# 程序员倾向于使用可用的最短写法。）

将成员标记为 public 会使该成员可供程序中的任何其他代码使用。

BankAccount 类提供了一个 InitBankAccount() 方法来初始化该类的成员，一个 Deposit() 方法来处理存款，以及一个 Withdraw() 方法来执行取款。Deposit() 和 Withdraw() 方法甚至提供了一些基本规则，例如“不能存入负数”和“取款不能超过账户中的金额”（我确信你会同意，这两条都是银行的好规则）。然而，只要 _balance 可被外部方法访问，所有人就都处于自觉遵守制度之下。（在这里，外部是指“类外部但在同一程序内”。）对于由程序员团队编写的大型程序，这种自觉遵守制度可能会成为问题。考虑到人类普遍容易犯错，它甚至可能对你（和我）造成问题。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_289_0.png)

编写良好的代码，其规则可由编译器强制执行，能让所有人免于偶尔被子弹打中脚趾这种意外。

不过，在你过于兴奋之前，请注意该程序无法编译。尝试编译时会生成以下错误消息：

```
'BankAccount.BankAccount._balance' is inaccessible due to its protection level.
```

我不知道它为什么不直接明说：“嘿，这是 private，所以别碰。”语句 ba._balance += 10; 是非法的，因为 _balance 对 Main() 不可访问，而 Main() 是 BankAccount 类外部的方法。将这一行替换为 ba.Deposit(10) 即可解决问题。BankAccount.Deposit() 方法是 public 的，因此可由 Main() 以及程序的其他部分访问。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_289_1.png)

不显式声明类成员的访问类型，等同于将其声明为 private。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_289_2.png)

默认访问类型是 private。不过，你应该包含 private 关键字以消除任何疑问。优秀的程序员会明确表达自己的意图，这是减少错误的另一种方法。

### 提前了解——其他安全级别

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_289_3.png)

理解本节需要你具备一些继承（见本迷你书第6章）和命名空间（见本迷你书第10章）的知识。如果愿意，你可以暂时跳过本节，但只需知道需要时它就在这里。

C# 提供以下安全级别：

- 一个 `public` 成员可由程序中的任何类访问。
- 一个 `private` 成员只能从当前类访问。
- 一个 `protected` 成员可从当前类及其任何子类访问。
- 一个 `internal` 成员可由同一程序模块或程序集中的任何类访问。
- 一个 `internal protected` 成员可从当前类及其任何子类访问，也可从同一模块中的类访问。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_289_4.png)

C# 的“模块”或程序集，是一段单独编译的代码，可以是 .EXE 文件中的可执行程序，也可以是 .DLL 文件中的支持库模块。单个命名空间可以跨越多个程序集。（本迷你书第10章解释 C# 程序集和命名空间，并讨论 public 和 private 之外的访问级别。）
