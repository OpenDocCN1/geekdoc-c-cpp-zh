

在第 10.3.2、10.3.3 和 10.3.4 节中，我们讨论了促进优化随机分配分配（RAR）程序的方法。所有这些程序都具有以下重要的渐近性质：

- 1. (10.6) 中的极大似然估计量 $\hat{\varrho}_{Em}$ 和 $\hat{\varrho}_{Cm}$ 对于 $\hat{\rho}_E$ 和 $\hat{\rho}_C$ 是强一致的；它们是渐近不相关的，且具有渐近二元正态分布。
- 2. 样本治疗分配比例 $N_E(m)/m$ 对于目标分配比例 $\rho$ 是强一致的，并且具有渐近正态分布，其渐近方差结构已知。

因此，在执行优化 RAR 程序后，可以使用标准的渐近估计量和检验进行统计推断 [35,36]。

## 10.3.2 序贯极大似然估计设计

序贯极大似然估计（SMLE）设计中，治疗随机化概率设置为目标分配比例的当前估计值 [22,46]。特别是，Rosenberger 及其作者在 [10] 中提出了针对 RSIHR 分配 (10.2) 的 SMLE 程序：

$$\phi_{m+l} = \frac{\sqrt{\hat{p}_{Em}}}{\sqrt{\hat{p}_{Em}} + \sqrt{\hat{p}_{Cm}}}} \quad (10.7)$$

他们证明了通过程序 (10.7) 得到的估计量和样本分配比例均具有强一致性和渐近正态性，并证明了 Wald 检验 $$Z_W = (\hat{p}_{Em} - \hat{p}_{Cm})\left(\frac{\hat{p}_{Em}}{N_{Em}(m)} + \frac{\hat{p}_{Cm}}{N_{Cm}(m)}\right)^{-1/2}$$ 在 $H_0: p_E = p_C$ 下从渐近标准正态分布。他们还通过模拟表明，与等随机化设计相比，程序 (10.7) 可以适度减少治疗失败，且对效能的损失最小或没有损失。SMLE 设计的局限性是其波动可能很大，这可能对效能产生负面影响。更详细的 RAR 程序在第 10.3.3 和 10.3.4 节中描述。

## 10.3.3 双重自适应偏硬币设计

双重自适应偏硬币设计（DBCD）是一类 RAR 程序，只要满足某些微的正则条件，它可以针对任何分配比例 $\rho$ [47,48]。DBCD 的核心要素是定义在 $[0,1] \times [0,1]$ 上的分配函数 $g(x, \rho)$。Hu 和 Zhang [48] 提出了以下分配函数：

$$g(x, \rho) = \begin{cases} \frac{\rho^\gamma}{x^\gamma} & 0 < x < 1 \\ \frac{(1-\rho)^\gamma}{(1-x)^\gamma}}{1-x} & x=0,1. \end{cases} \quad (10.8)$$

用户定义的参数 $\gamma \geq 0$ 控制随机程度（$\gamma=0$ 最随机，gamma \to \infty$ 几乎是确定性程序）。$\gamma$ 的作用很快就会变得清晰。

假设目标分配已选择为 $\rho = \rho(p_E, p_C)$。在 $m$ 个患者之后，目标分配估计为 $\hat{\rho}_m = \rho(\hat{p}_E, \hat{p}_C)$。DBCD 将第 $m+1$ 个患者分配到 $E$ 的概率为：

$$\phi_{m+1} = g\left(\frac{N_E(m)}{m}, \hat{\rho}_m\right)$$

其中 $g(x, \rho)$ 如 (10.8) 所示。如果 $\gamma=0$，DBCD 等于 SMLE 设计。Hu 和 Zhang [48] 证明，在 $\rho = \rho(p_E, p_C)$ 的条件下，分配对其自变量连续的，且样本比例和估计量是强一致且渐近正态的。具体而言，$N_E(m)/m$ 的方差为：

$$\sigma_{\gamma}^2 = \frac{\rho(1-\rho)}{(1+\gamma)^2} + \left(\frac{\partial \rho}{\partial p_E}\right)^2 \left(\frac{\partial \rho}{\partial p_C}\right)^2$$

从效能的角度来看，$\sigma_{\gamma}^2$ 越小越好。当 $\gamma=0$ 时，$\sigma_{\gamma}^2$ 最大。当 $\gamma \to \infty$ 时，$\sigma_{\gamma}^2$ 最小，程序几乎是确定性的。Rosenberger 和 Hu [35] 建议使用 $\gamma=2$ 在随机性和效能之间取得平衡。

## 10.3.4 高效自适应设计

Hu 及其作者 [50] 考虑了以下问题：能否找到一种既保持随机化、又能针对任何分配且波动最小的自适应设计？他们提出了一类高效自适应设计（ERADE），第 $m+1$ 个患者随机分配到 $E$ 的概率为：

$$\phi_{m+1} = \frac{\sqrt{\hat{p}_{Em}}}{\sqrt{\hat{p}_{Em}} + \sqrt{\hat{p}_{Cm}}}$$

其中 $0 \leq \zeta \leq 1$ 是控制随机性的用户定义参数。ERADE 的理论性质与 DBCD ；但一个根本区别是 ERADE 是离散的，而 DBCD 是连续的。事实上，当 $\zeta \to 1$ 时，ERADE 优于 DBCD。$N_E(m)/m$ 的方差为：

$$\sigma_{\zeta}^2 = \frac{\rho(1-\rho)}{(1+\zeta)^2} + \left(\frac{\partial \rho}{\partial p_E}\right)^2 \left(\frac{\partial \rho}{\partial p_C}\right)^2$$

这是 RAR 程序的下界。

## 10.3.5 RAR 设计的理论比较

Hu 和 Rosenberger [34] 推导了最优性、波动性和效能之间的关系，可用于 RAR 设计之间的比较。他们考虑了 RAR 后卡方检验非中心参数的二阶展开，并证明影响检验效能的三个重要因素是分配目标、目标的速度以及样本分配的波动性。对于具有相同目标的 RAR 程序，只能比较波动性。波动小的程序是理想的。Hu 及其作者 [51] 将渐近最优 RAR 程序定义为 $N_E(m)/m$ 方差最小的程序。

