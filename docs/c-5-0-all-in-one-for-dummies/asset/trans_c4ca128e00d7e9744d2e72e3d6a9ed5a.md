
```csharp
{
    public SubClass()
    {
        Console.WriteLine("Constructing SubClass (default)");
    }
    public SubClass(int i)
    {
        Console.WriteLine("Constructing SubClass (int)");
    }
}
```

执行此程序将生成以下结果：

```text
Invoking SubClass()
Constructing BaseClass (default)
Constructing SubClass (default)

Invoking SubClass(int)
Constructing BaseClass (default)
Constructing SubClass (int)
Press Enter to terminate...
```

程序首先创建一个默认对象。正如预期，C# 调用默认的 SubClass 构造函数，该构造函数先将控制权传递给默认的 BaseClass 构造函数。然后程序创建一个对象，并传入一个整数参数。同样如预期，C# 调用 SubClass(int) 构造函数。该构造函数调用默认的 BaseClass 构造函数，和前面的示例一样，因为它没有要传递的数据。

## 用 base 指定具体基类

子类构造函数可以使用 base 关键字调用特定的基类构造函数。

此功能类似于同一类中的一个构造函数使用 this 关键字调用另一个构造函数。

例如，考虑这个小程序 InvokeBaseConstructor：

```csharp
// InvokeBaseConstructor -- Demonstrate how a subclass can
//    invoke the base class constructor of its choice
//    using the base keyword.
using System;
namespace InvokeBaseConstructor
{
    public class BaseClass
    {
        public BaseClass()
        {
            Console.WriteLine("Constructing BaseClass (default)");
        }
        public BaseClass(int i)
        {
            Console.WriteLine("Constructing BaseClass({0})", i);
```

![](img/80ff26f06fc9ab951e1cd4257b867366_322_0.png)

![](img/80ff26f06fc9ab951e1cd4257b867366_322_1.png)

![](img/80ff26f06fc9ab951e1cd4257b867366_322_2.png)

不过，SavingsAccount 构造函数可以将信息传回 BankAccount 构造函数。这里只显示 Main() 和构造函数本身：

![](img/80ff26f06fc9ab951e1cd4257b867366_324_0.png)

```csharp
// ConstructorSavingsAccount -- Implement a SavingsAccount as
// a form of BankAccount; use no virtual methods, but
// implement the constructors properly.
using System;
namespace ConstructorSavingsAccount
{
    // BankAccount -- Simulate a bank account, each of which carries an
    // account ID (which is assigned upon creation) and a balance.
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
        // balance; return the amount withdrawn.
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
            return String.Format("{0} ({1})",
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
}
```

BankAccount 定义了两个构造函数：一个接受初始账户余额，另一个是默认构造函数，不接受初始余额。为了避免在构造函数内重复代码，默认构造函数使用 this 关键字调用 BankAccount(initial balance) 构造函数。

## 垃圾回收与 C# 析构函数

C# 提供了一种与构造函数相反的方法：析构函数。它的名称是类名前面加一个波浪号（~）。例如，~BaseClass() 方法是 BaseClass 的析构函数。

C# 在不再使用对象时调用析构函数。默认析构函数是唯一可以创建的析构函数，因为析构函数不能被直接调用。此外，析构函数始终是虚函数。

当涉及类的继承层次时，析构函数的调用顺序与构造函数相反。也就是说，子类的析构函数先于基类的析构函数被调用。

C# 中的析构函数方法远不如在 C++ 等其他面向对象语言中有用，因为 C# 具有非确定性析构。理解这个术语的含义——以及它为什么重要——需要一些解释。

当程序执行 new 命令（例如 new SubClass()）时，对象的内存从堆中借用。只要任何正在运行的程序使用对该内存的有效引用，这块内存就会保持保留状态。可能有多个变量引用同一个对象。

当最后一个引用超出作用域时，该内存被称为不可达。换句话说，在不再存在对该内存块的引用后，任何人都无法访问它。

当内存块首次变为不可达时，C# 不会做任何特别的事情。一个低优先级系统任务在后台执行，寻找不可达的内存块。为了避免对程序性能产生负面影响，这个“垃圾回收器”会在程序中活动很少时执行。当垃圾回收器找到不可达的内存块时，会将它们归还给堆。

通常，垃圾回收器在后台静默运行。只有当堆内存开始耗尽时，垃圾回收器才会在短时间内接管程序的控制权。

C# 析构函数——例如 ~BaseClass()——是非确定性的，因为它要等到对象被垃圾回收时才会被调用，而该任务可能在对象不再被使用很久之后才发生。事实上，如果程序在对象被找到并归还给堆之前终止，析构函数就永远不会被调用。非确定性意味着你无法预测对象何时会被垃圾回收。对象被垃圾回收并调用其析构函数之前，可能经过相当长的时间。

C# 程序员很少使用析构函数。C# 还有其他方法可以在不再需要借用的系统资源时归还它们，例如使用 Dispose() 方法，该主题超出了本书的范围。（你可以在帮助中搜索术语 Dispose 方法。）

