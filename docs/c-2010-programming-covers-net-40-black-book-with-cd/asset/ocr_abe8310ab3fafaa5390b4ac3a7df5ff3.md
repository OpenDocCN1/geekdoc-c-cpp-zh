# The ImageBrush Class

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

# Table 12.23: Properties of the ImageBrush Class

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

# The VisualBrush Class

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