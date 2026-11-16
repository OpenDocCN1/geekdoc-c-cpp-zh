First, the onShutDown() method is not abstract, so children are not required to override it. The second important part is the check for the current thread. The code cannot shut down the game thread and join the thread if the shutdown method is called from the game thread, so it is necessary to only shut down the game thread if you're not on the game thread.

```
package javagames.util;

import java.awt.*;
import java.awt.event.*;
import java.awt.image.BufferedStrategy;
import javax.swing.*;

public abstract class GameFramework extends JFrame implements Runnable {
    private BufferStrategy bs;
    private volatile boolean running;
    private Thread gameThread;

    protected int vx;
    protected int vy;
    protected int vw;
    protected int vh;

    protected FrameRate frameRate;
    protected RelativeMouseInput mouse;
    protected KeyboardInput keyboard;

    protected Color appBackground = Color.BLACK;
    protected Color appBorder = Color.LIGHT_GRAY;
    protected Color appFPSColor = Color.GREEN;
    protected Font appFont = new Font( "Courier New", Font.PLAIN, 14 );
    protected String appTitle = "TBD-Title";
    protected float appBorderScale = 0.8f;
    protected int appWidth = 640;
    protected int appHeight = 640;
    protected float appWorldWidth = 2.0f;
    protected float appWorldHeight = 2.0f;
    protected long appSleep = 10L;
    protected boolean appMaintainAspectRatio = false;
    protected boolean appDisableCursor = false;
    protected int textPos = 0;
}
```