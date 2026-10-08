
# Listing 16-13 shows the code enabling the chart to be displayed with tooltips.

LISTING 16-13: TooltipValuesSample.aspx

```assembly
using System;
using System.Data;
using System.Data.OleDb;
using System.Web.UI.DataVisualization.Charting;

namespace PetShopCharts
{
    public partial class TooltipValuesSample : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            var region = RegionList;
            var connection = Helpers.Utility.GetDataConnection(this);
            var commandStr = "SELECT Name, Total from PetSalesFor2007 where " +
                              "Region = '''' and KindID=5"; // Arthropods
            var command = new OleDbCommand(commandStr, connection);
            command.Open();
            var reader = command.ExecuteReader(CommandBehavior.CloseConnection);
            var points = Chart1.Series[0].Points;
            points.DataBind(reader, "Name", "Total");

            // Set legend texts
            foreach (var point in points)
            {
                point.LegendText = point.AxisLabel;
                point.AxisLabel = "*";
            }
            reader.Close();
            connection.Close();

            // Set up series
            var series = Chart1.Series[0];
            series.LegendTip = "#LEGENDTEXT: #VAL(D) pieces\n" +
                              "#PERCENT of total #TOTAL";
            series.LegendToolTip = "#PERCENT";
        }
    }
}
```

Code file [TooltipValuesSample.aspx] available for download at Wrox.com.

The Page_Load method uses a data reader to obtain the sales statistics from the database. This time, the data points are bound to the chart with the Series.Points.DataBind method. The following DataBindXY sets the legend text for data points, and removes their labels.

The most important statements of this sample are at the end of the body setting the Tooltip and LegendToolTip properties. The tokens in the property values (starting with a # character) are substituted with the concrete values at run-time.

When the server renders the chart image, it assigns a <map> element to the <img> tag, as the following short extract shows:

```html
<img id="Chart1" src="ChartImg.axd?i=chart_4bfd..." alt="usemap=#ChartImageMap" style="height:400px;width:500px;border-width:0px; />
<map name="ChartImageMap" id="ChartImageMap">
<area shape="poly" coords="176,207,241,309,241,..." title=""
alt="Bind-blend solid; legend 127 pieces
16, 26 % of total 781" />
<!--
-->
</map>
```

# Handling Clicks on Data Points

The Chart makes it easy to respond to events when you click on a data point or a legend item. The ClickDataPointsSample.aspx page shows you how to do that. It improves the TooltipValues.aspx page shows when you click on one of the doughnut chart slices, the slides are expanded. There are only a few changes in the code-behind file referred to Listing 16-13. These modifications are shown in Listing-14.

LISTING 16-1: ClickOnDataPointsSample.aspx

```assembly
using System;
using System.Data;
using System.Data.OleDb;
using System.Web.UI.Controls;

namespace PetShopCharts
{
    public partial class ClickDataPointsSample : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            // ...
            // Added to the Page_Load method
            series.PostBackValue = "#INDEX";
            series.LegendPostBackValue = "#INDEX";
            if (!IsPostBack)
            {
                series.Points[0].CustomProperties += "Exploded=true";
            }
        }

        protected void Chart1_Click(object sender, ImageMapEventArgs e)
        {
            int pointIndex = int.Parse(e.PostBackValue);
            var series = Chart1.Series[0];
            if (pointIndex >= 0 && series.Points.Count
            {
              series.Points[pointIndex].CustomProperties += "Exploded=true";
            }
        }
    }
}
```

Code file [OnClickDataPointsSample.aspx] available for download at Wrox.com.

Setting either the PostBackValue or the LegendPostBackValue of a series will initiate a postback when the series' data points (or any legend item associated with the series) is clicked. The code in Listing 16-14 sets these properties to #index so that the data point index is posted back when the click event is set to Chart_1's OnClick event parses the postback to obtain the index of the data point, clicked and sets the Exploded custom property of the slice clicked to true. Figure 16-14 shows what happens when you click on the Tumumble slice.

![](img/b5597c749e848b27b0d305153ae16106_738_0.png)

FIGURE 16-14: A slice of the doughnut chart

You can also click on the legend items to explode the appropriate data point slice.

# Interactivity With Ajax

Ajax (Asynchronous JavaScript and XML) is a group of interrelated web development techniques used on the client-side to create interactive web applications. Ajax, web applications can retrieve data from the server asynchronously in the background without interfering with the display and behavior of the existing page.

This section explores how easy it is to combine a chart's interactivity features with Ajax to improve the user experience.

> This chapter is definitely not about Ajax and related techniques. You can read a more detailed overview about Ajax and its improvements in .NET Framework 4.0 in Chapter 19. Chapter 20 introduces you to the Ajax Control Toolkit. This chapter only examines a few examples that may wet your appetite, but definitely won't present you with the full menu Ajax offers.

# Handling Click Events

With Ajax, you can post-back a message to the web page in a separate asynchronous communication channel using an XMLHttpRequest object at the background. When the page processes the request, it sends back the results, and a well-defined part of the page is refreshed after the results returned. This communication is asynchronous, so it allows you to interact with the page.

The PetShop project contains a page named AjaxClickEvent that allows you to click any point on the chart and refresh the subtitle with information about what has clicked. Figure 16-15 shows how the subtitle changes when you click on the second series.

![](img/b5597c749e848b27b0d305153ae16106_739_0.png)

FIGURE 16-15: Using Ajax to click events

To allow Ajax communication on your page, you must add an <asp:ScriptManager> and an <asp:UpdatePanel> to control your page:

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>Ajax event sample</title>
</head>
<body>
<form id="form1" runat="server">
<div>
    <asp:ScriptManager ID="ScriptManager1" runat="server" />
    <asp:UpdatePanel ID="UpdatePanel" runat="server">
    <ContentTemplate>
      <asp:Chart ...
        <!-- Chart details omitted -->
      </asp:Chart>
    </ContentTemplate>
    </asp:UpdatePanel>
</div>
</form>
</body>
</html>
```

The ScriptManager is responsible for managing ASP.NET script libraries and script files, partial-rendering, and client proxy generation for web and application services. The UpdatePanel control enables a section of the page to be partially rendered without a postback. The <ContentTemplate> element encapsulates the page section updated by the UpdatePanel.

Listing 16-15: How the Ajax controls work together with the page in an asynchronous manner.

```assemblyusing System;
using System.Data;
using System.Data.OleDb;
using System.Web.UI;
using System.Web.UI.DataVisualization.Charting;
using System.Web.UI.WebControls;

namespace PetShopCharts
{
    public partial class AjaxClickEvent : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            // Initialize chart from database
            var connection = "SELECT Name, ShopName from DogSalesData "
            var commandStr = "Where Region = 'East';";
            var command = new OleSqlCommand(commandStr, connection);
            command.Open();
            var reader = command.ExecuteReader(CommandBehavior.CloseConnection);
            Chart1.DataBindTable(reader, "ShopName", "Name", "Total", "");
            reader.Close();
            connection.Close();
            foreach (var series in Chart1.Series)
            {
                series.ChartType = ChartType.StackedColumn;
                series.IsValueShownAsLabel = true;
            }
        }
    }
}
```
