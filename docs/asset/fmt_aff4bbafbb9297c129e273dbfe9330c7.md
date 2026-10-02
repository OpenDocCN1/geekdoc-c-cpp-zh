
# 列表 23-22（续）

```asp
Protected Sub Button1_Click(ByVal sender As Object, ByVal e As EventArgs)
    Label.Text = "Hello &" & TextBox1.Text & "<br /> & Today is &" & TextBox2.Text
End Sub
</script>
<!DOCTYPE html>
<html>
<head>
    <run runat="server">
        <title>Script Combining</title>
    </run>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <asp:ScriptManager id="ScriptManager1" runat="server">
            </asp:ScriptManager>
            <asp:UpdatePanel id="UpdatePanel1" runat="server">
                <ContentTemplate>
                    What is your name?<br />
                    <asp:TextBox id="TextBox1" runat="server"></asp:TextBox>
                    <br />
                    <br />
                    What is today&#39;s date?<br />
                    <asp:TextBox id="TextBox2" runat="server"></asp:TextBox>
                    <asp:CalendarExtender id="CalendarExtender" runat="server" />
                </ContentTemplate>
            </asp:UpdatePanel>
```

# 列表 23-22（续）

```asp
<asp:CalendarExtender>
<br />
<br />
<asp:Button id="Button1" runat="server" Text="Submit" OnClick="Button1_Click" />
<br />
<br />
<asp:Label id="Label1" runat="server"></asp:Label>
</asp:UpdatePanel>
</form>
</body>
</html>
```

# C# 示例

```csharp
<%@ Page Language="C#" %>
<%@ Register Assembly="ScriptReferenceProfiler" TagPrefix="ccl" %>
<%@ Register Assembly="AjaxControlToolkit" TagPrefix="asp" %>
<script runat="server">
    protected void Button1_Click(object sender, EventArgs args)
    {
        Label1.Text = "Hello " + TextBox1.Text + "<br /> today is " + TextBox2.Text;
    }
</script>
```

这个简单的页面使用了 ASP.NET 来根据用户输入合并脚本。此页面顶部的包含了一些指令。

![](img/67a6707ff505c052edb96c0128fb3096_939_0.png)

图 23-17

运行此页面，你可以看到如图 23-16 所示的返回按钮选项列表。你还可以导航回此项目（或者如果需要，也可以向后），你将返回之前正在操作的页面。为了完成此任务，将提供的脚本粘贴到 `ScriptManager` 区域中。

# 列表 23-23 (续)

```xml
<Scripts>
</CompositeScript>
<asp:ScriptManager ID="UpdatePanel1" runat="server">
<asp:UpdatePanelTemplate>
  <ContentTemplate>
    What is your name?<br />
    <asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
    <br /> <br />
    What is today's date?<br />
    <asp:TextBox ID="TextBox2" runat="server"></asp:TextBox>
    <asp:CalendarExtender ID="TextBox2Extender" runat="server"
      Enabled="True" TargetControlID="Textbox2">
    </asp:CalendarExtender>
    <br /> <br />
    <asp:Button ID="Button1" runat="server" Text="Submit"
    <br /> <br />
    <asp:Label ID="Label" runat="server"></asp:Label>
  </ContentTemplate>
</asp:UpdatePanel>
</div
</form>
</body>
</html>
```

在 `<CompositeScript>` 部分中定义所有这些脚本，现在意味着所有这些脚本将被合并并一起发送到页面，从而提高您的 ASP.NET 应用程序的整体性能。

# ASP.NET AJAX 的未来

随着微软采用 jQuery JavaScript 库（将在第 25 节中介绍），ASP.NET AJAX 可能不会获得任何新功能，但由于它是 ASP.NET 的一部分，它仍然享有微软的支持。因此，只要 ASP.NET 受到支持，对 ASP.NET AJAX 特性的使用将获得支持。微软将对代码或功能进行升级，这非常独特。特别是对于遗留应用程序，我们并不认为 ASP.NET AJAX 需要被丢弃；然而，对于新应用程序，我们建议至少评估 jQuery 是否符合您的需求。

## 总结

Ajax 从根本上改变了 Web 应用程序开发方法。ASP.NET AJAX 是一个优秀的框架，它在 ASP.NET 网站的范围内促进了多种 AJAX 功能，包括部分页面更新。您不需要为每一个请求都完全拆除并重建页面。相反，您能够根据用户的请求，最终逐步地重建页面。但请注意，微软将进一步支持 ASP.NET AJAX，但可能不会为其添加任何新功能。

本章探讨了 Visual Studio 2012 默认安装的 ASP.NET AJAX 核心基础。除此之外，Ajax 还提供了更多内容，包括下一章的重点——Ajax Control Toolkit.

# 24

# Ajax Control Toolkit

本章包含哪些内容？

- 安装 Ajax Control Toolkit
- 为您的 Web 页面添加交互和动画

WROX. 本章代码下载

请注意，本章中的所有代码示例均作为该书籍网站（www.wrox.com）上“Download Code”（下载代码）选项卡中本章代码下载的一部分提供。

上一节引入了 ASP.NET AJAX 应用程序。您可能会奇怪，考虑到 ASP.NET Web Forms 高度依赖这种代码模块化方式，为什么 ASP.NET AJAX 的服务器控件是如此之少？原因是，微软将它们视为一个开源项目，而不仅仅是将它们整合到 Visual Studio 2012 中。

微软和社区的开发者开发了一系列具备 Ajax 能力的服务器控件，您可以在自己的 ASP.NET 应用程序中使用它们。最初，这些控件被统称为 ASP.NET Ajax Control Toolkit。然而，微软最终对该库进行了了重命名，使其听起来更像 ASP.NET 的一部分。它现在被称为 Ajax Control Toolkit，并托管在 CodePlex http://ajaxcontroltoolkit.codplex.com/ 上。图 24-1 显示了 Ajax Control Toolkit 的下载页面。

正如您从上一节记得的那样，ASP.NET AJAX 是构建 Web 应用程序的基础，允许浏览器更充分地运行，但它缺乏能够真正模糊 Web 和桌面应用程序区别的丰富 UI 元素。ASP.NET AJAX 包含了几个强大的 ASP.NET 控件，使向现有应用程序中添加 Ajax 功能或构建更好的用户体验变得简单。

# 第 24 章 Ajax Control Toolkit

# 第 24 章 AJAX Control Toolkit

4. 点击确定，Ajax Control Toolkit 控件将添加到你的 Visual Studio 工具箱中。
图 24-5 显示了结果。
工具箱中已添加 40 多个控件和扩展器（extenders），供你的 ASP.NET 应用程序使用。

## ASP.NET AJAX 控件

控件工具包提供的控件和扩展器数量很多。事实上，你有超过 40 多个控件和扩展器可供。本节将介绍这些项目以及你如何在 ASP.NET 应用程序中使用它们。

当你向页面添加 ASP.NET AJAX 服务器端控件时，你可能会注意到，若干个关注多种语言本地化的 DLL 已添加到解决方案的 Bin 文件夹中。所有资源文件都已组织到该文件夹内的语言文件夹中。图 24-6 展示了一个示例。

![](img/67a6707ff505c052edb96c0128fb3096_947_0.png)

图 24-5

图 24-6

除了添加到项目的本地化 DLL 之外，ASP.NET AJAX 控件就像 ASP.NET 中其他自定义服务器端控件一样被添加。列表 24-1 显示了在向页面添加单个 ASP.NET AJAX 控件后，你的 ASP.NET 页面应该的样子。

## 列表 24-1：添加 Ajax Control Toolkit 控件后 ASP.NET 页面的变化

```
<@ Page Language="C#" AutoEventWireup="true"
CodeFile="Default.aspx.cs" Inherits="Default" %>
<@ Register Assembly="AjaxControlToolkit"
Namespace="AjaxControlToolkit" TagPrefix="asp" %>
<!DOCTYPE html>
<html
<head runat="server">
<title>First Page</title>
</head>
<body>
<form id="form" runat="server">
<<div>
<asp:ToolkitScriptManager ID="ToolkitManager1" runat="server" />
<asp:AlwaysVisibleControlExtender
ID="AlwaysVisibleControlExtender1" runat="server"
TargetControlID="TextBox1">
</asp:AlwaysVisibleControlExtender>
<asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
</>
</form>
</body>
</html>
```

在此示例中，你可以看到使用 `@Register` 指令在页面上注册了 ASP.NET AJAX 控件。此直接指令指向 `AjaxControlToolkit` 程序集，并为所有引用此程序集的控件提供了 `asp` 标签前缀。Visual Studio 2012 默认会将引用添加到 `web.config`，但为了让我们的代码尽可能自包含，我们将这些引用移动到了本章顶部的 `@Register` 中。

Ajax Control Toolkit 提供的控件中另一个关注点是 `ToolkitScriptManager` 控件（你需要手动添加；Visual Studio 不会自动为你完成）。该控件派生自基 `ScriptManager` 控件并扩展了它，以处理默认的脚本合并，使得你的页面比以前更高效。本章提供的示例使用了此新版本的 `ScriptManager` 控件。

## Ajax Control Toolkit 扩展器 (Extenders)

你查看的第一组项目包含了属于 Ajax Control Toolkit 的控件。扩展器本质上是触达并扩展其他控件的控件。例如，你可以将 ASP.NET 验证控件（在本书第 6 章介绍）视为扩展器控件本身。例如，你可以向页面添加一个 `RequiredFieldValidator` 服务器端控件并将其与 `TextBox` 控件关联。这扩展了 `TextBox` 控件并改变了它的行为。通常情况下它只接受文本。现在，如果控件中没有输入任何内容，控件将触发一个事件回到 `RequiredFieldValidator`，后者的客户端行为由 JavaScript 控制。

Ajax Control Toolkit 的扩展器实现了相同的功能。这些控件通过客户端额外的 JavaScript 以及一些服务器端通信，扩展了 ASP.NET 服务器端控件的行为。

## AlwaysVisibleControlExtender

在浏览器中显示信息时，你可能希望将某些信息固定在用户的视图中。屏幕空间是有限的资源，有时某个屏幕元素应该始终可用，而无需用户滚动。`AlwaysVisibleControlExtender` 允许你指定任何 ASP.NET 控件具有此特性。你使用 `AlwaysVisibleControlExtender` 为控件指定位置，当用户滚动页面查看其他信息时，你指定的控件将保持在视野内。它似乎会随着用户的滚动或调整窗口大小而移动，以便在浏览器部分区域内保持相同的相对位置。

`AlwaysVisibleControlExtender` 只有六个属性。列表 24-2 提供了一个使用控件代码的示例。

## 列表 24-2：使用 AlwaysVisibleControlExtender

VB

```
<@ Page Language="VB" %>
<%@ Register Assembly="AjaxControlToolkit"
Namespace="AjaxControlToolkit" TagPrefix="asp" %>
<script runat="server">
    Protected Sub Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs)
        Response.Write("The page has been submitted!")
End Sub
</script>
<!DOCTYPE html>
<html>
<head>
    <title>AlwaysVisibleControlExtender</title>
</head>
<body>
    <form id="form1" runat="server">
    <div>
        <asp:ToolKitScriptManager Id="ToolKitScriptManager1" runat="server" />
        <asp:AlwaysVisibleControlExtender
        ID="AlwaysVisibleControlExtender1" runat="server"
        TargetControlID="TextBox1"
="10">
</asp:AlwaysVisibleControlExtender>
<asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
    </div>
</form>
</body>
</html>
```

（注：第 949-951 页的 OCR 文本包含大量的碎片化和重复错误。根据 Ajax Control Toolkit 的上下文，文本已经过清理，以反映 `AlwaysVisibleControlExtender` 和 `AnimationExtender` 控件的逻辑结构。）

# ASP.NET AJAX 控制 | 903

Doneet accusam Lorem. Ut consectetuer tempor massa.
Aenean tincidunt venenatis tellus. Suspisse molestie
cursus ipsum Curabitur ut lectus. Nulla eleor nec elit
convallis vulputate. Nullam mauris pulvinar Duis
orci. Phasellus tortor a nunc magnis.
Vestibulum porta tellus eu orci. Suspendisse quis massa.
Maecenas, erat non ullamcorper nonummy, mauris erat
elif odio, ut gravida nisi neque ipsum. Vivamus
facilisis. Cras viverra. Curabitur ut augue eget dolor
semper posuere. Aenean mauris
```

</Panel>
