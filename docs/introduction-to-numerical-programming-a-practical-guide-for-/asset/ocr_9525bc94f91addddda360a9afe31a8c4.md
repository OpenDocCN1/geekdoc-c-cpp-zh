y'_a^{(2)}. On the contrary, if y'_b^{(1)} and y'_b^{(2)} fall on different sides of y_b, it follows that y'_a is located between y'_a^{(1)} and y'_a^{(2)}, or

(y_b^{(1)} - y_b)(y_b^{(2)} - y_b) > 0 ⇒ y'_a ∉ [y'_a^{(1)}, y'_a^{(2)}], (12.77)
(y_b^{(1)} - y_b)(y_b^{(2)} - y_b) ≤ 0 ⇒ y'_a ∈ [y'_a^{(1)}, y'_a^{(2)}]. (12.78)

In a separation and root-refining strategy such as the ones discussed in Chapter 6, in the first case, one would drop the current interval and pass to a new trial interval [y'_a^{(1)}, y'_a^{(2)}]. In the second case, one would iteratively refine the derivative, and, implicitly, the solution, by bisecting the trial interval [y'_a^{(1)}, y'_a^{(2)}], until the target interval [y'_b^{(1)}, y'_b^{(2)}] bracketing the true end value y_b would decrease below a predefined tolerance.

The routine Shoot coded along these lines (see Listing 12.14) receives the entire x-mesh via vector x, along with the boundary values ya and yb, the limits dy1 and dy2 of the search interval for the first derivative, and the tolerance eps, within which the found solution is expected to meet the boundary value yb. For the repeated propagations from x[1] to x[nx] implied by the shooting algorithm, Shoot calls the auxiliary function Propag, which is a simple generic propagator based on the Euler–Cromer method.

Shoot initially performs two complete propagations for the input derivatives, dy1 and dy2, and compares the corresponding solution deviations, f1 and f2, from the desired boundary value yb. If f1 and f2 have the same sign, the interval between dy1 and dy2 certainly does not contain the sought initial derivative and the routine returns a fake dy and the flag exist set to 0. On the contrary, if the two trial solutions deviate on different sides of yb (f1 and f2 have opposite signs), the routine initiates the iterative refinement of the interval between dy1 and dy2 by bisection (see Section 6.2). At each halving step, Shoot starts the propagation with the previous average derivative, and retains, as bounding initial derivatives, those leading to final deviations of opposite signs and, which, obviously, continue to bracket the exact derivative. The ability to bracket the exact derivative, doubled by its algorithmic robustness and simplicity, are precisely the beneficial features that recommend the bisection method.

For illustration of the shooting method, we consider in the following the calculation of the Legendre polynomials, P_n(x), from their differential equation. The corresponding two-point boundary-value problem, complying with the commonly used standardization P_n(1) = 1, can be written as

d²P_n/dx² = 1/(1 - x²) [ 2x dP_n/dx - n(n+1)P_n ], (12.79)
P_n(-1) = (-1)^n,   P_n(1) = 1. (12.80)

We make explicit use of the well-defined parity of the Legendre polynomials and, taking into account their alternatively symmetric and antisymmetric character (determined by the independence of the ODE on the sign of x), the integration domain can be reduced from [-1,1] to [0,1]. In this context, the derivative at the origin, P'_n(0), which may be useful for comparison with numerical results, can be shown to satisfy the simple relation:
P'_n(0) = n P_{n-1}(0).