

如清单5.10所示，**MainWindow.xaml**文件与**UsingXAML**应用程序中的**MainWindow.xaml**文件相同，唯一不同的是用于**Window.xaml**文件中**Ellipse**控件的**Binding**属性。在本例中，我们通过代码实现绑定。

- 10. 将清单5.11中给出的代码添加到**MainWindow.xaml.cs**文件中：

### 清单5.11：使用代码后置文件实现数据绑定

```csharp
private void Window_Loaded(object sender, RoutedEventArgs e)
{
    Binding bnd = new Binding();
    bnd.Source = McListBox;
    bnd.Path = new PropertyPath("SelectedItem.Content");
    Ellipse1.SetBinding(Ellipse.FillProperty, bnd);
}
```

在清单5.11中，首先创建了一个**Binding**类的新对象，然后使用**Source**属性设置绑定源。同样，**Path**属性用于设置绑定源的属性，最后使用**SetBinding**属性将目标控件绑定到源。

- 11. 按F5键执行**UsingCodeBehindFile**应用程序。输出出现（图C#-5.23）。
- 12. 从“从下列列表中选择颜色”列表框中选择红色（图C#-5.24）。

椭圆被填充为红色（图C#-5.24）。

![](img/9862a98a1a2d3bb14334137965a1ec60_396_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_396_1.png)

## 使用Path属性

您还可以使用**Path**属性来指定希望在WPF应用程序中绑定的源值。例如，您可以使用**Path**属性将**TextBox**控件的**Text**属性绑定到数据元素。您还可以使用**Path**属性将控件的属性绑定到数据库的特定字段，如下面的代码片段所示。

```text
Path=Employees.FirstName
```

在前面的代码片段中，我们使用**Path**属性绑定了**Employees**表中的**FirstName**列。

执行以下步骤，通过创建名为**UsingPathProperty**的Windows窗体应用程序（也可在CD上获取），在WPF中使用**Path**属性实现数据绑定：

- 1. 打开**Microsoft Visual Studio 2010**。
- 2. 从菜单栏中选择**文件→新建→项目**。出现**新建项目**对话框。
- 3. 在**新建项目**对话框的**已安装模板**窗格中选择**Visual C#→Windows**。
- 4. 在**新建项目**对话框的中间窗格中选择**WPF应用程序**。
- 5. 在**名称**文本框中输入**UsingPathProperty**作为应用程序的名称。
- 6. 在**位置**组合框中输入要保存应用程序的完整路径。
- 7. 单击**新建项目**对话框中的**确定**按钮将其关闭。**UsingPathProperty**应用程序已创建。
- 8. 使用**Title**属性将**MainWindow**的标题设置为**使用Path属性进行绑定**。
- 9. 将清单5.12中给出的代码添加到**MainWindow.xaml**文件中：

### 清单5.12：使用Path属性实现数据绑定

```xml
<Window x:Class="UsingPathProperty.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Binding using the Path Property" Height="222" Width="300">
    <Grid DataContext="{Binding ElementName=mcListBox
                                  Path=SelectedItem}">
        <TextBlock Margin="10,10,10,121" FontWeight="Bold">Pick a color from below list</TextBlock>
        <ListBox Name="mcListBox" Height="100" Width="100"
                 Margin="28,46,0,0" HorizontalAlignment="Left"
                 VerticalAlignment="Top">
            <ListBoxItem>Orange</ListBoxItem>
            <ListBoxItem>Green</ListBoxItem>
            <ListBoxItem>Blue</ListBoxItem>
            <ListBoxItem>Gray</ListBoxItem>
            <ListBoxItem>LightGray</ListBoxItem>
            <ListBoxItem>Red</ListBoxItem>
        </ListBox>
        <Ellipse Height="100" Name="ellipse1" DataContext="{Binding
                 ElementName=mcListBox}" Stroke="Black" Margin="0,46,31,0"
                 VerticalAlignment="Top" HorizontalAlignment="Right" Width="116">
            <Ellipse.Fill>
                <Binding Path="SelectedItem.Content"/>
            </Ellipse.Fill>
        </Ellipse>
    </Grid>
</Window>
```

在清单5.12中，**Binding**属性用于将Ellipse控件的**Fill**属性绑定到ListBox控件的选中值。在代码中，请注意Ellipse控件的**DataContext**属性被设置为绑定定义。接下来，使用**ElementName**属性将ListBox控件与Ellipse控件绑定。然后，将ListBox控件的选中值传递给Ellipse控件内部**Binding**元素的**Path**属性。这样，Ellipse控件就与ListBox控件绑定了。

- 10. 按F5键执行**UsingPathProperty**应用程序。输出出现（图C#-5.25）。
- 11. 从“从下列列表中选择颜色”列表框中选择蓝色。椭圆被填充为蓝色（图C#-5.26）。

![](img/9862a98a1a2d3bb14334137965a1ec60_397_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_397_1.png)

图C#-5.25

图C#-5.26

## WPF中的绑定源

在数据绑定过程中，源指的是从中获取数据的对象。WPF支持四种类型的绑定源：公共语言运行时（CLR）对象、ADO.NET对象、可扩展标记语言（XML）数据和**DependencyObject**。这些绑定源允许您将WPF控件绑定到任何CLR对象、ADO.NET对象或XML对象。

在本节中，您将了解WPF中两种常见的绑定源：

- CLR对象
- ADO.NET对象

让我们详细讨论这些内容。

### 绑定到CLR对象

在WPF中，您可以使用任何CLR对象的公共属性或子属性将控件绑定到数据。WPF中的绑定对象使用CLR来检索属性的值。当您在WPF中使用CLR对象进行数据绑定时，应实现`INotifyPropertyChanged`接口。该接口帮助您在源属性更改时更新目标，从而确保绑定过程中使用的数据是最新的。您还可以使用`UpdateTarget()`方法更新目标属性，以提供适当的更改通知。

执行以下步骤，通过创建名为**BindingtoCLRObject**的Windows窗体应用程序（也可在CD上获取）来实现CLR对象绑定：

- 1. *打开* Microsoft Visual Studio 2010。
- 2. *从*菜单栏中选择**文件→新建→项目**。出现**新建项目**对话框。
- 3. 在**新建项目**对话框的**已安装模板**窗格中*选择* Visual C#→**Windows**。
- 4. 在**新建项目**对话框的**中间**窗格中*选择***WPF应用程序**。
- 5. 在**名称**文本框中*输入***BindingtoCLRObject**作为应用程序的名称。
- 6. 在**位置**组合框中输入要保存应用程序的完整路径。
- 7. *单击***新建项目**对话框中的**确定**按钮将其关闭。**BindingtoCLRObject**应用程序已创建。
- 8. 使用**Title**属性*将***MainWindow**的标题设置为**绑定到CLR对象**。
- 9. *将*清单5.13中给出的代码添加到**MainWindow.xaml**文件中：

### 清单5.13：创建BindingtoCLRObject应用程序的用户界面

```xml
<Window x:Class="BindingtoCLRObject.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Binding to a CLR Object" Height="300" Width="300">
    <Grid Name="myGrid" Margin="5,5,5,5">
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="30%" />
            <ColumnDefinition Width="70%" />
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
        <Button Margin="5,5,5,5" Grid.Column="1" Grid.Row="4"
                Name="Button" Click="Button_Click">SHOW DATA</Button>
    </Grid>
</Window>
```

将清单5.13中给出的代码添加到**MainWindow.xaml**文件中后，为您的应用程序添加一个类。

- 10. 在**解决方案资源管理器**中*右键单击*应用程序名称，然后从上下文菜单中选择**添加→类**来添加一个类，如图C#-5.27所示：

