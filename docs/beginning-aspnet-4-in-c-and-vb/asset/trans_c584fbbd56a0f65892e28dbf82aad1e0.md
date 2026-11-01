
```
protected void cycleButton_Click(object sender, EventArgs e)
{
    rainbowLabel1.Cycle();
}
```

*代码片段：PCS Custom C# WebSite1/Default.aspx.cs*

现在您可以查看示例，并在示例文本中循环切换颜色，如图 41-4 所示。

![](img/d7d2ffa0a76feaab821930e95daace93_1256_0.png)

图 41-4

您还可以用自定义控件做更多事情；实际上，可能性几乎是无穷无尽的，但您需要自己试验这些可能性。

## 母版页

母版页提供了一种极好的方式，使您的网站更易于设计。将页面布局的全部（或至少大部分）放在一个文件中，可以让您专注于网站各个网页更重要的内容。

母版页创建在扩展名为 .master 的文件中，并且可以通过“网站 → 添加新项...”菜单项添加，就像任何其他站点内容一样。乍一看，为母版页生成的代码与标准 .aspx 页面非常相似：

```
<%@ Master Language="C#" AutoEventWireup="true"
CodeFile="MyMasterPage.master.cs" Inherits="MyMasterPage" %>
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
            <asp:ContentPlaceHolder ID="ContentPlaceHolder1" runat="server">
            </asp:ContentPlaceHolder>
        </div>
    </form>
</body>
</html>
```

不同之处如下：

-   使用 <%@ Master %> 指令而不是 <%@ Page %> 指令，尽管属性相同。
-   在页眉中放置一个 ID 为 head 的 ContentPlaceHolder 控件。
-   在页面主体中放置一个 ID 为 ContentPlaceHolder1 的 ContentPlaceHolder 控件。

ContentPlaceHolder 控件正是让母版页如此有用的原因。您可以在页面上放置任意数量的此类控件，使用母版页的 .aspx 页面通过它们“插入”内容。您可以将默认内容放在 ContentPlaceHolder 控件内部，但 .aspx 页面可以覆盖这些内容。

要让 .aspx 页面使用母版页，您需要修改 <%@ Page %> 指令，如下所示：

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs"
Inherits="_Default" MasterPageFile="~/MyMasterPage.master"
Title="Page Title" %>
```

这里您添加了两个新属性：一个 MasterPageFile 属性，指定要使用的母版页；一个 Title 属性，设置母版页中 <title> 元素的内容。

或者，当您向包含母版页的网站添加 .aspx 页面时，您可以选择一个母版页。“添加新项向导”包含一个“选择母版页”复选框，如果选择此选项，向导的下一页会给出一个母版页列表，供您从 Web 应用程序中选择。然后，页面的生成代码将包含前面描述的 MasterPageFile 属性。

如果您想使用默认的母版页内容，.aspx 页面不必包含任何其他代码。此外，您不能包含 Form 控件，因为一个页面只能有一个 Form 控件，而母版页中已经有一个。

使用母版页的 .aspx 页面除了指令、脚本元素和 Content 控件之外，不能包含任何根级内容。您可以根据需要拥有任意数量的 Content 控件，每个 Content 控件都会将内容插入到母版页中的其中一个 ContentPlaceHolder 控件中。唯一需要注意的就是确保 Content 控件的 ContentPlaceHolderID 属性与您想要插入内容的 ContentPlaceHolder 控件的 ID 匹配。因此，要向前面显示的母版页添加内容，您只需要在 .aspx 文件中包含以下内容：

```
<%@ Page Language="C#" MasterPageFile="~/MyMasterPage.master"
AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="__Default"
Title="Untitled Page" %>

<asp:Content ID="Content1" ContentPlaceHolderID="head" runat="Server">
</asp:Content>
<asp:Content ID="Content2" ContentPlaceHolderID="ContentPlaceHolder1"
runat="Server">
Custom content!
</asp:Content>
```

母版页的真正强大之处在于，当您在母版页中的 ContentPlaceHolder 控件周围添加其他内容（如导航控件、站点徽标和 HTML）时体现出来。您可以为主内容、侧边栏内容、页脚文本等提供多个 ContentPlaceHolder 控件。

如果您不想为特定的 ContentPlaceHolder 提供内容，可以省略页面上的 Content 控件。例如，您可以从前面的代码中删除 Content1 控件，而不会影响最终的显示。

### 从网页访问母版页内容

当您向网页添加母版页时，有时需要从网页中的代码访问母版页。为此，您可以使用 Page.Master 属性，该属性将返回一个 MasterPage 对象形式的母版页引用。您可以将其强制转换为母版页文件定义的类型（对于上一节中的示例，这个类将被称为 MyMasterPage）。获得此引用后，您可以访问母版页类的任何公共成员。

此外，您可以使用 MasterPage.FindControl() 方法按标识符在母版页上定位控件。这使您能够操作母版页上位于内容占位符之外的控件。

一个典型的用途是：如果您定义了一个用于标准表单（带有提交按钮）的母版页，您可以在子页面中定位该提交按钮，并在母版页中为提交按钮添加事件处理程序。这样，您就可以提供例如响应表单提交的自定义验证逻辑。

### 嵌套母版页

“选择母版页”选项在您创建新母版页时也可用。通过使用此选项，您可以创建基于父母版页的嵌套母版页。例如，您可以创建一个名为 MyNestedMasterPage 的母版页，它使用 MyMasterPage，如下所示：

```aspx
<%@ Master Language="C#" MasterPageFile="~/MyMasterPage.master"
    AutoEventWireup="false" CodeFile="MyNestedMasterPage.master.cs"
    Inherits="MyNestedMasterPage" %>

<asp:Content ID="Content1" ContentPlaceHolderID="head" Runat="Server">
    <!--Disabled for child controls.-->
</asp:Content>
<asp:Content ID="Content2" ContentPlaceHolderID="ContentPlaceHolder1"
    Runat="Server">
    First nested place holder:
    <asp:ContentPlaceHolder ID="NestedContentPlaceHolder1" runat="server">

    </asp:ContentPlaceHolder>
    <br />
    <br />
    Second nested place holder:
    <asp:ContentPlaceHolder ID="NestedContentPlaceHolder2" runat="server">

    </asp:ContentPlaceHolder>
</asp:Content>
```

使用此母版页的页面将为 NestedContentPlaceHolder1 和 NestedContentPlaceHolder2 提供内容，但无法直接访问 MyMasterPage 中指定的 ContentPlaceHolder 控件。在此示例中，MyNestedMasterPage 固定了 head 控件的内容，并为 ContentPlaceHolder1 控件提供了模板。

通过创建一系列嵌套母版页，您可以为页面提供替代布局，同时保留基础母版页的某些方面不变。例如，根母版页可能包含导航和基本布局，而嵌套母版页可以提供具有不同列数的布局。然后，您可以在站点的页面中使用嵌套母版页，并在不同页面之间快速切换这些替代布局。

### PCSDemoSite 中的母版页

在 PCSDemoSite 中，使用了单个母版页 MasterPage.master（母版页的默认名称），代码如下：

```aspx
<%@ Master Language="C#" AutoEventWireup="true"
    CodeFile="MasterPage.master.cs"
    Inherits="MasterPage" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN"
    "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <link rel="stylesheet" href="StyleSheet.css" type="text/css" />
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
        <div id="header">
            <h1><asp:Literal ID="Literal1" runat="server"
                Text="<%$ AppSettings:SiteTitle %>" /></h1>
            <asp:SiteMapPath ID="SiteMapPath1" runat="server"
                CssClass="breadcrumb" />
        </div>
```
