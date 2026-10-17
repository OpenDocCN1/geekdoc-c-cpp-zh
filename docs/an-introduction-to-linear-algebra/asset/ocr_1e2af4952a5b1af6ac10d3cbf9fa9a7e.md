# Theorem 5.4.

If B is row equivalent to a matrix A, then there exists a nonsingular matrix C such that B = CA and C⁻¹B = A.

From the above considerations the following results are immediate.

# Theorem 5.5.

Suppose A = (aᵢⱼ) and B = (bᵢⱼ) are row equivalent echelon matrices with pivots a₁ⱼ₁, ⋯, aᵣⱼᵣ, and b₁ₖ₁, ⋯, bₛₖₛ, respectively. Then, r = s and jᵢ = kᵢ, i = 1, ⋯, r, i.e., A and B have the same number of nonzero rows and the pivot elements are in the same position.

# Theorem 5.6.

Every matrix A is row equivalent to an echelon matrix. This matrix is called the echelon form of A. However, the echelon form of a matrix A is not unique.

An m × n matrix A is said to be in row canonical form if it is an echelon matrix, each pivot element is equal to 1, and each pivot is the only nonzero element in its column.

# Example 5.2.

Matrices 0 and I are in row canonical form. The matrix A in Example 5.1 is not in row canonical form, whereas the following matrix is in row canonical form

A = ( 0 1 7 0 5 0 0 9 0 0 0 1 3 0 0 1 0 0 0 0 0 0 1 0 5 0 0 0 0 0 0 0 1 8 0 0 0 0 0 0 0 0 ) .

# Theorem 5.7.

Every matrix A is row equivalent to a unique matrix in row canonical form. This unique matrix is called row canonical form of A.

Two linear systems of m equations in n unknowns are said to be equivalent if they have the same solution(s). It is clear that an elementary row operation on the augmented matrix (A|b) is equivalent to applying the corresponding operation on the linear system (5.2) itself. Further, the new linear system obtained after applying an elementary row operation on (5.2) is equivalent to the linear system (5.2). Thus, the linear system corresponding to the matrix obtained after applying a finite sequence of row operations on the augmented matrix (A|b) is equivalent to the linear system (5.2). In fact, we have the following result.

# Theorem 5.8.

The linear system corresponding to the echelon form (row canonical form) known as echelon linear system (row canonical linear system) of the augmented matrix (A|b) is equivalent to the linear system (5.2).

# Theorem 5.9.

The linear system (5.2) has a solution if and only if the echelon form (row canonical form) of the augmented matrix (A|b) does not have a row of the form (0, ⋯ , 0, d), d ≠ 0.