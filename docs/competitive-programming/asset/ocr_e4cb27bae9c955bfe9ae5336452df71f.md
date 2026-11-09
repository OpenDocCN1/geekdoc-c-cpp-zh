+   6. UVa 10002 - Center of Masses (centroid of convex polygon, convex hull)
+   7. UVa 10065 - Useless Tile Packers (plus area of polygon)
+   8. UVa 10135 - Herding Frosh
+   9. UVa 10173 - Smallest Bounding Rectangle
+   10. UVa 11626 - Convex Hull

# 7.4  Intersection Problems

In geometry problems, we can virtually take any pair of objects and see if they intersect, and if they are: what is the point/area/volume of intersection? This is the source of many computational geometry problems in contests.

Line segment intersection is one the most frequent intersection problems. We can test whether two line segments intersect or not by using several ccw tests (code is shown below).

```
struct line { point p1, p2; }

int intersect(line line1, line line2) {
    return
        ((ccw(line1.p1, line1.p2, line2.p1) * ccw(line1.p1, line1.p2, line2.p2)) <= 0)
        &&
        ((ccw(line2.p1, line2.p2, line1.p1) * ccw(line2.p1, line2.p2, line1.p2)) <= 0);
}
```

However, intersections can occur between different types of objects other than two line segments. The other objects include: Cube, Box, Circle, Polygon, Triangle, Rectangle, etc. Some examples are shown below.

Programming Exercises solvable related to intersection problem:

+   - Line Segment Intersection
+     1. UVa 191 - Intersection
+     2. UVa 378 - Intersecting Lines
+     3. UVa 866 - Intersecting line segments
+     4. UVa 920 - Sunny Mountain
+     5. UVa 972 - Horizon Line
+     6. UVa 10902 - Pick-up sticks
+     7. UVa 11343 - Isolated Segments
+   
+   - Other Objects
+     1. UVa 453 - Intersecting Circles (circle and circle)
+     2. UVa 460 - Overlapping Rectangles (rectangle and rectangle)
+     3. UVa 737 - Gleaming the Cubes (cube and cube)
+     4. UVa 904 - Overlapping Air Traffic Control (3D-box and 3D-box)
+     5. UVa 10301 - Rings and Glue (circle and circle)
+     6. UVa 10321 - Polygon Intersection (convex polygon and convex polygon)