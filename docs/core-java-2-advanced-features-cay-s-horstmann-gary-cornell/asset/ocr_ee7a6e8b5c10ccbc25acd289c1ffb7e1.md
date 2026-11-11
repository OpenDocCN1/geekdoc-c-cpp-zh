# 11.2 Shapes

Here are some of the methods in the `Graphics` class to draw shapes:

+   - `drawLine`
+   - `drawRectangle`
+   - `drawRoundRect`
+   - `draw3DRect`
+   - `drawPolygon`
+   - `drawPolyline`
+   - `drawOval`
+   - `drawArc`

There are also corresponding fill methods. These methods have been in the `Graphics` class ever since JDK 1.0. The Java 2D API uses a completely different, object-oriented approach. Instead of methods, there are classes:

+   - `Line2D`
+   - `Rectangle2D`
+   - `RoundRectangle2D`
+   - `Ellipse2D`
+   - `Arc2D`
+   - `QuadCurve2D`
+   - `CubicCurve2D`
+   - `GeneralPath`

These classes all implement the `Shape` interface, which we will examine in the following sections.

# 11.2.1 The Shape Class Hierarchy

The `Line2D`, `Rectangle2D`, `RoundRectangle2D`, `Ellipse2D`, and `Arc2D` classes correspond to the `drawLine`, `drawRectangle`, `drawRoundRect`, `drawOval`, and `drawArc` methods. (The concept of a “3D rectangle” has died the death it so richly deserved—there is no analog to the `draw3DRect` method.) The Java 2D API supplies two additional classes, quadratic and cubic curves, that we will discuss in this section. There is no `Polygon2D` class; instead, the `GeneralPath` class describes paths made up from lines, quadratic and cubic curves. You can use a `GeneralPath` to describe a polygon; we’ll show you how later in this section.

To draw a shape, first create an object of a class that implements the `Shape` interface and then call the draw method of the `Graphics2D` class.