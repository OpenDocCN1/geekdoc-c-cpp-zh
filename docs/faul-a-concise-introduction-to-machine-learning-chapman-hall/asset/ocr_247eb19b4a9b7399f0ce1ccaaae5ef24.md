![](bbox=[0.28, 0.1, 0.72, 0.3])

Figure 2.30: Parallelepiped spanned by the vectors a1, a2 and a3, which are the columns of a 3 x 3 matrix A.

where |·| in this case denotes the modulus of the determinant of the Jacobian matrix Jg^-1(y) of g^-1 evaluated at y. In general, if f(x) is a function from R^b to R^a, then the Jacobian matrix Jf(x) is the a x b matrix containing the partial derivatives of all components,

```
J_f(\mathbf{x}) = \begin{pmatrix} \frac{\partial f_1}{\partial x_1}(\mathbf{x}) & \dots & \frac{\partial f_1}{\partial x_b}(\mathbf{x}) \\ \vdots & \ddots & \vdots \\ \frac{\partial f_a}{\partial x_1}(\mathbf{x}) & \dots & \frac{\partial f_a}{\partial x_b}(\mathbf{x}) \end{pmatrix}.
```

If a = b, the determinant of this matrix is called the Jacobian determinant. Confusingly, both, matrix and determinant, are often just referred to as the Jacobian. The matrix can be calculated for any a and b, while the determinant is only defined for a = b.

The modulus of the Jacobian determinant gives the factor by which volumes under the transformation by f shrink or expand. To visualize, the image of the unit cube in three dimensions under a 3 x 3 matrix A is the parallelepiped spanned by the columns of A. For example let

```
\mathbf{a}_1 = \begin{pmatrix} 1 \\ 1/2 \\ 0 \end{pmatrix}, \mathbf{a}_2 = \begin{pmatrix} 0 \\ 1 \\ -1/2 \end{pmatrix}, \mathbf{a}_3 = \begin{pmatrix} 1/2 \\ 0 \\ 1 \end{pmatrix}
```

be the columns of A as seen in Figure 2.30. The volume of this parallelepiped is the modulus of the determinant of A, which is also the scalar triple product (a1 x a2)^T a3 = 7/8.

We can now deduce the multivariate change-of-variable technique. If g : R^K -> R^K is an invertible and differentiable function, and x in R^K is a random variable with probability density function f_X(x), then y = g(x) in R^K is also a random variable and its probability density function is

```
f_Y(\mathbf{y}) = f_X(\mathbf{g}^{-1}(\mathbf{y})) |J_{\mathbf{g}^{-1}}(\mathbf{y})|.
```