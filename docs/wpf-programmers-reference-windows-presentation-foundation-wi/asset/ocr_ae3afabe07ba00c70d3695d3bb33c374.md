# STROKE PROPERTIES

The controls described in this chapter draw linear features. Whether they draw a single line segment, a closed ellipse, or a complex sequence of curves, lines, and polygons, they all basically draw lines.

WPF provides a special set of properties to control how those lines are drawn. These properties control the lines' color, style, and thickness.

The following table summarizes these controls' most important drawing properties:

| PROPERTY | PURPOSE |
|---|---|
| Fill | The control's drawing brush (This is similar to the Background property used by many other controls). |
| Stroke | The brush used to draw the control' edges (This is similar to the Foreground property used by many other controls). |
| StrokeDashArray | Array of values to tell how many pixels are drawn and then skipped to make a dash pattern The numbers are scaled by the line's thickness, so a value of 1 for a 5-pixel-wide line makes the line draw or skip 5 pixels. This makes dashes bigger and just looks better.
The line shown in Figure 8-1 uses the StrokeDashArray value (3, 3) and draws three times the line's width (5 pixels) and then skips three times the line's width. |
| StrokeDashCap | Determines the shape of the ends of the dashes. This can be Flat, Round, Square, or Triangle. The Flat style ends a dash exactly where it should end. The Round, Square, and Triangle styles place a shape (circle, square, or triangle) at the end of the dash so it extends slightly into the space between dashes. |
| StrokeDashOffset | Determines the distance from a beginning of a line to the start of the first dash. |
| StrokeEndLineCap | Determines the shape of the end of a line. This can be Flat, Square, Round, or Triangle. If the line ends at a blank space between dashes, then it ends with the dash end style outside the line's. If the line ends at end of a dash, the Round, Square, and Triangle caps may extend beyond the end of the segment (See the description of the StrokeDashCap property). |
| StrokeLineJoin | Determines how adjacent lines are joined in a Rectangle, Polyline, Polygon, or Path. This can be Miter (edges extend until they intersect), Bevel (corners are cut off), or Round (corners are slightly rounded). The effect is subtle unless the StrokeThickness is relatively large. |
| StrokeStartCap | Determines the shape of the start of a line. This is similar to StrokeEndLineCap. |
| StrokeThickness | The width of the line |