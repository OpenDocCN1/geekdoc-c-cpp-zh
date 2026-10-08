

![](img/b5597c749e848b27b0d305153ae16106_377_0.png)

这里是 *Focused* 状态的代码片段：

```
<VisualState x:Name="Focused">
<Storyboard>
  <DoubleAnimationUsingKeyFrames Storyboard.TargetProperty="Shape.StrokeThickness" Storyboard.TargetName="Ellipse">
<EasingDoubleKeyFrame Time="0" Value="2"/>
</DoubleAnimationUsingKeyFrames>
</Storyboard>
</VisualState>
```

这段代码片段简单地在 Focused 状态下将 Button 内部 Ellipse 的 StrokeThickness 属性设置为 2。这些属性是通过 Storyboards 设置的。Storyboard 是一种动画功能，因此对于设置属性来说可能显得大材小用，但 Storyboards 允许一些高级（以及如果使用不当则会产生波动）的功能——例如在 MouseOver 状态下无限地脉动按钮的颜色。

MouseOver 和 Pressed 状态的 XAML 与之前的非常相似。区别在于，整个状态组有一个过渡（transition）：

```xml
<VisualStateGroup.Transitions>
<VisualTransition GeneratedDuration="0:0:0.3"/>
</VisualStateGroup.Transitions>
```

这说明当属性在 VisualStateGroup 内发生变化时，变化应该作为平滑的线性动画发生，并持续 0.3 秒。也可以应用缓动（Easings）使过渡变为非线性的，甚至是弹跳的。视觉状态还可以有更特定的过渡。可以为进入或退出状态、或者在两个特定状态之间定义单独的过渡。

> 视觉状态也可以用于表示用户控件的状态，甚至可以是整个应用程序的状态。

还可以定义一个 Style 将此模板应用到所有 Button 上。毕竟，ControlTemplate 不过是一个属性，而属性可以通过样式进行设置：

```xml
<Style TargetType="Button">
  <Setter Property="Template" Value={StaticResource ButtonControlTemplate}/>
</Style>
```

在将此代码片段包含在外部资源的 Resources 部分并连同引用的 ButtonControlTemplate 资源之后，就可以移除 Button 的 Template 属性。此样式适用于所有 Button，因此您的应用程序的外观和感受将保持不变，额外的好处是新按钮会自动进行换肤。

# 数据绑定的模板

模板对于重新设计控件来说非常酷，但它们真正大放异彩的地方是数据绑定。例如，除了控件模板外，ListBox 有三个模板需要定义：

- Template：这定义了 ListBox 应该什么样子。
- ItemsPanel — 这定义了包含项的布局面板。
- ItemContainerStyle — 虽然它严格来说不是一个模板，但可以通过 ItemContainerStyle 更改 ListItems 的样式（因此也是模板）。

假设您想在一个美观的水平 ListBox 中列出之前数据绑定示例中的作者。代码后置部分（code-behind）与我们之前看到的 Author 示例（Listdatabinding）相同——唯一的是是将在 ListBox 中显示，因此 ListBox 的 ItemsSource 必须在构造函数的末尾设置。

```csharp
myListBox.ItemsSource = authors;
```

到目前为止 XAML 非常简单，如 8-13 所示。

| 列表 18: DataBindingTemplates.xaml |
| :--- |
| 可在 Wrox.com 下载 | `<UserControl x:Class="DataBindingTemplates.DataBindingTemplates" xmlns="http://schemas.microsoft.com/winx/2006/xaml/presentation" xmlns:x="http://schemas.microsoft.com/winx/2006/xaml" xmlns:d="http://schemas.microsoft.com/expression/blend/2008" xmlns:mc="http://schemas.microsoft.com/openxmlformats.org/markup-compatibility/2006" mc:Ignorable="d" d:DesignHeight="300" d:DesignWidth="400"><Grid Name="LayoutRoot" Background="White"><ListBox Name="myListBox" Height="88" Margin="8,8,8,0" VerticalAlignment="Top"/></Grid></UserControl>` |

代码文件 [DataBindingTemplates.xaml] 可在 Wrox.com 下载。

然而，运行代码的结果得到了一个相当失望的屏幕，如图 8-21 所示。

发生了什么？ListBox 并不知道要为每个 Author 显示什么，因此它（通过 ContentPresenter 控件）调用了每个 Author 对象的 ToString() 方法，并显示了每个其他结果的结果。要显示作者本身，必须定义 ItemTemplate。8-14 展示了如何可以这样做。

![](img/b5597c749e848b27b0d305153ae16106_379_0.png)

# 列表 8-14: BindingTemplates.xml

```xml
<UserControl x:Class="TemplateDememos.BindingTemplates"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.microsoft.com/openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d" d:DesignHeight="300" d:DesignWidth="400">
<Grid Name="LayoutRoot" Background="White">
  <ListBox Name="myListBox" Height="88" Margin="8,8,8,0" VerticalAlignment="Top"/>
</Grid>
</UserControl>
```
*(注：此处原文中 XAML 代码块与标题描述似乎有位置错乱，已按逻辑对齐翻译)*

然而，运行代码的结果得到了一个相当失望的屏幕，如图 8-21。

发生了什么？ListBox 并不知道要为每个 Author 显示什么，因此它（通过 ContentPresenter 控件）调用了每个 Author 对象的 ToString() 方法，并显示了所有其他结果的结果。要显示作者本身，必须定义 ItemTemplate。8-14 展示了如何可以这样做。

![](img/b5597c749e848b27b0d305153ae16106_379_1)

代码文件 [BindingTemplates.xaml] 可在 Wrox.com 下载。

现在项看起来还可以，但它们仍然是垂直排列的。这是因为如果没有定义，ListBox 使用 VirtualizingPanel 来排列项。VirtualizingPanel 就像 StackPanel，只是在创建当前滚动窗口可见项的视觉树时性能更好。重新定义 ItemsTemplate 后，可以将 VirtualizingPanel 替换为任何容器——例如 WrapPanel，甚至是按圆形排列项的 RadialPanel。对于这个示例，一个水平排列的 StackPanel 就够了。

```xml
<UserControl.Resources>
<DataTemplate x:Key="AuthorTemplate">
  <StackPanel Width="100">
    <TextBlock Text="Binding Name" x:Name="tbName" />
    <TextBlock Text="Binding Cycles" TextTrimming="Ellipsis" />
  </StackPanel>
</DataTemplate>
<ItemsPanelTemplate x:Key="ItemsPanelTemplate">
  <StackPanel Orientation="Horizontal"/>
</ItemsPanelTemplate>
</UserControl.Resources>
```

为了引用新创建的 ItemsPanelTemplate，ListBox 的声明变为：

```xml
<ListBox x:Name="MyListBox" Height="160" Margin="8,8,8,0" VerticalAlignment="Top"
  ItemTemplate={StaticResource AuthorTemplate}
  ItemsPanel={StaticResource ItemsPanelTemplate}">
```

结果。这就是 Item 样式的作用的地方。默认样式定义了 VisualStateGroups：

- CommonStates：鼠标悬停和聚焦/取消聚焦循环
- FocusStates
- LayoutStates：在项加载或卸载（即移除）时添加过渡
- SelectionStates：处理选择

演示 ItemContainerStyle 的示例带有轻微的弹跳效果旋转被选中的项。这很有趣，但不是业务应用程序中使用的东西。列表 8-15 展示了 ItemTemplate、ItemsPanelTemplate 和 ItemContainerStyle 的最终 XAML。

![](img/b5597c749e848b27b0d305153ae16106_380_0.png)

# 列表 8-15: DatabindingTemplates.xaml

```xml
<UserControl x:Class="TemplateDememos.DatabindingTemplates"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">
```

