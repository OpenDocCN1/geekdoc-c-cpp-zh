line segment at a time, or you can use one of the convenience methods to create common shapes: rectangle, oval, arc, or in this particular case a rounded rectangle. Once we have our rounded rectangle, we set the current context's fill color, using the graphFillColor property, and then we fill it in.

Core Graphics and UIKit support two basic drawing operations: fills and strokes. A fill operation paints the inside of a region or shape; a stroke draws the outline. Our context can have separate stroke and fill colors but can have only one fill or stroke color at a time (not including fill patterns and gradients).

```
// Save the current context.

CGContextRef context = UIGraphicsGetCurrentContext();

CGContextSaveGState(context);

// Limit drawing to inside the rounded rectangle.

[graphBorder addClip];
```

This step is short, but it's worth talking about in detail. Each graphics context maintains a stack of states. The states record a number of the graphics context's parameters. These include the following:

+   - Current transformation matrix
+   - Clip region
+   - Image interpolation quality
+   - Line width
+   - Line join
+   - Miter limit
+   - Line cap
+   - Line dash
+   - Flatness
+   - Should anti-alias
+   - Rendering intent
+   - Fill color space

+   - Stroke color space
+   - Fill color
+   - Stroke color
+   - Alpha value
+   - Font
+   - Font size
+   - Character spacing
+   - Text drawing mode
+   - Shadow parameters
+   - Pattern phase
+   - Font smoothing parameter
+   - Blend mode