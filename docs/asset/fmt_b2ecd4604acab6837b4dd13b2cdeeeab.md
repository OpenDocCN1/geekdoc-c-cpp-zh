
在清单 17.7 中，你可以看到在第三行和第二行添加了两个 `GridSplitter` 控件，分别为 `split1` 和 `split2`。第一个 `GridSplitter` 控件 `split1` 存在于 `Grid` 控件的第三行并跨越两列。`split1` 的 `HorizontalAlignment` 属性被设置为 `Stretch`，这意味着它通过扩展或收缩其内容来调整行的大小。第二个 `GridSplitter` 控件 `split2` 的 `VerticalAlignment` 属性被设置为 `Stretch`，这使得列可以被调整大小。

NOTE

> `Baby Panda.jpg` 和 `My Myla.jpg` 图像是通过在解决方案资源管理器中选择 `TextImageAppCS`→Add→Existing Item 添加到当前项目文件夹中的。

- 2. 按键盘上的 `F5` 键运行 `TextImageAppCS` 应用程序。输出显示如下，如图 17.32 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_916_0.png)

图 17.32：`TextImageAppCS` 应用程序的输出

- 3. 点击并拖动任一 `GridSplitter` 控件。注意行和列会自动调整大小，如图 17.33 所示：

```
</Grid>

</UserControl>
```

在清单 17.8 中，你可以看到使用了三个 `HyperlinkButton` 控件来导航到 `http://www.microsoft.com/`、`http://silverlight.net/getstarted/` 和 `http://silverlight.net/learn/tutorials.aspx` 网页。`TargetName` 属性被设置为 `_blank`，这意味着用户被导航到的网页将在新的空白浏览器窗口中打开。

- 3. 运行 `HyperlinkButtonDemoAppCS` 应用程序。输出显示如下，如图 17.34 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_918_0.png)

## 图 17.34：点击 `HyperlinkButton` 控件

- 4. 点击三个 `HyperlinkButton` 控件中的任意一个。相应的网页将在新的浏览器窗口或当前浏览器窗口的同一标签页中打开，如图 17.35 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_918_1.png)

## 图 17.35：导航到指定的网页

接下来，让我们讨论 Silverlight 3.0 的 `MediaElement` 控件。

## 使用 MediaElement 控件

如你所知，`MediaElement` 控件允许你在 Silverlight 应用程序中托管音频或视频或两者。执行以下步骤以学习如何使用 `MediaElement` 控件：

- 1. 创建一个名为 `MyMediaPlayerAppCS` 的 Silverlight 应用程序，可在光盘上获得，该应用程序托管在单个 HTML 页面中。在此之前，你需要在当前项目文件夹中添加要播放的媒体文件。为此，你需要使用添加现有项对话框。添加媒体文件后，在解决方案资源管理器中选择它并按键盘上的 `F4` 键。属性窗口出现，图 17.36。

- 2. 在属性窗口中选择 `Copy to Output Directory` 属性，将 `Copy to Output Directory` 属性的默认值从 `Do not copy` 选项更改为 `Copy if newer` 选项，如图 17.36 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_919_0.png)

`Copy if newer` 选项会在媒体文件为新文件时将其复制到当前项目文件夹。

- 3. 现在，打开 `MyMediaPlayerAppCS` 应用程序的 `MainPage.xaml` 文件并输入使用 `MediaElement` 控件的代码。清单 17.9 显示了 `MyMediaPlayerAppCS` 应用程序的 `MainPage.xaml` 文件的代码：

## 清单 17.9：显示 MainPage.xaml 文件的代码

```
<UserControl x:Class="MyMediaPlayerAppCS.MainPage"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d"
d:DesignHeight="600" d:DesignWidth="600">
<Grid x:Name="LayoutRoot" Background="SteelBlue" DataContext="{Binding}">
<Border BorderBrush="Yellow" BorderThickness="3"/>
<TextBlock Text="My Media Player" HorizontalAlignment="Center" FontSize="24" Margin="0,10,0,0" Foreground="Yellow"/>
<Button x:Name="play" Height="50" Width="50" Content="Play" Margin="0,0,100,425" Background="Yellow" Click="mediaPlay"/>
<Button x:Name="pause" Height="50" Width="50" Content="Pause" Margin="0,0,0,425" Background="Yellow" Click="mediaPause"/>
<Button x:Name="stop" Height="50" Width="50" Content="Stop" Margin="100,0,0,425" Background="Yellow" Click="mediaStop"/>
<Border Height="425" Width="525" BorderBrush="Yellow" BorderThickness="3" Margin="0,100,0,0"/>
<MediaElement x:Name="mediaEle" Height="400" Width="500" Margin="0,100,0,0" Source="wildlife.wmv" Stretch="UniformToFill" Volume="0.75" AutoPlay="False"
```

```
Balance="1" MediaOpened="mediaOpen" MediaFailed="mediaError"/>
<TextBlock x:Name="errorText" Text="" Height="50" Width="100" Foreground="Yellow"/>
<TextBlock x:Name="mediaFile" Height="50" Width="200" Foreground="Yellow" Text="Media File: " Margin="0,565,0,0" FontWeight="Bold"/>
<TextBlock x:Name="duration" Height="50" Width="200" Foreground="Yellow" Text="Total Time: " Margin="400,565,0,0" FontWeight="Bold"/>
</Grid>
</UserControl>
```

在清单 17.9 中，添加了一个 `MediaElement` 控件来托管视频文件 `Wildlife.wmv`。`MediaElement` 控件的 `Stretch` 属性被设置为 `UniformToFill`，这意味着视频占据整个控件而不改变原始纵横比。如果控件小于视频，则视频会被裁剪以适应控件。`MediaElement` 控件的 `Volume` 属性被设置为 `0.75`，这意味着媒体播放的音量为最大音量的 75%。此外，`MediaElement` 控件的 `AutoPlay` 属性被设置为 `False`，这意味着托管在控件中的媒体在媒体文件打开后不会自动开始播放，而需要手动开始播放。此外，`Balance` 属性被设置为 `1`，这意味着右立体声扬声器的音量为满音量。`MediaElement` 控件的 `MediaOpened` 和 `MediaFailed` 事件关联了事件处理程序。注意有三个名为 `Play`、`Pause` 和 `Stop` 的按钮，点击后分别开始、暂停和停止媒体的播放。

- 4. 打开 `MyMediaPlayerAppCS` 应用程序的 `MainPage.xaml` 文件的代码隐藏文件并输入如清单 17.10 所示的代码：

## 清单 17.10：显示 MainPage.xaml 文件的代码隐藏文件的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Net;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Animation;
using System.Windows.Shapes;
namespace MyMediaPlayerAppCS
{
    public partial class MainPage : UserControl
    {
        public MainPage()
        {
            InitializeComponent();
        }
        public void mediaOpen(object sender, RoutedEventArgs e)
        {
            mediaFile.Text += mediaEle.Source.ToString();
            duration.Text += mediaEle.NaturalDuration.TimeSpan.Hours.ToString() + ":" + mediaEle.NaturalDuration.TimeSpan.Minutes.ToString() + ":" + mediaEle.NaturalDuration.TimeSpan.Seconds.ToString();
        }
        public void mediaError(object sender, RoutedEventArgs e)
        {
            errorText.Text = "Failed to open the media";
        }
        public void mediaPlay(object sender, RoutedEventArgs e)
        {
            mediaEle.Play();
            play.Content = "Play";
        }
```

```
public void mediaPause(object sender, RoutedEventArgs e)
{
    mediaEle.Pause();
    play.Content = "Resume";
}
public void mediaStop(object sender, RoutedEventArgs e)
{
    mediaEle.Stop();
    play.Content = "Play";
}
}
```

在清单 17.10 中，`mediaOpen()` 方法在 `MediaElement` 控件中的媒体被打开时执行。此方法使用 `MediaElement` 控件的 `Source` 和 `NaturalDuration` 属性，在应用程序中显示媒体文件的名称和长度。`mediaPlay()` 方法在单击播放按钮时执行。此方法调用 `MediaElement` 控件的 `Play()` 方法。类似地，当你在应用程序中单击暂停和停止按钮时，`mediaPause()` 和 `mediaStop()` 方法中分别调用 `MediaElement` 控件的 `Pause()` 和 `Stop()` 方法。如果在打开或播放媒体时出现任何错误，则 `mediaError()` 方法会执行。

- 5. 通过在键盘上按 `F5` 键运行 `MyMediaPlayerAppCS` 应用程序。输出显示如下所示，如图 17.37 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_921_0.png)

## 图 17.37：MyMediaPlayerAppCS 应用程序的输出

你可以在应用程序中分别单击播放、暂停和停止按钮来播放、暂停和停止媒体文件。

#### 注意

> 视频 `Wildlife.wmv` 是通过在解决方案资源管理器中选择 `MyMediaPlayer`→Add→Existing Item 添加到当前项目文件夹的。

接下来，让我们学习关于 `Popup` 控件。

## 使用 Popup 控件

可能存在你想要提供额外信息或显示有关应用程序中某物，例如控件或 UI 元素 的帮助信息的情况。在这种情况下，你可以使用 Silverlight 3.0 中提供的 `Popup` 控件。`Popup` 控件在其他控件之上有界区域中显示信息。有界区域可以是作为 `Popup` 控件子项托管的任何 UI 控件。执行以下步骤以学习如何使用 `Popup` 控件：

- 1. 创建一个 Silverlight 应用程序，托管在单个 HTML 页面中，命名为 `PopUpHelpAppCS`，可在 CD 上获得。清单 17.11 显示了 `PopUpHelpAppCS` 应用程序的 `MainPage.xaml` 文件的代码：

## 清单 17.11：显示 MainPage.xaml 文件的代码

```
<UserControl xmlns:my="clr-namespace:System.Windows.Controls;assembly=System.Windows.Controls" x:Class="PopUpHelpAppCS.MainPage" xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml" xmlns:d="http://schemas.microsoft.com/expression/blend/2008" xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" mc:Ignorable="d" d:DesignHeight="400" d:DesignWidth="750" Foreground="Yellow">
<Grid x:Name="LayoutRoot" Background="Black">
<TextBlock Text="Silverlight 3 Controls" Margin="10,10,0,0" HorizontalAlignment="Center"/>
<TextBlock Text="TextBox" Margin="50,65,0,0"/>
<TextBox Text="This is a TextBox control" Margin="200,65,200,305" Foreground="Red" MouseEnter="showTextPopup" MouseLeave="hideTextPopup"/>
<Popup x:Name="popup1" HorizontalOffset="400" VerticalOffset="75">
<Popup.Child>
<Button Background="Green" VerticalAlignment="Top" MaxWidth="200" FontWeight="Bold" Foreground="DarkBlue" IsEnabled="False">
<Button.ContentTemplate>
<DataTemplate>
<Grid>
<TextBlock Text ="The TextBox control allows you to display text or retrieve text from user. In Silverlight 2, the TextBox control can display text in multiple lines and wrap text around the control." TextWrapping="Wrap"/></TextBlock>
</Grid>
</DataTemplate>
</Button.ContentTemplate>
</Button>
</Popup.Child>
</Popup>
<TextBlock Text="ListBox" Margin="50,145,0,0"/>
```
