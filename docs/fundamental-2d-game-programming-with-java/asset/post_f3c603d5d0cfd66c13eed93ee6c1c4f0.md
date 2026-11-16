
```java
public class Utility {

// other methods ...

public static void drawPolygon(
    Graphics g, Vector2f[] polygon ) {
    Vector2f P;
    Vector2f S = polygon[ polygon.length - 1 ];
    for( int i = 0; i < polygon.length; ++i ) {
        P = polygon[i];
        g.drawLine( (int)S.x, (int)S.y, (int)P.x, (int)P.y );
        S = P;
    }
}

public static void drawPolygon(
    Graphics g, List<Vector2f> polygon ) {
    Vector2f S = polygon.get( polygon.size() - 1 );
    for( Vector2f P : polygon ) {
        g.drawLine( (int)S.x, (int)S.y, (int)P.x, (int)P.y );
        S = P;
    }
}
}
```

In the processInput() method, the mouse position is converted to world coordinates (covered in Chapter 5, “Simple Game Framework”). The spacebar toggles the polygon winding. Left clicks with the mouse add polygon points and right clicks clear the polygon.

The updateObjects() method sets the selected variable if the mouse is inside the polygon. Random points are then tested against the polygon and placed in the appropriate list. The pointInPolygon() method presented previously is used to determine the location of points relative to the polygon. The render() method displays the winding, mouse coordinates in world position, as well as the control descriptions. If the mouse is located inside the polygon, the polygon is drawn green; otherwise, it is drawn blue. All the randomly generated points inside the polygon are drawn green and all the points outside the polygon are drawn red.

```java
package javagames.intersection;

import java.awt.*;
import java.awt.event.*;
import java.util.*;
import java.util.List;
import javagames.util.*;

public class PointInPolygonExample extends SimpleFramework {
    private static final int MAX_POINTS = 10000;
    private ArrayList<Vector2f> poly;
    private ArrayList<Vector2f> polyCpy;
    private ArrayList<Vector2f> inside;
    private ArrayList<Vector2f> outside;
    private Vector2f mousePos;
    private boolean selected;
    private boolean winding;
    public PointInPolygonExample() {
        appWidth = 640;
        appHeight = 640;
        appTitle = "Point In Polygon Example";
        appBackground = Color.WHITE;
        appFPSColor = Color.BLACK;
    }
    @Override
    protected void initialize() {
        super.initialize();
        // polygon points and lists of point inside
        // and outside the polygon
        poly = new ArrayList<Vector2f>();
        polyCpy = new ArrayList<Vector2f>();
        inside = new ArrayList<Vector2f>();
        outside = new ArrayList<Vector2f>();
        mousePos = new Vector2f();
    }
    @Override
    protected void processInput(float delta) {
        super.processInput(delta);
        mousePos = getWorldMousePosition();
        // draw polygon for algorithm testing
        if (keyboard.keyDownOnce(KeyEvent.VK_SPACE)) {
            winding = !winding;
        }
        if (mouse.buttonDownOnce(MouseEvent.BUTTON1)) {
            poly.add(mousePos);
        }
        if (mouse.buttonDownOnce(MouseEvent.BUTTON3)) {
            poly.clear();
        }
    }
    @Override
    protected void updateObjects( float delta ) {
        super.updateObjects( delta );
        // see if the mouse is inside the polygon
        selected = pointInPolygon( mousePos, poly, winding );
        // test random points against the polygon
        Random rand = new Random();
        inside.clear();
        outside.clear();
        for( int i = 0; i < MAX_POINTS; ++i ) {
            float x = rand.nextFloat() * 2.0f - 1.0f;
            float y = rand.nextFloat() * 2.0f - 1.0f;
            Vector2f point = new Vector2f( x, y );
            if( pointInPolygon( point, poly, winding ) ) {
                inside.add( point );
            } else {
                outside.add( point );
            }
        }
    }

    private boolean pointInPolygon( Vector2f point, List<Vector2f> poly,
                                    boolean winding ) {
        // point in polygon algorithm
        int inside = 0;
        if( poly.size() > 2 ) {
            Vector2f start = poly.get( poly.size() - 1 );
            boolean startAbove = start.y >= point.y;
            for( int i = 0; i < poly.size(); ++i ) {
                Vector2f end = poly.get( i );
                boolean endAbove = end.y >= point.y;
                if( startAbove != endAbove ) {
                    float m = ( end.y - start.y ) / ( end.x - start.x );
                    float x = start.x + ( point.y - start.y ) / m;
                    if( x >= point.x ) {
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

    @Override
    protected void render( Graphics g ) {
        super.render( g );
        // render instructions
        g.drawString( "Winding: " + (winding?"ON":"OFF"), 20, 35 );
        String mouse =
            String.format( "Mouse: (%.2f,%.2f)", mousePos.x, mousePos.y );
        g.drawString( mouse, 20, 50 );
        g.drawString( "Left-Click to add points", 20, 65 );
        g.drawString( "Right-Click to clear points", 20, 80 );
        g.drawString( "Space Bar to toggle winding", 20, 95 );
        Matrix3x3f view = getViewportTransform();
        // draw test polygon
        if( poly.size() > 1 ) {
            polyCpy.clear();
            for( Vector2f vertex : poly ) {
                polyCpy.add( view.mul( vertex ) );
            }
            g.setColor( selected ? Color.GREEN : Color.BLUE );
            Utility.drawPolygon( g, polyCpy );
        }
        // draw inside point blue, outside points red
        g.setColor( Color.BLUE );
        for( Vector2f vector : inside ) {
            Vector2f point = view.mul( vector );
            g.fillRect( (int)point.x, (int)point.y, 1, 1 );
        }
        g.setColor( Color.RED );
        for( Vector2f vector : outside ) {
            Vector2f point = view.mul( vector );
            g.fillRect( (int)point.x, (int)point.y, 1, 1 );
        }
    }

    public static void main( String[] args ) {
        launchApp( new PointInPolygonExample() );
    }
}
```

## USING AN AXIS ALIGNED BOUNDING BOX (AABB) FOR INTERSECTION TESTING

An axis aligned bounding box (AABB) is a rectangle that has edges parallel to the x-axis and y-axis. See Figure 7.6.

![](img/588a4cda8f2acae94a7e1987bf99400d_171_0.png)

Figure 7.6 Axis Aligned Bounding Box. © 2014 Timothy Wright.

Because the rectangle is not rotated, it is an easy shape to use for intersection testing. The shape can be represented with only a minimum and a maximum value, as shown in Figure 7.7. Note that AABBs cannot be rotated.

![](img/588a4cda8f2acae94a7e1987bf99400d_171_1.png)

Figure 7.7 AABB Representation. © 2014 Timothy Wright.

Transforming and drawing an AABB is straightforward.

```java
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

Because the shape is not rotated, you simply need to check if there's a point between both x and y minimum and maximum values. That's all that is needed to check if a point is within an AABB.

```java
private boolean pointInAABB( Vector2f p, Vector2f min, Vector2f max ) {
    return p.x > min.x && p.x < max.x &&
           p.y > min.y && p.y < max.y;
}
```

Checking if two AABBs overlap is also easy. If any of the values do not overlap, then there is no intersection. See Figure 7.8.

![](img/588a4cda8f2acae94a7e1987bf99400d_172_0.png)

Figure 7.8 AABB Intersection. © 2014 Timothy Wright.

```java
private boolean intersectAABB( Vector2f minA, Vector2f maxA,
       Vector2f minB, Vector2f maxB ) {
    if( minA.x > maxB.x || minB.x > maxA.x ) return false;
    if( minA.y > maxB.y || minB.y > maxA.y ) return false;
    return true;
}
```

## USING CIRCLES FOR INTERSECTIONS

Circles are also a useful shape to use for intersections testing. Circles can be represented as a center point and a radius, as shown in Figure 7.9.
