Give the ContentPresenter an OuterGlowmapEffect (defined in the template's
Resources section).

Make the white sparkle highlight visible with Opacity = 0.75. This makes the left edge
high brighter than the right highlight and prepares the sparkle for the animation
described next.

The Trigger's EnterActions occur when the MouseOver property becomes True. This code begins
a Storyboard that uses a DoubleAnimationUsingKeyFrames object to animate the sparkle highlight
bush. The brush uses a RotateTransform named sparkle that initially has Angle = 0, so the
bush is not rotated. The animation makes Angle sweep from 0 to 360 degrees over a 1-second period.
and repeats indefinitely.

The Trigger's ExitActions occur when the MouseOver property becomes no longer True (in
other words, becomes False). When that happens, the code stops the Storyboard that animates
the sparkle.

The Template's other triggers are much simpler. for the following code shows the IsPressed
property that executes when the user presses the button:

```
<Trigger IsPressed="True">
  <Setter TargetName="ellipseLeftHighlight" Property="Opacity" Value="0"/>
  <Setter TargetName="ellipseRightHighlight" Property="Opacity" Value="0.75"/>
  <Setter TargetName="cpContent" Property="BitmapEffect"
  Value="StaticResource bmePressed"/>
</Trigger>
```

![](bbox=[0.078, 0.448, 0.158, 0.535])

EllipseButton

This code uses some setters to do the following:

+   - Hide the upper-light highlight by setting Opacity = 0.
- Display the lower-right highlight by setting Opacity = 0.75.
- Give the ContentPresenter the OuterGlowmapEffect named bmePressed. This
effect, which is defined in the template's Resources section, uses a larger GlowSize than thenMouseOver effect, so the glow of the ContentPresenter is larger. You can see the
difference if you compare Figures 15-10 and 15-11.

The template's other triggers show in the following code work similarly:

```
<!-- Default -->
<Trigger Property="IsDefault" Value="True">
  <Setter TargetName="ellCover" Property="Opacity" Value="0.15"/>
  <Setter TargetName="ellEdgeHighlight" Property="Stroke"
  Value="StaticResource brDefaultEdgeHighlight"/>
</Trigger>

<!-- Not defaulted. -->
```

![](bbox=[0.078, 0.773, 0.158, 0.86])