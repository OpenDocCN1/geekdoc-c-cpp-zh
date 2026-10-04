

![](img/6df7bb88e9302e98442acc219cfbd7fc_310_0.png)

```sharp
// SimpleSavingsAccount -- 将 SavingsAccount 实现为一种
// 银行账户；不使用任何虚拟方法。
using System;
namespace SimpleSavingsAccount
{
    // BankAccount -- 模拟一个银行账户，每个账户
    // 都携带一个账户 ID（在创建时分配）
    // 和一个余额。
    public class BankAccount    // 基类
    {
        // 银行账户号码从 1000 开始并顺序增加。
        public static int _nextAccountNumber = 1000;
        // 为每个对象维护账户号码和余额。
        public int _accountNumber;
        public decimal _balance;
        // Init -- 使用下一个账户 ID 和指定的
        // 初始余额（默认 零）初始化银行账户。
        public void InitBankAccount()
        {
            InitBankAccount(0);
        }
        public void InitBankAccount(decimal initialBalance)
        {
            _accountNumber = ++_nextAccountNumber;
            _balance = initialBalance;
        }
        // Balance 属性。
        public decimal Balance
        {
            get { return _balance; }
        }
        // Deposit -- 允许任何正数的存款。
        public void Deposit(decimal amount)
        {
            if (amount > 0)
            {
                _balance += amount;
            }
        }
        // Withdraw -- 你可以提取最多余额的任何金额；
        // 返回取出的金额。
        public decimal Withdraw(decimal withdrawal)
        {
            if (Balance <= withdrawal) // 使用 Balance 属性。
            {
                withdrawal = Balance;
            }
            _balance -= withdrawal;
            return withdrawal;
        }
        // ToString - 将账户字符串化。
        public string ToBankAccountString()
        {
            return String.Format("{0} - {1:C}",
                _accountNumber, Balance);
        }
    }
    // SavingsAccount -- 一种产生利息的银行账户
    public class SavingsAccount : BankAccount    // 子类
    {
```

## 286 继承自 BankAccount 类（一个更复杂的示例）

```csharp
public decimal _interestRate;
// InitSavingsAccount -- 输入以 0 到 100 之间的
// 率表示率。
public void InitSavingsAccount(decimal interestRate)
{
    InitSavingsAccount(0, interestRate);
}
public void InitSavingsAccount(decimal initialBalance, decimal interestRate)
{
    InitBankAccount(initialBalance);  // 注意对基类的调用。
    this._interestRate = interestRate / 100;
}
// AccumulateInterest -- 每个周期调用一次。
public void AccumulateInterest()
{
    _balance = Balance + (decimal)(Balance * _interestRate);
}
// ToString - 将账户字符串化。
public string ToSavingsAccountString()
{
    return String.Format("{0} ({1}%)",
        ToBankAccountString(), _interestRate * 100);
}
public class Program
{
    public static void Main(string[] args)
    {
        // 创建银行账户并显示它。
        BankAccount ba = new BankAccount();
        ba.InitBankAccount(100M);  // M 后缀表示 decimal。
        ba.Deposit(100M);
        Console.WriteLine("Account {0}", ba.ToBankAccountString());
        // 现在是一个储蓄账户
        SavingsAccount sa = new SavingsAccount();
        sa.InitSavingsAccount(100M, 12.5M);
        sa.AccumulateInterest();
        Console.WriteLine("Account {0}", sa.ToSavingsAccountString());
        // 等待用户确认结果。
        Console.WriteLine("Press Enter to terminate...");
        Console.Read();
    }
}
```

BankAccount 类与书中其他章节有所不同。它带有重载初始化方法 `InitBankAccount()`：一个用于带有初始余额账户，另一个用于初始余额为零的账户。注意这个版本的 BankAccount 没有利用进展。如果你读完整章并看到 BankAccount 的最终版本，就能明白为什么我在这里“回退”了。

`Balance` 属性允许他人读取余额而不允许修改它。`Deposit()` 方法接受任何正数存款。`Withdraw()` 允许你在账户中有足够资金的情况下提取任何金额（我的银行很不错，但它没那么好）。`ToBankAccountString()` 创建了一个描述账户的字符串。

SavingsAccount 类继承了 BankAccount 的所有优秀特性。它还添加了利率和定期积累利息的能力。

`Main()` 执行了尽可能少的操作。它创建一个 BankAccount，显示账户，创建一个 SavingsAccount，积累一个周期的利息，并带上利率显示结果：

```
Account 1001 - $200.00
Account 1002 - $112.50 (12.5%)
Press Enter to terminate...
```

![](img/6df7bb88e9302e98442acc21cfbd7fc_312_png)

注意 `InitSavingsAccount()` 方法调用了 `InitBankAccount()`。它初始化了账户特定的数据成员。`InitSavingsAccount()` 可以初始化这些成员；但更好的做法是让 BankAccount 初始化它自己的成员。类应该对自己负责。

## IS_A 与 HAS_A —— 我困了

SavingsAccount 和 BankAccount 之间的关系是继承中基本的 IS-A 关系。在接下来的章节中，我将向你展示为什么，然后展示另一种 HAS-A 关系是什么样的作为对比。

## IS-A 关系

SavingsAccount 和 BankAccount 之间的 IS-A 关系通过前一节 SimpleSavingsAccount 程序中 `Program` 类的修改演示：

```csharp
public class Program
{
    // 添加这个：
    // DirectDeposit -- 自动存款我的工资。
    public static void DirectDeposit(BankAccount ba, decimal pay)
    {
        ba.Deposit(pay);
    }
    public static void Main(string[] args)
    {
        // 创建银行账户并显示它。
        BankAccount ba = new BankAccount();
        ba.InitBankAccount(100M);
        ba.Deposit(100M);
        Console.WriteLine("Account {0}", ba.ToBankAccountString());
        // 现在是一个储蓄账户
        SavingsAccount sa = new SavingsAccount();
        sa.InitSavingsAccount(100M, 12.5M);
        sa.AccumulateInterest();
        Console.WriteLine("Account {0}", sa.ToSavingsAccountString());
        // 等待用户确认结果。
        Console.WriteLine("Press Enter to terminate...");
        Console.Read();
    }
}
```

在实际上，什么都没有改变。唯一的真实区别是所有存款现在通过本地的 `DirectDeposit()` 完成，而它不是 `BankAccount` 的一部分。该方法的参数是银行账户和存款金额。

![](img/6df7bb88e9302e98442acc21cfbd7fc_313_0.png)

注意（重点来了）`Main()` 可以将银行账户或储蓄账户传递给 `DirectDeposit()`，因为 SavingsAccount IS-A BankAccount，并且拥有所有的权利和特权。因为 SavingsAccount IS-A BankAccount，你可以将 SavingsAccount 赋值给 BankAccount 类型的变量或方法参数。

## 通过使用关系访问 BankAccount

SavingsAccount 类可以以不同的方式访问 BankAccount 的成员，如下代码所示，其中关键行已加粗显示：

```csharp
// SavingsAccount -- 一种产生利息的银行账户
public class SavingsAccount_   // 注意下划线：这并不是
// SavingsAccount 类。
{
  public BankAccount _bankAccount;  // 注意这个，被包含的 BankAccount。
  public decimal _interestRate;
  // InitSavingsAccount -- 输入以 0 到 100 之间的
// 率表示率。
  public void InitSavingsAccount(BankAccount bankAccount, decimal interestRate)
  {
    this._bankAccount = bankAccount;
    this._interestRate = interestRate / 100;
  }
  // AccumulateInterest -- 每个周期调用一次。
  public void AccumulateInterest()
  {
    _bankAccount._balance = _bankAccount.Balance
      + (_bankAccount.Balance * interestRate);
  }
  // Deposit -- 允许任何正数的存款。
  public void Deposit(decimal amount)
  {
    // 委托给被包含的 BankAccount 对象。
    _bankAccount.Deposit(amount);
  }
}
```

