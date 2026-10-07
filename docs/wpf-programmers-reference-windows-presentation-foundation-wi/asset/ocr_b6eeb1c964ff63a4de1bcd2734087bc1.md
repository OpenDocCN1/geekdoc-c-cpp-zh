The Brushes example program shown in Figure G-1 demonstrates these kinds of brushes. The SolidColorBrush fills its Ellipse with dark gray, the LinearGradientBrush shades from white to the top to the bottom, and the RadialGradientBrush shades from white at the middle to black at the edges.

![](bbox=[0.095, 0.183, 0.603, 0.353])

FIGURE G-1

# DRAWINGBRUSH

A DrawingBrush fills areas with a Drawing object.

Table G-2 summarizes the DrawingBrush's most important properties.

TABLE G-2:

| PROPERTY | PURPOSE |
| --- | --- |
| AlignmentX | Determines how the Brush is aligned if the Stretch property is set to None so it doesn't stretch to fill the area |
| AlignmentY | Determines how the Brush is aligned if the Stretch property is set to None so it doesn't stretch to fill the area |
| Drawing | The Brush's content |
| Stretch | Determines how the Brush is stretched to fill its tiles. This can be None (the drawing is used at its original size), Uniform (the drawing is stretched to be as large as possible within the tile), UniformToFill (the drawing is uniformly stretched to fill the tile), and Fill (the drawing is stretched to fill the tile if it distorts the drawing |
| TileMode | Determines how the tile is repeated if necessary to fill the area. This can be None (the rest of the area is unfilled), Tile (the tile is repeated), FlipX (the tile is repeated with every other tile in the X direction flipped horizontally), FlipY (the tile is repeated with every other tile in the Y direction vertically), and FlipXY (both FlipX and FlipY). This only has an effect if Viewport is smaller than the filled area.
| Viewbox | Defines the part of the content used for the Brush. |