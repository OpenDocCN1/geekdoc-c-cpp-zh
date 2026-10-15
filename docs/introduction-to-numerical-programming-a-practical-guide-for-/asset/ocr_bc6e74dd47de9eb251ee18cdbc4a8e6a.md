# Theorem 8.1

Two real ($n \times n$) matrices, $\mathbf{A}, \mathbf{A}' \in \mathbf{M}_{\mathbb{R}}^{n \times n}$, are similar if and only if they are connected by a *similarity transformation*,

$$\mathbf{A}' = \mathbf{S}^{-1} \cdot \mathbf{A} \cdot \mathbf{S}, \tag{8.10}$$ 

where $\mathbf{S} \in \mathbf{M}_{\mathbb{R}}^{n \times n}$ is an invertible matrix.

Indeed, assuming that the action of the operator is described relative to a first basis by the matrix $\mathbf{A}$ and with respect to a second basis by another matrix $\mathbf{A}'$, we have

$$\mathbf{y} = \mathbf{A} \cdot \mathbf{x}, \quad \mathbf{y}' = \mathbf{A}' \cdot \mathbf{x}', \tag{8.11}$$ 

where $\mathbf{x}$ and $\mathbf{x}'$, on the one hand, and $\mathbf{y}$ and $\mathbf{y}'$, on the other, are the column matrix representations of the same vectors relative to the first basis and, respectively, to the second one. If $\mathbf{S}$ is the nonsingular matrix performing the basis change, then

$$\mathbf{x} = \mathbf{S} \cdot \mathbf{x}', \quad \mathbf{y} = \mathbf{S} \cdot \mathbf{y}'. \tag{8.12}$$

Plugging Relations 8.12 into the first of Equations 8.11, it follows $\mathbf{y}' = (\mathbf{S}^{-1} \cdot \mathbf{A} \cdot \mathbf{S}) \cdot \mathbf{x}'$, and, by comparing this result with the second of Equations 8.11, one obtains just Equation 8.10, which provides the necessary and sufficient condition for two matrices to be similar.

# Theorem 8.2

Two similar matrices have identical eigenvalues.

Indeed, let $\lambda$ be an eigenvalue of matrix $\mathbf{A}$, and $\mathbf{x}$, the corresponding eigenvector. By performing a basis change with the nonsingular matrix $\mathbf{S}$, we have $\mathbf{x} = \mathbf{S} \cdot \mathbf{x}'$ and the eigenvalue equation may be reformulated as $(\mathbf{S}^{-1} \cdot \mathbf{A} \cdot \mathbf{S}) \cdot \mathbf{x}' = \lambda \mathbf{x}'$, which proves the assertion.

By way of consequence, two similar matrices have identical eigenvalues and the corresponding eigenvectors can be deduced from one another by means of a similarity transformation. Specifically, from the reformulation (8.9) of the modal equation it follows that the matrices $\mathbf{A}$ and $\Lambda$ are similar. Matrices similar with diagonal matrices are termed *diagonalizable*.

The essence of the *diagonalization of matrices* consists in the fact that, provided a transformation matrix can be found which diagonalizes the considered matrix, the sought eigenvalues will reside on the main diagonal of the transformed matrix, while the columns of the transformation matrix (which can be identified with the modal matrix) will represent precisely the corresponding eigenvectors of the original matrix.

# 8.3 Jacobi Method

As mentioned in the introduction to this chapter, the solution of eigenvalue problems for *real symmetric matrices* is of utmost interest in many areas of applied sciences and engineering. Moreover, the effective utilization of the symmetry of the involved matrices leads to the considerable simplification of the developed numerical methods, which thus gain stability, accuracy, and efficiency (both in terms of operation cost and memory usage).

An essential property of the eigenvectors of real symmetric matrices is that they are real and orthogonal. As a consequence, the modal matrix $\mathbf{X}$ having them as columns is orthogonal and, implicitly, the diagonalization of a real symmetric matrix can be accomplished by means of an *orthogonal*