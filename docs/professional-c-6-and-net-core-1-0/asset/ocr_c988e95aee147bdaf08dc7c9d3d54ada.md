| Shape Class | Description |
|---|---|
| Line | You can draw a line from the coordinates x1, y1 to x2, y2. |
| Rectangle | You draw a rectangle by specifying Width and Height for this class. |
| Ellipse | You can draw an ellipse. |
| Path | You can draw a series of lines and curves. The Data property is a Geometry type. You can do the drawing by using classes that derive from the base class Geometry, or you can use the path markup syntax to define geometry. |
| Polygon | You can draw a closed shape formed by connected lines. The polygon is defined by a series of Point objects assigned to the Points property. |
| Polyline | Similar to the Polygon class, you can draw connected lines with Polyline. The difference is that the polyline does not need to be a closed shape. |

# Geometry

The previous sample showed that one of the shapes, Path, uses Geometry for its drawing. You can also use Geometry elements in other places, such as with a DrawingBrush.

In some ways, geometry elements are very similar to shapes. Just as there are Line, Ellipse, and Rectangle shapes, there are also geometry elements for these drawings: LineGeometry, EllipseGeometry, and RectangleGeometry. There are also big differences between shapes and geometries. A Shape is a FrameworkElement that you can use with any class that supports UIElement as its children. FrameworkElement derives from UIElement. Shapes participate with the layout system and render themselves. The Geometry class can’t render itself and has fewer features and less overhead than Shape. With WPF, the Geometry class derives from the Freezable base class and can be shared from multiple threads. With UWP apps, the Geometry class directly derives from DependencyObject. Freezable is not available here.

The Path class uses Geometry for its drawing. The geometry can be set with the Data property of the Path. Simple geometry elements that can be set are EllipseGeometry for drawing an ellipse, LineGeometry for drawing a line, and RectangleGeometry for drawing a rectangle.

# Geometries Using Segments

You can also create geometries by using segments. The geometry class PathGeometry uses segments for its drawing. The following code segment uses the BezierSegment and LineSegment elements to build one red and one green figure, as shown in Figure 30.3. The first BezierSegment draws a Bézier curve between the points 70,40, which is