
```csharp
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
// balance.  return the amount withdrawn.
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
// SavingsAccount -- A bank account that draws interest
public class SavingsAccount : BankAccount
{
    public decimal _interestRate;
    // InitSavingAccount -- Input the rate expressed as a
    // rate between 0 and 100.
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
        SavingsAccount sa = new SavingsAccount(12.5M);
        DirectDeposit(sa, 100M);
        sa.AccumulateInterest();
        Console.WriteLine("Account {0}", sa.ToSavingsAccountString());
        // Wait for user to acknowledge the results.
        Console.WriteLine("Press Enter to terminate...");
        Console.Read();
    }
}
```

BankAccount 定义了两个构造函数：一个接受初始账户余额，另一个是默认构造函数，不接受参数。为了避免在构造函数中重复代码，默认构造函数使用 this 关键字调用 BankAccount(初始余额) 构造函数。

SavingsAccount 类也提供了两个构造函数。SavingsAccount(利率) 构造函数调用 SavingsAccount(利率, 初始余额) 构造函数，并传入 0 作为初始余额。这个最通用的构造函数使用 base 关键字将初始余额传递给 BankAccount(初始余额) 构造函数，如图 6-1 所示。

图 6-1：
使用默认构造函数构造对象的路径。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_329_0.png)

## 第二册 — 第 6 章：继承：就只有这些吗？

### 垃圾回收与 C# 析构函数

C# 提供了一种与构造函数相反的方法：析构函数。它的名称在类名前面加上波浪号（~）。例如，~BaseClass() 方法就是 BaseClass 的析构函数。

C# 在不再使用对象时调用析构函数。默认析构函数是唯一可以创建的析构函数，因为析构函数不能直接调用。此外，析构函数始终是虚的。

当涉及类的继承链时，析构函数的调用顺序与构造函数的顺序相反。也就是说，子类的析构函数会在基类的析构函数之前被调用。

在 C# 中，析构函数的方法比在其他面向对象语言（如 C++）中要少得多，因为 C# 具有 *非确定性销毁*。理解该术语的含义——以及它为什么重要——需要一些解释。

当程序执行 new 命令时，例如 `new SubClass()`，对象的内存是从堆中借用的。只要有任何正在运行的程序使用对该内存的有效引用，该内存块就会一直保留。你可能有多个变量引用同一个对象。

当最后一个引用超出作用域时，内存被称为 *不可达*。换句话说，一旦没有更多引用指向它，就没有人可以访问该内存块。

C# 当内存块首次变得不可达时，并不会做任何特别的事情。有一个低优先级的系统任务在后台执行，查找不可达的内存块。为了避免对程序性能产生负面影响，这个“垃圾回收器”会在你的程序几乎没有活动时执行。随着垃圾回收器找到不可达的内存块，它会将它们归还给堆。

通常，垃圾回收器在后台静默运行。只有当堆内存开始耗尽时，垃圾回收器才会短暂接管程序的控制权。

C# 析构函数——例如 `~BaseClass()` ——是非确定性的，因为它要等到对象被垃圾回收后才会被调用，而这可能发生在对象不再被使用很久之后。事实上，如果程序在对象被找到并归还到堆之前就终止了，析构函数永远不会被调用。*非确定性*意味着你无法预测对象何时会被垃圾回收。在对象被垃圾回收并调用其析构函数之前，可能需要相当长的时间。

C# 程序员很少使用析构函数。C# 有其他方法在不再需要时归还借用的系统资源，使用 `Dispose()` 方法，这超出了本书的范围。（你可以在帮助中搜索 *Dispose method* 术语。）

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_331_0.png)

我修改了 Main()，去掉了那些该死的 Init...() 方法，改用构造函数代替。该程序的输出保持不变。

请注意 BankAccount 中的 Balance 属性，它具有 public 的 getter 但 protected 的 setter。这里使用 protected 可以防止在 BankAccount 外部使用，但允许在子类中使用受保护的 setter，这在 SavingsAccount.AccumulateInterest 中发生了，Balance 位于赋值运算符的左侧。（属性和 protected 关键字在第一册中。你可以在本书的索引中查找它们。）

## 第 7 章：多态——什么？

### 本章内容

- 决定是否隐藏或重写基类方法（选择真多！）
- 构建抽象类——你认真的吗？
- 声明一个方法及其所在类为抽象
- 使用 ToString，类的名片
- 将类密封以防止被子类化

在继承中，一个类“采用”另一个类的成员。因此我可以创建一个 SavingsAccount 类，从基类 BankAccount 继承 account_id 等数据成员以及 Deposit() 等方法。这很有用，但这种继承的定义不足以模仿商业世界中正在发生的事情。

> 提示：如果您对类继承不太了解（或不记得），请参阅本小书的第 6 章。

微波炉是一种烤箱，不是因为它看起来像烤箱，而是因为它执行与烤箱相同的功能。微波炉可能执行额外的功能，但至少它执行基础烤箱功能——最重要的是，当我说“StartCooking”时加热我的 nachos。（我依靠我的 Refrigerator 类对象来冷却啤酒。）我不太关心烤箱内部必须做什么来实现这一点，就像我不关心它是什么类型的烤箱、谁制造的、或者我妻子买它时是否在打折一样。（嘿，等一下——我确实关心最后一点。）

从我们人类的角度来看，微波炉与传统烤箱之间的关系似乎没什么大不了的，但请从烤箱的角度考虑这个问题。传统烤箱内部执行的步骤与微波炉可能采取的步骤完全不同。

> 记住：继承的强大之处在于子类不必完全按照编写的方式继承基类的每一个方法。子类可以在实现细节不同的同时继承基类方法的本质。

