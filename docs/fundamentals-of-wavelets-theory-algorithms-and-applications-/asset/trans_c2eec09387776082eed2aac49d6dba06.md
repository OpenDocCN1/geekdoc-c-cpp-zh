

(4.56) \(|G_\phi f(b, \xi)| = \frac{1}{2\pi} |\hat{\phi}(\omega_0 - \xi)|\)

(4.57) \(|W_\psi f(b, a)| = \frac{\sqrt{a}}{2\pi} |\hat{\psi}(a\omega_0)|.\)

从(4.56)和(4.57)可以清楚地看出，\(|G_\phi f(b, \xi)|\)和\(|W_\psi f(b, \xi)|\)不依赖于\(b\)。在频率轴上，由于\(|\hat{\phi}(0)| = 1\)，并假设\(|\hat{\phi}(\omega)| \le 1, \omega \neq 0\)，我们将在\(\xi = \omega_0\)处得到STFT的最大幅值。然后在\(\xi = \omega_0\)附近会有一个带，其宽度将取决于\(\Delta \hat{\phi}\)，即\(\hat{\phi}(\omega)\)的半径。

(4.57)的解释稍微复杂一些，因为与STFT不同，小波变换不会直接给出时频图。让我们考虑频率轴上的一个点\(\omega'，使得

(4.58) \(|\hat{\psi}(\omega')| = \max \{|\hat{\psi}(\omega)|; \omega \in (0, \infty)\}.\)

就所有实际目的而言，我们可以取\(\omega' = \omega^*\)。

现在如果我们考虑一个变量\(\xi = \omega^*/a\)并用新变量\(\xi\)重写(4.57)，我们有

(4.59) \(\left| W_\psi f \left( b, \frac{\omega^*}{\xi} \right) \right| = \frac{1}{2\pi} \sqrt{\frac{\omega^*}{\xi}} \left| \hat{\psi} \left( \frac{\omega^*}{\xi} \omega_0 \right) \right|.\)

因此，小波变换(4.57)的最大值将出现在\(\xi = \omega_0\)处，在\(\xi = \omega_0\)附近有一个带，其宽度取决于小波\(\tilde{\psi}(\omega)\)的半径\(\Delta_{\psi}^{\frac{1}{2}}\)。

作为下一个例子，令\(f(t) = \delta(t - t_0)\)。由于该函数包含所有频率分量，我们应当期望在时频平面上，在\(t = t_0\)处得到一条垂直线。将\(f(t) = \delta(t - t_0)\)代入(4.7)和(4.32)，我们得到

\(|G_{\phi}f(b, \xi)| = |\phi(t_0 - b)|.\) (4.60)

\(|W_{\psi}f(b, a)| = \frac{1}{\sqrt{a}} \left|\psi(\frac{t_0 - b}{a})\right|.\) (4.61)

STFT的解释很简单。如预期，它不依赖于\(\xi\)。我们得到一条近\(b = t_0\)处的、与频率轴平行的垂直线，其时域展宽由\(\Delta_{\phi}\)决定。对于小波变换，我们观察到它依赖于尺度参数\(a\)。用新变量\(\xi\)重写(4.61)，我们有

\(\left|W_{\psi}f\left(b, \frac{\omega^*_{\psi}}{\xi}\right)\right| = \sqrt{\frac{\xi}{\omega^*_{\psi}}} \left|\psi\left(\frac{\xi}{\omega^*_{\psi}}(t_0 - b)\right)\right|.\) (4.62)

虽然(4.62)表明了时域中三角函数的所有频率内容，但很明显，随着\(\xi\)的减小，时域展宽会增加。此外，最大值的位置将取决于\(\psi(t)\)的形状。读者可参考[4]以获取关于时频图解释的更多信息。

## 4.9 维格纳-维尔分布

在前面的章节中，我们已经考虑了信号的线性时频表示。STFT和CWT是线性变换，因为它们满足线性叠加定理：

(4.63) \( T[\alpha_1 f_1 + \alpha_2 f_2] = \alpha_1 T[f_1] + \alpha_2 T[f_2], \)

其中\(T\)可以表示STFT或CWT，\(f_1(t), f_2(t)\)是同一类中的两个不同信号，系数分别为\(\alpha_1\)和\(\alpha_2\)。这些变换很重要，因为它们提供了信号在时间\(t\)附近的*局部频谱*的解释。此外，其算法实现简便且计算效率高，增加了它们的优势。另一方面，这些线性变换无法提供信号在特定时刻的瞬时能量信息。直觉上，我们希望考虑如下类型的变换

\[
\int_{-\infty}^{\infty} |f(\tau - t)|^2 e^{-j\sigma\tau} d\tau = \int_{-\infty}^{\infty} f(t - \tau) \overline{f(t + \tau)} e^{-j\sigma\tau} d\tau.
\]

由于在给定时间确定信号的能量并不容易，因此考虑以时间位置\(t\)为中心的区间\((t - \tau/2, t + \tau/2)\)内的能量更有意义。为此，维格纳-维尔分布(WVD)定义为

\[
\mathbf{W}_f(t, \omega) = \frac{1}{2\pi} \int_{-\infty}^{\infty} f\left(t + \frac{\tau}{2}\right) \overline{f\left(t - \frac{\tau}{2}\right)} e^{-j\omega\tau} d\tau. \tag{4.64}
\]

常数\(1/2\pi\)是为了计算简便的归一化因子。我们应该注意，方程(4.64)不再满足线性性质。维格纳-维尔分布是一种非线性（或双线性）时频变换，因为信号在积分中出现了多次。人们还可以观察到，在给定时间\(t\)处，维格纳-维尔分布在距离\(\tau/2\)处对称地观察信号的左右两侧。计算\(\mathbf{W}_f(t, \omega)\)需要\(t \pm \tau/2\)处的信号信息，无法实时进行。

### 4.9.1 高斯调制啁啾

让我们考虑一个由高斯包络调制的啁啾信号

\[
f(t) = \left(\frac{a}{\pi}\right)^{\frac{1}{4}} \exp\left(\frac{-at^2}{2} + j\frac{bt^2}{2} + j\omega_0 t\right) \tag{4.65}
\]

其中\(\exp(-at^2/2)\)是高斯项，\(\exp(-jbt^2/2)\)是啁啾信号，\(e^{j\omega_0 t}\)是频移项。根据(4.64)，维格纳-维尔分布给出

(4.66)
\(\mathbf{W}_f(t,\omega) = \frac{1}{2\pi} \left(\frac{a}{\pi}\right)^{\frac{1}{2}} \int_{-\infty}^{\infty} \exp \left[ \frac{-a \left(t + \frac{\tau}{2}\right)^2}{2} + j \frac{b \left(t + \frac{\tau}{2}\right)^2}{2} + j\omega_0 \left(t + \frac{\tau}{2}\right) \right] \times \exp \left[ \frac{-a \left(t - \frac{\tau}{2}\right)^2}{2} - j \frac{b \left(t - \frac{\tau}{2}\right)^2}{2} - j\omega_0 \left(t - \frac{\tau}{2}\right) - j\omega \tau \right] d\tau = \frac{1}{2\pi} \left(\frac{a}{\pi}\right)^{\frac{1}{2}} e^{-a^2} \int_{-\infty}^{\infty} \exp \left( \frac{-a\tau^2}{4} + jbt\tau + j\omega_0\tau - j\omega \tau \right) d\tau.\)

使用第3章中给出的高斯函数的傅里叶变换，高斯调制啁啾的WVD为

(4.67)
\(\mathbf{W}_f(t,\omega) = \frac{1}{\pi} \exp \left( -\frac{a t^2}{2} - \frac{(\omega - \omega_0 - bt)^2}{a} \right).\)

该函数及其WVD如图4.9所示。

**图4.9：** 高斯调制啁啾信号的维格纳-维尔分布。

![](img/f73ae67732328dc36596b27ffe8d0152_162_0.png)

![](img/f73ae67732328dc36596b27ffe8d0152_162_1.png)

### 4.9.2 正弦调制啁啾

正弦调制啁啾信号由以下给出

\[
f(t) = \exp\left(j \frac{bt^2}{2} + j\omega_0 t\right). \tag{4.68}
\]

我们直接计算WVD以得到

(4.69)
\(\mathbf{W}_f(t,\omega)=\frac{1}{2\pi}\int_{-\infty}^{\infty} \exp \left( j \frac{b \left( t+\frac{\tau}{2} \right)^2}{2} + j \omega_0 \left( t+\frac{\tau}{2} \right) \right)\)
\(\times \exp \left( -j \frac{b \left( t-\frac{\tau}{2} \right)^2}{2} - j \omega_0 \left( t-\frac{\tau}{2} \right) - j \omega \tau \right) d\tau\)
\(= \frac{1}{2\pi} \int_{-\infty}^{\infty} \exp(jbt\tau + j\omega_0 \tau - j\omega \tau) d\tau\)
\(= \delta(\omega - \omega_0 - bt).\)

### 4.9.3 正弦信号

我们通过将啁啾参数\(b\)设为零，计算纯正弦信号\(e^{j\omega_0 t}\)的WVD。因此，

(4.70) \(e^{j\omega_0 t} \Longleftrightarrow \delta(\omega - \omega_0).\)

方程(4.67)和(4.69)的WVD在时频平面上分别是一条斜率为\(b\)的直线和一条与时间轴平行的直线。它们分别给于图4.10和图4.11。图4.12显示了高斯调制正弦函数的WVD。

图4.10：啁啾信号的维格纳-维尔分布。

![](img/f73ae67732328dc36596b27ffe8d0152_164_0.png)

![](img/f73ae67732328dc36596b27ffe8d0152_164_1.png)

图4.11：正弦函数的维格纳-维尔分布。

![](img/f73ae67732328dc36596b27ffe8d0152_165_0.png)

**图4.12：** 高斯调制正弦波的维格纳-维尔分布。

