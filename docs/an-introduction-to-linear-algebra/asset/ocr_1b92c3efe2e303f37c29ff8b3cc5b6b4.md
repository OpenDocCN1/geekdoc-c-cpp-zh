and (24.3) it follows that

\(A^+=\left(\begin{array}{ c c }
\frac{2}{3} & \frac{1}{\sqrt{3}} \\
\frac{2}{3} & -\frac{1}{\sqrt{3}} \\
\frac{1}{3} & 0 \\
0 & \frac{1}{\sqrt{3}}
\end{array}\right)\left(\begin{array}{ c c }
\frac{1}{3} & 0 \\
0 & \frac{1}{\sqrt{3}}
\end{array}\right)\left(\begin{array}{ c c }
1 & 0 \\
0 & 1
\end{array}\right).\)

A formal definition of Moore–Penrose inverse is as follows:

# ## Definition 24.1.

For a given \(m \times n\) matrix \(A\) the \(n \times m\) matrix \(A^+\) is called Moore–Penrose inverse if the following hold:

\((a) AA^+A = A, (b) A^+AA^+ = A^+, (c) (AA^+)^t = AA^+, (d) (A^+A)^t = A^+A.\)

(24.4)

From elementary calculations it follows that \(A^+\) given in (24.3) satisfies all the four equations (24.4), and hence every matrix \(A\) has a Moore–Penrose inverse \(A^+\). In fact, the equations in (24.4) determine \(A^+\) uniquely. For this, let \(B^+\) also be a Moore–Penrose inverse of \(A\), i.e.,

\((\tilde{a}) AB^+A = A, (\tilde{b}) B^+AB^+ = B^+, (\tilde{c}) (AB^+)^t = AB^+, (\tilde{d}) (B^+A)^t = B^+A.\)

(24.5)

Now from the eight equations in (24.4) and (24.5), we have

\(\begin{array}{ c c c }
A^+ & =^{(b)} & A^+AA^+ =^{(d)} A^t(A^+)^tA^+ =^{(\tilde{a})} A^t(B^+)^tA^t(A^+)^tA^+ \\
 & =^{(\tilde{d})} & B^+AA^t(A^+)^tA^+ =^{(d)} B^+AA^+AA^+ =^{(a)} B^+AA^+,
\end{array}\)

and similarly

\(\begin{array}{ c c c }
B^+ & =^{(\tilde{b})} & B^+AB^+ =^{(\tilde{c})} B^+(B^+)^tA^t =^{(a)} B^+(B^+)^tA^t(A^+)^tA^t \\
 & =^{(c)} & B^+(B^+)^tA^tAA^+ =^{(\tilde{c})} B^+AB^+AA^+ =^{(\tilde{a})} B^+AA^+.
\end{array}\)

We summarize our above considerations in the following result.

# ## Theorem 24.1.

For any \(m \times n\) matrix \(A\) the Moore–Penrose inverse \(A^+\) exists uniquely.

From Example 11.4 it is clear that if the right inverse (and similarly the left inverse) of an \(m \times n\) matrix exists then it may not be unique. In what follows, we shall show that the right and left inverses given in Problems 11.9 and 11.10 are in fact Moore–Penrose inverses, and hence unique. For this, we recall that an \(m \times n\) matrix is said to have a _full row (column) rank_ if and only if \(AA^t\) (\(A^tA\)) is invertible, which is equivalent to \(r(A) = m\) (\(r(A) = n\)).

# ## Theorem 24.2.

For an \(m \times n\) matrix \(A\) the Moore–Penrose inverse is

\(A^+=\left\{\begin{array}{ c c }
A^t(AA^t)^{-1}, & \text{if } r(A) = m \\
(A^tA)^{-1}A^t, & \text{if } r(A) = n.
\end{array}\right.\)

(24.6)