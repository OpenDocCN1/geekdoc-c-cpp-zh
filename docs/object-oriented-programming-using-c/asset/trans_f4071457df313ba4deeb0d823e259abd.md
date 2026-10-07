

# 使用 C# 的面向对象编程

```csharp
}
catch (MessageManagerSystem.Clients.UnknownClientException)
{
}

[TestMethod]
public void GetClient_TestGettingClient_ShouldNotGenerateException()
{
  MessageManagerSystem.Clients.Client c = new
  MessageManagerSystem.Clients.Client("Simon",
  "Room 1234", "x2000", 10);
  MessageManagerSystem.Clients.Client c2 = null;
  try {
    cb.AddClient(1, c);
    c2 = cb.GetClient(1);
  } catch (MessageManagerSystem.Clients.UnknownClientException) {
    Assert.Fail("Unknown client exception should not be thrown if client exists");
  }
}

[TestMethod]
public void GetClient_TestGettingClient_AttributesShouldNotChange()
{
  MessageManagerSystem.Clients.Client c = new
  MessageManagerSystem.Clients.Client("Simon",
  "Room 1234", "x2000", 10);
  MessageManagerSystem.Clients.Client c2 = null;
  try {
    cb.AddClient(1, c);
    c2 = cb.GetClient(1);
    Assert.AreEqual(c2.Credit, 10,"Value of returned credit not expected");
  } catch (MessageManagerSystem.Clients.UnknownClientException) {
  }
}
```

```csharp
[TestMethod]
public void GetClient_TestDeleteUnknownClient_ShouldGenerateException()
{
  try {
    cb.deleteClient(1);
    Assert.Fail("Unknown client exception should be thrown if client does not exist");
  } catch (MessageManagerSystem.Clients.UnknownClientException) {
  }
}

```客户端测试。

# 使用 C# 的面向对象编程

下图显示了测试结果：

| 结果 | 测试名称 |
|---|---|
| 通过 | DecreaseCredit5UnitsOfCredit_ShouldBe5 |
| 通过 | AddClient_TestAddTwice_ShouldGenerateException |
| 通过 | GetClient_TestGettingClient_AttributesShouldNotChange |
| 通过 | GetClient_TestGettingClient_ShouldNotGenerateException |
| 通过 | AddClient_TestAddTwice_Alternative |
| 通过 | IncreaseCredit_TestUnitsOfCredit_ShouldBe5 |
| 通过 | GetClient_TestDeleteClient_ShouldNotGenerateException |
| 通过 | GetClient_TestGettingUnknownClient_ShouldGenerateException |
| 通过 | AddClient_TestAddingClient_ShouldNotGenerateException |

通过为所有类和方法创建测试固件，我们可以在系统适应需求时运行这些测试。

# 11.13 生成文档

文档是必要的，并且可以自动生成（见第8章 C# 开发工具）。代码中放置了 XML 注释来描述所有的类、构造函数和方法。所有的参数、返回值和抛出的异常也都描述了。

# 面向对象编程 C#

Client 类的三个注释所示：

```csharp
/// <summary>
/// 管理客户端集合（排序字典），每个客户端都有一个 ID (int)。
/// </summary>
/// <remarks>Author Simon Kendall</remarks>
/// Version 1.0 (5th May 11)</remarks>
public class ClientBook
{
    private SortedDictionary<int, Client> clients;

    /// <summary>
    /// 获取客户端。
    /// </summary>
    public SortedDictionary<int, Client> clients
    {
        // ... lines missing
    }

    /// <summary>
    /// 初始化一个新的 ClientBook 实例。
    /// </summary>
    public ClientBook()
    {
        // ... lines missing
    }

    /// <summary>
    /// 初始化一个新的 ClientBook 实例并将其实例化传入的字典。
    /// </summary>
    /// <param name="clients">Client ID 对象的字典。</param>
    public ClientBook(SortedDictionary<int, Client> clients)
    {
        // ... code omitted
    }

    /// <summary>
    /// 将客户端添加到客户端簿中。
    /// </summary>
    /// <param name="client">客户端 ID。</param>
    /// <param name="newClient">新客户端。</param>
    /// <exception cref="ClientAlreadyExists">如果已存在具有 ClientID 的客户端则抛出异常</exception>
    public void AddClient(int clientID, Client newClient)
    {
        // ... code omitted
    }
}
```

一旦在整个代码中放置了 XML 注释并将其添加到 Sandcastle帮助文件生成器以描述命名空间，该工具只需点击按钮即可生成一组描述系统的网页……！

# 使用 C# 的面向对象编程

# 案例研究

下图显示了生成的 'Index.html' 文档，描述了最通用层的消息管理器……（此处省略重复的描述内容）。

