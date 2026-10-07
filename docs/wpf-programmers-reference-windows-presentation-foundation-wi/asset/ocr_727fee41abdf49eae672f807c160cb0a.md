# TABLE F-1 (continued)

| PROPERTY | PURPOSE |
| --- | --- |
| StrokeMiterLimit | Determines how pointy a corner can be when two segments connect as in a Polygon. |
| StrokeStartLineCap | Determines the shape of the Pen's starting end. This can be Flat, Round, Square, or Triangle. |
| StrokeThickness | Determines the Pen's thickness.

# EXAMPLE Understanding StrokeMiterLimit

The StrokeMiterLimit example program in Figure F-1 uses the following code to draw its shape. This example defines the Pen's Stroke property with an element attribute containing a RadialGradientBrush. It also sets StrokeMiterLimit to 3 as the sharpest corner on the lower right is visible.

```
<Polygon Points="100.3,30.2,250.0,30.7,200.5,75,170*" StrokeThickness="20"
<StrokeLineJoin="Miter" StrokeMiterLimit="3">
<Polygon.Stroke>
  <RadialGradientBrush>
    <GradientStop Offset="0" Color="Gray"/>
    <GradientStop Offset="0.5" Color="Gray"/>
    <GradientStop Offset="1" Color="Black"/>
  </RadialGradientBrush>
</Polygon.Stroke>
</Polygon>
```

![](bbox=[0.068, 0.398, 0.255, 0.848])

The Dashes example program in Figure F-2 demonstrates the StrokeStartLineCap, StrokeEndLineCap, and StrokeDash values.

![](bbox=[0.355, 0.688, 0.605, 0.848])