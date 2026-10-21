

到迭代矩阵
$$
\begin{pmatrix} u^{n+1} \\ u^{n} \end{pmatrix} = \mathbf{M} \begin{pmatrix} u^{n} \\ u^{n-1} \end{pmatrix} = \begin{bmatrix} \frac{b_2}{b_1} & \frac{b_1}{b_1} \\ 1 & 0 \end{bmatrix} \begin{pmatrix} u^{n} \\ u^{n-1} \end{pmatrix}.
$$

为了使系统稳定，我们必须验证 $\mathbf{M}$ 的特征值 $z_{1,2}$ 的范数小于或等于 1。特征方程为
$$\Phi_{NV}(z) = z^2 - \frac{b_2}{b_1}z - \frac{b_1}{b_1} = 0$$

因此，我们得出 $|z_1 \cdot z_2| = |\frac{b_1}{b_1}| = 1$ 且解的稳定性等价于 $|z_{1,2}| = 1$，即我们有 $|u^{n+1}| = |u^{n-1}|$。利用二次方程的显式解和
(3.11)
$$b_2 \in i\mathbb{R}, \qquad |b_2| \le 2|b_1|,$$

我们得到 $2\overline{b_1}\,z_{1,2} = b_2 \pm \sqrt{b_2^2 + 4|b_1|^2}$ 且 $|2\overline{b_1}|^2|z_{1,2}|^2 = |2b_1|^2$。因此，$|z_{1,2}| = 1$。结合 (3.10)，ODE (3.9) 的稳定性条件 (3.11) 变为
$$((1 - 4\theta)\lambda^2 + 2(1 - 2\theta)\lambda\gamma + \gamma^2)(\Delta t)^2 \le 16.$$

对于 $\gamma = \alpha = 0$ 且 $\frac{1}{4} \le \theta \le 1$，稳定性条件与步长 $\Delta t > 0$ 无关地得到满足，我们对初边值问题 (3.8) 有一个稳定性结果。这证明了下面的定理。

THEOREM 1. *数值格式 (3.6) 应用于关于零解的 (1.2)–(1.4) 的线性化在 $\frac{1}{4} \le \theta \le 1$ 时是稳定的。*

证明 (3.8) 在 $\alpha \ne 0$ 时的稳定性需要更多的计算。利用 (3.9) 中的 $\lambda$ 和 $\gamma$ 的表达式得到稳定性条件
$$(1 - 4\theta) + 2(1 - 2\theta)\frac{3\alpha}{\eta^2 + \xi^2} + \left(\frac{3\alpha}{\eta^2 + \xi^2}\right)^2 \le \left(\frac{4}{\omega\Delta t}\right)^2.$$

对于 $\theta = \frac{1}{2}$ 我们得到充分条件
$$-2 + \left(\frac{3\alpha}{\eta^2 + \xi^2}\right)^2 \le \left(\frac{3\alpha}{\eta^2 + \xi^2}\right)^2 \le \left(\frac{4}{(\xi^3 - 3\xi\eta^2)\Delta t}\right)^2$$

$$(\Delta t)^2 \le \left(\frac{4(\xi^2 + \eta^2)}{3\alpha(\xi^3 - 3\xi\eta^2)}\right)^2.$$

由于 $|\xi^3 - 3\xi\eta^2| \le (\xi^2 + \eta^2) \cdot \max\{|\xi|,|\eta|\}$，我们得到 $\Delta t$ 的充分条件
$$\Delta t \le \frac{4}{3|\alpha|\max\{|\xi|,|\eta|\}}.$$

对于 DFT，$\Delta x = \Delta y = \frac{W_s}{L}$ 时我们得到 $\max\{|\xi|,|\eta|\} = \frac{\pi}{\Delta x}$，因此我们有稳定性条件
(3.12)
$$\Delta t \le \frac{4}{3|\alpha|\pi}\,\Delta x.$$

作为推论，我们对初边值问题 (3.8) 在 $\alpha \ne 0$ 时有稳定性结果，定理 2。

THEOREM 2. *数值格式 (3.6) 应用于 (3.8) 在 $\theta = \frac{1}{2}$ 时是稳定的，如果时间步长 $\Delta t$ 满足条件 (3.12)。*

现在我们考察形如的扰动函数

```
(4.5)    u(x, y, t) = u0(x) + ε f(x) e^{i k y + γ t}, (4.6)    v(x, y, t) = v0(x) + ε g(x) e^{i k y + γ t}, (4.7)    w(x, y, t) = w0(x) + ε h(x) e^{i k y + γ t}.
```

因此我们考察具有指数增长的周期横向扰动。对于数值目的，我们也可以使用纯实数形式。

```
(4.8)    u(x, y, t) = u0(x) + ε f(x) cos(k y) e^{γ t}, (4.9)    v(x, y, t) = v0(x) + ε g(x) cos(k y) e^{γ t}, (4.10)   w(x, y, t) = w0(x) + ε h(x) sin(k y) e^{γ t}.
```

将这些表达式代入 (4.2)–(4.4) 并舍去与 ε² 成比例的项得到（用 ′ 表示 d/dx）

```
0 = 4 γ f − 4 f′ + f′′′ + 3 k² f′ −3 (u0 g)′ − 3 (v0 f)′ − 3 u0 i k h (4.11) f′ = + g′ − i k h (4.12) i k f = − h′ − i k g (4.13)
```

这是一个具有非恒定系数的线性常微分方程组。利用 h(x) = 1/(i k) (g′(x) − f′(x))，上述方程可以写成

```
f′′′(x) = (−4 γ + 3 u0′(x)) f(x) + (4 − 3 k²) f′(x) + 3 u0′(x) g(x) + 6 u0(x) g′(x) (4.14) g′′(x) = k² g(x) + f′′(x) + k² f(x) (4.15)
```

## 4.2. 已知解。

由于 fc(x − c t + s) 是原 NV 方程 (1.2)–(1.4) 的解，我们得出 (u0(x − s), v0(x − s), w0(x − s)) 求解系统 (4.2)–(4.4)，因此它们的导数必须求解线性化问题 (4.11)–(4.13)。由于 d/dx sech²(x) = −2 sech²(x) tanh(x)，我们得到解

```
(4.16)    f(x) = g(x) = sech²(x) tanh(x),    h(x) = 0
```

对于 k = γ = 0 时系统 (4.14)–(4.15) 的解。对于 k = 1 且 γ = 0 我们找到了

```
f(x) = + sech³(x) g(x) = − sech(x) tanh²(x) h(x) = − i sech(x) tanh(x) (4.17)
```

作为 (4.11)–(4.13) 的第二个显式解。借助这些解，我们将构造 Novikov-Veselov 方程关于参数 k 和 γ 的不稳定解。因此我们需要 (4.14)–(4.15) 的非零解。

## 4.3. 定位不稳定解。

利用函数 u0(x) = −2 sech²(x)，矩阵记号将高阶系统 (4.14)–(4.15) 转化为

一阶常微分方程组。

```
d/dx ( f \n f' \n f'' \n g \n g' ) = [ 0 1 0 0 0 \n 0 0 1 0 0 \n -4γ + 3 u0' (4 - 3 k²) 0 3 u0'(x) 6 u0 \n 0 0 0 0 1 \n k² 0 1 k² 0 ] ( f \n f' \n f'' \n g \n g' )
```

我们寻求满足 x → ±∞ 时衰减条件的非平凡解。我们使用渐近分析和数值方法的组合。必须分别考虑大 |x| 和小 |x|。我们采用以下方法：

- 选择一个大的值 M > 0。对于 |x| > M，我们使用 u0(x) ≈ 0 和初等渐近分析来构造满足衰减条件的解。
- 对于 |x| ≤ M，渐近分析不可行，因为 (4.14)–(4.15) 中的贡献 u0(x) 和 u0'(x) 必须被考虑。因此我们使用数值求解器在域 −M ≤ x ≤ +M 上构造一个基本矩阵 T，其中包含 −M ≤ x ≤ M 时线性系统解的信息。
- 然后将上述两个结果结合起来找到非平凡解存在准则 (4.23)。

### 4.3.1. 大 |x| 时解的行为。

对于 |x| 的大值，我们使用 u0(x) ≈ 0 并得到常系数线性微分方程的解耦系统。

```
(4.18) d/dx ( f \n f' \n f'' ) = [ 0 1 0 \n 0 0 1 \n -4γ (4 - 3 k²) 0 ] ( f \n f' \n f'' )
```

```
(4.19) d/dx ( g \n g' ) = [ 0 1 \n k² 0 ] ( g \n g' ) + ( 0 \n k² f' + f'' )
```

(4.18) 中矩阵的特征方程为

```
(4.20) λ³ + (3 k² - 4) λ + 4 γ = 0,
```

我们将该系统的特征值 λ₁, λ₂ 和 λ₃ 分别记为 p₁, p₂ 和 p₃。(4.19) 中的非齐次系统导致特征值 λ₄,₅ = ±k。利用三次多项式零点的 Cardano 公式，我们验证 (4.20) 在

```
4 γ² + (3 k² - 4)³ / 27 < 0.
```

时有三个不同的实值。对于我们要考察的 (k, γ) 域，我们可以使用

```
p₃ ≤ 0 ≤ p₁, p₂
```

并且对于 |γ| 的小值我们得到

```
(4.21) λ(γ) = { p₁ ≈ 0 + 4/(4 - 3 k²) γ \n p₂ ≈ +√(4 - 3 k²) - 2/(4 - 3 k²) γ \n p₃ ≈ -√(4 - 3 k²) - 2/(4 - 3 k²) γ }
```

解的形式为 $f(x) \approx c_1 e^{p_1 x} + c_2 e^{p_2 x} + c_3 e^{p_3 x}$。我们考察 $\gamma \ge 0$，并且对于 $x \to +\infty$，我们要求 (4.18) 的解 $f(x)$ 有界，因此 $$f(x) \approx f_+(x) = c_3 e^{p_3 x}。$$

接下来，考察 (4.19) 的形式 $$g''_+(x) - k^2 g_+(x) = k^2 f_+(x) + f''_+(x) = c_3 \left(k^2 + p_3^2\right) e^{p_3 x}$$ 解为 $$g_+(x) = \beta_1 e^{+k x} + \beta_2 e^{-k x} + c_3 \frac{k^2 + p_3^2}{p_3^2 - k^2} e^{p_3 x}。$$

由于该解必须在 $x \to +\infty$ 时保持有界，我们得到 $$g_+(x) = \beta_2 e^{-k x} + c_3 \frac{k^2 + p_3^2}{p_3^2 - k^2} e^{p_3 x}。$$

对于 $\gamma \ge 0$ 且 $x \to -\infty$ 的情况，类似地得到 $$f(x) \approx f_-(x) = c_1 e^{p_1 x} + c_2 e^{p_2 x}$$ 且 $$g(x) \approx g_-(x) = \beta_1 e^{+k x} + c_1 \frac{k^2 + p_1^2}{p_1^2 - k^2} e^{p_1 x} + c_2 \frac{k^2 + p_2^2}{p_2^2 - k^2} e^{p_2 x}。$$

对于 $0 < k^2 \ll 1$ 我们得到 (4.22) $$p_1^2 \approx \frac{4^2}{(4 - 3 k^2)^2} \gamma^2 \approx \gamma^2$$ 因此上述 $g(x)$ 的公式对于 $\gamma^2 \approx k^2 \ll 1$ 可能无效。对于 $k = 0$，$g$ 的方程简化为 $g''(x) = f''(x)$，并且 $x = \pm \infty$ 处的条件意味着 $g(x) = f(x)$。

### 4.3.2. 中间 |x| 的解

选择一个大的值 $M > 0$，我们构造 (4.14)–(4.15) 在 $-\infty < x \le -M$、$-M \le x \le +M$ 以及 $+M \le x < +\infty$ 时的非平凡解。我们寻求参数 $(c_1, c_2, c_3, \beta_1, \beta_2)$ 的非零值，使得我们找到一个非零解。利用解 $f_-$ 和 $g_-$ 定义矩阵

$$\mathbf{T}_- = \begin{bmatrix} e^{-p_1 M} & e^{-p_2 M} & 0 & 0 & 0 \\ p_1 e^{-p_1 M} & p_2 e^{-p_2 M} & 0 & 0 & 0 \\ p_1^2 e^{-p_1 M} & p_2^2 e^{-p_2 M} & 0 & 0 & 0 \\ \frac{p_1^2 + k^2}{p_1^2 - k^2} e^{-p_1 M} & \frac{p_2^2 + k^2}{p_2^2 - k^2} e^{-p_2 M} & 0 & e^{-k M} & 0 \\ \frac{(p_1^2 + k^2) p_1}{p_1^2 - k^2} e^{-p_1 M} & \frac{(p_2^2 + k^2) p_2}{p_2^2 - k^2} e^{-p_2 M} & 0 & k e^{-k M} & 0 \end{bmatrix}$$

其中 $$\mathbf{T}_- \begin{pmatrix} c_1 \\ c_2 \\ c_3 \\ \beta_1 \\ \beta_2 \end{pmatrix} = \begin{pmatrix} f(-M) \\ f'(-M) \\ f''(-M) \\ g(-M) \\ g'(-M) \end{pmatrix}$$

