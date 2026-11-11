# ### Exercise 7.10:

The winding number of a parametric curve $\gamma$ about a point $z_0$ of the complex plane is defined as

$$n(z_0,\gamma)=\frac{1}{2\pi i}\int_\gamma \frac{dz}{z-z_0}. \tag{7.141}$$

Show that by parameterizing each edge of the polygon with vertices $P_1,\dots,P_n$ with an interval of length 1, and treating the point with coordinates $(x,y)$ as the complex number $x+iy$, we can reduce this integral definition to the simplified one we gave for polygons.

# ### Exercise 7.11:

+   - (a) Show that the normal vector to a triangle with vertices $P_0,P_1,P_2$ computed by Plücker's method is indeed perpendicular to $P_1-P_0$; a similar computation works to show it's perpendicular to $P_2-P_0$.
+   - (b) Verify that for $P_0=(0,0,0)$, $P_1=(1,0,0)$, and $P_2=(0,1,0)$, the normal computed by Plücker's method points along the positive $z$-axis so that the vectors $P_2-P_0$, $P_1-P_0$, and $\mathbf{n}$ form a right-handed coordinate system.
+   - ◆ (c) Explain why the conclusion of part (b) holds regardless of the location of $P_0$, $P_1$, and $P_2$, as long as they do not lie on a single line.

# ### Exercise 7.12:

Let $P_0P_1P_2$ be a triangle in 3-space, and $\mathbf{n}$ its Plücker normal. Thinking of $\mathbf{n}$ as a covector, consider the function $v \mapsto \mathbf{n}\cdot v$. What is its value on vectors lying in the plane of the triangle?

# ### Exercise 7.13:

The inside-outside test for polygons based on ray intersections depends on the ray intersecting each edge in a single point. It also depends on the ray not passing through any polygon vertex, because if it did so, the intersections with both of the edges at the vertex would be counted. How can we avoid these problems?

+   - (a) A randomized algorithm, in which the ray direction is chosen randomly, will fail with probability zero (assuming we are using infinite-precision numbers). If the chosen ray is a failure case, we can randomly choose a new one, and with probability one the algorithm will finish.
+   - (b) We can find the set of all direction vectors of all edges in the polygon, and of all rays from the test point to all polygon vertices, and choose a direction which is different from all of these. Explain why, in the case of a very small quadrilateral, with vertices at $(\pm\varepsilon,0)$ and $(0,\pm\varepsilon)$, where $\varepsilon$ is the smallest floating-point number representable on the computer, and with a test point $Q$ at the origin, both of these approaches fail in practice. Will the more complex sum-of-inverse-cosines formula for computing the winding number work in this case?

# ### Exercise 7.14:

(To do this exercise, you'll need to know something about transformations of the plane; these will be covered in Chapter 10.)

+   - (a) Show that the area formula in Equation 7.122 is correct when $P_1$, $P_2$, and $Q$ do not lie on a line, and when $P_1$ is not on the $y$-axis, by doing two transformations: Shear in $y$ to move $P_1$ to the $x$-axis; then shear in $x$ to move $P_2$ to the $y$-axis. Show that shearing doesn't change the computed area; Cavalieri's principle shows that it doesn't change the actual area.
+   - (b) Show that the formula is right for the two remaining cases by presenting an argument for each. The formula for area is a continuous function of the coordinates of $P_1$, $P_2$, and $Q$. The actual area is also a continuous function of these coordinates. At this point we have shown that these two functions agree almost everywhere (e.g., whenever the three points do not lie on a line). By a continuity argument, they must therefore agree everywhere.