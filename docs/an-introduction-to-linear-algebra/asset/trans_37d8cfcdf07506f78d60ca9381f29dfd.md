

此结果被称为 *Cayley–Hamilton* 定理。

# **示例 16.3.** 将 (16.6) 乘以 $A^{-1}$，可得

$$A^{-1}=-\frac{1}{a_n}\left[(-1)^nA^{n-1}+a_1A^{n-2}+\cdots+a_{n-1}I\right]. \tag{16.7}$$

因此，若 $A^i$，$i=2,3,\cdots,n-1$ 已知，则矩阵 $A$ 的逆矩阵可被计算。特别是，对于 (16.4) 中的矩阵 $A$，我们有

$$\begin{aligned} A^{-1}&=-\frac{1}{8}[-A^2+7A-14I]\\ &= -\frac{1}{8}\left[-\begin{pmatrix}5&5&1\\5&11&5\\1&5&5\end{pmatrix}+7\begin{pmatrix}2&1&0\\1&3&1\\0&1&2\end{pmatrix}-14\begin{pmatrix}1&0&0\\0&1&0\\0&0&1\end{pmatrix}\right]\\ &=\begin{pmatrix}\frac{5}{8}&-\frac{2}{8}&\frac{1}{8}\\-\frac{2}{8}&\frac{4}{8}&-\frac{2}{8}\\\frac{1}{8}&-\frac{2}{8}&\frac{5}{8}\end{pmatrix}. \end{aligned}$$

P12. 对应于某个特征值的线性无关特征向量的个数称为其 *几何重数*。特征值的几何重数至多为其代数重数。相似矩阵 $A$ 和 $B$ 具有相同的特征值，且这些特征值具有相同的代数重数和几何重数：由于存在一个非奇异矩阵 $P$ 使得 $B=P^{-1}AP$，我们有 $(B-\lambda I)=P^{-1}AP-\lambda P^{-1}P=P^{-1}(A-\lambda I)P$，即，若 $A$ 和 $B$ 相似，则 $(A-\lambda I)$ 和 $(B-\lambda I)$ 也相似。因此，由问题 13.10 可知 $\det(A-\lambda I)=\det(B-\lambda I)$ 且 $\mathcal{N}(A-\lambda I)=\mathcal{N}(B-\lambda I)$，即，$A$ 和 $B$ 具有相同的特征值，且具有相同的代数重数和几何重数。

# **示例 16.4.** 矩阵

$$A=\begin{pmatrix}2&1&-1\\-3&-1&1\\9&3&-4\end{pmatrix}$$

的特征值为 $-1,-1,-1$。此外，对应于该特征值的唯一线性无关特征向量为 $(1,0,3)^t$。因此，特征值 $-1$ 的代数重数为 3，而其几何重数为 1。

# **示例 16.5.** 矩阵

$$A=\begin{pmatrix}-1&0&4\\0&-1&2\\0&0&1\end{pmatrix}$$

的特征值为 $-1,-1,1$。此外，对应于特征值 $-1$ 的线性无关特征向量为 $(1,0,0)^t$ 和 $(0,1,0)^t$。因此，特征值 $-1$ 的代数重数和几何重数均为 2。对应于特征值 1 的特征向量为 $(2,1,1)^t$。

本章讨论的计算特征值和特征向量的方法仅适用于小型矩阵。

# ## 问题

**16.1.** 设 \(\lambda_1, \cdots, \lambda_n\) 为 \(n \times n\) 矩阵 \(A\) 的（不一定互异）特征值。证明

+   (i) 对于任意常数 \(\alpha\)，\(\alpha A\) 的特征值为 \(\alpha\lambda_1, \cdots, \alpha\lambda_n\)

+   (ii) \(\sum_{i=1}^n \lambda_i = \text{Tr } A\)

+   (iii) \(\prod_{i=1}^n \lambda_i = \text{det } A\)

+   (iv) 若 \(A\) 为上（下）三角矩阵，即 \(a_{ij} = 0, i > j (i < j)\)，则 \(A\) 的特征值为 \(A\) 的对角元素

+   (v) 若 \(A\) 为实矩阵且 \(\lambda_1\) 为复数，对应的特征向量为 \(v^1\)，则至少存在一个 \(i, 2 \le i \le n\)，使得 \(\lambda_i = \overline{\lambda_1}\)，且对于这样的 \(i\)，\(\overline{v^1}\) 为对应的特征向量

+   (vi) 若存在某个正整数 \(k\) 使得 \(A^k = 0\)，即 \(A\) 为幂零矩阵，则 0 是 \(A\) 的唯一特征值

+   (vii) 若 \(A\) 为正交矩阵，则 \(|\lambda_i| = 1, i = 1, \cdots, n\)。

**16.2.** 求下列矩阵的特征值和特征向量

+   (i) \(\left(\begin{array}{ c c c }
+   4 & -2 & 1 \\
+   1 & 3 & 0 \\
+   2 & 8 & -1
+   \end{array}\right)\) (ii) \(\left(\begin{array}{ c c c }
+   3 & 0 & 0 \\
+   -4 & 6 & 2 \\
+   16 & -15 & -5
+   \end{array}\right)\) (iii) \(\left(\begin{array}{ c c c }
+   8 & -6 & 2 \\
+   -6 & 7 & -4 \\
+   2 & -4 & 3
+   \end{array}\right)\)。

**16.3.** 求下列矩阵的特征值和特征向量

+   (i) \(\left(\begin{array}{ c c }
+   4 & -2 \\
+   5 & 2
+   \end{array}\right)\) (ii) \(\left(\begin{array}{ c c c }
+   1 & 0 & 0 \\
+   2 & 1 & -2 \\
+   3 & 2 & 1
+   \end{array}\right)\) (iii) \(\left(\begin{array}{ c c c }
+   2 & 1 & -2 \\
+   -1 & 0 & 0 \\
+   1 & 1 & -1
+   \end{array}\right)\)。

**16.4.** 对问题 16.2 中给出的矩阵验证 Cayley–Hamilton 定理。

**16.5.** 使用 (16.7) 求问题 16.2 中给出矩阵的逆矩阵。

**16.6.** 求下列矩阵各特征值的代数重数和几何重数：

# # 16.15.

设 \( A \) 为 \( n \times n \) 矩阵，具有线性无关特征向量 \( u^1, \cdots, u^n \) 及其对应的特征值 \( \lambda_1, \cdots, \lambda_n \)，其中 \( |\lambda_1| > |\lambda_2| \ge |\lambda_3| \ge \cdots \ge |\lambda_n| \)，即，\(\lambda_1\) 为 *主特征值*)。进一步，设 \( \hat{u} = c_1 u^1 + \cdots + c_n u^n \)，其中 \( c_1 \neq 0 \)。证明 \( \lim_{m \to \infty} (1/\lambda_1^m) A^m \hat{u} = c_1 u^1 \)。特别是，对于 (16.4) 中的矩阵 \( A \) 证明

\(\frac{1}{4^8} A^8 \left( \begin{array}{ c } 1 \\ 1 \\ 1 \end{array} \right) = \frac{1}{4^8} \left( \begin{array}{ c c c } 11051 & 21845 & 10795 \\ 21845 & 43691 & 21845 \\ 10795 & 21845 & 11051 \end{array} \right) \left( \begin{array}{ c } 1 \\ 1 \\ 1 \end{array} \right) \simeq \left( \begin{array}{ c } 0.666672 \\ 1.333328 \\ 0.666672 \end{array} \right) \simeq k \left( \begin{array}{ c } 1 \\ 2 \\ 1 \end{array} \right),\)

其中 \( k \) 为常数。

# # 答案或提示

# ## 16.1.

(i) \( (\alpha A)x = (\alpha \lambda)x \)。

# (ii)

\( \det(A - \lambda I) = (a_{11} - \lambda) \cdot \text{cofactor}(a_{11} - \lambda) + \sum_{j=2}^n a_{1j} \cdot \text{cofactor } a_{1j} \)，且由于每一项 \( a_{1j} \cdot \text{cofactor } a_{1j} \) 都是次数至多为 \( n - 2 \) 的多项式，比较 \( \lambda^{n-1} \) 的系数，可得 \( (-1)^{n+1} \sum_{i=1}^n \lambda_i = \text{coefficient of } \lambda^{n-1} \text{ in } (a_{11} - \lambda) \cdot \text{cofactor}(a_{11} - \lambda) \)。因此，易于归纳可得 \( (-1)^{n+1} \sum_{i=1}^n \lambda_i = \text{coefficient of } \lambda^{n-1} \text{ in } (a_{11} - \lambda) \cdots (a_{nn} - \lambda) = (-1)^{n-1} \sum_{i=1}^n a_{ii} \)。

# (iii)

在 \( \det(A - \lambda I) = (-1)^n (\lambda - \lambda_1) \cdots (\lambda - \lambda_n) \) 中代入 \( \lambda = 0 \)。

# (iv)

由行列式展开即可得出。

# (v)

对于实系数多项式，复根仅以共轭对出现。因此 \(\lambda_1 = \mu + i\nu\) 和 \(\overline{\lambda_1} = \mu - i\nu\) 均为特征值。现若 \( u = v + iw \) 为对应于 \(\lambda_1\) 的特征向量，即 \( Au = \lambda_1 u \)，则由于 \( A \) 为实矩阵，\( A\overline{u} = \overline{\lambda_1} \overline{u} \)。

# (vi)

使用 P11。

# (vii)

若 \( A^{-1} = A^t \)，则由 P6 和 P7 可知 \( 1/\lambda = \lambda \)，即 \( \lambda^2 = 1 \)。

# ## 16.2.

(i) \( 4, (1,1,2)^t; 3, (0,1,2)^t; -1, (-4,1,22)^t \)。

# (ii)

\( 0, (0,1,-3)^t; 1, (0,-2,5)^t; 3, (1,0,2)^t \)。

# (iii)

\( 0, (1,2,2)^t; 3, (2,1,-2)^t; 15, (2,-2,1)^t \)。

# ## 16.3.

(i) \( 3 \pm 3i, (2,1 \mp 3i)^t \)。

# (ii)

\( 1, (-2,3,-2)^t; 1 \pm 2i, (0, \pm i, 1)^t \)。

# (iii)

\( 1, (1,-1,0)^t; \pm i, (1, \pm i, 1) \)。

# ## 16.4.

直接验证。

# ## 16.5.

(i) \( \frac{1}{12} \left( \begin{array}{ c c c } 3 & -6 & 3 \\ -1 & 6 & -1 \\ -2 & 36 & -14 \end{array} \right) \)。

# (ii)

奇异矩阵。

# (iii)

奇异矩阵。

# 16.6. (i) 对于 \(\lambda_1 = -1\)，代数重数为 2，几何重数为 1。对于 \(\lambda_2 = 3\)，代数重数和几何重数均为 1。
(ii) 对于 \(\lambda = 1\)，代数重数为 3，几何重数为 2。
(iii) 对于 \(\lambda_1 = 2\)，代数重数为 2，几何重数为 1。对于 \(\lambda_2 = 3\)，代数重数和几何重数均为 1。
16.7. \(C_1 + \lambda C_2 + \cdots + \lambda^{n-1}C_n\)。
16.8. (i) 直接验证。
(ii) \(P\) 的特征多项式为 \((-1)^n(\lambda^n - 1)\)。使用性质 P12。
16.9. 将 (4.6) 中的 \(x\) 替换为 \(x - \lambda\)。直接验证。
16.10. \(\lambda_i = a - 2\sqrt{bc} \cos\frac{i\pi}{n+1}\)，\(i = 1, \cdots, n\)。
16.11. 对应的矩阵为循环矩阵，其中 \(a_1 = x\)，\(a_2 = 1\)，\(a_3 = \cdots = a_{n-1} = 0\)，\(a_n = 1\)。因此，由问题 16.7 可知，其特征值为 \(\lambda_k = x + \omega_k + \omega_k^{n-1}\)。现由于 \(\omega_k = e^{2k\pi i/n}\)，可得 \(\lambda_k = x + 2\cos(2\pi k/n)\)。现使用问题 16.1(iii)。
16.12. 对应的矩阵为循环矩阵，其特征值为 \(\lambda_k = x + 2a\omega_k + \omega_k^2 + \omega_k^{n-2} + 2a\omega_k^{n-1}\)。
16.13. (i) 类似于 P4。
(ii) 类似于定理 12.3。
16.14. (i) 特征值和特征向量分别为 1、2、3、5 以及 \((4, -11, -4, 0)^t\)、\((0, 10, 3, 0)^t\)、\((0, 0, 0, 1)^t\)、\((0, 1, 0, 0)^t\)。
(ii) \(-x'' = \lambda x\)，\(x(0) = x(1) = 0\)，\(\lambda_n = n^2\pi^2\)，\(x_n(t) = \sin n\pi t\)，\(n = 1, 2, \cdots\)。
(iii) 特征值和特征向量分别为 1、2 以及 \((1, 0)^t\)、\((1, 1)^t\)。
16.15. \(A^m\hat{u} = A^m(c_1u^1 + \cdots + c_nu^n) = c_1\lambda_1^m u^1 + \cdots + c_n\lambda_n^m u^n\)，因此
\(\frac{1}{\lambda_1^m}A^m\hat{u} = c_1u^1 + \left(\frac{\lambda_2}{\lambda_1}\right)^m u^2 + \cdots + \left(\frac{\lambda_n}{\lambda_1}\right)^m u^n\)。

