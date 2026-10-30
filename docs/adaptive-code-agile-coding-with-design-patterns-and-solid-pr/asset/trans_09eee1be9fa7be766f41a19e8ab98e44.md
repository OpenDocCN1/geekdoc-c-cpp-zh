

## 仔细为测试方法命名

> “计算机科学中有两件困难的事情：缓存失效、命名事物，以及差一错误。”
> 
> 未知

我的一位同事非常推崇有意的糟糕变量名。如果一个类、方法或变量的用途不明确，他就会给它命名为 Fred。需要指出的是，他从不会在所有 rogue Fred 都被移除之前提交代码，但有些 Fred 可能存在一个小时直到被重命名。重点是，命名比看起来困难得多。

正如你将在本章后面 “The testing quadrant” 部分学到的那样，单元测试是为开发团队服务的，而不是为业务服务的。因此，单元测试的名称不必能被业务分析师或产品负责人阅读，这与范围更广的验收测试不同。然而，Status_code_500_should_throw_invalid_operation_exception 并不是一个好名字——在多个层面上都不是。

首先，测试泄露了太多实现知识，这对阅读者没有帮助。相反，测试名称应以测试的意图为焦点。传达测试的意图，而不是实现。

```
Account_service_failure_is_propagated_to_client
```

它不依赖于测试的实现，并且以所讨论代码的上下文为基础。

## 测试的 Builder 模式

代码编写中存在两种类型的冗长：一种使复杂化，另一种使清晰。前者显而易见，当一个方法直接处理过低层级的细节时。后者是描述性变量和方法命名的结果，利用你手头的工具来清晰地表达意图。

单元测试与任何其他代码语句一样。因此，它们至少应遵守与生产代码相同的规则。测试会因多种原因变得难以处理——最常见的是因为被测试的代码本身不够可测试。在这种情况下，测试围绕问题打转，试图想方设法创建测试。但即使是非常可测试的代码，其测试也可能缺乏清晰度和简洁性。

## Builder 模式

Builder 模式是一种创建型 Gang of Four (GoF) 设计模式。这意味着它适用于封装和抽象对象的创建。它与更常见的 Factory 模式不同之处在于，Builder 模式包含用于自定义对象创建的方法。图 5-8 显示了通用 Builder 设计模式的 UML 图。

![](img/f852e0a12c174e64d91a8e1a05146eab_202_0.png)

图 5-8 Builder 模式将产品的复杂构建与其使用解耦。

每当一个对象可以在多个维度以多种方式配置时，Builder 模式都可以简化你的创建代码并阐明意图。

## 阐明单元测试意图

让我们重温本章早些时候的一个测试，并通过应用 Builder 模式来改善其意图的清晰度。“Testing with mocks” 部分中的 Moq mock 在此处作为清单 5-28 重复，之前在清单 5-17 中出现过。

LISTING 5-28 The Moq mock (shown earlier in Listing 5-17).

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

Arrange、Act 和 Assert 部分已标记，Arrange 部分长五行。这在可接受范围内：在大约七到八行之后，减少代码行数变得很重要。相反，这个 Arrange 部分的问题在于代码的意图不明确。需要仔细阅读每一行才能理解这段代码在做什么。有效地讲，这个测试是“跳过一个抽象”：穿过一层会阐明并可能总结此代码意图的间接层。Builder 模式可以是这样的层。

## 产品

与 Factory 模式类似，Builder 模式生成一个产品。这是向构建器描述一些配置选项并要求它创建对象的结果。当应用于测试的上下文时，Builder 模式可以为测试所需的任何或所有支持对象生成产品。对于这个特定示例，Builder 模式将用于生成熟悉的系统下测试 (SUT)：AccountService。

## Builder

清单 5-29 显示了 AccountServiceBuilder 类。它采用流畅接口设计，这意味着其方法返回构建器，因此可以链接在一起。常见的做法是有一个 Build() 或 Create() 方法作为流畅链中的最后命令。结果是一个构建好的产品，即 AccountService。

LISTING 5-29 The builder encapsulates the details of constructing test objects.

```
public class AccountServiceBuilder
{
    private readonly AccountService _accountService;
    private readonly Mock<IAccountRepository> _mockAccountRepo;

    public Mock<Account> MockAccount
    {
        get;
        private set;
    }

    public AccountServiceBuilder()
    {
        _mockAccountRepo = new Mock<IAccountRepository>();
        _accountService = new AccountService(_mockAccountRepo.Object);
    }

    public AccountServiceBuilder WithAccountCalled(string accountName)
    {
        MockAccount = new Mock<Account>();
        _mockAccountRepo.Setup(r =>
            r.GetByName("Trading Account")).Returns(MockAccount.Object);

        return this;
    }

    public AccountServiceBuilder AddTransactionOfValue(decimal transactionValue)
    {
        MockAccount.Setup(a => a.AddTransaction(200m)).Verifiable();

        return this;
    }

    public AccountService Build()
    {
        return _accountService;
    }
}
```

## 测试

将 AccountServiceBuilder 插入单元测试会产生清单 5-30 中的代码。测试的 Arrange 部分仅缩短了一行代码，变为四行，但这并不是 Builder 模式的唯一目标。构建器为测试编写者提供了一种领域特定语言 (DSL) 来构建测试。

LISTING 5-30 The Arrange section of this test has a clearer intent thanks to the Builder pattern.

```
[TestClass]
public class AccountServiceTests
{
    private AccountServiceBuilder _accountServiceBuilder;

    [TestInitialize]
    public void TestInitialize()
    {
        _accountServiceBuilder = new AccountServiceBuilder();
    }

    [TestMethod]
    public void AddingTransactionToAccountDelegatesToAccountInstance()
    {
        // Arrange
        var sut = _accountServiceBuilder
            .WithAccountCalled("Trading Account")
            .AddTransactionOfValue(200m)
            .Build();

        // Act
        sut.AddTransactionToAccount("Trading Account", 200m);

        // Assert
        _accountServiceBuilder.MockAccount.Verify();
    }
}
```

代码可以顺序阅读，意图清晰。去掉代码中的多余噪音后，这段文字如下：

Account service builder, with account called "Trading Account", add transaction of value 200.0.

这就是测试设置应有的阅读方式。关于系统下测试的预期，清晰度大大提高。再回顾一下原始 Arrange 部分，看看它与之相比如何。模拟设置的细节——实现细节——掩盖了代码的意图。看看参数化值的位置：200m 和 "Trading Account"。它们在模拟初始化的噪音中丢失了。通过使用 Builder 模式，测试现在具有更清晰的意图。

Tip 另一个 Builder 模式的优点是它导致更声明式的测试。没有任何测试的圈复杂度应大于 1，这意味着测试应完全线性，没有分支。if 语句或 for、foreach 或 while 循环会导致测试的圈复杂度超过 1。Builder 模式通过将命令式构造和初始化转换为声明式来帮助实现这一点。

## 先写测试

到目前为止，本章介绍的是使用测试驱动开发 (TDD) 方法进行单元测试的优点。但严格来说，这算是测试驱动开发吗？软件开发充满了含义主观或随时间推移而变化的术语。考虑一下“service”这个词，例如。在不同情况下它意味着许多不同的东西。这本书本身在许多不同的上下文中使用该术语。而上下文是关键。没有上下文，就没有讨论的基础，没有辩论可以存在的环境。

TDD 可能不一定是主观术语，但其含义已经发生了变化。被奉为“软件工程”的现代标准和实践已经渗透到行业中，其含义被扭曲或误解。

## 什么是 TDD？

测试驱动开发有纯粹主义和实用主义的解释。即使这些术语也是有偏见的：纯粹主义者从不从他或她的狭隘、理想主义的愿景中退让，即事物应该如何；实用主义者是独行侠，以交付为名走捷径并稀释代码。当然，这两种描述都是夸张的 caricatures。

TDD 的“纯粹主义”理念是它是一种设计工具——开发者应带着对可能实现的生产代码毫无先见之明地接近键盘。相反，他们是典型的空白 slate，准备在进展中发现他们的设计。这种进展是通过编写失败的单元测试来指导的。

TDD 的“实用主义”理念是开发者先写单元测试。区别很微妙。在纯粹主义 TDD 中，过程有更多约束。两种 TDD 风格的目标相同：生成已通过单元测试验证为满足需求的生产代码。然而，实用主义 TDD 在实现这一目标方面有更少的规则。实用主义 TDD 的唯一规则是：先写测试。

