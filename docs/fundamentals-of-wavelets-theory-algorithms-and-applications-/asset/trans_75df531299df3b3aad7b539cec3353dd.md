

```
x = conv(x,g0) + conv(y,g1);
a0_rec = x(4:length(x)-4);
% First level reconstruction
y = zeros(2*length(w0), 1);
y(1:2:2*length(w0)) = w0(1:length(w0));
x = zeros(2*length(a0_rec), 1);
x(1:2:2*length(a0_rec)) = a0_rec;
x = conv(x,g0);
y = conv(y,g1);
y = x(1:length(y))+y;
s_rec = y(4:length(y)-4);
```

```
% Plot
figure(2)
subplot(3,2,1), plot(a1)
ylabel('a_ {-1}')
subplot(3,2,2), plot(w1)
ylabel('w_ {-1}')
subplot(3,2,3), plot(a0_rec)
ylabel('Reconstructed a_0')
subplot(3,2,4), plot(w0)
ylabel('w_ 0')
subplot(3,2,5), plot(s_rec)
ylabel('Reconstructed Signal')
```

## 注记

- 一个函数 \(f \in L^2(\mathbb{R})\) 具有线性相位，如果
```
\tilde{f}(\omega) = \pm |\hat{f}(\omega)| e^{-j a \omega}
```
其中 \(a\) 是某个实常数。函数 \(f\) 具有广义线性相位，如果
```
\tilde{f}(\omega) = \tilde{g}(\omega)e^{-j a \omega + b}
```
其中 \(\tilde{g}(\omega)\) 是实值函数，常数 \(a\) 和 \(b\) 也是实值。为了避免信号重建中的失真，滤波器必须具有线性或广义线性相位。

## 7.13 参考文献

- 1. C. K. Chui, J. C. Goswami, and A. K. Chan. “时-尺度域稠密集上的快速积分小波变换.” Numer. Math. (1995), 283–302.
- 2. J. C. Goswami, A. K. Chan, and C. K. Chui. “基于样条的快速积分小波变换算法.” In 超宽带短脉冲电磁学 2, ed. L. Carin and L. B. Felsen. New York: Plenum Press, 1995, 455–463.
- 3. G. Strang and T. Nguyen. 小波与滤波组. Wellesley: Wellesley-Cambridge Press, 1996.
- 4. P. P. Vaidyanathan. *多速率系统与滤波组*. Upper Saddle River, NJ: Prentice Hall, 1993.
- 5. M. Vetterli and J. Kovacevic. *小波与子带编码*. NJ: Prentice Hall, 1995.
- 6. A. N. Akansu and R. A. Haddad. *多分辨率信号分解*. Boston: Academic Press, 1992.
- 7. A. N. Akansu and M. J. Smith, (eds.) *子带与小波变换*. Boston: Kluwer Academic Press, 1995.

## 第八章

## 小波与算法专题

在第 7 章中，我们讨论了标准小波分解与重建算法。通过应用第 5.6 节所述的最优阶局部样条插值方案，我们得到了所需 B-样条级数表示的系数序列 $a^M$。然后，根据线性或三次样条插值的选择，我们应用变基序列（第 7.5 节）以获得双级数表示的系数序列 $\tilde{a}^M$，用于 FIR 小波分解。

按照第 7 章所述实现方案得到的典型时-尺度网格如图 7.7 所示。换言之，通过遵循此方案，可以（实时）获得给定信号在图 7.7 所示时-尺度位置上的 IWT 值。然而，在许多信号分析应用中，例如一些雷达和声纳应用中使用的宽带相关处理 [1]，关于 $f$ 在如此稀疏的二元点集合（如图 7.7 所示）上的 IWT 信息，对于信号所需的时频分析来说是不够的。因此，有必要在非二元点上也计算 IWT。通过在所有二元尺度上保持相同的时间分辨率，可以规避与标准小波分解算法相关的混叠和时变困难。此外，如本章将所示，仅在二元尺度上计算可能不适合分离函数的所有频率内容。

Rioul 和 Duhamel [2] 以及 Shensa [3] 引入并研究了一种用于以更精细时间分辨率计算 IWT 的算法。此外，在以更精细频率分辨率快速计算 IWT 方面也取得了一些进展，例如每八度多声道（mvpo）方案，该方案最初在参考文献 [4] 中提出（另见 [5]），后来由 Rioul 和 Duhamel [2] 借助 FFT 进行了改进。然而，mvpo 方案（无论是否使用 FFT）的计算复杂度会随尺度参数 $a$ 的取值数量而增加。例如，在基于 FFT 的计算方案中，信号和分析小波都必须以相同的采样率进行采样，采样率由信号的最高频率含量（或最小尺度参数）决定，并且对于任何固定的信号离散化，该采样率在随后的较大尺度值上无法更改。此外，即使在最高频率级别上，小波在时域中的宽度最窄，小波所需的采样数据数量也将显著大于金字塔算法中的分解系数数量。

本章将讨论快速积分小波变换（FIWT）。其他小波和算法，如脊小波、曲线小波、复小波和提升算法，将被简要描述。

## 8.1 快速积分小波变换

如前所述，在许多应用中，在时-尺度域的稠密点集上计算小波变换非常重要。本文介绍了一种快速算法 [6-8]。

### 8.1.1 更精细的时间分辨率

在本节中，我们将关注通过在每个尺度的时间轴上填充“空洞”来保持每个尺度上的相同时间分辨率——也就是说，我们希望计算 \((W_\psi x_M)(n/2^M, 1/2^s), n \in \mathbb{Z}, s < M\)。回顾第 7 章中讨论的标准算法仅在二元点 \(\{n/2^s, 1/2^s; n \in \mathbb{Z}, s < M\}\) 处给出 IWT 值。为了获得更精细的时间分辨率，我们首先观察到，对于每个固定的 \(n\)，通过引入符号

```
x_{M,n}(t) := x_M\left(t + \frac{n}{2^M}\right),
(8.1)
```

我们有

```
(W_\psi x_M)\left(\frac{n}{2^M}, \frac{1}{2^s}\right) = 2^{s/2} \int_{-\infty}^\infty x_M(t) \overline{\psi\left(2^s\left(t - \frac{n}{2^M}\right)\right)} dt
= 2^{s/2} \int_{-\infty}^\infty x_M\left(t + \frac{n}{2^M}\right) \overline{\psi\left(2^s t\right)} dt
= (W_\psi x_{M,n})\left(0, \frac{1}{2^s}\right).
(8.2)
```

现在，由于

```
x_M(t) = \sum_k \tilde{a}_{k,M} \tilde{\phi}(2^M t - k),
(8.3)
```

我们有

```
x_{M,n}(t) = \sum_k \tilde{a}_{k,M} \tilde{\phi}(2^M t + n - k)
= \sum_k \tilde{a}_{n+k,M} \tilde{\phi}(2^M t - k).
(8.4)
```

因此，我们从 (8.2) 观察到，$x_M$ 在 $(n/2^M, 1/2^s)$ 处的 IWT 与 $x_{M,n}$ 在 $(0, 1/2^s)$ 处的 IWT 相同。一般而言，对于每个 $k \in \mathbb{Z}$，我们甚至有

```
(W_\psi x_{M,n})(\frac{k}{2^s}, \frac{1}{2^s}) = 2^{s/2} \int_{-\infty}^{\infty} x_{M,n}(t) \overline{\psi(2^s t - k)} dt
= 2^{s/2} \int_{-\infty}^{\infty} x_M(t + \frac{n}{2^M}) \overline{\psi(2^s t - k)} dt
= 2^{s/2} \int_{-\infty}^{\infty} x_M(t) \overline{\psi(2^s t - k - \frac{n2^s}{2^M})} dt
= (W_\psi x_M)(\frac{k2^{M-s} + n}{2^M}, \frac{1}{2^s}),
(8.5)
```

其中 $s < M$。因此，对于任何固定的 $s$ 和 $M$（$s < M$），由于每个整数 $\ell$ 都可以表示为 $k2^{M-s} + n$，其中 $n = 0, ..., 2^{M-s} - 1$ 且 $k \in \mathbb{Z}$，我们通过将第 7 章的标准小波分解算法应用于函数 $x_{M,p}$，获得了 $x_M$ 在 $(2^M, 1/2^s)$ 处的所有 IWT 值 $(W_\psi f_M)(\frac{\ell}{2^M}, \frac{1}{2^s}) =: 2^{-s/2} \tilde{w}_{2^{1-M}s}$ (8.6)，其中 $s \in \mathbb{Z}$ 且 $s < M$。$s = M-1, M-2$ 和 $M-3$（但仅限 $r = 0, ..., 3$）的时-尺度网格如图 8.1 所示。

**图 8.1：** 沿时间轴填充空洞。

![](img/f73ae67732328dc36596b27ffe8d0152_355_0.png)

为了实现，我们需要符号

(8.7) $w_s = \{ \tilde{w}_{k 2^{1-M}s} \}_{k \in \mathbb{Z}}$ 和 $a_s = \{ \tilde{a}_{k 2^{1-M}s} \}_{k \in \mathbb{Z}}$，使得 $a_M = \tilde{a}_M$，

以及上采样操作的符号

(8.8)
\[
\sigma^p = \begin{cases} \text{恒等算子} & \text{对于 } p=0 \\ \sigma^{p-1}\sigma & \text{对于 } p \ge 1, \end{cases}
\]

其中

(8.9)
\[
\sigma \{x_n\} = \{y_n\}, \text{ 其中 } y_n = \begin{cases} x_{n/2} & \text{对于偶数 } n; \\ 0 & \text{对于奇数 } n. \end{cases}
\]

作为 (8.2) 和 (7.45) 的结果，对于 \(s = M - 1\)，我们有

(8.10)
\[
\begin{aligned} (\tilde{g}_1 * \tilde{a}_M)_n &:= \sum_k \tilde{g}_1[k] \tilde{a}_{n-k, M} \\ &= \sum_k \tilde{g}_1[-k] \bar{a}_{n+k}^M \\ &= 2^{(M-1)/2} (W_\psi x_{M,n}) \left(0, \frac{1}{2^{M-1}}\right) \\ &= \bar{a}_{n/2, M-1}. \end{aligned}
\]

以类似的方式可以证明

(8.11)
\[
\tilde{a}_{n/2, M-1} = (\tilde{g}_0 * \tilde{a}_M)_n.
\]

也就是说，根据 (8.7) 和 (8.8) 中的符号，我们有

