```
<BezierSegment Point1="90,37" Point2="130,46" Point3="150,63" />
<LineSegment Point1="120,110" />
<BezierSegment Point1="120,100" />
Point2="70,90" Point3="45,91" />
<LineSegment Point1="70,40" />
</PathFigure.Segments>
</PathFigure>
</PathGeometry.Figures>
</PathGeometry>
</GeometryDrawing.Geometry>
</GeometryDrawing>
<DrawingBrush.Drawing>
</DrawingBrush>
</Button.Background>
</Button>
```

# ImageBrush

To load an image into a brush, you can use the ImageBrush element. With this element, the image defined by the ImageSource property is displayed. The image can be accessed from the file system or from a resource within the assembly. In the example, the image is added as a resource to the assembly and referenced with the assembly and resource names:

```
<Button Content="Image Brush" Width="100" Height="80" Margin="5"
Foreground="White"
<Button.Background>
<ImageBrush ImageSource="/BrushesDemo;component/Budapest.jpg" />
</Button.Background>
</Button>
```

# VisualBrush

The VisualBrush allows you to use other WPF elements in a brush. Here, you can add a WPF element to the Visual property. The sixth element in Figure 35-8 contains a Rectangle and a Button:

```
<Button Content="Visual Brush" Width="100" Height="80">
<Button.Background>
<VisualBrush>
<VisualBrush.Visual>
<StackPanel Background="White">
<Rectangle Width="25" Height="25" Fill="Blue" />
<Button Content="Drawing Button" Background="Red" />
</StackPanel>
</VisualBrush.Visual>
</VisualBrush>
</Button.Background>
</Button>
```

You can add any UIElement to the VisualBrush. One example is that you can play a video by using the MediaElement:

```
<Button Content="Visual Brush with Media" Width="200" Height="150"
Foreground="White"
<Button.Background>
<VisualBrush>
<VisualBrush.Visual>
<MediaElement Source="./Stephanie.wmv" />
</VisualBrush.Visual>
</VisualBrush>
</Button.Background>
</Button>
```