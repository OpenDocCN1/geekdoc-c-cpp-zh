When using the parametric values returned from the following intersections tests, it is important to know whether the direction vector was normalized. If it was normalized, then only values between zero and the length are on the line segment. If it was not normalized, only values between zero and one are on the line segment.

# FINDING A LINE-RECTANGLE INTERSECTION

Determining whether a line has intersected a rectangle and knowing exactly where it intersects can be broken into two steps. The first step is to compute the intersections with the lines that form the rectangle. Keep in mind, there can be two or four intersections, and none of them may actually intersect the rectangle. See Figure 15.6.

![](bbox=[0.09, 0.35, 0.64, 0.56])

Figure 15.6
Rectangle Intersection.
© 2014 Timothy Wright.

Once these intersections are computed, then you can find the closest intersection that is actually on the rectangle. To simplify the test, the line being tested can be expressed as a parametric line. If an intersection is found, that point can then be tested to see if it is within the line segment bounds. The components of the rectangle are computed as shown in Figure 15.7.