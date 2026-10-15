

![](img/e073a4882197be4ab61103cbe0bcb394_938_0.png)

## 图 17.50：创建 Web 服务

“添加新项”对话框出现（图 17.51）。

- 7. 选择 WCF 服务选项并提供名称 MyService.svc，然后单击“添加”按钮，如图 17.51 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_938_1.png)

## 图 17.51：创建 WCF 服务

- 8. 在“解决方案资源管理器”中右键单击“引用”选项并从出现的上下文菜单中选择“添加服务引用”选项，如图 17.52 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_939_0.png)

## 图 17.52：添加引用

# 注意

您应在添加服务引用之前先构建一次解决方案。

“添加服务引用”对话框出现（图 17.53）。

- 9. 在“添加服务引用”对话框中，单击“发现”按钮。这会将可用的 Web 服务添加到“添加服务引用”对话框中的“服务”窗格中，如图 17.53 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_939_1.png)

## 图 17.53：定位服务

- 10. 从“服务”窗格中选择您刚刚创建的服务并单击“确定”按钮，如图 17.54 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_940_0.png)

## 图 17.54：服务已添加

# 注意

您应在将服务添加到 Silverlight 应用程序之前，先对应用程序进行一次构建。

创建服务后，下一步是为 Silverlight 添加数据检索技术。您需要为数据检索添加一个 LINQ to SQL 类。

- 11. 右键单击服务器项目 DataBindinginSilverlightCS.Web 并选择“添加→新建项”，如图 17.55 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_940_1.png)

## 图 17.55：添加 LINQ to SQL 类

## 第 17 章：使用 Silverlight 3 开发丰富的交互式应用程序

12. 在“添加新项”对话框（图 17.56）中选择 LINQ to SQL 类，并将其命名为 MyClass.dbml。

13. 单击“添加”按钮，如图 17.56 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_941_0.png)

图 17.56：LINQ to SQL 类

MyClass.dbml 窗口出现（图 17.57）。

14. 从“服务器资源管理器”将 Employees 表拖到 MyClass.dbml 中。Employees 表被添加到您的应用程序中，如图 17.57 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_941_1.png)

图 17.57：添加 Employees 表

15. 从“属性”窗口中选择 MyClassDataContext，然后将“序列化模式”属性更改为单向，如图 17.58 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_942_0.png)

## 图 17.58：更改属性

如图所示 17.58，“序列化模式”属性更改为单向，以确保数据可序列化。

- 16. 在 IMyService 接口的代码隐藏文件中，编写清单 17.20 中给出的代码：

## 清单 17.20：显示 IMyService 接口的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Runtime.Serialization;
using System.ServiceModel;
using System.Text;
namespace DataBindingInSilverlightCS.Web {
// NOTE: You can use the "Rename" command on the "Refactor" menu to change the interface name "IMyService" in both code and config file together.
[ServiceContract]
public interface IMyService {
[OperationContract]
void DoWork();
List<Employee> GetByLastName(string lastname);
}
}
```

- 17. 在输入 IMyService 接口的代码后，切换到 MyService.svc 的代码隐藏文件。

- 18. 在 WCF 服务类 MyService.svc 的代码隐藏文件中，右键单击 IMyService 接口并选择“实现接口→显式实现接口”，如图 17.59 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_942_1.png)

## 图 17.59：实现接口

这会生成一些代码。

17. 在 MyService.svc 类的代码隐藏文件中输入清单 17.21 中给出的代码：

## 清单 17.21：显示 MyService.svc 类代码隐藏文件的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Runtime.Serialization;
using System.ServiceModel;
using System.Text;
namespace DataBindinginSilverlightCS.web {
// NOTE: You can use the "Rename" command on the "Refactor" menu to change the class name "MyService" in code, svc and config file together.
public class MyService : IMyService {
public void DoWork() {
}
#region IMyService Members
public List<Employee> GetByLastName(string lastname) {
// throw new NotImplementedException();
DataBindinginSilverlightCS.web.MyClassDataContext db = new MyClassDataContext();
var data = from p in db.Employees
where p.LastName.Startswith(lastname)
select p;
return data.ToList();
}
#endregion
}
}
```

> 注意
> 您应将 `throw new NotImplementedException();` 语句作为注释，然后在 MyService.svc.cs 文件中添加代码。

现在您需要在添加代码后更新已创建的服务引用。

20. 右键单击 ServiceReference1 并选择“更新服务引用”以更新服务引用，如图 17.60 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_943_0.png)

## 图 17.60：更新服务引用

每次向应用程序添加新方法时，都应在项目中更新服务引用。

21. 切换到 Silverlight 应用程序 DataBindinginSilverlightCS 的 MainPage.xaml 文件以设计 UI。MainPage.xaml 文件的代码在清单 17.22 中给出：

## 清单 17.22：将接口添加到 Silverlight 应用程序

```
<UserControl x:Class="DataBindinginSilverlightCS.MainPage"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d" xmlns:data="clr-namespace:System.Windows.Controls;assembly=System.Windows.Controls.Data">
<StackPanel>
<StackPanel Orientation="Horizontal">
<TextBox x:Name="DataEntry" Width="100" Height="25"/>
<Button Width="50" Height="25" Content="Search" Click="Button_Click"/>
</StackPanel>
<StackPanel Orientation="Horizontal">
<data:DataGrid AutoGenerateColumns="True" Height="300" x:Name="DataGrid" Width="600" />
</StackPanel>
</StackPanel>
</UserControl>
```

22. 在向 Silverlight 应用程序添加 UI 后，将清单 17.23 中给出的代码添加到代码隐藏文件中：

## 清单 17.23：显示 MainPage.xaml 文件代码隐藏文件的代码

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
namespace DataBindinginSilverlightCS
{
public partial class MainPage : UserControl
{
public MainPage()
{
InitializeComponent();
}
private void Button_Click(object sender, RoutedEventArgs e)
{
ServiceReference1.MyServiceClient sc = new DataBindinginSilverlightCS.ServiceReference1.MyServiceClient();
sc.GetByLastNameCompleted += new EventHandler<DataBindinginSilverlightCS.ServiceReference1.GetByLastNameCompletedEventArgs>(sc_GetByLastNameCompleted);
sc.GetByLastNameAsync(DataEntry.Text);
}
void sc_GetByLastNameCompleted(object sender, DataBindinginSilverlightCS.ServiceReference1.GetByLastNameCompletedEventArgs e)
{
DataGrid.ItemsSource = e.Result;
}
}
}
```

添加代码后，更新服务引用并调试应用程序。输出显示如下图 17.61：

![](img/e073a4882197be4ab61103cbe0bcb394_945_0.png)

图 17.61：在 Silverlight 应用程序中检索数据

在此应用程序中，当您从 Employees 表中输入员工的姓氏并单击“搜索”按钮时，与相应员工相关的数据会显示在 DataGrid 控件中。接下来，让我们总结一下本章您所学到的内容。

## 摘要

在本章中，您学习了 Silverlight 技术及其主要特性和架构。您还学习了该技术如何提供跨平台、跨浏览器和跨设备的环境来开发交互式和动态 Web 应用程序。本章进一步讨论了如何安装 Silverlight 3.0 SDK 和 Silverlight 3.0 开发人员运行时环境。在本章中，您学习了如何使用 Visual Studio 2010 中的各种控件（如 AutoCompleteBox、Calendar、DataPager、GridSplitter、MediaElement、Popup 和 TreeView）创建 Silverlight 应用程序。此外，您还学习了如何将 Silverlight 内容托管在 ASP.NET Web 应用程序中。您还学习了如何在 Silverlight 3.0 应用程序中执行数据绑定。

下一章，您将学习 ASP.NET 4.0 Web 服务。

