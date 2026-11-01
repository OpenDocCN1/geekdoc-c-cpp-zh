

![](img/d7d2ffa0a76feaab821930e95daace93_1145_0.png)

图 37-9

一个图形可以在水平和垂直方向上对齐，并可以锚定到页面、内容、列或段落。以下代码中的 Figure 锚定在页面中心，但带有水平和垂直偏移。WrapDirection 被设置为使左右两列都环绕图形。图 37-10 显示了环绕的结果：

```xml
<Paragraph>
    <Figure HorizontalAnchor="PageCenter" HorizontalOffset="20"
        VerticalAnchor="PageCenter" VerticalOffset="20" WrapDirection="Both">
        <Paragraph Background="LightGray" FontSize="24">
            <Run>Lyrics Samples</Run>
        </Paragraph>
    </Figure>
</Paragraph>
```

![](img/d7d2ffa0a76feaab821930e95daace93_1145_1.png)

图 37-10

Floater 和 Figure 都用于添加不在主流程中的内容。虽然这两个功能看起来相似，但这些元素的特征却大不相同。下表解释了 Floater 和 Figure 之间的差异。

| 特征 | FLOATER | FIGURE |
|---|---|---|
| 位置 | 一个浮动器无法定位。它在有空间的地方渲染。 | 一个图形可以通过水平和垂直锚点进行定位。它可以相对于页面、内容、列或段落进行停靠。 |
| 宽度 | 一个浮动器只能放置在一列内。如果设置的宽度大于列大小，则会被忽略。 | 一个图形可以跨多列调整大小。图形的宽度可以设置为 0.5 页或 2 列。 |
| 分页 | 如果浮动器的大小超过列高，浮动器会断开并分页到下一列或页面。 | 如果图形的大小超过列高，只有适合列中的部分会被渲染；其他内容会丢失。 |

## 流文档

拥有所有 Inline 和 Block 元素后，现在你知道应该将什么放入流文档中。FlowDocument 类可以包含 Block 元素，而 Block 元素可以根据 Block 的类型包含 Block 或 Inline 元素。

FlowDocument 类的一个主要功能是用于将流程拆分为多个页面。这是通过 FlowDocument 实现的 IDocumentPaginatorSource 接口完成的。

FlowDocument 的其他选项包括设置默认字体和前景及背景画刷，以及配置页面和列大小。

以下 FlowDocument 的 XAML 代码定义了默认字体和字体大小、列宽，以及列之间的分隔线：

```
<FlowDocument xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
ColumnWidth="300" FontSize="16" FontFamily="Georgia"
ColumnRuleWidth="1" ColumnRuleBrush="Violet">
```

现在你只需要一种查看文档的方式。以下列表描述了几种查看器：

- **RichTextBox** — 一个简单的查看器，同时也允许编辑（只要 IsReadOnly 属性未设置为 true）。RichTextBox 不以多列显示文档，而是以滚动模式显示。这类似于 Microsoft Word 中的 Web 布局。可以通过将 HorizontalScrollbarVisibility 设置为 ScrollbarVisibility.Auto 来启用滚动条。
- **FlowDocumentScrollViewer** — 一个仅用于阅读而非编辑文档的阅读器。该阅读器允许缩放文档。还有一个带有缩放滑块的工具栏，可以通过 IsToolbarEnabled 属性启用。诸如 CanIncreaseZoom、CanDecreaseZoom、MinZoom 和 MaxZoom 之类的设置允许设置缩放功能。
- **FlowDocumentPageViewer** — 一个分页文档的查看器。使用此查看器，你不仅拥有缩放文档的工具栏，还可以从一页切换到另一页。
- **FlowDocumentReader** — 一个结合了 FlowDocumentScrollViewer 和 FlowDocumentPageViewer 功能的查看器。该查看器支持不同的查看模式，可以从工具栏设置或通过类型为 FlowDocumentReaderViewingMode 的 ViewingMode 属性设置。该枚举具有 Page、TwoPage 和 Scroll 的可能值。查看模式也可以根据需要禁用。

图 37-11 显示了之前创建的流文档，其中 FlowDocumentReader 处于 TwoPage 模式。

![](img/d7d2ffa0a76feaab821930e95daace93_1146_0.png)

图 37-11

## 固定文档

固定文档始终定义相同的外观、相同的分页，并使用相同的字体——无论文档被复制或使用在何处。WPF 定义了 FixedDocument 类，可用于创建固定文档，以及 DocumentViewer 类用于查看固定文档。

本章使用一个示例应用程序通过请求用户输入菜单计划来以编程方式创建固定文档，该计划用于创建固定文档。图 37-12 显示了该应用程序的主用户界面，用户可以在其中使用 DatePicker 类选择一天，在 DataGrid 中输入一周的菜单，并单击 Create Doc 按钮创建新的 FixedDocument。该应用程序使用在 NavigationWindow 内导航的 Page 对象。单击 Create Doc 按钮会导航到包含固定文档的新页面。

![](img/d7d2ffa0a76feaab821930e95daace93_1147_0.png)

图 37-12

Create Doc 按钮的事件处理程序 OnCreateDoc() 会导航到新页面。为此，处理程序实例化新页面 DocumentPage。该页面包含一个处理程序 NavigationService_LoadCompleted()，它被分配给 NavigationService 的 LoadCompleted 事件。在此处理程序内，新页面可以访问传递给页面的内容。然后通过调用 Navigate() 方法进行到 page2 的导航。新页面接收对象 menus，其中包含构建固定页面所需的所有菜单信息。menus 变量的类型为 ObservableCollection<MenuEntry>：

```
private void OnCreateDoc(object sender, RoutedEventArgs e)
{
    if (menus.Count == 0)
    {
        MessageBox.Show("Select a date first", "Menu Planner",
            MessageBoxButton.OK);
        return;
    }
    var page2 = new DocumentPage();
    NavigationService.LoadCompleted +=
        page2.NavigationService_LoadCompleted;
    NavigationService.Navigate(page2, menus);
}
```

代码片段 CreateXps/MenuPlannerPage.xaml.cs

在 DocumentPage 中，使用 DocumentViewer 来提供对固定文档的只读访问。固定文档在 NavigationService_LoadCompleted 方法中创建。通过事件处理程序，从第一页传递的数据会通过 NavigationEventArgs 的 ExtraData 属性接收。

```
Height = 40,
Fill = new RadialGradientBrush(Colors.Yellow, Colors.DarkRed)
};
FixedPage.SetLeft(ellipse, 500);
FixedPage.SetTop(ellipse, 50);
return ellipse;
}
```

GetDateContent() 方法访问 menus 集合以向文档添加日期范围：

```
private UIElement GetDateContent()
{
    string dateString = String.Format("{0:d} to {1:d}", menus[0].Day, menus[menus.Count - 1].Day);
    var text1 = new TextBlock
    {
        FontSize = 24,
        HorizontalAlignment = HorizontalAlignment.Center
    };
    text1.Inlines.Add(new Bold(new Run(dateString)));
    FixedPage.SetLeft(text1, 130);
    FixedPage.SetTop(text1, 90);
    return text1;
}
```

最后，GetMenuContent() 方法创建并返回一个 Grid 控件。该网格包含列和行，其中包含日期、菜单和价格信息：

```
private UIElement GetMenuContent()
{
    var grid1 = new Grid { ShowGridLines = true };

    grid1.ColumnDefinitions.Add(new ColumnDefinition
        { Width= new GridLength(50)});
    grid1.ColumnDefinitions.Add(new ColumnDefinition
        { Width = new GridLength(300)});
    grid1.ColumnDefinitions.Add(new ColumnDefinition
        { Width = new GridLength(70) });

    for (int i = 0; i < menus.Count; i++)
    {
        grid1.RowDefinitions.Add(new RowDefinition
            { Height = new GridLength(40) });

        var t1 = new TextBlock(
            new Run(String.Format("{0:ddd}", menus[i].Day)));
        t1.VerticalAlignment = VerticalAlignment.Center;
        t1.Margin = new Thickness(5, 2, 5, 2);
        Grid.SetColumn(t1, 0);
        Grid.SetRow(t1, i);
        grid1.Children.Add(t1);

        var t2 = new TextBlock(new Run(menus[i].Menu));
        t2.VerticalAlignment = VerticalAlignment.Center;
        t2.Margin = new Thickness(5, 2, 5, 2);
        Grid.SetColumn(t2, 1);
        Grid.SetRow(t2, i);
        grid1.Children.Add(t2);

        var t3 = new TextBlock(new Run(menus[i].Price.ToString()));
        t3.VerticalAlignment = VerticalAlignment.Center;
        t3.Margin = new Thickness(5, 2, 5, 2);
        Grid.SetColumn(t3, 2);
```

