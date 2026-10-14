

## 新 master 页面的 aspx 代码

图 9-3 顶部所示的列表展示了使用 Master Page 模板创建 master 页面时生成的 aspx 代码。可以看出，这段代码与为常规 ASP.NET 网页生成的 aspx 代码类似，但有两个重要的区别。

首先，代码不是以 Page 指令开头，而是以 Master 指令开头。这表明该文件包含的是 master 页面而不是常规 ASP.NET 页面。其次，master 页面包含两个 ContentPlaceHolder 控件。其中第一个位于 head 元素内，可用于在 head 元素内编码的任何元素。在大多数情况下，你会使用此内容占位符来放置一个 link 元素，以标识内容页面的外部样式表。第二个 ContentPlaceHolder 控件位于 div 元素内，用于页面的主要内容。

请注意，master 页面文件本身是一个格式良好的 HTML 文档，包含 html、head 和 body 元素。body 元素包含一个 form 元素，该元素又包含一个 ContentPlaceHolder 控件。你添加到 master 页面 body 中的任何元素都应出现在 form 元素内，但位于 ContentPlaceHolder 控件之外。同样，你添加到 master 页面标题中的任何元素，例如 link 元素，都应出现在 head 元素内，但位于 head 元素中的 ContentPlaceHolder 控件之外。

```aspx
<%@ Master Language="C#" AutoEventWireup="true" CodeFile="Site.master.cs"
Inherits="Site" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title></title>
    <asp:ContentPlaceHolder id="head" runat="server">
    </asp:ContentPlaceHolder>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <asp:ContentPlaceHolder id="ContentPlaceHolder1" runat="server">
            </asp:ContentPlaceHolder>
        </div>
    </form>
</body>
</html>
```

### Master 页面指令的属性

| Attribute | Description |
| --- | --- |
| Language | Specifies the language used for any code required by the page. |
| CodeFile | Specifies the name of the code-behind file. |
| Inherits | Specifies the name of the page class defined in the code-behind file. |

### ContentPlaceHolder 控件的属性

| Attribute | Description |
| --- | --- |
| ID | Specifies the name of the content placeholder. |
| Runat | Specifies that the control is a server-side control. |

### Description

- A master page must begin with a Master page directive and should include at least one ContentPlaceHolder control.
- By default, a master page contains two ContentPlaceHolder controls: one in the head element and one in the form element. The one in the head element is typically used for a link element that identifies an external style sheet. The one in the form element is used for the displayable elements of the content page.
- Any HTML or asp elements that you add to the master page will be displayed on every page that uses the master page, along with the content that’s defined for the ContentPlaceHolder control in the form element.

Figure 9-3    The aspx code for a new master page

## 万圣节商店 master 页面的 aspx 代码

图 9-4 显示了图 9-1 中 master 页面的完整 aspx 代码。首先，你应该注意到文档 head 包含一个 link 元素。该元素将名为 Main.css 的外部样式表链接到页面。此外，文档 head 包含默认添加的内容占位符。

接下来，注意页面的主 division 被分为另外三个 division。第一个 division 包含用于显示页面顶部横幅的 image 控件。第二个 division 包含四个段落，每个段落包含一个超链接。这些超链接用于创建表单左侧的导航菜单。第三个 division 包含表单的内容占位符。

在这三个 division 之后是一个单独的段落。该段落包含一个 label 控件，将用于显示距离万圣节还有多少天。

最后，注意此页面上的每个 division 和段落都有 id 属性或 class 属性。这些属性在外部样式表中使用，以在 master 页面上布局元素，使其显示如图所示 9-1。

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

### Description

- Most master pages include elements like banners and navigation controls.
- You can use CSS to lay out the elements on a master page just as you can any other page.

## master 页面的代码隐藏文件

master 页面与常规 ASP.NET 页面一样具有事件。因此，必须认识到，其中大多数事件是在内容页面的相应事件之后触发的。例如，master 页面的 Page Load 事件将在内容页面的 Page Load 事件之后处理。同样，内容页面的任何控件事件都在 master 页面的任何控件事件之前处理。但是请注意，内容页面和 master 页面的 Load 事件都在任何控件事件之前处理。

图 9-5 显示了图 9-4 中 master 页面的代码隐藏文件。此代码隐藏文件包含一个在 master 页面加载时执行的 Page_Load 方法。可以看出，此方法调用一个名为 DaysUntilHalloween 的方法，该方法计算并返回距离 10 月 31 日剩余的天数。然后，将适当的 message 分配给 lblMessage 标签的 Text 属性。

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

- Master pages have events just like regular ASP.NET pages. For this master page, the Load event is used to display the number of days remaining until Halloween.
- Most events for the content page are raised before the corresponding events for the master page. For example, the Load event for the content page is raised before the Load event for the master page. Similarly, events for controls in the content page are raised before events for controls in the master page.

