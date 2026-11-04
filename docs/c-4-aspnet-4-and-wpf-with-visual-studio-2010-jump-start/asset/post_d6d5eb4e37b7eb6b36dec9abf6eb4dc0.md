
## Professional ASP.NET 4 in C# and VB

![](img/7954dcc7dd1d929d072aec8e9531b6cc_38_0.png)

## Professional ASP.NET 4 in C# and VB

### Chart Server Control

One of the newest controls available to you now with ASP.NET 4 is the Chart server control. This control made its way into the core part of ASP.NET through a previous acquisition of the Dundas charting company and is a great control for getting you up and running with some good-looking charts.

The new Chart server control supports many chart types including:

- Point
- FastPoint
- Bubble
- Line
- Spline
- StepLine
- FastLine
- Bar
- StackedBar
- StackedBar100
- Column
- StackedColumn
- StackedColumn100
- Area
- SplineArea
- StackedArea
- StackedArea100
- Pie
- Doughnut
- Stock
- Candlestick
- Range
- SplineRange
- RangeBar
- RangeColumn
- Radar
- Polar
- ErrorBar
- BoxPlot
- Renko
- ThreeLineBreak
- Kagi
- PointAndFigure
- Funnel
- Pyramid

Those are a lot of different chart styles! You can find the Chart server control in the toolbox of Visual Studio 2010 underneath the Data tab. It is part of the System.Web.DataVisualization namespace.

When you drag it from the toolbox and place it on the design surface of your page, you are presented with a visual representation of the chart type that you are going to use. The next figure shows an example.

![](img/7954dcc7dd1d929d072aec8e9531b6cc_40_0.png)

Open up the smart tag for the control, and you find that you can assign a data provider for the chart as well as select the chart type you are interested in using. Changing the chart type gives you a sample of what that chart looks like (even if you are not yet working with any underlying data) in the design view of the IDE. The smart tag is shown in the next figure.

![](img/7954dcc7dd1d929d072aec8e9531b6cc_40_1.png)

There is a lot to this control, probably more than all the others and this single control could almost warrant a book on its own. To get you up and running with this chart server control, follow this simple example.

Create a new web application and add the AdventureWorks database to your App_Data folder within the application. After that is accomplished, drag and drop the Chart server control onto the design surface of your page. From the smart tag of the control, select `<New Data Source>` from the drop-down menu when choosing your data source. Work your way through this wizard making sure that you are choosing a SQL data source as your option. As you work through the wizard, you are going to want to choose the option that allows you to choose a custom SQL statement and use the following SQL for this operation:

```
SELECT TOP (5) Production.Product.Name, Sales.SalesOrderDetail.OrderQty
FROM Sales.SalesOrderDetail INNER JOIN Production.Product
ON Sales.SalesOrderDetail.ProductID = Production.Product.ProductID
ORDER BY Sales.SalesOrderDetail.OrderQty DESC
```

With that in place and the new chart server control bound to this data source control, you now find that you have more options in the smart tag of the chart server control, as shown in this figure.

Now you can select the series data members and choose what is on the x-axis and what is on the y-axis. You can see that I have assigned the Name of the product to be on the X-axis and the quantity ordered to be on the y-axis. After widening the chart's width a bit, you end up with code similar to the following in Listing 3-52.

![](img/7954dcc7dd1d929d072aec8e9531b6cc_41_0.png)

### Pro ASP.NET 9780470502204 Listing 3-52: Charting with the new Chart server control

```
<%@ Page Language="C#" AutoEventWireup="true"
CodeBehind="WebForm1.aspx.cs" Inherits="WebServerControls.WebForm1" %>
<%@ Register Assembly="System.Web.DataVisualization, Version=4.0.0.0",
    Culture="neutral", PublicKeyToken="31bf3856ad364e35"
    Namespace="System.Web.UI.DataVisualization.Charting" TagPrefix="asp" %>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>MultiView Server Control</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:Chart ID="Chart1" runat="server"
    DataSourceID="SqlDataSource1"
    Width="500px">
    <Series>
        <asp:Series ChartType="Bar" Name="Series1"
            XValueMember="Name"
            YValueMembers="OrderQty" YValuesPerPoint="2">
        </asp:Series>
    </Series>
    <ChartAreas>
        <asp:ChartArea Name="ChartArea1">
        </asp:ChartArea>
    </ChartAreas>
</asp:Chart>
<asp:SqlDataSource ID="SqlDataSource1" runat="server"
    ConnectionString="<%$ ConnectionStrings:ConnectionString %>"
    SelectCommand="SELECT TOP (5) Production.Product.Name,
Sales.SalesOrderDetail.OrderQty FROM Sales.SalesOrderDetail
INNER JOIN Production.Product ON
Sales.SalesOrderDetail.ProductID =
Production.Product.ProductID ORDER BY
Sales.SalesOrderDetail.OrderQty DESC"
</asp:SqlDataSource>
</div>
</form>
</body>
</html>
```

From this, you can see that there isn't much code needed to wire everything up. Most notably, you can see that putting this Chart server control on your page actually added a @Register directive to the top of the page. This is unlike most of the ASP.NET server controls.

Within the `<Series>` element of this control, you can have as many series as you want, and this is something that is quite common when charting multiple items side by side (such as a time series of prices for two or more stocks).

Running this code, you get results similar to what is presented here.

![](img/7954dcc7dd1d929d072aec8e9531b6cc_42_0.png)

### ASP.NET AJAX Control Toolkit

With the install of the .NET Framework 4 and through using Visual Studio 2010, you will find a few controls available that allow you to build ASP.NET applications with server-side AJAX capabilities. This is the framework to take your applications to the next level because you can accomplish so much with it, including adding specific AJAX capabilities to your user and custom server controls. Every AJAX enhancement added to your application will make your application seem more fluid and responsive to the end user.

You might be wondering where the big AJAX-enabled server controls are for this edition of Visual Studio 2010 if this is indeed a new world for building Web applications. The reason you do not see a new section of AJAX server controls is that Microsoft has treated them as an open source project instead of just blending them into Visual Studio 2010.

Developers at Microsoft and in the community have been working on a series of AJAX-capable server controls that you can use in your ASP.NET applications. These controls are collectively called the ASP.NET AJAX Control Toolkit. Recently, Microsoft has made the ASP.NET AJAX Control Toolkit a part of the Microsoft AJAX Library found at www.asp.net/ajaxlibrary. Downloading the library, you will find that it now also includes the complete AJAX Control Toolkit. The following figure shows the download page for the AJAX Library.

![](img/7954dcc7dd1d929d072aec8e9531b6cc_43_0.png)

To get set up, download the .zip file from the aforementioned site at www.asp.net/ajaxlibrary and unzip it where you want on your machine. Then follow these steps:

- 1. Install the controls into Visual Studio. Adding the controls to your Visual Studio 2010 Toolbox is very easy. Right-click in the Toolbox and select Add Tab from the provided menu. Name the tab as you want — for this example, the tab is called AJAX Controls.

- 2. With the new tab in your Toolbox, right-click the tab and select Choose Items from the provided menu, as illustrated in the next figure. The Choose Toolbox Items dialog appears.

![](img/7954dcc7dd1d929d072aec8e9531b6cc_45_0.png)

- 3. Select the AjaxControlToolkit.dll from the download. When you find the DLL and click Open, the Choose Toolbox Items dialog changes to include the controls that are contained within this DLL. The controls are highlighted in the dialog and are already selected for you (as shown in the next figure).

![](img/7954dcc7dd1d929d072aec8e9531b6cc_45_1.png)

- 4. Click OK, and the ASP.NET AJAX Control Toolkit's controls will be added to your Visual Studio Toolbox. The next figure presents the end result.
