# Non-Linear Differential Equations and Dynamical Systems

Using the binomial expansion (4.518) for the two terms on the r.h.s. of (4.529):

```
$$(1\pm ih)^n = \sum_{k=0}^n \frac{n}{k}(\pm ih)^k, \quad (4.529)$
```

yields by addition:

```
$$y_n = \sum_{k=0}^{n/2} \frac{n}{2k}(\pm ih)^{2k} = \sum_{k=0}^{n/2} \frac{n!(-)^k}{(2k)!(n-2k)}h^{2k}, \quad (4.530)$
```

involving powers of h. It has been shown that the solutions (problem 158) of the linear differential (4.522a) [finite difference (4.522b)] equations of second-order with constant coefficients are related (4.522a) [(4.525c)] by the discretization (4.512b) with step h; the corresponding initial conditions (4.531b, c) [(4.526c, d)] lead to the exact (4.523d) [approximate (4.528) (4.530)] solutions, that are compared next (note 4.11).

# NOTE 4.11: Comparison of the Exact and Approximate Solutions

The exact solution (4.523d) of the differential equation (4.522a) with boundary-conditions (4.523b, c) is given by (4.531b) at the points (4.531a) separated by her step h:

```
$$x_n = nh; \quad \cos(x_n) = \cos(nh) = \sum_{k=0}^\infty \frac{(-)^k}{(2k)!}(nh)^{2k}, \quad (4.531a-c)$
```

where the power series for the cosine (II.714a, b) = (4.531c) was used. Comparison of the exact (4.531a) [approximate (4.530)] solutions shows the substitution of coefficients (4.532a) [(4.532b):

```
$$n^{2k} \quad \leftrightarrow \quad \frac{n!}{(n-2k)!} = n(n-1)...(n-2k+1). \quad (4.532, b)$
```

The approximate solution (4.530) may be taken to order ($h^4$) in (4.533a) [(4.534a):

```
$$y_n^{(1)} = 1 - \frac{n(n-1)}{2}h^2 + \epsilon_n^{(1)}, \quad \epsilon_n^{(1)} - O(h^4), \quad (4.533a, b)$
```

```
$$y_n^{(2)} = y_n^{(1)} + \frac{n(n-1)(n-2)(n-3)}{24}h^4 + \epsilon_n^{(2)}, \quad \epsilon_n^{(1)} - O(h^6), \quad (4.534a, b)$
```