which allows us to easily eliminate $D$ from the picture. Now the problem is to minimize

$\mathscr{F}_s(A, B, C) = \sum_{i=1}^{n} [A(z_i - \bar{z}) + Bx_i + Cy_i]^2$ (5.52)

subject to the constraint

$4\bar{z}A^2 + B^2 + C^2 = 1.$ (5.53)

It is further convenient to introduce a new parameter, $A_0 = 2\bar{z}^{1/2}A$. Now we minimize

$\mathscr{F}_s(A_0, B, C) = \sum_{i=1}^{n} \left[ A_0\frac{z_i - \bar{z}}{2\bar{z}^{1/2}} + Bx_i + Cy_i \right]^2$ (5.54)

subject to

$A_0^2 + B^2 + C^2 = 1.$ (5.55)

**Reduction to eigenvalue problem.** Again we employ methods of linear algebra. The function (5.54) can be written in matrix form as

$\mathscr{F}_s = \| \mathbf{X}_0 \mathbf{A}_0 \|^2 = \mathbf{A}_0^T (\mathbf{X}_0^T \mathbf{X}_0) \mathbf{A}_0,$ (5.56)

where $\mathbf{A}_0 = (A_0, B, C)^T$ is the reduced and modified vector of parameters and

$\mathbf{X}_0 = \begin{bmatrix} (z_1 - \bar{z})/(2\bar{z}^{1/2}) & x_1 & y_1 \\ \vdots & \vdots & \vdots \\ (z_n - \bar{z})/(2\bar{z}^{1/2}) & x_n & y_n \end{bmatrix}$ (5.57)

is the $n \times 3$ modified data matrix. The constraint (5.55) simply means $\| \mathbf{A}_0 \| = 1$, i.e., $\mathbf{A}_0$ must be a unit vector.

The minimum of (5.56) is attained on the unit eigenvector of the matrix $\mathbf{X}_0^T \mathbf{X}_0$ corresponding to its smallest eigenvalue. This matrix is symmetric and positive-semidefinite, thus all its eigenvalues are real and nonnegative. Furthermore, this matrix is nonsingular, i.e., it is positive-definite, unless the data points lie of a circle or a line (i.e., admit a perfect fit).

**SVD-based Taubin fit.** Practically, one can evaluate $\mathbf{A}_0$ as follows. The simplest option is to call a matrix algebra function that returns all the eigenpairs of $\mathbf{X}_0^T \mathbf{X}_0$ and select the eigenvector corresponding to the smallest eigenvalue.

Alternatively, the eigenvectors of $\mathbf{X}_0^T \mathbf{X}_0$ can be found by singular value decomposition (SVD), as they coincide with the right singular vectors of $\mathbf{X}_0$. Accordingly, one can compute the (short) SVD of the matrix $\mathbf{X}_0$, i.e., $\mathbf{X}_0 = \mathbf{U}\boldsymbol{\Sigma}\mathbf{V}^T$, and then $\mathbf{A}_0$ will be the third (last) column of $\mathbf{V}$. This procedure bypasses the evaluation of the matrix $\mathbf{X}_0^T \mathbf{X}_0$ altogether and makes computations more stable numerically.

We call this algorithm **SVD-based Taubin fit**.