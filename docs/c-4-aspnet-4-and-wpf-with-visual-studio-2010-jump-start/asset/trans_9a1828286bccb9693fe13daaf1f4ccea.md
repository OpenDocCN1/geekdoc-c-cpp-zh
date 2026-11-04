
```csharp
Button btn;
Polygon pgn;
Rectangle rect;
Grid grd;
Ellipse ell;

switch (element.Tag.ToString())
{
    case "Red":
        btn = (Button)element.FindName("btnRepairDisk");
        btn.Click += new RoutedEventHandler(btnRepairDisk_Click);
        Code for other controls omitted
        break;

    case "Blue":
        Lots of code omitted

        // Uses the same event handler as rectMove.
        ell = (Ellipse)element.FindName("ellMove");
        ell.MouseDown += new System.Windows.Input.MouseButtonEventHandler(
            rectMove_MouseDown);

        grd = (Grid)element.FindName("grdExit");
        grd.MouseDown += new System.Windows.Input.MouseButtonEventHandler(
            grdExit_MouseDown);
        break;
}
```

代码首先使用 WPF 的 LoadComponent 方法加载所需 XAML 皮肤文件。它将窗口的主内容元素设置为从文件中加载的根元素，以便显示新的控件。

接下来，代码检查新加载的根元素的 Tag 属性，以查看它现在是否显示红色或蓝色皮肤。根据加载的皮肤，代码会在皮肤中查找特定控件并连接其事件处理程序。

## 打印视觉对象

WPF 中用于打印的核心类之一是 PrintDialog。该类提供方法让用户选择打印机、与打印队列交互以及将输出发送到打印机。

通常打印有三个步骤：

1. 创建一个新的 PrintDialog 对象并使用其 ShowDialog 方法向用户显示它。
2. 检查 ShowDialog 的返回结果以查看用户是否单击了 OK。
3. 使用 PrintDialog 的方法生成打印输出。

![](img/7954dcc7dd1d929d072aec8e9531b6cc_102_0.png)

SimplePrintWindow 示例程序使用以下代码执行这三个步骤：

```csharp
// Display the print dialog.
PrintDialog pd = new PrintDialog();

// See if the user clicked OK.
if (pd.ShowDialog() == true)
{
    // Print.
    pd.PrintVisual(this, "New Customer");
}
```

WPF 程序员参考 9780470477229 SimplePrintWindow

这非常简单，但有一个不幸的缺点：WPF 尝试在纸张的左上角绘制视觉对象。由于打印机通常无法打印到纸张边缘，结果会被截断。

与其将程序的窗口传递给 PrintVisual 方法，你可以创建一个包含窗口图像的控件层次结构。该层次结构可以使用 Grids、Viewboxes、Images、Rectangles 以及任何你想要生成结果的其他控件。它甚至可以包含额外的控件来生成页面页眉和页脚等项目。

下一幅图示中显示的 PrintWindow 示例程序使用这种方法以正常或放大比例居中打印其窗口。单击“Print Centered”按钮以正常比例打印窗口。单击“Print Stretched”按钮以尽可能大的尺寸在页面上打印窗口。

![](img/7954dcc7dd1d929d072aec8e9531b6cc_102_1.png)

PrintWindow 程序需要引用 ReachFramework 和 System.Printing 库。在 Visual Studio 中，打开 Project 菜单并选择“添加引用”。选择这两个库并单击 OK。

为了更轻松地使用这些库，程序包含以下 using 语句：

```csharp
using System.Printing;
using System.Windows.Media.Effects;
```

```csharp
    )

    // Make a VisualBrush holding an image of the Window's contents.
    VisualBrush vis_br = new VisualBrush(win);

    // Make a rectangle the size of the Window.
    Rectangle win_rect = new Rectangle();
    view_box.Child = win_rect;
    win_rect.Width = win.Width;
    win_rect.Height = win.Height;
    win_rect.Fill = vis_br;
    win_rect.Stroke = Brushes.Black;
    win_rect.BitmapEffect = new DropShadowBitmapEffect();

    // Arrange to produce output.
    Rect rect = new Rect(0, 0,
        pd.PrintableAreaWidth, pd.PrintableAreaHeight);
    drawing_area.Arrange(rect);

    // Print it.
    pd.PrintVisual(drawing_area, title);
}
```

WPF 程序员参考 9780470477229 PrintWindow

下一幅图显示了当程序窗口被拉伸并使用 Microsoft XPS Document Writer 打印时，首选项设置为横向方向并在 XPS Viewer 中显示的结果。

![](img/7954dcc7dd1d929d072aec8e9531b6cc_104_0.png)

以下代码片段显示了 ShapesPaginator 类的关键部分：

![](img/7954dcc7dd1d929d072aec8e9531b6cc_106_0.png)

```csharp
class ShapesPaginator : DocumentPaginator
{
    private Size m_PageSize;

    // Save the page size.
    public ShapesPaginator(Size page_size)
    {
        m_PageSize = page_size;
    }

    // Return the needed page.
    public override DocumentPage GetPage(int pageNumber)
    {
        const double WID = 600;
        const double HGT = 800;

        Grid drawing_grid = new Grid();
        drawing_grid.Width = m_PageSize.Width;
        drawing_grid.Height = m_PageSize.Height;

        switch (pageNumber)
        {
            case 0: // Ellipse
                Ellipse ell = new Ellipse();
                ell.Fill = Brushes.Orange;
                ell.Stroke = Brushes.Blue;
                ell.StrokeThickness = 1;
                ell.HorizontalAlignment = HorizontalAlignment.Center;
                ell.VerticalAlignment = VerticalAlignment.Center;
                ell.Width = WID;
                ell.Height = HGT;
                drawing_grid.Children.Add(ell);
                break;

            ... Code for other pages omitted ...

        }

        // Arrange to make the controls draw themselves.
        Rect rect = new Rect(new Point(0, 0), m_PageSize);
        drawing_grid.Arrange(rect);

        // Return a DocumentPage wrapping the grid.
        return new DocumentPage(drawing_grid);
    }

    // If pagination is in progress and PageCount is not final, return False.
    // If pagination is complete and PageCount is final, return True.
    // In this example, there is no pagination to do.
    public override bool IsPageCountValid
    {
        get { return true; }
    }

    // The number of pages paginated so far.
    // This example has exactly 4 pages.
    public override int PageCount
    {
        get { return 4; }
    }

    // The suggested page size.
    public override Size PageSize
    {
        get { return m_PageSize; }
        set { m_PageSize = value; }
    }

    // The element currently being paginated.
    public override IDocumentPaginatorSource Source
    {
        get { return null; }
    }
}
```

## 数据绑定

WPF 数据绑定让你将目标绑定到数据源，以便目标自动显示数据源中的值。例如，这让你可以：

- 让 `ListBox` 显示在 XAML 代码中定义的值数组。
- 让 `ListBox` 显示在代码后置中创建的对象列表。
- 让 `TreeView` 构建代码后置中创建的对象的分层显示。
- 让 `TextBoxes`、`Labels` 和其他控件显示 `ListBox`、`ComboBox` 或 `TreeView` 中当前选中项的额外详细信息。

额外的 WPF 数据绑定功能让你可以排序、过滤和分组数据；让用户修改控件以更新数据源；并验证对数据的更改。

### 绑定基础

数据绑定有以下四个基本部分：

- **目标** — 将使用绑定结果的对象
- **目标属性** — 将使用结果的目标对象的属性
- **源** — 为目标对象提供值的对象
- **路径** — 在源对象内定位值的路径

作为一个简单的例子，假设你想绑定 Label 控件的 Content 属性，以便 Label 显示你在 TextBox 中输入的任何内容。如果 Label 控件命名为 lblResult 且 TextBox 命名为 txtTypeHere，那么你需要创建一个绑定，其中：

- 目标是 lblResult（你希望绑定结果去到的控件）。
- 目标属性是 Content（你希望 Label 在其 Content 属性中显示结果）。
- 源是 txtTypeHere（提供值的对象）。
- 路径是 Text（源对象中数据的路径，在本例中为 TextBox 的 Text 属性）。

此处显示的 TextBoxToLabel 示例程序演示了这种简单绑定。当你在文本框中输入时，下面的两个标签会回显你输入的内容。

以下 XAML 代码显示了程序的工作原理：

![](img/7954dcc7dd1d929d072aec8e9531b6cc_108_0.png)

![](img/7954dcc7dd1d929d072aec8e9531b6cc_108_1.png)

```xml
<StackPanel Margin="5">
    <TextBox Name="txtTypeHere" Margin="5" Height="30" VerticalAlignment="Top" Text="Type here!"/>
    <Label Margin="5" BorderBrush="Yellow" BorderThickness="1">
        <Binding ElementName="txtTypeHere" Path="Text"/>
    </Label>
    <Label Margin="5" BorderBrush="Yellow" BorderThickness="1" Content="{Binding ElementName=txtTypeHere, Path=Text}"/>
</StackPanel>
```

下一幅图示中显示的 PersonSource 示例程序使用绑定，其 Source 属性设置为显示 Person 对象的信息。

![](img/7954dcc7dd1d929d072aec8e9531b6cc_108_2.png)

PersonSource 示例程序定义了一个 Person 类，其属性为 FirstName、LastName 和 NetWorth。程序的 XAML 代码包含以下命名空间定义，以便它可以使用该类：

```xml
xmlns:local="clr-namespace:PersonSource"
```
