

![](img/b5597c749e848b27b0d305153ae16106_355_0.png)

图 8-6：带有 HelloWorld 程序的 Visual Studio

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

Silverlight 有两种容器。ContentControls 只能有一个。你可以通过 Content 属性访问 ContentControl 的子元素。Button、Checkbox 和 ScrollViewer 是 ContentControl 的示例。之前在 HelloWorld 示例中使用了 Button 的 Content 属性。但如果你想在 Button 中放置多个一个元素怎么办？

技巧在于，你可以将一个 Panel 作为 ContentControl 的 Content。Panels 可以拥有多个子元素（Children 属性）。Grid（当你在 Visual Studio 中创建 UserControl 时它是默认的 Panel）就是此类 Panel 的示例。那么，如何在 HelloWorld 程序中在视频旁边放置文本呢？

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

现在 Button 的 Content 是 StackPanel。StackPanel 排它的子元素——居中的 TextBlock 和播放视频的 MediaElement。默认情况下，StackPanel 将子元素垂直排列。因此，用之前的 XAML 描述的 Button 看起来如图 8-9。

![](img/b5597c749e848b27b0d305153ae16106_357_0.png)

**图 8-9：带有文本和视频的按钮

如果你想更改布局使文本位于视频左侧，必须更改 StackPanel 本身并添加 Orientation 属性，如下：

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

在此段代码中，TextBlock 还接收了 VerticalAlignment 属性。如果省略，TextBlock 的高度将与相邻的 MediaElement 相同，因此文本将在顶部而不是底部显示。这展示了 Silverlight 的工作原理。决定显示方式的不是控件，而是它们的容器。StackPanel 将子元素垂直排列（如果 Orientation 属性设置为 Vertical），或将子元素水平排列（如果 Orientation 属性设置为 Horizontal）。

实际布局要复杂一点。子元素对于它们倾向的尺寸有发言权。作为布局的第一步，从视觉树的顶部开始，Silverlight 通过调用 MeasureOverride 询问每个元素它希望变成什么样。复合控件（如 Panel）通过调用子元素的 MeasureOverride 来计算答案。

在第二步中，ArrangeOverride 在整个树中被调用。在这种情况下，父元素告诉子元素实际的可用空间——适应空间是子元素的责任。如果可用空间小于控件需要的，可以添加滚动条、将内容缩放到某个大小（如图像或视频），或简单地裁剪。根元素可以多大的最终限制是给定 <object> 标签的大小——或者在浏览器外（OOB）应用程序的情况下，宿主窗口的大小。

# Silverlight 中的布局容器

Silverlight 中的布局容器包括：

- Border
- Canvas
- StackPanel
- Grid
- Viewbox

# Border

Border 只能有一个子元素（但像之前的 Button 一样，这可以是另一个容器）。正如名称所示，Border 在其内容周围画一个边框。

```xml
<Border HorizontalAlignment="Center" VerticalAlignment="Center" BorderBrush="Black" BorderThickness="3" CornerRadius="5">
<TextBox Text="TextBox with a lot of" />
</Border>
```

这创建了包裹 TextBox 的边框。正如你在图 8-10 中看到的，边框的厚度为 3 像素，圆角半径为 5 像素。在布局阶段，Border 询问 TextBox 测量自身，TextBox 也是通过测量自身来确定尺寸。由于 Border 没有特定的尺寸（这就是为什么使用了 HorizontalAlignment 和 VerticalAlignment），你可以通过修改 Border 的填充（Padding）属性来控制边框与 TextBox 之间的间距。Padding 属性在 Silverlight 中定义为像素。

# Canvas

Canvas 是最简单的 Panel，它可以拥有多个子元素。在 Canvas 中，你可以根据绝对坐标放置元素。Canvas 允许子元素具有任何大小。如果子元素不符合 Canvas ，它们仍然会在 Canvas 之外（在 WPF 中，你可以使用 ClipToBounds 属性将内容裁剪到边界）。Canvas 的大小不取决于它的子元素。这种简单性使其成为最快的布局控件，也是不需要自适应布局时的选择。

以下代码在 Canvas 中放置了一个矩形和一个圆形。圆形超出了 Canvas 的边界。

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

早些时候你了解到控件不负责自己的放置。那么，为什么可以在圆形和矩形上看到左和顶部的坐标呢？技巧在于这些坐标（Canvas.Left 和 Canvas.Top）是通过一种被称为附加属性（attached properties）的构造提供的。