
```
Content="False" Margin="15,15" />
<CheckBox IsChecked="{x:Null}" Content="Null" Margin="15,15" />
</StackPanel>
```

### 单选按钮
单选按钮允许在一系列选项中进行单一选择。选项由 `GroupName` 属性决定。在选择其中一个单选按钮后，该组只能通过编程方式完全取消选择。

```
<StackPanel Orientation="Horizontal">
<RadioButton GroupName="RBSample"
IsChecked="true"
Content="Red" Margin="15,15" />
<RadioButton GroupName="RBSample"
Content="White" Margin="15,15" />
<RadioButton GroupName="RBSample"
Content="Blue" Margin="15,15" />
</StackPanel>
```

### 滑块
滑块控件是一个范围输入控件。类似于 `ProgressBar`，该控件接受 `Minimum`、`Maximum` 和 `Interval` 值。此外，您可以指定显示刻度、位置和刻度频率。*刻度？* 它们是显示在滑块上的值线。

```
<Slider Interval="1" Minimum="1" Maximum="10" IsSnapToTickEnabled="True"
TickPlacement="BottomRight" TickFrequency="1"/>
```

### 日期选择器
Visual Studio 2012 中新增的 `DatePicker` 控件通过将 `TextBox` 与 `Calendar` 控件结合，提供了一种简洁的方法来获取（或显示）日期信息。其众多选项中包括选择多个日期以形成日期范围的能力。

```
<DatePicker />
```

### 日历
Visual Studio 2012 中也新增了 `Calendar` 控件。`Calendar` 与 `DatePicker` 的区别在于 `Calendar` 控件始终处于全显示模式，而 `DatePicker` 的默认外观类似于文本框。

```
<Calendar />
```

### 按钮
好吧，你抓到我了。`Button` 控件并不真正适合本节中的其他控件，因为它更像是一个操作控件。按钮响应用户的点击。以下代码展示了 Button 在窗口的代码隐藏文件中通过事件处理程序实现。在第 4 章中，你将了解到如何使用命令来获得对按钮的更多控制，但目前，点击按钮仅显示“Hello World。”

```
<Button Content="Click Me" Click="Button_Click" Width="60"/>
private void Button_Click(object sender, RoutedEventArgs e)
{
    MessageBox.Show("Hello World");
}
```

![](img/80ff26f06fc9ab951e1cd4257b867366_621_0.png)

图 2-18：
所有基本输入控件。

## 基于列表的控件

基于列表的控件（也称为项控件）增加了极大的灵活性。正如我在本书迷你书第 1 章中所讨论的，基于列表的控件不再需要依赖数据技巧或其他魔法来使内容对用户有意义，而是可以被模板化以显示有关所包含项目的更多详细信息。

数据绑定在本书迷你书第 3 章中有详细讨论，但控件如果没有要显示的内容则不会执行任何操作。ComboBox、ListBox 和 DataGrid 控件示例将绑定到表示 Person 的类。IList<Person>。请参阅 Person 类：

```
public class Person
{
    public string Name { get; set; }
    public string Address { get; set; }
    public string City { get; set; }
    public string State { get; set; }
    public string Zip { get; set; }
}
```

以下是基于列表的控件：

- ComboBox 和 ListBox：下面的示例中 ListBox 和 ComboBox 使用 DataTemplate 来创建所包含项目的显示。两个控件的主要区别在于 ComboBox 显示单个项目并带有下拉选择器（参见图 2-18），而 ListBox 显示允许空间内的整个项目列表并滚动其余部分（参见图 2-19）。ComboBox 可以设置为启用选择列表中不存在的项目，以及编辑列表中的项目。

![](img/80ff26f06fc9ab951e1cd4257b867366_622_0.png)

图 2-19 和图 2-20 中显示的 ComboBox 和 ListBox 在 DataTemplate 标签之间使用完全相同的 XAML，因此仅显示 ComboBox XAML。

以下 XAML 若没有代码隐藏文件中的额外代码支持将不会产生正确输出。第 3 行中的 {Binding} 元素需要一些代码支持。

### 列表 2-15：ComboBox XAML

```xml
<ComboBox Margin="5,0" HorizontalAlignment="Stretch" HorizontalContentAlignment="Stretch" ItemsSource="{Binding Path=People}">
    <ComboBox.ItemTemplate>
        <DataTemplate>
            <Border HorizontalAlignment="Stretch" BorderBrush="AliceBlue" BorderThickness="1">
                <Grid HorizontalAlignment="Stretch">
                    <Grid.RowDefinitions>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                    </Grid.RowDefinitions>
                    <Grid.ColumnDefinitions>
                        <ColumnDefinition Width="Auto"/>
                        <ColumnDefinition Width="*"/>
                        <ColumnDefinition Width="*"/>
                    </Grid.ColumnDefinitions>
                    <TextBlock Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="3" Margin="5,0" Text="{Binding Name}"/>
                    <TextBlock Grid.Row="1" Grid.Column="0" Grid.ColumnSpan="3" Margin="5,0" Text="{Binding Address}"/>
                    <TextBlock Grid.Row="2" Grid.Column="0" Margin="5,0" Text="{Binding City}"/>
                    <TextBlock Grid.Row="2" Grid.Column="1" Margin="5,0" Text="{Binding State}"/>
                    <TextBlock Grid.Row="2" Grid.Column="2" Margin="5,0" Text="{Binding Zip}"/>
                </Grid>
            </Border>
        </DataTemplate>
    </ComboBox.ItemTemplate>
</ComboBox>
```

![](img/80ff26f06fc9ab951e1cd4257b867366_622_1.png)

### 图 2-19：ComboBox。

![](img/80ff26f06fc9ab951e1cd4257b867366_623_0.png)

- TreeView：TreeView 是一个分层 ItemsControl，很像 Windows 资源管理器。节点（或分支）可以展开或收缩，为任何多级数据提供良好的用户界面。（参见图 2-21。）

列表 2-16 中显示的示例（取自 MSDN）使用硬编码数据，但通过简单的分层模板，树视图可以像其他任何控件一样绑定。

与这里的 ComboBox 和 DataGrid 示例不同，以下 TreeView XAML 无需额外代码支持即可正常工作。

### 列表 2-16：TreeView XAML。

```
    <TreeView Name="myTreeViewEvent" >
      <TreeViewItem Header="Employee1" IsSelected="True">
        <TreeViewItem Header="Jesper Aaberg"/>
        <TreeViewItem Header="Employee Number">
          <TreeViewItem Header="12345"/>
        </TreeViewItem>
        <TreeViewItem Header="Work Days">
          <TreeViewItem Header="Monday"/>
          <TreeViewItem Header="Tuesday"/>
          <TreeViewItem Header="Thursday"/>
        </TreeViewItem>
      </TreeViewItem>
      <TreeViewItem Header="Employee2">
        <TreeViewItem Header="Dominik Paiha"/>
        <TreeViewItem Header="Employee Number">
          <TreeViewItem Header="98765"/>
        </TreeViewItem>
        <TreeViewItem Header="Work Days">
          <TreeViewItem Header="Tuesday"/>
          <TreeViewItem Header="Wednesday"/>
          <TreeViewItem Header="Friday"/>
        </TreeViewItem>
      </TreeViewItem>
    </TreeView>
```

![](img/80ff26f06fc9ab951e1cd4257b867366_623_1.png)

### DataGrid
与 DatePicker 和 Calendar 控件一起，.NET 4 中也新增了 DataGrid。（参见图 2-22。）在 WPF 早期版本中 conspicuously 缺失的此控件是 WPF 工具包的一部分，该工具包是一个非同步发布，至今仍是 WPF 信息的极佳资源。

DataGrid 有五个基本列：

- DataGridTextColumn：用于文本
- DataGridCheckBoxColumn：用于布尔值
- DataGridComboBoxColumn：用于列表项
- DataGridHyperlinkColumn：用于显示链接
- DataGridTemplateColumn：用于设计自定义列

DataGrid 可以根据其绑定的数据自动生成列（如示例中所示）。然后它使用反射根据数据确定最佳列类型。

以下 XAML 若没有代码隐藏文件中的额外代码支持将不会产生正确输出。第 3 行中的 {Binding} 元素需要一些代码支持。

```
<DataGrid HorizontalAlignment="Stretch" VerticalAlignment="Stretch"
AutoGenerateColumns="True" ItemsSource="{Binding People}">
</DataGrid>
```

![](img/80ff26f06fc9ab951e1cd4257b867366_624_0.png)

### 图 2-22：一个简单的数据网格。

![](img/80ff26f06fc9ab951e1cd4257b867366_624_1.png)
