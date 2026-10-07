
$\beta$ 的 FE 估计器（在假设误差 $\varepsilon_{ij}$ 独立同分布的情况下，FE 模型中的 FGLS 估计器）可以证明等于变换模型中的 OLS 估计器，该模型被称为组内模型或均值差模型：

$$(y_g - \bar{y}_g) = (x_g - \bar{x}_g)'\beta + (\varepsilon_g - \bar{\varepsilon}_g) \quad (6.6)$$

其中，例如 $\bar{x}_g = N^{-1}\sum_{i=1}^{N_g} x_{gi}$。注意，聚类内不变的变量会消失，因为对于所有 $i$，$x_{gi} = x_g$ 意味着 $\bar{x}_g = x_g$。这是 $y$ 的聚类内变异对 $x$ 的聚类内变异的回归。因此，FE 估计也被称为组内估计量。

FE 估计是一致的，无论聚类特定效应是固定的还是随机的。但可能会导致效率损失，因为 FE 估计只使用了数据中的聚类内变异，且聚类不变回归变量的系数无法识别。

获取 $\beta$ 的 FE 估计有多种方法。首选方法是使用 `xtreg, fe` 并配合聚类稳健标准误。

- * 使用 xtreg, fe 使用 hh FE 进行 hh FE 估计*

- `xtreg parsing inhxep illness, fe vce(robust) note: Innhxep omitted because of collinearity.`

| 固定效应（组内）回归 | 观测值 | 27,753 |

| :--- | :--- | :--- |

| 分组变量: hh | 组数 | 5,739 |

| 每组观测值: | | |

| R 方方: | | |

| Within = 0.1541 | min = 1 | |

| Between = 0.2069 | avg = 4.8 | |

| Overall = 0.1816 | max = 19 |

$F(1,538) = 1155.53, Prob > F = 0.0000$

corr(u_i, Xb) = 0.0160

(已针对 hh 中的 5,739 个聚类调整了标准误)

| pharis | 系数 | 标准误. | t | P>|t| | [95% 置信区间] |

| :--- | :--- | :--- | :--- | :--- | :--- |

| inhxep | 0 (omitted) | | | | |

| illness | .6089755 | .0179147 | 33.99 | 0.000 | .5738555 | .644095 |

| _cons | .1233569 | .0111401 | 11.88 | 0.000 | .1105181 | .1541957 |

| sigma_u | .82219146 | |

| sigma_e | 1.0606587 | |

| rho | .37534725 (由于 u_i 引起的方差比例) | |

注意 lnhhexp 的系数无法识别。这是因为 lnhhexp 对于家庭中的每个个体都是相同的，lnhhexp 在聚类内没有变异，因此对于该变量 $(x_{gi} - \bar{x}_g) = 0$。illness 的系数为 0.609，类似于 OLS 估计的 0.624。截距不为零是因为 xtreg, fe 命令将 (6.6) 修改为：

$$(y_{gi} - \bar{y}_g) = \alpha + (x_{gi} - \bar{x}_g)'\beta + (\varepsilon_{gi} - \bar{\varepsilon}_g) \quad (6.7)$$

其中 $\bar{y}$ 和 $\bar{x}$ 是 $y$ 和 $x$ 的总体平均值。这得到了相同的估计。如果感兴趣 lnhhexp，那么 FE 估计在应用中没有用。但如果感兴趣 illness，即使 与家庭效应 $\alpha_g$ 相关，FE 估计也提供了一致估计。一致性只需要在控制了回归变量和聚类特定效应 $\alpha_g$ 后，illness 与剩余误差 $\varepsilon_{gi}$ 不相关。

### 6.6.3 FE 估计的聚类稳健标准误

与 RE 估计类似，在加入固定效应 $\alpha_g$ 后，通常仍然存在异方性和聚类内误差相关，因此推断应基于聚类稳健标准误。我们按照聚类控制顺序（无、家庭、村庄）比较了使用 xtreg, fe 对 FE 估计的 VCES。

- * 使用 hh 和各种标准误进行 FE 估计*

- `* xtreg inhxep illness, fe store FE_def`

- `* xtreg inhxep illness, fe vce(robust) store FE_rob`

- `* xtreg inhxep illness, fe vce(cluster hh) store FE_hh`

- `* xtreg inhxep illness, fe vce(cluster commune) store FE_comm`

- `* regress inhxep illness, vce(cluster hh) estimates FE_def FE_rob FE_comm OLS_hh, b(%4f) stats(N)`

| 变量 | FE_def | FE_rob | FE_hh | FE_comm | OLS_hh |

| :--- | :--- | :--- | :--- | :--- | :--- |

| lnhhexp | (omitted) | (omitted) | (omitted) | (omitted) | 0.0247 |

| illness | 0.0690 | 0.0690 | 0.0690 | 0.0690 | 0.0140 |

| | 0.0096 | 0.0179 | 0.0179 | 0.0276 | 0.0183 |

| _cons | 0.1324 | 0.1324 | 0.1324 | 0.0172 | 0.0235 |

| | 0.0087 | 0.0111 | 0.0111 | 0.0590 | 0.0367 |

| N | 27753 | 27753 | 27753 | 27753 | 27753 |

图例: b/se

第一列给出的默认误差严重低估了 illness 的标准误。第二列和第三列是相同的，证明了 vce(robust) 等于 vce(cluster var) 选项，前提是 clustervar 是 xtset 命令中的变量。这些是最常用的标准误。第四列在更广泛的社区层面进行聚类。这可能是因为住户嵌套在社区内，导致了更大的标准误。

FE 估计通常比 OLS 估计效率低，有时差异很大，因为它只使用了数据的变异。但在应用中，都聚类家庭的第三列和第五列在 illness 的标准误上差异很小。

### 6.6.4 计算 FE 估计的替代方法

模型 (6.5) 计算 FE 估计有替代方法。尽管这些方法得到了相同的 $\beta$ 估计和相似的默认标准误，我们强烈建议使用 xtreg, fe 命令。首先，xtreg, fe 的计算速度比对每个个体回归指示变量更快。其次，如果每个聚类的观测值很少，除 xtreg, fe 以外的命令会计算自由度而高估标准误。

一种方法是直接估计模型 (6.5) 中的 $\alpha_g, g=1, \dots, N_g$ 和 $\beta$。这是最小二乘虚拟变量（LSDV）估计器，通过 OLS 回归获得：

```
$y_{gi} = \left(\sum_{h=1}^{G} \alpha_h d_{h,gi}\right) + x'_{gi}\beta + \varepsilon_{gi} \quad (6.8)$
```

其中有 $G$ 个个体指示变量 $d_{h,gi}, g=1, \dots, G$，如果 $h=g$，则对于第 $g$ 个观测值 $d_{h,gi}=1$，否则 $d_{h,gi}=0$。

这种暴力方法涉及 $(G+K) \times (G+K)$ 矩阵的逆，在当前 $G+K=4168$ 的示例中是有问题的。因此，我们在下文中仅使用住户的子集来说明该方法。

我们将分析限制在恰好有 2 个成员的 441 个家庭中。

固定效应（FE）模型通过以下方式拟合：1) 应用 LSDV 模型的 `regress` 命令，2) `areg` 命令，以及3) `xtreg, fe` 命令。

对于 `regress` 命令，441 个虚拟变量作为 `i.hh` 输入，导致了大量的回归变量，从而使得 `matsize` 值较大。对于当前的示例并使用 Stata 17，并没有这个问题。在 Stata 17 之前的版本，可能需要使用 `set matsize` 命令将 `matsize` 从程序默认增大。在 Stata 17 中，`set matsize` 命令是多余的，但矩阵大小受 Stata版本的限制；`help limits` 命令提供了这些限制。

我们获得了默认标准误和聚类稳健标准误。我们有：

+ * 使用 xtreg, reg, areg 进行 hh FE 估计的各种标准误

* preserve

* keep if humansorninhh == 2

(删除了 26,871 个观测值)

+ * qui regress pharis inhhexp illness i.hh

* estimates store LSDV_dev

* qui areg pharis inhhexp illness, absorb(hh)

* estimates store ARE_dev

* qui xtreg pharis inhhexp illness, fe

* estimates store REG_dev

* qui regress pharis inhhexp illness i.hh, vce(cluster hh)

* estimates store LSDV_clu

* qui areg pharis inhhexp illness, absorb(hh) vce(cluster hh)

* display "AREG se times square-root(2) = "se[illness]/sqrt(2)

AREG times square-root(2) = .1281704

* estimates store ARE_clu

* qui xtreg pharis inhhexp illness, fe vce(cluster hh)

* estimates store XREG_clu

| 变量 | LSDV_dev | AREG_dev | XREG_dev | LSDV_clu | AREG_clu | XREG_clu |

|---|---|---|---|---|---|---|

| illness | 0.8402 | 0.8402 | 0.8402 | 0.8402 | 0.8402 | 0.8402 |

| | 0.0949 | 0.0949 | 0.0949 | 0.1813 | 0.1813 | 0.1282 |

| lnhxep | -0.3722 | (omitted) | (omitted) | -0.3722 | (omitted) | (omitted) |

| | 0.4035 | | | 0.0214 | | |

| _cons | 2.3366 | 0.0705 | 0.0705 | 2.3366 | 0.0705 | 0.0705 |

| | 1.3794 | 0.1095 | 0.1095 | 0.0000 | 0.1930 | 0.1257 |

| | 882 | 882 | 882 | 882 | 882 | 882 |

|---|---|---|---|---|---|---|

| r2 | 0.6188 | 0.6188 | 0.1512 | 0.6188 | 0.6188 | 0.1512 |

| df_m | 441.0000 | 1.0000 | 441.0000 | 0.0000 | 1.0000 | 0.0000 |

图例：b/se

. restore

`areg` 和 `xtreg, fe` 命令产生的系数估计完全相同。使用 `regress` 命令拟合的 LSDV 变体提供了相同的拟合效果以及相同的 `illness` 系数。其他系数的明显差异源于以下原因：LSDV 截距之所以不同，是因为 `areg` 和 `xtreg, fe` 命令使用总均值来估计 (6.7) 而不是 (6.6)。LSDV 的 `lnhxep` 系数是非零，而 `lnhxep` 是未被识别的，`regress` 命令不知道不可识别的来源，而是删除了一个家庭虚拟变量。

三种方法的 `illness` 默认标准误是相同的，且使用 `areg` 和 `xtreg, fe` 命令得到的截距默认标准误也是相同的。

重要的区别在于聚类稳健标准误。`areg` 和 LSDV 估计得到的标准误比 `xtreg, fe` 命令大得多。事实上，在这个示例中，`illness` 的差异是 $\sqrt{2} = 1.414$ 倍。

这种巨大差异的原因如下：聚类稳健估计使用了有限样本修正 $\{G/(G-1))\{(N-1)/(N-K)\}$，其中 $K$ 是已识别的回归变量数量，在本示例中 $N=882$。有两个已识别的回归变量（截距和 `illness`），因此 `xtreg, fe` 命令设置 $K=2$ 且 $N-K=882-2=880$。用于 LSDV 模型的 `are` 命令和 `regress` 统计了 440 个虚拟变量，导致 $K^*=442$ 且 $N-K^*=882-442=440$。这正好是使用 `xtreg, fe` 命令计算的 $N-K$ 的一半，导致 LSDV 的 VCE 是标准误的 $\sqrt{2}$ 倍。对于聚类稳健误差，虚拟变量不应计入自由度；应该使用 `xtreg, fe`。更一般地说，`areg` 和 LSDV 标准误是 `xtreg, fe` 标准误的 $\sqrt{(N-K)/(G-K)}$ 倍，其中 $K$ 是模型中已识别的回归变量数量（6.5）。相关 RE 模型在6.6.4节中个体效应建模为 $\alpha_g = \bar{x}_{1,g}\gamma + \eta_g$，其中 $\eta_g$ 是 i.i.d. 误差，且 $\bar{x}_{1,g}$ 是聚类内回归变量的平均值（6.5）变为 $y_{gi} = \bar{x}'_{g}\eta + \bar{x}'_{g}\gamma + (\eta_g + \varepsilon_{gi})$。该模型被解释为 RE 模型，其 假设取决于 $x_{gi}$ 和 $\bar{x}_{1,g}$。对于当前示例，我们获得了固定 hh 的 RE 估计：

* sort hh

* by hh: egen avelxp = mean(lnhexp)

* by hh: egen aveillness = mean(illness)

xtreg pharis avelxp aveillness lnnhexp illness, rce(cluster hh)：lnhexp 因为共线性被省略。

| 随机效应 GLS 回归 | 观测值 = 27,753 |

| 分组变量: hh | 分组数 = 7,739 |

| R平方: | 每组观测值: |

| Within = 0.1541 | 最小值 = 1 |

| Between = 0.2071 | 平均值 = 4.8 |

| Overall = 0.1818 | 最大值 = 19 |

| corr(u_i, X) = 0 (假设) | (针对 7,739 个 hh 聚类调整的标准误) |

| Wald chi2(3) = 1370.89 | Prob > chi2 = 0.0000 |

| | 系数 | 标准误 | z | P|z| | [95% 置信区间] |

|---|---|---|---|---|---|

| avelxp | .022084 | .014486 | 1.52 | .127 | -.006393 .0504773 |

| aveillness | .031165 | .028438 | 1.10 | .273 | -.024603 .0869329 |

| lnnhexp | 0 (省略) | | | | |

| illness | | .017153 | .000 | .573861 | .6440889 |

| _cons | | .069077 | .039396 | 1.55 | .122 | -.016134 .138295 |

| sigma_u | .6262406 | | | | |

| sigma_e | 1.0606587 | | | | |

| rho | | .2548818 | (由于 u_i 引起的方差比例) | |

illness 的系数与 FE 估计器相同。变量 `avelxp` 不聚类，因此被省略；如果回归变量顺序不同，`avelxp` 可能会被省略。

这种方法在非线性模型中非常有用，因为由于偶然参数问题，短面板没有标准的 FE 估计器；参见 2.2.1。同伴小组文献中使用的这种规范的变体包括一个回归变量，即在同伴小组或类似于同伴小组的参考组上的 x 平均值。其意图是控制同伴或参考组平均特征的影响，后者是研究样本的一个子集。Manski [1993] 的“均值线性”模型包含了同伴小组成员回归变量的平均值；这也被解释为捕捉截面相关性或社会相互依赖性的控制。

### 6.6.6 计算双向 FE 的方法

当固定效应产生两个不嵌套的不同原因时，会出现双向 FE 模型，例如对于每个雇主和员工可能有多个观测值的匹配雇主-员工数据。

如果两个维度上的固定效应很少，可以使用带有虚拟变量的 `regress` 命令。假设两个维度的标识符为 id 和 id2。那么我们可以输入 `regress y x.id i.id2`。
