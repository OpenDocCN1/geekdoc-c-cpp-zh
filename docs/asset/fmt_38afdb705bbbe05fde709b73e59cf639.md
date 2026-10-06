
其中 $N$ 是考试次数，$y$ 代表产生 $t$ 的所有可能的响应模式，$p(y|\theta)$ 是给定能力 $\theta$ 和项目参数估计的响应模式概率，$g(\theta)$ 是分布的密度。每个总分的期望频率基于联合后验分布的的模型值，$\chi^2$ 差异量是数据和模型参数的函数。

## 项目级指标

评估拟合的一种直观指标是每个项目响应每个类别的考试次数。与测试分分布类似，观测与后验预测项目分布之间的差异可以使用每个项目的卡方检验来总结：$\chi^2=\sum(O_{ik}-E_{ik})^2/E_{ik}$，其中 $O_{ik}$ 是项目 $j$ 类别 $k$ 的观测考试次数，$E_{ik}$ 是预测的考试次数。通过对所有 $N$ 次考试中项目 $j$ 类别 $k$ 的概率可以计算 $E_{ik}$：$E_{ik}=\sum p(y|\theta)$。这种 $\chi^2$ 指标被证明在使用 PPC 方法时有效（例如，Levy et al., 2009; Zhu & Stone, 2011）。与测试级指标类似，$\chi^2$ 指标依赖于数据和模型参数。

项目得分是测试分与特定项目之间的相关性。虽然这种指标不是经典的统计量，但已被证明对贝叶斯 IRT 模型分析是有效的。例如，Sinaray 等人 (2006) 发现这种差异量可以检测由 2PL 或 3PL 模型生成的 IRT 模型的设定错误。Zhu 和 Stone (2011) 显示该指标也适用于检测局部依赖性。

之前讨论的经典项目统计量，如 Yen 的 $Q_0$，也可以作为 PPC 的差异量来评估 IRT 模型拟合。这些统计量通过比较不同特质 $(\theta)$ 水平的分布扩展了项目得分分布的分析。例如，Yen 的 $Q_0$ 统计量是一种皮尔逊卡方检验，定义为：$\chi^2=\sum_{jk}(O_{ijk}-E_{ijk})^2/E_{ijk}$，其中 $O_{ijk}$ 是项目 $j$ 类别 $k$ 的观测考试次数，$E_{ijk}$ 是基于 IRT 模型和项目参数估计的预测考试次数。在 Yen 的统计量中，考试根据 $\theta$ 排序后被分为大小相等的子组。子组响应类别的期望频率是子组人数乘以在该类别中的响应概率。

最近，研究了这些不同指标在 PPC 方法中的性能（例如，Sinclair, 2006; Zhu & Stone, 2011）。在这些研究考虑的条件下，项目拟合统计量被发现可以检测 IRT 模型形式引起的不拟合，但在由于多维性或局部依赖引起的不拟合方面无效。

## 两对指标

传统上，IRT 模型底层的维度和局部独立假设使用反映项目响应之间关联的两对指标进行评估。例如，局部依赖统计量如 Yen 的 $Q_3$ 和优势值比 ($OR$) 都是两对指标的示例。

Yen 的 $Q_3$ 统计量在考虑潜在变量 $\theta$ 后测量项目对之间的相关性（Yen, 1991）。对于 $j$ 和 $j'$，$Q_3$ 定义为 $r(d_j, d_{j'})$，其中 $d$ 是项目 $j$ 上期望与观测响应之间的差异。Yen 的 $Q_3$ 可用于二分类或分类项目。作为 PPC 的差异量，以往的研究发现 $Q_3$ 在检测多维性和局部依赖方面比两对指标更有效力（例如，Lee et al., 2009; Sinclair et al., 2006; Zhu & Stone, 2011）。

Chen 和 Th (1997) 使用优势值比 ($OR$) 来评估二分类项目的局部依赖性。对于二分类项目 $j$ 和 $j'$，$OR$ 从 $2 \times 2$ 表 $n_{pq11}/n_{pq00}$ 计算，其中 $n_{pq}$ 是在项目 $j$ 上观察到 $p$ 或 1 以及在项目 $j'$ 上观察到 $q$ 或 0 的人数。如果不满足局部依赖性，$OR$ 将大于多维 IRT 模型下的预期值。$OR$ 被证明在 PPC 背景下检查不拟合的几个方面是有效的；与 Yen 的 $Q_3$ 相比，使用 $OR$ 作为差异量是因为 $OR$ 的计算依赖于数据和模型参数，而 $Q_3$ 的计算是

与得分项目不同，分类项目可以计算多个优势值，因为列联表是 $R \times C$ ($R, C \ge 2$)。一种方法是计算全局优势值比（Agresti, 2002）。对于任意两个项目，通过对每个项目的类别将 $R \times C$ 列联表简化为 $2 \times 2$ 列联表。全局优势值比被定义为 $2 \times 2$ 表的交叉比。例如，对于具有5 个类别的项目，可以将类别 3 和 4 视为*正确*响应，将类别 0、1 和 2 视为错误响应。因此，5 分类简化为 $2 \times 2$ 表。Zhu 和 Stone (2011) 发现全局优势值比是评估 GR 模型拟合的有效差异量。

## 个人拟合指标

贝叶斯框架产生的个人拟合统计量可以使用 PPC 方法。以往的研究检查了多种个人拟合统计量在 PPC 方法中的性能，结果表明在贝叶斯框架下某些统计量优于其他。最流行的个人拟合指标之一是 $l_z$ 统计量（Drasgow, Levine, & Williams, 1985），它定义为 $l_z = (l_z - E(l_z)) /\sqrt{Var(l_z)}$，其中 $l_z$ 是被试者响应模式的对数似然，$E(l_z)$ 表示二分类得分项目的 $l_z$ 期望值，$Var(l_z)$ 表示其方差。

```
$l_0 = \sum_{j=1}^{Y} \{Y_j \log[P_j(\theta)] + (1 - Y_j) \log[1 - P_j(\theta)]\}$
```

# 第 8 章：IRT 模型的贝叶斯模型检查

$Y_j$ 是项目 $j$ 的响应，$P_j(\theta)$ 是能力水平为 $\theta$ 的受试者正确回答的概率。$E(l_0)$ 和 $Var(l_0)$ 通过以下公式计算：

```
E(l_0) = \sum_{j=1}^{J} P_j(\theta)\log P_j(\theta) + [1 - P_j(\theta)]\log[1 - P_j(\theta)]
```

```
Var(l_0) = \sum_{j=1}^{J} P_j(\theta)[1 - P_j(\theta)] [log\frac{P_j(\theta)}{1-P_j(\theta)}]^2
```

## 模型拟合度评估

将观测数据计算出的差异统计量，与基于后验分布参数值在每个复制数据集中计算出的相同测量进行比较。如果模型拟合数据，则从观测数据计算出的差异应与从复制或模拟数据计算出的相同测量相似。因此，差异在贝叶斯统计中起着类似于假设检验的作用。

如所述，这种比较通常通过图形显示来呈现。例如，可以绘制 $T(\theta)$ 的直方图，并在直方图中绘制 $T(\theta)$。如果 $T(\theta)$ 接近直方图的中间区域，我们认为模型拟合良好。还可以计算预测概率值（PPP）来量化 $T(\theta)$ 在参考分布中的出现情况，其中接近 0 或 1 的 PPP 值（通常 < 0.05 或 PPP > 0.95）表明数据拟合不佳（Gelman et al., 2014）。

在经典模型拟合的假设检验中，考虑使用卡方统计量 ($\chi^2$）作为差异测量，其中期望值基于模型参数的采样值。通过计算后验分布的第 $r$ 次迭代（$\delta_r$）的测量，可以获得测量的经验采样分布。因此，通过 $R$ 次复制，获得一个经验分布 $\chi^2 (rep_r, \delta_r)$。例如，如果使用 $R=1000$ 个样本，则在 $1000$ 个 $\chi^2 (rep_r, \delta_r)$ 统计量下计算零假设的经验采样分布：

```
\chi^2 (rep_1, \delta_1),
\chi^2 (rep_2, \delta_2),
...
\chi^2 (rep_{1000}, \delta_{1000})
```

可以使用模型参数的点估计值来计算观测测量，或者通过使用来自后验分布的采样值在观测数据上计算测量来将其纳入。通过直接计算每对观测差异统计量与预测差异统计量 $\chi^2 (rep_r, \delta_r)$，可以使用 PPP 值来量化观测测量的似然概率。接近 1 的 PPP 值表示拟合良好，而接近 0 的 PPP 值则表明拟合不佳。本章的示例提供了同时使用图形显示和 PPP 来评估模型拟合度的方法。

## PPMC 应用示例

本节介绍示例，说明了在 IRT 模型中使用不同差异测量实现 PPMC 方法。我们继续使用 LSAT 数据评估二分 IRT 模型的拟合情况，并使用 DASH 数据评估多项模型的拟合情况。假设在运行本节中的程序之前，后验预测数据集已经完成了模拟。由于空间限制，仅使用了上述差异测量的子集，但本章的重点是进行 PPMC 分析。对图表感兴趣的读者应查阅 SAS GTL 文档。

### 示例 1：观测与预测分数分布——LSAT 数据

使用总分分布作为差异测量，评估了 IP 模型对 LSAT 数据的整体拟合情况。总分分布包含了跨测试中每个总分的人数频率。该分析是使用程序 8.4 的，该程序包含了用于比较观测和预测响应分布的 SAS 代码。从程序 8.4 可以看出，首先计算了观测数据（LSAT 数据）中每位受试者的总分 ①，并使用 `PROC FREQ` 过程观察了测试分数的频率。观测频率保存在 SAS 数据集 `OBS_DIST` 中 ②。然后对每个预测数据集计算相同的差异测量（总分），以获得预测响应的测试分数频率分布，并保存在 SAS 数据集 `ALL_PREDICT` 中 ③汇总结果（频率）使用宏 `TS` 保存 ④。使用 `PROC UNIVARIATE` 计算每个测试值预测频率的第 5、10、50、90 和 95 百分位数。这些分位数保存在 SAS 数据集 `PRED_PCTS` 中 ⑤。

为了比较观测和预测的测试分数分布，可以检查观测数据的频率分布以及预测响应的频率分布的第 5、50 和 95 百分位数，并将它们与 SAS 数据集 `OBS_PRED` ⑱ 合并，或使用 `SERIESPLOT` 语句和 SAS GTL 命令进行绘图。

你应该注意，后验预测数据集的格式是通过使用 `PROC MCMC` 中的 Format 2 生成的——即具有 NSIM 行预测（500行），每行包含 LSAT 数据集中所有观测值（1000个）的预测响应。为了使用带有 BY 语句的 `PROC FREQ`，必须将此数据集转换为 Format 1，以便后验预测集中的观测数量为 $1000 \times 500$。此任务通过程序 8.4 中的宏 `TS` 完成 ⑗。或者，可以使用程序 8.2 直接创建 Format 1 的后验预测数据集。

## 程序 8.4：观测与预测测试分数分布——1P 模型

```
* 控制变量 */
%let nperson=1000;      /*人数*/
%let nitem=5;            /*项目数*/

/* 获取观测分布中的差异测量 */
data ts_obs;
set lsat;
array x(nitem);
tts=sum(of x);
run;
proc freq data=ts_obs;
tables ts /=out_dist;
run;

/* 获取复制数据中的差异测量 */
%macro ts
data ts_pred;
set lsat_pred;
samplen;
%do i=1 to &nperson;
tts=0;
%do j=1 to &nitem;
tts=x(j).&i;
%end
&i=;
output;
%end
keep ts sample;
run;
%mend;
tts;

/* 计算预测差异的分布 */
proc freq data=ts_pred noprint;
tables ts /=out_all_preddist; by sample;
run;
/* 计算每个测试分数的频率 */
proc sort data=all_preddist; by ts sample; run;
proc univariate data=all_preddist noprint;
var count;
by ts;
out output=pred_pcts pctlpre= 5 10 90 95;
run;
```

输出 8.1 显示了使用 SAS GTL 绘制测试分数观测频率后，程序 8.4 的结果，图中包含了基于复制数据的总分 5、50 和 95 百分位数。我们可以看到，观测分布（实线）落在测试分数 5% 到 95% 后验预测分布之间，或者在测试分布的 98% 置信区间内。观测分数分布也与第 50 分布（虚线）非常接近。

首先计算，1P 模型在测试分数分布的所有水平上使用了 LSAT 数据。根据这种差异测量，没有证据表明拟合不佳。这可以与第 7 章中 LSAT 数据的模型比较结果进行比较。回顾第 7 章中“二分项目模型比较（LSAT 数据）”部分，1P、2P 和 3P 模型使用项目级和测试级的 CPO 统计量以及 DIC 统计量进行了比较。项目级和测试级 CPO 统计量表明，在 DIC 结果指示 2P 的地方，1P 模型更优。

## 218 使用 SAS 对项目反应模型进行贝叶斯分析

更倾向于该模型。使用总分作为差异度量得到的 PPMC 分析结果，与项目级和测试级 CPO  统计量所建议的偏优模型（1P PMC 模型）更为一致。

## 输出 8.1：观测与预测测试分分布的比较 – 1PL 模型

![](img/dd5368102e19084dcd107a02a82ba37c_233_0.png)

输出 8.1 比较了关于整个总分分布的观测分布和预测分布。你也可以使用汇总统计量（如数据的平均值、中位数标准差）来比较这些分布。程序 8.5 将 PPMC 分析扩展到，将测试分数的观测平均值和标准差与预测值的相同指标进行比较，同样使用了 LSAT 数据和 1PL 模型。这里使用的差异度量是总分的平均值和标准差，它们仅依赖于数据。请注意，这是基于 SAS 文档中为 `PROC MCMC` 提供的示例。

与程序 8.4 一样，程序 8.5 的第一步是根据观测和预测响应数据计算观测和预测测试分数。你应该注意，TS 与程序 8.4 中的宏 TS 不同。接下来，使用 `PROC means` 过程获取 1000 个观测测试分数的平均值和标准差。使用 `CALL SYNTAX` 语句输出图形。计算每个预测数据集（1000 个）测试分数的平均值和标准差。因此，存在观测数据的观测平均值和标准差，以及针对复制数据的 PPMC 标准差经验分布。

为了获得 PPMC 值，将这些预测值和观测值与观测值进行比较。如果预测平均值（或 SD）大于观测平均值（或 SD），则计数变量 COUNT、MEAN（以及 COUNT SD）加 1。PPMC 值等于计数变量的值除以预测响应数据集的数量（在本例中为 500 个）。换句话说，平均值度量的 PPC 值是预测平均值大于观测平均分数的比例所占的比例。可以打印观测和预测数据的平均值、标准差以及 PPMC 值。或者，也可以像输出 8.2 那样，使用 SAS GTL 命令和 `HISTOGRAM` 语句对这些结果进行图形比较。（参见 SAS Press 作者网页上程序 8.5 中的 GTL 命令。）

## 程序 8.5：观测与预测测试分数统计量的比较—1PL 模型

```sas
/* 控制变量 */
let nperson=1000;      /*人数*/
let nitem=5;            /*项目数*/

/* 获取观测数据集的测试分数 */
data data_obs;
  set lsat;
  array x(&nitem) ts=sum(x);
run;

/* 获取复制数据中的差异度量 */
%macro ts;
data ts_pred;
  set dir_lsat_pred;
  array ts(&nperson) tsl-ts&nperson;
  do i=1 to &nperson
    ts[i]=0;
    do j=1 to &nitem
      ts[i]=ts[i] + x[j];
    end
  end;
  output; keep tsl-ts&nperson;
run;
%end
%ts;

/* 计算观测数据测试分数的平均值 & 标准差 */
proc means data=data_obs noprint;
  var ts; output out=stat mean=mean stddev=sd;
run;
data data_null;
  set stat; call syntax('mean',mean); call syntax('sd',sd);
run;

/* 计算每个预测数据的测试分数的平均值 & 标准差，
并与观测平均值和标准差进行比较以获得 p 值 */
data pred;
  set ts_pred;
  mean = mean(of ts); sd = std(of ts);
run;
data ppp;
  set pred end=eof nobs=;
  count_mean = (mean&mean); count_sd =(sd&sd);
  if not then do;
    ppp_mean = count_mean/nobs; call syntax('pmean',ppp_mean);
    ppp_sd = count_sd/nobs; call syntax('psd',ppp_sd);
  end;
run;
data summary;
  length type $15;
  set stat ppp2 ppp;
  if _n=1 then type='Obs Dist'; else if _n=2 then type='Rep Dist';
else if _n=3 then type='PPP Value';
  label mean='Mean' sd='Mean of SDS' ppp_mean='PPP Mean' ppp_sd='PPP SD';
  drop _type _freq_
run;
proc print data=summary; run;
```
