# BOUNDING BOXES

The WPF layout engine treats graphic objects as if they were surrounded by an imaginary rectangle, the bounding box. It creates the bounding box based on the size and shape you specify for the object. Gradients are defined relative to that bounding box, not the actual shape.

![](bbox=[0.15, 0.23, 0.85, 0.5])

The bounding box is always rectangular, even though whatever it contains may not be.

Yes, I know this doesn't make sense if you're a mathematician. These aren't Cartesian coordinates; they're mapping coordinates.

The coordinates within the box range from 0,0 in the upper left to 1,1 in the lower right. That's true whether or not the bounding box is square.

You specify a position with a Point, which consists of two double values, x and y.

![](bbox=[0.25, 0.66, 0.92, 0.83])