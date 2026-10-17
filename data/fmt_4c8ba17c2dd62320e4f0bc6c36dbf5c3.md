
其中 `$p_{COMPLY4}$` 表示根据协变量 (`EXER0`, `VIT0`, `D1`) 进行逻辑回归得到的 `COMPLY4=1` 的预测概率。参见 10.4.2 关于基线 (`VIT0`) 和随访 (`VIT4`)，它们是残差平方根方差为 `$\sigma_{0,4,8}$` 的连续正态分布（其中 `g =` 恒等函数）。在 GLMs 的特定项中，所有模型都包含了基线协变量的主效应。

### 10.4.4 SAS PROC NLP

`PROC NLP` 过程提供了一套强大的工具，用于最小化或最大化非线性函数。回顾 Property (18) 完整的似然函数是 `f_s` 和 `f_t` 的函数。在这种参数化中，`$\theta$` 包含了 `$\beta, \eta, \lambda$` 和 `$\sigma$`。在这种参数化中，`PROC NLP` 特别适用于此应用，因为似然函数是 `$\theta$` 的非线性函数。在这里我们演示如何使用 NLP 来找到最大似然函数的 `$\theta$` 值。

具体而言，参数向量 `$\lambda$` 出现在 `f_s` 的部分中。此外，我们通过将数据输入到 SAS 来确保它们被加载：

```
libname lib 'My Documents';

proc data=lib.weight;

var subject exer0 vit0 d1 comply4 d2 comply8 d3;

run;
```

我们在这里显示前 12 行数据。结局是 `VIT16`。`DIET`、`EXER0` 和 `VIT0` 是基线修饰因子；`D1` 是基线到第 4 周的体重变化；`D2` 是第 4 周到第 8 周的体重变化；`D3` 是第 8 周到第 12 周的体重变化。

244 使用 SAS 进行观察性健康分析

### 输出 10.1 SAS NLP 数据

| Obs | subject | VIT0 | D1 | comply | VIT4 | D2 | VIT8 | VIT16 |
|---|---|---|---|---|---|---|---|---|
| 1 | 0 | 75.00 | -7.40 | 0 | 75.00 | -4.00 | 80.00 |
| 2 | 1 | 60.00 | -12.4 | 1 | 90.00 | -6.40 | 65.00 |
| 3 | 0 | 80.00 | -42.0 | 0 | 80.00 | -34.00 | 87.92 |
| 4 | 1 | 53.33 | -12.4 | 1 | 50.00 | 20.20 | 65.00 |
| 5 | 1 | 65.79 | -6.85 | 0 | 52.65 | -4.97 | 83.38 |
| 6 | 0 | 70.00 | -6.00 | 1 | 90.00 | -0.20 | 93.00 |
| 7 | 1 | 55.00 | -11.6 | 0 | 80.00 | -52.00 | 75.00 |
| 8 | 1 | 70.00 | -16.6 | 1 | 90.00 | -1.20 | 100.00 |
| 9 | 0 | 55.00 | -4.00 | 1 | 50.00 | -5.00 | 75.00 |
| 10 | 0 | 55.00 | -13.2 | 1 | 55.00 | -6.80 | 80.00 |
| 11 | 0 | 70.00 | -10.0 | 1 | 90.00 | -7.40 | 100.00 |
| 12 | 0 | 45.00 | -18.0 | 1 | 69.53 | -3.27 | 0 | 84.75 |

## 第10章 结构化嵌套模型

```
TITLE "MLE of the Weight Data Using PROC NLP -- &sysdate;"

ods output "Resulting Parameters"=lib.NLPEstimates;

ods output "Covariances"=lib.NLProbestvarcov;
```

接下来，我们调用 NLP 并使用 `DATA=` 选项指定数据集名称：

```sas
PROC NLP data=lib.all_weight_data vardef=n covariance=1 pcov;
```

在这里，我们还通过 `VARDEF=` 和 `COVARIANCE=` 选项指定了计算的标准误差类型。SAS NLP 使用 ML 理论的渐近结果（例如 Vaart, 1998 中的第 5.5 节）来计算 `$\theta$` 的所谓根（或三明治）方方差矩阵的估计值，我们将其记为 `$\delta(\theta)$`。通过指定 `$\Delta(\theta)$` 的对角线元素可以获取 `$\Delta(\theta)$`。ODS 语句插入 `PROC NLP` 以在输出中打印方差矩阵。如前所述，之前显示的 `ODS OUTPUT` 语句允许我们将 `$\Delta(\theta)$` 获取为 SAS 数据集，供后续计算。在第 10.4.4 节中，方差矩阵被用于计算估计参数特定线性组合的标准误差（从而计算置信区间）。

下一个语句指定了要执行的数值优化。在我们的案例中，我们感兴趣的是执行极大似然估计（ML）；因此，我们指示 `PROC NLP` 最大化 `loglik`，我们在后续编程语句中为 `PROC NLP` 定义了它：

```sas
MAX loglik;
```

下一个语句需要 `PARMS` 语句。`PARMS` 语句识别要估计的参数，并为数值优化程序设置初始值。在写出似然函数的编程语句后，设置 `PARMS` 语句会更容易。`PARMS` 语句的语法（出于空间考虑在此进行了简写）如下：

```sas
PARMS sig2=17.18,sig2vit4=15.99,sig2vit8=11.96,sig2vit0=18.23,beta0=65.44,......;
```

我们数据分析的完整 `PARMS` 语句见附录 10.b。

接下来的 `BOUNDS` 语句用于指定参数约束。在我们的分析中，我们将根方差限制为正数；如下：

```sas
BOUNDS sig2>1e-12,sig2vit0>1e-12,sig2vit4>1e-12,sig2vit8>1e-12;
```

`loglik` 中的参数没有任何约束。

接下来，我们转向用于设置待最大化对数似然编程语句。目标是定义 `loglik`。请记住，对数似然是给定过去信息的分布者 `f`'s 分布的函数，也是给定过去信息 `f_6` 的 `VIT16` 分布的函数，其中包含了我们感兴趣的主要 SNMM（结构化嵌套混合模型）。出于教学目的和调试的考虑，我们发现使用多个编程语句来设置似然函数比在一行代码中写出整个似然函数更好。`PROC NLP` 允许在 `BOUNDS` 语句之后执行此操作。

## 使用 SAS 进行观察性医疗分析

首先，我们计算对应于基线干扰条件函数的对数似然部分；此外，我们还计算了将用于 SNMM 条件似然的 `f_0`'s 的相关部分。这里展示了 `DIET`（饮食）二元基线调节变量的代码：

```sas
dietline1=gammall0; /* 仅截距逻辑回归模型 *
dietp=exp(dietline1)/(1+exp(dietline1));/* 使用反逻辑变换的概率 *
diet=diet*dietp+(1-diet)*dietp;/* 用于 DIET 的伯尔努利似然*
diet-diet=dietp;/* 用于 VIT16 的 SNMM 的残差 */
```

残差 `$\delta_{DIET}$` 在第 10.3.2 节的 `DIET` 属性 (19) 中推导出，用于详细说明函数的参数化模型。为了保持一致性，我们对唯一参数 `$\gamma_{10}$`（`DIET=1` 的几几比）应用反逻辑变换来计算 `DIET=1` 的概率，但我们也可以使用 `PROC NLP` 直接估计概率 `dietp`。其他方法也有效，但如果你想直接计算 `dietp`，应确保在 `BOUNDS` 语句中包含 `dietp`。我们对二分类基线调节变量 `EXER0` 使用了类似的代码（见附录 10.B）。

对于连续调节变量 `VIT0`，代码要简单得多。一行代码就创建了用于 `VIT16` SNMM 的残差 `$\delta_{VIT0}$` [参见属性 (19)]。同样，我们使用了仅截距的模型，因为基线调节变量 `VIT0` 之前没有历史：

```sas
dv0=VIT0-(gamm3_0); /* 用于 VIT16 SNMM 的残差 */
```

接下来，我们计算对应于基线后干扰条件函数的对数似然部分；`f_1`'s。这里展示了 `COMPLY4`（从性）第四周二元调节变量的代码：

```sas
compl41=gamma2_0 + gamma21_1*DIET + gamma2_2*EXER0 +
gamma21_3*D1; /* 对数模型 */
compl4=exp(compl41)/(1+exp(compl41));/* 概率 *
compl4p=exp(compl41)*(1-compl4p);/* 用于伯尔努利似然 */
dcompl=compl4-compl4;/* 用于 VIT16 SNMM 的残差 */
```

残差 `$\delta_{COMPLY4}$` 在属性 (19) 中推导出。用于 `COMPLY4` 逻辑回归的协变量——即 `EXER0` 和 `D1`——取决于初始模型选择（第 10.4 节和附录 10.A）。初始模型选择建议从 `COMPLY4` 的逻辑回归中移除 `VIT0`。对于第四周的连续调节变量 `VIT4`，我们仅使用以下编程语句创建结果 `$\delta_{COMPLY4}$`：

```sas
dvit4=VIT4-(gamma23_0 + gamma23_1*VIT0 + gamma23_2*D1 +
gamma23_3*VIT0);
```

再次，这里最终模型中的协变量根据初始模型选择（10.4.1 和附录 10.A）。对于第八周的二分类或连续调节变量使用类似的代码。编程语句的倒数第二步是计算条件平均（即 SNMM），以及用于 `VIT16` 条件分布（`DIET`, `EXER8`, `VIT8`）的对数似函数的残差，`f_t`：

```sas
snmmVIT16-beta0 + etal_res4*DIET + etal_res5*EXER0
+ etal_res6*VIT0*dvito
+ beta10_D1*D1
+ beta4_D1*DIET + beta5_D1*EXER0 +
+ beta6_D1
+ etal_res21*COMP4 + etal_res22*EXER4
+ etal_res23*VIT4
+ beta20_D2 + beta21_D2*COMP4 +
+ beta22_D2*EXER2 +
+ beta33_D3*VIT4 +
+ etal_res31*COMP8 + etal_res32*EXER8 +
+ etal_res33*VIT8
+ beta30_D3 + beta31_D3*COMP8 +
+ beta32_D3*EXER8 +
+ beta33_D3*VIT4
+ epsilon16-snmmVIT16;
```

对象 `snmmVIT16` 正是属性 (19)，我们感兴趣的 SNMM。感兴趣的参数——即 `$\mu_s$`——标记为 `beta`。最后一步是编写完整的对数似然（参见属性 [18]）。在三个点中，我们有两个调节变量和一个连续调节变量。因此，完整的对数似然是随时间变化的调节变量给定过去 `VIT16` 条件布的函数。如 10.3.3 所示，我们假设所有变量均为正态分布：

```sas
loglik = log(fdiet) [DIET] / bernoulli
+ log(fexer0) [EXER0] / bernoulli
+ log(sig2) - (dvito/(2*sig2)) [VIT0] / normal
+ log(fcomp4) [COMP4] / bernoulli
+ log(fexer4) [EXER4] / bernoulli
+ log(sig2) - (dvit4/(2*sig2)) [VIT4] / normal
+ log(fcomp8) [COMP8] / bernilli
+ log(fexer8) [EXER8] / bernoulli
+ log(sig2) - (epsilon/(2*sig2)) [VIT6] / normal;
```
