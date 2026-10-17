# # Theorem 5.10.

For the linear system corresponding to the echelon form (row canonical form) of the augmented matrix \((A|b)\), the following hold:

+   1. If \(r = n\), then the linear system has a unique solution.

+   2. If \(r < n\), then the linear system has an infinite number of solutions. Further, these solutions can be obtained in terms of \((n - r)\) unknowns \(\{x_1, \cdots, x_n\} \setminus \{x_{j_1}, \cdots, x_{j_r}\}\).

# # Theorem 5.11.

If \(m = n\), the system (5.2) has a unique solution if and only if \(A^{-1}\) exists. Further, this solution can be written as \(x = A^{-1}b\).

# # Proof.

If (5.2) with \(m = n\) has a unique solution, then in view of Theorem 5.10(1) the row canonical form of \(A\) is \(I\), and hence from Theorem 5.4 there exists a nonsingular matrix \(C\) such that \(I = CA\). This implies that \(A^{-1}\) exists. Conversely, if \(A^{-1}\) exists, then \(A(A^{-1}b) = (AA^{-1})b = b\), i.e., \(A^{-1}b\) is a solution. To show its uniqueness, let \(Au = b\), then \(u = (A^{-1}A)u = A^{-1}(Au) = A^{-1}b\).

# # Corollary 5.1.

If \(m = n\), the homogeneous system (5.3) has only the trivial solution if and only if \(\det(A) \neq 0\). Further, if (5.3) has only the trivial solution, the nonhomogeneous system (5.2) has a unique solution.

# # Corollary 5.2.

The homogeneous system (5.3) with more unknowns than equations has a nonzero solution.

The \(rank\) of a matrix \(A\), written as \(rank(A)\), is equal to the number of pivots \(r\) in an echelon form of \(A\); equivalently, \(A\) has at least one non-zero minor of order \(r\), and every minor of order larger than \(r\) vanishes. From Theorems 5.10 and 5.11, and the fact that an echelon form of the augmented matrix \((A|b)\) automatically yields an echelon form of \(A\), the following result follows.

# # Theorem 5.12.

+   1. The system (5.2) has a solution if and only if \(rank(A) = rank(A|b)\).

+   2. The system (5.2) with \(m = n\) has a unique solution if and only if \(rank(A) = rank(A|b) = n\).

The following example shows how row operations can be used to reduce a matrix to an echelon (row canonical) form.

# # Example 5.3.

Successively, we have

\(A = \begin{pmatrix} 1 & -2 & 3 & 1 \\ 1 & -1 & 4 & 3 \\ 2 & 5 & 7 & 4 \end{pmatrix} \begin{matrix} \\ \\ R_3 - R_1 \\ R_3 - 2R_1 \end{matrix} \sim \begin{pmatrix} 1 & -2 & 3 & 1 \\ 0 & 1 & 1 & 2 \\ 0 & 9 & 1 & 2 \end{pmatrix} \begin{matrix} \\ \\ R_3 - 9R_2 \end{matrix}\)

\(\sim \begin{pmatrix} 1 & -2 & 3 & 1 \\ 0 & 1 & 1 & 2 \\ 0 & 0 & -8 & -16 \end{pmatrix} \begin{matrix} \\ \\ R_3 / (-8) \end{matrix}\) (echelon form)