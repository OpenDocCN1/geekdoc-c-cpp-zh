

# 列表 5-13 一个仅用于测试目的的非常简单的存储库实现。

```
public class FakeAccountRepository : IAccountRepository
{
    public FakeAccountRepository(Account account)
    {
        this.account = account;
    }

    public Account GetByName(string accountName)
    {
        return account;
    }

    private Account account;
}
```

现在可以创建账户服务的实现了。列表 5-14 展示了 AccountService 类的新实现。

## 列表 5-14 AccountService 类的当前状态。

```
public class AccountService : IAccountService
{
    public AccountService(IAccountRepository repository)
    {
        this.repository = repository;
    }

    public void AddTransactionToAccount(string uniqueAccountName, decimal transactionAmount)
    {
    }

    private readonly IAccountRepository repository;
}
```

现在可以完成单元测试了，同时需要新增以下 Arrange 条件：

- 确保有一个可用于断言的 Account 实例。
- 确保有一个可用的 Fake IAccountRepository 实例，以便在构造服务时传入。

### 列表 5-15 此测试因正确的原因而失败：AccountService 尚未实现。

```
[TestClass]
public class AccountServiceTests
{
    [TestMethod]
    public void AddingTransactionToAccountDelegatesToAccountInstance()
    {
        // Arrange
        var account = new Account();
        var fakeRepository = new FakeAccountRepository(account);
        var sut = new AccountService(fakeRepository);

        // Act
        sut.AddTransactionToAccount("Trading Account", 200m);

        // Assert
        Assert.AreEqual(200m, account.Balance);
    }
}
```

如本列表所示，首先创建一个初始余额为零的账户。然后创建一个 FakeAccountRepository 实例，并将该账户传入其中。由于这个 fake 实现了账户存储库的接口，因此可以将其传递给 AccountService 类，也就是被测系统（SUT）。

调用测试目标方法后，断言账户的余额应为 200m。如图 5-5 所示，此断言会失败，因为目标方法尚未实现。

![](img/f852e0a12c174e64d91a8e1a05146eab_188_0.png)

## 图 5-5 继续从红色转为绿色的过程，此时你已经拥有了一个失败的测试。

现在，你已经有了一个用于规定生产代码中缺失行为的单元测试，接下来可以执行最简单的操作，让单元测试通过，如列表 5-16 所示。

### 列表 5-16 此 AccountService 实现使测试通过。

```
public class AccountService : IAccountService
{
    public AccountService(IAccountRepository repository)
    {
        this.repository = repository;
    }

    public void AddTransactionToAccount(string uniqueAccountName, decimal transactionAmount)
    {
        var account = repository.GetByName(uniqueAccountName);
        account.AddTransaction(transactionAmount);
    }

    private readonly IAccountRepository repository;
}
```

单元测试引导你在此实现中采取正确的做法。你必须使用存储库检索账户，并调用该账户的 AddTransaction 方法来修改只读的 Balance 属性。如果有人随后破坏了此方法，使其不再符合单元测试中设定的预期，你会很快发现问题。

## 模拟框架

不难想象，创建 mock 很快就会变得十分繁琐。设想一下你可能编写的所有单元测试组合，以及 SUT 可能需要的各种不同接口。仅仅为了支持单元测试，就需要编写大量额外代码。

还有另一种模拟 IAccountRepository 的方式，但需要使用外部模拟框架。编写 fake 的一个优点是，你可以独立编写它们，而不需要任何第三方依赖。不过，如今模拟框架已经非常普遍，而且可供选择的框架很多。下面的示例使用其中最流行的框架之一：Moq。这个名称有时读作 *Moh-kyoo*，有时读作 *Mok*。

通过 NuGet，你可以在在线源中搜索 Moq 包，从而快速添加对 Moq 的引用。Moq 背后的魔法在于，它可以为你要求模拟的任意接口创建动态代理。你将编辑现有测试，使用 Moq mock 替代手动创建的 fake，如列表 5-17 所示。

### 列表 5-17 Moq 等模拟框架可以让你非常轻松地创建 mock。

```
[TestMethod]
public void AddingTransactionToAccountDelegatesToAccountInstance()
{
    // Arrange
    var account = new Account();
    var mockRepository = new Mock<IAccountRepository>();
    mockRepository.Setup(r => r.GetByName("Trading Account")).Returns(account);
    var sut = new AccountService(mockRepository.Object);

    // Act
    sut.AddTransactionToAccount("Trading Account", 200m);

    // Assert
    Assert.AreEqual(200m, account.Balance);
}
```

测试中的更改以粗体突出显示。你不再实例化自己的 fake 存储库，而是创建一个新的 Mock<IAccountRepository> 对象。这个对象功能非常强大，可以让你为模拟的接口设置各种预期和行为。这个类并不实现你的接口，因此不同于 fake，它并不是 IAccountRepository 的直接可用实例。这是因为公共语言运行时（CLR）不允许类从泛型参数继承。相反，mock 与它创建的代理实例之间存在组合关系。Object 属性允许你访问底层的模拟接口，在本例中，该接口会被传入 AccountService。

在将 mock 提供给 SUT 之前，需要指定它应有的行为。默认情况下，Moq 定义的是宽松 mock，这意味着它们的所有返回值都是默认值。任何引用类型的默认值都是 null，这同样适用于 Account 类。宽松 mock 的另一种选择是 *严格* mock；当遇到你尚未指定的方法调用或属性访问时，严格 mock 会抛出异常。这两种选项都不是你需要的，因此必须手动设置一些预期行为。

Mock 实例的 Setup 方法非常巧妙。它接受一个 lambda 表达式，该表达式会将底层模拟类型的实例作为上下文参数提供。通过调用该类型上的方法，你可以指定：当使用完全相同的参数调用该方法时，应当发生某种行为。具体要指定什么取决于你的测试场景。Moq 允许你为方法调用设置以下预期：

- 调用其他 lambda 表达式。
- 返回指定值。
- 抛出指定类型的异常。
- 验证是否调用了此方法。

## Mock 与测试过度指定

使用 mock 进行测试是一种常见但可能十分繁重的做法。依赖 mock 的测试很容易变得过度指定。过度指定的测试十分脆弱，但你可以通过改变断言内容来避免这种脆弱性。当测试包含对被测系统（SUT）工作方式的深入了解时，就会产生这个问题。换句话说，当测试了解的是 SUT 的实现，而不是其预期行为时，这个测试就属于过度指定。

使用 mock 的单元测试可能需要了解 SUT 是如何实现的。不过，你始终应该记住，单元测试是对预期行为的规定，因此应避免针对实现细节编写测试。这可能包括调用 SUT 所依赖的其他接口。如果你断言某个接口上的方法必须被调用，那么测试就不再与某种行为绑定，而是与某种具体实现绑定。

过度指定的测试不理想，因为它们会阻碍对所测试生产代码进行重构。一个方法或类配套的、全部通过的单元测试套件，表明该方法或类的实现可以放心修改：只有当代码的预期行为被破坏时，测试才会失败。过度指定的测试无法提供这样的保证，因为即使预期行为仍然完整，只要方法或类的实现发生变化，它们也会失败。

在使用 mock 进行测试时，有两种方法可以避免测试过度指定。第一种方法是只测试行为。基于状态的测试就是测试预期行为的最佳示例。如果一个方法接受数据作为输入，并返回经过修改的数据作为输出，那么在测试时可以将该方法视为黑盒。如果该方法接受输入 A、B 和 C，并返回输出 X、Y 和 Z，那么它如何得出这些结果与测试无关。这样就可以重构该方法，而不会破坏单元测试。

第二种方法不太理想，但有时是唯一的选择。你可以将单元测试及其测试的实现视为一个原子单元：如果其中一个发生变化，另一个也必须随之变化。这相当于承认单元测试存在过度指定，并计划在重构时连同生产实现一起丢弃该单元测试。这并没有想象中那么浪费。正如你将在第三部分“SOLID 代码”中看到的，SOLID 代码会产生更小、更有针对性的类，而这些类本来就不会被修改。

对于这个测试，你希望采用第二种方式：返回指定值。Mock.Setup 方法调用的流式接口允许你将调用链接到 Returns 方法。这提高了可读性，并减少了测试中已经开始变得相当庞大的 Arrange 阶段。Returns 方法接收你之前已经创建的 Account 实例，这样就完成了对该 mock 预期行为的设置。简而言之，你向 mock 发出了以下指令：

> 当针对这个 IAccountRepository 实例调用 GetByName 方法，并且提供的账户名称为“Trading Account”时，返回这个 Account 类的实例。

