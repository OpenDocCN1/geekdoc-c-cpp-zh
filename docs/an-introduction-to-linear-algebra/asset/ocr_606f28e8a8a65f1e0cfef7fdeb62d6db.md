with diagonal elements $(\lambda_1,\ldots,\lambda_n)$, then $A^m$ is also a diagonal matrix with diagonal elements $(\lambda_1^m,\ldots,\lambda_n^m)$. Moreover, if $A$ is an upper (lower) triangular matrix, then $A^m$ is also an upper (lower) triangular matrix. Polynomials in the matrix $A$ are also defined. In fact, if $P_{m-1}(x)=\sum_{i=0}^{m-1}a_i x^i\in(P_m,F)$, then $P_{m-1}(A)=\sum_{i=0}^{m-1}a_iA^i$. Clearly, $P_{m-1}(A)$ is a square matrix. If $P_{m-1}(A)$ is the zero matrix, then $A$ is called a zero or root of $P_{m-1}(x)$.

The transpose of an $m\times n$ matrix $A=(a_{ij})$, written as $A^t$, is an $n\times m$ matrix that is obtained by interchanging the rows and columns of $A$, i.e., $A^t=(a_{ji})$. Thus for the matrices in Example 2.1,

![](bbox=[0.246, 0.294, 0.747, 0.352])

It follows that for the column vector

![](bbox=[0.424, 0.386, 0.563, 0.449])

$a^t$ is the row vector $a^t=(a_1,\ldots,a_n)$, and vice-versa.

For the transpose of matrices, the following hold:

+   1. $(A+B)^t=A^t+B^t$
+   2. $(cA)^t=cA^t$, where $c$ is a scalar
+   3. $(A^t)^t=A$
+   4. $(AB)^t=B^tA^t$ (note reversed order).

Clearly, a square matrix $A$ is symmetric if and only if $A=A^t$ and skew-symmetric if and only if $A=-A^t$. If $A$ is symmetric (skew-symmetric), then obviously $A^t$ is symmetric (skew-symmetric).

The trace of a square matrix, written as $\operatorname{tr}(A)$, is the sum of the diagonal elements, i.e., $\operatorname{tr}(A)=a_{11}+a_{22}+\cdots+a_{nn}$. Thus for the matrix $A$ in (2.1) the trace is $1+3+5=9$. For the trace of square matrices, the following hold:

+   1. $\operatorname{tr}(A+B)=\operatorname{tr}(A)+\operatorname{tr}(B)$
+   2. $\operatorname{tr}(A)=\operatorname{tr}(A^t)$
+   3. $\operatorname{tr}(cA)=c\operatorname{tr}(A)$, where $c$ is a scalar
+   4. $\operatorname{tr}(AB)=\operatorname{tr}(BA)$.

Finally, we remark that, especially for computational purposes, a matrix $A$ can be partitioned into submatrices called blocks, or cells by drawing horizontal and vertical lines between its rows and columns. This partition is not unique;