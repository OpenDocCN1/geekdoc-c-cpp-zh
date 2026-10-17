and

\[
u^i=\left(\sin\frac{i\pi}{n+1},\sin\frac{2i\pi}{n+1},\cdots,\sin\frac{ni\pi}{n+1}\right)^t,\qquad 1\le i\le n,
\]

also

\[
\det(B)=\prod_{i=1}^{n}\left[b_0+2b_1\cos\left(\frac{i\pi}{n+1}\right)\right].
\]

**Example 25.14.** For the matrix $B$ in (25.3) with $n=4$, it follows that

\[
\lambda_1=b_0+\frac{1+\sqrt5}{2}b_1,\quad
\lambda_2=b_0+\frac{1-\sqrt5}{2}b_1,\quad
\lambda_3=b_0-\frac{1-\sqrt5}{2}b_1,\quad
\lambda_4=b_0-\frac{1+\sqrt5}{2}b_1,
\]

\[
u^1=\begin{pmatrix}1\\\frac{1+\sqrt5}{2}\\\frac{1+\sqrt5}{2}\\1\end{pmatrix},\quad
u^2=\begin{pmatrix}1\\\frac{1-\sqrt5}{2}\\\frac{1-\sqrt5}{2}\\1\end{pmatrix},\quad
u^3=\begin{pmatrix}-1\\\frac{1-\sqrt5}{2}\\\frac{-1+\sqrt5}{2}\\1\end{pmatrix},\quad
u^4=\begin{pmatrix}-1\\-\frac{1+\sqrt5}{2}\\-\frac{1+\sqrt5}{2}\\1\end{pmatrix}.
\]

\[
\det(B)=(b_1^2-b_0^2-b_0b_1)(b_0b_1-b_0^2+b_1^2).
\]

In Toeplitz matrix $A$, if we take $a_i=a_{-(n-i)}$, $1=1,\cdots,n-1$, then it reduces to a circulant matrix (see [Problem 16.8](#)).

\[
A=\operatorname{circ}(a_0,a_1,\cdots,a_{-(n-1)})
\]

\[
=\begin{pmatrix}
a_0&a_{-1}&a_{-2}&\cdots&\cdots&a_{-(n-1)}\\
a_{-(n-1)}&a_0&a_{-1}&\cdots&\cdots&a_{-(n-2)}\\
a_{-(n-2)}&a_{-(n-1)}&a_0&\cdots&\cdots&a_{-(n-3)}\\
\vdots&\vdots&\vdots&\ddots&\vdots&\vdots\\
a_{-2}&\cdots&\cdots&a_{-(n-1)}&a_0&a_{-1}\\
a_{-1}&\cdots&\cdots&a_{-(n-2)}&a_{-(n-1)}&a_0
\end{pmatrix}. \tag{25.4}
\]

**Example 25.15.** For $n=4$, the eigenvalues of the matrix $A$ in (25.4) are

\[
\lambda_1=a_0-a_{-1}+a_{-2}-a_{-3},\qquad
\lambda_2=a_0+a_{-1}+a_{-2}+a_{-3},
\]
\[
\lambda_3=a_0-a_{-2}-i(a_{-3}-a_{-1}),\qquad
\lambda_4=a_0-a_{-2}+i(a_{-3}-a_{-1}).
\]

**Theorem 25.11.** For any two given circulant matrices $A$ and $B$, the sum $A+B$ is circulant, the product $AB$ is circulant, and $AB=BA$.

**Example 25.16.** For the matrices $A=\operatorname{circ}(2,1,5)$, $B=\operatorname{circ}(4,3,-1)$, we have $A+B=\operatorname{circ}(6,4,4)$ and $AB=BA=\operatorname{circ}(22,5,21)$.