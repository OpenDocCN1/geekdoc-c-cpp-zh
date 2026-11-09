
### Spheres

- 1. A Sphere is a perfectly round geometrical object in 3-D space.

- 2. The **Great-Circle Distance** between any two points A and B on sphere [38] is the shortest distance along a path on the **surface of the sphere**. This path is equal to the length of the Arc of the **Great-Circle** of that sphere that pass through the two points A and B.

The Great-Circle of a sphere is defined as the circle that runs along the surface of the sphere so that it cuts the sphere into two equal hemispheres. To find the solution to the Great-Circle Distance, we find the central angle AOB (see Figure 7.4) of the Great-Circle and use it to determine the length of the arc.

Although quite rare, some contest problems use this distance metric. Usually, the two points on the surface of a sphere are given as (latitude, longitude) pair. The following library code will help us obtain the shortest great-circle distance given two points on the sphere and the radius of the sphere. For the derivation of this library code, see [38].

![](img/2f3eff2c1d9ecd727dd36c1db12a8ec9_136_0.png)

![](img/2f3eff2c1d9ecd727dd36c1db12a8ec9_136_1.png)

Figure 7.4: Great-Circle and Great-Circle Distance (Arc A-B) (Figures from [46])

```cpp
double greatCircleDistance(double pLat, double pLong,
                           double qLat, double qLong, double radius) {
    pLat *= PI / 180; pLong *= PI / 180;
    qLat *= PI / 180; qLong *= PI / 180;
    return radius * acos(cos(pLat)*cos(pLong)*cos(qLat)*cos(qLong) +
                         cos(pLat)*sin(pLong)*cos(qLat)*sin(qLong) +
                         sin(pLat)*sin(qLat));
}
```

Programming Exercises related to the Great-Circle Distance:

- 1. UVa 535 - Globetrotter
- 2. UVa 10075 - Airlines (with APSP)
- 3. UVa 10316 - Airline Hub
- 4. UVa 10897 - Travelling Distance
- 5. UVa 11817 - Tunnelling The Earth

### Polygons

- 1. A **Polygon** is a plane figure that is bounded by a closed path or circuit composed of a finite sequence of straight line segments. These segments are called edges or sides. The point where two edges meet are the polygon’s vertex or corner. The interior of the polygon is sometimes called its body.

- 2. A polygon is said to be **Convex** if any line segment drawn inside the polygon does not intersect any edge of the polygon. Otherwise, the polygon is called **Concave**.

- 3. The area \(A\) of an \(n\)-sided polygon (either convex or concave) with \(n\) pairs of vertex coordinates given in some order (clockwise or counter-clockwise) is:

\[
A = \frac{1}{2}\left|\begin{array}{cc}
x_1 & y_1 \\
x_2 & y_2 \\
x_3 & y_3 \\
\vdots & \vdots \\
x_n & y_n
\end{array}\right|
= \frac{1}{2}(x_1y_2 + x_2y_3 + x_3y_4 + \cdots + x_ny_1 - x_2y_1 - x_3y_2 - x_4y_3 - \cdots - x_1y_n)
\]

This can be written into the library code below. Notice that our default setting is all-integer coordinates and use all-integer operations whenever possible. You need to change a part of this code if the given points are not integers:

```cpp
struct point { int x, y; } // a point has two members

int determinant(vector<point> P) { // default: integer computation
  int result = 0, x1, y1, x2, y2;
  for (int i = 0; i < P.size(); i++) {
    x1 = P[i].x; x2 = P[(i + 1) % P.size()].x;
    y1 = P[i].y; y2 = P[(i + 1) % P.size()].y;
    result += (x1 * y2 - x2 * y1);
  }
  return result;
}

// area is half of the determinant and the result may be a non-integer
double area(vector<point> P) { return fabs(determinant(P) / 2.0); }
```

- 4. The perimeter \(p\) of an \(n\)-sided polygon with \(n\) pairs of coordinates given in some order (clockwise or counter-clockwise) can be computed with Pythagorean theorem:

```cpp
double perimeter(vector<point> P) { // point has x & y
  double result = 0.0, x1, y1, x2, y2, dx, dy;
  for (int i = 0; i < P.size(); i++) {
    x1 = P[i].x; x2 = P[(i + 1) % P.size()].x;
    y1 = P[i].y; y2 = P[(i + 1) % P.size()].y;
    dx = x2 - x1;
    dy = y2 - y1;
    result += sqrt(dx * dx + dy * dy);
  }
  return result;
}
```

- 5. Testing if a polygon is convex (or concave) is easy with a quite robust^3 geometric predicate test called **CCW (Counter Clockwise) Test** (a.k.a. **Left-Turn Test**).

CCW test is a simple yet important predicate test in computational geometry. This test takes in 3 points \(p\), \(q\), \(r\) in a plane and determine if the sequence \(p \rightarrow q \rightarrow r\) is a left turn^4. For example, \(CCW(p,q,r)\) where \(p=(0,0)\), \(q=(1,0)\), \(r=(0,1)\) is true. This test can be implemented with the following library code:

```cpp
int turn(point p, point q, point r) {
    int result = (r.x - q.x) * (q.y - p.y) - (r.y - q.y) * (p.x - q.x);
    if (result < 0) return -1; // P->Q->R is a right turn
    if (result > 0) return 1;  // P->Q->R is a left turn
    return 0; // P->Q->R is a straight line, i.e. P, Q, R are collinear
}

// Note: sometimes, we change the '> 0' to '>= 0' to accept collinear points
bool ccw(point p, point q, point r) { return (turn(p, q, r) > 0); }
```

With the library code above, we can now check if a polygon is convex by verifying if all three consecutive points in the polygon make left-turns if visited in counter clockwise order. If we can find at least one triple where this is false, the polygon is concave.

Programming Exercises related to Polygons:

- 1. UVa 478 - Point in Figures: Rectangles, Circles, and Triangles (point inside polygon)
- 2. UVa 634 - Polygon (point inside polygon)
- 3. UVa 10078 - Art Gallery (testing if a polygon is convex)
- 4. UVa 10112 - Myacm Triangles (check if point in triangle with area tests like UVa 478)
- 5. UVa 11447 - Reservoir Logs (area of polygon)
- 6. UVa 11473 - Campus Roads (perimeter of polygon)

There are of course exists many other geometric shapes, objects, and formulas that have not been covered yet, like 3-D objects, etc. What we have covered so far are the ones which appear more frequently in programming contests.

Other Programming Exercises related to Basic Geometry that are not listed above:

- 1. UVa 10088 - Trees on My Island (Georg A. Pick's Theorem: \(A = i + \frac{b}{2} - 1\), see [43])
- 2. UVa 10297 - Beavergnaw (cones, cylinders, volumes)
- 3. UVa 10387 - Billiard (expanding surface, trigonometry)
- 4. UVa 11322 - Cylinder (circles, rectangles, cylinders)
- 5. UVa 11507 - Bender B. Rodriguez Problem (simulation)

## 7.3 Graham’s Scan

The **Convex Hull** of a set of points \(P\) is the smallest convex polygon \(CH(P)\) for which each point in \(P\) is either on the boundary of \(CH(P)\) or in its interior (see Figure 7.5.D). Every vertex in \(CH(P)\) is a vertex in original \(P\). Thus, the algorithm of finding convex hull must decide which vertices in \(P\) to be chosen as part of the convex hull.

![](img/2f3eff2c1d9ecd727dd36c1db12a8ec9_139_0.png)

Figure 7.5: Convex Hull \(CH(P)\) of Set of Points \(P\)

There are several convex hull algorithms available. In this section, we choose the \(O(n \log n)\) Ronald Graham’s Scan algorithm. This algorithm first sorts all \(n\) points of \(P\) (Figure 7.5.A) based on its angle w.r.t a point called pivot. In our example, we pick bottommost and rightmost point in \(P\) as pivot (see point 0 and the counter-clockwise order of the remaining points in Figure 7.5.B).

Then, this algorithm maintains a stack \(S\) of candidate points. Each point of \(P\) is pushed once on to \(S\) and points that are not going to be part of \(CH(P)\) will be eventually popped from \(S\). Examine Figure 7.5.C. The stack previously contains (bottom) 11-0-1-2 (top), but when we try to insert 3, 1-2-3 is a right turn, so we pop 2. Now 0-1-3 is a left turn, so we insert 3 to the stack, which now contains (bottom) 11-0-1-3 (top).

When Graham’s Scan terminates, whatever left in \(S\) are the points of \(CH(P)\) (see Figure 7.5.D), the stack contains (bottom) 11-0-1-4-7-10-11 (top)). Graham Scan’s eliminates all the right turns! Check that the sequence of vertices in \(CH(P)\) always makes left turns – a convex polygon.

The implementation of Graham’s Scan, omitting parts that have shown earlier like ccw function, is shown below.

```cpp
point pivot; // global variable
vector<point> polygon, CH;

int area2(point a, point b, point c) {
    return a.x * b.y - a.y * b.x + b.x * c.y - b.y * c.x + c.x * a.y - c.y * a.x;
}

int dist2(point a, point b) { // function to compute distance between 2 points
    int dx = a.x - b.x, dy = a.y - b.y; return dx * dx + dy * dy;
}

bool angle_cmp(point a, point b) { // important angle-sorting function
    if (area2(pivot, a, b) == 0) // collinear
        return dist2(pivot, a) < dist2(pivot, b); // which one closer

    int d1x = a.x - pivot.x, d1y = a.y - pivot.y;
    int d2x = b.x - pivot.x, d2y = b.y - pivot.y;
    return (atan2((double)d1y, (double)d1x) - atan2((double)d2y, (double)d2x)) < 0;
}
```
