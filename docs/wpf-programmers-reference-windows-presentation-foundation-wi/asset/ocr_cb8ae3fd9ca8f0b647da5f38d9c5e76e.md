The following code shows the new style. This version includes the previous Setters plus ones
for the Label's BorderRadius and BorderThickness properties.

```
<Style x:Key="OrangeStyle" TargetType="Control">
  <Setter Property="Width" Value="150" />
  <Setter Property="Height" Value="40" />
  <Setter Property="Background" Value="Orange" />
  <Setter Property="Margin" Value="5" />
  <Setter Property="BorderBrush" Value="Yellow" />
  <Setter Property="BorderThickness" Value="2" />
</Style>
```

![](bbox=[0.645, 0.145, 0.875, 0.305])

The ControlExample program shown in Figure 13-3 uses the following code to display two
Buttons and a Label. The upper button uses OrangeButtonStyle; the lower Button and the
Label both use OrangeStyle.

```
<StackPanel VerticalAlignment="Center">
  <Button Style={StaticResource OrangeStyle} Content="Button" />
  <Button Style={StaticResource OrangeStyle} Content="Button" />
  <Label Style={StaticResource OrangeStyle} Content="Label" />
</StackPanel>
```

![](bbox=[0.645, 0.465, 0.875, 0.535])

# Multiple Target Types

The previous section explains how to build a style that can affect
two control types (Button and Label) by setting the Style's
TargetType to a class that is ancestor of both control types.
(Button and Label both inherit from Control.)

But if you also want the style to affect rectangles: Button
and Label have the Control class as a common ancestor, but
Rectangle inherits from the Shape class instead of Control.
If you climb a bit higher in the inheritance hierarchy,
ever you'll find that Control and Shape both inherit from
FrameworkElement, so you might think you're free. You could simply create a style with
TargetType FrameworkElement and buildters as usual.

![](bbox=[0.645, 0.545, 0.875, 0.705])

But, unfortunately, FrameworkElement doesn't support all of them. For example, if you
try to change the Style's TargetType to FrameworkElement, Expression Blend flags errors
on the Background, Foreground, BorderBrush, and BorderThickness properties.

The problem is that first common ancestor of Button, Label, and Rectangle doesn't support all
of the properties you'd like to use. Fortunately, there is another way to specify the objects that
provide the style's properties.

Instead of indicating the class with the Style element's TargetType attribute, indicate it in the
Setter's Property attribute.