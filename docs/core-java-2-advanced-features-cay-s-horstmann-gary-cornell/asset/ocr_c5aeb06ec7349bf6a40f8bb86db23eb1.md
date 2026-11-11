| **java.awt.geom.Area** |
|---|
| • `void add(Area other)`<br>• `void subtract(Area other)`<br>• `void intersect(Area other)`<br>• `void exclusiveOr(Area other)`<br><br>carries out the constructive area geometry operation with this area and the other area and sets this area to the result. |

# ## 11.4 Strokes

The draw operation of the `Graphics2D` class draws the boundary of a shape by using the currently selected *stroke*. By default, the stroke is a solid line that is 1 pixel wide. You can select a different stroke by calling the `setStroke` method and supplying an object of a class that implements the `Stroke` interface. The Java 2D API defines only one such class, called `BasicStroke`. In this section, we’ll look at the capabilities of the `BasicStroke` class.

You can construct strokes of arbitrary thickness. For example, here is how to draw lines that are 10 pixels wide:

```
    g2.setStroke(new BasicStroke(10.0F));
    g2.draw(new Line2D.Double(. . .));
```

When a stroke is more than a pixel thick, the *end* of the stroke can have different styles. Figure 11.11 shows these so-called *end cap styles*. You have three choices:

+   - A *butt cap* simply ends the stroke at its end point.
+   - A *round cap* adds a half-circle to the end of the stroke.
+   - A *square cap* adds a half-square to the end of the stroke.

When two thick strokes meet, there are three choices for the *join style* (see Figure 11.12).

+   - A *bevel join* joins the strokes with a straight line that is perpendicular to the bisector of the angle between the two strokes.
+   - A *round join* extends each stroke to have a round cap.
+   - A *miter join* extends both strokes by adding a “spike.”