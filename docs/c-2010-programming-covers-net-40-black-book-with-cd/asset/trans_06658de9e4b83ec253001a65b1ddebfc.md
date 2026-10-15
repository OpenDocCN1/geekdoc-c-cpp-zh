

```csharp
get { return _state; }
set { _state = value; }
}
public Place(string name, string state)
{
    this._name = name;
    this._state = state;
}
}
public class Places : ObservableCollection<Place>
{
    public Places()
    {
        Add(new Place("India", "INDIA"));
        Add(new Place("Australia", "AUS"));
        Add(new Place("America", "USA"));
        Add(new Place("Africa", "AFR"));
        Add(new Place("Russia", "USSR"));
    }
}
}
```

前面的代码将数据绑定到窗口。您可以通过按 F5 键运行应用程序。清单 10.31 和清单 10.32 的输出如下所示，如图 10.61 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_490_0.png)

## 图 10.61：使用触发器的输出

在清单 10.31 和清单 10.32 中，DataTrigger 触发器被指定为：如果状态为 INDIA，则 ListBox 控件中对应项的前景色将被设置为红色。

## 使用 WPF 命令与控件

在 WPF 中使用命令的最简单方法之一是使用预定义的 RoutedCommand 类。Cut、Copy 和 Paste 是 ApplicationCommand 类中的预定义命令。MenuItem 控件具有调用命令的原生支持。创建一个名为 WPFCommands_with_Controls 的 WPF 应用程序（可在 CD 上获得）并将以下代码添加到 MainWindow.xaml 文件中，如清单 10.33 所示：

### 清单 10.33：显示使用 WPF 命令与控件的代码

```
```xml
<Window x:Class="WPFCommands_with_Controls.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="MainWindow" Height="350" Width="525">
    <Grid>
        <StackPanel>
            <Menu>
```

```
<MenuItem Command="ApplicationCommands.Paste" />
<MenuItem Command="ApplicationCommands.Copy" />
<MenuItem Command="ApplicationCommands.Cut" />
</Menu>
<TextBox Name="TextBox1"/>
<TextBox Name="TextBox2"/>
</StackPanel>
</Grid>
</window>
```

在清单 10.33 中，添加了三个具有 Cut、Copy 和 Paste 命令的 MenuItem 控件以及两个 TextBox 控件。您可以在一个 TextBox 控件中输入文本，并在另一个 TextBox 控件中执行 Cut 和 Paste 或 Copy 和 Paste 命令。例如，当您在 TextBox1 文本框中输入文本时，Cut 和 Copy 命令会被禁用。在您输入文本并选择它之后，Cut 和 Copy 命令会被启用。当您运行应用程序时，TextBox 控件会显示为空白。当您对 Text 控件执行某些操作时，您会得到如图 10.62 所示的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_491_0.png)

图 10.62：使用 WPF 命令与控件

## 在 WPF 应用程序中托管 Windows Forms 控件

在 WPF 中，您可以将 Windows Forms 的控件集成到 WPF 应用程序中。您需要一个包装器，即 WPF 控件来托管 Windows Forms 控件。此包装器是 WindowsFormsHost 类，位于 WindowsFormsIntegration.dll 程序集中。WindowsFormsHost 类派生自基类 HwndHost 和 FrameworkElement，因此可作为 WPF 元素使用。Windows Forms 中有一些控件在 WPF 应用程序中不可用。您可以通过在 WPF 应用程序中托管 Windows Forms 控件来添加它们。这些控件中的一些是 MaskedTextBox、DateTimePicker、MonthCalendar、DataGridView 和 PrintPreviewControl。让我们通过执行以下步骤学习如何在 WPF 应用程序中托管 Windows Forms 控件：

- 1. 创建一个名为 WindowsForms_in_WPFApplication 的 WPF 应用程序（可在 CD 上获得）。
- 2. 在解决方案资源管理器中添加对 WindowsFormsIntegration 程序集的引用，其名称为 WindowsFormsIntegration.dll。然后，添加对 Windows Forms 程序集的引用，其名称为 System.Windows.Forms.dll。
- 3. 将代码添加到 MainWindow.xaml 文件中，如清单 10.34 所示：

### 清单 10.34：显示在 WPF 应用程序中使用 Windows Forms 控件的代码

```
<window x:Class="WindowsForms_in_WPFApplication.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:wf="clr-namespace:System.Windows.Forms;assembly=System.Windows.Forms"
Title="HostingwfInwpf" Height="191" Width="182">
<Grid Height="108" Width="127">
<windowsFormsHost>
<wf:MaskedTextBox x:Name="Date" Mask="0000/00/00" />
</windowsFormsHost>
</Grid>
</window>
```

在前面的代码中，MaskedTextBox 控件被添加为 WindowsFormsHost 控件的子项。您可以通过按 F5 键运行应用程序。
清单 10.34 的输出，其中输入了日期，如图 10.63 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_492_0.png)

图 10.63：在 WPF 应用程序中显示 Windows Forms 控件

## 在 Windows Forms 应用程序中托管 WPF 控件

与前面将 Windows Forms 控件托管在 WPF 应用程序中的示例类似，您也可以将 WPF 控件托管在 Windows Forms 应用程序中。但是，您不能直接在 Windows Forms 应用程序中使用 WPF 控件。您需要使用来自 System.Windows.Forms.Control 命名空间的包装器类 ElementHost 来在 Windows Forms 应用程序中使用 WPF 控件。ElementHost 控件管理 WPF 控件。

让我们通过执行以下步骤学习如何在 Windows Forms 应用程序中托管 WPF 控件：

- 1. 创建一个名为 WPFControl_in_WindowsForm 的 Windows Forms 应用程序（可在 CD 上获得）您将得到一个空白的 Windows 窗体。
- 2. 右键单击项目名称并在解决方案资源管理器中选择 Add→New Item。
- 3. 在添加新项目对话框中选择用户控件（WPF）模板，提供名称 UserControl1.xaml，然后单击添加按钮以将用户控件添加到应用程序中。
- 在将用户控件添加到 Windows Forms 应用程序后，您将获得类似于 WPF 应用程序的界面。您可以将需要的 WPF 控件添加到新的 WPF 用户控件中。
- 4. 将 System.Xaml.dll 程序集的引用添加到项目中。
- 5. 将清单 10.35 中显示的代码添加到 UserControl1.xaml 文件中：
- 6. 通过从菜单栏中选择 Build→Build Solution 来构建应用程序。
- 7. 通过从工具箱的 WPF 互操作性选项卡中拖动它并将其放置在 Windows 窗体上，添加一个 ElementHost 控件。ElementHost 控件用于将 WPF 用户控件放置在窗体上。

### 清单 10.35：显示将 WPF 控件添加到 Windows Forms 应用程序的代码

```
<UserControl x:Class="WPFControl_in_WindowsForm.UserControl1"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    mc:Ignorable="d"
    d:DesignHeight="300" d:DesignWidth="300">

    <Grid>
        <Ellipse Margin="76,40,91,136" Name="ellipse1" Stroke="White" StrokeThickness="4" Fill="LightBlue"/>
        <Rectangle Margin="15,0,10,27" Name="rectangle1" Stroke="white" Height="110" VerticalAlignment="Bottom" StrokeThickness="4" Fill="Pink"/>
    </Grid>
</UserControl>
```

8. 单击右上角的箭头以显示智能标记，以选择 ElementHost 控件的内容，如图 10.64 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_493_0.png)

9. 在智能标记的 Select Hosted Content 下拉列表中选择 UserControl1。

您在 UserControl1.xaml 文件中创建的 WPF 应用程序将出现在 ElementHost 控件内部。

10. 通过按 F5 键运行应用程序。应用程序的输出如下所示，如图 10.65 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_493_1.png)

现在，让我们回顾一下本章讨论的主要主题。

## 摘要

在本章中，您学习了用于创建 WPF 应用程序的 WPF 的各种控件。您还学习了 WPF 中使用的资源、样式、模板和触发器。本章还讨论了 WPF 中的资源，它帮助您在一个地方定义应用程序中常用的值并重用它们。接下来，您学习了要在 WPF 应用程序中使用的样式、模板和触发器。您还学习了 WPF 命令，它帮助您对应用程序执行额外的操作，例如 Cut、Copy 和 Paste。

在下一章中，您将学习在 WPF 中使用排版和文档功能。
