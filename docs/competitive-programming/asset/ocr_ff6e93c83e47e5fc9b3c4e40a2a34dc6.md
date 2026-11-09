+   - Spheres

+   1. A Sphere is a perfectly round geometrical object in 3-D space.

+   2. The **Great-Circle Distance** between any two points A and B on sphere [38] is the shortest distance along a path on the **surface of the sphere**. This path is equal to the length of the Arc of the **Great-Circle** of that sphere that pass through the two points A and B.
+   
+   The Great-Circle of a sphere is defined as the circle that runs along the surface of the sphere so that it cuts the sphere into two equal hemispheres. To find the solution to the Great-Circle Distance, we find the central angle AOB (see Figure 7.4) of the Great-Circle and use it to determine the length of the arc.
+   
+   Although quite rare, some contest problems use this distance metric. Usually, the two points on the surface of a sphere are given as (latitude, longitude) pair. The following library code will help us obtain the shortest great-circle distance given two points on the sphere and the radius of the sphere. For the derivation of this library code, see [38].

![](bbox=[0.329, 0.375, 0.5, 0.521])

![](bbox=[0.514, 0.372, 0.685, 0.52])

Figure 7.4: Great-Circle and Great-Circle Distance (Arc A-B) (Figures from [46])

```
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

+   1. UVa 535 - Globetrotter
+   2. UVa 10075 - Airlines (with APSP)
+   3. UVa 10316 - Airline Hub
+   4. UVa 10897 - Travelling Distance
+   5. UVa 11817 - Tunnelling The Earth