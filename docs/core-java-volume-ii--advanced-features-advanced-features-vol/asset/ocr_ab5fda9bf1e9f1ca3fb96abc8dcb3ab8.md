To construct a `TexturePaint` object, specify a `BufferedImage` and an *anchor* rectangle.

```
```java
g2.setPaint(new TexturePaint(bufferedImage, anchorRectangle));
```
```

We will introduce the `BufferedImage` class later in this chapter when we discuss images in detail. The simplest way of obtaining a buffered image is to read an image file:

```
```java
bufferedImage = ImageIO.read(new File("blue-ball.gif"));
```
```

The anchor rectangle is extended indefinitely in *x* and *y* directions to tile the entire coordinate plane. The image is scaled to fit into the anchor and then replicated into each tile.

+   **java.awt.Graphics2D 1.2**
+   
+   - `void setPaint(Paint s)`
+     sets the paint of this graphics context to the given object that implements the Paint interface.

+   **java.awt.GradientPaint 1.2**
+   
+   - `GradientPaint(float x1, float y1, Color color1, float x2, float y2, Color color2)`
+   - `GradientPaint(float x1, float y1, Color color1, float x2, float y2, Color color2, boolean cyclic)`
+   - `GradientPaint(Point2D p1, Color color1, Point2D p2, Color color2)`
+   - `GradientPaint(Point2D p1, Color color1, Point2D p2, Color color2, boolean cyclic)`
+     constructs a gradient paint object that fills shapes with color such that the start point is colored with color1, the end point is colored with color2, and the colors in between are linearly interpolated. Colors are constant along lines perpendicular to the line joining the start and the end point. By default, the gradient paint is not cyclic—that is, points beyond the start and end points are colored with the same color as the start and end point. If the gradient paint is cyclic, then colors continue to be interpolated, first returning to the starting point color and then repeating indefinitely in both directions.

+   **java.awt.TexturePaint 1.2**
+   
+   - `TexturePaint(BufferedImage texture, Rectangle2D anchor)`
+     creates a texture paint object. The anchor rectangle defines the tiling of the space to be painted; it is repeated indefinitely in *x* and *y* directions, and the texture image is scaled to fill each tile.