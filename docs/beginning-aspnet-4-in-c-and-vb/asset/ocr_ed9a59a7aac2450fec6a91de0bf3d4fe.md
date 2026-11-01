the right eye. The first and third animation changes the Canvas.Left position for the eyes, and the second and fourth animation changes Canvas.Top. The animations in x and y direction have different time values that make the eye movement very interesting using the defined repeated behavior.

The second event trigger is fired as soon as the Click event of the buttonStopMoveEyes button occurs. Here, the storyboard is stopped with the StopStoryboard element, which references the started storyboard beginMoveEyes.

The third event trigger is fired by clicking the buttonResize button. With this animation the transformation of the Canvas element is changed. Because this animation doesn't run endlessly, there's no stop. This storyboard also makes use of the EaseFunction that was explained previously:

```
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
```