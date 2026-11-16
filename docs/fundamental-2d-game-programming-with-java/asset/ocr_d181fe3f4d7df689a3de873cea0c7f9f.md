```
public synchronized void keyReleased( KeyEvent e ) {
    int keyCode = e.getKeyCode();
    if ( keyCode >= 0 && keyCode < keys.length ) {
        keys[ keyCode ] = false;
    }
}

public void keyTyped( KeyEvent e ) {
    // Not needed
}
}
```

> **Tip**
> Don't forget that you can find the full source code on the book's website at http://www.indiegameprogramming.com.

The SimpleKeyboardExample class, located in the javagames.input package, is a simple test using the keyboard input class, replacing the rendering code with input processing code. Notice that the SimpleKeyboardInput is added to the application with the addKeyListener() method. Inside the game loop, instead of clearing the image and displaying the frame rate, the game clock checks for the spacebar or the arrow keys and prints out a message whenever the keys are pressed.

When checking the spacebar, the example uses a variable to save the state of the key, only printing to the console once every keypress. The arrow keys, however, continuously print their state to the console until they are released.

```
package javagames.input;

import java.awt.event.*;
import javax.swing.*;
import javagames.util.*;

public class SimpleKeyboardExample extends JFrame implements Runnable {
    private volatile boolean running;
    private Thread gameThread;
    private SimpleKeyboardInput keys;
    private boolean space;
    private boolean arrow;

    public SimpleKeyboardExample() {
        keys = new SimpleKeyboardInput();
    }

    protected void createAndShowGUI() {
        setTitle( "Keyboard Input" );
```