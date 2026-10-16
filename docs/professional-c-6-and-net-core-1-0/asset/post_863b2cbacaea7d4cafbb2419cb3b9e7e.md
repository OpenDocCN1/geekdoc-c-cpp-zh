
# 30 Styling XAML Apps

- Styling for WPF and UWP Apps
- Creating the base drawing with shapes and geometry
- Scaling, rotating, and skewing with transformations
- Using brushes to fill backgrounds
- Working with styles, templates, and resources
- Creating animations
- Visual State Manager

The wrox.com code downloads for this chapter are found at www.wrox.com/go/professionalscharp6 on the Download Code tab. The code for this chapter is divided into the following major examples:

- Shapes
- Geometry
- Transformation
- Brushes
- Styles and Resources
- Templates
- Animation
- Transitions
- Visual State

In recent years, developers have become a lot more concerned with having good-looking apps. When Windows Forms was the technology for creating desktop applications, the user interface didn't offer many options for styling the applications. Controls had a standard look that varied slightly based on the operating system version on which the application was running, but it was not easy to define a complete custom look.

This changed with Windows Presentation Foundation (WPF). WPF is based on DirectX and thus offers vector graphics that allow easy resizing of Windows and controls. Controls are completely customizable and can have different looks. Styling of applications has become extremely important. An application can have any look. With a good design, the user can work with the application without the need to know how to use a Windows application. Instead, the user just needs to have his domain knowledge. For example, the airport in Zurich created a WPF application where buttons look like airplanes. With the button, the user can get information of the position of the plane (the complete application looks like the airport). Colors of the buttons can have different meanings based on the configuration: they can show the either the airline, or on-time/delay information of the plane. This way, the user of the app easily sees what planes that are currently at the airport have small or big delays.

Having different looks of the app is even more important with Universal Windows Platform (UWP) apps. With these apps, the device can be used by users who haven’t used Windows applications before. With users who are knowledgeable of Windows applications, you should think about helping these users be more productive by having the typical process for how the user works easily accessible.

Microsoft has not provided a lot of guidance for styling WPF applications. How an application looks mainly depends on your (or the designer’s) imagination. With UWP apps, Microsoft has provided a lot more guidance and predefined styles, but you’re still able to change anything you like.

This chapter starts with the core elements of XAML—*shapes* that enable you to draw lines, ellipses, and path elements. After that you’re introduced to the foundation of shapes—*geometry* elements. You can use geometry elements to create fast vector-based drawings.

With *transformations*, you can scale and rotate any XAML element. With *brushes* you can create solid color, gradient, or more advanced backgrounds. You see how to use brushes within *styles* and place styles within XAML *resources*.

Finally, with *templates* you can completely customize the look of controls, and you also learn how to create animations in this chapter.

The sample code is available both with UWP apps and with WPF. Of course, where features are only available in one of these technologies, the sample code is only available there.

## Shapes

Shapes are the core elements of XAML. With shapes you can draw two-dimensional graphics using rectangles, lines, ellipses, paths, polygons, and polylines that are represented by classes derived from the abstract base class `Shape`. Shapes are defined in the namespaces `System.Windows.Shapes` (WPF) and `Windows.UI.Xaml.Shapes` (UWP).

The following XAML example draws a yellow face consisting of an ellipse for the face, two ellipses for the eyes, two ellipses for the pupils in the eyes, and a path for the mouth (code file Shapes[WPF|UWP]/Main[Window|Page].xaml):

```
<Canvas>
    <Ellipse Canvas.Left="10" Canvas.Top="10" Width="100" Height="100" Stroke="Blue" StrokeThickness="4" Fill="Yellow" />
    <Ellipse Canvas.Left="30" Canvas.Top="12" Width="60" Height="30">
        <Ellipse.Fill>
            <LinearGradientBrush StartPoint="0.5,0" EndPoint="0.5, 1">
                <GradientStop Offset="0.1" Color="DarkGreen" />
                <GradientStop Offset="0.7" Color="Transparent" />
            </LinearGradientBrush>
        </Ellipse.Fill>
    </Ellipse>
    <Ellipse Canvas.Left="30" Canvas.Top="35" Width="25" Height="20" Stroke="Blue" StrokeThickness="3" Fill="White" />
    <Ellipse Canvas.Left="40" Canvas.Top="43" Width="6" Height="5" Fill="Black" />
    <Ellipse Canvas.Left="65" Canvas.Top="35" Width="25" Height="20" Stroke="Blue" StrokeThickness="3" Fill="White" />
    <Ellipse Canvas.Left="75" Canvas.Top="43" Width="6" Height="5" Fill="Black" />
    <Path Stroke="Blue" StrokeThickness="4" Data="M 40,74 Q 57,95 80,74" />
</Canvas>
```

Figure 30.1 shows the result of the XAML code.

![](img/3d365b72b289213a91ade7eb366b8f35_1092_0.png)

### Figure 30.1

All these XAML elements can be accessed programmatically—even if they are buttons or shapes, such as lines or rectangles. Setting the Name or x:Name property with the Path element to mouth enables you to access this element programmatically with the variable name mouth:

```
<Path Name="mouth" Stroke="Blue" StrokeThickness="4"
```

```
Data="M 40,74 Q 57,95 80,74" />
```

With the next code changes, the mouth of the face is changed dynamically from code-behind. A button with a click handler is added where the SetMouth method is invoked (code file Shapes[WPF|UWP]/Main[Window|Page].xaml.cs):

```
private void OnChangeShape(object sender, RoutedEventArgs e)
{
    SetMouth();
}
```

When you’re using WPF, you can use the Path Markup Language (PML) from code-behind similar to what you’ve seen in the code snippets in this section with the Path element in XAML markup. Geometry.Parse interprets PML to create a new Geometry object. With PML, the letter M defines the starting point of the path, and the letter Q specifies a control point and an endpoint for a quadratic Bézier curve (code file ShapesWPF/MainWindow.xaml.cs):

```
private bool _laugh = false;

private void SetMouth2()
{
    if (_laugh)
    {
        mouth.Data = Geometry.Parse("M 40,82 Q 57,65 80,82");
    }
    else
    {
        mouth.Data = Geometry.Parse("M 40,74 Q 57,95 80,74");
    }
    _laugh = !_laugh;
}
```

Running the application results in the image shown in Figure 30.2.

![](img/3d365b72b289213a91ade7eb366b8f35_1093_0.png)

Figure 30.2

With UWP apps, the Geometry class doesn’t offer a Parse method, and you must create the geometry using figures and segments. First, you create a two-dimensional array of six points to define three points for the happy and three points for the sad state (code file Shapes[WPF|UWP]/Main[Window|Page].xaml.cs):

```
private readonly Point[,] _mouthPoints = new Point[2, 3]
{
    {
        new Point(40, 74), new Point(57, 95), new Point(80, 74),
    },
    {
        new Point(40, 82), new Point(57, 65), new Point(80, 82),
    }
};
```

Next, you assign a new PathGeometry object to the Data property of the Path. The PathGeometry contains a PathFigure with the start point defined (setting the StartPoint property is the same as the letter M with PML). The PathFigure contains a QuadraticBezierSegment with two Point objects assigned to the properties Point1 and Point2 (the same as the letter Q with two points):

```
private bool _laugh = false;
public void SetMouth()
{
    int index = _laugh ? 0: 1;

    var figure = new PathFigure() { StartPoint =
    _mouthPoints[index, 0] };
    figure.Segments = new PathSegmentCollection();
    var segment1 = new QuadraticBezierSegment();
    segment1.Point1 = _mouthPoints[index, 1];
    segment1.Point2 = _mouthPoints[index, 2];
    figure.Segments.Add(segment1);
    var geometry = new PathGeometry();
    geometry.Figures = new PathFigureCollection();
    geometry.Figures.Add(figure);

    mouth.Data = geometry;
    _laugh = !_laugh;
}
```

Using segments and figures is explained in more detail in the next section.

The following table describes the shapes available in the namespaces System.Windows.Shapes and Windows.UI.Xaml.Shapes.
