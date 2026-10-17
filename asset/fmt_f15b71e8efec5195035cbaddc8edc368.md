
J. Robinson. 1965. 基于递归原理的面向机器逻辑。Journal of the ACM, 12: 23-41. DOI: 10.1145/321250.3212253, 121, 135

D. Sacco and C. Zaniolo. 1990. 带否定逻辑程序中的稳定模型与非确定性。在 D. J. Rosenkrant and Y. Sagiv, ed., Proceedings of 9th ACM SIGACT-SIGMOD Symposium on Principles of DATABASE Systems, PODS 1990, pp. 205-217. ACM Press. DOI: 10.1145/298514.298572_19

![](img/820e45212e28eae9aa3922fcefe36_201.png)

# 参考文献

K. F. Sagonas, T. Swift, and D. S. Warner. 1994. 作为高效演绎引擎的 XSB。在 R. T. Snodgrass and M. Winslett, eds., Proceedings of 1994 ACM SIGMOD International Conference on Management of Data, pp. 442–453. ACM Press. DOI: 10.1145/191839.191927.122, 175

J. S. Schliff. 1995. 逻辑编程语义的表达能力。J. Comput. Syst. Sci., 51(1): 64–86. DOI: 10.1016/cs.1995.1053.176

R. M. Smullyan. 1961. 形式系统理论。Annals of Mathematical Studies, volume 47. Princeton University Press, Princeton, New Jersey.

A. Tarski. 1955. 格点理论定理及其应用。Pacific Journal of Mathematics, 5: 285–309. DOI: 10.2140/jpm.1955.5.285

M. Truszczynski. 2012. 通过归约连接一阶 ASP 与 FO-ID。在 E. Erdem, J. Lee, Y. Lier, and D. Pearce, Correct Reasoning - Essays in Honor of Vladimir Lifschitz, volume 7265 of LNCS, pp. 543–559. Springer. DOI: 10.1007/978-3-642-30743-3_177

M. van Emden and R. Kowalski. 1976. 作为编程语言的谓词逻辑语义。Journal of the ACM, 23(4): 733–742. DOI: 10.1145/321978, 128, 134

A. Gelder. 1993. 带否定的交替点逻辑程序。Journal of Computer and Systems, 47(1): 185–221. DOI: 10.1016/0022-102X(93)9024-6_173

A. Gelder, K. A. Ross, and J. Schlipf. 1998. 一般逻辑程序的无良基与良基语义。在 C. Edmondson and M. Yannakakis, eds., Proceedings of the Seventh ACM SIGMOD-SIGART Symposium on Principles of Database Systems, PODS 1998, pp. 221–230. ACM Press. DOI: 10.1145/308386.308444, 122, 138

A. Gelder, K. A. Ross, and J. Schlipf. 1991. 一般逻辑程序的良基语义。Journal of the ACM, 38(3): 620–650. DOI: 10.1145/116825.116838, 122, 136, 171, 173

S. Woltran. 2011. 扩展 datalog 程序之间的等价性——简要调查。在 O. Moor, G. Gottlieb, T. Fuchs, and J. Sellers, eds., Data Reload - First International Workshop, Datalog 2010, volume 6702 of Lecture Notes in Computer Science, pp. 106–119. DOI: 10.1007/978-3-642-24206-9_166

![](img/820e45212e28eaeacaa3922fce5fe36_202_0.png)

# 概率逻辑编程综述

Fabrizio Riguzzi, Theresa Swift

逻辑编程与概率的结合已被证明适用于建模元素之间存在复杂且不确定关系的领域。目前已经提出了许多概率逻辑编程（PLP）语义；其中，分布语义最近引起了越来越多的关注，并被许多语言采用，例如独立选择逻辑、PRISM、带注释析取的逻辑程序、ProbLog 和 prolog。

本章回顾了分布语义，从最简单的层化 Datalog 程序开始，展示了如何将定义扩展到包含函数符号和非层化否定的程序。本文还讨论了采用分布语义的语言，并将其相互以及与贝叶斯网络进行了比较。我们综述了遵循分布语义的 PLP 语言的现有推理方法。我们专注于 PRISM、ProbLog 和 PITA 系统。PRISM 系统是最早的之一，当程序满足限制时可以使用。ProbLog 引入了二进制决策图的使用，为消除这些限制并在更一般的程序上执行推理提供了计算基础。PITA 通过使用表和答案包含加速推理。它支持一般的概率程序，但也可以针对更简单的设置甚至概率推理进行优化。本章还讨论了各种方法的计算复杂度，以及通过近似来限制的技术。

## 3.1 引言

如果推理是数学逻辑的核心方面，那么不确定推理（Henry Kyburg 术语）则是许多计算逻辑特别是逻辑编程的核心。不确定推理包含了非单调推理、模糊逻辑和概率逻辑，以及逻辑与概率的结合。将概率与逻辑推理混合对于人工智能任务（如代理行为、复杂系统诊断、风险评估和构建学习）特别有吸引。它对于利用本身是概率的已有知识也有帮助，例如用于医学、生物信息学、自然语言处理、营销等领域。这些方面导致了对贝叶斯网络、马尔可夫网络和统计学习技术等概率形式的大研究。

这些趋势通过各种 PLP 方法反映在逻辑编程领域。这些方法包括语言和框架概率逻辑程序 [Dantsin 1991]、概率 Horn 演绎 [Poole 1993b]、PRISM [Sato 1995]、独立选择逻辑 [Poole 1997]、pD [Fuh 2000]、贝叶斯逻辑程序 [Kersting and Raadt 2001]、CLP [Costa et al. 2003]、带注释析取的逻辑程序 [Venenkens et al. 2004]、pB [Baral et al. 2009]、ProLog [De Raadt et al. 2007] 和 CP-Logic [Venenkens et al. 2009]。

一个稳定模型，甚至是一个良基模型。最后，贝叶斯网络的语义可以证明其在分布语义下等价于受限的概率逻辑程序类，这表明概率逻辑程序（PLP）的方法至少与贝叶斯网络一样强大。

出于这些原因，本章使用分布语义作为组织原则来提供 PLP 的介绍。我们对分布语义的关注使得本综述与 [De Raacdt and Kimmig 2015] 有不同，后者是一篇实用的概述，更多地关注 PLP 的实际编程。因此，第 3.2 节从某些 PLP 语言的示例开始。第 3.3 节形式地介绍了最小情况的情况——即具有单个分层模型的 Datalog——首先在第 3.3.1 节给出；以此为基础，第 3.2 节中的语言被证明对于分层 Datalog 具有表达力。接下来，第 3.3 节将分布语义扩展到带有符号的程序，通过将查询的每个解释（证明查询所需的概率事实集）与一组世界关联，并在这些集合上构建概率分布。作为最后的扩展，消除了每个世界具有单个分层模型的假设（第 3.4 节）。

第 3.4 节讨论了作为分布语义替代方案的概率逻辑语义。第 3.5 节讨论了与贝叶斯网络密切相关的 PLP 语言，并展示了贝叶斯网络如何等于 PLP 的特殊情况。

分布语义本质上是模型论的；第 3.6 节讨论了如何从概率逻辑程序进行推理。首先，在第 3.6.1 节回顾了相关的复杂度结果；由于概率逻辑程序的表达能力等于贝叶斯网络，很容易看出概率逻辑中的查询是 NP 硬的，实际上是 #P-完全的。第 3.6.2 节讨论了通用概率逻辑程序的精确继承技术，例如在 ProbLog 系统 [Kimmig. et. 2011] 中开创的二决策图的使用。第 3.6.3 节讨论了推理可处理的概率逻辑程序特殊情况，这些情况已被 PRISM 系统 [Sato. et. 2010] 特别利用。第 3.7 节以最后的讨论结束。

### 3.1.1 背景与假设

本综述可以供熟悉逻辑编程并想要学习其概率扩展的人士阅读，也可以供具有概率编程系统背景并想要学习如何在逻辑编程中建模和实现概率推理的人士阅读。在逻辑编程方面，我们假设对 Prolog/ASP 的语法和术语有基本的了解，并有一个通用概念，即程序根据否定的使用方式可能有不同类型的模型。例如，当前逻辑编程系统中实现了两种否定的语义：稳定模型和良基模型；请参阅 Truszczynski [2018] 以获得简要介绍。这两种语义在不使用否定的示例（确定性程序）或处理了否定的示例（分层程序）中是一致的 [Truszcynski 2018]。不需要关于这些模型的这些细节，例如它们如何通过不动点构建。在概率论方面，我们通常假设只对离散分布有基本的理解；在需要时会回顾其他概念的定义。

![](img/820e45212e28eaeac9aa3922fce5fe36_206_0.png)

## 3.2 分布语义的语言

遵循分布语义的语言在如何编码子句的选择以及如何陈述这些选择的概率方面有很大不同。然而，在所有语言中，选择之间都是相互独立的。正如第 3.3.2 节所示，只要各种类型的程序以相同的方式与世界关联，它们就具有相同的表达力。这一事实表明语言之间的差异是句法上的，同时也证明了讨论分布语义的合理性。

### 3.2.1 概率 Horn 归纳

在概率 Horn 归纳 `PHA` [1993] 和独立选择逻辑 `ICL` [1997] 中，选择通过以下形式进行表示：

```
disjoint(A_1 : p_1, ..., A_n : p_n)
```

其中 `$A_i$` 是离散的，`$\sum p_i = 1$`。对于最后的扩展，每个世界具有单个分层模型的假设被消除了（第 3.4 节）。（注：此处根据原文逻辑可能存在翻译对应重复，已按语意整合）。*更正：原文此处段落错乱，此处根据上下文重新翻译。* 实际上，对于每个世界，`$\theta$` 解释是随机的。在实践中，`disjoint` 语句的每个实例化都是独立同分布的随机变量（iid）。

![](img/820e45212e28eaeac9aa3922fce5fe36_207_0.png)

示例 3.1 的 PHA 程序编码了这样一个事实：如果某人感冒且其发烧，则他们会打喷嚏：

```
sneezing(X) :- flu(X), sneezing(X).
sneezing(X) :- fever(X), sneezing(X).
flu(bob).
fever(bob).

disjoint(sneezing(X) : 0.7, 0.3).
disjoint(sneezing(X) : 0.8, 0.2).
```

在这里，对于基于分布语义的其他语言，否定出现在身体中用于选择。

### 3.2.2 PRISM

`PRISM` 语言 [Sato. 1997] 与 PHA 类似，但它通过 `msw/3` 引入事实：

```
msw(SwitchName, Value).
```

该谓词的第一个参数是随机开关，第二个是整数，`SwitchName` 的可能取值集合定义为：

```
values(SwitchName, [v_1, ..., v_n]).
```

`SwitchName` 再次表示一个开关，`$p_j$` 是 `SwitchName` 取值为 `$v_j$` 的概率。每个世界通过为每个开关选择一个值得到的。

![](img/820e45212e28eaeac9aa3922fce5fe36_209_0.png)

示例 3.2 硬币掷展示了不同的 PLP 语言如何表示 iid 随机变量。假设硬币 `$c_1$` 不是均匀的，但 `$c_1$` 的所有掷都有相同的结果；换句话说，每次掷 `$c_1$` 都来自 iid 随机变量族。

```
values(c1, [head, tail])
:- sw(c1, [0.4, 0.6]).
```

在 PHA/ICL 和许多其他 PLP 语言中，`disjoint/1` 语句的每个基实例化可以使用 `msw/3` 的 trial id 来识别，`$c_1$` 的不同掷法需要通过语句的实例化模式表示，例如：

```
disjoint(coin(c1, TossNumber, head) : 0.4, coin(c1, TossNumber, tail) : 0.6).
```

在实践中，PRISM 接受包含 trial id 的 `msw/2` 原子，并且程序中的每次出现被认为关联到一个不同的变量。

示例 3.3 示例 3.1 可以在 PRISM 中编码为：

```
sneezing(X) :- flu(X), msw(flu.sneezing(X), 1).
sneezing(X) :- fever(X), msw(fever.sneezing(X), 1).
flu(bob).
fever(bob).

values(flu.sneezing(X), [1, 0]).
values(fever.sneezing(X), [1, 0]).
:- sw(flu.sneezing(X), [0.7, 0.3]).
:- sw(fever.sneezing(X), [0.8, 0.2]).
```

### 3.2.3 带有标注析取的的逻辑程序

在带有标注析取的的逻辑程序 `LPADs` [Vennekens et al. 2004] 中，替代方案通过子句的标注析取头部的消息来表示。一个标注析取子句的形式为：

```
$H_1 : p_1; \dots; H_i : p_i :- B_{i1}, \dots, B_{im}$
```

## 3.2 具有分布语义的语言

其中 `$H_{i1}, \dots, H_{in}$`, `$B_{i1}, \dots, B_{in}$` 是逻辑原子，而 `$p_{i1}, \dots, p_{in}$` 是 `[0, 1]` 区间内的实数，满足 `$\sum_{k=1}^n p_{ik} = 1$`。每个世界都是通过从每个标注析取句的地面化头部中选择一个原子得到的。

示例 3.4 示例 3.1 可以在 LPADs 中表示为：

```
$sneezing(X) : 0.7 \vee null : 0.3 :- flu(X). \quad (C_1)$
$sneezing(X) : 0.8 \vee null : 0.2 :- hay fever(X). \quad (C_2)$
```

```
$flu(bob).
hay fever(bob).
```

### 3.2.4 ProbLog

`ProbLog` [De Raedt et al. 2007] 的设计初为了尽可能为 Prolog 提供一个简单的概率扩展。在 ProbLog 中，替代方案通过形式如下的概率因子表示：

```
$p_i ::= A_i$
```

其中 `$p_i \in [0, 1]$` 且 `$A_i$` 是一个原子，这意味着 `$A_i$` 的每个地面化 `$A\theta$` 有概率 `$p_i$` 真，概率 `$1-p_i$` 假。每个世界都是通过选择或拒绝所有概率因子的每个地面化得到的。

示例 3.5 示例 3.1 可以在 ProbLog 中表示为：

```
$sneezing(X) :- flu(X),sneezing(X).
$sneezing(X) :- hay fever(X),hay fever.sneezing(X).
$flu(bob).
hay fever(bob).
$0.7 :- flu.sneezing(X).
$0.8 :- hay fever.sneezing(X).
```

与 LPADs 和 ProbLog 中，概率句的每个地面化都与一个随机变量相关，其取值数量与 LPADs 中的析取相同，而 ProbLog 有两个取值。对应于概率句不同实例的随机变量是独立同分布的（iid）。

- `CP-logic` [Vennekens et al. 2009] 具有与 LPADs 类似的语法，这些语言的语义与分层 Datalog 程序一致。

## 3.3 定义分布语义

在介绍分布语义时，我们使用术语“概率构造”（probabilistic construct）来指代不相交汇集、多开关、标注析取句和概率事实，以便讨论它们的共同属性。

分布语义适用于无限制的规范式逻辑程序。然而，为了解释起见，我们从第 3.3.1 节开始，首先进行了两个简化。

**Datalog 程序。** 如果一个程序没有函数符号，那么 Herbrand 宇宙是有限的，每个概率构造的地面化集也是有限的。

**分层程序。** 这些程序具有全序良好模型 [Van Gelfider et al. 1991]，或者等价地具有单模型 [Gelfond and Lifschitz 1988]。

基于上述分布语义，第 3.3.2 节讨论了第 3.2 节中列出的语言之间的关系。之后，在第 3.3.3 节取消了对 Datalog 程序的限制，并在第 3.3.4 节取消了分层的限制。我们注意到，在本节中，所有的概率分布都是离散的；然而，连续分布也被用于分布语义 [Gutmann et al. 2011a, Islam et al. 2012]。

### 3.3.1 分层 Datalog 程序的分布语义
