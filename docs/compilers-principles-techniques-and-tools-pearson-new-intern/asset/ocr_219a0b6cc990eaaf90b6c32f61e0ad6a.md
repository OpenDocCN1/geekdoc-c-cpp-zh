# ## 11.4. AFFINE ARRAY INDEXES

| ACCESS | AFFINE EXPRESSION |
|--------|-------------------|
| X[i-1] | $\begin{bmatrix}1 & 0\end{bmatrix}\begin{bmatrix}i \\ j\end{bmatrix} + [-1]$ |
| Y[i,j] | $\begin{bmatrix}1 & 0 \\ 0 & 1\end{bmatrix}\begin{bmatrix}i \\ j\end{bmatrix} + \begin{bmatrix}0 \\ 0\end{bmatrix}$ |
| Y[j,j+1] | $\begin{bmatrix}0 & 1 \\ 0 & 1\end{bmatrix}\begin{bmatrix}i \\ j\end{bmatrix} + \begin{bmatrix}0 \\ 1\end{bmatrix}$ |
| Y[1,2] | $\begin{bmatrix}0 & 0 \\ 0 & 0\end{bmatrix}\begin{bmatrix}i \\ j\end{bmatrix} + \begin{bmatrix}1 \\ 2\end{bmatrix}$ |
| Z[1,i,2*i+j] | $\begin{bmatrix}0 & 0 \\ 1 & 0 \\ 2 & 1\end{bmatrix}\begin{bmatrix}i \\ j\end{bmatrix} + \begin{bmatrix}1 \\ 0 \\ 0\end{bmatrix}$ |

Figure 11.18: Some array accesses and their matrix-vector representations

# ### 11.4.2 Affine and Nonaffine Accesses in Practice

There are certain common data access patterns found in numerical programs that fail to be affine. Programs involving sparse matrices are one important example. One popular representation for sparse matrices is to store only the nonzero elements in a vector, and auxiliary index arrays are used to mark where a row starts and which columns contain nonzeros. Indirect array accesses are used in accessing such data. An access of this type, such as $X[Y[i]]$, is a nonaffine access to the array $X$. If the sparsity is regular, as in banded matrices having nonzeros only around the diagonal, then dense arrays can be used to represent the subregions with nonzero elements. In that case, accesses may be affine.

Another common example of nonaffine accesses is linearized arrays. Programmers sometimes use a linear array to store a logically multidimensional object. One reason why this is the case is that the dimensions of the array may not be known at compile time. An access that would normally look like $Z[i,j]$ would be expressed as $Z[i*n + j]$, which is a quadratic function. We can convert the linear access into a multidimensional access if every access can