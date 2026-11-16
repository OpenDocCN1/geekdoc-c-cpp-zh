

(Constantin 95). 康斯坦丁·冯·阿尔特罗克. 模糊逻辑与神经模糊应用详解. Prentice-Hall, 1995.

(Cornelius 98). 模糊逻辑与专家系统应用，Cornelius T. Leondes 编，Academic Press, 1998.

(Kerre 00). 若安·阮和埃蒂安·E. 凯雷. 计算智能中的模糊如果-那么规则, Kluwer Academic Publishers, 2000.

(Da Ruan 97). 智能混合系统：模糊逻辑、神经网络与遗传算法, Kluwer Academic Publishers, 1997.

(Gardenfors 04). 彼得·加登福斯. 信念修正, 剑桥理论计算机科学丛书, 2004.

(Dempster 67). A. P. 登普斯特, "由多值映射诱导的上下概率," 《数理统计年刊》, 38, 第 325-329 页, 1967.

(Giarratano 91). 约瑟夫·贾拉塔诺等人. "摄像机跟踪系统的模糊逻辑控制," 第五届空间运行应用与研究年度研讨会 (SOAR '91), 第 94-99 页, 1991.

(Harris 00). 约翰·哈里斯. 模糊逻辑应用导论, Kluwer Academic Publishers, 2000.

(Ibrahim 03). 艾哈迈德·M. 伊布拉希姆. 嵌入式系统应用的模糊逻辑，随书附带 CDROM 并包含大量参考文献，Newnes 出版, 2003.

(Kosko 96). 巴特·科斯科. 模糊工程, Prentice Hall, 1996.

(Liu 04). 刘雨音. 模糊神经网络理论与应用（机器感知与人工智能）, World Scientific Publishing Company, 2004.

(Mendel 00). 不确定基于规则的模糊逻辑系统：导论与新方向, Prentice-Hall, 2000.

(Nguyen 99). 洪·T. 阮和埃尔伯特·A. 沃克. 模糊逻辑导论, CRC Press, 1999.

(Roger 96). 张志星, 孙传才, 水谷英司. 神经模糊与软计算：学习与机器智能的计算方法, Prentice-Hall, 1996.

(Ross 04). 蒂莫西·J. 罗斯. 工程应用模糊逻辑, John Wiley & Sons, 2004.

(Siller 04). 威廉·西勒和詹姆斯·J. 巴克利. 模糊专家系统：理论与应用, Wiley-Interscience, 2004.

## CHAPTER 6

## 第 6 章

### Design of Expert Systems

### 专家系统设计

### 6.1 INTRODUCTION

### 6.1 引言

In the previous chapters, we have discussed the general concepts and theory of expert systems and other intelligent decision making-systems. A number of papers have attempted to summarize the properties of intelligent systems. There are many pros and cons for each type (Begley 03). This chapter presents general guidelines for building practical expert systems designed for real-world applications, not research prototypes. A software engineering methodology is described so that an expert system can be a quality product developed in a cost-effective and timely manner.

在前面的章节中，我们讨论了专家系统及其他智能决策系统的一般概念和理论。许多论文试图总结智能系统的特性。每种类型都有其利弊 (Begley 03)。本章介绍了构建面向实际应用（而非研究原型）的实用专家系统的一般准则。本文描述了一种软件工程方法论，以便专家系统能够以具成本效益且及时的方式开发为高质量产品。

Many books, papers, and software tools have been devoted to the design of expert systems, covering all aspects in great detail. So this one chapter will not make you an instant expert. (You'll have to read the chapter first). However by understanding the principles that explain why expert systems are designed the way they are, you'll be better able to take advantage of sophisticated tools and methodologies. In fact the design of expert systems is part of a more general field called Knowledge Management (KM) which deals with all the knowledge assets available to an organization (Becera-Fernandez 03).

大量书籍、论文和软件工具都致力于专家系统的设计，详细涵盖了所有方面。因此，本章不会让你立刻成为专家。（你得先读完本章。）然而，通过理解解释专家系统为何如此设计的原理，你将能更好地利用复杂的工具和方法论。事实上，专家系统的设计是知识管理（KM）这一更广泛领域的一部分，知识管理涉及组织可用的所有知识资产 (Becera-Fernandez 03)。

KM is connected to the Information Management (IM) which is connected to the Information Processing (IP) which is connected to the Information Systems (IS) which is connected to the Information Technology (IT). (On second thought, if you can say KM, IM, IP, IT, three times in a row without mispronouncing, you are an Instant Expert!) KM is a major problem considering all the different types of resources for many different types of audiences such as office, web, FAQs, Help Desk (human and automated), email, fax, phone, product, program, developer, manager, end-user, and publicity.

KM 与信息管理（IM）相连，IM 与信息处理（IP）相连，IP 与信息系统（IS）相连，IS 与信息技术（IT）相连。（再想一想，如果你能连续三次不出错地说出 KM、IM、IP、IT，那你就是一位“即时专家”！）考虑到面向办公、网络、FAQ、帮助台（人工和自动化）、电子邮件、传真、电话、产品、程序、开发人员、经理、最终用户和宣传等众多不同类型受众的各种不同资源，KM 是一项重大问题。

Large companies have their own very detailed methods, documents, books, and software they developed to create, manage, maintain, and sell knowledge assets because it is such a profitable field (Conway 02). This is especially true when intelligent tools are created that can greatly reduce human expenses because that's even cheaper than global outsourcing.

大型公司拥有自己开发的非常详细的方法、文档、书籍和软件，用于创建、管理、维护和销售知识资产，因为这是一个非常有利可图的领域 (Conway 02)。当创建能够大幅降低人力成本的智能工具时，这一点尤其正确，因为这甚至比全球外包更便宜。

If you think how much time a typical person spends using computers, it's a tautology that we need computers to manage all the documents created by computers. Expert systems are widely used in business because they are so essential to the dramatically increasing amount of information and knowledge available on the web (Malhotra 01). As usual, links to software and other online resources for this chapter are listed in Appendix G.

如果你想想一个典型的人花在使用计算机上的时间有多少，那么我们需要计算机来管理计算机创建的所有文档，这是一句废话。专家系统在商业中被广泛使用，因为它们对于网络上剧增的信息和知识量至关重要 (Malhotra 01)。与往常一样，本章的软件和其他在线资源链接列在附录 G 中。

### 6.2 SELECTING THE APPROPRIATE PROBLEM

### 6.2 选择合适的问题

There are many ways and resources by which you can build a knowledge-based or expert system. There are even more ways you can waste your time and money (for example, donating to the Starving Authors and Copyeditors Fund, a for-profit organization). However, the Fourth Law of Wisdom states that before you set out on a journey, you should know your destination.

构建基于知识的系统或专家系统有许多方法和资源。浪费时间和金钱的方法更多（例如，向“饥饿作者和校对员基金”捐款，这是一个营利性组织）。然而，智慧第四定律指出，在踏上旅程之前，你应该知道目的地。

Before you build an expert system, you should select an appropriate problem, as discussed in Section 1.6. Like any software project, there are a number of general considerations that should be made before a large commitment of people, resources, and time to a proposed expert system. These general considerations are typical of project management concerns in conventional programs, but must be customized for the special requirements of expert systems. A very high-level view of project development is shown in Figure 6.1. The three general stages of Activity, Product Configuration, and Resource Management have some more specific considerations, shown below. These more specific considerations will be discussed as questions and answers to serve as guidelines for expert systems projects.

在构建专家系统之前，你应该选择一个合适的问题，如第 1.6 节所述。与任何软件项目一样，在向拟议的专家系统投入大量人力、资源和时间之前，应考虑许多一般性问题。这些一般性问题与常规程序中的项目管理关切典型，但必须针对专家系统的特殊要求进行定制。图 6.1 展示了项目开发的高层次视图。活动、产品配置和资源管理三个一般阶段有一些更具体的注意事项，如下所示。这些更具体的注意事项将以问答形式讨论，以作为专家系统项目的指导。

### Selecting the Appropriate Paradigm

### 选择合适的范式

### Why are we building an expert system?

### 我们为什么要构建专家系统？

This is probably the most important question to be asked of any project. The most desirable answer is that the president of the company wants it built. If that's not the case, see if the general advantages of expert systems as described in Chapter 1, Section 2 apply. Most of all, remember only management can authorize the system and technical personnel needed. If you decide to build it on your own time to show the company you were right, and then realize what a great product it is, and decide to quit and form your own company, there is the small matter of that Intellectual Property Agreement you signed. Most IPAs state that whatever you come up with, whether related or not to your job duties, 24x7x52, belongs to the company. In particular, the answer to this question must eventually be given to the owners or stockholders funding development. Before starting, there should be a clear identification of the problem, expert, and users.

这可能是任何项目都应该提出的最重要问题。最理想的答案是公司总裁希望构建它。如果不是这种情况，请查看第 1 章第 2 节中描述的专家系统的一般优势是否适用。最重要的是，请记住只有管理层才能批准系统和所需的技术人员。如果你决定利用自己的时间来构建它，以证明你是对的，然后意识到这是一个多么出色的产品，并决定辞职创办自己的公司，那么你签署的那份知识产权协议就是一个小问题。大多数 IPA 规定，无论你提出什么，无论是否与你的工作职责相关，24x7x52，都属于公司。特别是，这个问题的答案最终必须提供给资助开发的所有者或股东。在开始之前，应明确识别问题、专家和用户。

Note that the singular term expert is used, not plural experts. Just as the best way to guarantee trouble is to have multiple spouses at once, more than one expert will also guarantee trouble. Even the President only sees one doctor at a time, so it's not a matter of cost. Trying to model the expertise of multiple experts in one system is a bad idea. However, modeling the expertise of multiple experts in multiple systems using a blackboard architecture to reach at least a majority opinion is good. This does bring up what the fuzzy term good means. If nine out of ten doctors say the patient will die, the patient will inevitably choose the doctor that offers a treatment for life (unless the patient is really cheap and the treatment costs money). Trying to decide how to rank multiple expert opinions is a daunting task, usually more formidable than building a single expert system for a single expert. So we'll stick with the single-system-single-expert approach in this chapter and leave the multiple-experts-multiple-systems as a class project.

请注意，此处使用的是单数形式 expert，而非复数 experts。正如同时拥有多个配偶是麻烦的最佳保证一样，多个专家也会保证麻烦。即使是总统也一次只看一位医生，所以这不是成本问题。试图在一个系统中建模多个专家的专业知识是一个坏主意。然而，使用黑板架构在多个系统中建模多个专家的专业知识以达成至少多数意见是好的。这确实引出了模糊术语“好”是什么意思。如果十位医生中有九位说病人会死，病人必然会选择提供生命治疗的医生（除非病人非常吝啬而治疗需要花钱）。试图决定如何对多个专家意见进行排序是一项艰巨的任务，通常比为单个专家构建单个专家系统更具挑战性。因此，本章将坚持单系统-单专家方法，并将多专家-多系统作为课堂项目。

Figure 6.1 Project Management Tasks

图 6.1 项目管理任务

![](img/2c460d4de56b7ffaad3834eee20beaa0_372_0.png)

### Payoff

### 收益

What is the payoff?

收益是什么？

This question is related to the first question. However, this question is more pragmatic by asking for a specific return on investment of people, resources, time, and money. The payoff may be in money, increased efficiency, or any of the other advantages of expert systems described in Chapter 1. It is also important to remember that if no one uses the system, there will be no payoff. Because expert systems is different from conventional programming it is more difficult to answer this question.

这个问题与第一个问题相关。然而，这个问题更具实践性，因为它要求对人力、资源、时间和资金的投资有具体的回报。收益可能体现在资金、效率提高或第 1 章中描述的专家系统的其他任何优势上。同样重要的是要记住，如果没有人使用系统，就不会有收益。由于专家系统不同于常规编程，因此回答这个问题更加困难。

### Tools

### 工具

What tools are available to build the system?

构建系统有哪些可用工具？

There are many expert systems tools available today with advantages and disadvantages as discussed in Appendix G. However, this should be taken only as a guide since software tools develop so rapidly. Generally, you can count on an enhancement every couple years in each tool and a major revision every five

当今有许多专家系统工具可用，其优缺点已在附录 G 中讨论。然而，由于软件工具发展迅速，这只应作为参考。通常，你可以指望每种工具每隔几年就有一次增强，每五

