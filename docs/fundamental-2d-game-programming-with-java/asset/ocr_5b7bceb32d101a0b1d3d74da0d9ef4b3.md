The run() method has two methods added to it to allow subclasses the ability to run code before and after the main game loop:

+   initialize() is called before the game loop starts.

+   terminate() is called after the application is closed.

The initialize() method creates and initializes the frameRate object, the terminate() method is empty, and the game loop is the same. There is nothing performed in the terminate() method, and the game loop remains the same. The three methods used to perform game actions have been made protected so subclasses can override them.

```
protected void processInput(float delta)
protected void updateObjects(float delta)
protected void render(Graphics g)
```

The processInput() method calls the poll methods for the keyboard and mouse. The render() method draws the frame rate, and the updateObjects() method is empty for the time being. See Figure 5.3.

![](bbox=[0.09, 0.45, 0.36, 0.68])

# Figure 5.3 Game Loop.

```
package javagames.util;
import java.awt.*;
import java.awt.event.*;
import java.awt.image.BufferedStrategy;
import javax.swing.JFrame;
import javax.swing.SwingUtilities;
```