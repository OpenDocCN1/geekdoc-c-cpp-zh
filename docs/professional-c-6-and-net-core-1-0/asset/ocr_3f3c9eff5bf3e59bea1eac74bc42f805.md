![](bbox=[0.105, 0.065, 0.896, 0.208])

Figure 30.22

# # Animations

Using animations, you can make a smooth transition between images by using moving elements, color changes, transforms, and so on. XAML makes it easy to create animations. You can animate the value of any dependency property. Different animation classes exist to animate the values of different properties, depending on their type.

The most important element of an animation is the timeline. This element defines how a value changes over time. Different kinds of timelines are available for changing different types of values. The base class for all timelines is `Timeline`. To animate a property of type double, you can use the class `DoubleAnimation`. The `Int32Animation` is the animation class for `int` values. You use `PointAnimation` to animate points and `ColorAnimation` to animate colors.

You can combine multiple timelines by using the `Storyboard` class. The `Storyboard` class itself is derived from the base class `TimelineGroup`, which derives from `Timeline`.

> > **NOTE** *The namespace for animation classes is with WPF `System.Windows.Media.Animation` and with UWP apps `Windows.UI.Xaml.Media.Animation`.*

# ## Timeline

A `Timeline` defines how a value changes over time. The following example animates the size of an ellipse. In the code that follows, `DoubleAnimation` timelines change scaling and translation of an ellipse; `ColorAnimation` changes the color of the fill brush. The `Triggers` property of the `Ellipse` class is set to an `EventTrigger`. The event trigger is fired when the ellipse is loaded. `BeginStoryboard` is a trigger action that begins the storyboard. With the storyboard, a `DoubleAnimation` element is used to animate the `ScaleX`, `ScaleY`, `TranslateX`, and `TranslateY` properties of the `CompositeTransform` class. The animation changes the horizontal scale to 5 and the vertical scale to 3 within ten seconds (code file `AnimationUWP/SimpleAnimation.xaml`):

```
```xml
<Ellipse x:Name="ellipse1" Width="100" Height="40"
```
```