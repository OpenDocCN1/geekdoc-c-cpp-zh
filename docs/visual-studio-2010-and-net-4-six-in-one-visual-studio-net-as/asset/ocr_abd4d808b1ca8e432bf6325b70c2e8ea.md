# LISTING 16-11: BasicChartManagement.aspx.cs

![](bbox=[0.1, 0.101, 0.155, 0.155])

```
using System;
using System.Web.UI.DataVisualization.Charting;
```

```
namespace PetShopCharts
{
    public partial class BasicChartStateManagement : System.Web.UI.Page
    {
        protected void Form_Init(object sender, EventArgs e)
        {
            Chart1.EnableViewState = true;
        }
    }
```

```
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

```
    private void GenerateRandomData(Series series)
    {
        const double MaxStep = 5.0;
        series.Points.Clear();
        var rand = new Random((int)DateTime.Now.Ticks);
        var lastValue = 5.0;
        for (int i = 0; i < 50; i++
        {
            series.Points.AddXY(i + 1, lastValue);
            lastValue += MaxStep * rand.NextDouble() - MaxStep/2;
            series.Points[i].Values[0] = lastValue;
        }
    }
```

```
    private void AddNewSeries(string name, double distance)
    {
        RemoveSeries(name);
        var baseSeries = Chart1.Series["Default"];
        var newSeries = new Series(name);
        newSeries.ChartType = SeriesChartType.Spline;
        newSeries.BorderWidth = baseSeries.BorderWidth;
        Chart1.Series.Add(newSeries);
        foreach (var point in baseSeries.Points)
        {
            newSeries.Points.AddXY(point.XValue, point.YValues[0] + distance);
        }
    }
```