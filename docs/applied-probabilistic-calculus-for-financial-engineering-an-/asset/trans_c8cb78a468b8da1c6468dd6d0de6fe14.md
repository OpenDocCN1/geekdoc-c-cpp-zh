

**证明：**

由于 $C = Ef(S/E)$，由 (RE-3.5)，

$$\begin{aligned}
\frac{\partial C}{\partial E} &= \frac{\partial}{\partial E}[Ef(S/E)] \\
&= f(S/E) + E\frac{\partial f(S/E)}{\partial E} \\
&= f(S/E)\cdot 1 + E\cdot S\left(-\frac{1}{E^2}\right)\frac{\partial f}{\partial E} \\
&= f(S/E) - (S/E)f'(S/E)
\end{aligned}$$

因此，将 (RE-3.6) 中的 $f(S/E)$ 代入：

$$\frac{\partial C}{\partial E} = C/E - (S/E)F'(S/E) \tag{RE-3.8}$$

同样，由于 $C = Ef(S/E)$，由 (RE-3.4)，

$$\begin{aligned}
\frac{\partial C}{\partial S} &= \frac{\partial}{\partial S}[C] \\
&= \frac{\partial}{\partial S}[Ef(S/E)] \\
&= E\frac{\partial}{\partial S}[f(S/E)] \\
&= E(1/E)\frac{\partial}{\partial S}[f(S/E)] \\
&= (1)f'(S/E) \\
&= f'(S/E)
\end{aligned}$$

因此，

$$\frac{\partial C}{\partial S} = f'(S/E) \tag{RE-3.9}$$

即

$$\frac{\partial C}{\partial S} = f'(S/E) = f'$$

于是，

$$S\frac{\partial C}{\partial S} = Sf'(S/E) = Sf'$$

再次由 (RE-3.5)，

$$C = Ef(S/E)$$

因此，

$$\begin{aligned}
\frac{\partial C}{\partial S} &= \frac{\partial}{\partial S}[Ef(S/E)] \\
&= (1/E)\frac{\partial}{\partial S}[Ef(S/E)] \\
&= \frac{\partial}{\partial S}[Ef(S/E)] \\
&= f'(S/E)
\end{aligned} \tag{RE-3.10}$$

因此，

$$E\frac{\partial}{\partial E}(C) = \frac{\partial}{\partial E}[Ef(S/E)]$$

其中将 (RE-3.5) 中的 C 代入。

另外，由 (RE-3.8)，

$$\frac{\partial C}{\partial E} = C/E - (S/E)F(S/E) \tag{RE-3.11}$$

因此，

$$\frac{\partial C}{\partial E} = \frac{\partial}{\partial E}[Ef(S/E)]$$

$$= f(S/E) \tag{RE-3.12}$$

现在，

$$E\frac{\partial C}{\partial E} = E\left[C/E - (S/E)F(S/E)\right],\text{ 由 (RE-3.11)}$$ 
$$= C - SF(S/E)$$
$$= C - S\frac{\partial C}{\partial S},\text{ 由 (RE-3.10)}$$

因此，

$$S\frac{\partial C}{\partial S} = C = E\frac{\partial C}{\partial E} \tag{RE-3.13}$$

这是一个重要的中间结果。

类似地，可以证明

$$S^2\frac{\partial^2 C}{\partial S^2} = E^2\frac{\partial^2 C}{\partial E^2} \tag{RE-3.14}$$

这是一个最终结果，可以很容易地推导如下：

由于 $S\frac{\partial C}{\partial S} = C - E\frac{\partial C}{\partial E}$，由 (RE-3.13)

$$\frac{\partial C}{\partial S} = C/S - (E/S)\frac{\partial C}{\partial E}$$

且

$$\frac{\partial^2 C}{\partial S^2} = \frac{\partial}{\partial S}\left\{C/S - (E/S)\frac{\partial C}{\partial E}\right\}$$
$$= \frac{\partial}{\partial S}\left\{C/S\right\} - \frac{\partial}{\partial S}\left\{(E/S)\left(\frac{\partial C}{\partial E}\right)\right\}$$
$$= -(C/S^2) + (E/S^2)\left(\frac{\partial C}{\partial E}\right)$$

即，

$$S^2\frac{\partial^2 C}{\partial S^2} = -C + E\left(\frac{\partial C}{\partial E}\right) \tag{RE-3.15}$$

此外，由于

$$\frac{\partial C}{\partial E} = F(S/E),\text{ 由 (RE-3.12)}$$ 
$$E\frac{\partial C}{\partial E} = EF(S/E) = C,\text{ 由 (RE-3.5)}$$

因此，

$$\frac{\partial C}{\partial E} = \frac{C}{E} \tag{RE-3.16}$$

且

$$\frac{\partial^2 C}{\partial E^2} = \frac{\partial}{\partial E}\left[\frac{\partial C}{\partial E}\right]$$

根据定义

$$= \frac{\partial}{\partial E}\left[\frac{C}{E}\right],\text{ 由 (RE-3.16)}$$

$$= -\frac{C}{E^2} + \frac{1}{E}\frac{\partial C}{\partial E}$$

根据商法则求导

即

$$E^2\frac{\partial^2 C}{\partial E^2} = -C + E\frac{\partial C}{\partial E} \tag{RE-3.17}$$

结合 (RE-3.15) 和 (RE-3.17)，最终得到 (RE-3.14)，得证。

现在，将 (RE-3.14) 和 (RE-3.13) 中的项 $S^2\frac{\partial^2 C}{\partial S^2}$ 和 $S\frac{\partial C}{\partial S}$ 分别代入 Black–Scholes 方程 (RE-3.1)，结果为

$$\frac{\partial C}{\partial t} + \frac{1}{2}\sigma^2 S^2 \frac{\partial^2 C}{\partial S^2} + r S \frac{\partial C}{\partial S} - r C = 0 \tag{RE-3.1}$$

即，

$$\frac{\partial C}{\partial t} + \frac{1}{2}\sigma^2 \left(S^2 \frac{\partial^2 C}{\partial S^2}\right) + r\left(S\frac{\partial C}{\partial S}\right) - r C = 0$$

即，

$$\frac{\partial C}{\partial t} + \frac{1}{2}\sigma^2 \left(E^2 \frac{\partial^2 C}{\partial E^2}\right) + r\left(C - E\frac{\partial C}{\partial E}\right) - r C = 0$$

即，

$$\frac{\partial C}{\partial t} + \frac{1}{2}\sigma^2 \left(E^2 \frac{\partial^2 C}{\partial E^2}\right) - r E \frac{\partial C}{\partial E} = 0 \tag{RE-3.2}$$

即为 (RE-3.7)，得证。

## 4 使用 R 编程进行数据分析

在一则互联网在线广告中，有一则统计学家职位空缺的招聘广告，内容如下：

#### 职位摘要

- **统计学家 I**
  - **薪资：** 面议
  - **雇主：** XYZ 研究与统计
  - **地点：** Y 州 X 市
  - **类型：** 全职 – 入门级
  - **类别：** 金融分析师/统计、数据分析/处理、统计组织与管理
  - **所需学历：** 硕士及以上优先

XYZ 研究与统计是设计、管理和分析金融数据方面的全国领先机构。XYZ 与其他研究者合作，提供备受信赖的统计专业知识，并辅以先进的基于网络的数据管理系统。XYZ 的服务确保试验的及时、安全实施以及可靠的数据分析。

#### 职位描述

**职位概述：** 这是一个令人兴奋的机会，统计学家可以加入一个规模虽小但不断壮大的团队，专注于金融投资分析及相关转化研究。XYZ 位于 XX 市中心，负责设计、管理和分析各种投资和金融项目，以及相关市场数据的分析。成功的候选人将与统计学家同事和金融研究人员合作，设计、评估和解释投资研究。

**主要职责：** 与统计学家同事及其他金融工程师合作，分析投资情况及相关的辅助研究。准备表格、图表和书面研究结果摘要；与其他金融人员合作解释结果；并协助准备手稿。为合作人员提供统计咨询。完成分配的其他相关工作。

#### 任职要求

**所需资格：** 统计学、应用数学或相关领域的硕士学位。扎实的应用统计学知识。熟练使用 `R` 进行统计计算。

**优先职责/资格：** 统计咨询经验。`S-Plus` 或 `R` 编程语言经验。高维数据分析经验。良好的口头和书面沟通能力。出色的沟通/团队合作能力，以便有效协作。具备西班牙语能力者优先。

*在求职信中，请描述您的技能和经验如何与该职位的资格要求相匹配。*

如需了解更多关于 XYZ 的信息，请访问 www.XYZ.org。

显然，人们应注意到，职位明确要求具备使用 `R` 编程进行数据分析的专业熟练程度。

即使不在这样的求职市场中，作为从事金融、资产配置、投资组合优化等领域工作的统计学家，掌握包括 `R` 编程在内的技能组合也将是有帮助且有趣的。

### 4.1 数据与数据处理

*数据* 是可从中得出结论的事实或数字。当数据在某个框架内被记录、分类、组织、关联或解释，从而产生意义时，它们就变成了 *信息*。将数据转化为信息涉及多个步骤，这些步骤被称为 *数据处理*。本节介绍数据处理以及计算机如何高效且有效地执行这些步骤。

需要指出的是，许多这些处理活动都可以使用 `R` 编程进行，或者在 `R` 环境中借助可用的 `R` 包来执行——其中存储了 `R` 函数和数据集。

#### 4.1.1 引言

##### 4.1.1.1 编码

###### 4.1.1.1.1 自动化编码系统

下面的简化流程图展示了原始数据如何转化为信息：

数据 → 收集 → 处理 → 信息

一旦所有相关数据收集完毕，数据处理就开始了。数据从各种来源汇集并输入计算机，在计算机中进行处理以产生信息——即输出。

数据处理包括以下步骤：

- 数据编码
- 数据采集
- 编辑
- 插补
- 质量控制
- 生成结果

**数据编码** 首先，在原始数据输入计算机之前，必须对其进行编码。为此，调查回答需要被标记，通常使用简单的数字代码。这可以由现场的访问员或办公室员工完成。数据编码步骤非常重要，因为它使数据输入和数据处理更加容易。

调查有两种类型的问题——封闭式问题和开放式问题。对这些问题的回答会影响所执行的编码类型。

封闭式问题意味着只允许固定数量的预先确定的调查回答。这些回答已经被编码。

以下关于体育活动的调查问题就是一个封闭式问题的例子：

在为您提供以下益处方面，体育有多重要？

- 1) 非常重要
- 2) 有些重要
- 3) 不重要

开放式问题意味着允许任何回答，这使得后续编码更加困难。为了对开放式问题进行编码，处理者必须抽取一定数量的回答样本，然后设计一个包含所有可能答案的编码结构。

以下编码结构是一个开放式问题的例子：

您参加哪些体育活动？
请具体说明（28 个字符）________________________

