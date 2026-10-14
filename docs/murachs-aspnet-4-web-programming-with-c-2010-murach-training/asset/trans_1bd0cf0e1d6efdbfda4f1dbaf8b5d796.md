

# 为提供公共属性的主页提供代码隐藏文件

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;

public partial class Site : System.Web.UI.MasterPage
{
    public Label MessageLabel
    {
        get { return lblMessage; }
        set { lblMessage = value; }
    }

    protected void Page_Load(object sender, EventArgs e)
    {
        if (lblMessage.Text == "")
        {
            int daysUntil = DaysUntilHalloween();
            if (daysUntil == 0)
                lblMessage.Text = "Happy Halloween!";
            else if (daysUntil == 1)
                lblMessage.Text = "Tomorrow is Halloween!";
            else
                lblMessage.Text = "There are only " + daysUntil
                    + " days left until Halloween!";
        }
    }

    private int DaysUntilHalloween()
    {
        DateTime halloween = new DateTime(DateTime.Today.Year, 10, 31);
        if (DateTime.Today > halloween)
            halloween = halloween.AddYears(1);
        TimeSpan ts = halloween - DateTime.Today;
        return ts.Days;
    }
}
```

## Description

- 如果在母版页中将控件公开为公共属性，则内容页可以访问母版页中的控件。为此，您需要编写一个具有 get 和 set 访问器的属性。

# 如何从内容页访问母版页的公共属性

图 9-11 显示了如何从内容页访问母版页中的公共属性。如该图上半部分所示，您可以在内容页的 aspx 文件中使用 MasterType 指令来指定用于母版页的类型名称。此指令中指定的值指定了内容页的 Master 属性返回的对象的类型。因此，在此示例中，Master 属性将返回类型为 Site 的对象。如果查看前一图中的类声明，您会看到 Site 是定义母版页的类的名称。

该图第二部分显示了 Order.aspx 内容页代码隐藏文件中的两个方法。如您所见，Page_Load 方法调用了名为 DisplayCartMessage 的方法。此方法确定购物车中当前项目的数量，并相应地设置母版页 MessageLabel 属性公开的标签的 Text 属性。但请注意，如果购物车为空，则不会为消息标签分配任何值。在这种情况下，母版页的 Page_Load 方法将把标签设置为距离万圣节剩余的天数。

尽管在内容页的 aspx 文件中使用 MasterType 指令可以更轻松地访问母版页的属性，但您应该意识到此指令不是必需的。如果您不指定 MasterType 指令，Master 属性将返回类型为 Master 的对象。然后，您可以将此对象强制转换为母版页的实际类型以访问您创建的任何属性。

例如，您可以使用如下代码为 MessageLabel 属性分配文本：

```
MasterPage mp = (Site) this.Master;
if (cart.Count == 1)
    mp.MessageLabel.Text =
        "There is one item in your cart.";
else if (cart.Count > 1)
    mp.MessageLabel.Text =
        "There are " + cart.Count + " items in your cart.";
```

在这里，Master 对象被强制转换为 Site 对象，以便可以访问其 MessageLabel 属性。MasterType 指令的目的是避免这种笨拙的强制转换。

# Order.aspx 页的一部分

```aspx
<%@ Page Language="C#" MasterPageFile="~/Site.master"
    AutoEventWireup="true" CodeFile="Order.aspx.cs" Inherits="Order" %>

<%@ MasterType TypeName="Site" %>

<asp:Content ID="Content1" ContentPlaceHolderID="MainContent"
    runat="server">
    .
    .
    .
</asp:Content>
```

# Order.aspx 页代码隐藏文件中的两个方法

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    if (!IsPostBack)
    {
        ddlProducts.DataBind();
        this.DisplayCartMessage();
    }
    selectedProduct = this.GetSelectedProduct();
    lblName.Text = selectedProduct.Name;
    lblShortDescription.Text = selectedProduct.ShortDescription;
    lblLongDescription.Text = selectedProduct.LongDescription;
    lblUnitPrice.Text = selectedProduct.UnitPrice.ToString("c");
    imgProduct.ImageUrl = "Images/Products/" + selectedProduct.ImageFile;
}

private void DisplayCartMessage()
{
    CartItemList cart = CartItemList.GetCart();
    if (cart != null)
    {
        if (cart.Count == 1)
            this.Master.MessageLabel.Text
                = "There is one item in your cart.";
        else if (cart.Count > 1)
            this.Master.MessageLabel.Text
                = "There are " + cart.Count + " items in your cart.";
    }
}
```

## Description

- aspx 文件中的 MasterType 指令指定母版页类型的名称。如果您在内容页中包含此指令，则可以在代码隐藏文件中使用 Master 属性来访问母版页的公开属性。

Figure 9-11    如何从内容页访问母版页的公共属性

# Perspective

我希望本章已经说明了母版页的强大功能。事实上，我建议您对除最简单的应用程序之外的所有应用程序都使用母版页，即使您一开始在母版页中只有占位符。然后，当您准备为内容页提供专业外观时，您可以增强母版页，这也将增强您所有的内容页。

另一种选择是将常规内容页转换为稍后开发的母版页。但正如图 9-6 所示，这是一个耗时且容易出错的过程。提前规划要好得多。

# Terms

- master page
- content page
- content placeholder
- nested master pages
- parent master page
- child master page

# Exercise 9-1 — 为 Reservation 应用程序创建母版页

在此应用程序中，您将首先为 Reservation 应用程序创建一个简单的母版页。然后，您将添加两个使用母版页的内容页，并将两个现有页转换为内容页。

## Create the master page

- 1. 在 C:\aspnet4_cs 目录中打开 Ch09Reservation 应用程序。
- 2. 使用图 9-2 中的技术向项目添加一个名为 Site.master 的母版页。查看此页的 aspx 代码。特别是，注意 head 和 body 部分中的内容占位符。
- 3. 切换到设计视图，注意 body 部分中的内容占位符是如何显示的。
- 4. 在源视图中显示 Request 页面，并将页面顶部的 h1 和 h2 元素复制到剪贴板。然后，切换回母版页并将这些元素粘贴到 div 元素内但在内容占位符之前。注意 h1 和 h2 元素没有像在 Request 页面上那样格式化。
- 5. 在源视图中显示母版页，并为 div 元素添加 id 属性，其值为“page”。然后，将 Main.css 样式表附加到此页。现在，元素应该正确格式化。
- 6. 在 h1 和 h2 元素下方添加一个 ID 为“links”的 p 元素。然后，在此段落中添加三个超链接。将这些链接的内容设置为“Home”、“Reservation”和“About”，并为每个超链接添加 CssClass 属性，其值为“hyperlink”。此外，将预订链接的 NavigateUrl 属性设置为 Request.aspx，但不要为其他链接设置此属性，因为页面尚不存在。
- 7. 在设计视图中显示母版页以查看其外观。注意第一个和第三个链接未显示为链接，因为它们的 NavigateUrl 属性未设置。保存母版页。

## Create two new content pages

- 8. 使用图 9-6 的第一种技术创建一个名为 Home.aspx 的新内容页。注意添加到页面中并引用母版页中的内容占位符的两个 Content 控件。
- 9. 切换到设计视图，注意母版页上的元素已显示但呈灰色，因此您无法更改它们。
- 10. 单击 Content 控件并键入“主页正在开发中。”
- 11. 将主页设为起始页，然后运行应用程序以查看此页的外观。

