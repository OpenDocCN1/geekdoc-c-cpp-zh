
## Table 12.21: Properties of the RadialGradientBrush Class

| Property | Description |
|---|---|
| ColorInterpolationMode | Gets or sets a ColorInterpolationMode enumeration that specifies how the gradient's colors are interpolated |
| GradientOrigin | Gets or sets the location of the 2-D focal point that defines the beginning of the gradient |
| GradientStops | Gets or sets the brush's gradient stops |
| MappingMode | Gets or sets a BrushMappingMode enumeration for the coordinates of a gradient brush, whether they are absolute or relative for the output area |
| RadiusX | Gets or sets the horizontal radius of the outermost circle of the radial gradient |
| RadiusY | Gets or sets the vertical radius of the outermost circle of a radial gradient |
| SpreadMethod | Gets or sets the type of spread method that specifies how to draw a gradient that starts or ends inside the bounds of the object to be painted |

## The DrawingBrush Class

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

## Table 12.22: Properties of the DrawingBrush Class

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

## The ImageBrush Class

You can use the ImageBrush class to load an image into a brush. You can load the most common image file types, including bmp, png, gif, and jpeg file. The ImageSource property is used to display the image used in the ImageBrush class. By default, an image is stretched to fill the area that is used in the ImageSource property. However, you can modify this behavior by setting the Stretch property of the TileBrush class, which causes the image to preserve the aspect ratio of the image. You can create a repeating pattern of the image by setting the Viewport and TileMode properties. You can add the ImageBrush class to your application by adding the following code snippet:

```
<ImageBrush .../>
```

The inheritance hierarchy of the ImageBrush class is as follows:

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Freezable
        System.Windows.Media.Animation.Animatable
          System.Windows.Media.Brush
            System.Windows.Media.TileBrush
              System.Windows.Media.ImageBrush
```

The noteworthy properties of the ImageBrush class are listed in Table 12.23:

## Table 12.23: Properties of the ImageBrush Class

| Property | Description |
|---|---|
| AlignmentX | Gets or sets the horizontal alignment of content in the TileBrush base tile |
| AlignmentY | Gets or sets the vertical alignment of content in the TileBrush base tile |
| ImageSource | Gets or sets the image displayed by the ImageBrush class |
| Stretch | Gets or sets a value that specifies how the content of the TileBrush tile stretches to fit its tiles |
| TileMode | Gets or sets a value that specifies how a TileBrush tile fills the area that you are painting if the base tile is smaller than the output area |
| Viewbox | Gets or sets the position and dimensions of the content in a TileBrush tile |
| ViewboxUnits | Gets or sets a value that specifies whether the Viewbox value is relative to the bounding box of the TileBrush contents or the value is absolute |
| Viewport | Gets or sets the position and dimensions of the base tile for a TileBrush tile |
| ViewportUnits | Gets or sets a BrushMappingMode enumeration that specifies whether the value of the Viewport property, which indicates the size and position of the TileBrush base tile, is relative to the size of the output area |

## The VisualBrush Class

The VisualBrush class paints an area with a visual and it allows you to take the visual content of an element and use it to fill the area. For example, you can copy the appearance of a button in the window to a region in that window. It means you are using an existing image to create the duplicate image. Another way to specify the visual content of the VisualBrush class is to create a new Visual class and use it to set the Visual property of the VisualBrush class. With the VisualBrush class, you can also create effects such as reflection. You can also use the VisualBrush class to display a video by setting the Visual property to the MediaElement control. You can add the VisualBrush class to your application by adding the following code snippet:

```
<VisualBrush .../>
```

The inheritance hierarchy of the VisualBrush class is as follows:

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Freezable
        System.Windows.Media.Animation.Animatable
          System.Windows.Media.Brush
```

The noteworthy properties of the VisualBrush class are listed in Table 12.24:

## Table 12.24: Properties of the VisualBrush Class

| Property | Description |
|---|---|
| AlignmentX | Gets or sets the horizontal alignment of content in the TileBrush base tile |
| AlignmentY | Gets or sets the vertical alignment of content in the TileBrush base tile |
| AutoLayoutContent | Gets or sets a value that specifies whether the VisualBrush class will place the content |
| Stretch | Gets or sets a value that specifies how the content of the TileBrush stretches to fit its tiles |
| TileMode | Gets or sets a value that specifies how a TileBrush fills the area that you are painting if the base tile is smaller than the output area |
| Viewbox | Gets or sets the position and dimensions of the content in a TileBrush tile |
| ViewboxUnits | Gets or sets a value that specifies whether the Viewbox value is relative to the bounding box of the TileBrush contents or whether the value is absolute |
| Viewport | Gets or sets the position and dimensions of the base tile for a TileBrush tile |
| ViewportUnits | Gets or sets a BrushMappingMode enumeration that specifies whether the value of the Viewport, which indicates the size and position of the TileBrush base tile, is relative to the size of the output area |
| Visual | Gets or sets the brush's content |

## The Drawing Class

The Drawing class is an abstract class and it represents a 2-D drawing. It uses Drawing objects to draw different types of content. The Drawing objects are light-weight objects that enable you to add geometric shapes, images, text, and media to an application. The inheritance hierarchy of the Drawing class is as follows:

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Freezable
        System.Windows.Media.Animation.Animatable
          System.Windows.Media.Drawing
```

The noteworthy properties of the Drawing class are listed in Table 12.25:

## Table 12.25: Properties of the Drawing Class

| Property | Description |
|---|---|
| Bounds | Retrieves the axis-aligned bounds of the drawing's contents |
| CanFreeze | Retrieves a value that indicates whether the object is uneditable |
| DependencyObjectType | Retrieves a value that wraps the CLR type of the Drawing class |
| Dispatcher | Retrieves a value with which the Drawing class is associated |
| HasAnimatedProperties | Retrieves a value that indicates whether one or more AnimationClock objects is associated with any of the Drawing class dependency properties |
| IsFrozen | Retrieves a value that indicates whether the object is currently modifiable or not |
| IsSealed | Retrieves a value that declares whether this instance is currently read-only |
