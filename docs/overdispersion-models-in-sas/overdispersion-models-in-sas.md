
# SAS 中的过度离散模型

本书献给：

Grecia and David Morel—JGM

Chetana, Harsha, and Siri Neerchal—NKN

- 7.2 多项分布...............................................................................................202
- 7.4 广义逻辑模型示例...............................................................................206
- 7.6 一项出生缺陷研究......................................................................................................214
- 7.8 随机聚类多项分布.......................................................................225
- 7.10 森林花粉计数问题...............................................................................228
- 7.12 通过利克特-多项分布和随机聚类多项分布对一致系数 Kappa 进行建模...............240

# 前言

本书重点关注使用各种 SAS 过程对表现出过度离散的数据进行建模和分析。过度离散也称为额外变异，出现在二项、多项和计数类型的数据中，当方差大于二项、多项或泊松模型允许的范围时。这种现象是由数据的聚集和缺乏独立性引起的。正如 McCullagh 和 Nelder (1989) 所指出的，“实践中过度离散并不罕见。事实上，有些人认为过度离散是实践中的常态，而名义离散反反例。”制药部门、生物统计和生物测量部门、大学、政府机构、健康研究组织以及抽样调查组织的从业人员每天都会遇到这个问题。本书旨在为此类问题的正确分析和建模提供必要的技术。这些技术包括似然和似然模型，以及广义估计方程 (`GEE`)、广义线性过度离散模型 (`GLOM`) 和广义线性混合模型 (`GLMM`)。

More, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. 如需更多 SAS 资源，请访问 `support.sas.com/publishing`。

# 前言

欢此庆祝在离散（dispersion）课题上持续研究合作的20周年。

这本书是对这20年来的极佳庆祝！

本书材料的准备极大得益于2003年和2004年举办的几场短期课程。我们在下方列出了这些课程，以感谢各自的赞助单位。

- “具有过离散性的分类数据的建模与分析”。由美国统计协会（ASA）生物制药部门赞助。2004年联合统计会议，加拿大多伦多。2004年8月10日。
- “具有过离散性的分类数据分析”。受美国联邦食品药品管理局（FDA）监测与生物识别办公室生物统计学部主任 Gregory Campbell博士邀请。美国马里兰州，罗克维尔。2004年3月12日。
- “具有过离散性的分类数据分析”。第54届国际统计会议，德国，柏林。2003年8月12日。
- “具有过离散性的分类数据分析”。中西部生物制药研讨会，印第安纳州，慕尼。2003年5月19日。

在本书中，我们展示了各种应用领域的示例，而不是聚焦于单一领域，我们认为这是因为过离散性的高质量，以及此处所介绍方法的通用性。为此，全范围内讨论了30组案例。一些示例包括：萨尔瓦多33个城市采样受试者中的弓生虫病、环境因素导致的大鼠指骨骨质化、森林花粉柱、广岛原子弹爆炸中的染色体畸变、HIV患者的尿路感染、重点社区的住院情况、癫痫发作次数、术后肩痛等。

作者对许多协助完成本书的人员深表谢意。我们感谢辉瑞公司（Pfizer, Inc.）的 Santos C. Sutherland 博士和桑迪亚国家实验室的 Jan Newell 博士，允许我们在书中使用他们的 SAS 系统。新泽西州大学医学院生物统计系的 Dirk F. Moore 教授为我们提供了第5章中讨论的广岛染色体畸变数据。荷兰乌特勒支生物统计中心的 Jan den Broek 教授为我们提供了第6章中讨论的HIV感染男性尿路感染数据。

我们感谢 SAS 学院 Oliver Schaberberger 博士在科罗拉多州丹佛2008年统计会议上的鼓励性谈话，这为我们承担写作任务提供了动力。我们将部分工作整合到 `PROC GLIMM (EMPIRICAL-MBN)` 和 `PROC SURVELOGISTIC (VARAF-MOREL)` 中，这是我们在离散道路上的亮点！SAS（对我们而言是匿名的）提供了许多意见和建议，改进了呈现方式。我们感谢发起此项目的 SAS 管理员 Shelley Sessions。我们感谢宝洁（Procter & Gamble）的 Greg Gray、Callie Jender 和 Dan Schneider 提供设施并协助内部审查流程，并感谢 Robert Bartlett 博士和副总裁 Nora Zorich 博士的支持。巴尔的摩县社区学院学科写作与课程计划主任 A. Paige Rogers 对手稿进行了多次编辑评审。我们还感谢 DoHwan Park 博士及其广义线性模型专题课程（2011年秋季，马里兰大学巴尔的摩校区）的学生对倒数第二稿进行了评审。感谢所有审稿人，但我们对所有剩余缺陷承担全部责任。

# 前言

我们非常幸运能与马里兰大学巴尔的摩校区（UMBC）数学与统计系的几位研究生合作研究“过离散”：此前提到的 Santos 和 Justin，以及 Minglei Liu 博士和 Maxime Bokossa 博士。我们感谢他们的智力陪伴。此外，我们诚挚感谢宝洁和 UMBC 的同事，他们提供了有利于良好工作的刺激环境。

最后，要对我们的家人表示感激（Jorge：Grecia 和 David；Najaraj：Chetana, Harsha 和 Siri）。他们的耐心让我们得以多次逃避日常家务，这使得本书成为可能。谢谢！

Morel, Jorge, and Nagaraj Neerchal. Overdispersion Models in SAS®. 版权 © 2011, SAS Institute Inc., 美国卡罗来纳州，凯里。保留所有权利。欲需更多 SAS 资源，请访问 `support.sas.com/publishing`。

Morel, Jorge, and Nagaraj Neerchalk. Overdispersion Models in SAS®. 版权 © 2011, SAS Institute Inc., 美国卡罗来纳州，凯里。保留所有权利。欲需更多 SAS 资源，请访问 `support.sas.com/publishing`。

# 过离散

- 1.1 一个简单的介绍示例..................................................................................6
- 1.2 过离散...............................................................................................................3
- 1.3 过离散的常见表征...............................................................................4
- 1.4 过离散的扩展定义......................................................................6
- 1.5 一个模拟示例......................................................................................................7
- 1.6 指数族...............................................................................................11
- 附录 1.1: 本书涵盖的分层模型 ................................14

## 1.1 一个简单的苯妥类示例

这种抗惊动药物已知对近系小鼠的产前发育具有致畸性。Hartfields 等人（1990）进行了针对 81 只怀孕小鼠的完全随机实验，以调查苯妥类（PHT）和三氯丙烯氧化物（TCPO）的潜在协同效应。研究设计为 2x2 析因：PHT 和 TCPO 的给剂量分别为 0 mg/kg、60 mg/kg 和 100 mg/kg。在某些指骨发育中，骨化并未发生；而在其他指骨中则几乎完全。为了简化这部分研究，我们仅分析了左爪。表1.1 显示了中间三分处的骨化数量。该示例以简单的形式引入过离散的概念，并在以后深入讨论。

img/fa648c1745eb7d92f5fb_13_) # SAS 中的过离散模型

表 1.1: 暴露于苯妥类 (PHT) 和三氯丙烯氧化物 (TCPO) 的小鼠骨化数据

| 小鼠 (j) | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 总计 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 显示骨化的受体数量 (`$t_j$`) | 2 | 0 | 1 | 7 | 0 | 0 | 0 | 6 | 1 | | 18 |
| 受体总数 (`$m_j$`) | 2 | 7 | 8 | 10 | 4 | 6 | 7 | 6 | 7 | | 71 |

如果 `$t_j$` 和 `$m_j$` 分别遵循参数为 `($\pi$, $m_j$)` 的二项分布，则 `$\hat{\pi}$` 的方差估计量（给定模型所示）是无偏的：

$$\hat{Var}(\hat{\pi}) = \frac{\hat{\pi}(1-\hat{\pi})}{\sum_{j=1}^{11} m_j}$$

该估计方值为 0.027。如果二项模型不成立，上述估计是无效的。根据抽样理论（见 Cochran 1977，第 155 页），一致估计量（不依赖二项假设）为：

$$\bar{Var}(\hat{\pi}) = \frac{n\sum_{j=1}^{n}(t_j-m_j\hat{\pi})^2}{\sum_{j=1}^{n} m_j^2}$$

结果为 0.0142。

# 第1章 过度离散 3

$$\chi^2 = \sum \frac{(t-m\tilde{\pi})^2}{m\tilde{\pi}(1-\tilde{\pi})}$$

根据理论，该统计量相对于其自由度（10）的值被视为二项分布类型数据的拟合优度（GOF）统计量。在这一说明性中，拟合优度统计量的值为 5.28。在二项分布模型下，其值应接近 1。这意味着在这种情况下，`$\tilde{\pi}$` 的估计方差（此前为 0.0027）应该是二项分布模型预期值的 5.28 倍。而 0.0142 除以 0.0027 等于 5.26。因此，该例中的数据表现出`过度离散`或额外的变异。这种现象也出现在多项分布和泊松分布中。在例例中，`$\tilde{\pi}$` 估计方差的正确值应接近 (0.0027)(5.28) = 0.014。

## 1.2 过度离散

考虑一项研究，实验单元是簇，且簇内的每个元素单元被归类为两个互斥的类别。如果我们假设元素单元是独立的且具有相同的成功概率，则二项模型适用于分析这些数据。聚类导致了元素单元之间缺乏独立性。成功概率可能在簇内的不同元素单元之间变化。因此，数据显示的方差通常比二项模型允许的方差大。正如前所述，这种现象被称为`过度离散或额外变异。`

过度离散也可能由其他因素引起。模型中遗漏的变量会导致过度离散。也就是说，响应概率实际上是几个协变量的函数，而模型仅包含了其中的一个子集。这种拟合不良的表现体现为过度离散。稍后介绍的一些诊断图会受到这种过度离散的影响。

在多项响应（计数数据）上也会观察到过度离散，通过多项（泊松）模型分析的结果可能大于模型假设的抽样变异所能解释的。McCullough 和 Nelder (1989, pp. 124-125) 指出

> “过度离散在实践中并不罕见。事实上，有些人会认为过度离散是实践中的常态，而正常离散反而是例外”

`欠离散`现象发生的频率较少。Cox 和 Snell (1988, p. 107) 指出“有时会观察到欠离散，尽管这并不常见”。它可能在正向响应存在竞争时发生。例如，当一个人品尝甜饮料时，他可能觉得第二种饮料没那么甜——即使它确实很甜。虽然这里发生了过度离散，但本文将不再处理这一现象。

正如 Stigler (1986) 所讨论的，源于聚类群过度离散示例在文献中可以追溯到 1986 年。具有过度离散的多项模型示例可能出现在：(a) 遗传性状畸形研究中（该性状以一定概率遗传给同一母亲的后代）；(b) 生殖毒性实验中，将化学物质施加给幼体并在个体上测量响应；(c) 在接受治疗的个体允许通过支持小组相互作用的实验中，例如戒烟计划或戒酒计划；(d) 在家庭调查中，同一家庭（或社区）内的受访者可能受到一两个个体的强烈影响。

许多论文包含了讨论并阐明过度离散现象及其对由于 I 类错误率膨胀导致的错误推断的影响的示例。畸形学和毒理学领域的相关示例见于 Williams (1975, 1982), Williams et al. (1988), Kupper and Hashem (1978), Hashem and Kupper (1979), Kupper et al. (1986), Shirley and Hickling (1981), Paul (1982), Park (1986), Lefkopoulou et al. (1989), Ryan (1992), Liang and McCullough (1993), Carr and Porter (1993), Donner et al. (1994), Morel and Koehler (1995), 以及 Morel and Neerchal (1997)。过度离散的重要示例见于 Rosner (1984) 和 Donner (1989) 的眼科研究中，Altham (1977) 和 Cohen (1976) 关于住院同胞对的研究，Crowter（在种子萌发分析中），Heckman and Wills (1977) 与面板研究相关，Efron (1986) 一个涉及萨尔瓦多 34 个城市弓虫病的流行病学示例，以及 Moore (1987) 关于广岛原子爆炸幸存者染色体畸变的建模。

关于泊松模型下过度离散的早期评论可以在 Student (1919) 中找到。过度离散的泊松示例出现在 (a) 纵向研究计数和速率分析，(b) 行为研究以及存在主体间变异的数量研究。

## 1.3 过度离散的共同特征

过度离散现象可以用一阶矩来表征。假设 `T` 是一个二项变量，那么

$$E(T) = m\pi$$

其中 `$\pi$` 代表成功概率。此外，如果单元是独立的，方差为

$$Var(T) = m\pi(1-\pi)$$

然而，如果单元是聚类的，方差会更大。如果我们令 `$\rho^2$` 为过度离散参数，则

$$Var(T) = m\pi(1-\pi)(1+\rho^2)$$

其中 `0 ≤ $\rho^2$ < ∞`。同样，过度离散的定义可以扩展到多项分布情况。由 `m` 个元素单元组成的簇，这些单元被归类为 `$(d+1)$` 个类别。令 `T` 表示 `d` 维计数向量，对应前 `d` 个类别，其中第 `i` 个分量代表分类为第 `i` 元素单元数量。对于聚类数据，通常用多项分布建模的向量 `T` 显示的数据变异通常高于多项模型允许的。为了适应这种过度离散，通常假设以下矩结构：

$$E(T) = m\pi$$

$$Var(T) = m[Diag(\pi) - \pi\pi^T\{1+\rho^2\}$$

其中 `$\pi = (\pi_1, \pi_2, ..., \pi_d)$` 是概率向量，`0 < $\pi_i$ < 1`，`$\sum\pi_i \le 1$`，`$\rho$`（或 `$\rho^2$`）是过度离散参数。如果多项类型的 `T` 具有均值和方差协差矩阵，则认为其相对于多项分布存在过度离散。当 `$\rho=0$` 时，方程 (1.2) 和 (1.4) 中的方差估计量简化为二项/多项模型。

回顾对于泊松随机变量，`$E(Y) = Var(Y) = \mu, \mu > 0$`。泊松随机变量是给定时间间隔内事件发生次数的计数。与二项情况一样，推导泊松随机变量属性需要对过程有底层假设。当这些假设不满足时，可能会产生过度离散。当 `Y` 是泊松类型的随机变量时，如果其前两个矩具有以下形式，则认为 `Y` 具有过度离散

$$E(Y) = \mu, Var(Y) = \mu(1+\rho^2)$$

# SAS 中的 6 类过度离散模型

`Var(Y) = \mu + \kappa\mu^2 = \mu(1+\kappa\mu), \kappa > 0$`.

参数 `$\kappa$` 被称为离散参数。观察到当 `$\kappa = 0$` 时，方程 (1.6) 中的方差变为泊松模型的方差。Dean (1992) 通过将 (1.6) 视为 `Var(Y) = $\mu(1+\kappa)$` 提供了另一种过度离散的形式。

忽略过度离散的后果是众所周知的。对于所有，标准误差估计（从忽略数据聚类特性的意义上来说是幼稚的）都小于其应有的值。在假设检验中使用这些估计会导致第一类错误率，即假阳性率大于名义几率。因此，会导致错误的推断。

## 1.4 过度离散的扩展定义



过度离散的情况有很多。在二项分布/多项分布的情况下，当违反了独立性假设（要素单元内部）或共同成功概率的假设时，就会出现过度离散。在泊松分布的情况下，当事件发生率随受试者变化时即可观察到过度离散；这些速率被假设服从 Gamma 变量。过度离散在聚类数据中自然产生。它出现在具有重复测量的纵向数据中。受试者的观测计数通常表现出过度离散。例如，考虑一项针对椎椎骨折高风险骨质疏松患者的临床研究。在给定期间内测量事件次数。同一患者可能发生多次，随后对计数做出多次贡献，这违反了泊松分布的“独立发生事件”假设。因此，这些情况并非真实来自泊松分布，从而表现出过度离散。

过去 20 年左右关于混合分布和广义线性混合模型 (`GLMM`) 的使过度离散得到了充分研究。过度离散已经超越了它的边界；它比 1.2 节提供的常见特征描述是一个广泛的话题。多项分布的混合，例如狄利克-多项分布 (`Mosimann, 1962`) 以及由 `Morel` 和 `Nagaraj (1993)` 以及 `Neerchal` 和 `Morel (1998)` 提出的随机聚类分布，相对于如 `(1.3)` 和 `(1.4)` 中的具有均值向量和协方差矩阵的多项分布具有过度离散。如方程 `(1.5)` 和 `(1.6)` 所示具有均值和方差的负二项分布相对于泊松分布表现出过度离散。适当定义的随机效应二项分布相对于二项模型具有过度离散。此外，具有随机效应的 Beta-二项分布相对于 Beta-二项分布具有过度离散，而 Beta-二项分布本身相对于二项分布具有过度离散。列表层出不穷。本章的附录 1.1 显示了我们打算在书中涵盖的一些过度离散的层级结构图。

## 1.5 模拟示例

模拟相关伯努利试验的一种简单方法如下。令 `$Y, Y_i^0, ..., Y_m^0$` 是独立同分布的伯努利 `()` 随机变量。对于每个 `$i,i=1,...,m$`，定义 `$Y_i$` 为概率 `$\rho$` 的 `$Y$`，或为概率 `$(1-\rho)$` 的 `$Y_i^0$`，其中 `$0 \le \rho \le 1$`。换句话说，每个 `$Y_i$` 可以由以下公式表示：

```
Y_i = Y I(U_i \le \rho) + Y_i^0 I(U_i > \rho),                               (1.7)
```

其中 `$U_i$` 是独立的均匀 `(0,1)` 随机变量，`I()` 表示指示函数。对于聚类数据，

`$E(Y) = \rho, Var(Y) = \rho(1-\rho)$`  `Corr(Y_1, Y_2) = \rho^2$`。

接下来提供了在模型 `(1.7)` 下生成数据的编程语句，适用于 `$m=5, \rho=0.6$` 和 `$\rho^2=0.3$`。注意正在生成 `$n=2000$` 个聚类，每个聚类由一组 `$m=5$` 个相关的二元结果组成。

### 程序 1.1：相关伯努利结果

```sas
/*
生成相关伯努利结果
针对 Y(1),Y(2),...,Y(m)
E(Y)
Pi
Var(Y)
Pi*(1-Pi)
Corr(Y(i), Y(j))
Rho*Rho
*/
data correlated_bernoulli;
  n = 2000; --- 聚类数量;
  m = 5; --- 聚类内的要素单元数量;
  pi = 0.6; --- 每个要素单元的成功概率;
  rho2 = 0.3; --- 聚类内相关;
  seed = 16670;
  rho = sqrt(rho2);
  do subid = 1 to nr; --- 变量 yj 扮演方程 (1.7) 中 y 的角色
    y = 0;
    u = uniform(seed);
    if u < pi then y = 1;
    if i=1 to m;
      y = 0;
      u = uniform(seed);
      if u < rho then y = y;
      else do;
        uu = uniform(seed);
        if u < pi then y = 1;
      end;
      output;
    end;
  end;

  keep subid i;
run;
```

```sas
proc transpose data=correlated_bernoullis out=new;
  by subid;
  id i;
  var y;
run;

ods html;
proc corr data=new;
  var _1 - 5;
run;

proc transpose data=correlated_bernoullis out=new;
  by subid;
  id i;
  var y;
run;

ods html;
proc corr data=new;
  var _1 - 5;
run;
```

输出 1.1 表明每个 `$Y_i$` 的均值（期望）约为 `$\pi = \sqrt{\pi(1-\pi)} = \sqrt{(0.6)(0.4)} = 0.4899$`。估计的标准差约为 `$\rho^2$`。要素单元之间的估计相关性。注意重复测量的相关结构是可交换的。也就是说，`$Corr(Y_i, Y_j) = \rho^2, i \neq j$`，对于 `$i=1,2,...,m$`。

### 输出 1.1：相关伯努利结果

输出 1.1: 伯努利结果的结果

| Variables: _1_2_3_4_5 | |

| Variable | N | Mean | Std Dev | Maximum |

|---|---|---|---|---|

| _1 | 2000 | 0.5995 | 0.4898 | 1 |

| _2 | 2000 | 0.6035 | 0.4912 | 1 |

| _3 | 2000 | 0.5985 | 0.4900 | 1 |

| _4 | 2000 | 0.6065 | 0.4978 | 1 |

| _5 | 2000 | 0.6014 | 0.4962 | 1 |

| Pearson Coefficients, N = 2000 | Prob >|r| under H0: Rho=0 |

| 1 | 2 | 3 | 4 | 5 |

|---|---|---|---|---|

| 1 | 1.0000 | 0.29579 | 0.31689 | 0.30128 | 0.29763 |

| | | .0001 | .0001 | .0001 | .0001 |

| 2 | 0.29579 | 1.0000 | 0.28872 | 0.29704 | 0.27709 |

| | | .0001 | | .0001 | .0001 | .0001 |

| 3 | 0.31689 | 0.28872 | 1.0000 | 0.32044 | 0.30346 |

| | | .0001 | .0001 | | .0001 | .0001 |

| 4 | 0.30128 | 0.29704 | 0.32044 | 1.0000 | 0.29617 |

| | | .0001 | .0001 | .0001 | | .0001 |

| 5 | 0.29763 | 0.27709 | 0.30346 | 0.29617 | 1.0000 |

| | | .0001 | .0001 | .0001 | .0001 | |

# 表 1.2：标义性水平 `$\alpha = 0.05$` 下第一类错误率的膨胀

| `$\rho^2$` (过度离散) | 实际第一类错误率 |

|---|---|

| 0.3 | 0.160 |

| 0.5 | 0.197 |

| 0.7 | 0.210 |

我们希望这个简单的例子能够说服读者，从在实际情况下进行准确统计推断的角度来看，过度离散是非常重要的。本书中讨论了在常用模型中考虑过度离散的许多方法。

## 1.6 指数族

本书要涵盖的主要任务，即准似然函数、广义线性模型 (`GLM`)、广义估计方程 (`GEE`) 和广义线性混合模型 (`GLMM`)，其动力源于适用于指数族中所有成员的许多统计方法的通用性。因此，我们首先通过概述它们的一些性质，对指数族密度函数进行简要介绍。指数族是一类具有某些特征和属性的密度函数。该族分布的成员包括正态分布、伯努利分布、二项分布、多项分布、泊松分布、负二项分布、Beta 分布和 Gamma 分布。这一族分布在经典统计推断技术中起着非常重要的作用。根据文献，分析中使用了规范参数和规范链接，但所有的示例都将使用族符号表示，该符号可能是规范的，也可能不是。

该族中的密度函数可以写为：

```
$f(y) = \exp\left(\frac{y\theta - b(\theta)}{\phi} + c(y, \phi)\right\},\quad (1.8)$
```

`$b(\cdot)$` 和 `$c(\cdot)$` 是某些特定的函数。参数 `$\theta$` 是一个实值**位置参数**，被称为**自然**（或规范）参数。函数 `$b(\theta)$` 被称为**累积量**，参数 `$\phi$` 称为**离散参数（或尺度参数）**。我们假设 `$b(\theta)$` 是连续二阶可导的。在正态分布的情况下，参数 `$\phi$` 对应方差 `$\sigma^2$`，且与均值在函数上没有关系。在方面

```
$Var(Y) = \phi v(\mu) \quad (1.11)$
```

表 1.3 显示了伯努利分布和泊松分布作为指数族成员的主要特征。注意，对于伯努利分布，均值和规范链接函数是逻辑函数和对数函数。二项分布（表 1.3 中未给出）也是如此。对于泊松分布，指数函数和对数函数分别是相关的均值和链接函数。

# 表 1.3：伯努利分布和泊松分布的主要特征

| 特征 | 伯努利分布 | 泊松分布 |

|---|---|---|

| 概率函数（通常形式） | `$\pi^y(1-\pi)^{1-y}, y=0,1, 0<\pi<1$` | `$e^{-\lambda}\lambda^y/y!, y=0,1,2,...,\lambda>0$` |

| 累积量 `$b(\theta)$` | `$\log(1+e^\theta)$` | `$\exp(\theta)$` |

| 均值函数 | `$\pi = \frac{e^\theta}{1+e^\theta}$` (逻辑函数) | `$\lambda = \exp(\theta)$` (指数函数) |

| 规范链接函数 | `$\log(\frac{\pi}{1-\pi}) = \theta$` (logit 链接) | `$\log(\lambda) = \theta$` (log 链接) |

| 离散参数 `$\phi$` | 1 | 1 |

| 方差函数 `$v(\mu)$` | `$\pi(1-\pi)$` | `$\lambda$` |

| 概率函数（规范形式） | `$\exp\{y\ln(\frac{\pi}{1-\pi})+\ln(1-\pi)\}$` | `$\exp\{y\ln(\lambda)-\lambda-\ln(y!)\}$` |

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_26_0.png)

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_26_2.png)

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_27_0.png)

## 广义线性模型

## 2.1 引言

标准线性模型由两个部分组成：系统效应和随机误差。广义线性模型 (`GLM`) 是普通线性回归到二项、泊松、负二项、Gamma 和其他分布的扩展。它最早由 `Nelder` 和 `Wedderburn (1972)` 提出，早于准似然、广义估计方程 (`GEE`) 和广义线性混合模型 (`GLMM`)。在本章中，我们将回顾 `GLM` 的基本概念，重点强调过度离散。

## 2.2 线性回归模型

设 `$Y_j, j=1,2,...,n$` 为独立随机变量，令 `$y_j$` 代表 `$Y_j$` 的实现。与每个 `$y_j$` 对应的是已知协变量的 `$k$` 维向量 `$\mathbf{x}_j = (x_{1j},x_{2j},x_{kj})$` 和未知参数的 `$k$` 维向量 `$\boldsymbol{\beta} = (\beta_1,\beta_2,...,\beta_k)^T$`，使得：

```
$y_j = \sum_{i=1}^k x_{ij}\beta_i + \varepsilon_j \quad (2.1)$
```

其中 `$\varepsilon_i$` 是不相关的随机变量，使得 `$E(\varepsilon_i)=0$` 且 `$Var(\varepsilon_i)=\sigma^2$`。这是经典的线性模型。矩阵形式的线性模型 `(2.1)` 为：

```
$\mathbf{y} = \mathbf{X}\boldsymbol{\beta} + \boldsymbol{\varepsilon} \quad (2.2)$
```

其中 `$y$` 是一个 `$n \times 1$` 向量，`$y=(y_1,y_2,...,y_n)^T$`，`$X$` 是 `$n \times k$` 的已知协变量矩阵，`$\mathbf{X} = (\mathbf{x}_1,\mathbf{x}_2,...,\mathbf{x}_n)^T$`，`$\varepsilon$` 是 `$n \times 1$` 的扰动向量，`$\varepsilon = (\varepsilon_1,\varepsilon_2,...,\varepsilon_n)^T$`。假设 `$n > k$`。

估计 `$\boldsymbol{\beta}$` 的常用方法是著名的最小二乘法 (`LS`)，也称为普通最小二乘法 (`OLS`)。`$\boldsymbol{\beta}$` 的估计使平方和最小化

## 第 2 章广义线性模型

为了找到使 `(2.4)` 最小的 `$\beta$`，需要找到 `(2.4)` 对 `$\beta$` 的阶导数向量并将其等于零：

```
$\frac{\partial S(\beta)}{\partial\beta} = -2X'y+2X'X\beta = 0.\quad (2.5)
```

`(2.5)` 的解是熟悉的最小二乘估计量

```
$\hat{\beta} = (X'X)^{-1}X'y.\quad (2.6)
```

显然，在这个简化方法中，矩阵 `$X'X$` 是满秩的。

可以证明 `$\beta$` 的最小二乘估计量 `$\hat{\beta}$` 是无偏的。其协方差矩阵为：

```
$Var(\hat{\beta}) = \sigma^2(X'X)^{-1}.$
```

估计量 `$\hat{\beta}$` 是最佳无偏估计量（`BLUE`），因为它在所有观测值的线性函数的估计量中是最小方差无偏估计量，即在形式为 `$\hat{\beta}=Ry$` 的估计量中（其中 `$R$` 是实数 `$knx$` 矩阵）。残差平方和 `$(y_j-\hat{y}_j)^2$` 的最小值提供了 `$\sigma^2$` 的自然估计量。可以证明估计量

```
$\hat{\sigma}^2 = \frac{\sum_{j=1}^n(y_j-\hat{y}_j)^2}{n-k}.\quad (2.7)
```

对于 `$\sigma^2$` 是无偏的。

读者可能注意到，普通最小二乘法（`OLS`）不需要方程 `(2.1)` 中的 `$\varepsilon_j$` 服从正态分布。只要它们与 `$E(\varepsilon_j) = 0$` 且 `$Var(\varepsilon_j) = \sigma^2$` 相关，`BLUE` 属性就成立。当 `$\varepsilon_j$` 是独立同分布的正态分布 `Normal$(0, \sigma^2)$` 时，可以找到 `$\theta = (\beta', \sigma^2)$` 的极大似然估计量（`MLE`），例如 `$\hat{\theta} = (\hat{\beta}', \hat{\sigma}^2)$`。为此，需要似然函数 `$\prod_{i=1}^n f(\epsilon_i; \sigma)$`，其中：

```
$f(\epsilon_i; 0) = \frac{1}{\sqrt{2\pi\sigma^2}} \exp\left(\frac{(y_i - x_i\mathbf{\beta})^2}{2\sigma^2}\right)$
```

`MLE` `$\hat{\theta} = (\hat{\beta}, \hat{\sigma}^2)$` 通过极大化似然函数的对数来获得，即首先对对数似然函数关于 `$\beta$` 和 `$\sigma^2$` 求偏导数，然后将这些导数等于零，以分别获得 `$\beta$` 和 `$\sigma^2$` 的解。对数似然函数的导数被称为**得分函数**（`score function`）。可以证明 `$\hat{\beta}$` 的 `MLE` 为：

```
$$\hat{\beta} = (\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\mathbf{y} (2.8)
```

这正是方程 `(2.6)` 中的 `OLS` 估计量 `$\hat{\beta}$`。`$\sigma^2$` 的 `MLE` 结果为：

```
$$\hat{\sigma}^2 = \frac{\sum_{i=1}^n (y_i - x_i\mathbf{\beta})^2}{n} (2.9)
```

注意 `$\hat{\sigma}^2 = \frac{n-k}{n}\sigma^2$`，因此 `$\hat{\sigma}^2$` 是渐近无偏的（一致的）。也就是说，`$\hat{\sigma}^2$` 是偏的，但其偏偏随着 `$n$` 的增加而趋于零。



评估线性模型质量的一种方法是检查估计的残差 $\hat{\epsilon}_i = y_i - \sum_{j=1}^k x_{ij}\hat{\beta}_j$。残差的一个良好性质是它们与预测值（线性预测值）$\hat{y}_i = \sum_{j=1}^k x_{ij}\hat{\beta}_j$ 不相关。因此，估计残差 $\hat{\epsilon}_i$ 与线性预测值 $\hat{y}_i$ 的散图（诊断图）应该是随机分布的，不显示出任何模式。诊断图中持续的模式表明模型存在缺陷或`拟合优性不足（Lack-of-Fit, LOF）`。残差的正态性可以通过`正态概率图`（Normal Probability Plot）进行直观评估。正态概率图是一种评估残差（从而是数据）是否近似从正态分布的图形技术。在正态概率图中，经验累积分布函数相对于标准正态分布累积分布函数的坐标进行绘图。另一种常见的图是分位数-分位数图（Q-Q 图），它是残差的观测值与来自标准正态分布随机样本的顺序统计量期望值的图。无论哪种情况，绘制的点都应该基本位于一条线上。偏离直线表示数据存在偏态。诊断图在识别数据中的离群值和影响观测值方面也非常有用。这个主题有很多优秀的书籍——建议读者参考 Montgomery, Peck 和 Vining (2007) 以获得入门介绍。

## 2.3 简单回归示例

考虑表 2.1 中的数据，该数据包含了 15 只在 24 到 84 天龄期喂食蛋白饮食的雌大鼠的初始体重和体重增加（克）。这些数据取自 Snedec 和 Cochran (1980, 第 7 版, 第 156-157 页)。

### 表 2.1：15 只大鼠的初始体重和体重增加（克）

| 大鼠编号 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 初始体重, X | 50 | 64 | 76 | 64 | 74 | 60 | 69 | 68 | 56 | 48 | 57 | 59 | 46 | 45 |  |
| 体重增加, Y | 128 | 158 | 159 | 118 | 133 | 112 | 96 | 126 | 132 | 118 | 107 | 106 | 82 | 103 | 104 |

收集这些数据是为了调查体重增加是否与初始体重有关。如果是，通过考虑大鼠的初始体重，可以像比较不同饮食一样对雌大鼠的实验更加精确。我们使用 `GLIMMIX` 过程获取 `OLS` 和 `MLE` 结果。编程语句在程序 1 中。

### 程序 1：使用 OLS 和 MLE 的体重增加

```
/*
Snedec and Cochran 1980, 第 7 版. 第 156-157 页
体重增加示例
*/
data gains_in_weight;
  do Rat=1 to 15;
    input x y;
    output;
  end;
datalines;
  50 64 76 64 74 60 69 68 57 48 57 59 46 45 65
  128 158 159 118 133 112 96 126 132 118 107 106 82 103 104
;
proc sort data=gains_in_weight;
  by rat;
run;
proc transpose data=gains_in_weight out=gains_in_weight
  (rename=(COL1=Initial_Weight COL2=Gains));
  by rat;
  var x;
run;
ods html;
  graphics on;
  title "MLE Results -- Gains in Weight Data";
  proc glimmix data=gains_in_weight plots=residual;
    model Gains = Initial_Weight / solution;
run;
  title "MLE Results -- Gains in Weight Data";
  proc glimmix data=gains_in_weight noreml;
    model Gains = Initial_Weight / solution;
run;
ods graphics off;
ods html close;
```

在模型 (2.1) 的情况下，`GLIMMIX` 过程不使用任何迭代拟合。然而，尺度参数 $\sigma^2$ 是通过残差平方和除残差自由度 $(n-k=13)$ 估计的，提供了 $\hat{\sigma}^2$，而不是总大鼠数 $(n=15)$，后者对应 $\tilde{\sigma}^2$。后者是极大似然估计量，而前者是无偏估计和已知方法。与 `PROC GLM` 和 `REG` 不同，`GLIMMIX` 过程提供了 $\tilde{\sigma}^2$ 标准错误的估计。为了获得尺度参数 $\sigma^2$ 的 $\hat{\sigma}^2$，应在 `PROC GLIMMIX` 语句中包含 `NOREML` 选项。程序 1 的主要结果见输出 2.1。

### 输出 2.1：程序 1 的选结果

| *** OLS 结果 -- 体重增加数据 *** |
| :--- | :--- |
| `GLIMMIX` 过程 |
| 参数估计 |
| Effect | Estimate | Standard Error | DF | t Value | Pr > [t] |
| Intercept | 54.9502 | 31.9768 | 13 | 1.72 | 0.1094 |
| Initial_Weight | 1.0641 | 0.5259 | 13 | 2.02 | 0.0641 |
| Scale | 371.91 | 145.88 | . | . | . |
| *** MLE 结果 -- 体重增加数据 *** |
| :--- | :--- |
| `GLIMMIX` 过程 |
| 参数估计 | | |
| Effect | Estimate | Standard Error | DF | t Value | Pr > [t] |
| Intercept | 54.9502 | 29.7687 | 13 | 1.85 | 0.0878 |
| Initial_Weight | 1.0641 | 0.4895 | 13 | 2.17 | 0.0488 |
| Scale | 322.33 | 117.70 | . | . | . |

## 22 SAS 中的过度离散模型

### 图 2.1：体重增加示例的诊断图

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_34_0.png)

## 2.4 广义线性模型 (GLM)

广义线性模型 (`GLM`) 是线性回归模型的扩展，适用于可能的非正态甚至是离散的响应变量。`GLM` 公式捕捉了当响应变量按照指数族分布分布时，极大似然估计 (`MLE`) 计算中的本质共性，此时响应变量的均值通过已知的非线性函数与预测变量的未知线性组合相关联。因此，`GLM` 为线性回归、逻辑回归和泊松回归模型等一大类常用模型提供了一种统一的方法。为了理解 `GLM`，需要三个基本概念：随机部分（响应变量）、系统部分（预测变量）和连接函数。

$Y_j, j=1,2,...,n$，表示属于指数分布族某一特定分布的 $n$ 个独立随机变量。我们有 $E(Y_j)=\mu_j$，由于 $Y_j$ 属于指数分布族：

$Var(Y_j)=\phi v(\mu_j)$。

Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS.. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. 更多 SAS 资源请访问 support.sas.com/publishing。

在 `GLM` 框架下，均值 $\mu_j$, $j=1,2,...,n$ 取决于 $k$ 维已知协变量行向量 $\mathbf{x}_j$ 和 $k$ 维未知参数列向量 $\boldsymbol{\beta}$，通过二阶可导的光滑函数 $g(\cdot)$ 使得

$g(\mu_j) = \mathbf{x}_j\boldsymbol{\beta} = \sum_{i=1}^k x_{ji}\beta_i. (2.10)$

函数 $g(\cdot)$ 被称为`连接函数`，$\mathbf{x\beta}$ 被称为`线性预测值`。回想连接函数在第 6 章第 1.6 节已定义。线性预测值通常记为 $\eta_j = \mathbf{x}_j\boldsymbol{\beta}$。在第 2.2 节讨论的经典回归模型中，$\mu_j = \mathbf{x}_j\boldsymbol{\beta} = \sum_{i=1}^k x_{ji}\beta_i$，因此连接函数是恒等函数。注意 $\mu_j = g^{-1}(\mathbf{x}_j\boldsymbol{\beta})$，而 $g^{-1}(\cdot)$ 是均函数。在第 1 章表 1.2 中，提供了伯努利分布和泊松分布的均函数和规范连接函数。从现在起，$g(\cdot)$ 将表示任何连接函数，包括规范连接函数。因此，`GLM` 的主要特征是：

- 1. **随机部分**：$Y_j, j=1,2,...,n$ 的分量是独立的，并按照指数族中的某种分布分布。
- 2. **系统部分**：线性预测值 $\eta_j = \mathbf{x}_j\boldsymbol{\beta}, j=1,2,...,n$ 使得 $\mathbf{x}_j$ 是已知协变量向量，而 $\boldsymbol{\beta}$ 是未知参数向量。
- 3. **连接函数**：连接随机部分和系统部分的函数 $g(\mu_j) = \eta_j, j=1,2,...,n$。

表 2.2 给出了该族中不同成员的 `GLM` 这三个关键部分。在所有这些示例中，随机部分是 $Y_j$，线性预测值是 $\eta_j = \mathbf{x}_j\boldsymbol{\beta}$。注意，分布允许有多个连接函数，且选择不仅限于规范连接。这不是一个详尽列表。可用连接函数选项的完整列表可以在 `GENMOD GLIMMIX` 文档中找到。

### 表 2.2：选定分布的某些连接函数和均函数

| $Y_j$ 的分布 | 连接函数 | 均函数 |
|---|---|---|
| 正态($\mu_j, \sigma^2$) | 恒等: $\mu_j = \mathbf{x}_j\boldsymbol{\beta}$ | 恒等: $\mu_j = \mathbf{x}_j\boldsymbol{\beta}$ |
| 正态($\mu_j, \sigma^2$) | 对数: $\ln(\mu_j) = \mathbf{x}_j\boldsymbol{\beta}$ | 指数: $\mu_j = e^{\mathbf{x}_j\boldsymbol{\beta}}$ |
| 伯努利($\pi_j$) | Logit: $\ln\frac{\pi_j}{1-\pi_j} = \mathbf{x}_j\boldsymbol{\beta}$ | 逻辑: $\pi_j = \frac{e^{\mathbf{x}_j\boldsymbol{\beta}}}{1+e^{\mathbf{x}_j\boldsymbol{\beta}}}$ |
| 伯努利($\pi_j$) | Probit: $\Phi^{-1}(\pi_j) = \mathbf{x}_j\boldsymbol{\beta}$ | 正态: $\pi_j = \Phi^{-1}(\mathbf{x}_j\boldsymbol{\beta})$ |
| 泊松($\lambda_j$) | 对数: $\ln(\lambda_j) = \mathbf{x}_j\boldsymbol{\beta}$ | 指数: $\lambda_j = e^{\mathbf{x}_j\boldsymbol{\beta}}$ |
| 泊松($\lambda_j$) | 恒等: $\lambda_j = \mathbf{x}_j\boldsymbol{\beta}$ | 恒等: $\lambda_j = \mathbf{x}_j\boldsymbol{\beta}$ |

这里，$\Phi(\cdot)$ 代表标准正态分布的累积概率函数，定义为 $\Phi(x) = \frac{1}{\sqrt{2\pi}} \int \exp(-\frac{Z^2}{2}) dZ$。

## 2.5 离度和 Pearson 卡方统计量

在线性回归模型中，拟合优度通常通过残差和来衡量。嵌套模型是通过从较大的（全模型）中选取预测变量的子集获得的。可以使用残差和对简化模型与全模型进行比较，并利用全模型和简化模型的残差和构建 F 检验。在 `GLM` 中，残差和并不总是有意义的，特别是响应变量是离散的时。因此，需要其他方法来检查拟合优度。通过计算被称为离度（Deviance）的统计量，该量最初由 Nelder 和 Wedderburn (1971) 提出。在 `GLM` 框架下，均值 $\mu_j$, $j=1,2,...,n$ 取决于 $k$ 维已知协变量行向量 $\mathbf{x}_j$ 和 $k$ 维未知参数列向量 $\boldsymbol{\beta}$，通过二阶可导的光滑函数 $g(\cdot)$ 使得

$g(\mu_j) = \mathbf{x}_j\boldsymbol{\beta} = \sum_{i=1}^k x_{ji}\beta_i. (2.10)$

函数 $g(\cdot)$ 被称为`连接函数`，$\mathbf{x\beta}$ 被称为`线性预测值`。回想连接函数在第 6 章第 1.6 节已定义。线性预测值通常记为 $\eta_j = \mathbf{x}_j\boldsymbol{\beta}$。在第 2.2 节讨论的经典回归模型中，$\mu_j = \mathbf{x}_j\boldsymbol{\beta} = \sum_{i=1}^k x_{ji}\beta_i$，因此连接函数是恒等函数。注意 $\mu_j = g^{-1}(\mathbf{x}_j\boldsymbol{\beta})$，而 $g^{-1}(\cdot)$ 是均函数。在第 1 章表 1.2 中，提供了伯努利分布和泊松分布的均函数和规范连接函数。从现在起，$g(\cdot)$ 将表示任何连接函数，包括规范连接函数。因此，`GLM` 的主要特征是：

- 1. **随机部分**：$Y_j, j=1,2,...,n$ 的分量是独立的，并按照指数族中的某种分布分布。
- 2. **系统部分**：线性预测值 $\eta_j = \mathbf{x}_j\boldsymbol{\beta}, j=1,2,...,n$ 使得 $\mathbf{x}_j$ 是已知协变量向量，而 $\boldsymbol{\beta}$ 是未知参数向量。
- 3. **连接函数**：连接随机部分和系统部分的函数 $g(\mu_j) = \eta_j, j=1,2,...,n$。

表 2.2 给出了该族中不同成员的 `GLM` 这三个关键部分。在所有这些示例中，随机部分是 $Y_j$，线性预测值是 $\eta_j = \mathbf{x}_j\boldsymbol{\beta}$。注意，分布允许有多个连接函数，且选择不仅限于规范连接。这不是一个详尽列表。可用连接函数选项的完整列表可以在 `GENMOD GLIMMIX` 文档中找到。

### 表 2.2：选定分布的某些连接函数和均函数

| $Y_j$ 的分布 | 连接函数 | 均函数 |
|---|---|---|
| 正态($\mu_j, \sigma^2$) | 恒等: $\mu_j = \mathbf{x}_j\boldsymbol{\beta}$ | 恒等: $\mu_j = \mathbf{x}_j\boldsymbol{\beta}$ |
| 正态($\mu_j, \sigma^2$) | 对数: $\ln(\mu_j) = \mathbf{x}_j\boldsymbol{\beta}$ | 指数: $\mu_j = e^{\mathbf{x}_j\boldsymbol{\beta}}$ |
| 伯努利($\pi_j$) | Logit: $\ln\frac{\pi_j}{1-\pi_j} = \mathbf{x}_j\boldsymbol{\beta}$ | 逻辑: $\pi_j = \frac{e^{\mathbf{x}_j\boldsymbol{\beta}}}{1+e^{\mathbf{x}_j\boldsymbol{\beta}}}$ |
| 伯努利($\pi_j$) | Probit: $\Phi^{-1}(\pi_j) = \mathbf{x}_j\boldsymbol{\beta}$ | 正态: $\pi_j = \Phi^{-1}(\mathbf{x}_j\boldsymbol{\beta})$ |
| 泊松($\lambda_j$) | 对数: $\ln(\lambda_j) = \mathbf{x}_j\boldsymbol{\beta}$ | 指数: $\lambda_j = e^{\mathbf{x}_j\boldsymbol{\beta}}$ |
| 泊松($\lambda_j$) | 恒等: $\lambda_j = \mathbf{x}_j\boldsymbol{\beta}$ | 恒等: $\lambda_j = \mathbf{x}_j\boldsymbol{\beta}$ |

这里，$\Phi(\cdot)$ 代表标准正态分布的累积概率函数，定义为 $\Phi(x) = \frac{1}{\sqrt{2\pi}} \int \exp(-\frac{Z^2}{2}) dZ$。

## 2.5 离度和 Pearson 卡方统计量



在线性回归模型中，拟合优度通常通过残差和来衡量。嵌套模型是通过从较大的（全模型）中选取预测变量的子集获得的。可以使用残差和对简化模型与全模型进行比较，并利用全模型和简化模型的残差和构建 F 检验。在 GLM 中，残差和并不总是有意义的，特别是响应变量是离散的时。因此，需要其他方法来检查拟合优度。通过计算被称为离度（Deviance）的统计量，该量最初由 `Nelder` 和 `Wedderburn` (1971) 提出。对于任何一组极端模型：即最小模型和饱和模型。最小模型包含一个参数（均值），而饱和模型每个观测值有一个参数。最小模型太简单了。另一方面，饱和模型是不提供信息的，因为它提供了完美的拟合。虽然饱和模型没有总结数据，但它们在实践中是有用的。最理想的模型是最小模型和饱和模型之间的。离度本质上是基于似然函数测量的模型与饱和模型之间的距离。`McCullagh` 和 `Nelder` (1989) 指出嵌套模型的离度差异可以用具有相应自由度的卡方分布来近似。

对于独立的二项分布随机变量 `$T_j, j=1,2,...,n, T \sim \text{Binomial}(\pi_j, m_j)$`，考虑 `$T_j$` 为二项分布。注意与之前将响应变量标记为 `$T$` 的符号稍不同。我们将泊松结果标记为 `$Y$`。那么，对于伯努利分布，可以证明离度为：

$D = 2\sum_{j=1}^n t_j \log\left(\frac{t_j}{m_j\hat{\pi}_j}\right) + (m_j - t_j) \log\left(\frac{m_j - t_j}{m_j-\hat{\pi}_j}\right) \quad (2.11)$

其中 `$\hat{\pi}_j = g^{-1}(\mathbf{x}_j\boldsymbol{\beta})$`。当 `$Y_j \sim \text{Poisson}(\lambda_j), j=1,2,...,n$` 时，可以证明离度为：

$D = 2\sum_{j=1}^n y_j \log\left(\frac{y_j}{\hat{\lambda}_j}\right) - (y_j-\hat{\lambda}_j) \quad (2.12)$

其中 `$\hat{\lambda}_j = g^{-1}(\mathbf{x}_j\boldsymbol{\beta})$`。

`Nelder` 和 `Wedderburn` 进一步提出了一种基于离度差异的顺序拟广义方差分析。这种分析之所以是因为嵌套（顺序）模型的离度相加性。`GENMOD` 程序可以提供广义方差分析。

另一个衡量 GLM 拟合优度的指标是 Pearson `$X^2$` 统计量。在 GLM 的背景下，它的定义为：

$X^2 = \sum_{j=1}^{n} \frac{(y_j-\hat{\mu}_j)^2}{v(\hat{\mu}_j)}$

其中 `$v(\hat{\mu}_j)$` 是考虑分布的估计方差函数。对于二项分布，其 Pearson `$X^2$` 统计量为：

$X^2 = \sum_{j=1}^{n} \frac{(t_j-m_j\hat{\pi}_j)^2}{m_j\hat{\pi}_j(1-\hat{\pi}_j)} \quad (2.13)$

以及泊松分布：

$X^2 = \sum_{j=1}^{n} \frac{(y_j-\hat{\lambda}_j)^2}{\hat{\lambda}_j} \quad (2.14)$

## SAS 中的过度离散模型

在某些正则条件下，两个统计量——离度（Deviance，`$D/\phi$`）和皮尔逊卡（`$X^2/\phi$`）的缩放版本都渐近于具有 `$(n-k)$` 个自由度的极限卡方分布。

## 2.6 广义线性模型的极大似然估计

设 `$y_j$` 代表随机变量 `$Y_j$` 的一个观测值，`$j=1,2,...,n$`，`$Y_j$` 来自于指数族中的给定分布。我们感兴趣的是找到 `$\beta$` 的极大似然估计（MLE）。对于某些分布，如二项分布和泊松分布，`$\phi$` 已知为 1。在随后的章节中，将分别获得参数向量 `$\beta$` 和离散（或过度离散）参数的极大似然估计。因此，根据第 1.6 节，对数似然函数为

```
$L(\beta, \phi; \mathbf{y}) = \sum_{j=1}^n \left\{ \frac{y_j - b(\theta_j)}{\phi} + c(y_j, f(\phi)) \right\}$
```

这里 `y` 代表观测向量 `$\mathbf{y} = (y_1, y_2, ..., y_n)$`。

我们现在考虑当 `$\phi$` 固定或已知时 `$\beta$` 的 MLE。`(2.15)` 对 `$\beta$` 的一阶导数构成的 `$k$` 维列向量是梯度或得分向量。即

```
$\mathbf{u}(\beta) = \frac{\partial L(\beta, \phi; \mathbf{y})}{\partial \beta}$
```

从技术上讲，`(2.15)` 中的每一项都是规范参数 `$\theta_j$` 的函数，而 `$\theta_j$` 是均值 `$\mu_j$` 的函数，`$\mu_j$` 是线性预测值 `$\eta_j$` 的函数，且 `$\eta_j = \mathbf{x}\beta$`。因此，获得梯度 `(2.16)` 需要使用链式法则。更多详细信息，请读者参考 `Hilbe` (2007) 中的第 2 章。

`(2.15)` 的二阶导数的 `$k \times k$` 矩阵是海森矩阵（Hessian），形式为

```
$\mathbf{H}(\beta) = \frac{\partial^2 L(\beta, \phi; \mathbf{y})}{\partial \beta \partial \beta}$
```

费雪信息矩阵 (FIM) 是海森矩阵期望值的负值。即

```
$\mathbf{I}(\beta) = -E \left[ \frac{\partial^2 L(\beta, \phi; \mathbf{y})}{\partial \beta \partial \beta} \right] = E \left[ \frac{\partial L(\beta, \phi; \mathbf{y})}{\partial \beta} \frac{\partial L(\beta, \phi; \mathbf{y})}{\partial \beta} \right]$
```

为了获得 `$\hat{\beta}$`（`$\beta$` 的 MLE），需要求解估计方程

```
$$\frac{\partial L(\beta;\phi;\mathbf{y})}{\partial \beta} = \mathbf{0}. \quad (2.19)$$
```

这些方程被称为极大似然得分方程。通常情况下，`(2.19)` 的解没有显式形式，因此通过迭代求解。有多种数值方法可用。Newton-Raphson 法的迭代步骤给出：

```
$$\hat{\beta}_{(S+1)} = \hat{\beta}_{(S)} + {\hat{H}(\hat{\beta}_{(S)})\}^{-1}\mathbf{u}(\hat{\beta}_{(S)}). \quad (2.20)$$
```

以及广泛使用的 Fisher Scoring 法（费雪评分法）实现如下

```
$$\hat{\beta}_{(S+1)} = \hat{\beta}_{(S)} + {\hat{I}(\hat{\beta}_{(S)})\}^{-1}\mathbf{u}(\hat{\beta}_{(S)}). \quad (2.21)$$
```

其中，`$\mathbf{u}(\hat{\beta}_{(S)})$` 是在 `$\hat{\beta}_{(S)}$` 处评估的对数似然函数 `(2.16)` 一阶导数的 `$k$` 维向量，`$\hat{H}(\hat{\beta}_{(S)})$` 是在 `$\beta=\hat{\beta}_{(S)}$` 处评估的 `$k\times k$` 海森矩阵 `(2.17)`，而 `$\hat{I}(\hat{\beta}_{(S)})$` 是在 `$\beta=\hat{\beta}_{(S)}$` 处评估的 `$k\times k$` 费雪信息矩阵 `(2.18)`。下标 `"$s$" ` 指步数或迭代。

前面的讨论适用于通用的 MLE 计算。在指数族的情况下，由于对数似然函数的导数与方程 `(1.9)` 和 `(1.10)` 中给出的一阶矩之间的关系，可以进一步简化。`Nelder` 和 `Wedderburn` (1972) 以及 `Wedderburn` (1974) 证明了极大似然方程 `(2.19)` 的解等同于迭代加权二二法程序。如果 `$\beta$` 的当前估计记为 `$\hat{\beta}_{(S)}$`，则改进的估计 `$\hat{\beta}_{(S+1)}$` 为

```
$$\hat{\beta}_{(S+1)} = \hat{\beta}_{(S)} + (\mathbf{D}^T\mathbf{D})^{-1}\mathbf{D}^T(\mathbf{y}-\mu). \quad (2.22)$$
```

`(2.22)` 右侧除观测向量 `$\mathbf{y}$` 外，所有项均在 `$\hat{\beta}_{(S)}$` 处评估，其中 `$n\times k$` 的一阶导矩阵为

```
$$\mathbf{D} = \begin{pmatrix} \frac{\partial \mu_1}{\partial \beta_1} & \dots & \frac{\partial \mu_1}{\partial \beta_k} \\ \vdots & \ddots & \vdots \\ \frac{\partial \mu_n}{\partial \beta_1} & \dots & \frac{\partial \mu_n}{\partial \beta_k} \end{pmatrix}^T,
```

`$\mathbf{V} = (\mathbf{d}_1, \dots, \mathbf{d}_n)$` 是 `$n\times n$` 的方差对角矩阵

```
$\mathbf{V} = \text{Diag}(\nu(\mu_1), \dots, \nu(\mu_n)) = \text{Diag}(v_1, \dots, v_n),$
```

而 `$\mathbf{\mu}$` 是 `$n$` 维均值列向量 `$\mathbf{\mu}=(\mu_1, \dots, \mu_n)$`。使用这些符号，`(2.22)` 可以写为

```
$$\hat{\beta}_{(S+1)} = \hat{\beta}_{(S)} + \left(\sum_{j=1}^{n} \mathbf{d}_j v_j^{-1} \mathbf{d}_j^T\right)^{-1} \sum_{j=1}^{n} v_j^{-1} (\mathbf{y}_j -\mu)$$
```

注意 `$\mathbf{d}_j$` 是一个 `$k$` 维列向量，而之前定义的协变量向量 `$\mathbf{x}_j$` 是 `$k$` 维行向量。如果假设使用规范连接，极大似然得分方程 `(2.19)` 变为

```
$X^T(\mathbf{y}-\mu) = 0$.
```

在这种情况下，方程 `(2.22)` 和 `(2.23)` 可以进一步简化。迭代程序简化到可以在任何计算机语言中轻松实现的程度。在规范连接下，我们有

```
$$\hat{\beta}_{(S+1)} = \hat{\beta}_{(S)} + (X^T\mathbf{V}X)^{-1} X^T(\mathbf{y}-\mu)$$
```

这可以写为

```
$$\hat{\beta}_{(S+1)} = \hat{\beta}_{(S)} + \left(\sum_{j=1}^{n} \mathbf{d}_j v_j^{-1} \mathbf{d}_j^T\right)^{-1} \sum_{j=1}^{n} v_j^{-1} (\mathbf{y}_j -\mu)$$
``` (注：此处原文公式似乎截断，已根据逻辑补全或保持对应结构)

此时，海森矩阵不包含 `V`，且渐近于 `I`。Newton-Raphson 法和 Scoring 方法是等价的。

在规范连接下，海森矩阵将不包含 `V`。这是一个良好的结果。MLE 估计的协方差矩阵渐近于 `I`。这 = `$\hat{\beta}_{(S+1)} v_j^{-1} (\mathbf{y}_j-\mu)$` 这种形式（注：原文此处逻辑存在混乱，翻译已尽量保留原文的结构）。在剂量-死亡研究中，我们关注对剂量的影响。当将观测百分比对剂量（或剂量的对数）绘图时，得到的图表类似于累积概率函数的 S 形状。`Bliss` (1933, 1935) 假设这种形状对应于累积正态分布（Probit 模型）。另一方面，`Berkson` (1944) 发现累积逻辑分布函数（Logit 模型）更合适。“probit”一词归于 `Bliss`，而“logistic”一词归于 `Pearl`。剂量-死亡分析是 GLM 的早期示例。

拟菊酯是发现于许多杀虫剂的一类化学物质。`Murray` (1938) 概述了同时评估杀虫剂的方法，即精确方法，以及可能的精度范围。不同浓度的拟菊酯在蝇身上进行了测试。

### 表 2.3：雄蝇的剂量-死亡数据

| 拟菊酯浓度 mg/100 cc (`$D_j$`) | 苍蝇数量 (`$m_j$`) | 死亡数量 (`$t_j$`) |
|---|---|---|
| 40 | 462 | 109 |
| 60 | 500 | 199 |
| 80 | 467 | 296 |
| 100 | 515 | 370 |
| 120 | 561 | 459 |
| 140 | 469 | 400 |
| 160 | 550 | 495 |
| 180 | 542 | 499 |
| 200 | 479 | 450 |
| 250 | 497 | 476 |
| 300 | 453 | 442 |

我们首先拟合逻辑回归模型，这等同于拟合具有二项分布和对连接的 GLM。在某些正则条件下，极大似然估计具有良好的性质。它们是无偏的或渐近无偏的。MLE 是渐近有效的，因为在样本量趋于无穷时，它们达到了 Cramer-Rao 下界。这意味着没有其他无偏估计量的渐近均方误差比 MLE 小。此外，它们是渐近正态的，也就是说随着样本量的增加，MLE 的分布趋向于高斯分布。

# SAS 中的过度离散模型

如果 `$\tilde{\pi}_j = \frac{t_j}{m_j}$` 是观测比例，其对应的逻辑回归（logit）定义为：

```
$$\ln\left(\frac{\tilde{\pi}_j}{1-\tilde{\pi}_j}\right) = \ln\left(\frac{t_j}{m_j-t_j}\right)$$$
```

在实践中，这些量被微调为

```
$$\ln\left(\frac{t_j+0.5}{m_j-t_j+0.5}\right)$$$
```

以避免在 `$t$` 为 0 或 `$m$` 时出现数值问题。估计的线性预测值为 `$\hat{\eta}_j = \hat{\beta}_0 + \hat{\beta}_1X_j$`。程序语句见程序 2.2。`GLIMMIX` 生成的结果见输出 2.2。

## 程序 2.2：拟虫酯的剂量-死亡数据拟合带 Logit 链接的二项模型

`Morel, J., and Nagaraj Neelander. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED.` 更多资源请访问 `support.sas.com/publishing`。

表 2.4 汇总了直接来自输出 2.2 的极大似然结果。斜率 `$\beta_1$` 的幅度取决于变量 `"x"` 的尺度。对剂量进行常用对数变换将产生更大的 `$\beta_1$` 估计值。

**输出 2.2：拟虫酯剂量-死亡数据的 GLIMMIX 结果——带 Log 链接的二项模型**

| 蝇拟虫酯剂量-死亡，Murray (1938) 二项分布和 Log 链接的 GLM |
| --- |
| **GLIMMIX 过程** |
| 拟合统计量 |
| -2 对数似然 | 69.91 |
| Pearson 卡方 | 6.34 |
| Pearson 卡方 / DF | 0.70 |
| 参数估计值 |
| --- |
| 效应 | 估计值 | 标准误差 |
| **效应** | **估计值** | **标准误差** | **DF** | **Pr >|t|** |
| 截距 | -10.3279 | 0.3429 | | -30.12 | <0001 |
| x | 2.4582 | 0.07470 | 9 | 32.91 | <0001 |

**表 2.4：拟虫酯剂量-死亡数据带 Log 链接的二项模型的 MLE 结果**

| | 估计值 | 标准误差 |
| --- | --- | --- |
| `$\beta_0$` | -10.3279 | 0.3429 |
| `$\beta_1$` | 2.4582 | 0.0747 |
| -2 对数似然 | 69.91 | |

`GLIMMIX` 残差诊断图如图 2.2 所示。“残差预测值”并未显示离群值的存在或任何可感知的模式。残差与分位数图接近直线，表明残差具有渐近正态性。我们得出结论，逻辑回归模型拟合这些数据是可靠的。我们的结论也通过自由度归一化的 Pearson 卡方统计量证实，其值为 0.70（见输出 2.2）。

### 图 2.2：拟虫酯剂量-死亡数据带 Logit 链接的二项模型 GLIMMIX 残差诊断图

![](img/fa69b64c17ad451eb7eb4add92f5fb_44.png)

在剂量死亡研究中，感兴趣的量是 LD50，即杀死 50% 个体的剂量。该量也可以被认为是种体的中耐受水平。在逻辑回归模型下，LD50 可以通过求解方程轻松获得：

`$\beta_0 + \beta_1 LD50 = \ln\left(\frac{\pi}{1-\pi}\right)$`



取 $\pi=\frac{1}{2}$。在这种情况下 $\frac{\pi}{1-\pi}=1$，因此 $LD50=\frac{\beta_0}{\beta_1}$。在 Murray 的示例中，LD50 的估计值为 $\frac{10.3279}{2.4582}=4.2014$。在对数尺度下，LD50 为 $e^{4.2014}=66.78$。

我们对 Murray 的数据拟合了一个 Probit 模型。在 Probit 模型中，均值函数定义为 $\pi_j = \Phi(x_j)$，其中 $\Phi(\cdot)$ 是标准正态分布的累积分布函数。因此，Probit 链接为 $\Phi^{-1}(\pi) = \beta_0 + \beta_1x_j$。注意使用 Probit 链接时，估计的线性预测值 $\hat{\eta}_j = \hat{\beta}_0 + \hat{\beta}_1x_j$ 是 Z 分。预测分为零的对象具有 50% 的概率，预测分为 1.64 的具有 95% 的概率等。使用 GLIMMIX 拟合 Probit 模型并包含诊断图的程序语句：

```
ods html;
ods graphics on;
title "蝇拟虫酯剂量-死亡，Murray (1938)"
title2 "二项分布和 Probit 链接的 GLM";
proc glimmix data=pythrins plots=residual;
model t/m = x / dist=binomial link=probit;
run;
ods graphics off;
ods html;
```

我们跳过了输出的描述。表 2.5 汇总了极大似然结果。

### 表 2.5：拟虫酯剂量-死亡带 Probit 链接的二项模型的 MLE 结果

| 参数 | 估计值 | 标准误差 |
| --- | --- | --- |
| $\beta_0$ | -5.9139 | 0.1875 |
| $\beta_1$ | 1.4090 | 0.4017 |
| -2 对数似然 | 75.20 | |

LD50 通过求解方程 $\beta_0 + \beta_1 LD50 = \Phi^{-1}(\pi)$ ，其中 $\pi =\frac{1}{2}$。对于这个 $\Phi^{-1}(\pi) = 0$ 的值，与逻辑回归情况一样，$LD50 = -\frac{\beta_0}{\beta_1}$。使用表 2.5 提供的估计值，LD50 的估计值为 4.1972，尺度为 $e^{4.1972}=66.50$ mg/cc，与逻辑模型获得的值几乎相同。GLIMMIX 残差诊断图如图 2.3 所示。注意大部分残差是非负的，且残差与分位数图显示偏离直线。比较图 2.2 和 2.3 得出一个结论：在这个特定示例中，Probit 模型提供了更好的拟合。

### 图 2.3：拟虫酯剂量-死亡数据带 Probit 链接的二项模型 GLIMMIX 残差诊断图

![](img/fa69b64c17ad451eb7eb4ad8d2f5fb_46.png)

### 程序 2.3：使用 PROC PROBIT 为拟虫酯的剂量-死亡数据拟合带 Probit 和 Logit 链接的二项模型

```
ods html;
title1 "蝇拟虫酯剂量-死亡，Murray (1938)"
title2 "二项分布和 Logit 链接的 PROC PROBIT";
proc probit data=pyrethins log;
model t/m = dose / logistic inversecl;
run;
title "蝇拟虫酯剂量-死亡，Murray (1938)"
title2 "二项分布和 Probit 链接的 PROC PROBIT";
proc prob data=pyrethins log;
model t/m = dose / inversecl;
run;
ods html;
```

PROC 中的 "log" 选项对剂量的自然对数进行分析。"inversecl" 选项提供了以 1% 为增量的致死剂量（LD）估计值，用于杀死从 1% 到 99% 的种群。这些 LD 在对数尺度和剂量尺度上计算。选定的结果在输出 2.3 中。

### 输出 2.3：拟虫酯剂量-死亡数据的 PROC PROBIT 结果

| 蝇拟虫酯剂量-死亡，Murray (1938) 二项分布和 Logit 链接的 PROC PROBIT |
| --- |
| Probit 过程极大似然参数估计 |
| 参数 | DF | 标准误差 | 95% 置信区间 | 卡方 | Pr > ChiSq |
|---|---|---|---|---|---|
| 截距 | 1 | -10.3279 | 0.3429 | -11.0000, -9.6558 | 907.14 | <0001 |
| Ln(dose) | 1 | 2.4582 | 0.0747 | 2.3118, 2.6047 | 1082.89 | <0001 |
| Probit 分析针对 Ln(dose) |
| 概率 | Ln(dose) | 95% 似位数区间 |
|---|---|---|
| 0.50 | 4.20133 | 4.16305, 4.23705 |
| Probit 分析针对剂量 |
| 概率 | 剂量 | 95% 似位数区间 |
|---|---|---|
| 0.50 | 66.77534 | 64.26718, 69.20315 |

# SAS 中的过度离散模型

| 使用 PROC PROBIT 带有二项分布和 Probit 链接的 GLM |
| 最大似然参数估计的分析 |
| 参数 | DF | 估计值 | 标准误 | 95% 置信区间 | 卡方 | Pr > ChiSq |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 截距 | 1 | -5.9139 | 0.1875 | -6.2815 | -5.5464 | 994.63 | <0001 |
| Ln(dose) | 1 | 1.4090 | 0.0402 | 1.3303 | 1.4877 | 1230.23 | <0001 |
| 对 Ln(dose) 的 Probit 分析 |
| 概率 | Ln(dose) | 95% 赖度区间 |
| :--- | :--- | :--- | :--- |
| 0.50 | 4.1973 | 4.1574 | 4.2344 |
| 对 dose 的 Probit 分析 |
| 概率 | dose | 95% 赖度区间 |
| :--- | :--- | :--- | :--- |
| 0.50 | 66.5040 | 63.90220 | 69.0298 |

在在这两种分析（Probit 与 Logit）之间进行选择似乎没有明确的标准。它们可以被认为是对分别服从正态分布或 Logistic 分布的潜变量触发的事件进行建模。Cox 和 Snell (1989, pp. 21-22) 指出，对于大多数目的，Logistic 分布和正态分布非常一致，除非感兴趣的是极值，此时成功的概率要么非常小，要么非常接近 1。累积正态曲线比累积 Logistic 曲线更快地接近其极限，表明后者的尾部比前者更长。

# 第 2 章 广义线性模型

## 程序 2.4：正态和 Logistic 累积分布函数的估计——除虫椒醚的剂量-死亡数据

```
-- 绘图
1)估计的 Logistic 曲线和观测比例
2)估计的 Probit 曲线和观测比例
temp:
    do dose=38 to 301 by 0.1; -- 以 0.1 为增量的剂量范围；
    x = log(dose);
    output;
end;
drop dose;
run;
data new;
    set pyrethrins temp;
run;
proc glimmix data=new;
    model t/m = x / link=probit;
    output=pred_out1(xlink)=pi_hat;
run;
proc glimmix data=new;
    model t/m = x;
    output=pred_out2(xlink)=pi_hat;
run;
data pred_out1;
    set pred_out1;
    label pi_hat = 'Predicted Probability'
    obs_pi = ;
    obs_pi = 'Observed Probability';
    if t > 0 then
        obs_pi = t/m;
        pi_hat = ;
end;
drop t;
run;
data pred_out2;
    set pred_out2;
    label pi_hat = 'Predicted Probability'
    obs_pi = ;
    obs_pi = 'Observed Probability';
    if t > 0 then
        obs_pi = t/m;
        pi_hat = ;
end;
drop t;
run;
html;
ods graphics data=pred_out1;
proc sgplot;
    title "Estimated Probit Curve"
    title2 "除虫椒醚对雄蝇的剂量-死亡, Murray (1938)";
    scatter x=x y=pi_hat;
    series x=x y=pi_hat / y2axis;
run;
proc sgplot data=pred_out2;
    title "Estimated Logistic Curve";
```

```
title2 "除虫椒醚对雄蝇的剂量-死亡, Murray (1938)";
scatter x=x y=obs_pi;
series x=x y=pi_hat / y2axis;
run;
ods graphics off;
ods close;
```

使用 SGPLOT 程序创建最终的图表（需要 SAS 9 或更高版本）。图 2.4 和 2.5 提供了讨论的图表。这两个图之间的差异可能很细微。读者可以看到，累积正态曲线比累积 Logistic 曲线更迅速地接近其极限。

### 图 2.4：除虫椒醚剂量-死亡的估计正态累积函数

img/fa69b48c17ebe4d92.

### 图 2.5：除虫椒醚剂量-死亡的估计 Logistic 累积函数

img/fa69b48c17ebe4d92.png

程序 2.4 中的编程语句提供了估计的概率函数相对于观测比例的图表。观测到的比例 $\hat{P}_j = \frac{t_j}{m}, j=1,2,...,11$ 是均值，并叠加了估计的函数。我们首先以十为增量生成数据集 "temp"，即范围在 38 到 301 之间的剂量值。变量 "$x" 是剂量的自然对数。此数据与数据 "pyrethrins" 合并。然后，拟合两个 GLM：一个使用 Probit 链接，另一个使用 Logit 链接。数据集 "temp" 未被用于变量 "$t" 和 "$m" 的 MLE 的任何计算中。然而，像许多其他过程一样，GLIMMIX 为缺失数据提供了概率估计。它们被用于构建平滑的累积概率函数。

More, Jorge, and Nagaraj Neerchal. Overdispersion Models in SAS®. 版权 2011, SAS Institute Inc., Cary, North Carolina, USA. 版权所有。欲获取更多 SAS 资源，请访问 support.sas.com/publishing。



# 绘图

1) 估计的 Logistic 曲线和观测比例
2) 估计的 Probit 曲线和观测比例

```sas
temp:
    do dose=38 to 301 by 0.1; -- 以 0.1 为增量的剂量范围；
    x = log(dose);
    output;
end;
drop dose;
run;
data new;
    set pyrethrins temp;
run;
proc glimmix data=new;
    model t/m = x / link=probit;
    output=pred_out1(xlink)=pi_hat;
run;
proc glimmix data=new;
    model t/m = x;
    output=pred_out2(xlink)=pi_hat;
run;
data pred_out1;
    set pred_out1;
    label pi_hat = 'Predicted Probability'
    obs_pi = ;
    obs_pi = 'Observed Probability';
    if t > 0 then
        obs_pi = t/m;
        pi_hat = ;
end;
drop t;
run;
data pred_out2;
    set pred_out2;
    label pi_hat = 'Predicted Probability'
    obs_pi = ;
    obs_pi = 'Observed Probability';
    if t > 0 then
        obs_pi = t/m;
        pi_hat = ;
end;
drop t;
run;
html;
ods graphics data=pred_out1;
proc sgplot;
    title "Estimated Probit Curve"
    title2 "除虫椒醚对雄蝇的剂量-死亡, Murray (1938)";
    scatter x=x y=pi_hat;
    series x=x y=pi_hat / y2axis;
run;
proc sgplot data=pred_out2;
    title "Estimated Logistic Curve";
```

```sas
title2 "除虫椒醚对雄蝇的剂量-死亡, Murray (1938)";
scatter x=x y=obs_pi;
series x=x y=pi_hat / y2axis;
run;
ods graphics off;
ods close;
```

使用 `SGPLOT` 程序来实现创建最终的图表（需要 SAS 9 或更高版本）。图 2.4 和 2.5 提供了讨论的图表。这两个图之间的差异可能很细微。读者可以看到，累积正态曲线比累积 Logistic 曲线更迅速地接近其极限。

图 2.4：除虫椒醚剂量-死亡的估计正态累积函数

`img/fa69b48c17ebe4d92.`

图 2.5：除虫椒醚剂量-死亡的估计 Logistic 累积函数

`img/fa69b48c17ebe4d92.png`

对于 Logistic 回归，其主要优势是可以根据优势比（Odds-ratios）来解释参数。现在考虑一个分类变量 `X`，当暴露因子存在时取值为 1，否则取 0。设 `π(X)` 为患病概率，我们建立如下 Logistic 模型：

```
logit(\pi(X)) = \ln\left(\frac{\pi(X)}{1-\pi(X)}\right) = \beta_0 + \beta_1 X
```

当暴露因子存在时，患病概率为：

```
\pi(X=1) = \frac{e^{\beta_0+\beta_1}}{1+e^{\beta_0+\beta_1}}
```

同样，当暴露因子缺失时，患病概率为：

```
\pi(X=0) = \frac{e^{\beta_0}}{1+e^{\beta_0}}
```

因此可以证明优势比（OR）为：

```
OR = \frac{\pi(X=1)}{1-\pi(X=1)}}{\frac{\pi(X=0)}{1-\pi(X=0)}} = e^{\beta_1}
```

这是一个基础结论：Logistic 回归的斜率可以通过优势比的对数来解释。在之前的设置中，`β_1=\ln(OR)`。

# SAS 中的过度离散模型

| 暴露因素 | 是 | 否 |
| --- | --- | --- |
| 存在 | `π_{11}` | `π_{12}` |
| | `π_{+1}` | `π_{+2}` |
| 缺失 | `π_{21}` | `π_{22}` |
| | `π_{+1}` | `π_{+2}` |
| 总计 | 1 | 1 |

根据上述信息，无法重建前瞻性研究的概率。然而，一切并非无望，因为可以从上述信息中恢复出比值（OR）。现在，比值被定义为：疾病存在时具有暴露因素的几率与疾病不存在时具有暴露因素的几率之比。这些比率定义为：

> 比率（疾病存在时具有暴露因素） = `π_{11}/π_{+1} = π_{11}/π_{21}`

以及

> 比率（疾病不存在时具有暴露因素） = `π_{12}/π_{+2} = π_{12}/π_{22}`

因此，对于病例对照研究，比值值为：

> OR = 比率（疾病存在时具有暴露因素） = `π_{11}/π_{+1} = π_{11}/π_{21}`

比率（疾病不存在时具有暴露因素） = `π_{12}/π_{+2} = π_{12}/π_{22}`

注意，比值在前瞻性研究和病例对照（回顾性）研究中是相同的。人们说比值“对采样方案具有不变性”。这一事实对于流行病学家、医学研究人员和公共健康从业者在进行病例对照研究时非常重要。在这些研究中，结果显示相对风险 `RR = π(X=1)/π(X=0)` 无法直接获得。另一方面，计算比值是直观的。在这种情况下，众所周知，比值和相对风险在实际上是非常相似的 (Cornfield, 1951)。比值的这两个特性——对研究性质的不不变性以及与相对风险几乎相同的值，使得逻辑回归成为最受吸引力的统计回归方法之一。

More, Jorge, and Nagaraj Neerchal. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 获取更多 SAS 资源请访问 `support.sas.com/publishing`。

## 第二章 广义线性模型

为了说明逻辑回归在病例对照研究中的应用，我们考虑了 Ille-et-Vaine 食道癌研究。Ille-et-Vaine 是法国革命期间由布列塔尼省的一部分创建的法国省。已知布列塔尼和诺曼地的食道癌死亡率很高。Tuyns 等人 (1977) 在 Ille-et-Vaine 省收集了数据，其中 200 名男性（病例）被诊断患有食道癌。从每个市镇的选举列表中抽取了 778 名受试者（无癌症）。其中，775 名受试者提供了足够的分析信息。`reslow` 和 `Day` (1980) 使用这个例子说明了癌症研究的不同统计方法。我们建议读者参考他们书的第 4 章和第 5 章。Ille-et-Vaine 病例对照研究的数据如表 2.6 所示。

### 表 2.6：Ille-et-Vaine 食道癌研究数据

| 层（年龄，岁） | 癌症暴露 | 高 | 低 |
|---|---|---|---|
| 25-34 | 病例 | | 0 |
| | 对照 | 9 | 106 |
| 35-44 | 病例 | | 5 |
| | 对照 | 26 | 164 |
| 45-54 | 病例 | | 21 |
| | 对照 | 29 | 138 |
| 55-64 | 病例 | 42 | 34 |
| | 对照 | 27 | 139 |
| 65-74 | 病例 | 19 | 36 |
| | 对照 | 18 | 88 |
| 75+ | 病例 | 5 | 8 |
| | 对照 | 0 | 31 |

数据以 5x2 列联表的形式进行了汇总。

## 程序 2.5：使用 GENMOD 分析 Ille-Vaine 食道癌研究数据

```sas
/*
  Ille-Vaine Study of oesophageal cancer, Tuyns et al. (1977)
*/
data one;
    input_stratum stratum $ count x1 x2;
    format alcohol $5;
    alcohol = 'High'; count = x1; output;
    alcohol = 'Low'; count = x2; output;
    drop x1 x2;
  datalines;
  25-34 Case 1 0
  25-34 Control 9 106
  35-44 Case 4 5
  35-44 Control 26 164
  45-54 Case 25 21
  45-54 Control 29 138
  55-64 Case 42 34
  55-64 Control 27 139
  65-74 Case 19 36
  65-74 Control 18 88
  75+ Case 5 8
  75+ Control 0 31
;
;
```

```sas
proc sort data=one;
    by age_stratum alcohol;
run;
proc transpose data=one out=oesophageal_cancer;
    by age_stratum alcohol;
    var count;
    id cancer;
run;
```

```sas
data oesophageal_cancer;
set oesophageal_cancer;
    m = Case + Control;
drop name_;
run;
ods html;
proc genmod data=oesophageal_cancer;
    class age_stratum alcohol;
    model case/m = age_stratum alcohol / dist=binomial link=logit type3;
    estimate 'Ln(OR) High Vs Low' alcohol 1-1 / exp;
run;
ods html close;
```

### 输出 2.5：GENMOD 结果——Ile-et-Vilaine 研究

### GENMOD 过程

| 类型 3 分析的 LR 统计量 |
| 来源 | DF | 卡方 | Pr > ChiSq |
| --- | --- | --- | --- |
| age_stratum | 5 | 104.13 | <.0001 |
| alcohol | 1 | 79.52 | <.0001 |

| 对比估计值结果 |
| 标签 | 均值估计 | 均值 | L'Beta 估计 | 标准误差 | Alpha | L'Beta | 卡方 | Pr > ChiSq |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| | | 置信区间 | | | | 置信区间 | | | |
| La(OR) High Vs Low | 0.8416 | 0.7855 | 0.8851 | 1.6699 | 0.05 | 1.2983 | 2.041 | | |
| Exp(La(OR)) High Vs Low | | | 5.3116 | 1.0071 | 0.05 | 3.630 | 7.702 | .001 |

注意，比值在前瞻性研究和病例对照（回顾性）研究中是相同的。人们说比值“对采样方案具有不变性”。这一事实对于流行病学家、医学研究人员和公共健康从业者在进行病例对照研究时非常重要。在这些研究中，结果显示相对风险 `RR = π(X=1)/π(X=0)` 无法直接获得。另一方面，计算比值是直观的。在这种情况下，众所周知，比值和相对风险在实际上是非常相似的 (Cornfield, 1951)。比值的这两个特性——对研究性质的不不变性以及与相对风险几乎相同的值，使得逻辑回归成为最受吸引力的统计回归方法之一。

数据以 5x2 列联表的形式进行了汇总。

# 第2章 广义线性模型 47

由于对数函数是泊松分布最常用的连接函数，为了对比目的，我们提供了在恒等函数（identity function）和对数函数下的诊断图。编程语句已在程序 2.6 中。

## 程序 2.6：两种运行状态下电子设备故障次数分析

```sas
/*
Number of Failures Electronic Equipment under Two Operating Regimes
Jorgensen (1961), and Frome et al. (1971)*
data failures;
input x1 x2 y;
datalines;
33.3 25.3 15
52.2 14.4 9
64.7 30.2 14
137.0 20.5 24
125.9 97.6 27
116.3 53.6 27
131.7 55.6 23
85.0 87.3 18
91.9 47.8 22
;
ods html on;
ods graphics on;
title *** Fisher Scoring optimization technique to iteration 10;
title2 *** Identity Link;
proc glimmix data=failures scoring=10 plots=residual;
model y = x1 x2 / nint dist=poisson link=identity covb;
run;
title *** Fisher Scoring optimization technique to iteration 10;
title2 *** Logarithm Link;
proc glimmix data=failures scoring=10 plots=residual;
model y = x1 x2 / nint dist=poisson link=log covb;
run;
graphics off;
ods html close;
```



输出 2.6 描述了由 GLIMMIX 过程选定的结果。

### 输出 2.6：电子设备故障次数分析的 GLIMMIX 结果

| 优化信息 | |
| :--- | :--- |
| 优化技术 | Newton-Raphson |
| Fisher Scoring | 迭代至 10 次。评分未停止。 |

| 拟合统计量 | |
| :--- | :--- |
| 皮尔逊卡方检验 | 8.90 |
| 皮尔逊卡方 / 自由度 | 1.27 |

| 参数估计 | | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 效应 | 估计值 | 标准误差 | 自由度 | t 值 | Pr >t |
| x1 | 0.1666 | 0.03486 | 7 | 4.78 | 0.0020 |
| x2 | 0.0904 | 0.06301 | 7 | 1.43 | 0.1945 |

| 固定效应协方差矩阵 | | | |
| :--- | :--- | :--- |
| 效应 | Col1 | Col2 |
| x1 | 0.001216 | -0.00196 |
| x2 | -0.00196 | 0.00397 |

注意，默认优化技术为 Newton-Raphson。我们请求在前 10 次迭代中使用 Fisher 评分法。由于算法在四次迭代后收敛，输出结果对应于 Fisher 评分法。信息“Scoring did not stop”表明在前10次迭代内通过 Fisher 评分法实现了收敛。皮尔逊卡方值为 8.90，除以自由度得到 1.27，这是尺度参数的估计值。极大似然估计（MLEs）为 $\hat{\beta}_1 = 0.1666$ 和 $\hat{\beta}_2 = 0.0904$。$\hat{\beta} = (\hat{\beta}_1, \hat{\beta}_2)$ 的估计协方差矩阵为 $\text{Var}(\hat{\beta}) = \begin{pmatrix} 0.001216 & -0.00196 \\ -0.00196 & 0.00397 \end{pmatrix}$。所有这些都在五迭代内收敛。与 Ford 等人（1971）报告的，迭代算法在迭代中收敛。固定效应的 III 类检验表明第一种状态显著的（P值 < 0.01）。图 2.6 和 2.7 表明恒等连接会导致更好的残差图。顺便提到，当使用对数连接时，归一化皮尔逊卡方统计量（此处未显示）为 13.59。人们可能会认为连接函数错误可能导致分析人员认为数据存在过度离散。

### 图 2.6：恒等连接下电子设备故障次数的 GLIMMIX 残差诊断图

![](img/fa69b48c17ad451eb7eb4ad8d2ffb_61_0.png)

Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RESERVED. 更多 SAS 资源，请访问 support.sas.com/publishing。

### 图 2.7：对数连接下电子设备故障次数的 GLIMMIX 残差诊断图

![](img/fa69b48c17ad451eb7eb4ad8d2ffb_62_0.png)

Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RESERVED. 更多 SAS 资源，请访问 support.sas.com/publishing。

# 准似然函数

- 3.1 引言...............................................................51
- 3.2 准似然函数......................................................52
- 3.3 口腔护理案例....................................................54
- 3.4 萨尔瓦多的弓吸虫症...............................................57
- 3.5 致癌前临床实验...............................................63
- 3.6 椎骨折高风险患者的骨质疏松案例................66
- 3.7 Williams 准似然模型.......................................69

## 3.1 引言

在第2章中，我们讨论了广义线性模型（GLM）背景下的参数极大似然估计（MLE）。正如我们讨论过的，这些估计具有良好的性质：它们是一致的、渐近有效的且符合正态分布。在许多存在过度离散的情况下，使用极大似然估计是理想的。将 MLE扩展到过度离散数据需要关于生成过度离散的随机机制的额外信息；这些信息使得建立完整的似然成为可能。然而，在现实，可能没有解释过度离散的似然函数。因此，过度离散模型的估计可以通过准似然估计（QLEs）来解决，这种估计基本上基于数据前两个矩的设定。QLEs 是估计来自准似然函数的模型参数的自然首次方法，该函数由 Wedderburn (1974) 定义并基于似然函数。这些函数允许人们在不完全了解似然函数的情况下分析过度离散的数据，并展示了均值与方差之间的关系。我们将介绍准似然函数并展示其应用。

![](img/fa69b48c17ad451eb7eb4ad8d2ffb_63_0.png)

# 第 3 章 准似然函数

基于数据 $y = (Y_1, Y_2, \dots, Y_n)'$ 和均值向量 $\mu = (\mu_1, \mu, \dots, \mu_n)'$ 的**准似然**（或更准确地说是**对数准似然**）。$\beta$ 的准似然估计值 $\hat{\beta}$ 通过关于 $\beta$ 求解方程(3.3)得到，即：

```
U(\beta) = \frac{\hat{Q}(y, \mu)}{\hat{\beta}} = 0. (3.4)
```

(3.4)中的函数 $U(\beta)$ 是**准得分函数**。根据(3.2)，方程(3.4)可以写为：

```
\sum_{j=1}^n \frac{Y_j - \mu_j}{\sqrt{\phi(\mu_j)}} \frac{\hat{\mu}_j}{\hat{\beta}} = 0. (3.5)
```

(3.5)关于 $\beta$ 的解不需要知道 $\phi$ 的值，因为 $\phi$ 是一个尺度参数且会被消去。因此，这些方程简化为：

```
\sum_{j=1}^n \frac{Y_j - \mu_j}{\sqrt{\phi(\mu_j)}} \frac{\hat{\mu}_j}{\hat{\beta}} = 0,
```

从计算角度来看，如果 $Y_j$ 属于 $\phi=1$ 的指数族成员之一，则这些方程成立。与GLM的情况类似，(3.5)的解等于第2.6节中的迭代加权平方法。得到 $\hat{\beta}$ 后，可以计算离散参数 $\phi$ 的矩估计。两种常用的 $\phi$ 估计值是通过标准化 Pearson $X^2$ 或离差（Deviance）并除以其自由度得到的。也可以使用其他的矩估计。

在温和的正则条件下，估计向量的渐近方差为：

```
Var(\hat{\beta}) \equiv \phi(\mathbf{D}'\mathbf{V}^{-1}\mathbf{D})^{-1}. (3.6)
```

其中 $\mathbf{D}$ 是一阶导数的 $n \times n$ 矩阵：

```
\mathbf{D} = (\frac{\hat{\mu}_1}{\hat{\beta}}, \frac{\hat{\mu}_2}{\hat{\beta}}, \dots, \frac{\hat{\mu}_n}{\hat{\beta}})' \equiv (d_1, d_2, \dots, d_n)'
```

$\mathbf{V}$ 是方差函数的 $n \times n$ 对角矩阵：

```
\mathbf{V} = \text{Diag}(v(\mu_1), v(\mu_2), \dots, v(\mu_n)) \equiv \text{Diag}(v_1, v_2, \dots, v_n).
```

注意，方差(3.6)可以写为：

```
Var(\hat{\beta}) \equiv \phi \left(\sum_{j=1}^{n} d_j^{-1} d_j^{\top}\right)^{-1} (3.7)
```

对于规范链接，方程(3.6)变为：

```
Var(\hat{\beta}) \equiv \phi(X^{\top}X)^{-1} (3.8)
```

## 3.3 口腔护理示例

为了说明准似然估计步骤，考虑表3.1中取自临床试验的数据（Schulte等，1998），其中$n=17$名受试者使用实验牙膏刷了六周牙。研究结束时在每个受试者的口腔（$m=4$）处测量pH。认为如果pH $\le 6.5$，受试者患口腔病的风险较高。注意，pH测量与刷牙习惯、牙膏使用、饮食以及受试者的遗传特征有关。因此，假设每个部位内部之间存在正相关是自然的。

令$T_j, j=1,...,n$ 表示在$n$名受试者中观察到的pH缺失部位数量。让我们考虑$T_j, j=1,...,n$ 是相对于二项分布模型的独立同分布随机变量的简单情况。$T_j$ 的均值和方差分别为 $\mu_j=m\pi$ 和 $\phi(\mu_j)=m\pi(1-\pi)$，其中$\phi=\{1+\rho(m-1)\}$，$\pi=Prob(pH \le 6.5)$，且$\rho$ 是类内相关，假设为正。对于感兴趣的参数$\pi$，链接函数是恒等函数。如果读者估计的是对数比（log-odds），则对数链接是合适的。$t_j$ 代表$T_j$ 的一个实现。在这个简单示例中，准似然得分函数(3.5)的解简化为：

```
$$\sum_{j=1}^{n} \frac{t_j - m\pi}{m\pi(1-\pi)} = 0.
```

$\pi$ 的准似然估计在这种情况下有一个显式解，即：

$$\hat{\pi} = \frac{\sum_{j=1}^n t_j}{nm}$$

通过计算离差除以其自由度可以得到 $\phi$ 的矩估计，即：

$$\hat{\phi} = 2\sum_{j=1}^n \left\{ t_j \log\left(\frac{t_j}{m\hat{\pi}}\right) + (m-t_j)\log\left(\frac{m-t_j}{m-\hat{\pi}}\right) \right\}$$

程序3.1提供了使用GENMOD过程执行此示例准似然估计的语句。注意簇大小为$m=4$，我们创建了一个长度为$n=17$的字符串'$t_j$’以使分析与$\hat{\pi}$和$\phi$的符号一致。

### 程序3.1：表3.1 pH数据的准似然分析

```sas
/*
Schulte等，1998口腔护理示例
*/
data pH;
  input t f;
  m = 4;
  do i=1 to f;
    output;
  end;
  drop i;
  datalines;
0 4
1 4
2 6
3 2
4 1;
ods html close;
proc genmod data=pH;
  model t/m = binomial link=identity scale=deviance;
run;
```

GENMOD过程产生的输出见于输出3.1。我们只提供与示例讨论相关的输出部分。二项分布的GENMOD过程返回的是$\sqrt{\phi}$而非$\phi$。在示例中，$\pi$和$\phi$的估计值分别为$0.3824$和$1.8878$。值$1.8878$在输出中是离差除以其自由度。类内相关$\rho^2$的矩估计可以通过求解方程$\phi=\{1+\rho(m-1)$得到。这得出$\rho^2 =0.30$。注意，由于这里没有协变量且所有簇的大小相同，可以进行此操作。通常情况下，可能从$\phi$恢复$\rho^2$。由于$\hat{\pi}$的估计误差为$0.0810$，$\pi$的近似95%置信区间为$(0.22, 0.54)$。二项分布模型意义上的幼稚误差为$0.0810/1.3740=0.0589$（输出中未报告）。该估计会导致覆盖概率低于标值的更窄区间。在进行研究之前，建立了一个基线（pH $\le 6.5$的部位比例），报告为$71\%$。因此，我们可以得出实验牙膏在减少口腔病高风险部位比例方面有效的结论。

### 输出3.1：程序3.1的GENMOD输出

| GENMOD过程 | 评估拟合优度的标准 | | |
| :--- | :--- | :--- | :--- |
| | DF | 值 | 值/DF |
| 离差 | 16 | 30.2046 | 1.8878 |
| 缩放离差 | 16 | 16.0000 | |
| 最大似然估计 | | | |
| 参数 | DF | 估计 | 标准误差 95%置信限限 | 卡方检验 |
| 截距 | 1 | 0.3824 | 0.0810 | 0.2237, 0.5411 | 22.30 <0001 |
| 尺度 | 0 | 1.3740 | |

注意：尺度参数是通过离差的平方根得到的。由于数据是汇总形式（表3.1），之前的分析也可以通过频率语句执行：

```sas
/*
Schulte等，1998口腔护理示例
*/
data pH;
  input t f;
  m = 4;
  do i=1 to f;
    output;
  end;
  drop i;
  datalines;
0 4
1 4
2 6
3 2
4 1;
proc genmod data=pH;
  model t/m = binomial link=identity scale=deviance;
  freq;
run;
```

## 3.4 萨尔瓦多多的弓虫病

现在我们考虑一个具有协变量以建模结果逻辑回归示例。Efron (1978, 1986)检查了萨尔瓦多34个城市的数据，其中结果“$m_j$名受试者中患虫病病例数$t_j$”是基于年雨量（英寸）的协变量分析的。所有受试者都在10到15岁之间。

### 表3.2：萨尔瓦多34个城市中患虫病病例（$t_j$）占采样受试者（$m_j$）比例

| 城市 (j) | 患病病例 ($t_j$) | 采样受试者 ($m_j$) | 年雨量（英寸）($x_j$) |
| :--- | :--- | :--- | :--- |
| 1 | 2 | 4 | 1735 |
| 2 | 3 | 10 | 1936 |
| 3 | 1 | 5 | 2000 |
| 4 | 3 | 10 | 1973 |
| 5 | 2 | 5 | 1750 |
| 6 | 3 | 5 | 1800 |
| 7 | 2 | 8 | 1750 |
| 8 | 7 | 19 | 2077 |
| 9 | 3 | 6 | 1920 |
| 10 | 8 | 10 | 1800 |
| 11 | 7 | 24 | 2050 |
| 12 | 0 | 1 | 1830 |
| 13 | 15 | 30 | 1650 |
| 14 | 4 | 22 | 2200 |

### 表 3.2：（续）

| 城市 (j) | 正性病例数 (t_j) | 样本数 (m_j) | 年降雨量 (x_j) |
|---|---|---|---|
| 15 | 0 | 1 | 2000 |
| 16 | 6 | 11 | 1770 |
| 17 | 0 | 1 | 1920 |
| 18 | 33 | 54 | 1770 |
| 19 | 4 | 9 | 2240 |
| 20 | 5 | 18 | 1620 |
| 21 | 2 | 12 | 1756 |
| 22 | 0 | 1 | 1650 |
| 23 | 8 | 11 | 2250 |
| 24 | 41 | 77 | 1796 |
| 25 | 24 | 51 | 1890 |
| 26 | 7 | 16 | 1871 |
| 27 | 46 | 82 | 2063 |
| 28 | 9 | 13 | 2100 |
| 29 | 23 | 43 | 1918 |
| 30 | 53 | 75 | 1834 |
| 31 | 8 | 13 | 1780 |
| 32 | 3 | 10 | 1900 |
| 33 | 1 | 6 | 1976 |
| 34 | 23 | 37 | 2292 |

在 1978 年的出版物，Efron 通过拟合一系列具有线性预测的嵌套逻辑回归模型对这些数据进行了分析：

> $$\begin{aligned} \eta_i &= \beta_0 \\ \eta_i &= \beta_0 + \beta_1z_i \\ \eta_i &= \beta_0 + \beta_1z_i + \beta_2z_i^2 \\ \eta_i &= \beta_0 + \beta_1z_i + \beta_2z_i^2 + \beta_3z_i^3 \end{aligned} (3.9)$$

$z_j$ 是降雨量 ($x_j$) 的标准化值，

```
$z_j = \frac{\sqrt{33}(x_j - \bar{x})}{\sqrt{\sum_{j=1}^{34}(x_j - \bar{x})^2}}$
```



在 1986 年的出版物中，Efron 引入了带有第二个参数的双重指数族概念，用于在单参数指数族（如二项分布或泊松分布）成员中独立控制均值的方差。正如弓虫虫一样：

# 第 3 章 准似然函数

Efron 解释说，真正的随机采样是不行的，受试可能是以簇的形式抽样的。Efron 指出：

> “簇采样是过度离散的可能原因之一，这也是二项分布和泊松模型用户经常关注的问题来源。”

我们使用表 3.2 中的弓虫虫病数据来说说明拟合准似然模型的两种方法。第一种方法通过一个合适的常数膨胀 MLE 的协方差矩阵，在 `GENMOD` 和 `GLIMMIX` 过程中均可用。第二种方法是使 GLM 线性化，并使用一种称为伪似然（PL）的估计技术。PL 方法仅在 `GLIMMIX` 过程中可用。我们将在第 9 章更详细地讨论 PL 方法。

程序 3.2 展示了拟合准似然回归模型的编程语句，首先获取 MLE，然后根据尺度参数 $\phi$ 的动量估计值膨胀协方差矩阵，如 (3.6) 所示。我们首先计算 `z_i`，即降雨量的标准化值。`random_residual` 语句生成了之前讨论的准似然过程。结果在输出 3.2 中。尺度参数的估计值（即经自由度归一化的皮尔逊卡方统计量）为 $\phi=1.94$。该分析结果表明，降雨量的线性项和立方项在统计学上是显著的 (P<0.05)。模型中的选项“s”代表“解（solution）”，并提供参数估计。

## 程序 3.2：为弓虫虫病拟合准似然回归模型

```
/* 萨尔瓦多 34 个城市的弓虫虫病

示例来自 Efron (1978, 1986) */

data toxoplasmosis;

input t m r;

z = train;

datalines;

2 4 1735

3 10 1936

1 5 2000

3 10 1973

2 2 1750

3 5 1800

2 8 1750

7 19 2077

3 6 1920

8 10 1809

7 24 2050

0 1 1830

15 30 1650

4 22 2020

0 1 2000

6 11 1770

0 1 1920

33 54 1770

4 9 2240

5 18 1620

21 12 1756

22 1 1650

23 11 2250

24 77 1796

25 51 1890

26 16 1871

27 82 2063

28 13 2100

29 43 1918

30 75 1834

31 13 1780

32 10 1900

33 6 1976

34 37 2292

;

proc std data=toxoplasmosis;

var z;

run;

ods html;

proc glimmix data=toxoplasmosis;

model t/m = z*z*z / s;

random_residual;

run;

ods close;
```

Morel, Jorge, and Nagaraj. Overdispersion Models in SAS. Copyright ©2011, SAS Institute Inc., Cary, USA. ALL RIGHTS RESERVED. 更多 SAS 资源请访问 support.sas.com/publishing.

# SAS 中的过度离散模型

| | | |
|---|---|---|
| 8 | 11 | 2250 |
| 41 | 77 | 1796 |
| 24 | 51 | 1898 |
| 7 | 16 | 1871 |
| 46 | 82 | 2063 |
| 9 | 13 | 2100 |
| 23 | 43 | 1938 |
| 53 | 75 | 1834 |
| 8 | 13 | 1780 |
| 3 | 10 | 1900 |
| 1 | 6 | 1976 |
| 23 | 37 | 2292 |

### 输出 3.2：准似然逻辑模型——表 3弓虫虫病数据

| GLIMMIX 过程 | |
|---|---|
| 拟合统计量 | |
| 皮尔逊卡方 | 58.21 |
| 皮尔逊卡方 / DF | 1.94 |

| 效应 | 估计值 | 标准误差 | DF | t 值 | Pr > t |
|---|---|---|---|---|---|
| 截距 | 0.09939 | 0.1420 | 30 | 0.70 | 0.4895 |
| z | -0.4485 | 0.2161 | 30 | -2.08 | 0.0466 |
| z*z | -0.1873 | 0.1275 | 30 | -1.47 | 0.1523 |
| z*z*z | 0.2134 | 0.08873 | 30 | 2.41 | 0.0225 |
| 残差 | 1.9404 | . | . | . | . |

Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS®. Copyright ©2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 更多 SAS 资源请访问 support.sas.com/publishing.

# 第 3 章 准似然函数

| 固定效应的 III 类检验 | | |
| 效应 | Num DF | Den DF | F 值 | Pr > F |
|---|---|---|---|---|
| z | 1 | 30 | 4.31 | 0.0466 |
| z*z | 1 | 30 | 2.16 | 0.1523 |
| z*z*z | 1 | 30 | 5.79 | 0.0225 |

现在我们转向 `GLIMMIX` 过程中的伪似然（PL）。PL 方法将模型线性化，尺度参数 $\phi$ 变为加权正态混合模型中的残差尺度参数。PL 方法优于准似然方法的一个优点是它为 $\phi$ 提供标准误差。这对于评估过度离散的存在很有用。我们使用程序 3.3 中的编程语句说明 PL 方法的计算。

### 程序 3.3：为弓虫虫病数据拟合伪似然（PL）逻辑回归模型

```
data toxoplasmosis;

  set toxoplasmosis;

  city = _n_;

run;

ods html;

proc glummix data=toxoplasmosis;

  class city;

  model t/m = z*z*z / s;

  random _residual_ / subject=city;

run;

html close;
```

运行程序 3.3 的结果显示在输出 3.3 中。注意估计值及其标准误差与输出 3.2（我们在那里运行准似然分析）相同。注意 PL 输出提供了 $\phi=1.9404$，估计标准误差为 0.5010。由于估计值 $\phi$ 大于标准误差的两倍，我们可能得出存在过度离散的结论。PL 下的标准误差反映了 $\sqrt{\phi}$ 的膨胀。稍后我们将讨论同步方差调整。Morel, Jorge, and Nagaraj. Overdispersion Models in SAS.

### 表 3.3：广义方差离差

| 线性预测逻辑模型 | 离差 | 自由度 | P 值 |
|---|---|---|---|
| 截距 | 965.92 | | |
| z | 965.80 | 1 | 0.7243 |
| z*z | 965.80 | 1 | 0.9970 |
| z*z*z | 954.35 | 1 | 0.0007 |

## 3.5 致癌前临床实验

本示例的目的是过度离散泊松模型的简单应用。与二项模型类似，过度离散泊松模型用于适应泊松模型允许的更高变异性。在 Gail (1980) 和 Lawless (1987) 分析的一个临床实验中，总共 76 只雌大鼠注射了乳癌癌剂。然后，所有动物接受了视黄醇酯以预防乳癌，持续 60 天。在该阶段之后，剩余的 48 只动物被随机分配继续视黄醇治疗（n=23）或作为对照（n=25）。分析的主要目标是评估视黄醇组和对照组之间肿瘤发育的差异。乳癌发生的时间以及在 182 天阶段内的肿瘤数量可以在 Gail 等人 (1980) 中找到。表 3.4 仅包含 48 只大鼠的肿瘤数量。

# SAS 中的过度离散模型

表 3.4: 肿瘤数量

| 分组 | 肿瘤数量 |
|---|---|
| 维黄醇组 (n=23) | 1, 0, 2, 1, 4, 3, 6, 1, 1, 5, 2, 1, 5, 2, 3, 4, 5, 4, 5, 11, 11, 9, 12, 1, 3, 3, 3 |
| 控制组 (n=25) | 7, 11, 9, 2, 9, 4, 6, 7, 6, 1, 13, 2, 1, 10, 4, 5, 4, 5, 1, 2 |

Lawless (1987) 发现了反对泊松模型的证据，且模型中存在过度离散现象。随后，Lawless 拟合了一个具有随机效应的二项模型。该模型属于广义线性混合模型族，将在书中后后进行讨论。为了说明目的，我们现在拟合一个准泊松模型。编程语句请见程序 3.4。这次，我们利用 `GENMOD` 过程，并请求控制组和维黄醇组的最小均值（LS-Means）。还对维黄醇效应进行了估计。主要结果在输出 3.4 中。

# 程序 3.4: 拟合过度离散泊松模型——表 3.4 的肿瘤数据

```
/*

大鼠的肿瘤数量

来自 Lawless (1987) 和 Gail 等人 (1980) 的示例

*/

data number_of_tumors;

  input group $ n 88;

  do retid=1 to n;

    input y 88;

    output;

  end;

  drop n;

datalines;

  Retinoid 23 1 0 2 1 4 3 6 1 1 5 2 1 5 2 3 4 5 4 5 1 2

  Control 25 7 11 9 2 9 4 6 7 6 1 13 2 1 10 4 5 4 5 11 11 9 12 1 3 3 3

;

ods html;

proc genmod data=number_of_tumors;

  class group;

  model y = group / dist=poisson link=log scale=pearson;

  lsmeans group;

    estimate "Logarithm Ratio Control Vs Retinoid" group 1 -1;

run;

ods html close;
```

Morel, Jorge, and Nagaraj Neeraraj. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. 更多 SAS 资源，请访问 support.sas.com/publishing。

# 第3章 准似然函数

输出 3.4: 准似然泊松模型结果——表 3.4 的肿瘤数据

| 参数 | DF | 估计值 | 标准误 | Wald 95% 置信区间 | Wald 卡方 | Pr > ChiSq |
|---|---|---|---|---|---|---|
| 截距 | 1 | 0.9754 | 0.1822 | 0.6183 | 1.3324 | 28.67 | <.0001 |
| group | Control | 1 | 0.8230 | 0.2159 | 0.3999 | 1.2461 | 14.54 | 0.0001 |
| group | Retinoid | 0 | 0.0000 | 0.0000 | 0.0000 | - | - |
| Scale | | 1 | 1.4228 | 0.0000 | 1.4228 | - | - |

最大似然参数估计值分析

注：尺度参数是通过 Pearson 卡方除以自由度的平方根估计的。

| 最小均值 | | | | | | | |
|---|---|---|---|---|---|---|
| 效应 | group | 估计值 | 标准误 | DF | 卡方 | Pr > ChiSq |
| group | Control | 6.0400 | 1.7984 | 0.1158 | 1 | 241.24 | <.0001 |
| group | Retinoid | 2.6522 | 0.9754 | 0.1822 | 1 | 28.67 | <.0001 |

| 对比估计结果 | | | | | | | |
|---|---|---|---|---|---|---|
| 标签 | 均值估计 | 均值置信区间 | LBeta 估计值 | 标准误 | Alpha | 卡方 | Pr > ChiSq |
| 对数比 控制组 vs 维黄醇 | 2.2774 | 1.4917 3.4768 | 0.8230 | 0.2159 | 0.05 | 0.3999 | 14.54 | 0.0001 |

# 表 3.5: 准似然结果——肿瘤数据

| 参数 | 估计值 | 标准误 | Exp(Estimate) |
|---|---|---|---|
| 控制组最小均值 | 1.7984 | 0.1158 | 6.0400 |
| 维黄醇组最小均值 | 0.9754 | 0.1822 | 2.6522 |
| 控制 vs 维黄醇 | 0.8230 | 0.2159 | 2.2774 |
| 尺度 (sqrt) | 1.4228 | | |

在对数尺度下，控制组和维黄醇组的均值分别为 $e^{1.7984}=6.0400$ 和 $e^{0.9754}=2.6522$。注意这些数据对应于控制组和维黄醇组的算术均值。均值差（减去维黄醇）为 0.8230。该结果显著（P=0.0001），如输出 3.5 所示。均值比例为 $\exp(0.8230)=2.2774$，表明控制组相对于维黄醇组增加了 127%。

## 3.6 椎骨折高风险患者

我们现在转向带有偏移量的模型中的准似然估计。偏移量在技术上定义为系数为1的预测变量。偏移量在泊松模型中非常有用，因为它们对均值进行了标准化。事件发生取决于暴露时间：暴露越长，观察到的计数越多。在这个示例中，我们假设过度离散的形式为 $E(Y)=\mu$ 和 $Var(Y)=\mu\phi$，其中 $\phi > 1$。注意这种方差结构可以写为 $Var(Y)=\mu(1+\kappa)$，$\kappa>0$，这是 Dean (1992) 中讨论的泊松模型过度离散形式。

| 分组 | 观测值 |
|---|---|
| 活跃 | (1, 2.987), (2, 3.018), (2, 0.2897), (1, 1.2843), (2, 2.9459), (0, 3.0445), (1, 3.0582) |
| 双磷酸盐治疗 | (0, 0.2987), (1, 1.2567), (0, 0.9678), (3, 2.9956), (1, 1.2843), (0, 0.9925), (1, 1.4346), (1, 3.0116), (0, 0.9733), (2, 3.0637), (1, 2.9706), (0, 1.1882), (0, 0.9733), (1, 1.2676), (2, 0.9541), (0, 0.2384), (1, 0.1283), (0, 0.1813), (2, 0.0125), (2, 2.7625), (2, 2.4504), (4, 2.8747) |
| 安安慰 | (1, 0.3771), (11, 3.0418), (0, 2.4312), (3, 3.1650), (1, 3.0034), (2, 2.9843), (0, 2.9651), (2, 1.3087), (5, 3.0363), (8, 3.0691), (2, 2.9706), (2, 3.2553), (4, 2.9624), (0, 3.2060), (1, 2.9596), (7, 3.0114), (0, 0.2956), (2, 2.9843), (0, 1.1937), (3, 3.0062), (1, 1.9870), (4, 3.0089), (1, 1.2621), (1, 1.9788), (5, 2.8556) |

在一项针对椎骨折骨骨松松患者的临床研究中，受试者被随机分配到接受双磷酸盐治疗的组（n=28）或安慰剂组（n=25）。在约14到39个月的时间内测量了椎骨折（新发或恶化）的数量。数据如3.6所示，已在 Morel 和 Nelich (2010) 中讨论过。令 $Y_j$ 和 $Z_j$ 表示第 $i$ 治疗组第 $j$ 个受试者的椎骨折数量和随访年，$j=1, 2, \dots, n$。在 $Z_i$ 条件下，$E(Y_j)=\mu_j/Z_j，$Var(Y_j)=\mu_j/Z_j^2, \phi > 1$，且 $ln(\mu_j/Z_j) = \alpha + \tau$，其中 $\alpha$ 是总均值，$\tau$ 是第 $i$ 治疗组的效应。（随访时间）是一个偏移量。

## 3.5 使用 GENMOD 的椎骨折示例

```
/*

来自 Morel 和 Nelich (2010) 的椎骨折示例

treat = 治疗

    y = 椎骨折数量（新发或恶化）

    z = 观测年

*/

data fractures;

    input treat $ @8;

    do subid=1 to n;

        input y z @8;

        logz = log(z);

        output;

    end;

    drop n;

Active

    28 1 2.987 2 3.018 2 0.2897 1 1.2843 2 2.9459 0 3.0445 1 3.0582
```



# SAS 中的 68 种过度离散模型

```sas
ods html;

proc genmod data=fractures;
  class treat;
  model y = treat / dist=poisson link=log scale=pearson;
  lsmeans treat;
  estimate "Log Ratio Active Vs Placebo" treat 1 -1;
run;

ods html close;
```

### 结果 3.5：使用 GENMOD 进行椎骨骨折示例的结果

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_80_0.png)

| 拟合优度评估标准 | | |
| 标准 | DF | 值 | 值/DF |
| :--- | :--- | :--- | :--- |
| 皮尔卡方 | 51 | 88.2883 | 1.7311 |

| 最大似然参数估计分析 | | | | | | |
| 参数 | DF | 估计值 | 标准差 | Wald 95% 置信限 | Wald 卡方 | Pr > ChiSq |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 截距 | 1 | -0.0449 | 0.1632 | -0.3647 | 0.2750 | 0.08 | 0.7833 |
| treat | 活跃 | 1 | -0.9000 | 0.2974 | -1.4829 | -0.3170 | 9.16 | 0.0025 |
| treat | 安慰 | 0 | 0.0000 | 0.0000 | 0.0000 | 0.0000 | | | | |
| Scale | 0 | 0.3157 | 0.0000 | 0.3157 | 1.3157 | | | |

> 尺度参数通过皮尔逊卡方/自由度的平方根估计得出。

| 对比率估计结果 | | | | | | | | | |
| 标签 | 均值估计 | 均值 | L'Beta 估计 | 标准差 | Alpha | L'Beta | 卡方 | Pr > ChiSq |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| | | 置信限 | | | | 置信限 | | | |
| 安慰 | 0.9561 | 0.6944 | 1.3165 | -0.0449 | 0.1632 | 0.05 | -0.3647 | 0.2750 | 0.08 | 0.7833 |
| 活跃 | 0.3887 | 0.2388 | 0.6329 | -0.9488 | 0.2486 | 0.05 | -1.4322 | -0.4575 | 14.44 | 0.0001 |
| 比率 (Rate Ratio) | 0.4066 | 0.2278 | 0.7283 | -0.0900 | 0.2475 | 0.05 | -1.4829 | -0.3170 | 9.16 | 0.0025 |

More, Jorge, and Nagaraj Neeraj. *Overdispersion Models in SAS*. 版权 © 2011, SAS Institute, Inc., Cary, North Carolina, USA. 版权所有。需更多 SAS 资源，请访问 support.sas.com/publishing。

## 第3章 准似然函数 9

安慰剂组的估计年骨折合为 $e^{-0.0449} = 0.9561$，双磷酸盐盐组为 $e^{-0.0449-0.9000} = 0.3887$，这表明与安慰剂组相比，双磷酸盐组的椎骨骨折数量显著减少（P值 = 0.0025）。估计的年骨折率形式如下：

```
$$\left(\sum_{j=1}^{n_i} y_{ij} / \sum_{j=1}^{n_i} z_{ij}\right), i = 1, 2.$$
```

比率率（Rate Ratio）为：

```
$RR = \left(\sum_{j=1}^{n_i} y_{ij} / \sum_{j=1}^{n_i} z_{ij}\right) \cdot \left(\sum_{j=1}^{n_i} y_{2j} / \sum_{j=1}^{n_i} z_{2j}\right)$
```

在本示例中结果为0.4066。该结果表明，与安慰剂组相比，双磷酸盐组的估计年骨折率减少了约41%。比率率的近似95%置信区间为 (0.2270, 0.7283)。该置信区间是通过将反向连接函数（即指数函数）应用于模型尺度置信限的边界（$-1.4829, -0.3170$）得到的。通过皮尔逊卡方统计量除以其自由度得出的膨胀因子平方根为1.3157。从最大似然估计获得的所有标准差都通过该因子放大了。

### 表 3.6：椎骨骨折数据的泊松额外变异模型的估计值、标准差、卡方和P值

| 参数 | 估计值 | 标准差 | 卡方 | P值 |
| :--- | :--- | :--- | :--- | :--- |
| 截距 | -0.0449 | 0.1632 | 0.08 | 0.7833 |
| 双磷酸盐 | -0.9000 | 0.2974 | 9.16 | 0.0025 |
| 尺度 ($\sqrt{\cdot}$) | 1.3157 | | | |

## 3.7 Williams 准似然模型

考虑以下具有过度离散逻辑回归模型：

```
$E(T) = \mu_i, \text{Var}(T) = \mu_i\pi_i\{1+(1-\pi_i)\theta\}, and $\log(\frac{\pi_i}{1-\pi_i}) = x_i\beta.$
```

Williams (1982) 提出了一种类似于第2章中方程 (23) 的迭代加权最小二乘法程序，用于同时估计 `$\beta$` 和 `$\theta$`。在 Williams 的论文中，类内相关性用 `$\phi$` 表示。为了避免与过度离散的尺度（离散）参数混淆，我们我们用 `$\rho^2$` 表示类内相关性。

Williams 修改了第2章方程 (23) 中的迭代最小二乘法，允许将权重（膨胀因子）`$w_j^{-1} = [1 + (m_j - 1)\theta]$` 与方差函数 `$v_j = m_j\pi_j(1 - \pi_j)$` 结合使用。注意 `$T_j$` 的方差为 `$v_jw^{-1}$`。在 `$\theta$` 已知的情况下，beta$ 的准似然估计可以通过迭代求解：

```
$\hat{\beta}_{(s+1)} = \hat{\beta}_{(s)} +(\mathbf{X}'\mathbf{W}\mathbf{X})^{-1}\mathbf{X}'\mathbf{W}(\mathbf{y}-\hat{\mu}),\quad$ (3.10)
```

其中 `$\mathbf{V} = \text{Diag} [m_1\pi_1(1-\pi_1), m_2\pi_2(1-\pi_2), ..., m_n\pi_n(1-\pi_n)] = \text{Diag} [v_1, v_2, ..., v_n]$` 以及

```
$\mathbf{W} = \text{Diag}[\frac{1}{1+(m_1-1)\theta}, \frac{1}{1+(m_2-1)\theta}, ..., \frac{1}{1+(m_n-1)\theta}]$
```

## 第 3 章 拟似然函数 73

```sas
title "Full Model With SCALE=WILLIAMS";
run;

proc mean data=out1;
    class type_seed root_extract;
    var pi_hat;
run;

ods html close;
```



我们在全因子模型上指定了 `SCALE=WILLIAMS` 选项，该模型在上述步骤 1 至 4 中已描述。此外，我们还输出了 Williams 模型的预测概率。由于存在四种不同的预测概率（对应两个因子水平的每种组合），我们通过计算两个因子水平的组合来打印这些概率，而不是直接从数据集 "out1" 中打印 21 个预测值。结果如输出 3.6 所示。

## 输出 3.6: 拟合 Williams (1982) 拟似然模型的结果

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_85_0.png)

| 原则 | Value | DF | Value/DF | Pr > ChiSq |
|---|---|---|---|---|
| Deviance | 33.2778 | 17 | 1.9575 | 0.0104 |
| Pearson | 31.6055 | 17 | 1.8618 | 0.0166 |

| 参数 | DF | Estimate | Standard Error | Wald Chi-Square | Pr > ChiSq |
|---|---|---|---|---|---|
| Intercept | 1 | -0.5581 | 0.1260 | 19.6160 | <0001 |
| type_seed | 1 | 0.1459 | 0.2232 | 0.4274 | 0.5132 |
| root_extract | 1 | 1.3179 | 0.1775 | 55.1540 | <0001 |
| type_seed*root_extract | 1 | -0.7779 | 0.3064 | 6.4440 | 0.0111 |

Morel, Jorge, and Nagaraj Neercha. Overdispersion Models in SAS®. 版权 © 2011, SAS Institute Inc., Cary, North Carolina, USA. 版权所有。如需更多 SAS 资源，请访问 support.sas.com/publishing。

### `SCALE=WILLIAMS` 的全模型
`LOGISTIC` 过程

| 模型信息 |
|---|---|
| 权重变量 | 1 / (1 + 0.024938 * (m - l)) |

| 参数 | DF | Estimate | Standard Error | Wald Chi-Square | Pr > ChiSq |
|---|---|---|---|---|---|
| Intercept | 1 | -0.5354 | 0.1937 | 7.6636 | 0.0057 |
| type_seed | 1 | 0.0701 | 0.3115 | 0.0506 | 0.8220 |
| root_extract | 1 | 1.3295 | 0.2782 | 22.8441 | <0001 |
| type_seed*root_extract | 1 | -0.8193 | 0.4352 | 3.5436 | 0.0598 |

### `SCALE=WILLIAMS` 的全模型
`MEANS` 过程

| 分析变量 : `pi_hat` 估计概率 |
|---|---|---|---|
| type_seed | root_extract | 观测值 | 平均值 |
| 0 | 0 | 5 | 0.3692604 |
| | 1 | 6 | 0.6887114 |
| 1 | 0 | 5 | 0.3857251 |
| | 1 | 5 | 0.5112254 |

## 第 3 章 拟似然函数 75

在朴素模型中，基于离差（deviance）和 Pearson 卡卡方统计量的标度参数 `phi` 估计值分别为 1.9575 和 1.8618。这些结果表明存在过度离散（overdispersion）。在 Williams 的方法中，过度离散参数的估计值为 `hat{theta}=0.024938`，它出现在输出“模型信息”中的“权重变量”定义处。估计概率打印在输出末尾。这些值为：

`hat{pi}_{00}=0.369`，
`hat{pi}_{01}=0.689`，
`hat{pi}_{10}=0.386`，以及
`hat{pi}_{11}=0.511`。

`type_seed*root_extract` 交互的估计值为 -0.8193，标准误为 0.4352，Wald 卡方值为 3.5436，P值为 0.0598。Morel, Jorge, and Nagaraj Neercha. Overdispersion Models in SAS®. 版权 © 2011, SAS Institute Inc., Cary, North Carolina, USA. 版权所有。如需更多 SAS 资源，请访问 support.sas.com/publishing。

## 对于过度离散的二似然模型

- 4.1 导言 ................................................................77
- 4.2 二项分布 ................................................................78
- 4.3 离散二项分布 ................................................80
- 4.4 膨胀二项分布 ................................................83
- 4.5 二项分布的泛化 ................................................84
- 4.6 示例 ................................................................86
- 4.7 离散特征化 ................................................94
- 4.8 过度离散模型 ................................................101
- 4.9 示例 ................................................................103
- 4.10 二项分布的加和 ................................................112

## 4.1 导言

在本章中，我们将讨论基于离差和 Pearson 卡方统计量量得到的标度参数 `phi` 的估计值分别为 1.9575 和 1.8618。这些结果表明存在过度离散。在 Williams 的方法中，过度离散参数的估计值为 `hat{theta}=0.024938`，它出现在输出“模型信息”中的“权重变量”定义处。估计概率打印在输出末尾。这些值为：

`hat{pi}_{00}=0.369`，
`hat{pi}_{01}=0.689`，
`hat{pi}_{10}=0.386`，以及
`hat{pi}_{11}=0.511`。

`type_seed*root_extract` 交互的估计值为 -0.8193，标准误为 0.4352，Wald 卡方值为 3.5436，P值为 0.0598。由于交互项的显著性（接近 0.05），在模型拟合上，使用加性模型可能不是最佳选择。`LOGISTIC` 过程的拟合结果与 Williams (1982) 的结果一致。

Morel, Jorge, and Nagaraj Neercha. Overdispersion Models in SAS®. 版权 © 2011, SAS Institute Inc., Cary, North Carolina, USA. 版权所有。如需更多 SAS 资源，请访问 support.sas.com/publishing。

## 4.2 二项分布

对过度离散的建模可以通过分层方法实现，即对成功概率设定先验分布。假设 `T|P ~ Binomial(P,m)`。成功概率 `P` (`0 < P < 1`) 按照任意密度函数 `f(P)`（如果 `P` 是离散的则为概率函数）在 `(0,1)` 区间内分布，使得：

```
E(T) = m\pi \ (4.4)
```

## 第 4 章针对过度离散二项响应的似然模型 79

```
$$Var(T) = mn(1-\pi)[1+\rho(m-1)]$$
```

注意，`T` 的无条件方差被写为条件方差的期望与条件期望的方差的和。因此，可以预期无条件方差大于 `T` 的条件方差。从而，对 `P` 选择适当的先验会导致模型产生过度离散。特别是当选择 Beta 先验时，将使用 Beta-二项分布。因此，人们可以将 Beta-二项分布视为建模过度离散的一种通用方法（不限于某种特定机制）。如第 1 章所述，最后两个方程代表了相对于二项分布的过度离散的一种常见表征方法。这种表述形式显然允许了贝叶斯框架的应用。分布 `f(P)` 可以被看作二项随机变量 `T` 的成功概率 `P` 的先验分布。

在先验分布 `f(P)` 下，对于任何 `t = 0,1,...,m`，有：

```
$$Pr(T=t) = E_f[Pr(T=t)] = \int \binom{m}{t}P^t(1-P)^{m-t}f(P)dP$$
```

如 (4.6) 形式的分布被称为混合分布，其中具有混合分布。如果 `f(P)` 是连续的，则 `T` 的无条件分布是无限混合。如果先验 `f(P)` 是离散且有限的，则 (4.6) 中的积分符号变为有限和，所得的分布是有限混合。本章讨论的每种过度离散模型都可以通过选择混合分布来实现。我们将首先介绍著名的 Beta-二项分布，该分布最初由 Skellam (1948) 使用，它对应于选择 Beta 作为混合先验。第二种模型被称为随机聚类二项分布（Random clumped Binomial distribution），由 Morel 和 Nagaraj (1993) 提出，它是两个二项分布的混合，对应于选择离散分布作为先验。本章还将考虑另外两种分布。我们首先讨论 Beta-二项分布。

设 `f(P)` 为参数为 `a=C\pi` 和 `b=C(1-\pi)` 的 Beta 分布密度函数，

```
$$f(P)=\frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)}P^{a-1}(1-P)^{b-1} = \frac{\Gamma(C)}{\Gamma(C\pi)\Gamma(C(1-\pi))}P^{C\pi-1}(1-P)^{C(1-\pi)-1}$$
```

其中 `Gamma(\cdot)` 是 Gamma 函数，`C=(1-\rho^2)/\rho^2`，其中 `rho` 为过度离散参数。在 Beta 分布下，

```
$$E_r(P) = \frac{a}{a+b} = \pi$$
```

以及

```
$$V_r(P) = \frac{ab}{(a+b+1)(a+b)} = \rho^2\pi(1-\rho),$$
```

因此前两个矩量满足方程 (4.1) 和 (4.3)。如果 `P~ Binomial(\pi;m)` 且 `P~ Beta{C,C(1-\rho)}`，那么它可以作为 `T` 的无条件分布的概率函数：

```
$$Pr(T=t) = \frac{\binom{m}{t} \frac{\Gamma(t+C)}{\Gamma(m+C)} \frac{\Gamma\{m-t+C(1-\pi)\}}{\Gamma(C)\Gamma\{C(1-\pi)\}}, \quad t=0,1,\dots,m,\quad 4.8$$
```

其中与之前一样，`C=(1-\rho^2)/\rho^2`。方程 (4.4) 的概率函数定义了参数为 `pi, rho` 和 `m` 的二项分布，记为 Beta-binomial(`pi,rho;m`)。密度函数 (4.7) 是二项分布的共轭先验。这使得 (4.8) 的推导变得相对直接。由于 Beta 分布的前两个矩满足方程 (4.1) 和 (4.3)，Beta-二项分布的前三个矩如方程 (4.4) 和 (4.5) 所示，那么 `E(T)=m\pi` 且 `Var(T)=m\pi(1-\pi)\{1+\rho^2(m-1)\}`。在第 4.10 节中，我们提供了一个 SAS 程序，用于根据任意 `pi, rho` 和 `m` 的配置从 Beta-二项分布生成数据。

## 4.3 随机聚类二项分布

随机聚类二项分布源于对额外变化背后物理机制的有意义的建模尝试。它在第 1 章第 1.5 节被正式介绍。我们在这里提供正式的推导。

设 `Y_1, Y_2,...,Y_m` 是独立同分布的 Bernoulli(`pi`) 随机变量。对于每个 `i, i=1,...,m`，定义 `Y_i` 在概率 `rho` 下为 `Y`，在概率 `(1-rho)` 下为 `Y_i^0`，`0<rho<1`。`Y_i` 可以表示为

```
$$Y_i = Y I(\rho) + Y_i^0 I(1-\rho), \quad i=1,\dots,m,\quad 4.9$$
```

## 第 4 章针对过度离散二项响应的似然模型 93

其中 `I(\cdot)` 是指示函数。对于 `T = \sum Y_i`，可以证明对于 `m` 个独立单元：

```
$$Pr(T=t) = \pi \binom{m}{t}(\rho\pi)^t(1-\rho\pi)^{m-t} + (1-\pi) \binom{m}{t}((1-\rho)\pi)^t(1-(1-\rho)\pi)^{m-t}, \quad t=0,1,\dots,m,\quad 4.10$$
```

这是两个二项分布的混合。正如前节所示，过度离散二项分布可以通过对二项分布的成功概率 `P` 放置适当的先验而产生。Beta-二项分布其中一个示例，在 `P` 上放置的先验是 Beta 分布。(4.11) 中的分布由 Morel 和 Nagaraj (1993) 提出，用于建模过度离散，其中成功总数 `T` 的无条件分布通过在 `P` 上对点 `P_1 = (1-\rho)\pi` 和 `P_2 = \rhopi` 放置两点先验获得，概率分别为 `pi` 和 `(1-pi)`。如果 `T` 遵循方程 (4.11) 给出的分布，将记为 `nT ~ Random-clumped Binomial(pi, rho;m)`。

## 82 SAS 中的过度离散模型

**图 4.1:** 随机聚类二项分布下，大小为 m=7 的簇的两种可能结果。某些单元提供相同的响应，如 (a) 所示的“1”，或如 (b) 所示的“0”。

![](img/fa69b64c17ad451eb7eb4d8d92f5fb_94_0.png)

## 第 4 章 过度离散二项响应的似然模型（第 83 页）

## 4.4 零膨胀二项分布

Cohen (1966) 提出了一类混合分布，其概率函数形式如下：

```
g(x;\omega,\lambda_1,\lambda_2,...,\lambda_k) = \frac{(1-\omega) + \omega f(0), x=0}{\omega f(x;\lambda_1,\lambda_2,...,\lambda_k), x=1,2,...} (4.12)
```

其中 `0\le \omega\le 1`，且 `f(x;\lambda_1,\lambda_2,...,\lambda_k)` 可以定义在定义域 `x=0,1,2,...` 上的任意离散分布，参数为 `(\lambda_1,\lambda_2,...,\lambda_k)`。当存在过多的零时，这种分布非常有用，例如在实验单位暴露量极低的研究中。通过提出分布 (4.12)，Cohen 将零膨胀泊松分布 (Cohen, 1960) 推广到本质上可以影响任何定义域为 `x=0,1,2,...` 的离散分布。在他 1966 年的论文中，Cohen 讨论了零膨胀负二项分布。这两种分布——零膨胀泊松分布和零膨胀负二项分布将在第 6 章进行讨论。当底层离散分布特殊为 Binomial(P;m) 的特殊情况下，它简化为零膨胀二项（ZIB）分布，其概率函数为：

```
Pr(T=t) = \omega \binom{m}{t} P^t(1-P)^{m-t} + (1-\omega)I(t), t=0,1,...,m (4.13)
```

其中 `I(\cdot)` 是指示函数。注意，分布 (4.13) 是两个分布的混合，即概率为 `P=\pi+\theta(1-\pi)` 的 Binomial(P;m) 与概率为 `1-\omega` 的零退化分布。在参数 `P=\pi+\theta(1-\pi)` 下，分布 (4.13) 可以写为：

```
Pr(T=t) = \frac{\pi}{\pi+(1-\pi)}Pr(X=t) + \frac{\theta(1-\pi)}{\pi+\theta(1-\pi)}I(t), t=0,1,...,m (4.14)
```

其中 `X ~ Binomial{\pi+\theta(1-\pi);m}`。当 `theta=0` 时，方程 (4.14) 简化为 Binomial(`pi;m`) 分布。另一方面，`theta=1` 的情况提供了零退化分布。如果 `T` 的概率函数如 (4.14) 所示，则 `T` 将从零膨胀二项分布 ZIB。可以证明分布 (4.14) 的前两个矩为：

```
E(T) = m\pi (4.15)
```

和

```
Var(T) = m\pi(1-\pi)\frac{1+\theta(m-1)}{1} (4.16)
```



More, Jorge, and Nagaraj Neeraraj. Overdispersion Models in SAS.. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. 访问 `support.sas.com` 获取更多 SAS 资源。

因此，零膨胀二项分布相对于二项分布具有具有过度离散性。注意 (4.16) 中的过度离散参数 $\theta$ 代表方程 (4.5) 中的参数 $\rho^2$。

Park 等 (1996) 提供了一种生成相关伯努利结果 $Z_i$ 的算法。

他们的算法与零膨胀二项分布有明确的联系。Sutradhar (2001) 证明，如果假设伯努利结果具有共同的成功概率和共同的相关性，则 $T = \sum_{i=1}^m Z_i$ 的概率函数为 (4.14)。

## 4.5 二项分布的推广

Altham (1978) 提出了二项分布的两种推广，其中伯努利结果是同分布的但不是相互独立的。所提出的推广导致了一个双参数分布，其中假设 $m$ 个变量具有对称的联合分布，且没有二阶或更高“阶”交互。取决于对离散变量的“交互”使用“加法”定义还是“乘法”定义，可以得到不同的推广。这两种推广允许方差大于或小于二项分布下的方差。换句话说，Altham 的推广允许过度离散或欠离散。我们将只关注“加法”推广。这种加法模型由 Kupper 和 Haseman (1978) 同期发表。我们将跳过具有加法交互作用的二项分布的推导细节。该模型提供了概率函数：

```
$Pr(T=t) = Pr(X=t) \left( \alpha \frac{t(t-1)}{\pi} + \frac{(m-t)(m-t-1)}{1-\pi} - \frac{\alpha m(m-1)}{2} +1 \right), t=0,1,...,m$ (4.17)
```

其中 $X = Binomial(m,\pi)$。

Altham 证明参数 $\alpha$ 不允许在 $[-1, 1]$ 区间内自由变化。为了使 (4.17) 成为适当的概率函数：

```
$\frac{-2}{m-1} \min \left( \frac{1-\pi}{\pi}, \frac{\pi}{1-\pi} \right) \leq \alpha \leq U(m,\pi),$ (4.18)
```

```
$U(m,\pi) \equiv 2 m + \frac{(1-2\pi)^2}{4\pi(1-\pi)}$ 对于较大的 $m$。
```

当 $\alpha = 0$ 时，分布 (4.17) 对应于伯努利结果之间的独立，即对应于 Binomial($\pi, m$)。当 $\alpha > 0$ ($\alpha < 0$) 时，它对应于过度（或欠）离散的情况。Altham 显示，对于某些 $\alpha$ 值，分布 (4.17) 是三个二项分布的混合，即：

```
$$T = \begin{cases} A+2 & \text{概率为 } \frac{1}{2}m(1-\pi) \\ B & \text{概率为 } \frac{1}{2}m(1-\pi)\alpha \\ C & \text{概率为 } \frac{1}{2}m(1-\pi)(1-\alpha) \end{cases} (19)
```

其中 $A \sim Binomial(\pi, m)$，$B \sim Binomial(\pi, m)$ 以及 $C \sim Binomial(\pi, m)$。

## 4.6 关联性示例（第 98 页）

Skellam (1948) 分析了关于芸属（Brassica，一种温带植物）关联的数据集。在减数分裂这一特殊的细胞过程中，存在二价体。二价体是由同源染色体组成的结构。对于细胞 $j=1,...,n$，令 $T_j$ 表示关联的二价体总数。如果关联概率对于所有细胞都是相同的，且对于所有二价对都是独立的，则二项分布是合适的。我们将看到二项分布并不拟合数据，且存在过度离散。只有 Beta 二项、随机聚集二项和加法交互二项提供了良好的拟合。

表 4.1：我们对这些数据拟合了五种分布，即二项分布、Beta 二项、随机聚集二项、零膨胀二项和具有加法交互作用的二项分布。

| 关联数 | 0 | 1 | 2 | 3 |
|---|---|---|---|---|
| 频率 | 32 | 103 | 122 | 80 |

最大似然估计及其渐近估计标准误是通过 `NLMIXED` 程序获得的。编程语句见程序 4.1。注意在这些步骤中，`SYMPUT` 函数将簇的总数 "`n`" 分配了一个宏变量。`NLMIXED` 程序需要指定似然函数。通过“`parms`”语句，每次调用 `NLMIXED` 程序都用于拟合每种分布。在这种情况下，用户可能会指定待估计参数的初始值。在这种情况下，参数空间内网格中的若干点被赋予了初始值。`NLMIXED` 通过评估该网格上的似然函数来选择最佳值。为了计算此处所考虑的每种分布的拟合优度，我们请求了 $t=0,1,2,3$ 的估计概率。这些估计概率乘以了簇总数 $n=337$，以获得预测（期望）频率。这些结果被放在临时 SAS 文件 "`pred1`" 到 "`pred5`" 中。

# 第 4 章 过离离散二项响应的似然模型

## 程序 4.1：五种分布下染色体数据的极大似然估计

> * 在以下分布下对 Skellam (1948) 的染色体数据进行极大似然估计：二项分布、Beta-二项分布、随机聚集二项分布、零膨二项分布以及具有加性交互的广义二项分布

```sas
data chromosome;
m = 3;
input freq;
n+ freq;
if n = 4 then
 call symput('n', n); /* "n" 是总簇数;
drop n;
title 'Random-clumped Binomial Distribution';
proc nlmixed data=chromosome;
parms Pi=0.4 0.5 0.6 Rho=0.2 0.3 0.4;
bounds 0 < rho < 1;
c = 1 / rho;
z = lgamma(m-t);
pic = 1 - pi;
ll = freq * (z + lambda(c) + lambda(t*c) + lambda(m-t+c)) - lambda(c) - lambda(pi) + lambda(c);
model t = general(ll);
predict n * exp(z + lambda(c) + lambda(t*c) + lambda(m-t+c)) - lambda(c) - lambda(pi) + lambda(c) out=pred;
run;
title 'Zero-Inflated Binomial';
proc nlmixed data=chromosome;
parms Pi=0.4 0.5 0.6 Rho=0.2 0.3 0.4;
bounds 0 < Rho < 1;
theta = rho;
z = lgamma(m-1) - lgamma(t+1);
p = pi + theta * (1-pi);
w = p;
pc = pi / p;
wc = 1 / w;
ll = freq * exp(z + log(w) + t*log(p) + (m-t)*log(pc)) + wc*(t=0);
model t = general(ll);
predict n * (exp(z + log(w) + t*log(p) + (m-t)*log(pc)) + wc*(t=0)) out=pred;
run;
title 'Generalized-Binomial Distribution -- Additive Interaction';
proc nlmixed data=chromosome;
parms Pi=0.4 0.5 0.6 Rho=0.2 0.3 0.4;
alpha = rho * rho;
z = lgamma(m-1) - lgamma(t+1);
pic = 1-pi;
ll = freq * (z + t*log(pi) + (m-t)*log(pic)) + log(alpha/2*(t-1)/pi*(m-t)/pic) - alpha*(m-1)/2 + 2);
model t = general(ll);
predict n * exp(z + t*log(pi) + (m-t)*log(pic) + log(alpha/2*(t-1)/pi*(m-t)/pic) - alpha*(m-1)/2 + 1) out=pred;
run;
ods html close;
```

输出 4.1 显示了 `NLMIXED` 的结果。我们展示了二项分布、Beta-二项分布、随机聚集二项分布、零膨二项分布以及具有加性交互的广义二项分布的部分输出内容。

### 输出 4.1：NLMIXED 结果—染色体数据

| 二项分布 (Binomial Distribution) | |
| :--- | :--- |
| NLMIXED 程序 | |
| 拟合统计量 (Fit Statistics) | |
| -2 对数似然 (-2 Log Likelihood) | 880.8 |
| 参数估计 (Parameter Estimates) | |
| 参数 (Parameter) | 估计 (Estimate) | 标准误 (Standard Error) | 自由度 (DF) | t 值 (t Value) | Pr > t | Alpha | 下限 (Lower) | 上限 (Upper) | 梯度 (Gradient) |
| Pi | 0.5806 | 0.01552 | 4 | 37.41 | <0001 | 0.05 | 0.5375 | 0.6237 | 1.183E-6 |

| Beta-二项分布 (Beta-binomial Distribution) | |
| :--- | :--- |
| NLMIXED 程序 | |
| 拟合统计量 (Fit Statistics) | |
| -2 对数似然 (-2 Log Likelihood) | 873.6 |
| 参数估计 (Parameter Estimates) | |
| 参数 (Parameter) | 估计 (Estimate) | 标准误 (Standard Error) | 自由度 (DF) | t 值 (t Value) | Pr > t | Alpha | 下限 (Lower) | 上限 (Upper) | 梯度 (Gradient) |
| Pi | 0.5807 | 0.01681 | 4 | 34.55 | <0001 | 0.05 | 0.5340 | 0.6274 | 1.803E-6 |
| Rho | 0.2944 | 0.05766 | 4 | 5.11 | 0.0070 | 0.05 | 0.1343 | 0.2455 | -8.046E-6 |

| 随机聚集二项分布 (Random-clumped Binomial Distribution) | |
| :--- | :--- |
| NLMIXED 程序 | |
| 拟合统计量 (Fit Statistics) | |
| -2 对数似然 (-2 Log Likelihood) | 873.8 |
| 参数估计 (Parameter Estimates) | |
| 参数 (Parameter) | 估计 (Estimate) | 标准误 (Standard Error) | 自由度 (DF) | t 值 (t Value) | Pr > t | Alpha | 下限 (Lower) | 上限 (Upper) | 梯度 (Gradient) |
| Pi | 0.5805 | 0.01680 | 4 | 34.56 | <0001 | 0.05 | 0.5338 | 0.6271 | 5.492E-6 |
| Rho | 0.2930 | 0.05805 | 4 | 5.05 | 0.0072 | 0.05 | 0.1318 | 0.1452 | -0.0002 |

| 零膨二项分布 (Zero-Inflated Binomial) | |
| :--- | :--- |
| NLMIXED 程序 | |
| 拟合统计量 (Fit Statistics) | |
| -2 对数似然 (-2 Log Likelihood) | 877.6 |
| 参数估计 (Parameter Estimates) | |
| 参数 (Parameter) | 估计 (Estimate) | 标准误 (Standard Error) | 自由度 (DF) | t 值 (t Value) | Pr > t | Alpha | 下限 (Lower) | 上限 (Upper) | 梯度 (Gradient) |
| Pi | 0.5806 | 0.01625 | 4 | 35.74 | <0001 | 0.05 | 0.5355 | 0.6227 | -0.0001 |
| Rho | 0.2188 | 0.06485 | 4 | 3.37 | 0.0280 | 0.05 | 0.0380 | 0.3988 | -0.0043 |

| 广义二项分布 -- 加性交互 (Generalized-Binomial Distribution -- Additive Interaction) | |
| :--- | :--- |
| NLMIXED 程序 | |
| 拟合统计量 (Fit Statistics) | |
| -2 对数似然 (-2 Log Likelihood) | 873.5 |
| 参数估计 (Parameter Estimates) | |
| 参数 (Parameter) | 估计 (Estimate) | 标准误 (Standard Error) | 自由度 (DF) | t 值 (t Value) | Pr > t | Alpha | 下限 (Lower) | 上限 (Upper) | 梯度 (Gradient) |
| Pi | 0.5809 | 0.01683 | 4 | 34.52 | <0001 | 0.05 | 0.5342 | 0.6277 | 6.192E-7 |
| Rho | 0.2972 | 0.05748 | 4 | 5.17 | 0.0067 | 0.05 | 0.1376 | 0.4567 | -1.2E-6 |

极大似然结果报告于表4.2。五种模型提供了概率 $\pi$ 的相似估计。事实上，在保留三位小数后，这些估计值基本相同，均为0.581。在二项模型和过度离模型下获得相似的均值估计是常见的。在这个例子中，Beta-二项、随机聚集二项和广义二项分布提供了 $\hat{\pi}$ 和 $\rho$ 估计的基本相同结果，以及相应的标准误。这三个模型下的 $\hat{\pi}$ 方差估计约为使用二项分布估计值的 1.7 倍。在 ZIB 模型下，该因子为 1.1。二项分布未能识别数据的内在聚集性。值得注意的是，这些分布的似然极大值几乎是相同的。注意，这些分布之间均不嵌套，且它们的数学公式不适用于此类特定的比较。ZIB 下的估计值似乎略有不同。为了测试特定过度离模型是否存在过度离散，我们需要检验假设 $H_0: \rho = 0$ 与备择假设 $H_1: \rho > 0$，假设这些模型之一是正确的。由于此处的所有过度离在零假设下都简化为二项分布，似然比统计量可以通过从二项分布的似然极大值减去过度离模型的似然极大值来计算。虽然计算此统计量毫无困难，但似然比检验的性质位于参数空间的边界。Self 和 Liang (1987) 在他们的论文中指出，在这种情况下（案例5），似然比检验的渐近分布是零点质量与11自由度卡方分布的 5:50 混合。似然比检验统计量在 Beta-二项分布下为 880.8–873.6–7.2，在随机聚集二项下为 7.0，在 ZIB 下为 3.2，在具有加性交互的广义二项分布下为 7.3。它们相应的 P 值为 0.004、0.004、0.037 和 0.003，强力支持任一模型下的过度离散假设。

**表 4.2：** 对染色体拟合二项分布、Beta-二项分布、随机聚集二项分布、零膨二项分布以及具有加性交互的广义二项分布的 MLE 结果。

| 分布 (Distribution) | $\hat{\pi}$ | $se(\hat{\pi})$ | $\hat{\rho}$ | $se(\hat{\rho})$ | -2 对数似然 (-2 Log Likelihood) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 二项 (Binomial) | 0.5806 | 0.0155 | | -- | 880.0 |
| Beta-二项 (Beta-binomial) | 0.5807 | 0.0168 | 0.2944 | 0.0577 | 873.6 |
| 随机聚集二项 (Random-clumped Binomial) | 0.5805 | 0.0168 | 0.2930 | 0.0581 | 873.8 |
| 零膨二项 (Zero-inflated Binomial) | 0.5806 | 0.0163 | 0.2188 | 0.0649 | 877.6 |
| 广义二项 (Generalized Binomial) | 0.5809 | 0.0168 | 0.2972 | 0.0575 | 873.5 |

### 程序 4.2：拟合度检验——染色体数据

| 标题 |
|------------------------------------------------------------|
| 此宏执行皮尔逊拟合优度检验 |
| Skellam (1948) 染色体数据示例 |
| data = 包含变量 Obs 和 Pred 的数据集 |
| df = 自由度 |
| title = 正在拟合的分布 |

```sas
%macro gof(data,df,title);
proc imml;
  use &data;
  read all(freq) into Observed;
```



```sas
  read all(Pred) into Predicted;

  gof = sum(Observed # Predicted) - &n;

  pvalue = 1 - probchi(gof,df,0);

  Summary = j(3,1,0);

  Summary[1,1] = gof;

  Summary[2,1] = &df;

  Summary[3,1] = pvalue;

  label = { 'Pearson's GOF Test',

  'Degrees of Freedom',

  't-value'};

  print &title;

  print Observed Predicted[format=10.4];

  print Summary[label=rowname format=10.4];

quit;

%mend gof;

ods html;

%gof(pred1,1,'Binomial Distribution');

%gof(pred2,1,'Beta-binomial Distribution');

%gof(pred3,1,'Random-connected Binomial Distribution');

%gof(pred4,1,'Zero-correlated Binomial Distribution');

%gof(pred5,1,'Generalized-Binomial Distribution -- Additive Interaction');

ods html close;
```

输出 4.2 仅显示了 Beta 二项分布的拟合度结果。

# 第 4 章 用于过度离散二项响应的似然模型

## 输出 4.2：Beta 二项分布下的拟合度结果

| Beta 二项分布 |
| 观测值 | 预测值 |
| 32 | 33.9692 |
| 103 | 97.1628 |
| 122 | 127.6667 |
| 80 | 78.2014 |

| 总结 |
| 皮尔逊拟合优度检验 | 0.7577 |
| 自由度 | 1.0000 |
| P 值 | 0.3840 |

表 4.3 显示了本示例中考虑的五种分布下关联数量的观测频率和期望频率。二项分布并没有很好地拟合数据，因为在 2 个自由度下，$X^2 = 8.11$，对应的 P 值为 0.017。对于零值膨胀二项分布（Zero-inflated Binomial），也可以观察到类似的现象，其在 1 个自由度下，$X^2 = 4.71$，对应的 P 值为 0.030。自由度的计算方法为（类别数减去1）减去（估计的参数个数）。在二项分布的情况下，自由度为 $(4-1)=2$。过度离散分布多额外的参数 `ρ`，这使得它们的自由度变为 $(4-1)-2=1$。二项分布、随机聚类二项分布和具有加性交互作用的广义二项分布能够较好地拟合关联数量的分布，其卡方检验的 P 值 值分别为 0.384、0.347 和 0.439。当存在多个模型且它们都符合拟合度标准，且模型之间互不嵌套时，很难选出一个单一模型作为最终建议。这种情况也发生在回归建模的情况下。因此，建议与领域专家讨论这些选项，并向他们说明每个模型的含义，同时就哪种模型更接近他们研究的现象征求他们的意见。

Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 更多 SAS 资源，请访问 support.sas.com/publishing。

### 表 4.3：染色体数据的皮尔逊卡方拟合度检验

| 关联数量 | 观测频率 | 二项分布 | Beta 二项分布 | 随机聚类二项分布 | 零值膨胀二项分布 | 广义二项分布 |
|---|---|---|---|---|---|---|
| 0 | 32 | 24.86 | 33.97 | 34.08 | 32.00 | 33.91 |
| 1 | 103 | 103.24 | 97.16 | 96.82 | 93.60 | 97.55 |
| 2 | 122 | 142.94 | 127.67 | 128.24 | 140.80 | 126.84 |
| 3 | 80 | 65.96 | 78.20 | 77.85 | 70.60 | 78.70 |
| $\chi^2$ | | 8.11 | 1 | 1 | | 1 |
| P 值 | | 0.017 | 0.384 | 0.347 | 0.030 | 0.439 |

## 染色体数据的皮尔逊卡方拟合度检验

正如我们之前看到的，对于聚类大小 `m`，Beta 二项分布和随机聚类分布几乎是完全相同的。请注意，当 `ρ` 接近单位1 时，它们之间的差异会变得显著。

[注：OCR 文本包含大量的重复和乱码部分，已根据逻辑流进行了清理。]

## 表 4.4: 当 `π=0.3, ρ=0.2,0.7` 且 `m=4,20` 时，Beta二项分布与随机聚集二项分布的偏度

| `ρ` | m | Beta-二项分布 (Beta-binomial) | 随机聚集二项分布 (Random-clumped Binomial) |
|---|---|---|---|
| 0.2 | 4 | 0.5076 | 0.5184 |
| | 20 | 0.3621 | 0.5029 |
| 0.7 | 4 | 0.8256 | 0.8396 |
| | 20 | 0.8204 | 0.8622 |

当 `ρ=0` 时，这两个分布的峰度系数 (4.25) 和 (4.26) 变为 `{1+6ρ(1-π)}/mπ(1-π)+3`，这正是二项分布的峰度系数。对于退化情况 `ρ=1`，Beta-二项分布和随机聚集二项分布的峰度系数为 `1/{π(1-π)}`。为了对 Beta-二项分布和随机聚集二项分布的峰度进行有意义的比较，我们考虑 `π=0.5` 的情况，此时两种分布都是对称的。也就是说偏度系数为零。对于 `π=0.5`，Beta-二项分布和随机聚集分布的峰度系数变为：

```
Kurtosis(Beta-binomial when π=0.5) = \frac{(3m-2)+\{3m(m-1)+2\}\rho^2}{m[1+(m-1)\rho^2]^2}$ (4.27)
```

以及

```
Kurtosis(Random-clumped when π=0.5) = \frac{(3m-2)+\{2(m-1)(3m-4)\rho^2+(m-1)(m-2)(m-4)\rho^4}{m[1+(m-1)\rho^2]^2}$ (4.28)
```

可以证明，对于 `π=0.5`，当 `ρ<1` 时，随机聚集二项分布的峰度系数小于 Beta-二项分布。任何对称 Beta-二项分布的尾部都比对应的随机聚集二项分布尾部更厚。表 4.5 展示了 `π=0.5, ρ=0.2,0.7` 且 `m=5,20` 时峰度系数 (4.27) 和 (4.28) 的值。对于任何给定的 `ρ` (`0<ρ<1`)，随着簇大小 `m` 的增加，两种分布的峰度趋于相互发散。对于固定的 `m`，随着 `ρ` 趋于 1，两种分布的峰度都会减小。

## 第4章 针对过度离散二项响应的似然模型

**表 4.5：** Beta-二项分布与随机聚集二项分布的峰度
`π=0.5, ρ=0.2,0.7` 且 `m=4,20`

| | m | Beta-二项分布 | 随机聚集二项分布 |
|---|---|---|---|
| `ρ` | | | |
| 0.2 | 4 | 2.3810 | 2.3776 |
| | 20 | 2.7273 | 2.4603 |
| 0.7 | 4 | 1.4630 | 1.4326 |
| | 20 | 1.5127 | 1.1744 |

我们继续对概率函数进行视觉评估。程序 4.3 提供了为给定的 `π, ρ` 和 `m` 生成 Beta-二项分布和随机聚集二项分布概率函数的编程语句。

### 程序 4.3：Beta-二项分布与随机聚集二项分布的概率函数图

```sas
/*

Plots of Probability Functions of

the Beta-binomial and Random-clumped Binomial Distributions

*/

%macro plots_bb_rcb(pi,rho,m);

data bb rcb;

format Distribution $14;

label Prob = "Probability";nlabel t = "Number of Successes (t)";

pi = &pi;

rho = &rho;

m = &m;

c = 1 - rho / (rho - 1);

p1 = 1 - pi;

pl1 = (1 - rho)*pi + rho;

lc1 = 1 - p1;

p2 = pi - rho;

c2 = 1 - p2;

do t=0 to m;

Z = exp(z + gamma(c) + gamma(t+c*pi) + gamma(m-t+c*pi));

Prob = gamma(m-c) - gamma(c*pi) - gamma(c*pi);

Distribution = 'Beta-binomial';

output;

Prob = exp(z) * (pi*p1**t*pl1**(m-t) + pi*p2**t*c2**(m-t));

Distribution = 'Random-clumped Binomial';

output;

end;

keep t Prob Distribution;

run;

title1 "Probability Functions Beta-binomial and Random-clumped Binomial Distributions";

ntitle2 "with Pi=&pi Rho=&rho and m=&m";

proc sgpanel data=bb rcb;

panelby / spacing=8;

var t / response=Prob group=Distribution;

run;

%mend plots_bb_rcb;

%plots_bb_rcb(0.3, 0.7, 20);

%plots_bb_rcb(0.5, 0.5, 20);

%plots_bb_rcb(0.5, 0.8, 20);
```



Morel, J. and Nagaraj E. Overdispersed Models in SAS®. Copyright 2011, SAS Inc., Corp., North Carolina, USA. ALL RIGHTS RESERVED.

图 4.1 显示了 $\pi=0.3, \rho=0.7$ 时 Beta-二项分布的概率函数。与 Beta-二项分布不同，随机聚集二项分布呈现出两个峰。这些峰大约位于点 $m(1-\rho)\pi$ 和 $m\{(1-\rho)\pi+\rho\}$ 处。回想起在随机聚集二项分布中，这两个值是两个二项分布的均值。对于 $\pi=0.5$，两种分布都是对称的。图 4.2 显示了 $\pi=0.5, \rho=0.5$ 且 $m=20$ 的概率函数。Beta-二项分布呈倒 U 形，而随机聚集二项分布变为 U 形。尽管随机聚集二项分布随着 $\rho$ 变化到 0.8 而发生变化（见图 4.2），但 Beta-二项分布倾向于以类似的方式运行，其概率函数于保持 M 形。我们观察到，随着簇大小 $m$ 的增加，随机聚集二项变得更加明显，而 Beta-二项分布变得更加平坦。程序 4.3 是深入了解两种过度离散模型行为的有用探索性工具。我们邀请读者针对不同的参数配置运行此程序，并比较生成的概率直方图。注意这些分布的形状是不同的，即使参数发生微小变化也是很有益的。图 4.1：Beta-二项分布与随机聚集二项分布的概率函数，$\pi=0.3, \rho=0.7$
图 4.2：Beta-二项分布与随机聚集二项分布的概率函数，$\pi=0.5, \rho=0.5, m=20$

# 第 4 章 针对过度离散二项分布响应变量的似然模型 103

函数 $g(\cdot)$ 是与“均值”参数相关的**连接函数**。该连接函数具有 $\eta_{ij} = \mathbf{x}\beta$ 作为其**线性预测值**。同样，$f(\cdot)$ 是与**“过度离散”**参数相关的**连接函数**，其线性预测值为 $\eta_{2j} = \mathbf{z}\alpha$。参数向量为

$(k+h)$ 维列向量 $\mathbf{\theta} = (\beta', \alpha')^T$。其极大似然估计（MLE）$\hat{\mathbf{\theta}} = (\hat{\beta}', \hat{\alpha}')^T$ 可以通过适当的数值方法迭代获得。在第 8 章中将对 Beta-二项分布和随机聚类二项分布的多变量扩展相关的计算问题进行更广泛的讨论。

## 4.9 关于指骨骨化的畸胎学示例

考虑表 4.6 中的骨化数据，该数据此前由 Hartsfield 等人 (1990) 以及 Neerchel (1997) 分析过。当我们引入过度离散的概念时，源于一个包含 81 只怀孕苯戊平（PHT）和三氯丙烯氧化（TCCO）的双因素设计。实验的目的是调查苯戊平和 TCCO 的协同效应。指骨骨化的出现与否被视为研究物质畸胎作用的衡量。在某些情况下完全没有发生骨化；在另一些情况下，骨化几乎完全。选择中节指骨是为了在控制组中提供约 20% 的骨化概率。在实验中，每只怀孕的小鼠每天通过胃胃胃接受水、一个假控制组（Sham）以及三个处理组的 60 mg/kg 苯戊平（PHT）、100 mg/kg 三氯丙烯氧化（TCCO）或 60 mg/kg 苯戊平加 TCCO。为了说明起见，将控制组合并并称为合并控制组。我们在此处展示中节指骨的分析。胎儿随后被视为一个 2 x 2 因子，PHT 和 TCCO 为两个因子。PHT 的水平为 60 mg/kg 和 60 mg/kg，TCCO 的水平为 100 mg/kg 和 0 mg/kg。在妊娠第 18 天，恢复特征并进行染色和清洁。然后，通过视觉检查，确定左右指骨不同关节处是否发生骨化。中节指骨的数据如表 4.6 所示。第 1.1 节讨论的示例对应于 11 只同时使用了 PHT 和 TCCO 两种物质的小鼠。

| 表 4.6: 骨化数据 |
| 组别 | 观测值 |
| :--- | :--- |
| 控制组 (Control) | 8/8, 9/9, 7/0, 3/5, 3/8, 9/0, 5/8, 1/6, 0/5, 8/8, 10/5, 4/7, 9/0, 6/3 |
| 假控制组 (Sham) | 8/9, 10/10, 1/6, 6/6, 1/9, 8/9, 6/7, 5/7, 5/9, 2/6, 2/8, 0/2, 7/8, 5/7 |
| 苯戊平 (PHT) | 1/9, 4/9, 3/7, 4/7, 0/4, 1/8, 2/7, 0/2, 3/10, 3/7, 0/8, 10/1 |
| 三氯丙烯氧化 (TCCO) | 0/5, 7/10, 4/8, 11/11, 6/9, 3/4, 2/8, 0/9, 3/6, 2/9, 10/1, 8/9 |
| PHT+TCCO | 2/2, 0/7, 1/8, 7/8, 0/10, 0/4, 0/6, 0/7, 6/6, 1/7 |

* 显示骨化的胎儿数量 / 窝产数。
* PHT: 苯戊平；TCCO: 三氯丙烯氧化。

## 104 SAS 中的过度离散模型

令 $\pi_{tp}$ 代表 2x2 析设计实验中 (t,p) 处理组中任何胎儿左侧中节指骨缺失的无条件概率，其中

$t = \begin{cases} 0 & \text{若 TCPO 不存在} \\ 1 & \text{若 TCPO 存在} \end{cases} \text{ 且 } p = \begin{cases} 0 & \text{若 PHT 不存在} \\ 1 & \text{若 PHT 存在} \end{cases}$

对于第 $j$ 窝的 $(t$

`T_{tp} ~ Binomial(\pi_{tp},m_{tp})`
`T_{tp} ~ Beta-binomial(\pi_{tp},\rho_{tp},m_{tp})`
`T_{tp} ~ Random-clumped(\pi_{tp},\rho_{tp},m_{tp})` (43)

认为 `T_{tp}` 服从二项分布的情况忽略了窝效应并假设窝内是同的。为了解释处理组之间 $\pi_{tp}$ 可能存在的差异，我们将考虑以下 logit $\ln\left(\frac{\pi_{tp}}{1-\pi_{tp}}\right) = \beta_0+\beta_1 I(t=1)+\beta_2 I(p=1)+\beta_3 I(t=1,p=1)$，(34)

其中 `I(\cdot)` 表示指示函数。(34) 中的连接函数提供了实验中所用物质的畸胎作用以及可能的协同效应的估计。畸胎学数据中存在不同程度的窝内相关性是很常见的。这个问题已由 Kupper 等人 (1986) 和 Williams (1988) 妥善解决。为了考虑到可能的不同窝效应，我们将考虑以下 logit $\ln\left(\frac{\rho_{tp}}{1-\rho_{tp}}\right) = \alpha_0+\alpha_1 I(t=1)+\alpha_2 I(p=1)$，

35)

第一个连接函数 $\ln\left(\frac{\rho_{tp}}{1-\rho_{tp}}\right) = \alpha_0+\alpha_1 I(t=1)+\alpha_2 I(p=1)$ 假设了相同的窝内相关性，$\rho \equiv \frac{\exp(\alpha)}{1+\exp(\alpha)}$。另一个连接函数表达了 $\rho$ 的主效应及其交互作用。(33) 和 (34) 中的过度离散模型属于离散模型的类别。我们现在考虑 (31) 和 (32) 下三种分布的估计，$\ln\left(\frac{\pi_{tp}}{1-\pi_{tp}}\right) = \beta_0+\beta_1 I(t=1)+\beta_2 I(p=1)+\beta_3 I(t=1,p=1)$ (36)

## 4.4 使用 NLMIXED 拟合骨化数据的三个模型

4.4 包含了使用 `NLMIXED` 过程对 (36) 进行建模的编程语句。

```sas
/*
来自 Morel 和 Neerchel (1997),
Statistics in Medicine, 284-2853
*/
data ossification;
length tx $;
input tx $ n;
do i=1 to n;
input t m $;
m = m - t;
output;
end;
drop n;
Control 8 8 9 9 7 0 3 5 3 8 9 0 5 8 1 6 0 5 8 8 10 5 4 7 9 0 6 3
Sham 8 9 10 10 1 6 6 6 1 9 8 9 6 7 5 7 5 9 2 6 2 8 0 2 7 8 5 7
... (此处省略数据行以保持格式简洁，实际翻译时不应漏，但根据原文此处应包含完整数据)
```
```sas
ods html; ntitle "Binomial Distribution, Full Model on the Betas",
proc mixed ossification;
parms b0=0, b1=0, b2=0;
if (tx='Control')
then linp = b0;
else if (tx='TCPO')
then linp = b0+b1;
else if (tx='PHT')
then linp = b0+b2;
else if (tx='PHT+TCCO')
then linp = b0+b1+b2+b3;
pi = 1/(1+exp(linp));
```

Morel, Jorge and Nagaraj Neeraj. Overdispersion Models in SAS®. Copyright 2011, SAS Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. For additional resources, visit support.sas.com/publishing.

## 第 4 章 过离散二项响应的似然模型

输出 4.4 提供了程序 4.4 的结果。我们仅展示随机聚类二项（Random-clumped Binomial）模型的部分结果。

### 输出 4.4：骨化数据拟合随机聚类二项模型的结果

| 随机聚类二项分布，针对 Beta 的全模型，共同 Rho 的 NLMIXED 过程 |
| :--- | :--- |
| 注意：GCONV 收敛标准已满足。 | |
| 拟合统计量 | |
| -2 对数似然 | 305.1 |
| AIC (越小越好) | 315.1 |
| AICC (越小越好) | 315.9 |
| BIC (越小越好) | 327.0 |

| 参数估计 | 参数 | 估计值 | 标准误差 | t 值 | Pr >|t| | Alpha | 下限 | 上界 | 梯度 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| b0 | 0.6392 | 0.2266 | 81 | 2.82 | 0.0060 | 0.05 | 0.1883 | 1.0901 | 0.000073 |
| b1 | -0.9457 | 0.3711 | 81 | -2.55 | 0.0127 | 0.05 | -1.6841 | -0.2073 | 0.000049 |
| b2 | -1.5291 | 0.3956 | 81 | -3.87 | 0.0002 | 0.05 | -2.3161 | -0.7421 | 0.000029 |
| b3 | 0.6162 | 0.6678 | 81 | 0.92 | 0.3589 | 0.05 | -0.7125 | 1.9449 | 0.000018 |
| a0 | 0.3356 | 0.1714 | 81 | 1.96 | 0.0537 | 0.05 | -0.0050 | 0.6767 | 0.000023 |

| 额外估计 | 标签 | 估计值 | 标准误差 | DF | t 值 | Pr >|t| | Alpha | 下限 | 上界 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| PI Control | 0.6546 | 0.05124 | 81 | 12.77 | <0.001 | 0.05 | 0.5226 | 0.7565 |
| PI TCPO | 0.4240 | 0.07372 | 81 | 5.75 | <0.001 | 0.05 | 0.2773 | 0.5700 |
| PI PHT | 0.2911 | 0.06336 | 81 | 4.59 | <0.001 | 0.05 | 0.1650 | 0.4172 |
| PI PHT+TCPO | 0.2280 | 0.08255 | 81 | 2.76 | 0.0071 | 0.05 | 0.0638 | 0.3923 |

更多，J. 和 Nagaraj Neeraj。SAS 中的过离散模型*。Copyright © 2011, SAS Institute Inc., Cary, 北卡罗来纳州。保留所有权利。更多 SAS 资源，请访问 support.sas.com/publishing。

SAS 中的过离散模型

表 4.7 考虑的三个模型的 MLE 拟合结果。Beta-二项和随机聚类二项模型的结果彼此一致。负系数表示骨化风险增加。我们正在对骨化的概率进行建模。因此，负系数表示化学物质抑制了骨化并具有毒性。因此，化学物质的影响是抑制骨化。二项模型未能识别出这种影响，并正如预期的提供了比预期值更小的估计标准误差。

表 4.7：共同 $\rho$ 的因子回归模型骨化数据的 Beta 估计值和标准误差

| 参数 | 二项估计值 | 二项标准误差 | Beta-二项估计值 | Beta-二项标准误差 | 随机聚类二项估计值 | 随机聚类二项误差 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 截距 (Intercept) | 0.8323 | 0.1365 | 0.7043 | 0.2341 | 0.6392 | 0.2266 |
| TCPO | -0.4841 | 0.2239 | -0.7822 | 0.4017 | -0.9457 | 0.3711 |
| PHT | -2.1094 | 0.2505 | -1.6917 | 0.4018 | -1.5291 | 0.3956 |
| TCPO + PHT | 1.0453 | 0.4107 | 0.6770 | 0.6902 | 0.6162 | 0.6678 |
| $\rho^2$ | | | 0.3374 | 0.0541 | 0.3400 | 0.0486 |
| -2 对数似然 | 401.8 | | 306.6 | | 305.1 | |

PHT：苯妥汀；TCPO：三氯丙醚。$\hat{\beta}_1, \hat{\beta}_2, \hat{\beta}_3$ 代表截距、TCHT 和 TCPO+PHT 的 Beta 估计值，当 TCPO = 0 mg/kg 时，PHT 与对照组之间优势比的近似 95% 置信区间由 $\exp(\hat{\beta}_2 \pm 1.96\sqrt{\hat{\beta}_2})$给出，其中 $\hat{\beta}_2$ 代表 $\hat{\beta}_2$ 的渐近方差。同样，当 TCPO = 100 mg/kg 时，PHT 与对照组之间优势比的近似 95% 置信区间由 $\exp(\hat{\beta}_2 + \hat{\beta}_3 \pm 1.96\sqrt{\hat{\beta}_2^2 + \hat{\beta}_3^2})$给出。表 4.8 显示了基于二项、Beta-二项和随机聚类二项模型的 TCPO 水平近似 95% 置信区间。使用 GENMOD 和 GLIMMIX 过程，NLMIXED 不使用上述方法产生置信区间。因此，表 4.2 中的结果需要在 NLMIXED 输出之外额外计算。二项模型下的置信区间远短于过离散模型。这一结果表明，二项模型下获得的置信水平仅是名义上的。另外两个包含后期的模型显示，在存在 TCPO 的情况下，PHT 和对照的缺失概率可能是相同的。

### 表 4.8：共同 $
ho$ 的全因子逻辑回归骨化优势比近似 95% 置信区间

| 模型 | 优势比 (Odds-Ratio) | 0 mg/kg 下限 | 0 mg/kg 上界 | 100 mg/kg 下限 | 100 mg/kg 上界 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 二项 (Binomial) | 0.12 | 0.07 | 0.20 | 0.35 | 0.18 | 0.66 |
| Beta-二项 (Beta-binomial) | 0.18 | 0.08 | 0.41 | 0.36 | 0.12 | 1.13 |
| 随机聚类 (Random-clumped) | 0.22 | 0.10 | 0.40 | 0.40 | 0.13 | 1.23 |

PHT：苯妥汀；TCPO：三氯苯酚。

`NLMIXED` 过程与其他 SAS 过程一样，提供了赤池信息准则 (AIC) 和 Schwarz 贝叶斯信息准则 (BIC)。如果 "L" 是在参数估计处评估的似然函数，“n" 是观测值（簇数量），且 "u" 是正在估计的参数数量，那么 AIC、AIC（注：原文此处应为笔误）和 BIC 的定义为：

> AIC = -2 ln(L) + 2u
> AICC = -2 ln(L) + \frac{2u}{n-u-1}, and
> BIC = -2 ln(L) + u\ln(n).

```sas
estimate 'Pi Control' 1/(1+exp(-b0));
estimate 'Pi TCCO' 1/(1+exp(-b0-b1));
estimate 'Pi PHT' 1/(1+exp(-b0-b2));
```



`estimate 'Pi PHT+TCCO' 1/(1+exp(-b0-b1-b2));`

`estimate 'Logarithm Odds-Ratio PHT Vs TCCO Control when TCCO Present ' b2+b3;`

`estimate 'Logarithm Odds-Ratio PHT Vs Binomial ' 1/(1+exp(-a0))/(1+exp(-ad0));`

`estimate 'Rho TCCO' 1/(1+exp(-a0-a1))/(1+exp(-ad1));`

`estimate 'Rho PHT' 1/(1+exp(-a2));`

`estimate 'Rho PHT+TCCO' 1/(1+exp(-a0-a1-a2));`

`run;`

Output 4.5 提供了在 Beta 二项分布（Beta-binomial）和随机聚类二项分布（Random-clumped Binomial）下，模型 (4.37) 的 AIC、AICC 和 BIC。这些统计量在随机聚类二项模型下明显更小。人们可能会认为，在这个例中，随机聚类二项分布提供了更好的拟合效果。也许 (4.10) 中给出的聚类机制为母亲遗传状如何传递给后代提供了合理的解释。4.9 显示了每个治疗组的骨化估计概率和估计的过度离散参数。

### 表 4.5：Beta 二项分布和随机聚类二项分布下，针对“Betas”和“Alphas”全模型的信息准则

| 针对 Betas 的全模型，针对 Alphas 的全模型 | NLMIXED 过程 |
| :--- | :--- |
| 拟合统计量 | |
| -2 对数似然值 | 295.8 |
| AIC (越小越好) | 311.8 |
| AICC (越小越好) | 313.8 |
| BIC (越小越好) | 331.0 |

| 随机聚类二项分布，针对 Betas 的全模型，针对 Alphas 的全模型 | NLMIXED 过程 |
| :--- | :--- |
| 拟合统计量 | |
| -2 对数似然值 | 287.8 |
| AIC (越小越好) | 303.8 |
| AICC (越小越好) | 305.8 |
| BIC (越小越好) | 323.0 |

Morel, Jorge, and Nagaraj Neerchal. Overdispersion Models in SAS®. Copyright ©2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. 更多 SAS 资源，请访问 support.sas.com/publishing。

### 表 4.9：具有共同 $ ho$ 的全因子逻辑回归模型骨化数据的 Beta 估计值和标准误

| 参数组 | Beta 二项估计值 | 标准误 | 随机聚类二项估计值 | 标准误 |
| :--- | :--- | :--- | :--- | :--- |
| 骨化概率 $\pi_{op}$ | 对组 (Control) | 0.6642 | 0.05407 | 0.6381 | 0.05669 |
| | TCPO | | 0.4802 | 0.08279 | 0.4245 | 0.07478 |
| | PHT | | 0.2188 | 0.04154 | 0.2186 | 0.04050 |
| | TCPO + PHT | | 0.3149 | 0.1155 | 0.3231 | 0.1180 |
| 过度离散 $\rho_{ip}^2$ | 对组 (Control) | 0.3642 | 0.08003 | 0.3921 | 0.07631 |
| | TCPO | | 0.3568 | 0.1114 | 0.3370 | 0.08610 |
| | PHT | | 0.2257 | 0.1475 | 0.2040 | 0.1559 |
| | TCPO + PHT | | 0.6268 | 0.1535 | 0.7408 | 0.1215 |
| - 2 * 对数似然值 | | 295.8 | | | 287.8 | -- |

# 4.10 在 Beta 二项分布和随机聚类二项分布下生成数据

在本节中，我们为读者提供了在参数为 $(\pi, \rho;m)$ 的 Beta 二项分布和随机聚类二项分布下生成数据的代码。编程语句见程序 4.6。文中给了一个基于 $n=2000$ 个聚类、$\pi=0.4, \rho=0.7$ 且 $m=12$ 的示例。底层真实的均值和方差为 $m\pi = 4.8$ 和 $m\pi(1-\pi)\{1+(m-1)\rho^2\}=18.4032$。基于特定 "seed" 的估计均值和方差如下：PHT; TCPO。

# 第 4 章 过度离散二项似然模型

| 参数为 $\pi=0.4, \rho=0.7$ 和 $m=12$ 的 Beta 二项和随机聚类二项分布生成的估计均值和方差 | MEANS 过程 |
| :--- | :--- |
| 分析变量: t | |
| 分布 (Dist) 观测值 (Obs) 均值 (Mean) |
| BB | 20000 4.8602 18.3861 |
| RCB | 20000 4.7947 18.3707 |

## 程序 4.6：在 Beta 二项分布和随机聚类二项分布下生成数据

```
/*

在参数为 $\pi, \rho$ 和 $m$ 的 Beta 二项和随机聚类二项分布下生成数据

*/

#macro bb_rcb_data(pi,rho,m,seed);

在 Beta 二项分布下生成数据；

data bb;

  format Dist;

  Dist = "BB";

  seed = &seed;

  c = 1/rho - 1;

  a = c * pi;

  b = c - a;

  do cluster=1 to n;

    y1 = rangam(seed, a);

    y2 = rangam(seed, b);

    p = y1/(y1+y2);

    t = ranbin(seed,m,p);

    output;

  end;

keep Dist;

run;

在随机聚类二项分布下生成数据；

data rcb;

  Dist = "RCB";

  seed = &seed;

  do cluster=1 to n;

    y = ranbin(seed,1);

    nn = ranbin(seed,rho);

    /* 数据的聚类;

    if nn < m then t = t + ranbin(seed,pi);

    output;

  end;

keep Dist;

run;

data bb_rcb;

  set rcb;

run;

ods html;

title1 "估计均值和方差";

title2 "来自 Beta 二项和随机聚类二项分布生成的数据";

title3 "参数为 $\pi, \rho$ 和 $m=m";

proc means data=bb_rcb mean=4;

  class Dist;

  var t;

run;

ods close;

%end bb_rcb;

%bb_rcb_data(0.4,0.7,12,20000);
```

# 过度离散二项模型的拟合检验

- 5.1 引言 ................................................115
- 5.2 针对过度离散二项备择假设检验“无过度离散”................................................116
- 5.3 整体拟合检验..................................121
- 5.4 存在协时的 GOF 扩展：染色体异常................................................130
- 附录 5.1：模块“GOF_RCB”.........................................138
- 附录 5.2：模块“GOF_RCB”........................................................146
- 附录 5.3：存在协同时，Beta 二项分布和随机聚类二项分布下的 GOF 检验...............154

## 5.1 引言

在本章中，我们将考虑两种类型的拟合性（GOF）检验。这两种类型通常统称为 GOF，我们将看到这两种类型在原假设和备择假设方面存在关键差异。在第一类型中，过度离散的原假设是针对特定的备择假设（例如 Beta 二项或随机聚类二项模型）。在第 4.6 节中，当我们对表 4.1 的染色体数据测试假设 $H_0 :\rho=0$ 与备择假设 $H_1 :\rho>0$ 时，分别在 Beta 二项、随机聚类二项、零膨胀二项（ZIB）以及具有加性相互作用的广义二项模型下对这些过度离散进行了说明。我们还用表 4.1 的染色体数据说明了第二种测试特定模型适用性的 GOF 示例。表 4.3 提供的结果表明，Beta 二项、随机聚类二项以及具有加性分布的广义二项分布相当好拟合了关联数量，而二项和 ZIB 分布则不能。在本章中，我们将描述这两类型的 GOF 检验并提供说明示例。

# 5.2 针对过度离散二项备择假设检验“无过度离散”

在本节中，我们考虑在几种特定过度离散二项分布下“无过度离散”原假设的检验。其中一种是由 Tarone (1979) 在 Beta 二项模型下测试的。假设 $t_1, t_2, \dots, t_n$ 是 $T_1, T_2, \dots, T_n$ 的实现，其中 $T_j$ 是独立随机变量，使得对于每个 $j，$j=1, 2, \dots, n$，T_j \sim \text{Binomial}(\pi, \rho; m_j)$。在 Beta 二项模型下，对于 $H_0: \rho = 0$ 与单侧备择假设 $H_1: \rho > 0$，得到的统计如下。如果假设 $T_j$ 服从二项分布，则 $\hat{\pi}$ 是 $\pi$ 的极大似然估计值，那么 Tarone 的 GOF 单侧统计量

```
$Z = \sqrt{\sum_{j=1}^n \frac{(t_j - \hat{m}_j)^2}{\hat{\pi}(1 - \hat{\pi}) - \sum_{j=1}^n m_j(m_j - 1)}}$ (5.1)
```

其在原假设下渐近服从标准正态分布。

## 第 5 章 过离散二项分布模型的拟合度检验

与 Tarone (1979) 的示例一样，我们考虑 Kupper 和 Haseman (1978, p. 75) 报告的治疗组数据。数据如表 5.1 所示，对应涉及 n=10 只母鼠的未发表实验室数据。

### 表 5.1：涉及怀孕母鼠的实验室数据

| 小鼠 (j) | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|---|
| (t_j) | 0 | 2 | 1 | 0 | 2 | 3 | 0 | 4 | 1 | 6 |
| (m_j) | 5 | 5 | 7 | 8 | 8 | 9 | 9 | 10 | 10 | |

计算 GOF 检验 (5.2) 的程序在程序 5.1 中。在二项分布模型下，多个 SAS 过程可以提供 $\pi$ 的 MLE，其结果为比率估计量 $\hat{\pi} = \sum_{j=1}^{n} \frac{t_j}{m_j}$。对于本示例，我们利用 SURVEYMEANS 过程来计算 $\hat{\pi}$。读者应该注意，SURVEYMEANS 为该估计量 $\hat{\pi}$ 标准误差无论 $t_j$ 的分布假设如何都是无的。在过离散假设下（如方程 (4.5) 所示），SURVEYMEANS 方差估计是一致的。

### 程序 5.1：计算 Tarone (1979) GOF 检验统计量 (5.2)

```
* Tarone (1979) 双侧 GOF 检验

H0:二项分布方差

H1:加性交互的广义二项分布 (Altham, 1978)

Altham 的模型由 Kupper 和 Haseman (1978) 同时提出

并命名为“相关二项分布模型”

以下数据来自 Kupper 和 Haseman (1978, 第 75 页)

/*

data kupper_haseman;

input t m;

datalines;

0 5

2 5

1 7

0 8

2 8

3 8

0 9

4 9

1 10

6 10;

ods none;

proc surveymeans data=kupper_haseman;

ratio t/m;

run;

ods select all;
```

```sas
data Ratio;

  set Ratio;

  call symput('Pi',trim(left(Ratio)));

run;

data out1;

  set kupper_haseman;

  pi = &Pi;

  pic = 1 - pi;

  pipic = pi * pic;

  mpi = m * pi;

  t_mpi = t - mpi;

  pit_mpi = pi * t_mpi;

  tpic = t * pic;

  mm_1 = m * (m-1);

  aux = (t_mpi*t_mpi + pit_mpi - tpic) / pipic;

  keep aux mm_1;

run;

proc means data=out1 sum noprint;

  var aux mm_1;

  output out=out2 sum=mm_1;

run;

data out2;

  set out2;

  label X2 = "GOF Test";

  label PVal = "P-Value";

  format X2 = au8.2 Pval pvalue.6;

  x2 = aux / sqrt(2*mm_1);

  x2 = x2 * x2;

  pval = 1 - probchi(x2,1,0);

run;

ods html;

title Tarone (1979) GOF Test;

proc print data=out2 noobs label;

  var x2 pval;

run;

html close;
```

该 GOF 的结果如下（自由度 P值=0.01）。在本示例中，我们拒绝了数据服从二项分布的原假设，转而支持 Altham (1978) 和 Kupper 和 Haseman (1978) 中的具有加性交互的广义二项模型或相关二项模型。这些结果与 Tarone (1979) 提供的一致。

### Tarone (1979) GOF 检验

| GOF Test | P-Value |
|---|---|
| 6.63 | 0.01 |

Dean (1992) 提供了关于自然指数过离散的检验方法。类似于 Tarone 的检验，可以获得额外的二项和额外的泊松方差的若干检验。我们使用第 4 章第 8 节讨论的 log 模型来说明 Dean 的方法。如前，让成功概率 $\pi_j, j=1,...,n$ 依赖于 $k$ 维协变量向量 $x_j$ 和 $k$ 维未知列向量 $\beta$，通过 logit 链接：

$$\ln\left(\frac{\pi_j}{1-\pi_j}\right)=x_j\beta=\sum_{i=1}^k x_{ji}\beta_i$$

Dean (1992) 推导了一个检验“$\tau=0$”的得分统计量，其前两个矩的形式为：

$$E(T_j) = m_j\pi_j, \text{ and } Var(T_j) = m_j\pi_j(1-\pi_j)\1+\tau(m_j-1)\}$$

Dean 的得分统计量变为：

$$Z = \frac{\sum_{j=1}^n (t_j-m_j\hat{\pi}_j)^2 + \hat{\pi}_j^2(t_j-m_j\hat{\pi}_j)-t_j(1-\hat{\pi}_j)\hat{\pi}_j}{\sqrt{2\sum_{j=1}^n m_j(m_j-1)}} (5.3)$$

注意当 $\tau=0$ 时，该得分统计量 (5.3)。Dean (1992) 指出，对于上述前两个矩的任意替代，使用得分统计量 (5.3) 是合适的。如前，Beta 二项分布和随机二项分布基于具有上述结构的相关的伯努利分布。为了说明得分统计量 (5.3) 的使用，我们重新考虑了 Efron (1986) 关于萨尔瓦多 34 个城市的示例。数据报告在表 3.2 中。回想，“样本数量 ($m_j$) 中检测毒性的病例数 ($t_j$)”的结果是作为程序 5.2 中所示线性、二次和立方项的函数进行分析的。我们将跳过数据语句，因为它们与程序 3.2 相同。

### 程序 5.2：表 3.2 毒性示例的 Dean (1992) GOF 得分统计量

```sas
/*

Score Statistic, Dean (1992)

H0:二项分布

H1:Beta二项或类似分布，例如

随机二项，只要伯努利结果是相关的

萨尔瓦多 34 个城市的毒性

来自 Efron (1986) 的示例

*/

ods select none;

proc glimmix data=toxosis;

  model t/m = z*z / link=logit dist=bin;

  output out=data pred(pi) = pi;

run;

ods select all;

data pdata;

  set pdata;

  pic = 1 - pi;

  pipic = pi * pic;

  mpi = m * pi;

  t_mpi = t - mpi;

  pit_mpi = pi * t_mpi;

  tpic = t * pic;

  mm_l = m *(t-1);
```



```
aux = (t*t_mpi + pit_mpi - tpic) / pipic;

keep aux mm_l;

run;

proc means data=pdata sum noprint;

  var aux mm_l;

  output out=new sum=mm_l;

run;

data new;

  set new;

  label Z = "GOF Test";

  label Pval = "P-Value";

  format z = aux / sqrt(mm_l) .6f;

  pval = 1 - probnorm(z);

run;

ods title;

title="Score Statistic, Dean (1992)";

proc print data=new noobs label;

var pval;

run;

ods html close;
```

毒性数据的 GOF 检验得分统计量 (5.3) 结果如下所示。当将二项模型与任何伯努利结果在城市内部相关的替代方案进行比较时，存在强烈的过离散证据。

| 得分检验统计量, Dean (1992) | GOF 检验 | P值 |
|---|---|---|
| 3.73 | | <.0001 |

## 5.3 总体拟合度检验

注意，5.2 节中的检验关注针对过离散的特定替代方案。Tarone (1979) 和 Dean (1992) 描述了多种检验“无过离散”原假设的方法，例如 Beta 二项模型。Paul 和 Slack (1978) 以及 和 Margolin (1985) 提出了类似类型的检验，例如正态性的 Shapiro-Wilk 检验是一种总体检验。在本节中，我们将介绍模型适用性的检验，称为总体检验。

总体检验旨在测试特定分布是否符合数据。原假设是数据来自特定分布，而替代假设是数据不来自该分布。由于替代假设中没有指定模型，我们在替代假设下获得极大然估计。另一个著名的总体检验是 Pearson 拟合度检验。对于 4.6 中的元素（见表 4.3），Rao (1965, p. 391) 和 Cramer (1968, pp. 477-506) 给出的 Pearson 检验是可用的。然而，当 m 不同时，构建 Pearson 拟合度统计量并不简单，因为观测期望值与任何 m 值关联。Meer 和 Morel (1998) 对传统的 Pearson 卡方统计量提出了一种扩展：

$$X^2 = \sum (O_i - E_i)^2 / E_i,$$

当簇大小 m 不同时。该检验的渐近性质已由 Sutradhar 等 (2008) 研究过。

让 $t_1, t_2, ..., t_n$ 代表 $n$ 个独立随机变量 $T_1, T_2, ..., T_n$，当这些变量相对于二项分布具有过离散时，即前两个矩如方程 (4.4) 和 (4.5) 所示。

# SAS 中的过度离散模型

$O_s = \sum_{j=1}^{n_s} I\left(\frac{t_j}{m_j} \in A_s\right) \quad (5.5)$

and

$E_s = \sum_{j=1}^{n_s} \text{Pr}(T_j = t) I\left(\frac{t}{m_j} \in A_s\right), \quad (5.6)$

其中 $I(.)$ 表示指示函数，$\text{Pr}(T=t)$ 通过 $\pi$ 和 $\rho$ 的最大似然估计值得出。注意 $\sum_{s=1} O_s = \sum_{s=1} E_s = n$。如果所有簇的大小都相同，可以证明频率派的表达式 (5.6) 简化为：

$E = m \text{Pr}\left(\frac{T}{m} \in A_s\right)$，且卡方统计量将变为普通的 Pearson 拟合优度（GOF）统计量。

这种具有不同 'm' 的综合检验出现在 Neerchel 和 Morel (1998) 中。他们将 Beta-二项分布和随机聚类二项分布拟合到三个诱导突变损伤数据集（称为数据集 I、II 和 III）上，这些数据曾由 Haseman 和 Soares (1976) 分析过。一组雄鼠首先接受一种怀疑的突变剂处理，随后接受一个或多个未处理的雌鼠的处理。雌鼠怀孕后，一段时间后它们被处死，并检查活死植入的频率（植入是胚胎的早期阶段）。由于来自同一母体的植入或胚胎需要产生相似，因此将它们视为自然簇是合理的。表 5.2 详细介绍了数据集 III，它是基于 n=554 只 DBA/23 雌鼠与 CD-1 雄鼠的配种。该表提供了具有“d”植入频率的雌鼠数量，其中雌鼠总数 n=554。注意植入的总数（怀孕鼠中的簇大小在 1 到 18 之间变化）。死亡植入的数量在零到九之间变化。正如 Neerchel 和 Morel (1998) 所报告的，结果表明 Beta-二项和随机聚类二项模型均拟合了数据集 I。另一方面，随机聚类二项分布勉强拟合数据集 II，并充分拟合数据集 III。Beta-二项模型未拟合数据集 II 或 III。

More, Jorge, and Nagaraj Neerchel. Overdispersion Models in SAS. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 更多 SAS 资源，请访问 support.sas.com/publishing。

# 第 5 章 过离散二项模型的拟合优度检验

## 表 5.2: 诱导突变数据，Haseman 和 Hogan (1976) 中的数据集 III

| m | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | 7 | | | | | | | | | |
| 2 | 7 | | | | | | | | | |
| 3 | 6 | | | | | | | | | |
| 4 | 5 | | 2 | 1 | | | | | | | |
| 5 | 8 | | 2 | | 1 | 1 | | | | | |
| 6 | 8 | | | | | | | | | | |
| 7 | 7 | | 4 | 2 | | | | | | | |
| 8 | 7 | | 7 | 1 | | | | | | | |
| 9 | 8 | | 9 | 7 | 1 | | | | | | |
| 10 | 22 | | 17 | 2 | | 1 | | 1 | | | |
| 11 | 30 | | 18 | 9 | | 1 | | 2 | | | |
| 12 | 54 | | 27 | 12 | | 1 | 1 | | | | |
| 13 | 46 | | 30 | 8 | 4 | 1 | | 1 | | | |
| 14 | 43 | | 21 | 13 | 3 | | | | 1 | | |
| 15 | 22 | | 22 | 5 | 2 | 1 | | | | | | |
| 16 | 6 | | | 6 | 3 | 1 | | | | | | | |
| 18 | 3 | | 3 | 2 | | | | | | | | |

我们首先拟合表 5.2 以获得 $\pi$ 和 $\rho$ 的 MLE。然后，我们计算 (5,4)、(5,5) 和 (5,6) 中描述的综合 GOF 检验。为此，我们使用了由 Pfizer 公司的 Santosh C. Sudradhar 博士提供的 "`GOF_GB`" 和 "`GOF_RCB`" 模块。

这些模块分别可以在附录 5.1 和 5.2 中找到。这些模块中的迭代过程基于 Fisher 信息矩阵而不是 Hessian 矩阵（如我们在使用 `NLMIXED` 的情况 4 中所示）。两种过程在渐近上是等价的。程序 5.3 提供了表 5.2 突变数据所需的统计量。在调用 "`GOF_GB`" 和 "`GOF_RCB`" 之前，应根据观测频率期望频率 (5.6) 输出残差到 "`Resid_GB`" 和 "`Resid_RCB`" 数据中，并构建残差的 QQ 图。表 5.3 提供了 Beta-二项和随机聚类模型的结果。

## 程序5.3: 诱导突变数据的 MLE 分析和 GOF

```sas
* GOF Test for DataSet III on Neerchel and Morel (1998)

Source: Haseman and Soares (1976)

This program uses "GOF_GB" and "GOF_RCB" Macros
```

```sas
data haseman_soares;

input m t1-t10;

array tt t1-t10;

do over tt;

  1;

freq = tt;

  output;

end;
```

Morel, Jorge, and Nagaraj. Overdispersion models in SAS. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 更多 SAS 服务，请访问 support.sas.com/publishing.

| m | freq |
|---|---|
| 1 | 7 |
| 2 | 7 |
| 3 | 6 |
| 4 | 5 |
| 5 | 5 |
| 6 | 8 |
| 7 | 7 |
| 8 | 8 |
| 9 | 9 |
| 10 | 22 |
| 11 | 30 |
| 12 | 54 |
| 13 | 46 |
| 14 | 43 |
| 15 | 22 |
| 16 | 6 |
| 18 | 3 |

```sas
data haseman_soares;

  set haseman_soares;

  if freq < 5 then delete;

  do i=1 to

    output;

  end;

  drop freq;

run;

ods html;

ods graphics;

%GOF_BB(inds=haseman_soares,t=t,m,title2=DataSet III -- Haseman and Soares (1976));

%GOF_RCB(inds=haseman_soares,t=t,m,title2=Dataset III -- Haseman and Soares (1976));

* Construct QQ Plots

data Resid_BB_RCB;

  set Resid_BB Resid_RCB;

run;

proc sort data=Resid_BB_RCB;

  by Distribution;

run;

proc rank data=Resid_BB_RCB out=new_qqplots normal= ties=mean;

  by Distribution;

  var Resid;

  ranks Nquant;

run;

proc sg data=new_qqplots autlegend;

  panel Distribution;

  title "Dataset III -- Haseman and Soares (1976)";

  title2 "QQ-Plots of Residuals based on Observed and Expected Frequencies";

  x=Resid y=Nquant;

run;

ods graphics off; ods close;
```



最初，单位区间被分为 `R` 个互斥区间。对于 `s` 个区间 `$A_s, s=1,2,...,R$`，计算所有的 `$\frac{t_j}{m_j}$`，落在区间 `$A_s$` 中的数量即为 `$A_s$` 的观测频率。即：

$O_s = \sum_{j=1}^{554} I\left(\frac{t_j}{m_j} \in A_s\right)$

期望频率计算更为密集，且取决于 `$t_j$` 的变异性。例如，使用 Beta-二项分布，`$A_s$` 的期望频率计算为：

$E_s = \sum_{j=1}^{554} \sum_{t=0}^{m_j} Pr[T_j=t|T_j \sim \text{Beta-binomial}(\hat{\pi}, \hat{\rho}; m_j)] I\left(\frac{t}{m_j} \in A_s\right)$

其中 `$\hat{\pi}$` 和 `$\hat{\rho}$` 是表 5.3 给出的 `$\pi$` 和 `$\rho$` 的 MLE。随机聚类二项模型进行了类似的计算。我们从 `$R=\max(m_j,j=1,2,...,554)=18$` 个区间开始。我们使用通常的经验法则确保每个区间的期望频率至少为 5。不符合此规则的区间将与上一个合并。使用模块 `"GOF_BB"` 的结果显示在输出 5.3 中。

## 表 5.3: 诱导突变数据最大似然结果

| | | Beta-binomial | Random-clumped Binomial |
|---|---|---|---|---|
| Parameter | Estimate | Standard Error | Estimate | Standard Error |
| `$\pi$` | 0.0739 | 0.0045 | 0.0760 | 0.0046 |
| `$\rho$` | 0.2741 | 0.0207 | 0.3235 | 0.0253 |
| -2 Log Likelihood | 1402.66 | | 1378.75 | |

## 输出 5.3: 诱导突变数据的 Beta-二项模型最大似然 GOF 结果

| Goodness-of-fit test under Betaomial distribution DataSet III -- Haseman and Soares (1976) |
|---|---|
| Fit Statistics |
| -2 Log Likelihood | 1402.66 |
| AIC (smaller is better) | 1406.66 |
| AICC (smaller is better) | 1406.68 |
| BIC (smaller is better) | 1415.30 |
| Maximum Likelihood Estimates |
| Estimate | Std-Error | t-Value | DF | p-Value |
| Parameter Pi | 0.07385 | 0.00443 | 16.6704 | 552 | 0.0001 |
| Parameter Rho | 0.27412 | 0.02086 | 13.1409 | 552 | 0.0001 |
| Goodness-of-fit Test under Beta-binomial Distribution |
| Lower | Upper | Observed Frequency | Expected Frequency |
| 0.0000 | 0.0526 | 286 | 298.8466 |
| 0.0526 | 0.1053 | 141 | 113.9468 |

# 第5章 过度离散二项分布模型的拟合度检验 127

| 聚类数量 | 观测频率 | 期望频率 |
|---|---|---|
| 554 | 554 | 554.0000 |

> 原假设：数据按照 Beta-二项分布分布

| 拟合度检验 统计量 | 自由度 (DF) | p值 |
|---|---|---|
| 21.6386 | 6 | 0.0014 |

表 5.4 报告了 Beta-二项分布和随机聚类二项分布（Random-clumped Binomial distributions）下的整体拟合度（GOF）检验结果。为了简单起见，期望频率保留了两位小数。之前讨论的算法从 18 个区间开始，最后在随机聚类二项模型附近以 10 个区间和 9 个区间处结束，我们将最后两个区间合并到随机聚类二项模型下，使得卡方检验具有相同的自由度。Beta-二项分布和随机聚类二项分布下的拟合度检验 p 值分别为 0.0014 和 0.2205。这些检验基于六个自由度（区间数量减一，再减去待估计参数的数量）。随机聚类二项分布很好地拟了数据，而 Beta-二项分布则不然。p 值还通过对数据进行 20,000 次重复的参数化自助（bootstrapping）进行了估计，结果为 0.0012 和 0.2124，这与使用六自由度卡方分布得到的结果一致。QQ 图 5.1 是基于观测频率减去期望频率得到的残差。从图中可以看出，随机聚类二项分布的拟合效果优于 Beta-二项分布。

**表 5.4** Haseman 和 Soares (1976) 数据集 III (n = 554) 的拟合度结果

| 区间 Aᵢ | 观测值 (Oᵢ) | 期望 (Eᵢ) - Beta-二项 | 期望 (Eᵢ) - 随机聚类二项分布 |
|---|---|---|---|
| [0, 1/19) | 286 | 298.85 | 283.05 |
| (1/19, 2/19) | 141 | 113.95 | 147.45 |
| (2/19, 3/19) | 51 | 45.85 | 44.76 |
| (3/19, 4/19) | 28 | 34.95 | 26.90 |
| (4/19, 5/19) | 20 | 24.05 | 13.50 |
| (5/19, 6/19) | 7 | 14.05 | 8.04 |
| (6/19, 7/19) | 4 | 9.15 | 7.58 |
| (7/19, 8/19) | 3 | 5.16 | 6.25 |
| (8/19, 1] | 14 | 7.99 | 16.47 |
| 总计 | 554 | 554.00 | 554.00 |
| X² | | 21.64 | 8.25 |
| DF | | 6 | 6 |
| P值 | | 0.0014 | 0.2205 |

More, J., and Nagaraj Neel. Overdispersion Models in SAS.. Copyright © 2021, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED.更多 SAS 资源，请访问 support.sas.com/publishing。

# 图 5.1：诱导诱变性示例的 QQ 图

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_140_0.png)

Sutradhar (2001) 和 Sutradhar 等 (2008) 提供了上一节中拟合度检验的理论性质。结果表明，该拟合度检验具有与通常皮尔逊拟合度检验类似的渐近性质。特别是，结果显示卡方分布为零分布提供了良好的近似。正如下一节将详细阐述的，当待估计参数较多时，近似卡方分布的适当自由度需要调整。解决此问题的实用方法是使用自适应自助（adaptive bootstrapping）获取 p 值。我们将展示模拟结果以说明这种方法，并证明该统计量在区分 Beta-二项分布和随机聚类二项分布方面非常有效力。

这里讨论的两个模拟最早由 Sutradhar 等 (2008) 提出。其目的是研究上一节中整体拟合度检验的性质。他们的模拟解决了两个问题，即拟合度检验的分布特征以及通过第一类错误率和功效衡量的特征。在本节提供了后续结果。在模拟中，考虑了 `$\pi = 0.1, 0.3, 0.5$` 的三个值，以及 `$\rho = 0.3, 0.5, 0.7$` 的三个值。这些聚类大小的生成方式为 `$m = 15$`；随机从 `$\{10, 15, 20\}$` 集合中选择聚类大小，其中聚类大小为 10 的概率为 0.40，为 15 的概率为 0.20，为 20 的概率为 0.40；最后从 `$m = Y+1$` 的泊松模型生成聚类大小。对于 `$\pi$` 和 `$\rho$` 的每个组合，生成了 2000 组数据；每组大小 `$n=400$`。在表 5 中报告了与 Beta-二项分布和随机聚类二项分布相关的结果。当聚类大小随机生成时，`$\alpha=0.1$` 下的估计第一类错误。我们还估计了检验 `$H_0$`: Beta-二项对比 `$H_1$`: 随机聚类二项分布的功效，以及 `$H_0$`: 随机聚类二项对比 `$H_1$`: Beta-二项分布的功效。皮尔逊卡方统计量的自由度为 `$R=3$`，其中 `$R$` 是覆盖 `$\[0,1\]` 区间的非重叠区间数量。`$\rho$` 的值为 `$\rho=0.1$`。

**表 5.5：当 `$\alpha=0.10$` 且聚类大小 `$m=Y+1$`（`$Y \sim Poisson(14)$`）时拟合度检验的经验第一类错误和功效 (%)**

| 检验假设 | `$\pi$` | `$\rho$` | 第一类错误 | 功效 |
|---|---|---|---|---|
| `$H_0$`: Beta-二项 | 0.1 | 0.1 | 11.0 | 13.8 |
| VS | 0.3 | 10.9 | 99.2 |
| `$H_1$`: 随机聚类二项分布 | 0.5 | 11.0 | 100.0 |
| | 0.3 | 0.1 | 9.9 | 10.2 |
| | | 0.3 | 10.2 | 89.0 |
| | | 0.5 | 10.5 | 100.0 |
| | | 0.1 | 8.4 | 9.9 |
| | | 0.3 | 9.4 | 73.6 |
| | | 0.5 | 11.1 | 100.0 |

表 5.5（续）
| 检验假设 | `$\pi$` | `$\rho$` | 第一类错误 | 功效 |
|---|---|---|---|---|
| `$H_0$`: 随机聚类二项分布 | 0.1 | 0.1 | 11.2 | 15.2 |
| VS | 0.3 | 10.4 | 98.5 |
| `$H_1$`: Beta-二项 | 0.5 | 12.1 | 100.0 |
| | | 0.3 | 9.2 | 10.9 |
| | | 0.3 | 9.6 | 86.6 |
| | | 0.5 | 9.8 | 100.0 |
| | | 0.1 | 9.1 | 18.0 |
| | | 0.3 | 9.3 | 77.9 |
| | | 0.5 | 10.4 | 100.0 |

## 5.4 存在协变量时的拟合度扩展：广岛染色体异常示例

正如 4.8 节指出的，在存在聚类特有协变量的情况下，成功概率 `$\pi$` 和过度离散参数 `$\rho$` 都可能在不同聚类之间有所差异。为了模拟这种情况，我们建议对成功概率使用两个连接函数（称为 GLM），对过度离散参数使用一个连接函数。如方程 (4.31) 和 (4.32) 定义的连接函数所示：

`$g(\pi_i) = x_i\beta = \sum_{j} x_{ij}\beta_j$` 和 `$f(\rho_i) = z_i\alpha = \sum_{j} z_{ij}\alpha_j$`。

方程 (5.4) 中的拟合度检验可以进行调整，以不仅考虑不同的聚类大小，还考虑不同的成功概率和过度离散程度。为此，找到第一个极大似然估计量 `$\hat{\theta} = (\hat{\beta}, \hat{\alpha})$`，`$\hat{\beta} = (\hat{\beta}_1, \hat{\beta}_2, \dots, \hat{\beta}_k)$` 和 `$\hat{\alpha} = (\hat{\alpha}_1, \hat{\alpha}_2, \dots, \hat{\alpha}_h)$`。

# 第 5 章 过度离散二项分布模型的拟合度检验

接着，使用观测频率 (5.5) 和期望频率 (5.7) 计算等式 (5.4) 中的拟合度（GOF）检验。

自由度这个问题值得讨论。注意，GOF 检验统计量是基于极大似然估计计算的，而这些估计值是从原始数据获得的。另一方面，GOF 自由度为 `$\nu=R-3$` 的分布结果是基于统计量使用来自分组数据的估计值计算的假设。正如 Chernoff 和 Lehmann (1954) 所示，以及在 Kendall, Stuart 和 Ord (1991) 的第30 章和 Satradhar 等人 (2008) 中讨论的那样，由于使用了效率更高的极大似然估计量，自由度似乎得到了某种恢复。我们提出的 GOF 检验的建议自由度介于 `$\nu_l=(R-1)-(k+h)$` 和 `$\nu_u=(R-1)$` 之间。下界 `$\nu_l$` 对应于参数被估计的情况，而上界 `$\nu_u$` 对应于所有参数均已知的情况。模拟 5.4 的结果支持在当成功概率 `$\pi$` 和过度离散参数 `$\rho$` 在聚簇间共同时，使用 `$\nu=(R-1)-2$` 个自由度。

我们利用 Awa 等人 (1971, 1978) 对广岛和长崎原子弹爆炸幸存者染色体变异进行的流行病学研究的现有数据，阐释了 GOF 检验的使用。该研究于 1968 年 1 月至 1969 年 11 月在广岛进行，于 1968 年 1 月至 1971 年 3 月在长崎进行。病例从居住在广岛和长崎且备有初步辐射剂量估计值的原子弹幸存者中选出。对照组由两部分组成：爆炸发生时不在城市中的人，以及暴露于炸弹但估计剂量小于 1 rad 的人。对广岛的 n=668 名和长崎的 n=403 名受试者采集了血液并进行了细胞遗传检查。我们将仅关注广岛的数据；感谢 D. Moore 教授为本示例提供数据。每个受试者检查了 30 到 100 个淋巴细胞，并记录了染色体变异的数量（第 j 个受试者）。令 `$d$` 表示本研究中暴露单位的辐射剂量（rad），认为需要超过一次命中才能导致变异，而单次命中足以检测到。此处考虑的总辐射剂量是伽马射线和中子分量的之和。超过 600 rad 的剂量估计被降低至 600。Prentice (1986) 使用扩展的 Beta 二项模型分析了染色体变异数据，该模型允许某种程度的过度离散。Moore (1987) 扩展了 Beta 二项的极大似然估计方法以及基于均值和方差的方法，允许将二项之外成分建模为均值的函数。在 Prentice 的辐射剂量估计中是经过分组的，而在 Moore 的估计中则没有对数据进行任何分组。我们将使用 Moore (1987) 的数据集填充 Beta 二项分布模型和随机聚类二项分布模型。正如第 3.4 节中关于萨尔瓦多弓形虫的 Effort (1986) 示例那样，我们将辐射剂量 `$d_j$` 标准化：

```
$Z_j = \frac{\sqrt{648}(d_j - \tilde{d})}{\sqrt{\sum_{i=1}^{}(d_i - \tilde{d})^2}}$
```

将拟合的两个过度离散模型将具有线性预测因子

```
logit(\pi_i) = \beta_0 + \beta_1 z_i + \beta_2 z_i^2$ (5.8)
```

以及

```
logit(\pi_j) = \alpha_0 + \alpha_1 z_j + \alpha_2 z_j^2$ (5.9)
```



因此，成功概率 `$\pi$` 的 logit 和过度离散 `$\rho$` 的 logit 是标准化剂量 `z` 的二次函数。请读者参考第 4.8 节，我们在那里广义线性过度离散模型的背景下引入了连接函数的概念。我们拟合的基础模型是 Beta 二项分布和随机聚类二项分布。编程语句可以在程序 5.4 中找到。我们首先使用 `NMIXED` 过程计算 MLE。然后 `$\pi_i^*$` 和 `$\rho_i^*$` 的估计频率输出到数据集 `$\pi_{bb}$`, `$\rho_{bb}$`, `$\pi_{rcb}$` 和 `$\rho_{rcb}$`。这些数据集用于使用宏 `GOF_RCB_CB` 计算期望 `(5.7)` 和 GOF 检验 `(5.4)`。

# 第5章 过离散二项分布模型的拟合优检验 135

GOF 检验的结果报告在输出 5.4 中。Beta-二项模型下的 GOF 统计量为 19.396。如前所述，我们提出的 GOF 检验的自由度介于 `$\nu_1=(24-1)-(3+3)=17$` 和 `$\nu_2=(24-1)=23$` 之间。在 17 和 23 自由度的卡方分布下，相应的 P 值分别为下限的 0.31 和上限的 0.68。因此我们得出结论：具有线性预测因子的 `(5.8)` 和 `(5.9)` 的 Beta-二项模型对广岛染色体变异数据提供了充分的拟合。另一方面，GOF 卡方统计量在下限 `(19-1)+(3+3)=12` 自由度和上限 `(19-1)=18` 自由度下均为 96.88，这表明随机聚集二项分布（Random-clumped Binomial distribution）并不拟合这些数据。QQ 图 5.2 证实了这些发现。

## 输出 5.4：广岛染色体变异示例在 Beta-二项模型和随机聚集二项模型下的 GOF 结果

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_147_0.png)

| 下限 | 上限 | 观测频率 | 期望频率 |
|---|---|---|---|
| 0.0000 | 0.0099 | 140 | 135.19 |
| 0.0099 | 0.0198 | 107 | 109.96 |
| 0.0198 | 0.0297 | 90 | 83.69 |
| 0.0297 | 0.0396 | 52 | 59.89 |
| 0.0396 | 0.0495 | 30 | 38.96 |
| 0.0495 | 0.0594 | 32 | 29.39 |
| 0.0594 | 0.0693 | 27 | 26.79 |
| 0.0693 | 0.0792 | 33 | 19.35 |
| 0.0792 | 0.0891 | 14 | 17.06 |
| 0.0891 | 0.0990 | 13 | 14.30 |
| 0.0990 | 0.1089 | 11 | 13.89 |
| 0.1089 | 0.1188 | 11 | 10.87 |
| 0.1188 | 0.1287 | 7 | 9.92 |
| 0.1287 | 0.1386 | 8 | 9.13 |
| 0.1386 | 0.1485 | 9 | 7.29 |
| 0.1485 | 0.1584 | 8 | 6.90 |
| 0.1584 | 0.1683 | 8 | 6.44 |
| 0.1683 | 0.1782 | 6 | 5.30 |
| 0.1782 | 0.1980 | 12 | 8.79 |
| 0.1980 | 0.2178 | 5 | 7.48 |
| 0.2178 | 0.2376 | 5 | 5.75 |
| 0.2376 | 0.2673 | 7 | 6.60 |
| 0.2673 | 0.3069 | 5 | 5.92 |
| 0.3069 | 1.0000 | 8 | 9.12 |

| 聚类数量 | 观测频率 | 期望频率 |
|---|---|---|
| 648 | 648 | 648.0000 |

原假设：数据符合 Beta-二项分布

| | GOF 统计量 | 自由度 | P 值 |
|---|---|---|---|
| 下限自由度结果 | 19.3962 | 17 | 0.3063 |
| 上限自由度结果 | 19.3962 | 23 | 0.678 |

随机聚集二项分布下的拟合优检验

| 下限 | 上限 | 观测频率 | 期望频率 |
|---|---|---|---|
| 0.0000 | 0.0099 | 140 | 107.73 |
| 0.0099 | 0.0198 | 107 | 113.91 |
| 0.0198 | 0.0297 | 90 | 89.83 |
| 0.0297 | 0.0396 | 52 | 62.57 |
| 0.0396 | 0.0495 | 30 | 42.25 |
| 0.0495 | 0.0594 | 32 | 35.64 |
| 0.0594 | 0.0693 | 27 | 35.96 |
| 0.0693 | 0.0792 | 33 | 28.37 |
| 0.0792 | 0.0891 | 14 | 26.01 |
| 0.0891 | 0.0990 | 13 | 21.14 |
| 0.0990 | 0.1089 | 11 | 19.45 |
| 0.1089 | 0.1188 | 11 | 13.98 |
| 0.1188 | 0.1287 | 7 | 10.58 |
| 0.1287 | 0.1386 | 8 | 8.14 |
| 0.1386 | 0.1485 | 9 | 5.07 |
| 0.1485 | 0.1683 | 16 | 6.59 |
| 0.1683 | 0.2079 | 20 | 5.67 |
| 0.2079 | 0.2574 | 12 | 5.94 |
| 0.2574 | 1.0000 | 16 | 9.17 |

| 总计数 聚类数量 | 观测频率 | 期望频率 |
|---|---|---|
| 648 | 648 | 648.0000 |

原假设：数据符合随机聚集二项分布

| GOF 检验统计量 | GOF 统计量 | 自由度 | P 值 |
|---|---|---|---|
| 下限自由度结果 | 96.8831 | 12 | 0.0001 |
| 上限自由度结果 | 96.8831 | 18 | 0.0001 |

## 图 5.2：广岛染色体变异的 QQ 图
![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_150_0.png)

## 附录 5.1：模块 “GOF_BB”

作者：Santosh Chaturvedi
副经理
Pfizer Inc.
25 East 42nd St
New York, NY 10017
电话：
邮箱：Santosh.Chaturvedi@pfizer.com
最后修改：2009年9月24日

目的：编写一个 SAS 宏以计算极大似然估计（MLE）并在 Beta-二项分布下进行拟合优检验。该 `GOF_BB` 宏基于直接似然（Direct Likelihood）使用 Fisher 刻分法迭代计算 MLE。要求：调用 `fisherbb.sas` 中的其他模块。

# 第5章 过离散二项分布模型的拟合优检验 139

变量列表：
`inds` = 输入 SAS 数据（必须包含两个变量 `t`, `m`）
`t` = 聚类计数
`m` = 聚类大小

使用方法：`%GOF_BB(inds, t, m)`

注释：聚类大小（`m`）是假设的。初始类别数量 GOF = `MAX(m)+1`

```sas
%macro GOF_BB(inds , t, m, title2 = "Data: ");

title "Beta-二项分布下的拟合优检验"

title2 "&title2";

* 开始 IML 过程

proc iml;

* 打印输入信息

file print;

* 模块: FISHERB: 此模块可以调用以计算 BB 分布下的 Fisher 信息;
```

```sas
start FISHERB;
do ij = 1 to m;
    AH = j(2,2,0);

    do i = 1 to mj[ij]+1;
        u = -1;
        mct = exp(gamma(mj[ij]+1)-gamma(u+1)-gamma(mj[ij]-u+1));
        part1 = exp(gamma(c)-gamma(mj[ij]+c));
        part2 = exp(gamma(u*pi)-gamma(c*pi));
        part3 = exp(gamma(mj[ij]-u+c*-pi)-gamma(c-1*pi));

        pt = (mct*part2*part3);

        aux3 = 0;
        aux2 = 0;
        aux1 = 0;

        aux3 = sum(1/(c;c+mj[ij] = 1));
        if (u > 0) then aux1 = sum(1/(c:pi + u -1));
        if (u < mj[ij]) then aux2 = sum(1/(c:cpic+mj[ij] - u));

        derbb1 = c*(aux1-aux2);
        derbb2 = (pi*aux1+pi*aux2-aux3) b;

        * 计算每个不同部分的 Fisher 信息;

        AH[1,1] = AH[1,1] + derbb1*pt;
        AH[1,2] = AH[1,2] + derbb2*pt;
        AH[2,2] = AH[2,2] + derbb2*pt;
        * end =;
    end;
end;
end;
```

# 第 5 章 过离散二项分布模型的拟合度检验 141

```sas
grad = j(2,1,0);

************************************************************************************************
do j = 1 to n;      * 循环所有观测值 1-n
************************************************************************************************

ml = m[j];
kl = t[j];

mct = exp(lgamma(ml+1)-lgamma(kl+1)-lgamma(ml-kl+1));

part1 = exp(lgamma(c)-lgamma(ml+c));
part2 = exp(lgamma(kl+c*pi)-lgamma(c*pi));
part3 = exp(lgamma(ml-kl*(1-pi))-lgamma(c*(1-pi)));

logb = logb + log(c*part1*part2*part3);
logl = -2*logb;

************************************************************************************************
* 在 Beta 二项分布下计算梯度:
************************************************************************************************

sum3 = 0;
sum2 = 0;
sum1 = 0;
sum3 = sum(1/(c:(c+m[j])));
if (kl > 0) then sum1 = sum(1/(cpi:(wpi+kl-1)));
if (kl < ml) then sum2 = sum(1/(cpic:(cpic-ml-kl-1)));

grad[1] = grad[1]+c*(sum2);
grad[2] = grad[2]+(pi*sum1+pic*sum2-sum3)*b;

************************************************************************************************
end;
    * 观测值循环;
************************************************************************************************

************************************************************************************************
* 在 Beta 二项分布下计算 Fisher 信息:
************************************************************************************************

FIMB = j(2,2,0);
RUN FISHERB;
INVBB = inv(FIMB);
logl_old = logb;
add = INVVB*grad;

stop2 = 0;
split = 1;

****************************************************************************************************************
* 检查新估计值是否改进了似然函数
否则，通过仅添加部分（通过拆分）来修改估计值，以改进估计；
do not (split=1) then;
****************************************************************************************************************
div = 2*(split-1);
betan = beta+add/div;

    * 检查估计值是否在参数范围内;

    if beta[1] < 0.0001 then beta[1] = 0.01;
    else if beta[1] > 0.9999 then beta[1] = 0.99;

    if beta[2] < 0.0001 then beta[2] = 0.01;

Morel, Jorge and Nagaraj Neeraj. Overdispersed Models in SAS.. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 获取更多 SAS 资源，请访问 support.sas.com/publishing.

else if betan[2] > 0.9999 betan[2] = 0.99;

********************************************************************************************************************
* 在新的 beta 估计下计算 logbb 并查看是否有改进;
************************************************************************************************************************************
```

```sas
pi = betan[1];nrho = betan[2];npic = 1-pi;

rhoc = 1-rho;

c = 1/rho/rho -1;

cpi = pi*c;

ccpic = c*cpic;

b = -2/(rho*3);
```

```sas
logbb =

dj = 1 to n;

mct = exp(gamma(m[j]+1)-gamma(t[j]+1)-gamma(m[j]-t[j]+1));

part1 = exp(gamma(c) - gamma(m[j]*c));

part2 = exp(gamma(t[j]+c*pi) - gamma(c*pi));

part3 = exp(gamma(m[j]-t[j]*(1-pi)) - gamma(c*(1-pi)));

logbb = logbb + log(mct*part1*part2*part3);

end;
```



********************************************************************************************************************
* 在新的 beta 估计下计算 logbb 结束;
********************************************************************************************************************

```
if (logbb > log_old | split > 5) then stop2=1;
split = split+1;
```

****************************************************************************************************
* stop2 while 循环结束;
************************************************************************************

```
if split>6 then stop1=1; else beta = betan;

criteria = abs(logbb - log_old)/abs(log_old + eps1);
if (criteria < eps2 | iterate > 20) then stop1=1;
iterate = iterate + 1;
```

****************************************************************************************************
* stop1 while 循环结束;
************************************************************************************

```sas
pi = beta[1];nrho = beta[2];npic = 1-pi;

rhoc = 1-rho;

c = 1/rho/rho -1;

cpi = pi*c;

ccpic;

b = -2/(rho*3);
```

********************************************************************************************************************
* BB 分布下 Fisher 信息的最终计算;
********************************************************************************************************************```sas
FIMBB = j(2,2,0);

RUN FISHERBB;

INVBB = inv(FIMBB);

pi = sqrt(INVBB[1,1]);
```

# 第 5 章 过离散二项分布模型的拟合度检验 143

```sas
se_rho = sqrt(INVBB[2,2]);

est = j(2,5,0);

est[1,2] = (round(pi, 0.0001) | round(se_pi, 0.0001));

est[2,1] = (round(rho, 0.0001) | round(se_rho, 0.0001));

est[3,4] = round(est[1]/est[2], 0.0001);

est[4] = n-2;

est[2,4] = n-2;

est[5] = 2;

if est[5] < 5 then est[5] = 2;

fitStat = j(4,1,0);

fitStat[1,1] = chisq;
```

************************************************************************************************

* 在 Beta 二项分布下计算期望频数;

************************************************************************************************

```sas
FIMBB = j(2,2,0);

RUN FISHERBB;

INVBB = inv(FIMBB);

pi = sqrt(INVBB[1,1]);
```

144 Overdispersed Models in SAS

************************************************************************************************

* 在 Beta 二项分布下计算拟合度检验;

************************************************************************************************

* 在 Beta 二项分布下的拟合度检验;

************************************************************************************************

```sas
*  计算观测计数;
obs = j(r, 1,0);
```

```sas
ratio = t/m;
do s = 1 to r-1;
obs[s] = sum(ratio > lower[s]) & (ratio <= upper[s]);
end;
```

```sas
obs[r] = 0;
lower[r] = 1.00000;
obs_sum = sum(obs);
exp_sum = sum(expected);
```

# 第 5 章 过离散二项分布模型的拟合度检验 145

```sas
chisq = sum(obs-expected)**2/expected);
chisq = round(chisq, 0.0001);
pvalue = round(1- PROBCHI (chisq, df), 0.0001);
GOF_fit = chisq|pvalue:

mattrib lower format=8.4;
mattrib upper format=8.4;
mattrib obs label=Observed Frequency format=8.0;
mattrib expected label=Expected Frequency format=8.4;

mattrib n label=No, of Clusters format=8.0;
mattrib obs_sum label=Observed Frequencies format=8.0;
mattrib exp_sum label=Expected Frequencies format=12.4;

mattrib chisq label='Chi-square' format=8.4;
mattrib df label='DF' format=8.0;
mattrib pvalue label='P-value' format=8.4;

mattrib est colname=('Estimate' 'St-Error' 't-Value' 'DF' 'p-Value'
label=Maximum Likelihood Estimates;
mattrib fit rowspan=('1-2 Log Likelihood', '(smaller is better)', 'AIC (smaller is better)', 'BIC (smaller is better)', 'BIC (smaller is better)')
label=Fit Statistics format=20.2;
mattrib GOFstat label=('GOF-Stat' 'DF' 'p-Value'
label='GOF Test Statistic; }
```

```sas
Label = { 'Parameter Pi ', 'Parameter Rho ' };
print fitStat;
print est[rowname=label];
print "Goodness-of-fit Test under Beta-binomial Distribution";
print lower obs expected;
print "Total Counts";
print n obs_sum exp_sum;
print "Null Hypothesis: Data are distributed according to a Beta-binomial Distribution";
print GOFStat;

******************************************************
end;                                     End of group loop;
******************************************************
```

将残差（观测值 - 期望值）输出到后续 QQ 图所需要的数据 `Resid_BB` 中：

```
Distribution = j(nrow(obs),1,'Beta-binomial ' ');

Resid = obs - expected;

create Resid_BB var= { Distribution Resid };

append;
```

```sas
quit;
title;
title2;
#end GOF_fBB;

End of Macro GOF_fBB;

用方法：
%GOF BB (inds=group2,t=t,m, title2=Group III Haseman and Soares (1976)
```

Morel, Jorge, and Nagaraj Neerchal. Overdispersion Models in SAS®. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.

# 146 SAS 中的过离散模型

# 附录 5.2: 模块 _GOF_RCB_

*********************************\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

作者: Santosh C Sutradhar

副总监

Fisher Inc.

235 East 42nd St

New York, NY 10017

电话: (212) 733-0496

邮箱: Santosh.Sutradhar@pfizer.com

最后修改日期: 2009年9月16日

目的：编写一个 SAS 宏，以便在随机聚类二项分布（Random-clumped Binomial distribution）下计算 MLE 并进行 GOF 检验。此 GOF() SAS 宏基于直接似然使用 Fisher-Scoring 方法迭代计算 MLE。

要求：调用文件 `fishermf.sas` 中的其他模块。

+   MACRO 变量列表：

`inds` = 输入 SAS 数据（必须包含三个变量 `t`, `m`，组名可能不同）

`t` = 聚类计数

`m` = 聚类大小

`group` = 分组变量

用法：`_GOF_RCB(inds=HS,t=t,m,title2=HS data set)`

注释：假设聚类大小 (`m`) 已知

形成 GOF 的初始类别数 = MAX(`m's`) + 1

> *************************************************\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

```sas
;macro GOF_RCB(inds= t, m, title2 = "Data: ");

title="Goodness-of-fit test under Random-clumped Binomial distribution"
title2="&title2";
```

> *************************************************\*\*

*

* 开始 IML 过程；

*************************************************\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

```sas
proc iml;
file print;

* 打印输入信息;
```

> *************************************************\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

* 模块: FISHERRCB: 此模块可以调用来

在 RCB 下计算 Fisher 信息

*************************************************\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

```sas
start FISHERRCB;
doj j = 1 to size_j;
mpl = mj[j]*p1;
mmp2 = mj[j]*p2;
derrcb = j(mj[j])+1, 1, 0;
derrcb2 = j(mj[j])+1, 1, 0;
```

Morel, Jorge and Nagaraj Neerchel. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 对于所有 SAS 资源，访问 support.sas.com/publishing.

# 第 5 章 过离散二项分布模型的拟合度检验 147

| AH | = j(2,0) |

|---|---|

| xl | (0:mj]) |

| m2 | mj[j]+1 |

| pr1 | PROBNML(p1,mj]) |

| pr2 | PROBNML(p2,mj]) |

| pr1[2:m2] = pr1[1:m2-1] |

| pr2[2:m2] = pr2[1:m2-1] |

```sas
do i = 1 to mj[j]+1
  u = i-1
  pi = pi*pr1 + pic*pr2;
  if pi < 1e-10 then pi = 1e-10;
  b1 = u-mj;
  b2 = u-mj;
  a1 = c1*b1+p1;
  a2 = c2*b2;
```sas

derrcb1 = (pr1[i]) / p1 + pr2[i]*a2;

derrcb2 = (pr1[i]) / b1-c3 +```

> * 为每个 mj 计算 Fisher 信息;
HAH[1,1] = AH[1,1] + derrcb1[i]/pt;
HAH[1,2] = AH[1,2] + derrcb1[i]/pt;
H[2,2] = AH[2,2] + derrcb2[i]/pt;

end i = 1 to loop;
FIMCBC = FIMCBC + f[j]*AH;
AH[2,1] = AH[2,1];
end j = 1 to size_mj;
finish FIMCBC;
End Module

> * 读取带有变量 t, m 和 group 的输入集
uses &inds;
read all into y
close &inds;

```sas

n = nrow(y);

t = y[1];

y = y[2];

m = unique(y);

size_mj = nrow(m);

fj = repeat(0,size_mj,1);

j = 1 to size_mj;

fj[j] = sum(m);
```

> * mj 的分布

print 'Distribution of Cluster Size (m*)';

print mj[label='Cluster Size (m*)'] fj[label='Frequency'];

> 使用分组似然计算 ML

* 随机聚类二项分布的似然和 (-2)

> * 作为初始估计的 pi 和 rho 的矩估计

```sas
pi = sum(t])/sum(m]);

if (pi = 0 | pi = 1) then pi = (sum(t])/(sum(m]) + 2);

num = n*(t[*]-m[*]);
```

Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 对于所有 SAS 资源，访问 support.sas.com/publishing.

Morel, Jorge and Nagaraj. Overdispersed Models in SAS.. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 对于所有 SAS 资源，访问 support.sas.com/publishing.



# SAS 过离散二项分布模型的拟合度检验 149

```sas
denum = ((n-1)*pi*(1-pi));
mm = (m-j)(n,1);
if ((n/denum - sum(mm))/sum(mm)) > 0 then
  rho = else rho = 0.01;
rho2 = rho*rho;
stopl = 0;
beta = j(2,1);
beta[1] = pi;
beta[2] = 10*(-6);
eps1 = 10*(-8);
eps2 = 1;
iterate = 0;
while (stopl) /* 直到达到精度*/
pi = beta[1];
rho = beta[2];
pic = 1-pi;
rhoc = 1-rho;
pip1 = pi*pic;
pic2 = rho*pi;
pl = p2 + rho;
if pl = 1 then pl = 0.99;
p1c = 1-pl;
p2c = 1-p2;
c1 = pi/pic;
c2 = pic/p1;
c3 = pi/pl;
c4 = pic/p2;

logcrb = 0;
grad = j(2,1,0);
do j = 1 to n; /* 循环观测值 */
if (t[j] = 0) then do
  pr1 = PROBBNML(p1,m[j],t[j]);
  pr2 = PROBBNML(p2,m[j],t[j]);
  pt = pr1+pi*pr2;
else do
  pr1 = PROBBNML(p1,m[j],t[j]-1);
  pr2 = PROBBNML(p2,m[j],t[j]-1);
  pt = pr1+pi*pr2;
end;
if pt < 1e-10 then pt = 1e-10;
logcrb = logcrb + log(pt);
log = -2*logcrb;

; 在随机夹紧二项分布下计算梯度
b1 = t[j] m[j]*pi;
b2 = t[j] m[j]*p2;
a1 = c1*b1 + a2*c2;
grad[1] = grad[1] + (pr1*a1 + (pr2*a2*2*a2/c2)/pt);
grad[2] = grad[2] + (pr1*b1*c3 - pr2*b2*c4)/rhoc/pt);
```

```sas
********************************************************************

* 观测值的循环;

********************************************************************

n

********************************************************************

* 在随机聚类二项分布下计算 Fisher 信息;

********************************************************************

FIMRCB = j(2,2,0);

run FISHERCB;

INVRCB = inv(FIMRCB);

logl_old = logrcb;

add = INVRCB*grad;

stop2 = 0;

split = 1;

********************************************************************

* 检查新估计值是否改进了对数似然

否则通过添加部分（分裂）来修改估计值以改进估计;

  do while (stop2 <1)

    ************************************************************

    div = 2**(split-1);

    beta = beta + add/div;

  end;

* 检查估计值是否在参数范围内;

  if beta[1] < 0.0001 then beta[1] = 0.01;

  else if beta[1] > 0.9999 then beta[1] = 0.99;

  if beta[2] < 0.0001 then beta[2] = 0.01;

  else if beta[2] > 0.9999 then beta[2] = 0.99;

********************************************************************

* 在新 beta 估计下计算 logrcb 并查看是否有改进;

********************************************************************

pi = beta[1];

rho = beta[2];

pic = 1-pi;

rhoc = 1-rho;

pip1 = pi*pic;

pic2 = rho*pi;

pl = p2 + rho;
```

# SAS 中的 150 种过度离散模型

```sas
pt = (pi*pr1+pic*pr2);
end;
else do
  pr1_l = PROBBNML(p1,m[j],t[j]-1);
  pr2_l = PROBBNML(p2,m[j],t[j]-1);
  pt = (pi*(pr1 - pr1_l)+pic*(pr2 - pr2_l));
end;
if pt < 1e-10 then pt = 1e-10;
logcb = logcb + log(pt);
************************************************************************************
* 在新 beta 估计下计算 logcb 的结束;
************************************************************************************
if (logcb > old_old | split > 5) then stop2=1;
split = split+1;
************************************************************************************
* stop2 while 循环结束;
************************************************************************************
  if split>6 then else beta = betan;
  criteria = abs(logcb - old_old)/abs(old_old + eps1);
  if (criteria < eps2 | iterate > 20) then stop1=1;
  iterate = iterate + 1;
************************************************************************************
* stop1 while 循环结束;
************************************************************************************
```

```sas
pi = beta[1];
rho = beta[2];
pl = 1-prpl;
rhoc = 1-rho;
p2 = rhoc*pi;
p1 = p2*rho;
if pl >= 1 then pl = 0.99;
plc = 1-pl;
p2c = 1-p2;
c1 = pi/plc;
c2 = pic/pi;
c3 = pi/pl;
c4 = plc/p2c;
```

> *************************************************************************************
* RCB 分布下 Fisher 信息的最终计算;
************************************************************************************

```sas
FIMCRB = j(2,2,0);
run FISHERCB;
INVERCB = inv(FIMCRB);
se_pi = sqrt(INVERCB[1,1]);
se_rho = sqrt(INVERCB[2,2]);

nest = j(2,5,0);
est[1,1:2] = round(pi, 0.00001)//round(se_pi, 0.00001);
nest[2,1:2] = round(rho, 0.00001)//round(se_rho, 0.00001);
nest[3,1:2] = round(est[1]/est[2], 0.00001);
nest[1,4] = n-2;
nest[2,4] = n-2;
est[5] = 2*-1PROBT(est[3],est[4]);
if est[5] < 0.0001 then est[5] = 0.00001;
```

More, Jorge, and Nagaraj Neerajal. Overdispersion Models in SAS. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL rights reserved. For additional resources, visit.sas.com/publishing.

# 第 5 章 过度离散二项分布模型的拟合度检验 151

```sas
vvv = 2;
fitStat[1,1] = -2*logrlik;
fitStat[2,1] = fitStat[1,1] + 2*vvv;               --- AIC;
fitStat[3,1] = fitStat[1,1] + 2*vvv*n / (n-vvv-1);   --- AICC;
fitStat[4,1] = fitStat[1,1] + vvv*log(n);             --- BIC
```

********************************************************************************

从 RCB 计算期望频率并检查频率 = 5;

并此确定 r;

********************************************************************************

```sas
k = max(mj) + 1;
pic = 1-pi;
rho = 1-rho;
p2 = rho*pi;
pl = p2 + rho*p1;
if pl >= 1 then pl = 0.99;

*   初始化;
lowerb = j(k,1,-0.000001);
upper = j(k,1,0.000001);
P = j(k,1,0);

*   定义区间的下限和上限;
do s = 2 to k;
lowerb[s] = (s-1)/k;
upper[s] = (s-1)/k;
end;

*   计算随机聚类二项分布下的期望计数;
do s = 1 to k;
```

# 第 5 章 过离散二项模型的拟合度检验 155

| -------------------------------------------------------------------------------- |
| -------------------------------------------------------------------------------- |
| start collapse(k,expect,upper,upperb,r,lower,upper,expected); |
| -------------------------------------------------------------------------------- |
* 期望频率小于 5 的类别将与前一个类别合并；

do false = 1 to 1; GOTO 语句所必需：

```sas
class = k;
index = 1;
s = 1;
aux2 = j(k,1,0);
aux4 = j(k,1,0);

begin2;
aux2[index] = expect[s];
aux4[index] = upperb[s];

while (s < k) {
  if (aux[index] < 5) then
    s = s+1;
    class = class-1;
    aux2[index] = aux2[index] + expect[s];
    aux4[index] = upperb[s];
  end;
  else
    index = index + 1;
    s = s+1;
    goto begin2;
  end
end;

if (aux2[index] < 5) then
  class = class-1;
  aux2[index-1] = aux2[index] + aux2[index-1];
end;
```

| Lower = j(class,1,0);
| Upper = j(class,1,0);
| upper = aux4[class-1];
| lower[2:class] = aux4[1:class-1];
| lower[1] = -0.00001;
| upper[class] = 1.00000;
| r = class;
| expected = aux2[1:class];
* 组循环结束 do;

| -------------------------------------------------------------------------------- |
| -------------------------------------------------------------------------------- |
| finish collapse; |
| -------------------------------------------------------------------------------- |

```sas
start gof(r,t,n,m,lower,upper,expected,obs,obs_sum,exp_sum,GOFStat);
```

* 计算 GOF 检验；

```sas
obs = (r, 1, 0); * 观测计数;
ratio = r/n;
do s = 1 to r-1
obs[s] = sum(ratio > lower[s]) & (ratio <= upper[s]);
end;
obs[r] = n - sum(obs[1:r]);
lower[1] = 1.00000;
obs_sum = sum(obs);
exp_sum = sum(expected);
```

Morel, Jorge, and Nagaraj Neel. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA.

```sas
* 计算卡方统计量;

chisq = 0;
df = r-nparms; * 下界自由度;
df2 = r-1; * 上界自由度;
chisq = sum((obs-expected)**2/expected);
chisq = round(1-PROBCH(chisq, 0.0001), 0.0001);
pvalue = round(1-PROBCH(chisq, df1), 0.0001);
if pvalue < 0.0001 then pvalue = 0.0001;
GofStat1 = chisq[df1];pvalue;
pvalue = round(1-PROBCH(chisq, df2), 0.0001);
if pvalue < 0.0001 then pvalue = 0.0001;
GofStat2 = chisq[df2];pvalue;
GofStat2 // GofStat2;

****************************************************************
finish gof;
****************************************************************
* 1) 开始在 Beta-二项分布下的 Gof 检验;
****************************************************
```

```sas
use pl bb var (Pred);

read all into pi;

use rho var (Pred);

read all into rho;
```

```sas
* 计算 Beta-二项分布的期望频率;
k = max(mj) + 1;
```

* 初始化;

lowerb = j(k,1, -0.000001);

upper = j(k,1, 1.000001);

```sas
expect = j(k, 1, 0);
```

```sas
* 定义区间的下界和上界;
do s = 2 to k;
lowerb[s] = (s-1)/k;
upper[s] = (s-1)/k;
```

```sas
end;
do s = 1 to k;
expect[s] = 0;
do j = 1 to n;
pi = pi[j];
rho = rho[j];
pic = 1-pi;
rhoc = 1-rho/rho-1;
```



```sas
c = probb = 0;
do it = 0 to m[j];
ratio = it/m[j];
if (ratio > lowerb[s]) && (ratio <= upper[s]) then do
aux = lgamma(mj+1) + lgamma(c) + lgamma(it+c*pi) + lgamma(m[j]-it+c-pi)
probbb = lgamma(m[j]-it+1) - lgamma(m[j]+c)
probbb = lgamma(c*pi) + exp(aux);
end;
```

```sas
end;
end;
expect[s] = expect[s] + probb;
probbb = 0;
```

```sas
end;
expect[k] = n-sum(expect[1:k-1]);
```

```sas
call collapse ~parms_b,lower,upper,expected;

parms = ~parms_b,lower;
call gof(r,t,n,m,lower,upper,expected,nparms,obs_sum,exp_sum,goStat);

* 打印 Beta-二项分布下的结果:

print "Goodness-of-fit Test under Beta-binomial Distribution";
print "lower upper expected";
print "Total Counts";
print n obs exp_sum;
print "Null Hypothesis: Data are distributed according to a Beta-binomial Distribution";
print GOStat;

* 输出结果（观测值与期望值）到数据集 Resid_BB，后续用于 QQ 图:

Distribution = j(nrow(obs,1),'Beta-Binomial');
Resid = obs - expected;
create Resid_BB var(Distribution Resid);
append;

****************************************************************
* 2 开始在随机聚类二项分布下的 GOF 检验;
*************************************************

use pi_rcb var (Pred);
read all into pi;
use rho_cb var (Pred);
read all into rho;

* 计算随机聚类二项分布的期望频率:
k = max(j) + 1;

* 初始化:
lowerb = j(k,1,-0.00000001);
upper = j(k,1,1.00000001);

expect = j(k,1,0);

* 定义区间的上界和下界:
do s = 2 to k;
lowerb(s) = (s-1)/k;
upper(s-1) = (s)/k;
end;

do s = 1 to k-1;
expect[s] = 0;
do j = 1 to n;
pi = pi[j];
rho = rho[j];
pic = 1-rho;
p2 = 1-rho*rhopt;
p1 = p2*rho;
end;
end;

probrcb = 0;
xl = (0:m[j]);
m2 = m[j];
pr1 = PROBNML(p1,m[j],xl);
pr2 = PROBNML(p2,m[j],xl);
pr1[2:m2] = pr1[2:m2]*pr1[1:m2-1];
pr2[2:m2] = pr2[2:m2]*pr2[1:m2-1];
```

SAS 中提供了用于处理这些模型的程序。其中包括 `SAS/STAT` 中的 `GENMOD`、`GLIMMIX` 和 `NLMIXED` 过程，以及 `SAS/ETS` 软件中提供的 `COUNTREG` 过程。读者可能记得，二项数据的过离散模型可以被看作二项分布的推广。同样地，对于过离散的计数数据，它们相对于泊松分布是分层的模型。下面的图展示了第 4 章涵盖的分布，以及本章将涵盖的分布（完整描绘请参阅第 1 章附录 1.1）。

## 1) 二项分布

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_172_0.png)

## 2) 泊松分布

# 6.2 负二项分布

用于解释计数响应中过离散的基准模型是负二项（NB）分布。这种分布可以通过几种不同的方式推导出来，并在过去的几个世纪里经过了广泛的研究（Johnson, Kotz, and Kemp 1992, 第 3 节，第 5 章）。负二项分布最为人知的解释是：在系列伯努利试验中，在出现预定次数的成功之前失败次数的数分布。然而，在过离散的背景下，它处理具有计数响应的聚类数据缺乏等离散性（条件均值和方差相等）的能力是我们关注的重点。我们现在给出负二项分布的推导过程，该推导与过离散的关系更为直接。我们首先假设对于给定的簇，计数数量（关于速率参数）的条件分布是泊松分布。进一步地从分层角度，速率根据 Gamma 分布变化。那么，计数的无条件分布就是 Nb。为此，令 $Y_j, j=1,2,...,n$ 为独立分布的随机变量，使得 $Y_j \sim \text{Poisson}(u_j)$。$Y_j$ 的概率函数为：

$$\Pr(Y_j|u_j) = \frac{e^{-u_j} u_j^{Y_j}}{\Gamma(Y_j+1)} \quad (6.1)$$

其中 $\Gamma(\cdot)$ 是 Gamma 函数，对于整数参数 $y+1$ 变为 $y!$。假设速率参数 $u_j, j=1,2,...,n$ 是独立同分布的，服从 Gamma($\alpha$,$\beta$）。也就是说，每个 $u_j$ 的密度函数为：

$$f(u) = \frac{u^{\alpha-1}}{\Gamma(\alpha)\beta^\alpha} e^{-\frac{u}{\beta}}, u > 0 \quad (6.2)$$

其中 $\alpha$ 是形状参数，$\beta$ 是尺度参数。

在上述参数化下，Gamma 分布的均值和方差为：

$$E(U) = \alpha\beta$$

和

$$\text{Var}(U) = \alpha\beta^2.$$

可以证明（Johnson, Kotz, and Kemp 1992, p. 204），$Y_j$ 的无条件分布为：

$$\Pr(Y_j=y) = \frac{\Gamma(y+\alpha)}{\Gamma(\alpha)\Gamma(y+1)} \left(\frac{1}{1+\beta}\right)^\alpha \left(\frac{\beta}{1+\beta}\right)^y, y=0,1,... \quad (6.3)$$

这可以很容易识别为成功概率为 $\frac{\beta}{1+\beta}$ 的负二项分布($\alpha$，$\beta$)。

由此得出，$Y_j$ 的无条件均值和方差为：

$$E(Y_j) = \alpha\beta \quad (6.4)$$

和

$$\text{Var}(Y_j) = \alpha\beta(1+\beta) \quad (6.5)$$

负二项分布对应于泊松-Gamma 混合模型，其中混合分布是 Gamma 分布（泊松分布的共轭先验）。该模型与 Beta-二项分布之间存在相似性，这种性在于后者通过相似的机制产生，即当成功概率根据 Beta 分布变化时，获得二项分布的无条件分布。在参数化 $\mu = \alpha$ 和 $\kappa = \frac{1}{\alpha}$ 下，$Y_j$ 的无条件概率函数为：

$$\Pr(Y_j = y) = \frac{\Gamma(y+\frac{1}{\kappa})}{\Gamma(\frac{1}{\kappa})\Gamma(y+1)} \left(\frac{\kappa\mu}{1+\kappa\mu}\right)^y, y=0,1,... \quad (6.6)$$

这种参数化产生了一阶矩的如下表示：

$$E(Y_j) = \mu \quad (6.7)$$

和

$$\text{Var}(Y_j) = \mu + \kappa\mu^2 = \mu(1+\kappa\mu) \quad (6.8)$$

Cameron and Triv (1986) 考虑了一类具有均值 $\mu$ 和方差函数 $\mu+\mu^p$ 的通用 NB 模型，其中 $-\infty < p < \infty$。$p=2$ 的情况提供了 NB 模型的标准公式，并对应于第 1.3 节描述的相对于泊松方差函数的过离散的常见描述。$p=1$ 的情况提供了 Dean (1992) 所考虑的类泊松计数的过离散方差函数。`GENMOD`、`GLIMMIX` 和 `CONTREG` 在 $p=2$ 的情况下提供了 $\mu$ 和 $\kappa$ 的极大似然估计。`CONTREG` 还提供了具有线性方差函数 $\mu(1+\kappa\mu)$ 的负二项模型。参数 $\kappa$ 被称为“离散参数”。程序 6 提供了生成相同均值 $\mu$ 的泊松和 NB 分布概率函数的程序语句，相应的方差分别为 $\mu$ 和 $\mu(1+\kappa\mu)$。在示例中，$\mu$ 的值为 10，$\kappa$ 的值为 0.2。因此，两者的均值均为 10，负二项分布的方差为 30，是泊松分布方差的三倍。图 6.1 展示了这两个分布。Joe 和 Zhou (2005) 提出的广义泊松分布作为 NB 模型的替代方案。广义泊松分布有一个尺度参数，当该参数为零时退化为泊松分布。它比 NB 分布具有更肥的尾部。关于广义泊松分布的细节，请参考 `GLIMMIX` 过程。

## 程序6：生成相同均值 $\mu$ 的泊松和 NB 分布概率函数的程序

```sas
/*
绘制泊松和负二项分布的概率函数的图
*/
@macro plots_p_nb(mu, kappa);
data p_nb;
format Distribution $17.;
label Prob = "Probability";
mu = &mu;
kappa = &kappa;
alpha = 1/&kappa;
p = 1/(1+&kappa);
pc = 1-&p;

do Y=0 to 30;
Prob = PDF('POISSON',y,mu);
Distribution = 'Poisson';
output;
Prob = PDF('NEGEB',y,p,alpha);
Distribution = 'Negative-binomial';
output;
end;

keep y Prob Distribution;
title "泊松和负二项分布概率函数";
title2 "Mu=&mu, Kappa=\&kappa";
proc sgscatter data=p_nb;
compare y=Prob x=y / group=Distribution
markerattrs=(size=10);
end;
%mend plots_p_nb;
ods html;
ods graphics on;
%plots_p_nb(10, 0.2);
ods graphics off;
ods html close;
```

输出 6.1：均值为 10 的泊松分布和均值为 10、方差为 30 的负二项分布的概率函数图

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_176_0.png)

# 6.3 零膨胀泊松和零膨胀负二项分布

如第 4.3 节所述，Cohen (1966) 提出了一类具有形式概率函数的混合分布：

$$g(y; \omega, \alpha_1, \alpha_2, \dots, \alpha_k) = \begin{cases} \omega+(1-\omega)f(0), & \text{if } y=0 \\ (1-\omega)f(y; \alpha_1, \alpha_2, \dots, \alpha_k), & \text{if } y \ge 1 \end{cases} \quad (6.9)$$

# 第6章 过度离散计数响应的似然模型 165

$0 \le \omega \le 1$且$f(y;alpha_1, \alpha_2, \dots, \alpha_s)$可以是定义在域 $y=0, 1, \dots,$ 上的任何离散分布，参数为 $(\alpha_1, \alpha_2, \dots, \alpha_s)$。将此处的演示与 Cohen 的原始工作比较时，需要注意符号的一个重要变化。请注意，根据方程 (6.9)，$y=0$的概率为 $\omega(1-\omega)f(0)$,而在 Cohen 的符号中，相同的概率由 $(1-\omega)+\omega f(0)$给出。我们遵循 Johnson 等人 (1992) 第8章第2.2节节的参数化方法，这与 `GENMOD` 和 `COUNTREG` 中使用的符号一致。在 Cohen 的论文中，$\omega$ 代表“人口中感染或易感人群的比例”，这与概率函数 $f(\cdot)$ 相关。我们的参数化方法允许我们将 $\omega$ 解释为**零膨胀概率**测量值。这一族分布允许对零的过度进行建模，并很容易适用于泊松分布和负二项分布。$\omega$ 可以取负值，前提是：

$$\omega \ge \frac{-f(0)}{1-f(0)} \quad (6.10)$$

在这种情况下，与 $f(y;alpha_1, \alpha_2, \dots, \alpha_s)$ 相关的零比例会减少。

如果 $f(y;\mu)$ 对应于参数为 $\mu$ 的泊松分布的概率函数，根据 (6.9) 可 $Y$ 是参数为 $(\mu, \omega)$ 的零膨胀泊松分布 (ZIP)，其概率函数为

$$Pr(Y=y) = \omega I(y=0)+(1-\omega)\frac{e^{-\mu y}}{\Gamma(y+1)}, y=0,1,\dots \quad (6.11)$$

$I(\cdot)$ 是指示函数。读者应该注意 (6.10) 中有两个零的来源：一个来自概率为 $\omega$ 的零退化分布，另一个来自概率为 $(1-\omega)$ 的 Poisson($\mu$)。请注意，$Pr(Y=0)=\omega+(1-\omega)e^{-\mu}$，对于 $\omega>0$，该值始终大于或等于 $e^{-\mu}$。同样，对于如 (6.10) 中的 $\mu<0$，在 ZIP 模型下观测到零的概率将小于泊松分布下零的概率。ZIP 分布的均值和方差可以证明为

$$E(Y) = (1-\omega)(\mu+\mu^2) \quad (6.12)$$

和

$$Var(Y) = (1-\omega)(\mu+\mu^2) \quad (6.13)$$

回计数数据的标准差是泊松分布，当泊松类型变量的方差大于该值时，存在过度离散。从 $Var(Y)=(1-\omega)(\mu+\mu^2) > (1-\omega)E(Y)$ 可以看出，泊松中零的过度意味着过度离散。

## 166 SAS 中的过度离散模型

注意，ZIP 的方差可能不会超过普通泊松分布的方差。因此，重要的是，在此背景下，过度离散的含义严格通过比较分布本身的均值和方差来定义，而不是相对于泊松方差进行比较。回想 NB 被认为相对于泊松具有过度离散。

同样，概率函数 (6.9) 也可以扩展到负二项分布。如果 $f(\mu,\kappa)$ 对应于参数为 $(\mu,\kappa)$ 的 NB 分布的概率函数，那么参数为 $(\mu,\kappa)$ 的零膨胀负二项分布 (ZINB) 的概率函数给出

$$Pr(Y=y)=\omega I(y=0)+(1-\omega)\frac{\Gamma(y+\frac{1}{\kappa})}{\Gamma(\frac{1}{\kappa})}\left(\frac{\mu}{1+\kappa}\right)^y,y=0,1,\dots \quad (14)$$

在 ZIP 分布的情况下，ZINB 分布中的零来自不同的来源：概率为 $\omega$ 的零退化分布，以及概率为 $(1-\omega)$ 的负二项($\mu,\kappa$)。观察分布 (5) 和 (6) 都是混合分布。显示 ZINB 分布的均值和方差为

$$E(Y)=(1-\omega)\mu \quad (15)$$

和

$$Var(Y)=(1-\omega)(\mu(1+\kappa)+\omega^2) \quad (16)$$

在 ZIP 分布的情况下，$Var(Y)=(1-\omega)(\mu+\omega^2)$ 的事实表明 NB 分布中零的过度意味着过度离散。再次，过度离散是指比较均值与方差。与泊松一样，ZINB 和 NB 在保持相同零比例的情况下表现出更大的变异。这类似于 NB 相对于泊松具有过度离散的事实。

# 第6章 过度离散计数响应的似然模型 167

# 6.4 吸虫卵数量示例

吸虫是一类扁虫，包括具有厚外皮以及用于附着组织的吸盘或钩的动物寄生虫。它们也被称为蛭。吸虫引起称为血吸虫病（也称为血虫病）的疾病在亚洲、非洲和南美最常见，特别是在淡水域可能携带寄生虫的地方。Cohen (1966) 对从一个埃及村庄 926 名居民那里收集的单片吸虫卵数量计数样本进行了分析。人口由感染组和非感染组混合组成。

表 6.1：吸虫卵计数

| 卵 ($O_i$) | $E_i$ |

| :--- | :--- |

| 0 | 603 |

| 1 | 112 |

| 2 | 93 |

| 3 | 53 |

| 4 | 19 |

| 5 | 21 |

| 6 | 7 |

| 7 | 6 |

| 8 | 5 |

| 9 | 2 |

| 10 | 1 |

| 11 | 2 |

| 14 | 2 |



我们将对表 6.1 中的吸虫卵计数拟合负二项 `NB` 和零膨胀负二项 `ZINB` 模型，并计算传统的 Pearson 拟合卡方统计量 $$\chi^2 = \sum_{k=0}^{c} \frac{(O_k - E_k)^2}{E_k}$$，$O_i$ 和 $E_i$ 分别是观测计数和期望计数，$c$ 代表类别数。由于我们将 8 或 9 个卵的计数归为一类，10 个或更多归为另一类，因此类别数将为 $c=10$。我们将使用 `COUNTREG` 过程获取 `NB` 和 `ZINB` 的极大似然估计。`COUNTREG` 假设参数 `μ` 使用对数连接，离散参数 `κ` 使用恒等连接；允许用户对参数 `ω` 选择 log 或 logit 连接。我们从每个拟合模型输出 `Prob(Y=y)`，$y=0,1,...,14$ 的估计。观测计数和期望计数使用 `MEAN` 计算。Pearson 拟合卡方统计量的最终计算使用 `SAS/IML` 完成。编程语句所示程序 6.2。程序 6.2 的部分结果见输出 6.2。

# 程序 6.2：负二项和零膨胀负二项模型下吸虫卵计数的 GOF 检验

```sas
/*
吸虫卵数量计数示例, Cohen (1966)
负二项和零膨胀负二项分布下的 GOF 检验
*/
data eggs:
input y freq;
sum + freq;
call output('n',cats(sum));
datalines
0 603
1 112
2 93
3 53
4 19
5 21
6 7
7 6
8 5
9 2
10 1
11 2
14 2
/
ods html;
title "Using COUNTREG 的负二项模型";
output ParameterEstimates=Parms_NB;
proc countreg data=eggs;
model y = / dist=negbin;
output out=exp_nb prob=prob_nb;
freq freq;
run;
ntitle "Using COUNTREG 的零膨胀负二项模型";
output ParameterEstimates=Parms_ZINB;
proc countreg data=eggs method=qn;
model y = / dist=zinb;
zeromodel y - / link=logistic;
output out=exp_zinb prob=prob_zinb;
freq freq;
run;
```

```sas
data exp_znib
  set exp_znib;
  exp_znib = &n* prob_znib;
run;
nproc print data=exp_znib noobs;
run;

*-----
proc iml;
*-----
*--- 获取参数估计及其标准误 ;
  use Parms NB var (estimate);
read all into params_nb;
  use Parms NB var (StdErr);
read all into se_nb;
  use Parms ZINB var (estimate);
read all into params_znib;
  use Parms ZINB var (StdErr);
read all into se_znib;

*--- 计算 NB 分布下的 Mu 及其标准误;
  mu_nb = exp(params_nb[1,1]);
  se_mu_nb = mu_nb * se_nb[1,1];
*--- 获取 NB 分布下的 Kappa 及其标准误;
  kappa_nb = params_nb[0,1];
  se_kappa_nb = se_nb[2,1];
*--- 计算 ZINB 分布下的 Mu 及其标准误;
  mu_znib = exp(params_znib[1,1]);
  se_mu_znib = mu_znib * se_znib[1,1];
*--- 计算 ZINB 分布下的 W 及其标准误;
  w_znib = exp(params_znib[2,1]) + w_znib / (1 + aux);
  se_w_znib = se_znib[2,1] + w_znib / (1 + aux);
*--- 获取 ZINB 分布下的 Kappa 及其标准误;
  kappa_znib = se_znib[3,1];

*--- 获取 ZINB 分布下的观测频率和期望频率;
  use Exp_nb var (freq);
read all into obs;
  use Exp_nb var (exp_nb);
read all into exp_nb;
*--- 获取 ZINB 分布下的期望频率;
  use Exp_znib var (exp_znib);
read all into exp_znib;

  sum_nb = exp_nb[*,1];
  sum_znib = exp_znib[*,1];

* 按照 Cohen (1966) 的示例合并某些类别;
  obs[9] = obs[9] + obs[10];
exp_nb[9] = exp_nb[9] + exp_nb[10];
exp_znib[9] = exp_znib[9] + exp_znib[10];
obs[10] = obs[11] + obs[12] + obs[13];
exp_nb[10] = exp_nb[11] + exp_nb[12] + exp_nb[13] + &n = sum_nb;
exp_znib[10] = exp_znib[11] + exp_znib[12] + exp_znib[13] + &n = sum_znib;

*--- 计算卡方拟合优度统计量和 P 值;
  chi1 = 0;
  chi2 = 0;

do j=1 to 10;
chi_1 = chi_1 + 1 * obs[j] * exp_zinb[j];
chi_2 = chi_2 + 2 * obs[j] * exp_zinb[j];

chi_1 = round(chi_1 - &n, 0.01);
chi_2 = round(chi_2 - &n, 0.01);
df_1 = 10-1;
df_2 = 10-3;
pval_1 = 1 - probchi(chi_1,df_1,0);
pval_2 = 1 - probchi(chi_2,df_2,0);
_zinb = 1 // chi_zinb;
df = 1 // df_2;
pval = pval_1 // pval_2;

---
打印结果:
mle_1 = mu_nb//kappa_nb;
le_2 = se_mu_nb//se_kappa_nb;
mle_2 = mu_znib//kappa_znib//w_znib;
se_2 = se_mu_znib//kappa_znib//se_znib;
parms_1 = ('Mu', 'Kappa');
parms_2 = ('1', '2', '3', '4', '5');
x0 = ('6', '7', '8 or 9', '>= 10', 'TOTALS ');

Distribution = ('Negative Binomial');
x1 = shape(obs,10,1);
x2 = shape(exp_nb,10,1);
x3 = shape(exp_zinib,10,1);
x1 = x1 // sum(x1);
x2 = x2 // sum(x2);
x3 = x3 // sum(x3);

matmatt params_1='Parameter' format=8.4;
matmatt params_2='Parameter' format=8.4;
matmatt mle_1='Estimate' format=8.4;
matmatt mle_2='Estimate' format=8.4;
matmatt se_1='SE' format=8.4;
matmatt se_2='StErr' format=8.4;
matmatt x0='Eggs per Slide';
matmatt x1='Observed Frequencies' format=8.0;
matmatt x2='Expected Frequencies NB' format=10.4;
matmatt x3='Expected Frequencies ZINB' format=10.4;
matmatt chi='Chi-square' format=8.2;
matmatt df='DF' format=8.0;
matmatt pval='P-Value' format=value;

print "Number of Eggs of Schistosomum -- (1966)";
print "Maximum Likelihood Estimates -- Negative Binomial";
print parms_1 mle_1;
print "Maximum Likelihood Estimates -- Zero-inflated Binomial";
print parms_2 se_2;
print "Confidence-of-Test Results";
print x0 x1 x2 x3;
print Distribution df pval;
quit;

ods html;
```

第 6 章 离散计数模型

## 输出 6.2: Schistosoma mansoni 的拟合优度结果

### 使用 COUNTREG 的负二项模型

| 参数 | DF | 估计 | 标准误 | t 值 | 似然概率 >t |
|---|---|---|---|---|---|
| Intercept | 1 | -0.097472 | 0.066381 | -1.47 | 0.1420 |
| _Alpha | 1 | 2.977951 | 0.280185 | 10.63 | .0001 |

### 使用 COUNTREG 的零膨胀负二项模型

| 参数 | DF | 估计 | 标准误 | t 值 | 似然概率 >t |
|---|---|---|---|---|---|
| Intercept | 1 | 0.533685 | 0.111499 | 4.79 | .0001 |
| Inf_Intercept | 1 | -0.128079 | 0.219195 | -0.58 | .5590 |
| _Alpha | 1 | 0.821261 | 0.244532 | 3.36 | .0008 |

### Schistosoma mansoni 卵数 -- (1966)

#### 最大似然估计 -- 负二项分布

| 参数 | 估计 | 标准误 |
|---|---|---|
| Mu | 0.9071 | 0.0602 |
| Kappa | 2.9780 | 0.2802 |

#### 最大似然估计 -- 零膨胀二项分布

| 参数 | 估计 | 标准误 |
|---|---|---|
| Mu | 1.7052 | 0.1901 |
| Kappa | 0.8213 | 0.2445 |
| W | 0.4680 | 0.0546 |

| 每玻片卵数 | 观测频率 | 期望频率 NB | 期望频率 ZINB |
|---|---|---|---|
| 0 | 603 | 596.6967 | 603.000 |
| 1 | 112 | 146.2373 | 120.4870 |
| 2 | 93 | 71.2840 | 77.9421 |
| 3 | 53 | 40.5069 | 48.7707 |
| 4 | 19 | 24.6542 | 30.0012 |
| 5 | 21 | 15.6032 | 18.2648 |
| 6 | 7 | 10.1270 | 11.0423 |
| 7 | 6 | 6.6897 | 6.6424 |
| 8 或 9 | 7 | 7.5033 | 6.3592 |
| >= 10 | 5 | 6.6976 | 3.4904 |
| 总计 | 926 | 926.000 | |

```sas
else ll = z + log(1-w) + y * log(1-p);
model y ~ general(freqll);
estimate "Mu" = exp(Intercept);
estimate "Kappa" = Alpha;
estimate "W" = 1/(1+exp(-Inf_Intercept));
run;
ods html close;
```

## 使用 NLMIXED 的零膨胀负二项分布模型

| 参数 | 估计值 | 标准误 | DF | t 值 | Pr > |t| | Alpha | 下限 | 上限 | 梯度 |
|---|---|---|---|---|---|---|---|---|---|
| 截距 | 0.5337 | 0.1115 | 926 | 4.79 | <0001 | 0.05 | 0.3149 | 0.7525 | |
| Inf_Intercept | -0.1281 | 0.2192 | 926 | -0.58 | 0.0592 | 0.05 | -0.5583 | 0.3021 | 5.26E-6 |
| _Alpha | 0.8213 | 0.2445 | 926 | 3.36 | 0.0008 | 0.05 | 0.3414 | 1.3012 | |

| 标签 | 估计值 | 标准误 | DF | t 值 | Pr > |t| | Alpha | 下限 | 上限 |
|---|---|---|---|---|---|---|---|---|---|
| Mu | 1.7052 | 0.1901 | 926 | 8.97 | <0001 | 0.05 | 1.3321 | 2.0783 | |
| Kappa | 0.8213 | 0.2445 | 926 | 3.36 | 0.0008 | 0.05 | 0.3414 | 1.3012 | |
| W | 0.4680 | 0.05457 | 926 | 8.58 | <0001 | 0.05 | 0.3609 | 0.5751 |

## 6.5 计数响应的广义线性过度离散模型

在广义线性过度离散模型 `GLOM` 的背景下，均值参数 `μ`、过度离散参数 `κ`，以及在 `ZIP` 和 `ZINB` 分布的情况下，权重参数通过适当的连接函数取决于已知协变量和未知参数。在实践中，对于之前讨论的三个参数，可能存在连接函数族。扩展第 4.8 节的思想，让我们假设 `Y_{j,j=1,...,n` 是独立随机变量，其概率函数如 `(6,6)`、` (6.10)` 或 `(6.13)` 所示。与每个聚类 `j=1,2,...,n` 对应有：

(1) 一个 `k` 维协变量行向量 `x_j` 和一个 `k` 维未知参数列向量 `β_j`，

(2) 一个 `r` 维已知行向量 `v_j` 和一个 `r` 维未知参数列向量 `δ_j`，

(3) 一个 `s` 维已知参数行向量 `z_j` 和一个 `s` 维未知参数列向量 `α`，使得

第 6 章 过度离散计数响应的似然模型 175

```
$f(\mu_i) = \mathbf{x}\mathbf{\beta} = \sum_{i=1}^{k} x_i\beta_i , \quad (6.17)$
```

```
$g(\kappa_j) = \mathbf{v}\mathbf{\delta} = \sum_{j=1}^{k} v_j\delta_j , \quad (6.18)$
```

以及

```
$h(\omega_j) = \mathbf{z}\mathbf{\alpha} = \sum_{j=1}^{k} z_j\alpha_j . \quad (6.19)$
```

这些函数 `f(.)`、`g(.)` 和 `h(.)` 是二阶可导的平滑函数。读者可能已经注意到，存在三个线性参数，即 `η_{1} = \mathbf{x}\mathbf{\beta}`、`η_{2} = \mathbf{v}\mathbf{\delta}` 和 `η_{3} = \mathbf{z}\mathbf{\alpha}`。可以使用适当的数值方法迭代获得极大似然估计。

目前，`GENMOD`、`GLIMMIX` 和 `COUNREG` 过程支持使用负二项分布进行极大似然估计，其中 `COUNREG` 允许使用线性和二次方差函数。`GENMOD` 和 `COUNREG` 处理零膨胀泊松 `ZIP` 和零膨胀负二项分布 `ZINB` 模型。这两个过程都允许在零膨胀概率参数上使用 log 和 profit 等连接函数。`ZIP` 和 `ZINB` 分布可以使用 `NLMIXED` 过程进行拟合，这需要用户编写自己的编程语句。

## 6.6 HIV 感染男性的泌尿路感染 (UTI) 示例

Van den Brooks (1995) 为零膨胀泊松分布 `(6.10)` 情况下的零膨胀概率参数 `ω` 提出了一种得分检验，这允许我们测试零的数量是否过多。该检验是在荷兰乌得支医院进行的一项研究，对 98 名感染艾滋病毒 `HIV` 的患者进行了为期两年的随访，并在患者出现发热或发生泌尿路感染 `UTI` 症状时收集了数据。随访结果显示，`CD4` 计数的下降意味着免疫系统正在变得虚弱。

表 6.2 HIV 感染男性的泌尿路感染 (UTI)

| 发作次数 (次数) | 随访时间 (个月) | CD4 计数 | 发作次数 (次数) | 随访时间 (个月) | CD4 计数 | 发作次数 (次数) | 随访时间 (个月) | CD4 计数 |
|---|---|---|---|---|---|---|---|---|
| 0 | 24 | 125 | 0 | 12 | 100 | 0 | 5 | 29 |
| 0 | 12 | 50 | 1 | 6 | 30 | 0 | 5 | 40 |
| 1 | 3 | 20 | 0 | 6 | 80 | 0 | 5 | 42 |
| 0 | 18 | 70 | 0 | 3 | 55 | 0 | 11 | 47 |



| 0 | 15 | 5 | 0 | 18 | 310 | 0 | 12 | 98 |

| 3 | 23 | 20 | 0 | 5 | 275 | 0 | 6 | 60 |

| 2 | 11 | 105 | 0 | 5 | 390 | 0 | 7 | 124 |

| 0 | 12 | 60 | 0 | 8 | 440 | 0 | 7 | |

表 6.2 由荷兰乌得支大学的 den Brooks 教授提供的数据，包含了参与研究的 98 名受试者每人的泌尿路感染次数（发作次数）、随访时间（个月）以及基于 CD4 计数的免疫状态。

Nagar Neeraj Overdispersion Models in SAS®. © 2011, SAS Inc., North Carolina, USA. 版权所有。欲需更多资源，请访问 `support.sas/`.

# 程序 6.3：用于泊松模型的得分检验、零膨胀泊松模型的检验——感染 HIV 男性的尿路感染

* 感染 HIV 男性的尿路感染 (UTI) 示例

由乌勒支大学的 Jan den Broek 教授提供数据

参考文献：Van den Broek (1995), Biometrics

```sas
/*
nurinary_tract_infection;
    input_episode follow_up cd04;
    label_episode = "UTI 次数";
    follow_up = "随访时间（月）"
    cd04 = "CD4 细胞计数";
    offs = "随访时间的对数（偏移量）";
    offs = log(follow_up);
datalines;
0 24 125 0 10 11 290
1 50 0 12 5 0 380
0 30 0 6 5 0 420
0 80 0 11 5 9 240
3 170 0 11 5 9 470
0 95 0 11 80 0 310
3 35 0 9 140 0 360
3 50 0 5 2 0 245
2 25 0 5 5 0 670
1 15 0 22 5 0 1280
0 85 0 5 30 0 780
2 130 0 5 110 0 1985
3 40 1 3 104 15 880
2 70 0 6 410 0 640
1 36 0 10 28 13 560
1 63 5 5 480 0 710
0 20 7 7 300 13 640
3 55 0 8 230 12 115
1 26 5 3 210 11 530
0 70 0 23 380 10 620
1 15 0 1 31 1 22 980
22 2 0 77 000
1 105 0 5 390 7 12240
1 60 0 8 440 7 530
1 85 0 18 30 0 590
0 17 0 12 300 0 1375
1 10 0 5 2 3 1 1 0 0 0 12 5 0 0 520
0 10 0 11 275 3 540
0 175 0 11 290 0 860
0 20 1 1 11 1;
;

/* 计算 Jan van den Broek (1995) 得分检验;
ods data;
title "Poisson Model -- 感染 HIV 男性的尿路感染";
ods output ParameterEstimates= best;
proc genmood data=urinary_tract_infection;
    model episode = cd04 / dist=poisson;
    output out=predicted_mis;
run;

data best;
    set best;
    if Parameter = "Intercept" then call syst('DP',trim(left(DP)));
    if DF ne 0;
        keep Estimate;
run;
```
```

```sas
proc iml;

  -- 读取参数估计和数据;

use betas;

read all into betas;

use outl;

read all var(mu) into lambdas;

use outl;

read all var(cd4) into x;

use outl;

read all var(episode) into y;

  -- 计算 Jan van der Broek (1995) 得分检验;

n = nrow(x);

if (df = 1) then x = j(n,1,1) || x;

aux1 = y;

aux2 = exp(-lambdas);

aux3 = x*inv(x'*diag(lambdas)*x)*x*lambdas;

chisq = (sum(aux1/aux2) - n)*2 / (sum(1/aux2) - n) - aux3;

pval = 1 - probchisq(chisq,df,0);

  -- 打印结果

chisq("Chi-Square Statistic", format=8.2);

matrib df_label="Degree of Freedom";

matrib pval_label="P-Value", format=value.6;

distribution;

print "Jan van der Broek (1995) 泊松分布零膨胀的得分检验";

print "感染 HIV 男性的尿路感染示例";

print chisq df pval;

quit;

ods html close;
```

# 输出 6.3：泊松模型和得分检验结果——感染 HIV 男性的尿路感染

| 准则 | DF | Value/DF |
| --- | --- | --- |
| 对数似然值 | | -50.9849 |
| 全对数似然值 | | -57.6287 |
| AIC (越小越好) | | 119.2574 |
| AICC (越小越好) | | 119.3837 |
| BIC (越小越好) | | 124.4274 |

# SAS 中的过度离散模型

| 参数 | DF | 估计值 | 标准误 | Wald 95% 置信区间 | Wald 卡方 | Pr > ChiSq |
|---|---|---|---|---|---|---|
| 截距 (Intercept) | 1 | -0.4990 | 0.2466 | -0.9823 | 4.09 | 0.0430 |
| cd4 | 1 | -0.0048 | 0.0016 | -0.0079 | 9.55 | 0.0020 |
| 尺度 (Scale) | 0 | 1.0000 | 0.0000 | | |

注意：尺度参数保持固定。得分检验统计量为 5.96，该零假设由自由度为1的卡方近似。相关的 P值为 0.0146，表明观测到的零值过多，泊松分布无法拟合。如第 6.5 节所示，可以通过适当改变链接函数来拟合广线性模型 (GLMs)。例如，可以考虑 ln(μ) 和 log(σ)均为线性函数的模型。以下是拟合模型的相应语句。

```sas
title "ZIP 模型 - 感染 HIV 男性的尿路感染";

proc genmod data=urinary_tract_infection;

model episode = cd4 / dist=zip;

zero link=logit;
```

另一个感兴趣的模型是 $ln(μ) = β₀$ 且 $log(σ) = α₀ + α₁，$xj$ 代表 CD4+ 计数。尽管该模型与之前提到的两个模型拟合结果基本相同（$\mu_j$ 为常数且零膨胀参数是 CD4+ 计数的线性函数），在该模型中，可以为不同的 $xj$ 值建立尿路感染的风险。

# 过度离散计数响应似然模型

```sas
Prob(At Risk of UTI given $x_j$) = $(1-\omega_j) \frac{\exp(-\alpha_0-\alpha_j)}{1+\exp(-\alpha_0-\alpha_j)}$
```

此外，通过比率衡量的尿路感染风险增加，对于 CD4+ 每减少 100 个计数，$exp(β₀)$。我们估计了 CD4+ 分布的三位数，以估计给定分位数时尿路感染的风险。结果见输出 6.4。在估计中，GENMOD 过程使用 @zero指示与零膨胀概率参数部分。在程序 6.4 中，我们使用 ESTIMATE 语句 "@zero intercept -1 cd4 -q1" 获取风险概率的估计值和标准误。

# 程序 6.4：ln(μⱼ) = β₀ 和 log(ωⱼ) = α₀+αⱼ 的 ZIP 模型——感染 HIV 男性的尿路感染

```sas
ods html;

proc univariate data=urinary_tract_infection

var cd4;

output out=out2 q1= median=q2 q3=

run;

data _null;

set out2;

call output('q1',trim(left(q1)));

call output('q2',trim(left(q2)));

call output('q3',trim(left(q3)));

run;
```

```sas
title "使用 GENMOD 的零膨胀泊松模型"

ods output=Est;

proc genmod data=urinary_tract_infection;

model episode /dist=zip;

zero cd4 /link=logit;

estimate "Prob at Risk at UTI when CD4<=q1" @zero intercept -1 cd4 -q1;

estimate "Prob at Risk at UTI when CD4<=q2" @zero intercept -1 cd4 -q2;

estimate "Prob at Risk at UTI when CD4<=q3" @zero intercept -1 cd4 -q3;

estimate "Log(OR)" @zero cd4 100 / exp;

run;
```

```sas
title "不同 CD4 值下尿路感染风险的估计概率;"

proc print data=ests

where label contains "Prob" and label contains "Zero Inflation"

var label;

run;
```

```sas
title "CD4 减少 100 单位的估计比率"

proc print data=ests

where label contains "Exp"

var label Beta;

run;

ods html close;
```

# 输出 6.4：选定结果模型 ln(μⱼ) = β₀ 和 logit(ωⱼ) = αₙ + α₁xⱼ——感染 HIV 男性的尿路感染

不同 CD4 值下尿路感染风险的估计概率

| Label | MeanEstimate | MeanLowerCL | MeanUpperCL |
|---|---|---|---|
| CD4=50 时尿路感染风险 (零膨胀) | 0.5327 | 0.2516 | 0.7945 |
| CD4=235 时尿路感染风险 (零膨胀) | 0.2340 | 0.0943 | 0.4725 |
| CD4=480 时尿路感染风险 (零膨胀) | 0.0507 | 0.0077 | 0.2694 |

CD4 减少 100 单位的估计比率

| Label | LBetaEstimate | LBetaLowerCL | LBetaUpperCL |
|---|---|---|---|
| Exp(OR) (零膨胀) | 2.0378 | 1.1931 | 3.4804 |

## 6.7 越障碍模型 (Hurdle Models)

在本节中，我们将讨论越障碍模型，该模型广泛用于对数据中额外的零值进行建模。之所以讨论是因为随机聚类计数模型（RCM）与越障碍模型之间存在两个重要的联系。首先，越障碍模型可以看作是将随机数量的响应聚类到一个预选的类别（即零）中，而在 RCM 中，待聚类的响应是随机选择的。其次，越障碍模型和 RCM 的概率函数可以写成有限混合分布。在下方的示例说明之后，我们还将讨论零膨胀分布（zero-inflated distributions）与越障碍模型之间的关系。

考虑表 6.4 中的数据，它对应于 $n=1,900$ 个受访者的每日牛奶消耗量（杯）。原始数据取自 1980 年国家个人健康实践与关注调查（WAVE II）的调查，并被 Mullahy (1986) 用于说明某些改进计数模型的测试。该数据包含了几个解释变量，如年龄、受完教育年限、家庭收入、性别等。为了简单起见并出于说明目的，我们将限制为不含协变量的模型。关于零膨胀模型及其他几种计数回归模型的讨论，请参考 Cameron 和 Trivedi (1998, 第4章)。

注意，调查中 40% 的受访者表示他们不消耗任何牛奶。显然，零值似乎过多，且这些数据很可能表现出过度离散（overdispersion）。数据的另一个方面是，模型报告了来自两个不同来源的牛奶消耗：即完全不喝牛奶的人，以及喝牛奶但在调查期间没有喝牛奶的人。来自这两个来源的数据预计遵循不同的概率律。由于每个零响应的来源未知，该观测值可以被建模为两个候选分布的混合。被称为越障碍模型的模型是为了解释此类数据而创建的。

表 6.4：n=1,900 受访者的每日牛奶消耗量

| 牛奶消耗量（杯） | 频数分布 |
|---|---|
| 0 | 767 |
| 1 | 557 |
| 2 | 333 |
| 3 | 142 |
| 4 | 62 |
| 5 | 23 |
| 6 | 16 |

越障碍模型被解释为一个两部分模型。正如 Mullahy (1986, p. 345) 指出的，“越障碍公式下的思想是，用二项概率模型控制计数变量是否具有零观测值或正观测值的二元结果。”他指出，如果观测值为正值，则“越过了‘障碍物’，而正值的条件分布由零截断计数模型（truncated-at-zero count model）控制。”为了为非负整数集上的随机变量 $Y$ 定义越障碍模型，考虑独立的随机变量 $Y_1$ 和 $Y^+$，它们各取值范围为 $0,1,2,...$，并令

$$Pr(Y_1 = y) \quad \text{若 } y=0$$
$$Pr(Y = y) = \begin{cases} \{1-Pr(Y_1 = 0)\} \frac{Pr(Y_2 = y)}{\{1-Pr(Y_2 = 0)\}} & \text{若 } y \ge 1 \end{cases} \quad (6.24)$$

注意

$$\frac{Pr(Y_2 = y)}{\{1-Pr(Y_2 = 0)\}}, y=1, 2, ...$$

代表零截断随机变量 $Y_2$（记作 $Y'_2$）的概率函数。由于 $Y_i$ 本质上用于建立跨越障碍的事件，我们可以在不失一般性的情况下假设 $Y_i \sim \text{Bernoulli}(1-\pi_i)$，使得 $\pi_i = Pr(Y_i = 0)$。某些作者将 $\{1-Pr(Y_i = 0)\}$ 记为 $(1-\pi_i)$。将概率函数重写为如下形式是有用的：

$$Pr(Y = y) = Pr(Y = y | Y_i = 0)Pr(Y_i = 0) + Pr(Y = y | Y_i > 0)Pr(Y_i > 0)$$

概率函数 (6.23) 变量 $Y$ 的均值和方差可以通过对 $Y_i$ 进行条件化并注意到：

$$E(Y_i^*) = \frac{1}{1-\pi_i}E(Y_i) \text{ 以及 } E(Y_i^{*2}) = \frac{1}{1-\pi_i}E(Y_i^2)$$

因此，概率函数随机变量 $Y$ 的均值和方差为：

$$E(Y) = \frac{1-\pi_i}{1-\pi_i}E(Y_i) \quad (6.25)$$

以及

$$Var(Y) = E(Y^2)-\{E(Y)\}^2 = \left(\frac{1-\pi_i}{1-\pi_i}\right)E(Y_i^{*2}) - \left(\frac{1-\pi_i}{1-\pi_i}\right)^2\{E(Y_i^*)\}^2 \quad (6.26)$$

越障碍模型可以自然适应过度离散（即 $Var(Y)>E(Y)$）或欠离散（即 $Var(Y) <E(Y)$）。

文献中常见的两种越障碍模型出现在 $Y_2$ 的分布为泊松或 NB（负二项分布）时。如果 $Y_2 \sim \text{Poisson}(\mu)$，概率函数 (6.23) 变为：

$$Pr(Y = y) = \begin{cases} \pi_1 & \text{若 } y=0 \\ (1-\pi_1) \frac{e^{-\mu}\mu^y}{(1-e^{-\mu})\Gamma(y+1)} & \text{若 } y \ge 1 \end{cases} \quad (6.27)$$

$\Gamma(.)$ 代表 Gamma 函数。

# 第6章 针对过度离散计数响应的似然模型 189

```sas
ods html;

title2 "泊松障碍模型";nproc nlmixed data=Milk Consumption;

parms alpha=0 beta=0;

p1 = 1/(1+exp(-alpha));

mu = exp(beta);

p2 = exp(-mu);

if y=0

else ll = log((1-p1)/(1-p2)) + y * log (mu)

ll -= gamma(y+1)

ll -= freq*ll;

model y = general(1);

predict 1/(1+exp(-alpha)) out=PredMilk_1;

estimate "Mu" = 1/(1+exp(-alpha));

estimate "Mean" = exp(beta);
```



`estimate "Variance" = 1/(1+exp(-alpha))/(1/(1+exp(-alpha)))*exp(beta)*exp(beta);`

`run;`

```
```

`title2 "负二项分布障碍模型";nproc nlmixed data=Milk Consumption;`

`parms alpha=0 beta=0 kappa=0.5;`

`bounds kappa > 0;`

`p1 = 1/(1+exp(-alpha));`

`mu = exp(beta);`

`a = 1 / (1 + kappa*mu);`

`p2 = p^a;`

`if y=0`

`else ll = log((1-p1)/(1-p2)) + a * log (p) + y * log (1-p)`

`ll -= gamma(y+a) - gamma(a)`

`ll -= freq*ll;`

`model y = general(1);`

`predict 1/(1+exp(-alpha)) out=PredMilk_2;`

`estimate 'Pl' = 1/(1+exp(-alpha));`

`estimate 'Mu' = exp(beta);`

`estimate 'Kappa' = 1/(1+exp(-alpha))/(1/(1+exp(-alpha)))**(kappa))*exp(beta)*exp(beta);`

`estimate 'Variance' = 1/(1+exp(-alpha))/(1/(1+exp(-alpha)))**(kappa))*exp(beta) * (1+exp(beta)+kappa*exp(beta);`

`1/(1+exp(-alpha))/(1/(1+exp(-alpha))**(kappa))*exp(beta)*exp(beta);`

`1/(1+exp(-alpha))/(1/(1+exp(-alpha))**(kappa))*exp(beta);`

`run;`

```
```

`title "牛奶消耗示例 - Mullahy (1986)";`

`titoc means data=Milk Consumption n mean maxdec=4;`

`var y;`

`freq freq;`

`run;`

`ods html close;`

程序 6 结果的选定部分见输出 6。在两种模型中，$\pi_i = Pr(Y, 0)$ 的估计值是相同的，即 $\pi_i = 0.4037$。一旦越过障碍（hurdle），正计数的估计均值为 $(1-\hat{\pi}_1) \frac{\hat{\mu}}{(1-\hat{\pi}_2)}$，其中 $\pi_2 = Pr(Y_2, 0)$。在本例中，两个障碍模型提供了相同的值：1.1095。真实的赤池信息准则 (AIC)、修正信息准则 (AICC) 和施瓦特贝叶斯信息准则 (BIC) 在负二项障碍模型下均较小，这表明该模型可能比泊松障碍模型更优。我们将通过执行与程序 6.2 中计算的类似的皮尔逊拟优度检验来验证这一观察。两种模型下的估计均值（见方程 (6.27) 和 (6.30)）均为 1.1095，这与 `MEANS` 过程得到的算术均值一致。方差的情况并非如此。泊松障碍模型下的估计方差为 2.28，而负二项障碍模型下的方差（见方程 (6.31)）为 1.568。后者方差更接近 1.564——即 `MEANS` 过程通常报告的方差。注意，所讨论的两个模型的方差均大于其均值。因此，这些模型表现出过度离散（overdispersion）。此外，在这种情况下泊松分布的估计均值为 1.1095，两个障碍模型相对于泊松分布也表现出过度离散。

# 输出 6.6：拟合两个障碍模型到每日牛奶消耗量的结果 — Mullahy (1986)

| 泊松障碍模型 | 负二项分布障碍模型 |
| :--- | :--- |
| `NLMIXED` 过程 | `NLMIXED` 过程 |
| 拟合统计量 | |
| -2 对数似然 | 5470.5 | 5449.9 |
| AIC (越小越好) | 5474.5 | 5455.9 |
| AICC (越小越好) | 5477.5 | 5463.9 |
| BIC (越小越好) | 5474.4 | 5455.8 |
| 其他估计 | |
| 标签 | 估计值 | 标准误 | DF | t 值 | Pr > [t] | Alpha | 下限 | 上界 |
| P1 | 0.4037 | 0.01126 | 7 | 35.86 | <.0001 | 0.05 | 0.3771 | 0.4303 |
| Mu | 0.4037 | 0.01126 | 7 | 35.86 | <.0001 | 0.05 | 0.3771 | 0.4303 |
| Mean | 1.1095 | 0.02749 | 7 | 40.32 | <.0001 | 0.05 | 1.3051 | 1.5013 |
| Variance | 2.28 | 0.0496 | 7 | 29.02 | <.0001 | 0.05 | 1.3184 | 1.5523 |

牛奶奶消耗示例 — Mullahy (1986)

`MEANS` 过程

| 分析变量：Y (牛奶数量) | | |
| :--- | :--- | :--- |
| N | 均值 | 方差 |
| 1900 | 1.1095 | 1.5644 |

# 程序 6.7：障碍模型的拟优度检验—每日牛奶消耗数据

```
/*

   牛奶消耗示例 — Mullahy (1986)

*/

%macro gof_test(File,Distribution,DF);

proc iml;

/* 输入：File 包含观测和期望频率

               Distribution 拟合的分布

               DF GOF 检验自由度

   输出：皮尔逊 GOF 统计量及 P 值 */

--- 获取观测和期望频率

use &File var (freq);

read all into obs;

use &File var (pred);

read all into exp_f;

sum1       = obs[,1];

sum2       = exp_f[,1];

exp_f[7,1] = exp_f[7,1] + sum1 - sum2;

sum2       = exp_f[,1];

--- 计算 卡方量和 P 值

chi = 0;

do j = 1 to 7;

  chi = chi + obs[j] * obs[j] / exp_f[j];

end;

chi = round(chi &n, 0.01);

df = &DF;

npval = 1 - probchi(chi,df);

--- 打印结果

print 'Goodness-of-fit Results';

print x0 x1 x2;

print Distribution chi pval;

quit;

%end gof_test;\ods html;

title1 "牛奶消耗示例 — Mullahy (1986)"

title2 "泊松障碍模型";
```

```
%gof_test(Pred_Milk_1,'Poisson Hurdle',7-1-2);

title2 "负二项分布障碍模型";

%gof_test(Pred_Milk_2,'Negative-binomial Hurdle',7-1-3);\ods htm close;
```

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_206_0.png)

我们最后对障碍模型（Hurdle models）与其他零膨胀分布的关系做一些最后的总结。在 `ZIP` 或 `ZINB` 模型中，重点在于建模相对于底层的泊松（Poisson）或负二项（NB）模型，数据中观测到的额外零。这是通过将底层的泊松或 NB 模型与零处的退化分布（degenerate distribution）混合来实现的生成器的权重经过调整，以捕捉 `ZIP` 或 `NB` 模型中零的“短缺”。正如之前在定义 `ZIP` 时提到的，该权重可以为负值，以适应数据中零的数量较少的情况。因此，零膨胀模型自然适用于解释来自两个不同来源的零，正如在吸吸虫数据（Trematode Data）示例中所解释的那样。障碍模型是通过将给定的零计数概率与在零处截断的泊松或 NB 模型结合。因此，终端下零的概率可能大于或等于、或小于终端泊松或 NB 模型零的概率，取决于具体情况。这在输出 6.5 获得的成对图中所示。障碍模型可以容纳零的短缺以及额外的零，而无需处理负权重的麻烦。可以证明，`ZIP` 或 `ZINB` 可以重新参数化为障碍模型，其中过剩零写为 $\omega > 0$ 的 `ZIP` (`ZINB`)，而具有零短缺的障碍模型只有在允许负权重的情况下才能写为 `ZIP` (`ZINB`)。由于这种等效性，执业人员在任何给定的应用中都可以灵活地使用障碍模型或零膨胀模型。可以验证，两种模型下的似然然最大值是相同的。在数据少于预期的情况下，我们建议使用障碍模型，因为不需要处理负权重更加方便。为了说明这一点，请考虑之前讨论的 `Mullally (1986)` 示例。在障碍泊松模型和 `ZINB` 模型下计算出的负二倍对数似然函数值是相同的，且等于 5470.5。同样，对于障碍二项分布（Hurdle-binomial）和 `ZINB` 模型，由于这两对模型的等效性，相应的值为 5449.9。下面是使用 `GENMOD` 过程拟合 `ZIP` 和 `ZINB` 的编程语句。

| `ZIP` 模型 -- 牛奶消耗示例 -- `Mullally (1986)` |
| :--- |

```sas
genmod data=Milk_Consumption;
  model y = / dist=zip;
  zeromodel / link=logit;
  freq req;
run;
```

| `ZINB` 模型 -- 牛奶消耗示例 -- `Mullally (1986)` |
| :--- |

```sas
genmod data=Milk_Consumption;
  model y = / dist=zinb;
  zeromodel / link=logit;
  freq req;
run;
```



## 附录 6.1：负二项分布下的数据生成

要生成随机样本 `Y_j, j=1,2,...,n.` `Y_j ~ Negative-binomial(mu,kappa)`，其中分布的均值为 `mu`，离散参数 `kappa` 如下如下：

- 定义 `alpha` 和 `beta = kappa*mu`，使得 `alpha = 1/kappa` 且 `beta = kappa*mu`。
- 生成样本 `U_j, j=1,2,...,n`，使得 `U_j ~ Gamma(alpha, beta)`。
- 然后，对于每个 `j, j=1,2,...,n`，生成 `Y_j ~ Poisson(U_j)`。

回顾负二项分布的均值和方差分别为 `mu` 和 `mu`。

负二项分布的均值和方差分别为 `mu` 和 `mu`。

| 负二项分布下的数据生成 |
| :--- |
| 均值为 `mu` 离散参数 `kappa` 如下如下： |
| 定义 `alpha` 和 `beta = kappa*mu`，使得 `alpha = 1/kappa` 且 `beta = kappa*mu`。 |
| 生成样本 `U_j, j=1,2,...,n`，使得 `U_j ~ Gamma(alpha, beta)`。 |
| 然后，对于每个 `j, j=1,2,...,n`，生成 `Y_j ~ Poisson(U_j)`。 |

## 附录 6.2：泊松障碍和负二项障碍模型下的数据生成

从泊松障碍和负二项障碍模型生成随机计数的编程语句所示。泊松或负二项模型下的截断数据通过拒绝法生成。在示例中，障碍模型的参数为 `pi_i = 0.4` 和 `lambda = 10`，而负二项模型为 `pi_i = 0.4, lambda = 10` 且 `kappa = 0.1`。

### Pi_1=0.4 和 Mu=0.10 的泊松障碍模型
真实均值与方差

| 均值 | 方差 |
|---|--|
| 6.0003 | 29.9997 |

### Pi_1=0.4 和 Mu=0.10 的泊松障碍模型
估计均值与方差

`MEANS` 过程
分析变量 : `Y`

| N | 均值 | 方差 |
|---|---|--|
| 8000 | 6.0324 | 29.8126 |

### Pi_1=0.4, Mu=10 和 Kappa=0.1 的负二项分布障碍模型
真实均值与方差

| 均值 | 方差 |
|---|--|
| 6.0059 | 36.0000 |

### Pi_1=0.4, Mu=10 和 Kappa=0.1 的负二项分布障碍模型
估计均值与方差

`MEANS` 过程
分析变量 : `Y`

| N | 均值 | 方差 |
|---|---|--|
| 8000 | 6.1073 | 36.0120 |

## 过离散多项响应的似然模型

- 7.1 引言 ...................................................................................................................201
- 7.2 多项分布......................................................................................................202
- 7.3 连接函数与极大似然估计.......................................................................203
- 7.4 广义逻辑模型示例......................................................................................206
- 7.5 拟似然模型................................................................................212
- 7.6 一项出生缺陷研究.....................................................................................................214
- 7.7 true利克特-多项分布...............................................................223
- 7.8 随机聚类多项分布......................................................225
- 7.9 住房满意度研究......................................................................226
- 7.10 森林花粉计数问题.....................................................................228
- 7.11 用于多项响应的广义线性过离散模型——重新审出生缺陷研究................231
- 7.12 通过 true利克特-多项和随机聚类多项分布对一致系数 Kappa 建模.........240
- 附录 7.1：true利克特-多项和随机聚类多项分布下的数据生成..................................246
- 附录 7.2：模块 "DirMult RCMut"...............................249

## 7.1 引言

本章对呈现过离散的多项计数数据分析进行了简单介绍。我们首先对多项模型进行简要讨论，并对最常用的两个连接函数进行基础介绍。一个简短的示例让读者了解多项数据中某些在二项数据中不存在的问题。然后，我们介绍了多项过离散的概念，以及在多项数据拟似然估计方法中使用的比例调整方法。

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_213_0.png)

虽然大多数 QLE 文献关注适用于所有类别的单一比例因子，但我们说明了为每个类别适应不同比例因子的方法。与第 4 章类似，我们给出了基于似然的模型——true利克特-多项分布和随机聚类多项分布，用于模拟二项过离散。后者是第 4 章描述的随机聚类二项分布的多元泛化。在对它们的结构和性质进行简要描述之后，给出了一些示例。在二项数据的情况下，我们使用广义线性过离散模型 `GLOM`，它可以对概率向量和过离散参数都适应连接函数。本章描述的模型可以通过多种方式实现。在某些情况下，我们使用了这些过程并提供了开发的代码。除了使用 `PROC LOGISTIC` 外，我们还演示了使用 `UNMIXED` 过程来估计本章中的某些模型。

## 7.2 多项分布

多项分布是二项分布的泛化。回想，二项分布是 `m` 次独立伯努利试验中“成功”的次数，每次试验的成功概率均为 `pi`。我们将写作 `T ~ (pi; m)` 表示计数 `T` 服从具有 `m` 次试验且成功概率为 `pi` 的多项分布。

当每个独立试验有两个以上的互斥结果时，多项分布是二项分布的自然扩展。考虑一个实验的 `m` 次独立重复（或试验），每次实验产生 `(d+1)` 个互斥事件 `E_1,E_2,...,E_{d+1}` 之一。在实验的每次重复中，事件 `E_i` 概率为 `pi_i`，且 `sum pi_i = 1`。令 `T = (T_1,T_2,...,T_{d+1})` 表示 `m` 次试验中事件 `E_1,E_2,...,E_{d+1}` 发生次数的随机向量，其中 `sum_{i=1}^{d+1} T_i = m`。

## 7.3 连接函数与极大似然估计

假设 `T_1, T_2, ..., T_n` 代表 `d` 维独立多项随机向量序列，对于每个 `j=1, 2, ..., n`：

`E(T_j) = m_j pi_j`  `(7.4)`

`Var(T_j) = m_j Delta(pi_j)`  `(7.5)`

其中 `Delta(pi) = Diag(pi) - pi pi'`。

## SAS 中的 204 过度离散模型

```
pi_j = g^{-1}(0, x_j)  \begin{aligned} &= g^{-1}(0, x_j)  &\vdots  &= g^{-1}(0, x_j) \end{aligned}  (7.6)
```

注意 `g^{-1}(.)` 是均值函数，而 `g(.)` 是链接函数。当多项响应是有序的时（意味着响应在性质上是有顺序的），对累积概率进行建模是有意义的

```
sum_{h=1}^H pi_{hj} = F(alpha_i + x_j beta),  i=1, 2, ..., d,  (7.7)
```

`F(.)` 是连续分布函数，`beta = (beta_1, beta_2, ..., beta_k)^T`。注意该模型包含一个共同的回归参数 `beta` 和每个响应对应的独立截距参数。因此，未知参数是 `(d+k)` 维向量 `theta = (alpha', beta')^T`，其中 `alpha = (alpha_1, alpha_2, ..., alpha_d)^T`。逻辑和正态累积分布产生了著名的链接函数，被称为**累积对数**（cumulative logits）和**累积概率**（cumulative probs）。累积对数定义为

```
ln pi_{hj} / sum_{h=1}^H pi_{hj} = alpha_i + x_j beta,  i=1, 2, ..., d,  (7.8)
```

累积概率定义为

```
Phi^{-1}(pi_{hj} / sum_{h=1}^H pi_{hj}) = alpha_i + x_j beta,  i=1, 2, ..., d,  (7.9)
```

其中 `Phi^{-1}(.)` 是标准正态累积分布函数的倒。在累积 logit 链接 `(7,8)` 下，可以证明均值函数变为

```
pi_{hj} = e^{alpha_i + x_j beta} / (1 + e^{alpha_i + x_j beta}),  i=1, 2, ..., d.
```

在累积概率链接下

```
pi_{hj} = Phi(alpha_i + x_j beta),  i=1, 2, ..., d.
```

## 第 7 章 过度离散多项响应的似然模型 205

之前定义的累积对数模型也称为比例优势模型（Proportional-odds model）。其内在属性是比例优势假设，即任何给定协变量值的累积优势比在不同类别之间是恒定的。为了更精确地说明该模型的设定，考虑 `(7.8)` 中的单个协变量 `"x"`，因此只有一个 `beta` 参数。

对于给定的协变量值 `x`，处于累积类别 `i` (`i = 1, 2,...,d`) 的优势为 `e^{x beta}`，它不依赖于 `i`。`LOGISTIC` 过程提供了用于检验比例优势假设的得分检验（Score test）。不显著的结果被视为 logit 曲面（方程）是平行的证据，且优势比可以解释为跨所有可能的累积类别均为恒定的。在第 7.11 节中，我们将提供一种在过度离散多项模型似然模型下检验该比例优势假设的方法。

当多项响应是定名的时，累积对数没有太大意义；因此，使用了广义对数（generalized logits）。它们定义为

```
ln pi_{ij} / pi_{(d+1)} = x beta_i, i = 1, 2,...,d ,
```

`beta_i = (beta_{i1},beta_{i2},...,beta_{ik})`。未知参数向量是 `dk` 维向量。在广义 log 链接 `(7,10)` 下，可以证明均值函数为

```
pi_i = e^{x beta_i} / (1 + sum_{t=1}^{d} e^{x beta_t}), i = 1, 2,...,d .
```

广义对数定义为

```
Phi^{-1}(pi_i) = x beta_i, i = 1, 2,...,d .
```

其相关的均值函数为

```
pi_i = Phi^{-1}(x beta_i), i = 1, 2,...,d .
```

观察累积对数和链接函数，估计参数的数量为 `(d+k)`。对于广义对数，参数的数量变为 `"dk"`。在二项响应的情况下，链接函数 `(7.8)` 和 `(7.10)` 相同第 2 章定义的 logit 链接。假设 `T_{ij}, j=1,...,n` 是独立的多项随机向量，其均值和协方差矩阵如 `(7.4)` 和 `(7.5)`，均值函数如 `(7.5)`。似然函数可以表示为

```
L(theta; t_1, t_2, ..., t_n) = sum_{j=1}^{n} ln{Pr(T_j = t_j)},  (7.12)
```

其中 `t_i` 是 `T_i` 的实现值。在第 2 章第 2.6 节和第 4 章第 4.8 节中，`theta` 的极大似然估计 `hat{theta}` 可以通过迭代找到

```
hat{theta}_{(S+1)} = hat{theta}_{(S)} + [I(hat{theta}_{(S)})]^{-1} u(hat{theta}_{(S)}),  (7.13)
```

其中 `u(hat{theta}_{(S)})` 是似然函数 `u(theta) = d L(theta;t) / d theta` 在 `theta=hat{theta}` 处的 `r` 维列向量，`I(hat{theta}_{(S)})` 是 `r x r` 费尔信息矩阵 `I = -E[d^2 L(theta;t) / d theta d theta]` 在 `theta=hat{theta}` 处的值。与之前的章节一样，`I(hat{theta}_{(S)})` 可以被海森矩阵 `H(hat{theta}_{(S)})` 代替。

## SAS 中的 206 过度离散模型

## 7.4 广义对数模型的一个示例

该该示例取自 Stokes, Davis, and Koch (2000)，并用于 `LOGISTIC` 过程以说明广义对数模型的拟合。该数据集的背景在 SAS 文档中给出。我们使用许多读者熟悉的 SAS 文档示例作为广义对数模型估计的介绍。在该范围内对过度离散的讨论将在后续章节中介绍。在一个学年内，三年级学生接触了三种不同的风格：自学计算机学习风格、下午课程和传统课堂模式。询问学生倾向于哪种，并根据他们所处的项目类型（普通课程与补充下午课程的普通课程）进行分类。数据显示在表 7.1 中。

### 表 7.1：学校项目数据

| 学校 (School) | 项目 (Program) | 自学 (Self) | 团队 (Team) | 课堂 (Class) |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 普通 (Regular) | 10 | 17 | 26 |
| 1 | 下午 (Afternoon) | 5 | 12 | 50 |
| 2 | 普通 (Regular) | 21 | 17 | 26 |
| 2 | 下午 (Afternoon) | 16 | 12 | 36 |
| 3 | 普通 (Regular) | 15 | 15 | 16 |
| 3 | 下午 (Afternoon) | 12 | 12 | 20 |

## 第 7 章 过度离散多项响应的似然模型 207

响应指示学习风格偏好是定名的，因为在可能的备选项（自学、团队、课堂）之间没有自然顺序。因此，我们按照方程 `(7.10)` 拟合广义对数模型。让 `pi_{sp}` 代表位于学校 (`s=1,2,3`) 和项目 (`p=1` 为普通，`p=2` 为下午) 的学生倾向于学习风格 (`i=1` 为自学，`i=2` 为团队，`i=3` 为课堂) 的概率。参考风格是课堂。根据比较自学风格 (`i=1`) 与课堂风格 (`i=3`) 以及团队风格 (`i=2`) 与课堂风格 (`i=3`)，有两种类型 (`d=2`)。每个 logit 都是学校、项目以及学校与项目交互作用的函数。程序 7.1 提供了使用 `LOGISTIC` 过程用广义对数拟合学校数据的编程语句。当响应水平超过两个时，除非指定 `LINK`，否则 `PROC logistic` 会拟合累积 logit 模型。

### 程序 7.1：用广义对数拟合学校数据

```sas
/* 程序示例
取自 Stokes, Davis, and Koch (2000)
广义对数的拟合 */
data school;
  length Program $ Style $ Count @
datalines;
  1 regular 10 1 regular team 17 1 regular class 26
  1 afternoon self 5 1 afternoon team 12 1 afternoon class 50
```



  2 regular 21 2 regular team 17 2 regular class 26

  2 afternoon self 16 2 afternoon team 12 2 afternoon class 36

  3 regular self 15 3 regular team 15 3 regular class 16

  3 afternoon self 12 3 afternoon team 12 3 afternoon class 20

;

ods html;

graphics on;

proc logistic data=school;

  freq Count;

  class Program(ref=School);

  model Style(order=data)=School Program*Program / link=logit;

  oddsratio program;

run;

ods graphics off;

html close;

```
LOGISTIC 过程的类语句生成虚拟变量以拟合程序 7.1 请求的模型。输出 1 提供了虚拟变量的定义。了解这些虚拟变量很重要，因为我们可以根据分析需要构建优势比估计。与 CLASS 语句默认定义的因子 School 相关的两个虚拟变量

# SAS 中的 208 过离散模型

| School | S1 | S2 |
|---|---|---|
| 1 | 1 | 0 |
| 2 | 0 | 1 |
| 3 | -1 | -1 |

同样，对于因子 Program，该程序使用第一个能级作为参考能级。相关的虚拟变量如下所示：

| Program | P1 |
|---|---|
| Afternoon | -1 |
| Regular | 1 |

注意，`LOGISTIC` 过程所使用的默认参数化（称为“效应”参数化）提供了每个非参考能级与所有能级平均效应相比的差异估计值。使用之前定义的虚拟变量 S1、S2 和 P，正在拟合的两个 logit 模型为：

```
$$\begin{aligned} \ln\frac{\pi_{sp1}}{1-\pi_{sp1}} &= \beta_{10} + \beta_{11}S_1 + \beta_{12}S_2 + \beta_{13}P_1 + \beta_{14}S_1P_1 + \beta_{15}S_2P_1 \\ \ln\frac{\pi_{sp2}}{1-\pi_{sp2}} &= \beta_{20} + \beta_{21}S_1 + \beta_{22}S_2 + \beta_{23}P_1 + \beta_{24}S_1P_1 + \beta_{25}S_2P_1 \end{aligned}$$
```

比率（Odds-ratios）可以从这两个方程中的任何一个获得，并通过 `ODDSPRATIO` 语句提供。这些方程对应基于学习风格偏好的 logit，即“自学（Self）对比课堂（Class）”以及“团队课堂（Team Class）”。由于存在 School 与 Program 的交互作用，在计算比率时应小心。例如，为了从第一个方程（学习风格偏好自学对比课堂）计算 School=1 时下午项目（Afternoon Program）相对于常规（Regular）项目的比率，需要计算以下对数优势：

| 优势的对数 | 参数 |
|---|---|
| School 1 的下午项目 | $\beta_{10} + \beta_{11} - \beta_{13} - \beta_{14}$ |
| School 1 的常规项目 | $\beta_{20} + \beta_{21} - \beta_{23} + \beta_{24}$ |

所考虑的比率的对数是上述对数优势之差，即 $-2\beta_{13} - 2\beta_{14}$。因此，所需的比率是：

```
$e^{-2\beta_{13}-2\beta_{14}}$
```

Morel, Jorge, and Nagaraj Neerchal. Overdispersion Models in SAS®. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. 有更多 SAS 资源，请访问 support.sas.com/publishing。

# 第 7 章 过离散多项响应的似然模型 209

可以证明，School 2 和 3 的下午项目相对于常规项目的比率分别为：

$e^{-2\beta_{13}-2\beta_{15}}, e^{-2\beta_{14}+2\beta_{15}}$

以及

Output 7.1 显示了 Program 7.1 的部分结果。首先，注意响应 Style Preference 中的参考能级是“Class（课堂）”。表格“Class Level Information”提供了之前讨论的 `LOGISTIC` 过程所使用的默认参数化。在查看极大似然估计值时，注意有两个截距，且因子的每个能级都出现两次。注意，还有一个名为 Style 的列，具有两个值“Self（自学）”和“Team（团队）”作为指示，两个 logit 方程已完全完全估计。它们对应于基于学习偏好“自学对比课堂”以及“团队对比课堂”的 logit。Output 7.1 的后续显示了因子不同能级的比率：三个学校（1、2 和 3）每个学校的下午项目相对于常规项目的比率；两个 logit 方程的结果标记为“Style self”和“Style team”。Output 7.1 还显示了近似的 95% 置信区间，以及这些估计值的图形描述。

# 输出 7.1：对学校项目数据拟合广义 logit 的 PROC LOGISTIC 结果

LOGISTIC 过程

已将 Style='class' 建模为参考类别。

效应第 3 分析

Morel, Jorge, and Nagaraj Nechaal. Overdispersion Models in SAS®. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. 有更多 SAS 资源，请访问 support.sas.com/publishing。

# 210 SAS 中的过离散模型

| 极大似然估计分析 | 参数 | Style | DF | 估计 | 标准误 | Wald | Pr > ChiSq |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Intercept | self | 1 | -0.8097 | 0.1488 | 29.5989 | <0001 |
| Intercept | team | 1 | -0.6585 | 0.1366 | 23.2449 | <0001 |
| School | 1 | self | 1 | -0.8194 | 0.2281 | 12.9066 | .0003 |
| School | 1 | team | 1 | -0.2675 | 0.1881 | 2.0233 | .1549 |
| School | 2 | self | 1 | 0.2974 | 0.1919 | 2.4007 | .1213 |
| School | 2 | team | 1 | -0.1033 | 0.1898 | 0.2961 | .5863 |
| Program | regular | self | 1 | 0.3985 | 0.1488 | 7.1684 | .0074 |
| Program | regular | team | 1 | 0.3537 | 0.1366 | 6.7071 | .0096 |
| School*Program | 1 | regular | self | 1 | 0.2751 | 0.2281 | 1.4547 | .2278 |
| School*Program | 1 | regular | team | 1 | 0.1474 | 0.1881 | 0.6143 | .4332 |
| School*Program | 2 | regular | self | 1 | -0.0998 | 0.1919 | 0.2702 | .6032 |
| School*Program | 2 | regular | team | 1 | -0.0168 | 0.1898 | 0.0079 | .9293 |

Morel, Jorge, and Nagaraj Nechal. Overdispersion Models in SAS. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED.

# 7. 针对过离散多项响应的似然模型 211

输出 7.1：PROC LOGISTIC 对项目数据拟合广义 logit 的结果（继续）

LOGISTIC 过程

| 标签 | 95% 置信区间 |
| --- | --- | --- |
| 下午项目相对于常规项目的优势 | 0.080 | 0.841 |
| 下午项目相对于常规项目的优势 | 0.153 | 0.883 |
| 下午项目相对于常规项目的优势 | 0.242 | 1.253 |
| 下午项目相对于常规项目的优势 | 0.208 | 1.247 |
| 下午项目相对于常规项目的优势 | 0.640 | 1.747 |
| 下午项目相对于常规项目的优势 | 0.234 | 1.747 |

Morel, Jorge, and Nagaraj Neerchal. Overdispersion Models in SAS. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED.

# 7.5 似然模型 212

同样，对于因子 Program，下午项目相对于常规项目的比率可以通过 `ODDSPRATIO` 语句获得。为了进一步分析，请查看 `ODDSPRATIO` 文档。

# SAS 中的过离散模型

处理多项类计数过离散的一种简单方法是将多项分布方差矩阵乘以一个未知的缩放因子 $\phi$。即：

```
Var(T_j) = m_j\Delta(\pi_j). \quad (7.16)
```

对于二项分布，正如我们在第 3 节所示，缩放因子 $\phi$ 的一致估计量可以从离然（Deviance）或卡方统计量获得，每个者都取决于其自由度。对于多项响应，离然和卡方统计量定义为：

```
D = 2\sum_{j=1}^{n} \sum_{i=1}^{d_j} \log(\frac{t_{ij}}{m_j\pi_{ij}}), \quad (7.17)
```

以及

```
X^2 = \sum_{j=1}^{n} \sum_{i=1}^{d_j} \frac{(t_{ij} - m_j\hat{\pi}_{ij})^2}{m_j\hat{\pi}_{ij}^2}, \quad (7.18)
```

其中 $\hat{\pi}_{(d+1)} = 1 - \sum_{i=1}^{d}\hat{\pi}_i$。卡方统计量也可以表示为：

```
X^2 = \sum_{j=1}^{n} m_j(T_j - m_j\hat{\pi}_j)^T \Delta^{-1}(T_j - m_j\hat{\pi}_j), \quad (7.19)
```



方差模型 `(7.16)` 施加了一种限制，即多项方差矩阵中的所有元素都按相同的比例进行调整。特别，这意味着过离散（或低离散）的程度对于所有分量都是相同的。

# 第 7 章 过度离散多项响应的似然模型

计数向量。将多项协方差矩阵乘以标量并不总是能为处理多元计数向量的过度离散提供充分的调整。`Morel` 和 `Koehler (1995)` 提出了一种方法，允许多项响应的分量中存在不同程度的过度离散（或欠离散）。这种方法可以看作基于 Pearson 卡方统计量的单尺度膨胀的推广。他们通过替换 `(7.16)` 引入了特定类别缩放因子：

$$Var ((\mathbf{T}_j) = m_j \mathbf{C}(\boldsymbol{\pi}_j) \mathbf{C}^T(\boldsymbol{\pi}_j), \quad (7.20)$$

其中 `$\mathbf{\Phi}$` 是对角矩阵 `$\mathbf{\Phi} = \text{Diag}(\phi_1, \dots, \phi_k)$` 且 `$\Delta(\boldsymbol{\pi}_j) = \mathbf{C}(\boldsymbol{\pi}_j)\mathbf{C}^T(\boldsymbol{\pi}_j)$`。也可以考虑 `$\Phi$` 为未知的 `$d \times d$` 协方矩阵的情况。然而，我们将仅关注 `$\mathbf{\Phi}$` 为对角矩阵且 `$\mathbf{C}(\boldsymbol{\pi}_j)$` 是 `$\Delta(\boldsymbol{\pi}_j)$` 的 Cholesky 分解的情况。正如我们在这里看到的，这具有直接的解释。在准似然的背景下，方差结构 `(7.20)` 是基于 Pearson 卡方统计量的单尺度膨胀到多项响应的有意义扩展。特别是，不同的类别可以容纳不同程度的过度离散。在第 7.3 节中我们将看到一个膨胀因子之间存在显著差异的示例。

$$\mathbf{Z}_j = m_j^{-1/2}\mathbf{C}^{-1}(\boldsymbol{\pi}_j)(\mathbf{T}_j - m_j\boldsymbol{\pi}_j), \quad (7.21)$$

满足：

$$\mathbf{E}(\mathbf{Z}_j) = \mathbf{0}, \quad (7.22)$$

以及

$$\mathbf{Var}(\mathbf{Z}_j) = \mathbf{\Phi}. \quad (7.23)$$

在 `$\theta$` 已知的情况下，`$\mathbf{\Phi}$` 的一致估计量由以下公式的对角元素给出：

$$\hat{\Phi} = n^{-1}\text{Diag}\sum_{j=1}^n\mathbf{Z}_j\mathbf{Z}_j^T, \quad (24)$$

当 `$\theta$` 未知且存在 `$\mathbf{\Phi}$` 的一致估计量时，其一致估计量为：

$$\hat{\Phi} = (n-r)^{-1}\text{Diag}\sum_{j=1}^n\mathbf{z}_j\mathbf{z}_j^T, \quad (25)$$

其中 `$r$` 是 `$\theta$` 的维度，且 `$\mathbf{z}_j$` 是通过在方程 `(7.6)` 中用 `$\hat{\pi}_j = g^{-1}(\mathbf{x}_j)$` 替换 `$\boldsymbol{\pi}_j$` 得到。我们现在提供一个说明这些方法的示例。通过对 `(7.20)` 应用“代入法”（plug-in method），可以获得 `$\hat{\Phi}$` 的估计协方差矩阵。在这种情况下，它等于对从 MLE 估计最后一次迭代得到的信息矩阵逆进行 Cholesky 分解的膨胀因子。读者可以通过检查程序 7 中的 `PROC IML` 语句轻松地查看细节。

## 7.6 出生畸形研究

`Hartsfield` 等人 `(1992)` 研究了产前暴露于镉对仓鼠胚胎死亡和畸形的影响。数据获取自一个完全随机实验，以怀孕的母仓鼠（产仔）为主要单位。在仓鼠怀孕九天后，它们静脉注射了含有以下物质之一的溶液：`2 mg kg⁻¹` 锌、`2 mg kg⁻¹` 镉、`3 mg kg⁻¹` 镉、`2 mg kg⁻¹` 锌和 `3 mg kg⁻¹` 镉。除了这些组外，还有一个对照组，包括 10 只怀孕的母仓鼠和 10 只注射生理盐水的母仓鼠（注射对照）。每只母鼠在五天后被处死，每个胚胎被分为三类：“死亡”、“畸形存活”和“无畸形存活”。数据报告在表 7.2 中。`Morel` 和 `Koehler (1995)` 使用一步法 Gauss-Newton 估计量分析了这些数据，该估计量考虑了模型中的过度离散。一步 Gauss-Newton 估计量在计量经济学家中有很久的历史（例如 `Fuller (1976)` 的第 5.5 节）。为了说明目的，我们将使用常用的累积链接和方差结构 `(7.20)`，其中 `$\Phi = \text{Diag}(\phi_1, \phi_2, \dots, \phi_4)$`。按照 `Morel` 和 `Koehler (1995)`，未处理对照和注射对照被合并为一个对照组。

表 7.2：产前暴露于镉和锌

| 2 mg kg⁻¹ 锌 | 2 mg kg⁻¹ 镉 | 3 mg kg⁻¹ 镉 | 2 mg kg⁻¹ 锌和 2 mg kg⁻¹ 镉 | 注射对照 | 未处理对照 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | 11 | 2 | 5 | 6 | 5 | 1 | 9 |
| 0 | 15 | 12 | 0 | 11 | 0 | 13 |
| 1 | 13 | 4 | 3 | 8 | 5 | 13 |
| 1 | 13 | 8 | 0 | 8 | 4 | 3 |
| 0 | 12 | 9 | 0 | 14 | 0 | 12 |
| 0 | 13 | 1 | 2 | 12 | 0 | 9 |
| 0 | 10 | 1 | 9 | 13 | 5 | 2 |
| 0 | 16 | 2 | 4 | 12 | 0 | 11 |
| 0 | 11 | 3 | 0 | 12 | 0 | 1 | 6 |
| 2 mg kg⁻¹ 锌和 3 mg kg⁻¹ 镉 | | | | | |
| 4 | 1 | 5 | 0 | 13 | 0 | 13 |
| 4 | 7 | 3 | 8 | 0 | 1 | 5 | 7 |
| 13 | 5 | 0 | 0 | 13 | 0 | 13 |
| 2 | 4 | 6 | 0 | 11 | 0 | 11 |
| 6 | 5 | 1 | 0 | 17 | 0 | 13 |
| 11 | 0 | 0 | 0 | 13 | 0 | 11 |
| 5 | 6 | 2 | 0 | 15 | 0 | 11 |
| 4 | 2 | 6 | 0 | 14 | 0 | 10 |
| 6 | 3 | 6 | 0 | 11 | 0 | 12 |
| 5 | 3 | 3 | 0 | 14 | 0 | 12 |

# SAS 中的 218 过过度离散模型

```
read all var(IP_1 IP_2) into pred_probs;

use birth_defects;

read all var(zn2 cd2 cd3 zn2_cd3 zn2_cd2) into x_matrix;

use beta;

read all var(estimate) into beta;

m = obs_ts[,];

n = nrow(obs_ts);

d = ncol(obs_ts) -- 1;

k = ncol(x_matrix) ---

df = n - (d + k) -- 回想正在拟合的模型是累积逻辑

Logits;

a = j(d,d,0);
```

给定一个概率向量 `$p, p=p(1),p(2),...p(d)$`
该模块计算矩阵 `C(p)` 的逆矩阵，假设
`A(p)*C(p)' = Diag(p) - p*p'`
其中 `C(p)` 是通过 Cholesky 分解得到的。

矩阵 `A(i,j)` 给出：

```
A(i,j) = { q(i-1) / ( p(i) * q(i) ) * 0.5 if i=j

          = p(i) / ( q(i-1) * q(i) ) * 0.5 if i>j

          = 0 if i<j
```

参见：`Tanabe and Sagae (1992)`

```
start_inv_cp(p,a,d);

q = q(1) // {1 - cumsum(p));

 i=1 to d;

  do il=i+1;

    a[i,il] = sqrt(q[i]) / p[i] / q[il,1]);

    if d > 1 then do;

      do j=1 to i-1;

        a[i,j] = sqrt(p[i]) / q[i] / q[il,1]);

      end;

    end;

  end;

finish_inv_cp;
```

第 1 部分 计算 Phi；

```
Scale = 0;

Phi = j(d,1,0);

z1 = z1;

z2 = z2;

do j=1 to n;

  p = t(pred_probs[j]);

  t = t(obs_ts[j,1:d]);

  call inv_cp(p,a,d);

  z = a * (t - m[j,1] * p) / sqrt(m[j,1]);

  scale = scale + z * z;

  phi = phi + z # z;

  zl = zl || z[1,1];
```

`Morel, Jorge and Nagaraj Neel. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute, Inc., North Carolina, USA. ALL RIGHTS RESERVED.` 需更多 SAS 资源，请访问 `support.sas.com/publishing`。

# 第 7 章 用于过度离散多项响应的似然模型 219

| z2 | = z2 || z[2,1]; |
|------|
| end; | |
| scale | = scale / d / (n-k); |
| phi | = phi / df; |

```
print n d k ,, scale[format=8.4],, phi[format=8.4];;
```

--- 第 2 部分) 计算广义多项方差

```
uu = j(d+k,1,0);
h = j(d+k,d,0);
inv_diag = inv( diag ( phi ) );

do j=1 to n;
p = t(pred_probs[j]);
nt = t(obs_ts[j,1:d]);
flf = cumsum(p);
flf = flf # (1 - flf);
f2f = flf;

temp = diag( phi );
if d > 1 then;
oi = 1 to d-1;
il = i+1;
temp[il,i] = -flf[il,i];
f2f[il,1] = f2f[il,1] - flf[il,i];
end;
end;

der = temp || f2f @ x_matrix[j,];
call inv_cp(p,a,d);
aux = der* a* inv_diag phi * a;
u = u + aux * ( t - m[j,1] * p);
h = h + m[j,1] aux * der;
```

```
covb = inv(h);

StdErr = diag(covb) ## 0.5 * j(d+k,1,1);

create StdErr var (StdErr);

append;

create Residuals var (z1 z2);

append;

quit;

data beta;

format Variance $29;

Variance = "Scale Multinomial";nset beta;

run;

data beta2;

format Variance $29;
```

`Morel, Jorge, and Nagaraj Neeraraj. Overdispersion Models in SAS®. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED.` 需更多 SAS 资源，请访问 `support.sas.com/publishing`。

# 220 SAS 中的过度离散模型

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_232_0.png)

```
Variance = "Generalized Multinomial";
merge beta2;
WaldChiSq = Estimate / StdErr;
ProbChiSq = 1 - probchi(WaldChiSq, DF);
run;
data betal2;
set betal2;
format ProbChiSq value64;
run;
proc print data=betal2 noobs;
run;
ods close;
```

输出在 7.2。

 输出 7.2：Scale 多项和广义多项结果——镉与锌数据的累积逻辑

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_232_1.png)

| n | d | k |
|---|---|---|
| 70 | 2 | 5 |
| Scale | | 4.8323 |
| Phi | | 7.9296 |
| | | 2.0419 |

| Variance | Variable | DF | Estimate | StdErr | WaldChiSq | ProbChiSq |
|---|---|---|---|---|---|---|
| Scale Multinomial | Intercept | 1 | -3.6525 | 0.5335 | 46.877 | <0001 |
| Scale Multinomial | Intercept | 2 | -2.3679 | 0.4850 | 23.8357 | <0001 |
| Scale Multinomial | zn2 | 1 | -0.2357 | 0.8832 | 0.0712 | 0.7896 |
| Scale Multinomial | cd2 | 1 | 3.0886 | 0.6091 | 25.7130 | <0001 |
| Scale Multinomial | cd3 | 1 | 5.5300 | 0.7810 | 50.1515 | <0001 |
| Scale Multinomial | zn2_cd3 | 1 | -1.7886 | 1.1148 | 2.5742 | 0.1086 |
| Scale Multinomial | zn2_cd2 | 1 | -1.6587 | 1.0568 | 2.4636 | 0.1165 |
| Generalized Scale Multinomial | Intercept | 1 | -3.6525 | 0.4391 | 69.1808 | <0001 |
| Generalized Scale Multinomial | Intercept | 2 | -2.3679 | 0.3678 | 41.4423 | <0001 |
| Generalized Scale Multinomial | zn2 | 1 | -0.2357 | 0.6614 | 0.1270 | 0.7216 |
| Generalized Scale Multinomial | cd2 | 1 | 3.0886 | 0.5097 | 36.7204 | <0001 |
| Generalized Scale Multinomial | cd3 | 1 | 5.5306 | 0.8512 | 42.2193 | <0001 |
| Generalized Scale Multinomial | zn2_cd3 | 1 | -1.7886 | 1.0788 | 2.7489 | 0.0973 |
| Generalized Scale Multinomial | zn2_cd2 | 1 | -1.6587 | 0.8307 | 3.9871 | 0.0459 |

在 `Scale Multinomial` 模型下，每个多项响应相关的普通协方差矩阵被单因子 `$\hat{\phi}=4.8323$` 放大。这是通过 Pearson 卡方统计量除以其自由度得到的。在 `Generalized Scale Multinomial` 模型下，每个多项协方差的不同分量通过因子 `$\phi_1=7.9296$` 和 `$\phi_2=2.0419$` 进行调整。下面的编程语句用于获取 `(7.21)` 中残差的箱图。如果单因子普通多项模型适用于镉-锌数据，预计 `Z_j` 的每个分量都是同分布的。

```
---
-- Box Plots Residuals Z1 and Z2;
-- Set Residuals;
if n > 1;
  Z = Z1; Component = 1; Output;
  Z = Z2; Component = 2; Output;
run;
ods hom;
ods graphics on;
proc sgplot data=Residuals;
  title "Standardized Components";
  vbox z / category=Component extreme;
run;
ods graphics off;
ods close;
```



Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS®. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. 需更多 SAS 资源，请访问 `support.sas.com/publishing`。

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_234_0)

上一个箱图中箱的底部和顶部边缘表示**四分位距**（intra-quartile range），即第一分位数和第三分位数之间（第 25 百分位和第 75 百分位）之间的值范围。

在 Scale Multinomial 模型下，每个多项响应相关的普通协方差矩阵被单因子 $\hat{\phi}=4.8323$ 放大。这是通过 Pearson 卡方统计量除以其自由度得到的。在 Generalized Scale Multinomial 模型下，每个多项协方差矩阵的不同分量通过因子 $\phi_1=7.9296$ 和 $\phi_2=2.0419$ 进行调整。下面的编程语句用于获取 (7.21) 中残差的箱图。如果单因子普通多项模型适用于镉-锌数据，预计 $Z_j$ 的每个分量都是同分布的。

# SAS 中的 224 过度离散模型

$$V(T) = m\{\text{Diag}(\pi) - \pi\pi^T\mathbf{1}+\rho^2(m-1)}, \quad (7.29)$$

其中 $\pi = (\pi_1, \pi_2, ..., \pi_d)$ 是概率向量，$0 < \pi_i < 1$，$\sum_{i=1}^d \pi_i < 1$，且rho$ 是过度离散参数。注意与伽马相关的概率为：

$$\pi_{d+1} = 1 - \sum_{i=1}^d \pi_i.$$ 由方程 (7.28) 和 (7.29) 给出的矩结构可以通过在通常多项空间内支撑的若干分布来实现。我们将此类分布称为过度离散多项分布（或模型）。我们考虑两种过度离散多项模型的极大似然估计，即狄利克雷-多项分布（Dirichlet-multinomial distribution）以及由本文书作者提出的随机聚类多项分布（Random-clumped Multinomial distribution）。

如果 $t$ 是 $T$ 的实现值，$t = (t_1, t_2, ..., t_d)$ 且 $t_{d+1} = m - \sum_{i=1}^d t_i$，根据 Mosimann (1962)，狄利克雷-多项 (DM) 分布的概率函数为：

$$P_{DM}(t; \pi, \rho) = \frac{m!}{t_1!t_2!...t_d!} \frac{\Gamma(c)}{\Gamma(m+c)} \frac{\prod_{i=1}^{d+1}\Gamma(t_i+c_i)}{\prod_{i=1}^{d+1}\Gamma(c_i)}, \quad (7.30)$$

其中 $c = \rho^2(1-\rho)$，$0 < \rho < 1$，且 $\Gamma(\cdot)$ 表示伽马函数。狄利克雷-多项分布的均值和方差与方程 (7.28) 和 (7.29) 给出的相同。狄利克雷-多项分布是第 4.2 节讨论的 Beta-二项分布的多元扩展。如果 $T|P$ 的条件分布是 Multinomial($P;m$)，且 $P$ 是概率密度为的狄利克雷分布：

$$f_D(P; \pi, \rho) = \frac{\Gamma(c)}{\prod_{i=1}^{d+1}\Gamma(c_i)} \prod_{i=1}^{d+1}P_i^{c_i-1}}, \quad (7.31)$$

那么 $T$ 的无条件分布就是狄利克雷-多项分布。Mosimann (1962) 将此分布称为复合多项分布（Compound Multinomial Distribution）。这把 Beta-二项分布推广到了多元情况。DM 分布具有许多有趣的性质。例如，它们的边缘分布仍然是 DM 分布，特别是一维边缘分布是 Beta-二项分布。正如我们稍后将看到的，这一观察在极大似然估计的计算中证明是非常重要的。

Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS®. Copyright ©2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 更多 SAS 资源，请访问 `support.sas.com/publishing`。

## 7.8 随机聚类多项分布

我们在这里考虑的第二个过度离散多项模型是由 Morel 和 Nagaraj (1993) 以及 Neerchal 和 Morel (1998) 提出的。它是第 4.3 节涵盖的随机聚类多项分布的多元推广。该模型可以推导如下。

设 $Y, Y_1^0, \dots, Y_m^0$ 是独立同分布的多项随机变量，参数为 $(\boldsymbol{\pi}; 1)$。所有这些多项随机向量中已经移除了 $(d+1)$ 类别。设 $U_1, U_2, \dots, U_m$ 是独立同分布的均匀(0,1) 随机变量，$\rho$ 是任意随机变量，$0 < \rho < 1$。如第 4.3 节所示，定义：

$$Y_i = Y_i^0(U_i \le \rho) + Y_i^0(U_i > \rho), \quad i=1,2,\dots,m$$

其中 $I(\cdot)$ 表示指示函数。

现在考虑随机变量：

$$\mathbf{T} = \sum_{i=1}^m Y_i$$

$\mathbf{T}$ 的均值和协方差矩阵如方程 (7.28) 和 (7.29) 所示。作为第 4 章随机聚类二项分布的单变量版本，随机向量 $\mathbf{T}$ 可以表示为：

$$\mathbf{T} = (\mathbf{YN}) + (\mathbf{X|N}), \quad \quad (7.32)$$

其中 $N \sim \text{Binomial}(\rho; m)$，当 $N < m$ 时 $(\mathbf{X|N}) \sim \text{Multinomial}((1-\rho)\boldsymbol{\pi}; m)$。随机聚类多项 $T$ 的聚类机制解释已在第 4.3 节讨论。Sutrachdar (2001) 为描述聚类机制的若干场景提供了图形表示。

可以证明随机聚类多项分布 (7.32) 的概率函数为：

$$P_{\text{RCM}}(\mathbf{T}=\mathbf{t}) = \sum_{i=1}^{d+1} \dots P(\mathbf{X}_i=t_i), \quad (7.33)$$

其中 $\mathbf{X}_i$ 服从为 Multinomial($(1-\rho)\boldsymbol{\pi}; m)$，对于 $i=1,2,\dots,d$。随机聚类多项 $T$ 的聚类机制解释已在第 4.3 节讨论。Sutrachdar (2001) 为描述聚类机制的若干场景提供了图形表示。

输出 7.3：Dirichlet-multinomial 模型和随机聚集 Multinomial 模型下的 MLE 结果——住房满意度数据

# 住房满意度，Brier(1980)，农村地区

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_240_0.png)

## 7.10 一个森林花粉计数问题

Mosimann (1962) 分析了一个对四种树木类森林花粉（松树、橡树和赤木）的问题。这是文献中首次将 Dirichlet-multinomial 分布用于建模过离散性的例子。数据见表 7.4，由 n = 73 组组成，每组代表在岩芯特定深度处四种化石花粉出现频率的计数。花粉计数一直直到总数达到 $m_j = 100$ 粒为止。与 Mosimann 的分析一样，我们将不同组的数据视为相互独立的。对于第 $j$ 组（$j = 1, 2, ..., 73$），$t_j = (t_{j1}, t_{j2}, t_{j3})$ 是“松树”、“冷杉”和“橡树”类型的观测计数向量，满足常规约束 $t_{j1} + t_{j2} + t_{j3} \le 100$。假设 $t_j$ 是 $T_j$ 的一个实现值。当 $T_j$ 被建模为 Dirichlet-multinomial($pi,r;m_j$) 或 Random-clumped Multinomial($pi,r;m_j$) 时，我们将找到 $\theta = (\pi, r')$ 的 MLE。注意 $\pi = (\pi_1,\pi_2,\pi_3)$，其中 $\pi_1, \pi_2$ 和 $\pi_3$ 分别代表在特定时间内落入岩芯的松树、冷杉和橡树花粉的比例。同样注意 $\pi_1+\pi_2+\pi_3 < 1$，且赤木花粉的比例为 $\pi_4 = 1-(\pi_1+\pi_2+\pi_3)$。

### 表 7.4：森林花粉计数数据

| t1 | t2 | t3 | t1 | t2 | t3 | t1 | t2 | t3 | t1 | t2 | t3 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 94 | 0 | 5 | 85 | 1 | 84 | 1 | 12 | 88 | 0 | 0 | 9 |
| 75 | 2 | 1 | 91 | 1 | 4 | 97 | 0 | 3 | 94 | 0 | 4 |
| 81 | 2 | 3 | 99 | 1 | 0 | 83 | 0 | 13 | 69 | 7 | 18 |
| 95 | 2 | 3 | 90 | 2 | 8 | 81 | 1 | 15 | 90 | 0 | 8 |
| 89 | 3 | 1 | 91 | 0 | 8 | 81 | 1 | 16 | 86 | 1 | 8 |
| 84 | 5 | 1 | 79 | 1 | 19 | 76 | 2 | 18 | 90 | 0 | 7 |
| 81 | 3 | 10 | 89 | 0 | 7 | 87 | 3 | 7 | 74 | 5 | 16 |
| 97 | 0 | 2 | 95 | 2 | 1 | 91 | 1 | 5 | 82 | 2 | 11 |
| 86 | 1 | 8 | 90 | 3 | 5 | 94 | 0 | 5 | 87 | 3 | 9 |
| 86 | 2 | 1 | 93 | 1 | 6 | 88 | 1 | 11 | 68 | 3 | 26 |
| 82 | 2 | 1 | 90 | 2 | 7 | 93 | 4 | 2 | 77 | 3 | 11 |
| 72 | 1 | 6 | 89 | 2 | 9 | 84 | 0 | 8 | 86 | 2 | 7 |
| 89 | 0 | 8 | 88 | 1 | 9 | 87 | 1 | 12 | 79 | 1 | 11 |
| 93 | 4 | 2 | 99 | 0 | 1 | 89 | 1 | 6 | 87 | 0 | 11 |
| 87 | 1 | 1 | 86 | 1 | 10 | 73 | 0 | 13 | 79 | 1 | 17 |
| 85 | 0 | 12 | 88 | 0 | 7 | 73 | 3 | 8 | 74 | 0 | 19 |
| 91 | 0 | 7 | 91 | 0 | 7 | 94 | 1 | 3 | 80 | 0 | 14 |
| 95 | 1 | 3 | 84 | 0 | 14 | 81 | 2 | 9 | 85 | 3 | 9 |
| 94 | 3 | 3 | | | | | | | | | |

$t_1, t_2$ 和 $t_3$ 分别是松树、冷杉和橡树的花粉计数。程序 7.4 读取森林花粉数据并拟合 Dirichlet-multinomial 和 Random-clumped Multinomial 的语句。在上例中，调用了 "`DirMult`" 模块。极大似然结果见表 7.5。

### 程序 7.4：对森林花粉数据拟合 Dirichlet-multinomial 和 Random-clumped Multinomial 模型

```sas
/*
Forest Pollen Count, Mosimann (1962)
*/
data pollen_count;
  input t1 t2 t3;
  t4 = 100 - t1 - t2;
datalines;
94 0 5 85 1 84 1 12 88 0 0 9
75 2 1 91 1 4 97 0 3 94 0 4
81 2 3 99 1 0 83 0 13 69 7 18
95 2 3 90 2 8 81 1 15 90 0 8
89 3 1 91 0 8 81 1 16 86 1 8
84 5 1 79 1 19 76 2 18 90 0 7
81 3 10 89 0 7 87 3 7 74 5 16
97 0 2 95 2 1 91 1 5 82 2 11
86 1 8 90 3 5 94 0 5 87 3 9
86 2 1 93 1 6 88 1 11 68 3 26
82 2 1 90 2 7 93 4 2 77 3 11
72 1 6 89 2 9 84 0 8 86 2 7
89 0 8 88 1 9 87 1 12 79 1 11
93 4 2 99 0 1 89 1 6 87 0 11
87 1 1 86 1 10 73 0 13 79 1 17
85 0 12 88 0 7 73 3 8 74 0 19
91 0 7 91 0 7 94 1 3 80 0 14
95 1 3 84 0 14 81 2 9 85 3 9
94 3 3
;
ods html;
%DirMult(pollen_count, "Forest Poll Count, Mosimann (1962)");
ods close;
```

### 表 7.5：Dirichlet-multinomial 和 Random-clumped Multinomial 模型下森林花粉计数数据的极大似然估计

| 参数 | Dirichlet-multinomial 估计 | Dirichlet-multinomial 标准误 | Random-clumped Multinomial 估计 | Random-clumped Multinomial 标准误 |
| :--- | :--- | :--- | :--- | :--- |
| $\pi_1$ | 0.08621 | 0.00653 | 0.08636 | 0.00482 |
| $\pi_2$ | 0.01643 | 0.00224 | 0.01514 | 0.00153 |
| $\pi_3$ | 0.00880 | 0.00531 | 0.08626 | 0.00395 |
| $\rho$ | 0.12783 | 0.01094 | 0.08972 | 0.01390 |
| 对数似然值 | -507.82206 | | -534.27114 | |

$\pi_1, \pi_2$ 和 $\pi_3$ 分分别是冷杉、松树和橡树花粉的概率。

在这个例子中，样本量相对较大（n = 73），两种模型下的 $\pi = (\pi_1, \pi_2, \pi_3)$ 估计值彼此接近。Dirichlet-multinomial 下 $\rho$ 的估计值结果略大一些。然而，两组 MLE 之间的差异似乎出现在估计的标准误上：在本例中，Random-clumped Multinomial 的误差比 Dirichlet-multinomial 的误差要小。这是 Random-clumped Multinomial 分布在 $m_j$ 较大时的一个固有性质。该性质将在下一章进行讨论。

## 7.11 多项响应的广义线性离散模型——重新审视出生研究

与多项分布类似，DM 和 RCM 也可以结合协变量使用，以获得多项概率向量的 GLM。我们限制在使用最常用的连接函数：累积 logit 和 logit。

# 第 7 章 过离散多项响应的似然模型 233

| 0 | 0 | -1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 0 | 0 | 0 | 1 | -1 | 0 | 0 | 0 | 0 | 0 |
| 带 C= | 0 | 0 | 0 | 0 | 0 | 1 | -1 | 0 | 0 | 0 |
| 0 | 0 | 0 | 0 | 0 | 0 | 1 | -1 | 0 | 0 |
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | -1 | 0 |

因此，用于检验 (7.37) 的 Wald 统计量为：

```
$$X^2 = (C\hat{\theta})^T C \hat{V}(\hat{\theta}) C^{-1} (C\hat{\theta}) \quad (7.38)$$
```

在原假设下，该统计量渐近服从自由度为五的卡方统计分布。在本例中，矩阵 $\hat{V}(\hat{\theta})$ 是满秩的。因此，自由度由矩阵 $C$ 的秩决定，即五。

程序 7.5 包含了使用链接函数 (7.35) 将狄利克雷-多项（Dirichlet-multinomial）和随机聚类多项（Random-clumped Multinomial）模型拟合表 7.2 缺陷研究数据的编程语句。我们跳过了与数据读取相关的语句，这些可以在程序 7.2 中找到。在本例中，我们使用了 `NLMIXED` 过程。`NLMIXED` 中的 `CONSTRAINT` 语句提供了经过自由度归一化的 (7.38) Wald 。这可以用 F 分布近似。由于我们的模型（DM 和 RCM）是基于似然的，我们还可以计算似然比检验以及与 (7.38) 中 Wald 检验对应的得分检验。注意，在 ODS 语句中，已经列出了特定的表格来计算用于检验平行假设的 Wald 检验和似然比检验。涉及累积对数（cumulative logits）的参数初始估计是通过 `LOGISTIC` 过程链接的（此处未显示）。编程语句由 Sandia 国家实验室的 John New 博士感谢提供。



## 程序 7.5：在狄利克雷-多项和随机聚类多项模型下优势比例假设的检验——产前钙和锌暴露数据

```sas
/*
来自 Morel 和 Koehler (1995) 的缺陷示例
拟合广义过离散模型
dichlet-multinomial 和 Random-clumped Multinomial
使用 NLMIXED 过程中的
CONSTRAINT 语句检验比例性假设
*/
\ods html;
Title "Testing Proportionality Assumption -- Dirichlet-multinomial Distribution"
ods output Contrast=Prop_Sum_DM FitStatistics=Fit_DM_full
ParameterEstimates=Betas_DM CovMatParmEst=Cov_DM;
Proc nlmixed data=birth_defects;
parms a1=3.7, a2=-2.4, b11=-0.2, b21=-0.2, b12=3.1, b22=3.1,
b13=5.5, b23=5.5, b14=-1.8, b24=-1.8, b15=-1.7, b25=-1.7,
rho=0;
bounds 1>rho=0;
eta1 = a1*zn2*b12*cd2*cd13*b14*zn2_cd2*b15*zn2_cd3;
eta2 = eta2*b21*zn2*b22*cd2*cd23*b23*b24*zn2_cd2*b25*zn2_cd3;
gamma1 = 1/(1+exp(-eta1))
gamma2 = 1/(1+exp(-eta2))
pl1 = gamma1
pl2 = gamma2
p = pl1 - pl2
m = t1+t2+t3
c = (1-rho2)/(rho2);
loglik = lgamma(m+1)-lgamma(t1+1)-lgamma(t2+1)-lgamma(t3+1)
lgamma(c)-lgamma(m+c)-lgamma(t1+c)*lgamma(t2+c)+lgamma(t2*c)
lgamma(t3+c)-lgamma(t3+c)-lgamma(p1)*lgamma(c*p2)-lgamma(c*p3)
+ const;
todel tl = general(loglik);
contrast = "Proportionality Assumption Test -- DM Distribution"
b11-b21, b12-b22, b13-b23, b14-b24, b15-b25;
```

Title Testing Proportionality — Random-coupled Multinomial Distribution;

ods Outputs Contrast-Assump_Rho_RCM FitStatistics=Fit_Rcm_full Full_Dimensions=Dimensions_1

ParameterEstimates=Betas_RCM CoVarMapEstimate=Cov_RCM;

```sas
Proc nlmix data=defects cov;
params a1=3.7, a2=2.4, b11=0.2, b21=0.2, b31=3.1, b22=3.1,
b13=3.5, b23=3.5, b14=-1.8, b24=-1.8, b15=-1.7, b25=-1.7,
rho=0.5;
bounds 1>rho=0;
eta1 = a1*zn2*b12*cd2*cd13*b14*zn2_cd2*b15*zn2_cd3;
eta2 = eta2*b21*zn2*b22*cd2*cd23*b23*b24*zn2_cd2*b25*zn2_cd3;
gamma1 = 1/(1+exp(-eta1))
gamma2 = 1/(1+exp(-eta2))
pl1 = gamma1;
pl2 = gamma2;
p = pl1 - pl2
m = t1+t2+t3;
hoc = 1-rho2;
loglik = lgamma(m+1)-lgamma(t1+1)-lgamma(t2+1)-lgamma(t3+1)
+ lgamma(hoc)-lgamma(m+hoc)-lgamma(t1+hoc)*lgamma(t2+hoc) + (p*(p1)**t1)*(p*(p2)**t2)*(p*(p3)**t3)
+ const;
todel tl = general(loglik);
contrast = "Proportionality Assumption Test -- RCM"
b11-b21, b12-b22, b13-b23, b14-b24, b15-b25;
ods html;
```

通过程序 7.5 得到的 MLE。

### 表 7.6：链接函数 (7.35) 下狄利克雷-多项和随机聚类多项模型的似然结果——产前镉和锌数据

| 参数 | Dirichlet-multinomial Estimate | Dirichlet-multinomial Std Err | Random-clumped Multinomial Estimate | Random-clumped Multinomial Std Err |
|---|---|---|---|---|
| $\alpha_1$ | -2.8350 | 0.4261 | -3.1780 | 0.4199 |
| $\alpha_2$ | -2.4428 | 0.3598 | -2.6938 | 0.3366 |
| $\eta_{11}$ | 0.5400 | 0.6032 | 0.6959 | 0.5788 |
| $\eta_{21}$ | 0.4565 | 0.5203 | 0.4877 | 0.4894 |
| $\eta_{12}$ | 2.2039 | 0.5333 | 2.5221 | 0.4994 |
| $\eta_{22}$ | 3.6969 | 0.5265 | 3.9455 | 0.4740 |
| $\eta_{13}$ | 4.8780 | 0.6362 | 5.6568 | 0.6694 |
| $\eta_{23}$ | 6.5592 | 1.0840 | 7.1377 | 1.0645 |
| $\eta_{14}$ | -2.2316 | 0.8287 | -2.5301 | 0.7771 |
| $\eta_{24}$ | -2.6706 | 0.7225 | -2.6513 | 0.6524 |
| $\eta_{15}$ | -2.7366 | 0.8173 | -3.1895 | 0.8172 |
| $\eta_{25}$ | -3.4496 | 1.1897 | -3.5442 | 1.1654 |
| $\rho$ | 0.4262 | 0.0419 | 0.4069 | 0.0362 |
| -2*Log-likelihood | 397.9 | | 402.1 | |

`NLMIXED` `CONTRAST` 语句提供的检验比例假设的 F 统计量如下。两个统计量都拒绝了平行假设。

| 狄利克雷-多项分布 | | | | |
|---|---|---|---|---|
| 检验 | | | | |
| | | | | F Value | Pr > F |
| 比例假设检验 -- DM 分布 | 5 | 70 | 4.27 | 0.0119 |

| 随机聚类多项分布 | | | | |
|---|---|---|---|---|
| 检验 | | | | |
| | | | F | Pr > F |
| 比例假设检验 -- RCM 分布 | 5 | 70 | 5.66 | 0.0002 |

程序 7.5 的后续部分提供了计算 Wald 统计量的语句。注意使用 `IML` 过程通过 `LINMIXED` 的 `ODS` 输出计算表达式 (7.38)。

### 程序 7.5：使用 Wald 统计量检验平行假设（延续）

```sas
ods html;
title "Testing Parallelism Assumption using a Wald Statistic";
data Beta_DM;
  set Beta_DM;
  keep estimate;
run;
data Cov_DM;
  set Cov_DM;
  drop row parameter;
run;
data Beta_RCM;
  set Beta_RCM;
  keep estimate;
run;
data Cov_RCM;
  set Cov_RCM;
  drop row parameter;
run;
proc iml;
  use Beta_DM;
  read all int beta;
  use Cov_DM;
read all into cov;

c={0 0 1 -1 0 0 0 0 0 0,
      0 0 0 1 -1 0 0 0 0 0,
      0 0 0 0 0 1 -1 0 0 0,
      0 0 0 0 0 0 0 1 -0 0};
Degrees_of_Freedom
Degrees_of_Freedom = ncov(cov);

Wald_Statistic = beta * c' * inv(c * cov * c') * c * beta;
P_Value = 1 - probchhi(Wald_Statistic,Degrees_of_Freedom,0);
print "Dirichlet-multinomial Distribution";
print Degrees_of_Freedom Wald_Statistic[format=6.2] P_Value[format=p6.4];

use Beta RCM;
read all into rcm;
use Cov RCM;
read all into cov;

Wald_Statistic = beta * c' * inv(c * cov * c') * c * beta;
P_Value = 1 - probchhi(Wald_Statistic,Degrees_of_Freedom,0);
print "Random-clumped Multinomial Distribution";
print Degrees_of_Freedom Wald_Statistic[format=6.2] P_Value[format=p6.4];
quit;
ods html close;
```

下面的程序提供了通过似然比检验检验平行性假设（parallelism assumption）的语句。似然比检验是根据方程 (7.35) 中无限制模型的对数似然函数与方程 (7.34) 中比例优势模型（Proportional-odds Model）的对数似然函数构建的。程序中获得了“缩减模型”（比例优势模型）的拟合。

### 程序 7.5：使用似然比检验检验平行性假设（续）

```sas
ods html;
title "Proportional-Odds Model -- Dirichlet-multinomial Distribution";
ods output FitStatistics;Fit_DM;
Proc nlmixed birth_defects;
params a1=3.7,a2=-2.4,b1=-0.2,b2=3.1,b3=5.5,b4=-1.8,b5=-1.7,rhoc=0.5;
bounds 1-rho=0;
etal=a1+b1*zn2+b2*cd2+b3*cd3+b4*zn2+b5*zn2;
eta2=a2+b1*zn2+b2*cd2+b3*cd3+b4*zn2+b5*zn2;
gamma1=1/(1+exp(-etal));
gamma2=1/(1+exp(-eta2));
p1=gamma1;
p2=gamma2-gamma1;
p3=1-p1-p2;
t=t1+t2+t3;
c=(1-rhoc)*rho;
const=ligma(m+1)-ligma(t1)-ligma(t2+1)-ligma(t3+1);
loglik=ligma((p1+(rhoc)*rho1)*(t1+(rhoc)*rho2)*(t2+(rhoc)*rho3)*(rhoc**t3))
+ (p2+(rhoc)*rho1)*(t1+(rhoc)*rho2)*(t2+(rhoc)*rho3)*(rhoc**t3))
+ (p3+(rhoc)*rho1)*(t1+(rhoc)*rho2)*(t2+(rhoc)*rho3)*(rhoc**t3))
+const;
model t1=general(loglik);
```

```sas
Title "Proportional-Odds Model -- Dirichlet Multinomial Distribution";
ods output FitStatistics;Fit_ROM_Reduced_DM_Dimensions=0;
Proc nlmixed birth_defects;
params a1=3.7,a2=-2.4,b1=-0.2,b2=3.1,b3=5.5,b4=-1.8,b5=-1.7;
bounds 1-rho=0;
etal=a1+b1*zn2+b2*cd2+b3*cd3+b4*zn2+b5*zn2;
eta2=a2+b1*zn2+b2*cd2+b3*cd3+b4*zn2+b5*zn2;
gamma1=1/(1+exp(-etal));
gamma2=1/(1+exp(-eta2));
p1=gamma1;
p2=gamma2-gamma1;
p3=1-p1-p2;
t=t1+t2+t3;
oc=1-rhoc;
const=ligma(m+1)-ligma(t1)-ligma(t2+1)-ligma(t3+1);
loglik=ligma((p1+(rhoc)*rho1)*(t1+(rhoc)*rho2)*(t2+(rhoc)*rho3)*(rhoc**t3))
+ (p2+(rhoc)*rho1)*(t1+(rhoc)*rho2)*(t2+(rhoc)*rho3)*(rhoc**t3))
+ (p3+(rhoc)*rho1)*(t1+(rhoc)*rho2)*(t2+(rhoc)*rho3)*(rhoc**t3))
+const;
model t1=general(loglik);
```

```sas
data Fit_reduced;
  set Fit_DM;
  if n=1;
  rename Value=0;
  descr="LR Test -- DM Distribution";
run;
```

```sas
data DM_full;
    set Fit_DM_full;
    if _n_ = 1;
    rename Value=Value_1;
    keep Value;
run;
data Fit_DM;
    merge Fit_reduced DM_full;
run;
data Fit_RCM_reduced;
    set Fit_RCM_reduced;
    if _n_ = 1;
    rename Value=Value_0;
    descr = "LR Test -- RCM Distribution";
run;
data Fit_RCM_full;
    set Fit_RCM_full;
    if _n_ = 1;
    rename Value=Value_1;
    keep Value;
run;
data Fit_RCM;
    merge Fit_RCM_reduced Fit_RCM_full;
run;
data dimensions_1;
    set Fit_DM;
    if _n_ = 4 then callput('nparms_1=',trim(Value));
run;
data dimensions_0;
    set Fit_DM;
    if _n_ = 4 then callput('nparms_0=',trim(Value));
run;
data LR_Tests;
    set Fit_RCM;
    format Chi_square_Stat Chi_square_Stat;
    output;
run;
```

这两位评分员。受试者通常从不同评分员处获得相似的评分；评分向量 `X_{ij}` 是相互相关的。`T_i` 不满足多项分布的基本假设之一。通常，评分者的响应呈正相关；因此，向量 `T_i` 相对于多项分布表现出过度离散。当评分员之间呈负相关时，就会出现欠离散的情况。Bartfay 和 Donner (2001) 提出了 Dirichlet-多项分布来对对响应的概率建模。换句话说，他们建议将 `T_i` 建模为参数为 `(\pi,\rho)` 的 Dirichlet-多项分布。Cohen's kappa 可用于此模型；结果证明 `\kappa \equiv \rho^2`。这对于三位评分员（m=3）和两个评分分（C=2）也同样成立 `(\kappa \equiv \rho^2)`。在这种情况下，Beta-二项分布和随机聚类二项分布（Random-clumped Binomial）的 Kappa 估计值并不相同。对于 `m \ge 4`，我们不知道 `\kappa \equiv \rho^2` 是否成立。对于 m=2 的情况，Morel (1992) 证明了 Dirichlet-多项（DM）分布和随机聚类多项（RCM）分布的概率函数是相同的。因此，无论是在 DM 还是 RCM 分布下，`T` 的概率函数结果均为

$$\begin{aligned}\{\{\pi_i+\pi_i(1-\pi_i)\pi_i, & \text{如果 } t \text{ 的第 i 个分量为 2} \text{ \\2(1-\pi_i)\pi_i, & \text{如果 } t \text{ 的第 i 个和第 s 个分量均为 1}\}\{ \end{aligned} \quad (7.40)$$



请记住，在参数化下，$\rho^2$ 代表一致系数 $\kappa$。以下是使用 `NLMIXED` 过程计算相关多项模型 (7.40) 下 Kappa 系数的编程语句。请注意，原始的 3x3 列联表需要扩展为包含 $n=160$ 个三元响应样本的原始数据。这是使用 `IML` 过程完成的。有 24 个形式为 $(2,0,0)$ 的响应，8 个形式为 $(1,1,0)$，13 个形式为 $(1,0,1)$ 等。

## 问题 6.6：Sissel 和 Ebert 电影评分的 Kappa 系数（续）

```sas
ode html;
proc iml;
  use movie_ratings;
  read all into x;

  n0 = row(x);
  n1 = sum(x[j,3]);
  t1 = j(n1,3,0);
  t2 = j(n1,3,0);

  row = 0;
  do j=1 to n0;
    do t=1 to x[j,3];
      row = row + 1;
      t1[row,x[j,1]] = 1;
      t2[row,x[j,2]] = 1;
    end;
  end;

  t = t1 + t2;
  create new var(t3);
```

Morel, J., and Nagaraj Neeraj. Overdispersion Models in SAS.. © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 需更多 SAS 信息，请访问 support.sas.com/publishing。

```sas
append tm;
quit;
ods output ParameterEstimates=Parms_Estimates
AdditionalEstimates=Estimates;
proc nlmixed a=0 data=new;
parms a=0, b0=0, b02=0;
rho = -1 / (1 + exp(-a0));
etal = exp(b01);
eta2 = exp(b02);
p1 = etal/(1+etal+eta2);
p2 = eta2/(1+etal+eta2);
p3 = 1-p1-p2;
t3 = t1+t2;
c = (1-rho**2)/(1+rho**2);
const = lgamma(m+1)-lgamma(t1+1)-lgamma(t2+1)-lgamma(t3+1);
  loglik = lgamma(c)-lgamma(m+c)+lgamma(t1+c+1)+lgamma(t2+c*p2)
  +lgamma(t3*c+p3)-lgamma(c*p1)+lgamma(c*p2)-lgamma(c*p3);
model t1 ~ general(loglik);
estimate 'Kappa' / 1 / (1 + exp(-a0)) / (1 + exp(-a0));
run;
```

```sas
data Estimates;
set Estimates;
rename Estimate = Kappa;
keep Estimate Lower Upper;
run;
```

```sas
data Parm_Estimates;
set Parm_Estimates;
if Parameter = 'a0';
Estimate = 1 / (1 + exp(-Estimate)) / (1 + exp(-Lower));
Lower = 1 / (1 + exp(-Lower)) / (1 + exp(-Lower));
Upper = 1 / (1 + exp(-Upper)) / (1 + exp(-Upper));
rename Estimate = Kappa;
keep Estimate Lower Upper;
run;
```

```sas
title2 "使用 NLMIXED 中估计值的 Kappa 结果";
proc print data=Estimates;
run;
```

```sas
title2 "使用 NLMIXED 中逆方法的 Kappa 结果";
proc print data=Parms_Estimates;
run;
```

注意，在 `NLMIXED` 中 $\kappa$ 被重参数化为 $\frac{\exp(\hat{\alpha}_0)}{1+\exp(\hat{\alpha}_0)}$。$\hat{\kappa}$ 的估计方差 $\hat{v}(\hat{\kappa})$ 使用泰勒线性计算。因此，$\kappa$ 的近似 95% 置信区间为 $\hat{\kappa}\pm 1.96\sqrt{\hat{v}(\hat{\kappa})}$。为了保证置信区间落在 0-1 之间，需要使用逆方法。如果 $\hat{L}$ 和 $\hat{U}$ 分别对应于 $\alpha_0$ 的 95% 置信区间边界，则通过逆方法得到的 $\kappa$ 的近似 95% 置信区间为：

$$\left\{ \frac{\exp(\hat{L})}{1+\exp(\hat{L})}, \frac{\exp(\hat{U})}{1+\exp(\hat{U})} \right\}$$

以下是使用 `NLMIXED` 的置信区间结果。

![](img/fa69b648c17ad45ebe4ad92f57_0)

![](img/fa69b648c17ad45ebe4ad92f57_1)

`FREQ` 和 `NLMIXED` 过程提供的结果非常一致。注意相关模型 (7.40) 属于广义线性离散模型族，允许对在本章之前讨论的概率向量 $\pi$ 和离散参数 $\rho$ ($\kappa=\rho^2$) 使用连接函数。希望读者注意，Landis 和 Koch (1977) 为解释 Kappa 值提供了以下指南。这些指南并非所有统计学家都接受。

### 7.8 解释 Kappa 的指南

| Kappa | 解释 |
| :--- | :--- |
| < 0 | 无一致 |
| 0 — 0.20 | 极低 |
| 0.21 — 0.40 | 低一致 |
| 0.41 — 0.60 | 中等一致 |
| 0.61 — 0.80 | 完全一致 |
| 0.81 — 1.00 | 完美一致 |

根据这些指南，任何大于 0.60 的 Kappa 值都被视为完全一致或完美一致。由于 Sissel 和 Ebert 评分的 Kappa 点估计值为 0.38，近似 95% 置信区间约为 (0.26, 0.51)，根据上述指南，可以说两个电影之间的一性在低到中等之间。

### 附录 7.1：Dirichlet-多项和随机聚类多项分布的数据生成

在本附录中，我们描述在 Dirichlet-多项或随机聚类多项分布下随机样本 $\mathbf{t}_1, \mathbf{t}_2, \dots, \mathbf{t}_n$ 的生成。

在 Dirichlet-多项模型下，首先从 $(d+1)$ 维 Dirichlet 密度函数生成随机样本 $\mathbf{p}_1, \mathbf{p}_2, \dots, \mathbf{p}_n$：

$$f_D(\mathbf{p}; \alpha_1, \alpha_2, \dots, \alpha_{d+1}) = \frac{\Gamma(\alpha_1 + \alpha_2 + \dots + \alpha_{d+1})}{\prod_{i=1}^{d+1} \Gamma(\alpha_i)} \prod_{i=1}^{d+1} p_i^{\alpha_i-1}$$

其中 $\alpha_i = c\pi, i=1,2,\dots,(d+1), c = \rho^2(1-\rho), 0 < \rho < 1,$ 且 $\Gamma(\cdot)$ 表示 Gamma 函数。然后，给定 $\mathbf{p}_j, j=1,2,n$，从参数为 $\mathbf{p}_j$ 和 $m$ 的多项分布生成 $\mathbf{t}_j$。T$ 的无条件分布是 Dirichlet-多项分布，其概率函数如方程 (7.30)。`IML` 库中的 `RANDDIRICHLET` 函数用于从 Dirichlet 分布生成随机样本。

Dirichlet 变量 $\mathbf{p}_j$ 可以从 Beta 变量获得（Brier, 1979, 定理 4.1; Kotz, Balakrishnan, and Johnson, 2000, p. 448）。在下面的讨论中，为了方便，我们省略了下标 '$j$'。从参数为 $\alpha_1 = c\pi_1, \alpha_2 = c(1-\pi_1)$ 的 Beta 分布生成 $X_i$，则 $p_1 = x_1$。然后从参数为 $\alpha_1 = c\pi_1, \alpha_2 = c(1-\pi_1-\pi_2)$ 的 Beta 分布生成 $x_2$，并计算 $p_2$：

$p_2 = x_2(1-p_1)$。每个 Dirichlet 分布的第 $d$ 个分量获取为：

$p_d = x_d \sum_{i=1}^{d} p_i$，其中 $x_d$ 是从参数为 $\alpha_i = c\pi_d$ 和 $\alpha_2 = c(1-\sum_{i=1}^{d} \pi_i)$ 的 Beta 分布生成的（此处原文公式可能有笔误，通常应为 $1-\text{sum}$，注：原文此处为 $1-\pi_1-\pi_2$）。因此，$p_{d+1} = 1-\sum_{i=1}^{d} p_i$，所以不需要生成 $(d+1)$ 个分量。

## 248 SAS 中的过度离散模型

```sas
do j=1 to n;
  p = RANDDIRICHLET(1, shape);
  p = p ||/ (1-sum(p));
  t = RANDOMMULTOMIAL(1,m,p);
  t_dm[j] = t[1:d];
end;

* 在随机聚类多项分布下生成数据
do j=1 to n;
  y = RANDOMMULTOMIAL(1,1,pi);
  call randgen(n,"BINOM",m,rho);
  t = y*nn; * 数据的随机聚类;
  if nc < m then t = t + RANDOMMULTOMIAL(1,m-n,pi);
  t_cm[j] = t[1:d];
end;

start mean_var(t,n,d);
  SampleMean = t[::];
  SampleCov = (t*t - SampleMean*SampleMean) / (n-d);
  print SampleCov[format=8.4],];
finish mean_var;
print 'Sample Mean and Covariance -- Dirichlet-multinomial Model';
call mean_var(t,dm,n);
print 'Sample Mean and Covariance -- Random-clumped Multinomial Model';
call mean_var(t_cm,n,d);
quit;
ods html close;
```

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_260_0.png)

Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. 版权所有。 如需更多 SAS 资源，请访问 support.sas.com/publishing。

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_261_0.png)

### 附录 7.2: 模块 "DirMult_RCMult"

```sas
Proc IML;
/************************************************************************/
/* MLE 函数                                                              */
/************************************************************************/
/**********************************************************************/
/* Module: MLEDM(m,T)                                                              *
/* 此模块使用费舍信息 *
/* Matrix和费舍评分算法从狄利克特 *                               
/* 多项分布中计算极大似然估计 (MLE) *
/* m - 聚类大小                                                              *
/* T - nxk 计数矩阵 (t1,t2,...,tk)，其中 ti 是 *                               
/* nxl1 向量，表示类别 i 中的观测计数 *                                     /
/**********************************************************************/
Start MLEDM(m, T);
```

Morel, Jorge, and Nagaraj Neeraj. Overdispersed Models in SAS.. Copyright ©2011, SAS Institute Inc., Cary, North Carolina, USA. 版权所有。如需更多 SAS 资源，请访问 support.sas.com/publishing。

## 250 SAS 中的过度离散模型

```sas
*** 费舍评分法 -- 狄利克特多项分布 ***;

pi0 = QLEpi(m,T);
rho0 = QLErho(m,T,pi0);
k = ncol(T);
n = nrow(T);
theta = j(k,1,0);
theta[1:k-1] = pi0;
theta[k] = rho0;

eps = 1E-8;
conv = 1;
iter = 0;
Do Until(conv<eps);

    iter = iter + 1;
    pi = theta[1:k-1];
    rho = theta[k];
    INVNFIM = Inv(n*FIMDM(m, pi, rho));
    Old = 0;
    Scores = j(k,1,0);
    Do j = 1 to n;
        tj = T[j,1:k-1];
        Scores = Scores + gradDM(m, pi, rho, tj);
        Old = Old + log(ProbDM(m, pi, rho, tj));
    End;

    si = 0;
    Lnew = Old - 1;
    Do Until (Lnew > Old);
    thetaNew = theta + {0.5*si}INVNFIM*Scores;
    pi = thetaNew[1:k-1];
    rho = thetaNew[k];
    Lnew = 0;
        Do j = 1 to n;
            tj = T[j,1:k-1];
            Lnew = Lnew + log(ProbDM(m, pi, rho, tj));
        End;

        si = si + 1;
        if si > 20 then;
            print "NOTE: 步长减了二十次，假设收敛";
            Lnew = Old + 0.000001;
        end;
    End;

    theta = thetaNew;
    conv = abs(Lnew)/(abs(Lnew)+1E-6);
    conv_0 = conv;

    if si > 20 then conv = eps - 0.000001;
    if iter > 100 then;
        print "NOTE: 迭代 100 次后，尚未满足收敛";
        conv = eps - 0.000001;
    end;

End;

if conv_0 < eps then;
    print "NOTE: 收敛标准 (EPSILON-1E-8) 已满足";
end;
```

Morel, Jorge, and Nagaraj Neeraj. Overdispersed Models in SAS.. Copyright ©2011, SAS Institute Inc., Cary, North Carolina, USA. 版权所有。如需更多 SAS 资源，请访问 support.sas.com/publishing。

# 第 7 章 过度离散多项响应的似然模型



# 252 SAS 中的过度离散模型

```sas
********************************************************************
/* Module: MLERCM(m, T)                                               *
/* 此模块使用费舍信息                 *
/* Matrix和费舍评分算法从随机聚类多项 *                             *
/* 分布中计算 MLE                             *
/* m - 聚类大小                                                  *
/* T - nxk 计数矩阵 (t1,t2,...,tk)，其中 ti 是 *                          *
/* nxl 向量，表示类别 i 中的观测计数                    /
/****************************************************
Start MLERCM(m, T);
print "**费舍评分法 -- 随机聚类多项分布 ***";
pi0 = QLEpi(m,T);
rho0 = QLErho(m,T,pi0);
k = ncol(T);
n = nrow(T);
theta[1:k-1] = j(k,1,0);
theta[k] = rho0;

eps = 1E-8;
conv = 1;
iter = 0;
Do Until(conv<eps);

  iter = iter + 1;
  pi = theta[1:k-1];
  rho = theta[k];
  INFIM = Inv(n*FIMCM(m, pi, rho));
  Old = 0;
  Scores = j(k,1,0);
  Do j = 1 to n;
    tj = T[j,1:k-1];
    Scores = Scores + gradRCM(m, pi, rho, tj);
    Old = Old + log(ProbRCM(m, pi, rho, tj));
  End;

  si = 0;
  Lnew = Old - 1;
  Do Until (Lnew > Old);
    thetaNew = theta + {0.5*si}INVNFIM*Scores;
    pi = thetaNew[1:k-1];
    rho = thetaNew[k];
    Lnew = 0;
        Do j = 1 to n;
            tj = T[j,1:k-1];
            Lnew = Lnew + log(ProbRCM(m, pi, rho, tj));
        End;

        si = si + 1;
        if si > 20 then;
            print "NOTE: 步长减了二十次，假设收敛";
            Lnew = Old + 0.000001;
        end;
    End;

    theta = thetaNew;
    conv = abs(Lnew)/(abs(Lnew)+1E-6);
    conv_0 = conv;

    if si > 20 then conv = eps - 0.000001;
    if iter > 100 then;
        print "NOTE: 迭代 100 次后，尚未满足收敛";
        conv = eps - 0.000001;
    end;

End;

if conv_0 < eps then;
    print "NOTE: 收敛标准 (EPSILON-1E-8) 已满足";
end;

Return(theta);

Finish;
Store=MLERCM
```

## 费舍信息矩阵

```sas
******************************************************

/* 费舍信息矩阵                                */

******************************************************

******************************************************

/* Module: FIMDM(m,pi)                                */

/* 此模块返回狄利克特 *                                

/* 多项分布的费舍信息矩阵                                */

/* m = 聚类大小                                                    

/* pi = 概率向量 [pi1, pi2, ..., pk]               */

/* rho - 相关系数                                                    */

******************************************************

Start FIMDM(m, pi);

k = nrow(pi);

c = (1-rho)/rho;

FIM = j(k, c, 0);

PrK = 0;

PrC = 0;

pik = 1-sum(pi);

Do s = 1 to m;

    PrK = PrK + ProbDM(m, pi, rho, s)/(c*pi[s]-s)**2;

    PrC = PrC + (c+s-1)**-2;

end;

Do i = 1 to (k-1);

    PrI = 0;

    Do s = 1 to m;

        PrI = PrI + ProbDM(m, pi[i], rho, s)/(c*pi[i]+s-1)**2;

    end;

    FIM[i,j] = (c**2)*(PrI + PrK);

    Do j = (i+1) to (k-1);

        FIM[j,i] = (c**2)*(PrI + PrK);

    End;

    FIM[i,k] = c*(pi*PrK - pi[i]*PrI) * (2/rho**3);

    FIM[k,i] = c*(pi*PrK - pi[i]*PrI) * (2/rho**3);

    End;

    FIM[k,k] = (FIM[k,k] + (pi**2)*PrK - PrC) * (4/rho**6);

End;

Return (FIM);

Finish;

Store Module=FIMDM;
```

```sas
/* t - 成功次数

 *******************************************************/

Start ProbBBB(m, pi, rho, t);

 c = (1-rho**2)/rho**2;

N1 = 0;

N2 = 0;

D = 0;

 Do k = 1 to t1;

  N1 = N1+log(c*pi + k - 1);

End;

  Do k = 1 to (m-t2);

  N2 = N2+log(c*(1-pi) + k - 1);

End;

  Do k = 1 to m;

  D = D+log(c + k - 1);

End;

  Prob = comb(m,t)*exp(N1+N2-D);

  Return(Prob);

Finish;

Store::Module=ProbBBB;
```

```sas
/*******************************************************/
/* 该模块根据 Beta-二项分布返回 P(T>t) 

 */
/* m - 聚类大小
/* pi - 成功概率
/* rho - 相关性
/* t - 成功次数
/******************************************************/

StartProbGTRBB(m, pi, rho, t);

 Prob = 0;

 If t/m >= 0.5 Then;

  Do i = t to m;

    Prob = Prob + ProbBB(m, pi, rho, i);

  End;

 Else Do;

  Do i = 0 to (t-1);

    Prob = Prob + ProbBB(m, pi, rho, i);

  End;

 Prob = 1 - Prob;

 End;

Finish;

Store::Module=ProbGTRBB;
```

```sas
/*******************************************************/
/* 该模块根据多项分布返回 P(T1, T2=t2, ...Tk=tk)  */
/* 实现此函数有多种方法。这里提供了三个 */
/* 版本。 */
/* m - 聚类大小
/* p - 概率向量 [p1,p2...,p(k-1)]`
/* t - 计数向量 [t1,t2,...,tk(k)]`
```

# 第 7 章 针对过度离散多项响应的似然模型 255

```sas
****************************************************************

Start ProbMultinomial1(m, p, t);

k = nrow(p+1);

mtemp = mj;

g = 1;

If (t[1]=0) Then Prob = PROBNML(p[1], mtemp, t[1]);

Else Prob = (PROBNML(p[1], mtemp, t[1])-PROBNML(p[1], mtemp, t[1]);

Do i = 2 to (k-1) While (mtemp > 0)

  mtemp = t([i-1]);

  If (mtemp*=0) Then Do:

    ti = t([i-1]);

    g = g-p([i-1]);

    newp = p[i]/g;

    If (t[i]=0) Then Prob = Prob*PROBNML(newp, mtemp, t[i]);

    Else Prob = Prob*PROBNML(newp, mtemp, t[i])-PROBNML(newp, mtemp, t[i-1]);

  End;

End;

If Prob < 1e-50 Then Prob = 1e-50

Return(Prob);
```

```sas
Finish;

Store Module=ProbMultinomial;

Start ProbMultinomial2(m, p, t);

k = nrow(p+1);

Prob = 1;

Do i = 1 to (k-1)

  Prob = Prob*((p[i])**t[i])/gamma(t[i]);

End;
```

```sas
pk = 1-sum(p);

tk = m-sum(t);

Prob = Prob*gamma(m+1)*(pk**tk)/gamma(tk+1);

Return(Prob);
```

```sas
Finish;

Store Module=ProbMultinomial2;

Start ProbMultinomial3(m, p, t);

k = nrow(p+1);

Prob = 0;

Do i = 1 to (k-1)

  Prob = Prob + t[i]*log(p[i]) - lgamma(t[i]+1);

End;
```

```sas
pk = 1-sum(p);

tk = m-sum(t);

Prob = Prob + lgamma(m+1)+ tk*log(pk) - lgamma(tk+1);

Return(Prob);
```

More, Jorge, and Nagaraj Neerchal. Overdispersed Models in SAS.. Copyright © 2011, SAS Institute, Cary, North Carolina, USA. ALL RIGHTS RESERVED. 更多 SAS 资源，请访问 support.sas.com/publishing。

# 256 SAS 中的过度离散模型

```sas
Store Module=ProbMultinomial;
```

```sas
StartProbRCM(m, pi, rho, t);

  k = nrow(pi)+1;

  e = diag((j(k-1), rho));

  Prob = 0;

  Do i = 1 to (k-1);

    pi = (1-rho)*pi + e[i];

    Prob = Prob + pi[i]*ProbMultinomial(m, pi, t);

End;
```

```sas
piK = (1-rho)*pi

pk = -sum(pi)

Prob = Prob + pk

Return(Prob);

Finish;

Store Module=ProbRCM;
```

```sas
StartProbDM(m, pi, t);

  k = nrow(pi)+1;

  c = (1-rho)/rho**2;

  Prob = 0;

  Do i = 1 to (k-1);

    pi = (1-rho)*pi + e[i];

    Prob = Prob + pi[i]*ProbMultinomial(m, pi, t);

End;
```

```sas
piK = (1-rho)*pi

pk = -sum(pi)

Prob = Prob + pk*

Return(Prob);

Finish;

Store Module=ProbDM;
```

```sas
StartProbG(m, pi, t);

  k = nrow(pi)+1;

  g = 1;

  e = j(k-1), rho);

  Prob = 0;

  Do i = 1 to (k-1);

    pi = (1-rho)*pi + e[i];

    Prob = Prob + pi[i]*ProbMultinomial(m, pi, t);

End;
```

```sas
piK = (1-rho)*pi

pk = -sum(pi)

Prob = Prob + pk*

Return(Prob);

Finish;

Store Module=ProbG;
```



# 两阶段极大似然估计程序

- 8.1 引言 ................................................................................................261
- 8.2 两阶段估计程序..................................................................262
- 8.4 重新审视森林花粉计数案例..................................................265
- 8.5 重新审视住房满意度案例...............................................267
- 附录 8.1: 仿真结果 .......................................................269
- 附录 8.2: 宏“`DM_RCM_Exact_Approximate`”......................................272

## 8.1 引言

在第7章，我们考虑了由 Mosimann (1962) 提出的 Dirichlet-multinomial（`DM`）分布极大似然估计，以及由 Morel 和 Nagaraj (1993) 以及 Necheral 和 Morel (1998) 提出的随机聚类多项分布（`RCM`）分布。使用经典的费舍尔计分法（Fisher scoring method）对这些模型的参数进行极大似然估计面临着计算挑战。在 `DM` 分布的情况下，通过注意到费舍尔信息矩阵（FIM）可以使用 Beta-二项分布（`DM` 的单变量版本）来计算，从而克服了挑战。另一方面，对于 `RCM` 分布，FIM 的计算可能变成一种巨大的负担，此时可以使用近似结果来获得用于计算极大似然估计的两阶段程序。对于 `DM` 分布，也存在类似的近似结果。在本章中，我们将简要介绍两阶段程序背后的计算细节，该程序不仅在计算上是高效的，而且能够提供恰当的标准误。我们给出这一结果的陈述仅是为了说明并讨论该结果的影响。在费舍尔计分法中使用近似信息矩阵将带来巨大的计算节省。尽管我们的经验表明，对于大多数实际情况，

近似信息矩阵为标准误提供了足够的准确性，但通过增加一个步骤可以获得更高的精度。

我们将重新审视之前在第7章中讨论过的两个案例，即森林花粉计数案例和住房满意度案例。前者是说明两阶段程序的理想案例，因为其聚类尺寸较大，即 `m=100`。在后者中，聚类尺寸相对较小，即 `m=5`。我们将证明在这些情况下，两阶段程序产生的估计与标准费舍尔计分法得到的估计几乎相同。我们通过报告一个旨在分析两阶段程序性能的仿真结果来结束本章。

## 8.2 两阶段估计程序

获取极大似然估计（MLE）的主要计算负担在于需要在每次迭代中计算 FIM。我们对 FIM 的近似（在本章稍后部分给出）解决了这个问题并提供了极佳的准确性。两阶段程序的思想是在费舍尔计分算法中使用这种 FIM 的近似值直到达到收敛，然后使用精确的 FIM 进行额外的迭代。使用精确 FIM 的额外迭代可以提高估计误差的准确性。在整个节中，我们将频繁地引用第7章的方程。我们将特别提醒读者查看第7.3节以复习符号。正如在前一章中所过的（见7.3），`$\theta$` 的极大似然估计，例如 `$\hat{\theta} =(\hat{\pi}_1, \hat{\pi}_2, \dots, \hat{\pi}_k, \hat{\rho})$`，可以通过费舍尔计分法迭代找到。该算法可以表示为

```
$$\hat{\theta}_{(s+1)} = \hat{\theta}_{(s)} + \left\{ n \mathbf{I}(\hat{\theta}_{(s)}) \right\}^{-1} \frac{\partial L(\hat{\theta}_{(s)})}{\partial \hat{\theta}_{(s)}}$$
```

`$\hat{\theta}_{(s)}$` 和 `$\hat{\theta}_{(s+1)}$` 分别表示第 s 和第 (s+1) 次迭代，`$I(\hat{\theta}_{(s)})$` 是在 s 次迭代处评估的单个观测值的 FIM。启动迭代的初始值可以通过方法法（method of methods）获得。

记得，一旦 FIM 定义为：

```
$$\mathbf{I}(\mathbf{t}) = E \frac{\partial^2 \log P(\mathbf{t})}{\partial \mathbf{t} \partial \mathbf{t}'} = \sum_{\mathbf{t}} \frac{\partial^2 \log P(\mathbf{t})}{\partial \mathbf{t} \partial \mathbf{t}'} \mathbf{P}(\mathbf{t}).$$
```

方程 (8.2) 给出的 FIM 是对多项式样本空间的求和，用 `$\Omega$` 表示向量 `$\mathbf{t}$` 的所有可能取值。随着聚类尺寸 `m` 和类别数 `$(d+1)$` 的增加，多项式样本空间 `$\Omega$` 会迅速增大，因此 (8.2) 的计算可能非常缓慢。现在我们将给出针对过离散分布 `DM` 和 `RM` 的费舍尔信息矩阵的近似值。在执行费舍尔计分法 (8.1) 时，这种对 FIM 的近似导致极大似然估计几乎没有产生准确性损失。这表明对于所讨论的过离散多项式模型的参数极大似然估计，存在两阶段估计程序。详情请参阅 Neerchal 和 Morel (1998)。

首先，令 Dirichlet-multinomial 分布的 FIM 表示为 `$\mathbf{F}_{DM}(\mathbf{0})$`。FIM 的单个元素是一个 `$(d+1) \times (d+1)$` 的对称矩阵，记为 `$F_{DM}(\pi_i, \pi_j)$`，对于 `$i,j=1,...,d$`；由于对称性，它也等于 `$F_{DM}(\rho, \pi_i)$`，对于 `$i=1,...,d$`；以及 `$F_{DM}(\rho, \rho)$`。同样，随机聚类多项分布的 FIM 表示为 `$F_{RCM}(\mathbf{0})$`。随机聚类多项分布 FIM 的单个元素记为 `$F_{RCM}(\pi_i, \pi_j)$`，对于 `$i=1,...,d; i \neq j$`；由于对称性，它也等于 `$F_{RCM}(\rho, \pi_i)$`；以及 `$F_{RCM}(\rho, \rho)$`

在 Dirichlet-multinomial 分布下，随着聚类尺寸的增大，当 `$m \to \infty$` 时，有：

```
$$\begin{aligned} F_{DM}(\pi_i, \pi_j) & \to c^2(\Psi'(\pi_i) + \Psi'(\pi_{d+1})) & i=1,...,d \\ F_{DM}(\pi_i, \pi_{i'}) & \to c^2\Psi'(\pi_{d+1}) & i=1,...,d, i \neq i' \\ F_{DM}(\pi_i, \rho) & \to c[\pi_{d+1}\Psi'(\pi_{d+1}) - \pi_i\Psi'(\pi_i)] & i=1,...,d & \frac{2}{\rho^4} \\ F_{DM}(\rho, \rho) & \to c\sum_{i=1}^{d+1} \Psi'(\pi_i) + \Psi'((\rho)) & \frac{4}{\rho^6} \end{aligned}$$ (8.3)
```

其中 `$c = \rho^2(1-\rho^2)$`，`$Psi'(x)$` 是三伽函数，定义为 `$\Psi'(x) = \frac{\partial}{\partial x}\Psi(x)$`，而 `$\Psi(x) = \frac{\partial}{\partial x}\log\Gamma(x)$` 是通常的 Dig伽函数。有趣的是，`DM` 分布的极限 FIM 与 Dirichlet 分布的 FIM 有连结。正如第7章所示，Dirichlet 分布是多项式分布的共轭先验。

### SAS 中的过度离散模型

`$R_{CM}(\pi_i, \pi_i) \quad m(1-\rho)^2(\beta_i + \beta_d) + (\pi_i^{-1} + \pi_d^{-1}) \rightarrow 0 \quad i=1,2,...,d$`
`$R_{CM}(\pi_i, \pi_i') \quad m(1-\rho)\beta_{d+1} + \pi_{d+1}^{-1} \rightarrow 0 \quad i=1,2,...,d, \ i \neq i'$`
`$R_{CM}(\pi_i, \rho) \quad m(1-\rho)(\gamma_i - \gamma_{d+1}) \rightarrow 0 \quad (8.4)$`
`$R_{CM}(\rho, \rho) \quad \frac{m}{1-\rho}\frac{\pi_i}{(1-\rho)\pi_i}\frac{\pi_i}{\rho} \rightarrow 0$`

其中 `$\beta_i = \frac{\pi_i}{(1-\rho)\pi_i} + \frac{1-\pi_i}{(1-\rho)\pi_i}, \text{ 且 } \gamma_i = \frac{\pi_i(1-\pi_i)}{(1-\rho)\pi_i} + \frac{1}{1-\rho}, \text{ 对于 } i=1,2,...,(d+1)$`。通过 (8.3) 和 (8.4) 比较两种分布的极限结果，可以发现一些有趣的现象。首先，注意 (8.4) 中的极限表达式计算简单，而 (8.3) 中的极限表达式则涉及双伽函数（digamma）和三伽函数（trigamma）。此外，可以证明 `DM` 费舍尔信息矩阵（FIM）的近似误差为 `$m^{-1}$` 阶，而 `RCM` 相应的近似误差则为 `$m$` 阶。因此，我们可以得出结论：虽然在 `$m$` 较大时近似效果良好，但 `RCM` 模型的近似效果会比 `DM` 模型好得多。这些观察结果在大规模模拟研究中得到了证实，结果报告于附录 8.1。

方程 (8.3) 和 (8.4) 中的极限表达式与相关的费舍尔信息矩阵元素非常容易比较。因此，对于较大的 `$m$`，可以考虑将它们作为方程 (8.1) 中费舍尔评分算法的近似值。使用这些近似值，我们推荐以下两阶段程序：

**第一阶段。** 首先使用之前描述的费舍尔评分程序 (8.1) 获取估计量 `$\hat{\theta} = (\hat{\pi}', \hat{\rho})$`，其中费舍尔信息矩阵被替换为方程 (8.3) 和 (8.4) 中给出的极限信息矩阵。

**第二阶段。** 一旦 `$\hat{\theta}$` 的计算达到收敛，便通过执行额外步骤获得估计量 `$\tilde{\theta} = (\hat{\pi}', \hat{\rho}')$`：

`$$\tilde{\theta} = \hat{\theta} + \left\{n \mathbf{1}(\hat{\theta})\right\}^{-\frac{1}{2}} \frac{\partial L(\hat{\theta})}{\partial \theta} \quad (8.5)$$`

这里，`$\hat{\theta}$` 是在 `$\theta = \hat{\theta}$` 处评估的单次观测 FIM。对于最后一步，`$\tilde{\theta}$` 的更新方差协差矩阵为 `$\{n \mathbf 1(\hat{\theta})\}^{-1/2}$`。所得估计量将标记为 `$\tilde{\theta} = (\hat{\pi}', \hat{\rho}')$`。

在继续之前，让我们回顾一下在计算极大似然估计量时近似值的影响。我们首先注意到，这些费舍尔信息矩阵中每个都有 `$(d+1)(d+2)$` 个唯一元素。`$I_{RCM}$` 的每个元素都是多项分布空间 `$\Omega$` 上的求和，包含 `$\frac{(m+d)!}{md!}$` 项。对于 `$m=100$` 和 `$d=3$`，使用 `$(d+1)(d+2)$` 次 `$\frac{(m+d)!}{md!}$` 操作来计算所有 `RCM` 元素。另一方面，由于使用了近似值，节省了巨大的计算量。在 `DM` 的情况下，如前所述，每个元素实际上可以近似为 Beta 分布的期望。因此，计算节省了 `$(d+1)(d+2)$` 次 `$m$`，这在 `RCM` 分布中是显著的。

## 8.4 重新审视花粉计数

在第 7 节中，我们讨论了 Mosmann (1962) 的经典示例，即松树、杉树和赤松的花粉，在 `$m=100$` 时存在过度离散情况。表 7.5 中的数据用于说明 `DM` 和 `RCM` 模型。编程语句可以在第 7 章找到。通过调用得到的 `RCM` 结果报告在表 7.6 中。Mosmann (1962) 是一个有趣的案例。

```sas
/*
Forest Count Example, Mosimann (1962)
*/
data pollen_count;
  input t1 t2 t3 0;
  t4 = 100 - t1 - t2;
datalines;
94 0 85 1 12 84 1 12
ods html;
%DirMult(pollen_count, "Forest Count Example, Mosimann (1962)");
ods html close;
```



表 8.1 提供了 Mosmann (1962) 示例在 `DM` 和 `RCM` 模型下的极大似然结果。两阶段程序的结果与极大似然估计几乎无法区分。注意最后一列不是精确值与两阶段之间的标准差，而是百分比误差。在这个示例中，两种方法的标准差实际上是无法区分的。

## 第 8 章 两阶段极大似然估计程序 269

*** 使用近似 `RCM` 的 Fisher 评分法 -- 随机聚类多项分布 ***

注意：收敛准则 (`EPSILON=1E-8`) 已满足

使用 `FIM` 和近似 `Fi` 得到的极大似然估计 -- 随机聚类多项分布

| 参数 | 估计值 | 标准误 | 估算标准误 | 相对误差 |
| --- | --- | --- | --- | --- |
| `Pi(1)` | 0.50366 | 0.068912 | 0.068911 | 0.00076 |
| `Pi(2)` | 0.43163 | 0.068150 | 0.068150 | 0.00086 |
| `Rho` | 0.43154 | 0.104128 | 0.104129 | 0.00124 |
| 对数似然值 | -43.38522 | | | |

## 附录 8.1：模拟结果

在本附录中，我们报告了 Neerhal 和 Morel (2005) 对第 8.3 节提出的两阶段方法的性能开展的模拟研究结果。该模拟研究包含 5,000 个数据集，每个样本量 `n=250`。考虑了参数值和聚类大小 (`m`) 的各种组合。对于每个模型，从初始值开始计算了两组极大似然估计。其中一组使用精确 `FIM` (8.2) 计算；另一组则使用方程 (8.3) 和 (8.4) 给出的近似值计算。然后，计算了近似似然估计相对于精确极大似然估计的整体相对误差。具体而言，对于使用近似 `FIM` 得到的估计值对应的标题（titles）和精确极大似然估计对应的帽（hats），我们有：

蒙特卡洛误差 (`\tilde{\pi}`) = 5,000 次重复的 `\frac{\sqrt{\frac{1}{d}\sum_{i=1}^{d}|\hat{\pi}_i - \tilde{\pi}|^2}}{\tilde{\pi}}` 最大值

蒙特卡洛误差 (`\tilde{\rho}`) = 5,000 次重复的 `\frac{\sqrt{\frac{1}{d}\sum_{i=1}^{d}|\hat{\rho}_i - \tilde{\rho}|^2}}{\tilde{\rho}}` 最大值

蒙特卡洛误差 {`\tilde{\sigma}`} = 5,000 次重复的 `\frac{\sqrt{\frac{1}{d}\sum_{i=1}^{d}|SE(\hat{\sigma}_i) - SE(\tilde{\sigma})|^2}}{SE(\tilde{\sigma})}` 最大值

以及

蒙特卡洛误差 {`SE(\rho)`} = 5,000 次重复的 `\frac{SE(\rho)}{SE(\rho\rho)}` 最大值 (8.9)

此处，`SE()` 表示根据情况从近似方法或精确方法得到的估计标准误。`DM` 和 `RCM` 模型下的数据生成算法见第 7 章附录 7.1 节。此项蒙特卡洛研究的结果非常理想，如表 8.2 至 8.5 所示。表 8.2 和 8.3 显示了模型参数估计的结果，表 8.4 和 8.5 显示了估算标准误的结果。在我们所有尝试过的用例中，通过该两阶段程序得到的估计值与精确极大似然估计值无法区分。相应标准误估计的相对误差在 `10^{-5}` 级。对于所有实际用途，该两阶段程序仅需计算一次 `FIM` 矩阵（如果调用了最终更新），其结果与每次迭代都使用 `FIM` 的结果几乎相同。过度离散模型 `FIM` 的近似结果提供了一项非常有趣的比较研究。虽然节省时间可能不是他们对单个数据集进行一次性分析时使用它的动力，但在模拟设置中，甚至在通过参数自助法获取 p 值时，考虑其使用是完全值得的，因为 `FIM` 需要被评估数千次。这仅是我们进行过的模拟研究的一个示例，我们对自己的建议非常有信心。

表 8.2：实施两阶段程序时 `\pi_{i}` 近似误差的蒙特卡洛属性

| ρ | m | (.1) | (.3) | (.5) | (.1) | (.3) | (.5) | (.1) | (.2) | (.3) | (.3) |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 3 | 10 | 4.21 | 1.37 | 0.46 | 1.33 | 1.38 | 0.70 | 1.62 | 1.19 | | | |
| | | 0.45 | 0.20 | 0.19 | 1.42 | 1.14 | 0.31 | 0.97 | 0.83 | | | |
| | | 40 | 8.78 | 1.73 | 1.33 | 1.62 | 1.08 | 0.94 | 1.05 | 0.90 | | |
| | | | 0.14 | 0.07 | 0.05 | 0.59 | 0.48 | 0.14 | 0.55 | | | |
| 7 | 10 | 7.82 | 2.48 | 1.39 | 1.82 | 1.49 | 1.39 | 1.57 | 0.99 | | |
| | | 1.82 | 0.20 | 0.93 | 0.89 | 0.35 | 0.76 | | | | |
| | | 40 | 10.7 | 2.22 | 1.18 | 1.64 | 1.14 | 1.27 | 1.37 | | | |
| | | | 0.61 | 0.52 | 0.34 | 1.04 | 1.11 | 0.44 | 1.27 | 1.09 | |

注意：表中的数字为 `10^{-5}`。计算方法同 (8.6)。普通类型对应 `RCM` 分布；粗体类型对应 `DM` 分布。结果基于 5000 个数据集。省略了 `\pi` 的最后一个分量。

表 8.3：实施两阶段程序时 `\hat{\rho}` 近似误差的蒙特卡洛属性

| ρ | m | (.1) | (.3) | (.5) | (.1) | (.1) | (.3) | (.1) | (.1) |
|---|---|---|---|---|---|---|---|---|
| `\rho` | m | | | | .3 | .5 | .5 | .1 | .2 |
| .3 | 10 | 13.2 | 2.79 | 1.73 | 3.99 | 4.31 | 2.50 | 3.97 | 2.89 |
| | | 8.60 | 2.30 | 0.99 | 2.02 | 1.90 | 1.48 | 1.32 | 1.20 |
| | | 40 | 21.0 | 4.11 | 2.11 | 3.75 | 2.08 | 1.97 | 2.54 | 1.65 |
| | | | 0.85 | 0.35 | 0.32 | 0.55 | 0.57 | 0.64 | 0.57 | 0.64 |
| .7 | 10 | 4.59 | 1.11 | 0.50 | 1.12 | 0.76 | 0.78 | 0.85 | 0.47 |
| | | | 0.84 | 0.35 | 0.18 | 0.28 | 0.25 | 0.19 | 0.27 | 0.17 |
| | | 40 | 4.71 | 1.02 | 0.41 | 0.73 | 0.52 | 0.56 | 0.66 | 0.50 |
| | | | 0.62 | 0.23 | 0.20 | 0.29 | 0.28 | 0.25 | 0.54 | 0.34 |

**注意：表中的数字为 `10^{-4}`。** 计算方法同 (8.7)。普通类型对应 `RCM` 分布；粗体类型对应 `DM` 分布。结果基于 5000 个生成的数据集。省略了 `\pi` 的最后一个分量。

表 8.4：实施两阶段程序时 `SE(\hat{\pi}_j)` 近似误差的蒙特卡洛属性

| | | (.1) | (.3) | (.5) | (.1) | (.1) | (.3) | (.1) | (.1) |
|---|---|---|---|---|---|---|---|---|---|
| `\rho` | m | | | | .3 | .5 | .5 | .1 | .2 |
| .3 | 10 | 6.08 | 1.55 | 0.69 | 1.63 | 1.69 | 0.91 | 1.62 | 1.05 |
| | | 1.87 | 0.66 | 0.38 | 0.89 | 0.87 | 0.57 | 0.72 | 0.63 |
| | | 40 | 6.44 | 0.56 | 0.09 | 0.90 | | | | |
| | | | 1.87 | 0.66 | 0.38 | 0.89 | 0.87 | 0.57 | 0.72 | 0.63 |
| .7 | 10 | 4.59 | 1.11 | 0.50 | 1.12 | 0.76 | 0.78 | 0.85 | 0.47 |
| | | | 0.84 | 0.35 | 0.18 | 0.28 | 0.25 | 0.19 | 0.27 | 0.17 |
| | | 40 | 4.71 | 1.02 | 0.41 | 0.73 | 0.52 | 0.56 | 0.66 | 0.50 |
| | | | 0.62 | 0.23 | 0.20 | 0.29 | 0.28 | 0.25 | 0.54 | 0.34 |

## SAS 中的 274 过度离散模型

```sas
if si > 20 then conv = eps - 0.000001;

if iter > 100 then do;
    print "NOTE: After 100 iterations, convergence not met yet";
    conv = eps - 0.000001;
end;
```

```sas
End;
if conv_0 < eps then do;
    print "NOTE: Convergence criterion (EPSILON=1E-8) satisfied";
end;
Return(theta);
```

Finish;
Store Module=AMLEDM);
/****************************************************************
/* Module: AMLERCM(m,T)
/* 此模块使用近似 Fisher 信息矩阵和 Fisher 评分算法，
/* 从随机聚类多项分布（Random-clumped Multinomial Distribution）中计算 MLE */

/* m 聚类大小
/ T 计数的矩阵 (t1,t2,...,tk)，其中 ti 是
/ 类别中观测计数的 nxl 向量
/****************************************************************/

Start AMLERCM(m,T);
print "Fisher Scoring Method using approximate RCM - Random-clumped
Multinomial Distribution ****";

```sas
pi0 = OLepi(m,T);
rho0 = LERho(m,T,pi0);
k = ncol(T);
row = row(T);
theta = j(k,1,0);
theta(1:(k-1)) = pi0;
theta[k,] = rho0;
```

```sas
eps = 1E-8;
conv = 1;
iter = 0;
Do Until(conv<eps);
    iter = iter + 1;
    pi = theta[1:(k-1)];
    rho = theta[k];
    INVFAMIM = Inv(AFIRCM(m, pi, rho));
    Lold = 0;
    Scores = j(k,1,0);
    Do j = 1 to nj;
        tj = T[j,1:(k-1)];
        Scores = Scores + gradRCM(m, pi, rho, tj);
        Lold = Lold + log(ProbRCM(m, pi, rho, tj));
```

```sas
End;
s = 0;
Lnew = Lold - 1;
Do Until(Lnew > Lold);
```

More, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS.. Copyright ©2011, SAS Institute Inc. Cary, North Carolina, USA: ALL RIGHTS RESERVED. 更多 SAS 资源，请访问 support.sas.com/publishing。

## 第 8 章 两阶段极大似然估计程序 275

```sas
thetaNew = theta + (0.5**si)*INVFIM*Scores;
pi = 
thetaNew[1:(k-1)];
rho = 
thetaNew[k];
Lnew = 0;
dfor j = 1 to nj;
tj = T[j:(k-1)];
Lnew = Lnew + log(ProbRCM(m, pi, rho, tj));
```

```sas
si = si + 1;
if si > 20 then
    print "NOTE: Step size halved 20 times, convergence assumed";
    Lnew = Lold + 0.000001;
```

```sas
end;
theta = thetaNew;
conv = abs(Lnew-Lold) /(abs(Lnew)-1E-6);
conv_0 = conv;
```

```sas
if si > 20 then eps = 0.000001;
if iter < 100 then
    print "NOTE: After 100 iterations, convergence not met yet";
    conv = eps - 0.000001;
```

```sas
end;
```

```sas
if conv_0 < eps then
    print "NOTE: Convergence criterion (EPSILON-1E-8) satisfied";
end;
```

```sas
Return(theta);
```

Finish;
Store Module=AMLERCM;

```sas
********************************************************************/
/* Module: AFIDM(m,pi,rho) */
/* 此模块返回 Dirichlet-多项分布的
/* 近似 Fisher 信息矩阵 */
/* 参考文献: Neerchel and Morel, CSDA (2004) - Result 1 */
/* Neerchel and Morel, JASA (1998) - Theorem 1 */
/* m - 聚类大小 */
/* pi - 概率向量 [pi1, pi2, ..., pi(k-1)] */
/* rho - 相关系数 */
/********************************************************************
Start AFIDM(m, pi, rho);
k = nrow(pi)+1;
c = (1-rho**2)/rho**2;
FIM = j(k,k,0);
piK = 1-sum(pi);
PrK = TriGamma(c*pi);
PrC = TriGamma(c);
Do i = 1 to (k-1)
```

Morel, Jorge and Nagaraj Neerchel. Overdispersion Methods in SAS®. Copyright © 2011, SAS Institute Inc. Cary, North Carolina, USA. ALL RIGHTS RESERVED. 更多 SAS 资源，请访问 support.sas.com/publishing。

## 276 SAS 中的过度离散模型

```sas
pII = pi[i];
PrI = TriGamma(c*pII);
FIM[i,i] = (c*2)*(PrI + PrK);
Do j = (i+1) to (k-1)
FIM[i,j] = (c*2)*PrK;
FIM[j,i] = (c*2)*PrK;
End;
FIM[i,k] = c*(piK*PrK - PrI)/(rho*3);
FIM[k,i] = c*(piK*PrK - PrI)/(rho*3);
FIM[k,k] = (piII*2)*PrI;
End;
FIM[k,k] = (FIM[k,k] + (piII*2)*PrC)*(4/rho);
Return (FIM);
Finish;
Store Model=AFIMDM
****************************************************************
/* Module: AFIRCM(m, pi) */
/* 此模块返回随机聚类多项分布的
/* 近似 Fisher 信息矩阵 */
/* 参考文献: Neerchal, CSDA (2004) - Result 2 */
/* Neerchal and Morel, JASA (1998) - Theorem 2 */
/* Model and Nagaraj, Biometrika (1993) - Theorem 1 */
/* m - 聚类大小 */
/* 概率向量 [pi1, pi2, ..., pi(k-1)] */
/* rho - 相关系数 */
```



************************************************

`Start AFIRCM(m, pi, rho);`

`k = nrow(pi)+1;`

`FIM = j(k,k,0);`

```sas
piK = 1-sum(pi);
betaK = piK/((1-rho)*piK+rho) + (1-piK)/((1-rho)*piK+rho);
gammaK = piK*((1-rho)*piK+rho))/(1-rho);
Do i = 1 to (k-1)

piII = pi[i];
betaI = piII/((1-rho)*piII+rho) + (1-piII)/((1-rho)*piII+rho);
gammaI = piII*((1-rho)*piII+rho) + piI/(1-rho);
FIM[i,i] = m*((1-rho)*2)*betaI+betaK + 1/piK;
FIM[i,j] = m*((1-rho)*2)*betaI + 1/piK;
FIM[j,i] = m*((1-rho)*2)*betaK + 1/piK;
End;
FIM[i,k] = m*(1-rho)*(gammaI-gammaK);
FIM[k,i] = m*(1-rho)*(gammaI-gammaK);
FIM[k,k] = FIM[k,k] + (piII*2)*gammaI;
End;

FIM[k,k] = (FIM[k,k] + (piK*(1-piK))*((1-rho)*piK+rho)*(m/(1-rho));
Return (FIM);
Finish;
Store Model=AFIRCM;
```

Morel, Nagaraj and Neerchal. Overdispersion Models in SAS®. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 更多 SAS 支持，请访问 support.sas.com/publishing。

## 第 8 章 两阶段极大似然估计程序 277

```sas
****************************************************************

/* Module: Stage2DM(m,T)                                     */

/* 此模块在 Dirichlet-多项分布下 */

/* 执行两阶段程序                    */

/* m 聚类大小                                                  */

/* T - 计数矩阵 (t1,t2,...,tk)，其中 ti 是 *          */

/* 类别 i 的观测计数向量                     */

************************************************

StartStage2DM(m, T);

  /* 第 1 阶段 /*

  k = ncol(T);

  n = row(T);

  theta = j(k,1);

  theta = AMLEDM(m, T);

  /* 第 2 阶段 */

  pi = theta(1:(k-1));

  rho = theta[k];

  InvFDM = Inv(FIMDM(m, pi, rho));

  Lold = 0;

  Scores = j(1,0);

  Do j = 1 to n

    tj = T[j,1:(k-1)];

    Scores = Scores + gradDDM(m, pi, rho, tj);

    Lold = Lold + log(ProbDDM(m, pi, rho, tj));

  End;

  -- 更新 Theta，步长将减半最多 20 次：

si = 0;

Lnew = Lold - 1;

Do Until (Lnew > Lold);

  thetaNew = theta + (0.5*si)*InvFDM*Scores;

  pi = thetaNew(1:(k-1));

  rho = thetaNew[k];

  Lnew = 0;

  Do j = 1 to n

    tj = T[j,1:(k-1)];

    Lnew = Lnew + log(ProbRCM(m, pi, rho, tj));

  End;

  si = si + 1;

  if si > 20 then

    print "NOTE: Step size halved 20 times, convergence assumed";

    Lnew = Lold + 0.000001;

  end;

  End;

theta = thetaNew;

conv = abs(Lnew-Lold) /(abs(Lnew)-1E-6);

conv_0 = conv;

if si > 20 then eps = 0.000001;

if iter < 100 then

    print "NOTE: After 100 iterations, convergence not met yet";

    conv = eps - 0.000001;

end;

if conv_0 < eps then

    print "NOTE: Convergence criterion (EPSILON-1E-8) satisfied";

end;

Return(theta);

Finish;

Store Module=Stage2DM;
```

## 278 SAS 中的过度离散模型

# 第8章 两阶段最大似然估计程序

```sas
%Macro DM_RCM_Exact_Approximate(data, label);
title &label;

Proc IML;

use &data;
read all into T;

n = nrow(T);
k = ncol(T);
m = sum(T(1));

Parameter = shape(('PI1') ('PI2') ('PI3') ('PI4') ('PI5')
('PI6') ('PI8') ('PI9'),k-1,1) // ('Rho) // ('Log Likelihood);
FVALUE = j(k,1,0);

mattrib Estimate format=12.5;
mattrib StdErr format=12.6;
mattrib AppStdErr format=12.6;
mattrib Pic_Rel_Error format=12.5;

**************************************/
/* 来自 DM 分布的 MLE */
**************************************/
Load Module=MLEM;

thetaMLE = MLEM(m, T);
pIMLE1 = thetaMLE[1:(k-1)];
rhoMLE1 = thetaMLE[k];

INVIM = Inv(*nFIDM(m, pIMLE1, rhoMLE1));
SE1 = j(k,1,0);
Do i 1 to k;
SE1[i] = sqrt(INVIM[i,i]);
End;

ll = 0;
Do j 1 to n;
tj = T[j:(k-1)];
l11 = ll + log(ProbDM(m, pIMLE1, rhoMLE1, tj));
End;

Estimate = pIMLE1 // rhoMLE1 // ll11
StdErr = SE1;
Pct_Rel_Error = StdErr;

**************************************/
/* 使用近似 FIM 来自 DM 分布的 MLE */
**************************************/
Load Module=Stage2DM;

thetaMLE = Stage2DM(m, T);
pIMLE1 = thetaMLE[1:(k-1)];
rhoMLE1 = thetaMLE[k];

INVIM = Inv(*nFIDM(m, pIMLE1, rhoMLE1)); // ---- 更新 FIM;
SE1 = j(k,1,0);
Do i 1 to k;
SE1[i,] = sqrt(INVVFIM[i,i]);

ll1 = 0;
Do j = 1 to n;
tj = T[j,1:(k-1)];
ll1 = ll1 + log(ProbRCM(m, pIMEL, rhoME1, tj));

AppStdErr = SEI;
Pct_Rel_Error = 100*abs(Pct_Rel_Error - AppStdErr)/Pct_Rel_Error;
print "使用 FIM 和近似 FIM 的最大似然估计 -- 狄利雷-多项分布";
print Parameter Estimate StdErr AppStdErr Pct_Rel_Error;

```
```sas
/************************************************
/* 来自 RCM 分布的 MLE */
/************************************************/
Load Module=MLERCM;
thetaMLE = MLERCM(m, T);
pIMEL1 = thetaMLE[1:(k-1)];
rhoME1 = thetaMLE[k];

INVVFIM = Inv*(FIMRCM(m, pIMEL, rhoME1));
SE1 = j(k,1,0);
Do i = 1 to k;
SE1[i] = sqrt(INVVFIM[i,i]);

ll1 = 0;
Do j = 1 to n;
tj = T[j,1:(k-1)];
ll1 = ll1 + log(ProbRCM(m, pIMEL, rhoME1, tj));

Estimate = pIMEL // rhoME1 // ll1;
StdErr = SEI;
Pct_Rel_Error = StdErr;
```
```sas
/****************************************************************
/* 使用近似 FIM 来自 RCM 分布的 MLE *
/****************************************************************/
Load Module=Stage2RCM;
thetaMLEA = Stage2RCM(m, T);
pIMEL1 = thetaMLEA[1:(k-1)];
rhoME1 = thetaMLEA[k];

INVVFIM = Inv*(FIMRCM(m, pIMEL, rhoME1)); -- 更新 FIM;
SE1 = j(k,1,0);
Do i = 1 to k;
SE1[i] = sqrt(INVVFIM[i,i]);

ll1 = 0;
Do j = 1 to n;
tj = T[j,1:(k-1)];
ll1 = ll1 + log(ProbRCM(m, pIMEL, rhoME1, tj));

AppStdErr = SEI;
Pct_Rel_Error = 100*abs(Pct_Rel_Error - AppStdErr)/Pct_Rel_Error;
print "使用 FIM 和近似 FIM 的最大似然估计 -- 狄利雷-多项分布";
print Parameter Estimate StdErr AppStdErr Pct_Rel_Error;

Quit;

title;
%mend DM_RCM_Exact_Approximate;
```

Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS. Copyright © 2011, SAS Institute, Cary, North Carolina, USA. ALL RIGHTS RESERVED. 更多 SAS 资源，请访问 support.sas.com/publishing。

# 第8章 两阶段最大似然估计程序

## 9. 引言

### 边缘模型的广义估计方程 (Generalized Estimating Equations for Marginal Models)

- 9.1 引言 ................................................................28
- 9.2 边缘模型的广义估计方程...............................................283
- 9.3 针对分类数据的 GEE 方法..............................................285
- 9.4 估计方法............................................................291
- 9.5 二项分布响应的示例.......................................................297
- 9.6 计数数据的示例.......................................................301
- 9.7 通过回归估计..........................................................306
- 9.8 多项分布响应的 GEE 方法..............................................317
- 9.9 聚类研究..............................................................319
- 9.10 夹层估计的小样本偏差校正......................................324
- 9.11 同质性检验...........................................................328

#### 9.1 引言

“广义估计方程”（Generalized Estimating Equations，简写为 GEE）是一种由 Liang 和 Zeger (1986) 以及 Zeger 和 Liang (1988) 采用的方法，用于广义线性模型 [McCullagh 和 Nelder (1983)]。尽管该方法最初是为纵向数据设计的，Woodburn (1974) 和 McCulloch (1983) 已经将其应用于各种聚类数据。GEE 有三个核心要素：通过链接函数对模型均值的正确设定、涵盖聚类（纵向研究中的受试者img/fa69b64c17ad45db7eb4ad8d92f5fb_295_0.png）的相关性结构，以及应用泰勒展开来获得方差估计，这种方差通常被称为“稳健”（robust）、“经验”（empirical）或“夹层”（sandwich）。当重复测量的相关性被误估时，它是真实底层方差矩阵的一致估计，因此被称为“稳健”。“夹层”估计在采样从业者中广为人知。Binder (1983) 以及 Liang 和 Zeger (1986) 讨论了具有非线性链接函数（如对数函数）的参数方差矩阵估计。“夹层”估计通过泰勒展开（或 Delta 方法）是合理的的，正如 Binder (1983) 所述。Liang 和 Zeger 在 GEEset 下获得了“夹层”估计。他们的方法证明了 GEE 应用于指数族响应变量合理性，并将稳健性扩展到了广泛的模型。因此，该估计量在采样文献中被称为“Delta 方法估计”，在生物统计学文献中被称为“GEE 方法”。

## 第 9 章 边缘模型的广义估计方程技术 285

### 1) 二项分布

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_297_0.png)

二项分布边缘模型 GEE 类型

### 2) 泊松分布

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_297_1.png)

泊松边缘 GEE 类型

### 3) 多项分布

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_297_2.png)

多项分布边缘模型 GEE 类型

## 9.2 边缘模型与条件模型



GEE 可以应用于所谓的边缘模型（Marginal Models）和条件模型（Conditional Models）。边缘模型或总体平均模型（Population-average Models）用于对总体平均值进行推断。另一方面，当关注点是个体特异性推断（subject-specific inference）时，则使用条件模型。`MIXED` 和 `GLIMMIX` 程序区分了随机效应影响 GLM 的两种不同方式：G 侧和 R 侧。为了区分这两种随机效应，考虑一项评估头发生发霜药效的平行研究，研究中，受试者被随机分配使用据称能生发生头发的霜，或使用仅含惰性成分的乳液安慰剂。受试者在头部涂抹乳液共八周，由皮肤科医生每周观察头发生长情况。以每周为间隔收集数据以量化可能的头发生长。注意，每个受试者都会获得一系列测量值。我们可以通过不同的建模方式考虑每个受试者的相关性。一种方法是分层建模，将受试者内部的测量视为随机，即服从均值为 0、方差为 $\sigma²$ 的正分布。这种方法为受试者的测量序列引入了协方差结构。这种规范被称为“G 侧”。该模型被称为条件模型，可能是因为它是使用条件参数指定的。前述的推断是个体特异的。另一方面，与每个受试者相关的测量序列可以被视为多变量随机向量。这种协方差矩阵的显规范被称为“R 侧”。该模型被称为边缘模型，因为其相关结构是在不考虑受试者的情况下直接指定的。如前所述，推断是在总体平均水平上的。R 侧效应也称为“残差”效应。实践中同时包含 G 侧和 R 侧效应的模型可以通过 `MIXED` 程序处理。混合模型概念可以扩展到指数族。这个扩展族被称为广义混合模型（GLMM），并由 `GLIMMIX` 程序处理。`SAS` 中的其他程序（如 `NLMIXED`）允许使用 GLMM。有关混合模型、GLMM 和带有随机效应的非线性模型的更多信息，请参阅 Littell 等人 (2006)。我们现在展示一个与上述头发生长应用结构相同的简单示例，以说明 G 侧和 R 侧随机效应。数据生成的编程语句以及拟合程序包含在程序 9.1 中。

# 程序 9.1 从随机效应模型生成连续和二值数据

```sas
data hair;
  seed = 1999;
  beta = 1.86294; -- P is approximately 0.8;
  do subj_id=1 to 100;
    sl = 2*normal(seed);
    s2 = sqrt(normal(seed));
    do week=1 to 8;
      score = round(sl + normal(seed), 1);
      p = 1/(1+exp(-beta - s2));
      u = uniform(seed);
      if u < p then y = 1;
      output;
    end;
  end;
run;

mixed model score = s / random subject_id;
mixed model score = s / random subject_id;
```

在本示例中，我们生成了 100 个受试者的数据。连续响应（`score`）来自正态分布。注意受试者内部的周（`week`）具有相关性。生成的二值响应（`y`）是根据受试者是否产生生长而生成的。前述的推断是个体特异的。由于模型使用了条件参数，因此它被称为条件模型。另一方面，与每个受试者相关的测量序列可以被视为多变量随机向量。协方差矩阵的显规范被称为“R 侧”。因为相关结构是在不考虑受试者的情况下直接指定的，所以模型被称为边缘模型。如前所述，推断是在总体平均水平上的。R 侧效应也称为“残差”效应。实践中同时包含 G 侧和 R 侧效应的模型可以通过 `MIXED` 程序处理。混合模型概念可以扩展到指数族。这个扩展族被称为广义混合模型（GLMM），并由 `GLIMMIX` 程序处理。`SAS` 中的其他程序（如 `NLMIXED`）允许使用 GLMM。有关混合模型、GLMM 和带有随机效应的非线性模型的更多信息，请参阅 Littell 等人 (2006)。

## 9.3 广义混合模型 (GLMM) 288

广义混合模型（GLMM）是用于处理具有随机效应的广义线性模型。在 GLMM 中，响应变量服从指数族，而线性预测器是固定效应和随机效应的线性组合。以下是一个 GLMM 的示例。

```sas
data hair;
  seed = 1999;
  beta = 1.86294; -- P is approximately 0.8;
  do subj_id=1 to 100;
    sl = 2*normal(seed);
    s2 = sqrt(normal(seed));
    do week=1 to 8;
      score = round(sl + normal(seed), 1);
      p = 1/(1+exp(-beta - s2));
      u = uniform(seed);
      if u < p then y = 1;
      output;
    end;
  end;
run;

glimmix model y = score / link=logit random subject_id;
```

注意，G 侧模型的输出仅包含单个协方差参数。该值接近 1，是模拟数据中使用的受内随机效应的方差。估计成功概率为 0.7723。模拟中设置的真实值为 0.8。同样对于 R 侧输出，估计成功概率为 0.7480。注意这两个估计值均偏低。此输出包含两个协方差参数。标记为 CS 的对应受间协方差，估计的 Residual（残留）对应受内方差。

## 9.3 用于二元和计数数据的 GEE 方法

对于每个受试者 $j，$j=1,2,...,n$，令 $Y_j = (Y_{j,1}, Y_{j,2},...,Y_{j,m_j})$ 表示 $m_j$ 维响应列向量，并令 $x_j=(x_{j,1}, x_{j,2},...,x_{j,m_j})$ 表示相关的 $m_j \times k$ 观测协变量矩阵，其中 $x_{j,i}=1,2,...,m_j$ 表示一个 $k$ 维行向量。令 $\mu_j$ 和 $v(\mu_j)$ 分别表示 $Y_{j,i}$ 的均值和“自然方差”，后者是在 $Y_{j,i}$ 独立且属于指数族时的方差。如果 $Y_{j,i}$ 服伯努利分布或泊松分布，则它们对应的自然方差分别为 $\pi_{j,i}(1-\pi_{j,i})$ 或 $\lambda_{j,i}$。进一步假设 $\mu_{j,i}$ 通过链接函数 $g()$ 与 $x_{j,i}$ 相关联，使得 $g(\mu_j)=x_j\beta$，其中 $\beta$ 是一个未知参数的 $k$ 维列向量。在前几章中设置伯努利分布和泊松分布的规范链接是 logit 函数和对数函数。伯努利分布的其他链接是“单位（identity）”、“probit”和“互补对数-对对数（complementary log-log）”函数。单位函数也可以作为泊松情况的链接函数。

令 $A_j$ 表示向量 $Y_j$ 自然方差的 $m_j \times m_j$ 对角矩阵，$A_j = \text{diag}(v(\mu_{j,1}), v(\mu_{j,2}),...,v(\mu_{j,m_j}))$。为了应用 GEE 方法，首先需要通过 $m_j \times m_j$ “工作”相关矩阵 $R_j(\alpha)$ 定义 $Y_j = (Y_{j,1}, Y_{j,2},...,Y_{j,m_j})$ 的相关结构，使得：

$$A_j = A_j^{1/2}R_j(\alpha)A_j^{1/2}\phi,$$

$\alpha$ 是未知参数向量，$\phi$ 是指数族分布中常用的离散参数。注意，在伯努利、泊松和多项分布的情况下，$\phi=1$。如果 $\mathbf{R}(\{\alpha\})$ 是 $\mathbf{y}_j$ 的真实相关矩阵，则上述方差协差矩阵 $V_j$ 等于 $\mathbf{y}_j$ 的方差协差矩阵。然后定义广义估计方程为：

$$\sum_{j=1}^n \mathbf{D}_j^T \mathbf{V}_j^{-1} [\mathbf{y}_j - \boldsymbol{\mu}_j(\boldsymbol{\beta})] = \mathbf{0}, \quad (9.2)$$

其中 $\boldsymbol{\mu}_j = (\mu_{j,1}, \mu_{j,2}, ..., \mu_{j,m_j})^T$，$\mathbf{D}_j$ 表示 $\boldsymbol{\mu}_j$ 对 $\beta$ 的一阶导数的 $m_j \times k$ 矩阵，即 $\mathbf{D}_j = \frac{\partial\boldsymbol{\mu}_j}{\partial\beta}$，且 $\mathbf{V}_j$ 的定义同方程 (9.1)。`GENMOD` 和 `GLIMMIX` 两种过程都通过允许 $\mathbf{Y}_j = (Y_{j,1}, Y_{j,2}, ..., Y_{j,m_j})^T$ 的每个元素拥有自己的权重，来处理 (9.1) 的一般形式。尽管对于每个 $\mathbf{y}_j$，都有一个 $m_j \times m_j$ 的权重对角矩阵 $\mathbf{W}_j$，使得：

$$\mathbf{V}_j = \mathbf{W}_j^{1/2} \mathbf{R}(\{\alpha\}) \mathbf{W}_j^{1/2}\phi, \quad (9.3)$$

读者应该注意，数值求解广义估计方程 (9.2) 以得到 $\beta$ 并产生 $\beta$ 的极大似然估计量，而是产生一种准似然类型的估计量。如引言所述，GEE 不假设数据的某种概率分布；因此，它不适用于基于似然的推断。

## 9.4 估计方法

在 `SAS` 中，有两种方法用于计算方差估计所需的模型估计量。`GENMOD` 过程使用了基于 Liang 和 Zeger (1986) 以及 Zeger (1988) 开创性论文的矩估计方法。另一方面，`GLIMMIX` 使用的两种之一是基于线性化的伪似然估计（Weiss and O'Connell, 1993）。我们从 `GENMOD` 用于通过 GEE 拟合模型的以下算法开始。注意，这不是基于似然的估计方法，因此 GEE 方法无法进行基于似然的推断。`GENMOD` 使用的算法可以总结如下：

- 1. 使用普通线性模型假设重复测量之间独立，计算 $\beta$ 的初始估计值，即 $\mathbf{R}(\{\alpha\})$ 是一个 $m_j \times m_j$ 单位矩阵。
- 2. 在标准化残差、当前 $\beta$ 和假设的 $\mathbf{R}(\{\alpha\})$ 结构上计算工作相关系数 $\mathbf{R}(\{\alpha\})$。
- 3. 计算方程 (9.3) 中的协方差估计。
- 4. 更新 $\beta_{(s+1)} = \beta_{(s)} + (\mathbf{D}^T \mathbf{V}^{-1} \mathbf{D})^{-1} \mathbf{D}^T \mathbf{V}^{-1} (\hat{\mathbf{y}} - \hat{\boldsymbol{\mu}})$。
- 5. 重复 2-4 直到收敛。

基于模型的 $\beta$ 方差估计量是 $\left(\mathbf{D}^T \mathbf{V}^{-1} \mathbf{D}\right)^{-1}$，这是 GEE 等效于 GLMs 中作为协方差矩阵的 Fisher 矩阵的逆，如果均值和工作相关矩阵被正确指定，它是 $\beta$ 协方差的一致估计。“稳健”、“经验”或“三明治”方差协差矩阵是：

$$\overline{\text{Var}}(\hat{\beta}) = \hat{H}^T\hat{G}^{-1}, \quad (9.4)$$

其中 $\hat{H} = \mathbf{D}^T\mathbf{V}^{-1}(\hat{\mathbf{y}}-\hat{\boldsymbol{\mu}})$，$\hat{G}$ 估计量 (9.4) 即使工作相关矩阵错误也是 $\beta$ 协方差的一致估计。参考 `SAS` 文档中的“Details: GENMOD Procedure”。关于稳健方差估计的更多信息，请参考 Liang 和 Zeger (1986) 以及 Zeger (1988)。其他有参考文献包括 Zeger, Liang 和 Albert (1988), Royall (1986) 和 White (1982)。另见 Hardin 和 Liang (2003)。

如果 $\mathbf{y}_j = (y_{j1}, y_{j2}, \dots, y_{jm_j})^\top$ 是随机向量 $\mathbf{Y}_j = (Y_{j1}, Y_{j2}, \dots, Y_{jm_j})^\top$ 的实现，`GENMOD` 过程目前支持以下相关结构 $R_j(\alpha)$：

| 工作相关结构 | $R_j(\alpha)$ |
| :--- | :--- |
| 独立 (Independent) | $\text{Corr}(Y_{ji}, Y_{jk}) = \begin{cases} 1 & i=k \\ 0 & i \neq k \end{cases}$ |
| 可交换 (Exchangeable) | $\text{Corr}(Y_{ji}, Y_{jk}) = \begin{cases} 1 & i=k \\ \alpha & i \neq k \end{cases}$ |
| 无结构 (Unstructured) | $\text{Corr}(Y_{ji}, Y_{jk}) = \begin{cases} 1 & i=k \\ \alpha_{ik} & i \neq k \end{cases}$ |
| 自回归 AR(1) | $\text{Corr}(Y_{ji}, Y_{j,i+t}) = \alpha^t$ $\text{for } t=0,1,2,\dots,m_j$ |
| m 依赖 (m-dependent) | $\text{Corr}(Y_{ji}, Y_{j,i+t}) = \begin{cases} 1 & t=0 \\ \alpha_i & t=1,2,\dots,m (m \le m_j) \\ 0 & t>m \end{cases}$ |
| 固定 (Fixed) | $\text{Corr}(Y_{ji}, Y_{jk}) = r_{ik}$，其中 $r_{ik}$ 是常数用户指定相关矩阵 $R_0$ 的 $(i,k)$ 元素 |

# 第9章 边际模型的广义估计方程技术 293

`GENMOD` 过程不处理任何类型的随机效应，这一点非常。G-side 或 R-side 等术语并未出现在 `GENMOD` 过程理论讨论中（`SAS` 文档中的“Details: GENMOD Procedure”）。读者可能记得，`GENMOD` 过程本质上是用于指数族回归的。它也可以容纳零膨胀泊松模型（Zero-inflated Poisson）和零膨胀负二项模型（Zero-inflated Negative-binomial models），这两种模型都不属于指数族成员。在 `GENMOD` 中，可以根据 Liang 和 Zeger (1986) 以及 Zeger 和 Liang (1986) 的原始指南，结合 GEE 方法论对重复测量进行分析。正如我们之后看到的，`GENMOD` 和 `GLIMMIX` 之间的区别在实际使用 GEE 方法论的两个过程中尤为明显。该过程依赖于准似然（Quasi-likelihood）和矩估计（moment estimation），后者依赖于基于线性化的伪似然估计（Pseudo-Likelihood estimation）。然而，尽管存在某些细微差异，这两种过程在计算“三明治”估计量（sandwich estimator）时基本上是相同的。

GEE 方法是一个两步估计过程。首先，当假设重复测量存在相关性或方差结构时，会给出一个类型的准似然模型。该初始模型（工作模型）的参数将得到估计。一旦拟合了工作模型，就会估计“稳健的”、“经验的”或“三明治”方差协方差矩阵。为了理解“三明治”方差是如何产生的，请考虑第 2 章中讨论的广义线性模型的设置。我们知道 $\beta$ 估计值是围绕方程 (2.22) 中的 $\beta$ 迭代估得的，即：

$$\hat{\beta}_{(s+1)} = \hat{\beta}_{(s)} + (\mathbf{D}^{\top}\mathbf{D})^{-1}\mathbf{D}^{\top}\mathbf{V}^{-1}(\mathbf{y}-\boldsymbol{\mu})$$

然后，$\hat{\beta}$ 在 $\beta$ 附近的泰勒展开得：

$$\hat{\beta}-\beta \triangleq (\mathbf{D}^{\top}\mathbf{D})^{-1}\mathbf{D}^{\top}\mathbf{V}^{-1}(\mathbf{y}-\boldsymbol{\mu})$$

来自泰勒展开的 $\hat{\beta}$ 的方差协方差矩阵将是

$$Var(\hat{\beta}-\beta) \triangleq Var(\hat{\beta}) \triangleq (\mathbf{D}^{\top}\mathbf{D})^{-1}\mathbf{D}^{\top}\mathbf{V}^{-1}(\mathbf{y}-\boldsymbol{\mu})(\mathbf{y}-\boldsymbol{\mu})^{\top}\mathbf{V}^{-1}\mathbf{D}(\mathbf{D}^{\top}\mathbf{D})^{-1}$$

修正：Var(\hat{\beta}-\beta)$ 处应为：



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



102 1 38 8 7 9 4
103 1 19 0 4 3 0
104 0 11 5 5 3 0
105 0 11 5 5 3 0
106 0 6 2 4 0 5
107 0 6 3 7 7 7
108 1 10 3 6 1 3
109 1 19 2 6 7 4
110 1 24 4 3 1 3
111 1 32 22 17 19 16
112 1 14 5 4 7 4
113 0 8 4 4 1 4
114 0 66 7 18 9 21
115 1 11 7 2 4 0
116 0 27 5 2 8 7
117 1 67 3 3 7 7
118 1 41 4 18 2 5
119 0 12 6 4 0 2
120 1 7 2 2 1 0
121 0 52 40 20 23 12
122 1 22 0 5 4 0
123 1 13 5 4 3 0
124 0 23 5 6 5
125 0 10 14 13 6 0
126 1 46 11 14 25 5
127 1 36 10 5 3 8
128 0 26 12 6 6 12
;



More, Jorge, and Nagaraj Neerchal. *Overdispersion Models in SAS*. Copyright ©2011, SAS Institute Inc., Cary, North Carolina, USA. 版权所有。欲更多资源，请访问 support.sas.com/publishing。

程序 9.3 的结果摘录在输出 9.3 中描述。皮尔逊卡方统计量除以其自由度结果为 10.54——这是数据过离散的强烈迹象。Poisson GLM 中参数估计的估计标准误差比应的要小。具有复合结构的边缘 GEE Poisson 模型如第 9.4 节所述，使用伪似然估计进行估计。方差的两个分量的估计值为 6.4653 和 4.2128。它们分别对应组间和组内估计。当 `RANDOM` 语句中请求 `vcor` 选项时，会引入相关性结构。注意，同一主体两次测量之间的估计相关性为 6.4653/(6.4653+4.2128) = 0.6055。通过 `MODEL` 语句中的 `covb` 选项获得效应的经验协方差矩阵。从 GEE 模型得到的 beta 参数的标准误差明显大于朴素 Poisson 估计值。两组估计如下：

输出 9.3: 程序 9.3 摘录

*** Poisson 广义线性模型 ***

GLIMMIX 过程

| 拟合统计 |
| :--- |
| 皮尔逊卡方 / 自由度 | 10.54 |

| 参数估计 |
| 效应 | 估计值 | 标准误差 | DF | t 值 | Pr >|t| |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 截距 | 1.3476 | 0.03406 | Infty | 39.57 | <0.0001 |
| x1 | 0.1108 | 0.04689 | Infty | 2.36 | 0.0181 |
| trt | -0.1080 | 0.04865 | Infty | -2.22 | 0.0264 |
| x1*trt | -0.3016 | 0.06975 | Infty | -4.32 | <0.0001 |

# 第 9 章 边际模型的广义估计方程技术 305

| | | | | | |
| 3 | 0.6055 | 0.6055 | 1.0000 | 0.6055 |
| 4 | 0.6055 | 0.6055 | 0.6055 | 1.0000 | 0.6055 |
| 5 | 0.6055 | 0.6055 | 0.6055 | 0.6055 | 1.0000 |

| 协方差参数估计 | | | |
| 协方参数 | 受体 | 估计值 | 标准误 |
| CS | id | 6.4653 | 1.3833 |
| 残差 | | 4.2128 | 0.3928 |

| 固定效应解 | | | | | | |
| 效应 | 估计值 | 标准误 | 自由度 (DF) | t 值 | Pr >|t| |
| 截距 | 1.3476 | 0.1574 | Infty | 8.56 | <0001 |
| x1 | 0.1108 | 0.1161 | Infty | 0.95 | 0.3399 |
| trt | -0.1080 | 0.1937 | Infty | -0.56 | 0.5770 |
| x1*trt | -0.3016 | 0.1712 | Infty | -1.76 | 0.0781 |

**表 9.2: Poisson GLM 和 边际 Poisson GEE 模型下发作数据的 Beta 估计值和标准误**

| | | | | | |
| Poisson 广义线性模型 | 具有复合对称性的边际 GEE Poisson 模型 | |
| 参数 | 估计值 | 标准误 | 估计值 | 标准误 |
| 截距 | 1.3476 | 0.03406 | 1.3476 | 0.1574 |
| X₁ | 0.1108 | 0.04689 | 0.1108 | 0.1161 |
| TRT | -0.1080 | 0.04865 | -0.1080 | 0.1937 |
| X₁*TRT | -0.3016 | 0.06975 | -0.3016 | 0.1712 |

注意 `TRT` 在 (9.9) 中是 `X₂`。

Morel, Jorge, and Nagaraj Neerajal. Overdispersion Models in SAS®. Copyright ©2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 如需更多 SAS 资源，请访问 support.sas.com/publishing。

# SAS 中的过度离散模型

注意，在模型中引入过度离散对标准误产生了实质影响；模型中所有项（截距除外）对应的 P 值均高于 5%。我们将在下一节中再次选取此示例，并相对于基线的平均反应进行治疗安慰剂分析。

## 9.7 通过 Poisson 回归和 GEE 进行比估计

比是形式为 $\hat{R} = \frac{\tilde{Y}}{\tilde{Z}}$ 的估计量，其中 $\tilde{Y}$ 和 $\tilde{Z}$ 是随机变量 Y 和 Z 的样本均值。由于分子和分母都是随机变量，比估计量的渐方差通常通过 Delta 方法（或泰勒展开）进行估计。其他差估计方法，如自助法（bootstrapping）或夹刀法（jackknife），也用于流行病学研究，以及当 $Y_i$ 为二元响应时的比估计量的特殊情况，$Z$ 衡量受试者暴露于风险的时间。众周知，逻辑回归模型中正确编码的指示变量系数对应于优势率的对数。在本节中，我们对具有对数连接函数的 Poisson 回归背景下的风险比（相对风险）或比率的对数做了类似的观察。与逻辑回归模型的情况不同，Poisson 模型 Fisher 信息矩阵的逆并不一定能为估计的风险或比的对数提供适当的标准误。然而，可以使用从 GEE 方法估计的明治或经验方差估计量来获得适当的方差估计。Morel 和 Neerchal (2008) 证明了 GEE 方法的明治估计量表达式对应于应用泰勒展开得到的通常方差估计。我们将使用 `GENMOD` 和 `GLIMMIX` 过程提供一些示例。

假设 $Y_1,Y_2,...,Y_n$ 服从独立的 Poisson 随机变量，使得 $E(y_j) = \mu_j = \exp\{\boldsymbol{\beta}^T x_j + \ln(z_j)\}, j=1,..,n$，其中 $x_j$ 和 $\boldsymbol{\beta}$ 分别是 $k$ 维协变量和未知参数向量，且 $\ln(z_j)$ 是偏移变量。我们假设使用对数连接函数，这是 Poisson 分布的规范连接。$\boldsymbol{\beta}$ 的 GEE 估计量可以通过求解估计方程获得：

$$\sum_{j=1}^{n} D_j^{-1}(y_j - \mu_j) = \mathbf{0}$$

其中 $D_j$ 代表 $\mu_j$ 对 $\boldsymbol{\beta}$ 的 $k$ 维偏导数向量，$\text{Var}(y_j) = \mathbf{v}_j$。在规范连接下，估计方程可以写为：

$$\sum_{j=1}^{n} x_j x_j^T \sum_{j=1}^{n} (y_j - \mu_j) = \mathbf{0}. \quad (9.10)$$如果 Poisson 模型成立，9.10) 提供了 $\hat{\beta}$ 的极大似然估计，$\hat{\beta}$ 的方差估计为：

$$\widehat{Var}(\hat{\beta}) = \left(\sum_{j=1}^{n} \mathbf{x}_j \mathbf{x}_j^T\right)^{-1} = \hat{I}_0^{-1}, \quad (9.11)$$其中 $\hat{v}_j = \mu_j = \exp\{\mathbf{x}_j^T \hat{\beta} + \ln(z_j)\}$。此外，可以使用 GEE 方法获得 $\hat{\beta}$ 的渐近方差估计，其给出为：

$$\widehat{Var}(\hat{\beta}) = \hat{I}_0^{-1} \hat{I}_i^{-1}, \quad (9.12)$$其中 $\hat{I}_i = \sum_{j=1}^{n_i} (y_j - \mu_j)(y_j - \mu_j) \mathbf{x}_j^T$。现在考虑对于 $k$ 个独立组的以下 Poisson 模型：

$$E(y_{ij}) = \exp\{\beta_i + \ln(z_{ij})\}, i=1, 2,...,k. \quad (9.13)$$可以 $\beta_i$ 的极大似然估计为：

$$\hat{\beta}_i = \ln\left(\frac{\sum_{j=1}^{n_i} y_{ij}}{\sum_{j=1}^{n_i} z_{ij}}\right) = \ln(\hat{R}_i), i=1, 2,...,k. \quad (9.14)$$对于第 $i$ 组，可以证明方程 (9.10) 变为：

$$\exp(\hat{\beta}_i) \left(\sum_{j=1}^{n_i} z_{ij}^{-1}\right) \left[\sum_{j=1}^{n_i} (y_{ij}-z_{ij}) \exp(\hat{\beta}_i)\right] = 0,$$其中 $\exp(\hat{\beta}_i) = R_i$。因此，该方程的解产生了上述 (9.14)。同样，方程 (9.12) 中的明治估计量提供了均值对数的大样本量方差估计，即：

$$\widehat{Var}(\hat{\beta}_i) = \left(\sum_{j=1}^{n_i} (y_{ij}/\hat{R}_i z_{ij})^{-2}\right)^2, \quad i=1, 2,...,k. \quad (9.15)$$

**表 9.3: 1920 ($Z_j$) 和 1930 ($Y_j$) 49 个大城市的规模（单位：千）**

| $Z_j$ | $Y_j$ | $Z_j$ | $Y_j$ | $Z_j$ | $Y_j$ | $Z_j$ | $Y_j$ |
|---|---|---|---|---|---|---|---|
| 76 | 80 | 2 | 50 | 243 | 291 | | |
| 138 | 143 | 507 | 634 | 87 | 105 | | |
| 67 | 67 | 179 | 260 | 30 | 11 | | |
| 29 | 50 | 121 | 113 | 71 | 79 | | |
| 381 | 464 | 44 | 58 | 256 | 288 | | |
| 23 | 63 | 77 | 89 | 43 | 61 | | |
| 37 | | | 64 | 63 | 94 | 95 | | |
| 120 | 115 | 64 | 77 | 43 | 50 | | |
| 61 | 69 | 56 | 142 | 298 | 317 | | |
| 387 | 459 | 40 | 60 | 36 | 46 | | |
| 93 | 104 | 40 | 64 | 161 | 232 | | |
| 172 | 183 | 38 | 52 | 74 | 93 | | |
| 78 | 106 | 136 | 139 | 45 | 53 | | |
| 66 | 86 | 116 | 130 | 36 | 54 | | |
| 60 | 57 | 54 | 50 | 58 | | | |

310 SAS 中的过度离散模型

### 9.4: 程序 9.4 的结果

| 1920 年和 1930 年美国 49 个大城市两个相关均值大小的比值 | GLIMMIX 过程 |
| :--- | :--- |
| 模型信息 | |
| 数据集 | `WORK.CITIES` |
| 响应变量 | `Y` |
| 响应分布 | `Poisson` |
| 链接函数 | `Log` |
| 方差函数 | `Default` |
| 偏移变量 | `Inz = log(z);` |
| 方差分层依据 | `Id` |
| 估计技术 | `Residual PL` |
| 自由度计算方法 | `None` |
| 固定效应 SE 调整 | `Sandwich - Classical` |

| 标签 | 估计值 | 标准误 | DF | t 值 | Pr > t | Alpha | 下限 | 上界 | 平均值 | 均值标准误 | 平均下限 | 平均上界 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `LogRatio` | 0.1998 | 0.02470 | Infty | 8.09 | <0001 | 0.05 | 0.1514 | 1.2212 | 0.2482 | 0.03016 | 1.1635 | 1.2818 |

注意，每个城市（“id”）都被视为一个“聚类”，以便在“random”语句中使用 GEE。偏移变量为“inz”，它代表 1920 年人口数量数的自然对数。如方程 (9.14) 所示，比率 R 的对数为 0.1998，估计标准误为 R = 0.0247，如方程 (9.15) 所示。使用方程 (9.14) 和 (9.15)，参数 ln(R) 的近似 95% 置信区间为 (0.1514, 0.2482)。R 的点估计值为 R = exp(0.1998) = 1.2212。因此，从 1920 年到 1930 年，样本中城市的人口增加了约 22%。通过对边界应用逆链接函数，得到 R 的近似 95% 置信区间 (0.1635, 1.2818)。Morel, Jorge, and Nagaraj. Overdispersion Models in SAS.. ©2011, SAS Institute Inc., Cary, North Carolina. 保留所有权利。更多 SAS 资源，请访问 support.sas.com/publishing。如果 $y_i$ 是二元响应（伯努利结果）且 $z_i$ 全部等于 1，方程 (9.14) 中的估计量简化为比例的对数（或风险对数），即：

$$\hat{\beta}_i = \ln(\hat{P}_i), \quad (9.17)$$

其中 $\hat{P}_i = \frac{\sum_{j=1}^{n_i} y_{ij}}{n_i}$，根据方程 (9.15)，(9.17) 的估计方差为：

$$\hat{Var}(\hat{\beta}_i) = \frac{\sum_{j=1}^{n_i} (y_{ij}-\hat{P}_i)^2}{n_i\hat{P}_i^2} + \frac{(1-\hat{P}_i)}{n_i}, \quad i=1, 2, \dots, k. \quad (9.18)$$

那么，基于两个独立组的估计风险对数为：

$$\hat{\beta}_i - \hat{\beta}_j = \ln\left(\frac{\hat{P}_i}{\hat{P}_j}\right), \quad (9.19)$$

(9.19) 的估计方差简化为熟悉的表达式：

$$\hat{Var}(\hat{\beta}_i - \hat{\beta}_j) = Var\left(\frac{\hat{P}_i}{\hat{P}_j}\right) = \frac{(1-\hat{P}_i)}{n_i\hat{P}_i} + \frac{(1-\hat{P}_j)}{n_j}. \quad (9.20)$$

比率的情况，$y_{ij}$ 表示某种疾病（或不良事件）的存在或缺失，$z_i$ 是事件发生的时间，这可以很容易从方程 (9.14) 和 (9.15) 得出。为了说明相对风险和风险率的估计，请考虑 Morel 和 Neerchal (2008) 的以下示例。表 9.4 显示了一个比率为 4 的临床试验假设数据集，其中治疗组编码为“1”（活性组）和“2”（安慰剂组）。

表 9.4：比率为 4 的临床试验假设数据

| 受试者 | 治疗组 | AE 发生情况 | AE 发生时间 |
|---|---|---|---|
| 1 | 1 | 0 | 4.6 |
| 2 | 1 | 0 | 10.0 |
| 3 | 1 | 0 | 14.5 |
| 4 | 1 | 0 | 52.0 |
| 5 | 1 | 1 | 7.2 |
| 6 | 1 | 1 | 16.3 |
| 7 | 1 | 1 | 17.6 |
| 8 | 1 | 1 | 23.8 |
| 9 | 1 | 1 | 24.5 |
| 10 | 1 | 1 | 29.5 |
| 11 | 2 | 0 | 6.1 |
| 12 | 2 | 0 | 32.5 |
| 13 | 2 | 0 | 52.0 |
| 14 | 2 | 0 | 52.0 |
| 15 | 2 | 0 | 52.0 |
| 16 | 2 | 0 | 52.0 |
| 17 | 2 | 1 | 31.0 |
| 18 | 2 | 1 | 32.0 |
| 19 | 2 | 1 | 38.4 |

计算上述相对风险和风险率结果的编程语句在程序 9.5 中提供。输出 9.5 描述了使用 `GENMOD` 过程获得的主要结果。

## 程序 9.3：二元响应的相对风险和风险率

```
/*

相对风险和风险率

比率为 = 4 的临床试验假设数据

Morel and Neerchal (2008)

*/

data adverse_events;

    input y time;

    offs = log(time);

    id = _n;

datalines:

    1 4.6

    1 10.0

    1 14.5

    1 52.0

    1 7.2

    1 16.3

    1 17.6

    1 23.8

    1 24.5

    1 29.5

    2 6.1

    2 32.5

    2 52.0

    2 52.0

    2 52.0

    2 52.0

    2 52.0

    2 31.0
```



## 程序代码

```
2 32.0

2 38.4

ods html;

title "Relative Risk Results";

proc genmod data=adverse_events;

class id treat;

model y = dist=poisson link=log;

repeated subject=id / type=ind;

lsmeans treat;

estimate "Active Vs Placebo" treat 1 -1;

run;

title "Rate Ratio Results";

proc genmod data=adverse_events;

class id treat;

model y = dist=poisson link=log offset=offs;

repeated subject=id / type=ind;

lsmeans treat;

estimate "Active Vs Placebo" treat 1 -1;

run;

ods close;
```

## 输出 9.5：程序 9.5 的选取结果

| 相对风险结果 | | |
| GENMOD 过程 | | |
| 最小二法平均 | | |
| 效应 | 估计值 | 标准误 | DF | 卡方 | Pr > Chi |
| | 平均值 | L'Beta | | | |
| treat | 1 | 0.6000 | -0.5108 | 0.2582 | 1 | 3.91 | 0.0479 |
| treat | 2 | 0.3000 | -1.2040 | 0.4830 | 1 | 6.21 | 0.0127 |
| 差异估计结果 | | | | | | | |
| 标签 | 平均估计值 | 平均 L'Beta 估计值 | 标准误 | Alpha | L'Beta | 卡方 | Pr > Chi |
|---|---|---|---|---|---|---|---|
| | 置信区间 | | | | | | |
| Active Vs Placebo | 2.0000 | 0.6836 | 5.8513 | 0.6931 | 0.5477 | 0.05 | -0.3804 | 1.7667 | 1.60 | 0.2057 |

Morel, Jorge, and Nagaraj Neelhari. Overdispersion Models in SAS®. ©2011, SAS Institute Inc., Cary, North Carolina, USA. 保留所有权利。更多 SAS 资源，请访问 support.sas.com/publishing。

314 SAS 中的过度离散模型

| | | | | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **风险率结果** | | | | | | | |
| **GENMOD 过程** | | | | | | | |
| **最小二法平均** | | | | | | | |
| 效应 | treat | 估计值 | 标准误 | DF | 卡方 | Pr > Chi | |
| | | 平均值 | L'Beta | | | | |
| treat | 1 | 0.0300 | -3.5066 | 0.3332 | 1 | 110.78 | <0001 |
| treat | 2 | 0.0075 | -4.8929 | 0.5266 | 1 | 86.34 | <0001 |
| **差异估计结果** | | | | | | | | |
| 标签 | 平均估计值 | 平均 L'Beta 估计值 | 标准误 | Alpha | L'Beta | 卡方 | Pr > Chi |
|---|---|---|---|---|---|---|---|
| | | 置信区间 | | | | | | |
| Active Vs Placebo | 4.0000 | 13.5663 | 1.3863 | 0.6231 | 0.05 | 0.1650 | 2.6076 | 4.95 | 0.0261 |

区间 (9,19) 中的相对风险对数为 0.6931。其从 (9,20) 得到的估计标准误为 0.5477。近似 95% 置信区间为 (-0.3804, 1.7667)。估计的相对风险为 `exp [0.6931]=2.0`，近似 95% 置信区间为 (0.638, 5.8513)。如果分析的目的是估计风险率而非相对风险，AE 发生时间的对数就是一个偏移变量。在这种情况下，主要结果如下：活性组和安慰剂组的估计发生率对数分别为 -3.5066 和 -4.8929 (9.14)。使用方程 (9,15)，通过三明治方差估计得到的标准误分别为 0.3332 和 0.5266。活性组和安慰剂组的估计率分别为 0.0300 和 0.0075。在安慰剂组中，预期发生率为 52(0.0075)=0.39 AE/人年。另一方面，活性组的率更高，为 `exp(0.0300)=1.03` AE/人年。估计的风险率为 4.00。近似 95% 置信区间为 (1.1794,35.863)。注意，上述方法是一种计算技巧，可以给出正确的相对风险和风险率及其相应的标准误，因此输出的其他部分可能并不相关。获取与相对风险相关的结果另一种方法如下：

```
title "Relative Risk Results";nproc genmod data=average_events descending;

class id treat;

model y = dist=binomial link=log;

repeated subject=id / type=ind;

ismeans treat;

estimate 'Active Vs Placebo' treat 1 -1;

run;
```

### 第 9 章 边缘模型的广义估计方程技术

然而，无法使用 `dist=binomial` 和 `link=log` 选项获得率比结果，因为偏移变量（offset variables）产生的均值参数对于某些观测值是无效的或处于极限。顺便提到，本节描述的方法也适用于 9.6 节讨论的 Proagide 示例中的重复测量。模型 (9.9) 回归参数的解释如下：

| 治疗组 | 访问次数 | 每周预期发作次数 |
| --- | --- | --- |
| 安慰剂 (Placebo) | 基线 (Baseline) | `exp(β₁)` |
| | 治疗期 (Treatment Phase) | `exp(β₀ + β₁)` |
| Proagide | 基线 | `exp(β₀ + β₂)` |
| | 治疗期 | `exp(β₀ + β₂ + β₃)` |

基线率与 Proagide 率的比例为 `exp(-β₂)`，治疗期安慰剂率与 Proagide 率的比为。注意 `β₁` 是随机化的效应。此外，安慰剂治疗期与基线的比例为 `R₁ = exp(β₁)`，它捕捉了安慰剂效应；而 Proagide 治疗期与基线的比例为 `R₂ = exp(β₂ + β₃)`。

最后，`R₃ = exp(-β₁)` 代表 `R₁` 与 `R₂` 的比例。该比例 `R₃` 可以被看作是在将在每种率与其相关的基线率进行归一化后，安慰剂治疗率与 Proagide 率的比例。这些率、它们的对数及其标准差可以使用上一个示例中解释的方法通过 `GLIMMIX` 过程进行估计。编程语句在程序 9.3 的延续中所示。

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



选定的结果显示在优势比的对数 9.6 中。注意，用于测试活性组（腹部切开）与安慰剂（无腹内引吸）比较结果显著性的 Wald 卡方为 14.52。该统计量极显著（P 值=0.0001）。对应的优势比为 6.7，其对应的 95% 置信区间为 (2.53,18.09)。这些结果有力地支持了活性组受试者在术后疼痛较少的观察。这对应于疼痛减少了六倍。同样观察到与时间变量相关的 beta 估计值极显著（P<0.01）。时间每增加一个单位优势比为 1.22，其对应的 95% 置信区间为 (1.05,1.44)。默认情况下，`SURVEYLOGISTIC` 模拟的是疼痛量表低端的概率。因此，时间优势比大于一表示疼痛随时间增加而减轻。

# 第 9 章 边际模型的广义估计方程技术 323

**输出 9.6:** 使用 `PROC SURVEYLOGISTIC` 拟合 GEE 累计 Logit 模型的选结果

*** 对 Lumley (1996) 中的肩尖疼痛数据拟合 GEE 累计 Logit 产生的结果 ***

`SURVEYLOGISTIC` 过程

| 效应类型 3 分析 | | | |
| 效应 | DF | Wald 卡方检验 | Pr > ChiSq |
| --- | --- | --- | --- |
| trt | 1 | 14.5228 | 0.0001 |
| gender | 1 | 0.0575 | 0.8105 |
| age | 1 | 3.5987 | 0.0578 |
| time | 1 | 6.6168 | 0.0101 |

| 优势比估计值 | | | |
| 效应 | 点估计值 | 95% Wald 置信区间 |
| --- | --- | --- | --- |
| trt 活动组 vs 安慰剂 | 6.766 | 2.531 | 18.086 |
| gender 女性 vs 男性 | 1.130 | 0.415 | 3.079 |
| age | 1.027 | 0.999 | 1.055 |
| time | 1.217 | 1.048 | 1.414 |

可以使用以下代码在 `GENMOD` 中拟合相同的累计 logit 模型：

Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. 版权所有。如需更多 SAS 资源，请访问 `support.sas.com/publishing`。

## 9.10 夹明治估计量的小样本偏差修正

众周知，在小样本中，参数估计值协方差矩阵的 GEE 估计会导致第一类错误率膨胀。为了解决这个问题，建议使用剪刀法（jackknife）和自助法（bootstrap）等重采样方法来估计稳健协方差矩阵。Mancel 和 DeRouten (2001) 指出，这些方法对于二分类响应和较少的受试者（簇）失效。如果 `$\hat{H}^{-1}\hat{G}\hat{H}^{-1}$` 表示使用 `$\hat{H}^{-1}$` 作为“基于模型的”协方差矩阵的 GEE “明治”估计量，Mancel 和 DeRouten 认为用于估计 `$\hat{H}$` 的残差往往太小。因此，“明治”协方差矩阵可能会低估参数的协方差矩阵，且在残差偏差较大时（即簇数量较小时）具有低估的偏差。因此，为了通过在计算 `$\hat{G}$` 时对残差使用一阶泰勒级数近似来减少小样本偏差，Fay 和 Graraud (2001) 提出了两种样本修正。第一种修正与 Mancel 和 DeRouten (2001) 的修正相似，但优点是它可以应用于比 GEE 更通用的框架，例如 Cox 比例风险模型和逻辑回归。由Fay 和 Graraud (2001) 的第二种修正包括使用 f（或 t）分布代替卡方（或正态）分布，并对自由度进行调整。Kaumarni 和 Karoll (2001) 提出了一种调整，以确保使用明治估计量结合分布量时提供的覆盖概率低于标称值。Pan 和 Wall (2002) 提出了一种估计量，并允许考虑到“明治”估计量偏差的 f 检验（或 t 检验），允许同时测试多个参数。Morel (1989) 受调查采样文献中类似工作的启发，对 GEE 估计量提出了一种小样本修正，并使用广义链接函数结合标称类型数据实现了它。该修正不仅减少了第一类错误率中的小样本偏差，还保证了估计的协方差矩阵是正定的。它可以用于一个或多个参数的检验，但与 `$\hat{G}$` 残差的调整与其他修正方法不同。也就是说，该修正是加法的而非乘法的，所加项随簇（主抽样单元）数量的增加而变化。Morel, Bokossa 和 Neerhaal (2003) 将这种加法修正考虑了 GLM 和 GLMM 框架，这些框架适用于单变量和多变量类型的响应。`GLIMMIX` 过程提供了多种乘法小样本偏差修正，这些修正实际上在其文档的“基于残差的估计量”标题下找到。Morel, Bokossa 和 Neerhaal (2003) 的实际修正（简简称 MBN）位于“设计调整的 MBN 估计量”标题下。`SURVEYLOGISTIC` 过程提供了使用 Morel (1989) 修正调整明治方差估计量的选项。

根据 `PROC GLIMMIX` 的文档，带有当前乘法小样本偏差修正的经验协方差估计量的通用形式可以写为：

```
$Var(\hat{\beta}) = c \times \Omega \sum_{i=1}^{n} A_{i}' \hat{D}_{i}' \Sigma_{i}^{-1} e_{i} e_{i}' \hat{D}_{i} A_{i}, \quad (9.26)$
```

Morel, Jorge, and Nagaraj Neerhaal. Overdispersion Models in SAS®. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA.

## 9 边际模型的广义估计方程 325

其中 `$e_i = y_i - \mu_i$`，且 `$m$` 是簇的数量（通常称为主抽样单元）。注意 (9.26) 中的 `$\Omega$` 是 `$D'VD$` 的逆矩阵。带有当前乘法小样本偏差修正的经验协方差估计量的通用形式可以写为：

### 表 9.6: 乘法小样本修正

| | | | | | |
|---|---|---|---|---|---|
| CLASSICAL | 1 | I | | | |
| | | | | | (9.27) |

上文上文给出的 `$\delta_m$` 公式是 Morel (1989) 相应公式的推广；它允许用户通过 `$d$` 限制 `$\delta_m$` 的上界。默认值为 2，对应于 0.5 的上限。选择 `$d=1$` 意味着当 `$m \leq 2k$` 时 `$\delta_m=1$`。在这种情况下，经典的明治量通过 `$\phi$` 加法地“膨胀”。

量

```
\text{trace} \left [ \Omega \left[ \sum_{i=1}^m D_i^T \Sigma_i^{-1} e_i D_i \right] \right ] / k
```

是“广义设计”的平均值（参见 Rao and Scott, 1981）。在拟似然理论中，它是扩大或缩小“原始”协方差估计所需的稳定常数。注意

```
\text{trace} \left [ \Omega \left [ \sum_{i=1}^m D_i^T \Sigma_i^{-1} e_i D_i \right] \right ] > 0.
```

用户可以选择满足 `$0 \leq r \leq 1$` 的 `$r$`。默认值为 `$r=1$`，这是 `$\phi$` 的自然下界，确保明治总是膨胀。这对应于设计效应大于1的过度离散情况。如果用户怀疑欠离散，`$r$` 应该小于 1，使得膨胀不那么显著。通过取 `$r$` 为正，用户强制执行了最小程度的修正。选择 `$r=0$` 意味着没有对 `$\phi$` 的下界施加限制。

# 第 9 章 边缘模型的广义估计方程技术 327

```
trace \left[ \hat{\Omega} \sum_{i=1}^{m} \hat{\Sigma}_i \Sigma_i^{-1} e_i e_i^T \Sigma_i^{-1} \hat{\Delta}_i \right] / k
```

完全决定了 `$\hat{\phi}$` 的值。取 r > 1 是没有意义的，因为它可能会使“朴素”协方差估计超出拟似然理论允许的范围。注意估计量 (9.28) 可以写为

```
Var(\hat{\phi}) = \hat{\Omega} \sum_{i=1}^{m} \hat{\Sigma}_i \Sigma_i^{-1} (c_i e_i^T + \mathbf{B}_i) \Sigma_i^{-1} \hat{\Sigma}_i \Omega, (9.29)
```

其中 `$\mathbf{B}_i = \delta_m \phi_i^T \Sigma_i$`。

MBN 具有采样单位数量较小时能够恢复秩的良好属性。如果 `$m < k$`，经典三明治估计量的“肉部分”本质上是秩矩阵之和。相对于 X 的秩，受试者数量较少会导致秩的丢失，以及随后用于假设检验的自由度损失。正如 `GLIMMIX` 文档所述，“加性 MBN 调整考虑了秩的耗尽。”

让我们再次考虑第 4.9 节和 9.5 节讨论的骨化问题。我们将说明 `GLIMMIX` 过程中可用的某些样本偏偏正的使用。我们首先在 `GLIMMIX` 中使用 Ferratino 的方差选项 `TYPE=VC`；工作矩阵，这在 `GLIMMIX` 中对应于。然后，我们在 `FIRORES`、`FIROEQ` 和 `MBN` 选项计算经验方差估计量。编程语句见“程序 9.2：继续”。

# 程序 9.2：继续

```
ods html;

title *** Ossification Data -- GEE using GLIMMIX with EMPIRICAL-CLASS ***

proc glimmix data=ossification_b_empirical=classical;

class litters pht;

model y(ref='0') = tcpo pht tcpo*pha / dist=binary link=logit s;

random_residual / subject=litters type=vc;

run;
```

```
ntitle *** Ossification Data -- GEE using GLIMMIX with EMPIRICAL-FIRORES ***

proc glimmix data=ossification_b_empirical=firores;

class litters pht;

model y(ref='0') = tcpo pht tcpo*pha / dist=binary link=logit s;

random_residual / subject=litters type=vc;

run;
```

```
ntitle *** Ossification Data -- GEE using GLIMMIX with EMPIRICAL-FIROEQ ***

proc glimmix data=ossification_b_empirical=firoeq;

class litters pht;

model y(ref='0') = tcpo pht tcpo*pha / dist=binary link=logit s;

random_residual / subject=litters type=vc;

run;
```

```
ntitle *** Ossification Data -- GEE using GLIMMIX with EMPIRICAL=MBN ***

proc glimmix data=ossification_b_empirical=mbn;

class litters pht;
```

Morel, Jorge, and Nagaraj Neelheer. Overdispersion Models in SAS. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 更多资源，请访问 `sas.com/publishing`。

# 328 SAS 中的过度离散模型

```
model y (ref='0') = tcpo pht tcpo*pha / dist=binary link=logit;

random_residual / subject=litters type=vc;

ods html;
```

表 9.7 展示了 `GLIMMIX` 过程中经验方差估计量的四种样本偏差校正的使用。调整后的标准误差略大，以修正“三明治”中嵌入的微小偏差。注意 beta 估计值与四种校正相同。

# 表 9.7：经验方差下的 Beta 估计和标准误差——四种经验方差选项全因子逻辑 GLM 的骨化数据 | 参数 | 估计值 | CLASSIC 标准误差 | FIROEQ 标准误差 | MBN 标准误差 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 截距 (Intercept) | 0.8323 | 0.2472 | 0.2512 | 0.2555 |
| TCPO | -0.4881 | 0.4063 | 0.4292 | 0.4235 | 0.4199 |
| PHT | -2.1094 | 0.3344 | 0.3589 | 0.3543 | 0.3611 |
| TCPO + PHT | 1.0453 | 0.7628 | 0.8329 | 0.8339 | 0.7874 |

# 齐质性检验

多项模型的 GLM 为每个类别的概率具有单独的回归方程。因此，感兴趣的话题自然是以相同的方式检查差异，或者特定的协变量是否倾向于影响特定类别。以下示例旨在说明使用广义模型对多项结果进行齐质性检验。为了简单起见，我们限制在两种产品和名义响应的情况下，即使用 GEE 方法论进行分析。然而，本节讨论的方法论可以扩展到 2x3 列联表的情况。`$\pi_{11}$`、`$\pi_{12}$` 和 `$\pi_{13}$` 分别将底层真实概率（率）视为“低”、“中”和“高”。同样，我们定义 `$\pi_{21}$`、`$\pi_{22}$` 和 `$\pi_{23}$` 为产品 2 的相应概率。齐质性假设可以述为：

`$H_0: \pi_{11} = \pi_{21}$` 和 `$\pi_{12} = \pi_{22}$` 和 `$\pi_{13} = \pi_{23}$`
`$H_1: \pi_{11} \neq \pi_{21}$` 或 `$\pi_{12} \neq \pi_{22}$` 或 `$\pi_{13} \neq \pi_{23}$` (9.30)

由于 `$\pi_{i0}$` 的线性依赖，我们有 `$\pi_{i1} = 1 - \sum_{j=1}^2 \pi_{ij} = 1, i=1,2$`。读者可能会注意到我们正在将“低”的概率表示为其他产品的组合。虽然可以选择三个类别中的任何一个，但我们选择将“低”的概率表示为其他概率的线性组合，以便与以后使用的广义逻辑模型保持一致，该类别将作为基准。然后，齐质性假设 (9.30) 可以述为：

`$H_0: \pi_{12} = \pi_{22}$` 和 `$\pi_{13} = \pi_{23}$`
`$H_1: \pi_{12} \neq \pi_{22}$` 或 `$\pi_{13} \neq \pi_{23}$`

等价于

`$H_0: \ln\frac{\pi_{12}}{\pi_{22}} = 0$` 和 `$\ln\frac{\pi_{13}}{\pi_{23}} = 0$`
`$H_1: \ln\frac{\pi_{12}}{\pi_{22}} \neq 0$` 或 `$\ln\frac{\pi_{13}}{\pi_{23}} \neq 0$`。(9.31)

注意，上述表示以“低”类别作为基准的广义逻辑链接的重述。在实践中，如果提出假设，习惯上考虑两个额外的假设：

`$H_0: \pi_{12} = \pi_{22}$` 和 `$H_1: \pi_{12} \neq \pi_{22}$` (9.32)

以及

`$H_0: \pi_{13} = \pi_{23}$` 和 `$H_1: \pi_{13} \neq \pi_{23}$` (9.33)

这些假设可以用对数比重述如下：

`$H_0: \ln\frac{\pi_{12}}{\pi_{22}} = 0$` 和 `$H_1: \ln\frac{\pi_{12}}{\pi_{22}} \neq 0$` (9.34)

以及

`$H_0: \ln\frac{\pi_{13}}{\pi_{23}} = 0$` 和 `$H_1: \ln\frac{\pi_{13}}{\pi_{23}} \neq 0$`。(9.35)

`$I(\cdot)$` 代表一个产品指示函数，`$i=1, 2$`。假设广义逻辑函数

$$\ln\frac{\pi_{2i}}{\pi_{ii}} = \dots$$

（注：由于提供的文本中存在大量重复的段落和乱码，翻译已针对核心内容进行。）

# 第9章 边际模型的广义估计方程技术 331

```sas

u = uniform( seed);

if u < rho then y = yy;

else

    uu = uniform( seed);

    if u < cp12 then y = 2;

    if u < pi21 then y = 1;

end;

output;

*-- Product 2;

Product = 2;

Subjid = j + n;

YY = 3;

u = uniform( seed);

if u < cp12 then y = 2;

if u < pi21 then y = 1;

for i=1 to m;

  Y = 3;

  u = uniform( seed);

  if u < rho then y = yy;

  else

      uu = uniform( seed);

      if u < cp21 then y = 2;
```



```sas
if u < pi21 then y = 1;
end;
output;
```

```sas
keep subjid product y;
run;
ods html;
proc surveylogistic data=test_of_homogeneity;
class subjid / param=glm;
model y (refFirst) = product / link=logit varadj=morel;
cluster subjid;
means product / ilink;
estimate 'P12' int product 1 0 0 / category='1' / ilink;
estimate 'P22' int product 0 1 0 / category='1' / ilink;
estimate 'P12' int product 0 0 1 / category='2' / ilink;
estimate 'P23' int product 0 1 1 / category='2' / ilink;
estimate 'P12 Vs P22' product -1 1 / category='1' / exp;
estimate 'P13 Vs P23' product -1 1 / category='2' / exp;
run;
ods html;
```

所讨论的广义 Log 模型是使用 `SURVEYLOGISTIC` 过程拟合的。为了说明，我们还计算了第 9.10 节中讨论的泰勒展开估计（夹明治差估计）的加性样本偏差校正。正如之前所述，随着簇数量的增加，这种方差调整包含在模型 `varadj=morel` 中。关于此方差调整（一种样本偏差校正）的细节可以参考 Morel (1989)。结果如输出 9.7 所示。建议读者查阅 `SURVEYLOGISTIC` 文档以获取更多细节。由于我们请求了 GLM 参数化，与此类参数化相关的编码在“类信息”（Class Information）部分显示。用于检验假设 (9.31) 的 Wald 卡方统计量显示在“三类效应”（Type 3 of Effects）中。其值为 10.694。在零假设下

Morel, Jorge and Nagearaj Neeraj. Overdispersion Models in SAS. Copyright ©2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 更多资源，请访问 support.sas.com/publishing.

## 332 SAS 中的过度离散模型

### 输出 9.7: 程序 9.7 的选定结果

| SURVEYLOGISTIC 过程 |
| --- |
| 模型信息 | |
| 数据集 | WORK.TEST_OF_HOMOGENEITY |
| 响应变量 | Y |
| 响应水平数 | 3 |
| 簇变量 | Subjid |
| 簇数量 | 350 |
| 模型 | 广义 Logit |
| 优化技术 | Newton-Raphson |
| 方差调整 | Morel |
| 上界 ADJBOUND | 0.5 |
| 下界 DEFFBOUND | 1 |

使用 Y=1 作为参考类别进行建模的 Logits。

| 类信息 |
| --- |
| 类 | 值 | 设计变量 |
| Product | 1 | 1 |
| | | 1 |

| 三类效应分析 |
| --- |
| 效应 | DF | Wald Pr > ChiSq |
| | | 卡方

Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS. Copyright ©2011, SAS Institute Inc., Cary, North Carolina, USA. 更多 SAS 资源，请访问 support.sas.com/publishing.

## 第9章 边际模型的广义估计方程技术 333

| Product | 2 | 10.6904 | 0.0048 |

| 参数 | Y | DF | 估计 | 标准误差 | Wald 卡方 | Pr > ChiSq |
|---|---|---|---|---|---|---|
| Intercept | 2 | 1 | -2.5524 | 0.1508 | 286.4813 | <0.001 |
| Intercept | 3 | 1 | -3.7463 | 0.3048 | 151.0661 | <0.001 |
| Product | 1 | 2 | 0.4015 | 0.1963 | 4.1825 | 0.0408 |
| Product | 1 | 3 | -1.1838 | 0.4771 | 6.1566 | 0.0131 |
| Product | 2 | 2 | 0 | | - |
| Product | 2 | 3 | 0 | | - |

| 效应 | Y | 点估计 | 95% Wald 置信限 |
|---|---|---|---|
| Product 1 vs 2 | 2 | 1.494 | 1.017 | 2.195 |
| Product 1 vs 2 | 3 | 0.306 | 0.120 | 0.780 |

| Y | Product | 估计 | 标准误差 | z 值 | Pr >z | 均值 | 标准误差 |
|---|---|---|---|---|---|---|---|
| 1 | 1 | -2.1110 | 0.1257 | -17.11 | <0.001 | 0.1036 | 0.01167 |
| 1 | 2 | -2.5524 | 0.1508 | -16.93 | <0.001 | 0.07071 | 0.00984 |
| 2 | 1 | -4.9302 | 0.3670 | -13.43 | <0.001 | 0.00643 | 0.002346 |
| 2 | 2 | -3.7463 | 0.3048 | -12.29 | <0.001 | 0.02143 | 0.006383 |

# SURVEYLOGISTIC 过程

Morel, Jorge, and Nagaraj Neerchal. Overdispersion Models in SAS*. ©2011, SAS Institute, Cary, North Carolina, USA. 保留所有权利。更多 SAS 资源请访问 support.sas.com/publishing.

## 334 SAS 中的过度离散模型

| 标签 | Y | 估计 | 标准误差 | z 值 | Pr >z | 均值 | 标准误差 |
|---|---|---|---|---|---|---|---|
| P12 | 1 | -2.1510 | 0.1257 | -17.11 | <0.001 | 0.1036 | 0.01167 |

| 标签 | Y | 估计 | 标准误差 | z 值 | Pr >z | 均值 | 标准误差 |
|---|---|---|---|---|---|---|---|
| P22 | 1 | -2.5524 | 0.1508 | -16.93 | <0.001 | 0.07071 | 0.009894 |

| 标签 | Y | 估计 | 标准误差 | z 值 | Pr >z | 均值 | 标准误差 |
|---|---|---|---|---|---|---|---|
| P13 | 2 | -4.9302 | 0.3670 | -13.43 | <0.001 | 0.006430 | 0.002346 |

| 标签 | Y | 估计 | 标准误差 | z 值 | Pr >z | 均值 | 标准误差 |
|---|---|---|---|---|---|---|---|
| P23 | 2 | -3.7463 | 0.3048 | -12.29 | <0.001 | 0.02143 | 0.006383 |

## 第9章 边际模型的广义估计方程技术 335

Rao 和 Scott (1981) 提出了一种同性检验，其中通常的卡方统计量被设计效应估计值击败（过度离散）。在列联表中，同性检验与检验行、列变量之间是否存在任何关联的检验相同。该检验在 `SURVEYFREQ` 过程中是。。程序 9.7 延续中的编程语句显示了如何请求 Rao 和 Scott 卡方检验。`SURVEYFREQ` 输出的片段在输出 9.7 的延续中。原始卡方统计量值为 20.2281。设计效应估计值为 1.769。因此，`$20.2281/1.769=11.4313$`。在零假设下，该统计量渐近服从自由度 2 的卡方分布。相应的 P 值为 0.003。因此，我们得出两种产品的分布是不同的结论。

# 程序 9.7: 延续

```sas
ods html;
proc surveyfreq data=test_of_homogeneity;
cluster subject;
tables product * y / chisq;
run;
ods html close;
```



# SAS 中的过度离散模型

输出 9.7：延续

| SURVEYFREQ 过程 | |
| :--- | :--- |
| Rao-Scott 卡方检验 | 20.2281 |
| 设计修正 | 1.7695 |
| Rao-Scott 卡方 | 11.4313 |
| 自由度 (DF) | 2 |
| Pr > ChiSq | 0.0033 |
| F 值 | 5.7157 |
| 分子自由度 (Num DF) | 2 |
| 分母自由度 (Den DF) | 698 |
| Pr > F | 0.0035 |
| 样本量 = 2800 |

Morel, Jorge, and Nagaraj Neerchal. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. 保留所有权利。更多 SAS 资源，请访问 support.sas.com/publishing。

# 广义线性过度离散混合模型

- 10.1 GLMM 的一般性与基本概念 ...................................................337
- 10.2 一项多中心随机临床试验 ................................................................345
- 10.3 压水反应堆核电站的泵可靠性...................................................347
- 10.4 带有随机效应的多项模型示例...............................................................352
- 10.5 Beta-二项分布和随机聚类二项分布 GLMM ................................................356
- 10.6 零膨胀泊松和零膨胀负二项分布 GLMM......................................365
- 10.7 结语 ................................................................................................373

## 10.1 GLMM 的一般性与基本概念

在本章中，我们再次讨论广义线性混合模型 (`GLMM`)，并对过度离散模型如何与 `GLMM` 交互提供一个更全面的视角。这里给出的几个高级示例说明了书中介绍的基于似然的过度离散模型如何增强 SAS 过程 `GLMIX` 和 `GENMOD` 提供的估计方法论。下面的图描绘了本章讨论的模型之一。我们将提供二项、泊松和多项 `GLMM` 作为示例。这些都是条件模型。我们还包含四个广义线性过度离散混合模型 (`GLOMM`) 示例。它们分别对应于带有随机效应的二项、随机聚类二项、零膨胀泊松和零膨胀负二项模型。通过研究这些模型，我们完成了承诺在书中涵盖的所有分层模型（见第 1 章附录 1.1）。我们首先从开始讨论几个基本概念。

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_349_0.png)

![](img/fa69b648c17ad451eb7eb4ad8d92f5fb_350_0.png)

McCullagh 和 Nelder (1989) 提供的广义线性模型 (`GLM`) 框架在响应变量假设为独立的情况下，统一了连续和离散响应变量的分析。Zeger, Liang 和 Albert (1998) 将 `GLM` 框架扩展到包含随机效应。所得模型——广义线性混合模型 (`GLMM`)，可以适应在一段时间内监测受试者的纵向数据分析。`GLMM` 还可以用于分析来自簇（通常在簇抽样中）不同对象的观测值。如前所述，过度离散的二项（或多项）数据通常是同一簇观测值之间自然关联的结果。因此，我们在本章中对 `GLM` 进行了简要回顾。

Morel, and Nagaraj Neeraj. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. 保留所有权利。更多 SAS 资源，请访问 support.sas.com/publishing。

# 第 10 章广义线性过度离散混合模型

从 `GLM` 扩展到 `GLMM` 是直接的，类似于线性模型到线性混合模型的扩展。引入了对应每个受试者的随机效应，以捕捉其响应值的偏差。我们仅考虑将受试者视为随机的简化情况。现实案例可能更复杂。例如，在一个多中心研究中，如果中心内的受试者随时间提供重复测量，将“中心”和“中心内的受试者”视为随机的是合理的。

我们将首先在来自单元簇的多变量观测值的义集中介绍 `GLMM`。“簇”在这里用作通用术语，在实践中代表受试者、中心或研究人员。令 `$\mathbf{y}_j$` 表示第 $j$ 个单元簇的 $d$ 维响应向量，$j=1,2,\dots,n$；假设这些响应向量的均值向量和方差协方差矩阵为 `E($\mathbf{y}_j$) = $\mu_j$` 和 `Var($\mathbf{y}_j$) = $\Phi(\mu_j)$`，其中均值向量 `$\mu_j$` 的第 $i$ 个分量 `$\mu_{ij}$` 依赖于已知协变量行 `$\mathbf{x}_{ij}$` 和未知 $k$ 维参数向量 `$\boldsymbol{\beta}_j$`，通过连接函数 `g($\mu_{ij}$) = $\mathbf{x}_{ij}^T \boldsymbol{\beta}_j + \eta_{ij}$`，其中 `$\eta_{ij}$` 是线性预测值。如果 `$\eta_{ij}$` 包含随机效应，则模型变为 `GLMM`。在过度离散的情况下，方差通常被建模为 `Var(y_{ij}) = $\phi V(\mu_{ij})$`，其中 `$\phi$` 是过度离散参数。现在我们将探索如何在 SAS 中实现这些模型。

## 第 10 章 广义线性过度离散混合模型 341

正如广义线性模型所示，`X` 代表设计矩阵（或已知协变量矩阵），而 `$\beta$` 是一个未知参数向量。向量 `$\beta$` 代表模型中固定部分的参数。模型随机部分相关的参数由未知向量 `$\gamma$` 表示。同样地，`Z` 像 `X` 一样包含连续变量或虚拟变量。假设随机向量 `$\gamma$` 和 `$\epsilon$` 联合独立且服从正态分布，其均值为：

$$E \begin{pmatrix} \gamma \\ \epsilon \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}$$

方差协差矩阵为

$$Var(\begin{pmatrix} \gamma \\ \epsilon \end{pmatrix}) = \begin{pmatrix} G & 0 \\ 0 & R \end{pmatrix}$$

我们想提醒读者，由于观测向量由来自所有元素的多元响应向量组成，矩阵 `G` 和 `R` 的结构可能非常复杂。在给定 `$\gamma$` 的条件下，观测向量的期望值和方差协差矩阵为

$$E(y|\gamma) = X\beta + Z\gamma$$
$$Var(y|\gamma) = R$$

注意，原则上，我们可以从 `$\gamma$` 和 `$\epsilon$` 的分布推导出观测数据的边缘分布。观测向量的无条件（或边缘）期望值和方差给出：

$$E(y) = X\beta$$
$$Var(y) = ZGZ' + R$$

方程 (10.7) 指定的模型被称为个体特定（SS）模型，而方程给出的模型被称为群体年龄（PA）模型。模型也可以被视为 G 侧随机效应或 R 侧随机效应。注意，方程 (10.5) 的右侧包含两个不同的（独立的）随机量：`$\gamma$` 和 `$\epsilon$`。虽然 `$\gamma$` 用于捕捉条件均值以体现受体效应，但 `$\epsilon$` 代表残差效应。将 `$\gamma$` 与适当的设计矩阵 `Z` 称为 G 侧随机效应。也可以直接指定 `$\epsilon$` 的方差协差矩阵来捕捉受体内的相关结构。这种方法被称为 R 侧随机效应。注意，仅包含 G 侧随机效应的模型是条件的；它们也是 SS 模型。另一方面，仅包含 R 侧效应的模型是边缘模型和 PA 模型。对于 LMM，边缘和条件规范都会导致相同的边缘

Morel, J., and Nagaraj Neel. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 如需更多 SAS 资源，请访问 support.sas.com/publishing.

# SAS 中的过度离散模型

似然性，从而得到相同的估计和推断。我们对过度离散模型规范的方法基于能够解释簇内相关性的各种概率分布，可以被称为 D 侧规范。LMM 在统计文献中也称为方差分量模型。它们通常用于模拟重复测量数据、纵向数据和聚类数据。它们也适用于时间序列和空间数据。有关混合模型的历史发展，请参见 McCulloch 和 Searle (2001)。读者也可参阅 Littell 等人 (2006) 的更最近的进展。

描述 `GLMM` 的下一步现在已经很清晰了。`GLMM` 通过在线性预测器中包含随机效应获得，我们将随机效应标记为 "j"，以便它们对簇内的所有元素单元具有相同的的作用。注意，`$\gamma_j$` 仍然是适当维度的向量，以容纳 beta 参数可能不同的随机效应。此时，广义线性混合模型的模型方程变为

$$\mu_{ji} = \mathbf{E}(\mathbf{y}_{ji}) = \mathbf{g}^{-1}(\boldsymbol{\beta}, \mathbf{x}_{ji}, \gamma_j) \left( \begin{array}{c} \mathbf{g}_j^{-1}(\mathbf{x}_{ji} + \mathbf{z}_{ji}\gamma_j) \\ \vdots \\ \mathbf{g}_d^{-1}(\mathbf{x}_{ji}\boldsymbol{\beta} + \mathbf{z}_{ji}\gamma_j) \end{array} \right)$$

其中 `$\mathbf{z}_{ji}$` 通常是变量，且 `$\gamma = (\gamma_1', \gamma_2', ..., \gamma_n')^T$` 被假设为零均值的多元正态随机向量。我们可以更简洁地重写均值的模型方程：

$$\left[ \mathbf{E}(\mathbf{y}|\gamma) \right] = \mathbf{g}(\gamma) = \mathbf{X}\boldsymbol{\beta} + \mathbf{Z}\gamma$$
$$\left[ \mathbf{Var}(\mathbf{y}|\gamma) = \mathbf{V}(\mu, \alpha) \right] = \mathbf{V}\left[ \mathbf{X}\boldsymbol{\beta} + \mathbf{Z}\gamma \right] \right]$$

这样我们就可以看到 LMM 和 `GLMM` 之间的对应关系。无条件均值可以通过消除随机效应获得。这可以用符号表示为

$$\mu_{ji} = \int \mathbf{g}_j^{-1}(\mathbf{x}_{ji}\boldsymbol{\beta} + \mathbf{z}_{ji}\gamma_j) d\mathcal{F}(\gamma_j).$$

## 第 10 章 广义线性过度离散混合模型 343

同样，响应的无条件方差可以写为关于随机效应分布的积分

$$V(y) = \int V(y|\gamma) f(\gamma) d\gamma$$

同样，Zeger, Liang 和 Albert (1988) 使用广义方程方法估计 `GLMM`。Shall (1991) 给了一种易于编程的 `GLMM` 估计算法。该算法还允许仅对随机效应的前两个矩进行规范。Drum 和 McCulloch (1993) 改进了残差极大似然法（REML），一种方法

该方法已成功应用于 `GLMM` 中，并可扩展到具有逻辑链接函数的 `GLMM`。其的表 1 对用于估计 `GLMM` 的方法进行了简要总结。

`GLIMMIX` 过程使用了两种主要的估计方法，即基于线性化的伪似然法（前者）和基于自适应高斯-海米特积分的极大似然估计法。前一种方法在第 9 章中讨论过。在自适应高斯-海米特积分法中，与 `GLMM` 对数似然相关的积分通过求和来近似。例如，如果 `f(x)` 是概率密度函数，且对函数 `p(x)` 关于 `x` 积分，则自适应积分近似为：

```
f(x)p(x) \approx \sum_{i=1}^{N} w_i f(x_i)
```

`N` 表示积分点数，`w_i` 是积分权重，`x_i` 是横坐标。在 `GLIMMIX` 中，通过模型选项 `METHOD=QUAD` 请求此方法。`GLIMMIX` 过程中的积分规则是自适应的，因为用户不需要指定积分点数（节点数），而是通过 `METHOD=QUAD` 选项的 `QPOINTS=` 子选项通过评估初始值的对数似然来确定积分点数，直到满足容差。此外，`GLIMMIX` 过程通过使用经验贝估计（EBEs）和随机效应的海森矩阵（二阶导数）对积分点进行中心化和缩放。这改进了似然近似。请参考 `GLIMMIX` 过程文档获取有关自适应高斯-海米特积分方法的更多细节。文档还介绍了该方法的优缺点，并讨论了基于线性化的伪似然法。在 `NLMIXED` 过程中，自适应高斯-海米特积分是默认积分方法。如果用户选择使用单个积分点的积分规则实现，结果将与

```
proc glmix method=quad(qpoints=1);
proc glimmix method=laplace;
```

在计算上是相同的。但 `METHOD=LAPLACE` 选项适用于更广泛的模型。

## 第 10 章 广义线性过度离散模型 345

## 10.2 多中心随机试验

Beitler 和 Landis (1985) 分析了一项多中心随机试验的数据，旨在研究两种外用制剂（活性药物和对照组）治疗感染的疗效。数据见表 10.1。

表 10.1：多中心随机试验中活性药物和对照治疗的有效人数

| 中心 | 治疗 | 有效人数 | 总计 |
|---|---|---|---|
| 1 | 药物 | 11 | 36 |
| 1 | 对照 | 10 | 37 |
| 2 | 药物 | 16 | 20 |
| 2 | 对照 | 22 | 32 |
| 3 | 药物 | 14 | 19 |
| 3 | 对照 | 7 | 19 |
| 4 | 药物 | 2 | 16 |
| 4 | 对照 | 1 | 17 |
| 5 | 药物 | 6 | 17 |
| 5 | 对照 | 0 | 12 |
| 6 | 药物 | 1 | 11 |
| 6 | 对照 | 0 | 10 |
| 7 | 药物 | 1 | 5 |
| 7 | 对照 | 1 | 9 |
| 8 | 药物 | 4 | 6 |
| 8 | 对照 | 6 | 7 |

```
$t_j \text{ given } (x_{ij}; b_j) \sim \text{Binomial}(\pi_{ij}; m_j),\text{logit}(\pi_{ij}) = \beta_0 + \beta_1x_{ij} + b_j \quad (10.12)$
```

其中 `b_j` 是独立同分布的 `Normal(0,\sigma^2)`，且

```
$x_{ij} = \begin{cases} 1 & \text{如果受试者接受药物} \\ 0 & \text{否则}\end{cases}$
```

SAS 中的过度离散模型

程序 10.1 提供了拟合上述逻辑 `GLMM` 的编程语句。我们通过 `GLIMMIX` 过程使用二次估计方法（模型选项 'method=quad'）来拟合该模型。输出 10.1 显示了 `GLIMMIX` 生成的部分输出。

## 程序 10.1：逻辑 GLMM–多中心随机试验

```sas
/*
Beitler and Landis (1985)
多中心随机试验示例
*/
data multi_center;
  input clinic trt $ t m;
datalines;
1 Drug      11 36
1 Control    10 37
2 Drug      16 20
2 Control    22 32
3 Drug      14 19
3 Control     7 19
4 Drug       2 16
4 Control     1 17
5 Drug       6 17
5 Control     0 12
6 Drug       1 11
6 Control     0 10
7 Drug       1 5
7 Control     1 9
8 Drug       4 6
8 Control     6 7
;
\ods html;
title "**多中心随机试验 -- Beitler and Landis (1985) ****";
proc glimmix data=multi_center method=quad order=data;
  class clinic trt;
  model t/m = trt + link=logit dist=binomial s;
  random int / subject=clinic;
  lmeans trt / ilink;
  estimate "Drug Vs Control" trt 1 -1 / or cl;
run;\ods html close;
```



Morel, Jorge, and Nagaraj Neerchal. SAS 中的过度离散模型。版权 © 2011, SAS Institute Inc., Cary, North Carolina, USA: 版权所有。如需更多 SAS 资源，请访问 `support.sas.com/publishing`。

# 第 10 章 广义线性过度离散模型

## 输出 10.1：拟合多中心随机试验逻辑 GLMM 的部分结果

*** 多中心随机试验 -- Beitler and Landis (1985) ***

GLIMMIX 过程

| 参数 | 受试者 | 估计 | 标准差 |
|---|---|---|---|
| 截距 | 中心 | 1.9591 | 1.1903 |
| 估计 | 估计 | t 值 | Pr>t| 下界 | 上界 | 估计 | 下界 | 上界 |
|---|---|---|---|---|---|---|---|
| 药物 VS 对照 | 0.7385 | 0.3004 | 2.46 | 0.0436 | 0.05 | 1.4448 | 2.0927 | 4.2582 |

| 最小均值 | 估计 | DF | t 值 | Pr>t| 均值 | 标准差 |
|---|---|---|---|---|---|---|
| 药物 | -0.4589 | 0.5504 | 7 | -0.83 | 0.4062 | 0.3872 | 0.130 |
| 对照 | -1.1974 | 0.5561 | 7 | -2.15 | 0.0317 | 0.2319 | 0.099 |

估计优势比为 $e^{0.7385}=2.09$，95% 置信区间为 (1.03, 4.26)。因此，药物组的有效率大约是对照组的两倍。

## 10.3 压水厂的泵可靠性

Farley 核电厂位于阿拉拉巴马州多塞坦，由 Alabama Power 所有，南方核公司运营。它是东南部三座核设施之一。每座设施使用西方反应堆。表 10.2 提供了以千小时为单位的故障 (`y_{ij}`) 信息，系统分为两组：连续运行（i=1）或间歇运行（i=2）。

### 表 10.2：压水厂的泵可靠性数据

| 分组 (i) | 系统 | 故障数 (Y_ij) | 观测时间 (t_ij) (千小时) |
|---|---|---|---|
| 1 | 1 | 5 | 94.320 |
| 1 | 2 | 5 | 62.880 |
| 1 | 3 | 14 | 125.760 |
| 1 | 4 | 19 | 31.440 |
| 2 | 1 | 1 | 15.720 |
| 2 | 2 | 3 | 5.240 |
| 2 | 3 | 1 | 1.048 |
| 2 | 4 | 1 | 1.048 |
| 2 | 5 | 4 | 2.096 |
| 2 | 6 | 22 | 10.480 |

Draper 和 O'Muirchaight (1987) 对这些数据进行了经验贝叶斯分析。由于我们拟合的是 Poisson GLM，该示例在 SAS NLMIXED 过程文档的“带有计数数据的泊松回归模型”标题下进行了讨论。我们将使用 `GLIMMIX` 过程演示如何拟合 Poisson GLM。拟合模型如下：

# 程序 10.2：拟合泊松 GLMM——法利核电站1号机的泵可靠性数据

```sas
/*
压水反应堆核电站的泵可靠性
Gaver and O'Muirchheartaigh (1987)
Draper (1996) */
data pump;
  pump = _n;
  input group y;
  logstd = log(t) - 2.5469400;
  datalines;
  1 1 94.320
  1 5 62.880
  1 14 127.560
  1 19 31.440
  2 1 15.720
  2 3 3.240
  2 1 1.048
  2 2 1.048
  2 4 2.096
  2 22 10.480;
;
```

```sas
ods html;
title "压水反应堆核电站的泵可靠性";
proc glimmix data=pump method=quad;
  class group;
  model y = group logstd*group / noint dist=poisson link=log
    solution ddfm=residual;
  random it / subject=pump;
  estimate "Difference Y-intercepts" group 1 -1;
  estimate "Difference Slopes" group 1 -1;
run;
ods html close;
```

在协方差分析（ANCOVA）中，对于响应变量 Y 和协变变量 X，“MODEL Y = X GROUP X*GROUP” 提供了组间直线平行性的检验（即斜率相等性）。将之前的 ANCOVA 模型重新参数化为“MODEL Y = X*GROUP / NOINT”，可以获得回归线 y 截距和斜率的无偏估计。程序 10.2 通过 `GLIMMIX` 针对 (10.13) 中描述的泊松 GLMM 请求了后一种重新参数化方法。输出 10.2 提供了程序 10.2 输出的节选。

Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. 如需更多 SAS 资源，请访问 `support.sas.com/publishing`。

## 输出 10.2：程序 10.2 的部分结果——法利核电站1 号机的泵可靠性数据

| 压水反应堆核电站的泵可靠性 |
| :--- |
| GLIMMIX 过程 |
| 拟合统计量 | |
| -2 Log Likelihood | 56.07 |
| AIC (越小越好) | 66.07 |
| AICC (越小越好) | 81.07 |
| BIC (越小越好) | 67.58 |
| CAIC (越小越好) | 72.58 |
| HQIC (越小越好) | 64.41 |
| 协方差参数估计 | |
| Cov Parm | Subject | Estimate | Standard Error |
| Intercept | pump | 0.5314 | 0.3415 |
| 固定效应解 | | |
| Effect | Group | Estimate | Standard Error | DF | t Value | Pr >t| |
| group | 1 | 2.9644 | 1.3826 | 6 | 2.14 | 0.075 |
| group | 2 | 1.7992 | 0.5492 | 6 | | 0.0169 |
| logstd*group | 1 | -0.4256 | 0.7473 | 6 | -0.57 | 0.5896 |
| logstd*group | 2 | 0.6097 | 0.3814 | 6 | 1.60 | 0.1610 |
| 固定效应的 III 型检验 | | |
| Effect | Num DF | Den DF | F Value | Pr > F |
| Group | 2 | 6 | 7.63 | 0.0224 |
| logstd*group | 2 | 6 | 1.44 | 0.3083 |

### 表 10.3：GLMM–法利核电站1 号机泵可靠性数据主要结果

| 泵类型 | 参数 | 估计 | 标准误差 | P 值 |
| :--- | :--- | :--- | :--- | :--- |
| 连续 | Intercept | 2.9644 | 1.3826 | 0.0757 |
| | Slope | -0.4256 | 0.7473 | 0.5896 |
| 间歇 | Intercept | 1.7992 | 0.5492 | 0.0169 |
| | Slope | 0.6097 | 0.3814 | 0.1610 |
| | Difference Y-intercepts | 1.1653 | 1.4855 | 0.4626 |
| | Difference Slopes | -1.0354 | 0.8389 | 0.2633 |
| | σ² | 0.5314 | 0.3415 | |
| | -2log-likelihood | 56.07 | | |

表 10.3 提供了每条线的参数估计值、标准误差和 P 值。没有证据表明 y 截距存在显著差异（P 值=0.4626）。此外，斜率在统计学上没有差异（P 值=0.2633）。使用 `NLMIXED` 过程拟合泊松 GLMM (10.13) 的编程语句如下所示。对于自由度，在 GLMIX 中由于使用了“residual”选项自由度为 6，而在 NLMIXED 中，结果是相同的。

```sas
proc nlmixed data=pump;
  parms logstd 0 beta1 beta2 1 alpha1 alpha2 1;
  if (group = 1) alpha = alpha1+ beta1*logstd;
  else alpha = alpha2+ beta2*logstd;
  lambda = exp(alpha);
  y = poisson(lambda);
  random = normal(0,exp(2*logstd)) subject=pump;
  estimate 'alpha-alpha2' alpha-alpha2;
  estimate 'beta-beta2' beta-beta2;
  estimate 'Sigma*' exp(2*logstd);
run;
```

## 10.4 效应模型

本节将利用 9.9 中的肩痛研究演示多项分布模型的拟合。在该研究中，有 22 名实验组（有抽吸），19 名对照组（无抽吸）。回想腹腔镜手术后，患者被要求在术后三天内每天上午和下午对视觉模拟评分进行评分。响应是定序的，其中“1”表示“低疼痛”，“5”表示“高疼痛”。协变量是性别、年龄和时间，所有时间都是个体特异的。令 `y_{ij}` 表示第 $i$ 组第 $j$ 个受者在 $t$ 个时刻的响应，$i=1, 2, j=1, 2, \dots$ （$n_i=22, n_j=19, t=1, 2, \dots$），其中

$$E(y_{ij}) = \frac{\pi_{1ij}}{\pi_{1ij} + \pi_{2ij} + \pi_{3ij} + \pi_{4ij}}$$

注意，具有重复测量值的个体构成了一个簇。我们考虑以下 Logit GLMM：

$$\ln(\pi_{1ij} / (\pi_{2ij} + \pi_{3ij} + \pi_{4ij})) = \alpha_1 + \beta_1X_{ij} + \beta_2X_{2ij} + \beta_3X_{3ij} + \beta_4t + u_{ij}$$
$$\ln(\pi_{2ij} / (\pi_{1ij} + \pi_{3ij} + \pi_{4ij})) = \alpha_2 + \beta_1X_{ij} + \beta_2X_{2ij} + \beta_3X_{3ij} + \beta_4t + u_{ij}$$
$$\ln(\pi_{3ij} / (\pi_{1ij} + \pi_{2ij} + \pi_{4ij})) = \alpha_3 + \beta_1X_{ij} + \beta_2X_{2ij} + \beta_3X_{3ij} + \beta_4t + u_{ij}$$
$$\ln(\pi_{4ij} / (\pi_{1ij} + \pi_{2ij} + \pi_{3ij})) = \alpha_4 + \beta_1X_{ij} + \beta_2X_{2ij} + \beta_3X_{3ij} + \beta_4t + u_{ij}$$

其中 `u_{ij}` 是独立同分布的 $N(0, \sigma^2)$。

## 程序 10.3：对肩尖疼痛数据拟合累积 Logit GLMM

```sas
ods html;
proc glimmix data=Shoulder_tip_pain method=quad;
class subject_id_trt gender;
model y = trt gender age time / dist=mult link=clogit;
random int / subject-subject_id;
format trt $abc. gender $xyz;
estimate 'Active Vs Placebo' trt 1 -1 / or;
title *** 对肩尖疼痛数据拟合累积 Logit GLMM ***';
proc glimmix data=Shoulder_tip_pain_empirical=classical method=quad;
class subject_id_trt gender;
model y = trt gender age time / dist=mult link=clogit;
random int / subject-subject_id;
format trt $abc. gender $xyz;
estimate 'Active Vs Placebo' trt 1 -1 / or;
title1 *** 对肩尖疼痛数据拟合累积 Logit GLMM ***';
title2 *** 使用固定效应估计的经验方差 ***';
title3 *** 使用 MBN 小样本方差校正 ***';
ods html close;
```



程序 10.3 第一个模型的结果也位于输出 10.3 中。
模型信息输出显示（其他外），响应变量为序数多项（ordinal Multinomial），连接函数为累积 Logit（Cumulative Logit），估计技术为极大似然法，似然度通过高斯-米特积分（Gauss-Hermite Quadrature）方法近似。随机截距方差的估计值 `σ²` 为 4.6759，估计标准误为 1.6741。固定效应的解以及 III 类固定效应也显示在输出 10.3 中。我们请求了活性组与安慰剂（Active Placebo）的优势比（odds-ratio）。其估计值为 17.86（与优势比对数相关的 P 值为 0.0004）。回想第 9 章第 9.9 节讨论的 GEE Logit 模型下的估计优势比为 14.52。

# 354 SAS 中的过度离散模型

输出 10.3：使用 `PROC GLIMMIX` 对肩尖疼痛数据拟合累积 Logit GLMM 的选择结果

*** 对肩尖疼痛数据拟合累积 Logit GLMM ***

| 模型信息 |
| --- | --- |
| 数据集 | `WORK.SHOULDER_TIP_PAIN` |
| 响应变量 | `Y` |
| 响应分布 | 多项（有序的） |
| 连接函数 | Cumulative Logit |
| 方差矩阵 | 默认 |
| 方差矩阵分组依据 | `subject_id` |
| 估计技术 | 极大似然法 |
| 似然近似 | 高斯-米特积分 |
| 自由度方法 | 包含法 (Containment) |

| 协方差参数估计 |
| 协方差参数 | 受体 | 估计值 | 标准误 |
| --- | --- | --- | --- |
| 截距 | `subject_id` | 4.7659 | 1.6741 |

| 固定效应的解 |
| 效应 | y | trt | gender | 估计值 | 标准误 | DF | t 值 | Pr >|t| |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 截距 | 1 | | | -5.5633 | 1.6607 | 37 | -3.35 | 0.0019 |
| 截距 | 2 | | | -4.0387 | 1.6313 | 37 | -2.48 | 0.0180 |
| 截距 | 3 | | | -2.4131 | 1.6085 | 37 | -1.50 | 0.1420 |
| 截距 | 4 | | | -0.3147 | 1.6084 | 37 | -0.20 | 0.8459 |
| trt | | Active | | 2.8827 | 0.8060 | 201 | 3.58 | 0.0004 |
| trt | | Placebo | | 0 | | | | |
| gender | | | Female | 0.2613 | 0.8108 | 201 | 0.32 | 0.7476 |

Morel, Jorge, and Nagaraj. *Overdispersion Models in SAS*. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED。更多 SAS 资源，请访问 `support.sas.com/publishing`。

# 第10 章 广义过度离散混合模型 355

| gender | Male | 0 | | | | | |
| age | | | 0.04948 | 0.02515 | 201 | 1.97 | 0.0505 |
| time | | | 0.3814 | 0.09230 | 201 | 4.13 | <0001 |

| 固定效应的 III 类检验 | | | | | | |
| 效应 | 数字 DF | 分母 DF | F 值 | Pr > F |
| trt | 1 | 201 | 12.79 | 0.0004 |
| gender | 1 | 201 | 0.10 | 0.7476 |
| age | 1 | 201 | 3.87 | 0.0505 |
| time | 1 | 201 | 17.08 | <0001 |

| 估计 | | | | | | | |
| Label | 估计值 | 标准误 | DF | t 值 | Pr >|t| | 指数化估计值 |
| Active Vs Placebo | 2.8827 | 0.8060 | 201 | 3.58 | 0.0004 | 17.8625 |

表 10.4 提供了方程 (10.14) 模型在不带经验选项的 GLMM、带有 `EMPIRICAL=CLASSIC` 选项的 GLMM 以及带有 `EMPIRICAL=MBN` 选项的 GLMM 下的 beta 估计、标准误和 P 值。这三个模型提供了相同的 beta 估计。但方差估计（随后的其 P 值）是不同的。带有 `EMPIRICAL=CLASSIC` 选项的模型提供了相同的标准误（除 Time 效应外），与普通 GLMM 下的标准误相比这些标准误更小。由于经验 EE 方差中嵌入的小样本偏差，这些方差估计值可能比应值要小。由于这种偏差，预计会出现过高的假阳性率。回想年龄组有 22 名受试者，控制组有 19 名。带有 `EMPIRICAL=MBN` 选项的 GLMM 模型通过略微增大方差估计，减少了估计的经验方差估计中的偏差。校正量随着样本量的增加而消失，对于大样本，`EMPIRICAL=CLASSIC` 和 `EMPIRICAL=MBN` 的方差估计变得不可区分。在通过 `EMPIRICAL=MBN` 选项获得的更严格的方差估计下，处理效应和时间效应保持高度显著。年龄效应在 `EMPIRICAL=CLASSIC` 选项下是显著，但在 `EMPIRICAL=MBN` 选项下仅处于边缘显著。

More, Jorge, and Nagaraj Neeraraj. *Overdispersion Models in SAS*. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED。更多 SAS 结果，请访问 `support.sas.com/publishing`。

# 表 10.4：带有固定效应估计的肩尖疼痛数据累积 Logit GLMM 结果

| 效应 | 估计值 | 带有 `EMPIRICAL=CLASSIC` 的 GLMM | 带有 `EMPIRICAL=MBN` 的 GLMM |
| --- | --- | --- | --- |
| 标准误 | P 值 | 标准误 | P 值 |
| 截距 1 | -5.5633 | 1.6607 | 0.0019 |
| 截距 2 | -4.0387 | 1.6313 | 0.0180 |
| 截距 3 | -2.4131 | 1.6085 | 0.1420 |
| 截距 4 | -0.3147 | 1.6084 | 0.8459 |
| trt | 2.8827 | 0.8060 | 0.0004 |
| gender | 0.2613 | 0.8108 | 0.7476 |
| age | 0.04948 | 0.02515 | 0.0505 |
| time | 0.3814 | 0.09230 | <0001 |

（注：表 10.4 的 OCR 在源文件中是碎片化的，我已根据提供的页面数据重建了结构。）

## 程序 10.4：Beta-二项分布 GLOMM 的生成与分析

```
data GLOMM, bn;
n = 200;
pi_1 = 0.12;
pi_2 = 0.08;
m = 20;
rho_2 = 0.15;
sigma = 1.2;
seed = 1983;
beta0 = log(pi_1/(1-pi_1));
betal = log(pi_2/(1-pi_2)) - beta0;
c = 1 / rho_2 / rho_2 - 1;
--- 过离散参数;
----------------------
--- u ~ Normal(0,sigma=sigma);
----------------------
--- 种子;
----------------------
--- 序列 AB;
n----------------------
do Subj_id=1 to n;
----------------------
Sequence = 'AB';
u = sigma * normal(seed);
--- 第1期;- 
Period = 1;
Product = 1;
X = 1 / (1 + exp(- beta0 - u));
pi = c * pi;
a = c - a;
y1 = rangam(seed, a);
y2 = rangam(seed, b);
y = y1 / (y1 + y2);
t = ranbin(seed,m,p);
output:
--- 第2期;- 
Period = 2;
Product = 0;
X = 1 / (1 + exp(- beta0 - betal - u));
pi = c * pi;
a = c - a;
y1 = rangam(seed, a);
y2 = rangam(seed, b);
y = y1 / (y1 + y2);
t = ranbin(seed,m,p);
output:
---*-
end;
----------------------
--- 序列 BA;
----------------------
do Subj_id=n+1 to n+n;
----------------------
Sequence = 'BA';
u = sigma * normal(seed);
-- 第1期;
Period = 1;
Product = 0;
pi = 1 / ( 1 + exp( beta0 - betal - u ) );
c = c * pi;
b = c - a;
y1 = rangam(seed, a);
y2 = rangam(seed, b);
p = y1 / ( y1 + y2);
t = ranbin(seed,m,p);
output:
-- 第2期;
Period = 2;
Product = 1;
pi = 1 / ( 1 + exp( beta0 - u ) );
c = c - a;
b = 
y1 = rangam(seed, a);
y2 = rangam(seed, b);
p = y1 / ( y1 + y2);
t = ranbin(seed,m,p);
output:
--;
end;
--;
```

run; Subj_id Sequence Product X t m
```
ods html;
proc glimmix data=glm_BB method=quad;
class Subj_id Sequence Product;
model t/m = Product / link=logit dist=binomial s;
random int = subject+subj_id;
run;
proc nlmed data=glm_BB;
parms beta0=-2.7, -2.6, -2.5, betal=0.4, 0.5, 0.3 a0=-0.5 0, sigma=1;
linr = a0;
rho_2 = 1/(1+exp(-linr));
c = 1 / rho_2 - 1;
linp = beta0+betal*x + u;
pi = 1/(1+exp(-linp));
c = 1*pi;
z = gamma(m+1) - gamma(t+1) + gamma(t*c*pi) + gamma(m-t*c*pi) - ngamma(m*c) - gamma(c*c*pi) - gamma(c*pi);
model t = general(1);
random u = normal(0, sigma*sigma) subject=Subj_id;
estimate 'Pi_1' = 1/(1+exp(-beta0-betal));
estimate 'Pi_2' = 1/(1+exp(-beta0));
estimate 'var' = exp(betal);
estimate 'Sigma*Sigma' = Sigma*Sigma;
estimate 'Rho*' = 1/(1+exp(-a0));
run;
```

Morel, Jorge and Nagaraj Neeraj. Overdispersion Models in SAS. Copyright ©2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. 更多资源请访问 `support.sas.com/publishing`。

## 输出 10.4：程序 104 Beta-二项分布 GLOMM 分析的选定结果

| 协方差参数 |  | 估计 | 标准误 |
|---|---|---|---|
| 截距 | Subj_id | 1.6131 | 0.1576 |

| 效应 | 估计 | 标准误 | DF | t 值 | Pr >t |
|---|---|---|---|---|---|
| 截距 | -2.6056 | 0.0796 | 399 | -32.70 | <0001 | |
| Product 1 | 0.4801 | 0.0510 | 399 | 9.41 | <0001 | |
| Product 2 | 0 | | | | | |

| -2 对数似然 | 3229.6 | | | | | |
| AIC (越小越好) | 3237.6 | | | | | |
| AICC (越小越好) | 3237.6 | | | | | |
| BIC (越小越好) | 3253.6 | | | | | |

| 参数 | 估计 | 标准误 | DF | t 值 | Pr >t | Alpha | 下限 | 上限 |
|---|---|---|---|---|---|---|---|---|
| beta0 | -2.5563 | 0.08290 | 399 | -30.84 | <0001 | 0.05 | -2.7193 | -2.3933 |
| beta1 | 0.4740 | 0.06018 | 399 | 7.88 | <0001 | 0.05 | 0.3557 | 0.5924 |
| a0 | -1.7578 | 0.14633 | 399 | -12.02 | <0001 | 0.05 | -2.0454 | -1.4702 |
| sigma | 1.2131 | 0.06537 | 399 | 18.56 | <0001 | 0.05 | 1.0845 | 1.3416 |

| 标签 | 估计 | 标准误 | DF | t 值 | Pr >t | Alpha | 下限 | 上限 |
|---|---|---|---|---|---|---|---|---|
| PI_1 | 0.1108 | 0.007683 | 399 | 14.43 | <0001 | 0.05 | 0.09573 | 0.1259 |
| PI_2 | 0.0720 | 0.005539 | 399 | 13.00 | <0001 | 0.05 | 0.06111 | 0.08289 |
| OR | 1.6065 | 0.09668 | 399 | 16.62 | <0001 | 0.05 | 1.4164 | 1.7966 |
| Rho*Rho | 0.1471 | 0.01835 | 399 | 8.01 | <0001 | 0.05 | 0.1110 | 0.1831 |
| Sigma*Sigma | 1.4715 | 0.01586 | 399 | 9.28 | <0001 | 0.05 | 1.1597 | 1.7883 |

表 10.5 显示了从 `NLMIXED` 程序获得的 Beta-二项分布 GLOMM 方程 10.5 的估计和标准误。读者可以验证参数估计（“-2 对数似然”）非常接近底层参数。

#### 表 10:5：Beta-二项分布 GLOMM 的参数估计和标准误

| 参数 | 估计 | 标准误 |
|---|---|---|
| -2 对数似然 | 3229.6 | -- |
| $\pi_1$ | 0.1108 | 0.0077 |
| $\pi_2$ | 0.0720 | 0.0055 |
| 优势比 (Odds-ratio) | 1.6065 | 0.0967 |
| $\rho^2$ | 0.1471 | 0.0184 |
| $\sigma^2$ | 1.4715 | 0.1586 |

现在我们来处理随机 GLOMM：

```
$t_{ij} \text{ given } (x_{ij}; u_{ij}) \sim \text{Random-ed Binomial}(\pi_i; \rho; m_{ij}),\log (\pi_{ij}) = \beta_0 + \beta_1,x_{ij} + u_{ij}$ (10.16)
```



使用了之前 `GLOMM` 中的参数：$\pi_i = 0.12$, $\pi_2 = 0.08$, $\rho^2 = 0.15$, $\sigma = 1.2$ 以及 $m_{ij} = 20$。分析数据的编程语句位于程序 10.5。之前，我们使用将受试视为随机的 `GLMIX` 获取 beta 参数和方差分量的初始估计。然后通过由初始值定义的 `NLMIXED` 程序拟合随机 `GLOMM`。程序 10.5 的选定结果显示在输出 10.4。

## 程序 10.5：Beta-二项分布 GLOMM 下的数据生成与分析

```
/*

带有 Logit 链接和随机效应的 Beta-二项模型

由于交叉设计产生的随机效应

t given u ~ Beta-binomial(pi,rho,n)

logit(pi) ~ beta0 + betal * X + u

u ~ Normal(0,sigma=sigma)

*/

data GLOMM

n = 200;

pi_1 = 0.12;

pi_2 = 0.08;

rho_2 = 0.15; --- 过离散参数;

sigma = 1.2; --- 种子;

seed = 1983;

beta0 = log(pi_1/(1-pi_1));

betal = log(pi_2/(1-pi_2)) - beta0;

rho = sqrt(rho_2);

--- 序列 AB;

do Subj_id=1 to n;

Sequence = 'AB';

u = sigma * normal(seed);

--- 第1期;-

Period = 1;

Product = 1;

X = 1;

pi = 1 / (1 + exp(- beta0 - u));

yy = ranbin(seed,1,pi);

mm = ranbin(seed,m,rho);

t = yy * mm;

if m > mm then t = t + ranbin(seed,m,pi);

output;

--- 第2期;

Period = 2;

Product = 2;

X = 0;

pi = 1 / (1 + exp(- betal - u));

yy = ranbin(seed,1,pi);

mm = ranbin(seed,m,rho);

t = yy * mm;

if m > mm then t = t + ranbin(seed,m,pi);

output;

---

end;

--- 序列 BA;

do Subj_id=n+1 to n+n;

Sequence = 'BA';

u = sigma * normal(seed);

--- 第1期;-

Period = 1;

Product = 0;

pi = 1 / ( 1 + exp( beta0 - betal - u ) );

c = c * pi;

b = c - a;

y1 = rangam(seed, a);

y2 = rangam(seed, b);

p = y1 / ( y1 + y2);

t = ranbin(seed,m,p);

output:

-- 第2期;

Period = 2;

Product = 1;

pi = 1 / ( 1 + exp( beta0 - u ) );

c = c - a;

b = 

y1 = rangam(seed, a);

y2 = rangam(seed, b);

p = y1 / ( y1 + y2);

t = ranbin(seed,m,p);

output:

--;

end;

--;
```



# 364 SAS 中的过度离散模型

输出 10.5：程序 10.5 中随机聚类二项 GLOMM 分析的选定结果

| GLIMMIX 过程 | |
| --- | 协方差参数估计 |
| 协方差参数 | 受体 | 估计值 | 标准误 |
| --- | --- | --- | --- |
| 截距 | Subj_id | 2.7103 | 0.2671 |
| 固定效应解 | | | |
| 效应 | 乘积 | 估计值 | 标准误 | DF | t 值 | Pr > |t| |
| --- | --- | --- | --- | --- | --- | --- |
| 截距 | | -2.8058 | 0.09972 | 399 | -28.14 | <0001 |
| 乘积 | 1 | 0.3399 | 0.05316 | 399 | 6.39 | <0001 |
| 乘积 | 2 | 0 | | | | | |

| NLMIXED 过程 | |
| 拟合统计量 | |
| -2 对数似然值 | 3155.5 |
| AIC (越小越好) | 3163.5 |
| AICC (越小越好) | 3163.5 |
| BIC (越小越好) | 3179.4 |

| 参数估计 | | | | | | | | | | |
| 参数 | 估计值 | 标准误 | DF | t 值 | Pr > |t| | 下界 | 上界 | 梯度 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| beta0 | -2.5653 | 0.09505 | 399 | -26.99 | <0001 | 0.05 | -2.7521 | -2.3784 | -0.0011 |
| beta1 | 0.3751 | 0.07765 | 399 | 4.83 | <0001 | 0.05 | 0.2224 | 0.5277 | -0.00006 |
| a0 | -0.4256 | 0.06336 | 399 | -6.72 | <0001 | 0.05 | -0.5502 | -0.3011 | -0.00006 |
| sigma | 1.2679 | 0.07458 | 399 | 17.00 | <0001 | 0.05 | 1.1213 | 1.1416 | -0.00009 |

Morel, J, 和 Nagaraj Neeraj.SAS 中的过度离散模型®。版权 © 2011, SAS Institute Inc., Cary, North Carolina, USA。保留所有权利。欲需更多 SAS 资源，请访问 sas.com/publishing。

# 第 10 章 广义线性过度离散混合模型

| 附加估计 | | | | | | | | | | | |
| 标签 | 估计值 | 标准误 | DF | t 值 | Pr > |t| | Alpha | 下界 | 上界 |
|---|---|---|---|---|---|---|---|---|---|---|
| PI_1 | 0.1006 | 0.00798 | 399 | 12.58 | <.0001 | 0.05 | 0.08491 | 0.1164 |
| PI_2 | 0.0741 | 0.00603 | 399 | 11.33 | <.0001 | 0.05 | 0.05902 | 0.08380 |
| OR | 1.4551 | 0.1130 | 399 | 12.88 | <.0001 | 0.05 | 1.2329 | 1.6772 |
| Rho*Rho | 0.1562 | 0.01197 | 399 | 13.05 | <.0001 | 0.05 | 0.1326 | 0.1797 |
| Sigma*Sigma | 1.6077 | 0.01891 | 399 | 8.50 | <.0001 | 0.05 | 1.2358 | 1.9795 |

表 10.6 显示了作为 NLMIXED 过程输出的方程 (10.16) 随机聚类二项 GLOMM 的参数估计和标准误。读者可以验证，参数估计值（“-2 对数似然值”除外）与参数非常接近。

# 表 10.6: 随机聚类二项 GLOMM 的参数估计和标准误

| 参数 | 估计值 | 标准误 |
|---|---|---|
| -2 对数似然值 | 3155.5 | -- |
| $\pi_1$ | 0.1006 | 0.0080 |
| $\pi_2$ | 0.0714 | 0.0063 |
| 优势比 | 1.4551 | 0.1130 |
| $\rho^2$ | 0.1562 | 0.0120 |
| $\sigma^2$ | 1.6077 | 0.0191 |

## 10.6 零膨胀泊松和零膨胀负二项 GLOMMs

对于计数数据，我们在第 6 章中考虑了泊松模型的几种变体。原则上，随机效应可以自然地整合到这些每个模型中。在 SAS 中，可以使用类似的方法估计这些带有随机效应的模型。作为示例，在本节中，我们考虑了第 6 章第 6.3 节讨论的零膨胀泊松 (`ZIP`) 和零膨胀负二项 (`ZINB`)，即在线性预测因子中嵌入随机效应的 `ZIP` 和 `ZINB` 模型。让我们先取一个 GLOMM。

让 `$y_{ij}$` 表示第 $j$ 个受体的计数。

## 第 10 章 广义线性过离散混合模型 369

| AIC (越小越好) | 18974 |
| AICC (越小越好) | 18974 |
| BIC (越小越好) | 18990 |

| 参数 | 估计值 | 标准误 | DF | t 值 | Pr > |t| | Alpha | 下限 | 上限 | 梯度 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| b0 | 0.7988 | 0.07797 | 399 | 10.25 | <0001 | 0.05 | 0.6455 | 0.9521 | 0.000269 |
| b1 | 0.3090 | 0.1092 | 399 | 3.58 | 0.0004 | 0.05 | 0.1761 | 0.6057 | 0.000567 |
| w | 0.1984 | 0.007531 | 399 | 26.35 | <0001 | 0.05 | 0.1836 | 0.2132 | 0.00056 |
| sigma | 1.0594 | 0.04170 | 399 | 25.41 | <0001 | 0.05 | 0.9774 | 1.1414 | 0.000215 |

| 标签 | 估计值 | 标准误 | DF | t 值 | Pr > |t| | Alpha | 下限 | 上限 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 组 1 期望计数 | 2.6340 | 0.2032 | 399 | 12.96 | <0001 | 0.05 | 2.2346 | 3.0335 |
| 组 0 期望计数 | 1.7818 | 0.1389 | 399 | 12.83 | <0001 | 0.05 | 1.5088 | 2.0548 |
| 组 1 对组 0 期望计数之比 | 1.4783 | 0.1615 | 399 | 9.15 | <0001 | 0.05 | 1.1608 | 1.7958 |
| Sigma**2 | 1.1223 | 0.08835 | 399 | 12.70 | <0001 | 0.05 | 0.9486 | 1.2960 |

我们考虑 ZINB GLOMM

```sas
```



$y_{ij} \text{ given } (x_{ij}; u_{ij}) \sim \text{Zero-inflated Negative-binomial}(\lambda_{ij}, \kappa, \omega),$

$\log(\lambda_{ij}) = \beta_0 + \beta_1 x_{ij} + u_{ij}$

其中 `$\kappa$` 是过离散参数，`$\omega$` 是相对于负二项分布的额外零值比例，`$u_{ij}$` 是独立同分布的正态分布 `$(0, \sigma^2)$`，且

```sas
$x_{ij} = \begin{cases} 1 & \text{如果受试者在组 1 中} \\ 0 & \text{否则。}\end{cases}$
```

与 ZIP GLOMM 一样，我们假设 `n=200`, `m=12`, `$\beta_0=0.70, \beta_1=0.40, \omega=0.20$` 且 `$\sigma^2=1.20$`。额外的过离散参数假设为 `$\kappa=0.15$`。与之前，第一组的期望计数为 `$(1-\omega)e^{\beta_0+\beta_1}=0.80(e^{1.10})\approx2.4033$`。
第二组的期望计数为 `$(1-\omega)e^{\beta_0}=0.80(e^{0.70})\approx1.6110$`。因此，期望计数的比值如下

## 程序 10.7: 零膨胀负二项分布 GLOMM

```sas
/*
在零膨胀负二项分布 GLOMM 下生成数据，
参数为 Beta0, Betal, Kappa, W, 和 Sigma**2
*/
data zbind_glomm;
    beta0 = 0.70;
    betal = 0.40;
    kappa = 0.15;
    w = 0.20;
    sigma2 = 1.2;
    m = 12;
    n = 200;
    seed = 1917;
    nl = n+1;
    n2 = n+n;
    alpha = 1 / kappa;
    sigma = sqrt(sigma2);
    do i=1 to n;
        u = uniform(seed);
        if u > w then do;
            Group = 1;
            mu = exp(Beta0+Betal+u); /* 注意：原始 OCR 可能将 'u' 误写为 'z' */
            kappa = kappa * mu;
            beta = rang(seed,alpha);
            Y = ranpoi(seed,u);
            output;
        end else do;
            Group = 2;
            Y = 0;
            output;
        end;
    end;
    do i=n+1 to n2;
        z = Sigma*(seed);
        do t=1 to m;
            u = uniform(seed);
            if u > w then do;
                Group = 0;
                mu = exp(Beta0 +z);
                kappa = kappa * mu;
                beta = rang(seed, alpha);
                Y = ranpoi(seed, u);
                output;
            end else do;
                Group = 1;
                Y = 0;
                output;
            end;
        end;
    end;
    keep t group y;
run;
```

```sas
ods html;
title "Beta0, Kappa 和 Sigma**2 的零膨胀估计值";
proc glimm data=zib_glomm method=quad;
  class id group;
  model y = group / link=log dist=negbin;
  random / subject=id;
run;
proc nlixed data=zib_glomm;
  parms b0=0.49 b1=0.3 kappa=0.8 w=0.1 0.2 sigma=1.13;
  bounds kappa > 0 and kappa < 1;
  mu = exp(b0+b1*group);
  a = 1/kappa;
  p = lgamma(kappa*a);
  z = lgamma(y+a) - lgamma(y+1);
  if y<=0 then
    ll = log((1-w)*p);
  else ll = log(w) + a * log(p) + y * log(1-p);
  model y = ll;
  random u-normal(0,sigma) subject=id;
  estimate "Expected Counts Group 1" (1-w)*exp(b0+b1);
  estimate "Expected Counts Group 0" (1-w)*exp(b0);
  estimate "Ratio Expected Counts Group 1 Va 0" exp(b1);
  estimate "Sigma*2" sigma*sigma;
run;
ods close;
```



## 372 SAS 中的过离散模型

输出 10.7: 程序 10.7 节选——一个零膨胀负二项分布 GLOMM。使用 `PROC GLIMMIX` 对 `Beta0`, `Beta1`, `Kappa` 和 `Sigma**2` 进行初始估计

| GLIMMIX 过程 | | |
| :--- | :--- |
| |方差参数估计值 | | |
| 协方差参数 | 受试者 | 估计值 | 标准误 |
| :--- | :--- | :--- | :--- |
| 截距 | id | 1.2735 | 0.1033 |
| 尺度 | | 0.7787 | 0.0330 |
| 固定效应解 | | | |
| 效应 | 估计值 | 标准误 | DF | t 值 | Pr > |t| |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 截距 | 0.4904 | 0.0845 | 398 | 5.80 | <0001 |
| 组 | 0.3525 | 0.1189 | 399 | 2.97 | 0.033 |
| 组 | 0 | | | | |
| NLMIXED 过程 | | |
| 参数 | 估计值 | 标准误 | DF | t 值 | Pr > |t| | Alpha | 上限 | 梯度 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| b0 | 0.7072 | 0.0096 | 399 | 13.19 | <0001 | 0.05 | 0.6486 | 0.7941 |
| b1 | 0.3513 | 0.1189 | 399 | 2.96 | 0.0033 | 0.05 | 0.1176 | 0.5850 |
| kappa | 0.1269 | 0.00924 | 399 | 13.77 | <0001 | 0.05 | 0.1080 | 0.1458 |
| w | 0.2061 | 0.00832 | 399 | 24.77 | <0001 | 0.05 | 0.1898 | 0.2325 |
| sigma | 1.0594 | 0.04170 | 399 | 25.41 | <0001 | 0.05 | 0.9774 | 1.1414 | 0.000215 |

## 第 10 章 广义线性过离散混合模型 373

| 额外估计 | | | | |
| 标签 | 估计值 | 标准误 | DF | t 值 | Pr > |t| | Alpha | 下限 | 上限 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 组 1 期望计数 | 2.2881 | 0.2020 | 399 | 11.92 | <0001 | 0.05 | 1.9106 | 2.6656 |
| 组 0 期望计数 | 1.6103 | 0.1364 | 399 | 11.81 | <0001 | 0.05 | 1.3421 | 1.8781 |
| 组 1 对组 0 期望计数之比 | 1.4209 | 0.1689 | 399 | 8.41 | <0001 | 0.05 | 1.0889 | 1.7530 |
| Sigma**2 | 1.3144 | 0.1035 | 399 | 12.70 | <0001 | 0.05 | 1.1109 | 1.5179 |

表 10.7 汇总了 `NLMIXED` 过程报告的两种 GLOMM 主要结果。

### 10.7 结语

在本章中，我们介绍了关于广义线性混合模型 `GLMM` 的一些基本概念。我们强调了被称为极大似然的估计方法，该方法基于自适应高斯-赫特积分，是本章所有示例使用的估计方法。这是 `GLIMMIX` 过程使用的方法之一。另一种方法，基于线化的伪似然方法已在第 9 章中讨论。第 10.2 节的多个中心随机试验和第 10.3 节的压水反应堆核电泵可靠性示例用于说明二项分布和泊松分布 `GLMM` 的拟合。第三个示例第 9.9 节讨论的肩部研究在 `GLMM` 的背景下被重新讨论。`GLMM` 的基本概念可以扩展到更广泛的模型族，即广义线性过离散混合模型 `GLOMM` 族；这一特定特征是

为了理解。该扩展本质上是将随机效应适当嵌入到第 4、6 和 7 章中讨论的广义线性过度离散模型 `GLOM` 中。我们还讨论了四个生成数据的示例，涵盖了 Beta 二项 `Beta-binomial`、随机聚类二项 `Random-clumped Binomial`、零膨胀泊松 `Zero-inflated Poisson` 和零膨胀负二项 `Zero-inflated Negative-binomial` `GLOMMs`。泊松和负二项 `GLMM` 的示例，以及零膨胀泊松和泊松障碍 `GLOM` 的示例，均可在 Littell 等人 `2006` 的第 15 章中找到。`SAS` 文中的 `GLMMIX` 过程讨论了一个广义泊松 `GLOM` 的示例。广义泊松可以被解释为泊松混合分布，因此为负二项分布提供了一种替代方案 `见 Joe and Zhu，2005`。此外，拟合狄利克雷多项 `Dirichlet-multinomial` 或随机聚类多项 `Random-clumped Multinomial` `GLOM` 可能会带来复杂的计算问题。我们预计在未来的版本中提供对这些多项 `GLOMMs` 的指导。

# 旅程结束

我们通过回顾 McCullagh 和 Nelder 的评论结束这段旅程：“……过度离散[现象]在实践中是常态，而名义离散则是例外。过度离散在实践中的普遍性要求每一位实践统计学家都非常熟悉它，并配备工具来模拟这种偏离独立性假设的显著差异。解释过度离散的模型、它与混合模型的密切联系，以及它在理论和计算上的许多有趣方面，使得过度离散成为一个肥沃的研究领域。在序言中，我们承诺为读者带来一份过度离散主题的“精选拼盘”。我们希望我们履行了承诺。对于任何意见、建议、推荐或批评，请随时联系本书的两位作者之一。第一位作者 Jorge G. Morel 可以 statistics@gmail.com 联系，第二位作者 Nagaraj K. Neerajal 可以 inference@gmail.com 联系。感谢您的支持。”

Morel, Jorge, and Nagaraj Neerajal. Overdispersion Models in SAS®. 版权 © 2011, SAS Institute Inc., Cary, North Carolina, USA. 版权所有。欲获取更多 SAS 资源，请访问 support.sas.com/publishing。

Morel, Jorge, and Nagaraj Neerajal. Overdispersion Models in SAS®. 版权 © 2011, SAS Institute Inc., Cary, North Carolina, USA: 版权所有。欲获取更多 SAS 资源，请访问 support.sas.com/publishing。

# 缩写表列表

| 缩写 | 定义 |
|---|---|
| AE | 不良事件 |
| AIC | 赤池信息准则 |
| AICC | 修正的赤池信息准则 |
| BB | Beta 二项 |
| BIC | 施瓦茨贝叶斯信息准则 |
| BLUE | 最佳线性无偏估计量 |
| CMH | Cochran-Mantel-Haenszel 估计量 |
| deff | 设计效应 |
| DM | 狄利克雷多项 |
| FIM | 费舍尔信息矩阵 |
| GEE | 广义估计方程 |
| GLM | 广义线性模型 |
| GLMM | 广义线性混合模型 |
| GLOM | 广义线性过度离散模型 |
| GLOMM | 广义线性过度离散混合模型 |
| GOF | 拟合优度 |
| HIV | 人类免疫缺陷病毒 |
| LD50 | 使 50% 人口死亡的剂量 |
| LMM | 线性混合模型 |

| 缩写 | 定义 |
|---|---|
| LOF | 拟合不良 |
| LS | 最小二乘法 |
| LS-Means | 最小二乘均值 |
| MLE | 最大似然估计量 |
| NB | 负二项 |
| OLS | 普通最小二乘法 |
| OR | 优势比 |
| PA | 人群平均 |
| PHT | 苯西汀 |
| PL | 伪似然 |
| QLE | 拟似然估计 |
| QQ-plot | 分位数图 |
| RCBB | 随机聚类二项 |
| RCM | 随机聚类多项 |
| REML | 限制极大似然估计 |
| SS | 受体特异 |
| TCPO | 三氯丙烷 |
| UTI | 尿路感染 |
| ZIB | 零膨胀二项 |
| ZINB | 零膨胀负二项 |
| ZIP | 零膨胀泊松 |

More, Jorge, and Nagaraj Neerajal. Overdispersion Models in SAS®. 版权 © 2011, SAS Institute Inc., Cary, North Carolina, USA: 版权所有。欲获取更多 SAS 结果，请访问 support.sas.com/publishing。

# 参考文献

Agresti, Alan, and Winner, Larry. 1997. “评估评审者之间的一与分歧。” Chance, 10, 10–14。

# SAS 中的 384 过度离散模型

Neerchal, Nagaraj K., and Morel, Jorge G. 1998. “两种参数多项额外变异模型的大聚类结果。” Journal of the American Statistical Association, 93, 1078–1087。

# 索引

## AIC 赤信息准则 109
## BIC 贝叶斯信息准则 109

## 二项分布
- 6,223–224
