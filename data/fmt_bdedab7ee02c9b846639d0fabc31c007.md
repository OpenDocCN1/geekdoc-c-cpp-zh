
$$Var(\hat{\beta}-\beta) \triangleq Var(\hat{\beta}) \triangleq (\mathbf{D}^{\top}\mathbf{D})^{-1}\mathbf{D}^{\top}\mathbf{V}^{-1}(\mathbf{y}-\boldsymbol{\mu})(\mathbf{y}-\boldsymbol{\mu})^{\top}\mathbf{V}^{-1}\mathbf{D}(\mathbf{D}^{\top}\mathbf{D})^{-1}$$

如果通过 $\mathbf{D}^{\top}\mathbf{D}$ 定义 $\mathbf{H}$，且 $\mathbf{D}^{\top}\mathbf{V}^{-1}(\mathbf{y}-\boldsymbol{\mu})^{\top}\mathbf{V}^{-1}\mathbf{D}$ 为 $\mathbf{G}$，则方差协方差矩阵可以写为

$$Var(\hat{\beta}-\beta) \triangleq (\mathbf{D}^{\top}\mathbf{D})^{-1}\mathbf{G}(\mathbf{D}^{\top}\mathbf{D})^{-1}$$

。

# 294 过离散模型（Overdispersion Models）

“三明治”术语显然源于：

$$H^{-1} \quad G \quad H^{-1}$$

$$\uparrow \quad \uparrow \quad \uparrow$$

$$\text{Bread} \quad \text{Meat} \quad \text{Cheese}$$

现在我们转向基于线性化的伪似然估计，`GLIMMIX` 过程使用了这种方法。因此，广义线性混合模型的开始是：

$$y = X\beta + Z\gamma \quad (9.5)$$

其中 $\beta$ 是固定效应参数，$\gamma$ 是随机效应。$g(\cdot)$ 是连接函数，$g^{-1}(\cdot)$ 是其反函数，$\eta = X\beta + Z\gamma$ 是线性预测值。$\phi$ 是离散度参数。$X$ 包含了协变量，请参考 McCulloch 和 Searle (2001)。我们假设 $\gamma \sim \text{Normal}(0, G)$，且方差协方差矩阵为

$$G$$

。

# 第9章 边际模型的广义估计方程技术 295

广义线性模型（GLMM）的通用设置是

$$E(y|\gamma) = g^{-1}(X\beta + Z\gamma) = \mu \quad (9.6)$$

其中 $g(\cdot)$ 是连接函数，$g^{-1}(\cdot)$ 是其反函数，$\eta = X\beta + Z\gamma$ 是线性预测值。$Y$ 的方差为

$$Var(Y|\gamma) = A^{1/2}RA^{1/2} \quad (9.7)$$

其中 $A$ 是一个包含模型方差的对角矩阵，$R$ 是通过 `RANDOM` 语句指定的方差协方差矩阵。不要将其与之前描述的混淆。参考 SAS 文档中的“Mixed Models”部分。如果数据的条件分布包含一个额外的尺度参数，它要么属于方差函数，要么属于 $R$ 矩阵。在我们所讨论的模型中，不会出现这种情况，因为 $\phi=1$。基于线性化的伪似然估计来估计 (9.6) 中的 GLMM 参数的方法表示为：

$$Var(Y) = G + R$$

G-side 和 R-side 之间的关系根据 Wolfgang 和 O’Connell (1993) 的术语，表示为

$$\Sigma^* = \hat{\Delta}^{-1}A^{1/2}RA^{1/2}\hat{\Delta}^{-1}$$

## SAS 中的 296 过度离散模型

| 描述 | TYPE=covariance-structure | 结构 | 示例 |
| --- | --- | --- | --- |
| 方差分 | VC (默认) | 指定标准方差，是 G 侧和 R 侧协方差的默认结构。在 R 侧结构中，TYPE=VC 仅用于建模过度离散效应，或配合 GROUP= 选项指定异方差模型。指定复合对称结构，其具有恒定的方差和恒定的对称性 | $\begin{pmatrix} \sigma_B^2 & 0 & 0 & 0 \\ 0 & \sigma_B^2 & 0 & 0 \\ 0 & 0 & \sigma_{AB} & 0 \\ 0 & 0 & 0 & \sigma_{AB}^2 \end{pmatrix}$ |
| 复合对称 | CS | $Cov(\epsilon_i^*, \epsilon_j^*) = \begin{cases} \sigma+\phi & i=j \\ \sigma & i \neq j \end{cases}$ 复合对称结构在嵌套随机效应下自然产生，例如当抽样误差嵌套在实验误差中时。 | $\sigma+\phi & \sigma & \sigma & \sigma \\ \sigma & \sigma+\phi & \sigma \\ \sigma & \sigma & \sigma \\ \sigma & \sigma & \sigma & \sigma+\phi$ |
| 一阶自回归 | AR(1) | 指定一阶自回归结构，$Cov(\epsilon_i^*, \epsilon_j^*) = \sigma^2\rho^{|i-j|}$，其中 $i^*$ 和 $j^*$ 是根据第 $i$ 次和第 $j$ 次观测得出的，并不一定等于观测序号。 | $1 & \rho & \rho^2 & \rho^3 \\ \rho & 1 & \rho^2 & \rho \\ \rho^2 & \rho & 1 & \rho \\ \rho^3 & \rho & \rho & 1$ |
| 无结构 | UN | 指定一个由方差和相关性参数化的完全（无结构）协方差矩阵。如果你指定 UN(q)，则 GLIMMIX 过程将只估计矩阵的前 "q" 条带，并将所有更高条带的元素设置为零。 | $\sigma_{11}^2 & \sigma_{12}^2 & \sigma_{13}^2 & \sigma_{14}^2 \\ \sigma_{21}^2 & \sigma_{22}^2 & \sigma_{23}^2 & \sigma_{24}^2 \\ \sigma_{31}^2 & \sigma_{32}^2 & \sigma_{33}^2 & \sigma_{34}^2 \\ \sigma_{41}^2 & \sigma_{42}^2 & \sigma_{43}^2 & \sigma_{44}^2$ |

More, Jorge, and Nagaraj Neelheer. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. 更多 SAS 资源，请访问 support.sas.com/publishing。

## 第 9 章 边缘模型的广义估计方程技术 297

| 描述 | TYPE=covariance-structure | 结构 | 示例 |
| --- | --- | --- | --- |
| | CHOL | 指定一个通过其 Cholesky 根参数化的无结构协方差矩阵。这种参数化确保了生成的协方差矩阵至少是半正定的。如果对角线值不零，则它是正定的。GLIMMIX 过程限制 Cholesky 根的对角元素为正。这保证了当矩阵正定时时有唯一解。通常，建议使用 Cholesky 根参数化而非完全无结构的协方差矩阵（TYPE=UN）。如果 A 是正定矩阵，其 Cholesky 根是一个下三角矩阵 C，使得 $CCᵀ=A$。CHOL(q) 选项决定了对角线下方建模的带带数量。C 下三角部分中高于 "q" 条带的元素被设置为零。如果你考虑生成的协方差矩阵 $A=CC'$，则阶参数的作用是将所有距离对角线至少 "q" 个位置的非对角元素置零。记住，Cholesky 分解在计算上略为复杂。 | | |

## 9.5 二项分布/二分类响应的示例

在本节中，我们将利用第 4.9 节讨论的关于指骨骨化的畸形学示例，说明 GEE 用于二项分布或二分类（Bernoulli）结果的情况。回顾实验的目的是研究苯妥英酸（PHT）和三氯苯醚（TCPO）的协同效应，且指骨骨化的存在与否被视为 2×2 因子设计，其中 PHT 和 TCPO 为两个因子。

PHT 的水平为 60 mg/kg 和 0 mg/kg，TCPO 的水平为 100 mg/kg 和 0 mg/kg。骨化数据可以在表 4.6 中找到。我们首先使用独立工作相关矩阵获得 GEE 估计。程序 9.2 提供了使用对数连接函数和独立工作相关矩阵对畸形学数据拟合 GEE 模型的编程语句。在 DATA 步骤中，数据被重新编排，以便我们使用 `CLASS` 语句并指定带有交互作用的因子模型。`REPEATED` 语句请求 GEE 估计并将窝窝识别传递给 SAS。结果摘要提供在输出 9.2 中。

### 程序 9.2：使用独立相关矩阵对骨化数据拟合 GEE 模型

```
Fitting a GEE Model with Independent Correlation Matrix to the Ossification Data
```

if (condVar > someVal) {console.log("xxx")}

```
输出 9.2: 续接

*** 骨化数据 -- 使用可交换工作相关矩阵的 GENMOD 进行 GEE***

| | | | |
|---|---|---|---|
| GENMOD 过程 | | | |
| 可交换工作相关性 | | | |
| 相关性 | 0.2950399396 | | |
| GEE 参数估计的分析 | | | |
| 经验标准误差估计 | | | |
| 参数 | 估计值 | 标准误差 | 95% 置信限 | Z | Pr >|Z| |
| 截距 | 0.7360 | 0.2521 | 0.2420 | 1.2300 | 2.92 | 0.0035 |
| TCPO | 0 | -0.7557 | 0.4170 | -1.5731 | 0.0061 | -1.81 | 0.0700 |
| PHT | 0 | -1.9786 | 0.3558 | -2.6760 | -1.2812 | -5.56 | <.0001 |
| TCPO*PHT | 0 | 1.0408 | 0.7567 | -0.4423 | 2.5238 | 1.38 | 0.1690 |

表 9.1 显示了对应两种工作相关结构的 GEE 结果，以及在 Beta-二项分布和随机聚类二项分布下获得的估计值。GEE 与准似然似然（Quasi-likelihood）的相似之处在于，这两种方法都不基于似然函数。虽然准似然通过比例因子调整标准误差，但 GEE 标准误差是通过方差协方差矩阵的夹明治估计器得到的。对于读者来说，使用类似于第 3 章中提供的代码获取这些数据集的准似然估计值将很有启发性，而且基于似然的模型与 GEE 有显著不同。最后，需要注意的是，虽然我们可以对基于似然的模型执行第 5 章描述的拟合性检验，但我们不能以相同的方式检验 GEE 模型的有效性。

# 第 9 章 边缘模型广义估计方程技术

表 9.1: 四种不同模型下全因子设计骨化数据的 Beta 估计值和标准误差

| | | 带相关性的 GEE | 带有可交换相关性的 GEE | Beta-二项 | 随机聚类二项 |
|---|---|---|---|---|---|---|---|---|
| 参数 | 估计值 | 标准误差 | 估计值 | 标准误差 | 估计值 | 标准误差 | 估计值 | 标准误差 |
| 截距 | 0.8323 | 0.2472 | 0.7360 | 0.2521 | 0.7043 | 0.2341 | 0.6392 | 0.2266 |
| TCPO | -0.8481 | 0.4063 | -0.7557 | 0.4170 | -0.7822 | -0.4017 | -0.0457 | 0.3711 |
| PHT | -2.1094 | 0.3434 | -1.9876 | 0.3558 | -1.6917 | -0.4018 | -0.5129 | 0.3956 |
| TCPO + PHT | 1.0453 | 0.7628 | 1.0408 | 0.7567 | 0.6770 | 0.6902 | 0.6162 | 0.6678 |
| 过离散度 | | | 0.2950 | 0.3374 | 0.0541 | 0.3400 | 0.0486 |
*PHT: 苯妥类; TCPO: 三氯丙酮

## 9.6 癫痫发作计数示例

Thall 和 Vail (1990) 分析了一项研究癫痫药物疗效的临床试验数据。患有部分或复杂癫痫发作的患者被随机分配接受苯妥类或安慰剂。在为期八周的导入期内，记录了癫痫发作次数并作为基线。在导入期结束时进行随机化，尽管每个患者“交叉”到了另一组，随后是为期八周的治疗期，$Y_{ij}$ 表示主体 $i$ 在 $j=1, 2,...,5$ 时的发作次数。注意 $j=1$ 代表基线，$j \geq 2$ 代表治疗期。那么，带有时间偏移的对数模型拟合
$E(Y_{ij}) = \beta_0 + \beta_1 X_{i1} + \beta_2 X_{i2} + \beta_3 X_{i1} X_{i2} + \ln(t_{ij})$
其中 $X_{it} = \begin{cases} 1 & \text{治疗期} \\ 2 & \text{基线} \end{cases}$

具有可交换工作相关性的 GEE 模型结果可参见 GENMOD 文档。具有随机效应和复合方差协方差矩阵的 GEE 模型结果可参见 GLIMMIX 文档。程序 9.3 显示了读取数据并创建偏移变量，然后使用 GLIMMIX 程序拟合前述 GEE 的语句。

### 程序 S: 使用复合对称性的边缘 GEE Poisson 模型拟合发作数据

```sas
/*
Thall and Vail (1990) 示例
使用随机效应的边缘 GEE 模型
可参见 GLIMMIX 文档。
*/
data seizures;
  array c(5);
  input id dt c1-c5;
  do i=1 to 5;
    xl = (i > 1);
    ltime = (i-1)*log(8) + (i ne 1)*log(2);
    cnt = c(i);
  end;
  output;
  keep id cnt xl ltime;
datalines;
101 1 36 11 14 9 8
```
