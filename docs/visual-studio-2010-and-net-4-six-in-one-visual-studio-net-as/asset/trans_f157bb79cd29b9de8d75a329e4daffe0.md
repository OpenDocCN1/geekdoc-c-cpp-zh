
[content]

# 代码列表 8-8（续）

```cs
//Other authors...
};
myGrid.ItemsSource = authors;
}
private void AddAuthor_Click(object sender, RoutedEventArgs e)
{
    authors.Add(new Author ( Name = "New Author",
        Chapters = "New Author Chapters"));
}

public class Author
{
    public string Name { get; set; }
    public string Chapters { get; set; }
}
```

## 主/详情数据绑定

使用 UI-to-UI 绑定可以很容易地创建一个主/详情界面。代码列表 8-9 显示了在之前基础上扩展了详情面板的完整 XAML 代码。

# 代码列表 8-9: ListDatabinding.xaml

```xml
<UserControl x:Class="DatabindingDemo.ListDatabinding"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d"
d:Ignorable="d"
d:DesignHeight="300" d:DesignWidth="400"
xmlns:data="clr:System.Windows.Controls;assembly=System.Controls.Data">

<UserControl.Resources>
    <!-- 给 TextBlock 留出空间 -->
    <Style TargetType="TextBlock">
        <Setter Property="Padding" Value="8,8,8,8" />
    </Style>
</UserControl.Resources>

<Grid x:Name="LayoutRoot" Background="White">
    <StackPanel>
        <TextBlock HorizontalAlignment="Center" Text="Book Authors" />
        <Button Content="Add new author" Click="AddAuthor_Click" />
        <data:DataGrid x:Name="myGrid" />
        <!-- 详情面板 -->
<Border CornerRadius="10" BorderBrush="Black"
BorderThickness="1" Margin="10">
<StackPanel DataContext="{Binding ElementName=myGrid, Path=SelectedItem}">
<TextBlock HorizontalAlignment="Center"
Text="{Binding Path=Name, StringFormat={0}}"
Weight="Bold" />
</TextBlock>
<TextBlock HorizontalAlignment="Center"
Text="{Binding Path=Chapters, StringFormat={0}}"
TextWrapping="Wrap" />
</TextBlock>
</StackPanel>
</Border>
</Grid>
</UserControl>
```

代码文件 [ListDatabinding.xaml] 可在 Wrox.com 下载。

后台代码完全没有变化。运行此示例并从 DataGrid 中选择一行，将会在漂亮的圆角框中显示所选作者的详情，如图 8-17 所示。

| Name | Chapters |
|---|---|
| Andreas Volkov | Modern .NET Frameworks |
| Agnes Miller | History of Visual Studio and Current Editions, .NET Framework Version History, ASP .NET version history |
| Ethan Novak | Visual Studio Snapshots, Visual Studio Templates, Extending Visual Studio, Enhancements to the .NET Co |

**图 8-17**: 的主/详情 UI

那么，详情面板是如何工作的？详情面板的根是一个 Border。该 Border 的 DataContext 绑定到 DataGrid 的 SelectedItem 属性（正如其名称所示，它指向 DataGrid 中当前选中的项）。如果 DataGrid 显示的是 Author 类型的对象，SelectedItem 将包含 Author 类型的实例（如果没有选择任何内容，则为 null）。

这里的技巧再次利用了 DataContext 属性的继承特性。如果将 Border 的 DataContext 设置为选中的 Author，那么它视觉树中的所有后代都将具有相同的 DataContext。因此，两个 TextBlock 也会显示选中作者的 Name 和 Chapters 属性。注意，绑定具有非常实用的 StringFormat 绑定，它使用了与核心运行时相同的 String.Format 格式语法。

## 样式 (Styles)

你已经看到如何通过 Background、Stroke 等其他属性更改控件的外。例如，你可以通过以下 XAML 更改 TextBlock 的外观和行为：

```xml
<TextBlock Text="I am stylish, I am not?" HorizontalAlignment="Center"
Family="Comic Sans MS"
VerticalAlignment="Center" FontSize="20" Style="Italic"
FontWeight="Bold" TextTrimming="WordEllipsis" Width="199">
<TextBlock.Foreground>
<LinearGradientBrush EndPoint="0.5,1" StartPoint="0.5,0">
<GradientStop Color="Black" Offset="0" />
<GradientStop Color="Gray" Offset="1" />
</LinearGradientBrush>
</TextBlock.Foreground>
```

渲染时，该 XAML 看起来像：

```xml
<TextBlock Text="I am stylish, I am not?" HorizontalAlignment="Center"
Family="Comic Sans MS"
VerticalAlignment="Center" FontSize="20" Style="Italic"
FontWeight="Bold" TextTrimming="WordEllipsis" Width="199"
>
</TextBlock>
</TextBlock>
```

在元素内部定义样式时，内联样式存在几个问题。第一个问题是它们过于冗长且难以阅读。第二个问题是它们无法轻松复用，你必须重复 XAML。第三个问题是，如果你想更改整个应用程序的外观，没有一个中心位置可以进行。

幸运的是，Silverlight 的功能不仅限于内联。你可以创建定义对象样式的资源。例如，你可以在任何其他控件中使用这些资源。当然，Rectangle 只能引用该资源——前提是它在同一个 UserControl 内。如果你想在整个项目中复用该资源，可以创建一个新的资源字典并移动它，或者通过将其放入 App.xml 资源字典使其真正全局化。

尽管如此，有了资源，如果你想让你所有的 TextBlock 看起来都一样，必须将所有重要属性设置为适当的资源。样式统治一切！样式无非是一组属性。例如，你可以将 TextBlock 的属性收集到一个样式中：

```xml
<Style x:Key="TextBlockStyle" TargetType="TextBlock">
<Setter Property="Foreground" Value="(StaticResource ForegroundBrush)"/>
<Setter Property="Effect" Value="(StaticResource Effect1)"/>
<Setter Property="FontFamily" Value="(StaticResource FontFamily1)"/>
<Setter Property="TextTrimming" Value="WordEllipsis"/>
<Setter Property="FontSize" Value="20"/>
<Setter Property="FontStyle" Value="Italic"/>
<Setter Property="FontWeight" Value="Bold"/>
</Style>
```

该样式定义在资源字典中——要么在 UserControl 内，要么在外部字典中（如 App.xml）。使用之前的示例，TextBlock 的定义简化为如下：

```xml
<TextBlock Text="I am stylish, I am not?" HorizontalAlignment="Center"
VerticalAlignment="Center" Width="199"
Style="(StaticResource TextBlockStyle)" />
```

