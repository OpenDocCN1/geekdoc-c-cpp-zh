Close the path by calling the `closePath` method. It draws a line back to the starting point of the path.

To make a polygon, simply call `moveTo` to go to the first corner point, followed by repeated calls to `lineTo` to visit the other corner points. Finally, call `closePath` to close the polygon. The program in Listing 11.1 shows this in more detail.

A general path does not have to be connected. You can call `moveTo` at any time to start a new path segment.

Finally, you can use the `append` method to add arbitrary `Shape` objects to a general path. The outline of the shape is added to the end to the path. The second parameter of the `append` method is true if the new shape should be connected to the last point on the path, false otherwise. For example, the call

```
```
Rectangle2D r = . . .;
path.append(r, false);
```
```

appends the outline of a rectangle to the path without connecting it to the existing path. But

```
```
path.append(r, true);
```
```

adds a straight line from the end point of the path to the starting point of the rectangle, and then adds the rectangle outline to the path.

The program in Listing 11.1 lets you create sample paths. Figures 11.7 and 11.8 show sample runs of the program. You can pick a shape maker from the combo box. The program contains shape makers for

+   - Straight lines
+   - Rectangles, rounded rectangles, and ellipses
+   - Arcs (showing lines for the bounding rectangle and the start and end angles, in addition to the arc itself)
+   - Polygons (using a `GeneralPath`)
+   - Quadratic and cubic curves

Use the mouse to adjust the control points. As you move them, the shape continuously repaints itself.

The program is a bit complex because it handles multiple shapes and supports dragging of the control points.

An abstract superclass `ShapeMaker` encapsulates the commonality of the shape maker classes. Each shape has a fixed number of control points that the user can move around. The `getPointCount` method returns that value. The abstract method

```
```
Shape makeShape(Point2D[] points)
```
```