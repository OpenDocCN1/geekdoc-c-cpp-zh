

and
\(\sum_{i=1}^n a_{ij}\alpha_{ik}=0 \text{ if } j \neq k.\) (3.3)

因此，阶数为 \(n\) 的行列式可以表示为 \(n\) 个阶数为 \(n-1\) 的行列式。计算行列式 \(A\) 的公式 (3.1) 称为 _Laplace 展开_。特别是，对于阶数为 3 的行列式，我们有

\(\begin{vmatrix} a_{11} & a_{12} & a_{13} \\ a_{21} & a_{22} & a_{23} \\ a_{31} & a_{32} & a_{33} \end{vmatrix} = a_{11} \begin{vmatrix} a_{22} & a_{23} \\ a_{32} & a_{33} \end{vmatrix} - a_{12} \begin{vmatrix} a_{21} & a_{23} \\ a_{31} & a_{33} \end{vmatrix} + a_{13} \begin{vmatrix} a_{21} & a_{22} \\ a_{31} & a_{32} \end{vmatrix}\)
\(= a_{11}(a_{22}a_{33} - a_{23}a_{32}) - a_{12}(a_{21}a_{33} - a_{23}a_{31})\)
\(+ a_{13}(a_{21}a_{32} - a_{22}a_{31})\)
\(= a_{11}a_{22}a_{33} - a_{11}a_{23}a_{32} - a_{12}a_{21}a_{33} + a_{12}a_{23}a_{31}\)
\(+ a_{13}a_{21}a_{32} - a_{13}a_{22}a_{31}.\) (3.4)

为了找到与 (3.4) 类似的阶数为 \(n\) 的行列式的通用表达式，我们回顾一下，集合 \(N = \{1, 2, \cdots, n\}\) 的一个排列 \(\sigma\) 是 \(N\) 到其自身的一个一对一映射。这样的排列通常表示为 \(\sigma = i_1 i_2 \cdots i_n\)，其中 \(i_j = \sigma(j)\)。很明显，\(N\) 有 \(n!\) 个排列。所有这样的排列的集合表示为 \(S_n\)。例如，对于集合 \(\{1, 2, 3\}\)，有 6 个排列，且 \(S_3 = \{123, 132, 213, 231, 312, 321\}\)。如果 \(\sigma \in S_n\)，则逆映射 \(\sigma^{-1} \in S_n\)，并且如果 \(\sigma, \tau \in S_n\)，则复合映射 \(\sigma \circ \tau \in S_n\)。此外，恒等映射 \(\sigma \circ \sigma^{-1} = 12 \cdots n \in S_n\)。在 \(\sigma\) 中的一个 _逆序_ 是指一对整数 \((i, j)\)，使得 \(i > j\)，但在 \(\sigma\) 中 \(i\) 在 \(j\) 之前出现。我们说 \(\sigma\) 是偶排列或奇排列，取决于 \(\sigma\) 中逆序的数量是偶数还是奇数。我们还定义
\(\text{sgn } \sigma = \begin{cases} 1 & \text{if } \sigma \text{ has even permutation} \\ -1 & \text{if } \sigma \text{ has odd permutation.} \end{cases}\)

等价地，我们可以根据将排列置于自然顺序所需的最小交换次数是偶数还是奇数来定义排列为偶排列或奇排列。可以证明，对于任何 \(n\)，\(S_n\) 中的一半排列是偶排列，另一半是奇排列。

有了这些术语，就有
\(|A| = \sum_{\sigma \in S_n} (\text{sgn } \sigma) a_{1\sigma(1)} a_{2\sigma(2)} \cdots a_{n\sigma(n)}.\) (3.5)

**示例 3.1.** 在 \(12 \cdots n\) 中，逆序为零（偶），而在 \(321\) 中，逆序为三（奇），因为有两个数（3 和 2）大于且在 1 之前，还有一个数（3）大于且在 2 之前。在集合 \(S_3\) 中，排列 \(123, 231, 312\) 是偶排列，而 \(321, 213, 132\) 是奇排列，因此从 (3.5) 得到展开式 (3.4)。在 \(4312 \in S_4\) 中，4 在 3、1 和 2 之前，3 在 1 和 2 之前；因此逆序为 5（奇）。

# **示例 3.2.**

从 (3.5) 可以立即得出，对于下三角和上三角矩阵 \(A\)，我们有

$$|A|=\begin{vmatrix}a_{11}&0&\cdots&0\\a_{21}&a_{22}&\cdots&0\\\vdots&\vdots&\ddots&\vdots\\a_{n1}&a_{n2}&\cdots&a_{nn}\end{vmatrix}=a_{11}a_{22}\cdots a_{nn}$$

和

$$|A|=\begin{vmatrix}a_{11}&a_{12}&\cdots&a_{1n}\\0&a_{22}&\cdots&a_{2n}\\\vdots&\vdots&\ddots&\vdots\\0&0&\cdots&a_{nn}\end{vmatrix}=a_{11}a_{22}\cdots a_{nn}.$$

因此，特别是，对于单位矩阵 \(|I|=1\)。同样，可以得出

$$\begin{vmatrix}0&0&\cdots&0&a_{1n}\\0&0&\cdots&a_{2,n-1}&a_{2n}\\\vdots&\vdots&&\vdots&\vdots\\0&a_{n-1,2}&\cdots&a_{n-1,n-1}&a_{n-1,n}\\a_{n1}&a_{n2}&\cdots&a_{n,n-1}&a_{nn}\end{vmatrix}$$

$$=(-1)^{n+1}a_{1n}(-1)^na_{2,n-1}\cdots(-1)^3a_{n-1,2}a_{n1}$$

$$=(-1)^{(n-1)(n+4)/2}a_{1n}a_{2,n-1}\cdots a_{n-1,2}a_{n1}$$

和

$$\begin{vmatrix}a_{11}&a_{12}&\cdots&a_{1,n-1}&a_{1n}\\a_{21}&a_{22}&\cdots&a_{2,n-1}&0\\\vdots&\vdots&&\vdots&\vdots\\a_{n-1,1}&a_{n-1,2}&\cdots&0&0\\a_{n1}&0&\cdots&0&0\end{vmatrix}$$

$$=(-1)^{(n-1)(n+4)/2}a_{1n}a_{2,n-1}\cdots a_{n-1,2}a_{n1}.$$

我们注意到，对于一般行列式，表示式 (3.5) 仅具有理论意义；实际上，它有 \(n!\) 项需要求和，每一项需要 \((n-1)\) 次乘法，因此计算 \(|A|\) 总共需要 \((n-1)\times n!\) 次乘法，对于较大的 \(n\) 来说，这是一项艰巨的任务。为了大大减少计算工作，我们通常使用行列式的以下基本性质。

- 1. 如果 \(A\) 的任何一行或一列只有零元素，则 \(|A|=0\)。
- 2. 如果 \(A\) 的两行（或两列）相等或具有常数比，则 \(|A|=0\)。
- 3. 如果 \(A\) 的任何两行（或两列）相邻交换，则新矩阵 \(A_1\) 的行列式为 \(-|A|\)。
- 4. 如果 \(A\) 的一行（或一列）乘以一个常数 \(\alpha\)，则新矩阵 \(A_1\) 的行列式为 \(\alpha|A|\)。
- 5. 如果将 \(A\) 的一行（或一列）的常数倍加到另一行（或一列），则新矩阵 \(A_1\) 的行列式不变。
- 6. \(|A^t|=|A|\)。
- 7. \(|AB|=|A||B|=|BA|\)。行列式的这个性质非常有趣。对于示例 2.2 中给出的矩阵 \(A\) 和 \(B\)，我们已经看到 \(AB\ne BA\)。然而，我们有

$$|A|=\begin{vmatrix}1&1&0\\-1&2&1\\0&0&2\end{vmatrix}=6,\qquad |B|=\begin{vmatrix}2&3&4\\1&2&3\\-1&1&2\end{vmatrix}=-1,$$

$$|AB|=\begin{vmatrix}3&5&7\\-1&2&4\\-2&2&4\end{vmatrix}=-6,\qquad |BA|=\begin{vmatrix}-1&8&11\\-1&5&8\\-2&1&5\end{vmatrix}=-6.$$

因此，\(|AB|=|A||B|=|BA|\)。
- 8. 如果 \(A\) 的一行或一列的每个元素表示为两个数之和，则 \(|A|\) 可以写成两个行列式之和。例如，

$$\begin{vmatrix}a_{11}&a_{12}+b_{12}&a_{13}\\a_{21}&a_{22}+b_{22}&a_{23}\\a_{31}&a_{32}+b_{32}&a_{33}\end{vmatrix}=\begin{vmatrix}a_{11}&a_{12}&a_{13}\\a_{21}&a_{22}&a_{23}\\a_{31}&a_{32}&a_{33}\end{vmatrix}+\begin{vmatrix}a_{11}&b_{12}&a_{13}\\a_{21}&b_{22}&a_{23}\\a_{31}&b_{32}&a_{33}\end{vmatrix}.$$
- 9. 如果 \(A\) 的元素是 \(x\) 的多项式函数，并且当 \(x=a\) 时，两行或两列变得相同，则 \(x-a\) 是 \(|A|\) 的一个因式。

虽然任何阶数的行列式计算的系统程序将在第 6 章中给出，但以下示例说明了上述性质的有用性。

# **示例 3.3.** 我们有

$$\Delta=\begin{vmatrix}11&3&4\\19&6&5\\21&7&8\end{vmatrix}=-\begin{vmatrix}3&11&4\\6&19&5\\7&21&8\end{vmatrix}=-\begin{vmatrix}-1&11&4\\-1&19&5\\-1&21&8\end{vmatrix}$$

$$=\begin{vmatrix}1&19&5\\-1&11&4\\-1&21&8\end{vmatrix}=\begin{vmatrix}1&19&5\\0&30&9\\0&40&13\end{vmatrix}=\begin{vmatrix}30&9\\40&13\end{vmatrix}$$

$$=30\times13-9\times40=390-360=30.$$

# 示例 3.4. 我们有

\(\Delta = \left|\begin{array}{ c c c }
a-b-c & 2a & 2a \\
2b & b-c-a & 2b \\
2c & 2c & c-a-b
\end{array}\right| = \left|\begin{array}{ c c c }
a+b+c & a+b+c & a+b+c \\
2b & b-c-a & 2b \\
2c & 2c & c-a-b
\end{array}\right|\)
\(= (a+b+c) \left|\begin{array}{ c c c }
1 & 1 & 1 \\
2b & b-c-a & 2b \\
2c & 2c & c-a-b
\end{array}\right|\)
\(= (a+b+c) \left|\begin{array}{ c c c }
1 & 0 & 0 \\
2b & -b-c-a & 0 \\
2c & 0 & -c-a-b
\end{array}\right|\)
\(= (a+b+c) \left|\begin{array}{ c c }
-b-c-a & 0 \\
0 & -c-a-b
\end{array}\right| = (a+b+c)^3.\)

# 示例 3.5. Vandermonde 矩阵

\(V = \left(\begin{array}{ c c c c }
1 & 1 & \cdots & 1 \\
x_1 & x_2 & \cdots & x_n \\
x_1^2 & x_2^2 & \cdots & x_n^2 \\
\cdots &  &  &  \\
x_1^{n-1} & x_2^{n-1} & \cdots & x_n^{n-1}
\end{array}\right)\)

在多项式插值理论中起着重要作用。通过归纳法，我们将证明
\(|V| = \prod_{1 \leq i < j \leq n} (x_j - x_i).\)

确实，我们有
\(\left|\begin{array}{ c c }
1 & 1 \\
x_1 & x_2
\end{array}\right| = (x_2 - x_1)\)

和
\(|V| = \left|\begin{array}{ c c c c }
1 & 1 & \cdots & 1 \\
0 & x_2 - x_1 & \cdots & x_n - x_1 \\
0 & x_2^2 - x_2x_1 & \cdots & x_n^2 - x_nx_1 \\
\cdots &  &  &  \\
0 & x_2^{n-1} - x_2^{n-2}x_1 & \cdots & x_n^{n-1} - x_n^{n-2}x_1
\end{array}\right|\)
\(= \prod_{j=2}^n (x_j - x_1) \left|\begin{array}{ c c c c }
1 & 1 & \cdots & 1 \\
x_2 & x_3 & \cdots & x_n \\
x_2^2 & x_3^2 & \cdots & x_n^2 \\
\cdots &  &  &  \\
x_2^{n-2} & x_3^{n-2} & \cdots & x_n^{n-2}
\end{array}\right|\)
\(= \prod_{j=2}^n (x_j - x_1) \prod_{2 \leq i < j \leq n} (x_j - x_i) = \prod_{1 \leq i < j \leq n} (x_j - x_i).\)

