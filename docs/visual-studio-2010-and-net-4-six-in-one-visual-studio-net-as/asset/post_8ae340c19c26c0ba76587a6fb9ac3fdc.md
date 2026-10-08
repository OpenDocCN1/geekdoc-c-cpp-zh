
| PROPERTY | DESCRIPTION |
|---|---|
| IntervalOffset | Gets or sets the interval offset of an axis. This value is used as the interval offset of the labels of an axis, as well as the major tick marks and grid lines associated with the axis. |
| IntervalOffsetY | This property determines the interval offset type of an axis, and is used for the interval offset type of labels, major tick marks, or major grid lines of an axis. |
| IntervalType | This property determines the interval type of an axis, and is used for the interval type of labels, major tick marks, or major grid lines of an axis. |
| CustomLabels | Gets a `CustomLabelsCollection` object used to store `CustomLabels` objects. |
| IsLabelAutoFit | Gets or sets a flag that determines whether axis labels are automatically fitted. |
| LabelAutoFitMinSize | Gets or sets the minimum font size that can be used by the label auto-fitting algorithm. |
| LabelAutoFitMaxSize | Gets or sets the maximum font size that can be used by the label auto-fitting algorithm. |
| LabelAutoFitStyle | Gets or sets the allowable label changes that can be made to enable the label to fit along an axis. |
| LabelStyle | Specifies the style, formatting, and so forth, of axis labels. If the `IsLabelAutoFit` property is `true`, the font size, font angle, and the offset of labels are determined automatically. If any one of the `LabelStyle.Font.Size, Angle, IsStaggered` properties, the `IsLabelAutoFit` property will be set to `false`. |
| MaximumAutoSize | Gets or sets the maximum size of the axis, measured as a percentage of the chart area. This value is used by the automatic layout algorithm. |
| Enabled | Gets or sets a value that indicates whether an axis is enabled. If an axis is not enabled, the axis, along with its attributes (tick marks, strip lines, labels, and so forth), will not be displayed. If an axis is enabled, the axis, along with all its attributes (tick marks, strip lines, labels, and so forth), will be displayed, regardless of whether or not it is being used to plot a `Series`. A value of `Auto` is used, an axis may or not be displayed, depending on whether it is being used to plot a `Series`. The axes that are used to plot data are determined by `XAxisType` and `YAxisType` property settings. |

# TABLE 14-8 (continued)

| PROPERTY | DESCRIPTION |
|---|---|---|
| Crossing | Setting this property for a primary axis will determine where it crosses it, and similarly, setting it for a secondary axis will determine where the other secondary axis crosses. For example, setting the Crossing property of the primary X-axis determines where the Y-axis will cross. |
| IsLogarithmic | Gets or sets a flag that indicates whether the axis is logarithmic. Zeros or negative values are not allowed on logarithmic charts. |
| IsMarginVisible | Gets or sets a flag that determines whether to add a margin to the axis. |
| IsReversed | Gets or sets a flag that indicates whether the axis is reversed. If set to reversed, the values on the axis are in reverse sort order, and the direction of values on the axis is flipped. |
| IsStartedFromZero | Gets or sets a flag that indicates the minimum value of the axis will be automatically set to zero if all data point values are positive. If there are negative data point values, the minimum value of the data points will be used. |
| LogarithmBase | Gets or sets a value for the logarithm base of the logarithmic axis. |
| Minimum | Gets or sets the minimum value of an axis. Note that, if you set this value explicitly, the X-values of data elements must be taken into account. If all data points have X-values of zero, the Chart control will assume the first data point occurs at zero. Also, if the Minimum value is explicitly set, the IsStartedFromZero property will be ignored. The Minimum value must be less than the Maximum value. |
| Maximum | Gets or sets the maximum value of an axis. |
| ScaleBreakStyle | Gets or sets the axis scale break style. Scale breaks are intentional discontinuities on the Y-axis that are often used to redistribute the data points in a series chart. This feature improves readability when there are large differences between the high and low values of data in one series being plotted. Scale breaks are not drawn for differences between multiple series. |
| TextOrientation | Gets or sets the orientation of the text in the axis title. This property takes its value from the TextOrientation enumeration (Auto, Horizontal, Rotated90, Rotated270, Stacked). |
| Title | Gets or sets the title of the axis. |
| TitleAlignment | Gets or sets the alignment of an axis title. This property takes its value from the StringAlignment enumeration (Near, Center, Far). |
| TitleFont | Gets or sets the font properties of an axis. |
| TitleForeColor | Gets or sets the text color of an Axis object title. You can use any value ARGB (alpha, red, green, blue) color. |

Most properties can be used easily. When you change their values, the design surface refreshes immediately, and so you can check the effect of changes. However, there are a few properties that need further explanation.

# Strip Lines

Strip lines are used to draw rectangular strips across a ChartArea object, and are always drawn across the entire area. You can draw unlimited numbers of strip lines in a chart area. Listing 14-8 shows an example of setting up strip lines.

# LISTING 14-8: Windows Forms Code Setting Up Strip Lines

```csharp
using System;
using System.Drawing;
using System.Windows.Forms;
using System.Windows.Forms.DataVisualization.Charting;

namespace StripLines
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            // Set up data points
            var series = chart.Series[0];
            for (int i = 0; i < 6; i++)
            {
                series.Points.Add(new DataPoint(10 * i + 10, 5 * i + 5));
            }

            // Set up X-axis
            var xAxis = chart.ChartAreas[0].Axes[(int)AxisName.X];
            xAxis.MinorGrid.Enabled = true;
            xAxis.MinorTick = 5;

            // Set up strip line
            var stripLine = new StripLine();
            stripLine.BackColor = Color.Salmon;
            stripLine.Interval = 10;
            stripLine.StripWidth = 3;
            stripLine.Text = "#1";

            // Set up strip line
            var stripLine2 = new StripLine();
            stripLine2.BackColor = Color.LightBlue;
            stripLine2.Interval = 10;
            stripLine2.StripWidth = 3;
            stripLine2.Text = "#2";

            xAxis.StripLines.Add(stripLine);
            xAxis.StripLines.Add(stripLine2);
        }
    }
}
```

## Custom Axis Labels

Axis labels are automatically created when you set up data points, they are coming from either the XValue property of the data point, or the XValueMember specified for the series. The CustomLabel property of an instance holds CustomLabel objects that describe how a custom axis label should be displayed. Custom labels are displayed in rows that can be indexed from 0 to 10. This index can be accessed through the RowIndex property. Index value 0 is the label closest to the axis, while value 10 carries the label row. When you add any custom label in row 0, the default labels are not displayed. You can also set FromPosition and ToPosition values to define where to put the label on the specified axis.

### LISTING 14-9: Adding Custom Labels to an Axis

```csharp
using System;
using System.Drawing;
using System.Windows.Forms;
using System.Windows.Forms.DataVisualization.Charting;

namespace CustomLabelsSample
{
    public partial class Form : Form
    {
        public Form()
        {
            InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            // Obtain X-axis
            var xAxis = chart.ChartAreas[0].Axes[(int)AxisName.X];

            // Set up data points 
            var series = chart.Series[0];
            for (int i = 0; i < 6; i++)
            {
                series.Points.Add(new DataPoint(10 * i + 10, 5 * i + 5));
                // Custom label for data points
                var label = new CustomLabel(10*i + 20, "#" + i, 0);
                xAxis.CustomLabels.Add(label);
            }
        }
    }
}
```
