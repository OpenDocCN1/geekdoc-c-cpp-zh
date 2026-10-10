
```cs
BankAccount ba = new BankAccount();
ProcessAmount(ba);
SavingsAccount sa = new SavingsAccount();
ProcessAmount(sa);
}
}
public class BankAccount
{
    public BankAccount() { }
    public static void ProcessAmount(BankAccount ba)
    {
        Console.WriteLine("Processing BankAccount");
    }
}
public class SavingsAccount : BankAccount
{
    public SavingsAccount() : base() { }
    public static void ProcessAmount(SavingsAccount sa)
    {
        Console.WriteLine("Processing SavingsAccount");
    }
}
```

```cs
}
}
public class SubClass : BaseClass
{
    public SubClass()
    {
        Console.WriteLine("Constructing SubClass (default)");
    }
    public SubClass(int i1, int i2) : base(i1)
    {
        Console.WriteLine("Constructing SubClass({0}, {1})", i1, i2);
    }
}
public class Program
{
    public static void Main(string[] args)
    {
        Console.WriteLine("Invoking SubClass()");
        SubClass sc1 = new SubClass();
        Console.WriteLine("\nInvoking SubClass(1, 2)");
        SubClass sc2 = new SubClass(1, 2);
        // Wait for user to acknowledge.
        Console.WriteLine("Press Enter to terminate...");
        Console.Read();
    }
}
```

该程序的输出为：

```
Invoking SubClass()
Constructing BaseClass (default)
Constructing SubClass (default)
Invoking SubClass(1, 2)
Constructing BaseClass(1)
Constructing SubClass(1, 2)
Press Enter to terminate...
```

此版本与之前的示例相同，通过使用 `BaseClass` 和 `SubClass` 的默认构造函数创建一个默认的 `SubClass` 对象。

第二个对象通过表达式 `new SubClass(1, 2)` 创建。C# 调用了 `SubClass(int, int)` 构造函数，该函数使用 `base` 关键字将其中一个值传递给 `BaseClass(int)` 构造函数。`SubClass` 将第一个参数传递给基类处理，然后自己使用第二个值。

# 更新后的 BankAccount 类

网站上的 `ConstructorSavingsAccount` 程序是 `SimpleBankAccount` 程序的更新版本。然而在此版本中，`SavingsAccount` 构造函数可以将信息传回 `BankAccount` 构造函数。这里只显示了 `Main()` 和构造函数本身：

![](img/6df7bb88e9302e98442acc219cfbd7fc_324_0.png)

```cs
// ConstructorSavingsAccount -- Implement a SavingsAccount as
//   a form of BankAccount; use no virtual methods, but
//   implement the constructors properly.
using System;
namespace ConstructorSavingsAccount
{
    // BankAccount -- Simulate a bank account, each of which carries an
    //   account ID (which is assigned upon creation) and a balance.
    public class BankAccount
    {
        // Bank accounts start at 1000 and increase sequentially.
        public static int _nextAccountNumber = 1000;
        // Maintain the account number and balance for each object.
        public int _accountNumber;
        public decimal _balance;
        // Constructors
        public BankAccount() : this(0)
        {
        }
        public BankAccount(decimal initialBalance)
        {
            _accountNumber = ++_nextAccountNumber;
            _balance = initialBalance;
        }
        public decimal Balance
        {
            get { return _balance; }
            // Protected setter lets subclass use Balance property to set.
            protected set { _balance = value; }
        }
        // Deposit -- Any positive deposit is allowed.
        public void Deposit(decimal amount)
        {
            if (amount > 0)
            {
                Balance += amount;
            }
        }
        // Withdraw -- You can withdraw any amount up to the
        //   balance; return the amount withdrawn.
        public decimal Withdraw(decimal withdrawal)
        {
            if (Balance <= withdrawal)
            {
                withdrawal = Balance;
            }
            Balance -= withdrawal;
            return withdrawal;
        }
        // ToString -- Stringify the account.
        public string ToBankAccountString()
        {
            return String.Format("{0} - {1:C}",
                _accountNumber, Balance);
        }
    }
    // SavingsAccount -- A bank account that draws interest
public class SavingsAccount : BankAccount
{
    public decimal _interestRate;
    // InitSavingsAccount -- Input the rate expressed as a
    //   rate between 0 and 100.
    public SavingsAccount(decimal interestRate) : this(interestRate, 0) { }
    public SavingsAccount(decimal interestRate, decimal initial) : base(initial)
    {
        this._interestRate = interestRate / 100;
    }
    // AccumulateInterest -- Invoke once per period.
    public void AccumulateInterest()
    {
        // Use protected setter and public getter via Balance property.
        Balance = Balance + (decimal)(Balance * _interestRate);
    }
    // ToString -- Stringify the account.
    public string ToSavingsAccountString()
    {
        return String.Format("{0} ({1}%)",
            ToBankAccountString(), _interestRate * 100);
    }
}
public class Program
{
    // DirectDeposit -- Deposit my paycheck automatically.
    public static void DirectDeposit(BankAccount ba, decimal pay)
    {
        ba.Deposit(pay);
    }
    public static void Main(string[] args)
    {
        // Create a bank account and display it.
        BankAccount ba = new BankAccount(100M);
        DirectDeposit(ba, 100M);
        Console.WriteLine("Account {0}", ba.ToBankAccountString());
        // Now a savings account
        SavingsAccount sa = new SavingsAccount(100M);
        DirectDeposit(ba, 100M);
        Console.WriteLine("Account {0}", ba.ToBankAccountString());
        // Now a savings account
        sa.AccumulateInterest();
        Console.WriteLine("Account {0}", sa.ToSavingsAccountString());
        // Wait for user to acknowledge.
        Console.WriteLine("Press Enter to terminate...");
        Console.Read();
    }
}
```

C# 提供了一种与构造函数相反的方法：析构函数。它的名称在类名前面带有一个波浪号 `~`。例如，`~BaseClass()` 是 `BaseClass` 的析构函数。

# 垃圾回收与析构函数

C# 的析构函数比其他面向对象的语言（如 C++）有用得多，因为 C# 具有非确定性析构。理解该术语的含义以及它为什么重要需要一些解释。

`SavingsAccount` 类还提供了两个构造函数。`SavingsAccount(interest rate)` 构造函数会调用 `SavingsAccount(interest rate, initial balance)` 构造函数，并传递初始余额 0。这个最通用的构造函数使用 `base` 关键字将初始余额传递给 `BankAccount(initial balance)` 构造函数，如图 6-1 所示。

# 图 6-1:
使用默认构造函数构建对象的路径。

![](img/6df7bb88e9302e98442acc219cfbd7fc_327_0.png)

我修改了 `Main()` 以去掉那些该死的 `Init...( )` 方法，并用构造函数代替了它们。该程序的输出是相同的。

![](img/6df7bb88e9302e98442acc219cfbd7fc_327_1.png)

注意 `BankAccount` 中的 `Balance` 属性，它有一个公共的 getter（访问），但有一个受保护的 setter（访问器）。在这里使用 `protected` 可以防止 `BankAccount` 外部使用，但允许在子类中使用受保护的 setter，这在 `SavingsAccount.AccumulateInterest` 中发生，此时 `Balance` 在赋值运算符的左侧。（属性和 `protected` 关键字在第二本书第 5 章。你可以在本书的索引中查找。）

## 第 7 章：多态——什么？

### 本章内容

- 决定隐藏还是重写基类方法（这么多选择！）
- 构建抽象类——你是认真的吗？
- 将方法以及包含该方法的类声明为抽象
- 使用 `ToString`，类的名片
- 密封类以防止被子类化

![](img/6df7bb88e9302e98442acc219cfbd7fc_328_0.png)

在继承中，一个类“收养”另一个类的成员。因此，我可以创建一个 `SavingsAccount` 类，它从基类 `BankAccount` 继承如 `account id` 等数据成员以及如 `Deposit()` 等方法。这很有用，但这种继承的定义不足以模拟商业世界中的实际情况。

如果你对类继承并不了解（或不记得），请参阅本迷你书籍的第 6 章。

微波炉是一种烤箱，不是因为它看起来像烤箱，而是因为它执行了与烤箱相同的功能。微波炉可能会执行额外功能，但它至少执行基础的烤箱功能——最重要的是当我说“开始烹饪”时，加热我的玉米纳片。（我依靠我的 `Refrigerator` 类的对象来冷却啤酒。）我并不特别关心烤箱内部为了实现这一点点必须做什么，就像我不在意它是什么种类型的烤箱、谁制造的，或者在我妻子购买时是否在打折一样。（嘿，等一下——我在意最后那个。）

从人类的角度来看，微波炉和传统烤箱之间的关系似乎并不大，但请从烤箱的角度来考虑这个问题。传统烤箱在内部执行的步骤与微波炉可能采取的步骤完全不同。

![](img/6df7bb88e9302e98442acc219cfbd7fc_328_1.png)

继承的力量在于，子类不需要按照其编写的方式完全继承基类中的每一个方法。子类可以继承基类方法的精髓，同时以不同的方式实现细节。

### 重载继承的方法

正如本迷你书籍第 3 章所述（在索引中查找“重载”），只要参数的数量或类型不同（或只要两者都不同），两个或多个方法就可以具有相同的名称。

### 这是一个简单的方法重载案例

给两个方法赋予相同的名称就是重载，就像“把它们搞清楚让我的大脑过载了”。

方法的参数将成为其扩展名的一部分，如下例所示：

```csharp
public class MyClass
{
    public static void AMethod()
    {
        // 执行某些操作。
    }
    public static void AMethod(int i)
    {
        // 执行其他操作。
    }
    public static void AMethod(double d)
    {
        // 执行不同的操作。
    }
    public static void Main(string[] args)
    {
        AMethod();
        AMethod(1);
        AMethod(2.0);
    }
}
```
