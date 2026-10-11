
```csharp
get { return _balance; }
}
```

```csharp
// Deposit -- 允许任何正数存款。
public void Deposit(decimal amount) {
    if (amount > 0) {
        _balance += amount;
    }
}
```

```csharp
// Withdraw -- 你可以提取余额范围内的任何
// 金额；返回账户取款金额。
public decimal Withdraw(decimal withdrawal) {
    if (Balance <= withdrawal) // 使用余额
        withdrawal = Balance;
    _balance -= withdrawal;
    return withdrawal;
}
```

```csharp
// 将账户字符串化。
public string ToString() {
    return String.Format("{0} - {1:C}",
        _accountNumber, Balance);
}
```

```csharp
// SavingsAccount -- 一个产生利息的银行账户
public class SavingsAccount : BankAccount {
    private decimal _interestRate;
    // SavingsAccount -- 输入 0 到 100 之间的利率。
    public void InitSavingsAccount(decimal interestRate) {
        _interestRate = interestRate;
    }
}
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_314_0.png)

# 290 继承 BankAccount 类（一个更复杂的示例）

```csharp
public void InitSavingsAccount(decimal initialBalance, decimal interestRate)
{
    InitBankAccount(initialBalance); // 注意对基类的调用。
    this._interestRate = interestRate / 100;
}

// AccumulateInterest -- 每个个周期调用一次。
public void AccumulateInterest()
{
    _balance = Balance + (decimal) * _interestRate;
}

// 将账户字符串化。
public string ToSavingsAccountString()
{
    return String.Format("{0} ({1}%",
    BankAccountString(), _interestRate * 100);
}
public class Program
{
    public static void main(string[] args)
    {
        // 创建一个银行账户并显示。
        BankAccount ba = new BankAccount(1000);
        ba.Deposit(100); // M 后缀表示 decimal 类型。
        Console.WriteLine("{0}*", ba.BankAccountString());
        // 现在是一个储蓄账户
        SavingsAccount sa = new SavingsAccount();
        sa.InitSavingsAccount(12.58);
        sa.AccumulateInterest();
        Console.WriteLine("{0}*", sa.ToSavingsAccountString());
        // 等待用户确认结果。
        Console.WriteLine("Press Enter to terminate..*");
        Console.ReadLine();
    }
}
```

`BankAccount` 类与本书中其他章节的某些类并无二。它开始处理具有初始余额的账户，另一部分则是那些必须忍受零初始余额的账户。注意，这个版本的 `BankAccount` 并没有利用微小和最大的构造函数优势。如果你读完整个章节，你就能明白为什么我们稍后选择“回退”一点一下了。

`Balance` 属性允许他人读取银行账户而不必直接修改它们。`Deposit()` 方法接受任何正数存款。`Withdraw()` 允许你提取任何想要的金额，只要你的账户中有足够的钱。（我的银行很不错，但没那么好。）  
`BankAccountString()` 创建一个描述账户的字符串。

`SavingsAccount` 类继承了 `BankAccount` 的所有优秀特性。它还添加了利率以及定期累积利息的能力。

![](img/36596fb11aa4233d5cabd6ddd1d82e8_315_0.png)

# IS_A 与 HAS_A — 我太困惑了 291

`Main()` 执行的操作尽可能少就尽可能少。它创建一个 `BankAccount`，显示该账户，创建一个 `SavingsAccount`，累积一个周期的利息并显示结果，括号内的意图如下：

```
Account 1001 - $200
Account 1002 - $212.50 (12.500%)
Press Enter to terminate...
```

注意 `InitSavingsAccount()` 方法调用了 `InitBankAccount()`。它初始化了特定的成员。`InitSavingsAccount()` 方法本可以直接初始化这些成员；然而，更好的做法是 `BankAccount` 应该负责这一点。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_316_0)

## IS_A 与 HAS_A — 我太困惑了

`SavingsAccount` 和 `BankAccount` 之间的 `IS_A` 关系是基础性的。在接下来的章节中，我将展示替代方案，即 `HAS_A` 关系看起来是怎样的。

这种 `IS_A` 关系由下面的代码展示：

```csharp
public class Program
{
    // 添加这个：
    public static void Deposit(BankAccount ba, decimal pay)
    {
        ba.Deposit(pay);
    }
    // 创建一个银行账户并显示它。
    BankAccount ba = new BankAccount();
    ba.InitBankAccount(1000);
    ba.Deposit(100);
    Console.WriteLine("{0}*", ba.BankAccountString());
    // 现在是一个储蓄账户
    SavingsAccount sa = new SavingsAccount();
    sa.InitSavingsAccount(12.58);
    sa.AccumulateInterest();
    Console.WriteLine("{0}*", sa.ToSavingsAccountString());
    // 等待用户确认结果。
    Console.WriteLine("Press Enter to terminate...");
    Console.ReadLine();
}
```

# IS_A 与 HAS_A — 我太困惑了 292

事实上，什么都没有改变。唯一的区别是所有的存款现在通过本地方法进行。注意（这里是重点）`Main()` 可以将银行账户或储蓄账户传递给 `Deposit()`，因为 `SavingsAccount IS_A BankAccount` 并被赋予了所有的权利权限。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_317_0.png)

# 使用包含访问 BankAccount

`SavingsAccount` 类本可以以不同的方式访问 `BankAccount` 的成员，如下代码所示，其中关键部分以**粗体**显示：

```csharp
// 一个产生利息的银行账户
public class SavingsAccount {
    // 注意下划线：这不是
    // SavingsAccount 类。
    public BankAccount _bankAccount; // 注意这个，包含的 BankAccount。
    public decimal _interest;
    // 输入以百分比表示的
    // 0 到 100 之间的利率。
    public void initSavingsAccount(BankAccount account, decimal interestRate) {
        _bankAccount = account;
        _interest = interestRate / 100;
    }
    // 累积利息 每个周期调用一次。
    public void updateInterest() {
        _bankAccount.Balance += _bankAccount.Balance * _interest;
    }
    // Deposit 允许任何正数存款。
    public void deposit(decimal amount) {
        // 委托给包含的 BankAccount 对象。
        _bankAccount.Deposit(amount);
    }
    // 你可以提取余额范围内的任何
    // 金额；返回提取的金额。
    public double withdraw(decimal withdrawal) {
        return _bankAccount.Withdraw(withdrawal);
    }
}
```

在这种情况下，`SavingsAccount` 包含一个数据成员 `bankAccount`（而不是继承自 `BankAccount`）。`bankAccount` 对象包含了储蓄账户所需的余额和账户信息。

# 什么时候用 IS_A，什么时候用 HAS_A 293

需要的。也就是说，`SavingsAccount` 需要余额，它会向包含的 `BankAccount` 请求该余额。

在这种情况下，你就说 `SavingsAccount` **HAS_A**（拥有）一个 `BankAccount`。硬核面向对象的笑话说，`SavingsAccount` 组合了（composes）`BankAccount`。也就是说，`SavingsAccount` 部分由一个 `BankAccount` 组成。

## HAS_A 关系

`HAS_A` 关系在根本上不同于 `IS_A` 关系。在接下来的应用程序代码段中，这种区别看起来并不糟糕：

```csharp
// 创建一个新的储蓄账户。
BankAccount ba = new BankAccount();
SavingsAccount sa = new SavingsAccount(); // SavingsAccount 的 HAS_A 版本
sa.SavingsAccount(ba, 5);
// 向其存入 100 元。
// 现在积累利息。
sa.AccumulateInterest();
```

问题在于，这个修改过的 `SavingsAccount` 不能作为 `BankAccount` 使用，因为它没有继承自 `BankAccount`。相反，它包含一个 `BankAccount` —— 这不是同一个概念。例如，这个代码示例：

```csharp
// DirectDeposit - 自动存入我的工资。
void DirectDeposit(BankAccount ba, int pay) {
    ba.Deposit(pay);
}
void SomeMethod() {
    // 下面的示例失败了。
    DirectDeposit(sa, 100);
    continue;
}
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_318_0.png)

`Deposit()` 不能接受 `SavingsAccount` 来代替 `BankAccount`。对于 C# 而言，两者之间不存在明显的联系，因为这里不涉及继承。不过，不要因为这种情况就认为包含是一个坏主意。你只需要以不同的方式处理这个概念才能使用它。

# 什么时候用 IS_A，什么时候用 HAS_A

`IS-A` 和 `HAS_A` 关系之间的区别不仅仅是软件便利性的问题。这种关系在现实世界中也有推论。

*

# 294 支持继承的其他特性

例如，福特 `Explorer` **IS_A**（是一种）汽车（当它是直立的时候）。`Explorer` **HAS_A**（拥有）一个发动机。如果你的朋友说“开你的车过来”，而你开着 `Explorer` 出现，他没有理由抱怨。然而，如果你怀里抱着你 `Explorer` 的发动机出现，他可能就有意见了。（或者至少你看起来是那样）。

`Explorer` 类应该继承 `Car` 类，这不仅是为了让 `Explorer` 能够访问 `Car` 的方法，也是为了表达两者之间的基本关系。

遗憾的是，初级程序员可能会让 `Car` 继承自 `Motor`，这就像给 `Car` 访问 `Motor` 的成员一样简单，而 `Car` 运行恰恰需要这些成员。例如，`Car` 可以继承 `Motor.Go()` 方法。然而，这凸显了这种方法的问题：尽管人类在语言中很粗心，但制造汽车并不等同于制造发动机。汽车的“运行”（go）操作完全依赖于发动机，但它们并不是同一个东西 —— 你还需要挂上变速箱挡、释放刹车并完成其他任务。

也许不仅如此，继承自 `Motor` 误解了事实。汽车根本不是发动机的一种类型。

软件的优雅性本身就是一个值得实现的目标。它增强了可理解性、可靠性和可维护性（并治愈消化不良和痛风）。

硬核面向对象极客为了更简单的程序设计，倾向于使用 `HAS_A` 而非 `IS_A`。但在合理的情况下要使用继承，在 `BankAccount` 层次结构中这可能是合理的。

# 支持继承的其他特性

C# 实现了一组旨在支持继承的特性。我将在接下来的章节中讨论这些特性。

## 可替换类程序

程序可以在调用基类对象的地方使用子类。例如，你可能已经在我的某一个示例中见过了。`SomeMethod()` 可以将 `SavingsAccount` 对象传递给 `DirectDeposit()` 方法，而该方法期望一个 `BankAccount` 对象。

你可以让这种转换更加显式：

```csharp
BankAccount ba;
SavingsAccount sa = new SavingsAccount(); // 原始的，不是 SavingsAccount
// 或者；
ba = sa; // 隐式地将子类转换为基类。
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_319_0.png)

# 支持继承的其他特性 295

```csharp
ba = (BankAccount)sa; // 但倾向于显式转换。
// 不可以；
s = ba;
s = (SavingsAccount)ba; // 错误：隐式将基类转换为子类
// 然而，允许显式转换。
```

第一行将一个 `SavingsAccount` 对象赋值给 `BankAccount` 变量。C# 为你转换了对象。第二行使用强制转换显式地转换对象。

最后两行尝试将 `BankAccount` 对象转换回 `SavingsAccount`。你可以完成此操作，但 C# 不会为你完成。这就像是将较大的数值类型（如 `double`）转换为较小的类型（如 `float`）。C# 没有实现它，因为该过程涉及数据丢失。

`IS-A` 属性不是自反的。也就是说，即使一个 `Explorer` 是一辆汽车，汽车也不一定是 `Explorer`。同样，`BankAccount` 不一定是 `SavingsAccount`，因此不允许隐式转换。最后一行是允许的，因为程序员表达了愿意“放手一”。她一定知道些什么。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_320_0.png)

# 运行时的无效情况

通常，将对象从 `BankAccount` 转换为 `SavingsAccount` 是一个危险的操作。考虑这个示例：

```csharp
public static void ProcessAmount(BankAccount bankAccount)
// 向账户存入大额。
bankAccount.Deposit(10000.0M);
// 如果对象是 SavingsAccount，现在收集利息。
SavingsAccount savingsAccount = (SavingsAccount)bankAccount;
savingsAccount.AccumulateInterest();
public static void TestCast()
{
```

```csharp
SavingsAccount sa = new SavingsAccount();
ProcessAmount(sa);
BankAccount ba = new BankAccount();
ProcessAmount(ba);
}
```
