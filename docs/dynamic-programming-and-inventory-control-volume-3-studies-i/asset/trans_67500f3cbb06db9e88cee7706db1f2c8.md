

## 17.4. Q.V.I. 的解

从 $(a, A, B, b)$ 策略出发，我们将构造满足 (17.2.11)、(17.2.12)、(17.2.13) 的 $G^+(x), G^-(x)$。我们定义

(17.4.1)
$$
G^+_{ab}(x) = G^+_{ab}(a), \forall x \le a; \quad G^+_{ab}(x) = G^+_{ab}(a) + \int_a^x H^+_{ab}(\xi) d\xi, \forall x \ge a
$$

(17.4.2)
$$
G^-_{ab}(x) = G^-_{ab}(b), \forall x \ge b; \quad G^-_{ab}(x) = G^-_{ab}(b) - \int_x^b H^-_{ab}(\xi) d\xi, \forall x \le b,
$$

其中

(17.4.3)
$$
G^+_{ab}(a) = \frac{g^+(a) - c^+ \mu + \frac{\sigma^2}{2}(H^+_{ab})'(a)}{\alpha};
$$

(17.4.4)
$$
G^-_{ab}(b) = \frac{g^-(b) + c^- \mu + \frac{\sigma^2}{2}(H^-_{ab})'(b)}{\alpha}.
$$

我们首先验证

(17.4.5)
$$
G^+_{ab}(x) - G^-_{ab}(x) = (c^+ + c^-)x.
$$

由于

$(G^+_{ab})'(x) - (G^-_{ab})'(x) = H^+_{ab}(x) - H^-_{ab}(x) = c^+ + c^-$，

只需验证

(17.4.6)
$$
G^+_{ab}(a) - G^-_{ab}(a) = (c^+ + c^-)a.
$$

使用

$$
\begin{aligned}
G^-_{ab}(a) &= G^-_{ab}(b) - \int_a^b H^-_{ab}(\xi) d\xi \\
&= G^-_{ab}(b) - \int_a^b H^+_{ab}(\xi) d\xi + (c^+ + c^-)(b - a),
\end{aligned}
$$

以及公式 (17.4.3)、(17.4.4)，我们必须验证关系

$$
\begin{aligned}
g^+(a) - c^+ \mu + \frac{\sigma^2}{2}(H^+_{ab})'(a) \\
= g^-(b) + c^- \mu + \frac{\sigma^2}{2}(H^-_{ab})'(b) - a \int_a^b H^+_{ab}(\xi) d\xi + \alpha(c^+ + c^-)b,
\end{aligned}
$$

或

$$
-\frac{\sigma^2}{2}((H^-_{ab})'(b) - (H^+_{ab})'(a)) + \alpha \int_a^b H^+_{ab}(\xi) d\xi - (c^+ + c^-) \mu = f(b) - f(a) + \alpha c^+(b - a),
$$

这直接由 (17.3.6) 在 $a$ 和 $b$ 之间积分后得出。函数 $G^+_{ab}(x)$ 和 $G^-_{ab}(x)$ 满足 (17.3.1)、(17.3.2)、(17.3.3)。我们然后定义

我们注意到

$$
\begin{aligned}
AG^+(x) + \alpha G^+(x) &= g^+(x) - c^+ \mu, & \forall a < x < b \\
G^+(x) &= G^+_{ab}(a), & \forall x \le a \\
G^+(x) &= G^-_{ab}(b) + (c^+ + c^-)x, & \forall x \ge b
\end{aligned}
$$

因此，对于 \( x < a \)

\( AG^+(x) + \alpha G^+(x) = g^+(a) - c^+ \mu + \frac{\sigma^2}{2}(H_{ab}^+)'(a) \)。

接下来我们使用 \( (H_{ab}^+)'(a) < 0 \) 和

\( g^+(x) = f(x) + \alpha c^+ x = (-p + \alpha c^+)x \)
\( \ge (-p + \alpha c^+)a = g^+(a) \)

从而得出

\( AG^+(x) + \alpha G^+(x) \le g^+(x) - c^+ \mu, \quad \forall x < a \)。

对于 \( x > b \)，我们有

\( AG^+(x) + \alpha G^+(x) = -\mu(c^+ + c^-) + \alpha(c^+ + c^-)x \)
\( + g^-(b) + c^- \mu + \frac{\sigma^2}{2}(H_{ab}^+)'(b) \)。

然后我们使用 \( (H_{ab}^+)'(b) < 0 \) 和

\( g^-(b) = f(b) - \alpha c^- b = (h - \alpha c^-)b \le (h - \alpha c^-)b \)
\( = g^-(x) = g^+(x) - \alpha(c^+ + c^-)x \),

同样得出

\( AG^+(x) + \alpha G^+(x) \le g^+(x) - c^+ \mu, \quad \forall x > b \)。

接下来我们注意到，由于 $a, b$ 的选择，我们有

\( G_{ab}^+(a) = K^+ + \inf_{a < \eta < b} G_{ab}^+(\eta) \)

对于 \( x \le a \),

\( G^+(x) = G_{ab}^+(a) = K^+ + \inf_{a < \eta < b} G^+(\eta) \)
\( = K^+ + \inf_{x < \eta < b} G^+(\eta) = K^+ + \inf_{x < \eta} G^+(\eta) \)。

对于 \( x > a \)，要证明同样的不等式，我们需要验证

(17.4.7)
$$
0 \le K^+ + \inf_{x < \eta} \int_x^\eta H_{ab}^+(\xi) d\xi.
$$

对于 \( x > A $，这很明显，因为积分为正。因此我们可以考虑 $a \le x \le A$ 的情况。但此时

\( K^+ + \inf_{x < \eta} \int_x^\eta H_{ab}^+(\xi) d\xi = K^+ + \int_x^A H_{ab}^+(\xi) d\xi \)
\( \ge K^+ + \int_A^A H_{ab}^+(\xi) d\xi = 0 \)。

因此得到 (17.4.7)。考虑到 (17.2.11)，我们看到前两个不等式已满足。以同样的方式，我们验证 (17.2.12) 的前两个不等式也满足。最后，考虑三个区间 $(-\infty, a)$、$(a, b)$、$(b, +\infty)$，我们看到 (17.4.7) 和 (17.2.12) 中的第三个关系也满足。因此，我们通过 $(a, A, B, b)$ 策略找到了 Q.V.I. (17.2.11)、(17.2.12)、(17.2.13) 的一个解，从而也找到了 (17.2.6) 的解。

## 17.5. 计算方面

本节我们关注与求得四个数 $a, A, B, b$ 相关的计算方面。

### 17.5.1. A 和 B 的符号

我们知道 $A < B$ 且 $a < 0, b > 0$，但无法保证 $A, B$ 的符号。进一步研究这个问题很有意思。这也会在计算四个数时带来简化。考虑固定 $b$ 时求 $a(b)$。我们需要求解 $F(a(b), b) = 0$。但观察公式 (17.5.13) 可知，$F(a(b))$ 对 $b$ 的依赖仅通过 $A(a, b)$ 体现。因此，对于固定的 $b$，对子 $a(b), A(a(b), b)$ 可通过以下方程组求得

(17.5.1)
$$
F(a, b) = 0, H_{\alpha}^{+}(a) = 0.
$$

在求解该方程组时，计算过程取决于所求解 $A$ 的符号。若假设 $A < 0$，则对子 $a, A$ 成为下列方程组的解（回顾，在此框架下我们省略了写出固定正参数 $b$）

$$
K^{+} - \frac{1}{\alpha}(p - \alpha c^{+})(A - a) + \frac{1}{\alpha} \frac{p - \alpha c^{+}}{\beta_1 \beta_2} (\beta_1 - \beta_2) \frac{(\exp \beta_1(A - a) - 1)(\exp \beta_2(A - a) - 1)}{\exp \beta_1(A - a) - \exp \beta_2(A - a)} = 0
$$

$$
h - \alpha c^{+} - (p + h) \frac{\beta_1 \exp \beta_2 b - \beta_2 \exp \beta_1 b}{\beta_1 - \beta_2} = (p - \alpha c^{+}) \frac{\exp \beta_1(b - a)(\exp \beta_2(A - a) - 1) - \exp \beta_2(b - a)(\exp \beta_1(A - a) - 1)}{\exp \beta_1(A - a) - \exp \beta_2(A - a)}.
$$

此外，该方程组是逐次求解的。第一个方程定义 $A - a$ 且与 $b$ 无关。第二个方程将 $a$ 定义为 $b$ 的函数以及由第一个方程得到的 $A - a$ 的值。若定义函数

(17.5.2)
$$
Z(x) = -x + \frac{\beta_1 - \beta_2}{\beta_1 \beta_2} \frac{(\exp \beta_1 x - 1)(\exp \beta_2 x - 1)}{\exp \beta_1 x - \exp \beta_2 x},
$$

则第一个条件等价于

(17.5.3)
$$
Z(A - a) = \frac{-K^{+}\alpha}{p - \alpha c^{+}}.
$$

我们有

**引理 17.3.3.** 存在唯一的数 $\varpi > 0$，使得

(17.5.4)
$$
Z(\varpi) = \frac{-K^{+}\alpha}{p - \alpha c^{+}}.
$$

证明。我们计算

$$
Z'(x) = -1 + \frac{\beta_1 - \beta_2}{\beta_1 \beta_2} \frac{\beta_2 \exp \beta_2 x (\exp \beta_1 x - 1)^2 - \beta_1 \exp \beta_1 x (\exp \beta_2 x - 1)^2}{(\exp \beta_1 x - \exp \beta_2 x)^2}
$$
$$
= \frac{[\beta_2 (\exp \beta_1 x - 1) - \beta_1 (\exp \beta_2 x - 1)]}{\beta_1 \beta_2 (\exp \beta_1 x - \exp \beta_2 x)^2} \frac{[\beta_1 \exp \beta_1 x (\exp \beta_2 x - 1) - \beta_2 \exp \beta_2 x (\exp \beta_1 x - 1)]}{\beta_1 \beta_2 (\exp \beta_1 x - \exp \beta_2 x)^2}
$$

我们容易验证，对于 $x > 0$
$$
\beta_2(\exp \beta_1 x - 1) - \beta_1(\exp \beta_2 x - 1) < 0
$$
$$
\beta_1 \exp \beta_1 x (\exp \beta_2 x - 1) - \beta_2 \exp \beta_2 x (\exp \beta_1 x - 1) < 0
$$
因此 $Z'(x) \le 0$。此外，$Z(0) = 0$ 且 $Z(+\infty) = -\infty$。这蕴含了结果。

由 (17.5.3) 可断言
(17.5.5)
$$
A(a(b), b) - a(b) = \varpi \quad \text{if } A(a(b), b) \le 0.
$$

回到第二个条件，我们可以写出
(17.5.6)
$$
\begin{aligned}
h - \alpha c^- - (p+h) \frac{\beta_1 \exp \beta_2 b - \beta_2 \exp \beta_1 b}{\exp \beta_1 b - \exp \beta_2 b} &= (p - \alpha c^+) \ \frac{\exp \beta_1 b (a-b) (\exp \beta_2 \varpi - 1) - \exp \beta_2 b (a-b) (\exp \beta_1 \varpi - 1)}{\exp \beta_1 \varpi - \exp \beta_2 \varpi}
\end{aligned}
$$

这将 $a$ 定义为 $b$ 的函数。让我们引入数
(17.5.7)
$$
\varphi(\varpi) = \frac{\beta_1(\exp \beta_2 \varpi - 1) - \beta_2(\exp \beta_1 \varpi - 1)}{\exp \beta_1 \varpi - \exp \beta_2 \varpi},
$$

则有
$$
\varphi(\varpi) + \beta_1 = \frac{(\beta_1 - \beta_2)(\exp \beta_1 \varpi - 1)}{\exp \beta_1 \varpi - \exp \beta_2 \varpi}; \quad \varphi(\varpi) + \beta_2 = \frac{(\beta_1 - \beta_2)(\exp \beta_2 \varpi - 1)}{\exp \beta_1 \varpi - \exp \beta_2 \varpi},
$$

且 (17.5.6) 变形后变为
(17.5.8)
$$
L_\varpi(b-a) = \frac{\alpha(c^+ + c^-)(\beta_2 - \beta_1) + (p+h)[\beta_2(\exp \beta_1 b - 1) - \beta_1(\exp \beta_2 b - 1)]}{p - \alpha c^+},
$$

其中
(17.5.9)
$$
L_\varpi(x) = (\exp \beta_1 x - 1)(\varphi(\varpi) + \beta_2) - (\exp \beta_2 x - 1)(\varphi(\varpi) + \beta_1), \quad x \ge 0.
$$

我们也可以给出方程 (17.5.8) 的另一种表述。回顾 $Z^+(a, b)$ 的定义，我们容易验证 (17.5.8) 等价于

(17.5.10)
$$
\frac{Z^+(a, b)}{\exp \beta_1 b (a - b) - \exp \beta_2 b (a - b)} = \frac{\varphi(\varpi) - \alpha c^+}{\alpha(\beta_2 - \beta_1)}.
$$

现在，我们容易验证 $\varphi(0) = 0$。由 (17.3.13) 可知，当 $\varpi = 0$ 时，$a_0(b)$ 是 (17.5.10) 的唯一解。更一般地，我们提出

**引理 17.4.** 对于任何 $\varpi \ge 0$，存在唯一的 $a_\varpi(b)$ 解满足 (17.5.10)。

证明。当然，考虑方程 (17.5.8) 是等价的。函数 $L_\varpi(x)$ 满足

$$
\begin{aligned}
L'_\varpi(x) &= \beta_1(\varphi(\varpi) + \beta_2) \exp \beta_1 x - \beta_2(\varphi(\varpi) + \beta_1) \exp \beta_2 x; \\
L''_\varpi(x) &= (\beta_1)^2(\varphi(\varpi) + \beta_2) \exp \beta_1 x - (\beta_2)^2(\varphi(\varpi) + \beta_1) \exp \beta_2 x.
\end{aligned}
$$

我们注意到

(17.5.11)
$$
\varphi(\varpi) > 0, \quad \varphi(\varpi) + \beta_2 < 0,
$$

因此 $L''_\varpi(x)$ 是递减的，且

$$
L'_\varpi(0) = (\beta_1 - \beta_2)\varphi(\varpi), \quad L'_\varpi( +\infty ) = -\infty.
$$

