
```
<%@ Page Language="C#" MasterPageFile="~/Site.master" AutoEventWireup="true" CodeFile="Order.aspx.cs" Inherits="Order" %>

<asp:Content ID="HeaderContent" ContentPlaceHolderID="HeadContent" runat="server">
    <link href="Styles/Order.css" rel="stylesheet" type="text/css" />
</asp:Content>

<asp:Content ID="PageContent" ContentPlaceHolderID="MainContent" runat="server">
    <p id="products">
        <asp:Label ID="Label1" runat="server" Text="Please select a product:"></asp:Label>&nbsp;
        <asp:DropDownList ID="ddlProducts" runat="server" AutoPostBack="True" DataSourceID="AccessDataSource1" DataTextField="Name" DataValueField="ProductID">
        </asp:DropDownList>
    </p>
    <asp:AccessDataSource ID="AccessDataSource1" runat="server" DataFile="~/App_Data/Halloween.mdb" SelectCommand="SELECT [ProductID], [Name], [ShortDescription], [LongDescription], [ImageFile], [UnitPrice] FROM [Products] ORDER BY [Name]">
    </asp:AccessDataSource>
    <asp:Image ID="imgProduct" runat="server" Width="135px" />
    <div id="product">
        <p id="name"><asp:Label ID="lblName" runat="server"></asp:Label></p>
        <p id="shortdesc">
            <asp:Label ID="lblShortDescription" runat="server"></asp:Label>
        </p>
        <p id="longdesc">
            <asp:Label ID="lblLongDescription" runat="server"></asp:Label>
        </p>
        <p id="unitprice">
            <asp:Label ID="lblUnitPrice" runat="server"></asp:Label>&nbsp;
            <asp:Label ID="Label2" runat="server" Text="each"></asp:Label>
        </p>
    </div>
    <div id="order">
        <p id="quantity">
            <asp:Label ID="Label3" runat="server" Text="Quantity:"></asp:Label>&nbsp;
            <asp:TextBox ID="txtQuantity" runat="server"></asp:TextBox>
            <asp:RequiredFieldValidator ID="RequiredFieldValidator1" runat="server" CssClass="validator" ControlToValidate="txtQuantity" Display="Dynamic" ErrorMessage="Quantity is a required field.">
            </asp:RequiredFieldValidator>
            <asp:RangeValidator ID="RangeValidator1" runat="server" CssClass="validator" ControlToValidate="txtQuantity" Display="Dynamic" ErrorMessage="Quantity must range from 1 to 500." MaximumValue="500" MinimumValue="1" Type="Integer">
            </asp:RangeValidator>
        </p>
        <asp:Button ID="btnAdd" runat="server" Text="Add to Cart" OnClick="btnAdd_Click" />
        <asp:Button ID="btnCart" runat="server" Text="Go to Cart" PostBackUrl="~/Cart.aspx" CausesValidation="False" />
    </div>
</asp:Content>
```

图 9-8 Order 内容页的 `aspx` 代码

## 如何嵌套母版页

除了从母版页创建内容页之外，你还可以创建其他母版页。当你像这样嵌套母版页时，可以创建一个 *父母版页*，其中包含网站所有页面使用的元素。然后，可以创建 *子母版页*，它们在父母版页的内容基础上添加内容，并包含网站不同部分页面使用的元素。

## 如何创建嵌套母版页

要创建嵌套在另一个母版页中的母版页，可使用与图 9-2 中创建任何母版页类似的技术。但是，在选择 Master Page 模板并输入页面名称后，你需要勾选 Select Master Page 复选框。然后，系统会要求你选择要用作子母版页父级的母版页。

图 9-9 顶部的代码示例显示了子母版页的 `startup.aspx` 代码。此页面使用一个与你在图 9-4 中看到的类似的父母版页。主要区别是我删除了页面底部的段落。正如你可能还记得的，该段落包含一个标签，用于显示距离万圣节还有多少天。

请注意，此代码几乎与内容页的代码相同。唯一的区别是它以 `Master` 指令开头，而不是 `Page` 指令。不过，与父母版页的 `Master` 指令不同，子母版页的 `Master` 指令包含 `MasterPageFile` 和 `AutoEventWireup` 属性。

## 如何向子母版页添加内容

要向子母版页添加内容，可将元素添加到 `Content` 控件中。这在图 9-9 的第二个代码示例中有所说明。在这里，我向第二个 `Content` 控件添加了 `div` 和 `p` 元素。`div` 元素包含一个 `ContentPlaceHolder` 控件，可供从此母版页创建的任何内容页使用。而 `p` 元素包含原本包含在父母版页上的标签。

第一个 `Content` 控件包含一个 `link` 元素，用于标识页面使用的外部样式表。此外，它也包含一个 `ContentPlaceHolder` 控件。此控件可供任何内容页使用，以便为页面包含样式和其他页眉信息。

创建父母版页和子母版页后，你可以创建使用其中任何一个的页面。例如，如果你希望内容页包含指示距离万圣节还有多少天的标签，你可以创建一个使用子母版页的页面。但如果你不希望此标签包含在内容页中，可以创建一个使用父母版页的页面。

## 使用与图 9-4 中类似的母版页作为其父级的新的子母版页的 aspx 代码

```
<%@ Master Language="C#" MasterPageFile="~/Site.master"
    AutoEventWireup="true" CodeFile="ChildMasterPage.master.cs"
    Inherits="ChildMasterPage" %>

<asp:Content ID="Content1" ContentPlaceHolderID="head" Runat="Server">
</asp:Content>
<asp:Content ID="Content2" ContentPlaceHolderID="Main" Runat="Server">
</asp:Content>
```

## 向页面添加内容后的 aspx 代码

```
<%@ Master Language="C#" MasterPageFile="~/Site.master"
    AutoEventWireup="true" CodeFile="ChildMasterPage.master.cs"
    Inherits="ChildMasterPage" %>

<asp:Content ID="Content1" ContentPlaceHolderID="HeadContent" Runat="Server">
    <link href="Styles/Child.css" rel="stylesheet" type="text/css" />
    <asp:ContentPlaceHolder ID="HeadContent" runat="server">
    </asp:ContentPlaceHolder>
</asp:Content>
<asp:Content ID="Content2" ContentPlaceHolderID="MainContent" Runat="Server">
    <div id="main">
        <asp:ContentPlaceHolder ID="MainContent" runat="server">
        </asp:ContentPlaceHolder>
    </div>
    <p id="message">
        <asp:Label ID="lblMessage" runat="server"></asp:Label>
    </p>
</asp:Content>
```

## 描述

- 当你创建 *嵌套母版页* 时，*父母版页* 通常用于为网站中的每个页面提供元素。然后，不同的 *子母版页* 可用于为网站中不同类型的页面提供额外的元素。
- 要创建子母版页，请使用图 9-2 中创建母版页的技术，但勾选 Select Master Page 复选框，然后从显示的对话框中选择父母版页。
- 要向子母版页添加内容，请将内容放在 `Content` 元素的开始和结束标签之间。使用 `ContentPlaceHolder` 控件来标识可在使用该母版页的内容页中添加内容的位置。
- 当你使用嵌套母版页时，可以为父母版页或任何子母版页创建内容页。

## 如何从内容页访问母版页控件

在许多应用程序中，你需要从应用程序的内容页访问母版页中的一个或多个控件。例如，本章前面显示的母版页在页脚区域有一个标签，通常显示距离万圣节剩余的天数。但如果在显示某些内容页时，你想在此标签中显示其他信息怎么办？

例如，当用户使用 `Order.aspx` 页面购买产品时，你可能希望显示购物车中当前商品的数量，而不是距离万圣节还有多少天。为此，你可以将母版页控件公开为公共属性，然后从内容页访问该属性。

## 如何将母版页控件公开为公共属性

从内容页访问母版页上的控件的最简单方法是创建一个公共属性来提供对该控件的访问。图 9-10 说明了母版页的代码隐藏文件，展示了如何执行此操作。

首先，你在母版页中创建一个公共属性来标识你想要能够访问的控件。在这种情况下，属性的类型为 `Label`，属性名为 `MessageLabel`。然后，你为该属性编写 `get` 和 `set` 访问器。在这里，`get` 访问器返回 `lblMessage` 标签，而 `set` 访问器将属性值分配给 `lblMessage`。

请注意，我还在母版页的 `Page_Load` 方法中添加了另一个 `if` 语句。现在，只有当标签的 `Text` 属性值为空时，`lblMessage` 标签才会被设置为距离万圣节还有多少天。这样，如果内容页在其 `Page_Load` 方法中为此标签分配了值，母版页的 `Page_Load` 方法就不会覆盖该值。这之所以有效，是因为内容页的 `Page_Load` 方法在母版页的 `Page_Load` 方法之前被调用。

## 为提供公共属性的主页提供代码隐藏文件

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

- 如果在母版页中将控件公开为公共属性，则内容页可以访问母版页中的控件。为此，您需要编写一个具有 `get` 和 `set` 访问器的属性。

## 如何从内容页访问母版页的公共属性

图 9-11 显示了如何从内容页访问母版页中的公共属性。如该图上半部分所示，您可以在内容页的 `aspx` 文件中使用 `MasterType` 指令来指定用于母版页的类型名称。此指令中指定的值指定了内容页的 `Master` 属性返回的对象的类型。因此，在此示例中，`Master` 属性将返回类型为 `Site` 的对象。如果查看前一图中的类声明，您会看到 `Site` 是定义母版页的类的名称。

该图第二部分显示了 `Order.aspx` 内容页代码隐藏文件中的两个方法。如您所见，`Page_Load` 方法调用了名为 `DisplayCartMessage` 的方法。此方法确定购物车中当前项目的数量，并相应地设置母版页 `MessageLabel` 属性公开的标签的 `Text` 属性。但请注意，如果购物车为空，则不会为消息标签分配任何值。在这种情况下，母版页的 `Page_Load` 方法将把标签设置为距离万圣节剩余的天数。

尽管在内容页的 `aspx` 文件中使用 `MasterType` 指令可以更轻松地访问母版页的属性，但您应该意识到此指令不是必需的。如果您不指定 `MasterType` 指令，`Master` 属性将返回类型为 `Master` 的对象。然后，您可以将此对象强制转换为母版页的实际类型以访问您创建的任何属性。

例如，您可以使用如下代码为 `MessageLabel` 属性分配文本：

```
MasterPage mp = (Site) this.Master;
if (cart.Count == 1)
    mp.MessageLabel.Text =
        "There is one item in your cart.";
else if (cart.Count > 1)
    mp.MessageLabel.Text =
        "There are " + cart.Count + " items in your cart.";
```

在这里，`Master` 对象被强制转换为 `Site` 对象，以便可以访问其 `MessageLabel` 属性。`MasterType` 指令的目的是避免这种笨拙的强制转换。

## Order.aspx 页的一部分
