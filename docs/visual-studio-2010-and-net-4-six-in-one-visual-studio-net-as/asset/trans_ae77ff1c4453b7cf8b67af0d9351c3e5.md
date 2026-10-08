

# 列表 8-7 (继续)

```c
{
  if (PropertyChanged != null)
    PropertyChanged(this, new PropertyChangedEventArgs(propertyName));
  }

  public DateTime CurrentTime
{
    get { return DateTime.Now; }
  }

  public event PropertyEventHandler PropertyChanged;
}
```

代码文件 [ViewModel.cs] 可在 Wrox 下载。

起初，Clock示例应用程序似乎有点过于复杂。毕竟，你完全简单地在后置代码中创建一个定时器，并在定时器触发时更新 TextBlock 的上下文。然而，在处理复杂的主从关系和多个对象时，分离数据对象和数据绑定的优势变得显而易见。

> 还有一种流行的架构模式称为模型-视图-模型（MVVM），它高度依赖于数据绑定。MVVM 允许 UI 逻辑测试以及 UI 与应用程序逻辑的完全分离。深入讨论 MVVM 超出了本书的范围。如果你计划使用 Silverlight 或 WPF 开发严肃的应用程序，绝对应该熟悉这种模式。

使用 XAML 是我们描述对象层次结构的方式；在这里，你使用 XAML 特性来创建 ClockViewModel 类的实例，并将其分配给 UserControl 的 DataContext 属性。XML 命名空间 local 指包含 ClockViewModel 的程序集。当 XAML 被 Silverlight 运行时执行时，会创建 ClockViewModel 对象，该对象反而启动它的定时器。

Data 属性沿视觉树向下继承（但可以在任何元素上进行更改）。这意味着 LayoutRoot 网格及其所有子元素的 DataContext 都被设置为同一个 ClockViewModel 实例。DataContext 也被用于显示时间的 TextBlock 继承。

TextBlock 的 Text 属性包含一个数据绑定：Text="Binding Path=CurrentTime"。这将 Text 属性连接到 DataContext 的 CurrentTime 属性。在定时器的每次滴答中，PropertyChanged 事件都会被触发。INotifyPropertyChanged 接口（它仅定义了 PropertyChanged 事件）是 Silverlight 运行时学习数据绑定源变化的方式。触发 PropertyChanged 事件会指示 Silverlight 运行时更新所有绑定到相关数据对象的属性。从现在起，显示是自动的，并由 Silverlight 运行时处理。

`Binding` 子句有几个附加选项，可以使数据绑定更强大。一些最重要的选项包括：

- Converter（转换器）：这允许你创建自定义显示逻辑，并更轻松地将任何输入数据转换为底层字段的内容。（例如，如果你想在 TextBox 中显示和输入大小为 "24x48" 的属性，你可以实现 IValueConverter 并编写代码。）
- Mode（模式）：可以设置为 OneTime（一次性，不再更新）、OneWay（单向，默认）和 TwoWay（双向）。
- Source（源）：指定绑定的数据源。可以省略 Source，在这种情况下，DataContext 将是源对象，就像 Clock 示例一样。
- Path（路径）：可以省略简写形式。Clock 示例中的绑定表达式也可以写为 Text="{Binding CurrentTime}"。

# 两个元素之间的数据绑定

你可以绑定两个 UI 元素。这里有一个将 TextBox 绑定到 Slider 的小型示例：

```xml
<Slider HorizontalAlignment="Center" xName="slider1" Width="100"
  Margin="0,109,0,0" VerticalAlignment="Top" />
<TextBox HorizontalAlignment="Center" VerticalAlignment="Center"
  Binding="Path=Value, Mode=TwoWay, ElementName=slider1, ValidatesOnError=True" Width="40" />
```

如你所见，当你移动 Slider，TextBox 就会自动更新。同样，你可以在 TextBox 中输入一个数字，Slider 随之更新。这种自动绑定是通过依赖属性实现的，而不是用于业务对象的 INotifyPropertyChanged 接口。依赖属性本质上是能够参与数据绑定、样式和动画的控件属性，并由 Silverlight（或 WPF）运行时管理。

绑定在 TextBox 失去焦点时触发。Silverlight 中的输入控件已准备好显示验证错误。如果 TextBox 中的值无效（例如包含异常），则会抛出异常。将 Binding 的 ValidatesExceptions 属性设置为 True，异常将以友好的方式显示，如图 8-15 所示。进一步的绑定验证选项包括 ValidatesOnDataErrors 和 ValidatesOnNotifyErrors。

![](img/b5597c749e848b27b0d305153ae1610_366_0.png)

图 15：显示验证错误的 TextBox

# 对象列表的数据绑定

大多数时候的任务是同时显示多个对象——例如在 ListBox、DataGrid 或下拉列表中。假设应用程序必须列出这本书的作者。Author 对象非常简单：

```c
public class Author
{
    public string Name { get; set; }
    public string Chapters { get; set; }
}
```

要在 DataGrid 中显示 Author 对象列表，只需在 XAML 中声明 DataGrid：

```xml
<DataGrid Name="myGrid" />
```

并在后置代码中，将 DataGrid 的 ItemsSource 属性赋值为：

```csharp
myGrid.ItemsSource = authors;
```

如果 authors 是 IEnumerable<Author> 类型（或类似类型，如 List<Author>），并且它包含任何数据，对象将如图 8-16 所示显示。

![](img/b5597c749e848b27b0d305153ae161_367_0.png)

图 16：在 DataGrid 中显示作者

