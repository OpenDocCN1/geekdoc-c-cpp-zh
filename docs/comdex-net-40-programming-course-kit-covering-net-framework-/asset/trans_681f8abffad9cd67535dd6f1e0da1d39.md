

```aspx
<asp:GridView BackColor="#FFFFFF" ForeColor="#330099"
              HorizontalAlign="Center" />
<RowStyle BackColor="White" ForeColor="#330099" />
<SelectedRowStyle BackColor="#F6FCC6" Font-Bold="True" ForeColor="#663399" />
<SortedAscendingCellStyle BackColor="#FFEFBE" />
<SortedAscendingHeaderStyle BackColor="#AF0101" />
<SortedDescendingCellStyle BackColor="#F6F0C0" />
<SortedDescendingHeaderStyle BackColor="#7E0000" />
</asp:GridView>
```

在前面的清单中，我们已将 GridView 控件添加到 Default.aspx 页面。

- 22. 在 **Default.aspx** 文件的代码隐藏文件（**Default.aspx.cs** 文件）中编写清单 10.8 所示的代码：

### 清单 10.8：Default.aspx.cs 文件的代码

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using ServiceReference1;
public partial class _Default : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        NORTHWNDEntities svc = new NORTHWNDEntities(new
            Uri("http://localhost:9368/DataService/WcfDataService.svc/"));
        GridView1.DataSource = svc.Customers;
        GridView1.DataBind();
    }
}
```

在前面的清单中，NORTHWND 数据库通过 **WcfDataService.svc** 数据服务的 URL 绑定到 **GridView** 控件。

- 23. 按 F5 键运行应用程序。输出如图 ASP-10.42 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_693_0.png)

图 ASP-10.42

现在让我们总结本章讨论的主要主题。

### 小结

在本章中，你学习了创建 Web 服务和 WCF 服务。你还学习了如何在 ASP.NET 4.0 的客户端应用程序中使用这些服务。接下来，本章讨论了新的 WCF 数据服务功能以及如何创建 WCF 数据服务。

在下一章中，你将了解 Silverlight 4.0，它用于创建丰富的交互式 Web 应用程序。

## Silverlight 4.0 简介

### 第 11 章

### 本章内容：

- 探索 Silverlight 的关键功能
- 探索 Silverlight 4.0 的新功能
- 解释 Silverlight 体系结构
- 安装 Silverlight 4.0 工具
- Silverlight 应用程序中的程序集和文件
- Silverlight 应用程序中使用的控件
- 开发 Silverlight 应用程序

在 Web 开发的初期，**超文本标记语言（HTML）**被用于创建网站。这些网站的网页内容主要是静态的。随着时间推移，新的脚本语言（例如**可扩展超文本标记语言（XHTML）**和 JavaScript）以及新技术（例如层叠样式表（CSS）和 Adobe Flash）被引入。这些新语言和技术帮助 Web 开发人员创建交互式网站。然而，其中一些技术在 Web 服务器上部署成本高昂，并且它们在不同平台上的性能也有所差异。为了解决这些问题，Microsoft 推出了 **Silverlight**。

Silverlight 是一种用于创建网站的技术，这些网站可以具有高分辨率多媒体内容和引人注目的视觉效果，进而为你的网站提供吸引人的外观和感觉。它随 .NET Framework 一起发布，并与多种浏览器、设备和操作系统兼容；因此，你可以创建交互式网站。

Microsoft 发布的第一个 Silverlight 版本是 Silverlight 1.0。该版本于 2007 年发布，基于 JavaScript 应用程序模型。2008 年 10 月，名为 Silverlight 2.0 的 Silverlight 1.0 升级版发布，它受 Visual Studio 2008 Service Pack 1（SP1）支持。之后，Silverlight 2.0 的升级版发布，命名为 Silverlight 3.0，它受 Visual Studio 2010 支持。Silverlight 的最新版本是 Silverlight 4.0，它也受到 Visual Studio 2010 的完全支持。

在本章中，你将了解 Silverlight 的各种功能，包括 Silverlight 4.0 中引入的新功能。接下来，你将了解 Silverlight 4.0 的体系结构。进一步，你将了解如何在系统上安装 Silverlight 4.0 工具。你还将了解 Silverlight 4.0 中可用的不同控件。最后，你将学习使用新控件在 Silverlight 中开发应用程序。

让我们从讨论 Silverlight 的关键功能开始。

### 探索 Silverlight 的关键功能

Silverlight 以前称为 WPF/E，是 Windows Presentation Foundation（WPF）的子集，并继承了 WPF 的许多功能。例如，Silverlight 支持可扩展应用程序标记语言（XAML）、二维（2D）矢量图形、动画和多媒体。Silverlight 应用程序可以在多种 Web 浏览器中运行。Silverlight 提供多种功能，帮助 Web 开发人员和设计人员构建交互式网站。Silverlight 的主要功能如下：

- 由 .NET 编程模型支持
- 全面的用户界面（UI）框架
- 支持 Deep Zoom 技术
- 支持三维（3D）图形、动画和多媒体
- 支持网络连接
- 支持更高质量的视频和音频
- 浏览器外功能

现在，让我们详细讨论这些功能中的每一项。

### 由 .NET 编程模型支持

Silverlight 由 .NET Framework 编程模型支持，并且还从 .NET Framework 继承了类型安全和异常处理等功能。因此，你可以使用任何 .NET 语言（例如 Visual Basic 和 C#）轻松开发 Silverlight 应用程序。它还包括 .NET Framework 基类库中的许多类，使你能够处理输入/输出（I/O）操作、集合和泛型。Silverlight 还支持语言集成查询（LINQ），使你能够处理各种类型的数据源，例如网站中的结构化查询语言（SQL）数据库和可扩展标记语言（XML）文件。

### 全面的 UI 框架

Silverlight 具有全面的 UI 框架，其中包含预定义控件、布局、样式、主题和模板，可帮助你构建交互式网站以及有吸引力的网站。如果现有控件和样式集不能满足你的需求，你还可以在 Silverlight 应用程序中使用自定义样式和控件模板。这反过来有助于使你的网站更加用户友好。数据绑定和数据操作控件（例如 **DataGrid**）也可以用在 Silverlight 网站中，以便从数据库中检索和存储数据。

### 支持 Deep Zoom 技术

Silverlight 包含对一种称为 Deep Zoom 的技术的支持，该技术允许你在网站中缩放高分辨率图像。借助 Deep Zoom 技术，你可以轻松地同时放大或缩小多张图像。该技术只下载正在查看的区域，从而减少初始加载所需的时间。它还允许你同时查看数千张图像。

### 支持 3D 图形、动画和多媒体

Silverlight 具有对 2D 矢量图形和动画的内置支持。此外，它还允许你创建、变换和动画化 2D 形状。然而，随着 Silverlight 3.0 的发布，你可以执行透视 3D 变换，以创建包含新 3D 图形、动画功能和硬件加速效果的更具吸引力的 Web 视觉效果。透视变换是你可应用于可扩展应用程序标记语言（XAML）元素以模拟 3D 环境的变换。你可以通过在父元素内使用名为 Projection 的附加属性，将 3D 效果应用于 Silverlight 应用程序中的控件。请考虑以下代码片段：

```xml
<Button Height="90" Content="Perspective Transform">
<Button.Projection>
<PlaneProjection RotationY="60"/>
</Button.Projection>
</Button>
```

在前面的代码片段中，Button 控件被旋转以呈现透视效果，在 Y 轴上旋转 60 度。

此外，你可以通过使用故事板并控制动画时间线和速度，使你的网站具有动态效果。为此，你可以在网站中包含 .jpeg 或 .png 扩展名的图像。Silverlight 还支持多种多媒体格式，例如 .wma、.wmv 和 .mp3，以便在网站上播放多媒体内容。你还可以在 Silverlight 应用程序中使用高清（HD）质量视频（最高 720p）。

![](img/9862a98a1a2d3bb14334137965a1ec60_696_0.png)

> **矢量图形是用于表示几何图像的形状和绘图，例如点、线、曲线和多边形。**

### 支持网络连接

Silverlight 包含支持网络连接和预定义套接字的类。它允许你使用各种服务（例如超文本传输协议（HTTP）、XML、简易信息聚合（RSS）和表述性状态转移（REST））来开发分布式应用程序。Silverlight 扩展了网络连接的跨域支持，以便与服务器进行通信。

### 支持更高质量的视频和音频

Silverlight 支持高质量的视频和音频。它支持新的音频和视频格式，例如 H.264、高级音频编码（AAC）和运动图像专家组（MPEG）4。此外，它还包括对实时和按需 Internet Information Services（IIS）7 平滑流式处理、全高清（720+）播放以及原始音频或视频（AV）管道的支持。原始 AV 管道使 .NET 开发人员能够提供可在 .NET Framework 运行时环境之外托管的音频/视频解码。

### 浏览器外功能

浏览器外功能最早随 Silverlight 3.0 引入，使 Silverlight 应用程序能够在 Web 浏览器内或浏览器外运行。这意味着你可以安装一个 Silverlight

