# 14.2 The Inertia Tensor

In a given coordinate system, every rigid body has three moments of inertia (one for each of the coordinate axes) and three products of inertia. These six quantities form what is called the inertia tensor for the rigid body. The inertia tensor is ordinarily expressed as a 3x3 matrix, but it is symmetric, so there are only six distinct entries. For a set of particles, the inertia tensor I is given by the formula

```
(14.7) \(\mathbf{I} = \sum_k m_k \begin{bmatrix} y_k^2 + z_k^2 & -x_k y_k & -x_k z_k \\ -x_k y_k & x_k^2 + z_k^2 & -y_k z_k \\ -x_k z_k & -y_k z_k & x_k^2 + y_k^2 \end{bmatrix},\)
```

where the k-th particle has mass m_k and is located at the point (x_k,y_k,z_k) [1]. This formula can also be expressed as

```
(14.8) \(\mathbf{I} = \sum_k m_k \left( r_k^2 \mathbf{E}_3 - \mathbf{r}_k \otimes \mathbf{r}_k \right),\)
```

where E_3 is the 3x3 identity matrix, r_k=(x_k,y_k,z_k), and the operation \otimes is the tensor product giving

```
(14.9) \(\mathbf{r}_k \otimes \mathbf{r}_k = \begin{bmatrix} x_k^2 & x_k y_k & x_k z_k \\ x_k y_k & y_k^2 & y_k z_k \\ x_k z_k & y_k z_k & z_k^2 \end{bmatrix}.\)
```

The diagonal entries of the inertia tensor are the moments of inertia, and the off-diagonal entries are the products of inertia. It is always possible to find a coordinate system in which the products of inertia are all zero, and we call the axes of such a coordinate system the principal axes of inertia for a rigid body. In this gem, we