
# Unsteady, Non-Linear, and Chaotic Systems

The general integral of the differential equation (4.522a) is (4.523a), and the initial conditions (4.523b, c) lead to (4.523d):

$y(x) = A \cos x + B \sin x; \quad y(0) = A, \quad y'(0) = B, \quad y(x) = \cos x. (4.523a--d)$

The finite difference equation (4.522b) will be solved next (note 4.10) to compare with the exact solution (4.523d).

## NOTE 4.10: General Solution of a Finite Difference Equation

The finite difference equation (4.522b) has a (subsection 1.9.1) solution of the form (1.444a) = (4.524a) where $\lambda$ is a root of the characteristic polynomial (4.524b):

$y_n = \lambda^n; \quad 0 = \lambda^2 - 2\lambda + (1 + h^2)\lambda = (\lambda - \lambda_+)(\lambda - \lambda_-). \quad (4.524a--c)$

The roots (4.524c) of the characteristic polynomial (4.524b) are (4.525a) leading to the general solution (4.525b) = (4.525c):

$\lambda_{\pm} = 1 \pm ih; \quad y_n = A(\lambda_+)^n + B(\lambda_-)^n = A(1 + ih)^n + B(1 - ih)^n, \quad (4.525a--c)$

where $A, B$ are arbitrary constants determined from initial conditions. initial conditions (4.523b, c) for the differential equation (4.523a) correspond (4.511) to (4.526a, b) for the finite difference equation, and imply (4.526c, d):

$1 = y(0) = y_0, y'(0) = \frac{y_1 - y_0}{h}; \quad y_1 = y_0 = 1. \quad (4.526a--d)$

Substituting (4.525c) in (4.526c, d) leads to (4.527a, b) implying (4.527c), which determines the two constants of integration (4.528d, e):

$1 = y_0 = A + B, \quad 1_1 = A + B + ih(A - B); ih(A - B) = 0. \quad A = B = \frac{1}{2}. \quad (4.527a--e)$

Substitution of (4.527d, e) in (4.525b) represents the solution of the finite difference equation (4.522b) with initial conditions (4.526c, d):

$y_n = \frac{1}{2}[(1 + ih)^n + (1 - ih)^n]. \quad (4.528)$

# Non-Linear Differential Equations and Dynamical Systems

Using the binomial expansion (4.518) for the two terms on the r.h.s. of (4.529):

$$(1\pm ih)^n = \sum_{k=0}^n \frac{n}{k}(\pm ih)^k, \quad (4.529)$$

yields by addition:

$$y_n = \sum_{k=0}^{n/2} \frac{n}{2k}(\pm ih)^{2k} = \sum_{k=0}^{n/2} \frac{n!(-)^k}{(2k)!(n-2k)}h^{2k}, \quad (4.530)$$

involving powers of h. It has been shown that the solutions (problem 158) of the linear differential (4.522a) [finite difference (4.522b)] equations of second-order with constant coefficients are related (4.522a) [(4.525c)] by the discretization (4.512b) with step h; the corresponding initial conditions (4.531b, c) [(4.526c, d)] lead to the exact (4.523d) [approximate (4.528) (4.530)] solutions, that are compared next (note 4.11).

## NOTE 4.11: Comparison of the Exact and Approximate Solutions

The exact solution (4.523d) of the differential equation (4.522a) with boundary-conditions (4.523b, c) is given by (4.531b) at the points (4.531a) separated by her step h:

$$x_n = nh; \quad \cos(x_n) = \cos(nh) = \sum_{k=0}^\infty \frac{(-)^k}{(2k)!}(nh)^{2k}, \quad (4.531a-c)$$

where the power series for the cosine (II.714a, b) = (4.531c) was used. Comparison of the exact (4.531a) [approximate (4.530)] solutions shows the substitution of coefficients (4.532a) [(4.532b):

$$\frac{n!}{(n-2k)!} = n(n-1)...(n-2k+1). \quad (4.532)$$

The approximate solution (4.530) may be taken to order ($h^4$) in (4.533a):

$$y_n^{(1)} = 1 - \frac{n(n-1)}{2}h^2 + \epsilon_n^{(1)}, \quad \epsilon_n^{(1)} = O(h^4), \quad (4.533a, b)$$
$$y_n^{(2)} = y_n^{(1)} + \frac{n(n-1)(n-2)}{24}h^4 + \epsilon_n^{(2)}, \quad \epsilon_n^{(1)} = O(h^6), \quad (4.533a, b)$$

## NOTE 4.12: Effects of Step Size and Order of Approximation

The circular cosine has period $2\pi$ in (4.535a), and is skew-symmetric in the whole (4.535b) interval:

$$\cos(x+2\pi)=\cos x, \quad \cos(x+\pi)=-\cos x, \quad \cos\left(\frac{\pi}{2}-x\right)=-\cos\left(\frac{\pi}{2}+x\right), \quad (4.535a-c)$$

and thus it is sufficient to calculate it in one-quarter of the interval (4.536c) with equal steps: $n=0,...,N=50: 0\le x\le\frac{\pi}{2}, x_n=nh, h=\frac{\pi}{2N}=0.3146, 0.1570. (4.536-f)$

The effects of step size h and order of approximation on the order of the approximate (4.533a, b; 4.534a) versus the exact (4.531a–c) solution are considered next (note 4.12). In (problem 159) 10 steps are used corresponding to angles $\theta=18^\circ$ ($9^\circ$). Table 4.7 compares five points the exact solution (4.523d) with the approximate solution (4.530), using the first (second) order (4.533a) and the corresponding error (4.533b). The lower approximation (4.533a) applies only for $n\ge4$. The error increases with distance from the initial point, and the approximate solutions:

### TABLE 4.7 Comparison of Exact and Approximate Solutions

| $n$ | $\theta$ | $x_n=n\pi/10$ | $\cos(x_n)$ | $y_n^{(1)}$ | $e_n^{(1)}$ | $y_n^{(2)}$ | $e_n^{(2)}$ |
|---|---|---|---|---|---|---|---|
| 0 | $0^\circ$ | 0.000 | 1.000 | 1.000 | 0.000 | 1.000 | 0.000 |
| 1 | $18^\circ$ | 0.314 | 0.951 | 1.000 | +0.0484 | 1.000 | +0.0484 |
| 2 | $36^\circ$ | 0.628 | 0.809 | 0.901 | +0.0929 | 0.910 | +0.0929 |
| 3 | $54^\circ$ | 0.942 | 0.587 | 0.703 | +0.1116 | 0.731 | +0.1163 |
| 4 | $72^\circ$ | 1.256 | 0.309 | 0.407 | +0.0981 | 0.417 | +0.1085 |
| 5 | $90^\circ$ | 1.570 | 0.000 | 0.013 | +0.0143 | 0.064 | +0.0671 |

Note: The numerical solution of a differential equation leads to errors that: (i) increase with distance from the initial point; (ii) for the same distance from the initial point decrease for higher orders of the step size, e.g., $O(h^2)$ are more generally but not always more accurate $O(h)$ methods.

### TABLE 4.8 Higher Accuracy with Smaller Step Size

| n | $\theta$ | $x_n = n\pi/20$ | $\cos(x_n)$ | $y_n^{(1)}$ | $\epsilon_n^{(1)}$ | $y_n^{(2)}$ | $\epsilon_n^{(2)}$ |
|---|---|---|---|---|---|---|---|
| 0 | $0^\circ$ | 0.000 | 1.000 | 1.000 | 0.000 | 1.000 | 0.000 |
| 1 | $9^\circ$ | 0.157 | 0.987 | 1.000 | 0.012 | 1.012 | 0.012 |
| 2 | $18^\circ$ | 0.314 | 0.951 | 1.000 | +0.0484 | 1.000 | +0.0484 |
| 3 | $27^\circ$ | 0.453 | 0.891 | 0.915 | +0.024 | 0.925 | +0.034 |
| 4 | $36^\circ$ | 0.628 | 0.809 | 0.901 | +0.0929 | 0.910 | +0.0929 |
| 5 | $45^\circ$ | 0.785 | 0.701 | 0.753 | +0.046 | 0.756 | +0.043 |
| 6 | $54^\circ$ | 0.942 | 0.587 | 0.723 | +0.042 | 0.729 | +0.042 |
| 7 | $63^\circ$ | 1.099 | 0.453 | 0.481 | +0.055 | 0.503 | +0.051 |
| 8 | $72^\circ$ | 1.256 | 0.309 | 0.407 | +0.0981 | 0.417 | +0.1085 |
| 9 | $81^\circ$ | 1.413 | 0.156 | 0.114 | -0.044 | 0.185 | +0.031 |
| 10 | $90^\circ$ | 1.580 | 0.000 | -0.110 | -0.110 | 0.017 | 0.017 |
