

使用 C# 的面向对象编程与敏捷编程

## 测试 GetClient 方法

我们当然会测试系统中的所有方法，包括 `GetClient()` 方法。

我们需要执行的一个用例是测试：当我们尝试检索一个不存在的客户端时，是否会抛出异常。为了测试这一点，我们创建一个新的空 `BookOfClients` 并尝试从中检索一个客户端——任何客户端！

在这种情况下，我们希望系统生成一个未知客户端异常（unknown client exception）。由于我们通过创建一个空账本来初始化测试，除非我们先添加它们，否则我们无法检索任何客户端。

### 活动 1
查看下面的代码，并判断在代码的哪一点我们可以断言测试显示我们的系统已失败（点 A、B、C 或 D）。

```csharp
[TestMethod]
public void GetClient_TestGettingUnknownClient_ShouldGenerateException()
{
    // point A
    try {
        // point B
        BofC.GetClient(1);
        // point C
    }
    catch (BankManager.UnknownClientException)
{
        // point D
    }
}
```

### 反馈 1
在调用 ... 之前，我们无法确定 `GetClient()` 方法是否失败，因此我们不能在此放置 `Assert.Fail`。在点 A 或 B 处失败。

当我们调用此方法时，由于我们的客户端账本是空的，应该生成异常。`try` 块应该在此处终止并启动 `catch` 块；如果代码到达点 D，则表示测试成功而非失败。然而，如果代码到达点 C，则表示预期的异常没有生成，因此我们可以在此点断言 `GetClient()` 方法已失败。

此测试的完整代码如下....

## 使用 C# 的面向对象编程
## 敏捷编程

```csharp
[TestMethod]
public void GetClient_TestGettingUnknownClient_ShouldGenerateException () {
    try {
        BofC.GetClient(1);
        Assert.Fail("UnknownClient exception should be thrown if client does not exist");
    }
    catch (BankManager.UnknownClientException) {
    }
}
```

在测试我们的 `BookOfClients` 类之外，我们当然还会测试系统中的其他类。

![](img/e143b38d00f95425fa4f3efca0527189_196_0.png)

## 测试 Client 类

```csharp
[TestClass]
public class TestFixtureTests
{
    private MessageManagerSystem.Clients.Client c;

    [TestInitialize]
    public void TestInitialize()
    {
        c = new BankManager.Client("Simon", 10);
    }

    [TestCleanup]
    public void Cleanup()
    {
        c = null;
    }
}
```

在初始化时，我们创建了一个初始余额为 10 的新客户端。

严格来说，我们在编写 `BookOfClient` 测试之前先编写了 `Client` 测试，因为我们需要客户端对象来测试 `BookOfClients`。在 Visual Studio 中，可以确保这些测试先运行。

下面是一个测试 `AddMoney()` 方法的简单测试...

```csharp
[TestMethod]
public void AddMoney_TestAdd10ToBalance_FinalBalShouldBe20()
{
    c.AddMoney(10);
    Assert.AreEqual(20, c.Money, "Balance after adding 10 is not as expected. Expected: 20: "+c.Money);
}
```

上述使用了 `Assert.AreEqual()` 方法。如果前两个参数相等，则我们的代码通过了测试。如果它们不等，则我们的代码失败了，第三个参数是待显示的错误消息。为了尽可能提供帮助，错误消息指定了我们预期的余额以及调用 `AddMoney()` 方法后的实际余额。

在我们编写的所有测试中，如果测试方法结束时没有失败任何断言（assertions），则该测试通过了。

## 使用 C# 的面向对象编程
## 测试 ToString() 方法

间接测试客户端**所有**属性是否已正确存储的一种方法是测试 `ToString()` 方法是否返回预期的值。这有点棘，因为字符串的格式必须完全匹配，包括每个空格、标点符号和换行符。

另一种方法是测试每个属性的值。

### 活动 2
假设类的 `ToString()` 方法定义如下，创建一个测试方法来测试 `ToString()` 方法返回的值符合预期。

```csharp
public String ToString() {
    return ("Client name:" + Name + "\nBalance:" + Balance);
}
```
提示：我们已经通过创建一个名为 "Simon" 余额为 10 的客户端初始化了客户端测试。

该练习的一个解决方案如所示。

```csharp
[TestMethod]
public void ToString_TestClientValues() {
    Assert.AreEqual("Client name: Simon\nBalance: 10", c.ToString(),
"String returned is not as expected. Expected: Client name: Simon\nBalance: 10 Actual: " + c.ToString());
}
```

在这里我们假设从 `c.ToString()` 返回的字符串等于我们预期的字符串。这非常棘手，因为字符串的格式必须完全匹配，包括每个空格、标点符号和换行符。

此测试当然是在间接测试**所有**属性是否已正确存储，如果我们用来检查是否正确从客户端账本中检索了客户端，这将特别有用。

## 10.11 运行测试

设计好一组测试后，可以根据需要随时运行。在 Visual Studio 中，我们通过菜单运行。

## 使用 C# 的面向对象编程
## 10.12 测试驱动开发 (TDD)

虽然对于回归测试非常有用，但测试驱动开发 (TDD) 是一种主要与“敏捷”开发过程相关的技术。测试驱动开发的方法是：

- 1) 编写测试（在编写方法之前）。
- 2) 设置自动化测试，它会因为类还没有写而失败！
- 3) 编写类使测试通过

![](img/e143b38d00f95425fa4f3efca0527189_199_0.png)

丹麦理工大学 (DTU) 被评为欧洲最顶尖大学之一，并在顶尖国际研究人员的专家指导下提供国际认可的硕士学位。

## 10.13 TDD 周期

在进行测试驱动开发时，测试最初会导致编译错误，因为被测试的方法不存在！

创建一个存根方法（stub method）可以使测试通过，但测试将“失败”，因为被测试的实际功能尚未实现。

我们实现方法的正确的功能使测试成功。

对于复杂的方法，我们可能有多个周期：编写测试、失败、实现功能、通过、扩展测试、扩展功能、通过……以此构建解决方案。

## 10.14 TDD 的主张

对于 TDD 的一些主张包括：

- 测试成为开发中固有的一部分，而不是事后匆忙完成的步骤。
- 它鼓励程序员编写直接满足需求的简单代码。
- 一套完整的单元测试集与代码开发并行编译。
- 快速的“编写测试、编写代码、运行测试”循环（每个微小的开发增量）增加了程序员的信心和生产力。

在传统的软件生命周期中，如果软件项目进度落后，财务压力会导致软件在未经过充分测试和调试的情况下就被推向市场。在测试驱动开发中，这种情况是不可能的，因为测试是在系统实现之前编写的。

