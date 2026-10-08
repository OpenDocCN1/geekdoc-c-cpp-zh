

# 构建面向服务的应用程序 727

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_752_0.png)

**图 1-4：** 分层结构。

由于服务使用了通用格式——通常是基于 HTTP 的 XML——你可以相对容易地将应用程序的部分安装在各自的机器上，以按功能对其进行隔离。由于被删除部分的功能通过服务调用，因此你可以对应用程序进行水平扩展。

- **可重用性：** 每个组织都有一份其参与者列表——例如，客户端、用户、投票者、厨师或邮件列表订阅者。无论参与者的类型如何，列表中的所有人都有姓和名，以及识别特征。

它似乎今天编写的几乎每个应用程序都有一个“人员”（People）表。精明的程序员会使用巧妙的技巧来保持这些表同步，或共享信息，例如，但共享“人员”表只有一种方法——使用数据孤岛，如图 1-5 所示。

数据孤岛的工作原理如下：

- 1. 某些服务器上的数据库包含所有参与者的人口统计信息。
- 2. 数据孤岛被包含所有允许操作的服务层包围。
- 3. 服务层被系统中的所有其他应用程序消费，如图 1-5 所示。

这一系列步骤向你展示了重用的概念。它与代码片段无关（无论你听到什么）——它关乎*数据*。服务有助于提供对数据孤岛的访问。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_753_0.png)

1-5：数据孤岛。

# 提供 XML Web 服务

服务的常见用途是使用一个可以在任何地方消费的开放 API，让其他程序员能够公开访问你的信息。你可能还记得早些章节“合约驱动”中描述的 WSDL 文件——它可以让你的酷炫函数或宝贵数据对任何需要它的人可用。

在早些章节“构建面向服务的应用程序”中描述的人口孤岛示例中，如果你有一份宝贵的邮件列表并想让客户访问它，你可以将列表发送给他们。但是，如果你这样做，他们就可以永远使用它。相反，假设你可以在客户每次使用列表时对其收费。如果你为列表上实现的函数提供 Web 服务，你就可以跟踪列表的实际使用情况。

你可以在随处看到这种被称为跨边界提供（provision past the boundary）的概念。以 Twitter 为例。Twitter 并不是让用户去 Web 页面搜索数十亿条消息，而是提供了一个 WSDL 合约，让开发者能够在自己的应用程序中进行搜索。

Web 服务可以像任何其他 Web 一样被控制。以前在 RDBMS 级别处理的字段级或操作级安全性，现在可以构建在半公共 API 中。

# 构建三个示例应用

你可以通过几种方式在 C# 中构建服务，正如接下来三个章节所述。然而，本节的标题并不准确：我展示了如何通过三种不同的方式构建同一个应用程序。该应用程序 SHARP 会议系统（或其简单版本）是使用这些格式构建的：

- **ASMX：** 第一版本采用古老的 ASMX 格式：ASP.NET Web 服务。虽然这种格式在很大程度上被 WCF 取代，但它仍然可用。我在本章和下一章中介绍了它，因为它是某些情况的可行方案。
- **WCF：** Windows Communications Foundation (WCF) 是最重要的服务平台，它留了足够的篇幅让你入门。这个主题很宽泛，你可以找到许多指向其他资源的引用。
- **REST：** 表象层状态转换 (REST) 是地球上最老的服务，得益于 AJAX，它获得了新的生命。REST 并不是 .NET 世界中的一等公民，但它很重要。

整个过程使用单一数据模型，如图 1-6 所示，并对其提供了允许的操作。

| 会议 | 会话 | 列名 | 数据类型 | 允许 |
| :--- | :--- | :--- | :--- | :--- |
| Id | | int | [x] |
| Description | | varchar(1024) | [x] |
| LocationId | | text | [x] |
| | | Number | int | [x] |
| | | Speaker | int | [x] |
| | | StartTime | date | [x] |
| | | EndTime | datetime | [x] |
| | | ConferenceId | int | [x] |
| Locations | | | | |
| Id | | | | |
| PlaceName | | | | |

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_754_0.png)

| 参加 | 人 | | | |
| :--- | :--- | :--- | :--- | :--- |
| Id | | | | |
| PlaceName | | FirstName | | |
| SessionId | | LastName | | |
| | | EmailAddress | | |

这种思想是提供一个与本章描述的平台类似的状态驱动应用程序模型。最后，我向你展示如何解决三个不同的问题。否则会怎样？

# 第 2 章：构建 ASMX 服务

在本章中

- 熟悉 ASMX
- 创建 ASMX
- 构建 ASMX

在本章中，我们将熟悉 ASMX。学习如何创建和构建 ASMX 服务。

在下一章中，我们将查看 WCF。学习如何创建和构建 WCF 服务。

在最后一章中，我们将查看 REST。学习如何创建和构建 REST 服务。

# 构建 ASMX 服务

ASMX 是在 ASP.NET 中构建 Web 服务最简单的方法。它很容易学习，但不是最强大的。在本章中，我们将学习构建简单的 ASMX 服务。

要创建 ASMX 服务，你需要创建一个类并在方法上添加 `[WebMethod]` 属性。

```csharp
[WebServiceService]
public class HelloWorldService : WebService
{
    [WebMethod]
    public string HelloWorld(string name)
    {
        return "Hello " + name;
    }
}
```

这是一个简单的 ASMX 服务。它有一个方法 HelloWorld，接受字符串作为输入并返回字符串。在下一个示例中，我们将构建一个复杂的 ASMX 服务。该服务将有多个方法，并且将使用数据类型。

```csharp
[WebServiceService]
public class CalculatorService : WebService
{
    [WebMethod]
    public int Add(int a, int b)
    {
        return a + b;
    }

    [WebMethod]
    public int Subtract(int a, int b)
    {
        return a - b;
    }

    [WebMethod]
    public int Multiply(int a, int b)
    {
        return a * b;
    }

    [WebMethod]
    public int Divide(int a, int b)
    {
        if (b == 0)
        {
            throw new ArgumentException("Cannot divide by zero.");
        }
        return a / b;
    }
}
```

这是一个复杂的 ASMX 服务。它有四个方法，并且使用整数数据类型。要使用 ASMX 服务，你可以使用 Visual Studio 中的 Web Service Reference 工具。

```csharp
CalculatorService service = new CalculatorService();
int result = service.Add(5, 10);
Console.WriteLine(result);
```

这就是你在客户端代码中使用 ASMX 服务的方式。

在下一个示例中，我们将构建一个使用自定义对象的 ASMX 服务。

```csharp
[Serializable]
public class Person
{
    public int Id { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string Email { get; set; }
}

[WebServiceService]
public class PersonService : WebService
{
    [WebMethod]
    public Person GetPerson(int id)
    {
        // 在实际应用程序中，这将从数据库获取人员。
        return new Person
        {
            Id = id,
            FirstName = "John",
            LastName = "Doe",
            Email = "john.doe@example.com"
        };
    }
}
```

这是一个使用自定义对象的 ASMX 服务。要使用此服务，你需要在客户端代码中包含 Person 类。

```csharp
PersonService service = new PersonService();
Person person = service.GetPerson(1);
Console.WriteLine(person.FirstName + " " + person.LastName);
```

这就是你使用使用自定义对象的 ASMX 服务的方式。

# 构建 WCF 服务

WCF 是 .NET 中构建 Web 服务的现代方式。它比 ASMX 更复杂，但也更强大。在本章中，我们将学习构建简单的 WCF 服务。

要构建 WCF 服务，你需要定义一个接口。

```csharp
[ServiceContract]
public interface IHelloWorldService
{
    string HelloWorld(string name);
}
```

然后 WCF 服务实现该接口。

```xml
<services>
  <service name="HelloWorldService">
    <endpoint address="" binding="basicHttp" contract="IHelloWorldService" />
  </service>
</services>
```

这就是 WCF 服务。要使用它，你可以使用通道工厂代理。

```csharp
ChannelFactory<IHelloWorldService> factory = new ChannelFactory<IHelloWorldService>("service");
IHelloWorldService channel = factory.CreateChannel();
Console.WriteLine(channel.HelloWorld("World"));
```

这就是你使用 WCF 服务的方式。

```csharp
[ServiceContract]
public interface ICalculatorService
{
    int Add(int a, int b);
    int Subtract(int a, int b);
    int Multiply(int a, int b);
    int Divide(int a, int b);
}

public class CalculatorService : ICalculatorService
{
    public int Add(int a, int b) { return a + b; }
    public int Subtract(int a, int b) { return a - b; }
    public int Multiply(int a, int b) { return a * b; }
    public int Divide(int a, int b)
    {
        if (b == 0) throw new ArgumentException("Cannot divide by zero.");
        return a / b;
    }
}
```

这就是 WCF 服务实现。

```csharp
[ServiceContract]
public interface IPersonService
{
    Person GetPerson(int id);
}

[DataContract]
public class Person
{
    public int Id { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string Email { get; set; }
}

public class PersonService : IPersonService
{
    public Person GetPerson(int id)
    {
        return new Person { Id = id, FirstName = "John", LastName = "Doe", Email = "john.doe@example.com" };
    }
}
```

这就是你使用自定义对象的 WCF 服务的方式。

