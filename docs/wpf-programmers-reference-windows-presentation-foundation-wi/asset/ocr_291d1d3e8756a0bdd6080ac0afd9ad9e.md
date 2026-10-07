# BRUSHES

A brush determines how an area is filled. The area may be simple (such as a rectangle or ellipse) or complex (such as a polygon, overlapping pieces of a polyline, or a shape drawn by a Path control.

As mentioned earlier in this chapter, brush also determine how text is filled. That means that you can fill text with a solid color, a color gradient, or even a repeating pattern or picture. The PictureFilledText example program shown in Figure 10-11 draws some text filled with a picture of a few full of flowers.

![](bbox=[0.437, 0.176, 0.879, 0.296])

Figure 10-11

Before you learn about the different kinds of brushes that you can create, you should learn about two properties that affect any brush you use: FillRule and SpreadMethod. The following two sections describe these properties. The sections after describe the brush classes.

# FillRule

If the lines define an area across each other, then the object's FillRule property determines which pieces of the area are filled. If FillRule is Nonzero, then any piece of the screen is enclosed by the shape fill. If FillRule is EvenOdd, then only pieces of the screen that are enclosed an odd number of times by the shape are filled.

![](bbox=[0.666, 0.473, 0.879, 0.593])

Figure 10-12

The difference is hard to understand when described in words, but it's easy to understand if you look at an example. In Figure 10-12, the FillRules example program shows the difference between the two FillRule values.

# SpreadMethod

If a brush is not big enough to fill a drawn area, then its SpreadMethod determines how how remaining area is filled. For example, if you're filling a large rectangle with a small picture, the brush isn't big enough to fill the rectangle. The SpreadMethod property can take the values Pad, Reflect, Repeat.

The value Pad makes the brush fill the remaining area with its final color. For example, if the brush smoothly shades from white to green, then any remaining area is filled with green.

The value Reflect makes the brush reverse itself and continue filling the area. For example, suppose a brush shades from white to green. A larger area would be filled with white shading to green. This pattern would repeat until the entire area was filled.

The value Repeat makes the brush start over and repeat itself. If a brush shades from white to green, then a large area would be filled with white shading to green followed by an abrupt jump back to white shading to green.