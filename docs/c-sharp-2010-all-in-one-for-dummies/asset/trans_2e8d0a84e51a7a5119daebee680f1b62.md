
在 Treat Warnings As Errors 部分，选择 All。（如果某个警告变得烦人，你可以将其列在 Suppress Warnings 框中以免它出现在眼前。）当你将警告视为错误时，你被迫修复警告——就像你被迫修复真正的编译器错误一样。这种做法能写出更好的代码。即使你不启用 Treat Warnings As Errors 选项，也请将 Warning Level 保持在 4，并在每次构建后选择 Error List 窗口。

描述符 new，如以下示例代码所示，告诉 C# 方法的隐藏是有意为之，而不是疏忽的结果（并且它会使警告消失）：

```csharp
// No withdraw() pains now.
new public decimal Withdraw(decimal withdrawal)
{
    // . . . no change internally . . .
}
```

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_338_0.png)

此处关键字 new 的用法与用于创建对象的同名单词 new 无关。（C# 甚至连自己都重载了！）

## 回调到基类

查看本章前面展示的 HidingWithdrawal 示例中的 SavingsAccount.Withdraw() 方法。从此新方法内部对 BankAccount.Withdraw() 的调用包含了关键字 base。

以下没有 base 关键字的该方法版本无法工作：

```csharp
new public decimal Withdraw(decimal withdrawal)
{
    decimal amountWithdrawn = Withdraw(withdrawal);
    amountWithdrawn += Withdraw(1.5);
    return amountWithdrawn;
}
```

此调用与以下调用有相同的问题：

```csharp
void fn()
{
    fn(); // Call yourself.
}
```

从 fn() 内部对 fn() 的调用最终会反复调用自身（递归）。同样地，方法内部对 Withdraw() 的调用也会在循环中调用自身，程序最终会崩溃。

无论如何，你需要告诉 C#，从 SavingsAccount.Withdraw() 内部的调用旨在调用基类 BankAccount.Withdraw() 方法。一种方法是在调用前将 this 引用强制转换为 BankAccount 类的对象：

```csharp
// Withdraw -- This version accesses the hidden method in the base
//    class by explicitly recasting the this object.
new public decimal Withdraw(decimal withdrawal)
{
    // Cast the this reference into an object of class BankAccount.
    BankAccount ba = (BankAccount)this;
    // Invoking Withdraw() using this BankAccount object
    // calls the method BankAccount.Withdraw().
    decimal amountWithdrawn = ba.Withdraw(withdrawal);
    amountWithdrawn += ba.Withdraw(1.5);
    return amountWithdrawn;
}
```

此解决方案可行：调用 ba.Withdraw() 现在会调用 BankAccount 方法，正如预期的那样。此方法的问题在于对 BankAccount 的显式引用。程序的未来更改可能会重新排列继承层次结构，使得 SavingsAccount 不再直接继承自 BankAccount。这种类型的重新排列会以未来程序员可能难以发现的方式破坏此方法。（天哪，我永远也找不到这种 bug。）

你需要一种方法告诉 C# 调用层次结构中“紧邻上方”的类的 Withdraw() 方法，而无需显式命名它。那就是 SavingsAccount 扩展的类。C# 为此提供了关键字 base。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_339_0.png)

此关键字 base 与构造函数用于向其基类构造函数传递参数时使用的关键字相同。

以下代码片段中显示的 C# 关键字 base 与 this 类似，但无论该类是什么，都会自动强制转换为基类：

```csharp
// Withdraw -- You can withdraw any amount up to the
//    balance; return the amount withdrawn.
new public decimal Withdraw(decimal withdrawal)
{
    // Take the $1.50 off the top.
    base.Withdraw(1.5M);
    // Now you can withdraw from what's left.
    return base.Withdraw(withdrawal);
}
```

调用 base.Withdraw() 现在会调用 BankAccount.Withdraw() 方法，从而避免了递归“自我调用”问题。此外，如果继承层次结构发生变化，此解决方案也不会失效。

## 多态

你可以在子类中用同名方法重载基类中的方法。听起来这个过程很简单，但它引入了相当大的能力，而能力越大，危险越大。

这里有一个思想实验：你应该在编译时还是运行时决定调用 BankAccount.Withdraw() 还是 SavingsAccount.Withdraw()？

为了说明区别，我以一种看似无害的方式更改了之前的 HidingWithdrawal 程序。我将此新版本称为 HidingWithdrawalPolymorphically。（我通过省略不发生变化的部分精简了列表。）新版本如下所示：

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_340_0.png)

// HidingWithdrawalPolymorphically -- Hide the Withdraw() method in the base class with a method in the subclass of the same name.
// class Program
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

        // Create a bank account, withdraw $100, and
        // display the results.
        ba = new BankAccount(300M);
        MakeAWithdrawal(ba, 100M);

        // Try the same trick with a savings account.
        sa = new SavingsAccount(200M, 12);
        MakeAWithdrawal(sa, 100M);

        // Display the resulting balance.
        Console.WriteLine("When invoked through intermediary:");
        Console.WriteLine("BankAccount balance is {0:C}", ba.Balance);
        Console.WriteLine("SavingsAccount balance is {0:C}", sa.Balance);

        // Wait for user to acknowledge the results.
        Console.WriteLine("Press Enter to terminate...");
        Console.Read();
    }
}

以下程序的输出可能令人困惑，也可能不困惑，取决于你的预期：

When invoked through intermediary
BankAccount balance is $100.00
SavingsAccount balance is $100.00
Press Enter to terminate...

这次，而不是在 Main() 中执行取款，程序将银行账户对象传递给 MakeAWithdrawal() 方法。

第一个问题相当直接：为什么 MakeAWithdrawal() 方法甚至接受 SavingsAccount 对象，而它明明声明自己在寻找 BankAccount？答案很明显：‘因为 SavingsAccount IS_A BankAccount。’（参见本小书第 6 章。）

第二个问题比较微妙。当传入一个 `BankAccount` 对象时，`MakeAWithdrawal()` 调用 `BankAccount.Withdraw()`——这足够清楚。但当传入一个 `SavingsAccount` 对象时，`MakeAWithdrawal()` 调用的是同一个方法。它不应该调用子类中的 `Withdraw()` 方法吗？

控方打算证明调用 `ba.Withdraw()` 应该调用方法 `BankAccount.Withdraw()`。显然，`ba` 对象是一个 `BankAccount`。做任何其他事情只会混淆状态。辩方在 `Main()` 中有证人证明，尽管 `ba` 对象被声明为 `BankAccount`，但实际上它是一个 `SavingsAccount`。陪审团陷入僵局。两种论点同样有效。

在这种情况下，C# 站在了控方一边：两种可能性中更安全的做法是使用声明的类型，因为它避免了任何误解。对象被声明为 `BankAccount`，就这么定了。然而，这可能不是你想要的。

### 每次都使用声明的类型（这有错吗？）

在某些情况下，你不想选择声明的类型。你想要的（或者，引用流行乐队 Spice Girls 的歌词，“你真的、真的想要的”）是基于 *真实类型*——运行时类型——而不是声明的类型来做出调用。例如，你想使用存储在 `BankAccount` 变量中的 `SavingsAccount`。这种在 *在运行时决定* 的能力被称为 *多态*，或 *晚绑定*。每次都使用声明的类型被称为 *早绑定*，因为它听起来像是 *晚绑定* 的相反。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_341_0.png)

 ridiculous term *polymorphism* 来自希腊语：*Poly* 表示“多于一个”，*morph* 表示“转换”，而 *ism* 是一个相当无用的希腊语词。但我们只能接受它。

多态和晚绑定并不完全是同一个概念——但区别很微妙：

- *多态* 指的是在运行时决定调用哪个方法的一般能力。
- *晚绑定* 指的是语言实现多态的具体方式。

多态是面向对象（OO）编程强大之处的关键。它如此重要，以至于不支持它的语言不能自称是 OO 语言。（我认为这是 FDA 的规定：你不能给标签一个
