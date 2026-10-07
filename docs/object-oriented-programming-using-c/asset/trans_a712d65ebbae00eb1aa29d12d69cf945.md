

# 面向对象编程 C# 敏捷编程

有一种命名规范，可以使测试用例与被测试代码之间的关系变得清晰：

- 1) 用于存储测试的项目根据被测试的系统命名（例如，一个存储银行系统测试的项目可以命名为 `BankSystemTests`）。
- 2) 测试固件（Test Fixture）使用被测试类的名称进行命名（例如，假设银行系统中有一个名为 'Client' 的类，则测试固件命名为 `TestFixture_ClientTests`）。
- 3) 测试的命名使用：被测试的方法名+所应用的测试+预期结果（例如，一个名为 `AddMoney` 的方法可能有一个测试为...`AddMoney_Add5Pounds_BalanceEquals10`）。

在 Visual Studio 中，遵循菜单 `测试` -> `新建测试项目` -> `基本`将设置一个能够处理 C# 代码的测试套件。首先，将要求输入测试固件的名称，如果之前没有设置测试项目，则会要求输入名称。每个测试在被添加到测试固件时都需要单独命名。

创建了测试固件后，我们需要设置测试并编写测试本身。作为其中的一部分，我们需要指定被测试代码正确行为。我们使用 `Assert(...)` 方法来实现，这些方法必须为真，测试才能通过。

我们还利用属性（Attributes）为 Visual Studio 提供必要的信息，以便其运行测试……

- `[TestClass]` 属性表示该测试类将确实作为测试固件。因此，此属性必须放在每个测试固件的开头。

```csharp
[TestClass]
public class TestFixture_ClientTests
{
```

- `[TestInitialize]` 属性声明了一个在每个测试用例执行之前运行的方法。
- 测试用例是方法，必须跟在 `[TestMethod]` 属性。
- `[TestCleanup]` 属性声明了一个在每个测试用例执行后运行的方法。
- `[ExpectedException(typeof(...))]` 属性允许我们指定预期代码会生成异常。

我们很快就会看到这些内容的示例。

# 使用 C# 敏捷编程面向对象编程

## 10.9 断言示例

在设置测试用例时，我们进行进行断言。断言是一个语句，如果代码运行正常，则该陈言应为真。断言的示例包括……

- Assert.AreEqual(...)
- Assert.AreNotEqual(...)
- Assert.Fail(...)
- Assert.IsTrue(...)
- Assert.IsFalse(...)

正如我们在这里看到的，`Assert.AreEqual()` 和 `Assert.Fail()` 对于许多测试目的来说足够了。

`Assert.Fail()` 表示到达这一行意味着测试失败了！虽然我们说测试失败了，但从严格来说这不是真的。失败的不是测试，而是我们的代码失败了。测试成功地发现了我们代码中的错误。

![](img/e143b38d00f95425fa4f3efca0527189_191_0.png)

在爱立信（Ericsson），我们深信，我们每天所做的创新可以为人类、业务和社会创造一个更好的世界产生深远影响。加入我们吧。

在德国，我们特别寻找作为集成工程师的毕业生，负责：
- 无线接入和 IP 网络
- IMS 和 IPT

我们期待收到您的申请！欲申请并查看所有当前的招聘职位，请访问我们的网页：www.ericsson.com/careers

## 10.10 若干测试示例

为了说明测试框架，我们将创建几个测试用例来测试如下所示的 `BankManagement` 系统的功能：

![](img/e143b38d00f95425fa4f3efca0527189_192_0.png)

在该系统中，`BankManager` 类维护了一本客户簿（BofC）。可以通过 `AddClient()` 方法添加客户对象，该方法需要该客户的 ID 和要添加的客户对象。可以通过 `GetClient()` 方法检索客户，该方法需要 `ClientID` 作为参数，并返回客户对象（如果存在）或生成异常（如果不存在指定 ID 的客户）。

`Client` 类有一个构造函数，需要客户名称和客户余额。

为了简单起见，我们假设银行的每个客户只有一个账户（这显然不是一个现实的系统），而且我们不需要账号，因为每个客户都有一个唯一的 ID。

我们将专门测试以下能力……

- 向 `BookOfClients` 中添加一个客户 
- 尝试查找一个不存在的客户
- 通过调用 `AddMoney()` 方法增加客户的余额。

当然，这只是为了彻底演示系统中所有类和所有方法运行所需的测试用例的一小部分。

## 测试客户

为了测试是否可以添加客户，我们需要：

- 1) 通过创建一个新的空 `BookOfClients` 来设置测试
- 2) 创建一个客户并将其添加到 `BookOfClients`
- 3) 通过尝试检索刚刚添加的客户来检查客户是否已成功添加（本课程应该可以运行），并且最后
- 4) 我们需要测试检索到的客户是否与我们添加的客户具有相同的属性——确保确保在过程中没有被损坏。

首先，我们通过创建一个新的空 `BookOfClients` 对象 (BofC) 来初始化测试，并在结束时将其设置为 `null` 以清理测试。代码如下所示：

```csharp
[TestInitialize]
public void TestInitialize() {
    BofC = new BookOfClients();
}

[TestCleanup]
public void TestCleanup() {
    BofC = null;
}
```

接下来，我们通过向空的 `BofC` 添加客户来创建我们的第一个测试。如果系统生成了异常，我们就知道代码有问题。查看该测试代码：

```csharp
[TestMethod]
public void AddClient_TestNewClient_ExceptionNotGenerated() {
    Client c = new Client("Simon", "Room 1234", 200, 10);
    try {
        Bof.AddClient(c);
    } catch (Exception) {
        Assert.Fail("新客户不应抛出异常");
    }
}
```

如果上面的测试通过，我们知道代码没有生成异常，但并没有证明客户已添加。我们需要创建其他测试来显示我们可以检索刚刚添加的客户，并需要一个测试来显示在添加客户时属性没有被损坏。在我们确认该方法实际上可以工作之前，需要多个测试！

注意上面的测试名称通过对执行测试的描述和预期输出描述指示了被测试的方法。这种长测试名称是非常重要的。通过阅读长测试名称列表，我们可以确定系统的哪些部分已经测试，哪些部分被遗漏了。

除了描述的测试之外，还应该尝试两次添加相同 ID 的客户。我们的系统当然不允许这种情况发生。如果代码阻止了两次添加，则测试成功。

相反，如果在第二次添加相同客户时系统没有生成异常，则测试应该指示代码失败。该测试给如下所示：

```csharp
[TestMethod]
public void AddClient_TestExistingClient() {
    Client c = new Client("Simon", "Room 1234", 200, 10);
    try {
        Bof.AddClient(c);
        Bof.AddClient(c);
        Assert.Fail("如果添加两次，应抛出 ClientExists 异常");
    } catch (ClientExistsException) {
    }
}
```

编写上述测试的另一种方法是指定预期由 `[ExpectedException(...)]` 属性生成的异常。如果生成此异常中断了测试，则测试通过了。查看下方测试代码的另一种版本……

```csharp
[TestMethod]
[ExpectedException(typeof(ClientExistsException))]
public void AddClient_TestExistingClient() {
    Client c = new Client("Simon", "Room 1234", 200, 10);
    Bof.AddClient(c);
    Bof.AddClient(c);
}
```

