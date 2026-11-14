
因此

\(\sum_{j=[x-\hat{n}]+1}^{[x-s]} \frac{(g(x-j)-g(s))\lambda^j}{(\alpha+\lambda)^{j+1}} \le \frac{(h+p)\exp-\alpha L x^+}{\alpha}.\)

所以我们可以断言

\(\limsup_{s \to -\infty} \psi_s(x) \le \sum_{j=0}^{[x-\hat{n}]} \frac{(g(x-j)-g(s))\lambda^j}{(\alpha+\lambda)^{j+1}} + \frac{(h+p)\exp-\alpha L x^+}{\alpha}.\)

第一个求和式由若干项组成，每一项当 \(s \to -\infty\) 时都趋于 \(-\infty\)。这就完成了定理 14.3 的证明。

### 14.8.6. s, S 策略的最优性。

我们需要检查一组不等式和互补松弛条件。互补松弛性质显然得到满足。当 \(x < s\) 时，我们有

\(u_s(x) = -cx + E \int_0^L f(x-D(t)) \exp-\alpha t dt + \frac{g(s)+\lambda c}{\alpha},\)

并且我们必须检查

\((\alpha+\lambda)u_s(x) - \lambda u_s(x-1) \le f(x).\)

利用 \(u_s(x)\) 的值，这等价于 \(g(x) \ge g(s)\)，由于 \(s \le \hat{n}\)，这显然得到满足。

困难部分在于 \(x \ge s\) 的情况，此时必须满足不等式 (14.8.1)。代入 \(H_s(x)\) 后，这等价于

\(H_s(x) + (g(s)+\alpha c) \frac{1-\exp-\alpha L}{\alpha} \le K + c\alpha L \exp-\alpha L + \inf_{\eta \ge x} \left\{ cp(1-\exp-\alpha L) \right.\)
\(\left. + \exp-\alpha L E H_s(\eta-D(L)) + \int_0^L f(\eta-D(t+L)) \exp-\alpha t dt \right\}.\)

这可解释为

(14.8.13) \(H_s(x) \le K + \inf_{\eta \ge x} \psi_s(\eta).\)

由于右边为正，只有在 \(x > x_0\) 时才需要检查，其中 \(x_0\) 是 \(H_s(x)\) 首次为正或等于 0 的值。

回顾公式

\(H'_s(x+0) = \sum_{j=0}^{[x-s]} \frac{g'(x-j+0)\lambda^j}{(\alpha+\lambda)^{j+1}},\)

我们注意到 \(x_0 \ge \hat{n}\)。

对于整数 \(x\)，我们还可以写出公式

\(\left( \frac{\alpha+\lambda}{\lambda} \right)^x H'_s(x+0) = \sum_{k=-[x-s]}^x \frac{g'(k+0)}{\alpha+\lambda} \left( \frac{\alpha+\lambda}{\lambda} \right)^k .\)

然后考虑整数 \(x \ge x_0\)。我们可以假设 \(H'_s(x_0+0) \ge 0\)，这相当于假设在 \(x_0\) 稍后 \(H_s(x) > 0\)，否则我们要证明的性质在 \(x_0\) 之后成立。

因此

$$ \sum_{k=-\lceil s \rceil}^{x_0} \frac{g'(k+0)}{\alpha + \lambda} \left( \frac{\alpha + \lambda}{\lambda} \right)^k \ge 0. $$

由于对于 \( k \ge \tilde{n}, g'(k+0) \ge 0 \)，我们推导出

$$ \sum_{k=-\lceil s \rceil}^{x} \frac{g'(k+0)}{\alpha + \lambda} \left( \frac{\alpha + \lambda}{\lambda} \right)^k \ge 0, \forall x \ge x_0. $$

由此可见 \( H'_s(x+0) \ge 0, \forall x \ge x_0 \)。因此

$$ H_s(x) \le H_s(y), \forall y \ge x \ge x_0. $$

注意到 \( H_s(y) \le \psi_s(y), \forall y \ge s \)，我们轻易推导出

$$ H_s(x) \le K + \psi_s(y), \forall y \ge x \ge x_0, $$

证明已完成。

## 14.9. 带前置时间的泊松需求的遍历方法

### 14.9.1. 函数 \( \psi_s(x) \) 的研究。

我们现在考虑 \(\alpha = 0\) 的情况。首先得到

\( g(x) = E f(x - D(L)), \)

所以

\( g(x) = \begin{cases} -px + \lambda p L, & \text{if } x \le 0 \\ -p \sum_{k=\lceil x \rceil + 1}^{[x] + 1} (x - k) \frac{(\lambda L)^k}{k!} \exp -\lambda L + h \sum_{k=0}^{[x]} (x - k) \frac{(\lambda L)^k}{k!} \exp -\lambda L, & \text{if } x \ge 0 \end{cases} \)

接下来我们计算函数 \(\psi_s(x)\)。对于 \(x \ge s\)，我们有

\( \psi_s(x) = \frac{1}{\lambda} \left\{ \sum_{j=0}^{[x-s]} (g(x-j) - g(s)) + \exp -\lambda L \sum_{j=[x-s]+1}^{\infty} (g(x-j) - g(s)) \sum_{k=j+1}^{\infty} \frac{(\lambda L)^k}{k!} \right\}, \)

而对于 \(x \le s\)

\( \psi_s(x) = \frac{1}{\lambda} \sum_{j=0}^{\infty} (g(x-j) - g(s)) \sum_{k=j+1}^{\infty} \frac{(\lambda L)^k}{k!}. \)

在后续内容中，为稍作简化，我们假设 \(s\) 为整数。我们可以给出 \(\psi_s(x)\) 的显式公式，具体取决于 \(s\) 的符号。计算过程繁琐但并不困难。只需考虑 \(x \ge s\)。

假设 \(s \le x \le 0\) 为整数，我们有

(14.9.1) \( \psi_s(x) = pL(s - x) + \frac{1}{2} \lambda L^2 p - \frac{p}{\lambda} \exp -\lambda L \sum_{j=0}^{[x-s]} \frac{(\lambda L)^j}{j!} \cdot \left[ \left( x - \frac{1}{2} [x] - \frac{1}{2} j \right) ([x] - j + 1) - s(x - j) + \frac{s^2}{2} - \frac{s}{2} \right]. \)

我们利用以下事实

\( g(x) - g(s) = p(s - x), \)

当 \(s < x < 0\) 时。

接下来的情况是 \(s < 0 < x\)。注意，在这种情况下，

\(g(x) - g(s) = p(s - x) + (h + p)E(x - D(L))^+,\)

可以轻易验证，给出 \(\psi_s(x)\) 的公式是公式 (14.9.1) 加上一个额外项

\(\frac{h+p}{\lambda} \sum_{j=0}^{[x]} E(x - j - D(L))^+.\)

该项等于

\(\frac{h+p}{\lambda} \exp - \lambda L \sum_{j=0}^{[x]} \frac{(\lambda L)^j}{j!} \left(x - \frac{1}{2}[x] - \frac{1}{2}j\right)([x] - j + 1).\)

汇总结果，我们得到，对于 \(s < 0 < x\)

(14.9.2) \(\psi_s(x) = -pL(x - s) + \frac{1}{2}\lambda L^2 p + \frac{h}{\lambda} \exp - \lambda L \sum_{j=0}^{[x]} \frac{(\lambda L)^j}{j!} \left(x - \frac{1}{2}[x] - \frac{1}{2}j\right)([x] - j + 1) - \frac{p}{\lambda} \exp - \lambda L \sum_{j=s+[x]+1}^{[x] - s} \frac{(\lambda L)^j}{j!} \left(x - \frac{1}{2}[x] - \frac{1}{2}j\right)([x] - j + 1) + \frac{p}{\lambda} \exp - \lambda L \sum_{j=0}^{[x] - s} \frac{(\lambda L)^j}{j!} \left((x - j)s + \frac{s}{2} - \frac{s^2}{2}\right).\)

现在考虑 \(0 < s\) 的情况。我们回顾一下

\(g(x) - g(s) = p(s - x) + (h + p)E(x - D(L))^+ - (s - D(L))^+].\)

同样，我们需要向表达式 (14.9.1) 添加一个由以下给出的额外项

\(\frac{h+p}{\lambda} \sum_{j=0}^{[x] - s} E([(x - j - D(L))^+ - (s - D(L))^+] \\ + \exp - \lambda L \left[ \sum_{j=[x] - s + 1}^{\infty} E[(x - j - D(L))^+ - (s - D(L))^+] \sum_{k=j+1}^{\infty} \frac{(\lambda L)^k}{k!} \right]\)

我们可以将乘以 \(\frac{h+p}{\lambda}\) 的额外项表示如下

\(\exp - \lambda L \sum_{j=0}^{[x] - s - x} (x - j - s) \frac{(\lambda L)^k}{k!} + \exp - \lambda L \sum_{j=0}^{[x] - s - x} (x - j - k) \frac{(\lambda L)^k}{k!} \\ + \exp - 2\lambda L \lfloor_{j=[x] - s + 1}^{[x]} \sum_{m=0}^{k-j} \left( \sum_{m=0}^{[x] - j - s} (x - j - s) \frac{(\lambda L)^m}{m!} - \sum_{m=[x] - j + 1}^{s} (s - m) \frac{(\lambda L)^m}{m!} \right) \\ \cdot \sum_{k=j+1}^{\infty} \frac{(\lambda L)^k}{k!} \rfloor - \exp - 2\lambda L \sum_{j=[x] + 1}^{\infty} \sum_{m=0}^{\infty} (s - m) \frac{(\lambda L)^m}{m!} \sum_{k=j+1}^{\infty} \frac{(\lambda L)^k}{k!}\)

变换后我们得到

$$
\begin{aligned}
&\exp -\lambda L \sum_{k=0}^{s-1} \frac{(\lambda L)^k}{k!} ([x] - s + 1) \left( x - \frac{[x]}{2} - \frac{s}{2} \right) \\
&+ \exp -\lambda L \sum_{k=s}^{[x]} \frac{(\lambda L)^k}{k!} ([x] - k + 1) \left( x - \frac{[x]}{2} - \frac{k}{2} \right) \\
&+ \exp -2\lambda L \sum_{j=[x]+1}^{[x]} \sum_{m=s+1}^{[x]-j} \sum_{k=j+1}^{\infty} (x - j - s) \frac{(\lambda L)^m}{m!} \frac{(\lambda L)^k}{k!} \\
&- \exp -2\lambda L \sum_{j=[x]+1}^{[x]} \sum_{m=[x]-j+1}^{s} (s - m) \frac{(\lambda L)^m}{m!} \sum_{k=j+1}^{\infty} \frac{(\lambda L)^k}{k!} \\
&- \sum_{j=[x]+1}^{\infty} \sum_{m=s+1}^{\infty} (s - m) \frac{(\lambda L)^m}{m!} \sum_{k=j+1}^{\infty} \frac{(\lambda L)^k}{k!}.
\end{aligned}
$$

### 14.9.2. 局部最小值。

我们首先得到导数 \(\psi'_s(x + 0)\)。

对于 \(s < x < 0\)

(14.9.3) \(\psi'_s(x + 0) = -pL - \frac{p}{\lambda} \exp -\lambda L \sum_{j=0}^{[x]-s} ([x] - j + 1 - s) \frac{(\lambda L)^j}{j!}.\)

接下来我们考虑 \(s < 0 < x\) 的情况。我们有

(14.9.4) \(\psi'_s(x + 0) = -pL - \frac{p}{\lambda} \exp -\lambda L \sum_{j=[x]+1}^{[x]-s} ([x] - j + 1 - s) \frac{(\lambda L)^j}{j!} + \frac{\exp -\lambda L}{\lambda} \sum_{j=0}^{[x]} \frac{(\lambda L)^j}{j!} (h([x] - j + 1) + ps).\)

最后，对于 \(0 < s < x\)，我们有

(14.9.5) \(\psi'_s(x + 0) = -pL - \frac{p}{\lambda} \exp -\lambda L \sum_{j=0}^{[x]-s} ([x] - j + 1 - s) \frac{(\lambda L)^j}{j!} + \frac{h+p}{\lambda} \exp -\lambda L \left[ \sum_{j=0}^{s-1} \frac{(\lambda L)^j}{j!} ([x] - s + 1) + \sum_{j=s}^{[x]} \frac{(\lambda L)^j}{j!} ([x] - j + 1) - \exp -\lambda L \sum_{j=[x]+1}^{[x]+s} \sum_{l=j+1-s}^{\infty} \frac{(\lambda L)^l}{l!} \sum_{k=[x]+1}^{j} C_l^{j-k} \right].\)

我们可以验证对于 \(s < 0 < x\) 的公式

\(\psi'_s(x + 1 + 0) - \psi'_s(x + 0) = \exp -\lambda L \left[ \frac{h}{\lambda} \sum_{j=0}^{[x]+1-s} \frac{(\lambda L)^j}{j!} - \frac{p}{\lambda} \sum_{j=[x]+2}^{[x]+1-s} \frac{(\lambda L)^j}{j!} \right].\)
