
Note that because NSPoint, NSSize, and NSRect are data structures and not objects, no pointer star is required.

## Using Foundation Constants

A number of constants are predefined:

- NSZeroPoint Equal to 0,0
- NSZeroSize Width and height are both zero
- NSZeroRect A rect of zero size at 0, 0

You can use these wherever you need the equivalent NSPoint, NSSize, or NSRect.

## Using Foundation Functions

A collection of helper functions is included in Cocoa’s Foundation Functions. For a complete list, see the Foundation Functions Reference. You must review this reference before you start working with Cocoa graphics. These functions are essential timesavers. It can be helpful to print them out and pin them somewhere close and visible.

Table 16.3 lists a selection of the more commonly used functions. Equivalent functions for NSSize are listed in the Foundation Functions Reference.

**Table 16.3 Selected Foundation Functions**

| Function | Description |
|---|---|
| NSMakePoint | Packs two floats into an NSPoint |
| NSMakeRect | Packs four floats into an NSRect |
| NSEqualPoints | Returns YES if two points are identical |
| NSEqualRects | Returns YES if two rects are identical |
| NSIntersectionRect | Returns the rect where two input rects overlap |
| NSUnionRect | Returns the smallest rect that encloses two input rects |
| NSMidX and NSMidY | Returns the X or Y center of a rect |
| NSPointInRect | Returns YES if a point is inside a rect |

![](img/2b293e29fc15b0797f113b85dd429b6e_438_0.png)

**CAUTION**

Because the basic data element is a float, be careful when comparing points, rects, and sizes. Rounding errors may mean that similar values aren’t identical, and comparisons may fail because of a difference in the nth decimal place. This can become a problem when you multiply points and rects to scale them. You can use NSIntegralRect to round float values up to integers in a rect.

The oval path returns an oval or circle that touches the edges of the surrounding rectangle. If the height and width are equal, the path is circular.

For more complex shapes, you can define the path in sections. The number and order of sections are arbitrary, and they do not have to be contiguous. Useful methods include

- `moveToPoint`: Moves the drawing position to an arbitrary point without creating a mark.
- `lineToPoint`: Moves the drawing position to a point, creating a line.
- `closePath`: Moves the drawing position to the start of the path, creating a closed shape.

`relativeMoveToPoint:` and `relativeLineToPoint:` convenience methods are available. They take relative rather than absolute coordinates to simplify certain path calculations.

## Creating Bezier paths with control points

`curveToPoint:controlPoint1:controlPoint2:` draws a curve from the current position to a point using two control points to define a Bezier curve, as shown in Figure 16.8. The control points are invisible, but they define the shape of the curve. Bezier curves are used to define glyph shapes in fonts, but you can use them in any application that requires arbitrary line shapes.

**Figure 16.8**

A Bezier curve defined by two control points. The points are invisible “handles” that define the curvature of the path. They can be placed anywhere to create an almost infinite range of curves.

![](img/2b293e29fc15b0797f113b85dd429b6e_440_0.png)

## Creating composite Bezier paths

You can join paths to create complex composite paths. Use `appendBezierPath:` to join one path to another. Variations include

- `appendBezierPathWithPoints:` Takes an array and interprets the elements as points joined by line segments.
- `appendBezierPathWithArcFromPoint:toPoint:` Creates an arc between two points.
- `appendBezierPathWithGlyph:inFont:` Adds a font glyph from a selected font.

**NOTE**

You must use the appendBezierPath: methods to create arcs. You can only append arcs to a path; you can't initialize or create a path with an arc.

## Stroking and filling paths

Once you have a path object, you can draw it by calling the stroke and fill methods on it. Optionally, you can set a color, line type, and line width for these methods. The default color is black, the default line type is unbroken, and the default width is 1 pixel.

Additionally, you can define line end caps to create arrow heads or lines with curved terminations. You can also specify line mitres to create butt-end or sharpened line joins. See the NSBezierPath Class Reference for details. Color is global, but line features are properties of a path object.

As a very simple example, you'll create a rectangle offset from the edges of a container view. Rect calculations can become complex because the bottom-left origin complicates size and position calculation. It's often useful to center objects, but this is only possible by calculating the size and position manually.

Start by creating a new blank project. Create a new NSView subclass called RectsView. Open IB and assign the subclass to the container view. Add the following code to the drawRect: method in the new view:

```objective-c
- (void)drawRect:(NSRect)dirtyRect {
    float rectOffset = 30;
    NSRect boundsRect = self.bounds;
    NSRect newRect = NSMakeRect(boundsRect.origin.x+rectOffset,
                                boundsRect.origin.y+rectOffset,
                                boundsRect.size.width-2*rectOffset,
                                boundsRect.size.height-2*rectOffset);
    NSBezierPath *newPath =
        [NSBezierPath bezierPathWithRect:newRect];
    [newPath stroke];  //Draw the path
}
```

Save the file and nib. Build and Run the project. Figure 16.9 shows the result.

Change [newPath stroke] to [newPath fill]. Build and Run the project. You'll see that the rectangle is now filled with solid black, as shown in Figure 16.10.

## Using colors

In Cocoa, NSColor defines a color object. Call the set method on the color object to set fill and stroke colors. Convenience methods are available for various predefined colors. See the NSColor Class Reference for a list.

**Figure 16.10** Replacing stroke with fill fills the rectangle with a solid color.

![](img/2b293e29fc15b0797f113b85dd429b6e_443_0.png)

### Using calibrated colors

Color is an unexpectedly complex topic. Cocoa color is designed to support calibration — a mapping process that eliminates imperfections in color hardware. Monitors and printers often have poor calibration, so there is no guarantee that a given shade of blue or red will appear the same on two different devices.

A full discussion of calibration is outside the scope of this book, but you can use the colorWithCalibratedHue: and colorWithCalibratedRed:green:blue:alpha: methods to create calibrated color objects. These methods use the calibration features built into OS X to create colors that take into account existing calibration maps.

### Creating and drawing gradients

Gradients are not defined and used in the same way as color objects. An NSGradient object takes two or more colors and defines a smooth blend between them, as shown in Figure 16.11.

```objective-c
NSGradient *thisGradient = [[NSGradient alloc]
    initWithStartingColor: aColor
    endingColor: anotherColor];
```

Gradients are then drawn separately, either filling a rect with

```objective-c
[thisGradient drawInRect: aRect angle: angleInDegrees];
```

or filling a path with

```objective-c
[thisGradient drawInBezierPath: aPath angle: angleInDegrees];
```

The angle parameter rotates the gradient. There is no set method for a gradient.

**CAUTION**

Most graphics methods and functions take parameters in radians. The gradient drawing functions take an angle parameter in degrees.

**Figure 16.11**

Filling a rect with a gradient. The angle parameter rotates the gradient. Note that the rotation is around the bottom-left corner of the rect.

![](img/2b293e29fc15b0797f113b85dd429b6e_444_0.png)
