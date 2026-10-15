# Table 12.21: Properties of the RadialGradientBrush Class

| Property | Description |
|---|---|
| ColorInterpolationMode | Gets or sets a ColorInterpolationMode enumeration that specifies how the gradient's colors are interpolated |
| GradientOrigin | Gets or sets the location of the 2-D focal point that defines the beginning of the gradient |
| GradientStops | Gets or sets the brush's gradient stops |
| MappingMode | Gets or sets a BrushMappingMode enumeration for the coordinates of a gradient brush, whether they are absolute or relative for the output area |
| RadiusX | Gets or sets the horizontal radius of the outermost circle of the radial gradient |
| RadiusY | Gets or sets the vertical radius of the outermost circle of a radial gradient |
| SpreadMethod | Gets or sets the type of spread method that specifies how to draw a gradient that starts or ends inside the bounds of the object to be painted |

# The DrawingBrush Class

The DrawingBrush class paints an area by using the Drawing class, which can include shapes, text, video, images, or other drawings. The Drawing class describes the visible content of the DrawingBrush class, which stretches the drawing to fill the output area. The drawing that is shown with the brush is defined using the GeometryDrawing element. You can also create a repeating pattern of the drawing by setting the Viewport and TileMode properties of the DrawingBrush class. You can apply the DrawingBrush class to your application by adding the following code snippet:

```
<DrawingBrush .../>
```

The inheritance hierarchy of the DrawingBrush class is as follows:

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Freezable
        System.Windows.Media.Animation.Animatable
          System.Windows.Media.Brush
            System.Windows.Media.TileBrush
              System.Windows.Media.DrawingBrush
```

The noteworthy properties of the DrawingBrush class are listed in Table 12.22:

# Table 12.22: Properties of the DrawingBrush Class

| Property | Description |
|---|---|
| AlignmentX | Gets or sets the horizontal alignment of content in the TileBrush base tile |
| AlignmentY | Gets or sets the vertical alignment of content in the TileBrush base tile |
| Drawing | Gets or sets a value that describes the contents of the DrawingBrush class |
| Stretch | Gets or sets a value that specifies how the content of the TileBrush class stretches to fit its tiles |
| TileMode | Gets or sets a value that specifies how a TileBrush fills the area that you are painting if the base tile is smaller than the output area |
| Viewbox | Gets or sets the position and dimensions of the content in a TileBrush tile |
| ViewboxUnits | Gets or sets a value that specifies whether the Viewbox value is related to the bounding box of the TileBrush contents or whether the value is absolute |
| Viewport | Gets or sets the position and dimensions of the base tile for a TileBrush tile |
| ViewportUnits | Gets or sets a BrushMappingMode enumeration that specifies whether the value of the Viewport, which indicates the size and position of the TileBrush base tile, is relative to the size of the output area |