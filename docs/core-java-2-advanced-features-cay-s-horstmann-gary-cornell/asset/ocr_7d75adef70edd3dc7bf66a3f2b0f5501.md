| `java.awt.geom.Path2D.Float` |
|---|
| • `void moveTo(float x, float y)`<br>makes `(x, y)` the current point—that is, the starting point of the next segment.<br><br>• `void lineTo(float x, float y)`<br><br>• `void quadTo(float ctrlx, float ctrly, float x, float y)`<br><br>• `void curveTo(float ctrlx1, float ctrly1, float ctrlx2, float ctrly2, float x, float y)`<br>draws a line, quadratic curve, or cubic curve from the current point to the end point `(x, y)`, and makes that point the current point. |

| `java.awt.geom.Path2D` |
|---|
| • `void append(Shape s, boolean connect)`<br>adds the outline of the given shape to the general path. If connect is true, the current point of the general path is connected to the starting point of the added shape by a straight line.<br><br>• `void closePath()`<br>closes the path by drawing a straight line from the current point to the first point in the path. |

# 11.3 Areas

In the preceding section, you saw how you can specify complex shapes by constructing general paths composed of lines and curves. By using a sufficient number of lines and curves, you can draw essentially any shape. For example, the shapes of characters in the fonts that you see on the screen and on your printouts are all made up of lines and cubic curves.

Occasionally, it is easier to describe a shape by composing it from *areas*, such as rectangles, polygons, or ellipses. The Java 2D API supports four constructive *area geometry* operations that combine two areas into a new area.

+   - **add:** The combined area contains all points that are in the first or the second area.
+   - **subtract:** The combined area contains all points that are in the first but not the second area.
+   - **intersect:** The combined area contains all points that are in the first and the second area.