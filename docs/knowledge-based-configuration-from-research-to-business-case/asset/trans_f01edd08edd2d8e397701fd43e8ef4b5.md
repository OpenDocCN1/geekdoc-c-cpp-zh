

## 1 本书的动机

Alexander Felfernig\*, Lothar Hotz†, Claire Bagley‡, and Juha Tiihonen§

- \* Graz University of Technology, Graz, Austria
- † HITeC e.V., University of Hamburg, Hamburg, Germany
- ‡ Oracle Corporation, Burlington, MA, USA
- § Aalto University, Aalto, Finland

**摘要：** 欢迎阅读这本关于配置系统的书籍！本书的目的是让读者了解一个已在工业界成功集成并使用超过30年的人工智能领域。本书为来自工业、教育和研究领域的感兴趣读者提供了与配置相关的材料。

### 1.1 什么是配置？

本书的这一部分首先介绍动机，回顾历史发展（第2章）、相关技术问题（第3章）和商业利益（第4章）。第5章提供了本书组织的概述。

大规模生产。 在上个世纪的第一部分，亨利·福特推出了T型车（见图1.1），并通过引入大规模生产的概念彻底改变了汽车的制造方式，即高效生产大量相同的产品。福特本人对大规模生产的最好描述是：你可以拥有任何颜色的汽车，只要它是黑色的（关于1909年T型车的评论）。

大规模定制。 与此同时，相同产品的批量生产已成为过去的商业模式，因为买方市场占主导地位。这种情况对生产和销售流程提出了新的挑战，因为公司现在被迫提供满足客户个人需求的产品。因此，大规模定制范式（Anderson and Pine, 1996; Pine, 1999）得以确立。该范式基于在接近大规模生产定价条件下对高度变异产品的客户个体化生产思想。这意味着主要目标不仅是实现向更充分考虑客户需求和偏好的范式转变，而且要在大规模生产水平的时间和定价条件下实现这一目标。大规模定制时代为有效实施该范式而迫切需要的技术发展敲响了警钟。配置技术已发展成为支持大规模定制业务场景的领先技术。

基于知识的配置。 Sabin和Weigel（1998）对配置（作为一项活动）给出了一个定义，他们将配置定义为“设计活动的一种特殊情况，其中

如何基于一致性知识库测试和（自动化）调试的集成方法来测试此类系统。

- （3）对于*对配置技术教学感兴趣的工业界和学术界代表*，我们在整本书中提供了与个人电脑配置产品域相关的实际工作示例。我们选择该域是因为它众所周知，并且经常用作参考示例。此外，我们还提供了一套可自由用于配置系统课程的幻灯片。
- （4）对于*对配置系统感兴趣的研究人员*，我们提供了基本技术的概述以及对高级主题的介绍，最终引出未来研究的议题讨论。

本书内容的更深入概述，包括哪些部分对哪些读者群体有用，可以在[第5章](#)中找到。

## 参考文献

Anderson, D., Pine, B.J., 1996. Agile Product Development for Mass Customization. McGraw-Hill.

Falkner, A., Felfernig, A., Haag, A., 2011. Recommendation Technologies for Configurable Products. AI Magazine 32 (3), 99–108.

Mittal, S., Frayman, F., 1989. Towards a generic model of configuration tasks. In: 11th International Joint Conference on Artificial Intelligence (IJCAI-89), Detroit, Michigan, USA, vol. 2, pp. 1395–1401.

Pine, B.J., 1999. Mass Customization: The New Frontier in Business Competition. Harvard Business School Press.

Sabin, D., Weigel, R., 1998. Product configuration frameworks – a survey. IEEE Intelligent Systems 13 (4), 42–49.

## 2 配置技术的简史

Lothar Hotz\*, Alexander Felfernig†, Andreas Günter\*, and Juha Tiihonen‡

- \* HITeC e.V., University of Hamburg, Hamburg, Germany
- † Graz University of Technology, Graz, Austria
- ‡ Aalto University, Aalto, Finland

**摘要：** 近40年的配置技术促使我们对主要配置技术流进行简要概述。我们概述了该领域的技术发展，从20世纪70年代末的第一个专家系统到今天的配置解决方案。配置领域的庞大和复杂性使得不可能简洁地涵盖其所有相关方面。为本次概述的目的，我们决定重点关注以下四个不同但重叠的技术发展：（1）基于规则的配置器，（2）早期的基于模型的配置器，（3）主流配置环境，以及（4）大规模定制工具包。

### 2.1 基于规则的配置器

弱人工智能（Weak AI）（Searle, 1980）表示人工智能的狭义解释：它支持完成特定问题求解任务（如配置），而不涵盖人类认知能力的全部范围（见 Russell and Norvig, 2003）。在弱人工智能的思路下（当时该术语尚不为人知），在20世纪70年代开发了许多专家系统。成功的配置专家系统的例子有（1）R1/XCON（第一个版本于20世纪70年代末开发），一个计算机配置器（Bachant and McDermott, 1984; McDermott, 1982; Soloway et al., 1987）和（2）VT（垂直运输），西屋电梯公司用于处理电梯系统设计的系统（Marcus et al., 1987）。应用专家系统技术的主要原因之一是程序化（例如基于FORTRAN）方法解决配置问题失败。作为示例，我们重点关注R1/XCON配置器。

R1/XCON是由John McDermott最初基于OPS5（Forgy, 1981）实现的专家系统；即生产规则用于表达配置知识（见图2.1）。R1/XCON被开发用于支持VAX计算机系统的订单生成（最初用于Digital Equipment VAX-11系统，后来用于PDP、MICROVAX和MICRO-PDP）。

在引入R1/XCON之前，Digital Equipment（DEC）的计算机是手动配置的。因此，销售人员创建了错误、不完整和不可行的配置，这造成了巨大的额外开销和成本。DEC的总体净回报估计为每年4000万美元，这是成功交付有效且完全配置系统的结果。

```text
ASSIGN-POWER-SUPPLY-1

IF: THE MOST CURRENT ACTIVE CONTEXT IS ASSIGNING A POWER SUPPLY
    AND AN SBI MODULE OF ANY TYPE HAS BEEN PUT IN A CABINET
    AND THE POSITION IT OCCUPIES IN THE CABINET IS KNOWN
    AND THERE IS SPACE IN THE CABINET FOR A POWER SUPPLY
    AND THERE IS NO AVAILABLE POWER SUPPLY
    AND THE VOLTAGE AND FREQUENCY OF THE COMPONENTS IS KNOWN

THEN: FIND A POWER SUPPLY OF THAT VOLTAGE AND FREQUENCY
      AND ADD IT TO THE ORDER
```

**图 2.1**

R1/XCON中一个典型的规则（转述）（McDermott, 1982）。*条件*部分描述了当前的配置上下文（配置），而*动作*部分包括扩展该配置的动作。

尽管非常成功，R1/XCON有一个主要缺点：所选择的知识表示。基于规则的实现在知识库开发和维护方面触发了巨大的工作量（Soloway et al., 1987）。R1/XCON系统中定义的规则示例见图2.1。

R1/XCON的主要问题是领域知识与问题求解知识之间的依赖性；也就是说，当领域知识需要调整时，这会导致问题求解知识发生变化，反之亦然（Bachant and McDermott, 1984; Soloway et al., 1987）。换句话说，配置过程的结果在很大程度上取决于不同规则被解释的顺序。为了实现某个结果（配置），会应用晦涩的“技巧”来强制执行规则触发的特定序列（Soloway et al., 1987）。

这种不幸的情况促使了新的技术发展，可以用*基于模型的知识表示*这一术语来概括。¹

### 2.2 早期的基于模型的配置器

基于模型配置的主要特征是领域知识与问题求解知识之间清晰的分离。在配置上下文中，这通过产品特定知识与配置搜索相关知识的分离来实现；即找到一致的解决方案。

约束满足问题（CSPs）（见 Hotz et al., 2014²）是一种广泛使用的基于模型的知识表示形式主义。CSP的早期版本已在20世纪70年代末开发（Laurière, 1978; Mackworth, 1977）。多向性可以被认为是基于规则和基于约束问题求解之间的主要区别。

与基于约束的表示相反，规则基于*如果-那么结构*，其解释预设了从条件到动作部分的单向性。作为约束表述的限制使得可以为任意变量分配值。约束求解器可以传播

