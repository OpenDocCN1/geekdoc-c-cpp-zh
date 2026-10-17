
`VerticalAlignment="Bottom"` />

</Grid>

</Window>

```

清单 10.17 向窗口添加了一个 Frame 控件，该控件显示在代码隐藏文件中指定的 Web 页面。

现在，将代码添加到 `MainWindow.xaml.cs` 文件中，如清单 10.18 所示：

### 清单 10.18：在 `MainWindow.xaml.cs` 文件中实现 `NavigationWindow` 和 `Frame` 控件

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;
namespace Navigating_Window
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }
        private void button1_Click(object sender, RoutedEventArgs e)
        {
            //You need to change the uri path in this according to the HTML file
            //saved on your computer.
            if ((Boolean)List.IsChecked)
                myFrame.Navigate(new System.Uri("file:///D:/Black Books/DefinitionList.html"));
            else if ((Boolean)Details.IsChecked)
                myFrame.Navigate(new System.Uri("file:///D:/Black Books/TableColor.html"));
        }
    }
}
```

清单 10.18 添加了 `NavigationWindow` 控件。通过按 `F5` 键运行应用程序，`MainWindow` 窗口出现，其中包含两个 `CheckBox` 控件和一个 `Button` 控件。选择 `Details` 复选框并单击 `Click` 按钮（见图 10.51），Web 页面将在窗口内的框架中显示，如图 10.51 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_478_0.png)

图 10.51：显示 `NavigationWindow` 和 `Frame` 控件

## 使用资源、样式和模板

在章节的 In Depth 部分，你学习了关于资源、样式和模板的知识。在 Immediate Solutions 部分，你将通过一个应用程序学习这些概念的实际实现。

## 从代码中访问资源

现在让我们学习如何在 WPF 应用程序中从代码访问资源。创建一个名为 `AccessingResources` 的 WPF 应用程序（可在 CD 上获得）并将清单 10.19 中显示的代码添加到 `MainWindow.xaml` 文件中。

### 清单 10.19：显示在 `MainWindow.xaml` 文件中访问资源的代码

```
```xml
<Window x:Class="AccessingResources.MainWindow"
 xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
 xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
 Title="MainWindow" Height="350" Width="525">
 <Grid>
 <StackPanel Name="MyStackPanel">
 <StackPanel.Resources>
 <LinearGradientBrush x:Key="MyBrush" StartPoint="0.5,0" EndPoint="0.5,1">
 <GradientStop Offset="0.0" Color="LightPink"/>
 <GradientStop Offset="0.2" Color="Pink"/>
 <GradientStop Offset="0.7" Color="Darkorchid"/>
 </LinearGradientBrush>
 </StackPanel.Resources>
 </StackPanel>
 </StackPanel>
 <Button Name="Button1" Width="250" Height="100" Click="Button1_Click" />
 </Grid>
</Window>
```
```

前面的代码向窗口添加了一个 `Button` 控件。要通过代码访问资源，你需要将清单 10.20 中给出的代码添加到 `MainWindow.xaml.cs` 文件中。为此，将清单 10.20 中给出的代码添加到 `MainWindow.xaml.cs` 文件中。

### 清单 10.20：从代码访问资源

```
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;
using System.Windows.Controls;
namespace AccessingResources
{
 // <summary>
 // Interaction logic for MainWindow.xaml
 // </summary>
 public partial class MainWindow : Window
 {
 public MainWindow()
 {
 InitializeComponent();
 }
 private void Button1_Click(object sender, RoutedEventArgs e)
 {
 Control button = sender as Control;
 button.Background = button.FindResource("MyBrush") as Brush;
 }
 }
}
```
```

当你按 `F5` 键运行代码时，可以看到一个 `Button` 控件已添加到窗口中。当你单击 `Button` 控件时，控件的颜色会更改为你在 XAML 代码中指定的颜色。清单 10.19 和清单 10.20 中的代码输出如图所示 10.52：

![](img/e073a4882197be4ab61103cbe0bcb394_480_0.png)

图 10.52：从代码访问资源

> NOTE
> 如果 `FindResource` 方法找不到资源键，将抛出异常。如果不确定资源的可用性，可以使用 `TryFindResource` 方法。此方法在未找到资源时返回 null。

## 使用动态资源

如本章 In Depth 部分所述，资源有两种类型：静态和动态。两者之间的主要区别在于静态资源在编译时加载，而动态资源在运行时加载。让我们在 WPF 应用程序中使用动态资源。创建一个名为 `DynamicResources` 的 WPF 应用程序（可在 CD 上获得）并将以下代码添加到 `MainWindow.xaml` 文件中，如清单 10.21 所示：

### 清单 10.21：显示实现动态资源的代码

```
<Window x:Class="DynamicResources.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="MainWindow" Height="350" Width="525">
    <Grid>
        <StackPanel>
            <StackPanel.Resources>
                <SolidColorBrush x:Key="myBrush" Color="Red"/>
            </StackPanel.Resources>
            <Label Foreground="{DynamicResource myBrush}">Hello</Label>
            <Button Background="{DynamicResource myBrush}">DynamicResource</Button>
            <Button Background="{DynamicResource {x:Static SystemColors.ControlBrushKey}}">MyButton
            </Button>
        </StackPanel>
    </Grid>
</Window>
```

清单 10.21 向窗口添加了一个 `Label` 控件和两个 `Button` 控件。你可以看到对一个 `SolidColorBrush` 的引用被创建并传递给 `Label` 控件和其中一个 `Button` 控件。第二个 `Button` 控件采用默认系统颜色。当你将鼠标指针移到引用了 `SolidColorBrush` 颜色的 `Button` 控件上时，该 `Button` 控件也会采用系统颜色。你可以通过按 `F5` 键运行应用程序。清单 10.21 的输出如图所示 10.53：

![](img/e073a4882197be4ab61103cbe0bcb394_480_1.png)

图 10.53：使用动态资源

## 通过资源设置样式

资源在 WPF 中设置样式很有帮助，因为资源使样式能够在应用程序中重用。如果你将样式声明在应用程序的根元素中，该样式可以在应用程序中的任何位置使用。如果你将样式声明在应用程序的一个 XAML 文件中，则该样式只能在该 XAML 文件中使用。让我们学习如何在 WPF 应用程序中通过资源设置样式。创建一个名为 `SettingStyle_Resources` 的 WPF 应用程序（可在 CD 上获得）并将代码添加到 `MainWindow.xaml` 文件中，如清单 10.22 所示：

### 清单 10.22：显示设置样式的代码

```
<Window x:Class="SettingStyle_Resources.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="MainWindow" Height="350" Width="525">
<Grid>
<StackPanel x:Name="ButtonPanel" Background="PeachPuff">
<StackPanel.Resources>
<Style x:Key="MyButton">
<Setter Property="Button.Background" Value="Pink"/>
<Setter Property="Button.Foreground" Value="Blue"/>
<Setter Property="Button.MinWidth" Value="50"/>
<Setter Property="Button.MinHeight" Value="50"/>
<Setter Property="Button.Margin" Value="12"/>
</Style>
</StackPanel.Resources>
<Button Style="{StaticResource MyButton}">Button1</Button>
<Button Style="{StaticResource MyButton}">Button2</Button>
<Button Style="{StaticResource MyButton}">Button3</Button>
</StackPanel>
</Grid>
</Window>
```

在清单 10.22 中，有三个 `Button` 控件，它们被添加到 `StackPanel` 控件内部。所有 `Button` 控件具有相同的样式。`Button` 控件的样式通常通过资源定义。你只需在所有 `Button` 控件中引用该样式即可。现在，通过按 `F5` 键运行应用程序。图 10.54 显示了清单 10.22 的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_481_0.png)

图 10.54：控件上应用的样式

## 扩展现有样式

有些情况下，你希望两个控件共享相同的样式。你可以通过创建基于第一个样式的新样式来实现这一点。让我们学习如何在 WPF 应用程序中执行此操作。创建一个名为 `ExtendingStyle` 的应用程序（可在 CD 上获得）并将代码添加到 `MainWindow.xaml` 文件中，如清单 10.23 所示：

**清单 10.23：显示扩展现有样式的代码**

```xml
<Window x:Class="ExtendingStyle.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="MainWindow" Height="350" Width="525">
    <Window.Resources>
        <Style x:Key="BigFontButtonStyle">
            <Setter Property="Control.FontFamily" Value="Times New Roman" />
            <Setter Property="Control.FontSize" Value="18" />
            <Setter Property="Control.FontWeight" Value="Bold" />
        </Style>
        <Style x:Key="EmphasizedBigFontButtonStyle"
               BasedOn="{StaticResource BigFontButtonStyle}">
            <Setter Property="Control.Foreground" Value="White" />
            <Setter Property="Control.Background" Value="DarkBlue" />
        </Style>
    </Window.Resources>
    <Grid>
        <Button Height="41" Margin="26,24,39,0" Name="button1" VerticalAlignment="Top"
                Style="{StaticResource BigFontButtonStyle}">Using BigFontStyle</Button>
        <Button Height="35" Margin="26,94,39,0" Name="button2"
                VerticalAlignment="Top">Normal Button</Button>
        <Button Margin="0,0,0,69" Name="button3" Height="39" VerticalAlignment="Bottom"
                Style="{StaticResource EmphasizedBigFontButtonStyle}">Using EmphasizedBigFontButtonStyle</Button>
    </Grid>
</Window>
```
