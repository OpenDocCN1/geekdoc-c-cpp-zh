# Rectangle

A rectangular region with a top-left point (X, Y) and a width and height.

Shapes are always constructed from the top left corner, which is the (0,0) point of the local coordinate space.

# Simple Shapes and Text

Note that for simple drawing of shapes and text, all the work is done by the Canvas. You do not need to explicitly create shape, line, or text objects; instead, set Canvas attributes and invoke a dedicated drawing method of the Canvas object, for example:

+   1. Construct a canvas:
+   ```
+   Canvas::Construct()
+   ```
+   2. Clear the canvas:
+   ```
+   Canvas::Clear();
+   ```
+   3. Set the line colour to red:
+   ```
+   Canvas::SetForegroundColor(Color::COLOR_RED);
+   ```
+   4. Draw a rectangle onto the canvas:
+   ```
+   Canvas::DrawRectangle();
+   ```
+   5. Show the canvas to the display:
+   ```
+   Canvas::Show();
+   ```

For shapes, such as Ellipse, Polygon, Rectangle, set the fill attributes by calling Fill methods instead of plain Draw methods, for example:

```
Canvas::FillRectangle(const Color &color, const Rectangle &rect);
```

Text can be drawn to a Canvas in a similar way:

+   1. Construct a canvas.
+   2. Construct a font with style and size:
+   ```
+   Font::Construct(FONT_STYLE_ITALIC, 32);
+   ```
+   3. Clear the canvas.
+   4. Set the Canvas font:
+   ```
+   Canvas::SetFont(font);
+   ```
+   5. Draw "BuddyFix!" to the canvas:
+   ```
+   Canvas::DrawText(Point(55, 55), L"BuddyFix!");
+   ```
+   6. Show the canvas to the display.