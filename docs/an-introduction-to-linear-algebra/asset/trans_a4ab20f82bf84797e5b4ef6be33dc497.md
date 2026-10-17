

但 \( BA \) 可能未定义。此外，\( AB \) 和 \( BA \) 可能都存在，但可能不相等。

### 示例 2.1

对于矩阵

\[
A = \begin{pmatrix} 0 & 1 & 2 \\ 1 & 2 & 3 \\ 2 & 3 & 4 \end{pmatrix}, \quad B = \begin{pmatrix} 1 & -2 \\ -1 & 0 \\ 2 & -1 \end{pmatrix},
\]

我们有

\[
AB = \begin{pmatrix} 3 & -2 \\ 5 & -5 \\ 7 & -8 \end{pmatrix}.
\]

然而，\( BA \) 未定义。

### 示例 2.2

对于矩阵

\[
A = \begin{pmatrix} 1 & 1 & 0 \\ -1 & 2 & 1 \\ 0 & 0 & 2 \end{pmatrix}, \quad B = \begin{pmatrix} 2 & 3 & 4 \\ 1 & 2 & 3 \\ -1 & 1 & 2 \end{pmatrix},
\]

我们有

\[
AB = \begin{pmatrix} 3 & 5 & 7 \\ -1 & 2 & 4 \\ -2 & 2 & 4 \end{pmatrix}, \quad BA = \begin{pmatrix} -1 & 8 & 11 \\ -1 & 5 & 8 \\ -2 & 1 & 5 \end{pmatrix}.
\]

因此，\( AB \neq BA \)。

### 示例 2.3

对于矩阵

\[
A = \begin{pmatrix} 1 & 1 \\ 1 & 1 \end{pmatrix}, \quad B = \begin{pmatrix} 1 & -1 \\ -1 & 1 \end{pmatrix},
\]

我们有 \( AB = 0 \)。因此 \( AB = 0 \) 不意味着 \( A \) 或 \( B \) 是零矩阵。

对于矩阵乘法，以下性质成立：

- 1. \( A(BC) = (AB)C \)，结合律
- 2. \( A(B \pm C) = AB \pm AC \) 和 \( (A \pm B)C = AC \pm BC \)，分配律
- 3. \( AI = A \) 和 \( IA = A \)
- 4. \( k(AB) = (kA)B = A(kB), \ k \in F \)
- 5. \( A0 = 0 \) 和 \( 0B = 0 \)。

如果 \( A \) 是一个 \( n \times n \) 矩阵，则乘积 \( AA \) 记为 \( A^2 \)。一般来说，\( m \) 次乘积 \( AA \cdots A = A^{m-1}A = A^m \) 且 \( A^0 = I \)。另外，如果 \( m \) 和 \( p \) 是正整数，则根据结合律，我们有 \( A^m A^p = A^{m+p} \)。特别是，\( I = I^2 = I^3 = \cdots \)。此外，如果 \( A \) 是对角线元素为 \( (\lambda_1,\ldots,\lambda_n) \) 的对角矩阵，则 \( A^m \) 也是对角线元素为 \( (\lambda_1^m,\ldots,\lambda_n^m) \) 的对角矩阵。而且，如果 \( A \) 是上（下）三角矩阵，则 \( A^m \) 也是上（下）三角矩阵。矩阵 \( A \) 的多项式也已定义。事实上，如果 \( P_{m-1}(x)=\sum_{i=0}^{m-1}a_i x^i\in P_m(F) \)，则 \( P_{m-1}(A)=\sum_{i=0}^{m-1}a_iA^i \)。显然，\( P_{m-1}(A) \) 是一个方阵。如果 \( P_{m-1}(A) \) 是零矩阵，则 \( A \) 被称为 \( P_{m-1}(x) \) 的零点或根。

一个 \( m\times n \) 矩阵 \( A=(a_{ij}) \) 的转置，记为 \( A^t \)，是一个 \( n\times m \) 矩阵，通过交换 \( A \) 的行和列得到，即 \( A^t=(a_{ji}) \)。因此，对于示例 2.1 中的矩阵，

![](img/049a5f7ee46d1463ca7feb5fdb0d0a78_28_0.png)

由此可知，对于列向量

![](img/049a5f7ee46d1463ca7feb5fdb0d0a78_28_1.png)

\( a^t \) 是行向量 \( a^t=(a_1,\ldots,a_n) \)，反之亦然。

对于矩阵的转置，以下成立：

- 1. \( (A+B)^t=A^t+B^t \)
- 2. \( (cA)^t=cA^t \)，其中 \( c \) 是标量
- 3. \( (A^t)^t=A \)
- 4. \( (AB)^t=B^tA^t \)（注意顺序颠倒）。

显然，方阵 \( A \) 是对称矩阵当且仅当 \( A=A^t \)，是反对称矩阵当且仅当 \( A=-A^t \)。如果 \( A \) 是对称（反对称）矩阵，则显然 \( A^t \) 是对称（反对称）矩阵。

方阵的迹，记为 \( \operatorname{tr}(A) \)，是对角线元素之和，即 \( \operatorname{tr}(A)=a_{11}+a_{22}+\cdots+a_{nn} \)。因此，对于 (2.1) 中的矩阵 \( A \)，其迹为 \( 1+3+5=9 \)。对于方阵的迹，以下成立：

- 1. \( \operatorname{tr}(A+B)=\operatorname{tr}(A)+\operatorname{tr}(B) \)
- 2. \( \operatorname{tr}(A)=\operatorname{tr}(A^t) \)
- 3. \( \operatorname{tr}(cA)=c\operatorname{tr}(A) \)，其中 \( c \) 是标量
- 4. \( \operatorname{tr}(AB)=\operatorname{tr}(BA) \)。

最后，我们指出，特别是为了计算目的，矩阵 \( A \) 可以通过在其行和列之间绘制水平和垂直线分割为称为块或单元的子矩阵。这种分割不是唯一的；例如，矩阵

\[
A=\begin{pmatrix}1&0&7&3&4\\3&5&7&1&0\\0&4&3&2&7\\6&3&9&0&2\end{pmatrix}
\]

可以分割为

\[
\begin{pmatrix}1&0&7&3&4\\3&5&7&1&0\\0&4&3&2&7\\6&3&9&0&2\end{pmatrix}
=
\begin{pmatrix}A_{11}&A_{12}\\A_{21}&A_{22}\end{pmatrix},
\]

或

\[
\begin{pmatrix}1&0&7&3&4\\3&5&7&1&0\\0&4&3&2&7\\6&3&9&0&2\end{pmatrix}
=
\begin{pmatrix}A_{11}&A_{12}&A_{13}\\A_{21}&A_{22}&A_{23}\\A_{31}&A_{32}&A_{33}\end{pmatrix}.
\]

如果 \( A=(A_{ij})_{r\times s} \)，\( B=(B_{ij})_{s\times t} \) 且块 \( A_{ij},B_{ij} \) 可兼容，则 \( AB=(C_{ij})_{r\times t} \)，其中

\[
C_{ij}=\sum_{k=1}^{s}A_{ik}B_{kj}.
\]

在分块矩阵中，块可以被视为数字，以便执行矩阵之间的基本运算（具有正确阶数的块）。

## 问题

**2.1.** 将以下矩阵表示为一个下三角矩阵和一个主对角线为零的上三角矩阵之和

\[
A=\begin{pmatrix}1&3&5\\2&4&7\\6&-5&9\end{pmatrix}.
\]

**2.2.** 设 \( A=(a_{ij}), B=(b_{ij})\in M^{n\times n} \) 为上三角矩阵。证明 \( AB \) 是一个上三角矩阵，其对角线元素为 \( a_{ii}b_{ii} \)，\( i=1,\ldots,n \)。

**2.3.** 对于矩阵

\[
A=\begin{pmatrix}-1&2&4\\3&6&5\\6&5&8\end{pmatrix},\qquad B=\begin{pmatrix}3&-6&-5\\1&3&5\\3&5&7\end{pmatrix}
\]

## 答案或提示

- **2.1.** \( U=\begin{pmatrix}0&3&5\\0&0&7\\0&0&0\end{pmatrix},\quad L=\begin{pmatrix}1&0&0\\2&4&0\\6&-5&9\end{pmatrix}.\)
- **2.2.** \( AB=C=(c_{ij}) \)，如果 \( i>j \) 则 \( c_{ij}=0 \)，如果 \( j\ge i \) 则 \( c_{ij}=\sum_{k=i}^{j}a_{ik}b_{kj} \)。
- **2.3.** 直接计算。
- **2.4.** 直接计算。
- **2.5.** 直接计算。
- **2.6.** \( (A+B)^2=(A+B)(A+B)=A^2+AB+BA+B^2. \)
- **2.7.** 考虑 \( A=\begin{pmatrix}1&1\\1&1\end{pmatrix} \)。则 \( 1\cdot A=\begin{pmatrix}1&0\\0&1\end{pmatrix}\ne A \)。因此，B10 被违反。
- **2.8.** \( \begin{pmatrix}a&b\\c&d\end{pmatrix}=\begin{pmatrix}a&0\\0&0\end{pmatrix}+\begin{pmatrix}0&b\\0&0\end{pmatrix}+\begin{pmatrix}0&0\\c&0\end{pmatrix}+\begin{pmatrix}0&0\\0&d\end{pmatrix}.\)
- **2.9.** 设 \( C,D\in S \) 和 \( \alpha,\beta\in \mathbb{R} \)。则，\( (\alpha C+\beta D)B=\alpha CB+\beta DB=\alpha BC+\beta BD=B(\alpha C+\beta D). \)
- **2.10.** 使用数学归纳法原理。
- **2.11.** 设 \( A=(a_{ij})_{m\times n} \)，\( B=(b_{ij})_{n\times p} \)，\( C=(c_{ij})_{p\times r} \)，则 \( BC \) 和 \( AB \) 分别是 \( n\times r \) 和 \( m\times p \) 矩阵，\( A(BC) \) 的 \( ij \)-th 元素为
    
    \[
    \sum_{\mu=1}^{n}a_{i\mu}\left(\sum_{\nu=1}^{p}b_{\mu\nu}c_{\nu j}\right)=\sum_{\mu=1}^{n}\sum_{\nu=1}^{p}a_{i\mu}b_{\mu\nu}c_{\nu j}.
    \]
    
    同样，\( (AB)C \) 的 \( ij \)-th 元素为
    
    \[
    \sum_{\nu=1}^{p}\left(\sum_{\mu=1}^{n}a_{i\mu}b_{\mu\nu}\right)c_{\nu j}=\sum_{\nu=1}^{p}\sum_{\mu=1}^{n}a_{i\mu}b_{\mu\nu}c_{\nu j}.
    \]
- **2.12.** 类似于问题 2.11。
- **2.13.** (iv)
    
    \[
    (AB)^H_{ij} = \overline{(AB)_{ji}} = \overline{\sum_{k=1}^{n}a_{jk}b_{ki}}
    = \sum_{k=1}^{n}\overline{a_{jk}}\,\overline{b_{ki}}
    = (\overline{B}^{\,t}\overline{A}^{\,t})_{ij} = (B^H A^H)_{ij}.
    \]
- **2.14.** 赫米特矩阵：
    
    \[
    \begin{pmatrix}1&i&2-i\\-i&2&5\\2+i&5&3\end{pmatrix}
    \]
    
    反赫米特矩阵：
    
    \[
    \begin{pmatrix}i&i&2+i\\i&2i&5\\-2+i&-5&5i\end{pmatrix}
    \]
    
    正规矩阵：
    
    \[
    \begin{pmatrix}-i&-2-i\\2-i&-3i\end{pmatrix}.
    \]
- **2.15.** (i) 设 \( AB \) 为赫米特矩阵。则，\( AB=(AB)^H=B^HA^H=BA \)，即 \( A,B \) 交换。反之，设 \( A,B \) 交换。则，\( AB=BA=B^HA^H=(AB)^H \)，即 \( AB \) 是赫米特矩阵。
    
    (vii) \( A = \frac{1}{2}(A - A^H) + \frac{1}{2}(A + A^H) \)。
- **2.16.** 设 \( A = \begin{pmatrix} 1+i & 2 \\ 1 & -i \end{pmatrix} \)，\( B = \begin{pmatrix} 2i & 1 \\ 1-i & 3 \end{pmatrix} \)。\( \operatorname{tr}(AB) - \operatorname{tr}(BA) = 0 \neq n = \operatorname{tr}(I) \)。\( \operatorname{tr}(A^H A) = \sum_{i=1}^n \sum_{j=1}^n a_{ij} \overline{a_{ij}} \geq 0 \)。
- **2.17.** 检查 \( n=2 \) 的情况，并观察规律。

## 第 3 章

### 行列式

许多复杂的表达式，特别是在电气和机械工程中，可以通过将其表示为行列式的形式来优雅地求解。此外，2 阶和 3 阶行列式在几何上分别代表面积和体积。因此，行列式的工作知识是所有科学和工程学生的基本必需。在本章中，我们将简要概述行列式的重要性质。行列式在求解线性代数方程组中的应用将在第 6 章中介绍。

与方阵 \( n \times n \) 矩阵 \( A=(a_{ij})\in M^{n\times n} \) 相关的是 \( F \) 中的一个标量，称为 \( A \) 的 \( n \) 阶行列式，记为 \( \det(A) \)，或 \( |A| \)，或

![](img/049a5f7ee46d1463ca7feb5fdb0d0a78_35_0.png)

1 阶和 2 阶行列式定义为

![](img/049a5f7ee46d1463ca7feb5fdb0d0a78_35_1.png)

如果在矩阵 \( A \) 中我们选择任意 \( p \) 行和任意 \( p \) 列，其中 \( p\le n \)，则这些行和列交叉处的元素形成一个 \( p \) 阶方阵。这个新矩阵的行列式称为矩阵 \( A \) 的 \( p \) 阶余子式。\( A \) 的任何对角线元素的余子式称为主余子式。特别是，通过删除矩阵 \( A \) 的第 \( i \) 行和第 \( j \) 列得到的 \( (n-1)\times(n-1) \) 行列式是 \( (n-1) \) 阶余子式，我们记为 \( \tilde a_{ij} \)，并称 \( \alpha_{ij}=(-1)^{i+j}\tilde a_{ij} \) 为 \( a_{ij} \) 的余子式。用余子式表示，\( A \) 的行列式定义为

![](img/049a5f7ee46d1463ca7feb5fdb0d0a78_35_2.png)

此外，

![](img/049a5f7ee46d1463ca7feb5fdb0d0a78_35_3.png)

