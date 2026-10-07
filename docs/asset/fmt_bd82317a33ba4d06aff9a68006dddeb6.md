
在此示例中，`my.Script`文件现在将包含在每个使用此AJAX主页的内容页中。如果你的内容页需要使用AJAX能力，那么你不能在内容页上添加`ScriptManager`控件。相反，内容页将需要使用已经存在主页上的`ScriptManager`控件。

尽管如此，如果你的内容页需要向`ScriptManager`控件添加项目，它可以使用`ScriptManagerProxy`服务器控件访问主页上的该控件。`ScriptManagerProxy`让你能够向`ScriptManager`添加任何完全特定于包含包含的内容页的项目。

例如，列表5-23显示了内容页如何通过`ScriptManagerProxy`控件向页面添加额外的脚本。

```vb
@Page Language="VB", MasterPage="AjaxMaster.master" %>
<asp:Content ID="Content1" ContentPlaceHolderID="head" runat="server">
</asp:Content>
<asp:Content ID="Content2" ContentPlaceHolderID="ContentPlaceholder1" runat="server">
<asp:ScriptManagerProxy ID="ScriptManagerProxy" runat="server">
<Scripts>
  <asp:ScriptReference Path="myOtherScript.js" />
</Scripts>
</asp:ScriptManagerProxy>
</asp:Content>
```

在这种情况下，此内容页使用`ScriptManagerProxy`控件向页面添加了额外的脚本。此`ScriptManagerProxy`的工作原理与`ScriptManager`完全相同，区别在于它是为内容页设计的。

### 总结

当你创建在所有页面使用通用页眉、页脚或导航的应用时，主页是一个极佳的解决方案。本章介绍了ASP.NET中的主页并解释了如何使用它们。

## 主题与皮肤（THEMES AND SKINS）

本章包含内容：

- 应用和移除主题
- 创建自己的主题
- 程序化处理主题

主题与层样式表（CSS）相似，它们都能让你为页面定义视觉样式。然而，主题比CSS更进一步，因为它们可以包含CSS文件本身。你可以在应用程序、页面或服务器控件级别应用这些主题。

### 为单个ASP.NET页面应用主题

为了查看如何使用这些主题，创建一个包含文本、文本框、按钮和日历的基础页面，如列表6-1所示。

## 第6章 主题与皮肤

列表6-1：未使用主题的ASP.NET页面

```vb
@Page Language="VB" %>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
  <title>STLNET</title>
</head>
<body>
  <form id="form" runat="server">
    <h1>St. Louis .NET User Group</h1><br />
    <asp:TextBox ID="Textbox1" runat="server" /><br />
    <asp:Calendar ID="Calendar1" runat="server" /><br />
    <asp:Button ID="Button1" runat="server" Text="Button" />
  </form>
</body>
</html>
```

这个简单的页面显示了默认服务器控件，它们看起来很平常，但你可以通过ASP.NET主题来更改它们。当此主题页面在浏览器中调用时，它看起来就像图6-1所示。

![](img/7040c21013b8e6c23c612d6da3599ff8_277_0.png)

图6-1

你可以在不更改页面上每个服务器控件样式的情况下轻松更改此页的外观。通过页面指令，你只需应用一个构建（在本章稍后显示）或从网上下载的ASP.NET主题：

```vb
@Page Language="VB" Theme="SmokeAndGlass" %>
```

在页面指令中添加`Theme`属性将更改页面上示例`SmokeAndGlass`主题文件中定义的所有内容。使用此主题后，当我们在浏览器中调用页面时，得到了如图6-2所示的结果。

# 圣路易斯 .NET 用户组

| 日 | 一 | 二 | 三 | 四 | 五 | 六 |
|---|---|---|---|---|---|---|
| | 1 | 2 | 3 | 4 | 5 | 6 |
| 7 | 8 | 9 | 10 | 11 | 12 | 13 |
| 14 | 15 | 16 | 17 | 18 | 19 | 20 |
| 21 | 22 | 23 | 24 | 25 | 26 | 27 |
| 28 | 29 | 30 | 31 | | | |

图6-2

从这里你可以看到所有内容——包括字体、字体颜色、文本框、按钮等——都发生了变化。如果你有多个页面，你可能会发现，在构建时时无需为每项操作思考样式，因为样式已经为你进行了集中式定义。

### 为整个应用程序应用ASP.NET主题

除了使用`Page`指令中的`Theme`属性为ASP.NET页面应用ASP.NET主题外，你还可以从`web.config`文件在应用程序级别应用主题，如列表6-2所示。

+ 列表6-2：从`web.config`文件应用全局主题

```xml
<xml version="1.0"?>
<configuration>
  <system.web>
    <pages theme="SmokeAndGlass" />
  </system.web>
</configuration>
```

如果你在`web.config`文件中指定了，则不需要在ASP.NET页面的`Page`指令中再次定义主题。此主题将自动应用于应用程序中的每一个页面。如果你想以这种方式仅将主题应用于应用程序的特定部分，你可以这样做，并且可以使用`<location/>`元素来选择应用这些主题的区域。

### 从服务器控件中移除主题

无论是在应用程序级别还是页面级别设置的，你都可能对已定义题有替代方案。例如，通过更改你一直使用的文本框控件（来自列表6-1），将其背景设置为黑色并使用白色文字：

```asp
<asp:TextBox ID="TextBox1" runat="server"
  BackColor="#000000" Color="#ffffff" />
```

### 第6章 主题与皮肤（SKINS）

你通过使用`BackColor`和`Color`属性直接在控件本身中指定文本框的黑色背景和文字颜色。然而，如果你位于此文本控件的页面上应用了主题，你将看不到这些黑色或白色文字，因为这些更改被主题覆盖了。

要为你的ASP.NET页面应用主题但不应用于此文本控件，你只需使用文本框服务器控件的`EnableTheming`属性：

```asp
<asp:TextBox Id="TextBox1" runat="server"
  BackColor="#ffffff" EnableTheming="false" />
```

如果你将将此属性应用于列表6-1中的文本框服务器控件，你会发现`SmokeAndGlass`主题仍应用于整个页面，该主题应用于除文本框以外的每个页面。图6-3显示了这一结果。

![](img/7040c21013b8e6c23c612d6da3599ff8_279_0.png)

图6-3

如果你想关闭页面内的控件，请考虑使用`Panel`控件（或任何容器控件）来封装一组控件，并将`Panel`控件的`EnableTheming`属性设置为`False`。此设置将禁用`Panel`中包含的所有控件。

### 从网页中移除主题

现在，如果你想在`web.config`文件中为整个应用程序设置主题，但排除单个ASP.NET页面怎么办？在页面级别移除主题设置简单，就像在服务器控件级别一样。

`Page`指令包含一个`EnableTheming`属性，你可以用它从ASP.NET页面中移除主题。要移除由`web.config`文件中的主题设置应用的主题，只需按照如下方式构造`Page`指令：

```asp
<@ Page Language="VB" EnableTheming="False" %>
```

此构造将主题设为空——移除了在`web.config`文件中指定的任何设置。当在页面或控件级别将其设置为`False`时，系统将不会搜索`Theme`目录，也不会应用任何`.skin`文件（`.skin`文件用于定义ASP.NET服务器控件的样式）。当在页面或控件级别将其设置为`True`时，系统将搜索`Theme`目录并应用`.skin`文件。

如果因为页面级别的`EnableTheming`属性设置为`False`而禁用了主题，你可以通过将该控件的`EnableTheming`属性设置为`True`并同时应用特定主题来启用此页面上特定控件的主题，如下：

```asp
<asp:TextBox ID="TextBox" runat="server"
BackColor="#000000" ForeColor="#ffffff" EnableTheming="true" SkinID="mySkin"
/>
```

### 使用主页理解主题

当ASP.NET应用程序使用主页时，请注意`Page`和`Master`指令都包含`EnableTheming`属性。

![](img/7040c21013b8e6c23c612d6da3599ff8_280_0.png)

如果`Page`和`Master`指令都包含`EnableTheming`属性，同时使用它们的结果如何？假设你有有如下ASP.NET页面：

```asp
<@ Master Language="VB" EnableTheming="False" %>
```

在这种情况下，该页面的主题被禁用了。如果`Page`和`Master`指令都包含`EnableTheming`属性，同时使用它们的结果如何？假设你有有如下ASP.NET页面：

```asp
<@ Master Language="VB" EnableTheming="False" %>
```

在这种情况下，该页面的主题被禁用了。如果`Page`和`Master`指令都包含`EnableTheming`属性，同时使用它们的结果如何？假设你有有如下ASP.NET页面：

```asp
<@ Master Language="VB" EnableTheming="False" %>
```

在这种情况下，该页面的主题被禁用了。

### 创建你的主题

你会发现，在ASP.NET中创建主题是一个相当简单的过程。主题是跨应用程序应用一致视觉效果的极佳方法。

### 创建正确的文件夹结构

为了为应用程序创建自己的主题，你需要创建正确的文件夹结构。为此，右键点击你的项目并添加新文件夹。将文件夹命名为`App_Themes`。当你这样做时，`App_Themes`文件夹旁边没有典型的文件夹图标，而是一个带有画笔的文件夹图标，如图6-4所示。

在`App_Themes`内部，你可以为你可能使用的每个主题创建一个额外的文件夹。例如，如果你将有四个主题——夏季、秋季、冬季和春天——那么你就创建四个命名相应的文件夹。

由于许多原因，你可能在应用程序中使用多个主题——季节变化、业务部门、用户类别或用户偏好。

每个主题文件夹必须包含主题的元素，包括：

- 单个skin文件
- CSS文件
- 图片

### 创建皮肤（Skin）

皮肤是应用于ASP.NET页面服务器控件的样式定义。皮肤可以与CSS文件或图像配合工作。要为ASP.NET应用程序创建主题，你只需要在主题文件夹中使用单个skin文件。skin文件可以任意命名，但必须具有`.skin`扩展名。

尽管你的应用程序中有四个文件夹，但在本章中，请专注于创建夏季主题。右键点击`Summer`文件夹，选择添加新建项，并在列表中选择皮肤文件。将文件命名为`Summer.skin`。然后按照列表6-3所示完成皮肤。

### 列表6-3 Summer.skin文件

```asp
<asp:Label runat="server" ForeColor="#004000" Font-Names="Verdana"
-Size="X-Small" />
<asp:TextBox runat="server" ForeColor="#004000" Font-Names="Verdana"
-Size="X-Small" BorderStyle="Solid" BorderWidth="1px"
Border="#004000" Font-Bold="True" />
```

```asp
<asp:Button runat="server" ForeColor="#004000" FontName="Verdana"
FontSize="X-Small" BorderStyle="Solid" BorderWidth="1px"
BorderColor="#004000" FontBold="True" BackColor="#FF0000" />
```

### 创建您自己的主题

这段代码只是`Summer.skin`文件的一个示例。要在实际应用程序中使用它，您应该为每一个服务器控件创建一个定义。在这种情况下，你有三个地方可以放置不同类型的服务器控件定义：Summer、Label、Textbox和Button。当您将`Summer.skin`文件保存到文件夹中后，您的结构应该像Visual Studio 2010解决方案资源管理器中的图6所示。

与您放在.asp页面中的普通服务器控件定义一样，这些控件必须包含`runat="server"`属性。如果你在控件的皮肤化（skinned）版本中指定了此属性，你就可以将其包含在使用了此主题的.asp页面上的服务器控件中。请注意，皮肤化版本的控件不需要`id`属性。如果你包含了它，在尝试使用此主题时会报错。

如你所见，你可以为这三个控件提供许多视觉定义，这些定义将赋予页面夏日风的视觉效果和感受。该项目中的ASP.NET页面可以使用此自定义主题，正如本章稍些所示（参见代码列表6-4）。

![](img/7040c21013b8e6c23c612d6da3599ff8_282_0.png)

图6-5

### 代码列表6-4：在ASP.NET页面中使用Summer主题

```asp
<@ Page runat="server" %>
<script>
Protected Sub Button1_Click(sender As Object, ByVal e As System.EventArgs)
Label1.Text = "Hello &" + TextBox1.Text
End Sub
</script>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<head runat="server" />
<title>St. Louis .NET User Group</title>
</head>
<<body>
<form id="form" runat="server">
<asp:TextBox ID="Textbox1" runat="server" />
</asp:TextBox>
<br />
<br />
<asp:Button ID="Button1" runat="server" Text="Submit Your Query"
OnClick="Button1_Click" />
<br />
<br />
<br />
<asp:Label ID="Label1" runat="server" />
</form>
</</body>>
</html>
```

### 代码列表6-4（续）

```csharp
<% Page Language="C#" Theme="Summer" %>
<script runat="server">
    protected void Button1_Click(object sender, System.EventArgs e) {
        Label1.Text = "Hello " + TextBox1.Text.ToString();
    }
</script>
```
