
You can customize the stock chart so that you can enable or disable open and closing values. The data point with X value of 6 is displayed with a closed value.

The polar chart type is a circular graph on which data points are displayed using the angle, and the distance from the center point—according to the polar coordinate system. The X axis is located on the boundaries of the circle, and the Y axis connects the center of the circle with the X axis. Figure 14-36 shows an example of this chart type.

The radar chart used to display multivariate data in the form of a two-dimensional chart of three or more quantitative variables represented on axes starting from the same point. The relative position and angle of the axes is unfamiliar. It is also known as web chart, spider chart, and star chart. Unlike other chart types, the radar chart type uses the circumference of the chart as the X axis. Figure 14-37 shows an example of this chart type.

![](img/b5597c749e848b27b0d305153ae16106_657_0.png)

Figure 14-36: Polar chart example

## More About Custom Properties

Most chart types have a few custom properties you can use to customize chart rendering. When you set the ChartType property of a Series, you'll find a CustomProperties category that holds special properties interpreted in the context of the selected chart type. In Figure 14-38 you can see the custom properties of a column chart (on the left) and a stock chart (on the right) by side.

![](img/b5597c749e848b27b0d305153ae16106_657_1.png)

Figure 14-37: Radar chart example

If a custom property is applicable to both the chart's Series and DataPoint objects, a custom property that is set for a series affects all data points contained within that series. Data points belonging to the series inherit these properties, but you can change them. Custom properties that apply to DataPoint objects have a higher priority than those apply to Series. If the same custom property is set for a Series object and one of its DataPoint objects, the setting for the DataPoint object takes precedence.

For example, this feature was used when creating Figure 14-38, where a few data points have different style from the others.

| Name | MarkerStyle | Name |
|---|---|---|
| ChartType | Default | ChartType |
| DataStyle | Auto | DataStyle |
| EmptyFill | Auto | EmptyFill |
| LabelStyle | Auto | LabelStyle |
| MarkerPointWidth | | MarkerPointWidth |
| DataPointProperties | | DataPointProperties |
| UserObjectClass | | UserObjectClass |

Figure 14-38: Custom properties of a column chart and a stock chart

> There are many properties and custom properties you can use to tailor chart types to your needs. You can read more about them in the MSD documentation of the Chart control at http://msdn.microsoft.com/en-us/library/dd489233.(VS.10).aspx.

## Chart Coordinate System

The Chart uses a coordinate system to position titles, legends, annotations, and chart areas in the chart picture. To do this, it uses each element's Position property. The chart coordinate system has the following characteristics:

- The chart coordinate system has its origin (0, 0) in the upper-left corner of the chart picture.
- In the (X, Y) coordinates, the X value points to the horizontal axis, and the Y value points to the vertical axis.

The unit of measure is a percentage of the chart picture's width and height. Coordinate values must be between 0 and 100. Relative coordinates ensure that objects remain relative to one another when the chart is resized.

A chart area positions each of its elements using a similar coordinate system. Coordinates (0, 0) represent the upper-left corner of the chart area, and (100, 100) represent the lower-right corner of the chart area. When a legend is docked to a chart area, it is positioned using the chart area's coordinate system.

Understanding how the coordinate system works is especially when you want to implement custom drawing or user interactions (for example, mouse testing). To perform custom drawing using GDI+ functions in your code, you must convert the relative coordinates to absolute pixels. The ChartGraphics class contains methods for absolute-to-relative and relative-to-absolute conversion of PointF, RectangleF, and SizeF structures. To demonstrate these concepts, you can change the SimpleChart program to add custom drawings. Open the SimpleChart project, and then open SimpleChart.cs control in design view. In the Properties window, add an event handler for the PostPaint event, and write the method body as shown in Listing 14-7.

### LISTING 14-7: SimpleChart.cs (chart1_PostPaint Method)

```csharp
using System.Drawing;
using System.Windows.Forms;
using System.Windows.Forms.DataVisualization.Charting;
using System;

namespace WpfChart
{
    public partial class SimpleChart : UserControl
```

### LISTING 14-7 (continued)

```csharp
{
    public SimpleChart()
    {
        InitializeComponent();
        SetupChart();
    }

    private void SetupChart()
    {
        var title = new Title("This is a Window in WPF");
        title.Font = new System.Drawing.Font("Arial", 18, FontStyle.Bold);
        chart1.Titles.Add(title);
        var datapoints = chart1.Series[0].Points;
        for (int i = 0; i < 10; i++)
        {
            datapoints.Add(new DataPoint(i, Math.Pow(i, 2)));
        }
    }

    private void chartPostPaint(object sender, ChartEventArgs e)
    {
        // Uncomment this code to see how custom paint
        if (e.Element is ChartArea)
        {
            var chartArea = e.Element as ChartArea;
            var areaRect = new Rectangle(10.0F, 10.0F, 80.0F, 80.0F);
            var absAreaRect = e.ChartGraphics.GetAbsoluteRectangle(areaRect);
            var rect = new Rectangle((int)absAreaRect.X, (int)absAreaRect.Y, (int)absAreaRect.Width, (int)absAreaRect.Height);
            e.ChartGraphics.DrawRectangle(System.Drawing.Pens.Red, rect);
        }
        else if (e.Element is Series)
        {
            var series = e.Element as Series;
            foreach (DataPoint point in series.Points)
            {
                var position = new PointF();
                position.X = (float)e.ChartGraphics.GetPositionFromAxis("ChartArea", AxisName.X, point.XValue);
                position.Y = (float)e.ChartGraphics.GetPositionFromAxis("ChartArea", AxisName.Y, point.YValues);
                e.ChartGraphics.GetAbsolutePoint(position);
                for (int rad = 5; rad <= 35; rad += 10)
                {
                    e.ChartGraphics.Ellipse(System.Drawing.Pens.Black, position.X - rad / 2, position.Y - rad / 2, rad, rad);
                }
            }
        }
    }
}
```

This code draws a bounding rectangle around the chart area defined by the areaRect and leaves 10 percent padding within the chart area. The GetAbsoluteRectangle method of the ChartGraphics class is used to translate coordinates to absolute ones stored in absAreaRect.

The cycle iterates through data points draws concentric circles around data points. This cycle uses the GetPositionFromAxis method to translate the X value and Y value of a data point to absolute coordinates.

When you build and run the application, you can see the result of custom drawing, as shown in Figure 14-39.

![](img/b5597c749e848b27b0d305153ae16106_660_0.png)

Figure 14-39: Custom drawings

## Three-Dimensional Charts

As you have seen, the Chart control supports displaying three-dimensional charts. The ChartArea class has a property named Area3DStyle with the type of ChartArea3DStyle. This is the property you can use to set up and customize how the specific chart area should display a three-dimensional chart. Figure 14-40 shows how the properties in ChartArea.Area3DStyle correspond to the appearance of the three-dimensional chart.

![](img/b5597c749e848b27b0d305153ae16106_660_1.png)

Figure 14-40: Three-dimensional style properties

Table 14-3 summarizes the properties you can use to customize the three-dimensional view.

# **TABLE 14-3:** ChartArea3DStyle Properties

| PROPERTY | DESCRIPTION |
|---|---|
| Enable3D | Gets or sets a flag that toggles the three-dimensional rendering on and off for a chart area. |
| Inclination | Gets or sets the angle of rotation around the horizontal axes for three-dimensional chart areas. |
| IsClustered | Gets or sets a flag that determines whether the data series for a bar or column chart are clustered (is, displayed along distinct rows). For example, in Figure 14-40, you can see three series. Two of them use a column chart, the third uses a spine chart. The **Clustered** flag is set to **true**, and the two column charts share the same cluster. You should set this flag to **false**, you would see the chart as shown in Figure 14-41. |
| IsRightAngleAxes | Gets or sets a flag that determines whether a chart area is displayed using an isometric projection. Isometric views are not actually three-dimensional, the displayed angles of rotation may not match the actual angles. The actual angles are controlled using the *Rotation* and *Inclination* properties, respectively. |
| LightStyle | Gets or sets the type of lighting for a three-dimensional chart area. Use the LightStyle.None when you want no lighting to be applied. The LightStyle.Simplistic provides you with a simple lighting where the hue of all chart elements is fixed. When `Style.Realistic` is applied, the hue of all chart elements changes, depending on the amount of rotation. |
| Perspective | Gets or sets the center of perspective for a three-dimensional chart area. The allowable range is 0 to 100, and the default is 0. If you set the Perspective property, the IsRightAngleAxes property will be automatically set to false, because these properties are mutually exclusive. |
| PointDepth | Gets or sets the depth of data points displayed in a three-dimensional chart. The PointDepth property can be applied to set the depth of bar, column, line, pie, and spine chart points only. If you set this property for other chart types (for example, bubble and point charts cannot have their depths stretched), it will reserve extra space for the data, but will not increase their depths. |
| PointGapDepth | Gets or sets the distance between series rows in a three-dimensional chart area. The unit of measurement is expressed as a percentage of the distance between data points in row. |
| Rotation | Gets or sets the angle of rotation around the vertical axes for three-dimensional chart areas. |
| WallWidth | Gets or sets the width of the walls displayed in a three-dimensional chart area. The allowable range is 0 to 30 pixels. |
