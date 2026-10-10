
DetailsView 和 SqlDataSource 控件为你处理了大部分繁琐的工作。你只需要设置不同的模板，允许用户插入新行和更新现有行，然后由这两个控件处理剩余的所有工作。当你点击“插入”（Insert）链接时，正如你在之前的章节中看到的那样，程序会使用 JavaScript 对控件进行验证。同样的验证也会由 DetailsView 控件在服务器端再次执行，以确保提交的数据符合你的标准。如果数据有效，DetailsView 控件将根据模式插入或更新数据。要查看这些工作是如何运作的，请查看 `InsertItemTemplate` 中的 `Title` 列：

```
<InsertItemTemplate>
<asp:TextBox Id="TextBox" run="server" Text='<%# Bind("Title") %>' />
</asp:TextBox><asp:RequiredFieldValidator ControlToValidate="TextBox" ErrorMessage="Enter a title"
run="server" />
</asp:RequiredFieldValidator></InsertItemTemplate>
```

这段代码中最重要的部分是 `TextBox` 的 `Text` 属性进行了绑定。你之前见过通过使用 `Eval` 的单向绑定，它基本上是输出绑定列的值。然而，通过 `Bind`，你注意到了一些更强大的功能。`Bind` 允许你在来自 `SqlDataSource` 的列与页面上的控件之间建立双向的数据绑定。在这种情况下，评论的 `Title` 列被绑定到 `TextBox`。这意味着当控件必须显示其数据时（例如在更新现有行时），它必须显示评论的 `Title`。但重要的是，在回传（postback）时，在你点击“更新”（Update）链接后，控件理解 `TextBox` 控件与 `Title` 列之间的关系。因此，当你修改页面上的评论并点击“更新”时，DetailsView 会从表单中收集所有绑定数据（Title、Summary、Body、GenId 以及哪个项目已获得授权），然后将其发送到 `SqlDataSource` 控件，该控件为 `Review` 表的每个相关列设置了参数：

```
<asp:SqlDataSource Id="SqlDataSource1" run="server">

<UpdateParameters>
<asp:Parameter Name="Title" Type="String" />
<asp:Parameter Name="Summary" Type="String" />
<asp:Parameter Name="Body" Type="String" />
<asp:Parameter Name="GenId" Type="Int32" />
<asp:Parameter Name="Authorized" Type="Boolean" />
<asp:Parameter Name="UpdateDateTime" Type="DateTime" />
<asp:Parameter Name="Id" Type="Int32" />
</UpdateParameters>
</asp:SqlDataSource>
```

最终，`SqlDataSource` 收集所有参数值，将其注入 `UpdateCommand` 中，并发送到数据库。

这适用于 `Review` 表的所有列，但你可能注意到 `DateTime` 并不是任何 `SqlDataSource` 命令的一部分。那么其他列呢？数据库会自动设置为今天的日期和时间，没有必要在代码中包含它。`UpdateDateTime` 列则是另一回事了。显然，你不希望用户手动输入此列的值。系统应该帮助自动跟踪它。这就是为什么你通过将它的 `Visible` 属性设置为 `False` 从用户界面中隐藏了该控件。然而，`Insert` 和 `Update` 命令需要此列有一个值，你需要找到一种不同的方法来插入它。这就是 `Inserting` 和 `Updating` 事件派用用场。查看 `ItemInserting` 事件处理程序以大致了解其工作原理：

```
VB.NET
Protected Sub DetailsView1_ItemInserting(sender As Object,
    e As DetailsViewInsertEventArgs) Handles DetailsView1.ItemInserting
    e.Values("UpdateTime") = DateTime.Now
End Sub
```

```csharp
protected void DetailsView1_ItemInserting(object sender,
    DetailsViewInsertEventArgs e)
{
    e.Values["UpdateTime"] = DateTime.Now;
}
```

如你所知，`ItemInserting` 在 `InsertCommand` 发送到数据库之前之前触发。这是为用户界面中没有对应控件的列（例如 `UpdateDateTime`）提供（默认）值的绝佳位置。这段代码简单地将 `UpdateDateTime` 设置为今天的日期和时间。该值被发送到数据库，并用于为 `Review` 表的 `UpdateDateTime` 列赋值。

同样的原理也适用于 `Updating` 命令。在相应的事件中，你需要索引 `NewValues` 集合而不是 `Values` 集合，但原理是相同的。

你可能会认为，在 `Insert` 命令中你不需要设置 `UpdateDateTime`。毕竟，当你插入新行时，数据库会自动插入一个值。为了区分插入和更新，你需要进行更多手动工作。你必须从 `InsertCommand` 中删除该列，然后从 `<InsertParameters>` 集合中也删除该列。虽然这本身工作不大，但当你尝试修改 `SqlDataSource` 的 SQL 命令时，就会遇到麻烦，因为 `Insert` 和 `Update` 命令不同步。只需像这样设置 `UpdateDateTime` 代码即可解决许多此类问题。

当 `SqlDataSource` 控件进行插入或更新时，会分别触发 `ItemInserted` 或 `Updated` 事件。在这些事件内部，代码会检查 `e.Exception` 是否为 null/None。如果没有这个检查，无论是否发生错误，用户都会被重定向到 `Reviews.aspx` 页面。有了这个检查，用户将调用 `EndEditing()` 回到 `Reviews.aspx` 页面。

### VB.NET

```vb
Private Sub EndEditing()
    Response.Redirect("Reviews.aspx")
End Sub
```

### C#

```csharp
private void EndEditing()
{
    Response.Redirect("Reviews.aspx");
}
```

如果你有长数据列表需要展示，始终考虑在网格（grid）等控件上开启分页功能。如果你向用户展示包含许多项目的列表，他们往往会感到迷失。通常，每页大小设置在 10 到 20 个项目之间效果最好。

考虑将分页控件中的控件重命名，不要使用它们的默认值。例如，在之前的尝试（Try Out）中，你将 `sqlDataSource` 重命名为 `GenreDataSource`。这使得你更容易看到需要哪种数据源来获取有关类型的信息。如果分页中只有几个控件，这并不是问题，但一旦你的页面变得复杂，为控件选择区分性的名称就变得越来越重要。

考虑设置 `AddEditReview.aspx` 中验证控件的 CSS 类，并将其关联到 CSS 类。目前，你可以在根目录下的 `Styles` 文件夹中的样式表中创建它们，并将该文件链接到主页（master page）。在后续的章节中，你将为管理部分（Management）创建一个单独的主。

## 总结

本章基于你在第12章中学关于通过 SQL 访问数据库的通用知识。它首先讨论了 Visual Studio 工具箱中数据（Data）类别下的众多控件。

这些控件可以分为两组：数据绑定控件（data-bound controls）和数据源控件（data source controls）。第一组控件——包括 `GridView`、`DetailView` 和 `ListView`——用于在网页中显示数据。其中大多数（并非所有）通过暴露插入、更新和删除功能来允许你维护数据。

另一组数据源控件本身没有视觉外观。它们作为用户界面和数据库之间的桥梁。存在许多不同的数据源，每种对应特定的存储类型。在本章中，你看到了 `SqlDataSource` 控件，它允许你从许多不同的关系型数据库检索数据。

## 练习

- 1. 如果你需要创建一个用户界面，允许用户显示、排序、编辑和删除来自数据库的数据，最好的控件是哪一个？你如何将该控件连接到数据库？

- 2. 如果你想以以下格式显示数据库中类型的简单列表，你会选择哪种控件？

```
<<ul>
  <li>Punk/</li>
  <li>Hard Rock/</li>
  <li>Jazz/</li>
  <li>Techno/</li>
</ul>
```

- 3. `BoundField` 和 `TemplateField` 之间有什么区别？你会在什么情况下使用其中之一？

- 4. 存储连接字符串（connection strings）的最佳位置在哪里？你如何从该位置访问连接字符串？为什么你不应该将它们存储在页面中？

你可以在附录 A 中找到这些练习的答案。

## 本章所学

| 概念 | 说明 |
| :--- | :--- |
| 连接字符串 | 包含连接数据库（如 SQL Server）所需的必要信息的字符串。 |
| 数据源控件 | 一组 ASP.NET 控件，作为数据源（数据库、XML 文件等）与数据绑定控件之间的桥梁。 |
| 数据绑定表达式语法 | 用于将值从数据源绑定到控件属性（如标签和文本框）的语法。例如：`Text='<%# Bind("Title") %>'`。`Bind` 用于双向绑定，而 `Eval` 用于显示只读数据。 |
| 数据绑定控件 | 一组可以显示扁平和分级数据的 ASP.NET 控件。 |
| 表达式语法 | 一种简洁的语法，将各种来源（包括来自 `Web.config` 文件的连接字符串）绑定到控件属性。例如：`ConnectionString="<%# ConnectionStrings:PlainTextWroxConnectionString1 %>"` |
| InsertParameters UpdateParametersDelete Parameters | 一组用于向数据源控件提供数据以支持插入、更新和删除行为的参数。 |
| 命名实例 | 特定 SQL Server 实例的名称。用于区分同一台机器上的多个 SQL Server 安装。 |
| SelectParameters | 一组可以从来源（查询字符串、cookie 等）获取数据并可用于数据源控件中过滤数据的参数。 |

## 14

## LINQ 和 ADO.NET Entity Framework

- 什么是 LINQ 以及它的语法是什么样的
- 可用的不同 LINQ 形式以及何时适用使用
- 如何使用 ADO.NET Entity Framework
- 如何使用模型绑定（Model Binding）访问 ADO.NET Entity Framework
- 如何使用 `ListView` 和 `DataPager` 控件

**本章的 WROX.COM 代码下载**

你可以在 www.wrox.com/go/beaspnet451 的 Download Code 标签上找到本章的代码下载。代码位于第 14 文件夹中。

语言集成查询（LINQ）是一种与 .NET Framework 中使用的编程语言紧密集的查询语言。LINQ 允许你像 SQL 允许你在数据库中查询数据一样，从 .NET 编程语言中查询数据。事实上，LINQ 语法部分参考了 SQL 语言进行建模，使得熟悉 SQL 的程序员更容易开始学习 LINQ。

LINQ 有几种不同的实现，允许你通过 VB.NET 或 C# 代码访问并查询各种来源，包括内存中的数据、XML 文件、.NET DataSets 和数据库。在下一节中，你将对 LINQ 的核心支柱进行简要概述。本章的剩余部分将重点关注。

## 介绍 LINQ

ADO.NET Entity Framework (EF) 是一种允许你访问数据并使用 SQL Server 以及许多其他类型数据源的技术。ADO.NET 也用于 `SqlDataSource` 控件的底层，并通常用于“原始数据访问代码”（使用 C# 或 VB 编写，在不使用声明式控件的情况下连接数据库）。

LINQ 允许你像 SQL 允许你在数据库中查询数据一样，从 .NET 编程语言中查询数据。事实上，LINQ 语法部分参考了 SQL 语言进行建模，使得熟悉 SQL 的程序员更容易开始学习 LINQ。

LINQ 有几种不同的实现，允许你通过 VB.NET 或 C# 代码访问并查询各种来源，包括内存中的数据、XML 文件、.NET DataSets 和数据库。在下一节中，你将对 LINQ 的核心支柱进行简要概述。本章的剩余部分将重点关注。

然而，后者框架比 LINQ to SQL 要强大得多，并提供了更多功能。因为它更强大，所以 Entity Framework 比 LINQ to SQL 更受青，因此它是本章的主题。

关于其他类型实现性的更多信息，请访问 LINQ 官方首页：http://bit.ly/18ypUj。

## 介绍 ADO.NET ENTITY FRAME

EF 是一个对象关系映射（ORM），支持数据导向型软件应用程序的开发。通过 EF，你可以将表等一系列数据库对象转换为可以在代码中访问的 .NET 对象。然后，你可以在查询中使用这些对象，或直接在数据绑定场景中使用它们。EF 还允许你进行相反的操作：首先设计对象模型，然后让 EF 为你创建数据库结构。

使用 EF 既美观又灵活。使用设计器，你可以将表等对象从数据库拖放并释放到你的实体模型（Entity model）中。你拖到图表上的数据库对象将作为 .NET 对象变得可用。例如，如果你将 Review 表拖到图表中，你将得到一个强类型的 Review 类。正如本章后面所示，你可以使用 LINQ 查询和其他方法创建该类的实例。

> 注意：ADO.NET Entity Framework 本身就是一个庞大且复杂的话题。它的内容比本章能涵盖的多得多。要深入了解 EF，请阅读 Julian Berman 编写的优秀书籍《Programming Entity Framework Second Edition》。

当你向图表上拖入多个相关的表时，设计器会检测表与表之间的关系，然后在你的对象模型中复制这些关系。例如，如果你在代码中使用 LINQ to Entities 查询创建了一个 Review 实例（正如你后面看到的），你可以访问它的 Genre 属性，这反过来又让你访问像 Name 等属性：

```vb.net
Label.Text = myReview.Genre.Name
```

```csharp
Label.Text = myReview.Genre.Name;
```

同样，你可以访问特定流的关联 Reviews 集合，例如将其绑定到数据绑定控件上：

```vb.net
Repeater.DataSource = myGenre.Reviews
```

```csharp
Repeater.DataSource = myGenre.Reviews;
```

现在先不要担心具体的语法。你将在本章的剩余部分看到很多此类语法。这一节需要关注的是 EF 在你的 .NET 应用程序和 SQL Server 数据库之间创建了一个层。实体设计器（Entity Designer）为你处理了大部分工作，提供了一个你可以在应用程序中使用的整洁对象模型的访问。

## 将你的数据模型映射到对象模型

通过 EF，你将数据库中的项（如表、列和关系）映射到应用程序中对象模型中的对象和属性。VS 提供了极佳的工具来让这种映射尽可能简单，正如你在以下练习中所示。

### 尝试一个简单的 LINQ to Entities 示例

在本次“尝试”中，你将看到如何向项目添加 ADO.NET 实体数据模型文件，向模型中添加数据库，然后编写一个简单的 LINQ 查询来访问底层表中的数据。

- 1. 打开你到目前为止一直工作的 PlanetWrox 项目。右键点击 App_Code 文件夹，选择“添加” > “新建项”，并在左侧选择你的编程语言。点击“ADO.NET 实体数据模型”，输入 **PlanetWrox** 作为名称，并并点击“添加”将其添加到项目中。如果你在列表中没有看到它，请检查你是否右键点击了 App_Codes 而不是 App_Data 等其他文件夹。

- 2. 在随后的对话框中，确保选中了“从数据库生成”（Generate from Database）并点击“下一步”。

- 3. 在“选择你的数据连接”中，确保下拉列表中选中了 **PlanetWroxConnectionstring1**，并勾选“在 web.config 中设置设置”框框。你的对话框现在看起来像图 14-1。点击“下一步”进入“选择你的版本”对话框。选择 Entity Framework 6.0 并点击“下一步”。
