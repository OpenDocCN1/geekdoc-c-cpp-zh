
接下来，注意页面的主 division 被分为另外三个 division。第一个 division 包含用于显示页面顶部横幅的 `image` 控件。第二个 division 包含四个段落，每个段落包含一个超链接。这些超链接用于创建表单左侧的导航菜单。第三个 division 包含表单的内容占位符。

在这三个 division 之后是一个单独的段落。该段落包含一个 `label` 控件，将用于显示距离万圣节还有多少天。

最后，注意此页面上的每个 division 和段落都有 `id` 属性或 `class` 属性。这些属性在外部样式表中使用，以在 master 页面上布局元素，使其显示如图所示 9-1。

```aspx
<%@ Master Language="C#" AutoEventWireup="true" CodeFile="Site.master.cs" Inherits="Site" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Chapter 9: Master Page</title>
    <link href="Styles/Main.css" rel="stylesheet" type="text/css" />
    <asp:ContentPlaceHolder id="HeadContent" runat="server">
    </asp:ContentPlaceHolder>
</head>
<body>
    <form id="form1" runat="server">
        <div id="page">
            <div id="header">
                <asp:Image ID="Image1" runat="server" ImageUrl="~/Images/banner.jpg" />
            </div>
            <div id="sidebar">
                <p class="link">
                    <asp:HyperLink ID="HyperLink1" runat="server" NavigateUrl="~/Order.aspx" ForeColor="DarkOrange">Home</asp:HyperLink>
                </p>
                <p class="link">
                    <asp:HyperLink ID="HyperLink2" runat="server" NavigateUrl="~/Cart.aspx" ForeColor="DarkOrange">Your Shopping Cart</asp:HyperLink>
                </p>
                <p class="link">
                    <asp:HyperLink ID="HyperLink3" runat="server" NavigateUrl="~/Service.aspx" ForeColor="DarkOrange">Customer Service</asp:HyperLink>
                </p>
                <p class="link">
                    <asp:HyperLink ID="HyperLink4" runat="server" NavigateUrl="~/About.aspx" ForeColor="DarkOrange">About Us</asp:HyperLink>
                </p>
            </div>
            <div id="main">
                <asp:ContentPlaceHolder id="MainContent" runat="server">
                </asp:ContentPlaceHolder>
            </div>
            <p id="message">
                <asp:Label ID="lblMessage" runat="server"></asp:Label>
            </p>
        </div>
    </form>
</body>
</html>
```

## Description

- Most master pages include elements like banners and navigation controls.

- You can use CSS to lay out the elements on a master page just as you can any other page.

## master 页面的代码隐藏文件

master 页面与常规 ASP.NET 页面一样具有事件。因此，必须认识到，其中大多数事件是在内容页面的相应事件之后触发的。例如，master 页面的 `Page Load` 事件将在内容页面的 `Page Load` 事件之后处理。同样，内容页面的任何控件事件都在 master 页面的任何控件事件之前处理。但是请注意，内容页面和 master 页面的 `Load` 事件都在任何控件事件之前处理。

图 9-5 显示了图 9-4 中 master 页面的代码隐藏文件。此代码隐藏文件包含一个在 master 页面加载时执行的 `Page_Load` 方法。可以看出，此方法调用一个名为 `DaysUntilHalloween` 的方法，该方法计算并返回距离 10 月 31 日剩余的天数。然后，将适当的 message 分配给 `lblMessage` 标签的 `Text` 属性。

```aspx
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;

public partial class Site : System.Web.UI.MasterPage
{
    protected void Page_Load(object sender, EventArgs e)
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

### Description

- Master pages have events just like regular ASP.NET pages. For this master page, the `Load` event is used to display the number of days remaining until Halloween.

- Most events for the content page are raised before the corresponding events for the master page. For example, the `Load` event for the content page is raised before the `Load` event for the master page. Similarly, events for controls in the content page are raised before events for controls in the master page.

## 如何创建和开发内容页面

创建主页面后，您可以为该主页面创建和开发内容页面。下面的主题将展示如何操作。

### 如何创建内容页面

图 9-6 显示了如何创建内容页面。简而言之，您创建内容页面所使用的步骤与创建普通页面相同，但需要勾选 Select Master Page 复选框。然后，您可以从显示的 Select a Master Page 对话框中选择要为内容页面使用的主页面。

另外，您也可以在 Solution Explorer 中选择要使用的主页面，然后选择 Website→Add Content Page 命令。这将为所选主页面创建一个内容页面。请注意，使用此技术时，内容页面会自动命名为 `Default`。

本图中的代码示例显示了为图 9-4 所示的主页面创建名为 `Order` 的新内容页面时生成的代码。此代码与创建普通 ASP.NET 页面时生成的代码大不相同。虽然 `Page` 指令包含与普通 ASP.NET 页面相同的信息，但它还包含一个 `MasterPageFile` 属性，用于指定您选择的主页面。而且内容页面的其余部分也与正常的 ASP.NET 页面不同。

在描述其他差异之前，您应该知道，在内容页面的 `Page` 指令的 `Title` 属性中指定的标题会覆盖在主页面中指定的任何标题。这样，您就可以为每个内容页面显示不同的标题。但是，如果您希望每个内容页面使用相同的标题，则可以在主页面中指定标题，然后从内容页面中删除 `Title` 属性。

与普通 ASP.NET 页面不同，内容页面不包含 `Doctype` 指令或任何结构性 HTML 元素，如 `html`、`head`、`body` 或 `form`。这是因为这些元素由主页面提供。相反，内容页面为主页面中的每个内容占位符包含一个 ASP.NET `Content` 元素。在本例中，由于主页面包含两个占位符，因此内容页面包含两个 `Content` 元素。如您所见，这些元素的 `ContentPlaceHolderID` 属性标识了它们所关联的占位符。然后，您将页面内容放在 `Content` 元素的开始和结束标签之间。

本图还包含将普通页面转换为内容页面的步骤。如果您在不使用主页面的情况下开始一个网站，而后来决定使用主页面，则需要遵循此步骤。不幸的是，Visual Studio 并未提供自动执行此操作的方法。因此，您必须手动编辑每个页面，以将 `MasterPageFile` 属性添加到 `Page` 指令中，删除 `Doctype` 指令和结构性 HTML 元素（`html`、`head`、`body` 和 `form`），并添加一个或多个 `Content` 元素。

由于此转换过程容易出错，因此值得为除最简单的应用程序之外的所有应用程序使用主页面，即使每个主页面仅包含内容占位符也是如此。然后，当您准备好为应用程序中的页面提供一致的外观时，您可以增强主页面。

图 9-6 还显示了指定内容页面使用的主页面的另外两种方法。首先，您可以在 `web.config` 文件的 `pages` 元素中添加一个 `MasterPageFile` 属性，该属性指定要与未指定主文件的页面一起使用的主页面。其次，您可以在 `Page_PreInit` 方法中设置页面的 `MasterPageFile` 属性来在运行时指定主页面。但是，请注意，Web Forms Designer 不支持这两种技术。如果您使用它们，则将无法在 Design 视图中查看或编辑内容页面。

#### 使用图 9-4 中主页面创建的新页面的 aspx 代码

```
<%@ Page Language="C#" MasterPageFile="~/Site.master" AutoEventWireup="true" CodeFile="Order.aspx.cs" Inherits="Order" Title="Untitled Page" %>

<asp:Content ID="Content1" ContentPlaceHolderID="HeadContent" runat="Server">
</asp:Content>
<asp:Content ID="Content2" ContentPlaceHolderID="MainContent" runat="Server">
</asp:Content>
```

#### 创建新内容页面的两种方法

- 选择 Website→Add New Item 命令。然后，选择 Web Form 模板，输入表单的名称，勾选 Select Master Page 复选框，然后单击 Add。当 Select a Master Page 对话框出现时，选择您想要的主页面，然后单击 OK。

- 在 Solution Explorer 中选择主页面，然后选择 Website→Add Content Page 命令。

#### 如何将普通 ASP.NET 页面转换为内容页面

- 首先，在 `Page` 指令中添加一个 `MasterPageFile` 属性，以指定主页面的 URL。接下来，用如上所示的第二个 ASP.NET `Content` 元素替换包含页面实际内容的 `div` 元素。然后，如果 `head` 元素包含页面使用的其他元素，请用如上所示的第一个 `Content` 元素替换 `head` 元素。最后，删除 `Content` 元素之外的所有内容，仅保留 `Page` 指令。

#### 指定主页面的另外两种方法

##### 在 web.config 文件中

```
<system.web>
  <pages masterPageFile="Site.master" />
</system.web>
```

##### 在 Page_PreInit 方法中

```
protected void Page_PreInit(object sender, EventArgs e)
{
    MasterPageFile = "Site.master";
}
```

#### 描述

- 内容页面 aspx 代码中的 `Page` 指令包含一个 `MasterPageFile` 属性，用于指定主页面名称。

- 内容页面的 aspx 代码包含 `Content` 元素，用于指示应放置页面内容的 content placeholder 的 `ID`。您为页面创建的任何内容都应编码在这些元素的开始和结束标签之间。

- 您也可以在 `web.config` 文件或 `Page_PreInit` 方法中指定主页面。但是，Web Forms Designer 不支持这两种技术，因此您将无法在 Design 视图中查看内容页面。

### 如何向页面添加内容

图 9-7 显示了内容页面在 Design 视图中的外观。如您所见，主页面会与主页面 `form` 元素中内容占位符的 `Content` 控件一起显示。但是，您无法从此视图编辑主页面中的任何元素。您只能通过向内容区域添加文本或将控件从 Toolbox 拖到内容区域来编辑页面的内容。稍后，当您切换到 Source 视图时，您添加的任何元素都将出现在 `Content` 元素的开始和结束标签之间。

如果您使用的是在 `form` 元素中包含多个内容占位符的主页面，则每个占位符将有一个单独的 `Content` 控件。然后，您可以编辑这些控件各自的内容。

#### Design 视图中的内容页面

![](img/c024ccf88e28c30c07dd410d4342288f_344_0.png)

#### 描述

- 当您在 Design 视图中显示内容页面时，主页面的元素会显示出来，以便您可以了解它们将如何影响页面的最终外观。

- 要添加页面的内容，请单击 `Content` 控件。然后，您可以键入文本或使用 Toolbox 将控件拖到页面的内容区域。您添加的任何文本或其他元素都将放置在 aspx 文件中 `Content` 元素的开始和结束标签之间。

- 如果您只想为页面显示主页面的默认内容，请单击 `Content` 控件右上角的 Smart Tag 图标，然后选择 Default to Master’s Content。然后，您将无法编辑内容区域的内容。要再次编辑内容，请从 smart tag 菜单中选择 Create Custom Content。

#### Order 内容页面的 aspx 代码

为了帮助您了解如何向内容页面添加内容，图 9-8 展示了 Halloween Store 应用程序的 Order 页面的 aspx 代码。如您所见，此代码包含两个 `Content` 控件。第一个包含一个 `link` 元素，用于标识页面使用的外部样式表。当 Order 页面显示时，此样式表中的样式将与主页面标识的外部样式表中的样式合并。

第二个 `Content` 控件包含页面的主要内容。这与通常包含在标准页面的 `form` 元素中的内容相同。因此，您不应该有任何理解上的困难。

#### 内容页的 aspx 代码
