# # Invertible Matrices

where \( D_n \) is the same as in Problem 4.14.

# ## 4.16.

The \( n \times n \) matrix \( A_n = (a_{ij}) \), where

\( a_{ij} = \begin{cases} 1, & j - i = 1 \\ 1, & i = j \\ -1, & i - j = 1 \\ 0, & \text{otherwise} \end{cases} \)

is called the _Fibonacci matrix_. Let \( F_n = \det(A_n) \) to show that the _Fibonacci numbers_ \( F_n \) satisfy

+   (i) \( F_n = F_{n-1} + F_{n-2}, \ n = 1, 2, \cdots \) where \( F_{-1} = 0, \ F_0 = 1 \)

+   (ii) \( F_n = \frac{1}{2^{n+1} \sqrt{5}} \left[ (1 + \sqrt{5})^{n+1} - (1 - \sqrt{5})^{n+1} \right] \).

Also, find the inverse of the matrix \( A_n \).

# ## 4.17.

An \( n \times n \) matrix is called _nilpotent_ if \( A^k = 0 \) for some positive integer \( k \). Show that

+   (i) the following matrix is nilpotent

\( A = \begin{pmatrix} 2 & 11 & 3 \\ -2 & -11 & -3 \\ 8 & 35 & 9 \end{pmatrix} \)

+   (ii) every nilpotent matrix is singular

+   (iii) if \( A \) is nilpotent, then \( I - A \) is nonsingular

+   (iv) if the matrices \( A, B \) are nilpotent and \( AB = BA \), then \( AB \) and \( A + B \) are nilpotent.

# ## 4.18.

An \( n \times n \) matrix is called _idempotent_ if \( A^2 = A \). Show that

+   (i) matrices \( I \) and \( 0 \) are idempotent

+   (ii) if \( A \) is idempotent, then \( A^t \) and \( I - A \) are idempotent

+   (iii) every idempotent matrix except \( I \) is singular

+   (iv) if \( A \) is idempotent, then \( 2A - I \) is invertible and is its own inverse

+   (v) if the matrices \( A, B \) are idempotent and \( AB = BA \), then \( AB \) is idempotent.

# ## 4.19.

An \( n \times n \) matrix that results from permuting the rows of an \( n \times n \) identity matrix is called a _permutation matrix_. Thus, each permutation matrix has 1 in each row and each column and all other elements are 0. Show that

+   (i) each permutation matrix \( P \) is nonsingular and orthogonal

+   (ii) product of two permutation matrices is a permutation matrix.