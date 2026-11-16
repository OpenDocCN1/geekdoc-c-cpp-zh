![](bbox=[0.1, 0.09, 0.55, 0.35])

Figure 15.24
Reflection Vector Example.
© 2014 Timothy Wright.

The ReflectionVectorExample, as shown in Figure 15.24 and located in the javagames.collision package, calculates a reflection off a line segment. The EPSILON value is used to check for parallel lines. The variables s0, s1, p0, and p1 hold two line segments. The intersection vector holds the intersection point of the two lines, and the reflection vector holds the reflection calculated from the two line segments. The s0 and s1 lines stay in the same place, the p0 point is placed when the left mouse is clicked, and the p1 point follows the mouse.

The updateObjects() method calculates the intersection using the line-line intersection algorithm described earlier. The reflection vector is calculated if an intersection is found. The reflection vector is set to null if there is no intersection.

The getIntersection() method calculates the intersection point, returning a single intersection point instead of two parametric line values. The getReflectionVector() method calculates the reflection given an initial direction vector and a normalized vector perpendicular to the reflection surface.

The render() method draws the usual frame rate and usage information. The drawLine() method transforms and draws the line segment. The ReflectionVectorExample is as follows:

```
package javagames.collision;

import java.awt.*;

import java.awt.event.MouseEvent;

import javagames.util.*;
```