
```
return div( len() );

}

public float dot( Vector2f v ) {
    return x * v.x + y * v.y;
}

public float len() {
    return (float)Math.sqrt( x * x + y * y );
}

public float lenSqr() {
    return x * x + y * y;
}

public Vector2f perp() {
    return new Vector2f( -y, x );
}

public float angle() {
    return (float)Math.atan2( y, x );
}

public static Vector2f polar( float angle, float radius ) {
    return new Vector2f(
        radius * (float)Math.cos( angle ),
        radius * (float)Math.sin( angle )
    );
}

@Override
public String toString() {
    return String.format( "(%s,%s)", x, y );
}
}
```

# RESOURCES AND FURTHER READING

- Akenine-Moller, Tomas, and Eric Haines, Real-Time Rendering. 2nd Edition, A K Peters, 2002.
- Ericson, Christer, Real-Time Collision Detection, Focal Press, 2004.

# INTERSECTION TESTING

![](img/588a4cda8f2acae94a7e1987bf99400d_161_0.png)

It won’t be much of a game if objects fly about the screen but never interact with each other. Regardless of the kind of game, even if it is just to check whether the mouse is hovering over something, at some point intersection testing and collision detection will be necessary. The problem is that these topics can be complicated. Entire tomes of algorithms and math can be found on many shelves and people are still trying to find ways to improve on the algorithms. Most people assume that the huge 3D sandbox games are full of complicated ideas, but that simple (looking) 2D games are easy. After this chapter, it should be obvious that looks can be deceiving.

## POINT IN POLYGON TESTING

In order to determine if the mouse pointer is inside an object, two operations are needed. First, it is necessary to convert the mouse position in screen coordinates into world coordinates. This code was covered in Chapter 5, “Simple Game Framework.” Second, the objects need to be tested to see if the mouse position in world coordinates is inside the object. Testing if a point is inside a polygon is useful for a variety of situations in computer games.

An algorithm for determining if a point is inside a polygon is easy to understand, but there are lots of concepts that are not obvious at first. The test itself is easy to explain, but hard to implement. You take the point to be tested and extend a ray along the x-axis. Count every time the ray crosses the polygon. If it crosses an even number of times, it is outside. If it crosses an odd number of times, it is inside. See Figure 7.1.

![](img/588a4cda8f2acae94a7e1987bf99400d_162_0.png)

Figure 7.1 Point in Polygon. © 2014 Timothy Wright.

As shown in Figure 7.1, points 0, 2, and 4 are outside the polygon because they cross an even number of times. Points 1 and 3 are inside because they cross an odd number of times. Because the algorithm needs to know if the ray crosses a polygon line, the test can be broken into four different cases, as illustrated in Figure 7.2.

![](img/588a4cda8f2acae94a7e1987bf99400d_162_1.png)

Figure 7.2 Point in Polygon Cases. © 2014 Timothy Wright.

The first three cases, where the polygon line is either above, below, or behind the point, all evaluate to no intersection. Only number four counts as the ray crossing a polygon line.

```
private boolean pointInPolygon( Vector2f point, List<Vector2f> poly ) {
    boolean inside = false;
    if( poly.size() > 2 ) {
      Vector2f start = poly.get( poly.size() - 1 );
      boolean startAbove = start.y >= point.y;
      for( int i = 0; i < poly.size(); i++ ) {
        Vector2f end = poly.get( i );
        boolean endAbove = end.y >= point.y;
        if (startAbove != endAbove) {
            // TBD - test ahead or behind
        }
        startAbove = endAbove;
        start = end;
      }
    }
    return inside;
  }
```

The steps for the pointInPolygon() algorithm are as follows:

- 1. Don't bother if there are not at least three lines in the polygon.
- 2. Start with the last and first points.
- 3. Set startAbove to true if the first polygon point is above the y value of the point to check.
- 4. Loop through all the points in the polygon.
- 5. Since the code gets the last point in the polygon, start with the first.
- 6. Set endAbove to true if the second polygon point is above the y value of the point to check.
- 7. If both startAbove and endAbove are equal, then they are either both above or both below the point and there cannot be an intersection.
- 8. Save the startAbove state.
- 9. Make the end point the start point.
- 10. Return the result.

In order to determine whether the intersection is ahead or behind the ray, the point-slope equation can be used to solve for the unknown x coordinate value.

```
y - y1 = m(x - x1)
x - x1 = (y - y1) / m
x = x1 + (y - y1) / m
where m = Δy / Δx = (y2 - y1) / (x2 - x1)
```

Once the x intersection value is found, it is compared to the point's x value. If the intersection value is smaller than the point's x value, the intersection is behind the point, and no intersection occurs.

```
if(startAbove != endAbove) {
    float m = (end.y - start.y) / (end.x - start.x);
    float x = start.x + (point.y - start.y) / m;
    if (x >= point.x) {
        inside = !inside;
    }
}
```

### Point in Polygon Special Cases

This algorithm works well as long as the lines of the polygon do not intersect. The two following polygons have crossing lines, and both treat the dark shaded sections that are inside the polygon as if they were outside. See Figure 7.3.

![](img/588a4cda8f2acae94a7e1987bf99400d_164_0.png)

Figure 7.3 Point in Polygon Special Cases. © 2014 Timothy Wright.

To correctly identify these overlapped sections, the direction where the line crosses the ray can be counted. For every crossing, going from the top to the bottom, the count is incremented and for every crossing, going from the bottom to the top, the count is decremented. If the number of crossings has the same number of clockwise and counterclockwise crossings (the count is zero), then the point is outside. See Figure 7.4.

![](img/588a4cda8f2acae94a7e1987bf99400d_165_0.png)

Figure 7.4 Polygon Winding. © 2014 Timothy Wright.

The complete algorithm with and without winding is as follows:

```
private boolean pointInPolygon(
    Vector2f point, List<Vector2f> poly, boolean winding ) {
  int inside = 0;
  if( poly.size() > 2 ) {
    Vector2f start = poly.get( poly.size() - 1 );
    boolean startAbove = start.y >= point.y;
    for( int i = 0; i < poly.size(); ++i ) {
      Vector2f end = poly.get( i );
      boolean endAbove = end.y >= point.y;
      if( startAbove != endAbove ) {
        float m = (end.y - start.y) / (end.x - start.x);
        float x = start.x + (point.y - start.y) / m;
        if( x > point.x ) {
          if( winding ) {
            inside += startAbove ? 1 : -1;
          } else {
            inside = inside == 1 ? 0 : 1;
          }
        }
      }
      startAbove = endAbove;
      start = end;
    }
  }
  return inside != 0;
}
```

## Point in Polygon Example

The PointInPolygonExample, located in the javagames.intersection package and shown in Figure 7.5, uses the SimpleFramework class for all the boilerplate code. The poly list holds the polygon created by clicking on the screen. The polyCpy list holds the polygon transformed to screen coordinates. All points inside the polygon are placed into the inside list and all points outside are placed into the outside list. The mouse position is the converted world coordinates. The selected variable is set to true if the mouse is inside the polygon. The winding variable is true when the algorithm should use the winding when testing points.

![](img/588a4cda8f2acae94a7e1987bf99400d_166_0.png)

**Figure 7.5** Point in Polygon Example. © 2014 Timothy Wright.

There are a couple of new methods added to the Utility class to draw polygons. The code is the same as used in the previous examples, but it is easier to add it to the Utility class than to copy and paste it in all the examples.

```
package javagames.util;

import java.awt.Graphics;
import java.util.List;
```
