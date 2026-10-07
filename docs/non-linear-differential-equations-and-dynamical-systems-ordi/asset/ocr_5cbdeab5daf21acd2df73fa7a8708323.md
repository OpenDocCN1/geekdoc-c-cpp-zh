# Non-Linear Differential Equations and Dynamical Systems

![](bbox=[0.238, 0.125, 0.74, 0.263])

FIGURE 3.10

The proof of the sufficiency condition for a first-order differential to be equal the Stokes theorem stating that the flux of a continuously differentiable vector across a regular surface $D$ with area element $dS_{nm}$ supported on a closed regular curve or loop $\partial D$ equals the circulation of the vector along the boundary with arc length $ds$ and unit tangent vector $T_n$ and displacement $dx_s$.

# NOTE 3.10: Sufficient Condition for the Existence of an Integrating Factor

With respect to the conditions of integrability (3.282), its necessity was proved by (3.281a, b), for the sufficiency, it will show that if the conditions of integrability are satisfied it is possible to reduce a first-order differential with $N$ variables to one with $N-1$ variables. Applying the procedure leads to a first-order differential in two variables (3.145a, b), that always has an integrating factor. The procedure will be demonstrated by reducing the first-order differential in three variables (3.271) to one in two variables (3.145b). The proof will need the following result: if the vector (3.309a) satisfies the condition of integrability (3.309b) of zero helicity (3.282), so does (3.309e) any parallel vector field (3.309d), where $\mu$ is any continuously differentiable function (3.309c):

```
$X_n \in C^1(R^N): \sum_{m,s}(\partial_s X_n-\partial_n X_m)=0 \quad (3.309a, b)$
```

```
$\mu \in C^1(R^N), \quad Y_n=\mu X_n: \sum_{m,s}(\partial_s Y_n-\partial_n Y_m)=0.\quad (3.309c-e)$
```

This result can be proved directly by substituting (3.309d) in (3.282). Alternatively, if the first-order differential (3.274b) has an integrating factor $\lambda$, then the first-order differential using (3.310a):

```
$X_n=\mu Y_n, \quad df=\lambda\sum_{n=1}^N X_n dx_n=\mu\sum_{n=1}^N Y_n dx_n, \quad (3.310a, b)$
```