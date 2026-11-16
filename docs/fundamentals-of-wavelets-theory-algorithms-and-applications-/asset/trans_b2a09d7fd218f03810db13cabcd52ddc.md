

![](img/f73ae67732328dc36596b27ffe8d0152_166_0.png)

![](img/f73ae67732328dc36596b27ffe8d0152_166_1.png)

## 4.10 WIGNER-VILLE 分布的性质

WVD 具有若干对信号处理中信号表示至关重要的一般性质。本节将讨论其中一些性质。文献 [5] 已表明，Wigner-Ville 分布在时频平面上具有最高的信号能量集中度。任何比 WVD 具有更高能量集中度的分布都将违反不确定性原理。此外，它无法满足本节所讨论的所谓边缘性质。

### 4.10.1 实量

Wigner-Ville 分布始终是实数，无论信号是实信号还是复信号。通过考虑 Wigner-Ville 分布的共轭复数可以看出这一点：

$$
\begin{aligned}
\overline{\mathbf{W}_s(t, \omega)} &= \frac{1}{2\pi} \int_{-\infty}^{\infty} s\left(t - \frac{\tau}{2}\right) \overline{s\left(t + \frac{\tau}{2}\right)} e^{j\omega\tau} d\tau \\
&= \frac{1}{2\pi} \int_{-\infty}^{\infty} s\left(t + \frac{\tau}{2}\right) \overline{s\left(t - \frac{\tau}{2}\right)} e^{-j\omega\tau} d\tau \\
&= \mathbf{W}_s(t, \omega).
\end{aligned}
$$

(4.71)

Wigner-Ville 分布始终是实数，但并非始终为正。图 4.13 显示了一个在中心附近变为负值的函数的 WVD。因此，WVD 可能不适用于作为能量密度或概率密度的度量。

**图 4.13:** 指示 Wigner-Ville 分布可能为负的图。

### 4.10.2 边缘性质

信号处理中尤其关注能量守恒。这由分布的边缘性质来表达

(4.72)
\(\int_{-\infty}^{\infty} \mathbf{W}_f(t, \omega) d\omega = |f(t)|^2\)

(4.73)
\(\int_{-\infty}^{\infty} \mathbf{W}_f(t, \omega) dt = |\hat{f}(\omega)|^2\)

边缘（密度）仅用两个变量中的一个来表示能量密度。如果我们希望用 t 表示能量密度，只需对分布关于 \(\omega\) 进行积分（求和），反之亦然。信号的总能量可以通过对整个时频平面上的 Wigner-Ville 分布进行二维积分来计算。

$$
E = \int_{-\infty}^{\infty} |f(t)|^2 dt = \int_{-\infty}^{\infty} |\hat{f}(\omega)|^2 d\omega = \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} W_f(t, \omega) d\omega dt = 1.
$$

### 4.10.3 相关函数

我们可以轻松地从边缘性质中计算时域或频域的相关函数：

(4.74) \(\gamma_f(\tau') = \int_{-\infty}^{\infty} f(\tau) \overline{f(\tau + \tau')} d\tau = W_f(\tau', 0)\)

(4.75) \(\gamma_\omega(\omega') = \int_{-\infty}^{\infty} f(\omega) \overline{f(\omega + \omega')} d\omega = W_f(0, \omega').\)

## 4.11 二次叠加原理

我们回顾一下，WVD 是一个非线性分布，线性叠加原理不适用。例如，设一个多分量信号为

(4.76) \(f(t) = \sum_{k=1}^m f_k(t).\)

该信号的 Wigner-Ville 分布为

$$
\mathbf{W}_f(t, \omega) = \sum_{k=1}^m \mathbf{W}_{f_k}(t, \omega) + \sum_{k=1}^m \sum_{l=1, l \neq k}^m \mathbf{W}_{f_k, f_l}(t, \omega),
$$

(4.77)

其中 \(\mathbf{W}_{f_k}(t, \omega)\) 称为 WVD 的自项，而 \(\mathbf{W}_{f_k, f_l}(t, \omega)\) 是由以下定义的交叉项：

$$
\mathbf{W}_{f_k, f_l}(t, \omega) = \frac{1}{2\pi} \int_{-\infty}^{\infty} f_k \left(t + \frac{\tau}{2}\right) \overline{f_l \left(t - \frac{\tau}{2}\right)} e^{-j\omega\tau} d\tau.
$$

(4.78)

WVD 的这些交叉项也称为干扰项，代表多分量信号两个分量之间的能量交叉耦合。这些干扰项在大多数信号处理应用中是不希望的，许多研究工作都致力于减少这些项的贡献。我们必须记住，这些交叉项 [6, 7] 对于信号的完美重构是必要的。在信号检测和识别应用中，我们只关注发现具有显著能量的信号分量。由于不需要重构信号，交叉项变得不重要。

在雷达信号处理和雷达成像中，待处理信号具有类似线性啁啾或二次啁啾的时变频谱。使用 STFT 或 WT 表示啁啾信号会损失时频平面上的分辨率。然而，这些信号的 WVD 在时频平面上产生明确定义的能量集中，如图 4.10 所示。对于多分量信号，如果各分量的带宽重叠不太多，WVD 的能量集中在时频平面上会相距很远（见图 4.14）。然而，如果情况并非如此，则必须应用某种交叉干扰抑制技术，这会导致分辨率降低。

**图 4.14:** 多分量信号的 Wigner-Ville 分布。

![](img/f73ae67732328dc36596b27ffe8d0152_171_0.png)

## 4.12 模糊函数

模糊函数（AF）是 Wigner-Ville 分布的特征函数，在数学上定义为

$$
\mathbf{A}_f(u,v) = \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} e^{jut+jv\omega} W_f(t,\omega) dt d\omega.
$$

(4.79)

虽然 Wigner-Ville 分布是测量时频平面上信号能量密度的时频函数，但模糊函数是测量频移（多普勒）和时延平面上能量分布的分布。这是雷达信号处理中非常重要的函数，特别是在波形设计领域。本书末尾将介绍该函数的一些应用。

除了一个复常数外，我们可以用信号来表示 AF 为

(4.80) \(\mathbf{A}_f(\tau, \zeta) = K \int_{-\infty}^{\infty} f\left(t - \frac{\tau}{2}\right) \overline{f\left(t + \frac{\tau}{2}\right)} e^{-j\zeta t} dt,\)

其中 \(K\) 是一个复常数。该关系的证明可见文献 [8]。有关模糊函数的更多信息，读者可参阅 [9]。图 4.15 显示了啁啾信号的 AF。这种时频表示将在第 9 章中重新讨论，其中 *小波包* 与 Wigner-Ville 分布的组合应用于雷达信号检测。

**图 4.15:** 啁啾信号的模糊函数。

![](img/f73ae67732328dc36596b27ffe8d0152_173_0.png)

![](img/f73ae67732328dc36596b27ffe8d0152_173_1.png)

## 4.13 练习

- 1. 验证对于任何函数 \(\psi \in L^2(-\infty, \infty)\)，归一化函数 \(\psi_{k,s}(t) = 2^{s/2}\psi(2^s t - k)\)（其中 \(k, s \in \mathbb{Z}, t \in \mathbb{R}\)）与 \(\psi\) 具有相同的 \(L^2\) 范数：

\(\int_{-\infty}^{\infty} |\psi(t)|^2 dt = \int_{-\infty}^{\infty} |\psi_{k,s}(t)|^2 dt, \quad k, s \in \mathbb{Z}.\)

- 2. 考虑窗函数 \(g_a(t) = e^{-at^2}, a > 0\)。计算时域和频域中的窗宽并验证不确定性原理。

- 3. 帽函数 \(N_2\) 定义为

$$N_2(t) = \begin{cases} t & \text{for } 0 \le t < 1 \\ 2-t & \text{for } 1 \le t < 2 \\ 0 & \text{otherwise.} \end{cases}$$

计算 N2(t) 的时频窗。

- 4. 证明 \(\|f(t)\|^2 = \frac{1}{2\pi} \iint |G_\phi f(b, \xi)|^2 db \, d\xi\).

- 5. 已知 \(f(t) = \sin(\pi t^2)\)，并使用升余弦作为窗函数

$$\phi(t) = \begin{cases} 1 + \cos(\pi t), & |t| \le 1 \\ 0, & \text{otherwise,} \end{cases}$$

绘制窗移时域函数 \(f_3(t) = \overline{\phi(t-3)}f(t)\) 和 \(f_7(t)\) 及其频谱。

考虑时频原子或核

$$\begin{cases} \text{Re} \left[ \phi(t-4)e^{j4\pi t} + \phi(t-6)e^{j8\pi t} \right] \\ \text{Re} \left[ \phi(t-4)e^{j4\pi t} + \phi(t-6)e^{j6\pi t} \right] \end{cases}$$

绘制两个时频原子的频谱能量密度。评论两个原子的时频分辨率。

- 6. 在 CWT 中，证明归一化常数 \(1/\sqrt{a}\) 是使 \(\|\psi(t)\| = \|\psi_{b,a}(t)\|\) 所必需的。

