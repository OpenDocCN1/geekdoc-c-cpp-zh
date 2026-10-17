
中间区域上方显示设计板，下方显示 XAML。这种分视图是一个极佳的学习工具。该区域的任何更改（如移动按钮、更改颜色、添加新控件等）都会立即反映在下方，反之亦然。当 XAML 发生变化时，几秒钟即可在上方看到结果。在右下角，属性浏览器（Property Browser）是一个非常实用的功能——可以对属性进行搜索，如图 8-7 所示。

还有一个实用的开发者大纲窗口（Developer Outline）。由于 XAML 树可能会变得非常巨大，这有助于在文档中找到正确的元素。

![](img/b5597c749e848b27b0d305153ae16106_355_1.png)

对于某些开发者来说，Blend 那种“类设计”的外观有点吓人。他们可能不适应它。然而，对于处理 XAML 的开发者来说，Blend 是不可或缺的工具——遗憾的是，即使是灰色 LOB（线性业务）应用需要的某些功能也没有进入 Visual Studio（例如本章稍后讨论的 ItemTemplate 编辑）。在 Blend 中打开的相同 HelloWorld 程序（.NET 4 预览版）如图 8-8 所示。

图 8-7：VS2010 属性浏览器

![](img/b5597c749e848b27b0d305153ae16106_356_0.png)

**图 8-8：Blend 中的 HelloWorld 程序

再次，设计板和 XAML 视图占据了大部分屏幕。属性编辑器面板看起来更高级（由于不同的属性值更容易导航），可以通过拖动属性值来更改数值。属性在 Blend 中可以过滤，就像在 Visual Studio 中一样。工具箱用于缩放、平移工具和基本控件——其余控件可以在资源（Assets）面板中找到（并搜索）。对象（Objects）和时间轴（Timeline）面板是 Blend 操作的核心。与 Cider 的文档大纲不同，它是交互式的，支持拖放重新排列控件，右键点击提供选项，并可以使用时间轴展开以创建和编辑动画。

# 布局

布局意味着控件的大小以及在屏幕上的放置。Silverlight 的布局非常灵活。很容易创建自动适应以下内容的布局：

- 可用屏幕大小
- 显示的项目数量
- 显示元素的大小
- 放大倍数

Silverlight 的布局策略与 Forms 或 ASP.NET 不同。理解 Silverlight 布局的关键在于理解容器（Containers）。

Silverlight 有两种容器。`ContentControls` 只能有一个。你可以通过 `Content` 属性访问 `ContentControl` 的子元素。`Button`、`Checkbox` 和 `ScrollViewer` 是 `ContentControl` 的示例。之前在 HelloWorld 示例中使用了 `Button` 的 `Content` 属性。但如果你想在 `Button` 中放置多个一个元素怎么办？

技巧在于，你可以将一个 `Panel` 作为 `ContentControl` 的 `Content`。`Panels` 可以拥有多个子元素（`Children` 属性）。`Grid`（当你在 Visual Studio 中创建 `UserControl` 时它是默认的 `Panel`）就是此类 `Panel` 的示例。那么，如何在 HelloWorld 程序中在视频旁边放置文本呢？

```xml
<Button HorizontalAlignment="Center" VerticalAlignment="Center">
<Button.Content>
<StackPanel>
<TextBlock Text="I am a button!" HorizontalAlignment="Center" Margin="5" />
<MediaElement Width="100" Height="75" Source="http://msdnchnline.llnw.net/d1/ch9/0/8/7/7/4/SL3Expressionlaunch_ch9.vm" />
</StackPanel>
</Button.Content>
</Button>
```

现在 `Button` 的 `Content` 是 `StackPanel`。`StackPanel` 排它的子元素——居中的 `TextBlock` 和播放视频的 `MediaElement`。默认情况下，`StackPanel` 将子元素垂直排列。因此，用之前的 XAML 描述的 `Button` 看起来如图 8-9。

![](img/b5597c749e848b27b0d305153ae16106_357_0.png)

**图 8-9：带有文本和视频的按钮

如果你想更改布局使文本位于视频左侧，必须更改 `StackPanel` 本身并添加 `Orientation` 属性，如下：

```xml
<Button HorizontalAlignment="Center" VerticalAlignment="Center">
<Button.Content>
<StackPanel Orientation="Horizontal">
<TextBlock Text="I am a button!" HorizontalAlignment="Center" VerticalAlignment="Center" Margin="5" />
<MediaElement Width="100" Height="75" Source="http://msdnchnline.llnw.net/d1/ch9/0/8/7/7/4/SL3Expressionlaunch_ch9.vm" />
</StackPanel>
</Button.Content>
</Button>
```

在此段代码中，`TextBlock` 还接收了 `VerticalAlignment` 属性。如果省略，`TextBlock` 的高度将与相邻的 `MediaElement` 相同，因此文本将在顶部而不是底部显示。这展示了 Silverlight 的工作原理。决定显示方式的不是控件，而是它们的容器。`StackPanel` 将子元素垂直排列（如果 `Orientation` 属性设置为 `Vertical`），或将子元素水平排列（如果 `Orientation` 属性设置为 `Horizontal`）。

实际布局要复杂一点。子元素对于它们倾向的尺寸有发言权。作为布局的第一步，从视觉树的顶部开始，Silverlight 通过调用 `MeasureOverride` 询问每个元素它希望变成什么样。复合控件（如 `Panel`）通过调用子元素的 `MeasureOverride` 来计算答案。

在第二步中，`ArrangeOverride` 在整个树中被调用。在这种情况下，父元素告诉子元素实际的可用空间——适应空间是子元素的责任。如果可用空间小于控件需要的，可以添加滚动条、将内容缩放到某个大小（如图像或视频），或简单地裁剪。根元素可以多大的最终限制是给定 `<object>` 标签的大小——或者在浏览器外（OOB）应用程序的情况下，宿主窗口的大小。

# Silverlight 中的布局容器

Silverlight 中的布局容器包括：

- `Border`
- `Canvas`
- `StackPanel`
- `Grid`
- `Viewbox`

## Border

`Border` 只能有一个子元素（但像之前的 `Button` 一样，这可以是另一个容器）。正如名称所示，`Border` 在其内容周围画一个边框。

```xml
<Border HorizontalAlignment="Center" VerticalAlignment="Center" BorderBrush="Black" BorderThickness="3" CornerRadius="5">
<TextBox Text="TextBox with a lot of" />
</Border>
```

这创建了包裹 `TextBox` 的边框。正如你在图 8-10 中看到的，边框的厚度为 3 像素，圆角半径为 5 像素。在布局阶段，`Border` 询问 `TextBox` 测量自身，`TextBox` 也是通过测量自身来确定尺寸。由于 `Border` 没有特定的尺寸（这就是为什么使用了 `HorizontalAlignment` 和 `VerticalAlignment`），你可以通过修改 `Border` 的填充（`Padding`）属性来控制边框与 `TextBox` 之间的间距。`Padding` 属性在 Silverlight 中定义为像素。

## Canvas

`Canvas` 是最简单的 `Panel`，它可以拥有多个子元素。在 `Canvas` 中，你可以根据绝对坐标放置元素。`Canvas` 允许子元素具有任何大小。如果子元素不符合 `Canvas` ，它们仍然会在 `Canvas` 之外（在 WPF 中，你可以使用 `ClipToBounds` 属性将内容裁剪到边界）。`Canvas` 的大小不取决于它的子元素。这种简单性使其成为最快的布局控件，也是不需要自适应布局时的选择。

以下代码在 `Canvas` 中放置了一个矩形和一个圆形。圆形超出了 `Canvas` 的边界。

```xml
<Grid x:Name="LayoutRoot" Background="White">
<Canvas Width="200" Height="300" Background="Gray">
<Ellipse Width="150" Height="100" />
<Canvas Left="100" Top="100" Fill="Black" />
<Rectangle Width="150" Height="100" />
<Canvas Left="20" Canvas.Top="33" Fill="White" />
</Canvas>
</Grid>
```

早些时候你了解到控件不负责自己的放置。那么，为什么可以在圆形和矩形上看到左和顶部的坐标呢？技巧在于这些坐标（`Canvas.Left` 和 `Canvas.Top`）是通过一种被称为附加属性（attached properties）的构造提供的。

依赖属性。视觉树中 `Canvas` 的任何子元素都可以设置这些属性。尽管这些属性是在子元素内部设置的，但处理这些属性的责任是 `Canvas`，而属性本身是在定义在 `Canvas` 中的的。

### StackPanel

正如你之前所看到的，`StackPanel` 以水平或垂直方式排列其子元素。这里有一个稍微复杂的示例：

```xml
<StackPanel Orientation="Horizontal" Background="Black">
  <StackPanel Orientation="Vertical">
    <Button Content="Button 1" />
    <Button Content="Button 2" Width="100" />
    <Button Content="Button 3 with long text" />
  </StackPanel>
  <StackPanel Orientation="Horizontal" Background="Gray">
    <Button Content="Button 4" />
    <Button Content="Button 5" Height="40" />
    <Button Content="Button 6 with long text" />
  </StackPanel>
</StackPanel>
```

渲染结果如图 8-12 所示。

第一个 `StackPanel` 设置为水平方向，并有两个 `StackPanel` 作为其子元素。它们都有三个子元素 —— `StackPanel` A 将它们垂直排列，`StackPanel` B 将它们水平排列（后者具有灰色背景）。在垂直方向 `StackPanel` 的情况下，其宽度由其最大的子元素 —— `Button 3` 决定，该按钮包含最多的文本。`StackPanel` 会重新调整 `Button 1` 的大小以填充面板的宽度。`Button 2` 有指定的宽度，因此它不会被 `StackPanel` 调整大小。

在水平方向 `StackPanel` 的情况下，面板决定了其子元素的高度。`StackPanel` 的高度是由最外黑色 `StackPanel` 的高度决定的 —— 就像 `Button 4` 和 `Button 6` 的高度一样。`Button 5` 的 `Height` 属性被设置了，因此该设置具有优先级。

### Grid

`Grid` 是最复杂但也最多功能的布局控件。它与 HTML 表格有些相似。正如其名称所示，它允许将其子元素放置在行和列中。以下是一个示例（图 8-13 显示了 Visual Studio 中的 `Grid`）。

```xml
<Grid x:Name="LayoutRoot" Background="Gray">
  <Grid.RowDefinitions>
    <RowDefinition Height="1*" />
  </Grid.RowDefinitions>
```

![](img/b5597c749e848b27b0d305153ae16106_360_0.png)

图 8-12: 三个 StackPanel

```xml
<RowDefinition Height="*" />
</Grid.RowDefinitions>
<Grid.ColumnDefinitions>
<ColumnDefinition Width="136" />
<ColumnDefinition Width="264" />
</Grid.ColumnDefinitions>
<Ellipse Stroke="Black" StrokeThickness="1" Fill="White" />
<Ellipse Stroke="Black" StrokeThickness="3" Fill="White" Grid.Column="1" 
Margin="10,10,10,0" />
<Ellipse Stroke="Black" StrokeThickness="5" Fill="White" Grid.Row="1" 
Grid.ColumnSpan="2" />
</Grid>
```

![](img/b5597c749e848b27b0d305153ae16106_361_0.png)

图 8-13: 作为布局容器的 Grid

这段 XAML 代码创建了一个灰色背景的 `Grid`。`Grid` 有两行：第二行是第一行的两倍。这意味着如果 `Grid` 高为 300 像素，那么第一行将为 100 像素，第二行将为 200 像素。`Grid` 还有两列；它们的固定大小为 136 和 264 像素。也可以让行或列自动调整大小。在这种情况下，内容的大小以及其他行或列的剩余空间决定了该行或该列的大小。

`Grid` 中有三个椭圆（`Ellipses`）。第一个位于第 0 列第 0 行（如果未指定 `Grid.Row` 或 `Grid.Column` 属性，则第一个椭圆的大小由左上单元格的大小决定）。

第二个椭圆的 `Grid.Column="1"` 属性将其置于第一行的第二列。该椭圆还有一个 `Margin="10,10,10,0"`，这意味着顶部和左侧边距为 10 像素。第二个椭圆的大小也由右上单元格的大小减去指定的 `Margin` 决定。

第三个椭圆放置在第二行。它还设置了 `ColumnSpan="2"` 属性，因此它将占据第二行的两个单元格。

如果目的是让单元格的内容不占据整个空间，你必须更改 `HorizontalAlignment` 和 `VerticalAlignment` 属性。这些属性默认为 `Stretch`，但你也可以分别取 `HorizontalAlignment.Left`、`HorizontalAlignment.Center`、`HorizontalAlignment.Right` 或 `VerticalAlignment.Top`、`VerticalAlignment.Center`、`VerticalAlignment.Bottom`。在这种情况下，你可以使用 `Margin` 属性设置离单元格边缘的距离。

### Viewbox

`Viewbox` 是 Silverlight 核心框架新增的新内容。在 Silverlight 4.0 之前，它是 Silverlight Toolkit 的（Silverlight Toolkit 是微软开发的一组开源控件，不是 Silverlight 核心平台的一部分）。与 `Border` 一样，`Viewbox` 只能有一个子元素。`Viewbox` 的目标是将其内容缩放以适应可用空间。

# 列表 8-7 (继续)

```c
{
  if (PropertyChanged != null)
    PropertyChanged(this, new PropertyChangedEventArgs(propertyName));
  }

  public DateTime CurrentTime
{
    get { return DateTime.Now; }
  }

  public event PropertyEventHandler PropertyChanged;
}
```

代码文件 `[ViewModel.cs]` 可在 Wrox 下载。

起初，Clock示例应用程序似乎有点过于复杂。毕竟，你完全简单地在后置代码中创建一个定时器，并在定时器触发时更新 `TextBlock` 的上下文。然而，在处理复杂的主从关系和多个对象时，分离数据对象和数据绑定的优势变得显而易见。

> 还有一种流行的架构模式称为模型-视图-模型（MVVM），它高度依赖于数据绑定。MVVM 允许 UI 逻辑测试以及 UI 与应用程序逻辑的完全分离。深入讨论 MVVM 超出了本书的范围。如果你计划使用 Silverlight 或 WPF 开发严肃的应用程序，绝对应该熟悉这种模式。

使用 XAML 是我们描述对象层次结构的方式；在这里，你使用 XAML 特性来创建 `ClockViewModel` 类的实例，并将其分配给 `UserControl` 的 `DataContext` 属性。XML 命名空间 `local` 指包含 `ClockViewModel` 的程序集。当 XAML 被 Silverlight 运行时执行时，会创建 `ClockViewModel` 对象，该对象反而启动它的定时器。
