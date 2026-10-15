
``` 
<ListBox Height="58" Margin="200,0,200,75" Foreground="Red" MouseEnter="showListPopup" MouseLeave="hideListPopup" FontSize="11">
<ListBoxItem Content="Silverlight 1.0"/>
<ListBoxItem Content="Silverlight 2.0 Beta 1"/>
<ListBoxItem Content="Silverlight 2.0 Beta 2"/>
<ListBoxItem Content="Silverlight 3.0"/>
</ListBox>
<Popup x:Name="popup2" HorizontalOffset="400" VerticalOffset="150">
<Popup.Child>
<Button Background="Green" VerticalAlignment="Top" MaxWidth="200" FontWeight="Bold" Foreground="DarkBlue" IsEnabled="False">
<Button.ContentTemplate>
<DataTemplate>
<Grid>
    <TextBlock Text ="The ListBox control allows you to display a list of items" TextWrapping="Wrap"></TextBlock>
</Grid>
</DataTemplate>
</Button.ContentTemplate>
</Button>
</Popup.Child>
</Popup>
<TextBlock Text="Calendar" Margin="50,225,0,0"/>
<my:Calendar DisplayMode="Year" IsTodayHighlighted="True" SelectionMode="SingleDate" Margin="0,200,150,0" Foreground="Red" MouseEnter="showCalendarPopup" MouseLeave="hideCalendarPopup"/>
<Popup x:Name="popup3" HorizontalOffset="400" VerticalOffset="225">
    <Popup.Child>
        <Button Background="Green" VerticalAlignment="Top" MaxWidth="200" FontWeight="Bold" Foreground="DarkBlue" IsEnabled="False">
            <Button.ContentTemplate>
                <DataTemplate>
                    <Grid>
                        <TextBlock Text ="The Calendar control provides you the facility to select a particular date from the visible month or year. You can switch between months, years, or decades by using scroll arrows." TextWrapping="Wrap"></TextBlock>
                    </Grid>
                </DataTemplate>
            </Button.ContentTemplate>
        </Button>
    </Popup.Child>
</Popup>
</Grid>
</UserControl>
```

在清单 17.11 中，三个名为 `popup1`、`popup2` 和 `popup3` 的 `Popup` 控件被添加到页面中。每个 `Popup` 控件都有一个按钮作为其子项。按钮提供了显示帮助信息的有界区域。请注意，当鼠标指针放置在文本框、列表框或日历内时，`Popup` 控件会出现，并且当鼠标指针移出文本框、列表框或日历时，`Popup` 控件会消失。

2. 打开代码隐藏文件并输入代码，如清单 17.12 所示：

### 清单 17.12：显示 `MainPage.xaml` 文件的代码隐藏文件的代码

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

namespace PopUpHelpAppCS
{
    public partial class MainPage : UserControl
    {
        public MainPage()
        {
            InitializeComponent();
        }

        public void showTextPopup(object sender, RoutedEventArgs e)
        {
            popup1.IsOpen = true;
        }

        public void showListPopup(object sender, RoutedEventArgs e)
        {
            popup2.IsOpen = true;
        }

        public void showCalendarPopup(object sender, RoutedEventArgs e)
        {
            popup3.IsOpen = true;
        }

        public void hideTextPopup(object sender, RoutedEventArgs e)
        {
            popup1.IsOpen = false;
        }

        public void hideListPopup(object sender, RoutedEventArgs e)
        {
            popup2.IsOpen = false;
        }

        public void hideCalendarPopup(object sender, RoutedEventArgs e)
        {
            popup3.IsOpen = false;
        }
    }
}
```

3. 运行 `PopUpHelpAppCS` 应用程序。输出显示如下所示，如图 17.38 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_924_0.png)

图 17.38：`PopUpHelpAppCS` 应用程序的输出

4. 将鼠标指针悬停在文本框、列表框或日历上；相应的 `Popup` 控件会出现，如图 17.39 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_925_0.png)

图 17.39：显示 `Popup`

至此，你已学习如何使用 `Popup` 控件向用户显示一些信息。接下来，让我们学习关于 `TabControl` 控件。

## 使用 `TabControl` 控件

你已在本章的深入部分学习到，`TabControl` 控件可用于将多个控件分组到一个或多个选项卡中。每个选项卡占用相同的 UI 区域，因此可实现应用程序 UI 的最大利用率。执行以下步骤以使用 `TabControl` 控件：

1. 创建一个 Silverlight 应用程序 `StudentRecordsAppCS`（可在 CD 上获得），托管在 `.aspx` 页面中，以了解如何使用 `TabControl` 控件。

2. 在 `MainPage.xaml` 文件中添加 `TabControl` 控件。清单 17.13 显示了 `StudentRecordsAppCS` 应用程序的 `MainPage.xaml` 文件的代码：

### 清单 17.13：显示 `MainPage.xaml` 文件的代码

``` 
<UserControl xmlns:my="clr-namespace:System.Windows.Controls;assembly=System.Windows.Controls" x:Class="StudentRecordsAppCS.MainPage" xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml" xmlns:d="http://schemas.microsoft.com/expression/blend/2008" xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" mc:Ignorable="d" d:DesignHeight="450" d:DesignWidth="600">
<Grid x:Name="LayoutRoot" Background="OldLace">
<TextBlock Text="Student Records" Margin="10,10,0,0" HorizontalAlignment="Center" Foreground="Purple" FontSize="24" FontWeight="Bold"/>
<my:TabControl Height="315" Width="550" Background="Lavender" Foreground="Purple" TabStripPlacement="Left">
<my:TabItem Header="Howard, Ron" Foreground="Purple" FontWeight="Bold" FontSize="18">
<my:TabItem.Content>
<Canvas>
<TextBlock Text="Student ID: KS231" />
```
