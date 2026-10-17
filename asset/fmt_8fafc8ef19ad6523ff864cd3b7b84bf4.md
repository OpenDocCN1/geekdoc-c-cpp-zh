
```
<UserControl x:Class="Wrox.ProCSharp.WPF.BookUC"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
mc:Ignorable="d"
d:DesignHeight="300" d:DesignWidth="300">
<DockPanel>
<Grid>
<Grid.RowDefinitions>
<RowDefinition />
<RowDefinition />
<RowDefinition />
<RowDefinition />
</Grid.RowDefinitions>
<Grid.ColumnDefinitions>
<ColumnDefinition Width="Auto" />
<ColumnDefinition Width="*" />
</Grid.ColumnDefinitions>
<Label Content="Title" Grid.Row="0" Grid.Column="0" Margin="10,0,5,0" HorizontalAlignment="Left" VerticalAlignment="Center" />
<Label Content="Publisher" Grid.Row="1" Grid.Column="0" Margin="10,0,5,0" HorizontalAlignment="Left" VerticalAlignment="Center" />
<Label Content="Isbn" Grid.Row="2" Grid.Column="0" Margin="10,0,5,0" HorizontalAlignment="Left" VerticalAlignment="Center" />
<TextBox Grid.Row="0" Grid.Column="1" Margin="5" />
<TextBox Grid.Row="1" Grid.Column="1" Margin="5" />
<TextBox Grid.Row="2" Grid.Column="1" Margin="5" />
<StackPanel Grid.Row="3" Grid.Column="0" Grid.ColumnSpan="2">
<Button Content="Show Book" Margin="5" Click="OnShowBook" />
</StackPanel>
</Grid>
</DockPanel>
</UserControl>
```

在 `MainWindow.xaml.cs` 中的 `OnShowBook` 处理程序中，创建用户控件 `BookUC` 的新实例并向 `TabControl` 添加一个新的 `TabItem`。然后更改 `TabControl` 的 `SelectedIndex` 属性以打开新选项卡（代码文件 `BooksDemoLib/MainWindow.xaml.cs`）：

```
private void OnShowBook(object sender, ExecutedRoutedEventArgs e)
{
    var bookUI = new BookUC();
    this.tabControl1.SelectedIndex = this.tabControl1.Items.Add(
        new TabItem { Header ="Book", Content = bookUI });
}
```

构建项目后，您可以启动应用程序并通过单击超链接在 `TabControl` 中打开用户控件。

### Binding with XAML

除了作为数据绑定的目标之外，WPF 元素也可以作为源。您可以将一个 WPF 元素的源属性绑定到另一个 WPF 元素的目标。

在下面的代码示例中，使用数据绑定根据滑块调整用户控件内的控件大小。您向用户控件 `BookUC` 添加一个 `StackPanel` 控件，其中包含一个 `Label` 和一个 `Slider` 控件。`Slider` 控件定义了定义比例的 `Minimum` 和 `Maximum` 值，并将初始值 `1` 分配给 `Value` 属性（代码文件 `BooksDemoLib/BooksUC.xaml`）：

```
<DockPanel>
    <StackPanel DockPanel.Dock="Bottom" Orientation="Horizontal" HorizontalAlignment="Right">
        <Label Content="Resize" />
        <Slider x:Name="slider1" Value="1" Minimum="0.4" Maximum="3" Width="150" HorizontalAlignment="Right" />
    </StackPanel>
```

现在您设置 `Grid` 控件的 `LayoutTransform` 属性并添加一个 `ScaleTransform` 元素。使用 `ScaleTransform` 元素，`ScaleX` 和 `ScaleY` 属性是数据绑定的。两个属性都使用 `Binding` 标记扩展设置。在 `Binding` 标记扩展中，`ElementName` 设置为 `slider1` 以引用之前创建的 `Slider` 控件。`Path` 属性设置为 `Value` 属性以获取滑块的值：

```
<Grid>
    <Grid.LayoutTransform>
        <ScaleTransform x:Name="scale1" ScaleX="{Binding Path=Value, ElementName=slider1}" ScaleY="{Binding Path=Value, ElementName=slider1}" />
    </Grid.LayoutTransform>
```

运行应用程序时，您可以移动滑块，从而调整 `Grid` 内的控件大小，如图 34.16 和 34.17 所示。

源对象的属性 `Value`。对于派生自 `FrameworkElement` 的控件，您可以调用 `SetBinding` 方法来定义绑定。但是，`ScaleTransform` 不派生自 `FrameworkElement`，而是派生自 `Freezable` 基类。使用辅助类 `BindingOperations` 来绑定此类控件。`BindingOperations` 类的 `SetBinding` 方法需要一个 `DependencyObject`——示例中为 `ScaleTransform` 实例。使用第二个和第三个参数，`SetBinding` 方法需要目标的依赖属性（应绑定），以及 `Binding` 对象：

```
var binding = new Binding
{
    Path = new PropertyPath("Value"),
    Source = slider1
};
BindingOperations.SetBinding(scale1,
ScaleTransform.ScaleXProperty, binding);
BindingOperations.SetBinding(scale1,
ScaleTransform.ScaleYProperty, binding);
```

> **NOTE** 请记住，所有派生自 `DependencyObject` 的类都可以具有依赖属性。您可以在第 29 章了解有关依赖属性的更多信息。

您可以使用 `Binding` 类配置许多绑定选项，如下表所述：

| Binding Class Members | Description |
|---|---|
| Source | 使用此属性定义数据绑定的源对象。 |
| RelativeSource | 相对于目标对象指定源。这对于在错误源自同一控件时显示错误消息很有用。 |
| ElementName | 如果源是 WPF 元素，则可以使用 `ElementName` 属性指定源。 |
| Path | 使用此属性指定到源对象的路径。这可以是源对象的属性，但也支持索引器和子元素的属性。 |
| XPath | 使用 XML 数据源时，您可以定义 XPath 查询表达式来获取绑定数据。 |
| Mode | 模式定义绑定的方向。`Mode` 属性的类型为 `BindingMode`。`BindingMode` 是一个枚举，具有以下值：`Default`、`OneTime`、`OneWay`、`TwoWay` 和 `OneWayToSource`。默认模式取决于目标：对于 `TextBox`，默认是双向绑定；对于只读的 `Label`，默认是一向。`OneTime` 表示 |
| 属性 | 描述 |
| --- | --- |
| Mode | 使用 `OneTime` 绑定时，数据仅在初始时从源加载；`OneWay` 从源更新到目标。使用 `TwoWay` 绑定时，WPF 元素的更改会写回源。`OneWayToSource` 表示数据永远不会被读取，而是始终从目标写入源。 |
| Converter | 使用此属性指定一个转换器类，用于在 UI 和数据之间进行转换。转换器类必须实现接口 `IValueConverter`，该接口定义了方法 `Convert` 和 `ConvertBack`。您可以使用 `ConverterParameter` 属性向转换器方法传递参数。转换器可以是文化敏感的；并且文化可以用 `ConverterCulture` 属性设置。 |
| FallbackValue | 使用此属性定义一个默认值，当绑定不返回值时使用。 |
| ValidationRules | 使用此属性，您可以定义一个 `ValidationRule` 对象的集合，在从 WPF 目标元素更新源之前对其进行检查。类 `ExceptionValidationRule` 派生自类 `ValidationRule` 并检查异常。 |
| Delay | 此属性在 WPF 4.5 中新增。它使您能够指定在更新绑定源之前等待的时间量。这可用于希望在开始验证之前给用户一些时间输入更多字符的场景。 |

### 简单对象绑定

要绑定到 CLR 对象，只需使用 .NET 类定义属性，如 `Book` 类示例以及属性 `Title`、`Publisher`、`Isbn` 和 `Authors` 所示。此类位于 `BooksDemoLib` 项目的 `Models` 文件夹中（代码文件 `BooksDemoLib/Models/Book.cs`）。

```csharp
using System.Collections.Generic;

namespace BooksDemo.Models
{
    public class Book
    {
        public Book(string title, string publisher, string isbn,
                    params string[] authors)
        {
            Title = title;
            Publisher = publisher;
            Isbn = isbn;
            Authors = authors;
        }

        public Book()
            : this("unknown", "unknown", "unknown")
        {
        }

        public string Title { get; set; }
        public string Publisher { get; set; }
        public string Isbn { get; set; }

        public string[] Authors { get; }

        public override string ToString() => Title;
    }
}
```

在用户控件 `BookUC` 的 XAML 代码中，定义了多个标签和 `TextBox` 控件以显示图书信息。使用 `Binding` 标记扩展，`TextBox` 控件绑定到 `Book` 类的属性。使用 `Binding` 标记扩展，只需定义 `Path` 属性即可将其绑定到 `Book` 类的属性。无需定义源，因为源是通过分配 `DataContext` 定义的，如以下代码隐藏所示。模式由 `TextBox` 元素的默认值定义，这就是双向绑定（代码文件 `BooksDemoLib/Controls/BookUC.xaml`）：

```xml
<TextBox Text="{Binding Title}" Grid.Row="0" Grid.Column="1" Margin="5" />
<TextBox Text="{Binding Publisher}" Grid.Row="1" Grid.Column="1" Margin="5" />
<TextBox Text="{Binding Isbn}" Grid.Row="2" Grid.Column="1" Margin="5" />
```

使用代码隐藏，创建一个新的 `Book` 对象，并将图书分配给用户控件的 `DataContext` 属性。`DataContext` 是使用基类 `FrameworkElement` 定义的依赖属性。将 `DataContext` 分配给用户控件意味着用户控件中的每个元素都有一个默认绑定到相同的数据上下文（代码文件 `BooksDemoRibbon/MainWindow.xaml.cs`）：

```csharp
private void OnShowBook(object sender, ExecutedRoutedEventArgs e)
{
    var bookUI = new BookUC();
    bookUI.DataContext = new Book
    {
        Title = "Professional C# 5.0 and .NET 4.5.1",
        Publisher = "Wrox Press",
        Isbn = "978-0-470-50225-9"
    };
    this.tabControl1.SelectedIndex =
        this.tabControl1.Items.Add(
            new TabItem { Header = "Book", Content = bookUI });
}
```

启动应用程序后，您可以看到绑定的数据，如图 34.18 所示。

Figure 34.18

要查看双向绑定在实际中的效果（对 WPF 元素的输入更改会反映在 CLR 对象内部），用户控件中按钮的 `Click` 事件处理程序 `OnShowBook` 方法已实现。实现后，会弹出消息框以显示图书对象的当前标题和 ISBN 号码。图 34.19 显示了在应用程序运行时用户在输入中输入 Professional C# 6 后消息框的输出（代码文件 `BooksDemoLib/Controls/BookUC.xaml.cs`）：

![](img/3d365b72b289213a91ade7eb366b8f35_1330_0.png)

Figure 34.19

```csharp
private void OnShowBook(object sender, RoutedEventArgs e)
{
    Book theBook = this.DataContext as Book;
    if (theBook != null)
    {
        MessageBox.Show(theBook.Title, theBook.Isbn);
    }
}
```

### 更改通知

使用当前的双向绑定，数据从对象读取并写回。然而，如果数据不是由用户更改，而是直接从代码更改，则 UI 不会收到更改信息。您可以通过向用户控件添加一个按钮并实现点击事件处理程序 `OnChangeBook` 来轻松验证这一点（代码文件 `BooksDemoLib/Controls/BookUC.xaml`）：

```xml
<StackPanel Grid.Row="3" Grid.Column="0" Grid.ColumnSpan="2" Orientation="Horizontal" HorizontalAlignment="Center">
    <Button Content="Show Book" Margin="5" Click="OnShowBook" />
    <Button Content="Change Book" Margin="5" Click="OnChangeBook" />
</StackPanel>
```

在处理程序的实现中，数据上下文中的图书被更改，但用户界面不会显示更改（代码文件 `BooksDemoLib/Controls/BookUC.xaml.cs`）：

```csharp
private void OnChangeBook(object sender, RoutedEventArgs e)
{
    Book theBook = this.DataContext as Book;
    if (theBook != null)
    {
        theBook.Title = "Professional C# 6";
        theBook.Isbn = "978-0-470-31442-5";
    }
}
```
