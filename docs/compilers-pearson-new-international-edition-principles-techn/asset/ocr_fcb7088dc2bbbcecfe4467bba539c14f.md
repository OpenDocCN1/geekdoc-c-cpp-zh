| Access | Affine Expression | Rank | Nullity | Basis of Null Space |
|---|---|---|---|---|
| X[i-1] | $\begin{bmatrix}1 & 0\\0 & 1\end{bmatrix}\begin{bmatrix}i\\j\end{bmatrix}+\begin{bmatrix}-1\\0\end{bmatrix}$ | 1 | 1 | $\begin{bmatrix}0\\1\end{bmatrix}$ |
| Y[i,j] | $\begin{bmatrix}1 & 0\\0 & 1\end{bmatrix}\begin{bmatrix}i\\j\end{bmatrix}+\begin{bmatrix}0\\0\end{bmatrix}$ | 2 | 0 | |
| Y[j,j+1] | $\begin{bmatrix}0 & 1\\0 & 1\end{bmatrix}\begin{bmatrix}i\\j\end{bmatrix}+\begin{bmatrix}0\\1\end{bmatrix}$ | 1 | 1 | $\begin{bmatrix}1\\0\end{bmatrix}$ |
| Y[1,2] | $\begin{bmatrix}0 & 0\\0 & 0\end{bmatrix}\begin{bmatrix}i\\j\end{bmatrix}+\begin{bmatrix}1\\2\end{bmatrix}$ | 0 | 2 | $\begin{bmatrix}1\\0\end{bmatrix}, \begin{bmatrix}0\\1\end{bmatrix}$ |
| Z[1,i,2*i+j] | $\begin{bmatrix}0 & 0\\1 & 0\\2 & 1\end{bmatrix}\begin{bmatrix}i\\j\end{bmatrix}+\begin{bmatrix}1\\0\\0\end{bmatrix}$ | 2 | 0 | |

Figure 11.19: Rank and nullity of affine accesses

contiguous in C and $X[i,j]$ and $X[i+1,j]$ are contiguous in Fortran. Without loss of generality, in the rest of the chapter, we shall adopt the C (row-major) array layout.

As a first approximation, we consider two array elements to share the same cache line if and only if they share the same row in a two-dimensional array. More generally, in an array of $d$ dimensions, we take array elements to share a cache line if they differ only in the last dimension. Since for a typical array and cache, many array elements can fit in one cache line, there is significant speedup to be had by accessing an entire row in order, even though, strictly speaking, we occasionally have to wait to load a new cache line.

The trick to discovering and taking advantage of self-spatial reuse is to drop the last row from the coefficient matrix $F$. If the resulting *truncated* matrix has rank that is less than the depth of the loop nest, then we can assure spatial locality by making sure that the innermost loop varies only the last coordinate of the array.

**Example 11.25:** Consider the last access, $Z[i,i,2*i+j]$, in Fig. 11.19. If we