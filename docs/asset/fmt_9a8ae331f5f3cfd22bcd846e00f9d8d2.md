
在带有 `Main()` 的程序底部，以便你更好地看到问题。程序开始时创建一个 `Student` 对象并初始化其名称。这个简单的程序现在想做的只是输出由短消息和横幅产生的内容。

`Main()` 首先使用类或静态方法的方法输出横幅和消息。程序调用 `OutputBanner()` 方法输出横幅，调用 `OutputName()` 方法输出消息和学生姓名。`OutputBanner()` 方法向控制台输出一条简单的消息。`Main()` 将 `student` 作为参数传递给 `OutputName()`，以便它能够显示学生的名字。

接下来，`Main()` 通过调用 `student.OutputBannerAndName()` 使用实例方法输出横幅和消息。

`OutputBannerAndName()` 首先调用了静态的 `OutputBanner()`。假设类为 `Student`。没有传递对象，因为静态的 `OutputBanner` 不需要对象。接下来，`OutputBannerAndName()` 调用了 `OutputName()` 方法。`OutputName()` 也是一个静态方法，但它接受一个 `Student` 作为参数。`OutputBannerAndName()` 为该参数传递了它。

一个更有趣的情况是从 `OutputName()` 中调用 `ToString()`。`OutputName()` 被声明为静态的，因此没有 `this`。它有一个显式的 `Student` 对象，并使用它进行调用。

`OutputBanner()` 方法可能也会调用 `ToString`；然而，它没有 `Student` 可以使用。它没有引用，因为它是一个静态方法，并且没有被显式传递对象。注意示例代码中的第一行粗体字：静态方法无法调用实例。

静态方法无法在不显式提供对象的情况下调用非静态方法。没有对象，就没有调用。通常情况下，静态方法无法访问类中的任何非静态项。但非静态（实例）方法既可以访问静态也可以访问实例项：静态数据成员和静态方法。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_284_0.png)

| 第二卷 第 4 章 |
| :--- |
| 让我来说吧 |

## 第 5 章：让类对其负责

## 本章内容

- 通过访问控制让类自我保护
- 引入属性，一种特殊的方法
- 允许对象通过构造函数进行自初始化
- 为同一个类定义多个构造函数
- 构建静态或类成员

一个类必须对自己的行为负责。就像微波炉在你按错按键时不应该突然起火一样，一个类在面对错误数据时也不应该允许自己崩溃而亡。

为了对自己的行为负责，类必须确保其初始状态是正确的，并控制其后续状态以保持有效性。C# 提供了这两种能力。

## 限制对类成员的访问

简单的类将所有成员定义为 `public`。考虑一个银行账户程序，它维护一个名为 `balance` 的成员来保留每个账户的余额。将该数据成员公开化是让每个人都遵守信用制度。

我不清楚你的银行如何，但我的银行可不会慷到留下一堆钱和一个账本，让我每次从堆里加钱或取钱时都做标记。毕竟，我可能会忘记在账本上记录我的取款。

控制访问可以避免小错误，例如忘记在此处或那里记录取款，并成功地避免了一些取款方面的真正大错误。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_286_0.png)

我完全清楚你们这些在想什么：“只需加一条规则让其他类不能直接访问 `balance` 数据成员就就行了。”这种方法在理论上可能可行，但在实践中，从未、从未生效（262 限制对类成员的访问）。人们开始时有着良好的意图（比如我每天工作的意图），但这些良好的意图会被出门的日程压力重量所击碎。说起重量……

### 公开 BankAccount 的公开示例

下面的 `BankAccount` 类示例声明了它的所有方法为 `public`，并声明了它的数据成员 `_accountNumber` 和 `_balance`。注意，我故意让它处于一个错误状态以说明问题。以下代码块无法正确编译：

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_287_0.png)

```csharp
// 使用 double 变量创建银行账户

// 以存储账户余额（将余额保持在私有变量中

// 以向外部隐藏其实现细节）

// 注意：在你修正它之前，此程序将无法编译

// 因为 Main() 引用了 BankAccount 类的私有成员。

namespace BankAccount {

    public class Program {

        public static void Main(string[] args) {

            Console.WriteLine("This program doesn't compile in its state.");

            Console.WriteLine("Create a bank account object");

            BankAccount ba = new BankAccount();

            ba.InitBankAccount();

            // 通过 Deposit() 方法访问余额是可以的

            ba.Deposit() has access to all the data members.

            ba.Deposit(10);

            // 直接访问数据成员是编译错误。

            Console.WriteLine("Just in case you get this far supposed to generate a error");

            ba._balance = it;

            // 等待用户确认结果。

            Console.WriteLine("Press Enter to terminate...");

            Console.Read();

        }

    }

classBankAccount {

    // 定义一个表示简单账户的类。

    private int _nextAccountNumber = 1000;

    private int _accountNumber;

    // 将余额保持为 double 变量。

    private double _balance;

    // Init - 使用下一个 id
    // 和 0 余额初始化银行账户。

    public void InitBankAccount() {

        _accountNumber = ++nextAccountNumber;

        _balance = 0.0;

    }

    // GetBalance - 返回当前余额。

    public double GetBalance() {

        return _balance;

    }

}
```

* 限制对类成员的访问 263

```csharp
// AccountNumber
public int GetAccountNumber()
{
    return _accountNumber;
}
public void SetAccountNumber(int accountNumber)
{
    this._accountNumber = accountNumber;
}

// Deposit - 允许任何正数存款。
public void Deposit(double amount)
{
    if (amount > 0.0)
    {
        _balance += amount;
    }
}

// Withdraw - 你可以提取任何小于等于余额的
// 金额；返回提取的金额。
public double Withdraw(double withdrawal)
{
    if (_balance <= withdrawal)
    {
        withdrawal = _balance;
    }
    _balance = withdrawal;
    return withdrawal;
}

// GetString - 将账户数据作为字符串返回。
public string GetString()
{
    string s = String.Format("{#{0} = ({1}:C)}",
                               GetAccountNumber(), GetBalance());
    return s;
}
```

在这个代码示例中，`_balance -= withdrawal` 等于 `_balance`。（C# 程序员倾向于使用最简短的符号。）

标记一个成员使得该成员对程序中的任何其他代码可用。

`BankAccount` 类提供了一个 `InitAccount()` 方法来初始化类的成员，一个 `Deposit()` 方法来处理存款，以及 `Withdraw()` 方法提供了一些基本的规则，例如“你不能存款负数”（我确定这对于银行来说都是好规则）。然而，只要 `_balance` 对外部方法可见，每个人都必须遵守信用制度。（在此语境下，外部意味着“类外部但在同一程序内部”。）

## 264 限制类成员的访问

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_289_0.png)

编写良好的代码可以通过编译器可以强制执行的规则来约束从偶尔出现的子弹到大脚趾的每一个人。

在你感到太兴奋之前，请注意程序无法编译。尝试生成此代码时会产生此错误消息：

```
'BankAccount.BankAccount._balance' is inaccessible due to its protection level.
```

我不明白为什么它不直接说：“嘿，这是私有的，别乱碰。”语句 `ba_balance += 10;` 是非法的，因为 `ba_balance` 对于 `Main()` 方法是不可访问的，它是 BankAccount 类之外的方法。将此行替换为 `ba.Deposit(10)` 解决了问题。`BankAccount.Deposit()` 方法是公共的，因此 `Main()` 以及程序的其他部分都可以访问。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_289_1.png)

不显式声明类成员的访问类型等于声明了它。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_289_2.png)

默认访问类型是私有的。但是，你应该包含私有关键字以消除任何疑虑。优秀的程序员会让他们的意图显式化，这是减少错误的另一种方法。

## 跳过——其他安全级别

理解这一节取决于你是否具备一些继承知识（见本手册第 6 章）和命名空间知识（本手册第 10 章）。如果你愿意，可以跳过这一节，但只需知道当你需要时它在这里。

C# 提供了这些级别的安全：

- 公共（public）成员可以被程序中的任何类访问。
- 私有（private）成员仅可从当前类访问。
- 保护（protected）成员可以从当前类及其任何子类访问。
- 内部（internal）成员可以从同一个程序或程序集中的任何类访问。

C# 的“模块”或程序集（assembly）是一个独立编译的代码单元。可以是 `.EXE` 文件中的可执行程序，也可以是 `.DLL` 文件中的支持库模块。单个命名空间可以跨越程序集（本手册第 10 章解释了 C# 程序集和命名空间，并讨论了公共和私有之外的访问级别）。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_289_3.png)

- 内部保护（internal protected）成员可以从当前类和任何子类，以及从同一模块内的类访问。

## 为什么你应该关注访问控制

### 265

通过将成员声明为私有来隐藏提供了最大的安全性。然而，在许多情况下，你不需要那种级别的安全性的。毕竟，子类的成员已经依赖于基类的成员，因此保护（protected）提供了一个舒适的安全级别。

## 为什么你应该关注访问控制

将类的内部成员声明为公共是一个坏主意，至少出于以下原因：

- 如果所有数据成员都是公共的，你就无法轻易确定数据成员是在何时以及如何被修改的。为什么不在 `Deposit()` 和 `Withdraw()` 方法中加入更好的安全检查呢？事实上，有了这些方法会更好吗？类的任何方法都可以随时修改这些元素。如果其他方法可以访问这些元素，它们几乎肯定会胜出。

你的 `BankAccount` 程序可能运行了一个小时，你才注意到其中一个账户的余额为负数。`Withdraw()` 方法本可以确保这种情况不会发生，所以显然是另一个方法在没有通过 `Withdraw()` 的情况下访问了余额。找出哪个方法在什么条件下负责此是一个问题。

- 暴露类的所有成员会使接口变得过于复杂。作为一个使用 `BankAccount` 类的程序员，你不想知道类的内部工作原理。你只需要知道你可以存款和取款。这就像一台有 50 个按钮的糖果机，而不是只有你需要的几个。

- 暴露内部元素可能会导致类规则的破坏。例如，我的 `BankAccount` 类在任何情况下都不允许余额为负。这个业务规则应该被隔离在 `Withdraw()` 方法内部。否则，你必须在更新余额的地方添加此检查。

有时，通过使用访问修饰符，你可以防止你的类以无效的方式使用。例如，我的 `BankAccount` 类在任何情况下都不允许余额为负。这个业务规则应该被隔离在 `Withdraw()` 方法内部。否则，你必须在更新余额的地方添加此检查。

通过使用访问修饰符，你可以防止你的类以无效的方式使用。例如，我的 `BankAccount` 类在任何情况下都不允许余额为负。这个业务规则应该被隔离在 `Withdraw()` 方法内部。否则，你必须在更新余额的地方添加此检查。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_290_0)

### 291

## 266 为什么你应该关注访问控制

### 访问器方法

getter（获取器）是一个返回私有字段值的方法。相反，setter（设置器）是一个设置私有字段值的方法。在 C# 中，属性（properties）用于实现 getter 和 setter。属性是一种特殊的成员，看起来像数据字段，但可以使用赋值运算符进行读取或写入。

```csharp
public class BankAccount {
    private double _balance;
    public double Balance {
        get { return _balance; }
        set { _balance = value; }
    }
}
```

上面的代码定义了一个名为 `Balance` 的属性，带有一个 getter 和一个 setter。这允许外部代码读取和设置 `_balance` 字段，同时保持该字段为私有。

```csharp
BankAccount account = new BankAccount();
account.Balance = 1000;
Console.WriteLine(account.Balance);
```

然而，属性还允许向 setter 中添加逻辑。例如：

```csharp
public class BankAccount {
    private double _balance;
    public double Balance {
        get { return _balance; }
        set {
            if (value < 0) {
                throw new ArgumentException("Balance cannot be negative");
            }
            _balance = value;
        }
    }
}
```

这确保了余额永远不会被设置为负值。这是为什么属性比使用公共字段更好的原因之一。它们允许你封装逻辑并提供整洁的接口。

```csharp
public class BankAccount {
    private double _balance;
    public double Balance {
        get { return _balance; }
        set {
            if (value < 0) {
                throw new ArgumentException("Balance cannot be negative");
            }
            _balance = value;
        }
    }
    public void Deposit(double amount) {
        _balance += amount;
    }
    public void Withdraw(double amount) {
        if (_balance - amount < 0) {
            throw new InvalidOperationException("Insufficient funds");
        }
        _balance -= amount;
    }
}
```
