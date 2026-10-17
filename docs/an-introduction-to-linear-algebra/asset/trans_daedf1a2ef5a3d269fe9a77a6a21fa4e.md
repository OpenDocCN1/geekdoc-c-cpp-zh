

## 第 12 章

## 线性映射

在本章中，我们将一些早期的结果推广到两个向量空间之间的一般线性映射。这些映射具有普遍的意义和广泛的适用性，特别是因为它们保持了线性组合的加法结构。此外，通常可以用线性映射来近似任意映射，而线性映射可以相当容易地处理。

在接下来的内容中，除非另有说明，我们将考虑在同一个域 F 上的有限维向量空间 V 和 W。一个映射 \(L: V \rightarrow W\) 称为线性映射（也称为线性变换或线性算子），当且仅当它满足以下两个条件：

- 对于每一对向量 \(u, v \in V\)，\(L(u+v) = L(u) + L(v)\)。
- 对于任何标量 \(c \in F\) 和向量 \(u \in V\)，\(L(cu) = cL(u)\)。

因此，如果映射 L 保持了向量空间的两个基本运算，即向量加法和标量乘法，则它是线性的。特别是，第二个条件意味着 \(L(0) = 0\)。显然，上述两个条件可以统一如下：\(L: V \rightarrow W\) 是线性映射，当且仅当对于任何一对标量 \(\alpha, \beta \in F\) 和任何一对向量 \(u, v \in V\)，\(L(\alpha u + \beta v) = \alpha L(u) + \beta L(v)\)。对该条件的直接推广给出 \(L(c_1u^1 + \cdots + c_nu^n) = c_1L(u^1) + \cdots + c_nL(u^n)\)，对所有 \(c_i \in F\) 和 \(u^i \in V\) 成立。如果 \(W = V\)，则 L 被称为在 V 上的线性映射。

**Example 12.1.** 对于给定的矩阵 \(A \in M^{m \times n}\)，由 \(L_A(u) = Au\) 定义的映射 \(L_A: F^n \rightarrow F^m\) 是线性的。确实，根据矩阵的性质，对于所有 \(u, v \in F^n\) 和 \(c, d \in F\)，我们有

\(L_A(cu + dv) = A(cu + dv) = cAu + dAv = cL_A(u) + dL_A(v).\)

特别是，当

\(A = \begin{pmatrix} \cos \phi & -\sin \phi \\ \sin \phi & \cos \phi \end{pmatrix}\)

时，映射 \(L_A: R^2 \rightarrow R^2\) 将 xy 平面旋转角度 \(\phi\)。

**Example 12.2.** 考虑 V 作为区间 J 上所有实可积函数组成的无穷维空间。那么，\(L = \int_J\) 是一个线性映射。

确实，对于所有 \(\alpha, \beta \in R\) 和 \(u, v \in V\)，我们有

\(L(\alpha u + \beta v) = \int_J (\alpha u(x) + \beta v(x)) dx = \alpha \int_J u(x) dx + \beta \int_J v(x) dx = \alpha L(u) + \beta L(v)\)。

类似地，在区间 J 上所有实可微函数组成的空间 \(V\) 中，映射 \(L = d/dx\) 是线性的。

**Example 12.3.** 由 \(L(x, y, z) = (x, y, 0)^t\) 定义的投影映射 \(L: R^3 \rightarrow R^2\) 是线性的。然而，由 \(L(x, y, z) = (x+1, y+2, z+3)^t\) 定义的平移映射 \(L: R^3 \rightarrow R^3\) 不是线性的（非线性），因为 \(L(0) = L(0, 0, 0) = (1, 2, 3)^t \neq 0\)。由 \(L(x, y, z) = (|x|, yz)^t\) 定义的映射 \(L: R^3 \rightarrow R^2\) 也是非线性的。

线性映射 _zero_（对于每个 \(u \in V\)，\(L(u) = 0\)）和 _identity_（对于每个 \(u \in V\)，\(L(u) = u\)）分别记为 0 和 _I_。

**Theorem 12.1.** 设 \(\{u^1, \cdots, u^n\}\) 是 \(V\) 的一组基。那么，对于任何向量 \(w^1, \cdots, w^n \in W\)，存在唯一的线性映射 \(L: V \rightarrow W\)，使得 \(L(u^i) = w^i\)，\(i = 1, \cdots, n\)。

**Proof.** 设 \(u \in V\)。由于 \(\{u^1, \cdots, u^n\}\) 是 \(V\) 的一组基，存在唯一的标量 \(c_1, \cdots, c_n\) 使得 \(u = c_1 u^1 + \cdots + c_n u^n\)。我们声明 \(L(u) = c_1 w^1 + \cdots + c_n w^n\) 是所需的映射。为此，首先我们注意到 _L_ 是定义良好的，因为 \(c_i\)，\(i = 1, \cdots, n\) 是唯一的，并且由于 \(u^i = 0u^1 + \cdots + 0u^{i-1} + 1u^i + 0u^{i+1} + \cdots + 0u^n\)，我们有 \(L(u^i) = w^i\)，\(i = 1, \cdots, n\)。接下来，为了证明 _L_ 是线性的，设 \(v = b_1 u^1 + \cdots + b_n u^n \in V\) 和 \(k \in F\)，那么由于 \(u+v = (c_1+b_1)u^1 + \cdots + (c_n+b_n)u^n\) 和 \(ku = (kc_1)u^1 + \cdots + (kc_n)u^n\)，我们有 \(L(u+v) = (c_1+b_1)w^1 + \cdots + (c_n+b_n)w^n\) 和 \(L(ku) = (kc_1)w^1 + \cdots + (kc_n)w^n\)，因此得出 \(L(u+v) = L(u) + L(v)\) 和 \(L(ku) = kL(u)\)。最后，为了证明 _L_ 的唯一性，设 \(\tilde{L}: V \rightarrow W\) 是另一个线性映射，使得 \(\tilde{L}(u^i) = w^i\)，\(i = 1, \cdots, n\)。那么，对于每个 \(u \in V\)，我们有 \(\tilde{L}(u) = \tilde{L}(c_1 u^1 + \cdots + c_n u^n) = c_1 \tilde{L}(u^1) + \cdots + c_n \tilde{L}(u^n) = c_1 w^1 + \cdots + c_n w^n = L(u)\)，这意味着 \(L = \tilde{L}\)。

现在我们将第 10 章中给出的同构定义推广到一般向量空间。空间 _V_ 和 _W_ 被称为 _同构_，记作 \(V \simeq W\)，如果存在一个一对一且满射的线性映射 \(L: V \rightarrow W\)。这个映射 _L_ 被称为 _V_ 和 _W_ 之间的 _同构_。显然，\(\simeq\) 是一个等价关系，即，1. \(V \simeq V\)。2. 如果 \(U \simeq V\)，则 \(V \simeq U\)。3. 如果 \(U \simeq V\) 和 \(V \simeq W\)，则 \(U \simeq W\)。

**Theorem 12.2.** \(V \simeq W\) 当且仅当 \(\dim V = \dim W\)。

**Proof.** 设 _V_ 和 _W_ 是 _n_ 维向量空间。那么，根据第 10 章，\(V \simeq F^n\) 和 \(W \simeq F^n\)。现在，\(V \simeq W\) 由 \(\simeq\) 是等价关系这一事实得出。反之，如果 \(V \simeq W\)，则存在一个同构 \(L: V \rightarrow W\)。假设 \(\dim V = n\)，并设 \(S = \{u^1, \cdots, u^n\}\)

exists \(0 \neq u \in V\) such that \(L(u) = 0\). Thus, \(L\) is nonsingular if and only if \(\mathcal{N}(L) = \{0\}\).

**Theorem 12.3.** 设 \(L: V \rightarrow W\) 是一个线性映射。那么，\(L\) 是一对一的当且仅当 \(\mathcal{N}(L) = \{0\}\)，即，\(L\) 是非奇异的。

Proof. 由于 \(L(0) = 0\)，可知 \(0 \in \mathcal{N}(L)\)。如果 \(L\) 是一对一的，那么 \(0 \in V\) 是唯一映射到 \(0 \in W\) 的向量。因此，我们有 \(\mathcal{N}(L) = \{0\}\)。反之，设 \(\mathcal{N}(L) = \{0\}\)。如果对于 \(u, v \in V\) 有 \(L(u) = L(v)\)，那么 \(L(u - v) = 0\)。但这意味着 \(u - v = 0\)，即 \(u = v\)。因此，\(L\) 是一对一的。

**Corollary 12.1.** 方程 \(L(u) = w\) 最多有一个解当且仅当 \(\mathcal{N}(L) = \{0\}\)。

**Corollary 12.2.** 设 \(A\) 是一个 \(m \times n\) 矩阵，并定义 \(T: R^n \rightarrow R^m\) 为 \(Tx = Ax\)。那么，\(T\) 是一对一的当且仅当 \(A\) 的列线性无关。

**Example 12.5.** 由 \(L(x, y) = (2x + y, x + 2y)^t\) 定义的映射 \(L: R^2 \rightarrow R^2\) 是非奇异的，即一对一的。为此，只需证明 \(\mathcal{N}(L) = \{0\}\)，即 \((2x + y, x + 2y)^t = (0, 0)^t\) 的唯一解，这等价于方程组 \(2x + y = 0\)、\(x + 2y = 0\) 的零解。然而，由 \(\tilde{L}(x, y, z, w) = (x + 3y + 4z + 2w, 3x - 5y + 2z + 2w, 2x - y + 3z + 2w)^t\) 定义的映射 \(\tilde{L}: R^4 \rightarrow R^3\) 是奇异的。确实，\((1, \frac{7}{13}, -\frac{15}{13}, 1)^t \in \mathcal{N}(\tilde{L})\)。

**Theorem 12.4.** 设 \(L: V \rightarrow W\) 是一个线性映射。那么，\(\dim V = \dim R(L) + \dim \mathcal{N}(L)\)。

Proof. 假设 \(\dim \mathcal{N}(L) = r\) 且 \(\{u^1, \cdots, u^r\}\) 是 \(\mathcal{N}(L)\) 的一组基。进一步假设 \(\dim R(L) = s\) 且 \(\{w^1, \cdots, w^s\}\) 是 \(R(L)\) 的一组基。由于 \(L\) 是线性映射，对于每个 \(w^j \in R(L)\)，存在 \(v^j \in V\) 使得 \(L(v^j) = w^j\)。只需证明 \(S = \{u^1, \cdots, u^r, v^1, \cdots, v^s\}\) 是 \(V\) 的一组基。为此，设 \(u \in V\)。那么，由于 \(L(u) \in R(L)\)，存在标量 \(c_j\) 使得 \(L(u) = c_1 w^1 + \cdots + c_s w^s\)。设 \(\tilde{u} = c_1 v^1 + \cdots + c_s v^s - u\)。那么，可得

\[
\begin{array}{ c c c }
L(\tilde{u}) & = & L(c_1 v^1 + \cdots + c_s v^s - u) \\
 & = & c_1 L(v^1) + \cdots + c_s L(v^s) - L(u) \\
 & = & c_1 w^1 + \cdots + c_s w^s - L(u) = 0.
\end{array}
\]

但这意味着 \(\tilde{u} \in \mathcal{N}(L)\)，因此存在标量 \(a_i\) 使得

\(\tilde{u} = a_1 u^1 + \cdots + a_r u^r = c_1 v^1 + \cdots + c_s v^s - u,\)

这给出

\(u = c_1 v^1 + \cdots + c_s v^s - a_1 u^1 + \cdots - a_r u^r\)

因此集合 \(S\) 覆盖空间 \(V\)。为了证明 \(S\) 是线性无关的，设

\(x_1 u^1 + \cdots + x_r u^r + y_1 v^1 + \cdots + y_s v^s = 0,\) (12.1)

