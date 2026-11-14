

with

M(t) = M(t; V) = \sum_{\{n|\theta_n < t\}} v_n.

方程 (16.2.1) 中的新项是

k \left( \gamma t - \int_0^t y_s(s; V) ds \right),

该项描述了均值回归过程。库存的增加或减少以连续方式进行。因此，在时间间隔 dt 内，如果库存 y(t) 小于目标 \gamma \ge 0（且 k > 0），则库存增加 k(\gamma - y(t))dt。如果库存大于 \gamma，则库存相应减少相同数量。如果 k = 0，均值回归部分消失，我们恢复上一章的模型，只是没有跳跃。请注意，项 k\gamma t 可以与需求的确定性部分 -\nu t 合并，这在数学分析中会很明显。然而，这些项具有不同的经济解释，因此我们不将它们合并。因此，我们不对 k\gamma - \nu 的符号做任何假设。

成本泛函将与没有均值回归部分的情况相同。令

f(x) = hx^+ + px^-.

我们按如下定义成本泛函

(16.2.2) \quad J_x(V) = E \left[ \sum_{n=0}^\infty (K + c v_n) \exp -\alpha \theta_n + \int_0^\infty f(y_s(t; V)) \exp -\alpha t dt \right],

以及值函数

u(x) = \inf J_x(V).

### 16.2.2. Q.V.I.

然后可以写出源自动态规划的Q.V.I。我们引入算子

(16.2.3) \quad Au(x) = -\frac{1}{2} \sigma^2 u''(x) + (\nu + k(x - \gamma)) u'(x),

其中可以看到源自均值回归部分的项。算子 A 不再具有常系数。

Q.V.I. 由以下给出

(16.2.4)
Au(x) + \alpha u(x) \le f(x)
u(x) \le M(u)(x)
(Au(x) + \alpha u(x) - f(x))(u(x) - M(u)(x)) = 0

其中

M(u)(x) = K + \inf_{v > 0} [cv + u(x + v)].

像往常一样，我们寻找一个具有线性增长的 C^1 函数。标准论证表明，Q.V.I 的解即为值函数。

### 16.2.3. 变换

如同上一章所做的那样，考虑如下变换很方便

$$G(x) = u(x) + cx,$$

因此问题变为：寻找一个 \(x \in R\)、\(C^1\) 且具有线性增长的函数 \(G(x)\)，使其满足

$$(16.2.5) \quad \begin{aligned} AG(x) + \alpha G(x) \le g(x) + c(v - k\gamma) \\ G(x) \le K + \inf_{\eta \ge x} G(\eta) \\ (AG(x) + \alpha G(x) - g(x) - c(v - k\gamma))(G(x) - K - \inf_{\eta \ge x} G(\eta)) = 0 \end{aligned}$$

函数 \(g\) 由以下给出

$$(16.2.6) \quad g(x) = f(x) + c(\alpha + k)x.$$

## 16.3. s, S 策略

### 16.3.1. 阈值 s

给定一个数 s，我们按如下方式寻找 (16.2.5) 的解：

$$(16.3.1) \quad \begin{aligned} AG_s(x) + \alpha G_s(x) = g(x) + c(v - k\gamma), & \quad x > s \\ G_s(x) = K + \inf_{\eta \ge x} G_s(\eta), & \quad x \le s \end{aligned}$$

为了得到一个全局 \(C^1\) 的函数，我们施加条件

$$(16.3.2) \quad G'_s(s) = 0.$$

这是定义 s 的关系式。我们通过考虑

$$H_s(x) = G'_s(x),$$

它是以下问题的解

$$(16.3.3) \quad \begin{aligned} AH_s(x) + (\alpha + k)H_s(x) = g'(x), & \quad x > s \\ H_s(x) = 0, & \quad x \le s \end{aligned}$$

对于给定的 s，我们寻找狄里克莱问题 (16.3.3) 的一个有界连续解 \(H_s(x)\)。为了定义 s，我们使用第二个关系式 (16.3.1)，它可以写成如下形式

$$(16.3.4) \quad 0 = K + \inf_{\eta \ge s} \int_s^\eta H_s(\eta) d\eta.$$

请注意

$$(16.3.5) \quad g'(x) = \left\{ \begin{array}{ll} h + c(\alpha + k), & \text{if } x > 0 \\ -p + c(\alpha + k), & \text{if } x < 0 \end{array} \right.$$

我们做如下假设

$$(16.3.6) \quad -p + c(\alpha + k) < 0.$$

### 16.3.2. 格林函数

虽然可以通过近似程序证明 (16.3.3) 解的存在，但像在标准情况下所做的那样，获得显式公式很重要。为此，我们需要一个格林函数，即全空间内无右项的微分方程的解。我们引入以下问题

$$
\begin{aligned}
-\frac{1}{2}\sigma^2\Phi''(x) + (\nu + k(x - \gamma))\Phi'(x) + (\alpha + k)\Phi(x) &= 0, \forall x \in R \\
\Phi(0) &= 1, \quad \Phi(+\infty) = 0
\end{aligned}
$$

我们要证明

### 定理 16.1.

我们假设 (16.3.6)。(16.3.7) 存在唯一解，使得

(16.3.8) \Phi(x) > 0, \Phi'(x) < 0, \Phi''(x) > 0.

当 \(x \to -\infty\) 时，\(\Phi(x) \to +\infty\)，\(\Phi'(x) \to -\infty\)。考虑方程的根 \(\beta_k < 0, \beta_k^* > 0\) 
\(-\frac{1}{2}\sigma^2\beta^2 + \nu\beta + \alpha + k = 0,\)

我们有增长条件

$$
0 > \Phi'(x) \ge \frac{k}{\sigma^2} \frac{(x - \gamma)^2}{\beta_k^* - \beta_k} \left[ \beta_k \left( \beta_k^* - \Phi(0) \exp - \frac{k\gamma^2}{\sigma^2} \right) \exp \beta_k x + \beta_k^* \left( \Phi(0) \exp - \frac{k\gamma^2}{\sigma^2} - \beta_k \right) \exp \beta_k^* x \right], x \le 0
$$

### 证明。

我们首先在 \([0, +\infty)\) 上求解 (16.3.7)。这是一个狄里克莱类型的边值问题。它有唯一解，并且

0 \le \Phi(x) \le 1, x \ge 0,

并且我们有能量关系

(16.3.10) \frac{\sigma^2}{2} \int_0^{+\infty} \Phi'^2 dx + \left( \alpha + \frac{k}{2} \right) \int_0^{+\infty} \Phi^2 dx = -\frac{\sigma^2}{2} \Phi'(0) + \frac{1}{2} (\nu - k\gamma).

接下来，我们用 \(\Phi'(x)\) 对方程 (16.3.7) 进行试验，并在 0 到 \(x > 0\) 之间积分。我们得到

-\frac{\sigma^2}{4} \Phi'^2(x) + \frac{\sigma^2}{4} \Phi'^2(0) + \int_0^x (\nu + k(\xi - \gamma)) \Phi'^2(\xi) d\xi + \frac{\alpha + k}{2} (\Phi^2(x) - 1) = 0,

从这个公式中，可以很容易地看出 \(\Phi''(x)\) 在 \(x \to +\infty\) 时有一个极限，但由于 \(\Phi'^2(x)\) 也是一个 \(L^1\) 函数，这个极限必然为 0。因此，我们得到一个额外的能量关系

(16.3.11) \frac{\sigma^2}{4} \Phi'^2(0) + \int_0^{+\infty} (\nu + k(x - \gamma)) \Phi'^2(x) dx = \frac{\alpha + k}{2}.

由于 \(\Phi(\epsilon) < 1 = \Phi(0)\)，我们看到 \(\Phi'(0) \le 0\)。事实上，\(\Phi'(0) < 0\)。确实，如果令 \(\Psi(x) = \Phi'(x)\)，则 \(\Psi(x)\) 满足

(16.3.12) -\frac{1}{2} \sigma^2 \Psi''(x) + (\nu + k(x - \gamma)) \Psi'(x) + (\alpha + 2k) \Psi(x) = 0, x > 0,

并且我们已经知道 \(\Psi(+\infty) = 0\)。因此 \(\Psi(0)\) 不能为 0，否则 \(\Psi(x)\) 将恒为 0，从而 \(\Phi(x)\) 在 \([0, \infty)\) 上为常数，这是不可能的。由于 \(\Psi(0) \le 0\)，事实上 \(\Psi(0) < 0\)。必然 \(\Psi(x) \le 0\) 且在任何点都不能为 0，否则该点将是一个极大值，这也是不可能的。因此 \(\Psi(x) < 0, \forall x \ge 0\)。此外，\(\Psi'(x)\) 在任何点都不能为负或零。否则，\(\Psi(x)\) 将有一个负的局部最小值，这也是不可能的。因此 \(\Psi(x) = \Phi'(x) < 0, \forall x \in (0, \infty)\)。

我们因此证明了 \(x \in [0, \infty)\) 时的性质 (16.3.8)。

接下来，我们在 \((-\infty, 0]\) 上将方程 (16.3.7) 求解为一个给定 0 处初值的二维线性微分方程组。为方便起见，我们将改变 \(x\) 的符号，以在 \([0, \infty)\) 上求解一个系统。定义

\(y(x) = \Phi(-x), z(x) = \Phi'(-x), x > 0\)

那么对 \(y(x), z(x)\) 是以下问题的解

(16.3.13)
\[
\begin{aligned}
y' &= -z; \\
z' &= \frac{2}{\sigma^2}((kx - (\nu - k\gamma))z - (\alpha + k)y),
\end{aligned}
\]
在 \([0, \infty)\) 上，初始条件为 \(y(0) = 1, z(0) = z_0 = \Phi'(0) < 0\)。考虑矩阵

\(\mathcal{A}(x) = \left( \begin{array}{ c c }
0 & -1 \\
-\frac{2}{\sigma^2}(\alpha + k) & \frac{2}{\sigma^2}(kx - (\nu - k\gamma)) 
\end{array} \right),\)

然后我们将其与一组矩阵关联，称为 \(\Sigma(x, x_0), x \ge x_0\)，即满足微分方程的*基本矩阵*

\[
\begin{aligned}
\frac{d}{dx}\Sigma(x, x_0) &= \mathcal{A}(x)\Sigma(x, x_0); \\
\Sigma(x_0, x_0) &= I,
\end{aligned}
\]

其中 \(I\) 是单位矩阵。根据线性微分方程理论，矩阵 \(\Sigma(x, x_0)\) 对于任何 \(x \ge x_0\) 的对都定义良好。此外，(16.3.13) 的解由以下给出

\(\begin{pmatrix} y(x) \\ z(x) \end{pmatrix} = \Sigma(x, 0) \begin{pmatrix} 1 \\ z_0 \end{pmatrix},\)

因此它对任何 \(x > 0\) 都唯一确定。令

\(\varpi(x) = \exp -\frac{2}{\sigma^2} \left[ k \frac{(x+\gamma)^2}{2} - \nu x \right],\)

以及

\(\bar{z}(x) = z(x)\varpi(x),\)

那么对 \(y(x), \bar{z}(x)\) 是以下问题的解

(16.3.14)
\[
\begin{aligned}
y' &= -\frac{\bar{z}}{\varpi} \\
\bar{z}' &= -\frac{2}{\sigma^2}(\alpha + k)\varpi y
\end{aligned}
\]

初始条件为 \(y(0) = 1, \bar{z}(0) = z_0 \exp - \frac{k\gamma^2}{\sigma^2}\)。很容易看出 \(y(x) > 0, \bar{z}(x) < 0\)。经过简单变形后，我们得到 \(\bar{z}(x)\) 的以下积分方程

(16.3.15)
\[
\begin{aligned}
\bar{z}(x) &= \bar{z}(0) - \frac{2}{\sigma^2}(\alpha + k)y(0) \int_0^x \varpi(\xi) d\xi \\
&+ \frac{2}{\sigma^2}(\alpha + k) \int_0^x G(x, \eta) \bar{z}(\eta) d\eta,
\end{aligned}
\]

