

# 第 13 章

# 矩阵表示

在本章中，我们将建立线性映射与矩阵之间的联系。特别是，我们的讨论推广了定理 10.1 和 10.2。我们还将引入相似矩阵的概念，它在后续章节中起着重要作用。

与第 12 章一样，除非另有说明，此处我们也将考虑在同一域 F 上的有限维向量空间 V 和 W。设 $S=\{u^1,\ldots,u^n\}$ 和 $T=\{w^1,\ldots,w^m\}$ 分别为 V 和 W 的有序基，且 $L:V\to W$ 为线性映射。那么，对于每个 $j=1,\ldots,n$，存在唯一的标量 $a_{ij}$，$i=1,\ldots,m$，使得

$$L(u^j)=a_{1j}w^1+\cdots+a_{mj}w^m=\sum_{i=1}^{m}a_{ij}w^i. \tag{13.1}$$

显然，$(a_{1j},\ldots,a_{mj})^t\in F^m$ 是 $L(u^j)$ 在有序基 $T$ 中的坐标。因此，(13.1) 意味着线性映射 $L$ 完全由标量 $a_{ij}$ 确定。这个唯一的 $m\times n$ 矩阵 $A=(a_{ij})$ 称为相对于基 $S$ 和 $T$ 的 $L$ 的转换矩阵。现在设 $u=x_1u^1+\cdots+x_nu^n$ 为 $V$ 中的向量。那么，由 (13.1) 可得

$$L(u)=L\left(\sum_{j=1}^{n}x_ju^j\right)=\sum_{j=1}^{n}x_jL(u^j)$$
$$\phantom{L(u)}=\sum_{j=1}^{n}x_j\left(\sum_{i=1}^{m}a_{ij}w^i\right)=\sum_{i=1}^{m}\left(\sum_{j=1}^{n}a_{ij}x_j\right)w^i.$$

因此，如果
$$w=L(u)=y_1w^1+\cdots+y_mw^m, \tag{13.2}$$
则我们有
$$y_i=\sum_{j=1}^{n}a_{ij}x_j. \tag{13.3}$$

因此，如果 $(x_1,\ldots,x_n)^t_S$ 是 $u\in V$ 的坐标，$(y_1,\ldots,y_m)^t_T$ 是 $w=L(u)\in W$ 的坐标，则
$$y=Ax\quad\text{或}\quad y_T(L(u))=Ax_S(u). \tag{13.4}$$

因此，每个线性映射 \( L: V \to W \) 都可以由相对于基 \( S \) 和 \( T \) 的 \( m \times n \) 转换矩阵 \( A = (a_{ij}) \) 完全表征。通常，我们将此矩阵表示为 \( A_{ST} \)。

# **示例 13.1.** 在 \( (\mathcal{P}_3, \mathbb{R}) \) 和 \( (\mathcal{P}_2, \mathbb{R}) \) 中，分别考虑有序基 \( S = \{1, x, x^2\} \) 和 \( T = \{1, x\} \)。设 \( L: \mathcal{P}_3 \to \mathcal{P}_2 \) 为微分映射，即 \( L(a + bx + cx^2) = b + 2cx \)。对于该映射，我们有

- \( L(1) = 0 = 0(1) + 0(x) \)
- \( L(x) = 1 = 1(1) + 0(x) \)
- \( L(x^2) = 2x = 0(1) + 2(x) \)

因此，相对于给定基 \( S \) 和 \( T \) 的转换矩阵为

- \( A = \begin{pmatrix} 0 & 1 & 0 \\ 0 & 0 & 2 \end{pmatrix} \)。

特别是，对于多项式 \( P_3 = P_3(x) = 4 + 3x + 7x^2 \)，我们有 \( x_S(P_3) = (4, 3, 7)^t \)，因此

- \( y_T(L(P_3)) = \begin{pmatrix} 0 & 1 & 0 \\ 0 & 0 & 2 \end{pmatrix} \begin{pmatrix} 4 \\ 3 \\ 7 \end{pmatrix} = \begin{pmatrix} 3 \\ 14 \end{pmatrix} \)。

这立即给出 \( L(P_3) = 3 + 14x \)。

# **示例 13.2.** 设 \( L: \mathbb{R}^3 \to \mathbb{R}^2 \) 为由 \( L(x, y, z) = (x + y - z, x - y + z)^t \) 定义的线性映射，并设 \( S = \{(1, 1, 1)^t, (1, 1, 0)^t, (1, 0, 0)^t\} \) 和 \( T = \{(1, 2)^t, (2, 1)^t\} \)。由于

- \( (\alpha, \beta)^t = \frac{1}{3}(2\beta - \alpha)(1, 2)^t + \frac{1}{3}(2\alpha - \beta)(2, 1)^t \quad (13.5) \)

我们有

- \( L(u^1) = (1, 1)^t = \frac{1}{3}(1, 2)^t + \frac{1}{3}(2, 1)^t \)
- \( L(u^2) = (2, 0)^t = -\frac{2}{3}(1, 2)^t + \frac{4}{3}(2, 1)^t \)
- \( L(u^3) = (1, 1)^t = \frac{1}{3}(1, 2)^t + \frac{1}{3}(2, 1)^t \)

因此，相对于给定基 \( S \) 和 \( T \) 的转换矩阵为

- \( A = \begin{pmatrix} \frac{1}{3} & -\frac{2}{3} & \frac{1}{3} \\ \frac{1}{3} & \frac{4}{3} & \frac{1}{3} \end{pmatrix} \)。

现在，由于

- \( u = (a, b, c)^t = c(1, 1, 1)^t + (b - c)(1, 1, 0)^t + (a - b)(1, 0, 0)^t \)

由 (13.4) 可得

$$y_T(L(u))=Ax_S(u)=A(c,b-c,a-b)^t=\left(c-b+\frac{1}{3}a,b-c+\frac{1}{3}a\right)^t.$$

根据 (13.5)，我们还有

$$L(u)=(a+b-c,a-b+c)^t=\left(c-b+\frac{1}{3}a\right)(1,2)^t+\left(b-c+\frac{1}{3}a\right)(2,1)^t,$$

这证实了 (13.6)。

反之，假设给定一个 $m\times n$ 矩阵 $A$。那么，由关系 (13.4) 我们可以计算未知映射 $L$ 的坐标 $y_T(L(u))$。但是，(13.2) 唯一确定了映射 $L:V\to W$。可以很容易地验证，该映射是线性的。总之，我们发现，对于给定的两个向量空间 $V$ 和 $W$ 以及固定的有序基 $S$ 和 $T$，所有线性映射 $L:V\to W$ 的集合与所有矩阵 $M^{m\times n}$ 的集合之间存在一一对应关系。

现在设 $S=\{u^1,\ldots,u^n\}$，$\widetilde S=\{\widetilde u^1,\ldots,\widetilde u^n\}$ 为 $V$ 的有序基，且 $T=\{w^1,\ldots,w^m\}$，$\widetilde T=\{\widetilde w^1,\ldots,\widetilde w^m\}$ 为 $W$ 的有序基，且 $L:V\to W$ 为线性映射。由于 $L$ 可以由 $A=A_{ST}=(a_{ij})$ 和 $B=A_{\widetilde S\widetilde T}=(b_{ij})$ 表征，自然想知道这些矩阵之间的关系。为此，设

$$L(w^j)=\sum_{i=1}^{m}a_{ij}w^i,\quad j=1,\ldots,n$$

$$L(\widetilde u^j)=\sum_{k=1}^{m}b_{kj}\widetilde w^k,\quad j=1,\ldots,n$$

$$u^j=\sum_{\mu=1}^{n}p_{\mu j}\widetilde u^\mu,\quad j=1,\ldots,n$$

$$w^j=\sum_{\nu=1}^{m}q_{\nu j}\widetilde w^\nu,\quad j=1,\ldots,m.$$

那么，我们有

$$L(u^j)=L\left(\sum_{\mu=1}^{n}p_{\mu j}\widetilde u^\mu\right)=\sum_{\mu=1}^{n}p_{\mu j}L(\widetilde u^\mu)=\sum_{\mu=1}^{n}\sum_{k=1}^{m}p_{\mu j}b_{k\mu}\widetilde w^k$$

和

$$L(u^j)=\sum_{i=1}^{m}a_{ij}w^i=\sum_{i=1}^{m}a_{ij}\left(\sum_{\nu=1}^{m}q_{\nu i}\widetilde w^\nu\right)=\sum_{i=1}^{m}\sum_{\nu=1}^{m}a_{ij}q_{\nu i}\widetilde w^\nu.$$

通过比较 (13.11) 和 (13.12) 中 \(\tilde{w}^k\) 的系数，我们得到

\(\sum_{s=1}^m q_{ks}a_{sj}=\sum_{s=1}^n b_{ks}p_{sj},j=1,\cdots,n,k=1,\cdots,m.\) (13.13)

因此，如果 \(Q=(q_{ks})_{m\times m}\)、\(A=(a_{sj})_{m\times n}\)、\(B=(b_{ks})_{m\times n}\)、\(P=(p_{sj})_{n\times n}\) 是矩阵，则 (13.13) 等同于

\(QA=BP,\)

并且由于 \(P\) 可逆，我们有所需的关系

\(B=QAP^{-1}.\) (13.14)

在特殊情况下，当 \(V=W\)，且 \(S=T=\{u^1,\cdots,u^n\}\)，\(\tilde{S}=\tilde{T}=\{\tilde{u}^1,\cdots,\tilde{u}^n\}\) 时，我们有 \(P=Q\)，因此关系 (13.14) 简化为

\(B=PAP^{-1},\) (13.15)

这等同于

\(A=P^{-1}BP.\) (13.16)

**示例 13.3.** 除了示例 13.2 中给出的 \(L\)、\(S\)、\(T\) 之外，设 \(\tilde{S}=\{(1,0,0)^t,(0,1,0)^t,(0,0,1)^t\}\) 和 \(\tilde{T}=\{(1,0)^t,(0,1)^t\}\)。那么，我们有

\(A=\left(\begin{array}{ c c c }
\frac{1}{3} & -\frac{2}{3} & \frac{1}{3} \\
\frac{1}{3} & \frac{4}{3} & \frac{1}{3}
\end{array}\right),B=\left(\begin{array}{ c c c }
1 & 1 & -1 \\
1 & -1 & 1
\end{array}\right),Q=\left(\begin{array}{ c c }
1 & 2 \\
2 & 1
\end{array}\right)\)

\(P=\left(\begin{array}{ c c c }
1 & 1 & 1 \\
1 & 1 & 0 \\
1 & 0 & 0
\end{array}\right),P^{-1}=\left(\begin{array}{ c c c }
0 & 0 & 1 \\
0 & 1 & -1 \\
1 & -1 & 0
\end{array}\right).\)

对于这些矩阵，关系 (13.14) 立即成立。

**示例 13.4.** 设 \(L:R^2\rightarrow R^2\) 为由 \(L(x,y)=(2x+y,x+2y)^t\) 定义的线性映射，并设 \(S=\{(1,1)^t,(1,0)^t\}\) 和 \(\tilde{S}=\{(0,1)^t,(1,1)^t\}\)。由于

\(\begin{array}{ c c c }
L(1,1) & = & (3,3)^t=3(1,1)^t+0(1,0)^t \\
L(1,0) & = & (2,1)^t=1(1,1)^t+1(1,0)^t \\
L(0,1) & = & (1,2)^t=1(0,1)^t+1(1,1)^t \\
L(1,1) & = & (3,3)^t=0(0,1)^t+3(1,1)^t \\
(1,1)^t & = & 0(0,1)^t+1(1,1)^t \\
(1,0)^t & = & -1(0,1)^t+1(1,1)^t,
\end{array}\)

我们有

\(A=\left(\begin{array}{ c c }
3 & 1 \\
0 & 1
\end{array}\right),B=\left(\begin{array}{ c c }
1 & 0 \\
1 & 3
\end{array}\right),P=\left(\begin{array}{ c c }
0 & -1 \\
1 & 1
\end{array}\right),P^{-1}=\left(\begin{array}{ c c }
1 & 1 \\
-1 & 0
\end{array}\right).\)

# ## 矩阵表示

对于这些矩阵，关系 (13.15) 立即成立。

最后，设 \( A \) 和 \( B \) 为同阶的两个方阵。如果存在一个非奇异矩阵 \( P \) 使得 (13.16) 成立，则矩阵 \( A \) 和 \( B \) 称为相似，矩阵 \( P \) 称为相似矩阵。显然，示例 13.4 中的矩阵 \( A \) 和 \( B \) 是相似的。从我们上面的讨论可以清楚地看出，矩阵 \( A \) 和 \( B \) 相似当且仅当 \( A \) 和 \( B \) 表示相对于 \( V \) 的两个有序基的同一线性映射 \( L: V \to V \)。很明显，矩阵的相似性是一种等价关系，即自反性、对称性和传递性。

# ## 问题

**13.1.** 在 \( (\mathcal{P}_3, R) \) 和 \( (\mathcal{P}_4, R) \) 中，分别考虑有序基 \( S = \{1, 1+x, 1+x+x^2\} \) 和 \( T = \{x^3+x^2, x^2+x, x+1, 1\} \)。设 \( L: \mathcal{P}_3 \to \mathcal{P}_4 \) 为由 \( L(a+bx+cx^2) = (a+b) + (b+c)x + (c+a)x^2 + (a+b+c)x^3 \) 定义的线性映射。求转换矩阵。

**13.2.** 在 \( R^3 \) 和 \( R^2 \) 中，分别考虑有序基 \( \{(1,1,1)^t, (1,1,0)^t, (1,0,0)^t\} \) 和 \( \{(1,3)^t, (1,2)^t\} \)。设 \( L: R^3 \to R^2 \) 为线性映射 \( L(x,y,z) = (2x+z, 3y-z)^t \)。求转换矩阵。

**13.3.** 在 \( R^3 \) 和 \( R^4 \) 中，分别考虑有序基 \( S = \{(1,1,0)^t, (1,0,1)^t, (0,1,1)^t\} \) 和 \( T = \{(1,1,1,1)^t, (1,1,1,0)^t, (1,1,0,0)^t, (1,0,0,0)^t\} \)。设 \( L: R^3 \to R^4 \) 为线性映射 \( L(x,y,z) = (2x+y+z, x+2y+z, x+y+2z, 2x-y-z)^t \)。求转换矩阵。

**13.4.** 在问题 13.1 中，而不是 \( L \)，设给定的 \( 4 \times 3 \) 矩阵

\( A = \begin{pmatrix} 1 & -1 & 0 \\ 0 & 3 & -2 \\ 3 & 5 & 2 \\ 2 & 1 & 1 \end{pmatrix} \)

求线性映射 \( L: \mathcal{P}_3 \to \mathcal{P}_4 \)。

**13.5.** 在问题 13.2 中，而不是 \( L \)，设给定的 \( 2 \times 3 \) 矩阵

\( A = \begin{pmatrix} 2 & -1 & 3 \\ -3 & 2 & 1 \end{pmatrix} \)

求线性映射 \( L: R^3 \to R^2 \)。

**13.6.** 在问题 13.3 中，而不是 \( L \)，设给定的 \( 4 \times 3 \) 矩阵

\( A = \begin{pmatrix} -1 & 1 & 1 \\ 5 & 3 & -2 \\ 4 & 5 & 2 \\ 2 & 1 & -1 \end{pmatrix} \)

