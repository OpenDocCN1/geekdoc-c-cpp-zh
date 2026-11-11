**java.awt.geom.RectangularShape 1.2** *(Continued)*

- `double getWidth()`
- `double getHeight()`

  returns the width or height of the enclosing rectangle.
- `double getX()`
- `double getY()`

  returns the *x* or *y* coordinate of the top left corner of the enclosing rectangle.

**java.awt.geom.Rectangle2D.Double 1.2**

- `Rectangle2D.Double(double x, double y, double w, double h)`

  constructs a rectangle with the given top left corner, width, and height.

**java.awt.geom.Ellipse2D.Double 1.2**

- `Ellipse2D.Double(double x, double y, double w, double h)`

  constructs an ellipse whose bounding rectangle has the given top left corner, width, and height.

**java.awt.geom.Point2D.Double 1.2**

- `Point2D.Double(double x, double y)`

  constructs a point with the given coordinates.

**java.awt.geom.Line2D.Double 1.2**

- `Line2D.Double(Point2D start, Point2D end)`
- `Line2D.Double(double startX, double startY, double endX, double endY)`

  constructs a line with the given start and end points.

# ### 10.3.2 Using Color

The `setPaint` method of the `Graphics2D` class lets you select a color that is used for all subsequent drawing operations on the graphics context. For example: