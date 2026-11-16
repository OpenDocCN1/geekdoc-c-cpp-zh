![](bbox=[0.102, 0.085, 0.435, 0.225])

Figure 7.20
Line-Line Overlap.
© 2014 Timothy Wright.

```
if |n̂₁ * (C₁ - C₂)| > |n̂₁ * r₂| : no overlap
if |n̂₂ * (C₁ - C₂)| > |n̂₂ * r₁| : no overlap
```

Because the comparisons are only using distance, which is always a positive value, they use the absolute value to ensure that no negative values are computed.

![](bbox=[0.102, 0.445, 0.365, 0.635])

Figure 7.21
Line-Line Overlap Example.
© 2014 Timothy Wright.

The LineLineOverlapExample, located in the javagames.intersection package and shown in Figure 7.21, stores two lines—P, 0 for the initial line and start, end for the second line. The start point is placed when the left mouse button is clicked and the end point follows the mouse pointer.

Inside the updateObject() method, the two lines are checked to see if they overlap using the separating axis method. The two lines are used to find the center, the radius, and each axis normal. Then the projected distance between the centers is compared to the radius of both lines. If the distance is larger than the radius, there is no overlap.