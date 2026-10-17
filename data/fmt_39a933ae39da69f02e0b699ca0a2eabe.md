
列表 21.15 显示了用于准备数据的接口代码。现在，将列表 21.16 中提供的代码添加到 `MainWindow.xaml`：

列表 21.16：显示 `ADONETWPF` 中 `MainWindow.xaml.cs` 代码

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;
using System.Data;
using System.Data.SqlClient;
namespace ADONETWPF
{
    /// <summary>
    /// mainwindow.xaml 的交互逻辑
    /// </summary>
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }
        private void button_Click(object sender, RoutedEventArgs e)
        {
            SqlConnection myconnection = new SqlConnection();
            SqlDataAdapter myadapter = new SqlDataAdapter();
            SqlCommand cmd = new SqlCommand("SELECT EmployeeID, FirstName, LastName, City FROM Employees");
            myconnection.ConnectionString = "Data Source=.;Initial Catalog=Northwind;Integrated Security=True";
            myadapter.SelectCommand = cmd;
            DataSet ds = new DataSet();
            myadapter.Fill(ds);
            listViewDetails.ItemsSource = ds.Tables[0].DefaultView;
            myconnection.Close();
        }
    }
}
```

![](img/17af790174c480761404624aeed9b30b_1017_0)

| EmployeeID | Name | LastName | City |
|---|---|---|---|
| 1 | Thomas | Fuller | Seattle |
| 2 | Andrew | Thomas | Tacoma |
| 3 | Janet | Peacock | Kirkland |
| 4 | Margaret | Buchanan | Richmond |
| 5 | Steven | Suyama | London |
| 6 | Michael | King | London |
| 7 | Robert | Leering | London |

# WPF 中的 XML 对象

`XmlDataProvider` 类配合 XPath 用于与 XML 数据绑定对象。通过以下步骤创建 `BindingObject` 应用程序以绑定你的数据：

- 1. 创建名为 `BindingObject` 的 WPF 应用程序。
- 2. 使用记事本通过列表 21.17 中的代码创建 XML 文件并将其命名为 `Books.xml`。

列表 21.17：`Books` 的代码

```xml
<?xml version="1.0" encoding="utf-8"?>
<Book>
  <Title>C# 2012</Title>
  <Publisher>Dreamtech</Publisher>
  <Author>AgentSolutions</Author>
</Book>
```

- 5. 按 `F5` 键查看 `BindingObject` 应用程序的输出，如图 21.23 所示。

![](img/17af790174c480761404624aeed9b30b_1019_0)

## WPF 中绑定 XML

### 从 XML 文件检索数据

你也可以使用 `DependencyObject` 构造函数构建 WPF 对象。`DependencyObject` 构造函数的主要作用是获取属性值并提供更改通知。在 WPF 中使用 `DependencyObject` 构造函数进行绑定时，目标属性是一个依赖属性。

为了查看 `DependencyObject` 构造函数的功能，让我们创建一个名为 `DependencyObject` 的 WPF 应用程序，并将列表 21.19 中提供的代码添加到 `MainWindow.xaml`：

列表 21.19：`DependencyObject` 中 `MainWindow.xaml` 代码

```xml
<window x:Class="DependencyObject.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        title="MainWindow" Height="300" Width="Name">
  <Grid Height="28" Margin="64,30,94,0" Name="Label" VerticalAlignment="Top">
    <Label FontSize="15" FontWeight="Bold">choose a color:</Label>
    <StackPanel VerticalAlignment="Top" Margin="47,65,53,0" Name="combobox1">
      <ComboBox>
        <ComboBoxItem>RED</ComboBoxItem>
        <ComboBoxItem>BLUE</ComboBoxItem>
        <ComboBoxItem>YELLOW</ComboBoxItem>
        <ComboBoxItem>BLACK</ComboBoxItem>
      </ComboBox>
    </StackPanel>
    <Canvas Margin="89,0,89,82" VerticalAlignment="Bottom">
      <Canvas.Background>
        <Binding ElementName="combobox1" Path="SelectedItem.Content"/>
      </Canvas.Background>
    </Canvas>
  </Grid>
</window>
```

在列表 21.19 中，数据绑定由 `ComboBox` 控件和 `Canvas` 控件执行。`DependencyObject` 应用程序的输出见图 21:24。

## 解决方案

![](img/17af790174c480761404624aeed9b30b_1020_0.png)

图 21.24：`ComboBox`控件的绑定属性

在此应用程序中，`Canvas`控件的背景颜色会更改为在`ComboBox`控件中选中的颜色。

## 在 WPF 中绑定 Web 服务

现在，让我们创建一个应用程序来学习如何将 WPF 应用程序绑定到 Web 服务。在 `DataBindingWebService` 文件夹中创建一个名为 `MyWebService` 的 ASP.NET Web 服务应用程序。

执行以下步骤将 WPF 应用程序绑定到 Web 服务：

- 1. 创建一个名为 `DataBindingWebService` 的文件夹。
- 2. 创建一个名为 `MyWebService` 的 ASP.NET 空网站（Empty Web Site）。
- 3. 在解决方案资源器的 `MyWebService` 站点中添加一个 Web 服务 `MyWebService.asmx`。
- 4. 将列表 21.20 中提供的代码添加到 `MyWebService.asmx` 文件：

```
Listing 21.20: 显示 MyWebService.asmx 文件的代码
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Services;
using System.Data.SqlClient;
using System.Data.Component;
/*
// MyWebService 的摘要描述
*/
[WebServiceBinding(Namespace="http://tempuri.org/")]
[MyWebServiceBinding(ConfigName = "wProfiles.BasicProfile_1")]
// 要允许通过脚本使用 ASP.NET AJAX 调用此 Web 服务，请取消下行的注释：
// [System.Web.Services.ScriptService]
public class MyWebService : System.Web.Services.WebService
{
    // 如果使用设计组件，请取消下行的注释
    // [DataSetComponent]
    public DataSet GetDataSet()
    {
        System.Data.SqlConnection connection1 = new System.Data.SqlClient.SqlConnection();
        connection1.ConnectionString = "Data Source=DEBOLENA-PC;Initial Catalog=Northwind;Integrated Security=True";
        string select = "SELECT EmployeeID, FirstName, LastName, City, Country FROM Employees";
        SqlDataAdapter adapter = new SqlDataAdapter(select, connection1);
        DataSet ds = new DataSet();
        adapter.Fill(ds);
        return (ds);
    }
}
```

# 第 21 章：Windows Forms 和 WPF 中的数据绑定

- 5. 按 `F5` 键运行应用程序。`MyWebService` 应用程序的输出如图 21.25 所示：

![](img/17af790174c480761404624aeed9b30b_1021_0.png)

图 21.25：Web 服务文件的输出

创建 Web 服务后，执行以下步骤创建 WPF 应用程序。

- 6. 在 `DataBindingWebService` 文件夹中创建一个名为 `MyApp` 的 WPF 应用程序。
- 7. 将列表 21.1 中的代码添加到 `MainWindow.xml` 文件。

列表 21.1：显示 `MyWpf` 应用程序中 `MainWindow.xml`文件的代码

```
<window x:class="main.MainWindow"
      xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
      title="MainWindow" Height="400" width="600">
  <Grid name="Grid">
    <ListView x:Name="ListViewdetails" Margin="61,70,39,120">
      <ListView.ItemTemplate>
        <DataTemplate DataType="Resource EmployeeTemplate">
          <StackPanel>
            <LinearGradientBrush>
              <GradientStop Color="Bisque" Offset="0"/>
            </LinearGradientBrush>
          </StackPanel>
        </DataTemplate>
      </ListView.ItemTemplate>
      <ListView.View>
        <Grid>
          <GridColumn Header="Employee ID" DisplayMemberBinding="{Binding Path=ID}"/>
          <GridColumn Header="First Name" DisplayMemberBinding="{Binding Path=FirstName}"/>
          <GridColumn Header="Last Name" DisplayMemberBinding="{Binding Path=LastName}"/>
          <GridColumn Header="City" DisplayMemberBinding="{Binding Path=City}"/>
          <GridColumn Header="Country" DisplayMemberBinding="{Binding Path=Country}"/>
        </Grid>
      </ListView.View>
    </ListView>
    <Button Height="40" Margin="61,161,154,33" Name="button1" VerticalAlignment="Bottom" click="Button1_Click">Button</Button>
  </Grid>
</window>
```

## 解决方案

```
<Label Height="28" HorizontalAlignment="Left" Margin="11,10,0,0" Name="label1" VerticalAlignment="Top" Width="142" FontSize="13">来自 Web 服务的数据</Label>
</Grid>
```

在创建应用程序界面后，你需要将 `MyWebService` Web 服务的引用添加到 WPF 应用程序中。

- 8. 在解决方案资源器中右键点击解决方案名称 `MyWpf`，并选择“添加>现有网站（Add>Existing Web Site）”，如图 21.26 所示：

![](img/17af790174c480761404624aeed9b30b_1022_0.png)

图 21.26：添加网站

- 9. 在添加服务对话框中浏览并选择 `MyWebService`。
- 10. 在解决方案资源器中右键点击 `MyWpf` 项目，选择“添加引用（Add Reference）”，如图 21.27 所示：

![](img/17af790174c480761404624aeed9b30b_1023_0.png)

图 21.27：添加引用

# 第 21 章：Windows Forms 和 WPF 应用程序中的绑定

- 11. 点击对话框中的确定。这将在应用程序中定位服务。查看图 21.28：

![](img/17af790174c480761404624aeed9b30b_1024_0.png)

图 21.28：定位服务

- 12. 将 21.22 中的代码添加到 `MainWindow.cs`。

列表 21.22：`MyWpf` 应用程序中 `MainWindow.cs` 的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Navigation;
```
