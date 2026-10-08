

# 列表 16-8: DogSalChart.aspx

![](img/b5597c749e848b27b0d305153ae16106_726_0.png)

```
<@ Page Language="C#" AutoEventWireup="true" CodeBehind="DogSalChart.aspx.cs"
Inherits="PetShopCharts.DogSalChartData" %>
<asp:chart id="Chart1" server="server" height="500" width="800"
rendertype="BinaryStreaming" BackColor="Khaki" BackGradientStyle="DiagonalLeft"
BackSecondaryColor="DarkGoldenrod">
<asp:ChartArea>
<asp:Axis TitleName="Sales" Number="True" Font="Calibri, 14.25pt; style=bold"
MinimumGrid="True" Interval="100" LineColor="Silver" />
</asp:Axis>
<asp:AxisX Interval="*1" IsLabelFit="False" LabelAutoFitFontSize="12">
<asp:MajorGrid LineColor="Silver" />
<asp:LabelStyle Font="Calibri, 12pt; style=bold" />
</asp:AxisX>
</asp:ChartArea>
</asp:chart>
<asp:Legend>
<asp:Legend BackColor="Papawhip" BorderColor="DimGray"
DockedToChartArea="ChartArea" Name="Legend1"/>
</asp:Legend>
</asp:chart>
```

可以在 Wrox.com 下载代码文件 [DogSalChart.aspx]。

如你所见，此图表不包含任何 HTML 元素，只有 `<asp:chart>` 元素。坦率地说，设计器仍然支持所有的图表属性，就像它们嵌入在普通的 .aspx 页面中一样。图表的 `RenderType`设置为 `BinaryStreaming`。
DogSalChart.aspx 包含了使用 `DataBindCrossTable` 方法操作图表的逻辑，使用了与列表 16-6 所示相同的模式。通过以下代码提取指定区域的销售查询：

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    var region = Request["region"];
    var connection = Helpers.Utility.GetDataConnection(this);
    var commandStr = "SELECT Name, Total, ShopName from DogSalChart data where " +
    " Region = '" + region + '\';";
    var command = new OleDbCommand(commandStr, connection);
    //
```

列表 16-9 显示了引用 DogSalChart.aspx 的 BinaryStreamRendering.aspx 文件。

# 列表 16-9: BinaryStreamRendering.aspx

![](img/b5597c749e848b27b0d305153ae16106_727_0.png)

```asp
<%@ Page Language="C#" AutoEventWireup="true"
CodeBehind="BinaryStreamRendering.aspx.cs"
Inherits="PetShopCharts.BinaryStreamRendering">

<!DOCTYPE type HTML HTML 1.0 Transitional//EN//
"http://www.w3.org/TR/html1/DTD-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head>
  <meta charset="utf-8">
  <title>通过二进制流渲染的销售数据</title>
</head>
<body>
  <form id="form1" runat="server">
  <table>
    <tr>
      <td>
        <h2>西部地区的狗狗销售情况</h2>
        <asp:Image Id="ImageWest"
               ImageUrl="DogSalesChart.aspx?region=West"
               runat="server" Height="500px" Width="800px" />
      </td>
    </tr>
    <tr>
      <td>
        <h4 id="h4">东部地区的狗狗销售情况</h4>
        <asp:Image Id="ImageEast"
               ImageUrl="DogSalesChart.aspx?region=East"
               runat="server" Height="250px" Width="400px" />
      </td>
    </tr>
    <tr>
      <td>
        <h4 id="h4">北部地区的狗狗销售情况</h4>
        <asp:Image Id="ImageNorth"
               ImageUrl="DogSalesChart.aspx?region=North"
               runat="server" Height="250px" Width="400px" />
      </td>
    </tr>
  </table>
  </form>
</body>
</html>
```

> 可以在 Wrox.com 下载代码文件 [BinaryStreamRendering.aspx]。此文件包含三个引用 DogSalesChart.aspx 的 `<asp:Image>` 元素，具有三个区域设置。当然你可以设置 Image 元素的任何参数。第二个和第三个图像显示原始图像的一半大小。图 16-9 显示了你在浏览器中看到的 BinaryStreamRendering.aspx 页面。

# 西部地区的狗狗销售情况

![](img/b5597c749e848b27b0d305153ae16106_728_0.png)

东部地区的狗狗销售情况

北部地区的狗狗销售情况

![](img/b5597c749e848b27b0d305153ae1610.png)

**图 16-9:** 二进制渲染嵌入的图表

二进制流渲染是将图表嵌入旧版网站的另一种解决方案。你不需要触碰 .aspx 页面。使用 `<img>` 标签创建引用页面。

**列表 16-10:** BinaryStreamRendering.htm

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 1.0 Transitional//EN"
"http://www.w3.org/TR/html1/transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
  <title>旧版站点中的二进制流渲染图表</title>
</head>
<body>
  <h2>南部地区的狗狗销售情况</h2>
  <img src="DogSalesChart.aspx?region=South" height="500px" width="800px" alt="Southern Region" />
</body>
</html>
```
可以在 Wrox.com 下载代码文件 [BinaryStreamRendering.htm]

# 图表管理

ViewState 框架自动保存渲染页面及其控件的值，状态管理通过状态实现。当处理 ASP.NET 页面时，页面及其控件的当前状态转换为字符串并保存到名为 `__VIEWSTATE` 的隐藏字段中。

图表通常从文件或数据库获取数据，且状态并不一定存储在视图中。默认情况下，图表不使用视图状态。其 `EnableViewState` 属性设置为 `false`。

然而，在某些情况下使用状态性能更好。如果你预计图表页面会有多次回传且图表数据容易复制，状态可以帮助节省系统资源并提供更好的响应时间。当你动态创建图表时，可以从状态中受益。

使用状态时，应考虑从服务器到客户端的数据量。使用状态会导致网络流量少量增加，而使用数百或数千个数据点会导致网络流量大幅增加。

本节检查几个图表示例以演示状态管理。

# 保存图表状态

当你处理生成成本较高的图表数据并预计页面会有回传时，在回传之间持久化数据的可能方法是启用状态管理。PetShopCharts 项目中有一个代表此场景的示例。

BasicChartStateManagement.aspx 页面在 `Page_Load` 方法中生成随机系列。页面包含两个复选框，允许你在勾选或取消选择时立即向图表添加或移除上下曲线。每当你更改任何复选框控件的 `Checked` 属性时，就会发生回传。如果你无法在回传之间保存图表状态，就会丢失 `Page_Load` 方法中生成的系列。

列表 16-11 显示了页面的后台代码文件，允许你将系列信息存储在页面的视图状态中

![](img/b5597c749e848b27b0d305153ae16106_729_0.png)

图 16-10: BasicChartStateManagement.aspx 上的随机系列

# 列表 16-11: BasicChartManagement.aspx.cs

![](img/b5597c749e848b27b0d305153ae16106_730_0.png)

```csharp
using System;
using System.Web.UI.DataVisualization.Charting;

namespace PetShopCharts
{
    public partial class BasicChartStateManagement : System.Web.UI.Page
    {
        protected void Form_Init(object sender, EventArgs e)
        {
            Chart1.EnableViewState = true;
        }
    }

    protected void Page_Load(object sender, EventArgs e)
    {
        if (IsPostBack)
            GenerateRandomData(Chart1.Series[0]);
        if (UpperSpline.Checked)
            AddNewSeries("UpperSpline", 5.0);
        else RemoveSeries("UpperSpline");
        if (LowerSpline.Checked)
            AddNewSeries("LowerSpline", -5.0);
        else RemoveSeries("LowerSpline");
    }
```

