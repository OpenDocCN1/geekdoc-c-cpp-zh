
$$\int_{-\infty}^{\infty} \psi_{\ell,m}(t)\psi_{j,k}(t)\,dt = \begin{cases} 0, & j \neq \ell \text{ or } m \neq k \\ \|\psi\|^2, & j = \ell,\ m = k \end{cases}$$

因此，

$$d_{j,k} = \frac{1}{\|\psi\|^2}\int_{-\infty}^{\infty} g(t)\psi_{j,k}(t)\,dt.$$

## 附录 12B：数学预备知识

本章中使用的许多 R 函数可在基于小波的 CRAN 包中找到。然而，使用了三个 tswge 函数：`wv.wge`、`plotts.dwt.wge` 和 `plotts.mra.dwt`。下面将对其进行讨论，随后简要讨论其他包。

- a. `wv.wge(x)` 计算并绘制向量 `x` 中数据的 Wigner–Ville 时频表示。
  - `x` 是包含待分析实现的向量。
  - *示例：* tswge 数据集 `chirp`（如图 12.2a 所示）如图 12.4b 所示的 Wigner–Ville 图是通过以下命令得到的：

    ```
    data(chirp)
    wv.wge(chirp)
    ```

以下两个命令需与 CRAN 包 `waveslim` 中的 `dwt` 和 `mra` 函数一起使用。

- b. `plotts.dwt.wge(x, n.levels, type)`
  - 该函数计算 dwt，输出小波系数，以图 12.7 的格式绘制 DWT，并可选择绘制标度图（时-尺度图）。
  - `x` 是待分析的实现（`x` 必须是长度为 $2^{J_0}$ 的向量，其中 $J_0$ 为介于 2 和 14 之间的某个正整数）。
  - `n.levels`（默认值 = 4）是层数（$n.levels \le J_0$）。
  - `type` 指定所用小波的类型（默认值 = s8），即 Symlet(8) 小波。
  - 其他选择为 Daublet 小波 D4（鲨鱼鳍）、D6 和 D8 以及 Haar 小波（`haar`）。

  程序输出：

  - `d1` 至 `d(n.levels)`，即 `n.levels` 组小波系数。
  - `s(n.levels)`，即与 `n.levels` 相关的尺度系数，以及关于小波类型的信息（例如 `haar`、D4 等），以及属性 `boundary` 和 `class`，其默认值分别为 `dwt` 和 `periodic`。有关这些属性的更多信息，请参阅 `waveslim` 文档。

  **注释：** `plotts.dwt.wge` 基于 `waveslim` 函数 `dwt` 绘制 DWT（有关更多详细信息，请参阅 `waveslim` 文档）。

  **示例：** 要获得 `bumps256` 数据集如图 12.13a 所示的 DWT，请使用以下命令：

  ```
  data(bumps256)
  plotts.dwt.wge(bumps256, n.levels = 5, type = 'D6')
  ```

- c. `plotts.mra.wge(x, n.levels, type)`
  - `x` 是待分析的实现（`x` 必须是长度为 $2^{J_0}$ 的向量，其中 $J_0$ 为介于 2 和 14 之间的某个正整数）。
  - `n.levels`（默认值 = 4）是层数（$n.levels \le J_0$）。
  - `type` 指定所用小波的类型（默认值 = S8），即 Symlet(8) 小波。其他选择为 Daublet 小波 D4（鲨鱼鳍）、D6 和 D8 以及 Haar 小波（`haar`）。

  程序输出：

  - `S0` 至 `S(n.levels)`，即图 12.9b 所示的逼近，每一个的点数与 `x` 相同。

  **注释：** `plotts.mra.wge` 基于 `waveslim` 函数 `mra` 绘制 MRA（有关更多详细信息，请参阅 `waveslim` 文档）。

  **示例：** 要获得 `bumps256` 数据集如图 12.9b 所示的 MRA，请使用以下命令：

  ```
  data(bumps256)
  plotts.mra.wge(bumps256, n.levels = 4, type = 'S8')
  ```

  为了获得图 12.10a 和 b 中的 MRA 图，请将上面的第二个命令替换为

  ```
  plotts.mra.wge(bumps256, n.levels = 4, type = 'haar')
  ```

  和

  ```
  plotts.mra.wge(bumps256, n.levels = 4, type = 'D4')
  ```

  分别。

### 其他包

以下是其他可能有用的小波包的简要列表，其中一些已在本章中使用。

- 1. **waveslim：** 除上述提到的 `waveslim` 中 `dwt` 和 `mra` 函数的应用外，`waveslim` 包在本章中还用于以下内容：
  - a. *平滑：* 图 12.11 左面板顶部噪声 bumps 信号（代码中称为 `nbump256`）的平滑是通过使用 `waveslim` 函数 `dwt`、`universal.thresh` 和 `idwt` 完成的，如下所示：

    ```
    data(nbump256)
    nbumps256.dwt <- dwt(nbump256)
    snbumps256.dwt <- universal.thresh(nbumps256.dwt)
    snbumps256 <- idwt(snbumps256.dwt)
    ```

  - b. *二维小波：* 用于绘制图 12.3 中 `barbara` 图像及其相关 DWT 的基于 `waveslim` 的代码如下所示：

    ```
    par(mfrow = c(2,2), mar = c(.3,2.5,.5,1))
    data(barbara)
    bbarbara <- barbara[256:1,256:1]
    gcol <- c(0,.1,.2,.3,.4,.5,.6,.7,.8,.9,1)
    image(1:dim(bbarbara)[1], 1:dim(bbarbara)[2], bbarbara, col = gray(gcol))
    bbarbara.dwt <- dwt.2d(bbarbara, 'haar', 3)
    plot.dwt.2d(bbarbara.dwt)
    ```

- 2. **Rwave：** 图 12.4a 中线性 chirp 数据（tswge 文件 `chirp`）的 Gabor 谱可使用 Rwave 命令获得

  ```
  cgt(input = chirp, nvoice = 50, freqstep = .02, scale = 25, plot = TRUE)
  ```

  （请参阅 Rwave 文档以讨论输入参数。）

- 3. **wavethresh：** `wavethresh` 函数 `draw` 可用于绘制母小波和父小波。例如，命令

窗口

- iv. 绘制 AR 谱估计器
- v. 绘制 Gabor（使用 Rwave 中的 `cgt`）和 Wigner–Ville 谱

在每种情况下，讨论图中信息是否表明存在平稳性、TVF 等。如果过程似乎是平稳的，描述频率行为。如果过程具有 TVF，讨论其对图产生的效果。

## 12.2 考虑以下母小波：

$$\psi(x) = x,\quad -1 \le x \le 1$$
$$= 0,\quad \text{elsewhere}$$

求并绘制以下伸缩和平移，$\psi_{j,k}(x)$：

- a. $j = 2, k = 0$
- b. $j = 2, k = 3$
- c. $j = -1, k = 3$
- d. $j = -2, k = 3$

## 12.3 本题涉及以下三个数据集的分析：

- 1. prob12.3a
- 2. prob12.3b
- 3. prob12.1c

对于这些数据集：

a. 绘制与 DWT 相关的以下内容：
- i. DWT
- ii. MRA
- iii. 时-尺度图（标度图）

对于这些图中的每一个，讨论该图传达的信息。

## 12.4 考虑问题 12.3 中的三个数据集。对于这些数据集中的每一个绘制 Wigner–Ville 谱，并将其与问题 12.3b 中产生的三个基于小波的图进行比较。就时频谱信息而言比较这些图。

## 12.5 使用方程 12.24 和方程 12.26 中给出的矩阵 M，证明

a. $x_1 = -\frac{1}{\sqrt{2}}d_{1,1} - \frac{1}{2}d_{2,1} - \frac{1}{\sqrt{8}}d_{3,1} + \frac{1}{\sqrt{8}}s_{3,1}$.
b. 求 $x_2$ 的类似表达式。

## 12.6 使用小波分析和 Wigner–Ville 图分析以下数据集。描述这些分析所识别的任何 TVF 行为、突变等。

- a. bat（大棕蝙蝠的回声定位信号）
- b. doppler（多普勒信号）
- c. prob12.6c（模拟数据集）

## 13 G-平稳过程

### 13.1 广义平稳过程

在第 12 章中，我们考虑了用于分析具有时变频率（TVF）的非平稳过程的基于窗口的方法。这些包括短时傅里叶变换（Gabor），以及 Wigner–Ville 和小波表示。在本章中，我们引入了一种完全不同的方法来分析 TVF 数据，其中我们将平稳性的定义扩展到广义平稳（或 G-平稳）过程的类别。这种方法使我们能够将许多非平稳过程的时间索引变换为它们在其上平稳的索引集。

这里的介绍将是入门性的，并且不会详细涵盖这一主题。我们的目的是提供足够的信息，使读者对这种方法有基本的了解。该领域的大多数发展最近才出现在文献中，这些参考文献在此作为进一步细节的来源。

### 定义 13.1

设 $\{X(t) : t \in S\}$ 是定义在 $S \subset \mathbb{R}$ 上的随机过程，设 $u = g(t)$ 是到集合 $R_g \subset \mathbb{R}$ 的映射，并且设 $g^{-1}$ 表示指定的逆。则 $X(t)$ 是 G-平稳过程，如果

- i. $E[X(t)] = \mu$. (13.1)
- ii. $\mathrm{Var}[X(t)] = \sigma^2 < \infty$.
- iii. $E[(X(t) - \mu)(X(g^{-1}(g(t) + g(\tau))) - \mu)] = R_X(\tau)$.

该定义的实用性可能并不立即显而易见。为了更好地理解其含义，假设 $g$ 是时间轴的变换
