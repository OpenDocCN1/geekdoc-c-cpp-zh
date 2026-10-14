
测试向 `AddTransaction` 方法传入了一个值。这个值表示你正在添加到账户中的交易金额。它是一个 `decimal` 值，意味着精度非常高，但这个金额没有关联的货币值。为简单起见，这里假设所有账户和交易均以美元为单位。

完成 Arrange 和 Act 阶段后，你就可以进入测试的最后一部分了。

## 断言预期结果

到目前为止，前面这两个阶段实际上都只是这个测试以及每个单元测试的关键部分——断言——的铺垫。断言会为整个测试提供成功（绿色指示）或失败（红色指示）。测试方法名再次作为你所做断言的参照点——即账户余额已经发生改变。在这种情况下，断言将对实际值和预期值进行比较。这是一种在基于状态的测试中常见的断言类型，这类测试的断言依赖于 SUT 的状态。这个特定的断言要求实际值和预期值相等。

`Account` 类的 `Balance` 属性将被查询以获取实际值，而你将提供一个常量作为预期值。这意味着你事先必须知道预期值，这是编写测试时需要考虑的一个关键因素。不应该通过代码推导预期值，而应提前知道预期值是什么。在本场景中，这很容易。给定一个新账户，其初始余额未指定，因此为零，如果你向该账户添加 $200.00，那么预期余额应该是什么？

$0.00 + $200.00 = $200.00

因此，你可以编写 Assert 阶段并完成你的 AAA 测试，如清单 4-3 所示。

**清单 4-3 单元测试中已添加对预期行为的断言。**

单击此处查看代码图片

```
[TestClass]
public class AccountTest
{
    [TestMethod]
    public void AddingTransactionChangesBalance()
    {
        // Arrange
        var account = new Account();

        // Act
        account.AddTransaction(200m);

        // Assert
        Assert.AreEqual(200m, account.Balance);
    }
}
```

这个测试现在可以运行了。通过运行测试，你可以验证被测系统的行为是否符合预期。

## 运行测试

测试编写完成后，你需要使用单元测试运行器来运行它。单元测试位于测试项目中，这些项目的输出是程序集，而不是可执行文件。这意味着测试项目不能自行运行，而必须作为输入提供给单元测试运行器。Microsoft Visual Studio 通过其集成的测试运行器支持 MSTest 单元测试，而其他一些类型的单元测试则需要插件才能在 Visual Studio 中提供集成支持。

在 Visual Studio 中，你可以通过从“测试”>“运行”菜单中选择一个选项来运行 MSTest 单元测试。目前，你可以选择“所有测试”选项，其快捷键为 Ctrl+R, A。运行 AAA 单元测试的输出如图 4-1 所示。

![](img/65c1bad7a6b3cffae8cbb79664f0708b_151_0.png)

**图 4-1 在 Visual Studio 集成的 MSTest 单元测试运行器中运行单元测试。**

测试运行器以主从视图显示你选择运行的单元测试。左侧窗格中列出了测试列表，右侧窗格中显示所选测试的更多详细信息。你可以看到该测试执行耗时 14 毫秒，这根本不算多。这正是编写单元测试的优势之一——与手动测试所需的工作量相比，运行数千个单元测试并不需要太长时间。

然而，请注意测试断言失败了，因为预期值 200 与实际提供的值不匹配。`account.Balance` 属性被用作断言的实际值，但它返回了 0。

这是因为你还没有实现 `Account` 类。清单 4-4 展示了到目前为止所需的最小 `Account` 类实现。

**清单 4-4 被测系统不需要在单元测试之前实现。**

单击此处查看代码图片

```
public class Account
{
    public void AddTransaction(decimal amount)
    {

    }

    public decimal Balance
    {
        get;
        private set;
    }
}
```

正如你所看到的，这个类在 `AddTransaction` 方法中没有对传入的交易金额做任何处理，`Balance` 只是一个默认的自动属性，不过具有私有 setter。为了让这个测试通过，你必须实现 `Account` 类，使其满足你当前的预期。

## 测试驱动开发

要编写单元测试，你并不需要先拥有被测系统的完整实现。在测试驱动开发（TDD）中，最好在编写单元测试之前不要有可工作的被测系统。当你使用 TDD 方式编写软件时，你会同步编写单元测试和生产代码，并为生产代码中每个类的每个方法所表现出的每个预期行为编写一个失败测试。该失败测试仅仅是因为生产代码尚不存在而失败。测试声明——即断言——生产代码应该以某种方式运行，但由于它尚不存在，测试便失败。当生产代码以最简单的方式实现以满足测试要求后，测试就会成功。

## 红、绿、重构！

到目前为止，通过 AAA 的 `AddingTransactionChangesBalance()` 测试所产生的成果，是一个名为“红、绿、重构”的三阶段流程的第一部分。

1. 编写一个针对 SUT 预期行为的失败测试。
2. 仅实现足以让新测试通过且不破坏已有成功测试的 SUT 代码。
3. 如果可以对 SUT 进行任何重构以改进其设计或整体质量，那么现在正是进行重构的时机。

第一阶段会生成一个失败的测试，测试运行器用红色图标指示。第二阶段让那个失败的测试通过，将图标变为绿色。第三阶段允许你一点一点地逐步改进生产代码，而不用担心破坏其功能。

要将失败测试从红变绿（从失败变成功），你需要查看该流程的第二阶段：仅实现足以让测试通过的 SUT 代码。由于目前这是唯一的测试，你无需担心会破坏任何已有的成功测试。

该测试所断言的行为是：当向新账户添加一笔金额为 200 的交易后，账户余额为 200。清单 4-5 展示了让单元测试通过所需的最低限度代码。

**清单 4-5 当测试从红变绿时，永远只做最低限度的实现。**

单击此处查看代码图片

```
public class Account
{
    public Account()
    {
        Balance = 200m;
    }

    public void AddTransaction(decimal amount)
    {

    }

    public decimal Balance
    {
        get;
        private set;
    }
}
```

已更改的代码以**粗体**突出显示。为了使测试从红色变为绿色，代码为 `Account` 类引入了一个默认构造函数，该构造函数将 `Balance` 属性初始化为 `200m`。为了证明这有效——测试现在通过了——图 4-2 显示了在重新运行失败的测试后 Visual Studio 测试运行器的屏幕截图。

![](img/65c1bad7a6b3cffae8cbb79664f0708b_153_0.png)

**FIGURE 4-2 The test does, indeed, now pass—but is it correct?**

在你为自己喝彩并进入最终的重构阶段之前，你应该评估这是否是实现测试指定的预期行为的正确方式。你可以通过添加另一个期望的形式的另一个单元测试来证明这不是正确的实现。

要添加的测试定义了给定新创建的 `Account` 对象时 `Balance` 字段的预期值。回想一下，在向账户添加 200 美元的交易后，`Balance` 字段的预期值是如何计算的；它包含了未指定的开户余额为零的假设。这是一种预期行为，就像其他任何行为一样，因此你应该编写一个测试来断言你对代码的期望是否得到正确实现。列表 4-6 显示了 AAA 模式应用于此类单元测试。

**LISTING 4-6 The Arrange part of this test is omitted.**

[Click here to view code image](#code-image)

```
[TestMethod]
public void AccountsHaveAnOpeningBalanceOfZero()
{
    // Arrange

    // Act
    var account = new Account();

    // Assert
    Assert.AreEqual(0m, account.Balance);
}
```

首先，注意测试方法的名字再次描述了它断言的预期行为。在这种情况下，单元测试的 Arrange 部分为空，这意味着 AAA 语法中的这一部分是可选的。正在测试的 SUT 的部分是其默认构造函数的行为，这是 Act 阶段与 SUT 的唯一交互。最后，断言将之前陈述的假设形式化，即新的 `Account` 的余额为 `0m`。

这个单元测试失败的事实，即使第一个单元测试通过，也表明第一个单元测试期望的实现是错误的。图 4-3 显示了 MSTest 运行器的输出。

![](img/65c1bad7a6b3cffae8cbb79664f0708b_154_0.png)

**FIGURE 4-3 The second unit test fails because of the implementation of the first unit test’s expectations.**

从这个位置，如果你将对 `Account` 类的先前更改恢复，你将使你的开户余额测试从红色变为绿色，同时正确地导致你的添加交易测试再次失败。通过这样做，你证明了你对开户余额测试的 `Account` 类的实现是正确的，但对添加交易测试的实现是错误的。

添加每个新测试的效果是为 SUT 的可行实现创建了进一步的约束。每个测试都带有对行为的期望，每个期望都需要在 SUT 中取得平衡。确保两个测试都通过的另一种最简单的可能实现如列表 4-7 所示。

**LISTING 4-7 Both tests now pass with this implementation, but is it correct?**

Click here to view code image

```
public class Account
{
    public void AddTransaction(decimal amount)
    {
        Balance = 200m;
    }

    public decimal Balance
    {
        get;
        private set;
    }
}
```

新账户的余额现在将在创建时为零，但在调用 `AddTransaction` 时会变为 `200m`。当然，尽管两个测试现在都通过了，直觉应该告诉这是绝对错误的。先写最简单的事情——而不是直接跳到明显的正确解决方案——的目的是从你的直觉中推导出编码断言。你能写另一个单元测试使其失败并证明此实现不正确吗？列表 4-8 显示了一个示例。

**LISTING 4-8 This test is identical to the prior version but has a different amount value.**

[Click here to view code image](#code-image)

```
[TestMethod]
public void Adding100TransactionChangesBalance()
{
    // Arrange
    var account = new Account();

    // Act
    account.AddTransaction(100m);

    // Assert
    Assert.AreEqual(100m, account.Balance);
}
```

此测试方法与第一个测试添加交易的功能相同，但它添加的是 100 美元而不是 200 美元的交易。虽然差异很小，但足以证明 `Account.AddTransaction` 方法是错误的。

不出所料，这个新测试失败了。如果你更改 `Account` 类，使值 `100m` 硬编码到 `AddTransaction` 方法中，你将使原始测试失败并使此测试从红色变为绿色。相反，你现在可以实现正确的解决方案，如列表 4-9 所示。

**LISTING 4-9 All three tests pass with this implementation, but it is *still wrong!***

[Click here to view code image](#)

```
public class Account
{
    public void AddTransaction(decimal amount)
    {
        Balance = amount;
    }

    public decimal Balance
    {
        get;
        private set;
    }
}
```

有了此实现，并且你的全部三个单元测试都通过——之前都失败了——太阳正在照耀，一切在世界上都是正确的。除了它不是！再次，`AddTransaction` 方法的期望与实现的现实不匹配。第四个单元测试突出了这个问题，如列表 4-10 所示。

**LISTING 4-10 This unit test should finally help crack the AddTransaction method.**

[Click here to view code image](#)

```
[TestMethod]
public void AddingTwoTransactionsCreateSummationBalance()
{
    // Arrange
    var account = new Account();
    account.AddTransaction(50m);

    // Act
    account.AddTransaction(75m);

    // Assert
    Assert.AreEqual(125m, account.Balance);
}
```

此测试最终允许你发现 `AddTransaction` 方法的绝对正确功能——至少目前是这样。重点是，随着需求变化和新功能被添加，你需要将你对类的期望编码化，以便你可以回退到现有的单元测试，这些测试形成了一个安全网。如果没有它，你很容易对代码进行更改，在你手动测试的狭窄情况下似乎有效，但在异常输入下会中断，或在其他看似无关的地方中断。

你添加的测试断言账户的余额是其所有交易的汇总。之前，你最正确的实现会将余额设置为最后一次发生的交易的值，这意味着此测试将失败，你的实现尚未正确。列表 4-11 显示了使全部四个单元测试都通过的 `AddTransaction` 方法的实现。

**LISTING 4-11 This implementation is so far the best for AddTransaction.**

Click here to view code image

```
public class Account
{
    public void AddTransaction(decimal amount)
    {
        Balance += amount;
    }

    public decimal Balance
    {
        get;
        private set;
    }
}
```

在每个单元测试从红色变为绿色后，你有机会重构 SUT 的实现，但此示例非常简单。随着向 SUT 添加的每个新方法，此过程阶段变得更加重要。以这种方式重构将在本章后面更详细地介绍。

## More complex tests

前面的示例涉及以测试优先的方式对应用程序领域模型的一部分类进行单元测试。如第 2 章“Dependencies and layering”所述，领域模型是业务逻辑层的实现，位于用户界面和数据访问层之间。

### 规范

对于下一组测试，这些测试基于此 `Account` 类构建，你将测试业务逻辑层的不同部分：一个服务。此假设应用程序的用户界面可以绑定到任何框架——ASP.NET MVC、Windows Presentation Foundation (WPF) 或 Windows Forms——并且你的服务应无论框架如何都可重用。这意味着服务不会包含特定于这些框架的任何依赖项，但它将依赖于 `Account` 类，尽管是间接的。图 4-4 显示了将构成此示例的层和类之间的依赖关系。

![](img/65c1bad7a6b3cffae8cbb79664f0708b_158_0.png)

**图 4-4 构成你现在将测试的子系统的依赖关系和实现。**

统一建模语言（UML）图显示了构成你将创建的三层架构的三个包。用户界面将包含模型-视图-控制器（MVC）控制器，尽管这些可以分别是模型-视图-视图模型（MVVM）或模型-视图-演示者（MVP）的视图模型或演示者。具体来说，`AccountController` 将具有处理用户界面操作向账户添加交易的处理器。此控制器依赖于你准备实现的 `AccountService` 的接口。

`AccountService` 位于业务逻辑层，与其接口和由之前实现的 `Account` 类表示的领域模型一起。注意，这些包代表应用程序的逻辑层，而不是直接映射到 Visual Studio 项目，因此映射到程序集。这意味着你仍然更喜欢楼梯模式而不是随从反模式。`AccountService` 需要某种方式从你使用的任何持久存储中检索 `Account` 实例。因为你在业务逻辑层中使用了领域模型，所以数据访问层是使用对象/关系映射器 (ORM) 实现的。
