
## 第二卷，第 6 章——继承：我能得到的就这些吗？

### 继承很神奇

为了理解周围环境，人类构建了庞大的分类体系。例如，Fido 是狗的一个特例，狗是犬科动物的一个特例，犬科动物是哺乳动物的一个特例——如此类推。这种对事物进行分类的能力塑造了人类对世界的理解。

在 C# 这样的面向对象语言中，你会说类 `Student` 继承自类 `Person`。你还会说 `Person` 是 `Student` 的基类，而 `Student` 是 `Person` 的子类。最后，你会说 `Student` IS_A `Person`。（使用全大写字母和下划线是表达这种独特关系的常见方式——这个概念可不是我编出来的。）

注意，IS_A 关系不是自反的：虽然 `Student` IS_A `Person`，但反过来并不成立。`Person` IS_NOT_A `Student`。这样的陈述总是指一般情况。某个特定的 `Person` 实际上可能是 `Student`——但许多属于 `Person` 类的个体并不是 `Student` 类的成员。此外，`Student` 类具有一些不与 `Person` 类共享的属性。例如，`Student` 有平均绩点，而普通的 `Person` 则乐得没有。

继承关系具有传递性。例如，如果我将一个新类 `GraduateStudent` 定义为 `Student` 的子类，那么 `GraduateStudent` 也是一个 `Person`。它必然如此：如果一个 `GraduateStudent` IS_A `Student`，并且一个 `Student` IS_A `Person`，那么一个 `GraduateStudent` IS_A `Person`。

`SubClass` 获得 `BaseClass` 的所有成员作为自己的成员，再加上它可能添加到这一堆中的任何成员。`Main()` 演示了 `SubClass` 现在拥有一个数据成员 `_dataMember` 和一个成员方法 `SomeMethod()`，并与这个家族的全新成员——小方法 `SomeOtherMethod()`——会合，而这也是多么令人愉快啊。

该程序产生以下预期输出（每当我的某个程序按预期工作时，我通常都会有点惊讶）：

```
Exercising a base class object:
SomeMethod()
Exercising a subclass object:
SomeMethod()
SomeOtherMethod()
Press Enter to terminate...
```

### 为什么需要继承

继承具有若干重要功能。例如，你可能会认为继承减少了输入量。在某种程度上确实如此——在描述 `Student` 类时，你不需要重复 `Person` 的属性。一个更重要且相关的问题是那个重要流行词*复用*。软件科学家早就知道，每个新项目都从头开始并重新构建相同的软件组件，意义不大。

将软件开发中的情况与其他行业的情况相比较。想一想有多少汽车制造商会先制造自己的扳手和螺丝刀，然后再制造汽车。在那些这样做的制造商中，估计有多少会完全从头开始，为下一个车型制造所有新工具。其他行业的从业者发现，从现有的螺钉、螺栓、螺母，甚至电机和压缩机等更大的现成组件开始，比从头开始更有意义。

继承使你能够调整现有的软件组件。你可以让现有类适应新的应用，而无需进行内部修改。现有类被继承到——或者，正如程序员常说的，被*扩展*为——一个新的子类中，该子类包含必要的添加和修改。如果基类是别人编写的，你可能无法修改它，因此继承可以救场。

这种能力还带来了继承的第三个好处。假设你继承——扩展——一个现有类。后来，你发现基类有一个必须修正的 bug。如果你为了复用它而修改了该类，就必须在每个应用中分别手动检查、修正并重新测试该 bug。如果你继承该类时没有做更改，通常就可以轻松地将更新后的类放入另一个应用中。

但继承最大的好处在于，它描述了生活的本来方式。事物彼此继承属性。这是无法回避的。（*够了！*——正如我的意大利祖母会说的那样。）

### 从 BankAccount 类继承（一个更复杂的示例）

银行维护多种类型的账户。其中一种类型是储蓄账户，它具有简单银行账户的所有属性，还具备累积利息的能力。下面的 `SimpleSavingsAccount` 程序在 C# 中为这种关系建模。

![](img/80ff26f06fc9ab951e1cd4257b867366_309_0.png)

网站上的这个程序版本包含本章下一节的一些修改，因此与这里显示的代码清单略有不同。

![](img/80ff26f06fc9ab951e1cd4257b867366_310_0.png)

![](img/80ff26f06fc9ab951e1cd4257b867366_310_1.png)

```csharp
// SimpleSavingsAccount -- Implement SavingsAccount as a form of
//    bank account; use no virtual methods.
using System;
namespace SimpleSavingsAccount
{
    // BankAccount -- Simulate a bank account, each of which
    //    carries an account ID (which is assigned
    //    on creation) and a balance.
    public class BankAccount    // The base class
    {
        // Bank accounts start at 1000 and increase sequentially.
        public static int _nextAccountNumber = 1000;
        // Maintain the account number and balance for each object.
        public int _accountNumber;
        public decimal _balance;
        // Init -- Initialize a bank account with the next account ID and the
        //    specified initial balance (default to zero).
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
        // Deposit -- any positive deposit is allowed.
        public void Deposit(decimal amount)
        {
            if (amount > 0)
            {
                _balance += amount;
            }
        }
        // Withdraw -- You can withdraw any amount up to the
        //    balance; return the amount withdrawn.
        public decimal Withdraw(decimal withdrawal)
        {
            if (Balance <= withdrawal) // Use Balance property.
            {
                withdrawal = Balance;
            }
            _balance -= withdrawal;
            return withdrawal;
        }
        // ToString - Stringify the account.
        public string ToBankAccountString()
        {
            return String.Format("{0} - {1:C}",
                _accountNumber, Balance);
        }
    }

    // SavingsAccount -- A bank account that draws interest
    public class SavingsAccount : BankAccount    // The subclass
    {
        public decimal _interestRate;

        // InitSavingsAccount -- Input the rate expressed as a
        // rate between 0 and 100.
        public void InitSavingsAccount(decimal interestRate)
        {
            InitSavingsAccount(0, interestRate);
        }
        public void InitSavingsAccount(decimal initialBalance, decimal interestRate)
        {
            InitBankAccount(initialBalance); // Note call to base class.
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
            return String.Format("{0} ({1})",
                ToBankAccountString(), _interestRate * 100);
        }
    }

    public class Program
    {
        public static void Main(string[] args)
        {
            // Create a bank account and display it.
            BankAccount ba = new BankAccount();
            ba.InitBankAccount(100M); // M suffix indicates decimal.
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
}
```

`BankAccount` 类与本书其他章节中出现的一些类并无不同。它以一个重载的初始化方法 `InitBankAccount()` 开始：一个用于具有初始余额的账户，另一个用于初始余额为零即可满足的账户。注意，这个版本的 `BankAccount` 没有利用最新最先进的构造函数进展。如果你读完整章，并看到我在 `BankAccount` 的最终版本中清理了这个主题，那么你就能明白我为什么选择在这里“退后”一点。

`Balance` 属性允许其他人读取余额，但不允许他们修改余额。`Deposit()` 方法接受任何正存款。`Withdraw()` 允许你取出任意金额，只要你有
