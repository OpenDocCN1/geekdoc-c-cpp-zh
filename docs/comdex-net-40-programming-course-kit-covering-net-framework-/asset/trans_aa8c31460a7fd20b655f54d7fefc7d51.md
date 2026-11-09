
## 使用 DataPager 控件

DataPager 控件随 Silverlight 3.0 引入，用于当你有大量数据集合且无法在单页中显示全部数据的情况。此控件用于表示对数据集合进行分页所需的 UI。你可以为实现了 IPagedCollectionView 接口的数据集合提供分页功能。该接口包含为数据集合提供分页功能的方法和属性定义。

在 Silverlight 应用程序中，要配合 DataGrid 控件使用 DataPager 控件，请执行以下步骤：

- 1. 打开 Microsoft Visual Studio 2010，然后选择“文件”→“新建”→“项目”。将出现“新建项目”对话框。
- 2. 在“新建项目”对话框的“已安装的模板”窗格中，选择 Visual C#→Silverlight。
- 3. 从中间窗格中选择 Silverlight Application。
- 4. 在“名称”文本框中将应用程序名称指定为 SilverlightDataPager（光盘中也可用），并在“位置”组合框中指定适当位置。
- 5. 单击“确定”按钮。将出现“新建 Silverlight 应用程序”对话框。
- 6. 选中“在新网站中承载 Silverlight 应用程序”复选框。
- 7. 从“新建 Web 项目类型”下拉框中选择“ASP.NET Web 应用程序”项目选项。
- 8. 从“Silverlight 版本”下拉框中选择 Silverlight 4。
- 9. 选中“启用 WCF RIA Services”复选框。
- 10. 单击“确定”按钮。将创建 SilverlightDataPager 应用程序。
- 11. 将 MainPage.xaml 文件的代码替换为代码清单 11.6 中显示的代码，以设计应用程序的 UI：

**代码清单 11.6：** 显示 SilverlightDataPager 应用程序的 MainPage.xaml 文件的代码

```xml
<UserControl
    xmlns:sdk="http://schemas.microsoft.com/winfx/2006/xaml/presentation/sdk"
    x:Class="SilverlightDataPager.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    d:DesignHeight="300" d:DesignWidth="400">
<Grid x:Name="LayoutRoot" Background="Black" Height="300" Width="400">
<StackPanel x:Name="ContentStackPanel" Orientation="Vertical">
<sdk:DataGrid x:Name="myDataGrid" Height="200" Width="400" />
<sdk:DataPager x:Name="myPager" Source="{Binding Path=ItemsSource,
                ElementName=myDataGrid}" DisplayMode="Numeric"/>
</StackPanel>
</Grid>
</UserControl>
```

在代码清单 11.6 中，添加了一个 DataGrid 控件 myDataGrid 和一个 DataPager 控件 myPager。DataPager 控件用于在多个页面中显示 DataGrid 控件 myDataGrid 内的数据项。

- 12. 将 MainPage.xaml.cs 文件的代码替换为代码清单 11.7 中显示的代码：

**代码清单 11.7：** 显示 MainPage.xaml 文件的代码隐藏文件的代码

```csharp
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
using System.Windows.Data;
namespace SilverlightDataPager
{
    public partial class MainPage : UserControl
    {
        public MainPage()
        {
            InitializeComponent();
            PagedCollectionView pagedCollectionView = new PagedCollectionView
                ("WELCOME TO SILVERLIGHT 3");
            pagedCollectionView.PageSize = 5;
            myDataGrid.ItemsSource = pagedCollectionView;
        }
    }
}
```

在代码清单 11.7 中，将 **System.Windows.Data** 命名空间添加到 **SilverlightDataPager** 应用程序。创建了一个名为 pagedCollectionView 的 **PagedCollectionView** 类实例。该类用于对数据集合进行分组、排序、筛选和分页。接下来，将字符串 WELCOME TO SILVERLIGHT 3 传递给该对象，并使用 **String.Split()** 方法；该方法返回一个字符串数组，并查找由一个或多个字符分隔的所有子字符串。

- 13. 按 **F5** 运行 **SilverlightDataPager** 应用程序。将出现输出（图 ASP-11.26）。
- 14. 单击 **DataPager** 控件中的任意页码。将出现输出（图 ASP-11.27）。

![](img/9862a98a1a2d3bb14334137965a1ec60_720_0.png)

图 ASP-11.26

![](img/9862a98a1a2d3bb14334137965a1ec60_720_1.png)

图 ASP-11.27

在图 ASP-11.27 中，DataPager 控件 myPager 显示 DataGrid 控件中第四页的数据项。

## 使用 TreeView 控件

**TreeView** 控件随 Silverlight 3.0 引入，用于以节点形式显示分层数据。**TreeView** 控件中包含子节点的节点可以折叠和展开。你可以单击 TreeView 控件的任意节点来折叠或展开它。**TreeView** 控件是一种专用的 **ItemsControl** 控件，这意味着你可以通过设置其 **Items** 属性或 **ItemsSource** 属性，用一些内容填充 **TreeView** 控件。

现在，让我们执行以下步骤，在 Silverlight 应用程序中使用 TreeView 控件：

- 1. 打开 **Microsoft Visual Studio 2010**，然后选择 **文件→新建→项目**。将出现 **新建项目** 对话框。
- 2. 在 **新建项目** 对话框的 **已安装的模板** 窗格中，选择 **Visual C#→Silverlight**。
- 3. 从中间窗格中选择 **Silverlight 应用程序**。
- 4. 在 **名称** 文本框中将应用程序名称指定为 **SilverlightTreeView**（光盘中也可用），并在 **位置** 组合框中指定适当位置。
- 5. 单击 **确定** 按钮。将出现 **新建 Silverlight 应用程序** 对话框。
- 6. 选中 **在新网站中承载 Silverlight 应用程序** 复选框。
- 7. 从 **新建 Web 项目类型** 下拉框中选择 **ASP.NET Web 应用程序项目** 选项。
- 8. 从 **Silverlight 版本** 下拉框中选择 **Silverlight 4**。
- 9. 选中 **启用 WCF RIA Services** 复选框。
- 10. 单击 **确定** 按钮。将创建 **SilverlightTreeView** 应用程序。
- 11. 将 **MainPage.xaml** 文件的代码替换为代码清单 11.8 中显示的代码，以设计应用程序的 UI：

**代码清单 11.8：** 显示 **SilverlightTreeView** 应用程序的 **MainPage.xaml** 文件的代码

```xml
<UserControl
    xmlns:sdk="http://schemas.microsoft.com/winfx/2006/xaml/presentation/sdk"
    x:Class="SilverlightTreeView.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    d:DesignHeight="300" d:DesignWidth="400">
    <Grid x:Name="LayoutRoot">
        <sdk:TreeView Background="beige">
            <sdk:TreeViewItem Header="Programming Languages" Foreground="Red"
                FontFamily="Comic Sans MS" FontSize="15" FontWeight="Bold">
                <sdk:TreeViewItem Header="Structured Programming Language"
                    FontFamily="Georgia" FontSize="12" Foreground="HotPink">
                    <sdk:TreeViewItem Header="Object-Oriented Programming Languages"
                        FontFamily="Georgia" FontSize="12" Foreground="HotPink">
                        <sdk:TreeViewItem Header="Java" FontFamily="Courier New"
                            FontSize="10" Foreground="MidnightBlue">
                        </sdk:TreeViewItem>
                    </sdk:TreeViewItem>
                    <sdk:TreeViewItem Header="C#" FontFamily="Courier New" FontSize="10"
                        Foreground="MidnightBlue">
                    </sdk:TreeViewItem>
                </sdk:TreeViewItem>
                <sdk:TreeViewItem Header="VB.NET" FontFamily="Courier New"
                    FontSize="10" Foreground="MidnightBlue">
                </sdk:TreeViewItem>
            </sdk:TreeViewItem>
            <sdk:TreeViewItem Header="Dynamic Languages" FontFamily="Georgia"
                FontSize="12" Foreground="HotPink">
                <sdk:TreeViewItem Header="Python" FontFamily="Courier New"
                    FontSize="10" Foreground="MidnightBlue">
                </sdk:TreeViewItem>
            </sdk:TreeViewItem>
        </sdk:TreeView>
    </Grid>
</UserControl>
```
