
<ContentPresenter VerticalAlignment="Center" HorizontalAlignment="Center" />
<Grid>
<ControlTemplate.Triggers>
    <Trigger Property="IsMouseOver" Value="True">
        <Trigger.EnterActions>
            <BeginStoryboard>
                <Storyboard>
                    <DoubleAnimation Duration="0:0:0.3" AutoReverse="True" Storyboard.TargetProperty="(Rectangle.StrokeThickness)" Storyboard.TargetName="outline" By="1.2" />
                </Storyboard>
            </BeginStoryboard>
        </Trigger.EnterActions>
    </Trigger>
</ControlTemplate.Triggers>
</ControlTemplate>
<Setter.Value>
</Setter>
</Style>
<Window.Resources>
<Grid>
    <Button Style="{StaticResource AnimatedButtonStyle}" Width="200" Height="100" Content="Click Me!" />
</Grid>
</Window.Resources>

*代码片段 AnimationDemo/ButtonAnimationWindow.xaml*

以下表格列出了可以使用时间线执行的操作。

| 时间线属性 | 描述 |
|---|---|
| AutoReverse | 使用 AutoReverse 属性，您可以指定动画结束后，动画值是否应返回到原始值。 |
| SpeedRatio | 使用 SpeedRatio，您可以更改动画移动的速度。使用此属性，您可以定义相对于父级的关系。默认值为 1；将该值设置为更小会使动画移动得更慢；设置为大于 1 的值会使动画移动得更快。 |
| BeginTime | 使用 BeginTime，您可以指定从触发事件开始到动画启动那一刻之间的时间跨度。您可以指定天、小时、分钟、秒和秒的小数部分。这可能不是实时时间，具体取决于速度比率。例如，如果速度比率设置为 2，开始时间设置为 6 秒，则动画将在 3 秒后启动。 |
| AccelerationRatio DecelerationRatio | 对于动画，值不必以线性方式变化。您可以指定 AccelerationRatio 和 DecelerationRatio 来定义加速和减速的影响。两者的总和不得大于 1。 |
| Duration | 使用 Duration 属性，您可以指定动画一次迭代的持续时间。 |
| RepeatBehavior | 为 RepeatBehavior 属性分配 RepeatBehavior 结构，可以定义动画应重复的次数或持续时间。 |
| FillBehavior | 如果父时间线具有不同的持续时间，则 FillBehavior 属性很重要。例如，如果父时间线比实际动画的持续时间短，则将 FillBehavior 设置为 Stop 意味着实际动画停止。如果父时间线比实际动画的持续时间长，则 HoldEnd 会在将实际动画重置为其原始值（如果设置了 AutoReverse）之前保持其活动状态。 |

右眼。第一个和第三个动画更改眼睛的 Canvas.Left 位置，第二个和第四个动画更改 Canvas.Top。x 和 y 方向上的动画具有不同的时间值，结合定义的重复行为，使眼球运动非常有趣。

第二个事件触发器在 buttonStopMoveEyes 按钮的 Click 事件发生时触发。在这里，通过 StopStoryboard 元素停止情节提要，该元素引用了已启动的情节提要素 beginMoveEyes。

第三个事件触发器通过单击 buttonResize 按钮触发。通过此动画，Canvas 元素的变换会发生变化。由于此动画不会无限运行，因此没有停止。此情节提要还使用了前面解释过的 EasingFunction：

```xml
<Window x:Class="AnimationDemo.EventTriggerWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="EventTriggerWindow" Height="300" Width="300">
<DockPanel>
<EventTrigger>
<EventTrigger RoutedEvent="Button.Click" SourceName="buttonBeginMoveEyes">
<BeginStoryboard x:Name="beginMoveEyes">
<Storyboard>
<DoubleAnimation RepeatBehavior="Forever" DecelerationRatio=".8"
AutoReverse="True" By="6" Duration="0:0:1"
Storyboard.TargetName="eyeLeft"
Storyboard.TargetProperty="(Canvas.Left)" />
<DoubleAnimation RepeatBehavior="Forever" AutoReverse="True"
By="5" Duration="0:0:5"
Storyboard.TargetName="eyeLeft"
Storyboard.TargetProperty="(Canvas.Top)" />
<DoubleAnimation RepeatBehavior="Forever" DecelerationRatio=".8"
AutoReverse="True" By="-6" Duration="0:0:3"
Storyboard.TargetName="eyeRight"
Storyboard.TargetProperty="(Canvas.Left)" />
<DoubleAnimation RepeatBehavior="Forever" AutoReverse="True"
By="6" Duration="0:0:6"
Storyboard.TargetName="eyeRight"
Storyboard.TargetProperty="(Canvas.Top)" />
</Storyboard>
</BeginStoryboard>
</EventTrigger>
<EventTrigger RoutedEvent="Button.Click" SourceName="buttonStopMoveEyes">
<StopStoryboard BeginStoryboardName="beginMoveEyes" />
</EventTrigger>
<EventTrigger RoutedEvent="Button.Click" SourceName="buttonResize">
<BeginStoryboard>
<Storyboard>
<DoubleAnimation RepeatBehavior="2" AutoReverse="True"
Storyboard.TargetName="scale1"
Storyboard.TargetProperty="(ScaleTransform.ScaleX)"
From="0.1" To="3" Duration="0:0:5">
<DoubleAnimation.EasingFunction>
<ElasticEase />
</DoubleAnimation.EasingFunction>
</DoubleAnimation>
<DoubleAnimation RepeatBehavior="2" AutoReverse="True"
Storyboard.TargetName="scale1"
Storyboard.TargetProperty="(ScaleTransform.ScaleY)"
From="0.1" To="3" Duration="0:0:5">
<DoubleAnimation.EasingFunction>
<BounceEase />
</DoubleAnimation.EasingFunction>
</DoubleAnimation>
</Storyboard>
</BeginStoryboard>
</EventTrigger>
</DockPanel>
</Window>
```

DoubleAnimationUsingKeyFrames 是用于 double 类型的关键帧动画。其他关键帧动画类型包括 Int32AnimationUsingKeyFrames、PointAnimationUsingKeyFrames、ColorAnimationUsingKeyFrames、SizeAnimationUsingKeyFrames 和 ObjectAnimationUsingKeyFrames。

示例 XAML 代码通过动画处理 `TranslateTransform` 元素的 X 和 Y 值，实现了椭圆位置的动画。动画在椭圆加载时启动，方法是为 `RoutedEvent` `Ellipse.Loaded` 定义一个 `EventTrigger`。事件触发器通过 `BeginStoryboard` 元素启动一个 `Storyboard`。`Storyboard` 包含两个 `DoubleAnimationUsingKeyFrame` 类型的关键帧动画。关键帧动画由帧元素组成。第一个关键帧动画使用 `LinearKeyFrame`、`DiscreteDoubleKeyFrame` 和 `SplineDoubleKeyFrame`；第二个动画是 `EasingDoubleKeyFrame`。`LinearDoubleKeyFrame` 使值发生线性变化。`KeyTime` 属性定义应在动画中的何时达到 `Value` 属性的值。在这里，`LinearDoubleKeyFrame` 有三秒时间将属性 X 移动到值 30。`DiscreteDoubleKeyFrame` 在四秒后立即变为新值。`SplineDoubleKeyFrame` 使用贝塞尔曲线，其中两个控制点由 `KeySpline` 属性指定。`EasingDoubleKeyFrame` 是 .NET 4 中新增的帧类，支持设置缓动函数（如 `BounceEase`）来控制动画值：

```xml
<Canvas>
    <Ellipse Fill="Red" Canvas.Left="20" Canvas.Top="20" Width="25" Height="25">
        <Ellipse.RenderTransform>
            <TranslateTransform X="50" Y="50" x:Name="ellipseMove" />
        </Ellipse.RenderTransform>
        <Ellipse.Triggers>
            <EventTrigger RoutedEvent="Ellipse.Loaded">
                <BeginStoryboard>
                    <Storyboard>
                        <DoubleAnimationUsingKeyFrames Storyboard.TargetProperty="X"
                                Storyboard.TargetName="ellipseMove">
                            <LinearDoubleKeyFrame KeyTime="0:0:2" Value="30" />
                            <DiscreteDoubleKeyFrame KeyTime="0:0:4" Value="80" />
                            <SplineDoubleKeyFrame KeySpline="0.5,0,0.5,0.0"
                                KeyTime="0:0:10" Value="50" />
                            <LinearDoubleKeyFrame KeyTime="0:0:20" Value="150" />
                        </DoubleAnimationUsingKeyFrames>
                        <DoubleAnimationUsingKeyFrames Storyboard.TargetProperty="Y"
                                Storyboard.TargetName="ellipseMove">
                            <SplineDoubleKeyFrame KeySpline="0.5,0,0.0,0.9"
                                KeyTime="0:0:2" Value="50" />
                            <EasingDoubleKeyFrame KeyTime="0:0:20" Value="300">
                                <EasingDoubleKeyFrame.EasingFunction>
                                    <BounceEase />
                                </EasingDoubleKeyFrame.EasingFunction>
                            </EasingDoubleKeyFrame>
                        </DoubleAnimationUsingKeyFrames>
                    </Storyboard>
                </BeginStoryboard>
            </EventTrigger>
        </Ellipse.Triggers>
    </Ellipse>
</Canvas>
```

*代码片段 AnimationDemo/KeyFrameWindow.xaml*

## 可视化状态管理器

自 .NET 4 起，可视化状态管理器提供了一种控制动画的替代方法。控件可以具有特定状态。状态定义了一种在达到该状态时应用于控件的外观。状态转换定义了当一个状态变为另一个状态时会发生什么。

