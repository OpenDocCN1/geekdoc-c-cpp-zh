Given some eigenvalue \(\lambda\), which satisfies Eq. 3.26, the corresponding \(\mathbf{x}\) is called the corresponding *eigenvector*.<sup>7</sup>

# 3.2.8 Eigendecomposition

If a positive semidefinite matrix, \(A\), is also symmetric, then it may be written as \(A = BB^T\) for some matrix \(B\). Many of the matrices encountered in Computer Vision are positive semidefinite. In particular, covariance matrices, which we will encounter several times, have this property.

Assuming we know how to compute eigenvalues and eigenvectors, a positive semidefinite matrix can be written as

\(A = E \Lambda E^T,\) (3.27)

where \(E\) is a matrix in which each column is an eigenvector of \(A\), and \(\Lambda\) is a square, diagonal matrix with corresponding eigenvalues on the diagonal. Should \(A\) not be positive semidefinite and symmetric, but still invertible, the form simply changes to

\(A = E \Lambda E^{-1},\) (3.28)

We can find the null space easily by taking the eigendecomposition and considering all the eigenvectors that correspond to eigenvalues of zero. As an example, using the same matrix as we used in Eq. 3.7 earlier (which is *not* symmetric), we find

\(A = \begin{bmatrix} 4 & 5 & 6 \\ 1 & 2 & 3 \\ 2 & 4 & 6 \end{bmatrix} = \begin{bmatrix} 0.7560 & 0.9469 & 0.4082 \\ 0.2927 & -0.1438 & -0.8165 \\ 0.5855 & -0.2877 & 0.4082 \end{bmatrix} \times \begin{bmatrix} 10.5826 & 0 & 0 \\ 0 & 1.4174 & 0 \\ 0 & 0 & -0.0000 \end{bmatrix} \begin{bmatrix} 0.3727 & 0.6398 & 0.9069 \\ 0.7585 & -0.0884 & -0.9353 \\ 0.0000 & -0.9798 & 0.4899 \end{bmatrix}.\)

Observe that the right column of \(E\) (the left-hand matrix) is the eigenvector corresponding to the zero eigenvalue, and it is precisely the null space we found in the example in section 3.2.3. Also note that because \(A\) is not symmetric, we had to use \(E^{-1}\) for the third matrix in the product.

In this example, if we had two zero eigenvalues, the two corresponding eigenvectors would be a basis for the space of elements of the null space. That is, any vector that is a linear sum of those two vectors would be in the null space.

But of course, this only works for square matrices!

In the next section, we generalize this concept and develop *singular value decomposition*, or SVD.

<sup>7</sup> For any given matrix, there are only a few eigenvalue/eigenvector pairs.