
随后启动对象关系设计器 (O/R 设计器)，以便你可以可视化编辑要使用的数据库和表。打开“服务器资源管理器”窗口，并连接到 pubs 示例数据库。将 publisher 和 title 表拖放到 DataClasses.dbml 的设计图面上（见图 17-5）。

![](img/a977a875c7c627b45d939729705a252e_572_0.png)

图 17-5

按 Ctrl+S 保存 DataClasses.dbml 文件。保存该文件时，Visual Studio 2008 会保存表示你刚添加的实体和数据库关系的 .NET 类。你每向解决方案添加一个 LINQ to SQL 设计器文件，就会生成一个自定义 DataContext 类。它是用于操作表的主要对象。本例中，DataContext 类名为 DataClassesDataContext。

继续操作前，请务必保存 DataClasses.dbml。

### 使用 GridView 控件进行数据绑定

要显示表中的记录，可以使用 GridView 控件，它会在一个表中显示数据源的值，其中每列表示一个字段，每行表示一条记录。从工具箱中将 GridView 控件拖放到 Default.aspx 的设计图面上。在 GridView 控件的智能标记中，在“选择数据源”下拉列表中选择 <新建数据源...>（见图 17-6）。

![](img/a977a875c7c627b45d939729705a252e_572_1.png)

图 17-6

## 第 II 部分：使用 C# 进行应用程序开发

在“数据源配置向导”（见图 17-7）中，选择 LINQ 并单击“确定”。使用默认名称 LinqDataSource1。单击“确定”。

![](img/a977a875c7c627b45d939729705a252e_573_0.png)

图 17-7

如果你熟悉 ASP.NET 2.0 中的各种数据源控件（如 SqlDataSource 和 ObjectDataSource），LinqDataSource 控件的工作方式与它们非常相似。LinqDataSource 控件的特别之处在于，它不像 SqlDataSource 那样直接绑定到数据库，而是绑定到启用 LINQ 的数据模型。其美妙之处在于，你无需编写各种复杂的 SQL 查询（如插入、删除和修改）即可使用它。相反，你只需指定要使用的数据模型以及要对其执行的操作类型（如删除、插入或更新），然后该控件会自行完成这些操作。

先前生成的 DataClassesDataContext 对象会自动为你选中（见图 17-8）。单击“下一步”。

![](img/a977a875c7c627b45d939729705a252e_573_1.png)

图 17-8

## 第 17 章：开发 ASP.NET Web 应用程序

选择 titles 表，并单击 * 复选框以选择所有字段（见图 17-9）。

![](img/a977a875c7c627b45d939729705a252e_574_0.png)

图 17-9

单击“高级”按钮并选中所有复选框。单击“确定”（见图 17-10），然后单击“完成”。

![](img/a977a875c7c627b45d939729705a252e_574_1.png)

图 17-10

## 第 II 部分：使用 C# 进行应用程序开发

切换到 Default.aspx 页面的源视图，并观察 <asp:LinqDataSource> 元素：

```
<asp:LinqDataSource
ID="LinqDataSource1"
runat="server"
ContextTypeName="DataClassesDataContext"
EnableDelete="True"
EnableInsert="True"
EnableUpdate="True"
TableName="titles">
</asp:LinqDataSource>
```

选择 GridView 控件的智能标记，并选中五个复选框（见图 17-11）。

![](img/a977a875c7c627b45d939729705a252e_575_0.png)

图 17-11

这会使 GridView 看起来如图 17-12 所示。现在列名可单击，并且包含“编辑”、“删除”和“选择”的新列已添加到 GridView 控件中。此外，分页现已启用（位于 GridView 控件底部）。

![](img/a977a875c7c627b45d939729705a252e_575_1.png)

图 17-12

## 第 17 章：开发 ASP.NET Web 应用程序

单击 GridView 控件智能标记中的“自动套用格式”链接，并选择“Sand and Sky”方案。

GridView 控件包含 titles 表的所有字段，但有些字段你并不真正需要。因此选择 notes 列，并通过从“GridView 任务”中选择“删除列”来移除它（见图 17-13）。同时删除 advance、royalty 和 ytd_sales 列。

![](img/a977a875c7c627b45d939729705a252e_576_0.png)

图 17-13

现在 GridView 控件应如图 17-14 所示。

![](img/a977a875c7c627b45d939729705a252e_576_1.png)

图 17-14

## 第 II 部分：使用 C# 进行应用程序开发

现在，要调试应用程序，请按 F5。系统会询问是否修改 Web.config 文件以进行调试；单击“确定”。系统还会提示 Internet Explorer 中已禁用脚本调试；单击“是”继续调试。

图 17-15 显示 GridView 控件显示了 titles 表中的行。你可以通过单击列标题对行排序，并编辑和删除记录。

![](img/a977a875c7c627b45d939729705a252e_577_0.png)

图 17-15

### 显示出版商名称

如图 17-15 所示，出版商 ID 显示在 GridView 控件中的 pub_id 字段下。如果显示出版商名称而不是其 ID，对用户会更有帮助。为此，请切换到 Default.aspx 的源视图，并在 <asp:GridView> 元素内，将以下元素：

```
<asp:BoundField
DataField="pub_id"
HeaderText="pub_id"
SortExpression="pub_id" />
```

替换为：

```
<asp:TemplateField
HeaderText="Publisher">
<ItemTemplate>
<%#Eval("publisher.pub_name")%>
</ItemTemplate>
</asp:TemplateField>
```

实质上，这会将 GridView 中出版商列的标题改为 Publisher，并且值现在取自 DataClassesDataContext 类的 publisher.pub_name 属性。

## 第 17 章：开发 ASP.NET Web 应用程序

再次按 F5 调试应用程序，以查看出版商名称而不是出版商 ID（见图 17-16）。

![](img/a977a875c7c627b45d939729705a252e_578_0.png)

图 17-16

### 显示所选出版商的标题

到目前为止，titles 表中的所有标题都显示在 GridView 控件中。你可能希望将显示的标题限制为某个选定的出版商。为此，通过添加以下突出显示的代码，向 Default.aspx 页面插入另一个 LinqDataSource 控件：

```
<asp:LinqDataSource
    ID="LinqDataSource1"
    runat="server"
    ContextTypeName="DataClassesDataContext"
    EnableDelete="True"
    EnableInsert="True"
    EnableUpdate="True"
    TableName="titles">
</asp:LinqDataSource>
```

```
<asp:LinqDataSource
    ID="LinqDataSource2"
    runat="server"
    ContextTypeName="DataClassesDataContext"
    OrderBy="pub_name"
    Select="new (pub_name, pub_id)"
    TableName="publishers">
</asp:LinqDataSource>
```

## 第 II 部分：使用 C# 进行应用程序开发

注意第二个 LinqDataSource 控件具有 Select 属性，你可以在其中指定要检索的字段名称（本例中为 pub_name 和 pub_id）。

通过添加以下突出显示的代码，在页面顶部添加一个 DropDownList 控件：

```
<body>
    <form id="form1" runat="server">
        <div>
            Display titles by publisher:
            <asp:DropDownList
                ID="DropDownList1"
                runat="server"
                DataSourceID="LinqDataSource2"
                DataTextField="pub_name"
                DataValueField="pub_id"
                AutoPostBack="True">
            </asp:DropDownList>
        </div>
        <asp:GridView ID="GridView1" runat="server"
        ...
```

此添加会将 DropDownList 控件绑定到 LinqDataSource 控件。DropDownList 控件将显示出版商名称列表（pub_name），并且每个出版商名称以 pub_id 作为其值。

现在 Default.aspx 在设计视图中应如图 17-17 所示。你将看到文本“按出版商显示标题：”以及一个下拉列表控件。

![](img/a977a875c7c627b45d939729705a252e_579_0.png)

图 17-17

要配置第一个 LinqDataSource 控件，使 GridView 控件只显示来自所选出版商的标题，请单击 GridView 控件的智能标记，然后单击“配置数据源”链接（见图 17-18）。

![](img/a977a875c7c627b45d939729705a252e_579_1.png)

图 17-18
