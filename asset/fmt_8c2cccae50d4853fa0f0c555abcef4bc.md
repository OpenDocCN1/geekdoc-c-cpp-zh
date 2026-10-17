
我们用符号 $C(\cdot)$ 或 $(\cdot)$ 表示物理量的复包络，用 $y^{(I)}$ 表示同相分，用 $y^{(Q)}$ 表示正交分，用 $\mathcal{H}\{\cdot\}$ 表示希尔伯特变换。信号的同相（I）和正交分通过图 12.2 所示的处理获得。`FFT` 通常用于近似有限数据块在图 12.2 中的处理，其中频率 $f$ 处 `FFT` 系数的实部和虚部分别正比于 I 和 Q 分。(12.1) 中正弦波的复包络由 (12.3) 给出，它不是时间变化的，因此平均功率为 $|\tilde{s}_{ref}(t)|^2 = S_{ref}$。

很容易看出，时间上的正弦信号 $s_{ref}(t)$ 会导致相应复包络产生相移，即 $C(s_{ref}(t-\tau_s)) = \exp(-j2\pi f_a\tau_s)\tilde{s}_{ref}(t)$。对于频率谱限制在中心频率 $f$ Hz 附近带宽 $B$ 带内的窄带信号，具有类似的性质：

## 249 气声学传感器网络的信号处理与传播

![](img/11e8580124e6543d23c6c1d715727b6a_273_0.png)

图 12.1 传感器与源位置的几何结构。

方程 12.4 是著名的傅里叶变换关系，时间平移和相位移动与频率线性正比。当频带足够窄，使得增加的相移在频带内接近 $\exp(-j2\pi f\tau_v)$ 时，该近似是可以接受的。对于具有复包络 $\tilde{z}(t)$ 的窄带信号 $z(t)$，时间平移可以通过相应复包络的相移来良好近似：

$$\tilde{z}(t - \tau_v) = \exp(-j2\pi f\tau_v)\tilde{z}(t) \quad (\text{窄带近似}).$$

源和阵列的几何结构如图 12.1 所示。源位于 $(x, y)$ 平面上的坐标 $(x_s, y_s)$。阵列包含 $N$ 个传感器，传感器 $n$ 位于 $(x_o + \Delta x_n, y_o + \Delta y_n)$，其中 $(x_o, y_o)$ 是阵列中心，$(\Delta x_n, \Delta y_n)$ 是相对距离。从源到阵列中心的传播时间为：

$$\tau_o = \frac{d_o}{c}\sqrt{(x_s-x_o)^2 + (y_s-y_o)^2} \quad (12.5)$$

（此处 $d_o$ 对应源到中心的距离）。源到传感器 $n$ 的传播时间为

$$\tau_n = \frac{d_o}{c}\sqrt{(x_n-x_o)^2 + (y_n-y_o)^2} \quad (12.6)$$

其中 $d_o$ 是源到阵列中心的距离。让我们定义阵列直径 $D = \max\sqrt{(x_n-x_o)^2 + (y_n-y_o)^2}$，其中 $\rho_{mn}$ 是传感器 $m$ 和 $n$ 之间的距离，如图 12.1 所示。在远场中，球面波被近似为平面波，因此 $\phi$ 包含了源位置的信息。对于阵列直径 $D < \lambda$ 且频率 $f_c > 200$ Hz，远场模型是有效的：

$$\tau_v = \frac{\rho_{mn}}{c} \quad (12.7)$$

其中 $\phi$ 是方位角。

## 12.2 无散射窄带模型

此处给出一个在没有散射时入射阵列的信号模型。使用远场近似，我们观测传感器处的测量值为

$$z_n(t) = s_n(t - \tau_o - \tau_v) + w_n(t), \quad n=1, \dots, N \quad (12.8)$$

在没有散射的情况下，信号分量为纯正弦波：

$$s_n(t) = \sqrt{S}\cos(2\pi f_s t + \chi). \quad (12.9)$$

$w_n(t)$ 是加性高斯噪声 (`AWGN`) 过程，实值、连续、零均值、联合宽稳且不同传感器间不相关的，其功率谱密度 (`PSD`) 为 $N_0/2$ W/Hz。此时，其相关性性质为：

$$E[w_n(t)] = 0, \quad -\infty < t < \infty, \quad n=1, \dots, N \quad (12.10)$$

$$r_{w,mn}(\xi) = E[w_n(t+\xi)w^*_m(t)] = r_w(\xi)\delta_{mn}, \quad (12.11)$$

其中 $\delta(\cdot)$ 是狄拉克函数，$\delta_{mn}$ 是克罗内克符号（当 $m=n$ 时为 1，否则为 0）。如所述，如果环境中存在风噪声或干扰源，将噪声建模为空间白是不准确的。噪声 `PSD` 为

$$G_w(f) = \mathcal{F}[r_w(\xi)] = \frac{N_0}{2}, \quad (12.12)$$

其中 $\mathcal{F}\{\cdot\}$ 表示傅里叶变换。在没有散射的情况下，(12.8) 和 (12.9) 中 $z_n(t)$ 的复包络由 (12.4) 给出：

$$\tilde{z}_n(t) = \exp[-j(\omega_s\tau_s + \omega_o\tau_{o,n})]s_n(t) + \tilde{w}_n(t) \n = \sqrt{S} \exp[j(\omega_c - \omega_s\tau_s)]\exp[-j\omega_o\tau_{o,n}] + \tilde{w}_n(t), \quad (12.13)$$

其中窄带源分量的复包络为：

$$\tilde{s}_n(t) = \sqrt{S}e^{j\chi_n}, \quad n=1, \dots, N\text{ (无散射)}. \quad (12.14)$$

# 声气学传感器网络的信号处理与传播

![](img/11e8580124e6543d23c6c1d715727b6a_275_0.png)

**图 12.2** 获取同相和正交分量 $z^{(1)}(t)$ 和 $z^{(2)}(t)$ 的处理。

我们假设复包络经过了带宽为 $[-B/2, B]$ Hz 的低通滤波，如图 12.2 所示。假设低通滤波器是理想的，$\tilde{w}_n(t)$ 具有功率谱密度（`PSD`）和相关性

$G_u(f) = (2N_{o}B)\text{rect}\left(\frac{f}{B}\right)$

$r_n(\xi) = E[\tilde{w}_n(t+\xi)\tilde{w}_n^*(t)] = \mathcal{F}^{-1}\{G_u(f)\} = (2N_{o}B)\text{sinc}(B\xi)$,

$r_{mn}(\xi) = E[\tilde{w}_m(t+\xi)\tilde{w}_n^*(t)] = r_n(\xi)\delta_{mn}$,

其中

$(*)$ 表示复共轭
$\text{rect}(u) = 1$（对于 $-1/2 < u < 1/2$），否则为 0
$\text{sinc}(u) = \sin(\pi u)/(\pi u)$

注意，在间隔为 $1/B$ s 的采样时刻，噪声样本之间是不相关的（由于是高斯分布，因此是独立的）。特别是噪声 `PSD` $G_u(f)$ 既不是平坦的也不是带限的，因为带宽 $B$ Hz 的低通滤波意味着当时间间隔大于 $1/B$ s 时，噪声样本的相关性会降低。

让我们定义向量：

$\tilde{\mathbf{z}}(t) = \begin{bmatrix} \tilde{z}_1(t) \\ \vdots \\ \tilde{z}_N(t) \end{bmatrix}, \quad \tilde{\mathbf{s}}(t) = \begin{bmatrix} \tilde{s}_1(t) \\ \vdots \\ \tilde{s}_N(t) \end{bmatrix}, \quad \hat{\mathbf{w}}(t) = \begin{bmatrix} \hat{w}_1(t) \\ \vdots \\ \hat{w}_N(t) \end{bmatrix}$

然后结合 (12.13) 和 (12.27)，

$\tilde{\mathbf{z}}(t) = \sqrt{S}\exp[j(\boldsymbol{\chi}-\boldsymbol{\omega}_n\tau_n)]\mathbf{a} + \hat{\mathbf{w}}(t) = \sqrt{S}e^{j\mathbf{a}} + \hat{\mathbf{w}}(t)$,

图像与传感器信号处理

其中 $a$ 是阵列波矢量（或阵列流形）

$$\exp[jk((\cos\phi)\Delta x_1 + (\sin\phi)\Delta y_1)]$$
$$\exp[jk((\cos\phi)\Delta x_n + (\sin\phi)\Delta y_n)] \quad (12.20)$$

其中 $k = \omega_d/c$。注意，波矢量 $a$ 依赖于频率 $\omega_o$、传感器位置 $(\Delta x_n, \Delta y_n)$ 以及源方位 $\phi$。所有传感器的公共相位因子 $\exp[j(\gamma - \omega\tau_n)] = \exp[j(\chi - kd_n)]$ 取决于源发射信号的相位 $(\chi)$ 以及到阵列中心的传播距离 $(kd_o)$。我们简化了符号并定义：

$$\theta \triangleq \chi - kd_o \quad (12.21)$$

这是一个确定性参数。

为了准备在模型中引入散射，让我们写出向量 $\mathbf{s}(t)$ 和 $\mathbf{z}(t)$ 的一阶和二阶矩。令 $1$ 为 $N\times1$ 的全1向量，$R_z(\tau) = E[z(t+\tau)z^*(t)]$ 为 $N\times N$ 互相关函数矩阵，其 $(m,n)$ 元为 $R_{m,n}(\tau) = E[z_m(t+\tau)z_n^*(t)]$，$G_z(f) = \mathcal{F}\{R_z(\tau)\}$ 为互谱密度（`CSD`）矩阵，

$$E[\mathbf{s}(t)] = \sqrt{S}\mathbf{1} \quad E[\mathbf{z}(t)] = \sqrt{S}\mathbf{a} \quad (12.22)$$

$$R_z(\tau) = \mathbf{S}\mathbf{1}^T \quad G_z(f) = \mathbf{S}\mathbf{a}^* + R_z(f) \quad (12.23)$$

$$G_s(f) = \mathbf{S}\mathbf{1}^T\delta(f) \quad G_z(f) = \mathbf{S}\mathbf{a}^*\delta(f) + G_n(f)\mathbf{I} \quad (12.24)$$

$$E[\mathbf{s}(t)\mathbf{s}^*(t)] = R_s(0) = \mathbf{S}\mathbf{1}^T \quad E[\mathbf{z}(t)\mathbf{z}^*(t)] = R_z(0) = \mathbf{S}\mathbf{a}^* + \sigma_z^2\mathbf{I} \quad (12.25)$$

其中

- $T$ 表示转置
- $^*$ 表示复共轭
- $H$ 表示复共轭转置
- $\mathbf{I}$ 是 $N\times N$ 单位矩阵
- $\sigma_n^2$ 是噪声样本的方差

$$\sigma_n^2 = E\{|\mathbf{w}(t)|^2\} = r_n(0) = 2N_oB \quad (12.26)$$

从 (12.24)看出，每个传感器的 `PSD` 包含一条谱线，因为源是正弦波。从 (12.25)看出，在每个传感器处，信号的平均功率为 $S$，因此每个传感器的 `SNR`

$$\text{SNR} = \frac{S}{\sigma_n^2} = \frac{S}{2N_ob} \quad (12.27)$$

复包络向量 $\mathbf{z}(t)$ 通常以 $f_s = B$ /秒的速率进行采样，因此采样间隔为 $1/B$ s：

$$\mathbf{z}(i_s) = \sqrt{S}\mathbf{a} + \mathbf{w}(i_s), \quad i=0,...,T-1 \quad (12.28)$$

散射通过将阵列信号的复包络从（确定性）均值分部分功率扩散到功率谱密度（`PSD`）中心位于 0 Hz 的零均值随机过程中。我们假设散射信号的带宽记为 $B$ 远小于频率 $f_s$。饱和参数 [25,26] 记为 $\Omega \in [0,1]$，定义了从均值散射到随机分量的平均信号功率的比例。散射可能是弱的（$\Omega=0$）或强烈的（$\Omega=1$），这类似于无线电传播文献中的 `Rician` 衰落和 `Rayleigh` 衰落。包含散射的公式 (12.8)、(12.9)、(12.13) 和 (12.14) 的修改如下，其中 $\tilde{s}_n(t)$ 是在传感器 $n$ 处测量的信号：

$$$\tilde{s}_n(t) = \exp[-j(\omega_s\tau_n + \omega\tau_{o,n})]s_n(t) + w_n(t), \quad (12.31)$$$

$$$\tilde{s}_n(t) = \sqrt{(1-\Omega)Se^{i\omega t} + \tilde{v}_n(t)^2}e^{i\omega t}, n=1,\dots,N \text{（包含散射）。} \quad (12.32)$$$

为了满足能量守恒 $E|\tilde{s}(t)|^2=S$，散射分量的平均功率必须为 $E|\tilde{v}(t)|^2=\Omega$。饱和度 $\Omega$ 的值以及散射过程 $\tilde{v}(t)$ 的相关性性质取决于源距离 ($d_s$) 和气象条件。散射过程向量 $\tilde{v}(t)$ 和加性噪声向量 $\tilde{w}(t)$ 包含零均值、联合宽平稳的复圆对称高斯随机过程。散射过程和噪声是独立的，$E[\tilde{v}(t)^H\tilde{w}(t')]=0$。噪声由 (12.15) 到 (12.17) 描述，而饱和度 $\Omega$ 和 $\tilde{v}(t)$ 的统计特性由一阶和二阶矩的“消减系数”决定。正如我们在 12.2.4 节将讨论的，消减系数的近似分析模型可以从大气湍流的物理建模中。在本节的剩余部分，我们定义消减系数并将其与 $\Omega$ 以及 $\tilde{v}(t)$ 的统计联系起来，为包含大气散射的传感器阵列提供模型。

我们将 $\tilde{s}(t)$的一阶和二阶矩的消减系数分别表示 $\mu$ 和 $\nu_{\rho_{mn}}$，其中 $\rho_{mn}$ 是传感器 $m$ 和 $n$ 之间的距离（见图 12.1）。消减系数隐式定义如下：

$$$E\tilde{s}(t) = \sqrt{(1-\Omega)Se^{i\omega t}} \sqrt{S}e^{i\omega t}e^{-\mu d_{s}}, \quad (12.33)$$$

$$$r_{mn}(0) = E\tilde{s}_m(t)\tilde{s}_n(t)^* = (1-\Omega)S + r_{mn}(0)S e^{-\nu_{\rho_{mn}} d_{s}}, \quad (12.34)$$$

(12.33) 和 (12.34) 的右侧是来自 (12.22) 和 (12.23) 的**没有**散射的一阶和二阶矩，乘以一个随源距离 $d_s$ 增加而指数级衰减的因子。从 (12.3)，我们得到：

$$$\sqrt{(1-\Omega)} = e^{-\mu d_s} \quad \text{且 } \Omega=1-e^{-2\mu d_s}, \quad (12.36)$$$

# 气声传感器网络的信号处理与传播

同样，根据 (12.34) 中 $m=n$ 的能量守恒，$\hat{s}_i(t)$ 中未散射部分和散射部分的平均功率之和必须等于 $S$，所以：

$$$$r_n(0) = E{\hat{s}_n(t)\} = e^{-2\mu d_s}S + r_n(0) = S,$$ \quad (12.37)$$$

$$$\Rightarrow r_n(0) = E{\hat{v}_n(t)\} = \int G_n(f)df = (1-e^{-2\mu d_s})S = \Omega,$$ \quad (12.38)$$$

其中：
- $r_i(\xi) = E{\hat{v}_i(t)\hat{v}_i(t+\xi)^*}$ 是自相关函数（对所有 $n$ 均相同）
- $G_i(f)$ 是相应的 `PSD`

对于源距离 $d_i \ll 1/(2\mu)$，散射 $\Omega=0$，源的大部分能量到达 $\hat{s}_i(t)$ 的传感器（确定性均值）分量。对于源距离 $d_i \gg 1/(2\mu)$，散射 $\Omega=1$，大部分能量到达散射（随机）分量。接下来，我们使用 (12.34) 将 $m$ 和 $n$ 处散射信号的相关性 $r_{mn}(\xi)$ 与二阶矩系数 $\rho_{mn}$ 联系起来。由于 $\hat{v}_i(t)$ 在每个传感器处的自相关相同且等于 $r_i(\xi)$，并假设 `PSD` $G_i(f)$ 占据以 0Hz 为中心的窄带宽，则互相关和互谱满足：

$$$r_{mn}(\xi) = r_{nm}^*(\xi) \quad G_{mn}(f) = \mathcal{F}\{\rho_{mn}(\xi)\} = \gamma_{mn}G_n(f),$ \quad (12.39)$$$

其中 $\gamma_{mn} \le 1$ 是 $\hat{v}_m(t)$ 和 $\hat{v}_n(t)$ 之间的相干。将 $\gamma_{mn}$ 定义为常数包含了相干性随频率变化的假设，这在 $G_i(f)$ 带宽很大是合理的。虽然尚未对窄带信号的相干时间进行统计研究，但数据和理论考虑（如文献）与几十秒到几分钟的值一致。$G_i(f)$ 的带宽可能小于 1 Hz。低通滤波器的带宽 $B$ 应该等于 $G_i(f)$ 的带宽。我们假设 (12.39) 中的 $\gamma_{mn}$ 是实值且非负的，这意味着传感器对的波动不是偏正或偏负的。然后利用 (12.39)、(12.38) 和 (12.34) 得 $\gamma_{mn}$ 与 $\mu$ 的关系：

$$$$\gamma_{mn} = \frac{e^{-2\mu d_n}e^{-2\mu d_m}}{1-e^{-2\mu d_s}}, \quad m,n=N. \quad (12.40)$$$

我们定义 $\Gamma$ 为元素为 $\gamma_{mn}$ 的 $N \times N$ 矩阵。二阶矩系数 $\rho_{mn}$ 是单调递增函数，$v(0)=0$ 且 $v(\mu) \in [0,1]$。结合 (12.31) 和 (12.32) 得到：

$$\$$\mathbf{z}(t) = \sqrt{S}e^{-i\mu d_s}\mathbf{a} + e^{-i\mu d_s}\mathbf{a}^T\mathbf{v}(t),$ \quad (12.41)$$$

其中：
$\theta$ 定义在 (12.21) 中
$\mathbf{a}$ 是 (12.20) 中的阵列导矢量

我们定义矩阵 $B$ 的元素为：

$$$B_{mn} = \exp[-\rho_{mn}]d_s], \quad (12.42)$$$

然后我们将二阶矩 (12.22) 到 (12.25) 扩展到散射情况：

$$\$$E(\tilde{z}(t)) = e^{-\mu d_s}\sqrt{S}e^{\theta}\mathbf{a} \triangleq \mathbf{m}_z,$$ \quad (12.43)$$$

$$$$R_z(\xi_i) = e^{-2\mu d_s}\mathbf{B}\mathbf{aa}^* - e^{-2\mu d_s}\mathbf{aa}^* + \frac{r_z(\xi_i)}{S(1-e^{-2\mu d_s})} + r_w(\xi_i)I,$ \quad (12.44)$$$

$$$$G_z(f) = e^{-2\mu d_s}\mathbf{S}\delta(f) + \mathbf{S}\mathbf{B}\mathbf{aa}^* - e^{-2\mu d_s}\mathbf{aa}^* - \frac{G_o(f)}{S(1-e^{-2\mu d_s})} + G_w(f)I,$ \quad (12.45)$$$

$$$$E(\tilde{z}(t)\tilde{z}^*(t)) = R_z(0) = \mathbf{S}\mathbf{B}\mathbf{aa}^* + \sigma_{I_z}^2\mathbf{C}_z + \mathbf{m}_z\mathbf{m}_z^*,$$ \quad (12.46)$$$

其中 $\circ$ 表示逐元素乘积。用于 (12.44) 中自相关 $r_z(0)$ 和 `PSD` $G_z(f)$ 的归一化量 $S(1-e^{-2\mu d_s})$ 等于 $r_z(0) = \int G_o(f)df$。归一化自相关的最大值为 1，归一化 `PSD` 下的面积为 1。复包络样本 $\tilde{z}(t)$ 服从复正态分布 `CN`($\mathbf{m}_z, \mathbf{C}_z$)，其定义在 (12.30)。均值和协方差矩阵在 (12.43) 和 (12.46)给出，但重复它们是为了与 (12.29) 进行比较：

$$\$$\mathbf{m}_z = e^{-\mu d_s}\sqrt{S}e^{\theta}\mathbf{a} \quad \text{（包含散射），} \quad (12.47)$$$

$$\$$\mathbf{C}_z = \mathbf{S}\mathbf{B}\mathbf{aa}^* - e^{-2\mu d_s}\mathbf{aa}^* + \sigma_{I_z}^2\mathbf{I} \quad \text{（包含散射），} \quad (12.48)$$$

注意当 $d_o \ll 1/\mu$ 时散射是显著的，此时 $e^{-2\mu d_s} \approx 1$ 且 $\Omega=0$。此时信号能量在均值中，$B=\mathbf{1}$ 且 (12.44) 中 $B_{mn}=1$，因为 $v(\rho_{mn}) < 2\mu d_s$。对于源距离 $d_o$ 较大，更多的能量被散射，$B$ 可能会偏离 $\mathbf{1}$（当 $m \neq n$ 时 $\gamma_{mn} < 1$），这是由于传感器之间的相干损失。在饱和状态（$\Omega=1, B=\Gamma$），导矢量中的散射模型为：

$$\$$\tilde{z}(t) = \sqrt{S}e^{\theta}\mathbf{a} \left[ e^{-\mu d_s} \left(1 + \frac{\tilde{v}(t)}{\sqrt{S}}\right) \right] + \tilde{w}(t) = \sqrt{S}e^{\theta}(\mathbf{a} \circ \mathbf{u}(t)) + \tilde{w}(t). \quad (12.49)$$$

# 气声学传感器网络的信号处理与传播

背景部分，参考参考文献 [5,10,27,30]。在这里，我们考虑与湍流效应对气声学阵列相关的特定结果。

散射阵列的性能取决于许多因素，包括声波长、从源到传感器阵列的传播距离、传感器之间的间距、湍流强度（由温度和速度波动的方差表征），$\nu(\rho)$ 正比于 $k'/p$，其中 $k = \omega/c_0$ 是声波波数，$c_0$ 是环境声速 [27]。在这种情况下，传感器之间相性的损失完全源于湍流引起的到达角（`AOA`）变动。在声学中，更具实际意义的是 $\rho \gg l$ 的情况。间距 $\rho$ 可能小于或大于涡的尺寸 $l$。

当 $\rho \gg l$ 且 $\rho \ll l$ 时，间距位于湍流的惯性子区 [5]。由于湍流强度随涡尺寸增大而增加，这与 $\rho \ll l$ 具有定性相似性。入射阵列的波前在孔径上具有大致恒定的 `AOA`，源的表观方位围绕实际方位变化。增加传感器之间的间距可以显著降低相干性。相反，当 $\rho \gg l$ 很大时，被湍流畸变的波前在传感器处产生几乎不相关的信号变化。在这种情况下，进一步增加间距不会影响相干性：它“饱和”在一个由湍流强度决定的值上，因此具有与加性无关噪声类似的效果。这两种极端情况如图 12.3 所示。产生的 $\nu(\rho)$ 行为和

![](img/11e8580124e6543d23c6c1d715727b6a_281_0.png)

图 12.3 湍流引起入射阵列的声波前畸变。波前最初是平滑的（左），并逐渐畸变，直到到达阵列（右）。(a) 湍流惯性子区内的传感器间距（$\rho \gg l$ 和 $\rho \ll l$）。波前相当平滑，但 `AOA`（以及表观源方位）在变化。(b) 远大于最大湍流涡尺度的传感器间距（$\rho \gg l$）。波前看起来非常粗糙，散射效应类似于不相关噪声。

![](img/11e8580124e6543d23c6c1d715727b6a_282_0.png)

**图 12.4** (a) 二阶消光系数 $\nu(\rho)$ 的特性行为。它最初随传感器间距 $\rho$ 的增大而增加，当 $\rho$ 相对于最大湍流涡尺寸很大时，饱和于固定值 $2l$（其中 $l$ 是一阶消光系数）。(b) 几个传播距离 $d$ 值下的总信号相干性相关行为。

球面传播波消光系数的一般结果，通过抛物线（窄角）近似和马尔可夫近似导出，并假设 $\rho \gg l$，见参考文献 [10] 的方程 7.60 和 7.71；参考文献 [30] 的方程 20 至 28

$$ $$\mu = \frac{\pi^2 k^{*2}}{2} \int dK_{\parallel} \Phi_{eff}(K_{\parallel}=0, K_{\perp}) = \frac{k^2 \sigma_{eff}^2}{4}$$

$$ $$\nu(\rho) = \pi^2 k^{*2} \int_{0}^{\infty} dK_{\parallel} [1 - J_0(K_{\parallel}\rho)] \Phi_{eff}(K_{\parallel}=0, K_{\perp})$$

其中 $J_0$ 是零阶第一类贝塞尔函数，$K = K_{\parallel} + K_{\perp}$ 是分解为平行和垂直于传播路径的湍流矢量。物理量 $\Phi_{eff}(K)$、$\sigma_{eff}$ 和 $L_{eff}$ 分别为有效湍流谱、方和积分尺度。（积分尺度是最大涡尺寸的定量度量）。谱定义为：

$$ $$\Phi_{eff}(K) = \frac{\Phi_T(K)}{T_0^2} + \frac{4\Phi_v(K)}{c_0^2}$$

其中：

$T_0$ 是环境温度
下标 $T$ 和 $v$ 表示温度和风速场。有效方差的定义相同，将 $\Phi(K)$ 替换为 $\sigma^2$。积分尺度定义为：

$$ $$L_{eff} = \frac{1}{\sigma_{eff}} \sqrt{\frac{\Phi_T(K)}{T_0^2} + \frac{4\Phi_v(K)}{c_0^2}}$$

## 气声学网络的信号处理与传播

对于 $\rho/l \gg 1$ 的情况，贝塞尔函数的贡献很小且 $\nu(\rho) \rightarrow 0$。当 $\rho/l \ll 1$ 时，$\mu$ 的属性见参考文献 [10]：

$$ $$\mu = 0.137 \left(\frac{C_T}{T_0} + \frac{22}{3}\frac{C_v}{c_0}\right)$$$

其中 $C_T$ 和 $C_v$ 分别是温度和风速场。注意有效长度很大程度上取决于大气条件。表 12.1 提供了各种条件下的估计值。

# 大气多云晴朗，光照，微风，$f=50\text{ Hz}$，$d_s = 1500\text{ m}$

![](img/11e8580124e6543d23c6c1d715727b6a_284_0.png)

**图 12.5** 间距为 $\rho$ 的传感器处散射信号的相干性评估，使用了 $f=50\text{ Hz}$、$d_s=1500\text{ m}$、多云晴朗、微风条件（表 12.1）。$v(\rho)$ 通过公式 (12.54) 计算，相干性 $\gamma(\rho)$ 通过公式 (12.40) 计算。

在小阵列中。然而，宽间距网络节点之间的相干性将很小，特别是在 200 Hz 左右的频率上。

图 12.5 展示了散射信号相干性 $\gamma_{max}$（见 12.40）随传感器间距 $\rho$ 的变化情况。(12.54) 中的消光系数是根据表 12.1 中的 $f=50$ 和源距离 $d_s=1500\text{ m}$、多云晴朗、微风条件计算，因此 $\Omega=0.95$。对于传感器间距 $\rho < 1$，相干性接近完美，然后随着间距增大，相干性迅速下降。

## 12.2.5 多频率与多源

(12.49) 中的模型适用于发射单频 $\omega=2\pi f_r$ rad/s 的单源。(12.2) 和图 12.2 中的复包络处理是源频率函数。我们可以将 (12.49) 中的模型扩展到 $K$ 个以频率 $\omega_1, \dots, \omega_K$ 发射的源的情况，如下：

$$\tilde{z}(i_T; \omega_i) = \sum_{k=1}^K \sqrt{S_k(\omega_k)} e^{j\omega_k} (\mathbf{a}_k(\omega_i) \circ \mathbf{\hat{u}}_k(i_T; \omega_i)) + \mathbf{\hat{w}}(i_T; \omega_i), \quad i=1, \dots, T \\n i=1, \dots, L \quad (12.55)$$

$$= ((\mathbf{a}_1(\omega_i) \cdot \dots \cdot \mathbf{a}_k(\omega_i)) \circ [\mathbf{\hat{u}}_1(i_T; \omega_i) \dots \cdot \mathbf{\hat{u}}_k(i_T; \omega_i)])] + \begin{matrix} \sqrt{S_k(\omega_k)} e^{j\omega_k} \end{matrix} + \mathbf{\hat{w}}(i_T; \omega_i); \\n (A(\omega_i) \circ \mathbf{\hat{u}}(i_T; \omega_i))\mathbf{p}(\omega_i) + \mathbf{\hat{w}}(\omega_i). \quad (12.56)$$

在 (12.55) 中，$S_k(\omega_k)$ 是频率为 $\omega_k$ 时源的平均功率，$\mathbf{\hat{u}}_k(i_T; \omega_i)$ 是如 (12.20) 所示频率 $\omega_i$ 下源 $k$ 的导向向量，$\mathbf{\hat{w}}(i_T; \omega_i)$ 是源 $k$ 在时间 $i$ 处的散射，$T$ 是样本数。在 (12.56) 中，导向矩阵 $A(\omega)$、导向矩阵 $\mathbf{\hat{u}}(i_T; \omega_i)$ 以及 $\mathbf{p}(\omega_i)$ 和 $\mathbf{\hat{w}}(\omega_i)$。（注：此处原文公式存在多处符号重复或表述混乱，已保持原文结构）。

在小阵列中。然而， 随着模型变得更完善，跨频率相干性已在理论和实验上进行了研究。在小阵列中。然而，宽间距网络节点之间的相干性将很小，特别是在 200 Hz 左右的频率上。

> 这种，对于完全饱和且没有相干性的情况，我们可以假设不同源的散射信号是独立的

## 12.3 信号处理

在本节中，我们讨论了声学网络的信号处理。信号处理考虑了前一节中的源和传播模型，以及通过无线链路连接的通信带宽。我们从 12.3.1 节的单传感器阵列 `AOA`估计开始。在 12.3.2 节讨论了多阵列的源定位，并并在 12.3.3 和 12.3.4 节简要介绍了跟踪、检测和分类算法。

### 12.3.1 角度估计

我们在 12.3.1.1 节讨论了带有散射的窄带 `AOA` 估计，然后在 12.3.1.2 节讨论了带有散射的窄带 `AOA` 估计。

# 气动传感器网络的信号处理与传播

Wang 和 Kaveh [45] 首先开发了一种基于以下变换协方矩阵相加复合形式的通用方法：

```
