# # Chart Types

The Chart control can display more than 30 types of charts. Some of them are general-purpose chart types — like Column, Bar, and Area charts — but there are a few of them that have special applications — such as Stock, Polar, or Radar charts. You can set the chart type separately for each series, and each has exactly one chart type.

The ChartType property of a Series instance holds the chart type defining how the specific series is displayed. It takes the value from the SeriesChartType enumeration. One chart area may contain one or more series, and each may use separate chart types.

However, not all charts are compatible with each other — they cannot be shown in the same chart area. If you try to use incompatible charts together, you will get the following error messages:

+   - In design mode, the chart appears and the following message is displayed in the chart placeholder: "Chart Preview is not available. An action that you have performed caused failure in Chart Preview."
- At run-time, an InvalidOperationException is raised with the message: "The chart area contains incompatible chart types."

When you add data points to a series, each DataPoint instance may exactly one X value (defined by the XValue property) or one or more Y values (defined by the YValues property). Earlier in this process, you sample using only one Y value per data point, but there are chart types (for example Range, Bar, Candlestick, and Stock charts) that require more than two or four Y values.

Series has a property YPerPoint with a default value of 1. When you select the chart type, this will be automatically updated to the required number of Y values for the selected chart type. When you define a data point manually, you can set a comma-separated list of double values in the YValues property of a DataPoint. If you set the values programmatically, YValues is represented as a double array (double[], in C#), so you can use an array to set this property.

Series and DataPoint instances have custom properties that vary with chart types. For example, column and bar charts have a DrawStyle property defining how the column or bar is drawn (flat, cylinder, embedded, and so on).

![](bbox=[0.535, 0.755, 0.928, 0.893])

FIGURE 14-18: Column chart with two series

# # Column and Bar Charts

The most frequently used charts are column charts representing each value as a column. This is the default type for a series. Figure 14-18 shows a column chart with two series.