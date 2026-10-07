```
<Rectangle.Fill>
  <LinearGradientBrush EndPoint="0.25,0.5" StartPoint="0,0.5"
    SpreadMethod="Reflect">
    <GradientStop Color="White" Offset="0"/>
    <GradientStop Color="Blue" Offset="1"/>
  </LinearGradientBrush>
</Rectangle.Fill>
```

The first rectangle shades vertically from the top point (0.5, 0) to blue to the bottom point (0.5, 1).

The second rectangle adds an additional GradientStop object to make the gradient remain white until halfway through the brush before it starts shading to blue.

The third rectangle's Brush uses different StartPoint and Endpoint values to make the gradient move from the upper-left corner (0, 0) to the lower-right corner (1, 1). It uses GradientStop objects to make the colors blend from blue to lime.

The final rectangle's Brush has Endpoint (0.25, 0.5), so the brush only covers a quarter of the rectangle's width. The Brush's SpreadMethod is set to Reflect, so the brush reflects to cover the rest of the rectangle.

# RadialGradientBrush

The RadialGradientBrush and Endpoint properties to determine the brush's shape, the colors radiating away from a central point.

Instead of using StartPoint and Endpoint the brush's, RadialGradientBrush uses the properties GradientOrigin, RadiusX, and RadiusY.

GradientOrigin determines the point from which the colors radiate. By default, this is (0.5, 0.5), so the colors radiate from the center of the Brush's (0, 0) to (1, 1) coordinate system.

RadiusX and Radius determine how far the brush extends horizontally and vertically from the center, using the (0, 0) to (1, 1) coordinate system.

> REMEMBER THE RADIUS

Remember that the rectangle is half the width of a circle, so RadiusX and RadiusY values of 0.5 make the gradient fill the brush.

Note also that values of 0.5 make the gradient only reach to the sides of the brush not all the way into the corners. That means, for example, the corners of a rectangle are not covered by the gradient, so how they are filled depends on the SpreadMethod property.