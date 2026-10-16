

<Button>Button</Button>
</StackPanel>
</Window>

图 34.5 显示了 StackPanel 的子控件垂直排列。

![](img/3d365b72b289213a91ade7eb366b8f35_1303_0.png)

图 34.5

## WrapPanel

WrapPanel 将子元素从左到右依次放置，只要它们能在一行内容纳，就继续到下一行。面板的 Orientation 可以是水平或垂直（代码文件 LayoutSamples/WrapPanelWindow.xaml）：

```
<Window x:Class="LayoutSamples.WrapPanelWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/
        xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/
        winfx/2006/xaml"
        Title="WrapPanelWindow" Height="300" Width="300">
    <WrapPanel>
        <WrapPanel.Resources>
            <Style TargetType="Button">
                <Setter Property="Width" Value="100" />
                <Setter Property="Margin" Value="5" />
            </Style>
        </WrapPanel.Resources>
        <Button>Button</Button>
        <Button>Button</Button>
        <Button>Button</Button>
        <Button>Button</Button>
<Button>Button</Button>
<Button>Button</Button>
<Button>Button</Button>
<Button>Button</Button>
</WrapPanel>
</Window>
```

图 34.6 显示了该面板的输出。如果调整应用程序大小，按钮会相应地重新排列，以使一行内恰好容纳相应数量的按钮。

![](img/3d365b72b289213a91ade7eb366b8f35_1304_0.png)

图 34.6

## Canvas

Canvas 是一个面板，可让你显式定位控件。Canvas 定义了附加属性 Left、Right、Top 和 Bottom，可由子元素用于在面板内定位（代码文件 LayoutSamples/CanvasWindow.xaml）：

```
<Canvas Background="LightBlue">
    <Label Canvas.Top="30" Canvas.Left="20">Enter here:</Label>
    <TextBox Canvas.Top="30" Canvas.Left="120" Width="100" />
    <Button Canvas.Top="70" Canvas.Left="130" Content="Click Me!" Padding="5" />
</Canvas>
```

图 34.7 显示了 Canvas 面板及其定位后的子元素 Label、TextBox 和 Button 的输出。

# 图 34.7

> 注意 Canvas 控件最适合用于图形元素的布局，例如第 30 章中所示的 Shape 控件。

## DockPanel

DockPanel 与 Windows Forms 的停靠功能非常相似。在这里，你可以指定子控件应如何排列的区域。DockPanel 定义了附加属性 Dock；你可以在控件的子元素中使用 Left、Right、Top 和 Bottom 值设置该属性。图 34.8 显示了在 dock 面板中排列的带边框的文本块的结果。为了便于区分，为各个区域指定了不同的颜色（代码文件 LayoutSamples/DockPanelWindow.xaml）：

```
<DockPanel>
    <Border Height="25" Background="AliceBlue" DockPanel.Dock="Top">
        <TextBlock>Menu</TextBlock>
    </Border>
    <Border Height="25" Background="Aqua" DockPanel.Dock="Top">
        <TextBlock>Ribbon</TextBlock>
    </Border>
    <Border Height="30" Background="LightSteelBlue"
DockPanel.Dock="Bottom">
    <TextBlock>Status</TextBlock>
</Border>
<Border Height="80" Background="Azure" DockPanel.Dock="Left">
    <TextBlock>Left Side</TextBlock>
</Border>
<Border Background="HotPink">
    <TextBlock>Remaining Part</TextBlock>
</Border>
</DockPanel>
```

![](img/3d365b72b289213a91ade7eb366b8f35_1306_0.png)

图 34.8

## Grid

使用 Grid，你可以用行和列排列控件。对于每一列，你可以指定一个 ColumnDefinition。对于每一行，你可以指定一个 RowDefinition。以下示例代码列出了两列和三行。每一列和每一行都可以指定宽度或高度。ColumnDefinition 具有 Width 依赖属性；RowDefinition 具有 Height 依赖属性。你可以用像素、厘米、英寸或磅定义高度和宽度，或将其设置为 Auto 以根据内容确定大小。网格还允许星号大小调整，这意味着行和列的空间是根据可用空间以及相对于其他行和列计算的。当为列提供可用空间时，你可以将 Width 属性设置为 *。要使另一列的大小加倍，你指定 2*。示例代码定义了两列和三行，但未对列和行定义进行额外设置；默认是星号大小调整。

网格包含多个 Label 和 TextBox 控件。因为这些控件的父级是网格，所以你可以设置附加属性 Column、ColumnSpan、Row 和 RowSpan（代码文件 LayoutSamples/GridWindow.xaml）：

```
<Grid ShowGridLines="True">
    <Grid.ColumnDefinitions>
        <ColumnDefinition />
        <ColumnDefinition />
    </Grid.ColumnDefinitions>
    <Grid.RowDefinitions>
        <RowDefinition />
        <RowDefinition />
        <RowDefinition />
    </Grid.RowDefinitions>
    <Label Grid.Column="0" Grid.ColumnSpan="2" Grid.Row="0" VerticalAlignment="Center" HorizontalAlignment="Center" Content="Title" />
    <Label Grid.Column="0" Grid.Row="1" VerticalAlignment="Center" Content="Firstname:" Margin="10" />
    <TextBox Grid.Column="1" Grid.Row="1" Width="100" Height="30" />
    <Label Grid.Column="0" Grid.Row="2" VerticalAlignment="Center" Content="Lastname:" Margin="10" />
    <TextBox Grid.Column="1" Grid.Row="2" Width="100" Height="30" />
</Grid>
```

在网格中排列控件的结果如图 34.9 所示。为了更清晰地查看列和行，将 ShowGridLines 属性设置为 true。

![](img/3d365b72b289213a91ade7eb366b8f35_1308_0.png)

# 图 34.9

> 注意 对于每个单元格大小相同的网格，你可以使用 UniformGrid 类。

## Triggers

第 30 章中介绍了如何使用 Visual State Manager 动态更改控件的外观。Visual State Manager 同时受 WPF 和通用 Windows 平台支持。WPF 还为同一场景提供了属性触发器，并且针对不同场景还有其他触发器类型。本节讨论属性触发器、多触发器和数据触发器。

使用触发器，你可以根据某些事件或属性值更改动态更改控件的外观。例如，当用户将鼠标悬停在按钮上时，按钮可以改变其外观。通常，你需要用 C# 代码来完成此操作。使用 WPF，只要影响 UI，你也可以用 XAML 来完成此操作。

属性触发器在属性值更改时激活。多触发器基于多个属性值。事件触发器触发

> 注意 如果 IsPressed 属性设置为 true，则 IsMouseOver 属性也将为 true。按下按钮也需要鼠标位于按钮上方。按下按钮会触发其执行并相应地更改属性。在这里，触发器的顺序很重要。如果将 IsPressed 属性触发器移至 IsMouseOver 属性触发器之前，IsMouseOver 属性触发器将覆盖第一个触发器设置的值。

当触发原因不再有效时，你无需将属性值重置为原始值。例如，你无需为 IsMouseOver=true 和 IsMouseOver=false 定义触发器。一旦触发原因不再有效，触发器操作所做的更改会自动重置为原始值。

图 34.10 显示了触发器示例应用程序，其中在按钮获得焦点时，其前景色和字体大小从原始值更改。

![](img/3d365b72b289213a91ade7eb366b8f35_1310_0.png)

> **注意** 使用属性触发器时，极其容易更改控件的外观、字体、颜色、不透明度等。当鼠标移过它们时，键盘设置焦点——无需一行编程代码。

`Trigger` 类定义了以下属性来指定触发器操作。

| Trigger 属性 | 描述 |
|---|---|
| `PropertyValue` | 对于属性触发器，使用 `Property` 和 `Value` 属性指定触发器何时触发——例如，`Property="IsMouseOver"` `Value="True"`。 |
| `Setters` | 一旦触发器触发，你可以使用 `Setters` 定义一组 `Setter` 元素来更改属性值。`Setter` 类定义了属性 `Property`、`TargetName` 和 `Value`，用于更改对象属性。 |
| `EnterActions`, `ExitActions` | 而不是定义 setter，你可以定义 `EnterActions` 和 `ExitActions`。在这两个属性中，你可以定义一组 `TriggerAction` 元素。`EnterActions` 在触发器开始时触发（对于属性触发器，当 `Property`/`Value` 组合适用时）；`ExitActions` 在其结束前触发（就在 `Property`/`Value` 组合不再适用时）。可通过这些操作指定的触发器操作派生自基类 `TriggerAction`，例如 `SoundPlayerAction` 和 `BeginStoryboard`。使用 `SoundPlayerAction`，你可以开始播放声音。`BeginStoryboard` 与本章后面讨论的动画一起使用。 |

## MultiTrigger

属性触发器在属性值更改时触发。如果需要因为两个或多个属性具有特定值而设置触发器，可以使用 `MultiTrigger`。

`MultiTrigger` 具有 `Conditions` 属性，可指定属性的有效值。它还具有 `Setters` 属性，可让你指定需要设置的属性。在以下示例中，为 `TextBox` 元素定义了一种样式，使得当 `IsEnabled` 属性为 `True` 且 `Text` 属性值为 `Test` 时触发器适用。尝试在空白文本框中输入 Test。如果两者都适用，则 `TextBox` 的 `Foreground` 属性将设置为 `Red`（代码文件 `TriggerSamples/MultiTriggerWindow.xaml`）：

