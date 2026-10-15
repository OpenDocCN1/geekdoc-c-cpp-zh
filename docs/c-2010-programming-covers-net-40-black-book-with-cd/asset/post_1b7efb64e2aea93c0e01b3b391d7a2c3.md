
Duration property, the AccelerationRatio and DecelerationRatio properties are also specified. When you run the application, by pressing the F5 key on the keyboard, the four ellipses along with the button on the window is visible to you. When you click the StartAnimation button, the ellipse starts growing according to the speed attached to the ellipse. You can see the output after clicking the button in Figure 12.28:

![](img/e073a4882197be4ab61103cbe0bcb394_611_0.png)

Figure 12.28: Changing the Speed of Animation

## Reversing the Animation

In WPF, you can reverse an animation by specifying its AutoReverse property to true of the Timeline class. The animation can reverse itself after completing a forward iteration. Let’s create an application in which you can reverse the animation. To do this, create a WPF application named ReversingAnimation (also available in CD) and add the code, given in Listing 12.25, to the MainWindow.xaml file:

### Listing 12.25: Using the AutoReverse Property

```
<window x:Class="ReversingAnimation.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="MainWindow" Height="300" Width="300">
<StackPanel>
<Rectangle Height="43" Name="rectangle1" Stroke="Black" Width="88" Fill="Red"/>
<Rectangle Height="43" Name="rectangle2" Stroke="Black" Width="88" Fill="Yellow"/>
<Button Height="23" Name="button1" Width="166">
StartAnimation
<Button.Triggers>
<EventTrigger RoutedEvent="Button.Click">
<BeginStoryboard>
<Storyboard>
<DoubleAnimation Storyboard.TargetName="rectangle1" Storyboard.TargetProperty="width" Duration="0:0:2" From="88" To="250" AutoReverse="False"/>
<DoubleAnimation Storyboard.TargetName="rectangle2" Storyboard.TargetProperty="width" Duration="0:0:2" From="88" To="250" AutoReverse="True"/>
</Storyboard>
</BeginStoryboard>
</EventTrigger>
</Button.Triggers>
</Button>
</StackPanel>
</window>
```

In Listing 12.25, two rectangles and a button are added to the window. The animation is attached on the Click event of the StartAnimation button. When you click the Button control, the width of the rectangles starts increasing. The first rectangle stops after increasing as the AutoReverse property is set to False. The second

rectangle first increases and then moves back to its original size as the AutoReverse property is set to True. You can see the output after the animation ends in Figure 12.29:

![](img/e073a4882197be4ab61103cbe0bcb394_612_0.png)

Figure 12.29: Reversing the Animation

## Controlling the Behavior of Animation

You can control the behavior of the animation in WPF by specifying the RepeatBehavior property of the Timeline class. The RepeatBehavior property controls the number of times an animation repeats itself. The default value of the RepeatBehavior property is set to 1.0, which implies that the animation plays one time and does not repeat itself. You can specify the number of times for repeating the animation or you can even set the RepeatBehavior property to Forever to repeat the animation indefinitely. Let’s create an application to control the behavior of the animation. To do this, create a WPF application named ControllingAnimation (also available in CD) and add the code, given in Listing 12.26, to the MainWindow.xaml file:

### Listing 12.26: Using the RepeatBehavior Property

```
```xml
<Window x:Class="ControllingAnimation.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="MainWindow" Height="300" Width="300">
    <StackPanel>
        <Rectangle Height="32" Name="rectangle1" Stroke="Black" Width="90" Fill="Pink"/>
        <Rectangle Height="32" Name="rectangle2" Stroke="Black" Width="90" Fill="Pink"/>
        <Rectangle Height="32" Name="rectangle3" Stroke="Black" Width="90" Fill="Pink"/>
        <Rectangle Height="32" Name="rectangle4" Stroke="Black" Width="90" Fill="Pink"/>
        <Button Height="23" Name="button1" Width="155">Start</Button>
        <StackPanel.Triggers>
            <EventTrigger SourceName="button1" RoutedEvent="Button.Click">
                <BeginStoryboard>
                    <Storyboard>
                        <DoubleAnimation Storyboard.TargetName="rectangle1"
                                         Storyboard.TargetProperty="Width" From="90" To="200"
                                         RepeatBehavior="Forever" Duration="0:0:2"/>
                        <DoubleAnimation Storyboard.TargetName="rectangle2"
                                         Storyboard.TargetProperty="Width" From="90" To="200"
                                         RepeatBehavior="0:0:2" Duration="0:0:2"/>
                        <DoubleAnimation Storyboard.TargetName="rectangle3"
                                         Storyboard.TargetProperty="Width" From="90" To="200"
                                         RepeatBehavior="5x" Duration="0:0:2"/>
                        <DoubleAnimation Storyboard.TargetName="rectangle4"
                                         Storyboard.TargetProperty="Width" From="90" To="200"
                                         Duration="0:0:2"/>
                    </Storyboard>
                </BeginStoryboard>
            </EventTrigger>
        </StackPanel.Triggers>
    </StackPanel>
</Window>
```
```

```
</StackPanel>
</window>
```

In Listing 12.26, four rectangles and a button are added to the window. The RepeatBehavior property is attached to all the four rectangles. When you run the application by pressing the F5 key on the keyboard, and click the Start button, the animation starts and the rectangle starts increasing. You notice that the first rectangle goes on increasing indefinitely, as the RepeatBehavior property attached with rectangle1 is set to Forever. The second rectangle stops increasing after 2 seconds, as the RepeatBehavior property attached with rectangle2 is set to 0:0:2. The third rectangle stops increasing after five instances, as the RepeatBehavior property attached with rectangle3 is set to 5x. The fourth rectangle increases only once and then stops, as there is no RepeatBehavior property attached with rectangle4. You can see the output after the animation starts in Figure 12.30:

![](img/e073a4882197be4ab61103cbe0bcb394_613_0.png)

Figure 12.30: Controlling the Animation

## Specifying the Behavior of Animation after Ending

The default behavior of the animation in WPF is to come back to its original size and location at the end. You can change the default behavior using the FillBehavior property, which is a property of the Timeline class that specifies the nature of animation after it has stopped. The different values of the FillBehavior property are Stop and HoldEnd. The Stop value of the FillBehavior property causes the animation to revert back to its normal state. The HoldEnd value of the FillBehavior property causes the animation to remain at the end value when the animation ends. Let’s create an animation in which you can specify the behavior of animation. To do this, create a WPF application named BehaviorofAnimation (also available in CD) and add the code, given in Listing 12.27, to the MainWindow.xaml file:

### Listing 12.27: Using the FillBehavior Property

```
<Window x:Class="BehaviorofAnimation.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="MainWindow" Height="300" Width="450">
    <Grid>
        <Ellipse Height="41" HorizontalAlignment="Left" Margin="10,10,0,0" Name="rectangle1" Stroke="Black" VerticalAlignment="Top" Width="100" Fill="CadetBlue"/>
        <Rectangle HorizontalAlignment="Left" Margin="10,81,0,0" Name="ellipse1" Stroke="Black" Width="100" Fill="Aquamarine" Height="31" VerticalAlignment="Top" />
        <Button Height="23" HorizontalAlignment="Left" Margin="22,0,0,79" Name="button1" VerticalAlignment="Bottom" Width="75">
            Start
            <Button.Triggers>
                <EventTrigger RoutedEvent="Button.Click">
                    <BeginStoryboard>
                        <Storyboard>
                            <DoubleAnimation Storyboard.TargetName="rectangle1"
```
