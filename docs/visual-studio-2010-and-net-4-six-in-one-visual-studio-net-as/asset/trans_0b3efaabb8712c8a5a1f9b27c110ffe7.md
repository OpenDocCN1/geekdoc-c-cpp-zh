

在本章中，你将学习 ASP.NET Chart 控件的具体特性和行为：

- 创建图表 — 你将学习创建 ASP.NET 图表的基本步骤、处理回传（postback）事件以及将你的数据绑定到图表上。

- 渲染 ASP.NET 图表 — 尽管在使用 Windows Forms 图表时，你不需要处理它们的渲染，但由于 Web 应用程序的分布式特性，对于 ASP.NET 图表，你有多个渲染选项。你将在本章中学习这些选项。

- 图表状态管理 — 状态管理是所有 Web 应用程序的基础概念。在本章中，你将学习 ASP.NET Chart 如何实现这一概念。

- 用户交互性 — 图表本身“仅仅”是一个向你传达千言万语之的静态图形。为图表添加交互性可以提高客户在查看数据时的用户体验。在本章中，你将发现如何使用 ASP.NET Chart 为用户提供交互性。

> 在本章中，你将构建并分析简单的 ASP.NET Web Application 项目。本章中的模拟代码示例可以在 PetShopCharts .NET 程序中找到。你可以从书籍的下载网站 www.itext.com 下载源代码文件。重点是 ASP.NET Chart 控件，而不是通用的 ASP.NET 开发。你不需要在计算机上安装 Internet 信息服务 (IIS)。所有示例均适用于 Visual Studio 2010 安装的 ASP.NET 开发服务器。即使你是一个新手 Web 开发者，也能构建这些示例。

## 创建图表

第 14 章研究了有关 Windows Forms Chart 控件创建和使用的许多细节，并讨论了如何使用它们创建简单的应用程序。尽管 ASP.NET Chart 与 Windows Forms 控件共享相同的概念，但由于 Web 的分布式特性，在 Web 中创建图表时必须遵循不同的指南。在本节中，你将创建几个示例来学习如何在 ASP.NET 中启动图表。

## 在页面上添加图表

创建一个新的 ASP.NET Empty Web Application 并命名为 SimpleAspNetChart。添加一个名为 Default.aspx 的新 Form 项。它将成为应用程序的默认启动页。点击文档窗口底部的 Chart 标签使用 Default.aspx 的 Source 视图 — 除非你尚未处于此视图。在工具箱（Toolbox）上，展开 Data 选项卡，拖入 Chart 控件并将其放置在 `<div>` 和 `</div>` HTML 标签之间。Chart会自动创建 Series 和 ChartArea 元素，如列表 16-1 所示。

### 列表 16-1：添加 控件后的 Default.aspx

```csharp
<@ Language="C*" AutoEventWireup="true" CodeBehind="Default.aspx.cs" Inherits="SimpleAspNetChart.Default" %>

<%@ Register assembly="System.Web.Visualization, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856d364e35" namespace="System.Web.DataVisualization.Charting" tagprefix="asp" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>title</title>
</head>
<body>
<form id="form">
    <div>
        <asp:Chart ID="Chart1" runat="server">
            <Series>
                <asp:Series Name="Series1">
                </asp:Series>
            </Series>
            <ChartAreas>
                <asp:ChartArea Name="ChartArea1">
                </asp:ChartArea>
            </ChartAreas>
        </asp:Chart>
    </div>
</form>
</body>
</html>
```

`<Register>` 指令显示 Chart 控件可以在 System.Web.DataVisualization 程序程序集中找到。

当切换到 Design 视图时，可以看到图表的示例数据。但当你运行应用程序时，会显示一个空图表。你可以通过在 Series Collection Editor 中编辑 Series1 的 Points 属性在 Design 视图中向图表添加数据点，或者在 Source 视图中手动输入数据点。

```csharp
<asp:Chart ID="Chart1" runat="server" Width="490px">
    <Series>
        <asp:Series Name="Series1">
            <Points>
                <asp:DataPoint XValue="0" YValues="15" />
                <asp:DataPoint XValue="1" YValues="20" />
                <asp:DataPoint XValue="2" YValues="28" />
                <asp:DataPoint XValue="3" YValues="13" />
                <asp:DataPoint XValue="4" YValues="7" />
            </Points>
        </asp:Series>
    </Series>
    <ChartAreas>
        <asp:ChartArea Name="ChartArea1" />
    </ChartAreas>
</asp:Chart>
```

现在，当你运行应用程序时，你可以看到一个包含五个数据点的图表，如图 16-1 所示。

![](img/b5597c749e848b27b0d305153ae16106_713_0.png)

图 16-1：带有五个数据点的简单 Chart 控件

> 你可以像在 Windows Forms 控件中完全一样在 ASP.NET Chart 控件中设置数据点。在 Design 视图中选择 ASP.NET Chart 控件，在属性窗口中滚动到 Series 属性，找到 Series 编辑器并设置 Points。你也可以通过代码设置数据点，如列表 16-2 所示。你还可以在 Page_Load 事件中执行初始化，设置 ASP.NET Chart 标题和 Series。

### 列表 16-2：Default.aspx.cs 代码

```csharp
using System;
using System.Drawing;
using System.Web.UI;
using System.DataVisualization.Charting;

namespace SimpleAspNetChart
{
    public partial class Default : System.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            // 设置图表标题
            var title = new Title("This is ASP.NET Chart");
            title.Font = new Font("Calibri", 24, FontStyle.Bold);
            Chart1.Titles.Add(title);

            // 设置图表类型
            var series1 = Chart1.Series[0];
            series1.Points.Clear();
            series1.ChartType = ChartType.Spline;

            // 创建数据点
            for (int i = 0; i <= 10; i++)
            {
                series1.Points.Add(new DataPoint(i, Math.Pow(i, 2)));
            }
        }
    }
}
```

ASP.NET Chart 和所有相关类型可以在 System.Web.DataVisualization 命名空间中找到。

## 在事件方法中设置图表

与其他控件一样，图表可以在事件方法中设置。让我们更改列表 16-2 中的公式，以便指定显示的点数量和 Math.Pow 函数使用的指数。列表 16-3 显示了如何更改 Default.aspx 文件以更新参数。

![](img/b5597c749e848b27b0d305153ae16106_715_0.png)

图 16-2：在后台代码中初始化的图表

