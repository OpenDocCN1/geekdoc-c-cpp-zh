The resizing process progresses as follows:

+   1. Original. The new size is available inside the componentResized() event.
+   2. Shrink. The current size is adjusted. In this case, it is changed to % the current size. The center is calculated by taking the difference of the original size and the % size, and cutting the remaining area in half.
+   3. The new width and height are calculated using the adjusted smaller size, so there will be a border.
+   4. The adjusted size is centered in the smaller size just like the previous viewport was centered.

The example code is shown here:

```
package javagames.timeandspace;

import java.awt.*;
import java.awt.event.*;
import java.awt.image.*;
import javagames.util.*;
import javax.swing.*;

public class ViewportRatio extends JFrame implements Runnable {
	private FrameRate frameRate;
	private BufferStrategy bs;
	private volatile boolean running;
	private Thread gameThread;
	private RelativeMouseInput mouse;
	private KeyboardInput keyboard;
	private Canvas canvas;
	private Vector2f[] tri;
	private Vector2f[] triWorld;
	private float worldWidth;
	private float worldHeight;
	public ViewportRatio() {
	}
	protected void createAndShowGUI() {
		canvas = new Canvas();
		canvas.setBackground( Color.WHITE );
		canvas.setIgnoreRepaint( true );
		getContentPane().setBackground( Color.LIGHT_GRAY );
```