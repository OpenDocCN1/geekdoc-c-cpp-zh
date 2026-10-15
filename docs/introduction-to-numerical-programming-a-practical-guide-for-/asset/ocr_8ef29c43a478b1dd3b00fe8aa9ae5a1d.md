Practically, the process of root separation implies determining the signs of the function f(x) at the points of a sufficiently fine partition {x_m}, the choice of which largely depends on the particularities of the function. If the subintervals [x_m, x_{m+1}] are sufficiently small, according to the above theorem, each subinterval contains at most a real root of the equation f(x) = 0. As such, the intervals for which f(x_m)f(x_{m+1}) > 0 do not contain any root, while those for which f(x_m)f(x_{m+1}) ≤ 0 contain a single root.

# 6.2 Bisection Method

Let us consider the equation

```
f(x) = 0,
```

in which the real function f(x) is continuous on the interval [a, b]. We assume that, as a result of a previous root-separation process, Equation 6.2 has at most one root within [a, b]. Denoting this root by ξ, the following cases are possible:

+   a. If f(a) = 0, then the root is ξ = a;
+   b. If f(b) = 0, then the root is ξ = b;
+   c. If f(a)f(b) < 0, then the root is one of the interior points, ξ ∈ (a, b);
+   d. If f(a)f(b) > 0, then there is no root ξ ∈ [a, b].

Considering the occurrence of case (c), which is the only nontrivial one requiring actual computations, with a view to finding the contained root, we divide the interval [a, b] into two equal subintervals by the midpoint x0 = (a + b)/2, as can be seen in Figure 6.3. In particular, if f(x0) = 0, then ξ = x0 is the sought root. In the opposite case, we choose the subinterval [a1, b1] at whose ends the function has opposite signs and which, obviously, continues to confine the root, and we store its boundaries. One of the following cases can come about

```
a1 = a0,  b1 = x0,   if f(a)f(x0) < 0,
a1 = x0,  b1 = b0,   if f(a)f(x0) > 0.
```

![](bbox=[0.28, 0.78, 0.72, 0.94])

FIGURE 6.3 Halving process of the search interval for the bisection method.