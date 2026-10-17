
        `errorWindow.Show()`

    End Sub

End Class

```
来自 MainPage.xaml.vb 的代码片段
```

你可能已经注意到，这与你学到的 WPF 非常相似。总体思路相同。你可以在 XAML 中添加控件，然后修改控件的代码。这种 UI 与代码的分离有助于创建管理应用程序设计的简单架构。当同时使用 Visual Studio 和 Microsoft Expression Blend 时，这种分离非常有用。

### 控件

与 Windows 窗体开发一样，Silverlight 提供了一套大型控件集合，为你开发丰富的界面提供了大量选择。此外，你会发现 Silverlight 开发几乎与 WPF 开发相同，因为两者都使用 XAML 作为布局方法。

#### 布局管理

在开发 Silverlight 应用程序时，你有几种不同的选项可以将控件放置在主设计表面上：`Grid`、`StackPanel`、`Canvas`、`ScrollViewer` 和 `Border`。这些布局各自有一套功能，反映了使用时机；你并不局限于一种布局控件，因为你可以将它们嵌套在彼此内部以创建各种布局选项。

#### Grid

默认情况下，创建任何 Silverlight 控件时，你的根布局控件将是一个 `Grid`。`Grid` 控件提供了最大的灵活性，支持行和列等选项。如果你熟悉 HTML 表格，你会觉得这个选项很熟悉。`Grid` 控件使你能够使用 `Grid.RowDefinitions` 和 `Grid.ColumnDefinitions` 属性定义行和列。在行定义中，你可以设置两个主要选项，`Height` 和 `MinHeight`，但大多数时候你只需设置 `Height`。同样，在 `ColumnDefinitions` 中，你可以选择设置 `Width` 和 `MinWidth` 属性。以下示例设置了一个包含四个高度为 50 像素的行，以及四个宽度为 100 像素的列的网格：

```
<UserControl x:Class="SilverlightApplication1.SilverlightControl1"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    d:DesignHeight="300" d:DesignWidth="400">
    <Grid x:Name="LayoutRoot" Background="White">
        <Grid.RowDefinitions>
            <RowDefinition Height="50" />
            <RowDefinition Height="50" />
            <RowDefinition Height="50" />
            <RowDefinition Height="50" />
        </Grid.RowDefinitions>
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="100" />
            <ColumnDefinition Width="100" />
            <ColumnDefinition Width="100" />
            <ColumnDefinition Width="100" />
        </Grid.ColumnDefinitions>
    </Grid>
</UserControl>
```

来自 `SilverlightControl1.xaml` 的代码片段

图 19-5 显示了你在设计表面上会看到的内容。

![](img/d99870e80390742f93963da7be0b2e61_695_0.png)

图 19-5

```
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d"
d:DesignHeight="300" d:DesignWidth="400">
<Grid x:Name="LayoutRoot" Background="White">
    <Grid.RowDefinitions>
        <RowDefinition Height="50" />
        <RowDefinition Height="50" />
        <RowDefinition Height="50" />
        <RowDefinition Height="50" />
    </Grid.RowDefinitions>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="100" />
        <ColumnDefinition Width="100" />
        <ColumnDefinition Width="100" />
        <ColumnDefinition Width="100" />
    </Grid.ColumnDefinitions>
<Button Content="Button" Grid.Column="2" Grid.Row="1"
    Grid.ColumnSpan="2" Grid.RowSpan="2" />
</Grid>
</UserControl>
```

Code snippet from `SilverlightControl1.xaml`

`Grid` 控件还提供按比例的尺寸设置，因此您可以按比例设置网格的行和列。要启用按比例的尺寸设置，您只需将 `Height` 或 `Width` 设置为类似 `2*` 的值，这指定给定列应为设置为 `1*` 的其他列的两倍大小。例如，您可以像这样定义网格的行和列：

```
<UserControl x:Class="SilverlightApplication1.SilverlightControl1"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d"
d:DesignHeight="300" d:DesignWidth="400">
    <Grid x:Name="LayoutRoot" Background="White">
        <Grid.RowDefinitions>
            <RowDefinition Height="1*" />
            <RowDefinition Height="1*" />
            <RowDefinition Height="2*" />
            <RowDefinition Height="2*" />
        </Grid.RowDefinitions>
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="1*" />
            <ColumnDefinition Width="2*" />
            <ColumnDefinition Width="2*" />
            <ColumnDefinition Width="1*" />
        </Grid.ColumnDefinitions>
        <Button Content="Button" Grid.Column="2" Grid.Row="1"
            Grid.ColumnSpan="2" Grid.RowSpan="2" />
    </Grid>
</UserControl>
```

Code snippet from `SilverlightControl1.xaml`

前面的代码将导致布局看起来像图 19-7 所示。

![](img/d99870e80390742f93963da7be0b2e61_698_0.png)

### FIGURE 19-7

正如您所见，`Grid` 控件具有强大的功能；但它不仅仅局限于列和行结构。`Grid` 控件可以提供的一项功能是其他布局控件无法提供的锚定。正如您在第 15 章中所见，锚定对于放置可能被调整大小的用户控件上的控件非常有用。例如，如果您想在网格中心放置一个按钮，您可以像这样定义它：

```
<UserControl x:Class="SilverlightApplication1.SilverlightControl1"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    d:DesignHeight="300" d:DesignWidth="400">
    <Grid x:Name="LayoutRoot" Background="White">
        <Button Content="Button" Width="100" Height="30" HorizontalAlignment="Center"
            VerticalAlignment="Center" />
    </Grid>
</UserControl>
```

Code snippet from `SilverlightControl1.xaml`

一旦将按钮居中，您可以将 `HorizontalAlignment` 选项设置为 `Center`、`Left`、`Right` 或 `Stretch`；并且可以将 `VerticalAlignment` 选项设置为 `Center`、`Top`、`Bottom` 或 `Stretch`。这将使您的按钮相对于 `Grid` 控件放置。这对于将控件放置在右下角非常有用，但有时您可能不希望它直接位于底部并完全靠右。这时边距就派上用场了。例如，如果您想将按钮放置在右下角并从底部和右侧偏移 12 像素，您可以像这样定义它：

```
<UserControl x:Class="SilverlightApplication1.SilverlightControl1"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    d:DesignHeight="300" d:DesignWidth="400">
    <Grid x:Name="LayoutRoot" Background="White">
```

```
<Button Content="Button" Width="100" Height="30" HorizontalAlignment="Right" VerticalAlignment="Bottom" Margin="0,0,12,12" />
</Grid>
</UserControl>
```

Code snippet from `SilverlightControl1.xaml`

从您所看到的 `Grid` 控件的功能来看，应该很清楚它可以适应大多数情况。然而，虽然它可能是使用最广泛的布局控件，但它并不是唯一一个，也并不适合每种情况。

### StackPanel

`Grid` 的一个经常被忽视的方面是它没有提供放置实际堆叠控件的优化方式。`StackPanel` 控件最常用于想要以行或列的方式将项目并排或上下排列时。与 `Grid` 不同，`StackPanel` 不需要定义行和列；它只需要其 `Orientation` 值被设置。`Orientation` 值可以设置为 `Horizontal` 或 `Vertical`。

您可能会使用 `StackPanel` 来定义诸如菜单之类的元素，在其中放置多个按钮，如以下示例所示：

```
<UserControl x:Class="SilverlightApplication1.SilverlightControl1"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d"
d:DesignHeight="300" d:DesignWidth="400">
<StackPanel x:Name="LayoutRoot" Background="White">
<Button Content="Menu Item 1" Width="100" Height="30" Margin="5"/>
<Button Content="Menu Item 1" Width="100" Height="30" Margin="5"/>
<Button Content="Menu Item 1" Width="100" Height="30" Margin="5"/>
<Button Content="Menu Item 1" Width="100" Height="30" Margin="5"/>
</StackPanel>
</UserControl>
```

Code snippet from `SilverlightControl1.xaml`

这将创建一个堆叠面板，其中菜单项堆叠在彼此之上。或者，您也可以通过设置 `Orientation` 属性使菜单项并排堆叠，如以下示例所示：

```
<UserControl x:Class="SilverlightApplication1.SilverlightControl1"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d"
d:DesignHeight="300" d:DesignWidth="400">
<StackPanel x:Name="LayoutRoot" Background="White" Orientation="Horizontal">
<Button Content="Menu Item 1" Width="100" Height="30" Margin="5"/>
<Button Content="Menu Item 1" Width="100" Height="30" Margin="5"/>
<Button Content="Menu Item 1" Width="100" Height="30" Margin="5"/>
<Button Content="Menu Item 1" Width="100" Height="30" Margin="5"/>
</StackPanel>
</UserControl>
```
