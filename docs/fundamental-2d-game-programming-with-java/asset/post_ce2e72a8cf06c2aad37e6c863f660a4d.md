
```java
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
}
```

## THE PARTICLE CLASS

The Particle class represents a single element in the various explosions in the game.

```java
package javagames.completegame.object;

import java.awt.Color;
import java.awt.Graphics2D;
import javagames.util.Matrix3x3f;
import javagames.util.Vector2f;

public class Particle {
    private Vector2f pos;
    private Vector2f curPos;
    private Vector2f vel;
    private Vector2f curVel;
    private Color color;
    private float lifeSpan;
    private float time;
    private float radius;

    public Particle() {
    }

    public void setPosition( Vector2f pos ) {
        this.pos = pos;
    }

    public void setRadius( float radius ) {
        this.radius = radius;
    }

    public void setVector( float angle, float r ) {
        vel = Vector2f.polar( angle, r );
    }

    public void setColor( Color color ) {
        this.color = color;
    }

    public void setLifeSpan( float lifeSpan ) {
        this.lifeSpan = lifeSpan;
    }

    public void update( float delta ) {
        time += delta;
        curVel = vel.mul( time );
        curPos = pos.add( curVel );
    }

    public void draw( Graphics2D g, Matrix3x3f view ) {
        g.setColor( color );
        Vector2f topLeft =
            new Vector2f( curPos.x - radius, curPos.y + radius );
        topLeft = view.mul( topLeft );
        Vector2f bottomRight =
            new Vector2f( curPos.x + radius, curPos.y - radius );
        bottomRight = view.mul( bottomRight );
        int circleX = (int)topLeft.x;
        int circleY = (int)topLeft.y;
        int circleWidth = (int)( bottomRight.x - topLeft.x );
        int circleHeight = (int)( bottomRight.y - topLeft.y );
        g.fillOval( circleX, circleY, circleWidth, circleHeight );
    }

    public boolean hasDied() {
        return time > lifeSpan;
    }
}
```

## THE ASTEROID CLASS

The Asteroid class is updated by adding a sprite, and only uses the polygon for collision detection. Remember, however, that the polygon still needs to be translated and rotated. Instead of using the PolygonWrapper to wrap only the polygon, the sprite positions are also wrapped so both the sprite and the polygon can wrap from one side of the screen to the other.

```java
package javagames.completegame.object;

import java.awt.Graphics2D;
import java.util.*;

import javagames.util.*;

public class Asteroid {
    public enum Size {
        Large, Medium, Small;
    }
    private PolygonWrapper wrapper;
    private Size size;
    private Sprite sprite;
    private float rotation;
    private float rotationDelta;
    private Vector2f[] polygon;
    private Vector2f position;
    private Vector2f velocity;
    private ArrayList<Vector2f[]> collisionList;
    private ArrayList<Vector2f> positionList;

    public Asteroid( PolygonWrapper wrapper ) {
        this.wrapper = wrapper;
        collisionList = new ArrayList<Vector2f[]>();
        positionList = new ArrayList<Vector2f>();
        velocity = getRandomVelocity();
        rotationDelta = getRandomRotationDelta();
    }

    private Vector2f getRandomVelocity() {
        float angle = getRandomRadians( 0, 360 );
        float radius = getRandomFloat( 0.06f, 0.3f );
        return Vector2f.polar( angle, radius );
    }

    private float getRandomRadians( int minDegree, int maxDegree ) {
        int rand = new Random().nextInt( maxDegree - minDegree + 1 );
        return (float)Math.toRadians( rand + minDegree );
    }

    private float getRandomRotationDelta() {
        float radians = getRandomRadians( 5, 45 );
        return new Random().nextBoolean() ? radians : -radians;
    }

    private float getRandomFloat( float min, float max ) {
        float rand = new Random().nextFloat();
        return rand * ( max - min ) + min;
    }

    public void setSprite( Sprite sprite ) {
        this.sprite = sprite;
    }

    public Sprite getSprite() {
        return sprite;
    }

    public void setPolygon( Vector2f[] polygon ) {
        this.polygon = polygon;
    }

    public Vector2f[] getPolygon() {
        return polygon;
    }

    public void setPosition( Vector2f position ) {
        this.position = position;
    }

    public Vector2f getPosition() {
        return position;
    }

    public void setSize( Size size ) {
        this.size = size;
    }

    public Size getSize() {
        return size;
    }

    public void update( float time ) {
        position = position.add( velocity.mul( time ) );
        position = wrapper.wrapPosition( position );
        rotation += rotationDelta * time;
        collisionList.clear();
        Vector2f[] world = transformPolygon();
        collisionList.add( world );
        wrapper.wrapPolygon( world, collisionList );
        positionList.clear();
        positionList.add( position );
        wrapper.wrapPositions( world, position, positionList );
    }

    private Vector2f[] transformPolygon() {
        Matrix3x3f mat = Matrix3x3f.rotate( rotation );
        mat = mat.mul( Matrix3x3f.translate( position ) );
        return transform( polygon, mat );
    }

    private Vector2f[] transform( Vector2f[] poly, Matrix3x3f mat ) {
        Vector2f[] copy = new Vector2f[ poly.length ];
        for( int i = 0; i < poly.length; ++i ) {
            copy[ i ] = mat.mul( poly[ i ] );
        }
        return copy;
    }

    public void draw( Graphics2D g, Matrix3x3f view ) {
        for( Vector2f pos : positionList ) {
            sprite.render( g, view, pos, rotation );
        }
    }

    public boolean contains( Vector2f point ) {
        for( Vector2f[] polygon : collisionList ) {
            if( pointInPolygon( point, polygon ) ) {
                return true;
            }
        }
        return false;
    }

    private boolean pointInPolygon( Vector2f point, Vector2f[] polygon ) {
        boolean inside = false;
        Vector2f start = polygon[ polygon.length - 1 ];
        boolean startAbove = start.y > point.y;
        for( int i = 0; i < polygon.length; ++i ) {
            Vector2f end = polygon[ i ];
            boolean endAbove = end.y > point.y;
            if( startAbove != endAbove ) {
                float m = ( end.y - start.y ) / ( end.x - start.x );
                float x = start.x + ( point.y - start.y ) / m;
                if( x > point.x ) {
                    inside = !inside;
                }
            }
            startAbove = endAbove;
            start = end;
        }
        return inside;
    }
}
```

Don't forget that you can get the full source code on the book's website at http://www.indiegameprogramming.com.

## THE ASTEROIDFACTORY CLASS

The AsteroidFactory class has been updated to parse an XML file to create the asteroids instead of using hard-coded values. This way, you can use the files created by the Swing GUI in Chapter 16, “Tools.” The XML format is as follows:

```xml
<?xml version="1.0"?>
<models>
    <model bounds="0.5859375" size="Large" sprite="large0.png">
        <coord x="-0.029733956" y="0.283255100" />
        <coord x="-0.183098610" y="-0.111111104" />
    </model>
</models>
```

The base model file comes from saving the XML file from the polygon editor. The models saved from the editor were just pasted into this file, and the size and sprite image were added. Either importing an image and drawing the polygon shape, or exporting the polygon shape and filling it with a sprite will work for creating the rock sprites and model file. If you want, you can grab the sprites and model files from the download section of the book’s website.

```java
package javagames.completegame.object;

import java.awt.image.BufferedImage;
import java.io.InputStream;
import java.util.*;

import javagames.completegame.object.Asteroid.Size;
import javagames.util.*;

import javax.imageio.ImageIO;
import org.w3c.dom.Element;

public class AsteroidFactory {
    private Vector<Asteroid> small;
    private Vector<Asteroid> medium;
    private Vector<Asteroid> large;

    private float worldWidth;
    private PolygonWrapper wrapper;
    private Random rand;
```
