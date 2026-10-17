
```xml
Stroke="Black" Width="9" Fill="Blue" />

<Ellipse Canvas.Left="127" Canvas.Top="168" Height="10" Name="ellipse8"

Stroke="Black" Width="9" Fill="Blue" />

<Ellipse Canvas.Left="127" Canvas.Top="188" Height="10" Name="ellipse9"

Stroke="Black" Width="9" Fill="Blue" />

<Ellipse Canvas.Left="127" Canvas.Top="208" Height="10" Name="ellipse10"

Stroke="Black" Width="9" Fill="Blue" />

<Ellipse Canvas.Left="127" Canvas.Top="228" Height="10" Name="ellipse11"

Stroke="Black" Width="9" Fill="Blue" />

<Line X1="12" X2="400" Y1="145" Y2="115" Stroke="Black"

StrokeThickness="5" Height="158" Canvas.Left="131" Canvas.Top="114"

Width="42" />

<Path Name="path1" Stroke="Black" Data="M 60,113 Q 90,146 111,111"

StrokeThickness="5" Height="134" Canvas.Left="48" Canvas.Top="-14"

Width="145" />

<Line X1="124" X2="145" Y1="145" Y2="166" Stroke="Black"

StrokeThickness="5" Height="168" Canvas.Left="40" Canvas.Top="-7"

Width="147" />

<Line X1="145" X2="600" Y1="149" Y2="166" Stroke="Black"

StrokeThickness="5" Height="168" Canvas.Left="37" Canvas.Top="8"

Width="178" />

<Line X1="124" X2="170" Y1="145" Y2="16" Stroke="Black"

StrokeThickness="5" Height="115" Canvas.Left="-42" Canvas.Top="65"

Width="147" />

<Line X1="115" X2="145" Y1="145" Y2="166" Stroke="Black"

StrokeThickness="5" Height="168" Canvas.Left="-50" Canvas.Top="11"

Width="147" />

<Polygon Points="10,110 60,10 110,110" Fill="Blue" Height="55"

Canvas.Left="72" Canvas.Top="-7" Width="132" />

<Line X1="11" X2="145" Y1="145" Y2="166" Stroke="Black"

StrokeThickness="5" Height="163" Canvas.Left="83" Canvas.Top="110"

Width="41" />

<Line X1="145" X2="145" Y1="145" Y2="166" Stroke="Black"

StrokeThickness="5" Height="168" Canvas.Left="-23" Canvas.Top="94"

Width="151" />

<Line X1="145" X2="145" Y1="145" Y2="166" Stroke="Black"

StrokeThickness="5" Height="168" Canvas.Left="-1" Canvas.Top="94"

Width="147" />

<Line X1="11" X2="10" Y1="145" Y2="115" Stroke="Black"

StrokeThickness="5"

Height="158" Canvas.Left="121" Canvas.Top="-52" Width="42" />

<Polyline Name="Base" Points="10,110 6,10 110,110" Stroke="Black"

StrokeThickness="4" Height="52" Canvas.Left="209" Canvas.Top="210"

Width="50"/>

<Ellipse Canvas.Left="172" Canvas.Top="118" Height="100" Name="Ball"

Stroke="Black" Width="87">

<Ellipse.BitmapEffect>

<OuterGlowBitmapEffect GlowColor="DarkViolet" />

</Ellipse.BitmapEffect>

</Ellipse>

<Button Canvas.Left="235" Canvas.Top="12" Height="23"

Name="StartAnimation" Width="75">Start</Button>

<Button Canvas.Left="235" Canvas.Top="45" Height="23"

Name="StopAnimation" Width="75">Stop</Button>

</Canvas>

</Grid>

<DockPanel.Triggers>
```

```

<EventTrigger RoutedEvent="Button.Click" sourceName="StartAnimation">

  <BeginStoryboard Name="StartMoveBall">

    <Storyboard Name="MoveBall">

      <DoubleAnimation RepeatBehavior="Forever" AccelerationRatio="0.4" DecelerationRatio="0.4" AutoReverse="True" By="100" Duration="0:0:3" Storyboard.TargetName="Ball" Storyboard.TargetProperty="(Canvas.Left)"/>

    </Storyboard>

  </BeginStoryboard>

</EventTrigger>

<EventTrigger RoutedEvent="Button.Click" sourceName="StartAnimation">

  <BeginStoryboard Name="StartTable">

    <Storyboard Name="Table">

      <DoubleAnimation RepeatBehavior="Forever" AccelerationRatio="0.4" DecelerationRatio="0.4" AutoReverse="True" By="100" Duration="0:0:3" Storyboard.TargetName="Base" Storyboard.TargetProperty="(Canvas.Left)"/>

    </Storyboard>

  </BeginStoryboard>

</EventTrigger>

<EventTrigger RoutedEvent="Button.Click" sourceName="StopAnimation">

  <StopStoryboard BeginStoryboardName="StartMoveBall"/>

</EventTrigger>

<EventTrigger RoutedEvent="Button.Click" sourceName="StopAnimation">

  <StopStoryboard BeginStoryboardName="StartTable"/>

</EventTrigger>

</DockPanel.Triggers>

</DockPanel>

</Window>
```

在清单 12.22 中，我们向应用程序添加了两个按钮，并在 `Button` 控件上添加了一个 `EventTrigger` 对象。点击 `Start` 按钮时，动画开始，圆圈以及图形开始移动。应用程序中 `AutoReverse` 属性被设置为 `True`。因此，当圆圈到达窗口末端时，它会再次向后移动。动画会一直持续，直到你点击 `Stop` 按钮。点击 `Stop` 按钮时，图形停止移动并回到原始位置。当你通过按下键盘上的 `F5` 键运行应用程序时，你会得到输出，如图 12.26 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_608_0.png)

图 12.26：显示 `EventTrigger` 应用程序的输出

## 使用触发器

在 WPF 中启动动画最常见的方法是使用 `EventTrigger`。然而，你可以使用 WPF 中可用的不同类型的触发器来创建动画。例如，你可以使用属性触发器在 WPF 中创建动画。让我们使用属性触发器在 WPF 中创建动画。为此，创建一个名为 `UsingTrigger` 的 WPF 应用程序（也在 CD 上提供）并将清单 12.23 中给出的代码添加到 `MainWindow.xaml` 文件中：

### Listing 12.23: Creating Trigger

```xml
<Window x:Class="UsingTrigger.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="MainWindow" Height="300" Width="300">
    <Window.Resources>
        <Style x:Key="PropertyTrigger" TargetType="{x:Type Button}">
            <Setter Property="Opacity" Value="0.5" />
            </Setter>
        <Style.Triggers>
            <Trigger Property="IsMouseOver" Value="True">
                <Trigger.EnterActions>
                    <BeginStoryboard>
                        <Storyboard>
                            <DoubleAnimation Storyboard.TargetProperty="Opacity" To="1" Duration="0:0:1"/>
                        </Storyboard>
                    </BeginStoryboard>
                </Trigger.EnterActions>
                <Trigger.ExitActions>
                    <BeginStoryboard>
                        <Storyboard>
                            <DoubleAnimation Storyboard.TargetProperty="Opacity" To="0.5" Duration="0:0:1"/>
                        </Storyboard>
                    </BeginStoryboard>
                </Trigger.ExitActions>
            </Trigger>
        </Style.Triggers>
        </Style>
    </Window.Resources>
    <StackPanel>
        <Button Style="{StaticResource PropertyTrigger}">
            Move the Mouse over me to Start Animation
        </Button>
    </StackPanel>
</Window>
```

在清单 12.23 中，一个 `Button` 控件被添加到窗口上，动画通过触发器应用于它。`Button` 控件最初通过 `Opacity` 属性变得模糊。当你通过按下键盘上的 `F5` 键运行应用程序时，一个模糊的按钮在窗口上可见。当你将鼠标移至 `Button` 控件上时，它变得可见，而当你移开鼠标时，`Button` 控件再次变得模糊。你可以在图 12.27 中看到鼠标位于 `Button` 控件上时的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_609_0.png)

## 更改动画速度

在 WPF 中，你可以通过使用 `Timeline` 类的 `AccelerationRatio` 和 `DecelerationRatio` 属性来更改动画的速度。`AccelerationRatio` 属性指定时间轴持续时间的百分比，用于将时间流逝从零加速到其最大值。同样，`DecelerationRatio` 属性指定时间轴持续时间的百分比，用于将时间流逝从其最大速率减速到零。让我们创建一个应用程序，在其中更改动画的速度。为此，创建一个名为 `ChangingSpeed` 的 WPF 应用程序（也在 CD 上提供）并将清单 12.24 中给出的代码添加到 `MainWindow.xaml` 文件中：

### Listing 12.24: Using the AccelerationRatio and DecelerationRatio Properties

```xml
<Window x:Class="ChangingSpeed.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="MainWindow" Height="300" Width="300">
    <Grid>
        <Ellipse Height="30" Margin="9,29,0,0" Name="ellipse1" Stroke="Black"
            VerticalAlignment="Top" HorizontalAlignment="Left" Width="105" Fill="Red"/>
        <Ellipse Height="30" Margin="9,60,0,0" Name="ellipse2" Stroke="Black"
            VerticalAlignment="Top" HorizontalAlignment="Left" Width="105" Fill="Yellow"/>
        <Ellipse Height="30" Margin="9,92,0,0" Name="ellipse3" Stroke="Black"
            VerticalAlignment="Top" HorizontalAlignment="Left" Width="105" Fill="Green"/>
        <Ellipse Margin="9,121,0,111" Name="ellipse4" Stroke="Black"
            HorizontalAlignment="Left" Width="105" Fill="Red"/>
        <Button HorizontalAlignment="Left" Margin="9,0,0,15" Name="button1"
            Width="95" Height="23" VerticalAlignment="Bottom">
            StartAnimation
            <Button.Triggers>
                <EventTrigger RoutedEvent="Button.Click">
                    <BeginStoryboard>
                        <Storyboard>
                            <DoubleAnimation Storyboard.TargetName="ellipse1"
                                Storyboard.TargetProperty="(Ellipse.Width)"
                                Duration="0:0:10" From="105" To="250"/>
```
