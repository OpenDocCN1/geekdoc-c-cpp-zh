

# 为什么你应该关注访问控制

将类的内部成员声明为 `public` 是一个坏主意，至少基于以下原因：

-   由于所有数据成员都是公开的，你无法轻易确定数据成员是在何时以及如何被修改的。为什么还要费力在 `Deposit()` 和 `Withdraw()` 方法中构建安全检查呢？事实上，甚至没必要纠结于这些方法呢？任何类的任何方法都可以随时修改这些元素。如果其他方法可以访问这些数据成员，它们几乎肯定会这样做。

你的 `BankAccount` 程序可能运行了一个小时左右后，你才发现其中一个账户的余额为负数。`Withdraw()` 方法本可以确保这种情况不会发生，所以显然是另一个方法在没有通过 `Withdraw()` 的情况下访问了余额。找出是哪个方法负责的以及在什么条件下发生的，是一个困难的问题。

-   暴露类的所有数据成员会让接口变得过于复杂。作为一个使用 `BankAccount` 类的程序员，你不想知道该类的内部工作原理。你只需要知道你可以存款和取款即可。这就像一台有 50 个按钮的糖果机与一台只有几个按钮（即你需要的那些按钮）的机器相比。

-   暴露内部元素会导致类规则的扩散。例如，我的 `BankAccount` 类在任何情况下都不允许余额为负数。这一所需的业务规则应该被隔离在 `Withdraw()` 方法内部。否则，你必须在每个更新余额的地方都添加此检查。

有时，银行决定更改规则，允许“优质客户”在短时间内持有略微的负余额，以避免无意的透支。这时，你必须搜索整个程序，更新每个访问余额的代码段，以确保安全检查已同步更改。

让你的类和方法的访问权限不要超过所需的范围。我给你这个建议，并不是为了引起你对窥探型黑客的恐慌，而是为了建议采取一种谨慎的步骤，帮助你在编写代码时减少错误。尽可能使用 `private`，然后根据需要升级为 `protected`、`internal`、`internal protected` 或 `public`。

![](img/6df7bb88e9302e98442acc219cfbd7fc_286_0.png)

# 访问器方法

如果你更仔细地观察 `BankAccount` 类，你会发现看到其他几个方法。其中一个 `GetString()` 返回账户的字符串版本，适用于向任何 `Console.WriteLine()` 进行显示。然而，如果 `BankAccount` 对象的内容无法访问，那么显示其内容可能会变得困难。类应该有权决定如何显示自己。

此外，你还看到了两个“get”（getter）方法 `GetBalance()` 和 `GetAccountNumber()` 以及一个“set”（setter）方法 `SetAccountNumber()`。你可能会奇怪，为什么我要费力将数据成员 `_balance` 声明为 `private`，却提供一个公开的 `GetBalance()` 方法来返回它的值。我有两个理由：

-   `GetBalance()` 没有提供修改 `_balance` 方法——它仅仅返回其值。余额是只读的。用银行来类比，你可以随时查看余额；你不能在不使用银行取款机制的情况下从账户中取钱。

-   `GetBalance()` 为外部方法隐藏了类的内部格式。`GetBalance()` 可能会通过读取收据、加上账户费用并考虑银行可能想要从余额中扣除的任何金额来执行大量的计算。外部方法不知道也不在乎。当然，你会在意收了哪些费用——除非换银行，否则你对它们无能为力。

最后，`GetBalance()` 提供了一种机制，可以在类内部进行更改而不需要更改 `BankAccount` 的使用者。如果联邦储蓄保险（FDIC）强制你的银行以不同的方式存储存款，该指令不应该改变你访问账户的方式。

# 访问控制救急——一个示例

下面的 `DoubleBankAccount` 程序演示了 `BankAccount` 程序中的一个潜在缺陷。整个程序都在我的网站上；然而，下面的列表仅显示了 `Main()`——这是程序中与之前的 `BankAccount` 程序不同的部分：

![](img/6df7bb88e9302e98442acc219cfbd7fc_287_0.png)

```
// DoubleBankAccount -- 使用 double 变量创建银行账户
//     存储账户余额（将余额保持在私有
//     变量中以向外部世界隐藏其实现）。
using System;
namespace DoubleBankAccount
{
    public class Program
```

```
{
    public static void Main(string[] args)
    {
        // 打开一个银行账户。
        Console.WriteLine("Create a bank account object");
        BankAccount ba = new BankAccount();
        ba.InitBankAccount();
        // 存款。
        double deposit = 123.454;
        Console.WriteLine("Depositing {0:C}", deposit);
        ba.Deposit(deposit);
        // 账户余额
        Console.WriteLine("Account = {0}", ba.GetString());
        // 这里就是问题所在。
        double fractionalAddition = 0.002;
        Console.WriteLine("Adding {0:C}", fractionalAddition);
        ba.Deposit(fractionalAddition);
        // 结果余额
        Console.WriteLine("Resulting account = {0}", ba.GetString());
        // 等待用户确认结果。
        Console.WriteLine("Press Enter to terminate...");
        Console.Read();
    }
}
```

`Main()` 方法创建一个银行账户并存入 $123.454，这是一个包含小数分的金额。然后 `Main()` 向余额中存入了一小部分分，并显示了结果余额。

该程序的输出如下：

```
Create a bank account object
Depositing $123.45
Account = #1001 = $123.45
Adding $0.00
Resulting account = #1001 = $123.45
Press Enter to terminate...
```

用户开始抱怨：“我无法对我的账单进行对账。”问题在于程序对金额进行了四舍入入。最简单的解决办法是使用 `decimal` 类型来处理余额，正如 `DoubleBankAccount` 程序所示。

