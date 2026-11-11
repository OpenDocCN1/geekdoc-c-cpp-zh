```
```xml
<StackPanel DockPanel.Dock ="Left"
    Orientation="Vertical" Background="#ECE9D8">
    <TextBlock Margin="3" Text="Controls"/>
    <Button Margin="3,5" HorizontalAlignment="Left"
    Click="b1Click">Subdivide</Button>
    <Button Margin="3,5" HorizontalAlignment="Left"
    Click="b2Click">Clear</Button>
</StackPanel>
```
```

Now we modify the C# code in Window1.xaml.cs. We start by initializing both polygons to be empty:

```
```csharp
public partial class Window1 : Window
{
    Polygon myPolygon = new Polygon();
    Polygon mySubdivPolygon = new Polygon();
    bool isSubdivided = false;
    GraphPaper gp = null;
    [...]
    public Window1()
    {
        [...]
        initPoly(myPolygon, Brushes.Black);
        initPoly(mySubdivPolygon, Brushes.Firebrick);
        gp.Children.Add(myPolygon);
        gp.Children.Add(mySubdivPolygon);

        ready = true; // Now we're ready to have sliders
                      // and buttons influence the display.
    }
```
```

The polygon initialization procedure also sets the polygons to have different colors and a standard line thickness, and to make sure that when two edges meet at a sharp angle they are truncated, as shown at the bottom of Figure 4.4, instead of having the joint extended in a long miter as shown in the middle.

![](bbox=[0.735, 0.425, 0.895, 0.545])

Figure 4.4: When we thicken the vertex join at the top, we must miter it, as shown in the middle. At the bottom, the miter is limited.

```
```csharp
private void initPoly(Polygon p, SolidColorBrush b)
{
    p.Stroke = b;
    p.StrokeThickness = 0.5; // 0.5 mm thick line
    p.StrokeMiterLimit = 1;  // no long pointy bits
    p.Fill = null;           // at vertices
}
```
```

Handling a click on the Clear button is straightforward: We simply remove all points from each polygon and set the isSubdivided flag back to false:

```
```csharp
// Clear button
public void b2Click(object sender, RoutedEventArgs e)
{
    myPolygon.Points.Clear();
    mySubdivPolygon.Points.Clear();
    isSubdivided = false;

    e.Handled = true; // don't propagate click further
}
```
```

The Subdivide button is more complex. First, if the polygon is already subdivided, we want to replace myPolygon's points with those of the subdivided polygon. Then we can subdivide myPolygon and put the result into mySubdivPolygon.