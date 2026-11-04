
## 继承真是奇妙

为了理解周围的事物，人类构建了庞大的分类体系。例如，Fido 是狗的一种特例，狗是犬科的一种特例，犬科是哺乳动物的一种特例——如此等等。这种对事物进行分类的能力塑造了我们对世界的理解。

在 C# 这样的面向对象语言中，你会说 Student 类继承自 Person 类。你也会说 Person 是 Student 的基类，而 Student 是 Person 的子类。最后，你会说一个 Student IS_A Person。（使用全大写和下划线来表达这种独特关系是一种常见做法——这个概念不是我发明的。）

请注意，IS_A 属性不是自反的：虽然 Student IS_A Person，但反过来不成立。一个 Person IS_NOT 一个 Student。这样的陈述始终指的是一般情况。某个具体的 Person 实际上可能是 Student——但大量属于 Person 类的人并不属于 Student 类。此外，Student 类具有它与 Person 类不共享的属性。例如，Student 有绩点，但普通的 Person 完全没有也没关系。

继承属性是传递的。例如，如果我定义一个新类 GraduateStudent 作为 Student 的子类，那么 GraduateStudent 也是一个 Person。必须如此：如果 GraduateStudent IS_A Student 且 Student IS_A Person，那么 GraduateStudent IS_A Person。

SubClass 将 BaseClass 的所有成员作为自己的成员，再加上它可能添加的任何成员。Main() 演示了 SubClass 现在拥有一个数据成员 _dataMember 和一个成员方法 SomeMethod()，以及家族中全新的小方法 SomeOtherMethod()——这真是太令人愉快了。

程序产生以下预期输出（我通常在程序按预期工作时都会有点惊讶）：

```
Exercising a base class object:
SomeMethod()
Exercising a subclass object:
SomeMethod()
SomeOtherMethod()
Press Enter to terminate...
```

## 为什么需要继承

继承具有若干重要功能。例如，你可能会认为继承减少了打字量。在某种程度上确实如此——在描述 Student 类时，你不需要重复 Person 的属性。一个更重要且相关的议题是重用这一主要流行词。软件科学家们很早就知道，对每个新项目都从零开始并重建相同的软件组件是毫无意义的。

将软件开发的情况与其他行业进行比较。想想有多少汽车制造商在造车之前先自己制造扳手和螺丝刀。在这些人中，估计有多少会在下一款车型上完全重新开始并制造全新的工具。其他行业从业者发现，使用现有的螺丝、螺栓、螺母，甚至更大型的现成组件（如电机和压缩机）作为起点，比从零开始更有意义。

继承使你能够调整现有的软件组件。你可以在不进行内部修改的情况下将现有类适配到新应用中。现有类被继承到——或者程序员常说的，被扩展为——一个包含必要增添和修改的新子类中。如果基类是别人写的，你可能无法修改它，因此继承可以派上用场。

这种能力带来了继承的第三个好处。假设你继承自——扩展——一个现有类。后来，你发现基类有一个必须修正的错误。如果你修改了该类以便重用，你必须在每个应用中分别手动检查、修正并重新测试该错误。如果你不做更改的情况下继承了该类，通常可以将更新后的类轻松地插入到其他应用中。

但继承最大的好处是它描述了生活的本质。事物相互继承属性。无可避免。（Basta！——正如我的意大利奶奶会说的。）

## 从 BankAccount 类继承
(一个更复杂的示例)

银行维护多种类型的账户。其中一种，储蓄账户，拥有简单银行账户的所有属性，外加累积利息的能力。以下 SimpleSavingsAccount 程序在 C# 中模拟了这种关系。

网站上该程序的版本包含了本章下一节的一些修改，因此与此处显示的代码清单略有不同。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_313_0.png)

// SimpleSavingsAccount -- Implement SavingsAccount as a form of
// bank account; use no virtual methods.
using System;
namespace SimpleSavingsAccount
{
// BankAccount -- Simulate a bank account, each of which
// carries an account ID (which is assigned
// on creation) and a balance.
// public class BankAccount // The base class

// Bank accounts start at 1000 and increase sequentially.
public static int _nextAccountNumber = 1000;
// Maintain the account number and balance for each object.
public int _accountNumber;
public decimal _balance;
// Init -- Initialize a bank account with the next account ID and the
// specified initial balance (default to zero).
public void InitBankAccount()
{
    InitBankAccount(0);
}
public void InitBankAccount(decimal initialBalance)
{
    _accountNumber = ++_nextAccountNumber;
    _balance = initialBalance;
}
// Balance property.
public decimal Balance
{
    get { return _balance; }
}
// Deposit -- Any positive deposit is allowed.
public void Deposit(decimal amount)
{
    if (amount > 0)
    {
        _balance += amount;
    }
}
// Withdraw -- You can withdraw any amount up to the
// balance. return the amount withdrawn.
public decimal Withdraw(decimal withdrawal)
{
    if (Balance <= withdrawal) // Use Balance property.
    {
        withdrawal = Balance;
    }
    _balance -= withdrawal;
    return withdrawal;
}
// ToString -- Stringify the account.
public string ToBankAccountString()
{
    return String.Format("{0} ({1:C})", _accountNumber, Balance);
}

// SavingsAccount -- A bank account that draws interest
public class SavingsAccount : BankAccount // The subclass
{
    public decimal _interestRate;
    // InitSavingsAccount -- Input the rate expressed as a
    // rate between 0 and 100.
    public void InitSavingsAccount(decimal interestRate)
    {
        InitSavingsAccount(0, interestRate);
    }
}
public void InitSavingsAccount(decimal initialBalance, decimal interestRate)
{
    InitBankAccount(initialBalance);  // Note call to base class.
    this._interestRate = interestRate / 100;
}
// AccumulateInterest -- Invoke once per period.
public void AccumulateInterest()
{
    _balance = Balance + (decimal)(Balance * _interestRate);
}
// ToString -- Stringify the account.
public string ToSavingsAccountString()
{
    return String.Format("{0} ({1}%)",
        ToBankAccountString(), _interestRate * 100);
}
public class Program
{
    public static void Main(string[] args)
    {
        // Create a bank account and display it.
        BankAccount ba = new BankAccount();
        ba.InitBankAccount(100M);  // M suffix indicates decimal.
        ba.Deposit(100M);
        Console.WriteLine("Account {0}", ba.ToBankAccountString());
        // Now a savings account
        SavingsAccount sa = new SavingsAccount();
        sa.InitSavingsAccount(100M, 12.5M);
        sa.AccumulateInterest();
        Console.WriteLine("Account {0}", sa.ToSavingsAccountString());
        // Wait for user to acknowledge the results.
        Console.WriteLine("Press Enter to terminate...");
        Console.Read();
    }
}

BankAccount 类与本书其他章节中出现的某些类并不不同。它以重载的初始化方法 InitBankAccount() 开始：一个用于初始余额的账户，另一个则必须使用零初始余额。请注意，BankAccount 的这个版本没有利用最新的、最棒的构造函数改进。如果你读完本章并看到我在 BankAccount 的最终版本中清理了这个问题，你就能明白我为何在此处选择“稍微退后”一点。

Balance 属性允许其他人读取余额，而不让他们修改它。Deposit() 方法接受任何正存款。Withdraw() 允许你取出你想要的任意金额，只要账户里有足够的钱。（我的银行很不错，但它没*那样*好。）ToBankAccountString() 创建一个描述账户的字符串。

SavingsAccount 类继承了 BankAccount 的所有这些好东西。它还添加了利率以及按定期累积利息的能力。
