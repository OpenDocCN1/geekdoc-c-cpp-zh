The subsequent *backward substitution* operates based on the relations:

```
$$\begin{cases}
 x_{nj}=b_{nj}^{(n)}, & j=1,\ldots,m,\\
 x_{kj}=b_{kj}^{(k)}-\displaystyle\sum_{i=k+1}^{n}a_{ki}^{(k)}x_{ij}, & j=1,\ldots,m,\quad k=n-1,\ldots,1.
\end{cases} \tag{7.22}$$
```

and yields the components of the solution matrix **X** column wise (for each of the $m$ simultaneous systems), in reversed order.

Taking into account that the entire relevant information on the final matrix $A^{(n)}$ is contained at the end of the elimination phase exclusively in the upper triangle above the main diagonal, at the elimination step $k$, the elements $a_{kj}^{(k)}$ of the pivot row and, respectively, $a_{ij}^{(k)}$ of the nonpivot rows underneath do not need to be explicitly evaluated on column $j=k$, since they amount by definition to 1 or 0 and they are not reused anyway. This implies that one has to operate in matrix $A^{(k)}$ only on columns $j=k+1,\ldots,n$. As for the backward substitution, in implementing Relations 7.22, one can use a single array for storing both the constant terms $b_{kj}$ and the components $x_{kj}$ of the solution.

Algorithms capable of solving matrix equations corresponding to an arbitrary number of simultaneous linear systems open the possibility of treating a problem of great practical importance—inversion of square matrices. Indeed, considering as matrix of constant terms the unit matrix,

```
$$B=E_n=[\delta_{ij}]_{nn},$$
```

the solution of the system **A · X = B** is precisely the inverse of the coefficient matrix, that is, $X=A^{-1}$. This is, obviously, the nonspecific way in which any algorithm for solving matrix equations can be used to invert matrices.

Of a special interest, not the least for the sake of comparisons with other solvers for linear matrix equations, is the number of floating point operations (flops) required by the Gaussian elimination. By analyzing Equations 7.20 through 7.22, one gets the following operation counts:

+   - Transformation of the coefficient matrix A into upper triangular form:
+     - Summations and subtractions (Equation 7.21):

```
$$S_A(n)=\sum_{k=1}^{n}\sum_{j=k+1}^{n}\sum_{i=k+1}^{n}1=\frac{1}{3}n^3-\frac{1}{2}n^2+\frac{1}{6}n,$$
```

+     - Multiplications and divisions (Equations 7.20 and 7.21):

```
$$M_A(n)=\sum_{k=1}^{n}\sum_{j=k+1}^{n}1+\sum_{k=1}^{n}\sum_{j=k+1}^{n}\sum_{i=k+1}^{n}1=\frac{1}{3}n^3-\frac{1}{3}n.$$
```