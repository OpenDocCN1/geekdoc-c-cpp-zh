

# 584 数据的编辑、验证、转换与可视化

BindingOperations 是 WPF 提供的一个辅助类。它包含静态方法，使你能够在应用程序元素上添加和清空数据绑定定义。

以下代码展示了如何定义 `Binding` 对象，并将绑定赋值给标签的 Content：

```csharp
private void GenerateData() {
    Car car1 = new Car() { Make = "Athlon", Model = "XYZ" };

    Binding makeBinding = new Binding("Make");
    makeBinding.Mode = BindingMode.OneTime;
    BindingOperations.SetBinding(lblMake,
    Label.ContentProperty, makeBinding);

    Binding modelBinding = new Binding("Model");
    modelBinding.Mode = BindingMode.OneTime;
    BindingOperations.SetBinding(lblModel,
    Label.ContentProperty, modelBinding);

    this.DataContext = car1;
}
```

运行应用程序并观察其运行方式与你使用 XAML 定义绑定的方式相同。

依赖属性通常以后缀 "Property" 来定义，但你只有在浏览 MSDN 文档和通过代码访问它们时才能看到它们。在 XAML 中，你通过去掉名称中的 "Property" 后缀来指定依赖属性标记。

# 数据的编辑、验证、转换与可视化

在前面的节中，你领略了绑定语法并看到数据出现在屏幕上。本节基于这些知识，向你展示一个更新数据的简单示例，包括从用户界面元素更新数据，以及根据后台对象的变化更新用户界面。

完整的解决方案可以在 Web 上的 BindingSample2 项目获取。

要实现这一点，请按照以下步骤操作：

- 1. 创建一个新的 WPF 项目并命名为 BindingSample2。

让我们复用在 BindingSample1 中创建的 Car 类（注意：如果复制粘贴此类，请确保将类的命名空间更改为 BindingSample2。）

在此示例中，你将在 TextBox 控件中显示 Car 对象（DataContext）的型号和代码。这允许你编辑 Car 属性的值。你还将使用 `TwoWay` 绑定模式，以便从用户界面进行的更改将反映在 Car 对象中，而从后台代码对 Car 的任何更改将反映在用户界面上。

| 第5卷 | 第3章 | WPF 中的数据绑定 |

- 2. 定义两个按钮，一个显示包含 DataContext 当前值的消息框，另一个通过后台代码更改 DataContext。

在 MainWindow.xaml 中，将 Grid 替换为以下内容：

```xml
<Grid>
    <Grid.ColumnDefinitions>
        <ColumnDefinition/>
        <ColumnDefinition/>
    </Grid.ColumnDefinitions>
    <Grid.RowDefinitions>
        <RowDefinition/>
        <RowDefinition/>
    </Grid.RowDefinitions>
    <Grid Column="0">
        <StackPanel Orientation="Horizontal" Row="0" Column="0">
            <TextBox x:Name="lblMake" VerticalAlignment="Top"
                     Text="{Binding Make, Mode=TwoWay}" 
                     Width="200" Height="25" />
        </StackPanel>
        <StackPanel Orientation="Horizontal" Row="0" Column="1">
            <TextBox x:Name="lblModel" VerticalAlignment="Top"
                     Text="{Binding Model, Mode=TwoWay}" 
                     Width="200" Height="25" />
        </StackPanel>
        <Button x:Name="btnShowDataContextValue"
                Click="btnShowDataContextValue_Click"
                Content="Show CurrentContext Value"
                Row="1" Column="0" />
        <Button x:Name="btnChangeDataContextValue"
                Click="btnChangeDataContextValue_Click"
                Content="Change Data Context with Code-Behind"
                Row="1" Column="1" />
    </Grid>
</Grid>
```

- 3. 在后台代码 MainWindow.xaml.cs 中，添加以下方法：

```csharp
private void GenerateData()
{
    Car car = new Car() { Make = "Athlon", Model = "XYZ" };
    this.DataContext = car;
}

private void btnShowDataContextValue_Click(object sender,
    RoutedEventArgs e)
{
    Car dc = this.DataContext as Car;
    MessageBox.Show("Car Make: " + dc.Make + "\nCar Model: " + dc.Model);
}

private void btnChangeDataContextValue_Click(object sender,
    RoutedEventArgs e)
{
    Car dc = this.DataContext as Car;
    dc.Make = "Changed Make";
    dc.Model = "Changed Model";
}
```

- 4. 在 MainWindow() 中，确保在调用 `InitializeComponents()` 之后立即调用 `GenerateData()` 方法。

- 5. 运行此应用程序。DataContext 中的值正确显示在 TextBox 控件中。可以更改 TextBox 中的值。例如，将 Make 值更改为 Athlon，将型号更改为 XYZ。完成编辑后，点击 Show CurrentDataContext Value 按钮。你对 TextBox 中值所更改现在已反映在底层 DataContext 中（参见图 3-2）。

![](img/36596fb11aa4233d5cab0d6ddd1d82e_611_0.png)

图 3-2：使用 TwoWay 绑定模式编辑数据。

- 6. 点击 OK 按钮消除消息框。如果你查看 Change Data Context With Code-Behind 按钮的 Click 事件处理程序（btnChangeDataContextValue_Click），你会注意到 DataContext 对象的属性分别变为 Changed Make 和 Changed Model。

# 数据的编辑、验证、转换与可视化

- 7. 点击 Change Data Context With Code-Behind 按钮。

嗯。什么都没有发生。怎么回事？如果你点击 Show CurrentDataContext Value 按钮，你将看到已更改的属性。因为你使用的是 TwoWay 绑定，你的设置应该会自动更新你的 UI，对吧？错了！这是 WPF 的另一个特性，INotifyPropertyChanged 的上下文中起了作用。

INotifyPropertyChanged 是一个简单的接口，允许你的对象引发事件，通知其订阅者（即你的应用程序）属性值发生了变化。

对于集合，类似的接口是 INotifyChanged。WPF 提供了一个名为 ObservableCollection<T> 的泛型类，它实现了 INotifyChanged。当你创建的集合实现了 INotifyChanged 时，你需要确保集合中的对象也实现了 INotifyPropertyChanged。

INotifyPropertyChanged 接口包含一个必须实现的事件Changed，其参数是发生变化的的对象以及属性的名称。

- 8. 打开你的类，实现 INotifyPropertyChanged 接口。

该接口位于 System.ComponentModel 命名空间（在类顶部使用 System.ComponentModel;）。实现此接口为 Car 类增加了以下事件：

```csharp
public event PropertyChangedEventHandler PropertyChanged;
```

为了通知 Car 对象发生的更改，每当属性值变化时必须触发 PropertyChanged 事件。

- 9. 为了在 Car 类中实现这一点，创建一个名为 NotifyPropertyChanged 的辅助方法，它接收一个字符串属性并为对象实例和属性名称触发 PropertyChanged 事件：

```csharp
private void NotifyPropertyChanged(string propertyName)
{
    if (PropertyChanged != null)
    {
        this.PropertyChanged(this,
            new PropertyChangedEventArgs(propertyName));
    }
}
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e_612_0.png)

| 第5卷 | 第3章 | WPF 中的数据绑定 |

- 10. 现在你需要修改 Car 对象上每个公共属性的 Set 方法，每当属性值变化时调用 NotifyPropertyChanged 辅助方法。如下所示编辑公共属性：

```csharp
public string Make
  get { return _make; }
  set {
    if (_make != value)
      _make = value;
      NotifyPropertyChanged("Make");
    }
  }
```

```csharp
public string Model
  get { return _model; }
  set {
    if (_model != value)
      _model = value;
      NotifyPropertyChanged("Model");
    }
  }
```

- 11. 再次运行应用程序。

现在当你点击 Change Data Context with Code-Behind 按钮时，更改的值会自动反映在 TextBox 元素中。这是由于 TwoWay 绑定模式以及 INotifyPropertyChanged 实现的共同作用（参见图 3-3）。

图 3-3：带有 INotifyPropertyChanged 的 TwoWay 绑定。

![](img/36596fb11aa4233d5cab0d6ddd1d82e_612_1.png)

