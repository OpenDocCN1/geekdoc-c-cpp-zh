
$(y_b^{(1)} - y_b)(y_b^{(2)} - y_b) > 0 \Rightarrow y'_a \notin [y'_a^{(1)}, y'_a^{(2)}]$, (12.77)

$(y_b^{(1)} - y_b)(y_b^{(2)} - y_b) \le 0 \Rightarrow y'_a \in [y'_a^{(1)}, y'_a^{(2)}]$. (12.78)

In a separation and root-refining strategy such as the ones discussed in Chapter 6, in the first case, one would drop the current interval and pass to a new trial interval $[y'_a^{(1)}, y'_a^{(2)}]$. In the second case, one would iteratively refine the derivative, and, implicitly, the solution, by bisecting the trial interval $[y'_a^{(1)}, y'_a^{(2)}]$, until the target interval $[y'_b^{(1)}, y'_b^{(2)}]$ bracketing the true end value $y_b$ would decrease below a predefined tolerance.

The routine `Shoot` coded along these lines (see Listing 12.14) receives the entire `x`-mesh via vector `x`, along with the boundary values `ya` and `yb`, the limits `dy1` and `dy2` of the search interval for the first derivative, and the tolerance `eps`, within which the found solution is expected to meet the boundary value `yb`. For the repeated propagations from `x[1]` to `x[nx]` implied by the shooting algorithm, `Shoot` calls the auxiliary function `Propag`, which is a simple generic propagator based on the Euler–Cromer method.

`Shoot` initially performs two complete propagations for the input derivatives, `dy1` and `dy2`, and compares the corresponding solution deviations, `f1` and `f2`, from the desired boundary value `yb`. If `f1` and `f2` have the same sign, the interval between `dy1` and `dy2` certainly does not contain the sought initial derivative and the routine returns a fake `dy` and the flag `exist` set to 0. On the contrary, if the two trial solutions deviate on different sides of `yb` (`f1` and `f2` have opposite signs), the routine initiates the iterative refinement of the interval between `dy1` and `dy2` by bisection (see Section 6.2). At each halving step, `Shoot` starts the propagation with the previous average derivative, and retains, as bounding initial derivatives, those leading to final deviations of opposite signs and, which, obviously, continue to bracket the exact derivative. The ability to bracket the exact derivative, doubled by its algorithmic robustness and simplicity, are precisely the beneficial features that recommend the bisection method.

For illustration of the shooting method, we consider in the following the calculation of the Legendre polynomials, $P_n(x)$, from their differential equation. The corresponding two-point boundary-value problem, complying with the commonly used standardization $P_n(1) = 1$, can be written as

$d^2P_n/dx^2 = 1/(1 - x^2) [ 2x dP_n/dx - n(n+1)P_n ]$, (12.79)

$P_n(-1) = (-1)^n,   P_n(1) = 1$. (12.80)

We make explicit use of the well-defined parity of the Legendre polynomials and, taking into account their alternatively symmetric and antisymmetric character (determined by the independence of the ODE on the sign of x), the integration domain can be reduced from $[-1,1]$ to $[0,1]$. In this context, the derivative at the origin, $P'_n(0)$, which may be useful for comparison with numerical results, can be shown to satisfy the simple relation:

$P'_n(0) = n P_{n-1}(0)$.

## Listing 12.14 ODE Solver Based on the Shooting Method (Python Coding)

```
#================================================================================
def Propag(x, y, nx, y0, dy0, Func):
#--------------------------------------------------------------------------------
# Propagates the solution y[] of a Cauchy-problem for a 2nd order ODE on a
# regular mesh x[] with nx points, starting from y0 and dy0.
# Calls: EulerCromer1(x, hx, y, dy, Func); Func(x, y, dy) - RHS of ODE
#--------------------------------------------------------------------------------

hx = x[2] - x[1]
y[1] = y0; dy = dy0
for m in range(1,nx):
    (y[m+1], dy) = EulerCromer1(x[m],hx,y[m],dy,Func)

#================================================================================
def Shoot(x, y, nx, ya, yb, dy1, dy2, eps, Func):
#--------------------------------------------------------------------------------
# Solves a two-point boundary-value problem for a 2nd order ODE
#     y'' = f(x,y,y'), y(xa) = ya, y(xb) = yb
# on a regular mesh x[] with nx points, using the shooting method with trial
# initial derivatives dy in [dy1,dy2]. Returns the solution y[] satisfying
# the condition y(xb) = yb within tolerance eps, the used derivative dy, and
# an existence flag.
# Calls: Propag(x, y, nx, y0, dy0, Func); Func(x, y, dy) - RHS of ODE
#--------------------------------------------------------------------------------

    itmax = 100                         # max. number of bisections

    Propag(x,y,nx,ya,dy1,Func)          # propagate y for dy1
    f1 = y[nx] - yb                     # deviation at xb
    Propag(x,y,nx,ya,dy2,Func)          # propagate y for dy2
    f2 = y[nx] - yb                     # deviation at xb

    if (f1*f2 < 0):                     # check if dy exists in [dy1,dy2]
        exist = 1
        for it in range(1,itmax+1):     # refine dy by bisection
            dy = 0.5e0*(dy1 + dy2)      # new approximation
            Propag(x,y,nx,ya,dy,Func)   # propagate y
            f = y[nx] - yb              # deviation at xb
            if (f1*f > 0): dy1 = dy     # new semi interval
            else:         dy2 = dy
            if (fabs(f) <= eps): break  # deviation vanishes at xb ?

        if (it >= itmax): print("Shoot: max. no. of bisections exceeded !")
    else:
        dy = 1e10; exist = 0

    return (dy, exist)
```

Hence, detailing the initial conditions to be used at `x = 0` for even and, respectively, odd solutions, the Legendre polynomials can be regarded as solutions of the Cauchy problem:

```
y'' = 1/(1 - x²) [2x y' - n(n + 1) y],   (12.81)

y(0) = y_a,    y'(0) = 0,    n = 0,2,...   (12.82)

y(0) = 0,    y'(0) = y_a',    n = 1,3,...   (12.83)
```

with the additional constraint

$y(1) = 1.$ (12.84)

The homogeneity of the Legendre equation guarantees that any solution multiplied by a constant remains a solution, too. Correspondingly, for even $n$, the procedure amounts to the straightforward propagation from an arbitrary initial value $\tilde{y}(0) = y_a$, which is finalized by rescaling the found solution, $\tilde{y}(x)$, with the end value $\tilde{y}(1)$, that is, $y(x) = \tilde{y}(x)/\tilde{y}(1)$. In such a manner, the unused boundary condition, $y(1) = 1$, is clearly satisfied. As for the odd $n$-solutions, they require the actual application of the shooting method, which implies the determination of the correct initial derivative $y'_a$ by iterative bisections of the interval $(-\infty, +\infty)$.

A program designed to calculate the Legendre polynomials by the shooting method is presented in Listing 12.15. In particular, for $n = 5$, an integration step size $h = 10^{-4}$, and a relative tolerance $\varepsilon = 10^{-4}$

## Listing 12.15 Legendre Polynomials by the Shooting Method (Python Coding)
