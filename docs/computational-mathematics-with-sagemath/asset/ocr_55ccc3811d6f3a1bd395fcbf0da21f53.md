| Most useful commands (dense matrices) | |
| --- | --- |
| Solve a linear system | x = A\b |
| LU decomposition | P, L, U = A. LU() |
| Cholesky decomposition | C = A.cholesky() |
| QR decomposition | Q, R = A.QR() |
| Singular value decomposition | U, Sig, V = A.SVD() |
| Eigenvalues and eigenvectors | Val, Vec = A.eigenmatrix_right() |

TABLE 13.1 – Summary.

```
```python
sage: m = lil_matrix((n2, n2))
sage: for i in range(0,n2):
....:     m[i,i] = 1./A[i,i]
sage: msc = m.tocsc()
sage: from scipy.sparse.linalg import cg
sage: x = cg(A, b, M = msc, tol=1.e-8)
```
```

# ### 13.3.4 Eigenvalues, Eigenvectors

**The Power Method.** The power method is particularly well suited for huge sparse matrices; indeed, to implement the algorithm, it is enough to know how to perform matrix-vector and scalar products. As an example, let us come back to random walks on a sparse graph, and let us compute the stationary distribution using the power method:

```
```python
sage: from scipy import sparse
sage: from numpy.linalg import *
sage: from numpy import array
sage: from numpy.random import rand
sage: def power(A,x):        # power iteration
....:     for i in range(0,1000):
....:         y = A*x
....:         z = y/norm(y)
....:         lam = sum(x*y)
....:         s = norm(x-z)
....:         print("%i s=%s lambda=%s"%(i,s,lam))
....:         if s < 1e-3:
....:             break
....:         x = z
....:     return x
sage: n = 1000
sage: m = 5
sage: # build a stochastic matrix of size n
sage: # with m non-zero coefficients per row
sage: A1 = sparse.lil_matrix((n, n))
```
```