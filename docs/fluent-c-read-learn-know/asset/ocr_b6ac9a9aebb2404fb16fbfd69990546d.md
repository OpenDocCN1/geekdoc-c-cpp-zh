Add an easing function to the Height animation of the MouseEnter Storyboard. Which one do you think is most appropriate in this situation?

```
<DoubleAnimation Storyboard.TargetProperty="Height" To="75" >
    <DoubleAnimation.EasingFunction>
        <BackEase />
    </DoubleAnimation.EasingFunction>
</DoubleAnimation>
```

Each of the easing functions exposes some properties to control them, but they also work pretty well in their default configuration.

Aren't easing functions fun? I think the BackEase is best here, but that's a judgement call, and you might have preferred a different one.

When you set TargetProperty to an attached property, you need to wrap the property in parentheses: (Foreground.(SolidColorBrush.Color). Using this syntax, try adding a ColorAnimation that changes the text color.

```
<ColorAnimation Storyboard.TargetProperty="Foreground.(SolidColorBrush.Color)" To="Green" />
```

In this example, (Foreground).(SolidColorBrush.Color) works, but (Foreground).(SolidColorBrush).(Color) doesn't, because Color isn't an attached property. Sometimes it just takes a little trial and error to work out the exact syntax.