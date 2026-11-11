```
```java
innerPane.setOneTouchExpandable(true);
```
```

The "continuous layout" feature continuously repaints the contents of both components as the user adjusts the splitter. That looks classier, but it can be slow. Turn on that feature with the call

```
```java
innerPane.setContinuousLayout(true);
```
```

In the example program, we left the bottom splitter at the default (no continuous layout). When you drag it, you only move a black outline. When you release the mouse, the components are repainted.

The straightforward program in Listing 10.29 populates a list box with planets. When the user makes a selection, the planet image is displayed to the right and a description is placed in the text area on the bottom. Run the program, adjust the splitters, and try out the one-touch expansion and continuous layout features.

# Listing 10.29 — `splitPane/SplitPaneFrame.java`

```
```java
package splitPane;

import java.awt.*;

import javax.swing.*;

/**
 * This frame consists of two nested split panes to demonstrate planet images and data.
 */
class SplitPaneFrame extends JFrame
{
   private static final int DEFAULT_WIDTH = 300;
   private static final int DEFAULT_HEIGHT = 300;

   private Planet[] planets = { new Planet("Mercury", 2440, 0), new Planet("Venus", 6052, 0),
         new Planet("Earth", 6378, 1), new Planet("Mars", 3397, 2),
         new Planet("Jupiter", 71492, 16), new Planet("Saturn", 60268, 18),
         new Planet("Uranus", 25559, 17), new Planet("Neptune", 24766, 8),
         new Planet("Pluto", 1137, 1), };

   public SplitPaneFrame()
   {
      setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);

      // set up components for planet names, images, descriptions

      final JList<Planet> planetList = new JList<>(planets);
      final JLabel planetImage = new JLabel();
      final JTextArea planetDescription = new JTextArea();
```
```

*(Continues)*