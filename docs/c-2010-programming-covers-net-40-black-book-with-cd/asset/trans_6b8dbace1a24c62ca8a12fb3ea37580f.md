

| 表 10.56：System.Windows.Forms.Integration 命名空间的类 |
| Class | Description |
| IntegrationExceptionEventArgs | 为支持可选引发的异常的 EventArgs 类提供基类 |
| LayoutExceptionEventArgs | 为 LayoutError 事件提供数据 |
| PropertyMap | 提供在 Windows Forms 控件和 WPF 控件之间转换属性值的方式 |
| PropertyMappingExceptionEventArgs | 为 PropertyMappingError 事件提供数据 |
| WindowsFormsHost | 允许您在 WPF 页面上托管 Windows Forms 控件 |

在所有这些类中，实现互操作功能最重要的两个类是 WindowsFormsHost 和 ElementHost。您可以在 WPF 页面上托管 Windows Forms 控件时使用 WindowsFormsHost 类。

## 立即解决方案

## 使用 WPF 控件

在本节中，您将学习如何使用本章 *In Depth* 部分中讨论的 WPF 控件及其属性。让我们先讨论如何在 WPF 应用程序中使用 Calendar 和 DatePicker 控件。

## 使用 Calendar 和 DatePicker 控件

正如本章 *In Depth* 部分中已讨论的那样，您可以使用 Calendar 或 DatePicker 控件中的任一个来选择日期。现在让我们创建一个名为 Calendar_and_DatePicker 的 WPF 应用程序（可在 CD 上获得），以学习如何使用 Calendar 和 DatePicker 控件。为此，在 Calendar_and_DatePicker 应用程序的 MainWindow.xaml 文件中添加 Listing 10.1 所示的代码：

```
Listing 10.1: Using the Calendar and DatePicker Control

```xml
<Window x:Class="Calendar_and_DatePicker.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="MainWindow" Height="350" Width="525">
    <Grid>
        <Calendar Height="170" HorizontalAlignment="Left" Margin="12,65,0,0"
                  Name="calendar1" VerticalAlignment="Top" Width="180"
                  SelectionMode="MultipleRange">
            <Calendar.BlackoutDates>
                <CalendarDateRange Start="5/1/2010" End="5/10/2010"/>
            </Calendar.BlackoutDates>
        </Calendar>
        <DatePicker Height="25" HorizontalAlignment="Left" Margin="240,65,0,0"
                    Name="datePicker1" VerticalAlignment="Top" Width="243" FirstDayOfWeek="Monday"
                    SelectedDateFormat="Long" />
        <Label Content="Calendar" Height="28" HorizontalAlignment="Left"
               Margin="73,12,0,0" Name="label1" VerticalAlignment="Top" FontWeight="Bold"
               FontStyle="Italic" />
        <Label Content="DatePicker" Height="28" HorizontalAlignment="Left"
               Margin="334,12,0,0" Name="label2" VerticalAlignment="Top" FontWeight="Bold"
               FontStyle="Italic" />
    </Grid>
</Window>
```
```

在 Listing 10.1 中，我们添加了一个 Calendar 控件，其中我们指定了用户无法选择的日期范围，并将 Calendar 控件的 selection mode 更改为 MultipleRange，这允许用户选择多个日期范围。此外，我们还添加了一个 DatePicker 控件并更改了日期格式和一周的第一天。Calendar_and_DatePicker 应用程序的输出如 Figure 10.37 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_465_0.png)

## 通过 XAML 代码添加控件

您可以通过 XAML 代码或 code-behind 文件将控件添加到 WPF 应用程序。现在让我们学习如何通过 XAML 代码将一些常用控件添加到 WPF 应用程序。创建一个名为 AddingControls_XAML 的 WPF 应用程序（可在 CD 上获得）并将代码添加到 MainWindow.xaml 文件，如 Listing 10.2 所示：

Listing 10.2: Implementing Controls through XAML Code

```
<Window x:Class="AddingControls_XAML.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="MainWindow" Height="300" Width="300">
    <Grid>
        <Grid.RowDefinitions>
            <RowDefinition Height="29"/>
            <RowDefinition Height="27"/>
            <RowDefinition Height="71"/>
            <RowDefinition Height="135" />
        </Grid.RowDefinitions>
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="141"/>
            <ColumnDefinition Width="137" />
        </Grid.ColumnDefinitions>
        <Label FontSize="15">
            Login ID:
        </Label>
        <TextBox HorizontalAlignment="Right" Margin="0,0,-128,0" Name="Login" Width="128" />
        <Label FontSize="15" Grid.Row="1">
            Password:
        </Label>
        <TextBox Grid.Row="1" HorizontalAlignment="Right" Margin="0,0,-128,0" Name="Password" Width="128"></TextBox>
        <Button Margin="12,10,18,29" Name="Submit" Grid.Row="2">Submit</Button>
        <Button Grid.Row="2" Margin="14,10,21,29" Name="Clear" Grid.Column="1">Clear</Button>
    </Grid>
</Window>
```

在 Listing 10.2 中，两个 Label 控件、一个 TextBox 控件和一个 Button 控件被添加到窗口中。您可以通过按 F5 键运行应用程序。

Listing 10.2 的输出如 Figure 10.38 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_466_0.png)

Figure 10.38: Showing the Controls Added to a Window

您可以为 Login ID 文本框输入登录 ID，并在 Password 文本框中输入密码，最后单击 Submit 按钮。

## 通过 Code-Behind 文件添加控件

将控件添加到 WPF 应用程序的另一种方式是通过 code-behind 文件。现在让我们通过 code-behind 文件将一些常用控件添加到 WPF 应用程序。

## 第 10 章：使用 WPF 4.0 控件、资源、样式、模板和命令

为此，创建一个名为 AddingControls_CodeBehind 的 WPF 应用程序（可在 CD 上获得）并用 Listing 10.3 中突出显示的代码替换 MainWindow.xaml 文件中的 Grid 元素，以将 Grid 控件重命名为 myGrid，如下所示：

### Listing 10.3: Renaming the Grid control in the MainWindow.xaml File

```
```xml
<Window x:Class="AddingControls_CodeBehind.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="MainWindow" Height="350" Width="525">
    <Grid Name="myGrid">
    </Grid>
</Window>
```
```

在 Listing 10.3 中，Grid 控件的名称已更改为 myGrid。控件将从您的 code-behind 文件添加到 Grid 控件。因此，打开 MainWindow.xaml.cs 文件并添加 Listing 10.4 所示的代码：

### Listing 10.4: Adding Controls to the myGrid Grid Control

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
namespace AddingControls_CodeBehind
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
            Label myLabel = new Label();
            myLabel.Content = "Enter your Name:";
            myLabel.FontSize = 12;
            myLabel.FontWeight = FontWeights.Bold;
            myGrid.Children.Add(myLabel);
            TextBox myTextBox = new TextBox();
            myTextBox.Margin = new Thickness(0, 5, 10, 5);
            myTextBox.Height = 30;
            myTextBox.Width = 150;
            myGrid.Children.Add(myTextBox);
            myTextBox.HorizontalAlignment = HorizontalAlignment.Right;
            myTextBox.VerticalAlignment = VerticalAlignment.Top;
            Button myButton = new Button();
            myButton.Content = "Submit";
            myButton.FontSize = 11;
            myButton.FontWeight = FontWeights.Bold;
            myButton.Height = 50;
            myButton.Width = 75;
            myGrid.Children.Add(myButton);
```
