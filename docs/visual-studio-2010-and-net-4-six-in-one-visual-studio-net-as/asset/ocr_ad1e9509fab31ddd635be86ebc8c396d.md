# LISTING 14-9 (continued)

```
LabelStyle.None;
XAxis.CustomLabels.Add(label);
}

// --- Custom labels
var lowerLabel = new CustomLabel(0, 30, "Lower part", 1,
LabelMarkStyle.LineMark;
lowerLabel.ForeColor = Color.Red;
XAxis.CustomLabels.Add(lowerLabel);

var upperLabel = new CustomLabel(30, 70, "Upper part", 1,
LabelMarkStyle.LineMark;
upperLabel.ForeColor = Color.Green;
XAxis.CustomLabels.Add(upperLabel);

var domainLabel = new CustomLabel(0, 70, "Entire domain", 3,
LabelMarkStyle.None;
domainLabel.ForeColor = Color.Blue;
XAxis.CustomLabels.Add(domainLabel);
}

```

> Code file [Form1.cs] available for download at Wrox.com.

The CustomLabel constructor takes five arguments. The FromPosition and ToPosition values, and the third specify the text of the label. The fourth parameter sets the RowIndex of the label, while the fifth defines how marks should be drawn. Figure 14-44 shows the chart with the specified custom labels.

You can see from Listing 14-9 that, in the cycle creating the data points, all default labels are changed with custom ones. When you want to replace default labels, you add custom labels with RowIndex 0.

![](bbox=[0.473, 0.531, 0.856, 0.796])

FIGURE 14-44: Custom labels

# Data Points

You can add a lot of customizations to your data points. You can set each data point in your chart to have a different style. Customization is much more than setting colors, borders, fonts, and styles. Listing 14-10 shows you the code of a simple application that decorates four data points with different adornments.