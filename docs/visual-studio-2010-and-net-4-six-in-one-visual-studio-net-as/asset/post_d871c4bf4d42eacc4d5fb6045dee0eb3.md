
```xml
<ChartAreas>
  <asp:ChartArea Name="ChartArea1">
  </asp:ChartArea>
</ChartAreas>
<Titles>
  <asp:Title Font="Calibri, 24pt" Name="Title1">
  </asp:Title>
</Titles>
<asp:Chart>
<div>
</form>
</body>
</html>
```

Code file [Default.aspx] available for download at Wrox.com

The input parameters are represented by the PointsNumber and ExponentBox controls. When the user clicks DrawChartButton, the DrawChartButton_Click event handler is executed, and it sets up the chart's data points, as in Listing 16-4.

# LISTING 16-4: Default.aspx Implementing the DrawChartButton_Click Handler

![](img/b5597c749e848b27b0d305153ae16106_716_0.png)

```csharp
using System;
using System.Drawing;
using System.Web.UI.DataVisualization.Charting;

namespace SimpleAspNetCoreNet
{
    public partial class Default : System.Web.UI.Page
    {
        protected void Load(object sender, EventArgs e)
        {
            var series1 = Chart.Series[0];
            series1.ChartType = ChartType.SplineRange;
            SetTitleForInvalidState();
        }

        protected void DrawChartButton_Click(object sender, EventArgs e)
        {
            // Process input parameters
            int numberOfPoints;
            double exponent;
            if (!Int32.TryParse(PointsNumberBox.Text, out numberOfPoints) ||
                !Double.TryParse(ExponentBox.Text, out exponent))
            {
                SetTitleForInvalidState();
                return;
            }

            // Create data points
            for (int i = 0; i < numberOfPoints; i++)
            {
                Chart1.Series[0].Points.Add(new DataPoint(i,
                    Math.Pow(Math.Abs(numberOfPoints / 2.0 - i), exponent));
            }
        }
    }
}
```

# LISTING 16-4 (continued)

```csharp
// -- Set title
var title = Chart.Titles[0];
title.Text = String.Format("(0) points with exponent ({1)",
numberOfPoints, exponent);
title.ForeColor = Color.Black;

private void SetTitleForInvalidState()
{
    var title = Chart.Titles[0];
    title.Text = "No valid chart data specified...";
    title.ForeColor = Color.Maroon;
}
```

Code file [Default.aspx.cs] available for download at Wrox.

DrawChartButton_click checks if the input parameters can be parsed as numbers. If they cannot, the chart title is modified to signal a failure; otherwise, data points are calculated and the chart is changed. Figure 16-3 shows the chart after the DrawChartButton_click handler has been executed.

![](img/b5597c749e848b27b0d305153ae16106_717_0.png)

# Binding Data to the Chart

Most charts use data points as a result of or query against a database. ASP.NET controls support the .NET data binding mechanism, and the Chart also utilizes this to provide you with a convenient and easy way to set up your data points. In Chapter 14, you built a simple data-bound chart using LINQ expression, and also saw an overview of several data binding methods supported by the Chart control.

The ASP.NET Chart control supports the same mechanisms as the Windows Forms Chart control. This section utilizes the Chart.DataBindCrossTable method that provides a great support to obtain data points for multi-series charts.

Download the PetShopCharts sample and open its solution file in Visual Studio 2010. Open the DataBindCrossTable.aspx file in Code view. This page connects to a Microsoft Access

FIGURE 16-3: Chart after the "Draw Chart" button was clicked

database representing the Enterprise Resource Planning (ERP) system of a company managing a network of small pet shops, and creates a sales history. Listing 16-5 shows how the page binds the sales information coming from the database to the chart.

![](img/b5597c749e848b27b0d305153ae16106_718_0.png)

# LISTING 16-5: DataBindCrossTable.cs

```csharp
using System;
using System.Data;
using System.Data.OleDb;
using System.Web.UI.DataVisualization.Charting;

namespace PetShopCharts
{
    public partial class DataBindCrossTable : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            var connection = Helpers.Utility.GetDataConnection(this);
            var commandStr = "SELECT Period, Total from SalesByYear";
            var command = new OleDbCommand(commandStr, connection);
            connection.Open();
            var reader = command.ExecuteReader(CommandBehavior.CloseConnection);
            Chart1.DataBindCrossTable(
                "Category",
                "Period",
                "Total"
            );
            reader.Close();
            connection.Close();
            foreach (var series in Chart1.Series)
            {
                series.ChartType = SeriesType.Spline;
                series.BorderWidth = 4;
            }
        }
    }
}
```

Code file [DataBindCrossTable.aspx] available for download at Wrox.

The page uses the standard pattern to set up an Access database and prepares a reader object to execute a query. The GetDataConnection method of the Helpers static class is responsible for preparing this connection, and its source code is:

```csharp
public static OleDbConnection GetDataConnection(Page page)
{
    string fileName = page.MapPath("~/") + @"\App_Data\PetShopData.mdb";
    string connectionString = "Provider=Microsoft.Jet.OLEDB.4.0;Data Source=" + fileName;
    return new OleDbConnection(connectionString);
}
```

The bulk of the work is done by the DataBindCrossTable method:

```csharp
Chart1.DataBindCrossTable(
  reader,
  "Category",
  "Total"
);
```

This method reads the content represented by the reader and groups the records into series according to the second argument. The third and fourth arguments define the values for X and Y properties of data points, respectively. The first argument allows setting up data bindings for any other point properties. So, this sample creates separate data bindings using the Category field as the X and Total as the Y value. Because DataBindCrossTable creates a new series, you must define the properties of these newly instantiated series. This is why DataBindCrossTable invocation is followed by a foreach loop:

```csharp
foreach (var series in Chart.Series)
{
  series.ChartType = SeriesChart.Spline;
  series.BorderWidth = 4;
}
```

The DataBindCrossTable.aspx file contains several visual properties for the chart, but those do not influence data binding. When you run the application and navigate to the sample page, you can see that five series are created as a result of the DataBindCrossTable call, as shown in Figure 16-4.

![](img/b5597c749e848b27b0d305153ae16106_719_0.png)

FIGURE 16-4: Chart created with DataBindCrossTable

# RENDERING ASP.NET CHARTS

Thus far, how you have learned to create simple ASP.NET charts using the designer, how to set up data points manually and programmatically, and how to bind information coming from a database to your chart.

Although using Windows Forms charts you do not have to deal with the rendering, because of the distributed nature of web applications, ASP.NET charts have several rendering options. This section examines a few scenarios and how to choose the appropriate rendering option in a certain scenario.

There is no HTML tag for describing a chart or its chart elements. When you run the page that generates the output shown in Figure 16-4, very simple HTML content is generated, as in Listing 16-6.

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml/DTD/xhtml-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title>
Data binding with the DataBindCrossTable method</title>
</head>
<body>
<form method="post" action="DataBindCrossTable.aspx" id="form">
<div class="aspHidden">
<input type="hidden" name="__VIEWSTATE" id="__VIEWSTATE" value="WEPDGUJNI2M..." />
</div>
<div>
<img id="chart" src="ChartImg.axd?id=chart_cf32..." alt=""
style="height:400px;width:800px;border:0px;" />
</div>
</form>
</body>
</html>
```

The chart is represented by an image as the <img> HTML tag. The source of the image is a URL, like this:

/ChartImg.axd?id=chart_cf7323be4634374f9b87dbb136452ccd_0.png&g=751de08f64274dc0a8e4ab40b116ae5

The charts are managed by an HttpHandler that is accessed by the /ChartImg.axd address. The i and g request arguments identify the image to be retrieved. The ASP.NET Chart control has several properties to define how charts are rendered. You can find them under the
