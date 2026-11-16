Wait: J has 3 rows and something like 1000 columns. So \((J^T J)\) is something like \(1000 \times 1000\), a matrix that is computable, but probably not invertible. What we need to do is to manipulate the algebra until we find something involving \((JJ^T)^{-1}\), which is \(3 \times 3\) and not \((JJ^T)^{-1}\). Start with solving Eq. 10.100 for \(\Lambda\). Again, use the pseudoinverse and find

```
\(\Lambda = -(JJ^T)^{-1}J\mathbf{h}\) (10.101)
```

Now, multiply both sides of this equation by \(J^T\):

```
\(-J^T \Lambda = J^T(JJ^T)^{-1}J\mathbf{h}\) (10.102)
```

Observe that from Eq. 10.100, the left-hand side is just \(\mathbf{h}\), and the last two terms on the right-hand side are just \(\mathbf{r}\), and we get our final, computable answer:

```
\(\mathbf{h} = J^T(JJ^T)^{-1}\mathbf{r}\) (10.103)
```

Thus, given a point, \(\theta\) in \(d\) space, we can find the projection of that point onto the manifold of close shapes by

+   1. Compute \(\mathbf{r}\) and \(J\).
+   2. Compute \(\mathbf{h}\).
+   3. Add \(\mathbf{h}\) to \(\theta\).
+   4. Iterate. Yes, iterate. This derivation started out using first order Taylor series, so it only gets us close to the solution. This projection algorithm normally converges to a useful solution in just 2 or 3 iterations.

Now we have a method that will take us from a point in \(d\)-space to a point on the manifold, but that isn’t what we wanted. We wanted the geodesic between the two points.

# 10.7.6 Finding a Geodesic

A geodesic between two points on a surface is a path on the surface that is of minimum length. On the plane, geodesics are unique, however on other surfaces, they may not be unique. For example, on the earth, there is an infinite number of minimum length paths from the north pole to the south. Interestingly, every geodesic on the surface of a sphere is part of a circle (called a *great circle*) whose center is at the center of the earth.

If we can find a set of points that go from the first point to the second, remaining on the manifold, and we have a way to minimize the length of that path, we have a geodesic\(^{12}\). That is, the geodesic is the shortest curve on the manifold.

Assume we have two points, \(\theta\) and \(\theta_f\) (initial and final), both of which are known to lie on the manifold, and we seek the geodesic between them.

Begin by defining an operator \(P(\theta)\) that projects \(\theta\) onto the manifold of closed shapes. This is the projection operator we just derived.

+   1. Using Eq. 10.87, find \(n\) equally spaced points, \(\mathbf{d}\), along the Euclidean line between \(\theta\) and \(\theta_f\), including \(\theta\) and \(\theta_f\), as illustrated in Figure 10.25, and name these points \(\mathbf{d}_1 - \mathbf{d}_n\).

12 The authors are grateful to Lyle Noakes for his help in deriving this formulation.