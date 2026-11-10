We observe a convergence towards an almost diagonal matrix. The diagonal coefficients are approximations to the eigenvalues of A. Let us check:

```
```
sage: Aref.eigenvalues()
[58.030586202212, 92.91426499150643, 0.03226690899408103,
 4.022909479477674]
```
```

We can prove the convergence if the matrix is Hermitian positive definite. If we have a non-symmetric matrix, we should compute in C, the eigenvalues being a priori complex, and, if the method converges, the lower triangular part of $A_k$ tends to zero, while the diagonal tends to the eigenvalues of $A$.

The $QR$ method requires several improvements to become efficient, in particular because the successive $QR$ decompositions are expensive; among the common refinements, in general we first reduce the matrix $A$ to a simpler form (Hessenberg's form: upper triangular plus the first subdiagonal), which makes the $QR$ decompositions much cheaper; then, to speed-up convergence, we apply cleverly chosen translations $A := A + \sigma I$ (see for example [GVL12]). This is precisely the method used by Sage for dense matrices CDF or RDF.

# **In Practice.**

The above programs are mainly given as pedagogical examples; in practice, we will use the methods provided by Sage, which, whenever possible, call optimised routines from the Lapack library. The interface allows either to get only the eigenvalues, or both the eigenvalues and the corresponding eigenvectors:

```
```
sage: A = matrix(RDF, [[1,3,2],[1,2,3],[0,5,2]])
sage: eigen_vals, eigen_vects = A.eigenmatrix_right()
sage: eigen_vals
[ 6.39294791648918                0.0                0.0]
[                0.0 0.560519476111939                0.0]
[                0.0                0.0 -1.9534673926011215]
sage: eigen_vects
[ 0.542484060110651  0.927684562943908 0.09834254667424457]
[ 0.5544692861094349 0.10329475725336986 -0.617227053099068]
[ 0.6310902116870117 -0.3587917847435306  0.780614827194734]
```
```

This example computes the diagonal matrix with eigenvalues, and the eigenvector matrix (whose columns correspond to eigenvectors).

**EXAMPLE** (Computing the roots of a polynomial). Given a monic polynomial (with real or complex coefficients) $p(x) = x^n + a_{n-1}x^{n-1} + \cdots + a_1x + a_0$, it is easy to check that the eigenvalues of the companion matrix $M$, defined by $M_{i+1, i} = 1$ and $M_{1,n-i} = -a_i$, are the roots of $p$ (see §8.2.3), which thus gives a method to approximate these roots:

```
```
sage: def pol2companion(p):
....:     n = len(p)
....:     m = matrix(RDF, n)
....:     for i in range(1, n):
....:         m[i, i-1] = 1
....:     m.set_column(n-1, -p)
....:     return m
```
```