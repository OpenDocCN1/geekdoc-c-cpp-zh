
接下来，代码为窗口创建了一个 `VisualBrush`。`VisualBrush` 使用某些视觉对象（如控件，或者在本例中为程序的主窗口）的图像来填充区域。代码创建了一个矩形，将其放置在 `Viewbox` 内部，并用刷器填充它。

此时，所有用于在打印页面上以正确大小并居中显示 `Viewbox` 的对象都已就位。代码还需要执行最后两个步骤。

首先，它调用 `Grid` 的 `Arrange` 方法让子元素进行自我排列。其次，代码调用 `PrintDialog` 的 `PrintVisual` 方法来打印 `Grid`。

www.it-ebooks.info

图 30-4 显示了结果的预览。为了制作这张图，我在 `PrintDialog` 中选择 Microsoft XPS Document Writer，将窗口打印到 XML 纸张规范 (XPS) 文件。然后，我双击 XPS 文件，在图 30-4 所示的 XPS 查看器中显示它。你可以从图中看到窗口的图像是居中的。

![](img/73c7d7cb173bc2ebb3d8a9797355a5f3_468_0.png)

图 30-4

在图 30-4 中，窗口的图像看起来有些颗粒感且像素化了，但那是由于 XPS 查看器显示文档的方式造成的。文档本身是以极高分辨率生成的。在图 30-5 中，查看器将文档放大了 265%，所以你可以看到结果实际上非常平滑，最终的打印输出可以利用打印机较高的分辨率。

![](img/73c7d7cb173bc2ebb3d8a9797355a5f3_468_1.png)

图 30-5

www.it-ebooks.info

“放大打印窗口”示例程序与“居中打印窗口”程序类似，但它使用以下代码将 `Thickness` 对象作为边距传递给 `PrintWindowCentered` 方法。这将窗口图像拉伸以填充减去 5 像素边距后的可打印区域。

```csharp
// 打印放大的窗口图像。
private void printButton_Click(object sender, RoutedEventArgs e)
{
    PrintDialog printDialog = new PrintDialog();
    if (printDialog.ShowDialog() == true)
    {
        PrintWindowCentered(printDialog, this, "New Customer",
            new Thickness(5));
    }
}
```

图 30-6 显示了结果。注意窗口图像是居中的并填充了大部分可打印区域。

![](img/73c7d7cb173bc2ebb3d8a9797355a5f3_469_0.png)

图 30-6

除了 `PrintVisual`，`PrintDialog` 类提供了 `PrintDocument` 方法，可以打印 `FlowDocuments` 或 `FixedDocuments` 等多个对象。遗憾的是，这些主题在这里没有介绍。如果你需要这些功能，可以在网上找到更多信息：

- [`PrintDocument`](https://learn.microsoft.com/library/windows/controls/printdocument.aspx)
- [`FixedDocument`](https://learn.microsoft.com/library/windows/documents/fixeddocument.aspx)
- [`FlowDocument`](https://learn.microsoft.com/library/windows/documents/flowdocument.aspx)

## 尝试一下

在这里，创建一个打印并显示图 30-7 所示表格的程序。创建一个 `Student` 对象数组，然后遍历它们，显示图中所示的值。

![](img/73c7d7cb173bc2ebb3d8a9797355a5f3_470_0.png)

图 30-7

## 要求

在本节中，：

- 添加一个新的 Windows Forms 项目并创建程序主窗。
- 在打印和预览部分添加 `PrintDocument` 和 `PreviewDialog` 组件。
- 添加带有事件处理程序的打印和预览按钮。
- 添加带有 `FirstName` 和 `LastName` 属性的 `Student` 类。并给它一个整数数组 `TestScores` 属性。
- 创建 `PrintPage` 事件处理器。
- 创建 `Student` 对象数组。使用数组初始化器初始化它们。
- 遍历 `Student` 对象并打印它们。
- 在表格周围画一个矩形。

> 注意你可以从网站下载本节的代码和资源：https://www.microsoft.com/csharp24hour

## 提示

此示例没有对 `Student` 属性进行任何特殊处理，因此它们可以是自动实现的。定义 `x0`、`x1` 等变量来跟踪每一列会有帮助。

## 步骤

- 开始一个新的 Windows Forms 项目并创建程序主窗。在打印和预览部分添加 `PrintDocument` 和 `PreviewDialog` 组件。
- 添加带有事件处理程序的打印和预览按钮。这非常直观。
- 使用类似下面的代码：

```csharp
// 显示打印预览。
private void previewButton_Click(object sender, EventArgs e)
{
    textPreviewDialog.ShowDialog();
}

// 打印。
private void printButton_Click(object sender, EventArgs e)
{
    textDocument.Print();
}
```

- 添加带有 `FirstName` 和 `LastName` 属性的 `Student` 类。并给它一个整数数组 `TestScores` 属性。使用类似下面的代码：

```csharp
class Student
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public int[] TestScores { get; set; }
}
```

- 创建 `PrintPage` 事件处理器。
- 创建 `Student` 对象数组。使用数组和初始化器初始化它们。
- 遍历 `Student` 对象并打印它们。
- 在表格下方画一个矩形。使用类似下面的代码：

```csharp
// 打印表格。
private void textPrintDocument_PrintPage(object sender, System.Drawing.Printing.PrintPageArgs e)
{
    // 制作一些数据。
    Student[] students =
    {
        new Student() { FirstName="Ann", LastName="Archer", TestScores=new int[] {91, 92, 93, 94} },
        new Student() { FirstName="Bob", LastName="Blarth" }
    };
```

```csharp
    TestScores=new int[] {81, 82, 83, 84}},
    new Student() {FirstName="Cyd", LastName="Carter",
    TestScores=new int[] {71, 72, 73, 74}},
    new Student() {FirstName="Dan", LastName="Deever",
    TestScores=new int[] {61, 62, 63, 64}};
};

// 设置第一行和列的坐标。
int y = e.MarginBounds.Top;
int x0 = e.MarginBounds.Left;
int x1 = x0 + 200;
int x2 = x1 + 100;
int x3 = x2 + 100;
int x4 = x3 + 100;

// 创建一个使用的字体。
using (Font font = new Font("Times New Roman", 20)) {
    // 绘制表头
    e.Graphics.DrawString("Name", font, Brush.Black, x0, y);
    e.Graphics.DrawString("Test 1", font, Brush.Black, x1, y);
    e.Graphics.DrawString("Test 2", font, Brush.Black, x2, y);
    e.Graphics.DrawString("Test 3", font, Brush.Black, x3, y);
    e.Graphics.DrawString("Test 4", font, Brush.Black, x4, y);
    // 为第一行移动 Y
    y += 30;

    // 遍历学生显示他们的数据。
    foreach (Student student in students) {
        // 显示学生的值。
        e.Graphics.DrawString(student.FirstName + " " + 
            student.LastName, font, Brush.Black, x0, y);
        e.Graphics.DrawString(student.TestScores[0].ToString(),
            font, Brush.Black, x1, y);
        e.Graphics.DrawString(student.TestScores[1].ToString(),
            font, Brush.Black, x2, y);
        e.Graphics.DrawString(student.TestScores[2].ToString(),
            font, Brush.Black, x3, y);
        e.Graphics.DrawString(student.TestScores[3].ToString(),
            font, Brush.Black, x4, y);
        // 为下一行移动 Y。
        y += 30;
    }

    // 为所有内容画一个框。
    e.Graphics.DrawRectangle(Pens.Black,
        x0, e.MarginBounds.Top,
        x4, x0 + 100,
        y - e.MarginBounds.Top);

    // 我们只打印一页。
    e.HasPages = false;
}
}
```

## 练习

- 1. 复制你在本节“尝试一下”（Try It）中构建程序，并在行和列之间添加线条。
- 2. 编写一个程序，打印类似于图 30-8所示所示条形图。（提示：为条形选择一些“随机”值。）

![](img/73c7d7cb173bc2ebb3d8a9797355a5f3_473_0.png)

图 30-8

- 3. 复制你为练习 2 构建的程序，并修改它使文本值在条形上方居中显示。（提示：使用 `StringFormat` 对象。）
- 4. 构建一个包含具有项目（Item）、数量（Quantity）、单价（Unit price）和总计（Total）列的 `Grid` 控件的程序。创建显示网格数据的打印（Print）和预览（Preview）菜单。照常添加 `PrintDocument` 和 `PrintPreviewDialog` 控件。`PrintPage` 事件处理器应该：
    - a. 调用 `EndEdit` 方法收集当前的编辑内容（如果有）。
    - b. 遍历 `Grid` 的 `Columns` 集合，显示列标题。将每列的 `Width` 加到下一列的 X 坐标上。
    - c. 遍历 `Grid` 的 `Rows` 集合。对于每一行，遍历 `Cells` 集合，显示单元格的 `FormattedValue` 属性。
- 5. 复制你为练习 4 构建的程序，在行和列之间添加线条，并在表格周围画一个框。
- 6. 复制本节中描述的放大的打印窗口（在本节的下载资源中可用）。修改它使其横向打印窗口以填充更多的打印页面。提示：修改 `PrintWindowCentered` 方法，使其使用页面的可打印宽度和高度分别绘图网格的高度和宽度。然后将网格的 `LayoutTransform` 属性设置为一个 `RotateTransform` 对象，将其旋转 90°。创建网格的代码应该如下：

```
drawingGrid = new Grid();
drawingGrid.Width = printDialog.PrintableAreaHeight;
drawingGrid.Height = printDialog.PrintableAreaWidth;
drawingGrid.LayoutTransform = new RotateTransform(90);
```

- 7. [WPF] WPF 示例是通过打印窗口的图像来描述的，但类似的技术适用于任何视觉对象，如 `Grid`、`StackPanel` 或 `TextBox`。

对于此练习，构建一个包含 `TabControl` 的 WPF 程序。为它提供三个 `TabItem`（选项卡）。设置每个 `TabItem` 的 `Header`（页头）属性，并在页页边距内放置一个 `Grid`。在 `Grid` 内部放置一些 `Label`、`TextBox` 和其他控件。最后，为每个选项卡提供一个 `Button`。如果你不想自己构建控件，可以下载本节提供的练习 30-7a 程序作为起点。该项目定义了用户界面，但没有任何代码。

要进行打印，请使用前面程序中的 `PrintWindow` 方法，并进行以下几点：

- 将方法重命名为 `PrintGridCentered`。
- 使方法接受 `Grid` 作为参数而不是 `Window`。
- `Grid` 控件没有宽度或高度，因此其 `Width` 和 `Height` 属性不返回有意义的值。使用需要的 `ActualWidth` 和 `ActualHeight` 属性。
- 为了避免代码重复，编写一个 `PrintGrid` 方法，接收 `Grid`、标题字符串和 `Thickness`。它应该显示一个 `PrintDialog`，如果用户点击打印，它应该调用 `PrintGridCentered` 执行实际打印。

- 8. 编写一个 Windows 程序，预览并打印包含以下步骤的四个页面，使用 10 像素宽的线条概述：
    - 红色矩形
    - 绿色椭圆
    - 蓝色三角形
    - 紫色菱形

使形状在页边距内尽可能大，并用黑色虚线勾勒页面。

提示：要绘制三角形和菱形，使用带有 `Point` 数组的 `DrawPolygon` 方法。你可以根据需要更改其 `Color` 和 `DashStyle` 属性，使用同一个 `Pen` 来完成所有绘图。

- 9. [困难]假设你正在制作一本小册，你想让奇码页左侧缩进，偶码页右侧缩进，以便为装订留出空间。（这种额外的缩进被称为“装订页”）。编写一个 Windows Forms 程序，预览并打印 10 页具有 100 单位装订页的页面。在页边距周围画框，并在页边距内部、靠近装订页对侧的顶角显示页码。提示：

* 使用 `PrintDocument` 的 `QueryPageSettings` 事件设置边距。它应该处理三种情况：
    * 对于第一页，在 `e.PageSettings.Margins.Left` 上加 100。
    * 对于后续的奇数页，在左边距加 100，从右边距减去 100。
    * 对于偶数页，从左边距减去 100，在右边距加 100。
* 使用 `StringFormat` 对象的 `Alignment` 和 `LineAlignment` 属性来定位页码。

记住，`QueryPageSettings` 处理的是边距（margins），而不是边界（bounds）。例如，在右边距上加 100 会使边距边界的右边缘距离页面边缘远 100 单位。（是的，这可能会令人困惑。）

> 注意 请在 www.wrox.com/go/csharp24hourtrainer2evideos 选择第 30 节的在线视频。

## 第六部分

## Windows 应用程序

书的前几个部分侧重于桌面应用程序，但本节涵盖了 Windows Store 和 Windows Phone 应用程序。这些应用程序是为平板电脑和手机设计的。虽然为桌面应用程序学习的许多技术仍然适用，但这些应用程序的工作和行为有一些关键区别。

## Windows Store 应用程序

本节介绍了如何构建 Windows Store 风格的应用程序。请注意，你并不需要将这些应用程序上传 Windows Store。如果你喜欢，可以在计算机上本地构建并运行它们。在这里，“Windows Store 应用程序”意味着它们具有与 Store 中提供的应用程序类似的样式。

## 导航样式

Store 和手机应用程序在多个方面与桌面应用程序不同。一个很大的区别是它们如何处理设备空间。桌面应用程序通常与其他应用程序共享桌面，你可以最小化、最大化、调整大小、重新排列和关闭它们。Store 和手机应用程序通常覆盖整个设备。你可以在不同的应用程序之间切换，但无法调整大小和重新排列应用程序以同时查看多个。

由于 Store 和手机应用程序不显示多个窗口，因此通常使用与桌面应用程序不同的导航模型。桌面应用程序可能会显示多个对话框和其他窗口，你可以根据需要并在它们之间导航。
