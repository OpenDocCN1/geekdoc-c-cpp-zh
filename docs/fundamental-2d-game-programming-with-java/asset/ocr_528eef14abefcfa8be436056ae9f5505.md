# # USING THE RECTANGLE-RECTANGLE OVERLAP METHOD

To test for overlapping rectangles, the same method is used. The center, width, height, and two axis vectors need to be computed for each rectangle. See Figure 7.22.

![](bbox=[0.1, 0.18, 0.43, 0.3])

Figure 7.22 Rectangle Overlap Calculations. © 2014 Timothy Wright.

To project the radius onto an axis, a single vector to the corner cannot be used, because the rotation can cause the projection to be incorrect. See Figure 7.23. You must always project the width and height separately in order to project the correct radius.

![](bbox=[0.1, 0.51, 0.43, 0.63])

Figure 7.23 Rectangle Radius Projection. © 2014 Timothy Wright.

The RectRectOverlapExample, as shown in Figure 7.24 and located in the javagames.intersection package, holds the four points of a base rectangle that is copied for each of the two rectangles tested in the example. Each rectangle testing for overlap has an array of points, a position, and a rotation in radians. The intersection variable holds the state of the separating axis test.