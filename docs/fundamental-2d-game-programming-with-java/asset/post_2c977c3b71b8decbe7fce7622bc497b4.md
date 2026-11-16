
```java
public PolygonWrapper( float worldWidth, float worldHeight ) {
    this.worldWidth = worldWidth;
    this.worldHeight = worldHeight;
    worldMax = new Vector2f( worldWidth / 2.0f, worldHeight / 2.0f );
    worldMin = worldMax.inv();
}

public boolean hasLeftWorld( Vector2f position ) {
    return position.x < worldMin.x || position.x > worldMax.x ||
    position.y < worldMin.y || position.y > worldMax.y;
}

public Vector2f wrapPosition( Vector2f position ) {
    Vector2f wrapped = new Vector2f( position );
    if( position.x < worldMin.x ) {
    wrapped.x = position.x + worldWidth;
    } else if( position.x > worldMax.x ) {
    wrapped.x = position.x - worldWidth;
    }
    if( position.y < worldMin.y ) {
    wrapped.y = position.y + worldHeight;
    } else if( position.y > worldMax.y ) {
    wrapped.y = position.y - worldHeight;
    }
    return wrapped;
}

public void wrapPolygon( Vector2f[] poly, List<Vector2f[]> renderList ) {
    Vector2f min = getMin( poly );
    Vector2f max = getMax( poly );
    boolean north = max.y > worldMax.y;
    boolean south = min.y < worldMin.y;
    boolean west = min.x < worldMin.x;
    boolean east = max.x > worldMax.x;
    if( west ) renderList.add( wrapEast( poly ) );
    if( east ) renderList.add( wrapWest( poly ) );
    if( north ) renderList.add( wrapSouth( poly ) );
    if( south ) renderList.add( wrapNorth( poly ) );
    if( north && west ) renderList.add( wrapSouthEast( poly ) );
    if( north && east ) renderList.add( wrapSouthWest( poly ) );
    if( south && west ) renderList.add( wrapNorthEast( poly ) );
    if( south && east ) renderList.add( wrapNorthWest( poly ) );
}

private Vector2f getMin( Vector2f[] poly ) {
    Vector2f min = new Vector2f( Float.MAX_VALUE, Float.MAX_VALUE );
    for( Vector2f v : poly ) {
        min.x = Math.min( v.x, min.x );
        min.y = Math.min( v.y, min.y );
    }
    return min;
}

private Vector2f getMax( Vector2f[] poly ) {
    Vector2f max = new Vector2f( -Float.MAX_VALUE, -Float.MAX_VALUE );
    for( Vector2f v : poly ) {
        max.x = Math.max( v.x, max.x );
        max.y = Math.max( v.y, max.y );
    }
    return max;
}

private Vector2f[] wrapNorth( Vector2f[] poly ) {
    return transform( poly, Matrix3x3f.translate( 0.0f, worldHeight ) );
}

private Vector2f[] wrapSouth( Vector2f[] poly ) {
    return transform( poly, Matrix3x3f.translate( 0.0f, -worldHeight ) );
}

private Vector2f[] wrapEast( Vector2f[] poly ) {
    return transform( poly, Matrix3x3f.translate( worldWidth, 0.0f ) );
}

private Vector2f[] wrapWest( Vector2f[] poly ) {
    return transform( poly, Matrix3x3f.translate( -worldWidth, 0.0f ) );
}

private Vector2f[] wrapNorthWest( Vector2f[] poly ) {
    return transform(
        poly, Matrix3x3f.translate( -worldWidth, worldHeight )
    );
}

private Vector2f[] wrapNorthEast( Vector2f[] poly ) {
    return transform(
        poly, Matrix3x3f.translate( worldWidth, worldHeight )
    );
}

private Vector2f[] wrapSouthEast( Vector2f[] poly ) {
    return transform(
        poly, Matrix3x3f.translate( worldWidth, -worldHeight )
    );
}

private Vector2f[] wrapSouthWest( Vector2f[] poly ) {
    return transform(
        poly, Matrix3x3f.translate( -worldWidth, -worldHeight )
    );
}

private Vector2f[] transform( Vector2f[] poly, Matrix3x3f mat ) {
    Vector2f[] copy = new Vector2f[ poly.length ];
    for( int i = 0; i < poly.length; ++i ) {
        copy[i] = mat.mul( poly[i] );
    }
    return copy;
}
```

The ScreenWrapExample, as shown in Figure 8.7 and located in the javagames.prototype package, uses the PolygonWrapper class to wrap a square that is moved around the screen. The pos vector holds the position of the square. The poly array holds the square polygon. The renderList holds the copies of the square that are wrapped, as well as the original transformed polygon. The wrapper variable is the PolygonWrapper shown previously.

![](img/588a4cda8f2acae94a7e1987bf99400d_204_0.png)

Figure 8.7 Screen Wrap Example. © 2014 Timothy Wright.

The initialize() method creates all the objects and sets the mouse to relative movements so the object can be wrapped around the screen without the mouse leaving the screen. The processInput() method moves the square by using the mouse position if the absolute position is used and by adding the relative movement to the current position if relative movement is being used. This method also toggles relative mouse movement with the spacebar.

The transform() method creates a copy of the object and transforms it by the given matrix. The updateObjects() method clears the render list, wraps and transforms the square, and then uses the PolygonWrapper to add any copies of the object to the render list. The render() method draws all the objects in the render list to the screen.

```java
package javagames.prototype;
import java.awt.*;
import java.awt.event.KeyEvent;
import java.util.ArrayList;
import javagames.util.*;
public class ScreenWrapExample extends SimpleFramework {
    private Vector2f pos;
    private Vector2f[] poly;
    private ArrayList<Vector2f[]> renderList;
    private PolygonWrapper wrapper;
    public ScreenWrapExample() {
        appBorderScale = 0.9f;
        appWidth = 640;
        appHeight = 640;
        appMaintainRatio = true;
        appTitle = "Screen Wrap Example";
        appBackground = Color.WHITE;
        appFPSColor = Color.BLACK;
    }

    @Override
    protected void initialize() {
        super.initialize();
        mouse.setRelative( true );
        renderList = new ArrayList<Vector2f[]>();
        wrapper = new PolygonWrapper( appWorldWidth, appWorldHeight );
        poly = new Vector2f[] {
            new Vector2f( -0.125f, 0.125f ),
            new Vector2f( 0.125f, 0.125f ),
            new Vector2f( 0.125f, -0.125f ),
            new Vector2f( -0.125f, -0.125f ),
        };
        pos = new Vector2f();
    }

    @Override
    protected void processInput( float delta ) {
        super.processInput( delta );

        if( mouse.isRelative() ) {
            Vector2f v = getRelativeWorldMousePosition();
            pos = pos.add( v );
        } else {
            pos = getWorldMousePosition();
        }

        if( keyboard.keyDownOnce( KeyEvent.VK_SPACE ) ) {
            mouse.setRelative( !mouse.isRelative() );
            if( mouse.isRelative() ) {
                pos = new Vector2f();
            }
        }
    }

    @Override
    protected void updateObjects( float delta ) {
        super.updateObjects( delta );

        renderList.clear();
        pos = wrapper.wrapPosition( pos );
        Vector2f[] world = transform( poly, Matrix3x3f.translate( pos ) );
        renderList.add( world );
        wrapper.wrapPolygon( world, renderList );
    }

    private Vector2f[] transform( Vector2f[] poly, Matrix3x3f mat ) {
        Vector2f[] copy = new Vector2f[ poly.length ];
        for( int i = 0; i < poly.length; ++i ) {
            copy[i] = mat.mul( poly[i] );
        }
        return copy;
    }

    @Override
    protected void render( Graphics g ) {
        super.render( g );
        g.drawString( "Press Space to Toggle mouse", 20, 35 );

        Matrix3x3f view = getViewportTransform();
        for (Vector2f[] toRender : renderList ) {
            for (int i = 0; i < toRender.length; ++i ) {
                toRender[i] = view.mul( toRender[i] );
            }
            Utility.drawPolygon( g, toRender );
        }
    }

    public static void main( String[] args ) {
        launchApp( new ScreenWrapExample() );
    }
}
```

## MAKING A PROTOTYPE ASTEROID

The PrototypeAsteroid class, also located in the javagames.prototype package, represents a rock flying through space. Upon creation, a random velocity and rotation are created. Java's random number generator only returns floating-point numbers between zero and one, so to create random numbers that span an arbitrary range, additional steps are required. For example, to return random numbers from -3 to 7, follow these steps:

- 1. Calculate the distance between the number range by subtracting the minimum value from the maximum value.
- 2. Generate a random float from zero to one.
- 3. Multiply the random number by the distance.
- 4. Shift the range by adding the minimum.

The steps make it sound a lot more confusing than it actually is.

```java
private float getRandomFloat( float min, float max ) {
    float rand = new Random().nextFloat();
    return rand * ( max - min ) + min;
}
```

The same thing is done to get a random integer. Since the random generator returns a number from zero to count minus one, the method is adjusted slightly.

```java
private float getRandomRadians( int minDegree, int maxDegree ) {
    int rand = new Random().nextInt( maxDegree - minDegree + 1 );
    return (float)Math.toRadians( rand + minDegree );
}
```
