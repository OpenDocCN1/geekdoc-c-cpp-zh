Some of these, like the stroke or fill color, are simple enough to set and reset manually. In other cases, it may not be so easy to undo your changes. Look at the clipping path. Both the UIKit methods and the Core Graphics functions offer ways of adding shapes to the current clipping path; however, there’s no way to remove them.

The graphics context’s stack of states gives us an easy way to quickly undo a large number of changes. We can even roll back those hard-to-fix changes. By calling CGContextSaveGState() and CGContextRestoreGState(), we can push and pop the current state onto and off of the state stack.

In this particular case, we want to add the rounded rectangle to the clipping path (thus limiting all drawing to the inside of our rounded rectangle). However, we will still want to draw outside the rectangle later on. Therefore, we must save the state before we alter the clipping path.

![](bbox=[0.0, 0.43, 0.265, 0.585])

**NOTE:** You only need to use CGContextSaveGState() and CGContextRestoreGState() if you plan to undo state changes within your own drawing code. The system automatically creates a new graphics context each time a view is drawn. Any changes you make will not persist beyond the current draw cycle and the current view.

```
    // Draw graph paper background.
    [self.gridColor setStroke];

    CGContextSetLineWidth(context, self.gridLineWidth);

    // Draw horizontal.
    CGFloat y = innerBounds.origin.y + self.gridSquareSize;

    while (y < innerBounds.origin.y + innerBounds.size.height) {
        CGPoint segments[] = {CGPointMake(innerBounds.origin.x, y),
            CGPointMake(innerBounds.origin.x +
                        innerBounds.size.width, y)};

        CGContextStrokeLineSegments(context, segments, 2);

        y += self.gridSquareSize;
    }

    // Draw vertical.
    CGFloat x = innerBounds.origin.x + self.gridSquareSize;
```