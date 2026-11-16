# PUT ON YOUR THINKING HAT

![](bbox=[0.1, 0.05, 0.19, 0.21])

Here's a pair of simple animations that change the size of a button when the mouse enters and leaves it. Create a new project with a few buttons inside a StackPanel, add the style to the `<Resources>` element of the app.xaml file, and then answer the questions below.

```
<Style TargetType="Button">
<Style.Triggers>
<EventTrigger RoutedEvent="Button.MouseEnter">
<BeginStoryboard>
<Storyboard>
<DoubleAnimation Storyboard.TargetProperty="FontSize" To="36" />
<DoubleAnimation Storyboard.TargetProperty="Height" To="75" />
</Storyboard>
</BeginStoryboard>
</EventTrigger>
<EventTrigger RoutedEvent="Button.MouseLeave">
<BeginStoryboard>
<Storyboard >
<DoubleAnimation Storyboard.TargetProperty="FontSize" />
<DoubleAnimation Storyboard.TargetProperty="Height" />
</Storyboard>
</BeginStoryboard>
</EventTrigger>
</Style.Triggers>
</Style>
```

By omitting the From property, the animation starts with the current value of the property.

You can use the attached TargetProperty to specify a different target for each Timeline.

By omitting both From and To, the animation returns the property to its original value.

+   - The animation won't work unless you explicitly set the Height property of the buttons. Can you figure out why?
+   - What happens if you change the Height property of the MouseEnter animation to By="25" and then reenter the button before it finishes returning to its original size? Can you think of situations in which this might be the behavior you want?
+   - Try adding an easing function to the Height animation of the MouseEnter Storyboard. The Framework defines several. (Intellisense will help you out here.) Which one do you think is most appropriate in this situation?
+   - When you set TargetProperty to an attached property, you need to wrap the property in parentheses: Foreground.(SolidColorBrush.Color). Using this syntax, try adding a ColorAnimation that changes the text color.

![](bbox=[0.64, 0.72, 0.91, 0.88])