
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

# 快速打印，第二部分

如果你在不显示对话框的情况下调用 `PrintDocument`，则打印输出将立即发送到默认打印机。

以下代码片段显示了 `ShapesPaginator` 类的关键部分：

```csharp
class ShapesPaginator : DocumentPaginator {
    private Size m_PageSize;
    // 保存页大小。
    public ShapesPaginator(Size page_size) {
        m_PageSize = page_size;
    }
    // 返回需要的页面。
    public override DocumentPage GetPage(int pageNumber) {
        const double WIDTH = 600;
        const double HGT = 800;
        Grid drawing_grid = new Grid();
        drawing_grid.Width = m_PageSize.Width;
        drawing_grid.Height = m_PageSize.Height;
        switch (pageNumber) {
            case 0 : 
                Ellipse ell = new Ellipse();
                ell.Fill = Brushes.Orange;
                ell.Stroke = Brushes.Blue;
                ell.StrokeThickness = 1;
                ell.HorizontalAlignment = HorizontalAlignment.Center;
                ell.VerticalAlignment = VerticalAlignment.Center;
                ell.Width = WIDTH;
                ell.Height = HGT;
                drawing_grid.Children.Add(ell);
                break;
        }
        // 其他页的代码省略 ...
        // 排列以使控件绘制自己。
        Rect rect = new Rect(0, 0, m_PageSize);
        drawing_grid.Arrange(rect);
        // 返回一个封装 grid 的 DocumentPage。
        return new DocumentPage(drawing_grid);
    }
    // 如果分页正在进行且 PageCount 不是最终的，返回 False；
    // 如果分页完成且 PageCount 是最终的，返回 True；
    // 在此示例中，没有需要进行的分页。
    public override bool IsCountValid {
        return true;
    }
    // 目前已分页的页数。
```

```csharp
// 此示例恰好有 4 页。
public override int PageCount
{
    get { return 4; }
}

// 建议的页大小。
public override Size PageSize
{
    get { return m_PageSize; }
    set { m_PageSize = value; }
}

// 当前正在分页的元素。
public override IDocumentaginatorSource Source
{
    get { return null; }
}
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_349_0.png)

类构造函数接收一个在其上绘图的页面大小的参数，并保存该大小以供以后使用。

该类最感兴趣的部分是 `GetPage` 方法，它返回要打印的对象。它首先创建一个填充打印页的 `Grid`。

接下来，根据页码，代码将一个形状放置于 `Grid`。`GetPage` 方法随后管理 `Grid` 以产生输出。它通过返回一个初始化的 `DocumentPage` 来完成。

# 打印文档

通过使用 `PrintDialog` 方法，你可以像 `PrintShapes` 程序那样打印一系列图像。

然而，要产生相对复杂的输出，你需要编写一个复杂的 `DocumentPaginator` 类。例如，假设你想打印包含嵌入图像和表格的多页简报。构建处理这些布局的分页器将是一项苦差。

然而，使用 `FlowDocument` 和 `FixedDocument` 显示这种复杂输出要简单得多。`FixedDocument` 在特定位置显示项目。

以下章节将解释如何打印 `FlowDocuments` 和 `FixedDocuments`。

# 打印 FlowDocuments

与其构建复杂的分页器来产生输出，你可以构建一个 `FlowDocument` 并将段落、表格和其他元素放入其中。`FlowDocument` 会自动排列内容以利用可用空间。

遗憾的是 `FlowDocument` 类没有继承 `Visual` 类，因此你不能简单将其传递给 `PrintDialog` 的 `PrintVisual` 方法。你可以将包含 `FlowDocument` 的 `Window` 传递给 `PrintVisual`，但这样打印输出将仅包含当时可见的内容。

正确打印 `FlowDocument` 简单但令人困惑。基本思想是为打印队列创建一个 `XpsDocumentWriter`。该对象的 `Write` 方法可以在打印作业中创建一个分页器。为了让一切运行，你只需要弄清楚如何为 `FlowDocument` 构建分页器。

幸运的是，`FlowDocument` 类实现了 `IDocumentaginatorSource` 接口，并定义了一个返回文档分页器的 `DocumentPaginator` 属性。

以下代码显示了 `PrintDocument` 示例程序打开菜单并选择打印时如何打印其 `FlowDocument`：

```csharp
// 打印 FlowDocument。
private void mnFilePrint_Click(object sender, RoutedEventArgs e) {
    PrintDialog pd = new PrintDialog();
    if (pd.ShowDialog() == true) {
        // 为打印队列创建一个 Xps document writer。
        XpsDocumentWriter xps_writer = 
            PrintQueue.CreateXpsDocumentWriter(pd.PrintQueue);

        // 将 FlowDocument 转换为 IDocumentaginatorSource。
        IDocumentaginatorSource paginator_source = 
            (IDocumentaginatorSource)fdContents;

        // 使用 IDocumentaginatorSource 的
        // 属性获取分页器。
        xps_writer.Write(paginator_source.DocumentPaginator);
    }
}
```

