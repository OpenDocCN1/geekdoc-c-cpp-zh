
测试。在试验阶段，研究人员可能感兴趣于比较在功率消耗函数中使用具有不同 $\rho$ 值的设计，例如 0.3、0.9 或 1.5。图形化比较成为此项调查中ر项重要工具。

## 示例代码 2.10 使用功率消耗函数的高级乳腺癌试验

```
proc segdesign boundaryscale=stdz.plots=all;
rhodesignforcan: design nstages=4 method=errfuncpow(rho=0.3) alt=upper
stop-reject alpha=0.025 beta=0.1;
rhodesignforcan: design nstages=4 method=errfuncpow(rho=0.9) alt=upper
stop-reject alpha=0.025 beta=0.1;
rhodesignforcan: design nstages=4 method=errfuncpow(rho=1.5) alt=upper
stop-reject alpha=0.025 beta=0.1;
samplesize model=twamplesvival(nulledsurvtime=6 mesurvtime=8.25
actime=12 totaltime=24);
```

在这些三阶段设计中，使用了标准化的 $\chi$-统计量 (boundaryscale=stdz)。在 `samplesize` 语句中，我们使用了 `model=2twamplesvival` 来测试两条生存曲线，假设原分布中的中位生存时间为 6 个月，在备择分布中为 8.25 个月。这是基于指数生存分布假设。入组时间设定为 12 个月，总时间为 24 个月。

图 2.12 对应示例代码 2.10

![](img/f4ec2665c3484c528370923aeb5cb99f_119_0.png)

| 设计信息 | 数值 |
|---|---|
| n 边界标尺 | 标准化 Z |
| 备择假设 | 上界 |
| 提前停止 | 拒绝原假设 |
| 方法 | 误差搜索 |
| 边界键 | 均 |
| 备择参考 | 0.31845 |
| 阶段数 | 4 |
| Alpha | 0.025 |
| Beta | 0.1 |
| 功率 | 0.9 |
| 最大信息（固定样本量的百分比） | 131.9095 |
| 最大信息 | 136.6710 |
| 原假设参考 ASD（固定样本量的百分比） | 129.9934 |
| 备择参考 ASD（固定样本量的百分比） | 72.39965 |

| 阶段 | D(Group1) | D(Group2) | D(Group3) | N(Group1) | N(Group2) | N(Group3) | 事件（事件和样本量） | 时间 | 时间 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | 138.67 | 59.99 | 76.55 | 7945.43 | 121.66 | 121.66 | 34187.5 | 138.67 | 50.61 | 77.44 | 445.22 | 222.92 | 222.92 | 34.531 |
| 2 | 273.34 | 121.95 | 151.38 | 11994.63 | 331.58 | 331.58 | 68535.27 | 227.22 | 123.74 | 153.48 | 168.77 | 334.39 | 334.39 | 33.934 |
| 3 | 410.01 | 182.33 | 231.23 | 15225.65 | 557.39 | 557.39 | 334.39 | 428.85 | 195.95 | 228.16 | 268.52 | 334.39 | 334.39 | 107.2 |
| 4 | 546.59 | 242.57 | 298.13 | 20168.40 | 734.39 | 734.39 | 137548.57 | 546.57 | 289.13 | 308.68 | 334.39 | 334.39 | 138.7 |

图 2.12 示例代码 2.10 输出的部分内容仅显示了使用 $\rho = 0.3$ 的第一个设计 `rhignforcan`。膨胀因子为 131.9%，但在指定的备择参考下，它为 72.4%。曲妥单珠（组 2：原分布）所需的事件数列在 D(G2) 下，联合治疗组（组 1：备择分布）列在 D(Grp1) 下，最后一列为相应的所需的分阶段信息。团队可以在观察到总共 138 个事件（对应 34.5 的信息）后进行中期分析。根据默认入组率和指定的入组时间及总时间（accrual=12 和 totaltime=24），第一阶段需要 446 名受试者。中期分析所需的历时间为 8、12、17 和 24 个月，基于提供的入组信息。SAS 两种入组模型：均匀分布 (accrual=uniform) 和参数截断指数分布 (accrual=exp)，用于计算样本量和历时间。如果研究认为这些入组模型不适用于他们的情况，他们将指定自己的入组模型以估计所需的样本量和历时间。因此，如果 SAS 程序中未提供入组信息，则仅显示事件数，而不会显示样本量和历时间。中期分析仍需遵循事件数。

我们还请求所有图以将三个停止边界合并进行视觉比较。图 2.13 使用 3 种消耗函数的乳腺癌边界图和图 2.14 使用 3 种消耗函数的乳腺癌平均大小图，作为示例，分别显示 ASN 图。我们可以看到，$\rho = 0.3$ 的第一个设计在第一阶段对于有效性是激进的，而另外两个 ($\rho = 0.9, 1.5$) 在早期阶段是保守的。除非强烈认为两条曲线在早期阶段发散，否则在该试验开始时保守地停止更为理想。

然而，重要的是，在目前讨论的边界示例中，假设无效边界是无法越过的。也就是说，如果统计量越过边界，试验必须终止，否则 I 类错误率会膨胀。这被称为“绑定边界”。在计算有效性边界时，无效边界的存在会拉低有效性边界，从而在期分析忽略绑定无效边界时更容易越界，即可能膨胀 I 类错误。这种绑定无效通常对试验发起不利，因为无效决策并不总是明确。因此，有一种方法可以构建非绑定无效边界，非绑定边界允许在越界边界时继续试验，尽管与绑定无效边界相比这增加了总样本量。在这种情况下，为了更改默认设置 `stop-both (binding)`，可以选择 `stop-both (nonbinding)` 来构建非绑定无效边界。特殊问题，我们将回到监控问题，并简要介绍除绑定和非绑定无效边界外的监控工具。

## 图 2.13 使用 3 种消耗函数的乳腺癌边界图

![](img/f4ec2665c3484c528370923aeb5cb99f_122_0.png)

## 图 2.14 使用 3 种消耗函数的乳腺癌平均大小图

![](img/f4ec2665c3484c528370923_123_0.png)

## 示例：2 型糖尿病心血管风险的序贯试验设计

在评估 T2DM 心血管风险时，有很多开发选择；我们将关注限制在心血管结局试验 (CVOT)，以进一步说明用于组序设计的方法。评估 T2DM 心血管风险的各种方法的优点在别处讨论 [26, 27]。如所述，对于第一阶段，我们可以将非劣效原假设重写为 $H_{10}: \theta \le 0$，其中 $\theta = -\ln(\Delta_T / \lambda_C) + 0.5878$ 且 $\ln(1.8) = 0.5878$。备择假设变为 $H_{11}: \theta > 0$。这是 SAS 中优选的参数化，代码 2.11 2 型糖尿病心血管结局试验序贯分析用于说明此示例。

## 示例代码 2.11 2 型糖尿病心血管结局试验序贯分析

```
 第一阶段测试的固定设计，默认=0.1 *
proc seqdesign;
stagefixed: design stages=1 alt=twosided alpha=0.05;
samplesize model=twamplesvival(nullhazard=1.8 1.0 hazard=1.0);
run;

* 用于第一阶段测试 1.8 标准的三阶段序贯设计 /
* proc seqdesign errspend nstages=3 method=errfuncpow boundaryscale=mle plots=all;
stagedpower: design errspend=errfuncpow(rho=0.3) alt=twosided
alpha=0.05 cum(0.5 0.75 1)
samplesize model=twamplesvival(nullhazard=1.8 hazard=1.0)
ods Output=test_interim;
run;
```

```
* 第一阶段数据分析 /
proc ph data=T2DM;
model weeks*event(0)=treatment;
ods output ParameterEstimates=parms_interim;
run;
```

```
data params_interim;
set parms_interim;
where parameter='Treatment'; nparameter=parameter+0.5878;
scale='MLE'; nstage_1;
keep Scale_stage_1 parameter estimate stddr;
run;
```

```
proc seqtest boundary=test_interim parms(testvar=treatment)=parms_interim
foadjn=non-boundary scale=mle
ods Output=test_inter2;
```

```
* 第一阶段结束时的 1.3 标准期分析（20% 信息）
以及第二阶段在 50% 和 75% 时的中期分析 /
proc seqdesign errspend zctopp boundaryscale=mle plots=all;
stagedpower: design errspend=errfuncpow(rho=0.3) alt=twosided
alpha=0.05 cum(0.2 0.75 1)
samplesize model=twamplesvival(nullhazard=1.3 hazard=1.0)
ods Output=combtest_interim;
run;
```
