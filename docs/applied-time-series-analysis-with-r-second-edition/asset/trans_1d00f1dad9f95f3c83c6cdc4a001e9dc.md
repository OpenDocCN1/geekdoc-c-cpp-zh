

因此，GIF 是倒数，即

$$ \text{GIF} = \frac{1}{2\pi t^{-\lambda+1} + \frac12(1-\lambda)(2\pi)^2 t^{-2\lambda+1}+ \dots}
= \frac{t^{\lambda-1}}{2\pi}\Big[\frac{1}{1+\pi(1-\lambda)t^{-\lambda}+ \dots}\Big].$$

因此，对于大的 $t$，

$$\text{GIF} \simeq \frac{t^{\lambda-1}}{2\pi} = \frac{g'(t)}{2\pi} = \text{IF}.$$

Jiang等人(2006)表明，例13A.1的结果可以推广到任何解析的单调递增函数 $g(t)$。也就是说，如果 $H(t)=A\cos[g(t)]$，且 $g(t)$ 单调递增，则 $\delta=2\pi$，且 $\mathcal{P}(t; g, 2\pi)=g^{-1}(g(t)+2\pi)-t$。他们还表明，IF 是 GIF 的一阶泰勒级数近似。

## 13A.2 G(λ) 过程的瞬时谱

由于在许多信号中，整个频率结构随时间演化，因此需要 G(λ) 过程的瞬时谱的概念。为此，令 $f^* = 1/\delta$，并令 $G_X(f^*; \lambda)$ 表示 G(λ) 谱密度。例如，对于 G(p; λ) 模型，G(λ) 谱密度是与对偶拟合的 AR(p) 模型相关联的 AR(p) 谱密度。从定义13A.2和方程13A.2可以清楚地看出，$f^*$ 是 $f$（=GIF）和 $t$ 的函数。也就是说，由方程13A.2

$$f^* = 0, \quad \text{if } f = 0, \tag{13A.3}
= [\ln(1+1/(t f))]^{-1}, \quad \text{if } f \neq 0, \ \lambda = 0,
= \frac{\lambda}{(t+1/f)^{\lambda} - t^{\lambda}}, \quad \text{if } f \neq 0, \ \lambda \neq 0.$$

因此，我们可以通过方程13A.3中定义的 $f^*$ 来捕获瞬时频率。注意，由于 $G_X(f^*; \lambda)=G_X(-f^*; \lambda)$，我们总是取 $f^* \ge 0$ 和 $f \ge 0$。

### 定义13A.3

如果 $X(t)$ 是一个 G(λ) 过程，且 $G_X(f^*;\lambda)$ 是它的 G(λ) 谱，则 $X(t)$ 在时刻 $t$ 的瞬时谱（记作 $S(f,t;\lambda)$）定义为

$$S(f,t;\lambda)=G_X(f^*;\lambda). \tag{13A.4}$$

### 定理13A.1

如果 $X(t)$ 是一个 G(p,q;λ) 过程，则 $X(t)$ 在时刻 $t$ 的瞬时谱为

$$S(f,t;\lambda)=\sigma_a^2\frac{\prod_{j=1}^{q}|\beta_j-i2\pi f^*|^2}{\prod_{k=1}^{p}|\alpha_k-i2\pi f^*|^2}. \tag{13A.5}$$

其中 $f^*$ 由方程13A.3给出。

*证明：* 由方程13A.4直接得出。

## 13A.3 GLC(p) 过程的 GIF 与瞬时谱

对于 GLC(p) 过程，GIF 由下式给出：

$$f_t=\frac{2a}{(2at+b)\left(-1\pm\sqrt{\frac{1+8at}{(2at+b)^2}}\right)}. \tag{13A.6}$$

其中 + 和 - 分别与反射点右侧和左侧的频率相关。对应于方程13A.3和13A.4，可以得出瞬时谱 $S(f_t,t;a,b)$ 由 $S(f_t,t;a,b)=G(f^*;a,b)$ 给出，其中 $G(f^*;a,b)$ 是对偶的谱，且

$$f^*=\frac{f_t^2}{(2at+b)f_t+a}. \tag{13A.7}$$

参见Robertson等人(2010)和Jiang等人(2006)。

## 附录13B：R命令

有多个 tswge 函数可用于执行 TVF 数据的分析。这些函数尤其侧重于使用 G(λ; p) 模型来分析 TVF 数据。

- **a.** `gen.glambda.wge(n, lambda, phi, offset, vara, plot, sn)` 是一个函数，用于从给定的 G(λ; p) 模型生成长度为 n 的实现。

  `n` 是实现长度（xt，t = 1, ..., n），也就是说，它在等间隔点 1, ..., n 上求值。

  **注意：** 生成的模型基于零均值。如果 xt 是由 `gen.glambda.wge` 生成的时间序列，那么要将其转换为均值 μ = 10 的时间序列，只需计算 yt = xt + 10。

  - `lambda` 是模型中 λ 的值（默认是 lambda = 0，即 M 平稳模型）
  - `phi` 是一个 AR 参数向量（默认是 phi = 0）
  - `offset` 是偏移参数（例如，参见关于图13.2的讨论）（默认 = 60）
  - `vara` 是白噪声方差（默认 = 1）
  - `plot = TRUE`（默认）会生成所生成实现的图
  - `sn` 决定模拟中使用的种子。（见下面的注(5)。）

  **注意：**

  - 1. 该函数将 p 作为 phi 的长度。如果 phi = 0（默认），则 p 的值设为零。
  - 2. `gen.glambda.wge` 调用 tswge 函数 `gen.arma.wge`，而该函数又调用基础 R 函数 `arima.sim`。
  - 3. 如果你知道 AR 模型的因子而不是系数，调用实用函数 `mult.wge` 将很有用。
  - 4. 默认情况下，白噪声是零均值、方差 vara = 1 的正态噪声。
  - 5. sn = 0（默认）基于随机选择的种子产生结果。如果你希望在后续运行 `gen.glambda.wge` 时复现相同的实现，则在每次运行时将 sn 设置为相同的正整数。

  **示例：** 命令

  ```
  x = gen.glambda.wge(n = 500, lambda = 0.5, phi = c(1.9, -.99), offset = 25, vara = 1)
  ```

  生成并绘制来自用于生成图13.6b中实现的模型的一个实现。由于种子是随机选择的，这里生成的实现不会与图13.6b完全匹配，但会具有相同的频率递减的 TVF 特征。

- **b.** `est.glambda.wge(x, lambda.range, offset.range)` 估计（在指定范围内）产生“最平稳”对偶的 λ 和 offset。

  `x` 是一个等间隔 TVF 数据集

  `lambda.range` 是一个包含两个分量的向量，指定要考虑的 λ 的最小值和最大值。

  `offset.range` 是一个包含两个分量的向量，指定要考虑的 offset 的最小值和最大值。

  **示例：** 查找创建图13.4b中对偶数据集的 λ 和 offset 值的命令是

  ```
  data(fig13.2c)
  est.glambda.wge(fig13.2c, lambda.range = c(-.5, .5), offset.range = c(0, 100))
  ```

  **注意：** 返回的 lambda 和 offset 的顶部值是 lambda = -0.4 和 offset 63。参见例13.7。

- **c.** `trans.to.dual.wge(x, lambda, offset, plot)` 使用线性插值变换时间轴以创建对偶过程。

  `x` 是一个等间隔 TVF 数据集

  `lambda` 是 G(λ; p) 模型中 λ 的值（默认是 lambda = 0，即 x 是来自 M 平稳模型的实现）

  `offset` 是偏移参数（例如，参见关于图13.2的讨论）（默认 = 60）

  `plot = TRUE`（默认）会生成所创建的对偶实现的图

  该函数输出：

  `intX` 和 `intY`：输入实现 x 的长度为 n，x 的值在时间点 t = 1, ..., n 处可用。intY 值是原始时间尺度下、在 intX 的 n 个值处对原始时间序列进行插值得到的 n 个值。对偶数据集通过将这 n 个 intY 值分别与 t = 1, ..., n 关联而获得。

  `h` 是一个缩放参数的输出值，用于确保对偶实现和原始实现具有相同的长度。

  **注意：** `trans.to.dual` 基于 G(λ) 平稳建模。通过使用 λ = 0 获得 M 平稳模型。

  *示例：* 命令

  ```
  data(fig13.2c)
  y = trans.to.dual.wge(fig13.2c, lambda = -0.4, offset = 63)
  ```

  计算并在此情况下绘制图13.4b中所示的对偶数据，并使用 lambda 和 offset 指定的 G(λ) 时间变换将对偶数据保存在 y$intY 中，本例中的 lambda 和 offset 是在例13.7中获得的。

- **d.** `trans.to.original.wge(xd, lambda, offset, h, plot)` 将变换时间中的对偶数据集变换回原始时间尺度。

  lambda 和 offset 的值是先前在函数 `trans.to.dual.wge` 中用于变换时间轴的值，h 的值作为函数 `trans.to.dual.wge` 的输出获得。

  - `xd` 是在 `trans.to.dual` 中使用的 G(λ) 时间所指定的变换时间中的等间隔对偶数据集
  - `lambda` 是用于创建对偶的 G(λ) 变换中 lambda 的值
  - `offset` 是用于创建对偶的 G(λ) 变换中 offset 的值
  - `h` 是一个缩放参数（作为 `trans.to.dual` 的输出获得），旨在确保对偶实现和原始实现具有相同的长度
  - `plot = TRUE`（默认）会生成所创建的对偶实现的图

  该函数输出（并可选地绘制）`reintY`，这些是要相对于 t = 1, ..., n 绘制的 Y 值，用于近似原始 TVF 实现。

  *示例：* 在第13.5节讨论的用于在对偶空间中创建对偶、低通滤波对偶以及相关滤波数据的 G 滤波代码如下（使用真实值 lambda = 0 和 offset = 175）：

  ```
  data(fig13.18a)
  dual = trans.to.dual.wge(fig13.18a, lambda = 0, offset = 175)
  ```

