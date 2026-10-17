
你可以随时使用 `DataSet`，但有时你可能倾向于使用 `DataReader` 并直接与数据存储交互。通过使用命令对象（如 `SqlCommand` 和 `OleDbCommand` 对象），你对执行的内容以及返回的结果有更直接的控制。在某些不使用 `DataSet` 对你有利至关重要的情况下。

当你使用 `DataSet` 时，你不会产生开销成本，因为你是直接对数据源进行读写。以这种方式操作意味着你不需要实例化任何额外的对象——避免了这种性。

这在 ASP.NET 中配合 Web Forms 工作的情况下是真实的。如果你在处理 Web Forms，Web 页面每次都会重新创建。当这种情况发生时，只有页面通过调用数据源重新创建，除非你缓存了 `DataSet`，否则 `DataSet` 也会重新创建。这是一个可能昂贵的过程；因此，在这种情况下，你可能会发现使用 `DataReader` 直接操作数据源是有益的。在大多数使用 Web Forms 的情况下，你可能更希望使用 `DataSet`。

## 强类型 DataSet (Typed DataSet)

尽管 `DataSet` 功能强大，但它仍然存在一些局限性。`DataSet` 是在运行时创建的。它通过做出某些假设来访问特定的数据片段。看看你通常是如何访问非强类型 `DataSet` 中的特定字段的（列表 8-13）。

### 列表 8-13：访问 DataSet 中的字段

```VB
ds.Tables("Customers").Rows(0).Columns("CompanyName") = "XYZ Company"
```

前面的代码查看了 `Customers` 表、第一行（从 0 开始计数）的 `CompanyName` 列，并将 `XYZ Company` 的值分配给该字段。这非常简单，但它是基于某些假设并且在运行时生成的。`"Customers"` 和 `"CompanyName"` 是这行代码中的字符串字量。如果拼写错误，会在运行时发生错误。列表 8-14 显示了如何使用强类型 `DataSet` 为该字段分配相同的值。

### 列表 8-14：访问强类型 DataSet 中的字段

```VB
ds.Tables("Customers").Rows(0).Columns("CompanyName") = "XYZ Company"
```

现在，表名和要访问的字段不再被视为字符串字面量，而是被编码在 XML Schema 和从 `DataSet` 生成的类中。当你创建一个 `DataSet` 时，你正在创建一个根据架构实现表和字段的类。基本上，架构被编码在其中了。当你比较这两个示例时，你会发现强类型 `DataSet` 更易阅读和理解。它更不容易出错，而且错误是在编译时而不是运行时发现的。根结底，强类型 `DataSet` 是可选的，你可以自由使用任何风格。

## 在 ASP.NET 中使用 Oracle 作为你的数据库

如果你在企业领域工作，很多情况下你必须与 Oracle 数据库工作。`ADO.NET` 2.0 具有内置功能，可以使用 `System.Data.OracleClient` 命名空间与 Oracle 配合工作。首先，为了让 ASP.NET 连接到你的 Oracle 数据库，请在服务器上安装 Oracle 10 客户端。你可以从 Oracle 网站 `oracle.com` 获取该软件。如果你能够从服务器使用 SQL 连接到你的 Oracle 数据库。

# 第 8 章：使用 ADO.NET 进行数据管理

`oracle.com`。你可以在可以在项目中引用这个新的 DLL。现在只需在应用程序中导入并使用 `System.DataAccess.OracleClient` 即可。由 Oracle 构建的数据提供了使用 Oracle 10g 数据库所提供的更高级功能的能力。

## DataList 服务器控件

`DataList` 控件从 ASP.NET 初期就存在了。它是系列控件的一部分，这些控件允许你使用模板显示数据（尤其是重复类型的数据）。模板允许你为数据创建更复杂的布局，并执行诸如 `GridView` 服务器控件的功能。

像 `DataList` 控件这样基于模板的控件需要你付出更多工作。例如，你必须为自己构建常用任务。你不能依赖于可能熟悉的其他数据控件（例如分页）。

### 查看可用模板

在使用像 `DataList` 控件这样基于模板的控件时，核心思想是组合特定的模板来创建你所需的布局。`DataList` 控件有许多可以用于构建显示内容的模板。可用的模板定义在下表中：

| 模板 | 说明 |
|---|---|
| `AlternatingItemTemplate` | 与 `ItemTemplate` 配合使用，为布局中的所有奇数行提供布局。当你想要网格或每行都通过某种方式进行区分（例如具有不同的背景颜色）的布局时，通常使用。 |
| `EditItemTemplate` | 允许定义行或项目在编辑时的外观和行为。 |
| `FooterTemplate` | 允许定义模板中的最后一个项目。如果未定义，则不使用页脚。 |
| `HeaderTemplate` | 允许定义模板中的第一个项目。如果未定义，则不使用页眉。 |
| `ItemTemplate` | 用于定义显示中每个项目对应的行或布局的核心模板。 |
| `SelectedItemTemplate` | 允许定义行或项目在被选中时的外观和行为。 |
| `SeparatorTemplate` | 显示中项目之间使用的任何分隔符的布局。 |

### 使用 ItemTemplate

尽管 `DataList` 控件有七个模板可以使用，但你至少也需要 `ItemTemplate`。这里的代码列表 8-18 向你展示了来自 Northwind 数据库的公司名称。

#### 代码列表 8-18：显示 Northwind 数据库中的公司名称

```
<% Page Language="VB" AutoEventWireup="false" CodeFile="DataListControl.aspx.vb"
Inherits="DataListControl" %>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>DataList Control</title>
</head>
<body>
<form id="form" runat="server">
<div>
<asp:DataList Id="DataList1" DataSource="SqlDataSource">
<ItemTemplate>
Company Name:
<asp:Label Id="CompanyName" runat="server"
Text='<%# Eval("CompanyName") %>' />
<br />
<br />
</ItemTemplate>
</asp:DataList>
<asp:SqlDataSource Id="SqlDataSource" runat="server"
ConnectionString="DSN=Northwind;"
SelectCommand="SELECT [CompanyName] FROM [Customers]">
</asp:SqlDataSource>
</div>
</form>
</body>
</html>
```

`DataList` 控件至少需要一个 `ItemTemplate` 元素，你可以在其中定义了从数据源中遇到的每个项目的页面布局。在这种情况下，所有数据都是通过 `SqlDataSource` 控件从 Northwind 数据库提取的。`SqlDataSource` 控件仅从 `Customers` 表中提取 `CompanyName` 列。从那里，Item 部分定义了两个项目。第一个是静态项目“Company Name”，后面跟着一个 ASP.NET 服务器控件 `Label`。第二个是标准 HTML 元素。`Label` 的 `Text` 属性使用内联绑定（如本书的前几个章节所示）来绑定来自 `SqlDataSource` 控件的值。如果 `SqlDataSource` 控件输出多个数据点，你仍然可以通过在 `Eval` 中指定来指定：

```
<asp:Label Id="CompanyName" runat="server"
Text='<%# Eval("CompanyName") %>'
```

使用代码列表 8-18 中的代码将得到图 8-5 所示的结果。

![](img/eb54f286-ad47-bf83-e2d4-4790.png)图8-5

如果你查看页面源代码，可以看到 `DataList` 控件默认使用表格布局元素。

```html
<table id="DataList1" cellspacing="0" border="0" style="border-collapse:collapse;">
<tr>
<td>Company Name:
<span id="DataList1_ct100">ItemTemplate</span>
<br />
<br />
</td>
</tr>
<tr>
<td>Company Name:
<span id="DataList1_ct101">AlternatingItemTemplate</span>
<br />
<br />
</td>
</tr>
<!-- 代码省略 -->
</table>
```

虽然这种表格布局是默认的，但你可以通过 `DataList` 控件的 `RepeatLayout` 属性将其更改为标签。如 19 所示，你需要重构 `DataList`。

#### 代码列表 8-19：使用 RepeatLayout 修改输出

```asp
<asp:DataList ID="DataList1" runat="server" DataSourceID="SqlDataSource" RepeatLayout="Flow">
  <ItemTemplate>
    CompanyName:
    <asp:Label ID="CompanyNameLabel" runat="server"
    Text="<%# Eval("CompanyName")" />
    <br />
    <br />
  </ItemTemplate>
</asp:DataList>
```

`RepeatLayout` 的可选选项是 `Table` 或 `Flow`。`Table` 是默认值。使用 `Flow` 设置查看页面源代码时的输出如下：

```html
<span id="DataList1">
<span>
  CompanyName:
  <span id="DataList1_ct100">ItemTemplate</span>
  <br />
  <br />
</span>
<span>
  CompanyName:
  <span id="DataList1_ct101">AlternatingItemTemplate</span>
  <br />
  <br />
</span>
<!-- 代码省略 -->
</span>
```

### 使用其他布局模板

你会发现其他模板的使用与 `ItemTemplate` 一样简单。代码列表 8-20 展示了如何向公司名称显示添加 `AlternatingTemplate` 和 `SeparatorTemplate`。

#### 代码列表 8-20：同时使用 AlternatingTemplate 和 SeparatorTemplate

```asp
<% Page Language="VB" AutoEventup="false" CodeFile="DataListControl.aspx.vb"
Inherits="DataListControl" %>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
  <title>DataList Control</title>
</head>
<body>
  <form id="form1" runat="server">
  <div>
    <asp:DataList ID="DataList1" runat="server" DataSourceID="SqlDataSource">
      <ItemTemplate>
        Company Name:
        <asp:Label Id="CompanyNameLabel" runat="server" Text='<%# Eval("CompanyName") %>' />
        <br />
        <br />
      </ItemTemplate>
      <AlternatingItemTemplate>
        CompanyName:
        <asp:Label Id="CompanyNameLabel" runat="server" BackColor="LightGray" Text='<%# Eval("CompanyName") %>' />
        <br />
        <br />
      </AlternatingItemTemplate>
      <SeparatorTemplate>
        <hr />
      </SeparatorTemplate>
      <asp:DataSource ID="SqlDataSource" runat="server" ConnectionString="DSN=Northwind;" SelectCommand="SELECT [CompanyName] FROM [Customers]" />
    </asp:DataList>
  </div>
  </form>
</body>
</html>
```

在此处，`AlternatingItemTemplate` 是 `ItemTemplate` 的重复，但 `Label` 控件的 `BackColor` 添加在项目内部。`Separator` 用于每个项目之间，无论是来自 `ItemTemplate` 还是 `AlternatingItemTemplate`。在这种情况下，使用简单的 `<hr />` 在每个项目之间画一条线。其输出如图 8-6 所示。

此过程允许你更改交替行中项目的定义方式，并在元素之间放置分隔符。如果你想要交替行或交替样式，使用 `<AlternatingTemplate>` 元素可能并不总是最佳方法，但你会发现使用 `<AlternatingStyle>` 元素更好。这种方法在代码列表 8-21 中所示。

#### 代码列表 8-21：使用项目模板

```asp
<asp:DataList ID="DataList1" runat="server" DataSourceID="SqlDataSource"
BackColor="White" BorderColor="#999999" BorderStyle="Solid" BorderWidth="1px"
CellPadding="3" ForeColor="Black" GridLines="Vertical"
FooterStyle BackColor="#CCCCCC" />
```

# 第 8 章：使用 ADO.NET 管理数据

```
<AlternatingStyle BackColor="#CCCCCC" />
<SelectedItem BackColor="#000099" Font-Bold="True" ForeColor="White" />
<HeaderStyle BackColor="Black" Font-Bold="True" ForeColor="White" />
<ItemTemplate>
Name:
<asp:Label ID="CompanyNameLabel" runat="server" 
Text='<%# (CompanyName)% />
<br />
<br />
</ItemTemplate>
</asp:DataList>
```

![](img/54f286ad4789bbf83e3e279dd_0.png) 你注意到每个可用模板都有关联的样式元素。图 7 显示了这些样式的使用。

![](img/54f286ad4789bbf83e3e279dd_1.png)

## 多列操作

基于模板的控件在显示多列项目时比 `GridView` 等控件更具优势。`RepeatColumns` 属性处理了这个问题。使用该属性的代码在列表 8-22 中显示。

# 第 8 章：使用 ADO.NET 管理数据

### 列表 8-2：使用 RepeatColumns 属性创建多列

```
<asp:DataList ID="DataList1" runat="server" DataSourceID="SqlDataSource"
CellPadding="2" RepeatColumns="3" RepeatDirection="Horizontal">
<ItemTemplate>
Company Name:
<asp:Label ID="CompanyNameLabel" runat="server"
Text="# Eval("CompanyName") %>
<br />
<br />
</ItemTemplate>
</asp:DataList>
```

在页面中运行此代码将产生图 8-8 所示的结果。![](img/54f286ad4789bbf83e3e279dd_0.png) `RepeatDirection` 属性控制 `DataList` 控件布局绑定到 Web 页面的项目。可能的值包括 `Vertical` 和 `Horizontal`。默认值为 `Vertical`。将其设置为 `Vertical`，会得到以下结果：

+   项目 1

项目 2

项目 3

项目 4

当 `RepeatDirection` 属性设置为 `Horizontal` 时，项目将以水平方式布局：

+   项目 1

项目 2

项目 3

项目 4

项目 5

项目 6

## ListView 控件

`ListView` 控件是最新的模板控件之一。这是在 .NET Framework 3.5 版本中才可用的控件。它被认为是 `DataList` 控件的更好替代方案。你会发现该控件提供了更多的布局控制，并且在 Visual Studio 中运行良好良好，因为它提供了一系列向导，可以使用常用选项设置布局。
