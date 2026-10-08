# RENDERING ASP.NET CHARTS

Thus far, how you have learned to create simple ASP.NET charts using the designer, how to set up data points manually and programmatically, and how to bind information coming from a database to your chart.

Although using Windows Forms charts you do not have to deal with the rendering of charts, because of the distributed nature of web applications, ASP.NET charts, you have several rendering options. This section examines a few scenarios and how to choose the appropriate rendering option in a certain scenario.

There is no HTML tag for describing a chart or of the chart elements. When you run the page that generates the output shown in Figure 16-4, very simple HTML content is generated, as Listing 16-6.



```
<DOCTYPE html PUBLIC "//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml/DTD/xhtml-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title>
Data binding with the DataBindCrossTable method
</title>
</head>
<body>
<form method="post" action="DataBindCrossTable.aspx" id="form">
<div class="aspHidden">
<input type="hidden" name="__VIEWSTATE" id="__VIEWSTATE value="WEPDGUJNI2M..." />
</div>
<div>
<img id="chart" src="ChartImg.axd?id=chart_cf32..." alt=""
style="height:400px;width:800px;border:0px;" />
</div>
</form>
</body>
</html>
```

The chart is represented by an image as the <img> HTML tag signs. The source of the image is a URL, like this:

*=ChartImg.axd?id=chart_cf7323be4634374f9b87dbb136452ccd_0.png&g=751de08f64274dc0a8e4ab40b116ae5

The charts are managed by an HttpHandler that is accessed by the /ChartImg.axd address. The i and g request arguments identify the image to be retrieved. The ASP.NET Chart control has several properties to define how charts are rendered. You can find them under the