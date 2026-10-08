
# 第 2 章：使用 WPF 控件、资源、样式、模板和命令

在 WPF 中，你可以使用 `Frame` 控件导航到网页。你可以向 WPF 应用程序添加 `Frame` 控件并在 `Frame` 中调用网页。让我们向 WPF 应用程序添加 `Frame` 控件。为此，请创建一个名为 `Navigating_Window` 的 WPF 应用程序，并将列表 9.17 所示的代码添加到 `MainWindow.xaml`。

## 列表 9.17：在 MainWindow.xaml 文件中实现 Frame

```xml
<Window x:Class="Navigating_Window.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="Navigating_Window">
    <Grid>
        <Frame Name="myFrame" />
        <CheckBox Name="chkWeb" Content="Web" />
        <CheckBox Name="chkDetails" Content="Details" />
    </Grid>
</Window>
```

## 列表 9.18：在窗口中添加 Frame，并在代码显示网页

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Media;
using System.Windows.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;

{
    /// <summary>
    /// MainWindow.xaml 的交互逻辑
    /// </summary>
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }
        private void button1_Click(object sender, RoutedEventArgs e)
        {
            // 你需要根据电脑上保存的 HTML 更改此处的
            if (chkWeb.Checked)
                myFrame.Navigate(new Uri("http://www.google.com"));
            else if (chkDetails.Checked)
                myFrame.Navigate(new Uri("http://www.yahoo.com"));
        }
    }
}
```

按 `F5` 键运行应用程序，`MainWindow` 窗口带有 `CheckBox` 控件。选择 `Details` 复选框并点击按钮（见图 9.42），窗口内的 `frame` 中将显示网页，如图 9.42 所示：

![](img/17af790174c480761404624aeed9b30b_438_0.png) （此处为示例占位符）

# 使用资源、样式和模板

在章节的深度部分，你将学习资源、样式和模板。在直接解决方案部分，你将通过应用程序学习这些概念的实际实现。

## 代码中的资源

现在让我们学习如何在 WPF 应用程序中从代码访问资源。创建一个名为 `AccessingResources` 的 WPF 应用程序，并将列表 9.19 所示的代码添加到 `MainWindow.xaml` 文件中：

### 列表 9.19：在 MainWindow.xaml 中访问资源的代码

```xml
<window x:Class="AccessingResources.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
title="Accessing Resources" Height="350" width="525">
<Grid>
<StackPanel Name="MyTextBlock">
<LinearGradientBrush x:Key="Brush" StartPoint="0.5,0" Endpoint="0.5,1">
<GradientStop Offset="0.0" Color="Pink"/>
<GradientStop Offset="0.7" Color="Darkorchid"/>
</LinearGradientBrush>
</StackPanel>
<Resources>
</StackPanel>
<Button Name="Button" Width="250" Height="100" Click="Button_Click" />
</StackPanel>
</Grid>
</window>
```

# 第 9 章：使用 WPF 4.5 控件、资源、样式、模板和命令

```csharp
using System.windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;
namespace AccessingResources
{
    /// <summary>
    /// MainWindow.xaml 的交互逻辑
    /// </summary>
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }
        private void Button1_Click(object sender, RoutedEventArgs e)
        {
            Control button = sender as Control;
            button.Background = button.FindResource("Brush") as Brush;
        }
    }
}
```

当您按下 `F5` 键运行代码时

![](img/17af790174c480761404624aeed9b30b_439_0.png)

图 9.43：从代码访问资源

> 注意：如果 `FindResource` 方法没有找到资源键，则会抛出异常。如果您不确定资源是否可用，可以使用 `TryFind` 方法。如果未找到资源，该方法将返回 `null`。

# 使用动态资源

正如在本章的深入探讨部分所解释的资源有两种类型：静态和动态。两者之间的主要区别是，静态资源在编译时加载，而动态资源在运行时加载。让我们在 WPF 应用中使用动态资源。一个名为 `DynamicResources` 的 WPF 应用使用以下代码在 `MainWindow.xaml` 中实现动态资源，如列表 9.21 所示：

### 列表 9.21：使用动态资源的代码。MainWindow

```xml
<Window x:class="DynamicResources.MainWindow"
      xmlns="http://schemas.microsoft.com/winfx/2006/presentation"
      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
      Title="DynamicResources" Height="350" width="525">
<StackPanel>
    <StackPanel.Resources>
        <SolidColorBrush x:Key="MyBrush" Color="red"/>
    </StackPanel.Resources>
    <Label Foreground="{DynamicResource myBrush}">Hello</Label>
    <Button Background="{DynamicResource x:Static SystemColors.ControlBrush}" Content="MyButton"/>
</StackPanel>
</Window>
```

# 立即解决方案

列表 9.21 在窗口中添加了一个 `Label` 控件和两个 `Button` 控件。可以看到创建了一个单一的 `SolidColorBrush` 引用并传递给 `Label` 控件其中一个 `Button` 控件。第二个 `Button` 控件采用默认系统颜色。当您将鼠标移动到具有 `SolidColorBrush` 中引用颜色的 `Button` 控件上时，该按钮控件也会采用系统颜色。您可以通过按下 `F5` 键运行应用程序。列表 9.21 出现，如图 9.44 所示：

![](img/17af790174c480761404624aeed9b30b_440_0.png)

图 9.44：使用动态资源

# 通过资源设置样式

资源对于设置 WPF 资源非常有帮助，使样式可以在应用程序中被复用。如果您在应用程序的根元素中声明样式，则该样式可以在应用程序的任何地方使用。如果您在应用程序的某个 XAML 文件中声明样式，则该样式只能在相应的 XAML 文件中使用。创建一个名为 `SettingStyles through resources` 的 WPF 应用，并将代码添加到 `MainWindow.xaml` 文件中，如列表 9.22 所示：

### 列表 9.22：设置样式的代码

```xml
<Window class="SettingStyles"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
      Title="SettingStyles" Height="330" width="525">
<Grid>
  <StackPanel Name="MainPanel" Background="PeachPuff">
  <StackPanel.Resources>
  <Style x:Key="MyButton">
      <Setter Property="Button.Background" Value="Pink"/>
      <Setter Property="Button.Foreground" Value="Blue"/>
      <Setter Property="Button.MinWidth" Value="50"/>
      <Setter Property="Button.MinHeight" Value="50"/>
      <Setter Property="Button.Margin" Value="12"/>
    </Style>
  </StackPanel.Resources>
  <Button Style="StaticResource MyButton">Button1</Button>
  <Button Style="StaticResource MyButton">Button2</Button>
  <Button Style="StaticResource MyButton">Button3</Button>
  </StackPanel>
</Grid>
</Window>
```

在列表 9.22 中，有三个 `Button` 控件被添加到 `StackPanel` 控件内部。所有的 `Button` 控件都具有相同的样式。按钮的样式通常通过资源定义。您只需要在所有的 `Button` 控件中引用该样式。现在，按下 `F5` 键运行应用程序。

图 9.45 显示了列表 9.22 的输出：

![](img/17af790174c480761404624aeed9b30b_440_1.png)

图 9.45：应用到控件的样式

# 第 9 章：使用 WPF 4.5 控件、样式、模板和命令

# 扩展样式

在某些情况下，您希望两个控件共享相同的样式。可以通过创建一个基于第一个样式的新样式来实现。创建一个名为 `ExistingStyle` 的应用程序，并将代码添加到 `MainWindow.xaml` 文件中，如列表 9.23 所示：

### 列表 9.23：扩展样式的代码

```xml
<Window x:Class="ExistingStyle.MainWindow"
      xmlns="http://schemas.microsoft.com/winfx/2006/presentation"
      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
      Title="ExistingStyle" Height="320" width="525">
  <Window.Resources>
    <Style x:Key="EmphasizedButtonStyle" TargetType="Button">
      <Setter Property="Control.FontFamily" Value="Times New Roman" />
      <Setter Property="Control.FontSize" Value="18" />
    </Style>
    <Style x:Key="NormalButtonStyle" BaseOn="{StaticResource EmphasizedButtonStyle}">
      <Setter Property="Control.Foreground" Value="white"/>
      <Setter Property="Control.Background" Value="DarkBlue"/>
      <Setter Property="Control.FontWeight" Value="Bold"/>
    </Style>
  </Window.Resources>
  <Grid>
    <Button Style="{StaticResource NormalButtonStyle}">Button</Button>
    <Button Style="{StaticResource NormalButtonStyle}">Button</Button>
    <Button Style="{StaticResource NormalButtonStyle}">Button</Button>
  </Grid>
</Window>
```

在列表 9.23 中，有三个 `Button` 控件被添加到 `StackPanel` 控件内部。所有的 `Button` 控件都具有相同的样式。按钮的样式通常通过资源定义。第二个样式 `NormalButtonStyle` 使用 `BaseOn` 属性扩展了第一个样式 `EmphasizedButtonStyle`。您可以通过按下 `F5` 键运行应用程序。

图 9.46 显示了扩展样式的输出：

![](img/17af790174c480761404624aeed9b30b_441_0.png)

图 9.46：扩展样式

# 使用 DataTemplate 更改外观

在 WPF 中，您使用 `DataTemplate` 来更改数据类型的外观。这是通过使用 `DataTemplate` 的 `DataType` 属性实现的。例如，可能存在一种需要一个模板同时显示布尔值和字符串值的情况。`DataType` 属性在这种场景下非常有帮助。让我们在应用程序中使用 `DataTemplate`。如列表 9.24 所示：

### 列表 9.24：使用 DataTemplate
