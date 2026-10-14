

## DataPager 控件的属性

| 属性 | 说明 |
|---|---|
| ID | 控件的 ID。 |
| runat | 必须指定为 "server"。 |
| PageSize | 指定每个页面上要显示的项目数。默认值为 10。 |
| PagedControlID | 为其提供分页的 ListView 控件的 ID。仅当 DataPager 控件放置在 ListView 控件外部时使用。 |

## NextPreviousPagerField 元素的属性

| 属性 | 说明 |
|---|---|
| ButtonType | 要使用的按钮类型。可以指定 Button、Image 或 Link。 |
| ShowFirstPageButton | 确定是否显示第一页按钮。默认值为 False。 |
| ShowPreviousPageButton | 确定是否显示上一页按钮。默认值为 True。 |
| ShowNextPageButton | 确定是否显示下一页按钮。默认值为 True。 |
| ShowLastPageButton | 确定是否显示最后一页按钮。默认值为 False。 |

## NumericPagerField 元素的属性

| 属性 | 说明 |
|---|---|
| ButtonCount | 要显示的最大按钮数。 |
| ButtonType | 要使用的按钮类型。可以指定 Button、Image 或 Link。 |

## 使用两种分页器的 DataPager 控件的 Aspx 代码

```
<asp:DataPager ID="DataPager1" runat="server" PageSize="4">
    <Fields>
        <asp:NextPreviousPagerField ButtonType="Button"
            ShowFirstPageButton="True" ShowNextPageButton="False"
            ShowPreviousPageButton="False" />
        <asp:NumericPagerField ButtonCount="3" />
        <asp:NextPreviousPagerField ButtonType="Button"
            ShowLastPageButton="True" ShowNextPageButton="False"
            ShowPreviousPageButton="False" />
    </Fields>
</asp:DataPager>
```

## 生成的 DataPager 控件

![](img/c024ccf88e28c30c07dd410d4342288f_556_0.png)

## 描述

- 你可以使用 DataPager 控件的 PageSize 属性来指定每个页面上要显示的项目数。
- 你可以将 DataPager 控件放置在 ListView 控件之外。然后，你必须将 DataPager 控件的 PagedControlID 属性设置为要与其一起使用的 ListView 控件的 ID。
- NextPreviousPagerField 和 NumericPagerField 元素还具有属性，可让你更改显示的按钮的文本或图像。

## 使用 ListView 控件的列表应用程序

现在你已经学习了使用 ListView 控件的基本技能，以下主题介绍了使用此控件显示产品列表的应用程序的设计和代码。如果你将此应用程序与第 14 章中使用 GridView 控件的列表应用程序进行比较，你将开始看到 ListView 控件提供的灵活性。

## 产品列表应用程序

图 16-8 展示了产品列表应用程序。在这里，你可以看到 ListView 控件中的第一列包含 Halloween 数据库中 Products 表中每一行的产品名称。然后，第二列包含列表中包含的其他产品列的标题，第三列包含每个产品列的数据。这种类型的布局对于 GridView 控件来说是不可能的。

你还应该注意到与 ListView 控件一起使用的 DataPager 控件。此控件指定每个页面上应显示四个产品。它使用具有按钮上显示的文本自定义值的 next/previous 分页器实现。

## 产品列表应用程序

![](img/c024ccf88e28c30c07dd410d4342288f_558_0.png)

## 描述

- ProductList 应用程序使用 ListView 控件显示 Products 表中的所有产品。ListView 控件绑定到以 DataSet 模式工作的 SqlDataSource 控件。
- ListView 控件使用 Item 和 AlternatingItem 模板以不同的背景色显示每隔一行。
- ListView 控件内使用 DataPager 控件在每个页面上显示四个产品。

## aspx 文件

图 16-9 展示了产品列表应用程序的 aspx 代码。为了生成此应用程序使用的 ListView 控件的起始代码，我从 Configure ListView 对话框中选择了 flow layout。与使用 grid layout 生成的代码不同，flow layout 的代码不使用表格。这使得使用 CSS 应用样式变得容易。

此列表的第一页显示了 ListView 控件的 Layout 模板。此模板中的两个分区是默认生成的。第一个分区用作项目占位符的容器。在这种情况下，项目占位符在 span 元素内编码。

第二个分区包含 ListView 控件使用的 DataPager 控件。默认情况下，此分区使用 style 属性生成，但我删除了该属性并改为包含 id 属性。这样，我就能使用 CSS 格式化数据分页器。

如你所见，我将 DataPager 控件的 PageSize 属性设置为 4。然后，我使用 NextPreviousPagerField 元素来实现该控件。在这里，我设置了该元素的 FirstPageText、PreviousPageText、NextPageText 和 LastPageText 属性，以便按钮显示如前图所示的小于号和大于号。

我对此模板所做的唯一其他更改是在两个分区之前添加了一个段落。此段落包含在 ListView 控件顶部显示的文字。与包含 DataPager 控件的分区一样，我为此段落包含了一个 id 属性，以便我可以用 CSS 格式化它。

此列表的第二页显示了控件的 Item 模板。我对为此模板生成的 aspx 代码做了相当大的更改，以格式化数据，使其看起来如前图所示。要理解此代码的工作原理，你需要意识到显示产品名称的标签使用 CSS 浮动到剩余产品信息左侧。同样，标识每个剩余产品列的文字使用 CSS 浮动到显示列值的标签左侧。

此列表的第三页显示了 ListView 控件的 AlternatingItem 模板。此代码与 Item 模板的代码相同，只是我为此模板的主分区提供了 id 属性的不同值。这样，我就能为交替行分配不同的背景颜色。

SqlDataSource 控件也在此列表的第三页显示。请注意，这里数据源从 Products 和 Categories 表中检索数据。包含 Categories 表是为了可以显示 LongName 列而不是 Products 表中的 CategoryID 列。

## Default.aspx 文件

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Chapter 16: Product List</title>
    <link href="Main.css" rel="stylesheet" type="text/css" />
</head>
<body>
    <form id="form1" runat="server">
        <div id="page">
            <div id="header">
                <asp:Image ID="Image1" runat="server" ImageUrl="~/Images/banner.jpg" />
            </div>
            <div id="main">
                <asp:ListView ID="ListView1" runat="server" DataKeyNames="ProductID" DataSourceID="SqlDataSource1">
                    <LayoutTemplate>
                        <p id="product">Product</p>
                        <div ID="itemPlaceholderContainer" runat="server">
                            <span runat="server" id="itemPlaceholder" />
                        </div>
                        <div id="pager">
                            <asp:DataPager ID="DataPager1" runat="server" PageSize="4">
                                <Fields>
                                    <asp:NextPreviousPagerField ButtonType="Button" ShowFirstPageButton="True" ShowLastPageButton="True" FirstPageText="&lt;&lt;" PreviousPageText="&lt;" NextPageText="&gt;" LastPageText="&gt;&gt;" />
                                </Fields>
                            </asp:DataPager>
                        </div>
                    </LayoutTemplate>
                </asp:ListView>
            </div>
        </div>
    </form>
</body>
</html>
```

