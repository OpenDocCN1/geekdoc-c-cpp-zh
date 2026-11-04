
## 使用布局面板排列元素

设计窗口始于布局控件或面板。面板与内容控件不同之处在于它们可以容纳多个项目，并且根据面板的不同，会为您处理大量底层工作。

面板控制 UIElements 彼此之间以及与其包含的 UIElement 的关系，但不规定绝对定位。大多数应用程序窗口都需要某种面板组合来实现所需用户界面，因此了解它们所有都很重要。WPF 提供了六个核心面板：

- 堆栈面板
- 换行面板
- 停靠面板
- 画布
- 均匀网格
- 网格

## 堆栈面板

堆栈面板将 UIElements 放置在——等一下——堆栈中。项目以垂直堆叠（默认）的方式放置，如 DVD 堆叠，或水平排列，如书架上的书籍。重要的是要理解，项目在 XAML 中的出现顺序就是它们在面板中的出现顺序——XAML 中第一个 UIElement 出现在顶部（垂直）或最左侧（水平）。图 2-1 和 2-2 显示了同一组按钮在两种方向下的情况。清单 2-1 包含图 2-1 中所示垂直堆栈面板的 XAML。

你可以在 http://csharpfordummies.net 找到这些示例的代码。

![](img/80ff26f06fc9ab951e1cd4257b867366_604_0.png)

图 2-1：
垂直堆栈面板。

![](img/80ff26f06fc9ab951e1cd4257b867366_604_1.png)

第五册
第 2 章
理解 WPF 基础

### 清单 2-1：垂直堆栈面板 XAML

```xml
<StackPanel Name="pnlStack" Grid.Row="0" Orientation="Vertical">
  <Button Content="A Button"/>
  <Button Content="Another Button"/>
  <TextBlock Text="This is a text block"/>
  <Button Content="Short"/>
  <Button Content="Really Long Button Label"/>
</StackPanel>
```

![](img/80ff26f06fc9ab951e1cd4257b867366_605_0.png)

还记得本章开头渲染引擎与控件之间的对话吗？水平布局说明了当容器中控件的首选尺寸总和大于容器所能容纳的尺寸时可能发生的裁剪。

Orientation（以及所有其他属性）可以在运行时更改，如清单 2-2 所示。窗口底部的按钮会在单击事件中更改方向、按钮标签和窗口标题。第 4 章展示了编码按钮单击事件的更好方法。

### 清单 2-2：代码中更改堆栈面板方向

```csharp
private void cmdOrientation_Click(object sender, RoutedEventArgs e)
{
    Button button = sender as Button;
    if (button.Content.ToString() == "Set Vertical")
    {
        pnlStack.Orientation = Orientation.Vertical;
        button.Content = "Set Horizontal";
        Title = "Stack Panel - Vertical";
    }
    else
    {
        pnlStack.Orientation = Orientation.Horizontal;
        button.Content = "Set Vertical";
        Title = "Stack Panel - Horizontal";
    }
}
```

## 换行面板

换行面板会自动将溢出内容换行到下一行（或多行）。这与典型工具栏的工作方式不同，典型工具栏在没有足够空间显示时隐藏溢出项。图 2-3 和 2-4 显示了来自堆栈面板的相同内容控件（按钮和文本块的混合）在换行面板中的情况。第一个窗口有足够的空间显示所有 UIElements，第二个窗口则因空间不足而显示元素的换行。换行面板示例的 XAML 在清单 2-3 中。

图 2-3：
换行面板
（宽形式）。

![](img/80ff26f06fc9ab951e1cd4257b867366_606_0.png)

图 2-4：
换行面板
（窄形式）。

![](img/80ff26f06fc9ab951e1cd4257b867366_606_1.png)

请注意，即使使用换行面板，如果容器无法容纳最宽的项目（示例中的最后一个按钮），仍会发生一些裁剪。

### 清单 2-3：换行面板 XAML

```xml
<WrapPanel>
<Button Content="A Button"/>
<Button Content="Another Button"/>
<TextBlock Text="This is a text block"/>
<Button Content="Short"/>
<Button Content="Really Long Button Label"/>
</WrapPanel>
```

## 停靠面板

停靠面板使用附加属性（参见本迷你书第 1 章）来“停靠”子 UIElements。（参见图 2-5 和清单 2-4。）需要记住的重要一点是，子元素按 XAML 顺序停靠，这意味着如果有两个项目分配到左侧（通过 DockPanel.Dock="Left"），则 XAML 中出现的第一个 UIElement 获得面板的最左侧边墙，其后是下一个项目。

停靠面板还具有一个名为 LastChildFill 的设置。如果此项为 true，则 XAML 中的最后一个元素将填充剩余空间。未指定 Dock 设置的元素（在最后一个 XAML 元素之前）将默认为 DockPanel.Dock="Left"。

![](img/80ff26f06fc9ab951e1cd4257b867366_607_0.png)

图 2-5：
停靠面板。

### 清单 2-4：停靠面板 XAML

```xml
<DockPanel LastChildFill="True">
    <Button DockPanel.Dock="Left" Content="Far Left"/>
    <Button DockPanel.Dock="Left" Content="Near Left"/>
    <Button DockPanel.Dock="Top" Content="Top"/>
    <Button DockPanel.Dock="Bottom" Content="Bottom"/>
    <Button Content="Fill"/>
    <Button Content="Fill More"/>
</DockPanel>
```

## 画布

画布在 WPF 中有点异常，因为它不使用流布局，而是回到固定位置布局渲染。“什么？！”你说。“我以为流布局是未来的方向！”

确实如此……大多数时候。在某些情况下，应用程序的一部分需要以“旧方式”布局。用于设计平面图的图形应用程序就是一个完美的例子。

项目相对于任意一侧放置（或绘制）于画布上，图层通过 z 顺序处理。（参见图 2-6 和清单 2-5。）

![](img/80ff26f06fc9ab951e1cd4257b867366_607_1.png)

图 2-6：
画布示例。

### 清单 2-5：画布 XAML

```xml
<Canvas>
    <Rectangle Canvas.Left="40" Canvas.Top="40" Height="53" Name="rectangle1" Stroke="Black" Width="96" Fill="#FFEE2323" />
    <Ellipse Canvas.Left="28" Canvas.Top="142" Height="80" Name="ellipse1"
Stroke="Black" Width="161" Fill="#FF00D0FA" />
<Ellipse Canvas.Left="96" Canvas.Top="14" Height="108" Name="ellipse2"
Stroke="Black" Width="78" Fill="#FFED5620" />
</Canvas>
```

## 均匀网格

均匀网格将布局区域划分为大小相等的单元格。（参见图 2-7 和清单 2-6。）行数和列数在 UniformGrid XAML 标签中定义。如第 1 章所述，单元格内容使用 Grid.Row 和 Grid.Column 附加属性定位。请注意，行和列是从零开始的。

均匀网格不如网格（见下一节）多功能，但如果需要非常快速的棋盘格模式，它可以是一个有效的面板。为了突出单元格的边框，我添加了 Borders。有关 Borders 的更多信息，请参阅本章后面的“探索常用 XAML 控件”部分。

图 2-7：
均匀网格。

![](img/80ff26f06fc9ab951e1cd4257b867366_608_0.png)

### 清单 2-6：均匀网格 XAML

```xml
<UniformGrid Rows="2" Columns="2">
<Border Grid.Row="0" Grid.Column="0" BorderBrush="Black" BorderThickness="1"
HorizontalAlignment="Stretch" VerticalAlignment="Stretch">
<TextBlock Text="0,0"/>
</Border>
<Border Grid.Row="0" Grid.Column="1" BorderBrush="Black" BorderThickness="1"
HorizontalAlignment="Stretch" VerticalAlignment="Stretch">
<TextBlock Text="0,1"/>
</Border>
<Border Grid.Row="1" Grid.Column="0" BorderBrush="Black" BorderThickness="1"
HorizontalAlignment="Stretch" VerticalAlignment="Stretch">
<TextBlock Text="1,0"/>
</Border>
<Border Grid.Row="1" Grid.Column="1" BorderBrush="Black" BorderThickness="1"
HorizontalAlignment="Stretch" VerticalAlignment="Stretch">
<TextBlock Text="1,1"/>
</Border>
</UniformGrid>
```

## 网格

本迷你书第 1 章介绍了网格，它是屏幕设计的常见起点。事实上，当向项目添加新的 WPF 窗口时，网格是窗口中的默认面板。

网格使用行（RowDefinitions）和列（ColumnDefinitions）划分布局区域。网格与均匀网格的区别在于，网格允许通过定义 RowDefinition Height 和 ColumnDefinition Width 来调整单元格大小。

行和列的定义通过 Grid.RowDefinitions 和 Grid.ColumnDefinitions 标签指定（参见清单 2-7）。

### 清单 2-7：XAML 网格 RowDefinitions 和 ColumnDefinitions

```xml
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition Height="2*" />
        <RowDefinition Height="3*" />
    </Grid.RowDefinitions>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="*"/>
        <ColumnDefinition Width="2*"/>
    </Grid.ColumnDefinitions>
</Grid>
```

### 调整行和列大小

定义高度和宽度使用三种 GridUnitTypes：

- **像素：** 设备无关单位中的固定大小。
  
  你可以通过在定义中指定数字来基于 DIU 定义固定高度或宽度。这违背了流布局的原则，但确实有充分的理由这样做，例如当窗口上的图形图像缩放效果不佳（放大或缩小）且需要固定大小时。应谨慎使用固定大小，因为它会限制用户界面的有效性。如果内容是动态的或需要本地化，控件可能会裁剪内容或留下大量浪费的空间。

- **自动：** 大小基于内容的首选大小。
  
  Auto 定义允许行或列根据其内容确定可以有多大（或多小）。这是在布局过程的测量阶段决定的。

- **星号：** 大小使用所有剩余空间。
