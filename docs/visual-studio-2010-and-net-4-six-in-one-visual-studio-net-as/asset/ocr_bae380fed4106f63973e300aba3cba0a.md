Blend SDK installed, you can still launch the Storyboard from code-behind by adding Storyboard.Begin(); to the end of the constructor. You'll learn more about triggers, actions and behaviors in this chapter.

The root animation is called a Storyboard. The Storyboard has one or more child Animations that, in turn, sample, animate a single property on a single element. In the previous sample, Storyboard has two animations that control the Canvas.Left and Canvas.Top properties of the Ellipse. A single Storyboard can have child animations that affect different elements.

Child animations share the same clock. This means that starting the animations happens simultaneously. A Storyboard can be paused, reversed, seized, sought, or the common clock's speed can be changed (via the SpeedRatio property), thus making the entire Storyboard slower or faster.

![](bbox=[0.64, 0.096, 0.93, 0.27])

Animations can change properties of any type. However, they only work with dependency properties. There are different animations for different property types:

+   * DoubleAnimation for animating double properties (such as position and opacity).
* ColorAnimation for animating colors (Brushes)
* PointAnimation for Points.

+   * ObjectAnimation for changing properties of other types. ObjectAnimation does not support interpolation, because you can only set 30 percent of the Visibility property to Collapsed.

Another aspect of Silverlight and WPF animations is that the From property can be omitted. In this case, the value will navigate from its current value to the specified To value — as in the case of a panel sliding out when hovered, and sliding in the mouse leaves. With relative animations, extra code would be written to stop the panel from jumping when the mouse is moved off it before fully opens.

To make even more natural, Silverlight has keyframe and easing functionality. Keyframes help in cases when a simple value-to-value animation is not enough, and several, precisely controlled in-points are defined. Keyframes can also be used for discrete jumps between values, without interpolation.

Easing can also slow down, or even behave spring-like. For example, by adding BounceEasing function to the previous Canvas.Top animation, you can achieve the bouncing ball effect, as shown in Figure 8-26. Here is the part of the XAML that changed:

```
<DoubleAnimation TargetProperty="Canvas.Top" 
Storyboard.TargetName="ellipse" To="230" 
<DoubleAnimation.EasingFunction>
```

FIGURE 8-25: Simple animation