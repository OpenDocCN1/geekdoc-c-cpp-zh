```
Storyboard.TargetProperty="Width" From="100" To="400"
Duration="0:0:2" FillBehavior="HoldEnd"/>
<DoubleAnimation Storyboard.TargetName="ellipse1"
Storyboard.TargetProperty="Width" From="100" To="400"
Duration="0:0:2" FillBehavior="Stop"/>
</Storyboard>
</BeginStoryboard>
</EventTrigger>
</Button.Triggers>
</Button>
</Grid>
</Window>
```

In Listing 12.27, there is an ellipse, a rectangle, and a button. The animation is attached on the click of the Start button. When you run the application by pressing the F5 key on the keyboard, and click at the Start button, the ellipse and the rectangle starts increasing. After the animation ends, the ellipse stays at the end, while the rectangle comes back to its original state. This is because, the FillBehavior property attached with the ellipse is set to Stop and the rectangle is set to HoldEnd. You can see the output after the animation ends in Figure 12.31:

![](bbox=[0.249, 0.369, 0.676, 0.581])

# Running Multiple Animations Simultaneously

In WPF, you can run multiple animations simultaneously by using the ParallelTimeline class. The animation starts according to the specified BeginTime property. The child timelines also run in parallel to each other. You can nest multiple Storyboards inside a ParallelTimeline element within a parent Storyboard. In this way, all the Storyboard timelines and their animations run in parallel to each other. Let’s create an animation that runs multiple animations concurrently. To do this, create a WPF application named MultipleAnimations (also available in CD) and add the code, given in Listing 12.28, to the MainWindow.xaml file.

```
Listing 12.28: Using the ParallelTimeline Class
<Window x:Class="MultipleAnimations.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="MainWindow" Height="300" Width="300">
    <Grid>
        <Grid.Triggers>
            <EventTrigger RoutedEvent="Button.Click">
                <EventTrigger.Actions>
                    <BeginStoryboard>
                        <Storyboard>
                            <ParallelTimeline>
                                <Storyboard Storyboard.TargetName="button1"
Storyboard.TargetProperty="(Background).(SolidColorBrush.Color)">
```