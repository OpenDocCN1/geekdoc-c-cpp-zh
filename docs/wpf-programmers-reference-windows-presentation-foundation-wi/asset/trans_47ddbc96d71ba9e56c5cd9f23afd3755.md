

# 普通属性值

如前面的示例所示，你可以创建作为 `LinearGradientBrushes`、`RadialGradientBrushes` 和 `BitmapEffectGroups` 的资源。你还可以创建 `SolidColorBrushes`、`Thicknesses`（用于 Margin）、`DashStyles` 和 `Colors`（尽管这并没有你想象的那么有用——你可能想要 `Brush`、`FontFamilies`、`FontStyles` 以及你想使用的任何其他属性类型）。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_234_0.png)

这些“普通”属性值很容易理解且符合直觉。例如，让多个控件共享相同的 `Background`、`Margin` 或 `DashStyle` 是合理的。

上一节的示例演示了这种简单的属性类型。

# 控件

资源通常包含“普通”属性值，但也可以包含控件。例如，下面的 XAML 控件定义了一个 TextBox，它内部以两种不同的样式包含了一些文本：

```xml
<TextBlock x:Key="txtName" TextAlignment="Center">
  <Run>Click Me</Run><LineBreak/>
  <Run TextBlock.Foreground="Red"
        TextBlock.FontSize="20"
        TextBlock.FontStyle="Italic"
        TextBlock.FontWeight="Bold">
    PLEASE!
  </Run>
</TextBlock>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_234_1.png)

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_234_2.png)

`ContentResource` 程序使用以下代码将 Button 的 `Content` 属性设置为 `TextBlock` 资源，以便其显示：

```xml
<Button Width="125" Height="75" Content="{StaticResource txtButton}"/>
```

图 12-3 显示

在这个示例中，将 TextBox 设为资源并不能节省多少麻烦。它所需的代码量与你在 Button 中定义内容时的代码相差不多，而且你不可能拥有许多具有相同内容的按钮，因此你可能不会使用资源来减少重复。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_234_3.png)

图 12-3

这种技术在那些确实需要多个相同内容的副本的少数情况下要有用得多。例如，假设一个应用程序显示了一系列人物照片，你想为每张照片提供相同的菜单上下文：详情、电子邮件、电话和删除。下面的代码定义了一个包含这些命令的 `ContextMenu` 以及一个会产生阴影的 `BitmapEffect`：

```xml
<Window.Resources>
  <ContextMenu x:Key="ctxPerson">
    <MenuItem Header="Details" Click="mnuDetails_Click"/>
    <MenuItem Header="Email" Click="mnuEmail_Click"/>
    <MenuItem Header="Phone" Click="mnuPhone_Click"/>
    <Separator/>
    <MenuItem Header="Delete" Click="mnuDelete_Click"/>
  </ContextMenu>
  <BitmapEffectGroup x:Key="bmePerson">
    <DropShadowBitmapEffect/>
  </BitmapEffectGroup>
</Window.Resources>
```

以下代码显示了 Image 如何使用这些资源：

```xml
<Image Name="imgClaude" Width="100" Height="100" Stretch="Uniform"
MouseDown="img_MouseDown"
Source="Claude.jpg" Tag="Claude"
BitmapEffect="{StaticResource bmePerson}"
ContextMenu="{StaticResource ctxPerson}"/>
```

一系列 Button 可以使用相似的代码显示相同的 `ContextMenu`。
程序使用代码绑定来响应用户选择菜单项 MenuItem 的操作。
不幸的是，MenuItem 触发的 `Click` 事件处理程序不知道用户点击了哪个 Image 控件。MenuItem 的参数告诉我们点击的是哪个 MenuItem，但并没有说明哪个 Image 显示了上下文。

确定哪个 Image 显示了菜单的一种方法是在显示菜单时保存 Image 的引用。`ContextMenuResource` 示例程序为其所有 Image 控件的 `MouseDown` 事件处理程序分配了以下处理程序。如果用户在 Image 上按下右键，代码将保存该 Image 控件的引用，以便用户选择菜单项时使用。

```csharp
// 记住被点击的图片。
private Image m_ImageClicked = null;
private void img_MouseDown(Object sender, MouseButtonArgs e)
{
  if (e.RightButton == MouseButtonState.Pressed)
  {
    m_ImageClicked = (Image)sender;
  }
}
```

# 资源类型

```csharp
// 显示被点击人物详情。
private void mnuDetails_Click(object sender, RoutedEventArgs e)
{
    if (m_ImageClicked != null)
        MessageBox.Show("Display details for " + m_ImageClicked.ToString());
}
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_236_0.png)

ContextMenuResource

图 12-4 ContextMenuResource 示例显示了其共享的 `ContextMenu`。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_236_1.png)

图 12-4

# 简单数据类型

讽刺的是，在知道技巧之前，最简单的类型（如字符串、整数和双点数）在存储在资源时是最令人困惑的。问题在于 XAML 文件只认识 XAML 类型（如 `SolidColorBrush`），而不认识 `Double` 和 `Int32` 等系统类型。为了让文件理解这些类型，你需要给它一个命名空间属性，告诉它在哪个命名空间查找这些类型。例如，下面的 XAML 显示了一个 `Window` 元素。命名空间属性引用了在 mscorlib 中定义的数据类型。

```xml
<Window xmlns="http://schemas.microsoft.com/winfx/2006/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:sys="clr-namespace:System;assembly=mscorlib"
        x:Class="Window"
        Title="ResourceHierarchy"
        Width="350" Height="180"
        FontSize="16" FontWeight="Bold">
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_236_2.png)

ResourceHierarchy

# 

现在下面的代码定义了两个 `Double` 类型的资源。注意代码如何使用 `sys` 前缀来指示 `Double` 类型定义的位置。

```xml
<Window.Resources>
  <sys:Double x:Key="dblRadX">5</sys:Double>
  <sys:Double x:Key="dblRadY">20</sys:Double>
</Window.Resources>
```

下面的代码显示 Rectangle 可能会使用这些资源作为其 `RadiusX` 和 `RadiusY` 属性：

```xml
<Rectangle Margin="5" Width="175" Height="60"
Fill="Red" Stroke="Black" StrokeThickness="5"
RadiusX={StaticResource dblRadX}
RadiusY={StaticResource dblRadY}/>
```

这些简单数据类型允许你在资源中放置特定值。例如，你可以构建一个资源字典，包含应用程序用于标签、按钮和其他控件的所有字符串。对于不同的按钮（尽管你可能希望按钮和菜单项具有相同的文本），将这些值放在资源中会更便于更改。

图 12-5 中的 `DataTypes` 程序显示了 mscorlib 中定义的每个简单类型的资源。

| Byte | Object | Char |
| :--- | :--- | :--- |
| 255 | | -128 |
| Char | DateTime | 4/1/2010 |
| Decimal | 7.922816852842637893845903 | String | Any text value |
| Double | 1.797693148623187 | UInt16 | 6553 |
| Int16 | 32767 | UInt32 | 429497295 |
| Int32 | 2147483647 | UInt64 | 1844674403709551615 |
| Int64 | 9223372036854775807 |

> 发现数据类型
> 在 Visual Studio 中，你可以使用对象浏览器查看 mscorlib 等库中可用的数据类型。

你可以创建多个包含相同资源的资源字典，然后在它们之间轻松切换。第 16 节的“皮肤 (Skins)”部分对此技术有更多介绍。

# 资源层次结构

在 WPF 树中，许多对象可能有资源字典。当控件使用资源时，WPF 会向上遍历树，直到找到按名称定义的对象。

例如，假设一个 Window 包含一个带有 Label 的 StackPanel，而 Label 使用了名为 `LabelValue` 的资源。当它构建 Label 时，WPF 首先检查 Label 的资源字典（如果存在）以寻找 `LabelValue`。如果没找到，WPF 将移动到 StackPanel 并搜索其资源。如果仍然找不到，WPF 将继续向上到 Window 并检查其资源。

如果在逻辑树顶部的 Window 中仍未找到 `LabelValue` 资源，WPF 将检查 App.xaml 文件查看其是否定义了该资源。

如果经过这一切之后 WPF 仍然找不到该资源，应用程序将以多种方式失败。例如，Expression Blend 窗口设计器不会渲染需要资源的控件，如果你尝试运行应用程序，它会失败。相反，Visual Studio 的窗口设计器会显示错误消息且不绘制任何控件。

