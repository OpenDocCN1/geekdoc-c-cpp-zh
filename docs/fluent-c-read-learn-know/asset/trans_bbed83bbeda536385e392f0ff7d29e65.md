

## 带标题的内容控件

内容控件类层次结构中另一个重要的分支是派生自 HeaderedContentControl 的控件。带标题的内容控件是同时包含单个内容项和单个标题的控件。带标题内容控件的一个酷之处在于，与内容本身一样，标题可以是任何对象，例如 Image 或包含多个元素的面板。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_571_0.png)

Expander 控件可以向左、右、上或下打开，具体取决于 ExpandDirection 属性的设置。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_571_1.png)

GroupBox 仅在一个框中包含其内容，但通常用于控制一组 RadioButton 控件的行为。（我们将在下一节讨论这些控件。）

Expander 控件不直接支持滚动。此内容被包装在 ScrollViewer 中。

当 Expander 展开时，它会将其他内容推开。

### 戴上你的思考帽

你能重新创建示例窗口吗？以下是一些提示：

- 布局根是一个两列的 Grid。
- 两个 Expander 控件位于 Grid 右列的 StackPanel 中。
- 第一个 Expander 在 StackPanel 中包含一组 Label 控件。
- 第二个 Expander（其 Header 为 "2"）包含一个 ScrollViewer。ScrollViewer 包含一个 StackPanel。

### 你做得怎么样？

即使你的布局与我的略有不同，只要基本结构相同即可。（甚至结构也可以不同，只要窗口看起来相同。重要的是结果。）

```
<Grid>
<Grid.ColumnDefinitions>
<ColumnDefinition Width="232" />
<ColumnDefinition Width="146*" />
</Grid.ColumnDefinitions>
<GroupBox Header="Group Box" Height="135" Margin="10,10"
Name="groupBox1" Width="200">
<StackPanel>
<RadioButton FontSize="18" IsChecked="True">Option 1</RadioButton>
<RadioButton FontSize="18">Option 2</RadioButton>
<RadioButton FontSize="18">Option 3</RadioButton>
</StackPanel>
</GroupBox>
<StackPanel Grid.Column="1" >
<Expander Header="Expander 1" HorizontalAlignment="Left" Margin="20,10,0,0"
Name="expander1" IsExpanded="False">
<StackPanel>
<Label FontSize="14">Item 1</Label>
<Label FontSize="14">Item 2</Label>
<Label FontSize="14">Item 3</Label>
<Label FontSize="14">Item 4</Label>
</StackPanel>
</Expander>
<Expander Header="2" Margin="10,10" Name="expander2" ExpandDirection="Right"
IsExpanded="False" Padding="10,0" >
<ScrollViewer Height="75" >
<StackPanel>
<Label FontSize="14">Item 1</Label>
<Label FontSize="14">Item 2</Label>
<Label FontSize="14">Item 3</Label>
<Label FontSize="14">Item 4</Label>
</StackPanel>
</ScrollViewer>
</Expander>
</StackPanel>
</Grid>
```

你还没有见过 RadioButton 控件。语法写对了吗？如果写对了，做得好。

## 按钮

按钮是内容控件的最后一个重要分支。当然，你一直在使用基本的 Button，而你一直在做的事情——向 Click 事件添加代码——是任何类型按钮最常见的用法。但是是时候将按钮放在上下文中了。以下是类层次结构：

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_573_0.png)

我们将在第 18 章讨论 Command 对象。

ToggleButton 维护其状态。

RadioButton（几乎）总是成群结队。我们将在一两页内了解其工作原理。

CheckBox 可能看起来不像按钮，但如果你将“按钮”视为任何旨在被单击的东西，那么它就说得通了。

### 按钮内容

我们已经看到，ContentControl 的显著特征在于它定义了一个名为 Content 的属性。该属性定义为 Object，我已经说过这意味着它可以是任何东西。让我们使用熟悉的 Button 控件来探讨这一点的含义。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_574_0.png)

这是一个基本按钮。其内容（在属性语法中）定义为 Content="I'm a basic button"。你已经创建了很多这样的按钮。

这仍然是一个基本按钮。其内容使用属性语法定义：

```
<Button>
<Image Source="Binoculars.png" />
</Button>
```

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_574_1.png)

这挺酷的，但它有什么作用？我们应该添加一个标签，...

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_574_2.png)

这样更好。现在，我本可以将标签添加到图像中，但那真是走弯路。如果你想用不同的标签重复使用图像怎么办？相反，Button 的直接内容是一个包含 Image 和 Label 的 StackPanel：

```
<Button>
<StackPanel>
<Image Source="Binoculars.png" />
<Label>More Details</Label>
</StackPanel>
</Button>
```

### 单选按钮组

如果你回顾第 565 页的 RadioButton 部分类图，你会发现该类只为其派生自的 ToggleButton 添加了一个属性：GroupName，它定义为 String。与独立运行的其他类型按钮不同，RadioButtons 在组内交互——组内任何给定时间只能选择一个按钮。

创建 RadioButton 组有两种方法。你可以将它们嵌套在同一个容器中（通常，但不总是 GroupBox），或者可以显式地将 GroupName 属性分配给相同的值。

### 戴上你的思考帽

使用任何你喜欢的图像重新创建此窗口。当你运行它时，测试 RadioButton 和 CheckBox 对象的行为。它们都位于 GroupBox 内的 StackPanel 中，但行为不同。如何不同？

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_575_0.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_575_1.png)

### 你做得怎么样？

你可能使用了与我不同的布局对象，且大小可能不同。这没关系。

```
<Grid>
<Grid.ColumnDefinitions>
<ColumnDefinition Width="231" />
<ColumnDefinition Width="200" />
</Grid.ColumnDefinitions>
<Grid.RowDefinitions>
<RowDefinition Height="222" />
<RowDefinition Height="Auto" />
</Grid.RowDefinitions>
<Button Height="193" HorizontalAlignment="Left" Margin="10,10,0,0" Width="184">
<StackPanel>
<Image Source="Binoculars.png" Height="150" />
<Label HorizontalAlignment="Center" >More Details</Label>
</StackPanel>
</Button>
<GroupBox Grid.Column="1" Margin="10,10,10,19" Header="Choose one" Padding="10,10" BorderBrush="Black">
<StackPanel>
<RadioButton>Breakfast</RadioButton>
<RadioButton>Lunch</RadioButton>
<RadioButton>Dinner</RadioButton>
</StackPanel>
</GroupBox>
<GroupBox Grid.Row="1" Grid.ColumnSpan="2" Padding="10,10" Margin="10,10" Header="Choose as many as you like">
<StackPanel Orientation="Horizontal">
<CheckBox Margin="10,0">Mel</CheckBox>
<CheckBox Margin="10,0">Mel</CheckBox>
<CheckBox Margin="10,0">No, Pick Me!</CheckBox>
</StackPanel>
</GroupBox>
</Grid>
```

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_576_1.png)

### 休息一下

在完成复习并通过考察项控件来结束本章之前，为什么不快速休息一下呢？

Window 类与其他内容控件有何不同？

创建一组 RadioButton 有两种方法。是什么？

什么属性区分了内容控件？

你可以使用哪两种方法打开 Window？

什么属性区分了带标题的内容控件？

当你在组框中嵌套复选框时会发生什么？

如何在内容控件中嵌套多个对象？

## 项控件

控件层次结构的另一个重要分支是派生自 ItemsControl 的一组类。与内容控件一样，项控件采用单个内容元素，但该项是一个集合，即 Items 属性，它是 UIElement 对象的集合。（UIElement 是 FrameworkElement 的基类。）

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_578_0.png)

| 类 | 基类 |
|-------|------------|
| Control | FrameworkElement |

类层次结构的 Selector 分支添加了用户从 Items 集合中选择一个或多个项的能力。

| 类 | 基类 | 属性 | 方法 | 事件 |
|-------|------------|------------|---------|--------|
| TreeView | ItemsControl | SelectedItem, SelectedValue, SelectedValuePath | ExpandSubtree, ItemContainerGenerator, ScrollIntoView | SelectedItemChanged |

| 类 | 基类 | 属性 |
|-------|------------|------------|
| ItemsControl | Control | AlternationCount, HasItems, IsGrouping, IsTextSearchCaseSensitive, IsTextSearchEnabled, ItemContainerGenerator, Items, LogicalChildren |

| 类 | 类型 | 基类 | 属性 | 事件 |
|-------|------|------------|------------|--------|
| Selector | 抽象类 | Control | IsSynchronizedWithCurrentItem, SelectedIndex, SelectedItem, SelectedValue, SelectedValuePath | SelectionChanged |

菜单和工具栏也派生自 Selector。我们将在下一章中查看它们。

| 类 | 基类 | 属性 |
|-------|------------|------------|
| TabControl | Selector | SelectedContent, TabStripPlacement |

| 类 | 基类 | 属性 | 方法 |
|-------|------------|------------|---------|
| ListBox | Selector | SelectedItems | ScrollIntoView, SelectAll, UnselectAll |

| 类 | 基类 | 属性 | 事件 |
|-------|------------|------------|--------|
| ComboBox | Selector | IsDropDownOpen, IsEditable, IsReadOnly, IsSelectionBoxHighlighted, MaxDropDownHeight, SelectionBoxItem, SelectionBoxItemStringFormat, SelectionBoxItemTemplate, StaysOpenOnEdit, Text | DropDownClosed, DropDownOpened |

ListView 允许以不同方式显示其列表。（想想 Windows 资源管理器的项窗格。）这是使用模板和样式完成的，我们将在第 20 和 21 章中讨论。

| 类 | 基类 | 属性 |
|-------|------------|------------|
| ListView | ListBox | View |

