
服 $\chi_{(4)}^2$ 分布，其中 $C = I_4$（四阶单位矩阵），$\mathbf{V}_{\beta}$ 是总体响应第 1 至 4 次随访调整后治疗后的协方差矩阵。程序 2.6 中的 SAS/IML 代码执行了该分析。

## 程序 2.6 跨随访治疗响应的全局检验

```
proc iml;

  use _OUTDAT_DEPTEST;

  read all var(beta) into B;

  close;

  use _OUTDAT_COVBETA;

  read all var(V1 V2 V3 V4) into V;

  close;

  C = I(4);

  Q = t(B) * t(C) * inv(C) * V * t(C) * C * B;

  p = 1 - probchi(Q, nrow(C));

  print Q p;

quit;
```

当 $QGlobal=19.44$ 且 $p = 0.0006$ 时，分析表明至少一次随访存在非空治疗效应。注意，4 自由度检验 $QGlobal$ 的效能往往远低于使用跨随访平均治疗差异的 1 自由度检验；这也可以视为跨 4 次随访的治疗效应的全局检验。
额外的分析可以检验原假设，即治疗效应在不同研究随访之间没有差异，

> $H_0 : f_1 = f_2 = f_3 = f_4$。

此处，治疗 $\times$ 随访的统计量和 $p$ 值应基于备择假设下的方差，而非原假设下的方差，因为治疗效应已知是非空的。在这种情况下，

统计量

$Q_{visit} = \hat{\beta}^T C^T (CV_{\beta} C^T)^{-1} C \beta$

服 $\chi^2_{(3)}$ 分布，其中

$$\begin{bmatrix} 1 & 0 & 0 & -1 \\ 0 & 1 & 0 & -1 \\ 0 & 0 & 1 & -1 \end{bmatrix}$$

在程序 2.5 中更改 `HYPOTH ALT` 并设置
`C = {1 0 0 -1, 0 1 0 -1, 0 0 1 -1};`

在程序 2.6 中提供了 $Q_{Treatment \times Visit}= 12.57$ 且 $p = 0.0057$。这表明治疗效应在随访之间存在差异。在第 2.16 节中，我们将演示如何为具有多个响应的分析生成本质精确的结果。

### 2.5 二分类终点的分析

将使用案例研究 1 来说明带有适当协变量调整的二分类终点的分析。具体而言，在本节中，我们将分析第 1 次随访时（良好，优秀）对比（糟糕，差，一般）的二分类响应。如果主要关注点是治疗效应的检验，最合适的协方差矩阵是适用于无治疗差异原假设的矩阵。可以获得精确 $p$ 值；在原假设下，所有重采样数据集具有相同的协方差矩阵。为了说明，我们在协方差调整之前获得了跨分层的加权估计。此示例的 `%NParCov4` 调用在程序 2.7 中。

### 程序 2.7 第 1 次随访的协变量调整的比例差异

```
data RESP;

set RESP;

vlgoodex = (V1 in (3,4));
run;

%NParCov4(OUTCOMES) = vlgoodex, COVARS = gender age baseline
HYPOTH = NULL, STRATA = center, TRTGRPS = treatment, TRANSF
COMBINE = FIRST, EXACT = YES, NREPS = 5000, SEED = 78, DSNI
```

协变量不平衡标准 Q = 6.46 分布情况如下。该标准的渐近 $p$ 值为 0.0911，`OUTDAT CVTEST` 中基于 5000 个置换样本提供的精确 $p$ 值为 0.0922。看起来随机化在各分层之间提供了合理的协变量分布。当设置 `TRANSFORM = NONE` 时，模型在表 2.9 中提供了比例差异的治疗估计。

### 表 2.9 第 1 次随访的协变量调整的线性模型

| 结局 治疗效应 | 标准误 | 统计量 | P值 |
| :--- | :--- | :--- | :--- |
| 随访 1 | 0.1839 | 0.0781 | 5.5455 | 0.01 |

`OUTDAT EXACT` 中基于 5000 个置换样本提供的治疗效应精确 $p$ 值为 0.0164。因此，在调整性别、年龄和基线评分后，积极治疗提供了更高比例的良好或优秀响应。如果对优势比的置信区间感兴趣，我们可以在上述宏调用中指定 `HYPOTH = ALT` 和 `TRANSFORM = LOGISTIC`。然而，此分析导致 `%NParCov4` 出现错误！哪里出问题了？结局足够稀有，以至于某些重采样数据集在分层内的至少一个治疗组中没有成功病例，这导致估计失败。如果预期结局是稀缺的，在指定分析时应格外小心。例如，以下调整中心为协变量的分析结果（程序 2.8）。

### 程序 2.8 第 1 次随访增加中心作为协变量的逻辑模型

```
data RESP;

set RESP;

vlgoodex = (V1 in (3,4));
run;

%NParCov4(OUTCOMES) = vlgoodex, COVARS = gender age baseline
HYPOTH = NULL, STRATA = center, TRTGRPS = treatment, TRANSF
COMBINE = FIRST, EXACT = YES, NREPS = 5000, SEED = 78, DSNI
```

协变量不平衡标准 Q = 6.46 分布情况如下。（此处重复了之前的内容）该标准的渐近 $p$ 值为 0.0911，`OUTDAT CVTEST` 中基于 5000 个置换样本提供的精确 $p$ 值为 0.0922。看起来随机化在各分层之间提供了合理的协变量分布。当设置 `TRANSFORM = NONE` 时，模型在表 2.9 中提供了比例差异的治疗估计。
