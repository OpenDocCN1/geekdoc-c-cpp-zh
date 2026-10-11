
这就完成了程序的生命周期。当程序启动时，它调用 `LoadSkin` 加载红色皮肤。`LoadSkin` 加载控件并绑定它们的事件处理程序。特别是，它为 `pgnSkin` “切换皮肤”控件的 `MouseDown` 事件挂载了事件处理程序。当你点击多边形时，`pgnSkin_MouseDown` 事件执行并调用 `LoadSkin` 重新开始该过程。

# 304 | 第 17 章 打印

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_341_0.png)

图 17-1

## 文档图片

为了显示本章中的文档图片，我选择了 Microsoft XPS Writer 将输出保存为 XPS 文件。然后，我在 Internet Explorer 中打开了该文件（如图 17-1 所示），或使用 XPS Viewer 打开（如图 17-4 所示）。

遗憾的是，Internet Explorer 和 XPS Viewer 并不总是显示与打印机产生的相同结果。在整个章节中，当打印结果与插图显著不同时，我会注明。

## 打印视觉对象

WPF 打印的核心类之一是 `PrintDialog`。该类提供了相关方法，允许用户选择打印机、与打印队列交互，并将输出发送到打印机。

### 复习你的编程技能

WPF 不包含一个可以放置在窗口中的 `PrintDialog` 控件，XAML 代码也无法操作它。对于面向打印机的任务，你必须编写一些后台代码（code-behind）。

通常，打印有三个步骤：

- 1. 创建一个新的 `PrintDialog` 对象并使用其 `ShowDialog` 方法将其显示给用户。
- 2. 检查 `ShowDialog` 的返回结果，查看用户是否点击了 OK。
- 3. 使用 `PrintDialog` 的方法生成打印输出。

图 17-2 显示了 `PrintDialog.ShowDialog` 方法显示的对话框。从顶部的列表中选择打印机。点击“首选项”（Preferences）按钮设置打印机的高级选项，如纸盒、草稿或正常分辨率，以及纵向或横向方向。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_342_0.png)

图 17-2

接下来的章节将介绍两种打印视觉对象（Visual objects）的方法。第一简单但效果平平；第二种工作量较大，但输出结果好得多。

### 使用 PrintVisual 进行简单打印

`SimplePrintWindow` 示例程序使用以下代码执行这三个步骤：

```csharp
// 显示打印对话框。
PrintDialog pd = new PrintDialog();

// 查看用户是否点击了 OK。
if (pd.ShowDialog() == true)
{
    pd.PrintVisual(this, "New Customer");
}

SimplePrintWindow
```

在显示对话框并确认用户按了 OK 后，代码调用了 `PrintVisual` 方法，并将程序的窗口传递给它。`PrintDialog` 对象知道用户选择的打印机，并将视觉对象（在本例中为窗口）发送到打印机队列。

> 打印提示：如果你在不显示对话框的情况下调用 `PrintVisual`，则打印输出将立即发送到默认打印机。

# 306 | 第 17 章 打印

这非常简单，但有一个遗憾的缺点：WPF 尝试将视觉内容绘制在纸张的左上角。由于打印机通常无法打印到纸张边缘，结果会被裁切。

> 比打印更好
>
> 如果你选择 Microsoft XPS Document Writer 作为打印机，结果与你从打印机出来的看到的内容不同。页面大小将适应视觉对象，由于 Document Writer 可以打印到其逻辑纸张的边缘，因此结果不会被裁切。

`PrintVisual` 方法极其简单，但不会产生非常理想的结果。它在顶部和左边缘被裁切，并且无法对其进行旋转、缩放或居中。

接下来的章节描述了一种更灵活的打印方法。

### 使用 PrintVisual 进行高级打印

`PrintVisual` 方法将一个 `PrintVisual` 对象发送到打印机，但它不会对对象进行缩放、旋转或居中。坦率地说，这些是由你的程序完成的工作。

与其将程序传递给 `PrintVisual` 方法，不如你创建一个包含窗口图像的控件层次结构。这种层次结构可以使用 `Grid`、`Viewbox`、`Image`、`Rectangle` 以及任何你想生成结果的控件。它甚至可以包含额外的控件来生成页眉和页脚等项目。

`PrintWindow` 示例程序展示了这种方法，将其窗口在正常或放大比例下居中打印。点击“居中打印”（Print Centered）按钮以正常比例打印窗口。点击“拉伸打印”（Print Stretched）按钮在页面上尽可能地打印窗口。

`PrintWindow` 程序需要对 `ReachFramework` 和 `System.Printing` 库的引用。在 Visual Studio 中，打开项目并选择“添加引用”（Add Reference）。选择这两个库并点击 OK。

为了让这些库的使用更加简单，程序包含了以下 `using` 语句：

```csharp
using System.Printing;
using System.Windows.Media.Effects;
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_343_0.png)

图 17-3

程序的 Visual Basic 版本包含以下 `Imports` 语句：

```vbnet
Imports System.Windows.Shapes
Imports System.Windows.Media.Effects
```

当你点击它时，`PrintWindow` 程序使用以下代码开始打印过程。两个对话框都使用 `PrintDialog`，如果用户选择了选择器并点击了 OK，将调用 `PrintWindowCentered` 来完成所有有趣的工作。

```csharp
// 居中打印窗口。
private void btnPrintCentered_Click(object sender, RoutedEventArgs e)
{
    PrintDialog pd = new PrintDialog();
    if (pd.ShowDialog() == true)
{
        pd.PrintVisual(this, "New Customer");
    }
}
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_344_0.png)

```csharp
// 拉伸打印窗口。
private void btnPrintStretched_Click(object sender, RoutedEventArgs e)
{
    PrintDialog pd = new PrintDialog();
    if (pd.ShowDialog() == true)
{
    PrintWindowCentered(pd, this, "New Customer", null);
}
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_344_1.png)

以下代码是 `PrintWindowCentered` 函数：

```csharp
// 在打印机上居中打印。
private void PrintWindowCentered(PrintDialog pd, Window win,
String title, Thickness margin)
{
    // 创建一个 Grid 来持有内容。
    Grid drawing_area = new Grid();
    drawing_area.Width = pd.PrintableAreaWidth;
    drawing_area.Height = pd.PrintableAreaHeight;

    // 创建一个 Viewbox 来拉伸结果。
    Viewbox view_box = new Viewbox();
    drawing_area.Children.Add(view_box);
    view_box.HorizontalAlignment = HorizontalAlignment.Center;
    view_box.VerticalAlignment = VerticalAlignment.Center;

    if (margin == null)
    {
        // 不缩放居中。
        view_box.Stretch = Stretch.None;
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_344_2.png)

```csharp
    } else
    {
        // 适应边距进行缩放。
        view_box.Margin = margin.Value;
        view_box.Stretch = Stretch.Uniform;
    }

    // 使用 VisualBrush 持有窗口的图像。
    VisualBrush vis_br = new VisualBrush(win);

    // 创建一个与窗口大小相同的矩形。
    Rectangle win_rect = new Rectangle();
    view_box.Child = win_rect;
    win_rect.Width = min.Width;
    win_rect.Height = min.Height;
    win_rect.Fill = vis_br;
    win_rect.Stroke = Brushes.Black;
    win_rect.BitmapEffect = new DropShadowBitmapEffect();

    // 排版以产生输出。
    Rect rect = new Rect(0, 0,
    pd.PrintableAreaWidth, pd.PrintableAreaHeight);
    drawing_area.Arrange(rect);

    // 打印它。
    pd.PrintVisual(drawing_area, title);
}
```

接下来，代码将一个 Viewbox 居中放在 Grid 内部。记住，Viewbox 的作用是以各种方式拉伸其单个子元素。

如果例的 `margin` 参数为 `null`，代码应以正常比例显示窗口；它会将 Viewbox 的 `Stretch` 属性设置为 `None`。

如果例的 `margin` 参数不为 `null`，代码应该放大窗口。它将 Viewbox 的 `Margin` 属性设置为 `margin` 参数，使 Viewbox 扩展以填充 Grid（除边距以外的部分）。它还将 Viewbox 的 `Stretch` 属性设置为 `Uniform`，以便其在不改变纵横比（宽高比）的情况下尽可能地放大其子控件。

接下来，代码创建一个 `VisualBrush`，其中包含要打印的窗口图像。

它创建一个与窗口大小相同的 `Rectangle`，用 `VisualBrush` 填充该矩形，并将 `Rectangle` 放置在 Viewbox 中。Viewbox 会在合适拉伸 `Rectangle`。

接下来，代码调用 Grid 的 `Arrange` 方法。Grid 会递归地排列子元素并渲染它们。如果你省略了此调用，代码会运行，但打印结果将是空白。

最后，代码调用 `PrintDialog` 的 `PrintVisual` 方法来打印 Grid 及其内容。

如果用户点击对话框的“首选项”按钮并将打印机方向改为横向，`PrintDialog` 的 `PrintableAreaWidth` 和 `PrintableAreaHeight` 会自动切换，以便控件能够正确排列。

图 17-4 显示了当程序窗口被拉伸并使用 Microsoft XPS Document Writer 打印，且首选项设置为横向并在 XPS Viewer 中显示时的结果。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_346_0.png)

# 打印生成的输出

`PrintDialog` 对象的 `PrintVisual` 方法易于使用，可以产生缩放良好且居中的结果。然而，它假设你一次只打印页。如果你想打印更长的文档，你需要为每一页调用一次 `PrintVisual`，它会为每一页生成一个打印作业。这不是一个理想的解决方案。通常有更好的方法产生多页打印输出。

`PrintDialog` 对象的 `PrintDocument` 方法接收一个 `DocumentPaginator` 对象作为参数。

该对象生成打印输出的页面，而 `PrintDocument` 将它们放在单个打印作业中。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_347_0.png)

图 17-5

`DocumentPaginator` 是一个抽象类，定义了供你在子类中实现的方法。这些方法为 `PrintDocument` 方法提供信息，例如打印输出的总页数和打印的对象。

`PrintShapes` 示例程序使用继承自 `DocumentPaginator` 的 `ShapesPaginator` 类来打印四页形状。图 17-5 显示了由 Microsoft XPS Writer 打印机保存并在 XPS Viewer 中显示的输出。

以下代码显示了程序在你点击“打印形状”按钮时是如何响应的。与之前使用 `PrintVisual` 的代码一样，它显示一个 `PrintDialog` 并查看用户是否选择了打印机并点击确定。然后它调用 `PrintDocument` 方法，传递一个分页器对象和一个作业标题。

```csharp
// 打印形状。
private void btnPrintShapes_Click(object sender, RoutedEventArgs args) {
    PrintDialog pd = new PrintDialog();
    if (pd.ShowDialog() == true) {
        pd.PrintDocument(
            new ShapesPaginator(
                new Size(pd.PrintableAreaWidth, pd.PrintableAreaHeight),
                "Shapes")
            ));
    }
}
```

PrintShapes

## 快速打印，第二部分

如果你在不显示对话框的情况下调用 `PrintDocument`，则打印输出将立即发送到默认打印机。

以下代码片段显示了 `ShapesPaginator` 类的关键部分：
