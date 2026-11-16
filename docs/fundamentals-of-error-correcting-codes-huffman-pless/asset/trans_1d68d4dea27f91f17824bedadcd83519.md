

我们首先在 \(\mathbb{R}^n\) 中定义一个格。设 \(\mathbf{v}_1, \dots, \mathbf{v}_n\) 为 \(\mathbb{R}^n\) 中的 \(n\) 个线性无关向量，其中 \(\mathbf{v}_i = (v_{i,1}, v_{i,2}, \ldots, v_{i,n})\)。以基 \(\{\mathbf{v}_1, \dots, \mathbf{v}_n\}\) 的格 \(\Lambda\) 是 \(\mathbf{v}_1, \dots, \mathbf{v}_n\) 的所有整数组成的集合；这些基向量的整数组合是格上的 *点*。因此

\(\Lambda = \{z_1 \mathbf{v}_1 + z_2 \mathbf{v}_2 + \cdots + z_n \mathbf{v}_n \mid z_i \in \mathbb{Z}, 1 \le i \le n\}.\)

矩阵

\(M = \begin{bmatrix} v_{1,1} & v_{1,2} & \cdots & v_{1,n} \\ v_{2,1} & v_{2,2} & \cdots & v_{2,n} \\ \vdots & & & \\ v_{n,1} & v_{n,2} & \cdots & v_{n,n} \end{bmatrix}\)

被称为 \(\Lambda\) 的 *生成矩阵*；因此 \(\Lambda = \{\mathbf{z} M \mid \mathbf{z} \in \mathbb{Z}^n\}\)。\(n \times n\) 矩阵

\(A = M M^T\)

被称为 \(\Lambda\) 的 *格拉姆矩阵*；其 \((i, j)\)-项是 \(\mathbf{v}_i\) 和 \(\mathbf{v}_j\) 的（普通）内积（在实数域上）。格 \(\Lambda\) 的 *行列式* 或 *判别式* 是

\(\det \Lambda = \det A = (\det M)^2.\)

该行列式具有自然的几何意义：\(\det \Lambda\) 是 \(\Lambda\) 的 *基本平行多面体* 的体积，即区域

\(\{a_1 \mathbf{v}_1 + \cdots + a_n \mathbf{v}_n \mid 0 \le a_i < 1, a_i \in \mathbb{R} \text{ 对所有 } 1 \le i \le n\}.\)

### **示例 10.6.1**
以基 \(\mathbf{v}_1 = (1, 0)\) 和 \(\mathbf{v}_2 = (0, 1)\) 的格 \(\mathbb{Z}^2\) 的生成矩阵和格拉姆矩阵均等于单位矩阵 \(I_2\)。此外，\(\det \mathbb{Z}^2 = 1\)。该格显然是平面上所有整数坐标点的集合。

### **示例 10.6.2**
设 \(\mathbf{v}_1 = (\sqrt{2}, 0)\) 和 \(\mathbf{v}_2 = (\sqrt{2}/2, \sqrt{6}/2)\)。如图 10.3 所示，以基 \(\{\mathbf{v}_1, \mathbf{v}_2\}\) 的格 \(\Lambda_2\) 的生成矩阵和格拉姆矩阵为

\(M_2 = \begin{bmatrix} \sqrt{2} & 0 \\ \sqrt{2}/2 & \sqrt{6}/2 \end{bmatrix} \text{ 和 } A_2 = \begin{bmatrix} 2 & 1 \\ 1 & 2 \end{bmatrix}.\)

该格常被称为 *平面六角格*；其行列式为 3。

### **练习 604**
设 \(\Lambda_2\) 为示例 10.6.2 中的格。完成以下任务：(a) 在图 10.3 中绘制 \(\Lambda_2\) 的基本区域。(b) 从几何上验证基本区域的面积为 3。

如果一个格的格拉姆矩阵具有整数项，则任何两个格点之间的内积始终为整数值，且该格称为 *整格*。

示例 10.6.1 和 10.6.2 中定义的 \(\mathbb{Z}^2\) 和平面六角格均为整格。

请注意，在任何格中，我们都可以用同一标量重新缩放所有基向量；这不会改变格的“几何”，即 \(\mathbb{R}^n\) 中格点的相对位置，但可能会改变其他属性，例如格的整性或基本区域的大小（\(\det \Lambda\)）。

如果将 \(\Lambda\) 的每个基向量乘以标量 \(c\)，则得到的

![](img/0af7e79235839ec0eb8bcf8d229f37d4_442_0.png)

图 10.3 \(\mathbb{R}^2\) 中的平面六角格。

格记为 \(c\Lambda\)。\(c\Lambda\) 的生成矩阵为 \(cM\)，格拉姆矩阵为 \(c^2A\)。如果我们旋转或反射 \(\Lambda\)，也本质上得到相同的格。这引出了等价概念：生成矩阵为 \(M\) 的格 \(\Lambda\) 与格 \(\Lambda'\) *等价*，当且仅当存在标量 \(c\)、具有整数项且 \(\det U = \pm 1\) 的矩阵 \(U\)，以及具有实数项且 \(BB^T = I_n\) 的矩阵 \(B\)，使得 \(cUMB\) 是 \(\Lambda'\) 的生成矩阵。（矩阵 \(B\) 作为一系列旋转，矩阵 \(U\) 作为一系列反射。）通常，在格的等价类中选择代表格时，人们试图选择一个整格且行列式尽可能小的代表格。

使用 \(\mathbb{R}^n\) 中的普通内积，我们可以定义 \(\Lambda\) 的 *对偶格* \(\Lambda^*\) 为 \(\mathbb{R}^n\) 中所有与 \(\Lambda\) 中每个格点的内积为整数的向量集合；即，

\[
\Lambda^* = \{ \mathbf{y} \in \mathbb{R}^n \mid \mathbf{x} \cdot \mathbf{y} \in \mathbb{Z} \text{ 对所有 } \mathbf{x} \in \Lambda \}.
\]

如果 \(\Lambda = \Lambda^*\)，则整格 \(\Lambda\) 称为 *一模格* 或 *自对偶*。

### **定理 10.6.3**
设 \(\Lambda\) 为 \(\mathbb{R}^n\) 中的格，具有基 \(\mathbf{v}_1, \dots, \mathbf{v}_n\)、生成矩阵 \(M\) 和格拉姆矩阵 \(A\)。以下结论成立：

- (i) \(\Lambda^* = \{ \mathbf{y} \in \mathbb{R}^n \mid \mathbf{v}_i \cdot \mathbf{y} \in \mathbb{Z} \text{ 对所有 } 1 \le i \le n \} = \{ \mathbf{y} \in \mathbb{R}^n \mid \mathbf{y} M^T \in \mathbb{Z}^n \}\)。
- (ii) \(\Lambda^*\) 的生成矩阵是 \((M^{-1})^T\)。
- (iii) \(\Lambda^*\) 的格拉姆矩阵是 \(A^{-1}\)。
- (iv) \(\det \Lambda^* = 1/\det \Lambda\)。
- (v) \(\Lambda\) 是整格当且仅当 \(\Lambda \subseteq \Lambda^*\)。
- (vi) 如果 \(\Lambda\) 是整格，则
  \[
  \Lambda \subseteq \Lambda^* \subseteq \frac{1}{\det \Lambda} \Lambda = (\det \Lambda^*)\Lambda.
  \]
- (vii) 如果 \(\Lambda\) 是整格，则 \(\Lambda\) 是一模格当且仅当 \(\det \Lambda = \pm 1\)。

证明：我们将 (i) 和 (v) 的证明留作练习 605。对于 (ii)，设 \(\mathbf{w}_1, \dots, \mathbf{w}_n\) 为 \((M^{-1})^T\) 的行。那么 \((\mathbf{w}_1, \dots, \mathbf{w}_n)\) 是 \(\mathbb{R}^n\) 的一组基，且由于 \((M^{-1})^T M^T = (MM^{-1})^T = I_n\),

\[
\mathbf{w}_i \cdot \mathbf{v}_j = \begin{cases} 1 & \text{如果 } i = j, \\ 0 & \text{如果 } i \neq j. \end{cases}
\] (10.10)

特别是，由 (i) 可知 \(\{\mathbf{w}_1, \dots, \mathbf{w}_n\} \subseteq \Lambda^*\)。设 \(\mathbf{w} \in \Lambda^*\)。由于 \(\{\mathbf{w}_1, \dots, \mathbf{w}_n\}\) 是 \(\mathbb{R}^n\) 的一组基，故 \(\mathbf{w} = a_1 \mathbf{w}_1 + \cdots + a_n \mathbf{w}_n\)。因为 \(\mathbf{w} \in \Lambda^*\)，所以 \(\mathbf{w} \cdot \mathbf{v}_j \in \mathbb{Z}\)。但由 (10.10) 可知，对于 \(1 \le j \le n\)，\(\mathbf{w} \cdot \mathbf{v}_j = a_j\)。因此 \(a_j \in \mathbb{Z}\)，且 (ii) 成立。\(\Lambda^*\) 的格拉姆矩阵是 \((M^{-1})^T M^{-1} = (MM^T)^{-1} = A^{-1}\)，从而得到 (iii)。因此

\[
\det \Lambda^* = \det(A^{-1}) = \frac{1}{\det A} = \frac{1}{\det \Lambda}.
\]

从而得到 (iv)。

对于 (vi)，我们只需根据 (iv) 和 (v) 证明第二个包含关系。设 \(\mathbf{y} \in \Lambda^*\)。由 (i) 可知 \(\mathbf{y} M^T \in \mathbb{Z}^n\)，因此存在 \(\mathbf{z} \in \mathbb{Z}^n\) 使得 \(\mathbf{y} = \mathbf{z}(M^T)^{-1} = \mathbf{z} A^{-1} M\)。但 \(A^{-1} = (\det \Lambda)^{-1} \text{adj}(A)\)，其中 \(\text{adj}(A)\) 是 \(A\) 的伴随矩阵。因此

\[
\mathbf{y} = \mathbf{z}(\det \Lambda)^{-1} \text{adj}(A) M = \mathbf{z}'(\det \Lambda)^{-1} M,
\]

其中 \(\mathbf{z}' = \mathbf{z} \text{adj}(A) \in \mathbb{Z}^n\)，因为 \(\text{adj}(A)\) 具有整数项（由 \(\Lambda\) 是整格可知）。因此 \(\mathbf{y} \in (\det \Lambda)^{-1} \Lambda\)，验证了 (vi)。

最后，由 (vi) 可知，如果 \(\Lambda\) 是一模格，则 \(\det \Lambda = \det \Lambda^* = 1/(\det \Lambda)\)，从而 \(\det \Lambda = \pm 1\)。反之，如果 \(\det \Lambda = \pm 1\) 且 \(\Lambda\) 是整格，则 (vi) 表明 \(\Lambda \subseteq \Lambda^* \subseteq \pm \Lambda\)，且显然 \(\Lambda = \pm \Lambda\)，故 \(\Lambda = \Lambda^*\)。

### **练习 605**
证明定理 10.6.3 的 (i) 和 (v)。$\blacklozenge$

### **练习 606**
证明如果 \(\Lambda\) 是一个格，则 \(\Lambda = c\Lambda\) 当且仅当 \(c = \pm 1\)。$\blacklozenge$

在整格 \(\Lambda\) 中，对于所有 \(\mathbf{x} \in \Lambda\)，\(\mathbf{x} \cdot \mathbf{x}\) 都是整数。如果对于所有 \(\mathbf{x} \in \Lambda\)，\(\mathbf{x} \cdot \mathbf{x}\) 都是偶整数，则整格称为 *偶格*。特别是，格拉姆矩阵在其主对角线上具有偶数项。不是偶格的整格称为 *奇格*。如果一个格是偶一模格，则称为 *II型*；如果是奇一模格，则称为 *I型*。对于任意维度 \(n\) 都存在 I型格；然而，II型格存在当且仅当 \(n \equiv 0 (\text{mod } 8)\)。一模格已按等价关系分类至维度 25；请注意，I型码已分类至长度 30，II型码已分类至长度 32。

### **练习 607**
证明示例 10.6.1 中的格 \(\mathbb{Z}^2\) 是 I型格，而示例 10.6.2 中的 \(\Lambda_2\) 不是一模格。$\blacklozenge$

类似于测量码字之间的汉明距离，我们测量

