

## 使用 GridView 控件的列表应用程序

现在你已经学习了使用 GridView 控件的基础知识，下面这些主题将介绍一个使用 GridView 控件列出数据源行的应用程序的设计和代码。正如你将看到的，该应用程序提供了排序和分页功能，并且不需要一行 C# 代码。

## 产品列表应用程序

图 14-7 展示了产品列表应用程序。在这里，Halloweene 数据库的 Products 表中的数据在 GridView 控件中显示。数据每次显示 8 行，并在 GridView 控件底部显示数字分页按钮，以便用户在页面之间导航。此外，用户可以通过单击 ID、Name 和 Category 列的列标题对数据进行排序。

![](img/c024ccf88e28c30c07dd410d4342288f_476_0.png)

### 描述

- 产品列表应用程序使用 GridView 控件显示 Products 表中所有产品的列表。GridView 控件绑定到以 DataSet 模式工作的 SqlDataSource 控件。
- 前三列启用了排序。这样，用户就可以按 ID、Name 或 Category 对产品数据进行排序。
- 启用了分页，每页显示 8 个产品。
- 对 Unit Price 列应用了货币格式。

## aspx 文件

图 14-8 显示了此应用程序的 aspx 代码，该代码存储在 Default.aspx 文件中。由于不需要代码隐藏方法，因此未显示代码隐藏文件。

由于你已经熟悉了 aspx 文件中的所有代码，因此应该能够轻松地理解它。所以我只指出几个重点。

Columns 元素包含五个 BoundField 子元素，用于定义网格显示的字段。这五个列都从 SQL 数据源检索。前三个 BoundField 元素包含 SortExpression 属性以允许排序。第四个 BoundField 元素包含 DataFormatString 属性以应用货币格式。前两个字段的 ItemStyle 元素设置了字段的宽度，最后两个字段的 ItemStyle 元素将对齐方式设置为右对齐。否则，五個字段使用默认格式。

PagerStyle 元素用于将分页按钮居中显示在分页区域中。然后，PagerSettings 元素用于指定要显示的分页控件类型。

最后，SqlDataSource 控件使用以下 Select 语句从 Halloween 数据库检索数据：

```
SELECT [ProductID], [Name], [CategoryID],
    [UnitPrice], [OnHand] FROM [Products]
```

由于未设置 DataSourceMode 属性，因此使用默认的 DataSet 模式，这意味着可以启用排序和分页。

## Default.aspx 文件

```
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Chapter 14: Product List</title>
    <link href="Main.css" rel="stylesheet" type="text/css" />
</head>
<body>
    <form id="form1" runat="server">
        <div id="page">
            <div id="header">
                <asp:Image ID="Image1" runat="server"
                    ImageUrl="~/Images/banner.jpg" />
            </div>
            <div id="main">
                <asp:GridView ID="GridView1" runat="server"
                    AutoGenerateColumns="False" DataKeyNames="ProductID"
                    DataSourceID="SqlDataSource1" AllowPaging="True" PageSize="8"
                    AllowSorting="True" CellPadding="4" ForeColor="Black"
                    GridLines="None">
                    <Columns>
                        <asp:BoundField DataField="ProductID" HeaderText="ID"
                            ReadOnly="True" SortExpression="ProductID">
                            <HeaderStyle HorizontalAlign="Left" />
                            <ItemStyle Width="75px" />
                        </asp:BoundField>
                        <asp:BoundField DataField="Name" HeaderText="Name"
                            SortExpression="Name">
                            <HeaderStyle HorizontalAlign="Left" />
                            <ItemStyle Width="200px" />
                        </asp:BoundField>
                        <asp:BoundField DataField="CategoryID" HeaderText="Category"
                            SortExpression="CategoryID, Name" />
                        <asp:BoundField DataField="UnitPrice"
                            HeaderText="Unit Price" DataFormatString="{0:c}">
                            <ItemStyle HorizontalAlign="Right" />
                        </asp:BoundField>
                        <asp:BoundField DataField="OnHand" HeaderText="On Hand">
                            <ItemStyle HorizontalAlign="Right" />
                        </asp:BoundField>
                    </Columns>
                    <HeaderStyle BackColor="Gray" Font-Bold="True"
                        ForeColor="White" />
                    <RowStyle BackColor="White" ForeColor="Black" />
                    <AlternatingRowStyle BackColor="LightGray" ForeColor="Black" />
                    <PagerStyle BackColor="Gray" ForeColor="Blue"
                        HorizontalAlign="Center" />
                    <PagerSettings Mode="NumericFirstLast" />
                </asp:GridView>
                <asp:SqlDataSource ID="SqlDataSource1" runat="server"
                    ConnectionString="<%$ ConnectionStrings:HalloweenConnectionString %>"
                    SelectCommand="SELECT [ProductID], [Name], [CategoryID],
                        [UnitPrice], [OnHand] FROM [Products]">
                </asp:SqlDataSource>
            </div>
        </div>
    </form>
</body>
</html>
```

## 如何更新 GridView 数据

GridView 控件的另一个令人印象深刻的功能是它能够用很少的额外代码更新底层数据源中的数据。不过，在设置之前，你必须先使用上一章中描述的 Update、Delete 和 Insert 语句配置数据源。完成此操作后，你可以设置 GridView 控件以调用 Update 和 Delete 语句，你将在下一部分学习如何操作。然后，你将学习如何向 GridView 控件中插入一行。

## 如何使用命令字段

命令字段是包含一个或多个命令按钮的 GridView 列。图 14-9 显示了可在 GridView 控件的每一行中包含的五个命令按钮。请注意，Update 和 Cancel 按钮仅在用户单击 Edit 按钮编辑一行时显示。你不能在单独的命令字段中显示这些按钮。

当用户单击 Delete 按钮时，GridView 控件调用数据源控件的 Delete 方法，该方法从底层数据库中删除所选行。然后，GridView 控件重新显示数据，不包含已删除的行。

当用户单击 Edit 按钮时，GridView 控件将所选行置于编辑模式。在此模式下，用于显示可编辑绑定字段的标签被文本框替换，以便用户可以输入更改。此外，该行使用 EditRowStyle 元素提供的样式属性进行格式化。最后，Edit 按钮本身被 Update 和 Cancel 按钮替换。然后，如果用户单击 Update 按钮，GridView 控件将调用数据源控件的 Update 方法，该方法更新底层数据库。但如果用户单击 Cancel，则用户所做的任何更改都将被丢弃并重新显示原始值。

Select 按钮允许用户选择一行。然后，所选行将使用 SelectedRowStyle 元素中的设置显示。此外，SelectedIndex 和 SelectedRow 属性会更新以反映所选行。Select 按钮最常与 FormView 或 DetailsView 控件结合使用，以创建显示从 GridView 控件中选择的项目的详细信息的页面。你将在第 15 章学习其工作原理。

该图中的两个表格显示了 CommandField 元素的属性。例如，你可以将 ShowEditButton 属性设置为 True 以在命令字段中显示 Edit 按钮。你还可以使用 EditText 属性设置该按钮上显示的文本。

尽管单个命令字段可以显示多个按钮，但通常会为 Select、Edit 和 Delete 按钮创建单独的命令字段。还通常将 Select 和 Delete 按钮的 CausesValidation 属性设置为 False，因为这些按钮执行的操作不需要任何数据验证。另一方面，你通常会将 Edit 按钮的 CausesValidation 属性保留为 True，以便在用户单击 Update 按钮时执行验证。本章后面，你将通过创建模板字段学习如何使用验证控件与 Edit 按钮。

