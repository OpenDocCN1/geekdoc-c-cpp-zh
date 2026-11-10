# ## 13.2 Dense Matrices

# ### 13.2.1 Solving Linear Systems

**Methods to Avoid.** Using Cramer's formula should (almost) always be avoided. A recurrence reasoning shows that computing the determinant of an n × n matrix using Cramer's formula requires on the order of n! multiplications and additions. To solve a system of size n, we have to compute n + 1 determinants. Consider n = 20:

```
```sage
sage: n = 20; cost = (n+1)*factorial(n); cost
51090942171709440000
```
```

we obtain the huge value of 51 090 942 171 709 440 000 multiplications. Assuming our computer performs 3 · 10^9 multiplications per second, let us find how long the computation would last:

```
```sage
sage: v = 3*10^9
sage: print("%.3f" % float(cost/v/3600/24/365))
540.028
```
```

The computation would thus require about 540 years! Of course, we can use Cramer's formula to solve a 2 × 2 system, but not much beyond! All methods used in practice have in common a polynomial cost in the dimension, i.e., of order n^p, with p small (p = 3 in general).

**Practical Methods.** The solution of linear systems Ax = b is in most cases based on a factorisation of the matrix A into a product of two matrices A = M1 M2, where M1 and M2 correspond to “easy” linear systems. To solve Ax = b, we thus first solve M1y = b, then M2x = y.

For example M1 and M2 can be triangular matrices; in this case, once the factorisation is performed, we have to solve two triangular linear systems. The factorisation is much more expensive than solving the triangular linear systems (for example O(n^3) for the LU factorisation against O(n^2) for the triangular linear systems). When several systems with the same matrix have to be solved, we should therefore perform the matrix decomposition only once. Of course, we *never* invert a matrix to solve a linear system, since the inversion requires the matrix factorisation, followed by solving n systems instead of only one.

# ### 13.2.2 Direct Resolution

The simplest way to solve a linear system is illustrated by

```
```sage
sage: A = matrix(RDF, [[-1,2],[3,4]])
sage: b = vector(RDF, [2,3])
sage: x = A\b; x
(-0.200000000000018, 0.900000000000001)
```
```

Within Sage, matrices have a method `solve_right` to solve linear systems (which is based on the *LU* decomposition); this method is used above. We could also write: