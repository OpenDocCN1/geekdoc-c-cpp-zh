```
```
sage: C = B.echelon_form()
sage: C[3,5]*350
-1139x + 63y + 120z + 350t
```
```

We deduce that $F$ is the hyperplane of $\mathbb{R}^4$ defined by $-1139x + 63y + 120z + 350t = 0$.

It is also possible to get this equation by computing the left kernel of $A$, which gives the coordinates of the linear forms defining $F$ (here, there is only one form):

```
```
sage: K = A.left_kernel(); K
Vector space of degree 4 and dimension 1 over Rational Field
Basis matrix:
[     1  -63/1139 -120/1139 -350/1139]
```
```

A basis of the hyperplane defined by this linear form is given by the following vectors already obtained by A.column_space():

```
```
sage: matrix(K.0).right_kernel()
Vector space of degree 4 and dimension 3 over Rational Field
Basis matrix:
[     1      0      0  1139/350]
[     0      1      0    -9/50]
[     0      0      1   -12/35]
```
```

**Exercise 11 page 37.** (*A matrix equation*) Let us first define the $A$ and $C$ matrices:

```
```
sage: A = matrix(QQ, [[-2, 1, 1], [8, 1, -5], [4, 3, -3]])
sage: C = matrix(QQ, [[1, 2, -1], [2, -1, -1], [-5, 0, 3]])
```
```

As the equation $A = BC$ is linear, the set of solutions is an affine subspace of $\mathcal{M}_3(\mathbb{R})$. We search for a particular solution of our equation.

```
```
sage: B = C.solve_left(A); B
[ 0 -1  0]
[ 2  3  0]
[ 2  1  0]
```
```

Then, we determine the general form of the solutions, that is to say, the left kernel of $C$:

```
```
sage: C.left_kernel()
Vector space of degree 3 and dimension 1 over Rational Field
Basis matrix:
[1 2 1]
```
```

Then, we obtain the general form of the solutions of our equation:

```
```
sage: x, y, z = var('x, y, z'); v = matrix([[1, 2, 1]])
sage: B = B + (x*v).stack(y*v).stack(z*v); B
```
```