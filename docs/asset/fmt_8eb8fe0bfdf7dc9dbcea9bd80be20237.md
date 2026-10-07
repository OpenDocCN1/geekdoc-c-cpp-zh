
```
http://localhost:4113/NorthwindDataService.svc/
Products(1)?Expand=Suppliers/Products
```

使用这种结构，你正在查看产品列表中的第一个产品，并扩展该产品内部供应商的章节。然后，在供应商内部，这些供应商所销售的关联产品也在结果集中。如你所见，这种可以轻松地钻取嵌套关系的能力是非常强大的功能。

# 结果集中的排序

另一种管理来自 URI 查询的响应集的方法，是按照你定义的特定顺序获取集合结果。你可以使用 `orderby` 关键字作为查询字符串命令来实现：

```
http://localhost:4113/NorthwindDataService.svc/
Products?orderby=ProductName
```

在这种情况下，你将获得一个根据实体 `ProductName` 字段按字母顺序排列的完整产品列表。你还可以为提供的排序分配升序或降序值。默认分配的是升序。这意味着先前的查询与以下内容相同：

```
http://localhost:4113/NorthwindDataService.svc/
Products?orderby=ProductName desc
```

注意 URI 中 `ProductName` 和 `desc` 之间存在一个实际的空格。如果你想以反向顺序或降序）排列，请使用以下结构：

你还可以使用 WCF Data Services 执行嵌套排序：

```
http://localhost:4113/NorthwindDataService.svc/
Products?orderby=Discontinued asc, ProductName asc
```

# 在结果集中移动

作为该界面的终端用户，你可能发现，取决于数据库中的内容，你将处理相当大的结果集。如果你只需要数据库表的一部分，并且正在请求所有的客户（可能是 100,000 个或更多），该怎么办？

在这种情况下，WCF Data Services 提供了获取数据库较小子集并导航到所需页面的能力。这是通过两个查询字符串命令的组合实现的：`top` 和 `skip`。

它们本身也相当强大。例如，通过 `top` 命令，你可以根据正在进行的排序提取 `n` 个项目。例如，考虑此内容：

```
http://localhost:4113/NorthwindDataService.svc?$top=5
```

在这里，前五个实体（在此例中基于 `CustomerID` 值）被从数据库中提取并返回。如果你根据不同的值提取顶部的实体，可以使用类似下面的内容：

```
http://localhost:4113/NorthwindDataService.svc/Products?orderby=OnOrder$desc&$top=5
```

使用此示例，将根据订单项目数量返回顶部的产品。

你可以使用 `skip` 命令基本上跳过第一组定义的项目。例如，你可以执行类似以下的操作：

```
http://localhost:4113/NorthwindDataService.svc/Customers?$skip=5
```

在这种情况下，返回的客户减去了通常会返回的前五个。虽然此命令的值还有待疑问，但当它与 `top` 关键字结合时，其威力是显而易见的。

```
http://localhost:4113/NorthwindDataService.svc/Customers?$skip=10&$top=10
```

在这种情况下，你跳过了前十个实体，然后从这一点开始获取两个组各包含十个项目的集合。这使得通过此过程使用 URI 命令来获取所需数据页以执行某种类型的数据库分页变得非常简单。

# 过滤内容

最后一个命令是你可以调用的最强大的命令之一。它是一种允许你从数据库中过滤真正感兴趣的内容类型。这是通过使用 `filter` 命令完成的：

```
http://localhost:4113/NorthwindDataService.svc/Customers?$filter=Country eq 'Germany'
```

使用符号 `$` 前的 `filter` 命令，该命令的值为 `'Germany'`。通过此命令，你请求位于 `Germany` 的客户列表。在 URI 中，数据库属性是 `Country`，并且重要的是要正确指定此属性。这意味着如果你使用 `country` 而不是 `Country`，则结果集中将不会有任何项。`Germany` 值放在单引号中，运算符被指定为一组字符，而不是相等 `=`。使用 `filter` 命令，你用 `eq` 指定运算符。表 31-2 列出了你可以使用的逻辑运算符。

# 表 31-2

| 运算符 | 说明 | 示例 |
| :--- | :--- | :--- |
| Eq | 等于 | eq 'Germany' |
| Ne | 不等于 | ne 'Germany' |
| Gt | 大于 | gt 20 |
| Ge | 大于等于 | ge 20 |
| Lt | 小于 | lt 20 |
| Le | 小于等于 | le 20 |
| And | 逻辑与 | gt 0 and gt 0 |
| Or | 逻辑或 | gt 0 or lt 10 |
| Not | 逻辑非 | gt 0 not eq 'Chang' |

除了逻辑运算符外，你还可以使用一些算术运算符，如表 31-3 所示。

# 表 31-3

| 运算符 | 说明 | 示例 |
| :--- | :--- | :--- |
| Add | 加 | add 5 |
| Sub | 减 | sub |
| Mul | 乘 | mul |
| Div | 除 | div |
| Mod | 取模 | mod |

`Germany` 值放在单引号中，运算符被指定为一组字符。使用 `filter` 命令，你用 `eq` 指定运算符。表 31-2 列出了你可以使用的逻辑运算符。还有大量的字符串、日期和数学函数：

* endswith
* length
* indexof
* insert
* remove
* replace
* substring
* trim
* toupper
* day
* minute
* second
* month
* year
* ceiling
* floor

你可以这样使用这些函数：

```
http://localhost:4113/NorthwindDataService.svc/
Products?$filter=endswith(QuantityUnit,'bottles')
```

在这种情况下，你正在从数据库中检索以...结尾的产品。

# 在 ASP.NET 中消费 WCF 数据服务

现在你已经了解如何构建 WCF Data Service，下一步是在 ASP.NET 中消费它。在所有 .NET 中消费 WCF 数据服务是显而易见的，但本章重点在 ASP.NET 内部使用该技术。

要消费数据服务，在 Visual Studio 中创建一个标准的 ASP.NET 应用程序。在 `Default.aspx` 页面上创建一个仅包含 GridView 的简单页面。列表 31-42 展示了此示例。

# 列表 31-42：带有 GridView 的标准 ASP.NET 页面

```asp
<% Page Language="C#" AutoEventup="true"
CodeFile="Default.aspx" Inherits="Default" %>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>Working with Data Services</title>
</head>
<body>
<form id="form" runat="server">
<div>
<asp:GridView ID="GridView1" runat="server" BackColor="White"
BorderColor="#FDFDFDF" BorderStyle="None" Width="10%"
CellPadding="4"
ForeColor="Black" GridLines="Vertical">
<RowStyle Color="#F7FF7" />
<FooterStyle Color="#CCCCCC" />
<PageStyle Color="#F7FF7" HorizontalAlign="Right" />
<SelectedRow Style="#CE5D5A" Font-Bold="True" ForeColor="White" />
<HeaderStyle Color="#6B6B6B" Font-Bold="True" ForeColor="White" />
<AlternatingRow Style="White" />
</asp:GridView>
</div>
</form>
</body>
</html>
```

现在你已经准备好了页面，在 Visual Studio 资源管理器中右键点击项目，从提供的菜单中选择“添加引用”（Add Service Reference）。出现“添加引用”对话框。

由于 WCF Data Service 是标准的 `.svc` 文件，你可以在文本框中引用你的 Northwind `.svc` 文件并点击“转到”按钮。列表 31-31 显示与其他内容类似。

如如图所示，所有的底层对象都在对话框中表示。在“命名空间”（Namespace）文本框中，你可以将其命名为 Northwind，然后点击“确定”接受此配置。

下一步是从代码后页面使用此引用。此工作显示在列表 31-43 中。

![](img/7040c21013b8e6c23c612d6da3599ff8_1272_0.png)

图 31-31

除了前面代码中简单的查询外，在代码中使用 LINQ 时，你还可以开始使用本章之前介绍的一些命令逻辑。列表 31-44 显示了对 `Customer` 表的查询，其中你只感兴趣 `Country` 值为“Germany”的客户。

# 列表 31-44：使用 LINQ

```vbnet
Dim svc As New NorthwindEntities(New Uri("http://localhost:4113/NorthwindDataService.svc").ToString())
Dim query = From c In svc.Customers
Where c.Country.Contains("Germany")
Select c

GridView.DataSource = query
GridView.DataBind()
```

```csharp
var svc = new NorthwindEntities(new Uri("http://localhost:4113/NorthwindDataService.svc").ToString());

var query = from c in svc.Customers
where c.Country.Contains("Germany")
select c;

GridView.DataSource = query;
GridView.DataBind();
```

在此段代码中，执行了一个 LINQ 查询，然后将该对象绑定为 GridView 的 `DataSource` 值。这将在网格中产生另一个项目列表。

### 总结

本章是对 .NET 平台中 XML Web 服务的快速巡览。这绝对是一个值得专门出一本书的话题。本章向你展示了将数据和逻辑暴露为 SOAP 的威力，以及如何在你构建的 ASP.NET 中消费这些消息。

除了指出你在构建和消费基本 Web 服务方面所拥的力量外，本章还花了一些时间理解缓存、SOAP 头部的使用等。随着 Web 服务开始深度渗透到各种企业组织，这种模型每天都内置了许多强大功能。当你需要为应用程序获取某些数据或逻辑时，你很可能会采用本章介绍的策略。

尽管本章内容详尽，但它从广义上概述了框架的基础。当你开始深入研究这项技术时，你会发现它具有强大且可扩展的能力。

WCF Data Services 是暴露你的数据库内容的一种强大且新的方式。本章研究了通过对接口执行命令来过滤特定内容。许多命令可以作为 URI 的一部分，获取你感兴趣的特定结果。

然而，在处理 ASP.NET 页面时，使用代码（更具体说是使用 LINQ）同样可以从接口获取你想要的结果。如果你想让这些查询对用户隐藏并封装在你的代码中，那么这是最佳方法。记住，查询字符串对包含字符的数量也有限制，有时在代码中使用 LINQ 可能是你唯一的选择。

# 32

# 构建全球化应用程序

- 应用程序全球化
- 定义文化（包括服务器端和客户端）
- 处理本地和全局资源

开发者通常用他们的母语言构建 Web 应用程序，然后随着应用程序受众的扩大，他们意识到将应用程序全球化的需求。当然，理想情况是从一开始就构建能够处理国际受众的 Web 应用程序——但在许多情况下，由于需要额外的工作，这可能是不行的。

值得注意的是，在 ASP.NET 框架中，人们在解决 Web 应用程序的国际化方面做了巨大努力。你会很快发现，API 的更改、服务器控件功能的添加，甚至 Studio 本身，都让你在构建面向国际受众的应用程序时能够更轻松地完成额外工作。本章介绍了在为全球构建 Web 应用程序时需要考虑的一些重要事项。

# 文化与区域

在用户浏览器中打开的 ASP.NET 在特定的文化和区域设置下运行。在构建 ASP.NET 应用程序或页面时，其运行的定义文化取决于运行应用程序的服务器提供的文化和区域设置，或来自客户端（最终用户）的设置。默认情况下，ASP.NET 在由服务器定义的文化下运行。

世界由许多文化组成，每种文化都有自己的语言以及一套定义的观察和消费数字、使用货币、按字母排序等方式。.NET 框架使用 Request for Comments 1766 标准定义（用于识别语言的标记）来定义文化和区域，该标准使用用连字符分隔的两个字母代码来指定语言和区域。表 32-1 提供了某些文化的示例。

# 表 32-1

| 文化代码 | 描述 |
| :--- | :--- |
| en-US | 英语；美国 |
| en-GB | 英语；英国（大不伦） |
| en-AU | 英语；澳大利亚 |
| en-CA | 英语；加拿大 |

查看表中的示例，你可以看到定义了四种不同的文化。这四种文化既有相似之处也有差异。所有文化都说同一种语言（英语）。因此，每个文化设置中都使用了语言代码 en。在语言设置之后，区域（例如美国的 US、英国的 GB、澳大利亚的 AU 和加拿大的 CA）非常重要。正如你所意识到的，美国的英语与英国使用的英语略有不同，以此此类推。在日期和数值的表示上存在差异。这就是为什么要呈现文化的语言和区域的原因。

差异并不仅按国家划分。

# 理解文化

差异并不仅按国家划分。这四种文化既有相似之处也有差异。所有文化都说同一种语言（英语）。因此，每个文化设置中都使用了语言代码 en。在语言设置之后，区域（例如美国的 US、英国的 GB、澳大利亚的 AU 和加拿大的 CA）非常重要。正如你所意识到的，美国的英语与英国使用的英语略有不同，以此此类推。在日期和数值的表示上存在差异。这就是为什么要呈现文化的语言和区域的原因。

# 第 32 章 构建全球化应用程序

![](img/7040c21013b8e6c23c612d6da3599ff8_1279_0.png)

你可以通过新实例化 `CultureInfo` 对象来在重载方法中更改线程的区域设置，如列表 32-2 所示。

> 列表 32：使用 CultureInfo 对象更改线程

```VB
Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs) Handles Me.Load

System.Threading.Thread.CurrentCulture = New CultureInfo("th-TH")

Dim ci As CultureInfo = System.Threading.Thread.CurrentCulture

Response.Write("<br>" + ci.Info() + "<br>")

Response.Write("<br>" + ci.Name + ": " + ci.Name.ToString() + " &<br>")

Response.Write("<br>" + ci.Parent.Name + ": " + ci.Parent.Name.ToString() + " &<br>")

Response.Write("<br>" + ci.DisplayName + ": " + ci.DisplayName.ToString() + " &<br>")

Response.Write("<br>" + ci.EnglishName + ": " + ci.EnglishName.ToString() + " &<br>")

Response.Write("<br>" + ci.NativeName + ": " + ci.NativeName.ToString() + " &<br>")

Response.Write("<br>" + ci.ThreeLetterISOName + ": " + ci.ThreeLetterISOName.ToString() + " &<br>")

Response.Write("<br>" + ci.CalendarType + ": " + ci.CalendarType.ToString() + " &</p>")

End Sub
```

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    System.Threading.Thread.CurrentCulture = new CultureInfo("th-TH");
