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

Finally, you can use the append method to add arbitrary shape objects to a general path. The outline of the shape is added to the end to the path. The second parameter of the append method is true if the new shape should be connected to the last point on the path, false otherwise. For example,

```
Rectangle2D r = ...;
path.append(r, false);
```