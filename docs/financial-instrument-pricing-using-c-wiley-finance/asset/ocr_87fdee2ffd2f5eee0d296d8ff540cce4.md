# 21.10 EXERCISES AND PROJECTS

1. (FDM and Domain Transformation)
The boundary conditions for put options are always bounded for both y = 0 and y = 1. And the same conclusion holds for the payoff function (initial condition); it is always bounded. For call options on the other hand, the payoff function becomes:

```
max(S − K, 0) = max( (α y)/(1 − y) − K, 0 ).
```

In this case we see that the payoff is unbounded at y = 1. In such cases we adopt the heuristic approach by offsetting the boundary by a small amount ε (typically 0.001) and then using 1 − ε as the new boundary point.

2. (ADE for the Cox–Ingersoll–Ross Model)
In this exercise we approximate the CIR PDE using the standard implicit difference method (BTCS). Compare the results with the ADE method using domain transformation. In both cases we assume that the Feller condition σ < √2a holds and then no boundary conditions need be prescribed at r = 0.
We take the example of a one-factor zero-coupon bond (see Tavella and Randall, 2000). The initial boundary value problem is given by:

```
{
− ∂B/∂t + 1/2 σ² r ∂²B/∂r² + (a − b r) ∂B/∂r − r B = 0,    0 < r < r_max,    t > 0
B(r_max, t) = 0,    t > 0
− ∂B/∂t (0, t) + a ∂B/∂r (0, t) = 0,    t > 0,    a > 0
B(r, 0) = H(r) (payoff),    0 < r < r_max.
}
```

Please note that we are using forward time. The tricky part is the boundary condition at r = 0; it is a first-order hyperbolic equation. We thus conclude that the bond price B is not known at r = 0. To this end, the implicit Euler scheme is:

```
{
− (B_j^{n+1} − B_j^n)/k + σ_j^{n+1} D_+ D_- B_j^{n+1} + μ_j^{n+1} D_0 B_j^{n+1} − r_j B_j^{n+1} = 0,    1 ≤ j ≤ J − 1
σ ≡ 1/2 σ² r (slight misuse of notation)
μ ≡ a − b r
}
```