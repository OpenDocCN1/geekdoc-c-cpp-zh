```
// step 4: apply input matrix and add
w[0] += input[k] * c[0];
// etc ...
// step 5: inserted later
// step 6: write signal into delay lines
line[0][0] write[0] ] = w[0];
// etc ...
// step 7: bump cursors
read[0] = ( read[0] + 1 ) & mask[0];
write[0] = ( write[0] + 1 ) & mask[0];
// etc ...
}
}
```

# Choosing the Right Feedback Matrices

This section gets a little bit mathematical. In Smith's insightful online book [SmithOnline], he discusses special classes of feedback matrices, which are unitary ($A^T = A^{-1}$), or more generally, lossless. A lossless feedback matrix does not change signal energy as it circulates through the feedback loop. An FDN with such a matrix is either called a lossless prototype [Smith96] or a reverber filter [Jot91]. One advantage of lossless matrices is that with some of them, a matrix-vector multiply can be optimized to $O(n)$ time, instead of the usual $O(n^2)$.

An $n \times n$ feedback matrix $A_n$ is lossless, if and only if it has N linearly independent eigenvectors and its eigenvalues are of unit magnitude. All orthogonal rotation matrices, with and without reflection, can be used as lossless feedback matrices. The "density" of the matrix, which is how many nonzero elements it contains, determines the richness of the cross-coupling and therefore the speed of echo build-up.

A particularly attractive class of matrices is the Householder reflection, which is orthogonal and contains no zero elements. Assume $U_n$ is an $n \times n$ matrix with each element set to one, and $I_n$ is an $n \times n$ identity matrix, then
$A_n = I_n - U_n,$

A Householder reflection is especially nice in the 4 x 4 case, because all elements are of the same magnitude. A matrix-vector multiply can be implemented as one swizzled vector addition and three swizzled vector subtractions:

$$A_4 = \frac{1}{2} \left[ \begin{matrix} 1 & -1 & -1 & -1 \\ -1 & 1 & -1 & -1 \\ -1 & -1 & 1 & -1 \\ -1 & -1 & -1 & 1 \end{matrix} \right]$$