
在前面的清单中，System.Windows.Data 命名空间被添加到 SilverlightDataPager 应用程序中。还创建了一个名为 pagedcollectionview 的 PagedCollectionView 类的实例。字符串 WELCOMETOSILVERLIGHT3 被传递给对象 pagedcollectionview，并且还使用了 String.Split() 方法。String.Split() 方法返回一个字符串数组，用于查找字符串中由一个或多个字符分隔的所有子字符串。

- 3. 运行 SilverlightDataPagerCS 应用程序。输出如图 17.43 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_933_0.png)

## 图 17.43：显示 SilverlightDataPagerCS 应用程序的输出

- 4. 单击页面底部可见的 DataPager 中的任意页码。输出如图 17.44 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_933_1.png)

## 图 17.44：选择第四页后显示的输出

如图 17.44 所示，DataPager 控件 myPager 显示了 DataGrid 控件中第四页的数据项。接下来，让我们讨论 TreeView 控件。

## 使用 TreeView 控件

如前所述，您知道 Silverlight TreeView 控件可用于以节点形式显示分层数据。TreeView 控件中包含子节点的节点也可以折叠和展开。您可以单击 TreeView 控件的任意节点将其折叠，或展开该节点以显示其子节点。TreeView 控件是一种专门的 ItemsControl 控件，这意味着您可以通过设置其 Items 或 ItemsSource 属性来向 TreeView 控件填充内容。现在，执行以下步骤以在 Silverlight 应用程序中使用 TreeView 控件：

- 1. 创建一个名为 SilverlightTreeViewCS 的 Silverlight 应用程序（可在 CD 上获得）。清单 17.18 显示了 SilverlightTreeViewCS Silverlight 应用程序的 MainPage.xaml 文件的代码：

### 清单 17.18：显示 SilverlightTreeViewCS 应用程序的 MainPage.xaml 文件的代码

```
<UserControl xmlns:my="clr-namespace:System.Windows.Controls;assembly=System.Windows.Controls" x:Class="SilverlightTreeViewCS.MainPage" xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml" xmlns:d="http://schemas.microsoft.com/expression/blend/2008" xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" mc:Ignorable="d" d:DesignHeight="300" d:DesignWidth="400">
<Grid x:Name="LayoutRoot">
<my:TreeView Background="Beige">
<my:TreeViewItem Header="Programming Languages" Foreground="Red" FontFamily="Comic Sans MS" FontSize="15" FontWeight="Bold">
<my:TreeViewItem Header="Structured Programming Language" FontFamily="Georgia" FontSize="12" Foreground="HotPink">
<my:TreeViewItem Header="C" FontFamily="Courier New" FontSize="10" Foreground="MidnightBlue"/>
</my:TreeViewItem>
<my:TreeViewItem Header="Object-Oriented Programming Languages" FontFamily="Georgia" FontSize="12" Foreground="HotPink">
<my:TreeViewItem Header="Java" FontFamily="Courier New" FontSize="10" Foreground="MidnightBlue"/>
<my:TreeViewItem Header="C#" FontFamily="Courier New" FontSize="10" Foreground="MidnightBlue"/>
<my:TreeViewItem Header="VB.NET" FontFamily="Courier New" FontSize="10" Foreground="MidnightBlue"/>
</my:TreeViewItem>
<my:TreeViewItem Header="Dynamic Languages" FontFamily="Georgia" FontSize="12" Foreground="HotPink">
<my:TreeViewItem Header="Python" FontFamily="Courier New" FontSize="10" Foreground="MidnightBlue"/>
<my:TreeViewItem Header="Ruby" FontFamily="Courier New" FontSize="10" Foreground="MidnightBlue"/>
</my:TreeViewItem>
</my:TreeViewItem>
</my:TreeView>
</Grid>
</UserControl>
```

2. 运行 SilverlightTreeViewCS 应用程序。输出如图 17.45 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_934_0.png)

## 图 17.45：显示 SilverlightTreeViewCS 应用程序的输出

如图 17.45 所示，TreeView 控件的根节点可见。

- 3. 单击根节点“Programming Languages”左侧的三角形字形以展开它并查看其子节点。展开根节点后的输出如图 17.46 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_935_0.png)

图 17.46：展开根节点后显示的输出

如图 17.46 所示，TreeView 控件的根节点显示其子节点。您可以进一步展开子节点以查看它们的子节点。

接下来，让我们创建一个应用程序来学习如何将 Silverlight 与 ASP.NET 应用程序集成。

## 将 Silverlight 与 ASP.NET 应用程序集成

您已经在“深入探讨”部分了解到，您可以轻松地将 Silverlight 与 ASP.NET 应用程序集成。现在，执行以下步骤创建一个应用程序，以学习如何集成 Silverlight 和 ASP.NET 应用程序。

- 1. 创建一个名为 AnimatedButtonAppCS 的应用程序（可在 CD 上获得）。为此，打开 Visual Studio IDE 并选择“文件”→“新建”→“项目”。出现“新建项目”对话框。在“已安装的模板”窗格下，选择“Visual C#”→“Silverlight”，然后从中间窗格中选择“Silverlight 应用程序”。将应用程序的名称指定为 AnimatedButtonAppCS，并输入适当的位置以保存应用程序。

- 2. 单击“确定”按钮，这将显示“新建 Silverlight 应用程序”对话框（图 17.47）。

- 3. 选中“在新网站中承载 Silverlight 应用程序”复选框，然后单击“确定”按钮，如图 17.47 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_935_1.png)

图 17.47：选择在网站中承载 Silverlight 内容的选项

4. 打开 AnimatedButtonAppCS 应用程序的 MainPage.xaml 文件，并添加清单 17.19 所示的代码：

### 清单 17.19：显示 MainPage.xaml 文件的代码

```
<UserControl x:Class="AnimatedButtonAppCS.MainPage"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d"
d:DesignHeight="450" d:DesignWidth="450">

<Grid x:Name="LayoutRoot" Background="Red">
    <Grid.Triggers>
        <EventTrigger RoutedEvent="Grid.Loaded">
            <EventTrigger.Actions>
                <BeginStoryboard>
                    <Storyboard RepeatBehavior="Forever" AutoReverse="True">
                        <DoubleAnimation To="185" Duration="0:0:9"
Storyboard.TargetName="button1"
Storyboard.TargetProperty="Height"/>
                        <DoubleAnimation To="185" Duration="0:0:9"
Storyboard.TargetName="button1"
Storyboard.TargetProperty="Width"/>
                    </Storyboard>
                </BeginStoryboard>
            </EventTrigger.Actions>
        </EventTrigger>
    </Grid.Triggers>
    <Button x:Name="button1" Height="425" Width="425" Content="Silverlight and ASP.NET" Background="DarkCyan" Foreground="Red" FontWeight="SemiBold" FontSize="15"/>
</Grid>
</UserControl>
```

5. 在解决方案资源管理器中右键单击 AnimatedButtonAppCSTestPage.aspx 文件，然后选择“设为起始页”选项。

6. 按键盘上的 F5 键运行 AnimatedButtonAppCS 应用程序。应用程序的输出如图 17.48 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_936_0.png)

图 17.48：通过 Silverlight 在 ASP.NET Web 应用程序中实现的动画按钮

## 使用 Silverlight 应用程序进行数据绑定

您也可以在 Silverlight 应用程序中执行数据绑定。与 ASP.NET 应用程序一样，Silverlight 应用程序可以显示在 Web 浏览器中。与 Silverlight 1 不同，Silverlight 2 具有支持数据绑定功能的控件。Silverlight 的数据绑定功能以更少的运行时代码提供了更强大、更灵活的数据处理能力。对于 Silverlight 中的数据绑定，您可以使用 DataGrid 控件。让我们创建一个 Silverlight 应用程序来显示数据：

- 1. 创建一个名为 DataBindinginSilverlightCS 的 Silverlight 应用程序（可在 CD 上获得）。

- 2. 单击“新建项目”对话框中的“确定”按钮。将打开“新建 Silverlight 应用程序”对话框（图 17.49）。

- 3. 在“新建 Silverlight 应用程序”对话框中，选中“在新网站中承载 Silverlight 应用程序”复选框以承载 Silverlight 内容。

- 4. 在标记为“Silverlight 版本”的下拉列表中选择 Silverlight 3，然后单击“确定”按钮，如图 17.49 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_937_0.png)

图 17.49：为 Silverlight 应用程序指定宿主

这将在您的应用程序中创建两个项目，分别名为 DataBindinginSilverlightCS 和 DataBindinginSilverlightCS.Web。第一个项目 DataBindinginSilverlightCS 是 Silverlight 应用程序。第二个项目 DataBindinginSilverlightCS.Web 是作为 Silverlight 项目的测试环境为您创建的。

- 5. 从“服务器资源管理器”窗口创建到 Northwind 数据库中 Employees 表的连接。如果“服务器资源管理器”窗口尚未打开，可以通过选择菜单栏中的“视图”→“服务器资源管理器”选项来打开它。创建连接后，您需要创建 Web 服务。

- 6. 右键单击测试项目 DataBindinginSilverlightCS.Web，然后选择“添加”→“新建项”选项来创建 WCF 服务，如图 17.50 所示：

