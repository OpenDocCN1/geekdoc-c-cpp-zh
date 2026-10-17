Thus, the system has a solution if and only if $h=2$, and in such a case the solution is

$\left(\frac{1}{2}(10-k),\frac{1}{2}(6-k),-\frac{1}{2}(6-k)\right)^t.$

Since the columns of the matrix $A$ in (21.9) are linearly independent, from Corollary 21.1 and Example 18.6, it follows that the unique least squares solution of (21.9) can be obtained by solving the system

$\begin{pmatrix}\frac{6}{\sqrt{3}}&\frac{9}{\sqrt{3}}&\frac{18}{\sqrt{3}}\\0&\frac{3}{\sqrt{3}}&\frac{2}{\sqrt{3}}\\0&0&\frac{2}{\sqrt{6}}\end{pmatrix}\begin{pmatrix}\hat{x}_1\\\hat{x}_2\\\hat{x}_3\end{pmatrix}=\begin{pmatrix}\frac{1}{2\sqrt{3}}&-\frac{1}{2\sqrt{3}}&-\frac{2}{\sqrt{6}}\\\frac{1}{2\sqrt{3}}&\frac{1}{2\sqrt{3}}&-\frac{1}{\sqrt{6}}\\\frac{1}{2\sqrt{3}}&\frac{3}{2\sqrt{3}}&0\\\frac{3}{2\sqrt{3}}&-\frac{1}{2\sqrt{3}}&\frac{1}{\sqrt{6}}\end{pmatrix}\begin{pmatrix}2\\2\\h\\k\end{pmatrix}$

$=\begin{pmatrix}\frac{1}{2\sqrt{3}}(4+h+3k)\\\frac{1}{2\sqrt{3}}(3h-k)\\\frac{1}{\sqrt{6}}(k-6)\end{pmatrix}$.

Using backward process this system gives the unique least squares approximate solution of (21.9) as

$x_3=-\frac{1}{2}(6-k),\quad x_2=\frac{1}{2}(h-k+4),\quad x_1=\frac{1}{6}(38-4h-3k).$

Clearly, (21.11) is the same as (21.10) for $h=2$, as it should be.

For (21.9) the system (21.2) is

$\begin{pmatrix}12&18&36\\18&30&56\\36&56&110\end{pmatrix}\begin{pmatrix}x_1\\x_2\\x_3\end{pmatrix}=\begin{pmatrix}4+h+3k\\6+3h+4k\\10+4h+9k\end{pmatrix}$,

which as expected gives the same solution as (21.11).

# **Example 21.2.**

Consider the system

$\begin{pmatrix}1&3&2\\3&-5&-1\\4&2&3\\2&2&2\end{pmatrix}\begin{pmatrix}x_1\\x_2\\x_3\end{pmatrix}=\begin{pmatrix}1\\2\\3\\4\end{pmatrix}$.

In view of Problem 8.1(i), in this system the columns of the matrix $A$ are linearly dependent. Further, for this system the echelon form of the augmented matrix appears as

$\begin{pmatrix}1&3&2&\mid&1\\0&1&\frac{1}{2}&\mid&\frac{1}{14}\\0&0&0&\mid&-\frac{2}{7}\\0&0&0&\mid&\frac{16}{7}\end{pmatrix}$,