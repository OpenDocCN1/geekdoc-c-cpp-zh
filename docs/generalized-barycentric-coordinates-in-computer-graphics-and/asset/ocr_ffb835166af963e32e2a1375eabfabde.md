![](bbox=[0.16, 0.11, 0.84, 0.24])

Figure 1.2 Notation used for signed angles, distances, and signed areas in a polygon \( P \).

# 1.2.2 Discrete harmonic coordinates

Discrete harmonic coordinates [136, 309] arise from the standard piecewise linear finite element approximation to the Laplace equation and are given by the weight functions

\( w_i = \cot \beta_{i-1} + \cot \gamma_i, \quad i = 1, \dots, n, \)

where \( \beta_{i-1} \) and \( \gamma_i \) are the angles shown in Figure 1.2. Interestingly, it turns out that for all polygons, whose vertices lie on a common circle, these coordinates are identical to Wachspress coordinates and therefore possess the same properties [149]. For other strictly convex polygons, they are still well-defined and satisfy all properties in (1.10), except for non-negativity. For non-convex polygons, the denominator \( W \) of these coordinates vanishes at some points in the polygon's interior, so that they are not well-defined.

# 1.2.3 Mean value coordinates

The derivation of discrete harmonic coordinates suggests that different properties of harmonic functions can be exploited to derive other generalized barycentric coordinates. Floater [144] considers the circumflucential mean value property of a harmonic function \( u: P \to \mathbb{R} \), which states that for any disc \( B = B(x, r) \subset P \) of radius \( r > 0 \), centered at \( x \), with boundary \( \partial B \),

\( u(x) = \frac{1}{2\pi r} \int_{y \in \partial B} u(y) dy. \)

He then shows that applying (1.13) to a piecewise linear function leads to *mean value coordinates*. These coordinates are given by the weight functions

\( w_i = \frac{\tan(\alpha_{i-1}/2) + \tan(\alpha_i/2)}{r_i}, \quad i = 1, \dots, n, \)

where \( \alpha_{i-1} \) and \( \alpha_i \) are the angles shown in Figure 1.2 and \( r_i = \|v_i - x\| \). Hormann and Floater [206] show that mean value coordinates are well-defined even for sets of nested simple polygons and everywhere in the plane. They are positive inside the kernel of a star-shaped polygon and satisfy properties (1.10b)