![](bbox=[0.19, 0.11, 0.73, 0.3])

Figure 3.1 x1 and x2 are orthonormal bases. The projection of y onto x1 has length a1.

This matrix is skew-symmetric. That is, it is equal to the negative of its transpose. The cross product between two vectors x and y can then be defined as

```
x \times y = [x]_\times y = \begin{bmatrix} 0 & -x_3 & x_2 \\ x_3 & 0 & -x_1 \\ -x_2 & x_1 & 0 \end{bmatrix} \begin{bmatrix} y_1 \\ y_2 \\ y_3 \end{bmatrix} = \begin{bmatrix} x_2 y_3 - x_3 y_2 \\ x_3 y_1 - x_1 y_3 \\ x_1 y_2 - x_2 y_1 \end{bmatrix}. \quad (3.2)
```

Note that if x = y, their cross product is the zero vector:

```
x \times y = \mathbf{0}. \quad (3.3)
```

The advantage of describing this operation as a matrix is that you can perform the cross product operation (which is only defined for vectors) using matrix multiplication. Thus x x M = [x]_x M takes the cross product of x with each column of M.

# Linear Independence

Suppose we have n vectors x1, x2, ..., xn; if we can write v = a1x1 + a2x2 + ... + anxn, where a1, a2, ..., an ∈ R, then v is said to be a linear combination of x1, x2, ..., xn.

A set of vectors x1, ..., xn is said to be linearly independent if it is impossible to write any of the vectors as a linear combination of the others.

Given d linearly independent vectors, of d dimensions, x1, x2, ..., xd defined on R^d, then any vector y in the space may be written as y = a1x1 + a2x2 + ... + adxd.

Since any d-dimensional real-valued vector y may be written as a linear combination of x1, x2, ..., xd, the set {xi, i = 1, ..., d} is called a basis set and the vectors are said to span the space, R^d. Any linearly independent set of vectors can be used as a basis (necessary and sufficient). It is often particularly convenient to choose basis sets which are orthonormal.

For example, the following two vectors form a basis for R^2:

```
x_1 = [0 \quad 1]^T \quad \text{and} \quad x_2 = [1 \quad 0]^T.
```

This is the familiar Cartesian coordinate system. Here's another basis set for R^2:

```
x_1 = [1 \quad 1]^T \quad \text{and} \quad x_2 = [-1 \quad 1]^T.
```

1 Is this set orthonormal?