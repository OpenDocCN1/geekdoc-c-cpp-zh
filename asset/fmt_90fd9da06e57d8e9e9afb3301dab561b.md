
**图 11-25** `PriceListApplication2` 程序

# 第 11 章 异常处理

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_540_0.png)

514

**图 11-26** 当用户多次输入无效项目编号时 `PriceListApplication2` 程序的输出

# 两个真理一个假言

处理从外部方法抛出的异常

- 1. 当其他类的方法抛出异常时，这些方法不需要捕获它们；相反，你的调用程序可以捕获它们，由你决定如何处理。
- 2. 通常，你不希望被调用的方法处理它自己的异常；在许多情况下，你希望由调用程序以最适合应用程序的方式处理任何异常。
- 3. 当你设计包含可能抛出异常方法的类时，你几乎总是应该确保你的类恰当地处理每个异常。

> 虚假语句是 #3。当你设计包含可能频繁抛出异常方法的类时，你应该创建语句，以便那些可能抛出异常但不处理异常的方法能够运行。

# 通过调用栈跟踪异常对象

当一个方法调用另一个方法时，计算机操作系统必须跟踪方法调用的来源，并且在被调用方法完成后，程序控制必须返回到调用方法。例如，如果 `MethodA()` 调用了 `MethodB()`，操作系统

Copyright 2018 Cengage Learning. All Rights Reserved. 不允许全部或部分的复制、扫描或复制。WCN 02-200-202

必须“记住”在 `MethodB()` 结束后返回 `MethodA()`。同样，如果 `MethodB()` 调用了 `MethodC()`，那么在 `MethodC()` 执行期间，计算机需要“记住”它将返回到 `MethodB()` 并最终返回到 `MethodA()`。计算机存储必须返回的位置列表的内存位置被称为调用栈（call stack）。

如果一个方法抛出异常且未捕获，则异常将抛给调用栈“上方”的下一个方法；换句话说，它被抛给了调用该错误方法的方法。考虑以下事件序列：

- `MethodA()` 调用 `MethodB()`。
- `MethodB()` 调用 `MethodC()`。
- `MethodC()` 抛出一个异常 `Exception`。
- C# 在 `MethodC()` 中查找 `catch` 块。
- 如果不存在，则 C# 在 `MethodB()` 中查找相同的内容。
- 如果 `MethodB()` 没有针对该异常的 `catch` 块，则 C# 查找 `MethodA()`。
- 如果 `MethodA()` 没有捕获该异常，程序将终止，操作系统将显示错误消息。

这种通过调用方法链传递异常的系统被称为异常传播（propagating the exception）。它具有巨大的优势，因为它允许你的方法更恰当地处理异常。然而，一个使用多个类的程序可能会让程序员难以定位异常的源头。

你已经使用过 `Message` 属性来获取异常对象的信息。`StackTrace` 属性是另一个异常属性。当你捕获一个异常时，可以使用 `StackTrace` 的值提供调用栈中的方法列表，以便你确定创建异常的位置。

`StackTrace` 属性是一个非常有用的调试工具。当程序突然停止时，发现异常发生的方法很有帮助。通常，你不想在完成的程序中显示 `StackTrace` 属性；普通用户对晦涩的消息毫无，但在你开发程序时，使用 `StackTrace` 可以帮助你诊断问题。

# 案例研究：使用 StackTrace

考虑 `StackTrace` 有用的一个例子，图 11-27 中的 `Tax` 类。假设你的公司创建或发布了这个类，用于计算销售产品的税率。为了简单起见，假设只有两种税率——20美元或以下销售额为6%，超过20美元的销售额为7%。对于任何编写涉及产品销售程序的人来说，`Tax` 类都是有用的，但有一个缺陷：

阴影语句中的下标对于较高的税率被错误地设置为 2 而不是 1。如果在下一条语句中使用 `taxRate` 数组使用此下标，它将越界。

```csharp
class Tax {
    private static double[] taxRate = {0.06, 0.07};
    private static double CUTOFF = 20.00;
    public static double DetermineRate(double price)
    {
        int subscript;
        double rate;
        if(price <= CUTOFF)
            subscript = 0;
        else
            subscript = 2;
        rate = taxRate[subscript];
        return rate;
    }
}
```

图 11-27 `Tax` 类

假设你的公司还创建了一个修订后的 `PriceList` 类，如图 11-28 所示。该类与图 11-22 中的类类似，但包含了税费计算并在阴影语句中调用了 `DetermineTaxRate()` 方法。

```csharp
class PriceList {
    private static double[] price = {15.99, 27.88, 34.56, 45.89};
    public static void DisplayPrice(int item)
    {
        double tax;
        double total;
        double pr;
        pr = price[item];
        tax = pr * Tax.DetermineRate(pr);
        total = pr + tax;
        WriteLine("The total price is " + total.ToString("C"));
    }
}
```

图 11-28 包含对 `Tax` 方法调用的 `PriceList` 类

假设你编写了图 11-29所示的应用程序。你的应用程序在本章早期创建的价格列表类似，包括对 `PriceList.DisplayPrice()` 的调用。与 `PriceListApplication1` 和 `PriceListApplication2` 一样，你的新程序准备好输入并显示，然后捕获异常。当你使用已知良好的项目编号运行程序时，如图 11-30 所示，你会惊讶地看到你在 `catch` 块中编写的阴影“Error!”消息。在之前使用 `PriceList.DisplayPrice()` 的示例中，使用项目编号1将导致程序成功执行。

```csharp
using System;
using static System.Console;
class PriceListApplication3
{
    static void Main()
    {
        int item;
        try
        {
            Write("Enter an item number >> ");
            item = Convert.ToInt32(ReadLine());
            PriceList.DisplayPrice(item);
        }
        catch (Exception e)
        {
            WriteLine("Error!");
        }
    }
}
```

图 11-29 `PriceListApplication3` 程序

> 当你编译图 11-29 中的程序时，你会收到警告，称变量 `e` 已声明但从未未使用。如果你从 `catch` 块中省略项目 `e`，应用程序将以相同的方式执行且不会显示警告。

```
Enter an item number >> 1
Error!
```

图 11-30 当用户输入项目编号1时 `PriceListApplication3` 的执行

为了尝试发现导致 Error! 消息的原因，你可以将写入该消息的语句替换如下：

```
WriteLine(e.Message);
```

当将显示 `e.Message` 的语句添加到价格列表程序时，编译程序时不再出现“e 从未被使用”的警告。

然而，当你执行程序显示 `e.Message` 时，你会收到图 11-31 所示的输出，这表明索引超出了数组边界。你感到困惑，因为你知道 1 是价格数组中的一个有效项目编号，它不应该被认为超出边界。

```
Enter an item number >> 1
Index was outside the bounds of the array.
```

**图 11-31** 执行修改后的价格列表应用程序，在 `catch` 块中显示 `e.Message`

最后，你决定将 `catch` 语句中的 `WriteLine()` 参数替换为 `StackTrace` 的调用，如下所示：

```
WriteLine(e.StackTrace);
```

输出如图 11-32 所示。你可以看到应用程序中的错误源自的方法列表：`Tax.DetermineTaxRate()`，它是由 `PriceList.DisplayName()` 调用的，后者又是由 `Main()` 调用的。注意，列表中最后一个的方法是最后执行的第一个方法。在使用 `StackTrace` 之前，你可能甚至没有考虑过 `Tax` 类可能是问题的根源。如果你在一个小型组织中工作，你可以查看代码并修复它。如果你在一个较大的组织中工作或从外部供应商购买了该类，你可以联系创建该类的程序员寻求帮助。

```
Enter an item number >> 1
at Tax.DetermineTaxRate(Double price)
at PriceList.DisplayName(Int32 item)
at PriceListApplication3.Main()
```

**图 11-32** 执行修改后的价格列表应用程序，在 `catch` 块中显示 `e.StackTrace`

此示例中的类较小，以便你轻松跟随讨论。然而，现实世界的应用程序可能包含许多类，其中包含更多方法，因此使用 `StackTrace` 将变得越来越有益。在一个大型程序系统中，你可能会发现，测试时策略性地在整个程序定位 `StackTrace` 是非常有用的，并在程序完成后将其删除或注释掉。

观看视频：通过调用堆栈跟踪异常（Tracing Exceptions Through the Call Stack）。

### 真一假
**通过调用堆栈跟踪异常对象**

- 1. 计算机存储在系列方法调用后系统必须返回的位置列表的内存位置称为堆栈跟踪（stack trace）。
- 2. 如果一个方法抛出异常且没有捕获它，则异常将抛给调用该错误方法的方法。
- 3. 当你捕获 `Exception` 对象时，你可以输出 `StackTrace` 的值以显示调用堆栈中的方法列表，以便你确定错误的位置。

> 称为调用堆栈（call stack）。
> 在系列方法调用后系统必须返回的位置列表
错误的陈述是 #1。内存位置是计算机存储……的地方。

# 创建你自己的异常类

C# 提供了超过 100 种类别的异常（Exceptions），你可以在程序中抛出它们。然而，C# 的创建者无法预测你编写的程序中可能出现异常的每一种。例如，当银行余额为负数或外部实体尝试访问你的电子邮件帐户时，你可能想要创建一个异常。大多数组织对异常数据有特定规则，例如“员工编号不能超过三位数字”或“时薪必须低于最低工资”。当然，你可以用 `if` 语句处理这些潜在的错误情况，但你也可以创建自己的 `Exception` 子类。

要从一个可以实例化可抛出对象的自定义异常类型，你可以扩展 `Exception` 类（它是 `Exception` 的子类），或者你可以扩展 `Exception`。微软对此的建议随着时间推移发生了变化。

# 第 11 章 异常处理

在他人编写的类中你可能会看到 `ApplicationException` 的扩展，目前的建议是直接从 `Exception` 派生你自己的类。任何一种方法都会产生可以工作的程序。

11-33 显示了一个扩展 `Exception` 的 `NegativeBalanceException` 类。该类向其父类的构造函数传递了一个适当的字符串消息。如果你创建一个 `Exception` 对象并设计其 `Message` 属性，你将在应用程序中看到错误。当 `NegativeBalanceException` 构造函数传递字符串 "Bank balance is negative" 时，`Message` 属性将持有这个具描述性的消息。C# 文档建议你创建的所有异常子类消息都应该是语法上正确的、以句号结尾的完整句子。

```cs
class NegativeBalanceException : Exception
{
    private static string msg = "Bank balance is negative.";
    public NegativeBalanceException() : base(msg)
    {
    }
}
```

**图 11-33** `NegativeBalanceException` 类

当你创建一个像图 11-34 所示的 `BankAccount` 类时，你可以创建 `Balance` 属性设置器，当客户端尝试将余额设置为负数时抛出 `NegativeBalanceException`。

与其在图 11-34 的属性中创建 `nbe` 对象，你可以编写以下语句，它在一步内创建并抛出一个匿名的 `NegativeBalanceException`：`throw(new NegativeBalanceException());`。

微软文档建议为你创建的每个异常类创建三个构造函数：默认构造函数、一个接收字符串消息的构造函数，以及一个接收字符串消息和内部异常的构造函数。为了保持此示例简单，图 11-33 中的 `NegativeBalanceException` 仅包含一个构造函数。

11-35 显示了一个尝试将 `BankAccount` 余额设置为某个值的程序。当 `BankAccount` 类设置器抛出 `NegativeBalanceException` 时，`TryBankAccount` 中的 `catch` 块会执行，显示 `Message` 和 `StackTrace`。图 11-36 显示了输出。

```cs
using System;
using static System.Console;
class BankAccount
{
    private double balance;
    public int AccountNum {get; set;}
    public double Balance
    {
        get
        return balance;
    }
    set
    {
        if(value < 0)
        {
            NegativeBalanceException nbe = new NegativeBalanceException();
            throw(nbe);
        }
        balance = value;
    }
}
```

**图 11-34** `BankAccount` 类

```cs
using System;
using static System.Console;
class TryBankAccount
{
    static void Main()
    {
        BankAccount acct = new BankAccount();
        try
        {
            acct.AccountNum = 123;
            acct.Balance = -1000;
        }
        catch(NegativeBalanceException e)
        {
            WriteLine(e.Message);
            WriteLine(e.StackTrace);
        }
    }
}
```

**图 11-35** `TryBankAccount` 程序

```
Bank balance is negative.
at BankAccount.set(Double value)
at TryBankAccount.Main()
```
