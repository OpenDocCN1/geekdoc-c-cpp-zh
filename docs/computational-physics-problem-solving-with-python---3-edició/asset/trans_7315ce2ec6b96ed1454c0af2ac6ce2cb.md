

确定存在两个频率。在这种情况下，为了避免混叠，我们希望输入信号中不存在频率 $f>s/2$。这称为奈奎斯特准则（Nyquist criterion）。在实际应用中，一些应用通过滤除高频成分，然后只分析剩余的低频部分，来避免混叠的影响。（第 12.8.1 节讨论的低频 sinc 滤波器通常用于此目的。）虽然滤波会消除一些高频信息，但它会减小低频成分的失真，因此可能改善信号的重现效果。

如果需要高频的准确值，那么就需要通过增加在固定采样时间 $T=Nh$ 内采集的样本数量 $N$ 来提高采样率 $s$。保持采样时间不变并增加采样数量，可以使时间步长 $h$ 变小，并捕获更高的频率。增加 $N$，即增加频率数量并进行计算，会使之前较高的频率成分更靠近频谱中部，从而远离容易产生误差的两端。

如果增加总采样时间 $T=Nh$ 而保持 $h$ 不变，那么采样率 $s=N/T=1/h$ 保持不变。由于 $\omega_1=2\pi/T$，这会使 $\omega_1$ 变小，从而记录更多低频，并得到更平滑的频谱。正如我们所说的，这通常是在事后通过在数据集末尾补零来实现的。

**Listing 12.2** `DFTreal.py` 使用实数计算方法 `f(signal)` 的离散傅里叶变换。

```python
# DFTreal.py: Discrete Fourier Transform using real numbers

from visual.graph import *

signgr = gdisplay(x=0,y=0,width=600,height=250, \
                  title='Signal y(t)=3 cos(wt)+2 cos(3wt)+ cos(5wt) ', \
                  xtitle='x', ytitle='signal', xmax=2.*math.pi,xmin=0,ymax=7,ymin=-7)
signfig = gcurve(color=color.yellow,display=signgr)
imagr = gdisplay(x=0,y=250,width=600,height=250,\
        title='Fourier transform imaginary part',xtitle='x',\
        ytitle='Transf.Imag',xmax=10.0,xmin=-1,ymax=20,ymin=-25)
impart = gvbars(delta=0.05,color=color.red,display=imagr)

N = 200
Np = N
signal = zeros((N+1),float)
twopi = 2.*pi
sq2pi = 1./sqrt(twopi)
h = twopi/N
dftimag = zeros((Np),float)                         # Im. transform

def f(signal):
    step = twopi/N
    t = 0.
    for i in range(0,N+1):
        signal[i] = 3*sin(t*t*t)
        signfig.plot(pos=(t,signal[i]))
        t += step

def fourier(dftimag):                                      # DFT
    for n in range(0,Np):
        imag = 0.
        for k in range(0, N):
            imag += signal[k]*sin((twopi*k*n)/N)
        dftimag[n] = -imag*sq2pi                         # Im transform
        if dftimag[n] != 0:
            impart.plot(pos=(n,dftimag[n]))

f(signal)
fourier(dftimag)
```

### 12.5.2 Fourier Series DFT (Example)

为简化起见，让我们考虑傅里叶余弦级数：

$$y(t)=\sum_{n=0}^{\infty}a_n\cos(n\omega t),\qquad a_k=\frac{2}{T}\int_0^T dt\,\cos(k\omega t)y(t). \tag{12.42}$$

这里 $T\overset{\mathrm{def}}{=}2\pi/\omega$ 是系统的实际周期（不一定是小振幅下简谐运动的周期）。我们假设函数 $y(t)$ 在离散时间集合上采样

$$y(t=t_k)\equiv y_k,\qquad k=0,1,\ldots,N. \tag{12.43}$$

由于我们分析的是周期函数，我们保留 DFT 中使用的约定，要求函数以周期 $T=N h$ 重复自身；也就是说，我们假设第一个和最后一个点的振幅相同：

$$y_0=y_N. \tag{12.44}$$

这意味着作为输入使用的 $y$ 的独立值只有 $N$ 个。对于这 $N$ 个独立的 $y_k$ 值，我们只能唯一确定 $N$ 个展开系数 $a_k$。如果我们使用梯形法则近似 (12.42) 中的积分，我们确定 $N$ 个独立的傅里叶分量为

$$a_n \approx \frac{2h}{T}\sum_{k=1}^N \cos(n\omega t_k)\, y(t_k) = \frac{2}{N}\sum_{k=1}^N \cos\left(\frac{2\pi n k}{N}\right) y_k, \qquad n=0,\ldots,N.$$

由于我们只能从 $N$ 个独立的 $y(t)$ 值确定 $N$ 个傅里叶分量，我们对 $y(t)$ 的傅里叶级数必须仅以这些分量表示：

$$y(t) \approx \sum_{n=0}^N a_n \cos(n\omega t) = \sum_{n=0}^N a_n \cos\left(\frac{2\pi n t}{N h}\right).$$

总之，我们在 $N$ 个时间 $t_1,\ldots,t_N$ 上采样函数 $y(t)$。我们看到所有采样的 $y$ 值都对每个 $a_k$ 有贡献。因此，如果我们增加 $N$ 以确定更多系数，我们必须重新计算所有 $a_n$ 值。在第 13 章的波分析中，理论被重新表述，使得额外的采样可以确定更高的谱分量而不影响较低的分量。

### 12.5.3 Assessments

**简单解析输入**

在研究更复杂的问题之前，即使你使用的是软件包的傅里叶工具，做一些简单的检查总是好的。

- 1. 采样偶信号

  $$y(t) = 3\cos(\omega t) + 2\cos(3\omega t) + \cos(5\omega t).$$

  - a) 将其分解为其分量。
  - b) 检查分量基本上是实数且比例为 3 : 2 : 1（或功率谱为 9 : 4 : 1）。
  - c) 验证频率具有预期值（不仅仅是比例）。
  - d) 验证分量重新求和后得到输入信号。
  - e) 实验不同步长 $h$ 值以及扩大测量周期 $T = N h$ 的单独影响。

- 2. 采样奇信号

  $$y(t) = \sin(\omega t) + 2\sin(3\omega t) + 3\sin(5\omega t).$$

  将其分解为分量；然后检查它们基本上是虚数且比例为 1 : 2 : 3（或若绘制功率谱则为 1 : 4 : 9），并且它们重新求和后得到输入信号。

- 3. 采样混合对称信号

  $$y(t) = 5\sin(\omega t) + 2\cos(3\omega t) + \sin(5\omega t).$$

  将其分解为分量；然后检查有三个分量比例为 5 : 2 : 1（或若绘制功率谱则为 25 : 4 : 1），并且它们重新求和后得到输入信号。

- 4. 采样信号

  $$y(t) = 5 + 10\sin(t + 2).$$

  比较并解释通过采样 (a) 不含 5 的情况，(b) 按给定但不含 2 的情况，以及 (c) 不含 5 且不含 2 的情况所得到的结果。

- 5. 在我们讨论混叠时，我们检查了图 12.2 中显示的函数 $\sin(\pi t/2)$ 和 $\sin(2\pi t)$。采样函数

  $$y(t) = \sin(\pi t/2) + \sin(2\pi t) \tag{12.50}$$

  并探索混叠如何发生。具体来说，我们知道真实变换在 $\omega = \pi/2$ 和 $\omega = 2\pi$ 处包含峰值。以导致混叠的采样率以及更高且无混叠的采样率采样信号。比较每种情况下得到的 DFT 并检查你的结论是否与奈奎斯特准则一致。

**高度非线性振子**

回顾弹簧幂 $p = 12$ 的振荡数值解（见 (12.1)）。将解分解为傅里叶级数并确定至少贡献 10% 的高次谐波数量；例如，确定 $|b_n/b_1| < 0.1$ 的 $n$。检查重新求和分量后是否能再现信号。

**非线性扰动振子**

记住具有非线性扰动的谐振子 (8.2)：

$$V(x) = \frac{1}{2} k x^2 \left(1 - \frac{2}{3} a x\right), \qquad F(x) = -k x (1 - a x). \tag{12.51}$$

对于非常小的振荡幅度（$x \ll 1/a$），解 $x(t)$ 本质上应仅为傅里叶级数的第一项。

- 1. 我们希望信号包含“大约 10% 的非线性”。在此情况下，固定你的 $a$ 值使得 $a x_{\max} \approx 10\%$，其中 $x_{\max}$ 是振荡的最大振幅。对于剩余问题，保持 $a$ 值固定。

- 2. 将你的数值解分解为离散傅里叶谱。

- 3. 绘制前两个 $\omega$（非直流）傅里叶分量重要性百分比随初始位移 $0 < x_0 < 1/2a$ 的变化图。你会发现高次谐波随着振幅增大而变得更重要。由于同时存在偶分量和奇分量，$Y_n$ 应为复数。由于 10% 的幅度效应变为 1% 的功率效应，请确保对功率谱做半对数图。

- 4. 像往常一样，检查你的变换的重新求和是否能再现信号。

> （警告：你在级数中使用的 $\omega$ 必须对应系统的真实频率，而不是小振荡的 $\omega_0$。）

### 12.5.4 Nonperiodic Function DFT (Exploration)

考虑一个简单的模型（波包）来描述在空间和时间中运动的“局域化”电子。初始在 $x = 5$ 附近局域化的电子的一个良好模型是高斯乘以平面波：

$$\psi(x, t=0) = \exp\left[-\frac{1}{2}\left(\frac{x - 5.0}{\sigma_0}\right)^2\right] e^{i k_0 x}. \tag{12.52}$$

该波包不是动量算符⁶ $p = -i\,d/dx$ 的本征态，事实上包含动量分布。你的问题是求傅里叶变换

$$\psi(p) = \frac{1}{\sqrt{2\pi}} \int_{-\infty}^{+\infty} dx\, e^{i p x} \psi(x), \tag{12.53}$$

以确定 (12.52) 中的动量分量。

## 12.6 Filtering Noisy Signals

你测量的信号 $y(t)$ 显然包含噪声。你的问题是确定如果信号不含噪声，其谱中会存在哪些频率。当然，一旦你得到去除了噪声的傅里叶变换，你就可以将其变换以得到无噪声的信号 $s(t)$。

> 在解决此问题的过程中，我们考察了两种简单方法：自相关函数的使用和滤波器的使用。这两种方法在科学中都有广泛应用，我们的讨论并未做到公正。我们将在第 13 章波分析的讨论中再次看到滤波器。

## 12.7 Noise Reduction via Autocorrelation (Theory)

我们假设测量的信号是真实信号 $s(t)$ 与一些不受欢迎的噪声 $n(t)$ 之和，我们希望确定它：

$$y(t) = s(t) + n(t). \tag{12.54}$$

我们去除噪声的第一种方法依赖于噪声是随机过程这一事实，因此不应与信号相关。但我们

6) 我们使用自然单位，其中 ℏ = 1。

