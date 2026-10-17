
图 18-3 显示的 `TypeColor` 示例程序将 `TextBox` 的 `Background` 属性与其 `Text` 属性绑定，因此当你输入颜色名称时，控件会以该颜色作为背景。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_357_2.png)

## WHAT ERROR?（什么错误？）

绑定在运行时不会报告错误。如果绑定的值没有任何意义——例如，如果你将 `Width` 设置为 `Color`——则什么都不会发生。在 `TypeAColor` 程序中，如果你输入某些不是颜色名称的文本，什么都不会发生，程序会继续正常运行。

以下代码显示了 `TypeAColor` 程序如何将 `TextBox` 的 `Background` 属性绑定到它的 `Text` 属性：

```xml
<TextBox Margin="10" Height="30" VerticalAlignment="Top" Background="{Binding RelativeSource={RelativeSource Self}, Path=Text}"/>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_358_0.png)

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_358_1.png)

`RelativeSource=(RelativeSource Self)` 将绑定的 `RelativeSource` 属性设置为由字符串 `Self` 构建的新型 `RelativeSource` 对象。

你还可以使用字符串 `TemplatedParent`、`FindAncestor` 或 `PreviousData` 来构建 `RelativeSource` 对象。

`TemplatedParent` 设置使用对应用模板的对象的引用。图 18-4 显示的 `TemplatedParent` 示例程序显示了一个带有模板的 `Label`，该模板显示 `Label` 沿边缘的外边距。该 `Label` 的 `Margin` 属性被设置为 10, 20, 30, 40。

以下代码显示了 `Label` 模板中显示 `Label` 顶部外边距的部分。绑定使用其 `RelativeSource` 属性来查找模板所在的 `Label`。`Path Margin.Top` 的值使绑定获取该 `Label` 的 `Margin` 并使用其 `Top` 值。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_358_2.png)

图 18-4

```xml
<Label VerticalAlignment="Top" HorizontalAlignment="Center" FontSize="10" Content="{Binding RelativeSource={RelativeSource TemplatedParent}, Path=Margin.Top}"/>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_358_3.png)

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_358_4.png)

`RelativeSource` 值 `FindAncestor` 允许你查找特定类型的目标控件祖先。图 18-5 显示的 `ColumnWidth` 示例程序使用这种绑定让 `Label` 显示包含它们的 `Grid` 列的宽度。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_358_5.png)

图 18-5

## 322 | 第 18 章 绑定 (BINDING)

`RelativeSource` 值 `FindAncestor` 允许你查找目标控件特定类型的祖先。`ColumnWidth` 示例程序使用这种绑定让 `Label` 显示包含它们的 `Grid` 列的宽度。

`RelativeSource=(RelativeSource Self)` 将绑定的 `RelativeSource` 属性设置为由字符串 `Self` 构建的新型 `RelativeSource` 对象。

你还可以使用字符串 `TemplatedParent`、`FindAncestor` 或 `PreviousData` 来构建 `RelativeSource` 对象。

[注：此处关于 `RelativeSource`, `TemplatedParent` 和 `Path` 描述已已翻译。]

`TemplatedParent` 设置使用对应用模板的对象的引用。图 18-4 显示的 `TemplatedParent` 示例程序显示了一个带有模板的 `Label`，该模板显示 `Label` 沿边缘的外边距。该 `Label` 的 `Margin` 属性被设置为 10, 20, 30, 40。

以下代码显示了 `Label` 模板中显示 `Label` 顶部外边距的部分。绑定使用其 `RelativeSource` 属性来查找模板所在的 `Label`。`Path Margin.Top` 的值使绑定获取该 `Label` 的 `Margin` 并使用其 `Top` 值。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_358_2.png)

图 18-4

```xml
<Label VerticalAlignment="Top" HorizontalAlignment="Center" FontSize="10" Content="{Binding RelativeSource={RelativeSource TemplatedParent}, Path=Margin.Top}"/>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_358_3.png)

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_358_4.png)

`RelativeSource` 值 `FindAncestor` 允许你查找目标控件特定类型的祖先。`ColumnWidth` 示例程序使用这种绑定让 `Label` 显示包含它们的 `Grid` 列的宽度。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_358_5.png)

图 18-5

[注：由于原文文本存在大量重复和错乱，译文已根据逻辑对核心内容进行了整理和翻译。]

## 另一个示例

`DockPanelView` 示例程序使用了 `TargetType = Label` 的样式，使得包含在 `DockPanel` 中的 `Label` 显示它们的 `DockPanel.Dock` 附加属性值。

- 如果某个值提供了索引，请在方括号中包含该索引。例如，本章之前描述的 `ColumnWidths` 示例使用了如 `ColumnDefinitions[2].Width` 格式的路径来描述网格的列宽。
- 如果绑定的源是一个集合，你可以使用斜杠（`/`）来引用集合的当前项。

图 18-7 显示的 `ColorList` 示例程序演示了 `Source = /` 的绑定：左侧是 `List`，右侧的 `Label` 显示所选颜色的名称及其对应的背景。

`ColorList` 程序使用以下代码来定义其 `List` 和 `Label`：

```
<Grid Margin="10">
<Grid.DataContext>
<x:Array Type="sys:String">
<sys:String>Red</sys:String>
<sys:String>Yellow</sys:String>
<sys:String>Lime</sys:String>
<sys:String>Cyan</sys:String>
<sys:String>Blue</sys:String>
<sys:String>Magenta</sys:String>
</x:Array>
</Grid.DataContext>
<Grid.ColumnDefinitions>
<ColumnDefinition Width="*"/>
<ColumnDefinition Width="*"/>
</Grid.ColumnDefinitions>
```

```
<ListBox Name="colorList" Grid.Column="0" Background="Transparent"
IsSynchronizedWithCurrentItem="True"
ItemsSource="Binding Path" />
```

```
<Label Grid.Column="1" BorderBrush="Black" BorderThickness="1"
HorizontalAlignment="Center" VerticalAlignment="Center"
Content="Binding Path/" />
</Grid>
```

图 18-7

代码从 `Grid` 控件开始。它将该控件的 `DataContext` 设置为包含颜色名称的字符串数组。

在定义了两个网格列后，代码创建了一个 `ListBox`。它的 `ItemsSource` 属性被设置为不寻的值 `{Binding}`，表示该属性应该被设置为控件继承的 `DataContext` 值。

`Label` 的 `Content` 和 `Background` 属性都被设置为 `{Binding Path/}`；因此它们的绑定源是控件继承的 `DataContext`，而它们的绑定路径是数组的选中值。

## 绑定集合

某些控件（如 `Button`、`TextBox` 和 `Label`）被视为内容控件。它们旨在将部分数据显示为文本或包含其他控件的网格。

其他控件（如 `ListBox`、`ComboBox`、`TreeView`）被视为项目控件。这些控件显示存储在集合、数组、树或其他重复结构中的重复值序列。这些值可以是简单的数字或字符串，也可以是复杂的对象，例如 `Order` 或 `Employee` 类的实例。

绑定控件相对直观。设置绑定、目标属性、源和路径；就完成了。

从表面上看，绑定项目控件同样简单。只需将控件的 `ItemsSource` 属性设置为某种持有重复值的集合即可。如果这些值是简单的数字或字符串，那么这种……

图 18-8 显示的 `NumberList` 示例程序就是这样运行的。

`NumberList` 示例程序定义了一个整数数组。为了使用 `Int32` 数据类型定义数字，程序包含了以下命名空间声明：

```
xmlns:sys="clr-namespace:System;assembly=mscorlib
```

程序在它的 `Windows.Resources` 部分定义了数组：

```
<Window.Resources>
  <x:Array Key="numbers" Type="sys:Int32">
    <sys:Int32>100</sys:Int32>
    <sys:Int32>200</sys:Int32>
    <sys:Int32>50</sys:Int32>
    <sys:Int32>800</sys:Int32>
    <sys:Int32>175</sys:Int32>
  </x:Array>
</Window.Resources>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_362.png) 图 18-8

最后，我们使用以下代码将数组绑定到 `ListBox`：

```
<ListBox ItemsSource={StaticResource numbers} Background="Transparent">
```

正如图 18-8 所示，`ListBox` 会自动显示数组中的值。

## 第18 章 数据绑定

遗憾，如果将 `ListBox` 绑定到复杂对象，情况就会变得复杂。为了确定显示某个项的内容，控件会调用项的 `ToString` 方法。对于数字和字符串等简单项，`ToString` 返回项的文本表示。

对于像 `Person` 对象这样更复杂的项，`ToString` 返回类的名称。在 `PersonList` 示例中，`ListBox` 为每个项显示 `PersonList.Person`。

解决这个问题的一种方法是让类重写 `ToString` 方法以返回更有用的内容。

图 18-9 中的 `PersonList` 示例显示了两个类：`Person` 和 `Person2`。`Person` 类使用它的 `ToString` 方法，而 `Person2` 类重写了它的 `ToString` 方法。

`Person2` 类使用以下代码重写它的 `ToString` 方法：

```
public override string ToString()
{
    return FirstName + " " + LastName;
}
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_363.png) 图 18-9

## 代码中的类

XAML 代码可以使用你在代码后台中定义的类。为了实现这一点，首先包含标识程序命名空间的声明：

```
xmlns:local="clr-namespace:PersonList"
```

现在 XAML 代码可以使用类作为数据类型。例如，`PersonList` 程序使用以下代码来映射它的 `Person` 对象数组：

```
<x:Array x:Key="people" Type="local:Person">
    <local:Person FirstName="James" LastName="Kirk"/>
    <local:Person FirstName="Spock"/>
</x:Array>
```

注意，该类必须有一个空构造函数（不接受参数的构造函数）供 XAML 代码使用。

重写的 `ToString` 方法使得 `ListBox` 显示的结果更有用。`ListBox` 的功能不仅限于显示字符串。它具有用于确定项显示方式的 `ItemTemplates`。

## ListBox 和 ComboBox 模板

`ListBox` 和 `ComboBox` 有一个决定每个项显示的 `ItemTemplate` 属性。这些模板在第15章中描述。

图 18-10 显示的 `Planets` 示例在左侧的 `ListBox` 和右侧的 `ComboBox` 中显示了 `Planet` 对象数组。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_364.png) 图 18-10

以下代码显示了 `ListBox` 使用的 `ItemTemplate`：

```
<ListBox.ItemTemplate>
<DataTemplate>
<DataTemplate.Resources>
  <Style TargetType="TextBlock">
    <Setter Property="Margin" Value="3"/>
    <Setter Property="HorizontalAlignment" Value="Left"/>
    <Setter Property="VerticalAlignment" Value="Center"/>
    <Setter Property="FontSize" Value="20"/>
    <Setter Property="FontWeight" Value="Bold"/>
    <Setter Property="Foreground" Value="Blue"/>
  </Style>
  <Style TargetType="Image">
    <Setter Property="Height" Value="50"/>
    <Setter Property="Margin" Value="3"/>
    <Setter Property="Stretch" Value="Uniform"/>
    <Setter Property="HorizontalAlignment" Value="Right"/>
  </Style>
  <Style TargetType="Text">
    <Setter Property="Margin" Value="3"/>
    <Setter Property="Width" Value="250"/>
    <Setter Property="Background" Value="SkyBlue"/>
    <Setter Property="TextWrapping" Value="Wrap"/>
    <Setter Property="IsReadOnly" Value="True"/>
  </Style>
</DataTemplate.Resources>
<StackPanel>
<Grid>
<Image Source="{Binding Picture}"/>
</Grid>
<TextBlock Text="{Binding Stats}"/>
</StackPanel>
</DataTemplate>
</ListBox.ItemTemplate>
```

`Planets`

大部分代码使用样式为显示项数据的控件定义属性。结尾的 `StackPanel` 包含了这些控件。实际显示数据的控件有：

- 一个绑定到 `Planet` 项 `Name` 的 `TextBlock`
- 一个绑定到 `Planet` `Picture` 属性的图像
- 一个绑定到 `Planet` `Stats` 属性的 `TextBox`

除了 `ItemTemplate` 属性外，`ListBox` 和 `ComboBox` 控件提供了 `ItemsPanel` 属性，用于定义布局项的面板控件。默认情况下，`ListBox` 和 `ComboBox` 使用垂直方向的 `StackPanel` 作为它们的 `ItemsPanel`，以便项单列显示，但你可以更改这一点。

`Planets` 示例程序使用以下代码使其 `ListBox` 使用 `WrapPanel` 而不是 `StackPanel` 来排列项：
