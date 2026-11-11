nonboundary vertex of such a mesh. What is the topology of the star of the vertex? What is the topology of the link of the vertex?

**Exercise 9.4:** Show that the interpolation of values across a triangle using the scanline method is the same as the one defined using the barycentric method. Hint: Show that if the triangle is in the $xy$-plane, then each of the methods defines a function of the form $f(x, y) = Ax + By + C$. Now suppose you have two such functions with the same values at the three vertices of a triangle. Explain why they must take the same values at all interior points as well.

**Exercise 9.5:** The function $H$ of Equation 9.16 cannot exist; here’s a reason why. Suppose that it did. Define a new function

$$ K : [0, 2\pi] \times [0, 2\pi] \to [0, 2\pi] : (\theta, \phi) \mapsto H(\theta, \phi), \tag{9.26} $$

where we’re implicitly using the correspondence of the number $\theta$ in the interval $[0, 2\pi)$ with the point $(\cos\theta, \sin\theta)$ of $S^1$. Now consider the loop in the domain of $K$ consisting of three straight lines, from $(0, 0)$ to $(2\pi, 0)$, from $(2\pi, 0)$ to $(2\pi, 2\pi)$, and from $(2\pi, 2\pi)$ back to $(0, 0)$.

+   (a) Draw this path.
+   (b) For each point $p$ of this path, $K(p)$ is an element of $S^1$. Restricting $K$ to this path gives a map from the path to $S^1 \subset \mathbb{R}^2$. We can compute the winding number of this path about the origin in $\mathbb{R}^2$. Explain, using the assumed properties of $H$, why the winding numbers of the first two parts of the path must be equal.
+   (c) Explain why the winding number of the last part must be one.
+   (d) Conclude that the total winding number must be odd.
+   (e) Now consider shrinking the triangular loop toward the center of the triangle. The winding number will be a continuous integer-valued function of the triangle size. Explain why this means the winding number must be constant.
+   (f) When the triangle has shrunk to a single point, explain why the winding number must be zero.
+   (g) Explain why this is a contradiction.

**Exercise 9.6:** Use the 2D test bed to create a program to experiment with texture mapping. Display, on the left, a $100 \times 100$ checkerboard image, with $10 \times 10$ squares. Atop this, draw a triangle whose vertices are draggable. On the right, draw a fixed equilateral triangle above a $100 \times 100$ grid of tiny squares (representing display pixels). For each of these display pixels, compute and store the barycentric coordinates of its center (with respect to the equilateral triangle). Using the locations of the three draggable vertices in the checkerboard as texture coordinates, compute, for each display pixel within the equilateral triangle, the $uv$-coordinates of the pixel center, and then use these $uv$-coordinates to determine the pixel color from the checkerboard texture image (see Figure 9.14). Experiment with mapping the equilateral triangle to a tiny triangle in the texture image, and to a large one; experiment with mapping it to a tall and narrow triangle. What problems do you observe?

**Exercise 9.7:** Suppose that you have a polyline in the plane with vertices $P_0, P_1, \ldots, P_n$ and you want to "resample" it, placing multiple points on each edge, equally spaced, for a total of $k + 1$ points $Q_0 = P_0, \ldots, Q_k = P_n$.

+   (a) Write a program to do this: First compute the total length $L$ of the polyline, then place the $Q$s along the polyline so that they’re separated by $L/k$. This will require special handling at each vertex of the original polyline.
+   (b) When you’re done, you’ll notice that if $n$ and $k$ are nearly equal, many "corners" tend to get cut off the original polyline. It’s natural to say, "I want equally