# Listing 11.2 *(Continued)*

```
```java
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
```

| `java.awt.Graphics2D` | 1.2 |
|---|---|
| `void setStroke(Stroke s)` | sets the stroke of this graphics context to the given object that implements the Stroke interface. |

| `java.awt.BasicStroke` | 1.2 |
|---|---|
| Constructors | `BasicStroke(float width)`<br>`BasicStroke(float width, int cap, int join)`<br>`BasicStroke(float width, int cap, int join, float miterlimit)`<br>`BasicStroke(float width, int cap, int join, float miterlimit, float[] dash, float dashPhase)`<br><br>constructs a stroke object with the given attributes. |
| Parameters | **width** — The width of the pen<br><br>**cap** — The end cap style—one of `CAP_BUTT`, `CAP_ROUND`, and `CAP_SQUARE`<br><br>**join** — The join style—one of `JOIN_BEVEL`, `JOIN_MITER`, and `JOIN_ROUND`<br><br>**miterlimit** — The angle, in degrees, below which a miter join is rendered as a bevel join<br><br>**dash** — An array of the lengths of the alternating filled and blank portions of a dashed stroke<br><br>**dashPhase** — The “phase” of the dash pattern; a segment of this length, preceding the starting point of the stroke, is assumed to have the dash pattern already applied. |