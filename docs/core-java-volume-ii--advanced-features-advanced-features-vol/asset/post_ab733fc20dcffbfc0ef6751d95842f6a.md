
![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_720_0.png)

**Figure 11.32** The bounding rectangle of an ellipse and an arc

Internally, all graphics classes use float coordinates because float numbers use less storage space but have sufficient precision for geometric computations. However, the Java programming language makes it a bit more tedious to manipulate float numbers. For that reason, most methods of the graphics classes use double parameters and return double values. Only when constructing a 2D object you need to choose between the constructors with float and double coordinates. For example,

```
var floatRect = new Rectangle2D.Float(5F, 10F, 7.5F, 15F);
var doubleRect = new Rectangle2D.Double(5, 10, 7.5, 15);
```

The Xxx2D.Float and Xxx2D.Double classes are subclasses of the Xxx2D classes. After object construction, essentially no benefit accrues from remembering the subclass, and you can just store the constructed object in a superclass variable as in the code example above.

As you can see from the curious names, the Xxx2D.Float and Xxx2D.Double classes are also inner classes of the Xxx2D classes. That is just a minor syntactical convenience to avoid inflation of outer class names.

Finally, the Point2D class describes a point with an x and a y coordinate. Points are used to define shapes, but they aren’t themselves shapes.

Figure 11.33 shows the relationships between the shape classes. However, the Double and Float subclasses are omitted. Legacy classes from the pre-2D library are marked with a gray fill.

## 11.3.2.2 Using the Shape Classes

You already saw how to use the Rectangle2D, Ellipse2D, and Line2D classes in Volume I, Chapter 10. In this section, you will learn how to work with the remaining 2D shapes.

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_721_0.png)

Figure 11.33  Relationships between the shape classes

For the `RoundRectangle2D` shape, specify the top left corner, width, height, and the *x* and *y* dimensions of the corner area that should be rounded (see Figure 11.34). For example, the call

```
var r = new RoundRectangle2D.Double(150, 200, 100, 50, 20, 20);
```

produces a rounded rectangle with circles of radius 20 at each of the corners.

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_722_0.png)

**Figure 11.34** Constructing a RoundRectangle2D

To construct an arc, specify the bounding box, the start angle, the angle swept out by the arc (see Figure 11.35), and the closure type—one of Arc2D.OPEN, Arc2D.PIE, or Arc2D.CHORD.

```
var a = new Arc2D(x, y, width, height, startAngle, arcAngle, closureType);
```

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_722_1.png)

**Figure 11.35** Constructing an elliptical arc

Figure 11.36 illustrates the arc types.

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_723_0.png)

**Figure 11.36** Arc types

> **CAUTION:** If the arc is elliptical, the computation of the arc angles is not at all straightforward. The API documentation states: “The angles are specified relative to the nonsquare framing rectangle such that 45 degrees always falls on the line from the center of the ellipse to the upper right corner of the framing rectangle. As a result, if the framing rectangle is noticeably longer along one axis than the other, the angles to the start and end of the arc segment will be skewed farther along the longer axis of the frame.” Unfortunately, the documentation is silent on how to compute this “skew.” Here are the details:

Suppose the center of the arc is the origin and the point (x, y) lies on the arc. You can get a skewed angle with the following formula:

```
skewAngle = Math.toDegrees(Math.atan2(-y * height, x * width));
```

To construct quadratic and cubic curves, give the coordinates of the end points and the control points. For example:

```
var q = new QuadCurve2D.Double(startX, startY, controlX, controlY, endX, endY);
var c = new CubicCurve2D.Double(startX, startY, controlX1, controlY1,
    controlX2, controlY2, endX, endY);
```

Quadratic curves are not very flexible, and they are not commonly used in practice. Cubic curves (such as the Bézier curves drawn by the CubicCurve2D class) are, however, very common. By combining many cubic curves so that the slopes at the connection points match, you can create complex, smooth-looking curved shapes. For more information, we refer you to *Computer Graphics: Principles and Practice, Third Edition*, by James D. Foley, Andries van Dam, Steven K. Feiner, et al. (Addison-Wesley, 2013).

You can build arbitrary sequences of line segments, quadratic curves, and cubic curves, and store them in a GeneralPath object. Specify the first coordinate of the path with the moveTo method, for example:

```
var path = new GeneralPath();
path.moveTo(10, 20);
```

You can then extend the path by calling one of the methods lineTo, quadTo, or curveTo. These methods extend the path by a line, a quadratic curve, or a cubic curve. To call lineTo, supply the end point. For the two curve methods, supply the control points, then the end point. For example,

```
path.lineTo(20, 30);
path.curveTo(controlX, controlY, control2X, control2Y, endX, endY);
```

Close the path by calling the closePath method. It draws a straight line back to the starting point of the path.

To make a polygon, simply call moveTo to go to the first corner point, followed by repeated calls to lineTo to visit the other corner points. Finally, call closePath to close the polygon. The program in Listing 11.15 shows this in more detail.

A general path does not have to be connected. You can call moveTo at any time to start a new path segment.

Finally, you can use the append method to add arbitrary shape objects to a general path. The outline of the shape is added to the end of the path. The second parameter of the append method is true if the new shape should be connected to the last point on the path, false otherwise. For example,

```
Rectangle2D r = ...;
path.append(r, false);
```

appends the outline of a rectangle to the path without connecting it to the existing path. But

```
path.append(r, true);
```

adds a straight line from the end point of the path to the starting point of the rectangle, and then adds the rectangle outline to the path.

The program in Listing 11.15 lets you create sample paths. Figures 11.37 and 11.38 show sample runs of the program. You can pick a shape maker from the combo box. The program contains shape makers for

- Straight lines
- Rectangles, rounded rectangles, and ellipses
- Arcs (showing lines for the bounding rectangle and the start and end angles, in addition to the arc itself)
- Polygons (using a `GeneralPath`)
- Quadratic and cubic curves

Use the mouse to adjust the control points. As you move them, the shape continuously repaints itself.

The program is a bit complex because it handles multiple shapes and supports dragging of the control points.

An abstract superclass `ShapeMaker` encapsulates the commonality of the shape maker classes. Each shape has a fixed number of control points that the user can move around. The `getPointCount` method returns that value. The abstract method

```
Shape makeShape(Point2D[] points)
```

computes the actual shape, given the current positions of the control points. The `toString` method returns the class name so that the `ShapeMaker` objects can simply be dumped into a `JComboBox`.

To enable dragging of the control points, the `ShapePanel` class handles both mouse and mouse motion events. If the mouse is pressed on top of a rectangle, subsequent mouse drags move the rectangle.

The majority of the shape maker classes are simple—their `makeShape` methods just construct and return the requested shapes. However, the `ArcMaker` class needs to compute the distorted start and end angles. Furthermore, to demonstrate that the computation is indeed correct, the returned shape is a `GeneralPath` containing the arc itself, the bounding rectangle, and the lines from the center of the arc to the angle control points (see Figure 11.39).
