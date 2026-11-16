is zero, which happens when the two lines are parallel. The vectors A and B form the first line segment, and the vectors C and D form the second line segment. The intersect vector holds the intersection found using the first t value. If no intersection exists, the intersection value is null.

The processInput() method sets the D vector to the mouse position. Left-clicking sets each of the other three line points. Clicking the right mouse button clears all the points. The updateObjects() method finds the intersection of the two lines and then uses the first returned value to compute the intersection. The LineLineIntersection() method takes four vectors, two for each line segment, and returns the intersection values as an array with two values or null if no intersection is found.

The render() method draws the two line segments as well as crosshairs for the intersection location. The drawLine() method and the drawCrossHairs() methods are responsible for drawing the symbols on the screen. The LineLineIntersectionExample code is as follows:

```
package javagames.collision;

import java.awt.*;
import java.awt.event.MouseEvent;
import javagames.util.*;

public class LineLineIntersectionExample extends SimpleFramework {
    private static final float EPSILON = 0.00001f;

    private Vector2f A, B, C, D;
    private Vector2f intersect;

    public LineLineIntersectionExample() {
        appTitle = "Line Line Intersection";
        appBackground = Color.WHITE;
        appFPSColor = Color.BLACK;
    }

    @Override
    protected void processInput( float delta ) {
        super.processInput( delta );

        D = getWorldMousePosition();

        if( mouse.buttonDownOnce( MouseEvent.BUTTON1 ) ) {
            if( A == null ) A = D;
            else if( B == null ) B = D;
            else C = D;
        }
    }
```