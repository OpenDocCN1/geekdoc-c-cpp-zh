+   - Arcs sweep from a starting angle by the number of degrees specified by their arc angle (p. 651).
+   - Graphics methods drawArc (p. 651) and fillArc (p. 651) are used for drawing arcs.

# Section 15.7 Drawing Polygons and Polylines

+   - Class Polygon contains methods for creating polygons.
+   - Polygons are closed multisided shapes composed of straight-line segments.
+   - Polylines (p. 654) are a sequence of connected points.
+   - Graphics method drawPolyline (p. 656) displays a series of connected lines.
+   - Graphics methods drawPolygon (p. 656) and fillPolygon (p. 657) are used to draw polygons.
+   - Polygon method addPoint (p. 657) adds pairs of x- and y-coordinates to the Polygon.

# Section 15.8 Java 2D API

+   - The Java 2D API (p. 657) provides advanced two-dimensional graphics capabilities.
+   - Class Graphics2D (p. 632)—a subclass of Graphics—is used for drawing with the Java 2D API.
+   - The Java 2D API’s classes for drawing shapes include Line2D.Double, Rectangle2D.Double, RoundRectangle2D.Double, Arc2D.Double and Ellipse2D.Double (p. 657).
+   - Class GradientPaint (p. 632) helps draw a shape in gradually changing colors—called a gradient (p. 660).
+   - Graphics2D method fill (p. 660) draws a filled object of any type that implements interface Shape (p. 660).
+   - Class BasicStroke (p. 632) helps specify the drawing characteristics of lines.
+   - Graphics2D method draw (p. 660) is used to draw a Shape object.
+   - Classes GradientPaint and TexturePaint (p. 632) help specify the characteristics for filling shapes with colors or patterns.
+   - A general path (p. 662) is a shape constructed from straight lines and complex curves and is represented with an object of class GeneralPath (p. 662).
+   - GeneralPath method moveTo (p. 663) specifies the first point in a general path.
+   - GeneralPath method lineTo (p. 663) draws a line to the next point in the path. Each new call to lineTo draws a line from the previous point to the current point.
+   - GeneralPath method closePath (p. 664) draws a line from the last point to the point specified in the last call to moveTo. This completes the general path.
+   - Graphics2D method translate (p. 664) is used to move the drawing origin to a new location.
+   - Graphics2D method rotate (p. 664) is used to rotate the next displayed shape.

# Self-Review Exercises

15.1 Fill in the blanks in each of the following statements:

+   a) In Java 2D, method ______ of class ______ sets the characteristics of a line used to draw a shape.
+   b) Class ______ helps specify the fill for a shape such that the fill gradually changes from one color to another.
+   c) The ______ method of class Graphics draws a line between two points.
+   d) RGB is short for ______, ______ and ______.
+   e) Font sizes are measured in units called ______.
+   f) Class ______ helps specify the fill for a shape using a pattern drawn in a BufferedImage.