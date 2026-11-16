
```
// Toggle cursor
if (keyboard.keyDownOnce(KeyEvent.VK_C)) {
    disableCursor = !disableCursor;
    if (disableCursor) {
        disableCursor();
    } else {
        // setCursor( Cursor.DEFAULT_CURSOR ) is deprecated
        setCursor( new Cursor( Cursor.DEFAULT_CURSOR ) );
    }
}
```

```
private void render(Graphics g) {
    g.setColor( Color.GREEN );
    frameRate.calculate();
    g.drawString( mouse.getPosition().toString(), 20, 20 );
    g.drawString( "Relative: " + mouse.isRelative(), 20, 35 );
    g.drawString( "Press Space to switch mouse modes", 20, 50 );
    g.drawString( "Press C to toggle cursor", 20, 65 );

    g.setColor( Color.WHITE );
    g.drawRect( point.x, point.y, 25, 25 );
}
```

```
private void disableCursor() {
    Toolkit tk = Toolkit.getDefaultToolkit();
    Image image = tk.createImage( "" );
    Point point = new Point( 0, 0 );
    String name = "CanBeAnything";
    Cursor cursor = tk.createCustomCursor( image, point, name );
    setCursor( cursor );
}
```

```
protected void onWindowClosing() {
    try {
        running = false;
        gameThread.join();
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
    System.exit( 0 );
}
```

```
public static void main( String[] args ) {
    final RelativeMouseExample app = new RelativeMouseExample();
    app.addWindowListener( new WindowAdapter() {
        public void windowClosing( WindowEvent e ) {
            app.onWindowClosing();
        }
    });
    SwingUtilities.invokeLater( new Runnable() {
        public void run() {
            app.createAndShowGUI();
        }
    });
}
}
```

## RESOURCES AND FURTHER READING

“How to Write a Key Listener,” 1995, http://docs.oracle.com/javase/tutorial/uiswing/events/keylistener.html.

“How to Write a Mouse Listener,” 1995, http://docs.oracle.com/javase/tutorial/uiswing/events/mouselistener.html.

“How to Write a Mouse-Motion Listener,” 1995, http://docs.oracle.com/javase/tutorial/uiswing/events/mousemotionlistener.html.

This page intentionally left blank

## TRANSFORMATIONS

There are four different operations that you can do to a shape in 2D graphics. They are shown in Figure 3.1.

- Translation—Moving an object up, down, left, or right.
- Rotation—Spinning an object around a point.
- Scaling—Growing or shrinking an object.
- Shearing—Shifting an object in one or two directions.

![](img/588a4cda8f2acae94a7e1987bf99400d_69_0.png)

Figure 3.1 Translation, Rotation, Scaling, and Shearing. © 2014 Timothy Wright.

Each of these operations can be performed in different ways. They can be done by hand, to each coordinate in an object, or they can be concatenated into a matrix and then applied all at once. Each method has advantages and disadvantages, but for learning how these transformations are applied, calculating each coordinate by hand is best.

## USING THE VECTOR2F CLASS

The Vector2f class, located in the javagames.util package, is used to represent a location in space, as well as a direction. Notice that the 2D coordinate class has three values: x, y, and w. In order to use the matrix transformations to perform translation, there needs to be an extra coordinate value to get the matrix math to work. So pay no attention to the extra “w” coordinate behind the curtain, it will be explained later.

> **Note**
> Those of you familiar with vector algebra may look at the source code that follows and scream, “Wait! Points and vectors are not the same. Points have a w = 1, but vectors cannot be translated, and should have a w = 0.” I will cover that later too, so don’t worry. :-)

Translation is very simple. To move the coordinate up, down, left, or right, the distance is added to the coordinate:

```
x = x + tx;
y = y + ty;
```

Scaling is also simple. The coordinate values are multiplied by the scale factor, growing or shrinking them.

```
x = x * sx;
y = y * sy;
```

Shearing is only a little more complicated, shifting values relative to the other coordinate values. Notice the temporary value that’s used to keep the old value of x until after it is used to shear the y value. Without the temporary value, the updated values would be used to shear the y value instead of the original values. To shear the values, add to the x value the scaled y value, and to the y value add the scaled x value:

```
float tmp = x + sx * y;
y = y + sy * x;
x = tmp;
```

Rotation is more complicated to understand. Using a temporary value just like the shearing example, rotation is performed as follows:

```
float tmp = x * cos(angle) - y * sin(angle);
y = x * sin(angle) + y * cos(angle);
x = tmp;
```

In order to understand where this equation comes from, it is necessary to understand polar coordinates, which are covered later in this chapter. For now, just assume that it works.

```
package javagames.util;

public class Vector2f {
    public float x;
    public float y;
    public float w;

    public Vector2f() {
        this.x = 0.0f;
        this.y = 0.0f;
        this.w = 1.0f; //?!
    }

    public Vector2f( Vector2f v ) {
        this.x = v.x;
        this.y = v.y;
        this.w = v.w; //?!
    }

    public Vector2f( float x, float y ) {
        this.x = x;
        this.y = y;
        this.w = 1.0f; //?!
    }

    public Vector2f( float x, float y, float w ) {
        this.x = x;
        this.y = y;
        this.w = w; //?!
    }

    public void translate( float tx, float ty ) {
        x += tx;
        y += ty;
    }

    public void scale( float sx, float sy ) {
        x *= sx;
        y *= sy;
    }

    public void rotate( float rad ) {
        float tmp = (float)( x * Math.cos( rad ) - y * Math.sin( rad ) );
        y = (float)( x * Math.sin( rad ) + y * Math.cos( rad ) );
        x = tmp;
    }

    public void shear( float sx, float sy ) {
        float tmp = x + sx * y;
        y = y + sy * x;
        x = tmp;
    }
}
```

The VectorGraphicsExample, located in the javagames.transform package and shown in Figure 3.2, draws a polygon ship on the screen and applies translation, rotation, scaling, and shearing using the Vector2f class equations. The initialize() method sets up the polygon ship and calls reset(). The reset() method is responsible for setting all the transformation values back to their starting values.

![](img/588a4cda8f2acae94a7e1987bf99400d_72_0.png)

Figure 3.2
Vector Graphics Example.
© 2014 Timothy Wright.

There are keys mapped to the different transformation operations. R for rotation, S for shearing, T for translation, X for x-shearing, Y for y-shearing, and the spacebar to reset the values back to their starting values.

The polygon object is copied into the world list before being transformed. This way, the operations are not cumulative, but happen every frame. Not only does this leave the original model untouched, it allows multiple copies of the original to be used.

Each transformation operation is handled in the same way. First the Boolean value mapped to the specific transformation is checked. If it is true, then that transformation is applied, the bounds are checked, and the step values are adjusted accordingly. After the values are updated, the transformations are applied. Notice that the order of the transformations is important. Changing the order of the operations would change the results on the screen.

Inside the render() method, all the values of the translation flags are displayed. The transformed polygon is then drawn using the drawLine() method of the graphics object. The last point and first point are connected, and then each point is used to draw a line from that point to the previous point, producing a closed polygon.

```
package javagames.transform;
import java.awt.*;
import java.awt.event.*;
import java.awt.image.*;
import javagames.util.*;
import javax.swing.*;

public class VectorGraphicsExample extends JFrame
implements Runnable {

private static final int SCREEN_W = 640;
private static final int SCREEN_H = 480;
private FrameRate frameRate;
private BufferStrategy bs;
private volatile boolean running;
private Thread gameThread;
private RelativeMouseInput mouse;
private KeyboardInput keyboard;
private Vector2f[] polygon;
private Vector2f[] world;
```
