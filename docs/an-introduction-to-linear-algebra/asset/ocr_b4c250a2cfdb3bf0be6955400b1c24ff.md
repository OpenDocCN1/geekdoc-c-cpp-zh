# 21.4.

Show that the following system has no solution

```
$$\begin{pmatrix}1&2&1&5\\1&2&-1&1\\2&4&-3&0\end{pmatrix}\begin{pmatrix}x_1\\x_2\\x_3\\x_4\end{pmatrix}=\begin{pmatrix}1\\1\\3\end{pmatrix}.$$
```

Find its least squares solution.

# 21.5.

Show that the following system has no solution

```
$$\begin{pmatrix}2&1&3\\4&3&5\\8&2&16\\-4&1&-11\\-2&3&-5\end{pmatrix}\begin{pmatrix}x_1\\x_2\\x_3\end{pmatrix}=\begin{pmatrix}1\\2\\4\\2\\2\end{pmatrix}.$$
```

Find its least squares solution.

# Answers or Hints

+   21.1. $\left(\frac{1}{3},\frac{2}{3},1\right)^t$

+   21.2. $\left(2,\frac{13}{55},0\right)^t+\left(-5,\frac{48}{55},\frac{147}{55},1\right)^t c$.

+   21.3. $(0,1,1,0)^t+\left(-\frac{13}{30},\frac{9}{10},\frac{16}{15},1,0\right)^t c+\left(\frac{1}{30},\frac{7}{10},\frac{8}{15},0,1\right)^t d$.

+   21.4. That the Solution does not exist follows from the echelon form of the augmented matrix $\begin{pmatrix}1&2&1&5&|&1\\0&0&-2&-4&|&0\\0&0&0&0&|&1\end{pmatrix}$. Its least squares solution is $\frac{1}{15}(17,0,-3,0)^t+(-2,1,0,0)^t c+(-3,0,-2,1)^t d$.

+   21.5. That the Solution does not exist follows from the echelon form of the augmented matrix $\begin{pmatrix}2&1&3&|&1\\0&1&-1&|&0\\0&0&2&|&0\\0&0&0&|&4\\0&0&0&|&3\end{pmatrix}$. Its least squares solution is $\frac{1}{956}(491,680,-173)^t$.