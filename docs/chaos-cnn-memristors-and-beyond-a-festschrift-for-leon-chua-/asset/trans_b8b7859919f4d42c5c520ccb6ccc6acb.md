

(ii) 在 \((t_{i-1}, t_i)\) 上，\(2 \le i \le N\)：

为了在每个 \((t_{i-1}, t_i)\) 上定义 \(\psi(t)\)，我们对 \(2 \le i \le N\) 重复以下过程。令
\[
\psi(t) := (q_i - \tilde{q}_{i-1})(t - t_{i-1})/h, \quad t \in (t_{i-1}, t_i),
\]
则 \(\tilde{q}_{i-1} + \psi(t) \in V\)，\(t \in (t_{i-1}, t_i)\)。因此，
\[
\sup_{s \in (t_{i-1}, t_i)} |f(\tilde{q}_{i-1} + \psi(s))| \le C.
\]
考虑 (31) 中 \(t \in (t_{i-1}, t_i)\) 且 \(y(t_{i-1}) = \tilde{q}_{i-1}\) 的情形，则我们有
\[
y(t) - (\tilde{q}_{i-1} + \psi(t)) = \int_{t_{i-1}}^t \bigl(f(y(s)) - f(\tilde{q}_{i-1} + \psi(s))\bigr)\,ds + \int_{t_{i-1}}^t f(\tilde{q}_{i-1} + \psi(s))\,ds,
\]
这蕴含
\[
|y(t) - (\tilde{q}_{i-1} + \psi(t))| \le \int_{t_{i-1}}^t |f(y(s)) - f(\tilde{q}_{i-1} + \psi(s))|\,ds + \int_{t_{i-1}}^t |f(\tilde{q}_{i-1} + \psi(s))|\,ds
\]
\[
\le \int_{t_{i-1}}^t L|y(s) - (\tilde{q}_{i-1} + \psi(s))|\,ds + hC.
\]
由 Gronwall 不等式，我们有
\[
|y(t_i) - (\tilde{q}_{i-1} + \psi(t_i))| \le hC e^{Lh} < \epsilon/2,
\]
只要 \(h\) 足够小。记 \(\tilde{q}_i := y(t_i)\)。在最后阶段 \(i = N\) 时，我们有
\[
|y(T) - (\tilde{q}_{i-1} + \psi(T))| = |y(T) - q| < \epsilon/2.
\]
于是我们有 \(|S(T, \dot{\psi})x_0 - q| < \epsilon\)。证明完毕。

我们将证明以正概率，(24) 的解 \(\phi(t,\omega)p\) 可以在任意有限时间区间和任意初始点 \(p\) 上被 (31) 的解 \(S(t, \dot{\psi})p\) 近似。

**引理 4.** 假设 (H3)--(H4) 成立。给定分段连续的 \(\dot{\psi}\)，\(T > 0\) 和 \(\gamma > 0\)，集合 \(A_\gamma\) 定义为
\[
A_\gamma := \left\{ \omega : \sup_{p \in \mathbb{R}^n} \sup_{t \in [0,T]} |S(t, \dot{\psi})p - \phi(t,\omega)p| < \gamma \right\}, \tag{34}
\]
有 \(\mathbb{P}(A_\gamma) > 0\)。

**证明.** 根据引理 1 和引理 2，\(S(t, \dot{\psi})p\) 和 \(\phi(t,\omega)p\) 在 \(t \in [0,T]\) 上有定义。由 (24) 和 (31) 我们有
\[
d(x - y) = (f(x) - f(y))dt - \sigma \dot{\psi}(t)dt + \sigma dW(t). \tag{35}
\]
我们可以假设 \(\psi(0) = 0\)，因为它不影响 (31) 的解。令 \(\tilde{W}(t) := W(t) - \psi(t)\)，\(t \in [0,T]\)，则我们有
\[
d\tilde{W} = -\dot{\psi}(t)dt + dW. \tag{36}
\]
由 Girsanov 定理 ([19])，\(\tilde{W}\) 在概率 \(\tilde{\mathbb{P}}\) 下是布朗运动，其中
\[
\frac{d\tilde{\mathbb{P}}}{d\mathbb{P}} = \exp\left(\int_0^T \dot{\psi}(s) \cdot dW(s) - \frac12 |\dot{\psi}(s)|^2 ds\right) > 0. \tag{37}
\]
令 \(\tilde{\Lambda}_\varepsilon := \{\omega : \sup_{t \in [0,T]} |\tilde{W}(t,\omega)| < \varepsilon\}\) 且 \(\Lambda_\varepsilon := \{\omega : \sup_{t \in [0,T]} |W(t,\omega)| < \varepsilon\}\)，则 \(\tilde{\mathbb{P}}(\tilde{\Lambda}_\varepsilon) > 0\)，这由 (37) 蕴含 \(\mathbb{P}(\tilde{\Lambda}_\varepsilon) > 0\)。由此可得对 \(\omega \in \tilde{\Lambda}_\varepsilon\)，
\[
|\phi(t,\omega)p - S(t, \dot{\psi})p| \le \int_0^t |f(\phi(s,\omega)p) - f(S(s, \dot{\psi})p)|\,ds + \sigma |\tilde{W}(t)|
\]
\[
\le \int_0^t L|\phi(s,\omega)p - S(s, \dot{\psi})p|\,ds + \sigma \varepsilon. \tag{38}
\]
由 Gronwall 不等式，我们有
\[
\sup_{p \in \mathbb{R}^n} \sup_{t \in [0,T]} |S(t, \dot{\psi})p - \phi(t,\omega)p| < \sigma \varepsilon e^{LT}, \quad \omega \in \tilde{\Lambda}_\varepsilon.
\]
结论由取足够小的 \(\varepsilon\) 得到。

**定理 3 的证明.** 我们仍用 \(\phi(t,\omega)\) 表示具有图 1 所示分段常数扩散 \(\sigma(t)\) 的 (2) 的流。令 \(q_0\) 为初始点。我们可以假设 \(B(p_i, \epsilon)\) 位于 \(p_i\) 的稳定流形内，\(i = 1, \dots, N\)。

令 \(q_i \in \mathbb{R}^n\)。对每个 \(1 \le i \le N\)，由引理 3，存在分段连续的 \(\dot{\psi}_i(t)\)，\(t \in [S_i, T_i]\)，使得
\[
dy^{(i)} = f(y^{(i)})dt + \sigma(t)\dot{\psi}_i dt, \quad y^{(i)}(S_i) = q_{i-1}, \tag{39}
\]
的解满足
\[
y^{(i)}(T_i) \in B(p_i, \epsilon/2).
\]
由于 \(\sigma(t) = 0\) 且 \(y^{(i)}(T_i)\) 位于 \(p_i\) 的稳定流形中，于是
\[
y^{(i)}(t) \in B(p_i, \epsilon/2), \quad t \in [T_i, S_{i+1}],
\]
选取 \(q_i = y^{(i-1)}(S_{i-1})\)，\(2 \le i \le N\)，并令 \(\dot{\psi}(t)\) 为分段连续函数，定义为
\[
\dot{\psi}(t) = \begin{cases} \dot{\psi}_i(t), & t \in [S_i,T_i], \ 1 \le i \le N, \\ 0, & \text{otherwise.} \end{cases} \tag{40}
\]
则我们有
\[
S(t,\dot{\psi})q_0 \in B(p_i,\epsilon/2), \quad t \in [T_i,S_{i+1}], \quad 1 \le i \le N,
\]
由引理 4，集合
\[
\left\{\omega : \sup_{t\in[0,T]} |S(t,\dot{\psi})q_0 - \phi(t,\omega)q_0| < \epsilon/2 \right\}, \tag{41}
\]
具有正概率，这蕴含集合
\[
\Omega' := \{\omega : \phi(t,\omega)q_0 \in B(p_i,\epsilon_i), \ t \in [T_i,S_{i+1}], \ 1 \le i \le N\}, \tag{42}
\]
有 \(\mathbb{P}(\Omega') > 0\)。证明完毕。

## 4. 数值例子

在本节中，我们在四个标准测试例子上演示 ID 方法用于全局优化方法。它们被设计为具有许多局部极小值，这些极小值与全局极小值相似，且局部极小值很容易捕获解。在所有实验中，我们设参数 \(\alpha = 10\)，\(\gamma = 10\) 和 \(N = 10\)。

### 问题 1. 罚函数 Shubert 函数

令
\[
g_1(x) = \sum_{i=1}^{5} i \cos((i+1)x + 1) \tag{43}
\]
为标准 Shubert 函数。则罚 Shubert 函数定义为
\[
g(x) := g_1(x) + u(x,10,100,2) \tag{44}
\]
其中 \(u(x,a,k,m)\) 称为罚函数，定义为
\[
u(x,a,k,m) := \begin{cases} k(x-a)^m, & x > a, \\ 0, & -a \le x \le a, \\ k(-x-a)^m, & x < -a. \end{cases} \tag{45}
\]
如图 2 所示，函数 \(g\) 在区域 \(\{x : |x| < 10\}\) 中有 19 个局部极小值，其中三个为全局极小值。ID 方法的一个实现给出了圆圈标记的点，它们是扩散关闭后梯度流的收敛点。它找到了中间的全局最小值。

![](img/039e7d3c23390584a66737067db8b75b_487_0.png)

*图 2. 问题 3 的数值实验。蓝色圆圈标记非扩散步骤的收敛点。*

### 问题 2. 二维罚 Shubert 函数

它定义为
\[
g(x,y) = \left\{\sum_{i=1}^{5} i \cos((i+1)x + 1)\right\} \times \left\{\sum_{i=1}^{5} i \cos((i+1)y + 1)\right\} + u(x,10,100,2) + u(y,10,100,2). \tag{46}
\]
它在区域 \(\{(x,y) : |x| < 10, |y| < 10\}\) 中有 760 个局部极小值，其中 18 个为全局极小值，如图 3 所示。它还显示 ID 算法的任意一次实现给出圆圈标记的点。其中，它找到了三个全局极小值。

![](img/039e7d3c23390584a66737067db8b75b_488_0.png)

*图 3. 问题 4 的数值实验。黑色圆圈标记非扩散步骤的收敛点。*

### 问题 3. 具有参数 \(\beta\) 的二维罚 Shubert 函数

它定义为
\[
g(x,y) = \left\{\sum_{i=1}^{5} i \cos((i+1)x + 1)\right\} \times \left\{\sum_{i=1}^{5} i \cos((i+1)y + 1)\right\} + u(x,10,100,2) + u(y,10,100,2) + \beta[(x - 6.0835)^2 + (y + 5.8581)^2], \tag{47}
\]
其中 \(\beta > 0\) 为常数。点 \((x,y) = (6.0835, -5.8581)\) 是 \(\beta = 0\) 时 \(g\) 的全局极小化子。该函数与问题 2 中考虑的函数行为大致相同，但仅在 \((x,y) = (6.0853, -5.8581)\) 处有一个唯一的全局极小化子，如图 4 所示。我们展示了任意 ID 实现的收敛点（圆圈标记）的结果。与之前的问题类似，ID 方法能够找到全局极小值。

![](img/039e7d3c23390584a66737067db8b75b_488_1.png)

*图 4. 问题 5 的数值实验。黑色圆圈标记非扩散步骤的收敛点。*

### 问题 4. 一个多维函数

令
\[
g(x) = (\pi/n) \left\{ k \sin^2(\pi y_1) + \sum_{i=1}^{n-1} (y_i - A)^2[1 + k \sin^2(\pi y_{i+1})] + (y_n - A)^2 \right\}, \tag{48}
\]
其中
\[
x = (x_1, \dots, x_n) \in \mathbb{R}^n, \quad y_i = 1 + (x_i - 1)/4, \quad i = 1, \dots, n, \quad k = 10, \quad A = 1.
\]
该函数在区域 \(\{(x_1,\dots,x_n) : |x_i| < 10, \ i = 1,\dots,n\}\) 中大约有 \(5^n\) 个局部极小值，且唯一全局最小值位于
\[
x_i = 1, \quad i = 1, \dots, n.
\]
对于 \(n = 3\)，图 5 是函数 \(y = g(x_1,x_2,x_3)\) 的图在空间 \(x_3 = 1\) 上的投影图，说明全局极小化子被许多局部极小化子包围。任意 ID 实现对 \(n = 3\) 和 \(n = 4\) 按顺序访问的 10 个收敛点分别给出在表 1 中。

![](img/039e7d3c23390584a66737067db8b75b_488_2.png)

*图 5. 问题 6 中 \(y = g(x_1,x_2,x_3)\) 的图在空间 \(x_3 = 1\) 上的投影图。*

ID 方法对两种情况均找到了全局极小值。并且访问全局最小值的频率明显高于任何其他局部极小值。

