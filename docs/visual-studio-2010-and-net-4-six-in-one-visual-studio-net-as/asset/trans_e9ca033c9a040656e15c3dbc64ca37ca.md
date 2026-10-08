

# 列表 16-15 (续)

```csharp
// 设置 Ajax 事件处理
Chart1.Click += new ImageMapEventHandler(Chart1.Click);
foreach (Series series in this.Chart1.Series)
{
    series.PostBackValue = "Series: " + series.Name +
}
```

```csharp
protected void Chart1_Click(object sender, ImageEventArgs e)
{
    Chart1.Titles["MessageTitle"].Text = "Nothing";
    string[] input = e.PostBackValue.Split(',');
    if (input.Length == 2)
    {
        string[] seriesData = input[0].Split(',');
        if (input[0].Equals("Chart"))
        {
            Chart1.Titles["MessageTitle"].Text = "Last Clicked Element: " + 
                seriesData[0] + " #" + seriesData[1];
        }
        else if (input[0].Equals("Chart"))
        {
            var hit = this.Chart1.HitTest(
                Int32.Parse(seriesData[0]),
                Int32.Parse(seriesData[1]));
            if (hit == null)
            {
                Chart1.Titles["MessageTitle"].Text = 
                    "Last Clicked Element: " + hit.ChartElementType.ToString();
            }
        }
    }
}
```

在 `Page_Load` 方法使用 `DataBindCrossTable` 方法添加数据点后，它通过以下步骤设置了 Ajax 事件处理：

- 1. 订阅 `Chart1_Click` 事件处理方法。
- 2. 设置每个系列的回传值（postback values），发送系列名称和索引。
- 3. 将图表的 `onClick` 事件设置为回传，并在其参数中使用 `_getCoord` JavaScript 函数。
- 4. 将 `_getCoord` JavaScript 函数注入到页面脚本中。

由于这些设置，结果如下：

如果点击了数据点，`PostBackMessage` 将包含系列名称和数据点编号。如果点击了其他图表元素，`PostBackMessage` 将处理其坐标。在这种情况下，`HitTest` 方法会告诉命中了哪个图表元素。

最后，图表在服务器端进行更新，封装在 `UpdatePanel` 中的图表控件被异步设置回。在浏览器端，代表图表的图像被更新，而页面的其他部分（即 HTML 文档的其他部分）保持不变。

> 当你运行示例时，打开页面的源代码。你可以看到图表的 onClick 事件（在代表图表的 <img> 标签中）、`_getCoord` 函数，以及 `<area>` 标签带有相应回传值的 `_doPostBack` 调用。

# 触发图表事件

默认情况下，`UpdatePanel` 内部的任何回传控件都会导致异步回传并刷新面板。然而，你也可以配置页面上的其他控件来刷新 `UpdatePanel` 控件。

这种机制（控件触发）对于图表非常有用。点击 `Chart` 控件中的数据点或标签可以触发页面的其他部分——例如，它可以刷新一个表格，告知你所点击的数据点。

`PetShopCharts` 项目中的 `AjaxTriggerSample` 页面利用这种机制显示两个相关的图表。第一个堆叠柱状图显示了 2009 年销售统计的详情，数据按区域组织。当你点击此图表中的任何数据点时，第二个图表将通过触发器异步更新，显示详细的钻取。图 16-16 显示了这些图表的操作。

![](img/b5597c749e848b27b0d305153ae16106_743_0.png)

图 16-16：AjaxTriggerSample 页面的图表

要实现图 16-16 中所示的结果，你必须将第二个图表封装在 UpdatePanel 中并为其定义一个 `AsyncPostBackTrigger`，如列表 16-16 所示。为了可读性，省略了图表控件的细节。

# 列表 16-16: AjaxTriggerSample.aspx

```aspx
<%@ Language="C#" AutoEventWireup="true"
Behind="AjaxTriggerSample.aspx.cs"
Inherits="PetShopCharts.AjaxTriggerSample" %>

<!DOCTYPE html PUBLIC "//W3C//DTD HTML 1.0 Transitional//EN"
"http://www.w3.org/TR/html1/DTD/html1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>AJAX trigger sample</title>
</head>
```

```html
<<body>
  <form id="form1" runat="server">
    <div>
      <asp:ScriptManager ID="ScriptManager1" runat="server" />
      <asp:Chart ID="Chart1" runat="server" OnClick="Chart1_Click" ...>
        <!-- Chart details omitted -->
      </asp:Chart>
      <br />
      <br />
      <br />
      <asp:UpdatePanel ID="UpdatePanel1" runat="server">
        <ContentTemplate>
          <asp:Chart ID="Chart2" runat="server" BackColor="LightSkyBlue" ...>
            <!-- Chart details omitted -->
          </asp:Chart>
        </ContentTemplate>
        <Triggers>
          <asp:AsyncPostTrigger ControlID="Chart1" />
        </Triggers>
      </asp:UpdatePanel>
    </div>
  </form>
</body>
```

代码文件 [AjaxTriggerSample.aspx] 可在 Wrox 下载。在 UpdatePanel 控件的 `<Triggers>` 元素中定义的 `AsyncPostTrigger` 的 `ControlID` 属性。页面的后台代码（在列表 16-17 中）显示了 Chart 如何触发 Chart2 的更新![](img/b5597c749e848b27b0d305153ae16106_744_0.png)

# 列表 16-17: AjaxTriggerSample.aspx

```csharp
using System;
using System.Data;
using System.Data.OleDb;
using System.Web.UI.WebControls;
using System.Web.UI.ChartControls;

namespace PetShopCharts
{
    public partial class AjaxTriggerSample : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            var connection = Helpers.Utility.GetDataConnection(this);
            var commandStr = "SELECT Region, KindName, Total from SalesByAndRegion where Year=2009";
            var command = new OleDbCommand(commandStr, connection);
            connection.Open();
            var reader = command.ExecuteReader(CommandBehavior.Close);
        }
    }
}
```

# 列表 16-17 (续)

```csharp
protected void Chart_Click(object sender, ImageEventArgs e)
{
    var pars = e.PostBackValue.Split(',');
    var connection = Helpers.GetDataConnection(this);
    var commandStr = "SELECT Shopname, Total from AccumulatedSales where Year=2009 and Kindname='" + pars[0] + "' and Region='" + pars[1] + "'";
    var command = new OleDbCommand(commandStr, connection);
    command.Connection.Open();
    var reader = command.ExecuteReader(CommandBehavior.Close);
    Chart2.DataBindCrossTable(reader, "Shopname", "Total", "");
    reader.Close();
    connection.Close();
    foreach (var series in Chart2.Series)
    {
        series.ChartType = SeriesType.Column;
        series.ToolTip = "#AXISABEL sold by " + series.Name + " :VALD";
    }

    Chart1.DataBindCrossTable(reader, "Region", "Kindname", "");
    reader.Close();
    connection.Close();
    foreach (var series in Chart1.Series)
    {
        series.ChartType = SeriesType.StackedColumn;
        series.CustomProperties = "DrawingStyle";
        series.IsValueLabel = true;
        series.PostBackValue = "#AXISABEL" + series.Name;
        series.ToolTip = "#AXISABEL sold in " + series.Name + " :VALD";
    }
}
```
> 代码文件 [AjaxTriggerSample.aspx] 可在 Wrox 下载。

Page_Load 事件使用 DataTable 方法为每个区域创建系列。随后的 foreach 循环负责设置系列的视觉属性和 PostBackValue，这是该场景的关键。当你注释掉这一行并运行示例时，由于回传的发生，PostBackValue 触发了渲染脚本：

```csharp
series.PostBackValue = "#AXISABEL" + series.Name;
``````

# 实时图表

Ajax 的异步特性非常适合显示实时图表，在这种场景下，数据会被定期查询，图表会定期用新数据更新。PetShopCharts 项目中的 `AjaxRealTimeSample` 页面演示了这种场景。

页面包含一个显示虚拟指数股票交易所数据的图表，因此信息每秒刷新一次。图 16-17 显示了多次异步刷新后的图表。

![](img/b5597c749e848b27b0d305153ae16106_746_0.png)

图 16-17：多次刷新后的实时图表

