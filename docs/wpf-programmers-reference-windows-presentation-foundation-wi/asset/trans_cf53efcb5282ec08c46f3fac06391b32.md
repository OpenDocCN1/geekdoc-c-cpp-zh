

### 表 C-4：DockPanel 的关键附加属性

| 属性 | 目的 |
| --- | --- |
| DockPanel.Bottom | 使子元素填充 DockPanel 剩余区域的底部。 |
| DockPanel.Left | 使子元素填充 DockPanel 剩余区域的左侧。 |
| DockPanel.Right | 使子元素填充 DockPanel 剩余区域的右侧。 |
| DockPanel.Top | 使子元素填充 DockPanel 剩余区域的顶部。 |

### 使用 Dock示例

以下代码创建了一个包含 Menu（菜单）和 Grid（网格）的 DockPanel。正如通常预期的那样，Menu 靠在 DockPanel 的顶部。Grid 占据 DockPanel 的其余部分，可以包含你想在窗口上显示的任何内容。

```
<DockPanel LastChildFill="True">
  <Menu DockPanel.Dock="Top">
    <!-- 省略项 -->
  </Menu>
  <Grid>
    <!-- 省略其他控件。 -->
  </Grid>
</DockPanel>
```

### EXPANDER（折叠控件）

Expander 显示一个标题和一个图标，你可以点击它来显示或隐藏单个子元素。Expander 的关键属性见表 C-5。

### 表 C-5：Expander 的关键属性

| 属性 | 目的 |
| --- | --- |
| Background | 用于填充控件内部的颜色 |
| BorderBrush | 控件边缘的颜色 |
| BorderThickness | 控件边缘的厚度 |
| ExpandDirection | 决定内容展开的方向。可以是 Down（下）、Left（左）、Right（右）或 Up（上）。 |
| FontFamily | 字体族名称，例如 Times New Roman、Arial 或 Segoe（读作 see-go） |

446 | 附录 C 布局控件

### 表 C-5（续）

| 属性 | 目的 |
| --- | --- |
| FontSize | 文本的字体大小。通过附加 cm、in、px 或 pt 来指定厘米、英寸、像素（默认值）或磅（1/72 英寸），例如 "0.25in" 或 "12pt"。 |
| FontStyle |可以是 Normal（正常）、Italic（斜体）或 Oblique（倾斜，对于具有斜体样式的字体模拟斜体效果） |
| FontWeight | 文本的粗细。可以是 Thin、ExtraLight、Light、Normal、Medium、SemiBold、Bold、ExtraBold、Black 和 ExtraBlack，尽管许多字体在这些值上看起来是相同的。 |
| Foreground | 用于绘制 Expander Header（标题）的颜色 |
| Header | 显示在 Expander 顶部、展开/隐藏按钮旁边的文本 |
| HorizontalContentAlignment | 决定内容在控件内的水平对齐方式。可以是 Center（居中）、Left（左）、Right（右）或 Stretch（拉伸）。 |
| IsExpanded | 决定控件是否展开以显示其子元素。 |
| Padding | 在控件边缘与其内容之间添加额外空间 |
| VerticalContentAlignment | 决定内容在控件内的垂直对齐方式。可以是 Bottom（底部）、Center（居中）、Stretch（拉伸）或 Top（顶部）。 |

### 使用 Expander示例

以下代码创建一个包含 StackPanel 的 Expander。StackPanel 将包含 Expander 可以显示和隐藏的其他控件。

```
<Expander Header="Details" IsExpanded="True" BorderBrush="Blue">
<StackPanel>
  <!---- 省略其他控件。 -->
</StackPanel>
</Expander>
```

### EXPRESSION BLEND示例

Expression Blend 属性选项卡使用 Expander 让你能够显示和隐藏不同的属性组，如画刷（Brushes）、外观（Appearance）、布局（Layout）等。

### GRID

作为强大且实用的布局控件之一，Grid 允许你按行和列排列子元素。Grid 的关键属性见表 C-6。

### 表 C-6：

| 属性 | 目的 |
| --- | --- |
| Background | 用于填充控件内部的颜色 |
| ColumnDefinitions | 此属性元素包含定义列宽的 ColumnDefinition 对象 |
| RowDefinitions | 此属性元素包含定义行高的 RowDefinition 对象 |

子元素可以使用这些属性来告诉 Grid 如何定位自己。Grid 的关键附加属性见表 C-7。

### 表 C-7：

| 属性 | 目的 |
| --- | --- |
| Grid.Column | 包含子元素的列 |
| Grid.ColumnSpan | 子元素占据的列数 |
| Grid.Row | 包含子元素的行 |
| Grid.RowSpan | 子元素占据的行数 |

### 创建数据网格示例

以下代码构建了一个相当标准的数据输入表单，允许用户输入名称、地址和其他信息：

```
<Grid.RowDefinitions>
  <RowDefinition Height="40"/>
  <RowDefinition Height="30"/>
  <RowDefinition Height="30"/>
  <!-- 省略其他行定义 -->
</Grid.RowDefinitions>
<Grid.ColumnDefinitions>
  <ColumnDefinition Width="100"/>
  <ColumnDefinition Width="*"/>
</Grid.ColumnDefinitions>

<Label Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="2" Content="New Customer"
```

### SCROLLVIEWER（滚动器）

ScrollView 在滚动区域内显示单个子元素。ScrollView 的关键属性见表 C-8。

### 表 C-8：ScrollView 的关键属性

| 属性 | 目的 |
| --- | --- |
| Background | 用于填充控件内部的颜色 |
| HorizontalContentAlignment | 决定内容在控件内的水平对齐方式。可以是 Center、Left、Right 或 Stretch。 |
| VerticalContentAlignment | 决定内容在控件内的垂直对齐方式。可以是 Bottom、Center、Stretch 或 Top。 |
| HorizontalVisibility | 决定水平滚动条是否显示。可以是 Auto。 |
| VerticalVisibility | 决定垂直滚动条是否显示。可以是 Auto。 |
| Padding | 在控件边缘与其内容之间添加额外空间 |

### SILLY SCROLLBARS（奇怪的滚动条）

使用 ScrollViewer

以下代码创建了一个包含大图片的 ScrollViewer。当窗口足够小时，滚动条会出现。

```
<Grid>
    <ScrollView
        HorizontalScrollBarVisibility="Auto"
        VerticalScrollBarVisibility="Auto">
        <Image Stretch="None"
               Source="http://vb-helper.com/compressed_2.jpg" />
    </ScrollView>
</Grid>
```

 STACKPANEL（栈面板）

StackPanel 是最实用的布局控件之一。它以垂直或水平方式排列子元素。如果控件空间不足，它会裁剪任何子元素。StackPanel 的关键属性见表 C-9。

### 表 C-9：StackPanel 的关键属性

| 属性 | 目的 |
| --- | --- |
| Background | 用于填充控件内部的颜色 |
| Orientation | 决定控件是按行（Orientation = Horizontal）还是按列（Orientation = Vertical）排列子元素 |

### 使用 StackPanel示例

以下代码创建了按列排列的三个按钮。StackPanel 的 Resource 部分创建了一个未命样式，为按钮提供了一致的 Margin、Width 和 Height 属性。

```
<StackPanel>
  <StackPanel.Resources>
    <Style TargetType="Button">
      <Setter Property="Margin" Value="5"/>
      <Setter Property="Width" Value="100"/>
      <Setter Property="Height" Value="40"/>
    </Style>
  </StackPanel.Resources>
  <Button Content="Add Customer"/>
  <Button Content="Find Customer"/>
  <Button Content="Delete Customer"/>
</StackPanel>
```

 STATUSBAR（状态栏）

StatusBar 创建了一个区域（通常在窗口底部），你可以在那里向用户状态信息。你可以在 StatusBar 中放置 StatusBarItems、Button、ComboBox 以及其他控件。StatusBar 的关键属性见表 C-10。

### 表 C-10：StatusBar 的关键属性

| 属性 | 目的 |
| --- | --- |
| Background | 填充控件内部的颜色 |
| BorderBrush | 控件边缘的颜色 |
| BorderThickness | 控件的厚度 |

你可以将 Label 和 Button 直接放置在 StatusBar 中，但将 StatusBarItems 放置在 StatusBar 内部可以获得更好的效果。在这种情况下，StatusBar 的行为就像一个水平的 StackPanel，会拉伸最后一个子元素以填充可用空间。如果你直接将控件放置在 StatusBar 中，它不会拉伸最后一个控件。

