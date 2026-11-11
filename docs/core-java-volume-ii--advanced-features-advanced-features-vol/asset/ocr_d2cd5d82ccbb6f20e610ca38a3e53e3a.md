The program is similar to the program in Listing 11.15. The mouse listener remembers your click on the end point of a line segment, and the mouse motion listener monitors the dragging of the end point. A set of radio buttons signal the user choices for the end cap style, join style, and solid or dashed line. The `paintComponent` method of the `StrokePanel` class constructs a `GeneralPath` consisting of the two line segments that join the three points which the user can move with the mouse. It then constructs a `BasicStroke`, according to the selections the user made, and finally draws the path.

# Listing 11.16 `stroke/StrokeTest.java`

```
```java
package stroke;

import java.awt.*;
import java.awt.event.*;
import java.awt.geom.*;
import javax.swing.*;

/**
 * This program demonstrates different stroke types.
 * @version 1.05 2018-05-01
 * @author Cay Horstmann
 */
public class StrokeTest
{
   public static void main(String[] args)
   {
      EventQueue.invokeLater(() ->
         {
            var frame = new StrokeTestFrame();
            frame.setTitle("StrokeTest");
            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            frame.setVisible(true);
         });
   }
}

/**
 * This frame lets the user choose the cap, join, and line style, and shows the resulting
 * stroke.
 */
class StrokeTestFrame extends JFrame
{
   private StrokeComponent canvas;
   private JPanel buttonPanel;
```