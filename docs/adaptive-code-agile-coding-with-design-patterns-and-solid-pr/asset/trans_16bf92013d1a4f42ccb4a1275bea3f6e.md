

## 列表 5-24  手动断言抛出的异常。

```csharp
[TestMethod]
public void AccountExceptionsAreWrappedInThrowServiceException()
{
    // Arrange
    var account = new Mock<Account>();
    account.Setup(a => a.AddTransaction(100m)).Throws<DomainException>();
    var mockRepository = new Mock<IAccountRepository>();
    mockRepository.Setup(r => r.GetByName("Trading Account")).Returns(account.Object);
    var sut = new AccountService(mockRepository.Object);

    // Act
    try
    {
        sut.AddTransactionToAccount("Trading Account", 100m);
    }
    catch (ServiceException serviceException)
    {
        // Assert
        Assert.IsInstanceOfType(serviceException.InnerException, typeof(DomainException));
    }
}
```

对于这个测试来说，仅使用 ExpectedException 特性是不够的。你需要检查所抛出异常的 InnerException 属性，并断言它是一个 DomainException。这证明了领域异常被包装起来，同时保留了最初发生的错误。所有软件缺陷都可以被视为缺少单元测试的结果：也就是对预期行为的不完整说明。列表 5-25 展示了如何通过编辑生产代码来使测试通过。

## 列表 5-25  原始异常现在已由新异常正确包装。

```csharp
public void AddTransactionToAccount(string uniqueAccountName, decimal transactionAmount)
{
    var account = repository.GetByName(uniqueAccountName);
    if (account != null)
    {
        try
        {
            account.AddTransaction(transactionAmount);
        }
        catch (DomainException domainException)
        {
            throw new ServiceException("Adding transaction to account failed", domainException);
        }
    }
}
```

使这个测试通过后，你就可以返回去重现缺陷报告中最初的异常，并且这一次确定问题的根本原因。

## 测试设置

让我们回顾一下目前为止编写的测试。每个测试都逐渐变得更加复杂，需要更多代码来设置预期行为。如果能把这些代码提取到某个地方，就可以清理测试代码，并让它们变得更短一些，那就好了。MSTest 和其他单元测试框架一样，允许使用特殊的初始化和清理方法，这些方法分别在每个测试开始和结束时调用。初始化方法可以使用任意名称，但必须使用 TestInitialize 特性进行标记。

需要放入此方法中的代码，是几乎所有单元测试都共有的代码：实例化模拟对象。你可以将模拟对象存储为类中的私有字段，这样每个测试都仍然可以访问它们。对于 SUT 也可以采用同样的做法，因为它只需要将模拟仓储作为构造函数参数，并且它的构造不依赖于任何特定的单元测试。列表 5-26 展示了对测试类所做的必要修改，以支持设置方法。

## 列表 5-26  模拟对象和 SUT 可以在设置方法中构造。

```csharp
[TestClass]
public class AccountServiceTests
{
    [TestInitialize]
    public void Setup()
    {
        mockAccount = new Mock<Account>();
        mockRepository = new Mock<IAccountRepository>();
        sut = new AccountService(mockRepository.Object);
    }

    private Mock<Account> mockAccount;
    private Mock<IAccountRepository> mockRepository;
    private AccountService sut;
}
```

这些对象作为测试初始化方法的一部分构造后，该方法会针对每个测试方法分别调用。这样，你就可以通过移除这些对象的构造代码，简化部分单元测试代码。列表 5-27 展示了对最近那个单元测试 AccountExceptionsAreWrappedInThrowServiceException 所做的修改。

## 列表 5-27  这个测试稍微短了一些，也更容易阅读。

```csharp
[TestMethod]
public void AccountExceptionsAreWrappedInThrowServiceException()
{
    // Arrange
    mockAccount.Setup(a => a.AddTransaction(100m)).Throws<DomainException>();
    mockRepository.Setup(r => r.GetByName("Trading Account")).Returns(mockAccount.Object);

    // Act
    try
    {
        sut.AddTransactionToAccount("Trading Account", 100m);
    }
    catch (ServiceException serviceException)
    {
        // Assert
        Assert.IsInstanceOfType(serviceException.InnerException, typeof(DomainException));
    }
}
```

删除三行代码也许算不上代码量的大幅减少，但对所有单元测试产生的累积效果是：代码更具可读性。按照约定，你知道任何带有 mock 前缀的变量都是模拟对象，而变量 sut 则是你正在测试的系统。

## 单元测试模式

测试和生产代码一样，也可能变得难以处理且难以阅读。而且和生产代码一样，测试被阅读的次数远多于编写的次数——阅读者也形形色色。有人曾说过，你编写代码时应该假设下一个阅读代码的人是一个知道你住在哪里的精神病患者。当然，这种说法有些夸张，也很简洁，但其中确实包含着一丝真理。请体谅那些未来必须阅读你代码的可怜人：帮助他们完成工作，不要给他们制造障碍。

## 编写可维护的测试

既然测试的可读性至少和生产代码的可读性同等重要，那么该如何诊断现有测试中的可读性问题？又有哪些选项可以用来改善测试的可读性？

首先，可以对测试进行一些战术性的修改，以改善测试逐行阅读时的可读性。其次，也可以进行战略性的——或结构性的——修改，从更大范围影响可读性。

## 优先保持一致性

在互联网上争论完全是在浪费时间和精力。这种行为既徒劳又不合逻辑。然而，软件开发者往往依赖敏锐的逻辑感，却经常在互联网上争论。从追求完美算法类型的吹毛求疵，到“最佳语言”之争，开发者总是忍不住一头扎进毫无意义的争论中。

事实是，在实践层面，你有无穷多的选择可供决定。你不可能始终对所有选择进行批判性评估；因此，需要一种更好的启发式方法。任何代码库都应坚持的首要原则是*一致性*。这适用于许多方面。

不要为了类字段名称前置下划线的相对优点，或普遍使用 this 的好处而彼此争论。相反，应保持一致，并遵循代码已经确立的示例。争论所浪费的任何时间，都不如用来取得真正、实际且有形的进展。

这适用于整个代码库。然而，测试代码往往会引发最激烈的争论。

对于一个内部已经保持一致的棕地项目来说，这些都没有问题；但对于绿地项目，或其模式尚不明确的项目，该怎么办呢？对于绿地项目，应做出一个最容易被接受的决定，然后坚持执行。当项目代码已经呈现出多种命名约定或适用模式的混合状态时，应选择最常见的示例，并逐步将其余代码规范到与之匹配。

## 为每个类保持合理的测试夹具比例

在大多数情况下，测试夹具与生产类保持 1:1 的比例就足够了。使用单个测试夹具来测试多个被测系统会造成混淆，并违反最小惊讶原则。这与将多个类放在同一个文件中非常相似：应当避免这样做，以免其他人在浏览代码时遇到困难。

> **提示**  *最小惊讶原则*是一条指导原则，建议在面临选择时，选择最简单、最明显的选项。它旨在让后来者的生活更轻松——甚至可能让未来某个因奇怪决定而感到惊讶的自己也更轻松！

## 为被测系统命名

虽然编写代码时通常应避免使用缩写，但用于表示被测系统的变量名至少可以从保持一致性中受益。即使选择了其他名称，例如 target，在所有测试中使用一致的名称，也能让后续阅读代码的人快速定位并理解代码。

