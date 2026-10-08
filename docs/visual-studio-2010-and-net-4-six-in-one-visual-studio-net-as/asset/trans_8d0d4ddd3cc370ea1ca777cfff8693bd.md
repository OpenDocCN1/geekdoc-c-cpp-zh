
当你调整应用程序窗口时，图表会自动更新其视图以适应新的窗口大小。关闭应用程序。

## 添加新图表区域

在表单设计器中，选择图表并再次显示系列集合编辑器（Series Collection Editor）（你可能还记得，它是 Chart 类别下的 `Series` 属性）。这次，通过 `Add` 按钮在此编辑器器中添加一个新系列，并设置五个数据点（`DataPoints` 集合编辑器）。这次，`XValue` 使用从 0 到 4 的范围，`YValues` 使用从 5 到 1 的递减范围。

运行应用程序时，你将看到图表中显示两个数据系列，如图 14-6 所示。

图表可以包含一个或多个图表区域，这些用于同时显示图表背后数据的视图。例如，你可以将图 14-6 中的系列显示在不同的图表区域中。

![](img/b5597c749e848b27b0d305153ae16106_637_0.png)

图 14-6：图表中显示的两个系列

在表单设计器中，选择图表并点击 Chart 类别下 `ChartAreas` 属性旁的省略号来启动 ChartArea 编辑器。使用 `Add` 按钮添加一个新的图表区域（将命名为 `Chartarea2`），并点击编辑器。你会注意到图表被准备在上方窗格中，而空面板保持为空。空区域为 `Chartarea2` 预留，但目前它不包含任何数据。

再次回到系列编辑器。选择 `Series2` 并将其 `Chartarea` 属性（你可以在 Chart 类别下找到它）设置为 `Chartarea2`。现在，你的第二个区域也包含一个数据视图。运行应用程序时，如图 14-7 所示，你将看到两个系列显示在不同的图表区域中。

![](img/b5597c749e848b27b0d305153ae16106_637_1.png)

图 14-7：拥有各自系列的两个图表区域

你的图表简单美观，但没有说明你在其中能看到什么。

## 设置标题和图例

为图表添加标题可以帮助用户理解他们看到的数据。`Chart` 控件允许你为图表添加一个或多个标题，这些标题可以分配给图表或其中一个图表区域。设置图表标题非常简单。

点击 Chart 类别下 `Titles` 属性旁的省略号启动标题集合编辑器。使用 `Add` 按钮创建一个新标题，然后设置其 `Text` 属性——你可以在 `Appearance` 类别下方找到命名为 `(Text)` 的属性——设置为“My Secret Data”（我的秘密数据）。展开 `Font` 属性并将 `Size` 设置为 12。你可以立即在设计视图看到新创建的标题，它位于图表的顶部。

现在，再添加两个标题，并将它们的 `Text` 属性设置为“Increasing Trend”（上升趋势）和“Decreasing Trend”（下降趋势）。选择 `Title2`，并在属性格中向下滚动到 `Docking` 属性。在这里你找到五个决定标题显示方式和对齐方式的属性。

将 `DockedToChartArea` 设置为 `ChartArea`。“Increasing Trend”显示在第一个图表区域内。将 `IsDockedInsideChartArea` 设置为 `False`，标题将移动到图表区域外部，并靠在顶部。将 `Docking` 属性更改为 `Bottom`，标题将移动到图表区域下方。

以类似于 Title2 的方式更改 Title3，但这种情况下将 `DockedToChartArea` 设置为 `Chart2`。运行应用程序时，你将在图表中看到三个标题，如图 14-8 所示。

当你创建一个图表时，会自动为其添加一个图例。你可以在图 14-8 中包含 `Series` 和 `Series2` 的窗口右上角看到这一点。默认图例停靠在图表上，但你可以将图例附加到图表上。

点击 Chart 类别下 `Legends` 属性旁的省略号启动图例集合编辑器，点击 `Add` 按钮创建一个新图例。新的 `Legend2` 也停靠在图表上，并与系列关联，因此它是空的，正如其设计表面上的占位符所示。关闭图例集合编辑器，进入“编辑图表”（Edit Charts）。

选择 `Series1`，向下滚动到 Chart 类别，并将 `Name` 属性设置为“Revenue”（收入）。更改系列名称将立即使用 `Series1` 的新名称更新图例。同样，将 `Series2` 重命名为“Cost”（成本）。你可以将系列附加到图例显示。默认情况下，所有系列都附加到 `Legend`。向下滚动到 `Cost` 的 `Legend` 属性（你可以在 Legend 类别下找到它）并将其附加到 `Legend2`。现在，`Cost` 系列从第一个图例移动到新图例，设计器表面立即反映了这一点。

现在，返回编辑图例。图例在 `Docking` 类别有一组属性，决定它们在图表中的显示方式。选择 `Legend1` 并向下滚动到 `Docking` 属性。将 `DockedToChartArea` 设置为 `ChartArea`。将 `Legend2` 的相同属性更改为 `ChartArea2`，并将 `IsDockedInsideChartArea` 设置为 `False`。这一系列操作将每个图例都移动到其图表区域的右侧，如图 14-9 所示。

![](img/b5597c749e848b27b0d305153ae16106_638_0.png)

图 14-8：分配给图表的标题

![](img/b5597c749e848b27b0d305153ae16106_638_1.png)

图 14-9：每个图都有自己的系列

## 添加三维效果

在许多情况下，三维效果可以提供更好的视觉效果。通过 `Chart` 控件，你可以更改轴、字体和渐变。启动 `ChartArea` 并 `3D` 属性设置为 `True`，`Depth` 设置为 4，`Width` 设置为 0。当你运行应用程序时，如图 14-10 所示，图表将三维显示。

![](img/b5597c749e848b27b0d305153ae16106_639_0.png)

图 14-10：三维图表

## 程序添加数据

手动添加的数据也可以通过程序创建。启动系列编辑器清除已添加的数据。选择 `Revenue` 系列。进入 `Points` 属性并点击省略号显示数据点编辑器。选择所有数据点（按住 Shift 键点击第一个点和最后一个点），点击删除。对 `Cost` 系列执行相同的操作。

在设计表面，选择 `MainForm` 并点击属性窗口中的事件。双击 `Load` 创建一个在表单加载时运行的事件方法。你将使用此方法设置数据。14-1 显示了 `MainForm.cs` 的完整代码（删除了未使用的语句）。

# 列表 14-1：MainForm.cs

![](img/b5597c749e848b27b0d305153ae16106_640_0.png)

```
using System;
using System.Windows.Forms;
using System.Windows.Forms.DataVisualization.Charting;

namespace ProcessInfoChart
{
    public partial class MainForm : Form
    {
        public MainForm()
        {
            InitializeComponent();
        }

        private void MainForm_Load(object sender, EventArgs e)
        {
            var revnSeries = chart.Series("Revenue");
            var costSeries = chart.Series("Cost");
            for (int i = 0; i < 5; i++)
            {
                revnSeries.Points.Add(new DataPoint(i, i + 1));
                costSeries.Points.Add(new DataPoint(i, 5-i));
            }
        }
    }
}
```

你可以通过图表的 `Series` 属性访问系列。然后你可以通过系列名称或位置进行索引。这里使用了名称。系列的数据点可以通过 `Points` 属性进行操作。在列表中，根据构造函数中指定的 `XValue` 和 `YValues` 添加新的 `DataPoint` 实例。
