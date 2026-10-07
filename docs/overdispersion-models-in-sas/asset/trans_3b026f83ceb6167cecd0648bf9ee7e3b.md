
## 第 9 章 边缘模型的广义估计方程技术

然而，无法使用 `dist=binomial` 和 `link=log` 选项获得率比结果，因为偏移变量（offset variables）产生的均值参数对于某些观测值是无效的或处于极限。顺便提到，本节描述的方法也适用于 9.6 节讨论的 Proagide 示例中的重复测量。模型 (9.9) 回归参数的解释如下：

| 治疗组 | 访问次数 | 每周预期发作次数 |
| --- | --- | --- |
| 安慰剂 (Placebo) | 基线 (Baseline) | exp(β₁) |
| | 治疗期 (Treatment Phase) | exp(β₀ + β₁) |
| Proagide | 基线 | exp(β₀ + β₂) |
| | 治疗期 | exp(β₀ + β₂ + β₃) |

基线率与 Proagide 率的比例为 exp(-β₂)，治疗期安慰剂率与 Proagide 率的比为。注意 $\beta₁$ 是随机化的效应。此外，安慰剂治疗期与基线的比例为 $R₁ = exp(β₁)$，它捕捉了安慰剂效应；而 Proagide 治疗期与基线的比例为 $R₂ = exp(β₂ + β₃)$。

最后，$R₃ = exp(-β₁)$ 代表 $R₁$ 与 $R₂$ 的比例。该比例 $R₃$ 可以被看作是在将在每种率与其相关的基线率进行归一化后，安慰剂治疗率与 Proagide 率的比例。这些率、它们的对数及其标准差可以使用上一个示例中解释的方法通过 `GLIMMIX` 过程进行估计。编程语句在程序 9.3 的延续中所示。

## 程序 9.3：延续

```sas
ods html;
*** Rates Proagide Trial ***
proc glimmix data=seizures;
class id;
model cnt = trt xl1*trt dist=poison offset=time covb=none random / subject=typecorr;
estimate 'Rate Placebo Baseline' 1;
estimate 'Rate Placebo Treatment Phase' 1;
estimate 'Rate Proagide Baseline' 1;
estimate 'Rate Placebo TRT Phase' trt-1 xl1*trt 1;
estimate 'Rate Placebo Proagide Baseline' trt-1 xl1*trt -1;
estimate '(R1) Baseline TRT Phase / Placebo Baseline' xl1 1;
estimate '(R2) Proagide TRT Phase / Proagide Baseline' xl1*trt 1;
estimate '(R3) = (R1) / (R2)' xl1*trt -1;
run;
ods html close;
```

感兴趣的估计值在输出 9.3 的延续中显示。请参见 Jorge 和 Nagaraj 的 *Overdispersion Models in SAS*. Copyright ©2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RESERVED。有关更多 SAS 资源，请访问 sas.com/publishing。

## 输出 9.3：延续

| Rates Proagide Trial *** | | 估计值 | 标准误 | DF | t 值 | Pr >t | 均值 | 标准误 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Rate Placebo Baseline | 1.3476 | 0.1574 | Inf | 8.56 | <0.0001 | 3.8482 | 0.6055 |
| Rate Placebo TRT Phase | 1.4584 | 0.1986 | Inf | 7.69 | <0.0001 | 4.2991 | 0.8150 |
| Rate Proagide Baseline | 1.2396 | 0.1129 | Inf | 10.98 | <0.0001 | 3.4542 | 0.3900 |
| Rate Proagide TRT Phase | 1.1048 | 0.1577 | Inf | 6.65 | 2.8542 | 0.4502 |
| Placebo Baseline / Proagide Baseline | 1.1080 | 0.1937 | Inf | 0.56 | 1.1141 | 0.2158 |
| Placebo TRT Phase / Proagide TRT Phase | 1.4096 | 0.2466 | Inf | 1.66 | 1.0567 | 0.3715 |
| (R1) Proagide TRT Phase / Placebo Baseline | 0.1108 | 0.1161 | Inf | 0.3399 | 1.1172 | 0.1297 |
| (R2) Proagide TRT Phase / Proagide Baseline | -0.1908 | 0.1258 | Inf | -1.52 | 0.1294 | 0.8263 | 0.1040 |
| (R3) = (R1) / (R2) | 0.3016 | 0.1712 | Inf | 1.76 | 0.0781 | 1.3520 | 0.2315 |

两个基线率对数的差值（如前所述，这构成了随机化效应）为 0.1080，估计标准误为 0.1937。如所述，该结果在统计上并不显著（P=0.5770）。这两个率的比例为 1.1141。两个治疗期对数的差为 0.4096，估计标准误为 0.2466。该结果具有边缘显著性（P=0.0967）。这两个率的比例为 1.5063，表明 Proagide 使发作次数减少了约 50%。两个安慰剂率（治疗期到基线）的比例 $R_1$ 估计值为 1.1172。其对数为 0.1108，估计标准误为 0.1161。这对应的 $P$ 值 0.3399，表明没有安慰剂效应。两个 Proagide 率（治疗期到基线）的比例 $R_2$ 估计值为 0.8263。在模型尺度上，其对数结果为 -0.1908。最后，安慰剂治疗期率与 Proagide 率（通过其相应的基线率归一化）的估计比例为 1.3540，表明 Proagide 的药效使发作次数减少了约 35%。由对数线性模型提供的该比例的对数为 0.3016。其估计标准误为 0.1712，相关的 $P$ 值为 0.0781。

## 9.8 用于多项响应的 GEE 方法

考虑一种 $n$ 个簇的情况。如前几章所述，这些簇可以是家庭，其中家庭成员是元素单位；孕妇率，其中单个孕率内的胎儿是元素单位；组内成员是元素单位的情况，等等。在涉及重复测量的纵向研究中，每个个体构成一个簇，重复测量是元素单位。令 $m_j$ 表示第 $j$ 个簇中的元素单位数量，$j=1,...,m_j$。令 $y_j$ 表示一个 $(d+1)$ 维列向量 $y_j^*$。向量 $y_j^*$ 除第 $s$ 位置外全部为零。令 $\pi_j$ 表示第 $j$ 个簇中 $y_j^*$ 的期望值，$\pi_j = (\pi_{js1}^*, \dots, \pi_{js}^*)$，其中0 < \pi_{js} < 1$ 且 $\sum_{s=1}^{d+1}\pi_{js} = 1$。由于这种线性依赖关系，$\pi_j^*$ 是 $y_j$ 的最后一类。与每个 $y_j$ 关联的是一个 $k$ 维解释变量 $\mathbf{x}_j$，通过平滑函数 $g(\theta,\mathbf{x}_j)$ 依赖于未知参数 $\theta$ 的 $r$ 维向量，使得 $\pi_j = g^{-1}(\theta,\mathbf{x}_j) = \begin{pmatrix} g^{-1}(\theta,\mathbf{x}_{j1}) \\ \vdots \\ g^{-1}(\theta,\mathbf{x}_{jd}) \end{pmatrix}$ (9.21)。

链接函数的示例在 7.3 节中给出。现在可以使用上述均值结构和方差协差结构 $\mathbf{V}_j$ 来实施 GEE 方法，对于观测值 $y_{ji}$，$j=1,2,...,m_j$，其中 $\mathbf{V}_j = \begin{pmatrix} y_{j1} \\ y_{j2} \\ \vdots \\ y_{jm_j} \end{pmatrix}$ (9.22)。

SAS 中的过度离散模型

注意 $\mathbf{V}_j$ 是一个 $(dm)_j \times (dm)_j$ 矩阵，它反映了关于 $\mathbf{V}_j$ 结构的信念是均值向量 $\mu_j = (\mu_1^j, \mu_2^j, ..., \mu_m^j)$、一组额外的参数 $\alpha$ 以及一个离散（尺度）参数 $\phi$。目前，GENMOD 和 SURVEYLOGISTIC 只有独立工作矩阵 $\mathbf{V}_j = \text{BlockDiag}(\Delta_{j,1}, \Delta_{j,2}, ..., \Delta_{j,m})$，其中 $\Lambda_j = (\pi_1^j, ..., \pi_m^j)$。我们在下一节中讨论的 `GLIMMIX` 过程在包含 G 随机效应时允许结合明治方差估计进行计算。

多项结果的 GEE 扩展可以在 Lipschitz, Kim 和 Zhao (1994) 以及 Miller, Davis 和 Landis (1993) 中找到。

令 $\mathbf{D}(0,\mathbf{x}_j)=\mathbf{D}_j$ 表示 $\mathbf{g}(0,\mathbf{x}_j)$ 关于 $\theta_0$ 的 $d \times r$ 阶导数矩阵，令 $\mathbf{D}_j = (\mathbf{D}_{j,1}, \mathbf{D}_{j,2}, ..., \mathbf{D}_{j,m_j})^T$ 表示与均值向量 $\mu_j$ 关联的 $(dm)_j \times r$ 矩阵。GEE 估计量 $\theta$ 可以作为广义估计方程的一致解 $\hat{\theta}$：

$$\sum_{j=1}^n \mathbf{D}_j^T \mathbf{V}_j^{-1} (\mathbf{y}_j - \mu_j) = \mathbf{0}. \quad (9.23)$$
