![](bbox=[0.217, 0.141, 0.696, 0.506])

**Figure 11.14**  The *StrokeTest* program

choices for the end cap style, join style, and solid or dashed line. The `paintComponent` method of the `StrokePanel` class constructs a `GeneralPath` consisting of the two line segments that join the three points which the user can move with the mouse. It then constructs a `BasicStroke`, according to the selections the user made, and finally draws the path.

```
```java
// Listing 11.2  stroke/StrokeTest.java
package stroke;

import java.awt.*;
import java.awt.event.*;
import java.awt.geom.*;
import javax.swing.*;

/**
 * This program demonstrates different stroke types.
 * @version 1.04 2016-05-10
 * @author Cay Horstmann
 */
```
```