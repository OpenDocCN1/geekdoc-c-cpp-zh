
# LISTING 14-9 (continued)

```csharp
LabelStyle.None;
XAxis.CustomLabels.Add(label);
}

// --- Custom labels
var lowerLabel = new CustomLabel(0, 30, "Lower part", 1, LabelMarkStyle.LineMark);
lowerLabel.ForeColor = Color.Red;
XAxis.CustomLabels.Add(lowerLabel);

var upperLabel = new CustomLabel(30, 70, "Upper part", 1, LabelMarkStyle.LineMark);
upperLabel.ForeColor = Color.Green;
XAxis.CustomLabels.Add(upperLabel);

var domainLabel = new CustomLabel(0, 70, "Entire domain", 3, LabelMarkStyle.None);
domainLabel.ForeColor = Color.Blue;
XAxis.CustomLabels.Add(domainLabel);
}
```

> Code file [Form1.cs] available for download at Wrox.com.

The `CustomLabel` constructor takes five arguments. The FromPosition and ToPosition values, and the third specify the text of the label. The fourth parameter sets the RowIndex of the label, while the fifth defines how marks should be drawn. Figure 14-44 shows the chart with the specified custom labels.

You can see from Listing 14-9 that, in the cycle creating the data points, all default labels are changed with custom ones. When you want to replace default labels, you add custom labels with RowIndex 0.

![](img/b5597c749e848b27b0d305153ae16106_671_0.png)

FIGURE 14-44: Custom labels

## Data Points

You can add a lot of customizations to your data points. You can set each data point in your chart to have a different style. Customization is much more than setting colors, borders, fonts, and styles. Listing 14-10 shows you the code of a simple application that decorates four data points with different adornments.

## LISTING 14-10: Data Point Customization

![](img/b5597c749e848b27b0d305153ae16106_672_0.png)

```csharp
using System;
using System.Drawing;
using System.Windows.Forms;
using System.Windows.Forms.DataVisualization.Charting;
```

```csharp
namespace DataPointSample
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            var series = chart.Series[0];

            var dp1 = new DataPoint(0.0, 15.0);
            dp1.Color = Color.Black;
            dp1.BorderWidth = 3;
            dp1.Color = Color.LightGreen;
            series.Points.Add(dp1);

            var dp2 = new DataPoint(1.0, 10.0);
            dp2.Color = Color.Red;
            dp2.CustomProperties["Style"] = "Cylinder";
            dp2.MarkerStyle = MarkerStyle.Diamond;
            dp2.MarkerSize = 20;
            dp2.Color = Color.Goldenrod;
            series.Points.Add(dp2);

            var dp3 = new DataPoint(2.0, 20.0);
            dp3.CustomProperties["Style"] = "Diagonal";
            dp3.MarkerStyle = MarkerStyle.Border;
            dp3.Color = Color.DarkBlue;
            series.Points.Add(dp3);

            var dp4 = new DataPoint(3.0, 18.0);
            dp4.CustomProperties["Style"] = "Wedge";
            dp4.Font = new Font("Calibri", 18);
            series.Points.Add(dp4);
        }
    }
}
```

You can see from Listing 14-9 that, in the cycle creating the data points, all default labels are changed with custom ones. When you want to replace default labels, you add custom labels with RowIndex 0.

![](img/b5597c749e848b27b0d305153ae16106_671_0.png)

FIGURE 14-44: Custom labels

## Data Points

You can add a lot of customizations to your data points. You can set each data point in your chart to have a different style. Customization is much more than setting colors, borders, fonts, and styles. Listing 14-10 shows you the code of a simple application that decorates four data points with different adornments.
