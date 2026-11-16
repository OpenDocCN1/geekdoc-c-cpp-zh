+   1. If there is a constant term, $d$, divide by the constant, redefining the other coefficients (e.g., $a = \frac{a}{d}$), resulting in a form of the quadric equation in which the constant term is unity:
+   
+   $$ax^2 + by^2 + cz^2 + 2fyz + 2gzx + 2hxy + px + qy + rz + 1 = 0. \quad (12.103)$$

This equation can then be written in the following form

$$[x \ y \ z \ 1] \begin{bmatrix} a & h & g & p \\ h & b & f & q \\ g & f & c & r \\ 0 & 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} x \\ y \\ z \\ 1 \end{bmatrix} = 0. \quad (12.104)$$

+   2. Consider the upper left $3 \times 3$ submatrix. Obtain its three eigenvalues, $\lambda_1, \lambda_2, \text{and } \lambda_3$. Then find the reciprocal of each that is nonzero, $r_1 = \frac{1}{\lambda_1}, r_2 = \frac{1}{\lambda_2}, \text{and } r_3 = \frac{1}{\lambda_3}$.
+   3. At least one reciprocal must be positive to have a real surface.
+   4. If exactly one is positive then the surface is a hyperboloid of two sheets.
+   5. If exactly two are positive, then it is a hyperboloid of one sheet.
+   6. If all three are positive, it is an ellipsoid, and the square roots of $r_1, r_2, r_3$ are the major axes of the ellipsoid.
+   7. Otherwise the distance between the foci of hyperboloids is determined by the magnitudes of the $r$'s.

# 12.7.3 Fitting Ellipses and Ellipsoids

Although this section discusses fitting surfaces, we have introduced the concept of algebraic distance, and this is an appropriate place to consider again the simpler case of fitting ellipses to curve data, as well as the three-dimensional extension to fitting ellipsoids. An ellipse is described by the general equation for a conic section:

$$ax^2 + hxy + cy^2 + dx + ey + f = 0. \quad (12.105)$$

This implicit form describes not only ellipses, but lines, hyperbolas, parabolas, and circles. To guarantee that the resulting curve is an ellipse we must also ensure that it satisfies

$$b^2 - 4ac < 0. \quad (12.106)$$

Satisfying this constraint produces an optimization problem that is nonlinear. Instead, we could use residuals to find the coefficients $a - f$ exactly as was done in the previous section.

Following this approach provides a solution that works reasonably well but tends to fit of low curvature with hyperbolic arcs rather than with ellipses. Similar difficulties occur when attempting to fit ellipsoids to range data. See Wang [12.54], Rosin and West [12.36], and Fitzgibbon et al. [12.9] for more details.

There is a fast and easy solution to finding ellipses, which works well if neither end of the major axis is occluded, which we already discussed in Section 9.4, and another method by Lei and Wong [12.58], which uses accumulators in a powerful way.