
由不同的类表示。这让旧的 `MakeAWithdrawal()` 变得承担了太多的责任。目前，你的应用程序只处理两种类型的银行账户，但假设你的老板要求你实现一种新账户类型 `CheckingAccount`，而它有不同的 `Withdraw()` 要求。如果你不搜寻并找到每个检查其参数运行时类型的方法，你的程序将无法正常工作。

## 将方法声明为虚拟并对其进行重写

作为 `MakeAWithdrawal()` 的作者，你不想了解所有不同类型的账户。你希望把了解账户类型的责任交给使用 `MakeAWithdrawal()` 的程序员，让他们自己去处理账户类型，而你不需要被打扰。你希望 C# 根据对象的运行时类型来决定调用哪种方法。

你通过将基类方法标记为 `virtual` 关键字，并对每个子类版本的该方法标记为 `override` 关键字，来告诉 C# 在运行时对 `Withdraw()` 的版本做出决定。

我使用多态性重写了上一个节的程序示例。我在 `Withdraw()` 方法中添加了输出语句，以证明正确的方法确实被调用了（我还删除了任何重复信息）。这里是 `PolymorphicInheritance` 程序：

![](img/6df7bb88e9302e98442acc219cfbd7fc_340_0.png)

```csharp
// PolymorphicInheritance -- 在基类中多态地
//     隐藏一个方法。展示如何使用
//     virtual 和 override 关键字。
using System;
namespace PolymorphicInheritance
{
    // BankAccount -- 一个基础银行账户
    public class BankAccount
    {
        protected decimal _balance;
        public BankAccount(decimal initialBalance)
        {
            _balance = initialBalance;
        }
        public decimal Balance
        {
            get { return _balance; }
        }
        public virtual decimal Withdraw(decimal amount)
        {
            Console.WriteLine("In BankAccount.Withdraw() for ${0}...", amount);
            decimal amountToWithdraw = amount;
            if (amountToWithdraw > Balance)
            {
                amountToWithdraw = Balance;
            }
            _balance -= amountToWithdraw;
            return amountToWithdraw;
        }
    }
}
```

```csharp
// SavingsAccount -- 会产生利息的银行账户
public class SavingsAccount : BankAccount
{
    public decimal _interestRate;
    // SavingsAccount -- 输入以 0 到 100 之间的
    // 速率的速率。
    public SavingsAccount(decimal initialBalance, decimal interestRate)
        : base(initialBalance)
    {
        _interestRate = interestRate / 100;
    }
    // AccumulateInterest -- 每个周期调用一次。
    public void AccumulateInterest()
    {
        _balance = Balance + (Balance * _interestRate);
    }
    // Withdraw -- 你可以提取任何不超过余额的
    // 金额；返回提取的金额。
    override public decimal Withdraw(decimal withdrawal)
    {
        Console.WriteLine("In SavingsAccount.Withdraw()...");
        Console.WriteLine("Invoking base-class Withdraw twice...");
        // 扣除顶部的 $1.50。
        base.Withdraw(1.5M);
        // 现在你可以从剩余部分中取款。
        return base.Withdraw(withdrawal);
    }
}
public class Program
{
    public static void MakeAWithdrawal(BankAccount ba, decimal amount)
    {
        ba.Withdraw(amount);
    }
    public static void Main(string[] args)
    {
        BankAccount ba;
        SavingsAccount sa;
        // 显示结果余额。
        Console.WriteLine("Withdrawal: MakeAWithdrawal(ba, ...)");
        ba = new BankAccount(200M);
        MakeAWithdrawal(ba, amount);
    }
}
```
