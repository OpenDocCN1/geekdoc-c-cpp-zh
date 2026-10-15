# Adding Animations Using the TextEffect Class

The TextEffect class is mainly used to apply animations to the text. Let’s create a WPF application named Animation_TextEffect (also available on the CD-ROM) to learn how to add an animation to the text using the TextEffect class. For this, add the code given in Listing 11.7 to MainWindow.xaml of Animation_TextEffect.

```
**Listing 11.7: Adding Animation to the Text**

```xml
<Window x:Class="Animation_TextEffect.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="MainWindow" Height="300" Width="300">
    <Grid>
        <TextBlock FontSize="50" TextAlignment="Center" Margin="0,86,0,48">Hello
            <TextBlock.TextEffects>
                <TextEffect PositionStart="1" PositionCount="3" x:Name="myEffect">
                    <TextEffect.Transform>
                        <RotateTransform x:Name="myTransform" Angle="0" CenterX="10"
                        CenterY="10"/>
                    </TextEffect.Transform>
                </TextEffect>
            </TextBlock.TextEffects>
            <TextBlock.Triggers>
                <EventTrigger RoutedEvent="TextBlock.Loaded">
                    <EventTrigger.Actions>
                        <BeginStoryboard>
                            <Storyboard>
                                <ParallelTimeline RepeatBehavior="Forever">
                                    <DoubleAnimation Storyboard.TargetName="myTransform"
                                    Storyboard.TargetProperty="Angle" From="0" To="360" Duration="0:0:0.5"
                                    BeginTime="0:0:0" RepeatBehavior="1x" AutoReverse="False" />
                                </ParallelTimeline>
                            </Storyboard>
                        </BeginStoryboard>
                    </EventTrigger.Actions>
                </EventTrigger>
            </TextBlock.Triggers>
        </TextBlock>
    </Grid>
</Window>
```
```

In Listing 11.7, the animation is applied to the middle three letters of the word Hello. The text revolves around the path that is set within MainWindow for a fixed duration of time. The output of Listing 11.7 is shown in Figure 11.7:

![](bbox=[0.225, 0.693, 0.703, 0.894])

**Figure 11.7:** Showing the Output of the Animation_TextEffect Application