
## DRAWING THE FULL TREND LINE

While similar to the previous method in many ways, drawTrendLine adds a few layers of complexity. Here, we’re going to draw two labeled reference lines. One corresponds to the minimum weight, one to the maximum. We will also need to coordinate their appearance, so even though the weight labels may have different widths, the left edge of the reference lines remains properly aligned. Finally, we need to dynamically size our graph so our trend line fills the bulk of the view.

Again, because of the length of this method, we will look at it in smaller chunks.

```objective-c
- (void)drawTrendLine {
    // Draw the reference lines.
    UIFont* font = [UIFont boldSystemFontOfSize:self.fontSize];
    CGFloat textPadding = font.lineHeight / 2.0f;
    CGFloat topY = self.margin * 2 + textPadding;
    CGFloat bottomY = self.bounds.size.height - topY;
}
```

We start by requesting the bold system font again. Then we calculate a textPadding variable based on half the font’s height. We then use this value and our margin property to calculate a safe upper and lower limit for our reference lines. After all, we don’t want to cut off the tops and bottoms of our labels.

```objective-c
NSString* topLabel =
    [WeightEntry stringForWeightInLbs:self.graphStats.maxWeight
                               inUnit:self.units];
NSString* bottomLabel =
    [WeightEntry stringForWeightInLbs:self.graphStats.minWeight
                                inUnit:self.units];
CGSize topTextSize = [topLabel sizeWithFont:font];
CGSize bottomTextSize = [bottomLabel sizeWithFont:font];
// Get the maximum width.
CGFloat textOffset =
    topTextSize.width > bottomTextSize.width ?
        topTextSize.width : bottomTextSize.width;

[self drawReferenceLineWithLabel:topLabel
                           font:font
                           atY:topY
                           withTextWidthOffset:textOffset];
[self drawReferenceLineWithLabel:bottomLabel
                           font:font
                           atY:bottomY
                           withTextWidthOffset:textOffset];
```

Next, we create our weight labels for the top and bottom reference lines. As stated earlier, the top line will be our maximum weight, while the bottom will be our minimum weight. We then calculate the size of each of these.

Here we use C’s ternary conditional operator to determine the maximum width (see “Operators” in Chapter 2). This expression says that if the top width is greater than the bottom width, we use the top width. Otherwise we use the bottom.

Finally, we call our helper method to draw the two reference lines. Notice that we use the same textOffset for both of them.

```objective-c
CGFloat startX = self.margin * 4 + textOffset;
CGFloat endX = self.bounds.size.width - (self.margin * 3);
UIBezierPath* trendLine = [UIBezierPath bezierPath];
trendLine.lineWidth = self.trendLineWidth;
trendLine.lineCapStyle = kCGLineCapRound;
trendLine.lineJoinStyle = kCGLineJoinRound;
// Get starting point.
CGRect graphBounds =
    CGRectMake(startX, topY, endX - startX, bottomY - topY);
```

Here, we want to make sure the graph starts well to the right of our labels. So, we utilize our textOffset variable and our margin property to calculate the starting and ending x-coordinates.

Once we have the start and end x-coordinates, we create an empty UIBezierPath. This will hold our trend line. We set the width based on our trendLineWidth property and then give it rounded caps and joins. We discussed the caps earlier. Joins define the shape of the corners where two line segments connect.

As the last step in this snippet, we create a rectangle based on our startX, endX, topY, and bottomY values.

```objective-c
// Process all the entries.

[self.graphStats processWeightEntryUsingBlock:
    ^(WeightEntry* entry) {
        CGPoint point =
            [self coordinatesForEntry:entry inBounds:graphBounds];
        if (trendLine.empty) {
            // If we don't have any points,
            // move to the starting point.
            [trendLine moveToPoint:point];
        }
        else {
            // Otherwise, draw a line to the next point.
            [trendLine addLineToPoint:point];
        }
    }];
    [self.trendLineColor setStroke];
    [trendLine stroke];
}
```

Finally, we use our processWeightEntryUsingBlock: method to process all the WeightEntries in our GraphStats object (see “Building GraphStats” at the beginning of this chapter).

We start by calling the coordinatesForEntry:inBounds: helper method to calculate the entry’s coordinates within our selected bounds. Then, if our Bezier path is empty, we move the cursor to the starting point. Otherwise, we add a new line segment stretching from the current cursor location to the provided point. This also updates the cursor’s location to the new point.

Once the path is complete, we set the stroke color and draw it.

## DRAWING THE REFERENCE LINES AND LABELS

Now let’s implement the reference line helper method:

```objective-c
- (void)drawReferenceLineWithLabel:(NSString*)label
                              font:(UIFont*)font
                                 atY:(CGFloat)y
                  withTextWidthOffset:(CGFloat)xOffset {
    // Set x-coordinate.
    CGFloat x = self.margin * 2.0f;
    [self.textColor setFill];
    [label drawAtPoint:CGPointMake(x, y - (font.lineHeight / 2.0f))
             withFont:font];
    x += self.margin + xOffset;
    UIBezierPath* referenceLine = [UIBezierPath bezierPath];
    referenceLine.lineWidth = self.referenceLineWidth;
    [referenceLine moveToPoint:CGPointMake(x, y)];
    [referenceLine addLineToPoint:
        CGPointMake(self.bounds.size.width -
            (self.margin * 2.0f), y)];
    [self.referenceLineColor setStroke];
    [referenceLine stroke];
}
```

We start by creating an x-coordinate that is inset by twice the margin property—once to bring us to the edge of the rounded rectangle, then once more to give us a nice margin inside it. Notice that we are using the same margin value for all the margins: the distance between the view's bounds and the rounded rectangle, the distance between the left side of the rounded rectangle and our reference label, and the distance between the reference label and the reference line. We could have used different margin parameters, but this simplifies the code and provides a clean, uniform appearance.

We then set the fill color to our textColor property, and draw our text using the UIStringDrawing drawAtPoint:withFont: method. This draws a single line of text whose upper-left corner is the given point. Notice that this method uses the text drawing mode and colors from the current context; however, you do not need to set the context's font. The drawAtPoint:withFont: method manages the font for you automatically.

By default, text is drawn using only the fill color. You can change this if you want by calling the Core Graphics CGContextSetTextDrawingMode() method to add outlines (as well as other drawing effects).

Additionally, we want our text to be vertically centered on the y-coordinate. Notice how we offset the drawing point by subtracting half the font's line height from our y-coordinate. This moves the label up, centering its bounding box appropriately.

Next, we move the x-coordinate in by using our text width offset and margin. We create our path, a single horizontal line segment that runs from the x- and y-coordinates to the right margin. We set the line width and color, and then we draw the line.

This approach is somewhat different from the one we used to draw the grid lines. Here, we are using UIKit's UIBezierPath. There, we used Core Graphics' CGContextStrokeLineSegments() function. As we said earlier, there are a number of duplicate (or near-duplicate) methods between the two frameworks. This often gives us several different ways to accomplish the same basic task. You can pick whichever approach works best in your particular application.
