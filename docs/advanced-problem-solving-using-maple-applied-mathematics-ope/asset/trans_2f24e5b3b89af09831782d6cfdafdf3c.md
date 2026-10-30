

最小二乘法的关键假设是

- 因变量与自变量之间的关系是线性的，
- 误差相互独立且呈正态分布，并且
- 误差的同方差性[^10]。

如果任何假设不满足，则模型的充分性受到质疑。在初级课程中，残差图中的模式是否出现被用来获取有关模型充分性的信息。 (参见 [A19978], [D2012])。

## 正态性假设丢失

在 logistic 和 Poisson 回归中，因变量的概率介于 0 和 1 之间。根据 Neter [NKNW1996]，该约束同时丢失了上述的正态性和恒定方差假设。在没有这些假设的情况下，F 和 t 检验不能用于分析回归模型。当这种情况发生时，用概率 p 的 logistic 变换，称为 logit p，对模型和数据进行变换，将区间 [0, 1] 映射到 (−∞, +∞)，消除 0–1 约束：

$$\ln\left(\frac{p}{1-p}\right)=\beta_0+\beta_1x_1+\beta_2x_2+\cdots+\beta_nx_n$$

$\beta$s 现在可以解释为增加或减少事件的“对数几率”，并且 $\exp(\beta)$（“几率乘数”）可用于作为相关解释变量单位增加或减少的几率比。

当因变量为计数形式时，我们面临另一种不同的约束。计数都是对应于罕见事件的正整数。因此，Poisson 分布（而不是正态分布）更为合适，因为 Poisson 的均值大于 0，且计数都是正整数。回想一下，Poisson 分布给出了在时间段 t 内发生 y 次事件的概率为

$$P(y;\mu)=\frac{\exp(-\mu t)\cdot(\mu t)^y}{y!}.$$

然后，因变量的对数与解释变量的线性函数相关联。

$$\ln(Y)=\beta_0+\beta_1x_1+\beta_2x_2+\cdots+\beta_nx_n$$

因此

$$Y=(e^{\beta_0})(e^{\beta_1x_1})(e^{\beta_2x_2})\cdots(e^{\beta_nx_n}).$$

换句话说，Poisson 回归模型将“对数结果率”表示为预测变量的线性函数，有时称为“暴露变量”。

$b_i$ 的估计值是用于最大化对数似然函数 $\ln L$ 的数值搜索方法（如果收敛）的最终值（6.4）。$se(b_i)$ 的值，$b_i$ 的标准误差估计值，是方差-协方差矩阵 $VC = -H(X'B^{-1}B)^{-1}B^{-1}$ 主对角线的平方根。$t_i^* = b_i/se(b_i)$ 的值和 $p$ 值，概率 $P(T > |t_i^*|)$。在下面的 Poisson 回归分析汇总表中，设 $m$ 为模型中的变量数，设 $k$ 为因变量 $y$ 的数据元素数。汇总见表 6.10。

**TABLE 6.10: Poisson Regression Variables Summary**

|  | Degrees of Freedom ($df$) | Deviance | Mean Deviance ($MDev$) | Ratio |
|---|---|---|---|---|
| Regression | $m$ | $D_{reg}=D_t-D_{res}$ | $MDev(reg)=D_{reg}/m$ | $\lvert MDev(reg)\rvert$ |
| Residual | $k-1-m$ | $D_{res}=$ result from the full model with $m$ predictors | $MDev(res)=D_{res}/(k-1-m)$ |  |
| Total | $k-1$ | $D_t=$ result from reduced model $y=e^{b_0}$ | $MDev(t)=D_t/(k-1)$ |  |

请注意，使用 Poisson 回归的前提是因变量 $Y$ 必须是离散计数，且大数是罕见事件。我们选择了两个有已发表解的数据集作为基本示例。首先，程序概述如下：

- **Step 0.** 输入 $X$ 和 $Y$ 的数据。
- **Step 1.** 对于 $Y$：
  - (a) 生成直方图，并且  
  - (b) 对 Poisson 分布进行卡方拟合优度检验。¹

  如果 $Y$ 服从 Poisson 分布，则继续。如果 $Y$ 是“计数数据”，则无论卡方检验结果如何，都使用 Poisson 回归。
- **Step 2.** 计算使 (6.5) 最小化的常数模型 $y=\exp(b_0)$ 中的 $b_0$ 值；即最小化两倍偏差。
- **Step 3.** 计算使偏差 (6.5) 最小化的模型 $y = \exp(b_0 + b_1 x)$ 中的 $b_0$ 和 $b_1$ 值。
- **Step 4.** 解释结果和几率比。

我们将按照上述大纲逐步进行一个示例。

## Example 6.10. Hospital Surgeries.

一组医院收集了剖腹产手术数量与总出生人数的数据（见表 6.11）。

**TABLE 6.11: Total Births vs. Caesarean Surgeries**

|    |      |      |      |      |      |      |      |      |      |      |
|----|------|------|------|------|------|------|------|------|------|------|
| Total | 3246 | 2750 | 2507 | 2371 | 1904 | 1501 | 1272 | 1080 | 1027 | 970 |
| Special | 26 | 24 | 21 | 21 | 21 | 20 | 19 | 18 | 18 | 17 |
| Total | 739 | 679 | 502 | 236 | 357 | 309 | 192 | 138 | 100 | 95 |
| Special | 17 | 16 | 16 | 16 | 16 | 15 | 14 | 14 | 13 | 13 |

使用医院的数据集按照上述步骤执行 Poisson 回归。

**Step 0.** 输入数据。

```
> zhc := [3246,2750,2507,2371,1904,1501,1272,1080,1027,970,739,679,502,236,357,309,192,138,100,95] :
> yhc := [26,24,21,21,21,20,19,18,18,17,17,16,16,16,16,15,14,14,13,13] :
> N := nops(yhc);
N := 20
```

**Step 1.** 绘制直方图，然后对 `yhc` 进行卡方拟合优度检验（如适用）。

（注意：Maple 的 Histogram 函数在 Statistics 包中。分箱数据有大量选项；我们将使用 `frequencyscale = absolute` 使条的高度等于相关箱中条目的频率。用 `TallyInto` 收集箱计数。）

```
> with(Statistics):
Dirac(0) := 1.0: # needed for the Poisson distribution
> Bins := $[min(yhc)..max(yhc)];
Bins := [13,14,15,16,17,18,19,20,21,22,23,24,25,26]
```

```
> Histogram(yhc, frequencyscale = absolute);
```

![](img/0f04050177d82aebd17d3383d7334896_283_0.png)

```
> TallyInto(yhc, default, bins = max(yhc) - min(yhc) + 1):
> ObsFreq := rhs~ (%);
ObsFreq := [2, 2, 1, 4, 2, 2, 1, 1, 3, 0, 0, 1, 0, 1]
```

现在进行卡方检验。首先，从估计的 Poisson 分布生成预测值。

```
> λ_est := Mean(yhc);
λ_est := 17.750000000000
```

```
> P := Distribution(Poisson(λ_est)) :
```

```
> PredFreq := [seq(N*PDF(P,t), t in Bins)];
PredFreq := [1.090438738, 1.382520543, 1.635982643, 1.814918244, 1.894988167, 1.868668887, 1.745730144, 1.549335503, 1.309557389, 1.056574712, 0.8154000494, 0.6030562866, 0.4281699634, 0.2923083404]
```

我们准备使用 Maple 的卡方检验 `ChiSquareGoodnessOfFitTest`，显著性水平为 0.05。使用 `summarize = embed` 选项，因为它产生最易读的输出。命令以冒号终止：“嵌入输出”使得返回结果变得不必要。

**Step 3.** 找到最佳指数模型 $y = \exp(b_0 + b_1x)$。让我们使用 Maple 的 `ExponentialFit` 找到模型。

```
> ExponentialFit(zhc, yhc, x, summarize = embed) :
```

### Summary

Model: $14.136875e^{0.00019056858x}$

| Coefficients | Estimate | Standard Error | t-value | $P(>\lvert t\rvert)$ |
|---|---|---|---|---|
| Parameter 1 | $2.64879$ | $0.0192928$ | $137.294$ | $0.$ |
| Parameter 2 | $0.000190569$ | $0.0000132697$ | $14.3612$ | $2.66 \times 10^{-11}$ |

R-squared: 0.999650  
Adjusted R-squared: 0.999611

### Residuals

| Residual Sum of Squares | Residual Mean Square | Residual Standard Error | Degrees of Freedom |
|---|---:|---:|---:|---:|
| 0.0574687 | 0.00319270 | 0.0565040 | 18 |

### Five Point Summary

| Minimum | First Quartile | Median | Third Quartile | Maximum |
|---|---|---|---|---|
| -0.102894 | -0.0420307 | 0.00279072 | 0.0449234 | 0.0788279 |

**Step 4.** 通过计算几率比得出结论。  
使用几率乘数 $\exp(\beta_1)$ 作为近似几率比，通常称为 Poisson 回归的风险比。

```
> OR := exp(0.000190569);
OR := 1.000190587
```

OR 表示 x 增加一个单位时可能增加的幅度。（这个概念与线性规划中的“机会成本”和经济学中的“边际收益”有何关系？）

返回本章开头描述的菲律宾识字率与暴力关系的例子。

## Example 6.11. Violence in the Philippines.

显著暴力行为的数量，SigActs 表 6.12 中，是整数计数。

