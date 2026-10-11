
感兴趣的估计值在输出 9.3 的延续中显示。请参见 Jorge 和 Nagaraj 的 *Overdispersion Models in SAS*. Copyright ©2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RESERVED。有关更多 SAS 资源，请访问 `sas.com/publishing`。

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

注意 $\mathbf{V}_j$ 是一个 $(dm)_j \times (dm)_j$ 矩阵，它反映了关于 $\mathbf{V}_j$ 结构的信念是均值向量 $\mu_j = (\mu_1^j, \mu_2^j, ..., \mu_m^j)$、一组额外的参数 $\alpha$ 以及一个离散（尺度）参数 $\phi$。目前，`GENMOD` 和 `SURVEYLOGISTIC` 只有独立工作矩阵 $\mathbf{V}_j = \text{BlockDiag}(\Delta_{j,1}, \Delta_{j,2}, ..., \Delta_{j,m})$，其中 $\Lambda_j = (\pi_1^j, ..., \pi_m^j)$。我们在下一节中讨论的 `GLIMMIX` 过程在包含 G 随机效应时允许结合明治方差估计进行计算。

多项结果的 GEE 扩展可以在 Lipschitz, Kim 和 Zhao (1994) 以及 Miller, Davis 和 Landis (1993) 中找到。

令 $\mathbf{D}(0,\mathbf{x}_j)=\mathbf{D}_j$ 表示 $\mathbf{g}(0,\mathbf{x}_j)$ 关于 $\theta_0$ 的 $d \times r$ 阶导数矩阵，令 $\mathbf{D}_j = (\mathbf{D}_{j,1}, \mathbf{D}_{j,2}, ..., \mathbf{D}_{j,m_j})^T$ 表示与均值向量 $\mu_j$ 关联的 $(dm)_j \times r$ 矩阵。GEE 估计量 $\theta$ 可以作为广义估计方程的一致解 $\hat{\theta}$：

$$\sum_{j=1}^n \mathbf{D}_j^T \mathbf{V}_j^{-1} (\mathbf{y}_j - \mu_j) = \mathbf{0}. \quad (9.23)$$

## 第 9 章 边缘模型的广义估计方程技术

### 9.9 肩痛患者示例

Lumley (1996) 和 Luo (2000) 分析了一项关于腹内引吸减轻腹镜手术后肩痛的随机临床试验数据。这些数据最初在 Jorgensen 等人 (1995) 中进行分析。手术期间腹部的膨胀会将肝脏与膈肌分离，并对连接两者的附着产生压力。这种压力表现为肩部的放射痛。移除残留筋膜可能会减轻肩部。活性组有 22 名受试者（腹内引吸），控制组有 19 名受试者（无腹内引吸）。腹镜手术后，要求患者在术后及术后三天内的视觉模拟量表对肩部疼痛进行评分（共六个时间点）。由于零过多，该量表被简化为有序类别，其中疼痛评分“1”表示“轻微疼痛”，“5”表示“剧烈疼痛”。除了治疗变量，还有三个协变量，即年龄、性别时间和。协变量是针对特定受试者和时间的。腹镜胆囊切除术后肩部疼痛的数据如表 9.5 所示。让 $y_{ijt}$ 表示第 $i$ 个治疗组第 $j$ 个受试者在 $t$ 时刻的响应，$i=1, 2,\dots,n$ ($n=22, t=1,2,\dots,6$)。因此，响应向量的类别数为 $d=4$。$y_{ijt}$ 的空间为：

$$y_{ijt} \in \begin{pmatrix} 0 & 0 & 0 & 0 \\ 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \end{pmatrix}$$

其中

$$E(y_{ijt}) = \begin{pmatrix} \pi_{1ijt} \\ \pi_{2ijt} \\ \pi_{3ijt} \\ \pi_{4ijt} \end{pmatrix}$$

按照惯例 $\pi_{5ijt} = 1 - \sum_{k=1}^4 \pi_{kij}$。我们将使用“三明治”估计量 (9.24) 和均值拟合一个 GEE 累积 Logit 模型（边缘模型）：

$$\ln \left( \pi_{ijt} / (\pi_{2ijt} + \pi_{3ijt} + \pi_{4ijt} + \pi_{5ijt}) \right) = \alpha_1 + \beta_1 X_{1ijt} + \beta_2 X_{2ijt} + \beta_3 X_{3ijt} + \beta_4 t_t$$
$$\ln \left( \pi_{ijt} / (\pi_{2ijt} + \pi_{3ijt} + \pi_{4ijt} + \pi_{5ijt}) \right) = \alpha_2 + \beta_1 X_{1ijt} + \beta_2 X_{2ijt} + \beta_3 X_{3ijt} + \beta_4 t_t, \quad (9.25)$$
$$\ln \left( \pi_{ijt} / (\pi_{3ijt} + \pi_{4ijt} + \pi_{5ijt}) \right) = \alpha_3 + \beta_1 X_{1ijt} + \beta_2 X_{2ijt} + \beta_3 X_{3ijt} + \beta_4 t_t$$
$$\ln \left( \pi_{ijt} / (\pi_{4ijt} + \pi_{5ijt}) \right) = \alpha_4 + \beta_1 X_{1ijt} + \beta_2 X_{2ijt} + \beta_3 X_{3ijt} + \beta_4 t_t$$

其中 $X_{19}$ 和 $X_{20}$ 是经过正确编码的分类变量，分别代表治疗组和性别；$X_{30}$ 代表受试者的年龄。模型拟合将使用 `SURVEYLOGISTIC` 过程完成。

表 9.5: 腹镜胆囊切除术后肩尖疼痛数据

| 治疗组 | 性别 | 年龄（岁） | 时间 1 | 时间 2 | 时间 3 | 时间 4 | 时间 5 | 时间 6 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Y | F | 64 | 1 | 1 | | 1 | 1 | 1 |
| Y | M | 41 | 3 | 2 | | 1 | 1 | 1 |
| Y | F | 77 | 3 | 2 | 2 | 1 | 1 | 1 |
| Y | F | 54 | 1 | 1 | | 1 | 1 | 1 |
| Y | F | 66 | 1 | 1 | 1 | 1 | 1 | 1 |
| Y | M | 56 | 1 | 2 | | 1 | 1 | 1 |
| Y | M | 81 | 1 | 3 | 2 | | 1 | 1 |
| Y | F | 24 | 2 | 2 | | 1 | 1 | 1 |
| Y | F | 56 | 1 | 1 | | 1 | 1 | 1 |
| Y | F | 29 | 3 | 1 | | 1 | 1 | 1 |
| Y | M | 65 | 1 | | | 1 | 1 | 1 |
| Y | F | 68 | 2 | 1 | | 1 | 1 | 2 |
| Y | F | 77 | 1 | 1 | 2 | 2 | 2 | 2 |
| Y | M | 35 | 3 | 1 | 1 | | 3 | 3 |
| Y | F | 66 | 2 | 1 | | 1 | 1 | 1 |
| Y | F | 70 | 1 | 1 | | 1 | 1 | 1 |
| Y | F | 79 | 1 | 1 | | 1 | 1 | 1 |
| Y | F | 65 | 2 | 1 | | 1 | 1 | 1 |
| Y | F | 61 | 4 | 4 | 2 | | 2 | 2 |
| Y | F | 67 | 4 | 4 | 4 | 2 | | 1 |
| Y | F | 32 | 1 | 1 | | 2 | 1 | 1 |
| Y | F | 33 | 1 | 1 | 1 | 2 | | 2 |
| N | F | 20 | 5 | 2 | 3 | 5 | 4 | |
| N | F | 50 | 1 | 5 | 3 | 4 | 5 | |
| N | F | 40 | 4 | 4 | 4 | 4 | 1 | 3 |
| N | M | 54 | 4 | 4 | 4 | 4 | 4 | 3 |
| N | M | 34 | 2 | 3 | 4 | 3 | 3 | 2 |
| N | F | 34 | 3 | 4 | 3 | 3 | 2 | 2 |
| N | F | 34 | 3 | 4 | 3 | 3 | 3 | | |
| N | F | 34 | 3 | 4 | 4 | | | | |
| N | M | 56 | 3 | 3 | 4 | 4 | 3 | 3 |
| N | F | 82 | 1 | 1 | 1 | 1 | 1 | 1 |
| N | M | 52 | 1 | 5 | 5 | 4 | 3 | 3 |
| N | F | 65 | 1 | 3 | 2 | 2 | 1 | 1 |
| N | M | 53 | 2 | 2 | 3 | 4 | 2 | 2 |
| N | F | 40 | 2 | 2 | 1 | 3 | 3 | 3 |
| N | M | 58 | 1 | 1 | 1 | 1 | 1 | 1 |
| N | F | 63 | 1 | 1 | 1 | 1 | 1 | 1 |
| N | M | 41 | 5 | 5 | 4 | 3 | 3 | 3 |
| N | M | 72 | 3 | 3 | 3 | 1 | 1 | 1 |
| N | F | 60 | 5 | 4 | 4 | 2 | 2 | 2 |
| N | M | 61 | 1 | 3 | 3 | 2 | 1 | 1 |

程序 9.6 提供了读取表 9.5 数据以及拟合之前 GEE Logit 模型的程序语句。

程序 9.6: 对肩部数据拟合 GEE Logit 模型

```sas
Reference: Lumley, T. (1996) "Generalized Estimating Equations for Ordinal Data: A Note on Working Structures." Biometrics 52, 354-363

data Shoulder_tip_pain;

  input trt $ gender $ age t1-t6;

  subject_id = _n;

  array tt t1-t6;

  do tt;

    y = tt;

    time = _i;

    output;

  end;

  datalines;

  y f 64 1 1 1 1 1

  y m 41 3 2 2 1 1

  y f 77 3 2 2 1 1

  y f 54 1 1 1 1 1

  y f 66 1 1 1 1 1 1

  y m 56 1 2 1 1 1

  y f 81 3 2 1 1 1

  y m 24 2 2 1 1 1

  y f 56 1 1 1 1 1

  y m 29 3 1 1 1 1

  y f 65 1 1 1 1 1

  y m 68 2 1 1 1 2

  y f 77 1 1 2 2 2

  y m 35 3 1 1 3 3

  y f 66 2 1 1 1 1

  y m 70 1 1 1 1 1

  y f 79 1 1 1 1 1

  y m 65 2 1 4 2 2

  y f 61 4 4 2 2 1

  y m 67 4 4 2 1 1

  y f 32 1 1 2 1 2

  y m 33 1 1 2 1 2

  y f 20 5 2 3 5 4

  y m 50 1 5 3 4 3

  y f 40 4 4 4 4 1

  y m 54 4 4 4 4 3

  y m 34 2 3 4 3 3

  y f 34 3 4 3 3 2

  y m 56 3 3 4 4 3

  y f 82 1 1 1 1 1

  y m 52 1 5 5 4 3

  y f 65 1 3 2 2 1

  y m 53 2 2 3 4 2

  y f 40 2 2 1 3 3

  y m 58 1 1 1 1 1

  y f 63 1 1 1 1 1

  y m 41 5 5 4 3 3

  y m 72 3 3 3 1 1

  y f 60 5 4 4 2 2 2

  y m 61 1 3 3 2 1 1

;;
```
