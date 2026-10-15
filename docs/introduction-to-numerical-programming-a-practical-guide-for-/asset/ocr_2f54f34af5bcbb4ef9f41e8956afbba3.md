+   - `fill = color`—fill color of the ellipse’s interior. An empty string `""` means “transparent” and this is the default.
+   - `outline = color`—color of the border around the ellipse. The default outline color is `"black"`.
+   - `width = width`—width in pixels of the border around the ellipse. The default is 1.

**Canvas rectangle objects** are used for drawing rectangles on the canvas, specified by the top left corner `(x1,y1)` and the bottom right corner `(x2,y2)`. The syntax for creating a rectangle object on the canvas is

```
id = w.create_rectangle(x1, y1, x2, y2, option=value,...)

```

and returns the id of the created item.

Options (selected):

+   - `fill = color`—fill color of the rectangle’s interior. An empty string `""` means “transparent” and this is the default.
+   - `outline = color`—color of the border around the rectangle. The default outline color is `"black"`.
+   - `width = width`—width in pixels of the border around the rectangle. The default is 1.

**Canvas text objects** are used for displaying one or more lines of text on the canvas. The syntax for producing the text on the canvas w at position `(x,y)` is

```
id = w.create_text(x, y, option=value,...)

```

and returns the id of the created item.

Options (selected):

+   - `anchor = CENTER`—by default, the text is centered horizontally and vertically about `(x,y)`. For example, for `anchor = NW`, the upper left corner of the text-bounding rectangle is placed at the reference point `(x,y)`. Other legal arguments are N, NE, E, SE, S, SW, and W.
+   - `fill = color`—text color. The default is `"black"`.
+   - `font = font`—tuple of font attributes. For example, to create a 14-point Helvetica regular font, one would use `font = ("Helvetica",14)`.
+   - `justify = LEFT` (default), `CENTER`, or `RIGHT`. For multiline texts, the option controls how the lines are justified.
+   - `text = string`—text to be displayed. The newline character `"\n"` can be used to force line breaks.
+   - `width = width`—maximum line width. Lines longer than this value are wrapped. By default, the text width is set by the longest line.

# 3.2.2 Methods for Updating Canvas Widgets

In its most rudimentary form, updating or animating the display implies deleting the content of widgets and redrawing it.

The Canvas widget, in particular, supports the method `delete`, which enables deleting selectively or entirely the displayed items. The general syntax is

```
w.delete(item)

```