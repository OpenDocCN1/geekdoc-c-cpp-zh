
## Listing 11.2 *(Continued)*

```java
// This component draws two joined lines, using different stroke objects, and allows the user to
// drag the three points defining the lines.
//
class StrokeComponent extends JComponent
{
    private static final Dimension PREFERRED_SIZE = new Dimension(400, 400);
    private static final int SIZE = 10;

    private Point2D[] points;
    private int current;
    private float width;
    private int cap;
    private int join;
    private boolean dash;

    public StrokeComponent()
    {
        addMouseListener(new MouseAdapter()
        {
            public void mousePressed(MouseEvent event)
            {
                Point p = event.getPoint();
                for (int i = 0; i < points.length; i++)
                {
                    double x = points[i].getX() - SIZE / 2;
                    double y = points[i].getY() - SIZE / 2;
                    Rectangle2D r = new Rectangle2D.Double(x, y, SIZE, SIZE);
                    if (r.contains(p))
                    {
                        current = i;
                        return;
                    }
                }
            }

            public void mouseReleased(MouseEvent event)
            {
                current = -1;
            }
        });

        addMouseMotionListener(new MouseMotionAdapter()
        {
            public void mouseDragged(MouseEvent event)
            {
                if (current == -1) return;
                points[current] = event.getPoint();
                repaint();
            }
        });
    }

    /**
     * Sets solid or dashed lines.
     * @param d false for solid, true for dashed lines
     */
    public void setDash(boolean d)
    {
        dash = d;
        repaint();
    }

    public Dimension getPreferredSize() { return PREFERRED_SIZE; }
}
```

| `java.awt.Graphics2D` | 1.2 |
|---|---|
| `void setStroke(Stroke s)` | sets the stroke of this graphics context to the given object that implements the Stroke interface. |

| `java.awt.BasicStroke` | 1.2 |
|---|---|
| Constructors | `BasicStroke(float width)`<br>`BasicStroke(float width, int cap, int join)`<br>`BasicStroke(float width, int cap, int join, float miterlimit)`<br>`BasicStroke(float width, int cap, int join, float miterlimit, float[] dash, float dashPhase)`<br><br>constructs a stroke object with the given attributes. |
| Parameters | **width** — The width of the pen<br><br>**cap** — The end cap style—one of `CAP_BUTT`, `CAP_ROUND`, and `CAP_SQUARE`<br><br>**join** — The join style—one of `JOIN_BEVEL`, `JOIN_MITER`, and `JOIN_ROUND`<br><br>**miterlimit** — The angle, in degrees, below which a miter join is rendered as a bevel join<br><br>**dash** — An array of the lengths of the alternating filled and blank portions of a dashed stroke<br><br>**dashPhase** — The “phase” of the dash pattern; a segment of this length, preceding the starting point of the stroke, is assumed to have the dash pattern already applied. |

## 11.5 Paint

When you fill a shape, its inside is covered with *paint*. Use the `setPaint` method to set the paint you want to an object whose class implements the Paint interface. The Java 2D API provides three such classes:

- The `Color` class implements the `Paint` interface. To fill shapes with a solid color, simply call `setPaint` with a `Color` object, such as

```java
g2.setPaint(Color.red);
```

- The `GradientPaint` class varies colors by interpolating between two given color values (see Figure 11.15).

![](img/7dd923a566750151a3aab0dacd0cdaa5_817_0.png)

**Figure 11.15** Gradient paint

- The `TexturePaint` class fills an area with repetitions of an image (see Figure 11.16).

![](img/7dd923a566750151a3aab0dacd0cdaa5_817_1.png)

**Figure 11.16** Texture paint

You can construct a `GradientPaint` object by specifying two points and the colors that you want to use at these two points.

```java
g2.setPaint(new GradientPaint(p1, Color.RED, p2, Color.YELLOW));
```

Colors are interpolated along the line joining the two points. Colors are constant along lines perpendicular to that joining line. Points beyond an end point of the line are given the color at the end point.

Alternatively, if you call the `GradientPaint` constructor with `true` for the *cyclic* parameter,

```java
g2.setPaint(new GradientPaint(p1, Color.RED, p2, Color.YELLOW, true));
```

then the color variation *cycles* and keeps varying beyond the end points.

To construct a `TexturePaint` object, specify a `BufferedImage` and an *anchor* rectangle.

```java
g2.setPaint(new TexturePaint(bufferedImage, anchorRectangle));
```

We will introduce the `BufferedImage` class later in this chapter when we discuss images in detail. The simplest way of obtaining a buffered image is to read an image file:

```java
bufferedImage = ImageIO.read(new File("blue-ball.gif"));
```

The *anchor* rectangle is extended indefinitely in *x* and *y* directions to tile the entire coordinate plane. The image is scaled to fit into the anchor and then replicated into each tile.

| java.awt.Graphics2D 1.2 |
|---|
| • `void setPaint(Paint s)`<br>sets the paint of this graphics context to the given object that implements the `Paint` interface. |

| java.awt.GradientPaint 1.2 |
|---|
| • `GradientPaint(float x1, float y1, Color color1, float x2, float y2, Color color2)`<br>• `GradientPaint(float x1, float y1, Color color1, float x2, float y2, Color color2, boolean cyclic)`<br>• `GradientPaint(Point2D p1, Color color1, Point2D p2, Color color2)`<br>• `GradientPaint(Point2D p1, Color color1, Point2D p2, Color color2, boolean cyclic)`<br>constructs a gradient paint object that fills shapes with color such that the start point is colored with `color1`, the end point is colored with `color2`, and the colors in between are linearly interpolated. Colors are constant along lines perpendicular to the line joining the start and the end point. By default, the gradient paint is not cyclic—that is, points beyond the start and end points are colored with the same color as the start and end point. If the gradient paint is cyclic, then colors continue to be interpolated, first returning to the starting point color and then repeating indefinitely in both directions. |

- **java.awt.TexturePaint 1.2**
  - `TexturePaint(BufferedImage texture, Rectangle2D anchor)` creates a texture paint object. The anchor rectangle defines the tiling of the space to be painted; it is repeated indefinitely in x and y directions, and the texture image is scaled to fill each tile.

## 11.6 Coordinate Transformations

Suppose you need to draw an object, such as an automobile. You know, from the manufacturer’s specifications, the height, wheelbase, and total length. You could, of course, figure out all pixel positions, assuming some number of pixels per meter. However, there is an easier way: You can ask the graphics context to carry out the conversion for you.

```java
g2.scale(pixelPerMeter, pixelPerMeter);
g2.draw(new Line2D.Double(coordinates in meters)); // converts to pixels and draws scaled line
```

The scale method of the Graphics2D class sets the coordinate transformation of the graphics context to a scaling transformation. That transformation changes user coordinates (user-specified units) to device coordinates (pixels). Figure 11.17 shows how the transformation works.

![](img/7dd923a566750151a3aab0dacd0cdaa5_819_0.png)

Figure 11.17 User and device coordinates

Coordinate transformations are very useful in practice. They allow you to work with convenient coordinate values. The graphics context takes care of the dirty work of transforming them to pixels.

There are four fundamental transformations.

- Scaling: blowing up, or shrinking, all distances from a fixed point
- Rotation: rotating all points around a fixed center
- Translation: moving all points by a fixed amount
- Shear: leaving one line fixed and “sliding” the lines parallel to it by an amount that is proportional to the distance from the fixed line

Figure 11.18 shows how these four fundamental transformations act on a unit square.

![](img/7dd923a566750151a3aab0dacd0cdaa5_820_0.png)

**Figure 11.18** The fundamental transformations

The scale, rotate, translate, and shear methods of the Graphics2D class set the coordinate transformation of the graphics context to one of these fundamental transformations.

You can compose the transformations. For example, you might want to rotate shapes and double their size; supply both a rotation and a scaling transformation:

```java
g2.rotate(angle);
g2.scale(2, 2);
g2.draw(...);
```

In this case, it does not matter in which order you supply the transformations. However, with most transformations, order does matter. For example, if you want to rotate and shear, then it makes a difference which of the transformations you supply first. You need to figure out what your intention is. The graphics
