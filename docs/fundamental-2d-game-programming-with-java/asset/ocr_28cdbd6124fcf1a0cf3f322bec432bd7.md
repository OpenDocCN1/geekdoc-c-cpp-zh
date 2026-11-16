# Tip

Make sure to convert the radians to degrees before using the drawArc() method.

```
```java
package javagames.transform;

import java.awt.*;
import java.awt.event.*;
import java.awt.geom.*;
import javagames.util.*;
import javax.swing.*;

public class PolarCoordinateExample extends JFrame
        implements Runnable {

    private static final int SCREEN_W = 640;
    private static final int SCREEN_H = 480;

    private FrameRate frameRate;
    private BufferStrategy bs;
    private volatile boolean running;
    private Thread gameThread;
    private RelativeMouseInput mouse;
    private KeyboardInput keyboard;
    private Point coord;

    public PolarCoordinateExample() {
    }

    protected void createAndShowGUI() {
        Canvas canvas = new Canvas();
        canvas.setSize( SCREEN_W, SCREEN_H );
        canvas.setBackground( Color.BLACK );
        canvas.setIgnoreRepaint( true );
        getContentPane().add( canvas );
        setTitle( "Polar Coordinate Example" );
        setIgnoreRepaint( true );
        pack();

        // Add key listeners
        keyboard = new KeyboardInput();
        canvas.addKeyListener( keyboard );

        // Add mouse listeners
        // For full screen : mouse = new RelativeMouseInput( this );
        mouse = new RelativeMouseInput( canvas );
        canvas.addMouseListener( mouse );
        canvas.addMouseListener( mouse );
    }
```
```