# 28.14. Basis Functions in the Mesh

(0 ≤ q < 10).

+   10n_n + 2|(k,l)| + q ~ t
+   10n_n + 2|(k,m)| + q ~ t
+   10n_n + 2|(k,n)| + q ~ t
+   10n_n + 2|(l,m)| + q ~ t
+   10n_n + 2|(l,n)| + q ~ t
+   10n_n + 2|(m,n)| + q ~ t

(0 ≤ q < 2), and

+   10n_n + 2n_e + |(k,l,m)| ~ t
+   10n_n + 2n_e + |(k,l,n)| ~ t
+   10n_n + 2n_e + |(k,m,n)| ~ t
+   10n_n + 2n_e + |(l,m,n)| ~ t

We are now ready to define the required basis functions in the mesh, namely, piecewise polynomial functions for which the degrees of freedom in the mesh vanish, except for only one degree of freedom, whose value is 1. Indeed, for each fixed 0 ≤ i ≤ N, the basis function φ_i is defined in M in such a way that its only nonzero degree of freedom in the mesh is the i th one:

```
φ_i ≡ { h_{i,t} if i ~ t,
0 if i ∤ t
(for every t ∈ M).
```

Thus, every function f that (a) is continuous in M, (b) is a polynomial of degree five in each individual tetrahedron t ∈ M, (c) has a continuous gradient across the edges and side midpoints in M, and (d) has a continuous Hessian at the nodes in M can be written uniquely as a linear combination of the basis functions in the mesh:

```
f = \sum_{i=0}^{N-1} f^{(i)} φ_i ,
```

where f^{(i)} is the i th degree of freedom of f (the value of the corresponding partial derivative of f at the corresponding node, edge midpoint, or side midpoint) in the mesh. Indeed, in each particular tetrahedron t ∈ M, both the left-hand side and the right-hand side of the above equation have the same 56 degrees of freedom, so they must be identical to each other in t. Since this is true for every t ∈ M, they must be identical throughout the entire mesh M as well.

Below we use the basis functions φ_i (0 ≤ i < N) to assemble the N × N stiffness matrix.