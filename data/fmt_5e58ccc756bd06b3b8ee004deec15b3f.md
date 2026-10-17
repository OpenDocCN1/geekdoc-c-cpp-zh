
`CustomLabel` 构造函数接受五个参数。`FromPosition` 和 `ToPosition` 值以及第三个参数指定标签的文本。第四个参数设置标签的 `RowIndex`，而第五个参数定义了绘制标记的方式。图 14-44 显示了带有指定自定义标签的图表。

从代码列表 14-9 可以看出，在创建数据点的循环中，所有默认标签都被自定义标签替换。当你想要替换默认标签时，添加 `RowIndex` 为 0 的自定义标签。

![](img/b5597c749e848b27b0d305153ae16106_671_0.png)

图 14-44：自定义标签

## 数据点

你可以对数据点添加许多自定义内容。你可以设置图表中的每个数据点具有不同的样式。自定义远不止设置颜色、边框、字体和样式。代码列表 14-10 显示了一个简单应用程序的代码，该程序使用不同的装饰装饰了四个数据点。

### 代码列表 14-10：数据点自定义

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

| 注释类型 (ANNOTATION TYPE) | 描述 (DESCRIPTION) |
| --- | --- |
| PolygonAnnotation | 代表多边形注释，派自 `PolyLineAnnotation`。你可以使用标准属性来设置多边形的填充区域。 |
| ImageAnnotation | 代表图像注释。`Image` 属性指定了要使用的图像名称。`ImageWrapMode` 设置图像的绘制模式。你可以使用 `ImageTransparentColor` 定义一种颜色，在绘制图像时该颜色将被替换为透明色。 |
| AnnotationGroup | 代表一组注释，并实现了组合设计模式。此外，它将嵌套的装饰器映射到 `Annotations` 集合属性中。 |

图 14-47 显示了一个带有几个注释的简单图表。

![](img/b5597c749e848b27b0d305153ae16106_676_0.png)

**图 14-47：** 带有注释的图表

图中共有四个注释。有一个用于图表区域的 `RectangleAnnotation`，其中包含“Does not tell. ...”文本。其他三个注释锚定在数据点上。Visual Basic 数据点包含一个 `CalloutAnnotation`，而 F# 数据点有两个注释——`ArrowAnnotation` 和一个 `TextAnnotation`。

### 锚定注释

注释可以属于图表区域的锚点，也可以锚定在某个数据点上。在指定注释的位置和大小时，有两种方式可以使用这些值：

- 将注释的 `AxisX`、`AxisY` 或这两个属性的组合都设置为 `ChartArea` 对象的 `AxisX` 和 `AxisY` 属性。
- 使用 `AnchorDataPoint` 属性将注释锚定到数据点。在这种情况下，其位置将自动计算。在设计时间期间，属性网格允许你从已添加到图表系列中选择数据点。

表 14-10 描述了一些以 `Anchor` 前缀开头的属性，它们定义了注释将如何被锚定。

#### 表 14-10：锚定属性

| 属性 (PROPERTY) | 描述 (DESCRIPTION) |
|---|---|
| Anchorage | 获取或设置注释相对于锚点的对齐方式。注释必须通过使用 `AnchorDataPoint` 属性或设置 `AnchorX` 和 `AnchorY` 属性来锚定。其 X 和 Y 属性必须为 NaN [设计模式下为 NotSet]。 |
| AnchorDataPoint | 获取或设置注释锚定的数据点。注释锚定在指定数据点的 X 和 Y 值上，并自动使用相同的轴。若要相对于数据点自动定位注释，请确保其 X 和 Y 属性设置为 NaN。`AnchorAlignment` 属性可以用于更改注释相对于锚点的自动对齐方式。当你使用此属性时，`AnchorX` 和 `AnchorY` 属性被设为 Double。将此值设置为引用值（Visual Basic 中为 `Nothing`）可以禁用对数据点的锚定。 |
| AnchorOffsetX | 获取或设置注释 X 位置的偏移量。 |
| AnchorOffsetY | 获取或设置注释 Y 位置的偏移量。 |
| AnchorX | 获取或设置注释锚定的 X 坐标。若要相对于锚点自动定位注释，请确保 X 属性设置为 NaN。`AnchorAlignment` 属性可以用于更改注释相对于锚点的自动对齐。`AnchorOffsetX` 和 `AnchorOffsetY` 属性可添加额外的间距。此属性的优先级高于 `AnchorDataPoint`。 |
| AnchorY | 获取或设置注释锚定的 Y 坐标。 |

### 移动注释

默认情况下，注释固定在图表区域的。由于它们使用相对坐标系，你可以调整图表和注释的大小并保持它们的相对位置。

通过几个属性，允许用户使用鼠标选择、调整大小和移动注释。这是一项强大的功能，因为你可以创建在运行时添加和放置注释的应用程序。

图 14-48 显示了图 14-47 中的 `RectangleAnnotation` 如何被选择、调整大小和移动。

![](img/b5597c749e848b27b0d305153ae16106_677_0.png)

在图 14-48 中，可以看到 `RectangleAnnotation` 被选中、调整了大小并移动。要启用此功能，必须将 `Interactivity` 属性设置为 true。在本章之前，你在表 14-9 中看到了哪些属性会影响注释。

| 属性 (PROPERTY) | 描述 (DESCRIPTION) |
|---|---|
| AllowMoving | 指定是否允许用户移动注释。 |
| AllowEditing | 指定是否允许用户编辑注释。 |
| AllowPath | 指定是否允许用户编辑路径。 |
| AllowResizing | 指定是否允许用户调整注释大小。 |
| AllowSelection | 指定是否允许用户选择注释。 |
| AllowText | 指定是否允许用户选择文本。 |

如果你计划调整注释，必须将 `Interactivity` 属性设置为 true。表 14-12 描述了这些事件。

#### 表 14-12

| 事件 (EVENT) | 描述 (DESCRIPTION) |
|---|---|
| Placed | 当放置注释时发生。 |
| PositionChanged | 当位置更改时发生。 |
| PositionChanging | 位置即将更改时发生。此事件使用 `PositionChangingEventArgs` 参数，允许在更改之前检查新位置。 |
| SelectionChanged | 当选择更改时发生。 |
| TextChanged | 当文本更改时发生。 |

## 将数据绑定到系列

在本章之前，你看到了一些示例（代码 14-2 和 14-3），它们使用 `DataSource` 属性来绑定数据。`DataSource` 属性接受许多类型的数据，包括：

- DataView
- DataSet
- Arrays
- Lists
- SqlCommand/OleDbCommand
- SqlDataAdapter/OleDataAdapter
- IEnumerable

你可以通过 `XValueMember` 和 `YValueMember` 属性将数据绑定到系列。数据绑定也可以用于从数据源到图表其他属性的信息。

数据绑定是 .NET 框架中的通用技术，有多种形式。例如，Windows Forms、ASP.NET 和 WPF 技术的绑定实现略有不同。本章的 Chart 控制使用的是 Windows Forms 技术。要查看 Windows 数据绑定的详细说明，请访问 MSDN 页面：http://msdn.microsoft.com/en-us/library/ef2xyb3(US.100).aspx。

虽然在设计时间你只能通过 `DataSource` 属性将数据绑定到图表，但 Chart 控制有一些方法允许你对该机制进行更多控制。表 14-13 描述了这些方法。

### 表 14-13：Chart控件的数据绑定方法

| 方法 (METHOD) | 描述 (DESCRIPTION) |
|---|---|
| DataBind | 此方法将 Chart 控制绑定到指定的数据源。在将数据源设置为图表且不需要其他数据操作的情况下，不需要显式调用 `DataBind` 方法。在这些情况下，Chart 本身会在渲染之前将数据绑定到数据源。 |
| DataBindTable | 此方法自动创建并将系列绑定到指定的数据表，并可选地映射 X 值。表的每列都成为系列的 Y 值，每列对应一个系列。也可以提供系列的 X 值字段。 |
| DataBindCrossTable | 数据绑定将图表绑定到表，为列中的每个唯一值创建一个系列。 |

你可以使用 `ProcessInfoChart` 示例来使用 `DataBind` 方法代替设计时间绑定。将 `MainForm.cs` 中的代码更改为代码 14-11 所示。

### 代码 14-11：使用 DataBind 方法的 MainForm.cs

```go
using System;
using System.Windows.Forms;
using System.Windows.Forms.DataVisualization.Charting;
using System.Collections.Generic;

namespace ProcessInfoChart
```

## 列表 14-11（续）

```sharp
public partial class MainForm : Form
{
    public MainForm()
    {
        InitializeComponent();
    }
    private void MainForm_Load(object sender, EventArgs e)
    {
        chart1.DataSource = null;
        var processes = new List<ProcessInfo>(ProcessList.GetTopSet(10));
        chart1.Series.Clear();
        chart1.DataTable(processes, "Name");
        chart1.Series[1].ChartArea = "ChartArea2";
        chart1.Series[1].Legend = "Legend";
    }
}
```

> 代码文件 `MainForm.cs` 可在 Wrox 下载。

因为 `DataTable` 会创建一个新的系列，这会清空 `Series` 集合，然后直到 `Series[1]` 使用第二个图表区域和实际图例。

你可以直接通过 `Series.Points` 属性绑定数据（其类型为 `DataPoint Collection`）。表 14-14 描述了 `DataPointCollection` 实例可用的数据绑定方法。

### 表 14-14：DataPointCollection 的数据绑定方法

| 方法 | 描述 |
|---|--- |
| DataBind | 将数据点的 X 值、Y 值(s) 和属性值（如 Tooltip 或 LabelStyle）绑定到数据源。 |
| DataBindXY | 将集合中数据点的 X 值和 Y 值(s)绑定到指定数据源的指定列。 |
| DataBindY | 将数据点的 Y 值(s) 绑定到指定数据源的指定列。 |

你可以修改 `ProcessInfoChart` 示例以使用系列的的数据绑定方法。将 `MainForm.cs` 中的代码更改为列表 14-12 所示的代码。

### 列表 14-12：使用 DataBindXY 方法的 MainForm.cs

![](img/b5597c749e848b27b0d305153ae16106_682_0.png)

```csharp
using System;
using System.Windows.Forms;
using System.Windows.Forms.DataVisualization.Charting;
using System.Collections.Generic;
```

```csharp
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
            chart1.DataSource = null;
            var processes = new List<ProcessInfo>(ProcessList.GetTopWorkingSet(10));
            var series1 = chart1.Series[0];
            series1.Points.DataBindXY(processes, "Name", processes, "WorkingSet");
            var series2 = chart1.Series[1];
            series2.Points.DataBindXY(processes, "Name", processes, "PeakWorkingSet");
        }
    }
}
```

代码文件 `MainForm.cs` 可在 Wrox.com 下载。

> 表 14-13 和表 14-4 中的方法对它们可以接受的数据类型有若干限制。它们也有一些优缺点。你可以在 MSDN 文档中查看它们：http://msdn.microsoft.com/en-us/library/dd456766(VS.100).aspx。

## 数据操作器 (DataManipulator)
