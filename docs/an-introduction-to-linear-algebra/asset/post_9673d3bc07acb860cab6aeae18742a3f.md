
## 21.4.

Show that the following system has no solution:

\[
\begin{pmatrix}
1&2&1&5\\
1&2&-1&1\\
2&4&-3&0
\end{pmatrix}
\begin{pmatrix}
x_1\\x_2\\x_3\\x_4
\end{pmatrix}
=
\begin{pmatrix}
1\\1\\3
\end{pmatrix}.
\]

Find its least-squares solution.

## 21.5.

Show that the following system has no solution:

\[
\begin{pmatrix}
2&1&3\\
4&3&5\\
8&2&16\\
-4&1&-11\\
-2&3&-5
\end{pmatrix}
\begin{pmatrix}
x_1\\x_2\\x_3
\end{pmatrix}
=
\begin{pmatrix}
1\\2\\4\\2\\2
\end{pmatrix}.
\]

Find its least-squares solution.

## Answers or Hints

- 21.1. \(\left(\frac{1}{3},\frac{2}{3},1\right)^t\)

- 21.2. \(\left(2,\frac{13}{55},0\right)^t+\left(-5,\frac{48}{55},\frac{147}{55},1\right)^t c\).

- 21.3. \((0,1,1,0)^t+\left(-\frac{13}{30},\frac{9}{10},\frac{16}{15},1,0\right)^t c+\left(\frac{1}{30},\frac{7}{10},\frac{8}{15},0,1\right)^t d\).

- 21.4. That the solution does not exist follows from the echelon form of the augmented matrix
  \[
  \begin{pmatrix}
  1&2&1&5&|&1\\
  0&0&-2&-4&|&0\\
  0&0&0&0&|&1
  \end{pmatrix}.
  \]
  Its least-squares solution is
  \[
  \frac{1}{15}(17,0,-3,0)^t+(-2,1,0,0)^t c+(-3,0,-2,1)^t d.
  \]

- 21.5. That the solution does not exist follows from the echelon form of the augmented matrix
  \[
  \begin{pmatrix}
  2&1&3&|&1\\
  0&1&-1&|&0\\
  0&0&2&|&0\\
  0&0&0&|&4\\
  0&0&0&|&3
  \end{pmatrix}.
  \]
  Its least-squares solution is
  \[
  \frac{1}{956}(491,680,-173)^t.
  \]

## Chapter 22

## Quadratic Forms

Quadratic forms occur naturally in physics, economics, engineering (control theory), and analytic geometry (quadratic curves and surfaces). Particularly, recall that the equation (quadratic form) of a central quadratic curve in a plane, after translating the origin of the rectangular coordinate system to the centre of the curve, appears as

\[
q_2(x,y)=(x,y)
\begin{pmatrix}
a&b\\
b&c
\end{pmatrix}
\binom{x}{y}
=ax^2+2bxy+cy^2=d.
\]

We also know that by rotating the axes (using a proper transformation) this equation (quadratic form) in a new coordinate system can be reduced to a “canonical” (diagonal) form:

\[
q_2(x',y')=(x',y')
\begin{pmatrix}
a'&0\\
0&c'
\end{pmatrix}
\binom{x'}{y'}
=a'x'^2+c'y'^2=d.
\]

In this chapter we shall study quadratic forms in \(n\) variables \(x_1,\cdots,x_n\), i.e.,

\[
q_n(x_1,\cdots,x_n)=\sum_{i=1}^{n}b_i x_i^2+2\sum_{i<j}^{n}c_{ij}x_i x_j,\quad b_i,c_{ij}\in R.
\tag{22.1}
\]

Clearly, in (22.1) each term is of degree two.

In matrix form, (22.1) can be written as

\[
q_n(x)=q_n(x_1,\cdots,x_n)=x^tAx,
\tag{22.2}
\]

where \(A=(a_{ij})\) is an \(n\times n\) symmetric matrix with \(a_{ii}=b_i\), \(a_{ij}=a_{ji}=c_{ij}\). In (22.2), if we let \(x=Py\), a linear transformation of the variables, then it follows that

\[
q_n(y)=(Py)^tA(Py)=y^t(P^tAP)y,
\tag{22.3}
\]

i.e., \(P^tAP\) provides the matrix representation of \(q_n\) in the new variables. Now since \(A\) is symmetric, in view of Theorem 18.2, we can always find an orthonormal matrix \(Q\) and the diagonal matrix \(D\) consisting of the eigenvalues of \(A\) such that \(D=Q^{-1}AQ=Q^tAQ\). Thus, with the proper choice of the matrix \(P\), (22.3) in the new variables can be reduced to a diagonal form,

\[
q_n(y)=y^tDy.
\tag{22.4}
\]

We summarize our above discussion in the following result.

## Theorem 22.1

If \(A\) is a symmetric matrix, then there exists an orthonormal matrix \(Q\) such that the transformation \(y=Q^tx\) changes the quadratic form (22.2) into the diagonal quadratic form (22.4).

## Example 22.1

Consider the quadratic form

\[
q_3(x_1,x_2,x_3)=11x_1^2+11x_2^2+14x_3^2-2x_1x_2-8x_1x_3-8x_2x_3,
\tag{22.5}
\]

which in matrix form is the same as \(q_3(x)=x^tAx\), where the symmetric matrix \(A\) is as in (18.1). From Example 18.4 it is clear that (22.5) can be reduced to a diagonal form,

\[
q_3(y_1,y_2,y_3)
=(y_1,y_2,y_3)
\begin{pmatrix}
6&0&0\\
0&12&0\\
0&0&18
\end{pmatrix}
\begin{pmatrix}
y_1\\y_2\\y_3
\end{pmatrix}
=6y_1^2+12y_2^2+18y_3^2.
\]

Here, in view of Remark 18.3, the new variable vector \(y\) is

\[
y=Q^tx=
\begin{pmatrix}
\frac{1}{\sqrt{3}}&\frac{1}{\sqrt{3}}&\frac{1}{\sqrt{3}}\\
-\frac{1}{\sqrt{2}}&\frac{1}{\sqrt{2}}&0\\
-\frac{1}{\sqrt{6}}&-\frac{1}{\sqrt{6}}&\frac{2}{\sqrt{6}}
\end{pmatrix}
\begin{pmatrix}
x_1\\x_2\\x_3
\end{pmatrix}
=
\begin{pmatrix}
\frac{1}{\sqrt{3}}(x_1+x_2+x_3)\\
\frac{1}{\sqrt{2}}(-x_1+x_2)\\
\frac{1}{\sqrt{6}}(-x_1-x_2+2x_3)
\end{pmatrix}.
\]

## Example 22.2

Consider the quadratic form

\[
q_4(x_1,x_2,x_3,x_4)
=x_1^2+\frac{5}{3}x_2^2-\frac{5}{6}x_3^2-\frac{5}{6}x_4^2
+2x_1x_2+2x_1x_3+2x_1x_4
-\frac{8}{3}x_2x_3-\frac{8}{3}x_2x_4+\frac{7}{3}x_3x_4,
\tag{22.6}
\]

which in matrix form is the same as \(q_4(x)=x^tAx\), where the symmetric matrix \(A\) is as in Example 18.5. From this example, it is clear that (22.6) can be reduced to a diagonal form.

Here the new variable vector \(y\) is

\[
y=Q^tx=
\begin{pmatrix}
\frac{1}{\sqrt{12}}(3x_1+x_2+x_3+x_4)\\
\frac{1}{\sqrt{6}}(-2x_2+x_3+x_4)\\
\frac{1}{\sqrt{6}}(-x_1+x_2+2x_3)\\
\frac{1}{\sqrt{12}}(-x_1+x_2-x_3+3x_4)
\end{pmatrix}.
\]

Now we classify the quadratic form (22.2) according as its values: The quadratic form \(q_n(x)\) is called *positive definite* if \(q_n(x)>0\), \(x\in R^n/\{0\}\), and *positive semidefinite* if \(q_n(x)\ge 0\), \(x\in R^n\). The quadratic form \(q_n(x)\) is called *negative definite* if \(q_n(x)<0\), \(x\in R^n/\{0\}\), and *negative semidefinite* if \(q_n(x)\leq 0\), \(x\in R^n\). The quadratic form \(q_n(x)\) is called *indefinite* if it is both positive and negative for \(x\in R^n\).

## Theorem 22.2

If \(A\) is a symmetric matrix, then the quadratic form \(q_n(x)=x^tAx\) is positive definite if \(A\) has only positive eigenvalues, negative definite if \(A\) has only negative eigenvalues, and indefinite if \(A\) has both positive and negative eigenvalues.

## Proof

If \(\lambda_1,\cdots,\lambda_n\) are the eigenvalues of \(A\), then from (22.4) it follows that

\[
q_n(y)=\lambda_1y_1^2+\cdots+\lambda_ny_n^2,
\]

where \(y=Q^{-1}x=Q^tx\). Thus, if all eigenvalues of \(A\) are positive, then from the fact that \(y=0\) implies \(x=0\) (one-to-one correspondence between \(y\) and \(x\)), we find \(q_n(x)>0\) for all \(x\in R^n/\{0\}\), i.e., \(q_n(x)\) is positive definite. If \(\lambda_k\leq 0\), we can select \(y=e^k\), then \(q_n(y)=\lambda_k\leq 0\), i.e., \(q_n(x)\) is not positive definite. The other cases can be discussed similarly.

## Example 22.3

In view of *Theorem 22.2* the quadratic form (22.5) is positive definite, whereas (22.6) is indefinite. From *Example 18.1*, it is clear that the quadratic form

\[
q_3(x_1,x_2,x_3)
=-11x_1^2-11x_2^2-14x_3^2+2x_1x_2+8x_1x_3+8x_2x_3
\]

is negative definite (the eigenvalues of the corresponding matrix are \(-6,-12,-18\)).

The rest of the results in this chapter find maximum and minimum of the quadratic form \(q_n(x)\) subject to some constraints, and so belong to a broad field known as *constrained optimization*.

## Lemma 22.1

For the quadratic form \(q_n(x)=\sum_{i=1}^n b_i x_i^2\) subject to the constraint \(\|x\|_2=1\), the following hold:

- (i) The maximum value is \(b_k=\max\{b_1,\cdots,b_n\}\) and is attained at \(x=e^k\).
- (ii) The minimum value is \(b_\ell=\min\{b_1,\cdots,b_n\}\) and is attained at \(x=e^\ell\).

## Proof

Clearly,

\[
q_n(x)=\sum_{i=1}^n b_ix_i^2\leq b_k\sum_{i=1}^n x_i^2=b_k.
\]

Further, at \(x=e^k\), \(q_n(e^k)=b_k\).

## Theorem 22.3

Let the symmetric matrix \(A\) in (22.2) have the eigenvalues \(\lambda_1\leq\cdots\leq\lambda_n\), and \(x^1,\cdots,x^n\) be the corresponding eigenvectors. Then, for the quadratic form \(q_n(x)=x^tAx\) subject to the constraint \(\|x\|_2=1\), the following hold:

- (i) The maximum value is \(\lambda_n\) and is attained at \(x=x^n/\|x^n\|_2\).
- (ii) The minimum value is \(\lambda_1\) and is attained at \(x=x^1/\|x^1\|_2\).

## Proof

From Theorem 22.1 it follows that the transformation \(x=Qy\) reduces (22.2) to the diagonal form (22.7); here, \(Q\) consists of vectors that are obtained by orthonormalizing the eigenvectors \(x^1,\cdots,x^n\). Now since \(y=Q^tx\) and the matrix \(Q\) is orthonormal, we have

\[
\|y\|_2^2=\|Q^tx\|_2^2=(Q^tx,Q^tx)=(Q^tx)^t(Q^tx)=x^tQQ^tx=x^tx=(x,x)=\|x\|_2^2.
\]

Thus, \(\|y\|_2=1\) if and only if \(\|x\|_2=1\), and hence \(x^tAx\) and \(y^tDy\) assume the same set of values as \(x\) and \(y\) range over the set of all unit vectors. Now since in view of Lemma 22.1 the maximum (minimum) value of \(q_n(y)\) is attained at \(e^n\) (\(e^1\)), for \(q_n(x)\) the maximum (minimum) value is attained at \(x=Qe^n\) (\(Qe^1\)) \(=x^n/\|x^n\|_2\) (\(x^1/\|x^1\|_2\)).

## Example 22.4

From Example 22.1 and Theorem 22.3, it follows that

\[
6\leq 11x_1^2+11x_2^2+14x_3^2-2x_1x_2-8x_1x_3-8x_2x_3\leq18
\]

provided \(x_1^2+x_2^2+x_3^2=1\). The left equality holds for \(x=\left(\frac{1}{\sqrt{3}},\frac{1}{\sqrt{3}},\frac{1}{\sqrt{3}}\right)^t\), and the right equality holds for \(x=\left(-\frac{1}{\sqrt{6}},-\frac{1}{\sqrt{6}},\frac{2}{\sqrt{6}}\right)^t\).

## Example 22.5

From Example 22.2 and Theorem 22.3, it follows that

\[
-2\leq
\left\{
\begin{aligned}
&x_1^2+\frac{5}{3}x_2^2-\frac{5}{6}x_3^2-\frac{5}{6}x_4^2+2x_1x_2+2x_1x_3\\
&\quad+2x_1x_4-\frac{8}{3}x_2x_3-\frac{8}{3}x_2x_4+\frac{7}{3}x_3x_4
\end{aligned}
\right\}
\leq3
\]

provided \(x_1^2+x_2^2+x_3^2+x_4^2=1\). From Example 18.5 it follows that the left equality holds for

\[
x=\left(-\frac{1}{\sqrt{6}},-\frac{1}{\sqrt{6}},\frac{1}{\sqrt{6}},0\right),
\quad
\left(-\frac{1}{\sqrt{12}},\frac{1}{\sqrt{12}},-\frac{3}{\sqrt{12}},\frac{3}{\sqrt{12}}\right),
\quad
\left(0,0,-\frac{1}{\sqrt{2}},\frac{1}{\sqrt{2}}\right).
\]

The right-hand equality holds at

\[
\left(0,-\frac{2}{\sqrt{6}},\frac{1}{\sqrt{6}},\frac{1}{\sqrt{6}}\right).
\]

## Remark 22.1

By letting \(x_i=a_iz_i\), \(1\leq i\leq n\), we can transform the optimization problem \(q_n(x)=x^tAx\) subject to \(\sum_{i=1}^n x_i^2/a_i^2=1\) into

\[
q_n(z)=(a_1z_1,\cdots,a_nz_n)A(a_1z_1,\cdots,a_nz_n)^t
\]

subject to \(\|z\|_2=1\), for which Theorem 22.3 is applicable. In particular, if \(a_i=a\), \(1\leq i\leq n\), then it simply reduces to \(q_n(z)=a^2q_n(x)\) subject to \(\|x\|_2=1\).

## Example 22.6

From Remark 22.1 and Example 22.4, it follows that

\[
24\leq11x_1^2+11x_2^2+14x_3^2-2x_1x_2-8x_1x_3-8x_2x_3\leq72
\]

provided \(x_1^2+x_2^2+x_3^2=4\). The left equality holds for

\[
x=\left(\frac{2}{\sqrt{3}},\frac{2}{\sqrt{3}},\frac{2}{\sqrt{3}}\right)^t,
\]

and the right equality holds for

\[
x=\left(-\frac{2}{\sqrt{6}},-\frac{2}{\sqrt{6}},\frac{4}{\sqrt{6}}\right)^t.
\]

Finally, in this chapter we shall prove the following result.
