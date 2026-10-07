This list does not cover every way in which property values might be changed, but it covers the most intuitive and useful ways. The others are beyond the scope of this chapter. For more information on property value precedence, see Microsoft’s “Dependency Property Value Precedence” web page at mdn.microsoft.com/ms743230.aspx.

# NO STYLE

Suppose you have defined an unnamed style but don't want the style to apply to a particular control of type. Then you can control the Style to the special value (x:Null) to indicate that it should have no style. For example, the following code creates a Label that has no Style:

```
<Label Style="x:Null" Content="Test" />
```

# STYLE INHERITANCE

Resources you apply the same property values to multiple controls. Styles let you group resources into packages to make it even easier to give controls a common appearance.

Style inheritance lets you build one style based on another. That makes it easier still to give controls a common look and even if they don't share the same final styles.

The child inherits all of the Setters and other values defined by the parent style. You can then override some of those values if you like.

To make one style inherit from another, add a BasedOn attribute to its starting element, and set the attribute’s value to the parent Style. Note that the Style is an object defined in a resource dictionary, so you should set it with a StaticResource statement.

For example, the following code defines two brushes for Styles:

```
<LinearGradientBrush Key="GreenBrush" StartPoint="0,0" EndPoint="1,0">
  <GradientStop Color="Green" Offset="0"/>
  <GradientStop Color="Lime" Offset="0.3"/>
  <GradientStop Color="Transparent" Offset="0.8"/>
</LinearGradientBrush>
```

```
<LinearGradientBrush Key="BlueBrush" StartPoint="0,0" EndPoint="1,0">
  <GradientStop Color="Blue" Offset="0"/>
  <GradientStop Color="White" Offset="1"/>
</LinearGradientBrush>
```

```
<Style Key="SizeType" TargetType="FrameworkElement">
  <Setter Property="Width" Value="150"/>
  <Setter Property="Height" Value="30"/>
  <Setter Property="HorizontalAlignment" Value="Left"/>
  <Setter Property="VerticalAlignment" Value="Top"/>
  <Setter Property="Margin" Value="5"/>
</Style>
```