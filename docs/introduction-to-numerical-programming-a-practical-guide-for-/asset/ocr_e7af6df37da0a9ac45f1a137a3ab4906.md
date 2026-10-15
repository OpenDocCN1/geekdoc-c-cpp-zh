results from the first equation using $x_2$ and $x_3$:

$x_3 = 3,$

$x_2 = 13/10 - 11/10x_3 = -2,$

$x_1 = 10/3 - 4/3x_2 - 5/3x_3 = 1.$

Thus, the solution of the considered linear system is

$x_1 = 1,\quad x_2 = -1,\quad x_3 = 3.$

Taking a step forward toward deriving the general algorithm of the Gaussian elimination, we consider now the case of a $3 \times 3$ linear system with symbolic coefficients:

$\begin{cases}
a_{11}x_1+a_{12}x_2+a_{13}x_3=b_1\\
a_{21}x_1+a_{22}x_2+a_{23}x_3=b_2\\
a_{31}x_1+a_{32}x_2+a_{33}x_3=b_3.
\end{cases}$

The matrix form of this system,

$\begin{bmatrix}a_{11}&a_{12}&a_{13}\\a_{21}&a_{22}&a_{23}\\a_{31}&a_{32}&a_{33}\end{bmatrix}\begin{bmatrix}x_1\\x_2\\x_3\end{bmatrix}=\begin{bmatrix}b_1\\b_2\\b_3\end{bmatrix},$

can be cast as matrix equation,

$\mathbf{A}\cdot\mathbf{x}=\mathbf{b},$

where $\mathbf{A}=[a_{ij}]$ is the coefficient matrix, $\mathbf{x}=[x_i]$ is the column vector of the unknowns, and $\mathbf{b}=[b_i]$ is the column vector of the constant terms.

At the first step of the forward elimination (marked by an upper index (1)), we aim to eliminate $x_1$ from all equations, except for the first one. To this end, we start by dividing the first row by the pivot element $a_{11}$, which is assumed to be nonzero:

$\begin{cases}
x_1+a_{12}^{(1)}x_2+a_{13}^{(1)}x_3=b_1^{(1)}\\
a_{21}x_1+a_{22}x_2+a_{23}x_3=b_2\\
a_{31}x_1+a_{32}x_2+a_{33}x_3=b_3.
\end{cases}$

If, on the contrary, $a_{11}$ is zero, the first equation has to be interchanged with another one that has a nonzero leading coefficient. We then subtract the first equation, multiplied by the coefficient $a_{21}$ of $x_1$, from the second equation and, respectively, multiplied by $a_{31}$, from the third equation. Thus, we obtain the transformed system:

$\begin{cases}
x_1+a_{12}^{(1)}x_2+a_{13}^{(1)}x_3=b_1^{(1)}\\
a_{22}^{(1)}x_2+a_{23}^{(1)}x_3=b_2^{(1)}\\
a_{32}^{(1)}x_2+a_{33}^{(1)}x_3=b_3^{(1)}.
\end{cases}$