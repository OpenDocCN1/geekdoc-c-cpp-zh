

![](img/cf72ea860016d2d680fc085fc06f265a_689_0.png)
图 21-11

你将看到，使用 Code First 时，你只需创建 C# 对象和集合，Entity Framework 就会为你创建数据库结构，并让你轻松地导航数据库对象之间的关系，然后查询数据库中的相关对象。

## 试一试

导航数据库关系：BegVCSharp_21_2_DatabaseRelations

请按照以下步骤在 Visual Studio 2015 中创建示例：

- 1. 在目录 C:\BegVCSharp\Chapter21 中创建一个名为 BegVCSharp_21_2_DatabaseRelations 的新控制台应用程序项目。
- 2. 单击 OK 创建项目。
- 3. 像上一个示例一样，使用 NuGet 添加 Entity Framework。转到“工具” → “NuGet 包管理器” → “为解决方案管理 NuGet 程序包”。
- 4. 在 NuGet 包管理器中，选择 Entity Framework，取消选中“包括预发行版”复选框，并获取 Entity Framework 最新的稳定版本。单击 Install 按钮。由于上一步已经下载过，因此无需再次下载。在“预览更改”对话框中单击 OK，并在“许可证接受”对话框中单击“我接受”按钮。
- 5. 打开主源文件 Program.cs。与上一个示例一样，添加 System.Console、System.Data.Entity 和 DataAnnotations 命名空间的 using 语句，以及创建 Book 类的代码：

```csharp
using System.Data.Entity;
using System.ComponentModel.DataAnnotations;
using static System.Console;

namespace BegVCSharp_21_2_DatabaseRelations
{
    public class Book
    {
        public string Title { get; set; }
        public string Author { get; set; }
    }
}
```

然后，你创建了一个简单的 LINQ 查询，用于列出所有商店的信息：

```csharp
var query = from store in db.Stores
            orderby store.Name
            select store;
```

用于打印查询结果的代码非常简单，因为它只处理对象和集合，没有任何数据库特定的代码：

```csharp
WriteLine("Bookstore Inventory Report:");
foreach (var store in query)
{
    WriteLine($"{store.Name} located at {store.Address}");
    foreach (Stock stock in store.Inventory)
    {
        WriteLine($"-- Title: {stock.Item.Title}");
        WriteLine($"-- Copies in Store: {stock.OnHand}");
        WriteLine($"-- Copies on Order: {stock.OnOrder}");
    }
}
```

要在每家商店下面打印其库存，你只需像处理任何集合一样使用 foreach 循环。

## 处理迁移

开发代码时，你不可避免地会改变主意。你可能会为某个属性想出一个更好的名称，或者意识到需要新的类或关系。如果你更改了通过 Entity Framework 连接到数据库的类中的代码，则首次运行修改后的程序时会遇到图 21-14 中显示的 InvalidOperationException。

![](img/cf72ea860016d2d680fc085fc06f265a_695_0.png)
图 21-14

让数据库与已更改的类保持同步很复杂，但 Entity Framework 再次提供了一个使这一过程相对容易的机制。正如错误消息所建议的，你需要向程序添加 Code First Migrations 包。

为此，请转到“工具” → “NuGet 包管理器” → “包管理器控制台”。这会打开如图 21-15 所示的命令窗口。

要在数据库更新到新的类结构时启用自动迁移，请在包管理器控制台的 PM> 提示符下输入以下命令：

```
Enable-Migrations -EnableAutomaticMigrations
```

![](img/cf72ea860016d2d680fc085fc06f265a_696_0.png)
图 21-15

这会向你的项目添加一个 Migrations 类，如图 21-16 所示。

![](img/cf72ea860016d2d680fc085fc06f265a_696_1.png)
图 21-16

Entity Framework 会比较数据库和程序的时间戳，并在数据库与类不同步时提醒你。要更新数据库，只需在包管理器控制台的 PM> 提示符下输入以下命令：

```
Update-Database
```

## 从现有数据库创建和查询 XML

在最后一个示例中，你将结合到目前为止学到的有关 LINQ、数据库和 XML 的所有知识。

XML 通常用于在客户端和服务器计算机之间，或在多层应用程序的“层”之间传递数据。常见的做法是在数据库中查询某些数据，然后根据这些数据生成 XML 文档或片段，再传递给另一层。

在下面的“试一试”中，你创建查询以在前一个示例的数据库中查找某些数据，使用 LINQ to Entities 查询这些数据，然后使用 LINQ to XML 类将数据转换为 XML。这是 Database First（相对于 Code First 编程）的一个示例，即从现有数据库生成 C# 对象。

## 本章你学到的内容

| 主题 | 关键概念 |
| --- | --- |
| 使用数据库 | 数据库是持久化、结构化的数据存储库。虽然数据库种类很多，但用于业务数据的最常见类型是关系数据库。 |
| Entity Framework | Entity Framework 是一组用于在 C# 对象和关系数据库之间进行对象关系映射的 .NET 类。 |
| 如何使用 Code First 创建数据 | 通过使用 Entity Framework 中的 Code First 类，你可以利用对象关系映射直接从 C# 类和集合创建数据库。 |
| 如何将 LINQ 与数据库一起使用 | LINQ to Entities 可以利用用于创建数据的相同 Entity Framework 类，对数据库执行功能强大的查询。 |
| 如何导航数据库关系 | Entity Framework 可以通过在 C# 代码中使用虚拟属性和集合，创建并导航数据库中相关的实体。 |
| 如何从数据库创建和查询 XML | 可以通过在单个查询中组合 LINQ to Entities、LINQ to Objects 和 LINQ to XML，从数据库构造 XML。 |

## 第四部分

## 其他技术

- 第 22 章：Windows Communication Foundation
- 第 23 章：Windows Store 应用

## 22

## Windows Communication Foundation

## 本章你将学习：

- 了解 WCF
- 掌握 WCF 概念
- 理解 WCF 编程

## 本章的 WROX.COM 代码下载

本章的 wrox.com 代码下载可在 www.wrox.com/go/beginningvisualcsharp2015programming 的 Download Code 选项卡中找到。代码位于 Chapter 22 下载中，并按本章中的名称单独命名。

近年来，随着互联网使用日益普及，Web 服务迅速增加。Web 服务就像一个由计算机而不是人使用的网站。例如，你不必浏览关于自己最喜欢电视节目的网站，而可以使用桌面应用程序通过 Web 服务获取相同的信息。这里的优点是，同一个 Web 服务可以被各种应用程序甚至网站使用。此外，你也可以编写自己的应用程序或网站来使用第三方 Web 服务。也许你还可以把最喜欢电视节目的信息与地图服务结合起来，显示拍摄地点。

.NET Framework 已经支持 Web 服务一段时间了。不过，在较新版本的框架中，Web 服务与另一种称为远程处理（remoting）的技术相结合，创建了 Windows Communication Foundation（WCF），这是一种用于应用程序之间通信的通用基础结构。

