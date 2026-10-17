
# 深入理解

注意
.NET 编译器会自动创建生成的文件（`.g.cs` 文件），如果不需要，否则你不应操作这些文件的内容。

在编译 XAML 代码后，生成的文件（`.g.cs` 文件）和 .NET 语言代码会被语言编译器（`csc.exe`）编译成程序集。程序集可以是可执行文件（`exe`）或动态链接库（`dll`），并包含 `.xaml` 文件作为资源。当 WPF 应用程序编译完成后，你就可以运行它。你可以通过选择调试->开始调试（`DEBUG->Start Debugging`）选项或按下键盘上的 `F5` 来。这将启动 WPF 应用程序的调试，意味着应用程序被编译并执行。通过调试选项，你可以控制 WPF 应用程序执行的许多方面，例如设置断点、单步进入和逐步执行语句等。调试器允许你修复编译时错误和运行时错误（异常）。

注意
在 WPF 应用程序中，每个窗口（独立 WPF 应用程序）和页面（`XBAMLs`）都有一个 `.xaml` 文件和一个 `.g.cs` 文件。

## 第 8 章：介绍 Windows Presentation Foundation

### 即时解决方案

#### 使用 WPF 窗口

你在本章的较早部分已经了解到，独立 WPF 应用程序拥有承载了应用程序其他元素和控件的窗口。你还了解到，当你创建一个独立 WPF 应用程序时，应用程序会自动包含一个窗口。请注意，WPF 窗口是 `Window` 类的实例。现在，让我们通过以下步骤创建一个名为 `WPFWindows` 的独立 WPF 应用程序：

- 1. 点击开始 -> 所有程序 -> Visual Studio 2012 -> Visual Studio 2012。Visual Studio 2012 IDE 打开。
- 2. 点击启动页上的“新建项目”或选择文件->新建（`FILE -> New`）。出现“新项目”对话框（图 8.26）。
- 3. 从左侧窗格选择已安装->Visual C#->Windows，并从中间窗格选择 WPF 应用程序模板。在文本框中输入一个名称。在本例中，我们输入了 `WPFWindows`（图 8.26）。
- 4. 在位置组合框中为应用程序输入位置。在本例中，我们输入了 `D:\CSharp2012 BlackBook\Chapter 08\Code\`

![](img/17af790174c480761404624aeed9b30b_359_0.png)

- 5. 点击确定按钮。在 Visual Studio 2012 中打开 Windows WPF 应用程序，如图 8.27 所示。

![](img/17af790174c480761404624aeed9b30b_359_1.png)

- 6. 在解决方案管理器中右键点击项目名称并选择添加→窗口（`Add→Window`）。出现“新建项”对话框，如图 8.28 所示。

![](img/17af790174c480761404624aeed9b30b_360_0.png)

图 8.28：添加新建项对话框

- 7. 点击新建项对话框中的添加按钮，向 WPF 应用程序添加名为 `Window1` 的新 WPF 窗口。
- 8. 在 `MainWindow` 的设计视图（`MainWindow.xaml` 文件）中添加五个命名为 `ChangeLocation`、`AutoFit`、`ChangeBorder`、`AnotherWindow` 和 `Exit` 的按钮，并按照代码 8.12 所示设置其属性：

Listing 8.12：在 WPF应用程序中添加按钮的 XML 代码

```xml
<window Class="WpfApp.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Grid" Width="300" Height="300">
  <Grid>
    <Button Height="23" Name="ChangeLocation"
            Click="ChangeLocation_Click"
            VerticalAlignment="Top" Margin="15,20,0,0" />
    <Button Height="23" Name="AutoFit" Click="AutoFit_Click"
            VerticalAlignment="Top" Margin="0,40,0,0" />
    <Button Height="23" Name="ChangeBorder" Click="ChangeBorder_Click"
            VerticalAlignment="Top" Margin="15,60,0,0" />
    <Button Height="23" Name="AnotherWindow" Click="AnotherWindow_Click"
            VerticalAlignment="Top" Margin="15,100,0,0" />
    <Button Height="23" Name="Exit" Click="Exit_Click" Margin="15,180,0,0"
            VerticalAlignment="Top" HorizontalAlignment="Left" />
  </Grid>
</window>
```

在代码 8.12 中，`MainWindow`（默认窗口）的标题被设置为 FirstWindow，`Height` 和 `Width` 属性设置为 300。`ChangeLocation`、`AutoFit`、`ChangeBorder`、`AnotherWindow` 和 `Exit` 按钮的 `Click` 属性被设置为对应按钮 Click 事件的相应处理程序。

- 9. 现在，让我们在后台代码文件（`MainWindow.xaml.cs`）中为五个按钮的 Click 事件设置事件处理程序：

Listing 8.13：设置 MainWindow 的属性。

## 第 8 章：介绍 Windows Presentation Foundation

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Forms;
using System.Windows.Media;
using System.Windows.Shapes;

namespace WPFWindows
{
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }

        private void ChangeLocation_Click(object sender, RoutedEventArgs e)
        {
            // 实现代码
        }

        private void AutoFit_Click(object sender, RoutedEventArgs e)
        {
            // 实现代码
        }

        private void ChangeBorder_Click(object sender, RoutedEventArgs e)
        {
            // 实现代码
        }

        private void AnotherWindow_Click(object sender, RoutedEventArgs e)
        {
            // 实现代码
        }

        private void Exit_Click(object sender, RoutedEventArgs e)
        {
            App.Current.Shutdown();
        }
    }
}
```

### 即时解决方案

在 `AnotherWindow_Click` 方法中，通过 `Hide()` 方法隐藏 `MainWindow`。此外，创建了一个 `newWindow` 实例并使用 `Show()` 方法显示。最后，在 `Exit_Click` 方法中，通过 `Shutdown()` 方法关闭应用程序。

打开 `Window1.xaml` 文件并添加以下代码来设计 UI：

Listing 8.14：为 Window1 添加 XAML 代码

```xml
<Window Class="WPFWindows.Window1"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="SecondWindow" Height="300" Width="300">
  <Grid>
    <Button Margin="0,50,0,90" Name="ShowFirst"
            Click="ShowFirst_Click"
            Content="ShowFirst"/>
  </Grid>
</Window>
```

在代码 8.14 中，`Window1` 的标题为 SecondWindow。你还可以看到名为 `ShowFirst` 的按钮。`Click` 事件绑定到了 `ShowFirst_Click` 方法。

打开 `Window1.xaml` 文件，在 `Window1` 类中添加以下代码段以实现 `ShowFirst_Click` 方法：

```csharp
private void ShowFirst_Click(object sender, RoutedEventArgs e)
{
  MainWindow mainwin = new MainWindow();
  mainwin.WindowState = WindowState.Normal;
  mainwin.Show();
}
```

按下 `F5` 运行 `WPFWindows`。在输出中，你将看到 First 窗口处于最大化状态。点击 `ChangeLocation` 按钮，First 窗口将以正常大小显示，如图 8.29 所示：

![](img/17af790174c480761404624aeed9b30b_362_0.png)

图 8.29：正常大小下的 First

如果你点击 `AutoFit` 按钮，`MainWindow` 将调整大小以适应内容（按钮），如图 8.30 所示：

![](img/17af790174c480761404624aeed9b30b_362_1.png)

图 8.30：自动调整 MainWindow 以适应内容

## 第 8 章：介绍 Windows Presentation Foundation

注意，只有 `MainWindow` 的宽度发生了变化；高度保持不变。

你还可以点击 `ChangeBorder` 按钮为 `MainWindow` 添加边框。当你点击 `AnotherWindow` 按钮时，`SecondWindow` 会出现，如图 8.31 所示：

![](img/17af790174c480761404624aeed9b30b_363_0.png)

图 8.31：SecondWindow

现在，如果你点击 FirstWindow 按钮，`MainWindow` 将再次出现。如果你点击 `MainWindow` 上的 `Exit` 按钮，WPF 应用程序将停止运行并立即关闭。

### XAML 为 Grid 添加行和列

本章的 Grid 部分解释了 `Grid` 元素（或控件）默认添加到独立的 WPF 应用程序和 XAML 中。正如你可能记得的，`Grid` 元素默认有一个单元格，即一行一列。如果你想在垂直方向上增加网格中单元格的数量，需要在 `Grid` 中添加更多行。如果存在多余的行，你也可以删除这些行。同样，为了增加网格水平方向上的单元格数量，需要添加更多列。通过这种方式，每行都可以有多个列。

注意，你在 XAML 中做的更改会立即反映在设计（Design view）中，反之亦然。现在，让我们通过以下步骤创建一个名为 `RowsColumns` 的独立 WPF 应用程序：

- 1. 打开 Visual Studio 2012 并创建一个新的 WPF Application GridRowsColumns。
- 2. 在应用程序的 `MainWindow.xaml` 文件的 `<Grid>` 和 `</Grid>` 标签内添加高亮代码：

```xml
<Grid>
  <RowDefinitions>
    <RowDefinition Height="20"/>
    <RowDefinition Height="50"/>
    <RowDefinition Height="50"/>
    <RowDefinition Height="50"/>
  </RowDefinitions>
</Grid>
```

在前面的代码段中，`Grid RowDefinitions` 元素是 `Grid` 元素的子元素。`Grid.RowDefinitions` 有四个 `RowDefinition` 元素，定义了网格中的四行。第一行的高度为 20 像素，第二行为为 50 像素。第三行和第四行的高度为 50，其中星号 `*` 表示网格中剩余的空间。

- 3. 在 `GridColumns` 应用程序 `<Grid>` 和 `</Grid>` 标签内部使用以下高亮代码向网格添加列：

```xml
<Grid>
  <RowDefinitions>
    <RowDefinition Height="20"/>
    <RowDefinition Height="50"/>
    <RowDefinition Height="50"/>
    <RowDefinition Height="50*"/>
  </RowDefinitions>
  <ColumnDefinitions>
    <ColumnDefinition Width="25"/>
    <ColumnDefinition Width="50"/>
  </ColumnDefinitions>
</Grid>
```

## 立即解决方案

```xml
<ColumnDefinition width="30*"/>
<ColumnDefinition width="50*"/>
<GridDefinitions>
<Grid>
```

在前面的代码段中，`Grid.ColumnDefinitions` 元素是 `Grid` 元素的子元素。`Grid.ColumnDefinitions` 有四个子元素 `ColumnDefinition` 元素，定义了网格中的四列。`ColumnDefinition` 元素的 `Width` 属性用于设置每列的宽度。第一列和第二列的宽度分别为 25 和 50 像素，然而第三列和第四列的宽度将为 30 和 50，其中星号 `*` 表示网格中剩余空间的百分比。

尽管视图立即显示了你通过 XAML 代码添加的行和列，但让我们使用 `Button` 控件或元素让你看得更清楚。

- 4. 在 `<Grid>` 和 `</Grid>` 标签内部添加以下高亮代码来显示行和列：

```xml
<Grid>
<Grid.RowDefinitions>
<RowDefinition Height="20*"/>
<RowDefinition Height="30*"/>
<RowDefinition Height="50*"/>
</Grid.RowDefinitions>
<Grid.ColumnDefinitions>
<ColumnDefinition width="25*"/>
<ColumnDefinition width="50*"/>
<ColumnDefinition width="30*"/>
<ColumnDefinition width="50*"/>
</Grid.ColumnDefinitions>
<Button Name="button1" Grid.Row="0" Grid.Column="0" Grid.RowSpan="2"/>
<Button Name="button2" Content="Yes" Grid.Row="2" Grid.Column="1"/>
<Button Name="button3" Content="No" Grid.Row="2" Grid.Column="2"/>
<Button Name="button4" Content="Cancel" Grid.Row="3" Grid.Column="2" Grid.ColumnSpan="2"/>
</Grid>
```

在高亮代码中，使用了名为 `button1`、`button2`、`button3` 和 `button4` 的四个元素。`button1` 元素通过将 `Grid.Row` 和 `Grid.Column` 属性设置为零，出现在第一行第一列。`Grid.RowSpan` 和 `Grid.Column` 属性指示了 `button1` 所在的行和列。`Grid.RowSpan` 属性被设置为 2，这意味着 `button1` 跨越了两行。同样，`button2` 出现在第三行第二列，`button3` 出现在第三行第四列，`button4` 出现在第四行第三列，如图 8.32 所示。

![](img/17af790174c480761404624aeed9b30b_364_0.png)

图 8.32：Grid 中的行和列

## 第 8 章：介绍 Windows Presentation Foundation
