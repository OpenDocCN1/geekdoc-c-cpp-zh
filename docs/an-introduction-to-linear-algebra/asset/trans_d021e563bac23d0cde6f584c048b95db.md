

矩阵 $A$ 和 $C$ 为单调矩阵。因此，[定理 25.8](#) 适用，且矩阵 $B$ 必为单调矩阵，事实上我们有

$$B^{-1}=\begin{pmatrix}\frac{11}{4}&\frac{1}{2}&\frac{3}{4}\\\frac{5}{4}&\frac{1}{2}&\frac{1}{4}\\\frac{1}{2}&0&\frac{1}{2}\end{pmatrix}.$$

## 定理 25.9.

设 $n\times n$ 矩阵 $A$ 写作 $A=I-B$，其中 $B=(b_{ij})\geq 0$ 且（在任意范数下）$\|B\|<1$。则矩阵 $A$ 为单调矩阵。

## 例 25.11.

考虑以下矩阵及其逆矩阵

$$A=\begin{pmatrix}1&-\frac{1}{2}&-\frac{1}{4}\\-\frac{1}{4}&\frac{1}{2}&-\frac{1}{6}\\-\frac{1}{6}&-\frac{1}{3}&1\end{pmatrix},\qquad A^{-1}=\begin{pmatrix}\frac{32}{19}&\frac{42}{19}&\frac{15}{19}\\\frac{20}{19}&\frac{19}{19}&\frac{33}{38}\\\frac{12}{19}&\frac{30}{19}&\frac{27}{19}\end{pmatrix}.$$

由 [定理 26.6](#) 可知矩阵 $A$ 为单调矩阵。因为

$$A=I-B=\begin{pmatrix}1&0&0\\0&1&0\\0&0&1\end{pmatrix}-\begin{pmatrix}0&\frac{1}{2}&\frac{1}{4}\\\frac{1}{4}&\frac{1}{2}&\frac{1}{6}\\\frac{1}{6}&\frac{1}{3}&0\end{pmatrix},$$

矩阵 $B$ 满足 [定理 25.9](#) 的所有条件，因此矩阵 $A$ 为单调矩阵。

## 定理 25.10.

设 $n\times n$ 矩阵 $A$ 为对称、正定矩阵，并写作 $A=I-B$，其中 $B=(b_{ij})\geq 0$。则矩阵 $A$ 为单调矩阵。

## 例 25.12.

对于矩阵

$$A=\begin{pmatrix}1&-\frac{1}{3}&0&0\\-\frac{1}{3}&1&-\frac{1}{3}&0\\0&-\frac{1}{3}&1&-\frac{1}{3}\\0&0&-\frac{1}{3}&1\end{pmatrix}$$

其特征值为

$$\frac{5}{6}-\frac{1}{6}\sqrt{5},\quad \frac{1}{6}\sqrt{5}+\frac{5}{6},\quad \frac{7}{6}-\frac{1}{6}\sqrt{5},\quad \frac{1}{6}\sqrt{5}+\frac{7}{6}$$

为正，因此它是正定矩阵。我们可以写 $A=I-B$，其中

$$B=\begin{pmatrix}0&\frac{1}{3}&0&0\\\frac{1}{3}&0&\frac{1}{3}&0\\0&\frac{1}{3}&0&\frac{1}{3}\\0&0&\frac{1}{3}&0\end{pmatrix}.$$

且

\[
u^i=\left(\sin\frac{i\pi}{n+1},\sin\frac{2i\pi}{n+1},\cdots,\sin\frac{ni\pi}{n+1}\right)^t,\qquad 1\le i\le n,
\]

也有

\[
\det(B)=\prod_{i=1}^{n}\left[b_0+2b_1\cos\left(\frac{i\pi}{n+1}\right)\right].
\]

## 例 25.14.

对于 (25.3) 中的矩阵 $B$，当 $n=4$ 时，有

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

在 Toeplitz 矩阵 $A$ 中，若取 $a_i=a_{-(n-i)}$，$1=1,\cdots,n-1$，则其退化为循环矩阵（参见 [问题 16.8](#)）。

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

## 例 25.15.

当 $n=4$ 时，矩阵 $A$ 在 (25.4) 中的特征值为

\[
\lambda_1=a_0-a_{-1}+a_{-2}-a_{-3},\qquad
\lambda_2=a_0+a_{-1}+a_{-2}+a_{-3},
\]
\[
\lambda_3=a_0-a_{-2}-i(a_{-3}-a_{-1}),\qquad
\lambda_4=a_0-a_{-2}+i(a_{-3}-a_{-1}).
\]

## 定理 25.11.

对于任意两个给定的循环矩阵 $A$ 和 $B$，和 $A+B$ 为循环矩阵，积 $AB$ 为循环矩阵，且 $AB=BA$。

## 例 25.16.

对于矩阵 $A=\operatorname{circ}(2,1,5)$，$B=\operatorname{circ}(4,3,-1)$，有 $A+B=\operatorname{circ}(6,4,4)$ 且 $AB=BA=\operatorname{circ}(22,5,21)$。

## 问题

**25.1.** 利用定理 25.1 证明以下矩阵为可约矩阵：
\(A = \begin{pmatrix} 2 & 3 & 5 & 2 \\ 0 & 5 & 3 & 0 \\ 0 & 3 & 2 & 0 \\ 0 & 4 & 1 & 0 \end{pmatrix}, \quad B = \begin{pmatrix} 0 & 1 & 3 & 2 \\ 0 & 5 & 0 & 7 \\ 2 & 0 & 0 & 1 \\ 0 & 3 & 0 & 2 \end{pmatrix}.\)

**25.2.** 证明定理 25.2。

**25.3.** 利用定理 25.2 判断以下矩阵是可约还是不可约：
\(A = \begin{pmatrix} 0 & 2 \\ 3 & 4 \end{pmatrix}, \quad B = \begin{pmatrix} 3 & 2 \\ 0 & 4 \end{pmatrix}, \quad C = \begin{pmatrix} 4 & 0 & 7 \\ 11 & 8 & 0 \\ 0 & 5 & 8 \end{pmatrix}.\)

**25.4.** 证明定理 25.4。

**25.5.** 利用定理 25.4 证明以下矩阵可逆：
\(A = \begin{pmatrix} 7 & 2 & 3 \\ 1 & 5 & 2 \\ 3 & 4 & 8 \end{pmatrix}, \quad B = \begin{pmatrix} 5 & 4 & 1 \\ 3 & 3 & 0 \\ 0 & 6 & 6 \end{pmatrix}.\)

**25.6.** 证明定理 25.6。

**25.7.** 证明例 25.1 中的矩阵 $C$ 和 $D$ 不是单调矩阵。

**25.8.** 设 $A=(a_{ij})$ 和 $B=(b_{ij})$ 为 $n\times n$ 单调矩阵。证明若 $A\ge B$，即 $a_{ij}\ge b_{ij}$，$1\le i,j\le n$，则 $A^{-1}\le B^{-1}$。

**25.9.** 利用定理 25.6 证明以下矩阵为单调矩阵
\(A = \begin{pmatrix} 2 & 2 & -3 \\ -3 & 2 & 2 \\ 2 & -3 & 2 \end{pmatrix}, \quad B = \begin{pmatrix} 28 & -7 & 1 \\ -42 & -28 & 70 \\ 14 & 35 & -27 \end{pmatrix}.\)

**25.10.** 证明定理 25.9。

**25.11.** 求以下矩阵的特征值和特征向量：
\(A = \begin{pmatrix} 1 & 3 & 0 & 0 \\ 3 & 1 & 3 & 0 \\ 0 & 3 & 1 & 3 \\ 0 & 0 & 3 & 1 \end{pmatrix}, \quad B = \begin{pmatrix} a_0 & 0 & a_{-2} & 0 \\ 0 & a_0 & 0 & a_{-2} \\ a_{-2} & 0 & a_0 & 0 \\ 0 & a_{-2} & 0 & a_0 \end{pmatrix}.\)

**25.12.** 证明 $\operatorname{circ}(1,-1,2,3)\operatorname{circ}(4,1,5,-3)=\operatorname{circ}(20,6,3,6)$。

# 答案或提示

**25.1.** \(\begin{pmatrix}2&3&0&0\\3&5&0&0\\1&4&0&0\\5&3&2&2\end{pmatrix}=\begin{pmatrix}0&0&1&0\\0&1&0&0\\0&0&0&1\\1&0&0&0\end{pmatrix}A\begin{pmatrix}0&0&0&1\\0&1&0&0\\1&0&0&0\\0&0&1&0\end{pmatrix}.\)

\(\begin{pmatrix}5&7&0&0\\3&2&0&0\\1&2&0&3\\0&1&2&0\end{pmatrix}=\begin{pmatrix}0&1&0&0\\0&0&0&1\\1&0&0&0\\0&0&1&0\end{pmatrix}B\begin{pmatrix}0&0&1&0\\1&0&0&0\\0&0&0&1\\0&1&0&0\end{pmatrix}.\)

**25.2.** 设 $A$ 为不可约矩阵，并假设其有向图 $G$ 不是强连通的。假设 $G$ 有 $n$ 条边。则存在顶点 $v_i$ 和 $v_j$，使得它们之间不存在任何路径。我们用 $S$ 表示与 $v_j$ 相连的边的集合，用 $T$ 表示其余边的集合。显然集合 $S$ 和 $T$ 都非空，因为 $v_j\in S$ 且 $v_i\in T$。这意味着没有边 $v\in S$ 与边 $w\in T$ 相连，因为否则 $w\in S$，这与事实不符。如果我们对图 $G$ 中的边进行重新排序，并假设前 $q$ 条边在 $S$ 中，接下来的 $n-q$ 个顶点在 $T$ 中，则对于 $r\in S$、$s\in T$ 有 $a_{rs}=0$。但这与我们假设 $A$ 为不可约矩阵矛盾。逆命题需要类似的论证。

**25.3.** $A$ 不可约，$B$ 可约，$C$ 不可约。

**25.4.** 假设 $A$ 为严格对角占优且不可逆。则 $A$ 的至少一个特征值为零，设为 $\lambda_m=0$。设与 $\lambda_m$ 对应的特征向量为 $u=(u_1,\ldots,u_n)$。由于 $Au=\lambda_m u=0$，可得 $\sum_{j=1}^n a_{ij}u_j=0$，$1\le i\le n$。设 $\|u\|_\infty=\max_{1\le i\le n}|u_i|=|u_k|$。则有 $a_{kk}u_k=-\sum_{j=1,j\ne k}^n a_{kj}u_j$，由此得 $|a_{kk}|\le\sum_{j=1,j\ne k}^n|a_{kj}||u_j/u_k|$，或 $|a_{kk}|\le\sum_{j=1,j\ne k}^n|a_{kj}|$。但这与我们假设 $A$ 为严格对角占优矩阵矛盾。

**25.5.** 矩阵 $A$ 为严格对角占优，其逆矩阵为 $\frac{1}{187}\begin{pmatrix}32&-4&-17\\-2&47&-17\\-17&-34&51\end{pmatrix}$。矩阵 $B$ 为对角占优且不可约，其逆矩阵为 $\frac{1}{12}\begin{pmatrix}6&-6&-1\\-6&10&1\\6&-10&1\end{pmatrix}$。

**25.6.** 设 $A$ 为单调矩阵且 $A^{-1}=(b^1,\ldots,b^n)$。则 $Ab^j=e^j\ge0$，$1\le j\le n$ 蕴含 $b^j\ge0$，$1\le j\le n$。因此，$A^{-1}\ge0$。反之，若 $A^{-1}\ge0$ 且 $Au\ge0$，则 $u=(A^{-1}A)u=A^{-1}(Au)\ge0$。

**25.7.** 根据 [定理 25.6](#)，只需观察

