
该控件仍然缺少滚动功能，以防项无法在屏幕上显示完整。可以通过为 `ListView` 控件定义模板来更改此行为。

`ListViewStyle2` 样式根据水平项对齐的要求定义了水平和垂直滚动条行为。此样式还包含对之前定义的数据模板和容器项模板的资源引用。通过设置 `Template` 属性，你现在还可以更改整个 `ListView` 控件的 UI（代码文件 `TemplatesUWP/Styles/ListTemplates.xaml`）：

```xml
<Style x:Key="ListViewStyle2" TargetType="ListView">
    <Setter Property="ScrollViewer.HorizontalScrollBarVisibility" Value="Auto"/>
    <Setter Property="ScrollViewer.VerticalScrollBarVisibility" Value="Disabled"/>
    <Setter Property="ScrollViewer.HorizontalScrollMode" Value="Auto"/>
    <Setter Property="ScrollViewer.IsHorizontalRailEnabled" Value="False"/>
    <Setter Property="ScrollViewer.VerticalScrollMode" Value="Disabled"/>
    <Setter Property="ScrollViewer.IsVerticalRailEnabled" Value="False"/>
    <Setter Property="ScrollViewer.ZoomMode" Value="Disabled"/>
    <Setter Property="ScrollViewer.IsDeferredScrollingEnabled" Value="False"/>
    <Setter Property="ScrollViewer.BringIntoViewOnFocusChange" Value="True"/>
    <Setter Property="ItemTemplate" Value="{StaticResource CountryDataTemplate}" />
    <Setter Property="ItemContainerStyle" Value="{StaticResource ListViewItemStyle1}" />
    <Setter Property="ItemsPanel">
        <Setter.Value>
            <ItemsPanelTemplate>
                <ItemsStackPanel Orientation="Horizontal" Background="Yellow"/>
            </ItemsPanelTemplate>
        </Setter.Value>
    </Setter>
    <Setter Property="Template">
        <Setter.Value>
            <ControlTemplate TargetType="ListView">
                <Border BorderBrush="{TemplateBinding BorderBrush}"
                    BorderThickness="{TemplateBinding BorderThickness}"
                    Background="{TemplateBinding Background}">
                    <ScrollViewer x:Name="ScrollViewer">
                        <!--ScrollViewer definitions removed for clarity-->
                        <ItemsPresenter FooterTransitions="{TemplateBinding FooterTransitions}"
                            FooterTemplate="{TemplateBinding FooterTemplate}"
                            Footer="{TemplateBinding Footer}"
                            HeaderTemplate="{TemplateBinding HeaderTemplate}"
                            Header="{TemplateBinding Header}"
                            HeaderTransitions="{TemplateBinding HeaderTransitions}"
                            Padding="{TemplateBinding Padding}"/>
                    </ScrollViewer>
                </Border>
            </ControlTemplate>
        </Setter.Value>
    </Setter>
</Style>
```

**NOTE** 在 WPF 中，`ListView` 控件的模板看起来与 UWP 模板相似。`ItemsPresenter` 不提供 UWP `ItemsPresenter` 的许多属性，例如与过渡相关的属性。

有了这个资源，`ListView` 的定义变得简单，只需在 `ItemsSource` 获取数据之外再引用 `ListViewStyle2` 即可（代码文件 `Templates [WPF|UWP]/StyledList.xaml`）：

```xml
<ListView ItemsSource="{Binding Countries}" Margin="10"
    Style="{StaticResource ListViewStyle2}" />
```

新的视图显示在图 30.22 中。现在可以使用滚动条了。

![](img/3d365b72b289213a91ade7eb366b8f35_1136_0.png)

图 30.22

## Animations

使用动画，您可以通过移动元素、颜色变化、变换等方式在图像之间实现平滑过渡。XAML 使创建动画变得容易。您可以为任何依赖属性的值设置动画。存在不同的动画类来为不同类型的属性值设置动画，具体取决于其类型。

动画中最重要的元素是时间线。该元素定义了值如何随时间变化。针对不同类型的值变化提供了不同种类的时间线。所有时间线的基类是 `Timeline`。要为类型为 `double` 的属性设置动画，可以使用类 `DoubleAnimation`。`Int32Animation` 是 `int` 值的动画类。您使用 `PointAnimation` 来为点设置动画，使用 `ColorAnimation` 来为颜色设置动画。

您可以通过使用 `Storyboard` 类来组合多个时间线。`Storyboard` 类本身派生自基类 `TimelineGroup`，后者派生自 `Timeline`。

> **NOTE** 动画类的命名空间在 WPF 中为 `System.Windows.Media.Animation`，在 UWP 应用中为 `Windows.UI.Xaml.Media.Animation`。

### Timeline

`Timeline` 定义了值如何随时间变化。以下示例对椭圆的大小进行动画处理。在下面的代码中，`DoubleAnimation` 时间线更改椭圆的缩放和位移；`ColorAnimation` 更改填充画刷的颜色。`Ellipse` 类的 `Triggers` 属性被设置为一个 `EventTrigger`。事件触发器在椭圆加载时触发。`BeginStoryboard` 是一个触发器动作，用于开始故事板。通过故事板，使用 `DoubleAnimation` 元素来为 `CompositeTransform` 类的 `ScaleX`、`ScaleY`、`TranslateX` 和 `TranslateY` 属性设置动画。动画在十秒内将水平缩放更改为 5，垂直缩放更改为 3（代码文件 `AnimationUWP/SimpleAnimation.xaml`）：

```xml
<Ellipse x:Name="ellipse1" Width="100" Height="40"
    HorizontalAlignment="Left" VerticalAlignment="Top">
    <Ellipse.Fill>
        <SolidColorBrush Color="Green" />
    </Ellipse.Fill>
    <Ellipse.RenderTransform>
        <CompositeTransform ScaleX="1" ScaleY="1" TranslateX="0" TranslateY="0" />
    </Ellipse.RenderTransform>
    <Ellipse.Triggers>
        <EventTrigger>
            <BeginStoryboard>
                <Storyboard x:Name="MoveResizeStoryboard">
                    <DoubleAnimation Duration="0:0:10" To="5" Storyboard.TargetName="ellipse1" Storyboard.TargetProperty="(UIElement.RenderTransform).(CompositeTransform.ScaleX)" />
                    <DoubleAnimation Duration="0:0:10" To="3" Storyboard.TargetName="ellipse1" Storyboard.TargetProperty="(UIElement.RenderTransform).(CompositeTransform.ScaleY)" />
                    <DoubleAnimation Duration="0:0:10" To="400" Storyboard.TargetName="ellipse1" Storyboard.TargetProperty="(UIElement.RenderTransform).(CompositeTransform.TranslateX)" />
                    <DoubleAnimation Duration="0:0:10" To="200" Storyboard.TargetName="ellipse1" Storyboard.TargetProperty="(UIElement.RenderTransform).(CompositeTransform.TranslateY)" />
                    <ColorAnimation Duration="0:0:10" To="Red" Storyboard.TargetName="ellipse1" Storyboard.TargetProperty="(Ellipse.Fill).(SolidColorBrush.Color)" />
                </Storyboard>
            </BeginStoryboard>
        </EventTrigger>
    </Ellipse.Triggers>
</Ellipse>
```

在 WPF 中，XAML 代码略有不同。因为没有 `CompositeTransform` 元素，所以使用 `TransformGroup` 元素（代码文件 `AnimationWPF/SimpleAnimation.xaml`）：

```xml
<Ellipse.RenderTransform>
    <TransformGroup>
        <ScaleTransform x:Name="scale1" ScaleX="1" ScaleY="1" />
        <TranslateTransform X="0" Y="0" />
    </TransformGroup>
</Ellipse.RenderTransform>
```

使用 `ScaleTransform` 和 `TranslateTransform` 会导致动画访问 `TransformGroup` 的集合，并通过索引器访问 `ScaleX`、`ScaleY`、`X` 和 `Y` 属性：

```xml
<DoubleAnimation Duration="0:0:10" To="5" Storyboard.TargetName="ellipse1" Storyboard.TargetProperty="(UIElement.RenderTransform).Children[0].(ScaleTransform.ScaleX)" />
<DoubleAnimation Duration="0:0:10" To="3" Storyboard.TargetName="ellipse1" Storyboard.TargetProperty="(UIElement.RenderTransform).Children[0].(ScaleTransform.ScaleY)" />
<DoubleAnimation Duration="0:0:10" To="400" Storyboard.TargetName="ellipse1" Storyboard.TargetProperty="(UIElement.RenderTransform).Children[1].(TranslateTransform.X)" />
<DoubleAnimation Duration="0:0:10" To="200" Storyboard.TargetName="ellipse1" Storyboard.TargetProperty="(UIElement.RenderTransform).Children[1].(TranslateTransform.Y)" />
```

除了在变换组中使用索引器之外，还可以通过其名称访问 `ScaleTransform` 元素。以下代码简化了属性的名称：

```xml
<DoubleAnimation Duration="0:0:10" To="5"
    Storyboard.TargetName="scale1"
    Storyboard.TargetProperty="(ScaleX)" />
```

在 WPF 中，还需要在 `EventTrigger` 中指定 `RoutedEvent` 属性。在 Windows 通用应用中，事件会在元素加载时自动触发。这可以在 WPF 中显式指定：

```xml
<EventTrigger RoutedEvent="Loaded">
    <BeginStoryboard>
```

图 30.23 和图 30.24 显示了动画椭圆的两个状态。

![](img/3d365b72b289213a91ade7eb366b8f35_1138_0.png)

图 30.23

![](img/3d365b72b289213a91ade7eb366b8f35_1138_1.png)

图 30.24

动画远不止是不断出现并立即显示的典型窗口装饰动画。您可以为业务应用程序添加动画，使用户界面感觉更具响应性。光标移动到按钮上或按钮被点击时的外观由动画定义。

下表描述了您可以使用时间线做什么。

| 时间线属性 | 描述 |
|---|---|
| `AutoReverse` | 使用此属性指定动画的值在动画结束后是否应返回到其原始值。 |
| `SpeedRatio` | 使用此属性转换动画移动的速度。您可以在相对于父级的关系中定义它。默认值是 1；将比率设置为较小的值会使动画移动变慢；将值设置为大于 1 会使其移动更快。 |
| `BeginTime` | 使用此项指定从触发事件开始到动画开始时刻的时间跨度。您可以指定天、小时、分钟、秒以及秒的小数部分。这可能不是实际时间，具体取决于速度比率。例如，如果速度比率设置为 2，且开始时间设置为六秒，则动画将在三秒后开始。 |
| `Duration` | 使用此属性指定动画一次迭代的持续时间。 |
| `RepeatBehavior` | 将 `RepeatBehavior` 结构分配给 `RepeatBehavior` 属性后，您可以定义动画应重复多少次或重复多长时间。 |
| `FillBehavior` | 如果父时间线具有不同的持续时间，则此属性很重要。例如，如果父时间线短于实际动画的持续时间，将 `FillBehavior` 设置为 `Stop` 意味着实际动画停止。如果父时间线长于实际动画的持续时间，`HoldEnd` 会在重置为其原始值之前保持实际动画处于活动状态（如果设置了 `AutoReverse`）。 |

根据 `Timeline` 类的类型，可能还有更多属性可用。例如，使用 `DoubleAnimation`，您可以为动画的开始和结束指定 `From` 和 `To` 属性。另一种选择是指定 `By` 属性，其中动画以 `Bound` 属性的当前值为起点，并按 `By` 指定的值递增。

### 缓动函数

到目前为止您看到的动画中，值以线性方式变化。在现实生活中，运动永远不会以线性方式发生。运动可能会缓慢开始并逐渐变快，直到达到最高速度，然后在到达终点前减速。当您让球掉落到地面时，球会在停在地面之前弹跳几次。这种非线性行为可以通过使用缓动函数来创建。
