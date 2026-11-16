When the mouse input is polled, this value is copied over and made available to the game loop. The current mouse position is available with the following method:

```
public Point SimpleMouseInput.getPosition()
```

Lastly, to monitor the input from the mouse scroll wheel, the input class implements the MouseWheelListener:

```
mouseWheelMoved(MouseEvent e)
```

The following method returns the clicks of the mouse wheel. If the number is negative, the wheel has been moved away from the user. If the value is positive, the wheel has been moved toward the user.

```
public int MouseWheelEvent.getWheelRotation()
```

This value is also saved in the poll() method, and is made available to the game loop from the following method:

```
public int SimpleMouseInput.getNotches()
```

The code for the SimpleMouseInput class is shown here:

```
package javagames.util;
import java.awt.*;
import java.awt.event.*;

public class SimpleMouseInput
implements MouseListener, MouseMotionListener, MouseWheelListener {
    private static final int BUTTON_COUNT = 3;
    private Point mousePos;
    private Point currentPos;
    private boolean[] mouse;
    private int[] polled;
    private int notches;
    private int polledNotches;
    public SimpleMouseInput() {
        mousePos = new Point( 0, 0 );
        currentPos = new Point( 0, 0 );
        mouse = new boolean[ BUTTON_COUNT ];
        polled = new int[ BUTTON_COUNT ];
    }
    public synchronized void poll() {
        mousePos = new Point( currentPos );
```