
# LISTING 16-15 (continued)

```csharp
// Set up Ajax event handling
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

After the `Page_Load` method adds data points using the `DataBindCrossTable` method, it sets up Ajax event handling with the following steps:

- 1. Subscribes to the `Chart1_Click` event handler method.
- 2. Sets the postback values of each series sending the series name and index.
- 3. Sets the Chart's `onClick` event to a postback using the `_getCoord` JavaScript function in its arguments.
- 4. Injects the `_getCoord` JavaScript function into the scripts of the page.

As a result of this setup:

If a data point was clicked, `PostBackMessage` contains the series name and the data point number. If the other chart element was clicked, `PostBackMessage` handles its coordinates. In this case, the `HitTest` method tells which chart element was hit.

At the end, the chart is updated at the server side and the chart control encapsulated within the `UpdatePanel` is set back asynchronously. At the browser, the image representing the chart is updated, while the rest of the page (that is, the rest of the HTML document) remains.

> When you run the sample, open the source code of the page. You can see the chart's onClick event (in the <img> tag representing the chart), the _getCoord function, and the _doPostBack calls of <area> tags with the appropriate postback values.

# Triggering Chart Events

By default, any postback control inside an `UpdatePanel` causes an asynchronous post-back and refreshes the panel. However, you can also configure other controls on the page to refresh an `UpdatePanel` control.

This mechanism (control is raised) is very useful for charts. Clicking a data point or a label in a `Chart` control can triggering other parts of the page — for example, it can refresh a table telling you out the data point you clicked.

The `AjaxTriggerSample` page in the `PetShopCharts` project utilizes this mechanism to display two related charts. The first stacked column chart shows details about 2009's sales statistics, where data is organized into regions. When you click any of the data points in this chart, the second chart is updated asynchronously by a trigger to show detail drill-downs. Figure 16-16 shows these charts in action.

![](img/b5597c749e848b27b0d305153ae16106_743_0.png)

FIGURE 16-16: Charts of the AjaxTriggerSample page

To achieve the result you see in Figure 16-16, you must wrap the second chart into an UpdatePanel and define an AsyncPostBackTrigger for it, as shown in Listing 16-16. The Chart controls' details are omitted from this for the sake of readability.

# LISTING 16-16: AjaxTriggerSample.aspx

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
<body>
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

Code file [AjaxTriggerSample.aspx] available for download at Wrox. The ControlID attribute of AsyncPostTrigger defined in the <Triggers> elements for the UpdatePanel control. The code-behind of the page (in Listing 16-17) shows how Chart triggers the update of Chart2. ![](img/b5597c749e848b27b0d305153ae16106_744_0.png)

# LISTING 16-17: AjaxTriggerSample.aspx

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

# LISTING 16-17 (continued)

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
        series.ToolTip = "#AXISABEL sold by " + series.Name + " : #VALD";
    }
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
    series.ToolTip = "#AXISABEL sold in " + series.Name + " : #VALD";
}
```

> Code file [AjaxTriggerSample.aspx] available for download at Wrox.com

The Page_Load event initializes a chart with the DataBindTable method that creates series for each region. The foreach cycle following the data binding is responsible for setting up the visual series properties, and PostBackValue, which is the key in this scenario. The following assignment sets the postback value so that the axis label and the series name is passed back when the user clicks a data point:

```csharp
series.PostBackValue = "#AXISABEL" + series.Name;
```

When you comment out this line and run the sample, because postback happens, PostBackValue triggers rendering postback scripts.

So, when the user clicks a data point, the Chart1 Click event handler is invoked as a result of the asynchronous postback. It obtains the PostBackValue sent by Chart1 as a property of its ImageEventArgs parameter. Chart1 Click splits this value into two parts that will be used as input parameters for the query being carried out as the data source of Chart2. Binding to the query results to Chart2, the foreach cycle sets the series' properties.

This kind of master-detail chart selection is very powerful. If it takes a few seconds (let's say few) while the second chart gets updated, you can use an Ajax UpdateProgress control. While the chart is being updated, the user is not prevented from examining the first chart. Or, you can use any controls instead of the second chart, and with this mechanism, you can also cascade controls in a master-detail scenario.

# Real Time Charts

The asynchronous nature of Ajax is a great candidate for displaying real-time charts where data is queried periodically, and a chart is updated with the new data regularly. The AjaxRealTimeSample page of the PetShopCharts project demonstrates this scenario.

The page contains a chart that displays real-time stock exchange data of fictitious indices so that information is refreshed every second. Figure 16-17 shows the chart after several asynchronous refreshes.

![](img/b5597c749e848b27b0d305153ae16106_746_0.png)

Figure 16-17: Real-time chart after several refreshes
