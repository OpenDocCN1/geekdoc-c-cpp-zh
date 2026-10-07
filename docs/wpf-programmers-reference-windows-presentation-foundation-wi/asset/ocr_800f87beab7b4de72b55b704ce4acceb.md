# EXAMPLE Using LinearGradientBrushes

The following code shows how the program Brushes shown in Figure G-1 creates its LinearGradientBrush:

```
<Ellipse Grid.Row="0" Grid.Column="2" Stroke="Black">
  <Ellipse.Fill>
    <LinearGradient StartPoint="0,0" EndPoint="0,1">
      <GradientStop Offset="0" Color="White"/>
      <GradientStop Offset="1" Color="Black"/>
    </LinearGradient>
  </Ellipse.Fill>
</Ellipse>
```

# RADIALGRADIENTBRUSH

A RadialGradientBrush fills areas with a color gradient that shades between two or more colors radially.

Table G-7 summarizes the RadialGradientBrush’s most important properties.

# TABLE G-7: Key Properties of RadialGradientBrush

| PROPERTY | PURPOSE |
|---|---|
| Center | The center point of the ellipse to which the gradient shades |
| GradientOrigin | The point where the gradient begins |
| GradientStops | A collection of objects that define the Brush’s colors at different parts of the gradient |
| MappingMode | Determines how the StartPoint and Endpoint are mapped to the Brush. This can be Absolute (the points' coordinates are in pixels) or RelativeToBounding[the point (0, 0) is the upper-left corner of the brush and (1, 1) is the lower-right corner]. |
| RadiusX | The X radius (half-width) of the outer ellipse to which the gradient shades |
| RadiusY | The Y radius (half-height) of the outer ellipse to which the gradient shades |
| SpreadMethod | Determines how an area is filled if the Brush doesn't completely cover it. This can be Pad, Reflect, or Repeat. |

The gradient starts at the object’s GradientOrigin point and shades to the edges of an ellipse centered at the point Center.