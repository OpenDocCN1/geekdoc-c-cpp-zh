
```
<Polygon Points="10,110 60,10 110,110" Fill="Blue" Height="55" Canvas.Left="72" Canvas.Top="-7" Width="132" />
<Line X1="11" X2="145" Y1="145" Y2="166" Stroke="Black" StrokeThickness="5" Height="163" Canvas.Left="83" Canvas.Top="110" Width="41" />
<Line X1="145" X2="145" Y1="145" Y2="166" Stroke="Black" StrokeThickness="5" Height="168" Canvas.Left="-23" Canvas.Top="94" Width="151" />
<Line X1="145" X2="145" Y1="145" Y2="166" Stroke="Black" StrokeThickness="5" Height="168" Canvas.Left="-1" Canvas.Top="94" Width="147" />
<Line X1="11" X2="10" Y1="145" Y2="115" Stroke="Black" StrokeThickness="5" Height="158" Canvas.Left="121" Canvas.Top="-52" Width="42" />
<Polyline Points="10,110 6,10 110,110" Stroke="Black" StrokeThickness="4" Height="52" Canvas.Left="209" Canvas.Top="210" Width="50"/>
<Ellipse Canvas.Left="172" Canvas.Top="118" Height="100" Name="ellipse12" Stroke="Black" Width="87">
<Ellipse.BitmapEffect>
<OuterGlowBitmapEffect GlowColor="DarkViolet" />
</Ellipse.BitmapEffect>
</Ellipse>
<Slider Canvas.Left="22" Canvas.Top="304" Height="21" Name="slider1" Width="339" Value="10" Maximum="100"/>
</Canvas>
</Canvas>
</Window>
```

现在，按 F5 键运行 `SimpleBindinginWPF` 应用程序。`SimpleBindinginWPF` 应用程序的输出如图 25.18 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1238_0.png)

图 25.18：在 WPF 中显示简单绑定

在 `SimpleBindinginWPF` 应用程序中，`Canvas` 控件绑定到了 `Slider` 控件。您可以通过移动 `Slider` 控件来前后移动 `Canvas` 控件。

## 在 WPF 中绑定 CLR 对象

要将 WPF 应用程序绑定到 CLR 对象，需要定义应用程序中使用的所有字段的属性。CLR 对象使用 `INotifyPropertyChanged` 接口在 WPF 中实现绑定。

让我们创建一个名为 `BindingtoCLRObject` 的 WPF 应用程序（也可在 CD 上获得）来实现 CLR 对象绑定。执行以下步骤来创建 `BindingtoCLRObject` 应用程序：

1. 创建一个名为 `BindingtoCLRObject` 的 WPF 应用程序。
2. 将清单 25.12 中给出的代码添加到 `MainWindow.xaml` 文件：

### 清单 25.12：显示 `BindingtoCLRObject` 应用程序中 `MainWindow.xaml` 文件的代码

```
<Window x:Class="BindingtoCLRObject.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="MainWindow" Height="300" Width="300">
<Grid Name="nameGrid" Margin="5,5,5,5" >
<Grid.ColumnDefinitions>
<ColumnDefinition Width="30*" />
<ColumnDefinition Width="70*" />
</Grid.ColumnDefinitions>
<Grid.RowDefinitions>
<RowDefinition Height="50" />
<RowDefinition Height="50" />
<RowDefinition Height="50" />
<RowDefinition Height="50" />
<RowDefinition Height="50" />
</Grid.RowDefinitions>
<Label Grid.Column="0" Grid.Row="0">Name:</Label>
<TextBox Width="200" Height="30" Grid.Column="1" Grid.Row="0" Text="{Binding Name}" />
<Label Grid.Column="0" Grid.Row="1">Age:</Label>
<TextBox Width="200" Height="30" Grid.Column="1" Grid.Row="1" Text="{Binding Age}" />
<Label Grid.Column="0" Grid.Row="2">Profile:</Label>
<TextBox Width="200" Height="30" Grid.Column="1" Grid.Row="2" Text="{Binding Profile}" />
<Label Grid.Column="0" Grid.Row="3">EmployeeID:</Label>
<TextBox Width="200" Height="30" Grid.Column="1" Grid.Row="3" Text="{Binding EmployeeID}" />
<Button Margin="5,5,5,5" Grid.Column="1" Grid.Row="4" Name="Button" Click="Button_Click">SHOW DATA</Button>
</Grid>
</Window>
```

3. 在解决方案资源管理器中右键单击 `BindingtoCLObject` 项目名称，然后选择“添加”→“类”，如图 25.19 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1239_0.png)

图 25.19：在 `BindingtoCLObject` 项目中添加类

此时将打开“添加新项”对话框。

4. 在“名称”文本框中输入名称（例如 `Data.cs`），然后单击“添加”按钮。
5. 将清单 25.13 中提供的代码添加到 `Data.cs` 文件中：

### 清单 25.13：显示 `BindingtoCLObject` 应用程序中 `Data.cs` 文件的代码

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace BindingtoCLROBject
{
    class Data
    {
        public Data(string name, string age, string profile, string id, params string[] names)
        {
            this.name = name;
            this.age = age;
            this.profile = profile;
            this.id = id;
            foreach (string Employee in names)
            {
                this.names.Add(name);
            }
        }

        public Data()
            : this("", "", "", "")
        {
        }

        private string name;
        public string Name
        {
            get { return name; }
            set { name = value; }
        }

        private string age;
        public string Age
        {
            get { return age; }
            set { age = value; }
        }

        private string profile;
        public string Profile
        {
            get { return profile; }
            set { profile = value; }
        }

        private string id;
        public string EmployeeID
        {
            get { return id; }
            set { id = value; }
        }

        public override string ToString()
        {
            return name;
        }

        private readonly List<string> names = new List<string>();

        public string[] Names
        {
            get { return names.ToArray(); }
        }
    }
}
```

在清单 25.13 中，创建了具有 `Name`、`Age`、`Profile` 和 `EmployeeID` 这四个属性的`Data`类，同时还创建了一个包含员工姓名的列表。

6. 将清单 25.14 中提供的代码添加到 `MainWindow.xaml.cs` 文件中：

### 清单 25.14：显示 `BindingtoCLROBject` 应用程序中 `MainWindow.xaml.cs` 文件的代码

```
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

namespace BindingtoCLROBject
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        private Data name1 = new Data();

        public MainWindow()
        {
            InitializeComponent();
            nameGrid.DataContext = name1;
        }

        private void Button_Click(object sender, RoutedEventArgs e)
        {
            string message = name1.EmployeeID;
            string caption = name1.Name;
            MessageBox.Show(message, caption);
        }
    }
}
```

7. 按 F5 键运行 `BindingtoCLROBject` 应用程序。运行该应用程序时，会出现包含四个文本框的窗口。在所有文本框中添加数据，然后单击“SHOW DATA”按钮。您可以在图 25.20 中看到 `BindingtoCLROBject` 应用程序的最终输出：

![](img/e073a4882197be4ab61103cbe0bcb394_1241_0.png)

图 25.20：显示消息框

## 在 WPF 中绑定 ADO.NET 对象

要将 WPF 应用程序绑定到 ADO.NET 对象，您需要创建连接字符串，并通过指定控件的 `ItemSource` 和 `ItemTemplate` 属性来绑定控件。接下来创建一个名为 `ADO.NETtoWPF` 的 WPF 应用程序（也可在 CD 上获得），并将清单 25.15 中提供的代码添加到 `MainWindow.xaml` 文件中：

### 清单 25.15：显示 `ADO.NETtoWPF` 应用程序中 `MainWindow.xaml` 文件的代码

```
<Window x:Class="ADO.NETtoWPF.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="MainWindow" Height="300" Width="500">
    <Grid x:Name="Grid1">
        <ListView Name="ListViewEmployeeDetails" Margin="0,0,0,53" ItemTemplate="{DynamicResource EmployeeTemplate}" ItemsSource="{Binding Path=Table}"
HorizontalAlignment="Left" Width="478" Height="172" VerticalAlignment="Bottom">
            <ListView.Background>
                <LinearGradientBrush>
                    <GradientStop Color="Bisque" Offset="0"/>
                </LinearGradientBrush>
            </ListView.Background>
            <ListView.View>
                <GridView>
                    <GridViewColumn Header="Employee ID" DisplayMemberBinding="{Binding Path=EmployeeID}"/>
                    <GridViewColumn Header="First Name" DisplayMemberBinding="{Binding Path=FirstName}"/>
                    <GridViewColumn Header="Last Name" DisplayMemberBinding="{Binding Path=LastName}"/>
                    <GridViewColumn Header="City" DisplayMemberBinding="{Binding Path=City}"/>
                    <GridViewColumn Header="Country" DisplayMemberBinding="{Binding Path=Country}"/>
                </GridView>
            </ListView.View>
        </ListView>
        <Button Height="22" Margin="185,0,183,12" Name="button1" VerticalAlignment="Bottom" Click="button1_Click">Click Me</Button>
```
