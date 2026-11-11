appends the outline of a rectangle to the path without connecting it to the existing path. But

```
```
path.append(r, true);
```
```

adds a straight line from the end point of the path to the starting point of the rectangle, and then adds the rectangle outline to the path.

The program in Listing 11.15 lets you create sample paths. Figures 11.37 and 11.38 show sample runs of the program. You can pick a shape maker from the combo box. The program contains shape makers for

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

computes the actual shape, given the current positions of the control points. The `toString` method returns the class name so that the `ShapeMaker` objects can simply be dumped into a `JComboBox`.

To enable dragging of the control points, the `ShapePanel` class handles both mouse and mouse motion events. If the mouse is pressed on top of a rectangle, subsequent mouse drags move the rectangle.

The majority of the shape maker classes are simple—their `makeShape` methods just construct and return the requested shapes. However, the `ArcMaker` class needs to compute the distorted start and end angles. Furthermore, to demonstrate that the computation is indeed correct, the returned shape is a `GeneralPath` containing the arc itself, the bounding rectangle, and the lines from the center of the arc to the angle control points (see Figure 11.39).