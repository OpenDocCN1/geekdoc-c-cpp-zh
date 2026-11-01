
## 项目控件

ItemsControl 类包含一个可以通过 Items 属性访问的项目列表。派生自 ItemsControl 的类在下表中显示。

| 项目控件 | 描述 |
|---|---|
| Menu ContextMenu | 类 Menu 和 ContextMenu 派生自抽象基类 MenuBase。你可以通过在项目列表中放置 MenuItem 元素并关联命令来向用户提供菜单。 |
| StatusBar | StatusBar 控件通常显示在应用程序底部，以向用户提供状态信息。你可以在 StatusBar 列表中放置 StatusBarItem 元素。 |
| TreeView | 对于项目的层次结构显示，你可以使用 TreeView 控件。 |
| ListBox ComboBox TabControl | ListBox、ComboBox 和 TabControl 具有相同的抽象基类 Selector。此基类使从列表中选择项目成为可能。ListBox 显示列表中的项目。ComboBox 具有额外的 Button 控件，仅在按钮被点击时才显示项目。通过 TabControl，内容可以以表格形式排列。 |
| DataGrid | DataGrid 控件是一个可自定义的网格，用于显示数据。此控件在 .NET 4 中新增，并在下一章中详细讨论。 |

## 带头的项目控件

HeaderedItemsControl 是包含项目但同时具有标题的控件的基类。类 HeaderedItemsControl 派生自 ItemsControl。

派生自 HeaderedItemsControl 的类在下表中列出。

| 带头的项目控件 | 描述 |
|---|---|
| MenuItem | 菜单类 Menu 和 ContextMenu 包含 MenuItem 类型的项目。菜单项可以连接到命令，因为 MenuItem 类实现了 ICommandSource 接口。 |
| TreeViewItem | TreeView 类可以包含 TreeViewItem 类型的项目。 |
| ToolBar | ToolBar 控件是一组控件的容器，通常是 Button 和 Separator 元素。你可以将 ToolBar 放置在 ToolBarTray 内部，后者处理 ToolBar 控件的重新排列。 |

## 装饰

对单个元素添加装饰使用 Decorator 类完成。Decorator 是一个基类，具有 Border、Viewbox 和 BulletDecorator 等派生类。ButtonChrome 和 ListBoxChrome 等主题元素也是装饰器。

![](img/d7d2ffa0a76feaab821930e95daace93_1059_0.png)

以下示例演示了 Border、Viewbox 和 BulletDecorator，如图 35-12 所示。

Border 类通过在其周围添加边框来装饰 Children 元素。你可以定义边框的画刷和厚度、背景、角的半径以及其子元素的内边距：

```
</ListBox>
<Button>Button</Button>
</StackPanel>
</Window>
```

代码片段 LayoutDemo/StackPanelWindow.xaml

你可以在图 35-13 中看到 StackPanel 的子控件垂直组织。

![](img/d7d2ffa0a76feaab821930e95daace93_1061_0.png)

图 35-13

## 换行面板

WrapPanel 将子元素从左到右依次定位，只要它们适合当前行，然后继续下一行。面板的方向可以是水平或垂直：

```
<Window x:Class="LayoutDemo.WrapPanelWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="WrapPanelWindow" Height="300" Width="300">
<WrapPanel>
<Button Width="100" Margin="5">Button</Button>
<Button Width="100" Margin="5">Button</Button>
<Button Width="100" Margin="5">Button</Button>
<Button Width="100" Margin="5">Button</Button>
<Button Width="100" Margin="5">Button</Button>
<Button Width="100" Margin="5">Button</Button>
<Button Width="100" Margin="5">Button</Button>
<Button Width="100" Margin="5">Button</Button>
</WrapPanel>
</Window>
```

代码片段 LayoutDemo/WrapPanelWindow.xaml

图 35-14 显示了面板的输出。如果调整应用程序大小，则按钮将被重新排列以使其适合一行。

![](img/d7d2ffa0a76feaab821930e95daace93_1061_1.png)

图 35-14

## 画布

Canvas 是一个面板，允许你显式定位控件。Canvas 定义了附加属性 Left、Right、Top 和 Bottom，可由子元素用于在面板内定位：

```
<Window x:Class="LayoutDemo.CanvasWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="CanvasWindow" Height="300" Width="300">
<Canvas Background="LightBlue">
<Label Canvas.Top="30" Canvas.Left="20">Enter here:</Label>
<TextBox Canvas.Top="30" Canvas.Left="120" Width="100" />
<Button Canvas.Top="70" Canvas.Left="130" Content="Click Me!" Padding="5" />
</Canvas>
</Window>
```

代码片段 LayoutDemo/CanvasWindow.xaml

对于一列，你可以将 Width 属性设置为 *。要使另一列的大小加倍，你指定 2*。示例代码定义了两列和三行，没有使用列和行定义定义额外的设置；默认是星号大小。

网格包含多个 Label 和 TextBox 控件。因为这些控件的父级是网格，所以你可以设置附加属性 Column、ColumnSpan、Row 和 RowSpan：

```
<Window x:Class="LayoutDemo.GridWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="GridWindow" Height="300" Width="300">
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
        <Label Grid.Column="0" Grid.ColumnSpan="2" Grid.Row="0"
               VerticalAlignment="Center" HorizontalAlignment="Center" Content="Title" />
        <Label Grid.Column="0" Grid.Row="1" VerticalAlignment="Center"
               Content="Firstname:" Margin="10" />
        <TextBox Grid.Column="1" Grid.Row="1" Width="100" Height="30" />
        <Label Grid.Column="0" Grid.Row="2" VerticalAlignment="Center"
               Content="Lastname:" Margin="10" />
        <TextBox Grid.Column="1" Grid.Row="2" Width="100" Height="30" />
    </Grid>
</Window>
```

代码片段 LayoutDemo/GridWindow.xaml

将控件排列在网格中的结果如图 35-17 所示。为了更方便地查看列和行，属性 ShowGridLines 被设置为 true。

![](img/d7d2ffa0a76feaab821930e95daace93_1063_0.png)

图 35-17

> 对于每个单元格大小相同的网格，你可以使用 UniformGrid 类。

## 样式和资源

你可以通过设置属性，例如 FontSize 和 Background，使用 Button 元素来定义 WPF 元素的外观，如下所示：

```
<Button Width="150" FontSize="12" Background="AliceBlue" Content="Click Me!" />
```

代码片段 StylesAndResources/MainWindow.xaml

而不是为每个元素定义外观，你可以定义存储在资源中的样式。要完全自定义控件的外观，可以使用模板并将其存储到资源中。

### 样式

控件的 Style 属性可以分配给具有相关 setter 的 Style 元素。Setter 元素定义 Property 和 Value 属性，并将指定属性设置为值。在这里，设置了 Background、FontSize 和 FontWeight 属性。Style 设置为 TargetType Button，以便可以直接访问 Button 的属性。如果样式的 TargetType 未设置，则属性可以通过 Button.Background、Button.FontSize 访问。这在需要设置不同元素类型的属性时尤其重要。

```
<Button Width="150" Content="Click Me!">
    <Button.Style>
        <Style TargetType="Button">
            <Setter Property="Background" Value="Yellow" />
            <Setter Property="FontSize" Value="14" />
            <Setter Property="FontWeight" Value="Bold" />
        </Style>
    </Button.Style>
</Button>
```

代码片段 StylesAndResources/MainWindow.xaml

直接使用 Button 元素设置 Style 在样式共享方面帮助不大。样式可以放入资源中。在资源中，你可以将样式分配给特定元素，将样式分配给所有类型元素，或为样式使用键。要将样式分配给所有类型元素，请使用 Style 的 TargetType 属性并通过指定 x:Type 标记扩展 (x:Type Button) 将其分配给 Button。要定义需要引用的样式，必须设置 x:Key：

```
<Window.Resources>
    <Style TargetType="{x:Type Button}">
        <Setter Property="Background" Value="LemonChiffon" />
        <Setter Property="FontSize" Value="18" />
    </Style>
    <Style x:Key="ButtonStyle">
        <Setter Property="Button.Background" Value="Red" />
        <Setter Property="Button.Foreground" Value="White" />
        <Setter Property="Button.FontSize" Value="18" />
    </Style>
</Window.Resources>
```

在以下 XAML 代码中，第一个按钮——其元素属性中未定义样式——获得为 Button 类型定义的样式。对于下一个按钮，Style 属性使用 StaticResource 标记扩展 ({StaticResource ButtonStyle}) 设置，而 ButtonStyle 指定了之前定义的样式资源的键值，因此该按钮具有红色背景和白色前景：

```
<Button Width="200" Content="Uses named style"
    Style="{StaticResource ButtonStyle}" Margin="3" />
```
