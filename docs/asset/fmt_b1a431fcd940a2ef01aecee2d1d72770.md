
| `IsExpanded` | 决定控件是否展开以显示其子元素。 |
| `Padding` | 在控件边缘与其内容之间添加额外空间 |
| `VerticalContentAlignment` | 决定内容在控件内的垂直对齐方式。可以是 `Bottom`（底部）、`Center`（居中）、`Stretch`（拉伸）或 `Top`（顶部）。 |

## 使用 Expander示例

以下代码创建一个包含 `StackPanel` 的 `Expander`。`StackPanel` 将包含 `Expander` 可以显示和隐藏的其他控件。

```
<Expander Header="Details" IsExpanded="True" BorderBrush="Blue">
<StackPanel>
  <!---- 省略其他控件。 -->
</StackPanel>
</Expander>
```

## EXPRESSION BLEND示例

Expression Blend 属性选项卡使用 `Expander` 让你能够显示和隐藏不同的属性组，如画刷（Brushes）、外观（Appearance）、布局（Layout）等。

## GRID

作为强大且实用的布局控件之一，`Grid` 允许你按行和列排列子元素。`Grid` 的关键属性见表 C-6。

### 表 C-6

| 属性 | 目的 |
| --- | --- |
| `Background` | 用于填充控件内部的颜色 |
| `ColumnDefinitions` | 此属性元素包含定义列宽的 `ColumnDefinition` 对象 |
| `RowDefinitions` | 此属性元素包含定义行高的 `RowDefinition` 对象 |

子元素可以使用这些属性来告诉 `Grid` 如何定位自己。`Grid` 的关键附加属性见表 C-7。

### 表 C-7

| 属性 | 目的 |
| --- | --- |
| `Grid.Column` | 包含子元素的列 |
| `Grid.ColumnSpan` | 子元素占据的列数 |
| `Grid.Row` | 包含子元素的行 |
| `Grid.RowSpan` | 子元素占据的行数 |

## 创建数据网格示例

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

`ScrollView` 在滚动区域内显示单个子元素。`ScrollView` 的关键属性见表 C-8。

### 表 C-8：ScrollView 的关键属性

| 属性 | 目的 |
| --- | --- |
| `Background` | 用于填充控件内部的颜色 |
| `HorizontalContentAlignment` | 决定内容在控件内的水平对齐方式。可以是 `Center`、`Left`、`Right` 或 `Stretch`。 |
| `VerticalContentAlignment` | 决定内容在控件内的垂直对齐方式。可以是 `Bottom`、`Center`、`Stretch` 或 `Top`。 |
| `HorizontalVisibility` | 决定水平滚动条是否显示。可以是 `Auto`。 |
| `VerticalVisibility` | 决定垂直滚动条是否显示。可以是 `Auto`。 |
| `Padding` | 在控件边缘与其内容之间添加额外空间 |

### SILLY SCROLLBARS（奇怪的滚动条）

使用 `ScrollViewer`

以下代码创建了一个包含大图片的 `ScrollViewer`。当窗口足够小时，滚动条会出现。

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

## STACKPANEL（栈面板）

`StackPanel` 是最实用的布局控件之一。它以垂直或水平方式排列子元素。如果控件空间不足，它会裁剪任何子元素。`StackPanel` 的关键属性见表 C-9。

### 表 C-9：StackPanel 的关键属性

| 属性 | 目的 |
| --- | --- |
| `Background` | 用于填充控件内部的颜色 |
| `Orientation` | 决定控件是按行（`Orientation = Horizontal`）还是按列（`Orientation = Vertical`）排列子元素 |

### 使用 StackPanel示例

以下代码创建了按列排列的三个按钮。`StackPanel` 的 Resource 部分创建了一个未命样式，为按钮提供了一致的 `Margin`、`Width` 和 `Height` 属性。

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

## STATUSBAR（状态栏）

`StatusBar` 创建了一个区域（通常在窗口底部），你可以在那里向用户状态信息。你可以在 `StatusBar` 中放置 `StatusBarItems`、`Button`、`ComboBox` 以及其他控件。`StatusBar` 的关键属性见表 C-10。

### 表 C-10：StatusBar 的关键属性

| 属性 | 目的 |
| --- | --- |
| `Background` | 填充控件内部的颜色 |
| `BorderBrush` | 控件边缘的颜色 |
| `BorderThickness` | 控件的厚度 |

你可以将 `Label` 和 `Button` 直接放置在 `StatusBar` 中，但将 `StatusBarItems` 放置在 `StatusBar` 内部可以获得更好的效果。在这种情况下，`StatusBar` 的行为就像一个水平的 `StackPanel`，会拉伸最后一个子元素以填充可用空间。如果你直接将控件放置在 `StatusBar` 中，它不会拉伸最后一个控件。

以下代码构建了一个 `DockPanel`，其顶部显示一个 `Menu`，底部显示一个 `StatusBar`，中间部分显示一个 `Grid`：

```xml
<DockPanel>
  <Menu DockPanel.Dock="Top">
    <!-- 省略了菜单项。 -->
  </Menu>

  <StatusBar DockPanel.Dock="Bottom">
    <StatusItem>
      <Label Content="Status:"/>
    </StatusItem>
    <Label Content="Normal" Background="White" Padding="10,6,10,6">
      <BitmapEffect>
        <BevelItBitmapEffect EdgeProfile="BulgedUp"/>
      </BitmapEffect>
    </Label>
  </StatusItem>
    <StatusItem HorizontalAlignment="Right">
    <Button Content="Disconnect"/>
  </StatusItem>
  </StatusBar>

  <Grid>
    <!-- 省略了其他控件。 -->
  </Grid>
</DockPanel>
```

`StatusBar` 包含一对带有 `Label` 的 `StatusItems`。第三个 `StatusItem` 设置了 `HorizontalAlignment = Right`，因此该项被移动到 `StatusBar` 的右边缘。

## TABCONTROL（选项卡控件）

`TabControl` 显示了一系列选项卡，你可以在其中放置不同的信息组。该控件应包含一系列 `TabItems`，每个 `TabItem` 包含一个项目（通常是一个容器，如 `Grid`）。`TabControl` 的属性见表 C-11。

### 表格 C-11：TabControl 的关键属性

| 属性 | 用途 |
| --- | --- |
| `Background` | 用于填充选项卡内容内部区域的颜色。此颜色不填充头部区域。 |
| `BorderBrush` | 选项卡内容边缘的颜色。这不包含头部区域。 |

#### 表格 C-11（续）

| 属性 | 用途 |
|---|---|
| `BorderThickness` | 内容区域的边框厚度。这不包含头部区域。 |
| `FlowDirection` | 决定选项卡是从右到左还是从左到右排列。 |
| `FontFamily` | 字体族名称，如 `Times New Roman`、`Arial` 或 `Segoe` |
| `FontSize` | 文本的字体大小。后附加 `cm`、`in`、`px` 或 `pt` 以指定厘米、英寸（默认值）或磅（1/72 英寸），例如 `"0.25inch"` 或 `"12"`。 |
| `FontStyle` | 可以是 `Normal`（正常）、`Italic`（斜体）或 `Oblique`（对于没有斜体样式的字体模拟斜体） |
| `FontWeight` | 文本的粗细。可以是 `Thin`、`ExtraLight`、`Light`、`Normal`、`Medium`、`Semibold`、`Bold`、`ExtraBold`、`Black`，尽管许多字体在这些值下看起来是相同的。 |
| `Padding` | 控件边缘与选项卡内容之间添加的额外空间。不包含头部区域。 |
| `SelectedIndex` | 当前选中选项卡的从 0 开始的索引。 |
| `TabStripPlacement` | 决定条的位置。可以是 `Bottom`（底部）、`Left`（左侧）、`Right`（右侧）或 `Top`（顶部）。 |

表 C-12 总结了放在 `TabControl` 内部的 `Tab` 对象最重要的属性。

## 表格 C-12：TabItem 对象的关键属性

| 属性 | 用途 |
|---|---|
| `Foreground` | 用于绘制头部文本的颜色 |
| `Header` | 标签上显示的内容。通常是纯文本。 |
| `IsSelected` | 决定此选项卡当前是否被选中。 |
| `Padding` | 头部区域边缘与头部控件之间添加的额外空间 |

## 示例 使用 TabControl

以下代码创建了一个 `TabControl`，其中包含三个头部分别为 Customers（客户）、Products（产品）和 Employees（员工）的 `TabItems`：

```xml
<TabControl>
  <TabItem Header='Customers'>
    <Grid>
      <!-- 省略了控件。 -->
    </Grid>
  </TabItem>
  <TabItem Header="Products">
    <Grid>
      <!-- 省略了控件。 -->
    </Grid>
  </TabItem>
  <TabItem Header="Employees">
    <Grid>
      <!-- 省略了控件。 -->
    </Grid>
  </TabItem>
</TabControl>
```

## 示例 使用旋转的 TabControl

以下代码与上一个示例相似，区别在于将选项卡放置在 `TabControl` 的左侧。代码使用 `styTabHeader` 样式将头部旋转 -90 度，这样它们就不会占用巨大的空间。

```xml
<TabControl StripPlacement="Left">
  <TabControl.Resources>
    <Style x:Key="styTabHeader" TargetType="TextBlock">
      <Setter Property="FontSize" Value="14"/>
      <Setter Property="FontWeight" Value="Bold"/>
      <Setter Property="Padding" Value="4,0,4,0"/>
      <Setter Property="LayoutTransform">
        <Value>
          <RotateTransform Angle="-90"/>
        </Value>
      </Setter>
    </Style>
  </TabControl.Resources>
  <TabItem>
    <TabItem.Header>
      <TextBlock Text="Customers" Style="StaticResource styTabHeader"/>
    </TabItem.Header>
    <Grid>
      <!-- 省略了控件。 -->
    </Grid>
  </TabItem>
  <TabItem>
    <TabItem.Header>
      <TextBlock Text="Products" Style="StaticResource styTabHeader"/>
    </TabItem.Header>
    <Grid>
      <!-- 省略了控件。 -->
    </Grid>
  </TabItem>
  <TabItem>
    <TabItem.Header>
      <TextBlock Text="Employees" Style="StaticResource styTabHeader"/>
    </TabItem.Header>
    <Grid>
      <!-- 省略了控件。 -->
    </Grid>
  </TabItem>
</TabControl>
```

图1：旋转选项卡

## TOOL AND TOOLRAY（工具栏与工具托）

`Toolbar` 显示了一系列按钮、组合框和其他工具。`ToolTray` 包含一个或多个带。关键属性见表 C-13。

#### 表格 C-13

| 属性 | 用途 |
|---|---|
| `Background` | 用于填充工具栏内部 |
| `FlowDirection` | 决定带是从右到左还是从左到右排列。 |
| `IsLocked` | 如果为 `True`，用户无法移动带。 |
| `Orientation` | 决定带的方向 |

#### 表格 C-14：Toolbar 的属性

| 属性 | 用途 |
|---|---|
| `Background` | 用于填充工具栏内部的颜色 |
| `Band` | 决定 `Toolbar` 占据的带 |
| `BorderBrush` | 工具栏边缘的颜色 |
| `BorderThickness` | 工具栏的厚度 |

## 示例 使用 Toolbars

图 C-2 所示工具栏使用以下代码创建一个带有 `Toolbar` 和 `StatusBar` 的窗口。`Toolbar` 包含位于两个带中的三个。

```xml
<DockPane.Dock="Top" Background="LightGray">
  <ToolBar Band="0" BandIndex="0">
    <Button>
      <Image Source="New.ico"/>
    </Button>
    <Button>
      <Image Source="Open.ico"/>
    </Button>
  </ToolBar>
  <ToolBar Band="0" BandIndex="1">
    <Button>
      <Image Source="Copy.ico"/>
    </Button>
    <Button>
      <Image Source="Cut.ico"/>
    </Button>
  </ToolBar>
</DockPane>
```

图 C-2

```xml
<ToolBar Band="1" Height="30">
  <Button>
    <Image Source="Add.png"/>
  </Button>
  <Button>
    <Image Source="Cancel.png"/>
  </Button>
  <Button>
    <Image Source="Ok.png"/>
  </Button>
</ToolBar>
```

## UNIFORMGRID（均匀网格）

`UniformGrid` 将其子项在均匀大小的行和列中排列。`UniformGrid` 的关键属性见表 C-15。

表格 C-15

| 属性 | 用途 |
