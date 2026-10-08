Data binding is a general technology in the .NET framework that has several flavors. For example, Windows Forms, ASP.NET, and WPF technologies have a slightly different implementation for data binding — according to the differences in the technologies behind them.

The Chart control treated in this chapter uses the Windows Forms technology. To see a detailed description of Windows data binding in .NET 4, visit the MSDN page at http://msdn.microsoft.com/en-us/library/ef2xyb3(US.100).aspx.

While, at design-time, you can bind data to the chart only through the DataSource property, the Chart control has a few methods that allow you more control over this mechanism. Table 14-13 describes these methods.

# TABLE 14-13: Data-Binding Methods of the Chart Control

| METHOD | DESCRIPTION |
|---|---|
| DataBind | This method binds the Chart control to the specified data source. In cases where a data source is set to a chart, and no other data operations are required, the DataBind method does not have to be explicitly called. In these cases, the Chart itself will bind the data to the data source prior to being rendered. |
| DataBindTable | This method automatically creates and binds series to the specified data table, and optionally maps X-values. Each column of the table becomes a Y-value for a series, with one series per column. The X-value field of the series can also be provided. |
| DataBindCrossTable | Data binds a chart to the table, with one series created per unique value in a given column. |

You can use the ProcessInfoChart sample to use DataBind method instead of design-time. Change the code in MainForm.cs to that shown in Listing 14-11.

# LISTING 14-11: MainForm.cs Using the DataBindTable Method

```
using System;
using System.Windows.Forms;
using System.Windows.Forms.DataVisualization.Charting;
using System.Collections.Generic;

namespace ProcessInfoChart
```