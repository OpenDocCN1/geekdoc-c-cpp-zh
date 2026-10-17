
coordinates \((y_1,y_2,y_3)^t\) 相对于基 \(S\) 为 \((a,b,c)^t\)。现在可以利用 (10.4) 得到 \((a,b,c)^t\) 相对于基 \(T\) 的坐标 \((x_1,x_2,x_3)^t\)，如下所示：

$$
\begin{pmatrix}x_1\\x_2\\x_3\end{pmatrix}
=
\begin{pmatrix}1&-1&0\\0&1&-1\\0&0&1\end{pmatrix}
\begin{pmatrix}a\\b\\c\end{pmatrix}
=
\begin{pmatrix}a-b\\b-c\\c\end{pmatrix}.
$$

因此，相对于基 \(T\) 的多项式 \(P_2(x)=a+bx+cx^2\) 为
\[
P_2(x)=(a-b)+(b-c)(1+x)+c(1+x+x^2).
\]

## 问题

- 10.1. 求向量 \((a,b,c)^t\in R^3\) 相对于下列有序基的坐标：

  (i) \(\{(1,1,5)^t,(1,-1,3)^t,(7,2,1)^t\}\)

  (ii) \(\{(1,-1,3)^t,(1,1,5)^t,(7,2,1)^t\}\)。

- 10.2. 求向量 \((a,b,c,d)^t\in R^4\) 相对于下列有序基的坐标：
  \(\{(1,0,0,4)^t,(0,0,0,3)^t,(0,0,2,5)^t,(5,4,0,0)^t\}\)。

- 10.3. 求矩阵 \(\begin{pmatrix}a&b\\c&d\end{pmatrix}\) 相对于有序基
  \[
  \left\{\begin{pmatrix}1&0\\-1&0\end{pmatrix},\begin{pmatrix}0&1\\1&0\end{pmatrix},\begin{pmatrix}1&-1\\0&0\end{pmatrix},\begin{pmatrix}1&0\\0&-1\end{pmatrix}\right\}
  \]
  的坐标。

- 10.4. 求多项式 \(P_3(x)=a+bx+cx^2+dx^3\in(P_4,R)\) 相对于下列有序基的坐标：

  (i) \(\{1,1+x,1+x+x^2,1+x+x^2+x^3\}\)

  (ii) \(\{1,(1-x),(1-x)^2,(1-x)^3\}\)。

- 10.5. 在 \(R^3\) 中考虑有序基 \(S=\{(1,0,1)^t,(-1,0,0)^t,(0,1,2)^t\}\) 和 \(T=\{(-1,1,0)^t,(1,2,-1)^t,(0,1,0)^t\}\)。对于这些基，计算转换矩阵，并利用它求向量 \((7,3,4)^t\) 相对于每个基的坐标。

- 10.6. 在实轴上所有复值函数构成的向量空间中，考虑有序基 \(S=\{1,e^{ix},e^{-ix}\}\) 和 \(T=\{1,\cos x,\sin x\}\)。对于这些基，计算转换矩阵，并利用它求函数 \(3+5\cos x+7\sin x\) 相对于基 \(S\) 的坐标。

- 10.7. 考虑向量空间 \((P_n,R)\) 及其有序基 \(S=\{1,x,\cdots,x^{n-1}\}\)。证明：

  (i) \(T=\{L_1(x),\ldots,L_n(x)\}\)，其中
  \[
  L_i(x)=\frac{(x-x_1)\cdots(x-x_{i-1})(x-x_{i+1})\cdots(x-x_n)}{(x_i-x_1)\cdots(x_i-x_{i-1})(x_i-x_{i+1})\cdots(x_i-x_n)}
  \]
  且 \(x_1<\cdots<x_n\) 为 \(R\) 中的点，也是 \((P_n,R)\) 的一个基。

  (ii) 将基 \(S\) 转换为基 \(T\) 的转换矩阵是 [示例 3.5](#) 中给出的范德蒙矩阵。

- **10.8.** 在 [定理 10.2](#) 中，令 \(S=\{(5,0,3)^t,(3,5,7)^t,(-1,-4,11)^t\}\) 且
  \[
  A=\begin{pmatrix}11&3&4\\19&6&5\\21&7&8\end{pmatrix}.
  \]
  求有序基 \(T\)。

- **10.9.** 在 [定理 10.2](#) 中，令 \(T=\{(5,0,3)^t,(3,5,7)^t,(-1,-4,11)^t\}\) 且 \(A\) 如 [问题 10.8](#) 所示。求有序基 \(S\)。

## 答案或提示

- **10.1.** (i) \(\frac{1}{58}(-7a+20b+9c,\,9a-34b+5c,\,8a+2b-2c)^t\).

  (ii) \(\frac{1}{58}(9a-34b+5c,\,-7a+20b+9c,\,8a+2b-2c)^t\).

- **10.2.** \((a-\frac45b,-\frac43a+\frac53b-\frac56c+\frac13d,\frac23c,\frac14b)^t\).

- **10.3.** \(\frac12(a+b-c+d,\,a+b+c+d,\,a-b+c+d,\,-2d)^t\).

- **10.4.** (i) \((a-b,b-c,c-d,d)^t\).

  (ii) \((a+b+c+d,-b-2c-3d,c+3d,-d)^t\).

- **10.5.** \(\begin{pmatrix}-2&-5&-2\\-1&-6&-2\\1&2&1\end{pmatrix},\quad(-11,-4,22)^t_T,\quad(-2,-9,3)^t_S\).

- **10.6.** \(\begin{pmatrix}1&0&0\\0&\frac12&-\frac{i}{2}\\0&\frac12&\frac{i}{2}\end{pmatrix},\quad(3,5,7)^t_T,\quad(3,\frac{5-7i}{2},\frac{5+7i}{2})^t_S\).

- **10.7.** (i) 见 [问题 1.5](#).

  (ii) \(x^j=x_1^jL_1(x)+\cdots+x_n^jL_n(x),\quad j=0,1,\ldots,n-1.\)

- **10.8.** \(T=\{(91,11,397)^t,(26,2,128)^t,(27,-7,135)^t\}\).

- **10.9.** \(S=\{\frac1{30}(-83,-263,-213)^t,\frac1{30}(46,76,-114)^t,\frac1{30}(9,69,219)^t\}\).

# 推论 11.1.  $r(A)=r(A^t)=r(A^H)$.

# 定理 11.2.  设 \(A\in\mathbb{C}^{m\times n}\) 且 \(B\in\mathbb{C}^{n\times p}\)。则 \(r(AB)\le \min\{r(A),r(B)\}\)。

# 证明.

设 \(A=(a_{ij})\)，\(B=(b_{ij})\) 且 \(AB=C=(c_{ij})\)。由于 \(c_{ij}=\sum_{k=1}^{n}a_{ik}b_{kj}\)，其中 \(i=1,\cdots,m\)，\(j=1,\cdots,p\)，可得

$\begin{pmatrix}c_{1j}\\\vdots\\c_{mj}\end{pmatrix}=\begin{pmatrix}a_{11}\\\vdots\\a_{m1}\end{pmatrix}b_{1j}+\cdots+\begin{pmatrix}a_{1n}\\\vdots\\c_{mn}\end{pmatrix}b_{nj},\quad j=1,\cdots,p$

因此 \(AB\) 的列向量由 \(A\) 的列向量线性表示；类似地，\(AB\) 的行向量由 \(B\) 的行向量线性表示。故 \(C(AB)\subseteq C(A)\) 且 \(R(AB)\subseteq R(B)\)，这立即推出 \(r(AB)\le r(A)\) 且 \(r(AB)\le r(B)\)。综合以上，得 \(r(AB)\le\min\{r(A),r(B)\}\)。

# 推论 11.2.

- 1. 若乘积 \(AB\) 中的某个矩阵为非奇异矩阵，则 \(AB\) 的秩等于另一个矩阵的秩。
- 2. 若 \(P\) 和 \(Q\) 为非奇异矩阵，则 \(r(PAQ)=r(A)\)。

# 证明.

- 1. 设矩阵 \(A\) 为非奇异矩阵。由定理 11.2 可得 \(r(AB)\le r(B)\)，又因为 \(B=A^{-1}(AB)\)，故 \(r(B)\le r(AB)\)。因此，\(r(AB)=r(B)\)。
- 2. 由于 \(P\) 和 \(Q\) 为非奇异矩阵，故 \(r(PAQ)=r(AQ)=r(A)\)。

# 定理 11.3.  设 \(A,B\in\mathbb{C}^{m\times n}\)。则 \(r(A+B)\le r(A)+r(B)\)。

# 证明.

设 \(A=(a_{ij})\)，\(B=(b_{ij})\)，且 \(\{u^1,\cdots,u^p\}\) 与 \(\{v^1,\cdots,v^q\}\) 分别为 \(C(A)\) 和 \(C(B)\) 的基。则

$\begin{pmatrix}a_{1j}+b_{1j}\\\vdots\\a_{mj}+b_{mj}\end{pmatrix}=\begin{pmatrix}a_{1j}\\\vdots\\a_{mj}\end{pmatrix}+\begin{pmatrix}b_{1j}\\\vdots\\b_{mj}\end{pmatrix}=\sum_{i=1}^{p}\alpha_{ij}u^i+\sum_{i=1}^{q}\beta_{ij}v^i,\quad j=1,\cdots,n.$

因此，\(A+B\) 的第 \(j\) 列可表示为 \(p+q\) 个向量 \(u^1,\cdots,u^p,v^1,\cdots,v^q\) 的线性组合。故 \(A+B\) 的列空间由这些向量的线性组合生成。因此，

$\dim C(A+B)=\dim\left\{\sum_{i=1}^{p}s_i u^i+\sum_{i=1}^{q}t_i v^i\right\}$

# 矩阵的秩

且 \(r(A+B) \leq p+q\)。显然，若列向量集 \(\{u^1, \cdots, u^p, v^1, \cdots, v^q\}\) 线性无关，则 \(r(A+B) = p+q\)。\(\blacksquare\)

# ## 推论 11.3.

\(r(A+B) \geq |r(A) - r(B)|\).

# ## 证明.

显然，\(r(A) = r(A+B-B) \leq r(A+B) + r(-B) = r(A+B) + r(B)\)，故 \(r(A+B) \geq r(A) - r(B)\)。类似地，\(r(A+B) \geq r(B) - r(A)\)。\(\blacksquare\)

现在回顾，对于给定矩阵 \(A \in C^{m \times n}\)，其零空间 \(\mathcal{N}(A) \subseteq C^n\) 是一个向量空间。\(\mathcal{N}(A)\) 的维数称为 \(A\) 的 _零度_，记作 \(n(A)\)。

# ## 定理 11.4.

若 \(A \in C^{m \times n}\)，则 \(r(A) + n(A) = n\)。

# ## 证明.

设 \(B\) 为矩阵 \(A\) 的行最简形。由于矩阵 \(A\) 的秩为 \(r(A)\)，\(B\) 的前 \(r(A)\) 行非零，即 \(B\) 有 \(r(A)\) 个主元。因此，齐次线性方程组 (5.3) 的等价形式 \(Bx = 0\) 将有 \(r(A)\) 个基本变量和 \(n - r(A)\) 个自由变量。故方程组 (5.3) 有一组 \(n - r(A)\) 个线性无关的解，即 \(n(A) = n - r(A)\)。\(\blacksquare\)

# ## 推论 11.4.

\(r(A) + n(A^t) = m\)。

# ## 推论 11.5.

若 \(r(A) = n \leq m\)，则 \(A\) 的 \(n \) 列线性无关，且 \(x = 0\) 是齐次线性方程组 (5.3) 的唯一解。

# ## 示例 11.1.

矩阵

\(A = \left( \begin{array}{ c c c c }
1 & 2 & 1 & 5 \\
1 & 2 & -1 & 1 \\
2 & 4 & -3 & 0
\end{array} \right)\)

的行最简形和列最简形为

\(\left( \begin{array}{ c c c c }
1 & 2 & 1 & 5 \\
0 & 0 & 1 & 2 \\
0 & 0 & 0 & 0
\end{array} \right) \text{ 和 } \left( \begin{array}{ c c c c }
1 & 0 & 0 & 0 \\
1 & 2 & 0 & 0 \\
2 & 5 & 0 & 0
\end{array} \right).\)

因此，\(r(A) = 2\)，集合 \(\{(1,2,1,5), (0,0,1,2)\}\) 生成 \(R(A)\)，集合 \(\{(1,1,2)^t, (0,2,5)^t\}\) 生成 \(C(R)\)。由行最简形还可知，集合 \(\{(-2,1,0,0)^t, (-3,0,-2,1)^t\}\) 生成 \(\mathcal{N}(A)\)，且 \(n(A) = 2\)。

# ## 示例 11.2.

对于问题 6.1(i) 中的矩阵 \(A\)，\(n = 4, r(A) = 3, n(A) = 1\)。对于问题 6.1(ii) 中的矩阵 \(A\)，\(n = 5, r(A) = 4, n(A) = 1\)。对于问题 6.1(iii) 中的矩阵 \(A\)，\(n = 6, r(A) = 3, n(A) = 3\)。

现在，对于给定矩阵 \(A \in M^{m \times n}\)，若存在矩阵 \(L \in M^{n \times m}\)（或 \(R \in M^{n \times m}\)）使得 \(LA = I\)（或 \(AR = I\)），则称 \(L\)（或 \(R\)）为 \(A\) 的 _左逆_（_右逆_）。
