(2.61) \( A[\boldsymbol{e}_1 \ \boldsymbol{e}_2 \ \boldsymbol{e}_3] = [\mu_1\boldsymbol{e}_1 \ \mu_2\boldsymbol{e}_2 \ \mu_3\boldsymbol{e}_3] \).

To be more concise, we put equation (2.61) into a compact matrix form,

\( AE = E \begin{bmatrix} \mu_1 & 0 & 0 \\ 0 & \mu_2 & 0 \\ 0 & 0 & \mu_3 \end{bmatrix} = E\mu \) (2.62)

where \(\mu\) is a diagonal matrix and \(E\) is the eigen matrix. If the matrix \(E\) is nonsingular, we diagonalize the matrix \(A\) by premultiplying (2.62) by \(E^{-1}\):

(2.63) \( E^{-1}AE = \mu \).

Therefore, we have used the eigenmatrix \(E\) in a linear transformation to diagonalize the matrix \(A\).

# 2.7.4 Change of Basis

One may view the matrix \(A\) in the previous example as a matrix that defines a linear system

\(\boldsymbol{y} = \begin{bmatrix} y_1 \\ y_2 \\ y_3 \end{bmatrix} = A\boldsymbol{x} = A \begin{bmatrix} x_1 \\ x_2 \\ x_3 \end{bmatrix}.\) (2.64)

The matrix \(A\) is a transformation that maps \(\boldsymbol{x} \in \mathbb{R}^3\) to \(\boldsymbol{y} \in \mathbb{R}^3\). The components of \(\boldsymbol{y}\) are related to that of \(\boldsymbol{x}\) via the