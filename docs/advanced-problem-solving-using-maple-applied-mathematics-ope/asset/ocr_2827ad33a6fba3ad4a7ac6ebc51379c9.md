Load the linear algebra package, enter the system’s matrix in augmented form, row reduce the matrix using Gaussian elimination, and then interpret the results:

```
with(LinearAlgebra):
A := <2,1,-1>|<4,3,3>|<4,1,2>|<4,4,-1>;
A :=
\begin{bmatrix}
2 & 4 & 4 & 4\\
1 & 3 & 1 & 4\\
-1 & 3 & 2 & -1
\end{bmatrix}
ReducedRowEchelonForm(A);
\begin{bmatrix}
1 & 0 & 0 & 2\\
0 & 1 & 0 & 1\\
0 & 0 & 1 & -1
\end{bmatrix}
```

We interpret the results as a unique solution: $(x,y,z)=(2,1,-1)$.

Let’s increase the dimension by one.

# **Example 5.2.** A $4 \times 4$ System.

Determine the solution of the following system of linear equations.

$$\begin{aligned}
2x+4y+4z+2w&=2\\
2x+2y+z-w&=-1\\
x+4y-z-2w&=1\\
-x+2y+w&=1
\end{aligned}$$

```
B := Matrix([[2,4,4,2,2],[2,2,1,-1,-1],[1,4,-1,-2,1],[-1,2,0,1,1]]);
B :=
\begin{bmatrix}
2 & 4 & 4 & 2 & 2\\
2 & 2 & 1 & -1 & -1\\
1 & 4 & -1 & -2 & 1\\
-1 & 2 & 0 & 1 & 1
\end{bmatrix}
ReducedRowEchelonForm(B);
\begin{bmatrix}
1 & 0 & 0 & -1 & 0\\
0 & 1 & 0 & 0 & 0\\
0 & 0 & 1 & 1 & 0\\
0 & 0 & 0 & 0 & 1
\end{bmatrix}
```

We interpret the results: The system has no solution as the last row of the row reduced augmented matrix gives the equation $0=1$.