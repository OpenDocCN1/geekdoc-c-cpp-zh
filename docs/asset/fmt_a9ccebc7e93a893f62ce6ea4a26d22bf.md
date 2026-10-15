
您现在可以通过按 F5 键运行应用程序。结果如图 13.25 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_681_0.png)

在下一节中，您可以看到如何为 Web Form 添加背景颜色。

## Adding a Background Color to a Web Form

.NET 允许您使用 `<body>` 标签的 `bgColor` 属性更改 Web Form 的背景颜色。让我们使用 `FileSystemWebsite` 应用程序学习如何更改 Default Web 页面的背景颜色。为此，执行以下步骤：

1. 在 Design View 中选择 Web Form。接下来，在 Properties 窗口中，单击 `BgColor` 属性的省略号按钮。More Colors 对话框出现，如图 13.26 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_682_0.png)

**Figure 13.26:** The More Colors Dialog Box

2. 选择一种颜色并单击 OK 按钮，如图 13.26 所示。所选颜色使用 Listing 13.5 中给出的突出显示的代码行应用于 Default Web 页面。

**Listing 13.5:** Adding Background Color of a Web Form

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"

"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">

<head runat="server">

<title>Welcome Page</title>

</head>

<body bgcolor="#99ff66">

<form id="form1" runat="server">

<div>

</div>

</form>

</body>

</html>
```

3. 按 F5 键运行 Web 站点，输出会显示页面背景颜色已更改，如图 13.27 所示：

**Figure 13.27:** The Default Web Page with its Background Color Set

在下一节中，您将学习如何为 Web Form 添加背景图像。

## Adding a Background Image to a Web Form

您还可以为应用程序的 Default Web 页面添加背景图像。我们使用 `FileSystemWebsite` 应用程序学习如何为其 Default Web 页面添加背景图像。为此，执行以下步骤：

1. 向应用程序添加图像。现在在 Design View 中，选择 Web 页面并在 Properties 窗口中，单击 Web 页面的 `Background` 属性的省略号按钮。Select Project Item 对话框出现，如图 13.28 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_683_0.png)

**Figure 13.28:** The Select Project Item Dialog Box

> **NOTE**
> 要向应用程序添加图像，只需复制图像文件，右键单击 Solution Explorer 中的项目名称，然后从上下文菜单中选择 Paste 选项。

2. 选择图像文件并单击 OK 按钮，如图 13.28 所示。所选背景图像使用 Listing 13.6 中给出的突出显示的代码行添加到 Default Web 页面：

**Listing 13.6:** Adding a Background Image to a Web Form

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">

<head runat="server">

<title>Welcome Page</title>

</head>

<body background="penguins.jpg" bgcolor="#99ff66">

<form id="form1" runat="server">

<div>

</div>

</form>

</body>

</html>
```

3. 按 F5 键运行应用程序，输出出现，如图 13.29 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_684_0.png)

**Figure 13.29:** The Default Web Page with its Background Image Set

接下来您将学习如何向 Web Form 添加不同的控件。

## Adding Controls to a Web Form

如果 Web Form 不包含任何 Web 控件，则 Web Form 仍不完整。通常，几乎所有 Web Form 都附带控件。在本节中，您将学习如何向 Web Form 添加控件并探索控件的各种属性。我们以 `FileSystemWebsite` 应用程序的相同示例为例，并向其 Default Web 页面添加控件。为此，从 Toolbox 拖放三个 `Label` 控件、两个 `TextBox` 控件和一个 `Button` 控件到 Default Web 页面并设置其文本，如图 13.30 所示。当您按 F5 键执行应用程序时，输出显示，如图 13.30 所示：

**Figure 13.30:** The Design View of the Default Web Page

## Hiding and Displaying Controls

让我们学习如何使用其 `Visible` 属性在 Web 页面上隐藏和显示控件。我们使用 `FileSystemWebsite` 应用程序作为示例，在 Web 页面首次加载时隐藏 Default Web 页面底部的标签。为此，执行以下步骤：

1. 在设计时选择 `Label` 控件，并在 Properties 窗口中将其 `Visible` 属性设置为 `false`。

2. 按 F5 键执行应用程序，结果将显示，如图 13.31 所示：

**Figure 13.31:** Displaying the Page with the Label Hidden

在图 13.30 中，您可以看到 Web 页面底部的标签是可见的，但在图 13.31 中，它是隐藏的。现在，如果您想通过按钮显示隐藏的标签，双击按钮，例如 Design 视图中的 Welcome 按钮，并在按钮的 `Click` 事件中添加以下代码：

```
protected void Button1_Click(object sender, EventArgs e)
{
    Label3.Visible = true;
    Label3.Text = "welcome " + TextBox2.Text;
}
```

3. 在文本框中输入姓名和学号，然后单击欢迎按钮。标签控件变为可见，并显示文本 Welcome <UserName>，如图 13.32 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_686_0.png)

图 13.32：显示带有欢迎信息的可见标签

## 禁用和启用控件

当你不希望用户访问某个控件时，通常会禁用该控件。通常，你会禁用具有自动生成的用户 ID 的控件。让我们学习如何禁用包含用户学号的文本框。我们在欢迎按钮的 `Click` 事件中禁用文本框。为此，在按钮控件的 `Click` 事件中添加高亮代码，如清单 13.7 所示：

### 清单 13.7：禁用和启用按钮控件的代码

```
protected void Button1_Click(object sender, EventArgs e)
{
    Label3.Visible = true;
    Label3.Text = "welcome " + TextBox2.Text;
    TextBox1.Enabled = false;
}
```

默认情况下，`Enabled` 属性设置为 `true`。现在，通过按 F5 键执行应用程序。禁用的文本框显示为灰色，如图 13.33 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_686_1.png)

图 13.33：显示禁用的文本框

现在，要启用此文本框，只需将其 `Enabled` 属性设置为 `true` 即可。

## 设置控件的标题和字体

你可以使用其 `Text` 属性为任何控件设置标题。此属性在设计时和运行时均可用。向 Web 表单添加控件后，可以在属性窗口中将适当的文本放在 `Text` 属性中来设置其标题。

你可以使用其 `Font` 属性更改控件的字体。为此，首先选择控件，然后在属性窗口中展开 `Font` 属性。最后，设置字体和大小属性，如图 13.34 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_687_0.png)

图 13.34：使用属性窗口设置字体集

与设置 `Text` 属性类似，我们已为 Default Web 页面上的所有控件设置了 `Font` 属性。通过按 F5 键运行 `FileSystemWebsite` 应用程序，所有控件的字体都会发生变化，如图 13.35 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_687_1.png)

图 13.35：显示字体已更改的 Web 表单

## 设置控件的 Tab 顺序

假设你的鼠标停止工作，但你仍想访问网站。你该怎么做呢？当然，你可以使用键盘。为了使网页上的控件可以通过键盘访问，你必须使用 `TabIndex` 属性为控件设置正确的 Tab 顺序。`TabIndex` 属性是当前控件在 Tab 顺序中的索引，通常从 0 开始。当用户按下 Tab 键时，焦点会根据 Tab 索引按升序从一个控件移动到另一个控件。在本节中，我们学习如何为 Default Web 页面上的所有控件设置 Tab 顺序。为此，选择要设置 Tab 顺序的控件并在属性窗口中打开其属性。现在，将控件的 `TabIndex` 属性设置为 0，下一个控件设置为 1，以此类推。在本例中，将 `TextBox1` 的 `TabIndex` 设置为 1，`TextBox2` 设置为 2，最后将 `Button1` 设置为 3。通常，你永远不会为标签控件设置 Tab 键。`Default.aspx` Web 页面的源视图如清单 13.8 所示：

### 清单 13.8：在 Web 页面中设置控件的 Tab 顺序

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">

<head runat="server">

<title>welcome Page</title>

</head>

<body background="nature.jpg" bgcolor="#99ff66">

<form id="form1" runat="server">

<div style="font-weight: 800; font-family: Arial; font-size: xx-large; font-style: normal;">

welcome to C# 2010 Black Book

</div>

<p>&nbsp;</p>

<p>&nbsp;</p>

<p style="margin-left: 400px">

<asp:Label ID="Label1" runat="server" Font-Bold="True" Text="Roll Number" Font-Names="Bookman Old Style" Font-Size="Small"></asp:Label>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

<asp:TextBox ID="TextBox1" runat="server" Font-Names="Bookman Old Style" Font-Size="Small" TabIndex="1"></asp:TextBox>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

</p>

<div style="margin-left: 400px">

<asp:Label ID="Label2" runat="server" Font-Bold="True" Text="Name" Font-Names="Bookman Old Style" Font-Size="Small"></asp:Label>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

<asp:TextBox ID="TextBox2" runat="server" Font-Names="Bookman Old Style" Font-Size="Small" TabIndex="2"></asp:TextBox>

</div>

<p style="margin-left: 480px">

<asp:Button ID="Button1" runat="server" Font-Bold="True" Text="Welcome" Width="121px" Font-Names="Bookman Old Style" Font-Size="Medium" onclick="Button1_Click" TabIndex="3" />

</p>

<div style="margin-left: 120px">

<br />

</div>
```

## 设置控件的样式

在设计视图中处理网页时，通常需要对网页的某些部分进行细微更改，例如为文本添加样式、为元素应用边框或对齐图像。在这种情况下，你需要为需要设置样式的元素创建内联样式表。在本节中，让我们学习如何为网页的 `<h1>` 元素设置样式。为此，请执行以下步骤：

- 1. 在设计视图中打开 `FileSystemWebsite` 应用程序的 Default Web 页面。选择 `<div>` 元素并选择 Format→New Style 菜单项。New Style 对话框出现，如图 13.36 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_689_0.png)

- 2. 选择对话框顶部选择器下拉列表并选择内联样式选项。此选项可确保新样式作为内联样式应用于 `<div>` 元素。

- 3. 现在根据你的选择应用样式设置，完成后单击 OK 按钮。在 Default Web 页面的源视图中，你可以看到样式已应用于 `<div>` 元素，如清单 13.9 所示：

### 清单 13.9：设置控件的样式

```
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">

<head runat="server">

<title>Welcome Page</title>

</head>

<body background="nature.jpg" bgcolor="#99ff66">

<br />

<asp:Label ID="Label3" runat="server" Font-Names="Bookman Old Style" Font-Size="Small" Text="Label" Visible="False"></asp:Label>

</div>

</form>

</body>

</html>

<form id="form1" runat="server">

<div style="border-style: ridge; font-weight: 800; font-family: 'Bookman Old Style'; font-size: xx-large; font-style: normal;">
```
