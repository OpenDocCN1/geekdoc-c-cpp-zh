
logit[g(h_{ij}, y_{ij})] = logit [pr(D_i = j|D_i \geqslant j, y_{ij})] = h_{ij} \psi + \omega y_{ij} \(7.3.11)

$i = 1, \dots, N$。当 $\omega$ 等于零时，假设的脱落模型为 MAR（随机缺失），所有参数都可以使用 SAS 轻松估计，因为我们用于线性混合模型的测量模型以及假设服从逻辑回归的脱落模型可以被分别拟合。如果 $\omega \neq 0$，则假设的脱落过程为 MNAR（非随机缺失）。模型 (7.3.11) 为脱落过程 $f(d_{il}|y_{ip}, \psi)$ 提供了构建模块。作为一个告示，我们不应忽视事实：脱落机制的真实性质无法仅根据观测数据来确定（Molenbergh et al., 2008），这表明需要进行敏感性分析。

Rubin (1976) 以及 Little and Rubin (2014) 证明，在 MAR 和温和的正则条件下（参数 $\theta$ 和 $\Psi$ 在功能上独立），当忽略缺失数据机制时，基于似然和贝叶斯的推断是有效的（参见 Verbecke and Molenberghs, 2000）。从实践上说，感兴趣的似然基于因子 $f(Y|O)$。这被称为可忽略性（ignorability）。我们将在 7.5 节和 7.6 节中详细讨论这一点。

实际意义是，具有似然估计功能和处理不完全观测受试者能力的软件模块可以处理正确的似然函数，提供有效的参数估计和似然比值。这里有几点提示。首先，当科学关注的某部分指向无响应过程时，显然两个过程都需要被考虑。尽管如此，在 MAR 下，两个过程可以分别建模并估计参数。其次，似然推断通常与采样分布的引用相关（例如，用于精密度估计量和统计假设检验；Kenwood and Molenberghs, 1998）。然而，实际意义是，当基于观测信息而非期望信息矩阵，且在参数假设正确的情况下，标准误差和相关检验是有效的。第三，可能很难完全排除 MNAR 机制的作用。这一点在引言中已经提到，将在 7.9–10 节中进一步讨论。第四，当即使存在谎言（例如在最后一次机会两个治疗组之间的比较中）时，完整的纵向分析也是必要的。在后一种情况下，拟合模型可以作为最后一次机会推断的依据。一种常见的批评是需要考虑一个模型。然而，需要注意的是，在许多临床试验设置中，重复测量是平衡的，即对所有受试者考虑了一组共同的（通常是有限的）测量时间，这允许先验指定一个饱和模型（例如，针对固定效应的全组别与时间交互作用模型，以及非结构化的协方差矩阵）。这种可忽略的线性混合模型规格说明由 Mallinckcrodt et al. (2001ab) 给出。

## 7.3.4 广义估计方程

概述 有时被提到的全似然方法的两个问题是它们涉及的计算复杂性以及对模型假设的敏感性。当我们主要感兴趣一阶边缘均值参数和两对关联参数（即二阶矩）时，全似然程序可以用准似然方法代替（McCullagh and Nelder, 1989）。在准似然中，均值响应被表示为协变量的参数函数；方差被假设为均值的函数，可能取决于未知的尺度参数。Wedderburn (1974) 首次指出似然理论和准似然理论对于指数族是一致的，并为任何广义线性模型提供回归参数的一致估计，即使链接函数和方差函数的选择不对应指数族。

对于聚类和重复数据，Liang and Zeger (1986) 提出了所谓的广义估计方程（GEE 或 GEE1），它们只需要对我们愿意采用的单变量边缘分布进行正确的指定，而对关联结构仅做出“工作”假设。它们估计与个人二元响应向量期望值相关的参数，并对关联结构表述工作性假设。该方法将回归参数的估计方程与基于矩的相关性参数估计相结合。

Prentice (1988) 将其结果扩展到允许对概率和两对相关性进行联合估计。Lipschitz, Laird and Harrington (1991) 修改了 Prentice (1988) 的估计方程，允许通过几率而非边缘相关性对关联建模。采用 GEE1 时，我们不使用关联结构的信息估计主效应参数。结果显示，即使关联结构误设定，GEE1 也能产生一致的主效应估计量。然而，严重的误设定会严重影响 GEE1 估计量的效率。此外，当科学兴趣放在关联参数上，应避免使用 GEE1。

包含边缘关联的这些估计方程的二阶扩展（GEE2）已由 Liang, Zeger and Taqish (1992) 研究。他们指出，GEE2 几乎是完全有效的，尽管在关联结构误设定时，主效应参数的估计可能会出现偏差。

Carey, Zeger and Diggle (1993) 提出了所谓的交替逻辑回归（ALR），适用于对数链接的重复二元数据，并使用几率对关联建模。虽然 Molenberghs and Verbeke (2005) 也允许关联建模，但它们的计算比 GEE2 更简单。

## 方法论细节

在对 GEE 方法进行简要概述后，现在将进一步解释 GEE 方法论。我们首先回顾在对边缘正态模型 $Y_i \sim N(X_i, V_i)$ 下计算极大似然估计时使用的得分方程：

```
$\sum_{i=1}^N X_i(A_i^{1/2} R_i A_i^{1/2})^{-1}(y_i - X_i\beta) = 0\quad (7.3.12)
```

其中边缘协方差矩阵 $V_i$ 被分解为形式 $V_i = A_i^{1/2} R_i A_i^{1/2}$，$A_i$ 是对角矩阵；主对角线元素为边缘方差；$R_i$ 等于边缘相关矩阵。其次，

在边际广义线性模型（marginal generalized linear model）计算极大似然估计时，假设单位内的响应是相互独立的（即忽略重复测量结构），其得分方程如下：

```
$$\sum_{i=1}^N \frac{\partial \mu_i}{\partial \beta}(A_i^{1/2}R_{ii}^{1/2})^{-1}(y_i - \mu_i) = 0. \quad (7.3.13)$$
```

注意，(7.3.12)的形式与(7.3.13)相同，但考虑了重复测量之间的相关性。对(7.3.13)进行考虑相关结构的直接扩展为：

```
$S(\beta) = \sum_{i=1}^N \frac{\partial \mu_i}{\partial \beta}(A_i^{1/2}R_{ii}^{1/2})^{-1}(y_i - \mu_i) = 0, \quad (7.3.14)$
```

该方程通过将单位矩阵 $I_{ni}$ 替换为相关矩阵 $R_i = R_i(\alpha)$ 得到，通常被称为*工作相关矩阵*（working correlation matrix）。通常，边际协方差矩阵 $V_i = A_i^{1/2}R_iA_i^{1/2}$ 包含一个未知参数向量 $\alpha$——导致 $V_i(\beta, \alpha) = A_i^{1/2}(\beta)R_i(\alpha)A_i^{1/2}(\beta)$——在实践中用一个一致估计量进行替换。

假设边际均值 $\mu_i$ 已正确设定为 $h(\mu_i) = X_i$，可以证明在较的正则条件下，通过求解(7.3.14)得到的估计量 $\hat{\beta}$ 渐近从正态分布，均值为 $\beta$，协方差矩阵为：

```
$I_0^{-1}I_1^{-1}, \quad (7.3.15)$
```

其中

```
$I_0 = (\sum_{t=1}^N \frac{\partial \mu_t}{\partial \beta}\frac{\partial \mu_t}{\partial \beta}^T), \quad I_1 = (\sum_{t=1}^N \frac{\partial \mu_t}{\partial \beta}^T V_t^{-1}Var(y_t)V_t^{-1}\frac{\partial \mu_t}{\partial \beta})$
```

在实践中，(7.3.15)中的 $Var(y_i)$ 被替换为 $(y_i - \mu_i)(y_i - \mu_i)^T$，在均值再次被正确设定的唯一条件下，它是无偏的。

注意，现在只要假设关于一阶矩的模型假设是正确的，就可以对均值结构获得有效的推断。同样注意，尽管源于似然法，但(7.3.14)中的GEE方程不能解释为对应于数据向量 $y_i$ 的某个全似然的得分方程。

Liang 和 Zeger (1986) 针对工作相关提出了基于矩的估计。为此，首先定义离差：

```
$e_{ij} = \frac{y_{ij} - \mu_{ij}}{\sqrt{v(\mu_{ij})}}$
```

并按上述方式稍显复杂地分解方差：

```
$V_i = \phi A_i^{1/2} R_i^{1/2},$
```

其中 $\phi$ 是过度离散参数。

工作相关的一些常用选择包括：Corr($Y_{ip}$ $Y_{ik}$) = $0, j \neq k$；可交换性（Corr($Y_{ip}$ $Y_{ik}$) = $\alpha, j \neq k$）；AR(1)（Corr($Y_{ip}$ $Y_{it+t}$) = $\gamma, t=0,1,...,n_i-j$）；以及无结构性（Corr($Y_{ip}$ $Y_{ik}$) = $\alpha_{jk}, j \neq k$）。通常使用基于矩的估计方法来估计这些参数，作为集成迭代估计程序的一部分（Aerts, Geiger, Molberghs, and Ryan, 2002）。过度离散参数也以类似的方法获得。基于 Liang 和 Zeger (1986) 拟合 GEE 的标准迭代程序如下：

(1) 使用单变量 GLM（即假设独立性）计算 $\beta$ 的初始估计；
(2) 计算估计方程所需的量，如均值和方差；
(3) 计算 Pearson 离差 $e_{ij}$；
(4) 计算 $\alpha$ 的估计；
(5) 计算 $R_i(\alpha)$；
(6) 计算 $\phi$ 的估计；
(7) 计算 $V_i(\beta, \alpha) = \phi A_i^{1/2} R_i(\alpha) A_i^{1/2}$；
(8) 更新 $\beta$ 的估计：

```
$\beta^{(t+1)} = \beta^{(t)} - \left[ \sum_{i=1}^N \frac{\partial \mu_i}{\partial \beta} V_i^{-1} \frac{\partial \mu_i}{\partial \beta} \right] \left[ \sum_{i=1}^N \frac{\partial \mu_i}{\partial \beta} V_i^{-1} (y_i - \mu_i) \right].
```

步骤 (2)–(8) 迭代直到收敛。

在 SAS 中，有三个过程可以用于 GEE。首先是 `GENMOD` 过程。在基本形式下，它对单变量数据拟合广义线性。添加 `REPEATED` 语句，可以分析重复测量，可以使用相关结构。从 SAS 9.4 开始，可以使用 `GEE`。它与 `GENMOD` 基本等同，但其主要吸引在于加权 GEE，参见 7.7 节。如前所述，也可以使用 `GLIMMIX` 过程，提供了随机效应。

## 7.4 简单方法与 MCAR

我们将简要回顾一些仍在广泛使用的相对简单的方法。对于许多方法，需要 MCAR，而对于像 LOCF（最后观测终结）的方法，条件则不同。

### 7.4.1 完整案例分析

完整案例分析仅包含所有计划观测值的样本。这种方法有明显的缺点。首先，总是丢失大量信息。此外，当缺失机制为 MAR 而非 MCAR 时，可能会产生偏差。

### 完整案例分析与 SAS

执行完整案例分析的唯一步骤是删除未获得所有测量样本。当数据按“水平”组织时（即每个样本一条记录），这异常容易。对于“垂直”组织的数据需要稍多数据处理，可以使用下文讨论的 SAS 宏。

例如，对于年龄相关退行性试验，运行下一个语句产生完整案例数据集，用于连续结果（diff 是正确读取的字母与基线之间的差）：

# 程序 7.1 为完整案例分析准备数据（连续结果）

```
cc(data=armd155,id=subject,time=time,response=diff,out=arm)
```

以及用于二元结果（bindif 是 diff 的离散化，非负值为 1，否则为 0）。参见程序 7.2。

# 程序 7.2 为完整案例分析准备数据（离散结果）

```
cc(data=armd111,id=subject,time=time,response=bindif,out=a)
```

显然，`cc` 宏需要四个参数。`data` 是待分析的数据。如果没有指定，则使用最近的数据集。`id` 指定数据集中包含标识变量的名称，`time=` 指定样本内部的顺序。结果变量通过 `response=` 参数传递，`out` 定义宏创建的输出数据集名称。

## 程序 7.3 完整案例分析（连续性结局）

```sas
proc mixed data=armdcc2 method=ml;

title CC - 连续 ;

class time treat subject;

model diff = time*time / noint solution ddfm=kr;

repeated time time / subject=subject type=un;

run;
```

相比之下，如果将形式如 (7.7.28) 的 GEE 应用于完成完成者（completers），则可以使用以下代码进行标准 GEE。
请参见程序 7.4。

## 程序 7.4 完整案例分析（二分类结局，GEE, PROC GENMOD）

```sas
proc genmod data=armdcc;

title CC - GEE ;

class time treat subject;

model bindiiff = time*time / noint dist=binomial;

repeated subject=subject / withinsubject=time type=exch

run;
```

或者参见程序 7.5。

## 程序 7.5 完整案例分析（二分类结局，GEE, PROC GEE）

```sas
proc gee data=armdcc;

title CC - GEE ;

class time treat subject;

model bindiiff = time*time / noint dist=binomial;

repeated subject=subject / withinsubject=time type=exch

run;
```

此外，对于基于线性化的 GEE 版本，并带有经验修正的标准标准误，我们可以使用程序

## 7.6.

## 程序 7.6 完整案例分析（二分类结局，GEE, 线性化版本，PROC GLIMMIX）

```sas
proc glimmix data=armdcc empirical;

title CC - GEE - 线性化版本 - 经验 ;

loptions maxaxiter=50 technique=newrap;

class time treat subject;

model bindiif = time treat*time / noint solution dist=binary

random _residual_ / subject=subject type=cs;

run;
```

对于广义线性混合模型 (7.5.17)，使用数值积分时，以下代码非常有用。程序 7.7。

## 程序 7.7 完整案例分析（二分类结局，GLMM, PROC GLIMMIX）

```sas
proc glimmix data=armdcc method=gauss(q=20);

title CC - 混合 - 积分 ;

loptions maxaxiter=50 technique=newrap;

class time treat subject;

model bindiif = time treat*time / noint solution dist=binary

random intercept / subject=subject type=un gcororr;

run;
```

使用 NLMIXED，我们可以使用程序 7.8。

## 程序 7.8 完整案例分析（二分类结局，GLMM, PROC NLMIXED）

```sas
data help;

set armdcc;

time1=0; if time=1 then time1=1;

time2=0; if time=2 then time2=1;

time3=0; if time=3 then time3=1;

time4=0; if time=4 then time4=1;

run;

proc nlmixed data=help qpoints=20 maxiter=100 technique=new

title CC - 混合 - 数值积分 ;

eta = betall*timel beta2*time2 beta3*time3 beta4*time4

b (beta21*timel beta22*time2 beta23*time3 beta24*time4)

*(2-treat);

p = exp(tau)/(1 exp(tau));

model bindif binary(p);

rand b normal(0,tau) subject=subject;

estimate tau 2 tau*tau;

run;
```
