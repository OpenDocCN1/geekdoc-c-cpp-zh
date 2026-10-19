− dU(x)/dx Φ(x)|_a^b + ∫_a^b dx dU(x)/dx Φ′(x) = ∫_a^b dx 4πρ(x)Φ(x)  (23.7)

⇒ ∫_a^b dx dU(x)/dx Φ′(x) = ∫_a^b dx 4πρ(x)Φ(x) .  (23.8)

Equation 23.8 is the weak form of the PDE, “weak” in the sense that it does not require the existence of the second derivative of U, or the continuity of ρ. Because the approximate and exact solutions are related by the integral of their difference over the entire domain, the algorithm provides the global best agreement between the two.

# 23.4.2

# Galerkin Spectral Decomposition

The approximate solution to the weak PDE proceeds via three steps. First, we split the full domain of the PDE into subdomains called elements, then we find approximate solutions within each element, and finally we match the elemental solutions onto each other. For our 1D problem, the subdomain elements are straight lines of equal length, while for the 2D problem to be considered soon, the elements are triangles (Figure 23.4).

The critical step in the FEM is the expansion of the solution U in terms of a set of basis functions φ_i:

U(x) ≈ Σ_{j=0}^{N−1} α_j φ_j(x) .  (23.9)

Even when the basis functions are not sines or cosines, this expansion is still called a spectral decomposition. We will choose φ_i’s that are convenient for computation, and so the solution reduces to determining the unknown expansion coefficients α_j. Later, in order to satisfy the boundary conditions, we will add an additional term to this expansion.

Considerable study has gone into determining the effectiveness of different basis functions φ_i that are used to represent the solution on the finite elements. If the sizes of the finite elements are made sufficiently small, then good accuracy is obtained with simple piecewise-continuous basis functions φ_i. For our 1D problem, we use finite elements that are line segments between x_i and x_{i+1}, and we use basis functions, representing the solution on each line segment, that have the form of triangle or “hats” between x_{i−1} and x_{i+1} (Figure 23.2). We also require that each basis function equals 1 at the x_i vertex, φ_i(x_i) = 1:

φ_i(x) = { 0, for x < x_{i−1}, or x > x_{i+1},  (h_i = x_{i+1} − x_i), (23.10)
 (x − x_{i−1})/h_{i−1}, for x_{i−1} ≤ x ≤ x_i,
 (x_{i+1} − x)/h_i, for x_i ≤ x ≤ x_{i+1} . }