```
Storyboard.TargetName="medBoing"/>
</ParallelTimeline>

<!-- Move the ball and its shadow. -->
<ParallelTimeline BeginTime="0:0:0" AutoReverse="True">
<DoubleAnimationUsingKeyFrames
Storyboard.TargetName="ellBall"
Storyboard.TargetProperty="(Canvas.Top)"
<SplineDoubleKeyFrame KeyTime="0:0:1"
KeySpline="0.5,0 1,1"
Value="120"/>
</DoubleAnimationUsingKeyFrames>
<DoubleAnimationUsingKeyFrames
Storyboard.TargetName="ellShadow"
Storyboard.TargetProperty="Opacity">
<SplineDoubleKeyFrame KeyTime="0:0:1"
KeySpline="0.5,0 1,1"
Value="1"/>
</DoubleAnimationUsingKeyFrames>
</ParallelTimeline>
</Storyboard>
```

The Storyboard contains two ParallelTimeline objects that run independently. The first waits 1 second until the ball is touching the “ground” and then uses a MediaTimeline object to play the sound effect.

![](bbox=[0.21, 0.47, 0.53, 0.66])

The second ParallelTimeline contains two DoubleAnimationUsingKeyframes objects, one to control the ball's Canvas.Top property and one to control the shadow's Opacity. As the ball's animation moves the ball downward, the shadow's animation makes the shadow more opaque. When the animations end, the ball is touching the “ground,” and the shadow is fully opaque.

# TEMPLATES

Properties and styles determine a control's appearance and behavior.

In contrast, templates determine a control's structure. They determine what components make up the control and how those components interact to provide the control's features.