# Ellipse Button Triggers

When events occur, the template's triggers make appropriate changes to the control's appearance. Mostly these involve changing Opacity values to make some controls more visible while hiding others.

The IsMouseOver property shown in the following code is the most interesting of the plate's triggers:

```
<Trigger Property="IsMouseOver" Value="True">
  <Setter TargetName="ellipseLeftHighlight" Property="Opacity" Value="1"/>
  <Setter TargetName="ellipse" Property="Opacity" Value="0"/>
  <Setter TargetName="content" Property="Opacity" Value="1"/>
  <Setter TargetName="content" Property="BitmapEffect" Value="StaticResource bmeMouseOver"/>
  <Setter TargetName="sparkle" Property="Opacity" Value="0.75"/>

<!-- Start the sparkle animation. -->
<Trigger.EnterActions>
  <BeginStoryboard StoryName="begSparkle">
    <Storyboard BeginTime="0:0:1" RepeatBehavior="Forever">
      <DoubleAnimationUsingKeyFrames
        Duration="0:0:2"
        Storyboard.TargetName="transSparkle
        Storyboard.Target="Angle">
        <LinearDoubleKeyFrame
          Value="0" KeyTime="0:0:0"/>
        <LinearDoubleKeyFrame
          Value="360" KeyTime="0:0:1"/>
        <LinearDoubleKeyFrame
          Value="360" KeyTime="0:0:2"/>
      </DoubleAnimationUsingKeyFrames>
    </Storyboard>
  </BeginStoryboard>
</Trigger.EnterActions>

<!-- Stop the sparkle animation. -->
<Trigger.ExitActions>
  <StopStoryboard BeginName="begSparkle"/>
</Trigger.ExitActions>
</Trigger>
```

![](bbox=[0.785, 0.727, 0.873, 0.742])

This code uses simple setters to do the following immediately when it starts:

+   - Make the upper-left highlight fully opaque instead of translucent.
- Make the light gray color that tones down the other controls transparent so that all of the other controls have their full brightness.
- Make the ContentProperty fully opaque instead of translucent.