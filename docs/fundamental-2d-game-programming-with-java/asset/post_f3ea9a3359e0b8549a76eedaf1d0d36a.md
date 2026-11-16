
```java
if( intersectCircle( c0, r0, c1, r1 ) ) {
    circle0Collision = true;
    circle1Collision = true;
}
if( intersectCircleAABB( c0, r0, min0Cpy, max0Cpy ) ) {
    circle0Collision = true;
    rect0Collision = true;
}
if( intersectCircleAABB( c0, r0, min1Cpy, max1Cpy ) ) {
    circle0Collision = true;
    rect1Collision = true;
}
if( intersectCircleAABB( c1, r1, min0Cpy, max0Cpy ) ) {
    circle1Collision = true;
    rect0Collision = true;
}
if( intersectCircleAABB( c1, r1, min1Cpy, max1Cpy ) ) {
    circle1Collision = true;
    rect1Collision = true;
}
}
private boolean pointInAABB( Vector2f p, Vector2f min, Vector2f max ) {
    return p.x > min.x && p.x < max.x &&
           p.y > min.y && p.y < max.y;
}
private boolean pointInCircle( Vector2f p, Vector2f c, float r ) {
    Vector2f dist = p.sub( c );
    return dist.lenSqr() < r*r;
}
private boolean intersectAABB(
    Vector2f minA, Vector2f maxA, Vector2f minB, Vector2f maxB ) {
    if( minA.x > maxB.x || minB.x > maxA.x ) return false;
    if( minA.y > maxB.y || minB.y > maxA.y ) return false;
    return true;
}
private boolean intersectCircle(
    Vector2f c0, float r0, Vector2f c1, float r1 ) {
    Vector2f c = c0.sub( c1 );
    float r = r0 + r1;
    return c.lenSqr() < r*r;
}
private boolean intersectCircleAABB(
Vector2f c, float r, Vector2f min, Vector2f max ) {
float d = 0.0f;
if ( c.x < min.x ) d += ( c.x - min.x )*( c.x - min.x );
if ( c.x > max.x ) d += ( c.x - max.x )*( c.x - max.x );
if ( c.y < min.y ) d += ( c.y - min.y )*( c.y - min.y );
if ( c.y > max.y ) d += ( c.y - max.y )*( c.y - max.y );
return d < r*r;
}

@Override
protected void render( Graphics g ) {
super.render( g );
// render instructions
g.drawString( "Dragging: * + dragging", 20, 35 );
g.drawString( "Click and hold to drag shapes", 20, 50 );
g.drawString( "Press [SPACE] to reset", 20, 65 );
// render objects
g.setColor( rectCollision ? Color.BLACK : Color.BLUE );
drawAABB( g, min0Cpy, max0Cpy );
g.setColor( rect1Collision ? Color.BLACK : Color.BLUE );
drawAABB( g, min1Cpy, max1Cpy );
g.setColor( circle0Collision ? Color.BLACK : Color.BLUE );
drawOval( g, c0, r0 );
g.setColor( circle1Collision ? Color.BLACK : Color.BLUE );
drawOval( g, c1, r1 );
}

// draw the AABB
private void drawAABB( Graphics g, Vector2f min, Vector2f max ) {
Matrix3x3f view = getViewportTransform();
Vector2f topLeft = new Vector2f( min.x, max.y );
topLeft = view.mul( topLeft );
Vector2f bottomRight = new Vector2f( max.x, min.y );
bottomRight = view.mul( bottomRight );
int rectX = (int)topLeft.x;
int rectY = (int)topLeft.y;
int rectWidth = (int)( bottomRight.x - topLeft.x );
int rectHeight = (int)( bottomRight.y - topLeft.y );
g.drawRect( rectX, rectY, rectWidth, rectHeight );
}
```

## USING THE SEPARATING AXIS METHOD

The separating axis method for testing if two objects overlap is more complicated than the previous tests, but it can handle any convex shape rotated to any position. Although it will not give the exact collision point by itself, it can be very useful for testing if objects overlap.

The idea is simple: if there exists an axis of separation between two convex polygons, then the objects do not overlap. In other words, if you can draw a line between two shapes, they cannot overlap. See Figure 7.14.

![](img/588a4cda8f2acae94a7e1987bf99400d_182_0.png)

Figure 7.14 Separating Axis Method.

There are many examples on the Internet if you are looking for a rigorous mathematical proof of the theorem. For the purposes here, Figure 7.14 shows adequate proof. Keep in mind that this only works for convex polygons. If there are any interior angles greater than 180 degrees, the polygon is concave and the separating axis test will not work. Figure 7.15 shows an example of a failing test due to a concave polygon.

![](img/588a4cda8f2acae94a7e1987bf99400d_183_0.png)

Figure 7.15 Concave Polygon Problems. © 2014 Timothy Wright.

### Tip

If you have a concave polygon, it can always be broken up into multiple convex polygons for testing. See Figure 7.16.

![](img/588a4cda8f2acae94a7e1987bf99400d_183_1.png)

Figure 7.16 Splitting Concave Polygons. © 2014 Timothy Wright.

It is easy to see how to draw a line between two objects, but this test needs to be done in the code using math. Fortunately, not only is the general case easy, there are some optimizations that can also be applied to symmetrical shapes.

To test if shapes overlap, do the following: for each line segment in both shapes, create a perpendicular normal vector, and project all the points onto the normal using the dot product. See Figure 7.17.

![](img/588a4cda8f2acae94a7e1987bf99400d_184_0.png)

Figure 7.17 Projection Lines. © 2014 Timothy Wright.

Once the points are projected onto the perpendicular normal, if the projections overlap, then the polygons overlap. If none of the projections contains any overlapping areas, then there is no overlap. See Figure 7.18.

![](img/588a4cda8f2acae94a7e1987bf99400d_184_1.png)

Figure 7.18 Overlapping Projections. © 2014 Timothy Wright.

Also, as shown in the following examples, if the object being projected is symmetrical, then the radius of each object can be compared to the distance between the two object centers. This test is just like testing for overlapping circles. This concept is shown in Figure 7.19.

![](img/588a4cda8f2acae94a7e1987bf99400d_185_0.png)

Figure 7.19 Rectangle Overlap. © 2014 Timothy Wright.

The distance ($d$) above and the sum of ($r_1$) and ($r_2$) are used to determine if the objects overlap. If any one of the tests fails, then the objects do not overlap. If no axis has a separation between objects, then they intersect, provided the objects do not curve about each other. One good thing about this method is that it works in more than two dimensions. In the previous illustration, the only axis that does not have an overlap is ($n_3$).

## USING THE LINE-LINE OVERLAP METHOD

The center of each line can be found using the midpoint formula:

```
midpt = \frac{P_0 + P_1}{2}
```

Using the center of each line, the distance to either endpoint is the radius of the line. That same radius, when normalized to a length of one, is the axis used for the projection. Because the radius of each line, when projected onto itself, is always zero, only the radius of the other line is compared to the projected center distance. See Figure 7.20.

![](img/588a4cda8f2acae94a7e1987bf99400d_186_0.png)

Figure 7.20 Line-Line Overlap. © 2014 Timothy Wright.

```
if |n̂₁ * (C₁ - C₂)| > |n̂₁ * r₂| : no overlap
if |n̂₂ * (C₁ - C₂)| > |n̂₂ * r₁| : no overlap
```

Because the comparisons are only using distance, which is always a positive value, they use the absolute value to ensure that no negative values are computed.

![](img/588a4cda8f2acae94a7e1987bf99400d_186_1.png)

Figure 7.21 Line-Line Overlap Example. © 2014 Timothy Wright.

The LineLineOverlapExample, located in the javagames.intersection package and shown in Figure 7.21, stores two lines—P₀ for the initial line and start, end for the second line. The start point is placed when the left mouse button is clicked and the end point follows the mouse pointer.

Inside the updateObject() method, the two lines are checked to see if they overlap using the separating axis method. The two lines are used to find the center, the radius, and each axis normal. Then the projected distance between the centers is compared to the radius of both lines. If the distance is larger than the radius, there is no overlap.
