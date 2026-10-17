
*(注：根据提供的 OCR 片段，XML 内容已经过截断/清理，但保留了结构。)*

# 立即解决方案

6. 重复步骤 5 以为每个科目选择日期。图 14.31 显示了在 `SubjectScheduleApp` 中从 `DatePicker` 控件选择日期后的应用程序输出：

## 创建你自己的日程表

| 学目 | 选择日期 |
| --- | --- |
| 生物学 | 2013年10月2日，星期三 |
| 化学 | 2013年10月4日，星期五 |
| 英语 | 2013年10月3日，星期四 |
| 金融 | 2013年10月7日，星期一 |
| 数学 | 2013年10月12日，星期六 |
| 物理 | 2013年10月15日，星期二 |

图 14.31：`SubjectSchedule` 应用中所有 `DatePicker` 控件中的日期

通过此，我们学会了如何使用 `DatePicker` 控件。接下来，让我们学习如何在 Silverlight 应用中使用 `GridSplitter` 控件。

## 使用 GridSplitter 控件

`GridSplitter` 控件允许 Silverlight 应用的用户重新调整 `Grid` 控件的行和列。执行以下步骤，演示如何使用 Silverlight `GridSplitter` 控件来调整网格的行和列

- 1. 创建一个应用程序列表并将其命名为 `TextImageApp`。列表 14.7 显示了 `TextImageApp` 中 `MainPage.xaml` 文件的代码：

列表 14.7：`MainPage.xaml` 文件的代码

# 第 14 章：使用 Silverlight 5.0 增强 Web 应用

```
Domestic Cat Scientific Name: Felis Catus Genus: Felis

isReadOnly="True" Background="LightBlue"/>

<Image Source="Myla.jpg" Row="2" Grid.Column="1"

Margin="10"/>

<GridSplitter:Name="split1" Height="20" Width="250" Grid.Row="2"

Grid.Column="1" Grid.ColumnSpan="2" HorizontalAlignment="Stretch"

VerticalAlignment="Top" Background="Steel"/>

<GridSplitter:Name="split2" Height="20" Width="250" Grid.Row="1"

Grid.Column="1" Grid.RowSpan="2" HorizontalAlignment="Left"

VerticalAlignment="Stretch" Background="Steel"/>
```

在列表 14 中，你可以使用两个 `GridSplitter` 控件，`split1` 和 `split2`，它们分别被添加到第三行和第二行。第一个 `GridSplitter` `split1` 存在于 `Grid` 控件的第三行，并跨越两列。`split1` 的 `HorizontalAlignment` 属性设置为 `Stretch`，这意味着它通过扩展或收缩来调整行的大小。第二个 `GridSplitter` `split2` 将其 `VerticalAlignment` 属性设置为 `Stretch`，这允许对列进行大小调整。

通过在解决方案资源管理器中选择“添加→现有项 TextTextImage”，将“熊猫”和“我的 Myla.jpg”添加到当前项目文件夹中。

- 2. 按键盘上的 `F5` 键运行 `TextImageAsset` 应用程序。输出出现，如图 14.32 所示：

![](img/17af790174c480761404624aeed9b30b_729_0.png)

- 3. 点击并拖动任何一个 `GridSplitter` 控件。注意行和列会自动调整大小，如图 14.33 所示

![](img/17af790174c480761404624aeed9b30b_730_0.png)

图 14.33：在 `TextImageApplication` 中调整行和列

现在你已经学会了如何使用 `GridSplitter` 控件调整 `Grid` 控件的行和列，让我们让我们讨论 `HyperlinkButton` 控件。

## 使用 HyperlinkButton 控件

`HyperlinkButton` 通过允许在点击事件中导航到 Web 或不同的 Web 应用，将按钮和超链接的功能结合。遵循以下步骤学习如何使用 `HyperlinkButton` 控件：

- 1. 创建一个名为 `HyperlinkButton` 的 Silverlight 应用查看 `HyperlinkButton` 控件。
- 2. 打开 `HyperlinkButton` 应用的 `MainPage.xml` 文件，并添加列表 14:4 所示的代码。

列表 14:4：`MainPage.xml` 的代码

```
<userControl x:Class="HyperlinkButtonDemo.MainPage"

xmlns="http://schemas.microsoft.com/winfx/2006/presentation"

xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"

xmlns:d="http://schemas.microsoft.com/expression/blend/2008"

xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"

mc:Ignorable="d"

d:Height="300" d:Width="500">

<Grid x:Name="MainGrid" BorderBrush="Black" Height="300" Width="500">

<HyperlinkButton x:Name="HyperlinkButton" Background="yellow" Height="35" Width="175"

Foreground="Red" Margin="0,0,0" Content="Microsoft site" 

ToolTip.ToolTip="Find Everything About Here"

NavigateUrl="http://www.microsoft.com" TargetName="_blank"/>

<HyperlinkButton Background="yellow" Height="35" Width="175"

Margin="0,20,0" Content="Getting started with silverlight" />

</Grid>
```

# 第 14 章：使用 Silverlight 5.0 增强 Web 应用

```
Foreground="Red" NavigateUri="http://silverlight.net/getstarted/"

TargetName="_blank" Tooltip.Tooltip="Find everything about Silverlight"

<Hyperlink background="yellow" Height="175" Margin="0,50,0,0"

Content="Silverlight" Foreground="Red" NavigateUri="http://silverlight.net/learn/tutorials.aspx"

TargetName="_blank" Tooltip.Tooltip="Find easy-to-learn lessons on Silverlight"/>

<Grid>
```

看到三个 `Hyperlink` 控件用于导航到 `http://www.microsoft.com/`、`http://silverlight.net/getstarted/` 和 `http://silverlight.net/tutorials.aspx` 页面。`TargetName` 属性设置为 `_blank`，允许在新浏览器窗口中打开导航到的 Web 页面。

- 3. 运行 `HyperlinkButtonDemo`。输出出现，如图 14:34 所示：

![](img/17af790174c480761404624aeed9b30b_731_0.png)

- 4. 点击三个 `Hyperlink` 控件之一。相应的 Web 页面在新浏览器窗口或当前浏览器的标签页中打开，如图 14:35 所示：

![](img/17af790174c480761404624aeed9b30b_731_1.png)

## 立即解决方案

接下来，让我们讨论 Silverlight 5.0 的 `MediaElement` 控件。

## 使用 MediaElement 控件

周知，`MediaElement` 控件允许你在 Silverlight 应用中托管音频或视频。执行以下步骤学习如何使用 `MediaElement` 控件。

- 1. 创建一个托管在单页中的 `MediaPlayer`。在此，你需要在当前项目文件夹中添加想要播放的媒体。要实现此，你需要使用添加项框。添加媒体文件后，在解决方案资源管理器中选择它并按 `F4` 键编辑。出现属性窗口（图 14.36）。
- 2. 在属性窗口中选择“输出到”属性，将“输出目录”的默认值更改为“从复制”（`Copy never`），如图 14.36 所示。

![](img/17af790174c480761404624aeed9b30b_732_0.png)

图 14.36：`LiveMedia.wmv` 的属性窗口

如果媒体文件是新的，“从复制”选项会将媒体文件复制到当前项目文件夹中。

- 3. 打开应用程序 `MediaPlayer` 的 `MainPage.xaml` 文件，并输入使用 `MediaElement` 控件的代码。列表 14.9 显示了 `MediaPlayer` 应用中 `MainPage.xaml` 文件的代码。

列表 14.9：`MainPage.xaml` 的代码

```
<UserControl x:Class="MyMediaPlayer:xaml.MainPage"

      xmlns="http://schemas.microsoft.com/winfx/2006/presentation"

      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"

      xmlns:d="http://schemas.microsoft.com/expression/blend/2008"

      xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"

      mc:Ignorable="d"

      d:DesignHeight="600" d:DesignWidth="600">

  <Grid x:Name="Grid" Background="Blue" DataContext=
```

```
<TextBlock x:Name="mediaFile" Height="50" width="200" Foreground="Yellow"

Text="Media File: Margin="0,565,0,0" FontWeight="Bold"/>

<TextBlock x:Name="duration" Height="50" width="200" Foreground="Yellow"

Text="Total Time: Margin="400,565,0,0" FontWeight="Bold"/>

</UserControl>
```

在 L19 中 `MediaElement` 托管视频文件（`Wildlife.wmv`）。`MediaElement` 的 `Stretch` 属性设置为 `Uniform`，这意味着在不改变纵横比的情况下填充控件。如果控件比视频小，视频将被裁剪以适应它。`MediaElement` 的 `Volume` 属性设置为 `0.75`，这意味着媒体播放时的音量为最大值的 75%。`MediaElement` 的 `AutoPlay` 属性设置为 `False`，这意味着媒体加载后不会自动播放。你需要手动启动播放。此外，`MediaElement` 的 `MediaOpened` 和 `MediaFailed` 事件关联了相应的事件处理程序。

- 4. 打开 `MediaPlayer` 应用的 `MainPage.xml` 文件的代码文件，并输入列表 14.10 所示的代码：

## 立即解决方案

```csharp
mediaEle.Pause();

play.Content = "Resume";

public void mediastop(object sender, RoutedEventArgs e)

{

    mediaEle.Stop();

    play.Content = "Play";

}
```

在列表 14.10 中，当 `MediaElement` 控件中的媒体打开时，`mediaOpen()` 方法会执行。该方法使用 `MediaElement` 控件的 `Source` 和 `NaturalDuration` 在应用程序中显示媒体文件的名称和长度（时间）。点击播放按钮时，`mediaPlay()` 方法会执行。同样，当你调用应用程序中的 `pause()` 和 `stop()` 按钮时，会在 `mediaElement.mediastop()` 方法中调用 `MediaElement` 控件的 `Pause()` 和 `Stop()` 方法。如果在打开或播放媒体时发生任何错误，`mediaError()` 方法会执行。

- 5. 按键盘上的 `F5` 键运行 `MyMediaPlayer` 应用程序。输出如图 14.37 所示：

![](img/17af790174c480761404624aeed9b3b_734_0.png)

图 14.37：`MyMediaPlayer` 程序的输出

你可以点击应用程序中的播放、暂停和停止按钮来分别暂停和停止媒体文件。

> 注意
> 视频 `Wildlife.wmv` 通过在解决方案资源管理器中选择“添加→现有项→MyMediaPlayer” 添加到当前项目文件夹中。

接下来，让我们学习 `Popup` 控件。

## 使用 Popup 控件

在某些情况下，你可能想要提供额外信息或显示帮助信息，例如控件或 UI 元素。在这种情况下，你可以利用 Silverlight 5.0 提供的 `Popup` 控件。`Popup` 在其他控件上方的边界区域内显示信息。该边界区域可以是作为 `Popup` 控件子元素的任何 UI 控件。按照以下步骤使用 `Popup` 控件：

- 1. 创建一个名为 `PopupHelpApp` 的 Silverlight 应用程序（托管在单个 HTML 页面中）。列表 14.11 显示了 `PopupHelpApp` 应用程序的 `MainPage.xaml` 文件的代码：

```xml
Listing 14.11: MainPage.xaml 的代码

userControl x:Class="PopupHelpApp.MainPage"

xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation/sdk"

xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml/presentation"

xmlns:local="http://schemas.microsoft.com/winfx/2006/xaml"
```

## 使用 TabControl

在本章的“数据”部分中，你已经学习了 `TabControl` 可以将多个控件分组在一个或多个标签页（tabs）中。每个标签页占据相同的 UI 区域，因此可以实现应用程序 UI 的最大利用。按照以下步骤使用 `TabControl` 控件：

- 1. 创建一个名为 `StudentRecordsApp` 的 Sliver ，并将其托管在 `.aspx` 页面中，以查看如何使用 `TabControl` 控件；
- 2. 在 `Main.xaml` 文件中添加 `TabControl`。14.13 显示了 `StudentRecords` 应用程序 `Main.xaml` 文件的代码：

```xml
14.13: Code for the Main.xaml
```
