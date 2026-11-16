```
@Override
protected void onShutDown() {
    super.onShutDown();
    GraphicsEnvironment ge =
        GraphicsEnvironment.getLocalGraphicsEnvironment();
    GraphicsDevice gd = ge.getDefaultScreenDevice();
    gd.setDisplayMode( currentDisplayMode );
    gd.setFullScreenWindow( null );
}
}
```

The SwingFramework, located in the same package, is an example of extending the GameFramework and adding Swing components. This framework is used to create a better editor for the game assets. The getScreenWidth() and getScreenHeight() methods return the canvas size, which will be the portion of the GUI with the game rendering. The renderFrame() method is the same as the WindowFramework.

The fun stuff happens in the createFramework() method. First, the look and feel is updated to the Nimbus version. Then a main panel is created. This panel creates a game canvas on another panel, uses a null layout manager to maintain the aspect ratio, and adds the whole thing to the center of the main panel using a BorderLayout. The usual input and buffer strategy are created with the canvas.

Because a null layout is used, whenever the canvas size and location are updated, the repaint() method is called. Also, notice that this framework creates another method to be overridden. The onCreateAndShowGUI() is called after the creation of the Swing component, but before the GUI is visible, so other components can be added. This class will be extended further with the updated PolygonEditor later in the chapter.

```
package javagames.util;
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;
```

```
public class SwingFramework extends GameFramework {
    protected Canvas canvas;
    private JPanel mainPanel;
    private JPanel centerPanel;
    protected JPanel getMainPanel() {
        if( mainPanel == null ) {
            mainPanel = new JPanel();
        }
```