

关于一组特定的功能，而不是任何具体的实现。这使我们的代码能够接受不同的集合类型，而无需修改。在下一章中，我们将通过创建和实现自己的接口来深入探讨具体做法，这将使我们的应用程序易于扩展。

## 第3章 如何创建接口以增加可扩展性

我们已经看到接口如何帮助我们让代码经得起未来的考验。现在，是时候看看接口如何让我们的代码易于扩展了。如果我们制定一个核心应用程序可以使用的契约，那么我们就可以接入任意数量的符合该契约的不同实现。为此，我们将探讨接口的具体做法。首先，我们将看到如何创建自己的接口。在这种情况下，是一个仓储接口，帮助我们连接不同的数据源。然后我们将看到如何通过编写多个仓储来实现这个接口。这些仓储将让我们能够从Web服务、文本文件和SQL数据库获取数据。在创建了这些不同的实现之后，我们将通过使用工厂方法来消除重复代码。这将把具体细节移到项目的不同部分，这样我们就可以专注于正在处理的代码的重要功能。在我自己的工作中，我创建了一个规则引擎，允许轻松添加不同的规则类型。我还组装了自定义工作流，允许完全控制每一步，我还使用过一个授权客户端，它可以连接到不同类型的用户存储。这些可扩展的应用程序都是通过接口实现的。

假设我们有一个将部署到多个客户端站点的应用程序。每个客户端对于存储和检索数据都有自己的偏好。我们的应用程序需要从各种来源获取数据。可能是一个Web服务，它给我们返回数据的表示形式，其中JSON代表JavaScript Object Notation，或者是一个包含值的CSV文本文件，或者是一个关系数据库，如Microsoft SQL Server或SQLite。也可能是一个文档数据库，或者是一个云中的服务，如Amazon AWS，或者是一个Azure函数调用，为我们提供所需的数据。与每个数据源交互都有特定的方式。当我们使用Web服务时，我们通过网络进行HTTP调用。对于文本文件，我们使用文件输入/输出操作。但是我们不希望核心应用程序代码处理这些细节。相反，我们将建立一个仓储。以下是Martin Fowler对仓储模式的描述。仓储模式使用一个用于访问领域对象的接口，在领域层和数据映射层之间进行中介。让我们探讨一下这意味着什么。仓储模式让我们将应用程序代码与特定的数据存储技术分离。我们不希望应用程序代码需要知道如何进行HTTP调用或打开文件系统上的文件。相反，仓储负责这些细节。然后，仓储将数据作为应用程序可以使用的标准C#对象公开。在我们的案例中，我们将创建几个不同的仓储。服务仓储将知道如何向返回JSON数据的Web服务发出HTTP调用，这些数据使用JavaScript Object Notation格式化。CSV仓储将知道如何打开文件系统上的文件并解析值。SQL仓储将知道如何使用Entity Framework连接到SQLite数据库。那么这些如何接入我们的应用程序呢？通过接口。我们将创建一个仓储接口，作为我们的契约，其中包含与数据交互的方法。

```csharp
private IActionResult PopulatePeopleView(string readerType)
{
    IPersonReader reader = readerFactory.GetReader(readerType);
    IEnumerable<Person> people = reader.GetPeople();
    ViewData["ReaderType"] = reader.GetType().ToString();
    return View("Index", people);
}
```

对于仓储，有几种不同的方法。我们将从CRUD仓储开始，其中CRUD代表创建、读取、更新和删除。这些是我们获取和更新数据对象所需的基本操作。CRUD仓储描述了读和写操作。但是当我们查看使用数据的代码时，我们只有读取操作。有一个关于接口的实践，可以让我们的代码更易于维护。这个实践是让我们的接口只包含客户端使用的方法。因此，如果我们的客户端代码只读取数据，那么我们的接口也应该只包含读取操作。所以我们将创建一个只包含读取操作的仓储接口。

```csharp
public interface IPersonReader
{
    IEnumerable<Person> GetPeople();
    Person GetPerson(int id);
}
```

我们将使用术语“数据读取器”而不是“仓储”，因为它更好地描述了实际功能。我们的接口有两个成员。GetPeople返回Person对象的IEnumerable，这允许我们获取整个数据集合。此外，我们有一个GetPerson方法，它接受一个id作为参数并返回单个Person记录。在下面的演示中，我使用Visual Studio 2019。在Visual Studio Code中运行项目略有不同。首先，我们将创建一个实现我们接口的数据读取器。具体来说，我们将创建一个服务数据读取器。我们最终会得到多个数据读取器。除了服务读取器，我们还将有一个使用文本文件的CSV读取器和一个使用SQLite数据库的SQL读取器。一旦应用程序开始使用这些数据读取器，我们将移除重复代码。我们的接口将使这变得更容易。那么，让我们直接看代码吧。现在我们来到了Visual Studio，打开了Extensibility解决方案。这里有三个项目。PersonReader.Interface项目包含我们的接口。People.Service项目是一个提供数据的Web服务。PeopleViewer项目是一个向用户展示数据的Web应用程序。在查看代码之前，让我们运行应用程序看看我们有什么。当我按F5启动项目时，你会看到两个控制台窗口打开。这是因为我们的解决方案设置为同时启动Web服务和Web应用程序。在我们的Web应用程序中，我们有三个链接，一个用于从Web服务获取数据，一个用于从CSV文本文件获取数据，一个用于从SQL数据库获取数据。

```csharp
using System.Collections.Generic;

namespace PersonReader.Interface
{
    public interface IPersonReader
    {
        IEnumerable<Person> GetPeople();
        Person GetPerson(int id);
    }
}
```

这包含了我们将要实现的接口，其中有两个方法：返回Person的IEnumerable的GetPeople，以及根据ID返回单个Person记录的GetPerson。让我们看一下Person对象。我只需右键单击并选择“查看定义”（Peek Definition），这会显示我们的Person类有六个属性和一个对ToString方法的重写。这些属性与服务返回的字段相匹配。

```csharp
public class Person
{
    public int Id { get; set; }
    public string? GivenName { get; set; }
    public string? FamilyName { get; set; }
    public DateTime StartDate { get; set; }
    public int Rating { get; set; }
    public string? FormatString { get; set; }

    public override string ToString()
    {
        if (string.IsNullOrEmpty(FormatString))
            FormatString = "{0} {1}";
        return string.Format(FormatString, GivenName, FamilyName);
    }
}
```

那么现在让我们创建一个实现此接口的服务读取器。对于这个示例，我们将把它放在一个单独的项目中。我将右键单击Readers文件夹，选择“添加”->“新建项目”，然后当对话框出现时，我会选择“类库”，我们将看到这是一个用于创建面向.NET Standard或.NET Core的类库的项目。尽管描述中没有提到，但它也面向.NET 5。我们单击“下一步”，在项目名称中选择PersonReader.Service，再单击“下一步”。对于目标框架，我们选择.NET 5.0，然后我们就创建项目。在我们的新项目中，会看到一个Class1.cs文件，我将右键单击它并选择“重命名”，将其命名为ServiceReader。我喜欢重命名文件，因为当我重命名文件时，Visual Studio会询问我是否也要重命名类。当我选择“是”时，我们现有的Class1将变为ServiceReader。

```csharp
using System;

namespace PersonReader.Service
{
    public class ServiceReader
    {
    }
}
```

我们的ServiceReader需要实现IPersonReader接口，所以我将写 `: IPersonReader`。你会注意到我在这里没有得到任何IntelliSense，因为我没有添加到接口项目的项目引用，而且文件顶部也没有using语句。但Visual Studio在这里可以帮助我们。如果我按Ctrl+.，其中一个选项是添加对PersonReader.Interface项目的引用，它也会在文件顶部添加using语句。

