

## Default.aspx 文件

```
<ItemTemplate>
    <div id="itemtemplate">
        <p class="name">
            <asp:Label ID="NameLabel" runat="server" Text='<%# Eval("Name") %>' />
        </p>
        <div class="info">
            <p class="label">Category:</p>
            <p class="control">
                <asp:Label ID="CategoryLabel" runat="server" Text='<%# Eval("Category") %>' />
            </p>
            <p class="label">Short Description:</p>
            <p class="control">
                <asp:Label ID="ShortDescriptionLabel" runat="server" Text='<%# Eval("ShortDescription") %>' />
            </p>
            <p class="label">Long Description:</p>
            <p class="control">
                <asp:Label ID="LongDescriptionLabel" runat="server" Text='<%# Eval("LongDescription") %>' />
            </p>
            <p class="label">Unit Price:</p>
            <p class="control">
                <asp:Label ID="UnitPriceLabel" runat="server" Text='<%# Eval("UnitPrice", "{0:c}") %>' />
            </p>
            <p class="label">On Hand:</p>
            <p class="control">
                <asp:Label ID="OnHandLabel" runat="server" Text='<%# Eval("OnHand") %>' />
            </p>
        </div>
    </div>
</ItemTemplate>
<AlternatingItemTemplate>
    <div id="alternatetemplate">
        <p class="name">
            <asp:Label ID="NameLabel" runat="server" Text='<%# Eval("Name") %>' />
        </p>
        <div class="info">
            <p class="label">Category:</p>
            <p class="control">
                <asp:Label ID="CategoryLabel" runat="server" Text='<%# Eval("Category") %>' />
            </p>
            <p class="label">Short Description:</p>
            <p class="control">
                <asp:Label ID="ShortDescriptionLabel" runat="server" Text='<%# Eval("ShortDescription") %>' />
            </p>
            <p class="label">Long Description:</p>
            <p class="control">
                <asp:Label ID="LongDescriptionLabel" runat="server" Text='<%# Eval("LongDescription") %>' />
            </p>
            <p class="label">Unit Price:</p>
            <p class="control">
                <asp:Label ID="UnitPriceLabel" runat="server" Text='<%# Eval("UnitPrice", "{0:c}") %>' />
            </p>
            <p class="label">On Hand:</p>
            <p class="control">
                <asp:Label ID="OnHandLabel" runat="server" Text='<%# Eval("OnHand") %>' />
            </p>
        </div>
    </div>
</AlternatingItemTemplate>
</asp:ListView>
<asp:SqlDataSource ID="SqlDataSource1" runat="server" ConnectionString="<%# ConnectionStrings:HalloweenConnectionString %>" SelectCommand="SELECT Products.ProductID, Products.Name, Categories.LongName AS Category, Products.ShortDescription, Products.LongDescription, Products.UnitPrice, Products.OnHand FROM Products INNER JOIN Categories ON Products.CategoryID = Categories.CategoryID ORDER BY Products.Name">
</asp:SqlDataSource>
</div>
</div>
</form>
</body>
</html>
```

## 如何对 ListView 数据进行分组

ListView 控件最激动人心的功能之一，是它能够对数据进行分组，从而以两列或更多列的形式显示数据。在接下来的主题中，你将学习分组数据的基本技巧，并看到一个使用分组的简单应用程序。

### 如何定义分组的模板

图 16-10 展示了如何为使用分组的 ListView 控件定义模板。这里假设你最初是从生成表格的布局（如网格布局）开始创建 ListView 控件的。如果是从不生成表格的布局开始创建，具体步骤会有所不同。

首先，将 Layout 模板中内部表格的 ID 属性改为 `groupPlaceholderContainer`，并将该表格内行的 ID 属性改为 `groupPlaceholder`。你也可以通过将 ListView 控件的 `GroupPlaceholderID` 属性设置为其他值，来为组占位符的 ID 属性指定不同的值。

接下来，向控件添加一个 Group 模板。大多数情况下，该模板包含一行，其 ID 属性设置为 `itemPlaceholderContainer`。然后，可以将该行中单个单元格的 ID 属性设置为 `itemPlaceholder`。应用程序运行时，Item 模板会替换项占位符，Group 模板会替换组占位符。

最后，将 ListView 控件的 `GroupItemCount` 属性设置为每个组中要包含的项目数量。在本示例中，我将该属性设置为 2，结果如图顶部所示。请注意，虽然图中未显示 ListView 控件的 Item 模板，但通过查看控件中每个产品的数据，你应该能推断出 Item 模板的基本内容。如果仍然难以理解其工作原理，在看完下一个完整的应用程序示例后，应该会清楚许多。

尽管可以按照我刚才描述的方式修改 ListView 控件以使用分组，但你可能会发现，先为分组生成基本代码，再修改代码以自定义显示效果会更加简便。为此，你可以从“配置 ListView”对话框中选择“平铺布局”。随后，ListView 控件会自动配置 Layout 和 Group 模板，如图中所示。此外，控件的 `GroupItemCount` 属性会被设置为 3，Item 模板也会被格式化，使其显示效果与图顶部的 ListView 控件一致。

### 使用分组的产品列表应用程序

为了演示如何使用分组功能，图 16-11 展示了一个使用分组的产品列表应用程序。可以看到，该应用程序显示每个产品的名称和图片，产品以三列形式展示。虽然这是一个简单的应用程序，但它有助于你理解分组功能的实用价值。

### 分组的产品列表应用程序的 aspx 文件

图 16-12 展示了分组产品列表应用程序的代码。首先需要注意，ListView 控件的 `GroupItemCount` 属性设置为 3，这使得数据源中的三个项目显示在 ListView 控件的每一行中。

第二点需要注意的是，Layout 模板中包含一个作为组占位符的表格行。该占位符将被 Group 模板替换，你可以在本清单第一页底部看到这个 Group 模板。而 Group 模板又包含一个单行的表格单元格，作为项占位符。

本清单第二页显示了 ListView 控件的 Item 模板。请注意，由于 Group 模板中的项占位符是表格单元格，Item 模板也需以表格单元格开头。然后，在该单元格内编写两个段落。第一段包含一个标签，绑定到数据源的 Name 列；第二段包含一个图像，绑定到数据源的 ImageFile 列。注意，用于图像的绑定表达式包含图像文件的路径。这是必要的，因为 ImageFile 列仅包含文件名，不包含路径。

本清单第二页还显示了 ListView 控件绑定的 SqlDataSource 控件。该数据源简单地从 Products 表检索 Name 和 ImageFile 列，并按 Name 列对返回的行进行排序。

### Default.aspx 文件

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Chapter 16: Grouped Product List</title>
    <link href="Main.css" rel="stylesheet" type="text/css" />
</head>
<body>
    <form id="form1" runat="server">
        <div id="page">
            <div id="header">
                <asp:Image ID="Image1" runat="server" ImageUrl="~/Images/banner.jpg" />
            </div>
            <div id="main">
                <asp:ListView ID="ListView1" runat="server" DataSourceID="SqlDataSource1" GroupItemCount="3">
                    <LayoutTemplate>
                        <table runat="server">
                            <tr runat="server">
                                <td runat="server">
                                    <table ID="groupPlaceholderContainer" runat="server" border="0">
                                        <tr ID="groupPlaceholder" runat="server">
                                        </tr>
                                    </table>
                                </td>
                            </tr>
                            <tr runat="server">
                                <td runat="server" align="center">
                                    <asp:DataPager ID="DataPager1" runat="server" PageSize="6">
                                        <Fields>
                                            <asp:NumericPagerField />
                                        </Fields>
                                    </asp:DataPager>
                                </td>
                            </tr>
                        </table>
                    </LayoutTemplate>
                    <GroupTemplate>
                        <tr ID="itemPlaceholderContainer" runat="server">
                            <td ID="itemPlaceholder" runat="server">
                            </td>
                        </tr>
                    </GroupTemplate>
                </asp:ListView>
            </div>
        </div>
    </form>
</body>
</html>
```

