
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

In Listing 12.22, we have added two buttons to the application and an EventTrigger object to the Button control. On the click of the Start button, the animation starts and the circle along with the figure start moving. The AutoReverse property is set to True in the application. Therefore, when the circle reaches at the end of the window, it moves back again. The animation continues until you click the Stop button. When you click the Stop button, the figure stops moving and comes back to its original place. When you run the application by pressing the F5 key on the keyboard, you get the output, as shown in Figure 12.26:

![](img/e073a4882197be4ab61103cbe0bcb394_608_0.png)

Figure 12.26: Showing the Output of the EventTrigger Application

## Using Triggers

The most common way to start an animation in WPF is to use an EventTrigger. However, you can use the different types of triggers available in WPF to create an animation. For example, you can use property trigger to create animations in WPF. Let’s create animations in WPF using property triggers. To do this, create a WPF application named UsingTrigger (also available in the CD) and add the code, given in Listing 12.23, to the MainWindow.xaml file:

### Listing 12.23: Creating Trigger

```
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

In Listing 12.23, a Button control is added to the window on which the animation is applied with the help of a trigger. The Button control is initially blurred with the help of the Opacity property. When you run the application, by pressing the F5 key on the keyboard, a blurred button on the window is visible to you. When you move the mouse over the Button control, it becomes visible, and when you remove the mouse, the Button control again becomes blurred. You can see the output when the mouse is over the Button control in Figure 12.27:

![](img/e073a4882197be4ab61103cbe0bcb394_609_0.png)

## Changing the Speed of Animations

In WPF, you can change the speed of animation by using the AccelerationRatio and DecelerationRatio properties of the Timeline class. The AccelerationRatio property specifies the percentage of the timeline duration accelerating the passage of time from zero to its maximum. Similarly, the DecelerationRatio property specifies the percentage of timeline duration decelerating the passage of time from its maximum rate to zero. Let's create an application in which we are changing the speed of animation. To do this, create a WPF application named ChangingSpeed (also available in the CD) and add the code, given in Listing 12.24, to the MainWindow.xaml file:

### Listing 12.24: Using the AccelerationRatio and DecelerationRatio Properties

```
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
                            <DoubleAnimation Storyboard.TargetName="ellipse2"
                                Storyboard.TargetProperty="(Ellipse.Width)"
                                Duration="0:0:10" AccelerationRatio="0.4" From="105" To="250"/>
                            <DoubleAnimation Storyboard.TargetName="ellipse3"
                                Storyboard.TargetProperty="(Ellipse.Width)" Duration="0:0:10"
                                DecelerationRatio="0.6" From="105" To="250"/>
                            <DoubleAnimation Storyboard.TargetName="ellipse4"
                                Storyboard.TargetProperty="(Ellipse.Width)" Duration="0:0:10"
                                AccelerationRatio="0.4" DecelerationRatio="0.6" From="105"
                                To="250"/>
                        </Storyboard>
                    </BeginStoryboard>
                </EventTrigger>
            </Button.Triggers>
        </Button>
    </Grid>
</Window>
```

In Listing 12.24, four ellipses are added to the window and the animation is applied to all of them. The EventTrigger object is added on the click of the StartAnimation button. When you click the button, the ellipse starts increasing. The speed of increasing the width of the ellipse is different. The first ellipse increases with the speed specified in the Duration property. In the second ellipse, along with the Duration property, the AccelerationRatio property is also specified, which specifies the increasing speed of the ellipse. In the third ellipse, the Duration and DecelerationRatio properties are specified. In the fourth ellipse, along with the
