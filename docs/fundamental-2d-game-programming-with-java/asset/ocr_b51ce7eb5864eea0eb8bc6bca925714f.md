# USING AN AXIS ALIGNED BOUNDING BOX (AABB) FOR INTERSECTION TESTING

An axis aligned bounding box (AABB) is a rectangle that has edges parallel to the x-axis and y-axis. See Figure 7.6.

![](bbox=[0.1, 0.2, 0.44, 0.33])

Figure 7.6 Axis Aligned Bounding Box. © 2014 Timothy Wright.

Because the rectangle is not rotated, it is an easy shape to use for intersection testing. The shape can be represented with only a minimum and a maximum value, as shown in Figure 7.7. Note that AABBs cannot be rotated.

![](bbox=[0.1, 0.51, 0.44, 0.63])

Figure 7.7 AABB Representation. © 2014 Timothy Wright.

Transforming and drawing an AABB is straightforward.

```
private void drawAABB( Graphics g, Vector2f min, Vector2f max ) {
    Matrix3x3f view = getViewportTransform();

    Vector2f topLeft = new Vector2f( min.x, max.y );
    topLeft = view.mul( topLeft );

    Vector2f bottomRight = new Vector2f( max.x, min.y );
    bottomRight = view.mul( bottomRight );

    int rectX = (int)topLeft.x;
    int rectY = (int)topLeft.y;
```