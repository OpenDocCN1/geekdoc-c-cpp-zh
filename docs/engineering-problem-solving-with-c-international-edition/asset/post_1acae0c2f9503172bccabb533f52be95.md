
/* Exit program. */
return 0;
}
/*-------------------------------------------------------------*/
/* This function computes the x coordinate of the center of a  */
/* circle given three points on the circle.                    */
/*-------------------------------------------------------------*/
double circle_xcoord(double x1,double y1,double x2,double y2,
                     double x3,double y3)
{
  /* Declare variables.                                        */
  double m12, m23, xc_num, xc_den, xc;
  /* Compute slopes of the two lines between points.           */
  m12 = (y2 - y1)/(x2 - x1);
  m23 = (y3 - y2)/(x3 - x2);
  /* Compute the x coordinate of the center of the circle.     */
  xc_num = m12*m23*(y1 - y3) + m23*(x1 + x2) - m12*(x2 + x3);
  xc_den = 2*(m23 - m12);
  xc = xc_num/xc_den;
  /* Return the x coordinate of the center.                    */
  return xc;
}
/*-------------------------------------------------------------*/

## 5. TESTING

We first test the program with the data from the hand example. This generates the following interaction:

```
Enter x and y coordinates for first point:
-1 -1
Enter x and y coordinates for second point:
1 1
Enter x and y coordinates for third point:
3 -1
Center of Circle: (1.0,-1.0)
Radius of Circle: 2.0
```

The answer matches the hand example, so we can then test the program with additional points.

## MODIFY!

These problems relate to the program developed in this section for finding the center and the radius of a circle given three points on the circle.

- 1. Modify the program so that it also prints the equation of the circle.
- 2. If either line is vertical, then the corresponding slope is infinite. Determine if this occurs, and print an error message before exiting the program.
- 3. If line P1P2 is vertical, exchange the values of P2 with P3. Then check to see if this now yields two non-vertical lines. If so, continue processing.
- 4. If line P2P3 is vertical, exchange the values of P2 with P1. Then check to see if this now yields two non-vertical lines. If so, continue processing.
- 5. Combine the solutions to problems 3 and 4 above. This solution will now work properly unless all three points are vertical, but that indicates an error in the points, because they cannot all three be on the same circle.

## 4.4 Problem Solving Applied: Iceberg Tracking

Large icebergs are tracked by satellites, and their location is specified using latitude and longitude. It is important to be able to determine the distance between the iceberg and nearby ships. In this section, we will develop a program that determines the distance between two objects when we are given their latitudes and longitudes. Before developing the program, we need to briefly discuss latitudes and longitudes and develop the equation that allows us to determine the distance between two points using latitudes and longitudes.

- Great circle
- Prime meridian
- Equator
- Latitude
- Longitude
- Global Positioning System

Assume that the earth is represented by a sphere with a radius of 3960 miles. We can then define a position on the earth’s surface in terms of a grid determined by a latitude and a longitude measurement. To understand these measurements, we first need to review the definition of a great circle—a circle formed by the intersection of a sphere and a plane that passes through the center of the sphere. If the plane does not pass through the center of the sphere, it will be a circle with a smaller circumference and hence is not a great circle. The prime meridian is a north–south great circle that passes through Greenwich, just outside London, and through the North Pole. The equator is an east–west great circle that is equidistant from the North Pole and South Pole. Thus, we can define a rectangular coordinate system such that the origin is the center of the earth, the z-axis goes from the center of the earth through the North Pole, and the x-axis goes from the center of the earth through the point where the prime meridian intersects the equator (see Figure 4.6). The latitude is an angular distance, is measured in degrees, and extends northward or southward from the equator (as in 25°N); and the longitude is an angular distance, is measured in degrees, and extends westward or eastward from the prime meridian (as in 120°W).

The Global Positioning System (GPS), originally developed for military use, uses 24 satellites circling the earth to pinpoint a location on the surface. Each satellite broadcasts a coded radio signal indicating the time and the satellite’s exact position 11,000 miles above the earth. The satellites are equipped with atomic clocks that are accurate to within one second every 70,000 years. A GPS receiver picks up the satellite signal and measures the time between the signal’s transmission and its reception. By comparing signals from at least three satellites, the receiver can determine the latitude, longitude, and altitude of its position.

![](img/02c4582f051c5b51776411c92b079035_192_0.png)

The shortest distance between two points on a sphere is shown to be on the arc of the great circle containing them. If we know the angle between two vectors from the center of the earth to the two points defining the arc, we can then estimate the distance as a proportion of the earth’s circumference. To illustrate, suppose that the angle between two vectors from the center of the earth is 45°. Then the angle is 45/360, or 1/8 of a complete revolution. Hence, the distance between the two points is 1/8 of the earth’s circumference (π times twice the radius) or 3,110 miles.

The best way to compute the shortest distance between two points that are specified in latitude and longitude is through a series of coordinate transformations. Recall that the spherical coordinates (ρ, ϕ, θ) of a point P in a rectangular coordinate system represent the length ρ (rho) of the vector connecting the point to the origin, the angle ϕ (phi) between the positive z-axis and the vector, and the angle θ (theta) between the x-axis and the projection of the vector in the xy-plane (see Figure 4.7). We then convert the spherical coordinates to rectangular coordinates (x, y, z). Finally, a simple trigonometric equation computes the angle between two points (or vectors) in rectangular coordinates. Once we know the angle between the two points, we can then use the technique described in the previous paragraph to find the distance between the two points.

We need to use equations that relate latitude and longitude to spherical coordinates, that convert spherical coordinates to rectangular coordinates, and that compute the angle between two vectors. Figure 4.7 is useful in relating the notation to the following equations:

![](img/02c4582f051c5b51776411c92b079035_192_1.png)

- Latitude/longitude and spherical coordinates: \(\alpha = 90^\circ - \phi, \beta = 360^\circ - \theta\)
- Spherical and rectangular coordinates: \(x = \rho \sin \phi \cos \theta, y = \rho \sin \phi \sin \theta, z = \rho \cos \theta\)
- Angle \(\gamma\) between two vectors \(\mathbf{a}\) and \(\mathbf{b}\): \(\cos \gamma = \mathbf{a} \cdot \mathbf{b} / (|\mathbf{a}||\mathbf{b}|)\)
  - where \(\mathbf{a} \cdot \mathbf{b}\) is the dot product of \(\mathbf{a}\) and \(\mathbf{b}\) and \(|\mathbf{a}|\) is the length of the vector \(\mathbf{a}\).
- Dot product of two vectors \((x_a, y_a, z_a)\) and \((x_b, y_b, z_b)\) in rectangular coordinates: \(\mathbf{a} \cdot \mathbf{b} = x_a x_b + y_a y_b + z_a z_b\)
- Length of a vector \((x_a, y_a, z_a)\) in rectangular coordinates: \(|\mathbf{a}| = \sqrt{(x_a^2 + y_a^2 + z_a^2)}\)
- Great circle distance: distance \(= (\gamma/(2\pi))(\text{earth's circumference}) = (\gamma/(2\pi))(\pi \cdot 2 \text{ radius}) = \gamma \cdot 3960\).

Pay close attention to the angle units in these equations. Unless otherwise specified, it is assumed that the angles are measured in radians. (Recall that an angle in degrees can be converted to radians by multiplying it by the factor \(\pi/180\).)

Write a program that asks the user to enter the latitude and longitude coordinates for two points in the Northern Hemisphere. Then compute and print the shortest distance between the two points.

### 1. PROBLEM STATEMENT

Compute the shortest distance between two points in the Northern Hemisphere.

### 2. INPUT/OUTPUT DESCRIPTION

For this program, the input is the latitude and longitude of two points in the Northern Hemisphere. The output is the shortest distance between the points, as shown in the following diagram.

![](img/02c4582f051c5b51776411c92b079035_193_0.png)
