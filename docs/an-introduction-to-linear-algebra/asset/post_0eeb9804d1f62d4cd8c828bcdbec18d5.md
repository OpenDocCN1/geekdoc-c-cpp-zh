
Combining Remark 7.1 with Theorem 23.4, we have the following result.

## Theorem 23.5.

If all principal minors \(\det(A^k)\), \(k=1,\cdots,n\), of a symmetric matrix \(A\) are positive, then \(A\) can be uniquely factored as \(A=LDL^t\), where \(L\) is a lower triangular matrix with all diagonal elements \(1\), and \(D\) is a diagonal matrix with all positive elements.

### Proof.

In view of Remark 7.1 and Theorem 23.4, the factorization \(A=LD\hat{U}\) is unique, where the diagonal matrix \(D\) has only positive elements. Now since \(A\) is symmetric, we have

\[
LD\hat{U}=A=A^t=\hat{U}^tD^tL^t=\hat{U}^tDL^t,
\]

which immediately implies that \(\hat{U}=L^t\). \(\blacksquare\)

## Remark 23.2.

We denote the diagonal elements of \(D\) as \(0<d_{ii}\), \(i=1,\cdots,n\), and define the diagonal matrix \(D^{1/2}\) with elements \(0<\sqrt{d_{ii}}\), \(i=1,\cdots,n\). Then, the above factorization can be written as

\[
A=LDL^t=(LD^{1/2})(D^{1/2}L^t)=(LD^{1/2})(LD^{1/2})^t=L_cL_c^t,
\]

where \(L_c=LD^{1/2}\). The factorization \(A=L_cL_c^t\) is called *Cholesky decomposition*. Now let us denote by \(L_{k-1}\) the \((k-1)\times(k-1)\) upper left corner of \(L_c\), \(a_k\) the first \(k-1\) entries in column \(k\) of \(A\), \(\ell_k\) the first \(k-1\) entries in column \(k\) of \(L_c^t\), and \(a_{kk}\) and \(\ell_{kk}\) the \(kk\) entries of \(A\) and \(L_c\), respectively. Then, the Cholesky algorithm is:

\[
\begin{aligned}
L_1&=\sqrt{a_{11}}=\ell_{11}\\
L_{k-1}\ell_k&=a_k,\quad\text{compute }\ell_k\\
\ell_{kk}&=\sqrt{a_{kk}-\ell_k^t\ell_k}\\
L_k&=\begin{pmatrix} L_{k-1} & 0 \\ \ell_k^t & \ell_{kk} \end{pmatrix},\quad k=2,\cdots,n.
\end{aligned}
\]

## Example 23.3.

Using the Cholesky algorithm for the matrix \(A\) in (18.1), we successively have

\[
\ell_{11}=\sqrt{11},\quad \ell_{21}=-\frac{1}{\sqrt{11}},\quad \ell_{22}=\sqrt{\frac{120}{11}},
\]
\[
\ell_{31}=-\frac{4}{\sqrt{11}},\quad \ell_{32}=-\sqrt{\frac{96}{55}},\quad \ell_{33}=\sqrt{\frac{54}{5}}.
\]

Thus, the Cholesky decomposition of the matrix \(A\) in (18.1) is

\[
\begin{pmatrix}
\sqrt{11} & 0 & 0 \\
-\frac{1}{\sqrt{11}} & \sqrt{\frac{120}{11}} & 0 \\
-\frac{4}{\sqrt{11}} & -\sqrt{\frac{96}{55}} & \sqrt{\frac{54}{5}}
\end{pmatrix}
\begin{pmatrix}
\sqrt{11} & -\frac{1}{\sqrt{11}} & -\frac{4}{\sqrt{11}} \\
0 & \sqrt{\frac{120}{11}} & -\sqrt{\frac{96}{55}} \\
0 & 0 & \sqrt{\frac{54}{5}}
\end{pmatrix}.
\]

We are now in the position to prove the main result of this chapter.

## Theorem 23.6 (Sylvester’s criterion).

A symmetric matrix \(A\) is positive definite if and only if all principal minors \(\det(A^k)\), \(k=1,\cdots,n\), are positive.

### Proof.

If \(A\) is positive definite, then all principal minors are positive, as follows from Theorems 23.2 and 23.3. Conversely, the matrix \(A\) has the Cholesky decomposition, i.e., \(A=L_cL_c^t\). Since \(\det(A)>0\), the matrix \(L_c^t\) must be non-singular, and hence \(L_c^tx\neq 0\) for all \(x\neq 0\). From this, we find

\[
x^tAx=x^tL_cL_c^tx=(L_c^tx)^t(L_c^tx)=\|L_c^tx\|^2>0.
\]

Hence, the matrix \(A\) is positive definite.

## Example 23.4.

For the matrix \(A\) in (18.1), we have \(\det(A^1)=11>0\), \(\det(A^2)=120>0\), \(\det(A^3)=1296>0\); thus in view of Theorem 23.6, the matrix \(A\) is positive definite. This in turn implies that the quadratic form in (22.5) is positive definite.

Finally, in this chapter we shall prove the following result.

## Theorem 23.7 (polar decomposition).

Let the \(n\times n\) matrix \(A\) have rank \(r\). Then, \(A\) can be factored as \(A=PQ\), where \(P\) is a symmetric \(n\times n\) positive semidefinite matrix of rank \(r\), and \(Q\) is an \(n\times n\) orthogonal matrix. If \(r=n\), then the matrix \(P\) is positive definite.

### Proof.

We rewrite the singular value decomposition (19.1) as

\[
A=U\Sigma V^t=U\Sigma U^tUV^t=(U\Sigma U^t)(UV^t)=PQ. \tag{23.1}
\]

In (23.1), the matrix \(Q=UV^t\) is the product of two orthogonal matrices, and hence in view of Problem 4.7, is orthogonal. The matrix \(P=U\Sigma U^t\) is symmetric, also orthogonally similar to \(\Sigma\), and hence in view of P12 (in Chapter 16) \(P\) has the same rank and eigenvalues as \(\Sigma\). This implies that \(P\) is positive semidefinite. Clearly, if \(r=n\) then all diagonal elements of \(\Sigma\) are positive, and thus \(P\) is positive definite. \(\blacksquare\)

## Example 23.5.

For the matrix in Problem 16.2(ii), the singular value decomposition is \(U\Sigma V^t\), where

\[
U=\begin{pmatrix}
-0.0886 & -0.7979 & -0.5963 \\
0.3080 & -0.5912 & 0.7454 \\
-0.9472 & -0.1176 & 0.2981
\end{pmatrix},
\quad
\Sigma=\begin{pmatrix}
23.7448 & 0.0000 & 0.0000 \\
0.0000 & 2.6801 & 0.0000 \\
0.0000 & 0.0000 & 0.0000
\end{pmatrix},
\]
\[
V^t=\begin{pmatrix}
-0.7014 & 0.6762 & 0.2254 \\
-0.7128 & -0.6654 & -0.2218 \\
0.0000 & 0.3162 & -0.9487
\end{pmatrix}
\]

and the polar decomposition is \(PQ\), where

\[
P = U\Sigma U^t = \begin{pmatrix}
1.8927 & 0.6163 & 2.2442 \\
0.6163 & 3.1893 & -6.7409 \\
2.2442 & -6.7409 & 21.3406
\end{pmatrix},
\]
\[
Q = UV^t = \begin{pmatrix}
0.6309 & 0.2825 & 0.7227 \\
0.2054 & 0.8373 & -0.5066 \\
0.7482 & -0.4680 & -0.4702
\end{pmatrix}.
\]

## Problems

- **23.1.** Show that if a symmetric matrix \(A\) is positive definite, then the diagonal elements are positive. Is the converse true?
- **23.2.** Let \(A\) be a symmetric positive definite matrix and \(C\) be a nonsingular matrix. Show that the matrix \(C^tAC\) is also symmetric positive definite.
- **23.3.** Let \(A\) and \(B\) be \(n \times n\) symmetric positive definite matrices. Show that \(A+B\), \(A^2\), \(A^{-1}\) are also symmetric positive definite. In each case, is the converse true? What can we say about the matrices \(BAB\) and \(ABA\)?
- **23.4.** Let \(A\) and \(B\) be \(n \times n\) symmetric positive definite matrices such that \(AB = BA\). Show that \(AB\) is positive definite. Is the converse true?
- **23.5.** Let \(S\) be the set of all \(n \times n\) symmetric positive definite matrices. Is \(S\) a subspace of \(M^{n \times n}\)?
- **23.6.** Let \(A \in R^{n \times n}\) be a symmetric positive definite matrix. Show that for column vectors the function \((u, v) = u^tAv\) is an inner product on \(R^n\).
- **23.7.** The matrix \(C\) in Problem 14.4 is a symmetric positive definite matrix.
- **23.8.** Show that the matrix \(A_n(2)\) given in (4.2) is a symmetric positive definite matrix.
- **23.9.** Use Theorem 23.5 to show that the following symmetric matrices are positive definite: \(A = \begin{pmatrix} 1 & 2 & 3 \\ 2 & 8 & 12 \\ 3 & 12 & 34 \end{pmatrix}, \quad B = \begin{pmatrix} 16 & 4 & 4 & -4 \\ 4 & 10 & 4 & 2 \\ 4 & 4 & 6 & -2 \\ -4 & 2 & -2 & 4 \end{pmatrix}, \quad C = \begin{pmatrix} 2 & 1 & 1 & 2 \\ 1 & 3 & 2 & 1 \\ 1 & 2 & 4 & 3 \\ 2 & 1 & 3 & 5 \end{pmatrix}.\)
- **23.10.** Use Theorem 23.5 to show that the following symmetric matrix is not positive definite: \(D = \begin{pmatrix} 2 & 1 & 1 & 2 & 1 & 2 \\ 1 & 3 & 2 & 1 & 3 & 4 \\ 1 & 2 & 4 & 3 & 1 & 0 \\ 2 & 1 & 3 & 5 & 1 & 2 \\ 1 & 3 & 1 & 1 & 0 & 1 \\ 2 & 4 & 0 & 2 & 1 & 5 \end{pmatrix}.\)
- **23.11.** Find Cholesky decomposition for the symmetric matrices \(A, B,\) and \(C\) given in Problem 23.9.
- **23.12.** For the quadratic form \(q_3(x_1,x_2,x_3)=x_1^2+5x_2^2+2x_3^2+2\alpha x_1x_2+2x_1x_3+6x_2x_3\), find the values of \(\alpha\) so that it is positive definite.

## Answers or Hints

- **23.1.** If \(A\) is positive definite, \((e^k)^tAe^k=a_{kk}>0,\ k=1,\cdots,n.\) The converse is not true; consider the matrix \(\begin{pmatrix} 2 & 5 \\ 5 & 3 \end{pmatrix}.\)
- **23.2.** Let \(y=Cx\neq 0\) for \(x\in R^n\setminus\{0\}.\) Then, we have \(x^tC^tACx=y^tAy>0,\) since \(A\) is positive definite.
- **23.3.** If \(x^tAx>0\) and \(x^tBx>0\) for all \(x\in R^n\setminus\{0\},\) then \(x^t(A+B)x>0,\) and hence \(A+B\) is positive definite. The converse is not true, in fact, matrices \(A=\begin{pmatrix}-1 & 0 \\ 0 & 2\end{pmatrix}\) and \(B=\begin{pmatrix}3 & 0 \\ 0 & -1\end{pmatrix}\) are not positive definite, but \(C=A+B=\begin{pmatrix}2 & 0 \\ 0 & 1\end{pmatrix}\) is positive definite.

  Since \(A\) is positive definite, from Theorem 23.2 it is nonsingular. Now from Problem 23.2 it follows that \(A^2=A^tIA\) is positive definite. The converse is not true. In fact, the matrix \(A=\begin{pmatrix}-1 & 0 \\ 0 & 2\end{pmatrix}\) is not positive definite, but \(A^2=\begin{pmatrix}1 & 0 \\ 0 & 4\end{pmatrix}\) is positive definite.

  Let \(x\in R^n\setminus\{0\}\) and \(y=Ax\neq 0.\) We have \(y^tA^{-1}y=x^tA^tA^{-1}Ax=x^tAx>0.\) The converse follows by replacing \(A\) by \(A^{-1}.\) Since matrices \(A\) and \(B\) are invertible, from Problem 23.2 it follows that matrices \(BAB\) and \(ABA\) are positive definite.
- **23.4.** Since \(AB=BA\) and matrices \(A\) and \(B\) are symmetric, \(AB\) is symmetric. Suppose \(\lambda\) is an eigenvalue of the matrix \(AB\) and \(x\neq 0\) is the corresponding eigenvector. Then, \(ABx=\lambda x\) implies that \(x^tBABx=\lambda x^tBx,\) and hence \(\lambda=x^tBABx/x^tBx>0,\) since \(x^tBx>0\) and \(x^tBABx>0.\) Thus, \(AB\) is positive definite. The converse is not true. For this, note that the matrix \(C=\begin{pmatrix}3 & 0 \\ 0 & 4\end{pmatrix}\) is positive definite, and \(C=AB=BA\) where
