
# 使用 SAS 进行观察性医疗健康数据分析

![](img/fe9ff008f88baacd415148b0b25dd58c_0_0.png)

![](img/fe9ff008f88baacd415148b0b25dd58c_1_0.png)

![](img/fe9ff008f88baacd415148b0b25dd58c_1_1.png)

本手册的正确书目引用格式如下：Faries, Douglas, Andrew C. Leon, Josep Maria Haro, and Robert L. Oberchain. 2010. Analysis of Observational Health Care Data Using SAS*. Cary, NC: SAS Institute Inc.

SAS® Publishing 提供完整的书籍、电子书和电子产品选择，帮助客户充分利用 SAS 软件的潜力。有关更多关于我们的电子书、在线学习产品、CD 和纸质书籍的信息，请访问 SAS Publishing 网站 support.sas.com/publishing 或拨打 1-800-727-3228。

前言 ix

11.4 总结...................................................................... 282

12.1 引言.................................................................................. 287

参考文献 ................................................................................................ 381

# 前言

## 引言

近年来，观察性数据——如真实世界试验、患者登记库和医疗报赔数据库分析——的使用和重要性日益增加。观察性研究产生了真实世界数据——关于治疗或政策在实践中如何运作的信息——这对于实际操作至关重要。此类数据被研究人员和医疗决策者用于评估治疗策略并做出决策。然而，与随机试验相比，针对观察性数据的统计分析技术和标准尚不完善。由于选择偏差等问题，对各种类型观察性数据的文献综述批评其在质量、一致性和报告透明方面的不足。许多决策者对此类数据的低质量分析经验有限，导致了对这类工作缺乏信任。一些研究小组开始提供提高此类分析质量的通性指导。然而，在实施此类方法方面仍然缺乏实践细节。

我们编写这本书的目标是提供一种资源，使研究人员能够进行高质量的观察性数据分析，以透明的方式呈现数据，并基于数据确保准确解读和适当决策。每章包含了背景信息、数据示例、SAS 代码、输出以及针对这些主题的方法指南。鉴于观察性研究的广泛性，潜在用户包括统计学家、健康结果研究人员、流行病学家、医学研究人员、医疗管理人员、统计程序员、教授、研究生以及其他人。

# 本书大纲

本书的主要目标是提供相关信息，允许研究人员对观察性数据进行高质量分析，以透明的方式展示数据，并确保基于数据的准确解读和适当的决策。为了实现这一目标，书中包含了关于横断面和纵向偏差调整通用方法的详细章节，随后是关注费用数据库分析、经济分析和观察性研究设计的较短章节。

第一章概述了分析观察性数据涉及的问题。从统计角度来看，观察性数据分析中最常见的挑战是处理由于缺乏随机化导致的偏差（混杂）。当感兴趣的组未随机化时，它们在许多关键特征上可能存在差异且可能不可比性。标准的统计方法可能会产生关联而非因果推断。本书包含一个包含六章的详细章节，涵盖偏差调整的核心问题。该部分包含了常用的倾向评分方法（通过回归、分层和匹配应用），以及双稳健估计、工具变量和新开发的局部控制等替代方案。此外，还有一个单独章节讨论了处理协变量数据的实际问题。

# 横断面偏差调整：

- 第2章，“倾向评分分层与回归”

- 第3章，“用于估计治疗效应的倾向评分匹配”

- 第4章，“治疗效应的双稳健估计”

- 第5章，“带有缺失值的倾向评分”

- 第6章，“解决选择偏差的工具变量法”

- 第7章，“使用 JMP 的局部控制方法”

纵向真实数据的分析包含了这些挑战，以及患者切换治疗的可能性、时间依赖混杂和删失记录。书的下一部分提供了四种针对纵向真实数据的分析方法的细节：

- 第8章，“用于观察性数据分析的两阶段纵向倾向调整”

- 第9章，“使用边际结构模型对纵向观察性数据的分析”

- 第10章，“结构嵌套模型”

- 第11章，“纵向倾向评分的回归模型”

报赔数据库已成为一个日益增长的研究领域，因为账单数据库提供了访问数千患者数据的直接途径。这些数据库更频繁地用于解决如资源利用、患者结局、治疗成本和临床试验中无法实际解决的安全信息等问题。例如，检测事件需要的比临床试验中通常包含的得多的患者。此外，此类数据可能还可以评估药物组合和患者亚集等问题。本书包含一个提供此类分析通性指导的章节，以及一个演示如何从医疗数据库进行安全性分析的章节：

- 第12章，“开展观察性数据库研究的良好实践”

- 第13章，“使用大型医疗数据库的剂量反应分析”

随着医疗成本的上升成为一个主要问题，使用观察性数据的另一个增长研究领域是成本和成本效益分析。临床试验通常不是评估医疗支付者所承担真实成本的最佳来源——试验有严格的入组标准、合并症限制、多用药限制、合并药物限制以及强制性的随访和程序。因此，观察性数据是这些信息的首选来源。然而，对成本进行适当分析和展示是困难的，最近的文献综述对方法论的一致性和成本报告质量提出了问题¹

¹见 Doshi, J.A., H.A. Glick, and D. Polsky 2006. "Analyses of cost data in economic evaluations alongside randomized controlled trials." Value in Health 9: 334–340.

虽然大部分内容侧重于现有数据的分析方法，但研究人员经常面临设计观察性研究的挑战。最后一部分包含了关于样本量确定以及处理测量偏差和赞助者偏差等更广泛问题的指导：

- 第 17 章，“解决观察性研究中的测量偏差和赞助者偏差”

- 第 18 章，“观察性研究的样本量计算”

## 贡献者

Aristide Achy-Brou, 约翰斯霍普金斯大学

Daniel Almiral, 密歇根大学

Peter Austin, 多伦多大学，临床评估科学学院

Heijing Bang, 康奈尔大学韦尔医学院

John Brooks, 艾荷华州大学

Maria Chiu, 临床评估科学学院

Cynthia Cofman, VA, 达勒姆和杜克大学

William Crown, i3 创新

Peter Davey, 邓迪大学

Marie Davidian, 北卡罗来纳州州立大学

Elizabeth DeLong, 杜克大学

Douglas E. Faries, 礼来美国

Constantine Frangakis, 约翰斯霍普金斯大学

Michelle Funk, 北卡罗来纳州大学

Hassan Ghomaree, 康奈尔大学韦尔医学院

Ron Goeree, 麦克马斯特大学

Michael Gisswold, 约翰斯霍普金斯大学

Joseph Mariao, 巴塞罗那圣神

Don Heicker, 芝加哥大学

Dave Hutchinson, Advanced PCS 健康系统

Sin-Ho Jung, 杜克大学

Zbigniew Kadzila, 礼来

Dennis T. Ko, 临床评估科学学院

Taiyeong Lee, SAS 学院

Andrew C. Leon, 康奈尔大学韦尔医学院

R. Scott Leslie, MedImpact 医疗系统

Chunshan Li, 康奈尔大学韦尔医学院

Xiang Ling, 昂今森

Ilya Linovich, 礼来

Bradley Martin, 阿肯西州大学医学院

Brenda Thomas, Care Scientific

Susan A. Murphy, 密歇根大学

Robert L. Oberchain, 风险效益统计

Xiaoming Peng, 礼来美国

Yongming Qi, 礼来

Paul Stang, 西切斯特大学

David Staez, 巴塞罗那圣神

Jack V. Tu, 多伦多大学临床评估科学学院

Honkun Wang, 弗吉尼亚州大学

Ouhong Wang, 昂今森

Chris Weisen, 北卡罗来纳州大学

Daniel Weitreich, 北卡罗来纳州大学

Andrew Willan, 多伦多大学

xii 前言

Will S. Yancy Jr., 杜克大学

赵宏伟, 德克斯州立大学

## 作者页面

每本 SAS 出版物都有作者页面，包含与作者相关的多个功能，包括简介；即将出版书籍及作者其他作品的描述；联系信息；示例章节链接以及示例代码和数据；活动和额外内容等。

您可以通过 http://support.sas.com/authors 访问作者页面。

所有提供示例代码的书籍字母列表，请参见 http://support.sas.com/bookcode。选择标题以显示书籍的示例代码。

如果您无法通过网站访问代码，请发送电子邮件至 saspress@sas.com。

# 致谢

作者们感谢审稿人员提供的多条质量建议，以改进本文。此外，作者们还要感谢礼来公司的研究顾问 Alex Dmitenko，他为开展这项工作提供了启发。特别感谢 SAS 出版的采购编辑 George McDaniel，他在帮助我们完成这个项目过程中提供的指导和工作。我们还感谢实现这一切的整个 SAS 出版团队。这些人员包括：编辑 Kathy Restivo、执行编辑 Mary Beth Steinbach、技术出版专家 Candy Farrell、封面设计师 Patrice Cherry、设计师 Jennifer Dilley 以及营销专家 Stacey Hamilton 和 Shelly Goodwin。

SAS 提供了丰富的资源，帮助您建立 SAS 技能并探索和应用 SAS 的力量。无论您处于专业环境还是学术环境，我们都有学习产品可以帮助您最大化对 SAS 的投资。

| 类别 | 链接 |
| :--- | :--- |
| 书店 | http://support.sas.com/publishing/ |
| 培训 | http://support.sas.com/training/ |
| 认证 | http://support.sas.com/certify/ |
| 知识库 | http://support.sas.com/resources/ |
| 支持 | http://support.sas.com/techsupp/ |
| 学习中心 | http://support.sas.com/learn/ |
| 社区 | http://support.sas.com/community/ |

如果您对本书有任何意见或问题，可以通过以下方式通过 SAS 联系作者：

请在信函中注明书名。

要查看通过 SAS 出版提供的所有书籍完整列表，请访问 http://support.sas.com/publishing。

SAS 出版新闻：订阅 SAS Publishing News 月刊电子报，通过电子邮件接收所有新 SAS 出版的最新信息。访问 http://support.sas.com/subscribe。

## 引言

第 1 章 观察性研究简介 ............................................3

### 观察性研究简介

Heejung Bang

- 1.1 观察性研究与实验性研究 ................................................................ 3

1.2 观察性研究中的问题....................................................................................... 9

1.3 研究设计............................................................................... 9

1.4 方法 ................................................................................. 10

1.5 报告的一些指南 ................................................................ 13

致谢 ................................................................................15

### 1.1 观察性研究与实验性研究

虽然大部分内容侧重于现有数据的分析方法，但研究人员经常面临设计观察性研究的挑战。最后一部分包含了样本量确定以及处理测量偏差和赞助者偏差等更广泛问题的指导：

- 第 17 章，“解决观察性研究中的测量偏差和赞助者偏差”

- 第 18 章，“观察性研究的样本量计算”

当研究人员设计并执行实验研究时，分配是可以控制的。事实上，观察性研究被称为随机试验。

在 RCT 中主体是随机分配的，而观察性研究观察疾病的发生和进展。

其目的是阐明，在：

观察性研究与 RCT 的优缺点如下：

- Benson, 2000

- Hartz, 2002

- Grimes and Schulz, 2002

- Rubin, 2003

- Park et al., 2007

- Levi et al., 2008

RCT 的主要优点是它是可能的。事实上，研究人员希望减少偏差和潜在的混杂。

观察性研究不使用随机化带来了分析挑战。由于缺乏随机化，治疗组和控制组在许多方面存在差异，因为分配不受研究人员的控制。很难确定差异的具体原因和方式。结果，应用于观察性研究的标准统计技术可能会产生偏估计。事实上，需要强大的额外假设和先进的方法来调整偏差和混杂。此外，当不使用随机化时，对研究背景的理解变得非常重要。（有时，观察性研究是在没有比较计划的情况下进行的——例如评估治疗模式、风险因素和疾病负担。）

另一方面，观察环境更不人工、更现实；人们的生活和行为没有受到限制规则或特定建议的影响，可以更好地观察疾病的发生和进展。因此，这些研究为评估社区中需要治疗的人的治疗效果提供了机会。此外，观察性数据有助于检查治疗的安全性（特别是罕见或后期效应）。如果医疗专业人员等待 RCT 设计和实施，相关信息将需要多年才能可用。因此，医疗保健提供者和政策制定者在短期内必须根据目前的发现采取行动（Ware, 2003）。

# 第1章 观察性研究介绍 5

与瞻性随机对照试验（RCT）相比，医学记录将导致医疗决策中使用观察性数据增加。

在这里，值得提到以各种方式改变我们生活的里程碑式观察性研究。其中，让我介绍两项研究：弗兰明汉心脏研究（FHS）和女性健康计划（WHI）。1948年，FHS在国立卫生研究院（NIH）的指导下启动了一项雄心勃勃的健康研究项目。当时，对心脏病和中风的具体原因知之甚少，但心血管疾病的死亡率自世纪初以来一直在上升，已成为一种流行。这项流行病学研究收集的五十年数据确定了与心血管疾病相关的重大风险，为研究人员基于弗兰明汉发现开展临床试验铺了道路，引发了预防医学的革命，并改变了医学界和大众对疾病起源的观点（http://www.framinghamheartstudy.org）。1991年，NIH还建立了WHI，以解决绝经后女性最常见的死亡、残疾和生活质量下降原因，包括心血管疾病、癌症和骨质疏松。WHI是一项为期15年的工程，也是美国此类最大的预防研究之一。WHI的三大组成部分是：

- 1. 测试经证明的预防方法的随机对照试验（RCT）

- 2. 用于识别疾病预测因素的观察性研究

- 3. 调查健康行为的社区预防研究

其中观察性研究提供了证实RCT获得结果的信息（http://www.nhlbi.nih.gov/whi/）。

## 观察性研究中的问题

### 1.2.1 关联与因果关系

为了研究暴露是否导致结果，我们必须首先理解关联或相关性（意味着一个因素存在时另一个更常见）与因果关系之间的区别。观察性数据产生关于治疗-结果关系的违背直觉的（即与我们的预期或机制认为的运作方式相反）或不一致的结果并非罕见。非随机治疗的典型场景是“指征治疗”。病情较重的人倾向于服用更多、更高剂量的药物（按疾病严重程度进行选择）。结果是，高剂量药物在朴素分析中可能显示出较差的结果。同样，对于被认为有益的治疗或饮食，即使事实并非如此。为什么？这可能是因为与不这样做的人在其他方面有所不同（例如经济状况更好或有额外的需求），他们使用廉价的产品（或服务），因此这些产品可能比昂贵的产品提供更高的满意度。人们可能会天素地得出结论，认为便宜的产品会导致更大的满意度。在这种情况下，将粗略的关联解释为因果关系是不恰当的，因为此类发现可能只是简单的关联。如果对相同的比较进行RCT，可能会得出相反的结果。

# 使用SAS分析观察性健康数据

为什么*因果关系*被认为是重要的？Rose（1985）指出，如果原因可以被消除，易感性就不再重要了。关联因素和相关因素都不具备这种力量。一种治疗方法被认为具有真实效应，如果在所有可能的治疗分配下（包括未给予实验单位的治疗，即与事实相反或反事实的治疗）下所会观察到的值存在差异；Rubin (1978)、Maldonado 和 Greenland (2002) 以及 Hofer (2005)。在研究中，因果关系是使用对照组的基础（Ryetnik et al., 2004）。

反事实效应的想法源于18世纪的哲学家大卫·休谟，他说“我们可以通过观察来定义一个对象的原因……其中如果第一个对象没有，第二个对象永远没有。”休谟的一句引言可能是：“所有关于存在的问题都建立在因果关系之上。”因果关系的反事实概念和随机化逻辑由 Neyman (1923) 和 Fisher (1926) 引入统计学。



让我们通过使用反事实对一个具有治疗和连续结果（例如血压或胆固醇）的RCT建立设定来说明基本概念。让`Z`表示治疗指标，如果分配了活性治疗则`Z`为1，如果分配了对照治疗或安慰剂则`Z`为0。我们假设在每个`Z`水平上，受试者存在一个反事实结果`Y(Z)`。`Y(1)`和`Y(0)`永远不会被同时观察到，因为不可能同时对同一个人进行治疗和不治疗，无法计算个人的治疗效应。选择一种治疗分配，并仅观察分配的值（无论是`Y(1)`还是`Y(0)`）。受试者的治疗效应在概念上定义为不可观测的变量`Y(1)-Y(0)=τ`。（更现实地说，一种替代的随机观点更可行；未知的真实效应可以定义为`E{Y(1)}-E{Y(0)}=`，其中`E`表示期望。）如果它不为，那么治疗对结果就具有因果效应。此外，可以假设在每个水平上都有一个反事实（例如二元的）剂量`D(Z)`。现实中，我们只能看到`d=Z*D(1)-(1-Z*)D(0)`和`y=Z*Y(1)+(1-Z*)Y(0)`。使用观测值构建治疗效应估计器请参见`Bang and Davis (2007)`。

因果关系与关联之间的混淆是健康报告中最大的问题之一，尤其是媒体报道的煽动性发现以及科学界的重大争议。“原因”一词被严重滥用、误用或误解（`Meister, 2007`）。为了确定一个因素与结果之间的关联是否可能是因果性的，`Hill（1995）`提出了以下系列考虑因素：

- 强度 (`Strength`)
- 一致性 (`Consistency`)
- 特异性 (`Specificity`)
- 时间顺序性 (`Temporality`)
- 生物学梯度 (`Biological gradient`)
- 合理性 (`Plausibility`)
- 协调性 (`Coherence`)
- 实验 (`Experiment`)
- 类比 (`Analogy`)

# 第1章 观察性研究介绍

尽管这些考虑因素（经常被错误地称为因果准则，`Phillips and Goodman, 2004`）对流行病学思维产生了持久影响。`Hill`对其用处表示了矛盾态度，并说：“我的任何观点都为因果关系假设提供不可辩驳的证据，也没有观点可以被视为必要条件。”对于因果关系的时间顺序性（即原因必须在结果之前），其他条件对于判断观察到的关联是否为因果既不是必要的也不是充分的（`Rothman and Greenland, 1998`）。`Rothman`和`Greenland (2005)`得出流行病学中没有因果标准，认为：“流行病学中的因果推断被视为对效应的测量练习，而不是根据准则来判断效应是否存在的过程。”

## 1.2.2 偏倚与混杂

选择偏倚和混杂是内部有效性的两个主要威胁。实际上，它们是密切相关的概念，因为混杂会导致选择偏倚。当单位或个体被选中参与研究或被分配治疗的概率不同，且该个体的特征与结果混杂时，就会发生选择偏倚。结果是任何结论可能是错误的且不可推广的。选择偏倚分为两种：已准确测量的（测量混杂因素），称为选择偏倚；以及未测量但怀疑是因果的。

**混杂**可能导致对因变量（结果）与自变量（例如风险或暴露）之间关联性的因果错误结论。如果没有另一个变量的数据无法有效估计感兴趣的参数（例如风险或优势比），那么该变量就是混杂因素。不幸的是，理解和混杂是困难的概念。每个概念都有各种定义，但文献中的大多数定义都是性质的描述。它们的定义似乎在演变。关于这一问题的更严格、深入的讨论，请参见`Greenland`和`Cook (1981)`、`Robins`和`Morgenstern (1987)`以及`Greenland`等`(1999)`。

让我举几个混杂的现实例子。饮酒者患肺癌率高于不饮酒者。酒精会导致肝癌，但目前未知会导致肺癌。什么解释了这种关联？混杂因素可能是吸烟：饮酒者烟吸得更多，而吸烟会导致肺癌。为了评估混杂对肺癌可能的影响，我们可以在吸烟水平内比较饮酒者。例如，白发看起来是心脏病的风险因素。如果年龄未知，白发的人发生心脏病的的概率比其他人高。然而，如果两人年龄相同，但只有一个人白发，那么白发的人风险不太可能增加。最初的关联是虚假的白发，因为在模型中加入年龄后，不再是独立的风险因素（`Brotman et al., 2005; Gotto, 2007`）。在第三个例子中，1930-1939年间德国奥登堡的人口增长与中风数量之间似乎存在相关性，但我们很难相信

# 使用 SAS 对观察性数据进行分析

杀死鹳鸟会降低人类的出生率！在这种情况下，第三个变量可能是时间（`Box et al., 1978; Davidian, 1998`）。

总而言，混杂是一个复杂的过程，其中多个（已知和未知的）因素会影响结果，因此标准的统计方法（如回归分析或分层分析中使用的方法）不能完全解决这一问题。此外，严格来说，目前还没有针对混杂的统计检验，尽管许多人认为有。`Pearl (2000)`认为，混杂变量不能仅通过统计学概念来定义；必须具备一些因果假设。

## 1.2.3 可重复性与第一类错误

可重复性（即希尔的一致性）对于随机对照试验（RCTs）而言，对于对于观察性研究一样，都是一个非常重要的科学概念；本质上，它意味着如果在另一项研究中测试相同的假设，预计特定研究的结果将再次发生。偶然无法解释这种预期。“关联”（Association）是一个强有力的词，应该留给那些不仅仅是偶然可以解释的变化（`Dunn, 2004`）。无法重复的科学发现应当立即丢弃。可重复性的重要性如何强调都不为过。具有显著性或预测性但不可重复的结果将误导公众，导致时间和资源不必要的浪费，并且无法为研究人员或科学家提供任何服务。

关于观察性研究可重复性的文献观点不一（`Benson and Hartz, 2002; Ioannis, 2005`）。`Austin`等人`(2006)`证明，对显著性的寻找会引导研究人员进入未知领域。事实上，对寻找显著性的建模、对新奇性的追求、忽略多重假设检验、混淆关联与因果关系，以及对这些规范缺乏兴趣，导致了大量无产出的结果（`Freeman, 2008; Breslow`）。我们目前拥有许多信誉较低的研究发现，重复和严谨评估变得与发现同样重要，甚至比发现更（`Ioannis, 2006`）。对于希望确立自己观察性研究专家的医疗研究人员来说，一个审慎的格言似乎是“重复或灭亡”或“验证或灭亡”，而不是“发表或灭亡”。

虽然一些观察性数据是先验设定的，但其他一些需要在事后基础上开发——即在实际数据分析期间（`Gelman and Hill, 2006`）。如果根据数据回溯性地构建，那么没有任何分析是真正前瞻性的。基于主要假设的发现比来自二次分析或通过事后分析发现的发现要强大得多，因为二次分析的世界是如此巨大。合理性必须以怀疑的态度来看，因为人类的想象力似乎能够为任何出乎意料的事物找到理由（`Ware, 2003`）。

即使是设计最精密的观察性研究也可能存在缺陷和模糊性，因此重复是必要的。在尝试重复发现时，应尝试在可能影响原始研究的偏倚估计估计治疗效应（`Rosenbaum, 2005`）。`Lindsay`和`Ehrenberg (1993)`认为，“重复不需要也不应该是完全意义上的重复”。相反，他们认为重复“可以被设计为扩展先前结果的范围，从而得出更有力的泛化结论”。证据的强度来自于尽管条件存在差异但获得了相同的结果。这些作者为重复性研究的设计提供了一些策略。

# 第 1 章 观察性研究导论

在本章中，我强调了“因果”的重要性。然而，关于因果的不同视角对读者将是有用的。`Taleb (2001)`和`Lund (2007)`认为，社会需要更多关注随机性。社会希望为每一个发生的事件找到原因。极端的飓风或今年的情况真的是是因为厄尔尼诺现象和/或全球变暖吗？你城市今年减少的两起谋杀案是归于新的警用巡逻车（报纸标题），还是归于严重的家庭纠纷（随机性？）尽管我们尽可能地寻找原因，但某些现象可以通过随机性和/或具有非零概率的极端事件来解释。

## 1.3 研究设计

随机化解决了选择偏倚和混杂问题，但未能解决模型设定错误。

由于选择和实施合适的因果推断方法并非易事，许多研究人员通过相对简单的统计程序分析观测数据，并根据这些分析得出结论。将随机对照试验（RCTs）视为 RCT，将观测性研究视为观测性研究是理想的。纵向观测性研究中治疗效应的分析变得更加困难，因为变量之间关系（即治疗、混杂因素和结局）随时间的动态变化增加了额外的复杂性。就像现实生活中的观测性研究可能出现多种定性和定量上都不同的场景一样。在缺乏统一分析解决方案的情况下，每个特定场景都需要根据数据结构和可用性、治疗操作/机制以及所需的假设来量定制方法。观测数据分析的关键组成部分可以是：

- 因果知识
- 针对给定数据识别最合适的方法
- 针对特定情况对方法进行适当调整
- 彻底的假设检验以及严谨的敏感性分析

从传统的统计分析转向多变量数据的因果分析必须进行范式转变（`Pearl, 2000`）。

在过去的至少二十里，利用观测数据建立因果关系的方法论已成为多个科学学科的活跃领域，包括（生物统计学、流行病学、经济学和社会科学）。得益于统计技术的进步，用于观测数据的因果方法变得比以往任何时候都更有前景。如果能从观测或次级数据分析中推导出因果关系，就可以节省资源。今天，强调从 RCT 和观测性研究中获得一致或可比的结果。这种结合可能会得出治疗有效性的确定性结论。

### 1.4.2 统计方法

在许多应用中，建议遵循规则：

- 规则 1：定义你的研究问题。在科学问题形成良好之前，不要收集数据！
- 规则 2：考虑 RCT 或其变体是否比观测性研究更适用于你的目标，在观测研究中，分组随机试验（`Cornfield, 1978; Hannan, 2006`）、准随机试验（`Shashid et al., 2002`）和实际试验（`Tunis et al., 2003; MacPherson, 2004`）可以作为选项。在治疗/暴露效应的因果推断方面，要分析实验陷阱和设计陷阱（`Petti, 1998; Rubin, 2008`）。
- 规则 3：当 RCT 不是选项且将进行观测性研究时，在充分理解研究科学背景的情况下，选择适用于观测研究的合适设计和统计方法。

## 使用 SAS 进行观测健康数据分析

这里总结了常用的观测数据统计工具：

倾向性评分（PS）是在给定观测协变量的情况下，接受治疗而非接受对照的条件概率。这个简单的汇总得分可以控制许多变量，通常被称为平衡分。它可以用于分分层（即分类）、基于模型的调整、匹配或这些技术的结合（`Rosenbaum and Rubin, 1983`）。

工具变量（IV）

`IV`是一个与暴露相关但与结局无关的因素（见第 6 章）。例如，香烟的大小（此处指烟量或规格）可能会影响孕妇的吸烟概率，但没有理由相信它直接影响婴儿的出生体重（`Greenland, 2000; Wunsch, 2007; Moffitt, 2003`）。因此，`IV`可以改变个体的暴露，并且仅通过这种影响改变感兴趣的结局（`Wright, 1928; Angrist et al., 1996`）。

边际结构模型（MSM）和结构嵌套模型（SNM）

`MSM`通过逆概率治疗加权生成伪值，使得潜在的混杂因素不再是混杂因素。在 RCT 中，`MSM`也可以用于在存在时间依赖混杂因素的情况下估计时间依赖暴露的因果效应，这些因素在纵向研究中受到先前暴露的影响。`SNM`是`MSM`的替代方案，通过`g`估计法（`g-estimation`）估计参数（`Robins, 1999; Robins et al., 1996`）。

在本书的后续章节中，详细介绍了这些和其他用于观测数据分析方法。实施各种基于 PS 的调整的具体介绍将在第 2 至 5 章中给出。`IV`调整见第 6 章。处理时间依赖混杂和随时间变化的治疗的纵向分析数据方法（如`MSM`和`SNM`）将在第 8 至 11 章中描述。每章都描述了如何使用`SAS`实现新开发的处理观测数据复杂性的方法。选择`SAS`作为本书的分析软件工具是因为它是各种研究人员常用的统计分析工具，并具有处理此类方法复杂性的灵活性。虽然不存在这些统计方法的预设程序，但每章提供的代码可能允许相对容易地实现这些方法。

处理偏倚和混杂的特征描述和方法论在不同学科传统上存在差异。在社会科学和经济学中，基于`IV`方法占据主导地位。识别`IV`是成功的关键，但并不清楚如何识别此类变量。相反，在公共卫生和医学（例如流行病学和生物统计学）中，选择偏倚通常被视为混杂，流行的方法通过显式使用观测混杂因素进行适当调整，如`PS`和`MSM`方法（`Hogan and Lancaster, 2004`）。统计学家、流行病学家和经济学家经常对相似的话感兴趣，但他们通常使用不同的语言来解释结果，这可能会产生障碍。一些研究人员可能会尝试弥合这一鸿沟。一些研究人员可能也会尝试弥合这一鸿沟（`Gunasekara et al., 2008`）。

最近，已有一些尝试处理特定的治疗场景（`Murphy, 2003; Moodie et al., 2007`）和非随机化伴随（`Wu et al., 2008`）。

### 1.4.3 敏感性分析的重要性

即使在使用了新方法后，仍然存在一些问题和怀疑：我们可以相信因果估计吗？我们有多确定？是否存在未解释的偏倚？如果未观测混杂因素被测量和调整，结论会有什么变化？

由于因果推断涉及做出可测试或不可测试的假设，因此假设的合理性和验证至关重要。在实践中，我们不能期望任何假设都成立。未观测混杂的缺失使得经济学家不愿采用基于`PS`或`MSM`的方法，依赖`IV`。相反，一些流行病学家怀疑 是否只是幻想（`Hernán and Robins, 2006`），甚至经济学家也建议谨慎（`Heckman, 1995`）。

偏倚的幅度取决于偏离模型的程度，但偏差的大小可以通过敏感性分析来解决。自从`Cornfield`等人（`1959`）提出第一个检测隐性偏倚的敏感性分析以来，已经提出了各种定量处理敏感性的方法策略。这里不讨论具体的方法。特别是`Brumback`等人（`2004`）说明了即使在`Hernán`等人（`2002`）应用最先进的方法处理数据后，敏感性分析的重要性。他们的重新分析对未观测混杂相当敏感，提供了一个令人警醒的信息：怀疑因果估计的有效性和可信度是合理的。医疗研究人员的良好态度应该是只依赖一种方法。虽然通常没有进行敏感性分析，但它们应该是所有因果分析的关键组成部分。

偏的另一个来源是模型设定错误。由于因果建模受到多种模型类型的影响，建议使用双稳健估计。见第 4 章，`Lunford and Davidian (2004)`以及`Bang and Robins (2005)`。

面向流行病学家、统计学家、研究人员以及负责观察性研究开展和结果传播的期刊编辑：

- 非随机设计评估的透明报告 (`TREND`) (`http://www.trend-statement.org/`)
- 流行病学观察性研究报告规范 (`STROBE`) (`http://www.strobe-statement.org/`) (`von Elm`等人，`2007`)
- 良好的流行病学实践：流行病学研究的适当规范 (`http://www.iatemp.com/pdfs/GEPNov07.pdf`)

这些指南可以被视为随机对照试验（RCT）的报告对照试验报告标准（`CONSORT`）在观察性研究中的对应版本 (`http://www.consort-statement.org/`) (`Begg`等人，`1996; Moher`等人，`2001`)。

其他重要的指南还包括：

- 流行病学观察性研究的荟萃分析 (`MOOSE`) (`Stroup`等人，`2000`)
- 药典评价与实践指南 (`http://www.pharmacopeia.org/resources/guidelines.08027.cfm`)
- 药物经济学指南 (`http://www.ispor.org/workpaper/adpanel/index.asp`)
- 药物、剂量和疫苗研究指南 (`http://www.rcrnxr.org/ISPE_good_epidemiology_`)

由于观察性研究的荟萃分析更容易产生偏倚（研究内、研究间以及其他），因此进行敏感性分析（`Rosenthal, 1979; Duval and Tweedie, 2000; Copas and Shi, 2000`）以及适当解释结果（`Shapiro, 2004; Young and Bang, 2004; Phillips, 2004; Fisher`等人，`2007`）尤为重要。此外讨论了观察性研究荟萃分析在药物开发和监管过程中的潜在作用（`Berlin and Colditz, 1999; Temple, 1999`）。

然而，我们应该建议所有这些声明都是通用指南，并没有为数据分析提供特定的统计方法，因为观察性研究的分析非常复杂，分析方法非常先进，和/或我们仍然需要在方法上寻求共识。希望这项工作有助于对针对真实数据的适当统计方法产生更深入的理解和一致的应用。

作者对本项目贡献的支持源于康奈尔医学院临床与转化科学奖（`NIH UL1-RRO24996`）。作者在威尔-康奈尔医学院教授一门“观察性数据的统计方法”课程。作者感谢 `Paula Trushin`、`Stan Young`、`Varsha Shah`、`Yolanda Barron`、本书的编辑以及两位匿名审稿人阅读手稿并提供宝贵意见。此外，作者还感谢 `Sander Greenland`、`John Kaufman` 和 `Michael Oakes` 在观察性研究的各种课题上的智力交流和学术建议。

`Aliagaga, M., and B. Gunderson. 1998. Interactive Statistics. Upper Saddle River, New Jersey: Prentice Hall.`

`Angrist, J. D., G. W. Imbens, and D. B. Rubin. 1996. "Identification of causal effects using instrumental variables." Journal of the American Statistical Association 91: 444–455.`

`Austin, P. C., M. M. Mandmani, D. N. Juniper, and J. E. Hux. 2006. "Testing multiple hypotheses resulted in spurious associations: a study of astrological signs and health." Journal of Clinical Epidemiology 59: 964–969.`



第1章 观察性研究引言

## 摘要

Bang, H., and C. E. Davis. 2007. "On estimating treatment effects under non-compliance in randomized trials: are intent-to-treat or instrumental variables perfect solutions? Statistics in Medicine 26: 954–964.

Bang, H., and J. M. Robins. 2005. "Doubly robust estimation in missing data and causal inference models." Biometrics 61: 962–972.

Begg, C., M. Cho, S. et al., 1996. "Improving the quality of reporting of controlled trials. The CONSORT statement." The Journal of the American Medical Association 276 (8): 637–639.

Benson, K., and A. J. Hartz. 2002. "A comparison of observational studies and randomized, controlled trials." New England Journal of Medicine 342: 1788–1888.

Berlin, A., and Graham A. Coliditz. 1999. "The role of meta-analysis in the regulatory process for food, drugs, and devices." The Journal of the American Medical Association 281 (9): 830–834.

Box, O. E., W. G. Hunter, and J. S. Hunter. 1978. Statistics for Experiments: Introduction to Design, Data Analysis, and Model Building. New York: John Wiley & Sons, Inc. Breslow, N. E. 2003. "Are statistical contributions to medicine undervalued?" Biometrics 59: 1–8.

Brotman, D. J., Walker, M. S. Lauer, and R. G. O’Brien. 2005. "In search of fewer risk factors." Archives of Internal Medicine 165: 138–145.

Brumback, A. M., J. M. Hernán, and J. M. Robins. 2004. "Sensitivity analysis for unconfounded." Statistics in Medicine 23: 749–767. (注：原文此处可能存在引用错误，已按逻辑对齐)

Christfield, D. J., Rice, R., and Greenland, S. 2004. "Risk factors, confounding, and." Archives of Internal Medicine 65 (6): 868–875.

Cochran, W. G. 1965. "The arrangement of." Ministry of Agriculture 33: 1. Journal of the Royal Society (Series A) 128: 234–266.

Concato, J., Shah, R., and Horwitz, J. 2006. "Randomized, controlled trials, and." New England Journal of Medicine 342: 1887–1892.

Copas, J. B. and Shi, S. 2000. "Trim and fill: sensitivity analysis." Biometrics 21: 247–262.

Cornfield, J. 1978. "Randomization by." Journal of Epidemiology 10: 301–312.

Duval, S. and Tweedie, R. 2000. "Instrumental variables for causal inference." Biometrics 55: 455–463.

Fisher, R. A. 1926. "The association of." Proceedings of the Royal Society 58: 295–300.

Freedman, D. A. 2008. "Oasis or mirage?" Chance 21: 59–61.

Freedman, D. A., and Greenland, S. 2005. "Hormone replacement therapy does not save- lives." Biometrics 61: 918–920.

Gelman, A., and Hill, J. 2006. "Data Analysis Using Regression and Multilevel Models." New York: Cambridge.

Gotto, A. M. 2007. "Role of C-reactive protein in coronary risk." American Journal of Cardiology 99: 718–725.

Greenland, S., Robins, J. M., and Pearl, J. 1999. "Confounding and collapsibility in causal inference." Statistical Science 14: 29–46.

Greenland, S. 2000. "An introduction to instrumental variables for epidemiologists." International Journal of Epidemiology 29: 722–729.

Grimes, D. A., and Schulz, K. F. 2002. "Bias and causal associations in observational research." The Lancet 359: 248–252.

Hannan, P. J. 2006. "Experimental social epidemiology: Community trials." In Methods of Epidemiology, 341–369. Edited by J. M. Oakes and J. S. Kaufman. San Francisco: Jossey-Bass/Wiley.

Heckman, J. J. 1995. "Instrumental variables: a causation tale." NBER Working Paper No.1815. Available at `http://rn.com/abstract=225094`.

Hernán, M., Brumback, A. B., and Robins, J. M. 2002. "Estimating the causal effect of zidovudine on CD4 count with a structural model for repeated measures." Statistics in Medicine 21: 1689–1709.

Hernán, M., and Robins, J. M. 2006. "Instruments for causal inference: an epidemiologist's dream." Epidemiology 17 (4): 360–372.

Hill, A. B. 1965. "The environment and disease: association or causation?" Proceedings of the Royal Society of Medicine 58: 295–300.

Höfler, M. 2005. "The Bradford Hill considerations on causality: a counterfactual perspective." Emerging Themes in Epidemiology 2 (11).

Hogan, W. J., and Lancaster, T. 2004. "Instrumental variables and inverse probability weighting for causal inference in longitudinal observational studies." Statistical Methods in Medical Research 13: 17–48.

Ioannidis, J. P. A. 2006. “研究结果的演变与转化：从实验室到何处？”PLoS Clinical Trials 1 (7): e36.

Levi, M. G., Koving, S. C. Cgetier, M. Vermeulen, H. R. Büller, and F. R. Rosendal. 2008. “接受维生素 K 拮抗剂患者的出血，这些患者本应根据抗凝治疗指征被排除在外。”Blood 111 (9): 4471–4476.

Lindsay R.M., and A. S. C. Ehrenberg. 1993. “重复研究的设计。”The American Statistician 47: 217–228.

Little, R., and D. B. Rubin. 2000. “通过潜在结果法分析临床和流行病学研究中的因果效应：概念与分析方法。”Annual Review of Public Health 21: 121–145.

Lunford, J. K., and D. Davidan. 2004. “通过倾向评分估计治疗效应进行分层和加权：一项比较研究。”Statistics in Medicine 23: 2937–2960.

Lund, R. 2007. “白天鹅的复仇。”The American Statistician 61: 189–191.

MacPherson, H. 2004. “实用性临床试验。”Complementary Therapies in Medicine 12 (2–3): 136–140.

Maldonado, G., and S. Greenland. 2002. “估计因果效应。”International Journal of Epidemiology 31: 422–429.

Meister, K. 2007. “区分关联与因果：：记者的指南。”来源于 `http://www.acsh.org/publications/pubid.1629/pub_detail.asp`

Mietinen, O., and E. F. Cook. 1981. “混杂因素：证据与检测。”American Journal of Epidemiology 114: 593–603.

Moffitt, R. 2003. “人口研究中的因果分析：经济学家的视角。”Population and Development Review 29: 448–458.

Moher, D., K. F. Schulz, and D. Altman. 2001. “CONSORT 声明：改进平行组随机试验报告质量的修订建议。”The Journal of the American Medical Association 285 (15): 1987–1991.

Moodie, E. E., M. S. Richardson, and D. A. Stephens. 2007. “揭示最优动态治疗方案的迷雾。”Biometrics 63: 445–457.

Murphy, S. A. 2003. “最优动态治疗方案。”Journal of the Royal Statistical Series, B (Statistical Methodology) 65: 331–366.

Neyman, J. 1923. “论概率论在农业实验中的应用。”选自《论文原理》，第9节，译于 Statistical Science (1990) 5: 465–480.

Park, J., H. Bang, and I. Cachette. 2008. “临床试验中的盲法，是时候做得 better。”Complementary Therapies in Reasoning and Innovation 16 (3): 121–123.

Pearl, J. 2000. 因果关系：推理与推断的模型。新版：剑桥大学出版社。

Petitti, D. B. 1998. “激素替代疗法与心脏病预防：基于观察的实验。”The Journal of the American Medical Association 280 (7): 650–652.

Petitti, D. B., and D. A. Freedman. 2005. “邀请评论：带有统计学调整的流行病学家能走多远？”American Journal of Epidemiology 162: 415–418.

Phillips, C. V. 2004. “现场的发表偏倚。”“奥斯汀·布拉德福·希尔爵错过的教训。”Epidemiological Perspectives and Innovations 1: 3.

Rimm, A. A., and M. Mortin. 1978. “作为宗教的临床试验。”Biomedicine: The European Journal of Clinical and Biological Research 28: 60–63.

Robins, J. M. 1999. “作为因果推断工具的边际结构模型与嵌套模型。”选自《流行病学统计学：环境与临床试验》。M. E. Hollar 和 D. Berry 编。IMA 116: 95–134。纽约：Springer-Verlag.

Robins, J. M., and H. Morgenberg. 1987. “混杂因素的基础。”Computers and Mathematics with Applications 14: 866–919.

Robins, J. M., M. A. Hernán, and B. Brumback. 2000. “边际结构模型与因果效应。”Epidemiology 11: 550–560.

Rose, G. 2001. “流行病学中的随机性。”Epidemiology 30: 427.

Rosenbaum, P. 2005. “观察性研究。”Encyclopedia of Statistics 3: 145.

Rosenbaum, P., and D. B. Rubin. 1983. “倾向评分在观察性研究中的作用。”Biometrika 70: 41–55.

Rosenthal, R. 1979. “抽屉问题。”Psychological Bulletin 86: 638–641.

Rothman, K. J., and S. Greenland. 1998. 现代流行病学。第2版。Lippincott.

Rothman, K. J., and S. Greenland. 2005. “流行病学中的混杂因素。”American Journal of Public Health 95: 144–150.

Tunis, S. R., D. B. Stryer, and C. M. Clancy. 2003. “增加临床决策的价值。”The Journal of the American Medical Association 290: 1624–1632.

Vandenbroucke, J. P., E. von Elm, D. G. Altman, P. C. Götzche, C. D. Mulrow, et al. 2007. “加强观察性研究报告（STROBE）：解释与说明。”PLoS Medicine 4 (10): e297.

von Elm, E., D. G. Altman, M. Egger, S. J. Pocock, P. C. Götzche, et al. 2007. “观察性研究报告（STROBE）声明：指南。”PLoS Medicine 4 (10): e296.

Ware, J. H. 2003. “国家肺气肿治疗试验——证据有多强？”New England Journal of Medicine 348: 2055–2056.

Wright, P. G. 1928. 动植物油税。纽约：Macmillan.

Wu, C. O., X. Tian, and H. Bang. 2008. “用于纵向研究中随时间干预效应的变系数模型。”Statistics in Medicine 27: 3042–3056.

Wunsch, G. 2007. “混杂与控制。”Demographic Research 16: 97–120.

Young, S. S., H. Bang, and D. Kennedy. 2004. “重审抽屉问题/回复。”Science 306: 1133–1134.



在非随机研究中，比较不同干预措施的有效性是困难的，因为干预措施之间存在基线差异。倾向评分是调整此类差异的合适方法，因此可以获得无偏的有效性估计。在本章介绍了分层法和回归法，这两种常用的倾向评分方法。为了说明问题，本文使用分层和回归倾向评分方法，对一项比较两种抗抑郁药物治疗效果的观察研究数据进行了分析。

# 2.1 引言

医学研究的主要目标之一是阐明干预或治疗与健康结果之间的因果关系。随机临床试验（RCTs）是设计治疗效益的金标准（Grimes and Schulz, 2002）。然而，其开展的受控环境限制了结果在日常实践中的推广性（Rothwell, 2005）。此外，出于伦理或实际原因，在某些情况下这些试验是不可行的。观察性研究被认为是 RCT 的补充，因为它们旨在代表真实的临床状况（McKee et al., 1999）。这类研究的设计最大化了外部效度，但通常是以牺牲一定程度的内部效度为代价。

在 RCT 中，治疗对结果的影响通常被认为是因果性的，因为接受不同治疗的患者被认为是可交换的（即：除了所评估的干预外，它们的特征预期是相同的）；然而，在观察性研究中，可交换假设并不成立，因为患者被赋予不同的药物恰恰是因为他们在预后因素存在差异（Hernán and Robins, 2006a）。因此，在分析观察性研究时，需要使用常用的统计方法来减少混杂。

# 2.2 倾向评分：定义与原理

1983 年，Rosenbaum 和 Rubin 开发了倾向评分的概念，作为传统多元回归建模的替代方案，用以估计观察性研究中干预或治疗的效果。倾向评分的目标是平衡研究组（两组：治疗组和对照组）之间的观测协变量，以模拟随机研究的情况（Joffe and Rosenbaum, 1999）。

为了正式定义倾向评分的概念，我们需要一些符号。令 `X` 代表研究对象（在分配治疗之前）的观测协变量，`Z` 代表受试者的治疗指数（`Z=1` 表示治疗，`Z=0` 表示未治疗）。那么，倾向评分是在给定观测协变量的情况下治疗的条件概率，即 `PS(Z=1|X)`。

倾向评分具有若干理论属性，这些属性在其他地方得到了严密的证明（Rosenbaum and Rubin, 1983），因此在此不再给出。尽管如此，倾向评分如何实现平衡的洞察是可见的。在平衡的双臂随机研究中，对于每个 `X`，每个患者的倾向评分都等于 1/2（即：具有不同观测协变量的个体接受治疗的概率相同，且反之，观测协变量的每个可能值在两个组中发生的概率也相等）。通常在观察性研究中，由于观测协变量 `X` 中包含某些倾向特征，某些个体更有可能接受治疗而不是作为对照，或者 `PS-X > 1/2`。类似地，其他个体更有可能是对照组而不是接受治疗，或者 `PS-X < 1/2`。因此，在分析观察性研究时，需要应用常用的统计方法来减少混杂。因此，在使用倾向评分模型时，是关键的，以确保观测协变量的每个可能值在两个组中发生的概率是相似的。

通常，观察性研究中的倾向评分是未知的，因此必须从数据中估计。有几种方法（Setoguchi et al., 2008; Woo et al., 2008）：

- `probit` 回归
- 判别分析
- 分类回归树
- 神经网络
- 广义加性模型

然而，它们最常用逻辑回归估计。逻辑回归的因变量是 `Z`（`Z=1` 为进入治疗组的事件），自变量是观测协变量 `X`。这些变量可以是分类的或连续的。

尽管常用倾向评分，但关于构建倾向评分模型的细节（即哪些变量应包含在模型中）指导很少。Weitzen 等（2004）调查了文献中使用的方法并发现多种方法——包括简约法、显著性检验、逐步法；先验选择以及拟合良好检验。进一步的研究（Weitzen et al., 2005）并未推荐拟合良好检验。常见的建议是倾向于包含，以避免遗漏混杂变量。也就是说，所有与结果和暴露相关的协变量（即使 p 值大于 0.05），并对连续变量考虑非线性形式。这种建议是因为利用的是预测值，而不是模型的参数估计，因此过度参数化和共线性等建模问题不被认为是关键的。

虽然建模倾向评分的最佳方法没有完全共识，但普遍认为最重要的问题是倾向评分在组间是否实现了平衡。事实上，D’Agostino 和 D’Agostino (2007) 指，“倾向评分建模的成功取决于治疗组和对照组之间是否实现了前治疗特征的平衡。”

在- 在实践中，我们经常利用协变量的预设，然后进行敏感性分析。在本章中，我们关注的不是建模，而是评估倾向调整对治疗组实现平衡的方法（见第 2.5 节）。

为了增加分析的可信度，Rubin (2007) 建议在获取结果数据之前完成倾向评分的估计。这样，就可以保证倾向模型的选择不受其对最终分析的影响。事实上，研究人员并没有使用各种倾向评分模型运行多次分析，并选择最终为研究者产生最理想结果的模型。这种完成倾向评分建模的方法并不意味着不需要彻底的敏感性分析，但在我们看来，对于前瞻性观察研究来说是一种很有方法。

此外注意，如果比较多种治疗，可以通过拟合多元逻辑回归估计每种治疗的倾向评分，选择一种治疗作为参考类别（Imbens, 2000）。

# 2.4 使用倾向评分估计治疗效应：分层与回归调整

一旦估计了倾向评分，就有多种方法可以使用它们来控制混杂。这些包括分层、多变量回归模型中作为协变量的回归调整以及其他方法（Austin and Mandami, 2006; D’Agostino, 1998; Rosenbaum and Rubin, 1983）。在本章中，我们重点关注前两种方法。倾向评分匹配将在第 3 章介绍。

在倾向评分分层中，根据估计的倾向评分将受试者分为不同的组。根据倾向评分的分位数分为五组是常见的做法，因为研究发现五组可以消除大约 90% 的混杂变量偏倚（Cochran, 1968）。当样本量较大时（例如在医疗数据库分析中），更多的倾向评分组会使组内患者产生更大的异质性。这可能导致倾向组内特定治疗的样本量较小或为零。虽然目前没有关于倾向组最佳数量明确指南，但应该考虑这些权衡和分析，以确保结果对倾向组数量的合理选择不敏感。

一旦患者根据倾向评分被分为同质分层，就会在每个五位数内估计治疗差异，并将五个估计的治疗效应合并为一个总治疗效应。其基本思想是，在分层中，通过比较治疗组与相似患者进行验证性比较——“相似”被定义为倾向评分相似的患者。

在倾向评分回归调整中，通过多变量回归模型估计治疗效应，该模型包含治疗指标 `$Z$` 以及倾向评分本身（要么作为连续协变量，要么根据倾向评分五位数作为分类协变量）。对于两种以上的治疗方法，必须将参考治疗的倾向评分纳入多变量回归模型中，可以作为连续协变量或通过使用倾向评分分位数作为类别的分类协变量。

尽管该领域缺乏来自理论或模拟研究的详细指导，但其他研究人员会在多变量回归模型中加入额外变量！（D’Agostino and D’Agostino, 2007; Cadrette et al., 2008）。D’Agostino and D’Agostino (2007) 建议拟合一个模型来估计治疗效应，该模型包含一部分被认为是最潜在混杂因素的患者特征。为了增加治疗效应的精确性（就像在随机试验的回归模型分析中所做的那样），以及倾向评分建模后可能存在的任何残差不，应该包含与结果指标有强相关性的变量，或在倾向评分后有显著残差的变量。倾向评分分层分析的类似扩展是为每个分位数分层使用回归模型。这些扩展对应于第 4 章提出的双重稳健方法（另见 Luceford and Vivian, 2004）。

无论选择倾向评分分层还是倾向评分回归，在执行结果分析之前，都应对倾向调整进行彻底评估。倾向评分的主要功能是解释混杂。因此，如第 2.3 节所述，使用倾向评分应该在所比较的治疗组之间产生协变量的平衡。评估倾向调整产生的平衡的具体方法描述在第 2.5 节中。

最后，敏感性分析至关重要。从观察性数据得出因果推断需要假设（例如，无未测混杂因素、正性），并且应该检查这些假设。例如，虽然永远无法证明没有缺失的混杂因素，但可以考虑依赖此假设的工具变量进行分析（如第 6 章所述）。然而，为了使用工具变量获得无偏估计，必须满足其他几个条件（Herin and Robins, 2006b）。另一种选择是测试结果对未测混杂的敏感性（Schneweiss, 2006；另见第 2.6.1 节）。检查每个治疗组的倾向分布有助于评估倾向（每种治疗的正性选择或协变量的平衡）。治疗组内协变量平衡的敏感性可以通过倾向匹配等方法进行评估，这种方法可以提供平衡，但可能存在样本量的权衡（Austin et al., 2007a）。

总之，倾向评分分层或回归分析不仅仅是估计倾向评分和运行调整模型。质量分析包括对倾向评分产生的平衡进行评估、统计假设的评估、敏感性分析以及报告的透明度。透明度很重要，因为读者应该能够理解所执行分析的质量，知道做了什么决策、何时做出以及为什么做出。

# 2.5 倾向评分的评估

在随机研究报告中，通常会显示一张比较治疗组和对照组之间最重要的治疗前协变量分布的表格，以评估随机化是否有效。由于倾向评分的目的是是非随机观察性研究中创建准随机实验，如果实现了准随机化，也可以采取类似的方法。如第 2.3 节所述，倾向评分调整成功的关键评估是证明倾向评分在比较治疗之间产生了平衡。

评估倾向模型产生的平衡有多种方法。Austin and Mandani (2006) 和 Austin (2008) 提供了方法的良好总结。从高层次来说，方法包括：

- 1. 评估治疗组之间协变量的标准化差
- 2. 评估倾向评分分布
- 3. 比较治疗组之间协变量的分布
- 4. 评估拟合优统计量

具体而言，对于倾向评分分层分析，由于治疗比较是在每个倾向评分分层内进行的，因此重点是评估分层内的平衡。倾向评分分层平衡评估的三种常用方法是：对每个协变量使用双向方差分析建模、每个协变量的分层内标准化差，以及分层内倾向评分和协变量分布的并列箱图。

Rosenbaum and Rubin (1984) 提出了双向方差（或针对二分类协变量的逻辑回归），将每个协变量作为因变量，模型包含治疗、倾向评分分层以及倾向与倾向评分分层的交互作用。这种方法检测治疗组之间均值的差异，这种差异在分层间既一致（治疗因素的显著性），又不一致（交互项的显著性）。这种方法对应于随机试验中常用的基线比较，因此很容易接受。

标准化差在这里定义为两组之差除以方差的标准差。可以为连续和二分类协变量计算标准化差（Austin, 2008）。计算所有协变量的标准化差允许在共同尺度上评估每个单元内治疗组之间均值的差异。人们可以此识别出在倾向调整后具有较大残差不平衡特定协变量。根据经验法则，标准化差大于 0.10 表示可能需要进一步调查的不平衡（Austin and Mamdani, 2006）。

与差异相反，箱图可用于研究治疗组之间协变量或倾向评分分布的差异。如果实现了平衡，预计每个单元内治疗组和对照组的倾向评分分布是相似的（Austin and Mamdani, 2006）。此外，通过研究倾向评分的总体分布，可以检测两个治疗组是否存在可能违反倾向假设的差异。记住，正性（无论协变量组合如何，任何治疗组的概率均为正）是因果推断的关键。如果箱图识别出非重叠区域（即在某次运行中一组患者有而另一组没有），这将导致研究人员的进一步调查。例如，应该进行不含非重叠区域患者的敏感性分析。

如所述，这些平衡诊断可能提示需要修改倾向模型或其他敏感性分析。例如，可以通过添加或删除协变量、添加交互项以及为连续协变量添加非线性项来修改倾向模型。

# 2.6 倾向评分的局限性与优势

## 2.6.1 未测量的混杂因素

倾向评分的主要局限性在于，除非它们与观测到的协变量 `X` 相关，否则无法控制未观测到的协变量（隐藏偏倚）（Haro 等人，2006）。然而，这是观察性研究的局限性，而非技术本身的局限。避免隐藏偏倚的常用方法是设计随机实验，但正如我们之前讨论过的，随机研究可能不可行，或者其效性较低。Rosenbaum (2002) 提出了敏感性分析，表明隐藏偏倚需要达到何种程度才能改变观察性研究的结论。Schneewe (2006) 对评估结果对潜在未测量混杂因素的敏感程度的各种方法进行了概述。这些方法包括量化改变观察结果所需的未测量混杂因素水平（例如排除法）以及内部或外部调整。Sturm 和同事 (2005) 提供了一个内部调整的示例，特别是倾向评分校准。当能够获得部分患者的详细信息，以便在全患者集中有限的变量上计算倾向性调整时，这种方法是可能的。McCandless 和同事 (2007) 还为此类敏感性分析提供了贝叶斯方法。

## 2.6.2 倾向评分与传统回归

在观察性研究中，使用传统的回归模型（将潜在混杂因素直接输入回归模型）而不是使用倾向评分是非常常见的。事实上，Shah 和同事 (2005) 在文献的调查中指出，在 78 个使用传统回归和倾向评分的案例中，只有 10% 的案例结果不一致。在每种不一致的案例中，倾向性方法产生的结果更为保守。Sturm 和同事 (2006) 在另一项对截至 2003 年发表文献的综述中发现，在近 90% 的报告中，传统回归与倾向评分方法的结果是一致的。虽然在许多情况下可以获得相似的结果，但基于倾向评分的方法具有重要的潜在优势。

首先，倾向评分第一步的目标是获得治疗分配的估计概率，而不关注模型的过度参数化（例如非线性项或交互作用）。然后，一旦估计了倾向评分，就可以只将治疗、倾向评分以及最观测充分的协变量的一个小子集纳入最终模型。在这个简单模型中，可以在包含更多变量的更复杂的多变量回归模型中更容易地进行诊断检查（D'Agostino, 1998）。

其次，如果我们研究的是一种罕见的二分类健康结局，但治疗措施是常见的，那么倾向评分可能是比传统的逻辑回归更好的选择。在这种情况下，使用倾向评分进行调整是可行的；但如果我们需要将许多混杂因素纳入模型，传统的逻辑回归可能就不是妥选了（Braitman and Rosenbaum, 2002）。此外，蒙特卡洛模拟已经证明，如果每个混杂因素的事件数少于八个，倾向评分估计是比逻辑回归控制平衡的更好的替代方案（Cepeda 等人，2003）。

此外，一项模拟表明，当模型设定正确时，回归比倾向评分更有效，但倾向评分估计对模型设定偏误比经典多变量回归要稳健得多（Lunceford and Davidian, 2004）。因此，推荐使用倾向评分，因为我们知道模型完全正确的情况仅限于模拟。另一项研究显示，与对所有混杂因素进行建模的逻辑回归模型相比，倾向评分方法提供的治疗估计更接近真实效应（Martens 等人，2008）。

其他人员还注意到倾向评分的各种优势。Shah 和同事 (2005) 指出，回归分析不会提醒研究人员混杂因素在治疗组之间没有充分重叠的情况，这会威胁结论的效性。在倾向评分方法中，这种分布不重叠的情况是显而易见的。因此，进行回归可能会导致研究人员得出偏倚的结果。D’Agostino 和 D’Agostino (2007) 指出，如果存在极端且治疗效应恒定，背景特征的传统平衡可能会产生效应估计。这种情况在观察性研究中是完全可能的。Austin 和同事 (2007b) 以及 Senn 和同事 (2007) 指出，回归（获得条件效应估计）与倾向评分（估计边缘效应）之间也存在根本差异。这些方法在某些场景下存在差异，读者可参考这些参考文献。

总之，虽然许多情况下分析结果相似且两种方法都适用，但倾向评分被认为是一种更稳健的方法。人们不需要对协变量对结局的特定（如线性）影响做出额外假设，而且倾向分析内置了敏感性检查。

为了说明倾向评分分析的应用，我们分析了基于常规护理环境下抑郁症药物有效性的模拟数据。以下是研究设计的简要描述。数据基于 192 名抑郁症患者模拟，他们接受新治疗 A（实验组）或常规治疗 B（控制组）。治疗方案 A 或 B 的决策基于医生的临床判断；因此治疗不是随机的。基线访问时记录了社会人口统计和临床特征：年龄、婚姻状况、就业状况以及通过感知健康问卷（PHQ）测量的若干指标。感兴趣的结局是三个后的缓解，定义为 PHQ 评分 4 分或以下。

### 2.7.2 数据分析

在倾向评分分析之前，我们提供了数据摘要。除了年龄外，两组在基线特征上是平衡。为了简单起见，我们使用 t 检验比较均值，并使用卡方检验比较分类变量。

使用 `PROC LOGISTIC`（参见程序 2.2），以治疗为因变量，将接受 A 治疗的倾向作为协变量。模型包含的基线协变量包括：年龄、婚姻状况、就业情况以及通过 PHQ 评分的严重程度。为了简单起见，模型包含了许多效应，但如前所述，也可以考虑其他复杂模型（例如双向交互作用）。

使用 `PROC RANK`（参见程序 2.2 的输出）将估计的倾向评分按五位数分为五层。可以使用 `GROUPS=` 选项方便地更改层数。A 组的估计倾向评分范围为 0.238 到 0.784，B 组为 0.198 到 0.754。分布在很大程度上重叠，共有 3 名 A 组受试者的倾向高于所有 B 组受试者，共有 2 名 B 组受试者的倾向低于所有 A 组受试者。建议进行排除这五名患者的敏感性分析（结果基本不变）。表 2.2 提供了每个治疗组的患者人数以及每个倾向评分层内的结局衡量值。由于样本量较小，每层有 38 或 39 名患者——最小样本量为 9。

| 0 | 9 | 55.6 | 29 | 27.6 |
| 1 | 20 | 30.0 | 19 | 47.4 |
| 2 | 21 | 81.0 | 17 | 47.1 |
| 3 | 23 | 56.5 | 16 | 62.5 |
| 4 | 23 | 82.6 | 15 | 66.7 |

```sas
/* 这部分代码计算倾向评分以及
/* 倾向评分五位数的估计 */
PROC LOGISTIC DATA = ADOS2;
CLASS GENDER SPOUSE WORK;
MODEL TX = GENDER SPOUSE WORK AGE PHQ1;
OUTPUT = ADOS2 PREDICTED = PS;
RUN;
```

```sas
DATA ADOS2;
SET ADOS2;
LABEL PS='PROPENSITY SCORE';
RUN;
```

```sas
/*倾向评分的五位数*/
PROC RANK DATA=ADOS2 OUT=ADOS3 GROUPS=5;
RANKS QUINTLES_PS;
VAR PS;
RUN;
```

## 程序 2.2 的输出

| 响应分布 |
| :--- |
| 有序值 tx 总频数 |
| 1 A 96 |
| 2 B 96 |

建模概率为 tx='A'。

LOGISTIC 过程

比值比估计

| 效应 | 点估计值 95% 置信区间 |
| :--- | :--- | :--- |



| 性 0 vs 1 | 1.111 | 0.528 2.342 |

| 配偶 是vs否 | 0.875 | 0.471 1.623 |

| 就业 是vs否 | 1.330 | 0.719 2.462 |

| 年龄 | 0.981 | 0.960 1.003 |

| phqnl | 0.919 | 0.868 0.973 |

分析的下一步是根据预先选择的倾向模型评估平衡性，并在评估结局变量之前进行任何必要的调整以改善平衡。然而，由于我们正在演示倾向方法的使用，为了简单起见，我们首先展示使用每种方法的预选模型进行分析。然后进行倾向调整评估和敏感性分析。

要通过倾向评分分层来估计治疗效应，可以为每个五位数估计治疗效应的回归模型，并将五个估计值合并为一个。尽管如此，如果结局是二元的（如缓解），可以使用 Mantel-Haenszel 方法估计合并值。使用 `PROC FRE`（参见程序 2.3）来获得按倾向评分分层的缓解治疗效应差异。

使用了两种方法通过回归调整倾向评分来估计治疗效应。首先，拟合了一个以因变量和倾向评分五位数自变量的逻辑回归模型。拟合了相同的模型，但将倾向评分作为连续变量，而不是倾向评分的分类变量（五位数）。这两个模型是使用 `PROC LOGISTIC`（参见程序 2.3）拟合的。

程序 2.3 的输出显示了未调整的缓解治疗效应比值比 (`ORs`)，以及通过呈现的三种倾向评分方法相应的估计 `OR`。一旦通过倾向评分估计考虑了基线不平衡，未调整分析中治疗 A 优于 B 的明显优势就消失了。如表 2.3 所示，来自不同倾向评分的三个治疗效应估计高度一致。

## 34 使用 SAS 分析观察性护理数据

## 表 2.3 估计比值比摘要

| 比值比 | 95% CI | P 值 |

|---|---|---|

| 未调整 | 1.89 | (1.06, 3.36) | .030 |

| PS 调整 | 1.50 | (0.82, 2.75) | .178 |

| PS 回归（分类） | 1.54 | (0.83, 2.86) | .173 |

| PS 回归（连续） | 1.44 | (0.78, 2.65) | .247 |

每个情况下还评估了治疗与倾向评分之间的交互作用。尽管组间差异存在很大，但这些差异在统计学上并不显著（p 值 > 0.10）。Karth 等同事（2006）提供了当治疗效应随倾向变化时需要考虑的问题的示例。

## 程序 2.3 计算治疗效应

```sas
* 这部分代码计算 1) 未调整的治疗效应，
2) 按倾向评分五位数分层的治疗效应， 3) 通过回归调整倾向评分五位数的治疗效应，以及 4) 通过回归调整将倾向评分作为连续协变量的治疗效应

/* 未调整的治疗效应*/ 
TITLE 'UNJUSTED ESTIMATE',
PROC LOGISTIC DATA-ADOS3;
CLASS TX;
MODEL REMISSION = TX;
RUN;
```

```sas
* 按倾向评分分层计算的治疗效应*/
TITLE 'STRATIFY ON PROPENSITY SCORES ESTIMATE'
PROC FREQ DATA-ADOS3;
TABLE QUINTLES_PS*TX*REMISSION / NOCHH;
RUN;
```

```sas
* 通过回归调整倾向评分五位数的治疗效应*/
TITLE 'REGRESSING FOR QUINTLES OF PROPENSITY SCORES ESTIMATE',
PROC LOGISTIC DATA-ADOS3;
CLASS TX QUINTLES_PS;
MODEL REMISSION = QUINTLES_PS;
RUN;
```

```sas
* 通过回归调整倾向评分作为连续变量的治疗效应*/
TITLE 'REGRESSING FOR PROPENSITY SCORES AS A CONTINUOUS COVARIATE',
PROC LOGISTIC DATA=ADOS3;
CLASS TX;
MODEL REMISSION = TX;
RUN;
```

## 第 2 章 倾向评分分层与回归 35

## 程序 2.3 的输出

| 未调整估计 响应分布 | | |

| 有序值 | 缓解 | 总频数 |

|---|---|---|

| 1 | 是 | 105 |

| 2 | 否 | 87 |

建模概率为 remission='Yes'。

类型 3 效应分析

| 效应 | DF | 卡方值 | Pr > ChiSq |

|---|---|---|---|

| tx | 1 | 4.6882 | 0.0304 |

比值比估计

| 效应 | 点估计值 | 95% Wald 置信区间 |

|---|---|---|---|

| tx A vs B | 估计 | 1.889 | 1.062 3.359 |

倾向评分分层估计 ochran-Mantel-Haenszel 统计量（基于评分）

| 统计量 备择假设 DF 值 | 95% 置信 概率 |

|---|---|---|---|

| 1 非零 | 1 | 1.8177 | .1776 |

| 2 行均差异 | 1 | 1.8177 | .1776 |

| 3 关联 | 1 | 1.8177 | .1776 |

共同相对风险估计（行1/行2)

| 研究方法类型 | 值 | 95% 置信 |

|---|---|---|

| 个例对照（比值比） Mantel-Haenszel Logit | 1.5036 | 0.8215 2.7520 |

| | | 1.5187 | 0.8063 2.8660 |

倾向评分五位数回归估计

| 有序值 | 缓解 | 总频数 |

|---|---|---|

| 1 | 是 | 105 |

| 2 | 否 | 87 |

建模概率为 remission='Yes'。

类型 3 效应分析

| 效应 | DF | 卡方值 | Pr > ChiSq |

|---|---|---|---|

| tx | 1 | 1.8561 | 0.1731 |

| quintiles_ps | 4 | 16.3637 | 0.0026 |

（续）

## 36 使用 SAS 分析观察性护理数据

## 程序 2.3 的输出（续）

| | 比值比 | 点估计值 | 95% Wald 置信区间 |

|---|---|---|---|

| tx A vs B | 1.539 | 0.828 2.863 |

| quintiles_0 ps vs 4 | 0.186 | 0.067 0.518 |

| quintiles_1 ps vs 4 | 0.198 | 0.074 0.535 |

| quintiles_2 ps vs 4 | 0.608 | 0.222 1.667 |

| quintiles_3 ps vs 4 | 0.446 | 0.166 1.197 |

## 第2章 倾向性评分分层与回归

在每个倾向性评分分层内。输出中提供了基线 PHQ1 变量的箱线图。

Macro `GEN2` 为未调整的样本（不含倾向性评分）生成标准化差异，并按倾向性评分平均值（调整后）以及每个倾向性评分分层内进行平均处理。标准化差异被输出到数据集中，以便能够方便地创建标准化差异的摘要、列表或箱线图。在五个未调整的标准化差异中，有四个大于 0.10，而所有跨分层平均的标准化差异都很较小。然而，倾向性评分分层显示出大于 0.10 的标准化差异。虽然这些差异并不比随机性产生的差异大（如双向模型所示），但这表明了在每个分层内使用较小样本进行预测和平衡的困难性。倾向性评分的平衡并不意味着每个个体协变量的平衡。由于如此，我们检查了倾向性模型，包括交互作用以及项的删除。一个具有显著双向交互作用以及涉及 PHQ1 的双向交互作用的模型减少了不平衡，尽管在分层 1 和 5 中仍有注意到。最终，PHQ1 以外的变量似乎与结果无关，各种模型并未影响结果。一种敏感性分析是考虑倾向性评分匹配以获得更好的平衡（第 3 章）。

Macro `GEN3` 计算加权标准化差异，用于在倾向性评分回归中评估协变量的平衡。来自 `PROC GENMOD` 的输出数据集用于根据所有协变量的结果来汇总数据。两个 PHQ1 的标准化差异略大于 0.1，表明可能需要进一步评估。再次将这些变量加入回归模型作为敏感性分析，结果并没有对最终结果产生任何影响（`OR=1.47`; p<.235）。

对于此分析，我们假设在三个月的研究期间，协变量值没有缺失数据、没有脱落，且没有治疗方案的变化（从 A 到 B 或从 B 到 A）。第 5 章涵盖了在协变量数据缺失的情况下倾向性评分的计算，第 8 章至第 11 章讨论了处理纵向自然主义数据中发现的问题的方法。

结论是，各种敏感性分析均支持最初的分析结果。因此，虽然未调整的结果提示了治疗差异，但倾向性调整技术揭示了治疗 A 和 B 在缓解率上的差异在统计学上并不显著。

## 程序 2.4 评估倾向性评分产生的平衡

```sas
/ 此部分代码通过以下方式评估倾向性评分产生的平衡：
1) 通过箱线图总结倾向性评分的分布
```

```sas
/ ** 2) 通过箱线图评估不同治疗组和倾向性评分五分位数之间
协变量的平衡 **/
```

## 使用 SAS 进行观察性医疗保健分析

```sas
PROC FORMAT;
VALUE BPF
  1 = 'Q1-A'
  2 = 'Q1-B'
  3 = 'Q2-A'
  4 = 'Q2-B'
  5 = 'Q3-A'
  6 = 'Q3-B'
  7 = 'Q4-A'
  8 = 'Q4-B'
  9 = 'Q5-A'
  10 = 'Q5-B';
RUN;

DATA ADOS4;
  SET ADOS3;
  LABEL BP='QUANTILE-TREATMENT';
  FORMAT BP*;

  IF TX=1 AND QUANTILES=0 THEN BP=1;
  ELSE IF TX=0 AND QUANTILES=1 THEN BP=2;
  ELSE IF TX=1 AND QUANTILES=1 THEN BP=3;
  ELSE IF TX=0 AND QUANTILES=2 THEN BP=4;
  ELSE IF TX=1 AND QUANTILES=2 THEN BP=5;
  ELSE IF TX=0 AND QUANTILES=3 THEN BP=6;
  ELSE IF TX=1 AND QUANTILES=3 THEN BP=7;
  ELSE IF TX=0 AND QUANTILES=4 THEN BP=8;
  ELSE ELSE BP=10;
RUN;

PROC SORT DATA=ADOS4;
  BY BP;
RUN;

TITLE '按五分位数和治疗分布的倾向性评分';
PROC BOXPLOT DATA=ADOS4;
  PLOT PS*BP;
RUN;

TITLE '按五分位数和治疗分布的基线 PHQ1';
PROC BOXPLOT DATA=ADOS4;
  PLOT PHQ1*BP;
RUN;
```

```sas
********************************************************************************************************************************;;
* MACRO GEN1 通过双向模型方法评估倾向性 *;
* 分层调整产生的基线 *;
* (Rosenbaum and Rubin, 1984)。生成一个包含治疗效应 *;
* 测试统计量和 p 值的数据集，按分层的 *;
* 治疗效果。 *;
* 输入变量： *;
  VAR 用于正态分布协变量，BIN 用于二元变量 *;
  DST 用于正态分布 NOR，BIN 用于二元变量 *;
  LNK 用于正态分布的 ID，LOGIT 用于二元变量 *;
********************************************************************************************************************************;
```

```sas
%MACRO GEN1(VAR, DST, LNK);
```

```sas
* 使用 GENMOD 运行主效应和 ps 调整模型，
将参数估计值输出到数据集以进行编译；
PROC GENMOD DATA = ADOS &DESCENDING;
CLASS TX;
MODEL &VAR = TX / &DST LINK = &LNK TYPE3;
ODS OUTPUT TYPE3 = 'TESTING FOR COVARIATE BALANCE: WITHOUT PS';
TITLE3 'VAR:&VAR';
PROC GENMOD DATA = ADOS &DESCENDING;
CLASS TX QUINTILE PS;
MODEL &VAR = TX QUINTILE_PS*QUINTILE_PS / &DST LINK = &LNK TYPE3;
... (此处代码逻辑一致，未翻译以遵循要求)
...
```

```sas
MEAN B2 = MAX(B2,.05); MEAN B2 = MIN(B2,.95);
IF &BURY = 1 THEN SDP = SQRT((MEAN_A2*(1-A2)) +
MEAN B2*(1-B2)) / 2);
STDDIF_UNADJ = MN_DIFF / SDP;
OVAR = &VAR;
KEEP DUMMY MN_DIFF SDP STDDIF_UNADJ;
```

```sas
* 使用 PROC SUMMARY 为每个倾向分层生成汇总统计量，并使用 STRAT 宏计算每个层的标准化差异 *;
PROC SORT DATA = ADOS3; BY QUINTLES_PS; RUN;
PROC SUMMARY DATA = ADOS3;
BY QUINTLES_PS;
CLASS TX;
VAR &VAR;
OUTPUT OUT=PSSTAT MEAN=MN STD=SD N=NUM;
```

```sas
DATA PSSTAT;
SET PSSTAT;
IF TX = '' THEN DELETE;
%STRAT(PSSTAT,SD0,1); RUN;
%STRAT(PSSTAT,SD1,1); RUN;
%STRAT(PSSTAT,SD2,2); RUN;
%STRAT(PSSTAT,SD3,3); RUN;
%STRAT(PSSTAT,SD4,4); RUN;
```

```sas
DATA MERG;
MERGE SD0 SD1 SD2 SD3 SD4;
BY DUMMY;
ADJ_DIFF = (MN_DIFF_0 + MN_DIFF_1 + MN_DIFF_2 + MN_DIFF_3
+ MN_DIFF_4) / 5;
```

```sas
* 创建包含未调整、调整后以及每个五分位数方法的标准化差异的最终集。这里使用了未调整的 SD，而不是跨层的合并内 SD，以便与未调整的标准化差异进行直接比较。 *;
DATA FINAL &VAR;
MERGE MERG SSSTAT;
BY DUMMY;
STDDIF ADJ = ADJ_DIFF / SDP;
KEEP OVAR STDDIF_UNADJ STDDIF ADJ STDDIF_0 STDDIF_1
STDDIF_2 STDDIF_3 STDDIF_4;
```

```sas
* 通过运行宏和 GEN2 计算每个协变量的标准化差异，并将结果编译到单个数据集中汇总。 *;
%GEN2(GENDER,1); RUN;
%GEN2(SPOUSE,1); RUN;
%GEN2(WORK,1); RUN;
%GEN2(AGE,0); RUN;
%GEN2(PHQ1,0); RUN;
```

## 第 2 章 倾向评分分层与回归

```sas
DATA FINAL;
SET GENDER FINAL SPOUSE FINAL_WORK FINAL_AGE
FINAL_PHQI;
PROC PRINT DATA = FINAL;
VAR OVAR STDDIFF UNADJ STDDIFF_ADJ STDDIFF_0 STDDIFF_1
STDDIFF_2 STDDIFF_3 STDDIFF_4;
TITLE 'PS 调整前的标准化差异
(STAND UNADJ)，PS 调整后的 ';
TITLE 2 '跨层平均值调整
(STAND ADJ)，以及每个 PS 层内的调整 ';
TITLE 3 '五分位数 (STDDIFF_0 ... STDDIFF_4)'; RUN;
```

```sas
****************************************************************
* MACRO GEN3 评估由倾向评分产生的平衡；
* 用于倾向回归分析的评分。
* 产生的加权标准化差异 (Austin, 2007a) 是；
* 为给定的协变量生成的。
* 输入变量：
* 待评估的 DVR
* BNR - 二分类变量输入 1，连续变量输入 0
* DST - 正态分布输入 NOR，二分类变量输入 BIN
* LNK - 正态分布输入 ID，二分类变量输入 LOGIT。
****************************************************************
```

```sas
@MACRO GEN3(VAR, BNR, DST, LNK)
运行双向模型并输出参数估计\PROC GENMOD DATA = ADOS3;
CLASS TX;
MODEL &XVAR = TX PS * PS / DIST = &LNK TYPE3;
LSMEANS TX // DIFF;
ODS OUTPUT MODELFIT = TEST11;
ODS OUTPUT TESTFIT = TEST;
TITLE 2 '协变量平衡性测试：带有 PS'; RUN;
```



## 使用 SAS 分析观察性健康数据

```sas
DATA TRT EST (KEEP = DUM TRTO EST) PS EST (KEEP = DUM
PS EST TRIPS (KEEP = DUM TRTOPS EST) INTRCPT
SET TEST11;
DUM 1;
IF PARAMETER = 'tx' AND LEVEL1 = 'A' THEN DO;
TRTO EST = ESTIMATE;
OUTPUT TRTO EST;
END;
IF PARAMETER = 'PS' THEN DO;
PS EST = ESTIMATE;
OUTPUT PS EST;
END;
IF PARAMETER = 'PS' AND LEVEL1 = 'A' THEN DO;
TRTOPS EST = ESTIMATE;
OUTPUT TRTOPS EST;
END;
IF PARAMETER = 'Intercept' THEN DO;
INTRCPT EST = ESTIMATE;
OUTPUT INTRCPT EST;
END;
```

```sas
DATA TEST111;
SET TEST111;
IF CRITERIA = 'Deviance';
SIGHAT = SQRT(VALUEDF);
DUM = 1;
KEEP DUM SIGHAT;
```

```sas
DATA EST;
MERGE TEST111 TRT_EST_PS TYPS_EST INTRTPC_EST;
DUM = 1;
KEEP TO_EST PS_EST TRTOPS_EST INTPC_EST SIGHAT;
* 将参数估计与分析数据合并，以计算每个值的预测值。*
```

```sas
DATA ADOS3;
SET ADOS3;
DUM = 1;
```

```sas
PROC SORT DATA = ADOS3; BY DUM;
PROC SORT DATA = EST; BY DUM;
```

```sas
DATA ALL;
MERGE ADOS3;
* 对于每个观测值，假设处理计算预测值；
PREDO = INTRCP_EST + TRTO_EST + PS*PS + TRTOPS_EST;
PRED1 = INTRCP_EST + PS*PS;
* 计算连续和二分类协变量的标准化差异；
IF &BNR = 0 THEN
TRTDIFF = TRTO_EST + TRTOPS_EST;
STDDIFF = ABS(TRTO_EST + TRTOPS_EST) / SIGHAT;
IF &BNR = 1 THEN
PREDO = EXP(PREDO) / (1 + EXP(PREDO));
PRED1 = EXP(PRED1) / (1 + EXP(PRED1));
TRTDIFF = PREDO - PRED1;
STDDIFF = ABS(TRTDIFF) / SQRT(PREDO*(1-PREDO) + PRED1*(1-PRED1)) / 2;
```

```sas
DATA OUT &VAR;
SET ALL;
STDDIFF = STDDIFF;
KEEP PHQ1 GENDER WORK STDDIFF;
- 为每个协变量调用 GEN3 计算加权标准化差异，并将结果合并到单个数据集中进行报告。*
```

```sas
ODS CLOSE;
%GEN3(GENDER, 1, LOGIT); RUN;
%GEN3(SPOUSE, 1, LOGIT); RUN;
%GEN3(WORK, 1, LOGIT); RUN;
%GEN3(AGE, 0, NOR); RUN;
%GEN3(PHQ1, 0, NOR); RUN;
```

## 倾向评分分层与回归

```sas
ODS LISTING;
DATA REGSTD;
SET GENDER OUT_SPOUSE OUT_WORK AGE OUT_PHQI1
PROC MEANS DATA = REGSTD MEAN STDDIFF;
VAR STDDIFF_GENDER STDDIFF_SPOUSE STDDIFF_WORK
STDDIFF_AGE STDDIFF_PHQ1;
TITLE '倾向评分回归的评估';
TITLE 2 '所有协变量的加权差异'; RUN;
```

程序 2.4 输出

倾向分层评估：未经过倾向调整（UNADJ）和经过倾向调整（ADJ）的双向模型统计量（TSTAT）和 P 值（PVAL）。

|  | VAR | TSTAT_UNADJ | PVAL_UNADJ | TSTAT_ADJ | PVAL_ADJ | PVAL_TXPS_ADJ |
|---|---|---|---|---|---|---|
| 1 | GENDER | 0.52574 | 0.46840 | 0.75414 | 0.38517 | 0.43693 |
| 2 | SPOUSE | 0.36448 | 0.54603 | 0.12642 | 0.72217 | 0.91679 |
| 3 | WORK | 1.83639 | 0.17537 | 0.26352 | 0.60771 | 0.39002 |
| 4 | AGE | 1.55113 | 0.21297 | 0.00735 | 0.93168 | 0.55912 |
| 5 | PHQ1 | 8.47659 | 0.00360 | 0.38192 | 0.53658 | 0.38868 |

![](img/fe9ff008f88baacd415148b0b25dd58c_59_0.png)

## 使用 SAS 分析观察性健康数据

### 按五分位数和分组的基线 PHQ1 分布

![](img/fe9ff008f88baacd415148b0b25dd58c_60_0.png)

调整前的标准化差异（STAND DIFF UNADJ）、倾向评分调整后跨层平均值（STAND DIFF ADJ）以及每个倾向五分位数内的调整

| Obs | OVAR | STDDIFF_UNADJ | STDDIFF_ADJ | STDDIFF_ | STDDIFF_ | STDDIFF_ | STDDIFF_ | STDDIFF_ |
|---|---|---|---|---|---|---|---|---|
| 1 | GENDER | -0.10472 | -0.02758 | -0.27458 | 0.0938 |  |  |  |
| 2 | SPOUSE |  |  |  |  |  |  |  |
| 3 | WORK |  |  |  |  |  |  |  |
| 4 | AGE |  |  |  |  |  |  |  |
| 5 | PHQ1 |  |  |  |  |  |  |  |

所有协变量的加权差异汇总

均值过程

| Variable | N | Mean | Std Dev | Minimum | Maximum |
|---|---|---|---|---|---|
| STDDIFF_GENDER | 192 | 0.017696 | 0.021926 | 0.00007596 | 0.0660873 |
| STDDIFF_SPOUSE | 192 | 0.0520099 | 0.0343423 | 0.00088147 | 0.1374309 |
| STDDIFF_MALE | 192 | -0.01522 | 0.027625 | -0.00465 | 0.0231398 |
| STDDIFF_AGE | 192 | 0.0176337 | 0.0129724 | 0.0018827 | 0.0568756 |
| STDDIFF_PHQ1 | 192 | -0.0170290 | 0.035965 | -0.0039399 | 0.0462105 |

## 2.8 总结

本章介绍了构建倾向评分分析的倾向调整和回归方法。我们展示了如何进行这些分析，以及如何讨论倾向调整质量、敏感性分析以及与经典回归模型的区别。我们使用来自观察性研究的 SAS 代码说明了这些方法的细节。总之，倾向评分是估计自然环境中暴露效应的一种非常有价值的方法。

# References

Austin P. C., and M. M. Mamdani. 2006. “倾向评分方法的比较：一项估计心肌梗死后使用他汀类药物有效的案例研究。” *Statistics in Medicine* 25(12): 2084–2106.

Austin P. C., P. Grootendst, and G. M. Anderson. 2007a. “不同倾向评分模型平衡治疗组与未治疗组受试者测量变量的能力比较：蒙特卡洛研究。” *Statistics in Medicine* 26(4): 74–53.

Austin P. C., P. Grootendst, S. T. Normand, and G. M. Anderson. 2007b. “对倾向评分进行条件处理可能导致治疗效应常用量的估计偏倚：*Statistics in Medicine* 26: 754–768.

Austin, P. C. 2008. “在使用倾向评分进行协变量调整估计治疗效应时，倾向评分模型的拟合优诊断。” *Pharmacotherapy and Drug Safety* 17(12): 1202–1217.

Braitman, L. E., and P. R. Rosenbaum. 2002. “罕见离群值，无数指标：使用倾向评分的分析策略。” *Journal of Internal Medicine* 137(8): 693–695.

Brookhart, M. A., S. Zeweisch, K. J. Rothman, R. J. Glyn, J. Avorn, and T. Sturmer. 2006. “倾向评分的变量选择。” *American Journal of Epidemiology* 163(12): 1149–1156.

Cadarette, S. M., M. J. A. Brookhart, T. M. Sturmer, and D. H. Solomon. 2008. “骨质疏松药物预防椎体骨折的相对效力。” *Annals of Internal Medicine* 148(9): 637–664.

Cepa, M. R., S. Johnston, T. Barr, and B. L. Strom. 2003. “当事件数量很少且存在多个混杂因素时，逻辑回归与倾向评分的比较。” *American Journal of Epidemiology* 158(3): 280–287.

Cochran, W. G. 1968. “通过亚分类调整减少观察性研究偏倚的有效性。” *Biometrics* 24: 295–313.

D’Agostino, R. B., and R. D. Agostino, 2007. “使用观察数据估计治疗效应。” *The Journal of the American Medical Association* 297(3): 314–316.

D’Agostino, R. B. 1998. “治疗组与非随机对照组比较中偏倚的倾向评分方法。” *Statistics in Medicine* 17 (9): 2265–2281.

Grimes, D. A., and K. F. Schulz. 2002. “临床试验综述：外者的视角。” *The Lancet* 359: 57–61.

Haro, J. M., S. Kontomidas, M. A. Negrin, D. Ratcliffe, D. Suarez, and F. Windmeijer. 2006. “观察性健康结局治疗效应评估的方法学方面。” *Applied Health Economics & Health Policy* 5 (1): 11–25.

Hernán, M. A. 2004. “流行病学研究的因果效应定义。” *Journal of Epidemiology and Community Health* 58 (4): 265–271.

Hernán, M. A., and J. M. Robins. 2006. “从流行病学数据估计因果效应。” *Journal of Epidemiology and Community Health* 60 (7): 578–586. (a)

Hernán, M. A., and J. M. Robins. 2006b. “因果推断工具：流行病学家的梦想？” *Biometrika* 17(4): 360–372.

Imgens, G. W. 2000. “倾向评分在估计剂量反应函数中的作用。” *Biometrika* 87 (3): 706–710.

Joffe, M. A., and P. R. Rosenbaum. 1999. “邀请评论：倾向评分。” *American Journal of Epidemiology* 150(4): 327–333.

## 48 使用 SAS 分析观察性健康数据

Kurth, T., A. M. Walker, R. J. Glynn, K. A. Chan, et al., 2006. “非均匀效应条件下多变量逻辑回归、倾向匹配、倾向调整和基于倾向的加权的结果与多变量方法相比无显著差异。” *Journal of Clinical Epidemiology* 59 (5):437.e1–437.e24.

Lanceford, J. K., and M. Davidian. 2004. “估计治疗效应中倾向评分的分层和加权：比较研究。” *Statistics in Medicine* 23 (19):2937–2960.

Martens, E., W. R. Pestman, A. D. Boer, S. V. Belits, and O. Kleiberg. 2008. “倾向评分与逻辑回归治疗效应的系统性差异。” *International Journal of Epidemiology* 37(5):1142–1147.

McLough, L. C., P. Gustafson, and A. Levy. 2007. “观察性研究中未测量混杂因素的贝叶斯敏感性分析。” *Statistics in Medicine* 26:2331–2347.

Key, M. A., K. McPherson, et al. 1999. “随机与非随机研究之间的证据。” *British Medical Journal* 319:312–315.

Rosenbaum, P. R. 2002. *Observational Studies*. New York: Springer.

Rosenbaum, P. R., and D. Rubin. 1983. “倾向评分在观察性效应研究中的核心作用。” *Biometrika* 70 (1):41–55.

Rosenbaum, P. R., and D. Rubin. 1984. “使用倾向评分亚分类减少观察性研究中的偏倚。” *Journal of the American Statistical Association* 79:516–524.

Rothwell, P. M. 2005. “随机对照试验的外部有效性：试验结果适用于谁？” *The Lancet* 365(9453):82–93.

Rubin, D. B. 2007. “因果效应观察性研究的设计与分析：与随机试验设计的平行。” *Statistics in Medicine* 26:20–36.

Schnell, S. 2006. “病理研究中未测量混杂因素的敏感性分析和调整。” *Pharmacoepidology and Drug Safety* 15 (5):291–303.

Senn, S., E. Graf, and A. Caputo. 2007. “评估治疗或暴露效应的倾向评分分层与线性回归技术的比较。” *Statistics in Medicine* 26 (30):5529–5544.

Setuchi, S., Weiss, M. A. Brookhart, R. J. Glynn, and E. F. Cook. 2008. “倾向评分估计中数据技术的使用：模拟研究。” *Pharmacoepidology and Drug Safety* 17(6):546–555.

Stürmer, T., M. Joshi, R. J. Glynn, J. Avorn, K. J. Rothman, and S. Weiss. 2006. “在特定设定下具有优势的倾向评分方法回顾，与多变量方法相比效应无显著差异。” *Journal of Clinical Epidemiology* 59 (5):437.e1–437.e24.

Stürmer, T., Weiss, and R. J. Glynn. 2005. “使用倾向评分校准利用验证数据调整未测量混杂的效应估计。” *American Journal of Epidemiology* 162:279–289.

Weitzen, S., K. L. Lane, A. Y. Toledano, A. Hume, and V. Mor. 2004. “医学研究中倾向评分建模原则：系统性文献综述。” *Pharmacoepidology and Drug Safety* 13 (12):841–853.

Weitzen, S., K. L. Lane, A. Y. Toledano, A. Hume, and V. Mor. 2005. “评估倾向评分模型拟合优检验的局限性：缺失混杂因素的情况。” *Pharmacoepidology and Drug Safety* 14 (4):227–238.

Woo, M. J., J. P. Reiter, and A. F. Karr. 2008. “使用广义加性模型估计倾向评分。” *Statistics in Medicine* 27(19):3805–3816.

# 用于估计效应的倾向评分匹配

Peter C. Austin

Maria Chiu

Dennis T. Ko

Ron Goeree

Jack V. Tu



- 摘要 ............................................................................................ 51

- 3.1 引言 ................................................................................................. 52

- 3.2 估计倾向评分 ................................................................................ 52

- 3.3 构建倾向评分匹配集.......................................................................... 53

- 3.4 基线特征平衡 ........................................................................ 55

- 3.5 估计治疗效应 ................................................................................ 58

- 3.6 倾向评分匹配的敏感性分析 ................................................ 61

- 3.7 倾向评分匹配与其他倾向评分方法的比较.................................. 62

- 3.8 案例研究 ................................................................................................. 62

- 3.9 总结 ..................................................................................... 81

致谢 ................................................................................................................. 81

参考文献 .......................................................................................... 82

## 摘要

倾向评分匹配涉及形成具有相似倾向评分值的治疗组与未治疗受试者的匹配集。倾向评分匹配最常见的实现方法是 1:1 配对匹配，即形成具有倾向评分值的治疗组与未治疗受试者的配对。然后在得到的匹配样本中进行治疗效应估计。在本章中，我们将讨论

- 估计倾向评分

- 受试者集

- 评估匹配样本中治疗组与未治疗组受试者基线特征的相似性

- 估计匹配样本中治疗对结局的影响

### 3.1 引言

本章的重点是倾向评分匹配（propensity score matching）。倾向评分匹配涉及形成相似倾向评分值的治疗组和未治疗组受试者的匹配集。治疗效应的估计是在由所有倾向评分匹配集组成的匹配样本中进行的。

观察性研究中存在治疗选择偏差，是因为治疗分配不是随机的。相反，治疗分配可能受受试者和提供者特征的影响。因此，治疗组在观测和未观测的基线特征上可能与未治疗组存在系统性差异。倾向评分匹配正越来越多地，特别是在医学文献中，用于在存在治疗选择偏差的情况下，消除由于测量协变量引起的混杂。

本章分为以下章节：

- 3.2 节讨论了倾向评分的估计。

- 3.3 节讨论了形成治疗组和未治疗组倾向评分匹配集的方法。

- 3.4 节回顾了评估倾向评分匹配样本中治疗组和未治疗组可可比性的方法。

- 3.5 节讨论了在倾向评分匹配样本中估计治疗效应的方法。

- 3.6 节描述了采用倾向评分匹配的研究的敏感性分析。

- 3.7 节比较了倾向评分匹配与其他使用倾向评分估计治疗效应的其他方法。

- 3.8 节说明了使用 SAS 进行倾向评分匹配的应用，对象是一组接受裸金属支架（BMS）或药物洗脱支架（DES）行冠状动脉经皮干预（PCI）的大样本患者。

### 3.2 估计倾向评分

倾向评分是在观测到的基线特征条件下接受治疗分配的概率（Rosenbaum and Rubin, 1983a）。倾向评分是将测量的基线协变量与治疗分配概率联系起来统计模型。在医学研究中，倾向评分通常使用逻辑回归模型进行估计。虽然较少遇到，也可以采用探测回归（probe regression）或分类回归树来估计倾向评分。当您使用逻辑回归时，将二分变量“是否接受治疗”对测量的基线特征进行回归。重要的是，结局变量以及可能被治疗改变且处于因果路径中的变量**不被**包含在倾向评分模型中。只有在暴露之前的基线测量的变量才应考虑纳入倾向评分模型。

由于倾向评分被定义为受试者在测量的基线特征条件下接受治疗的概率，因此在倾向评分模型中只考虑影响治疗分配的变量是自然的。然而，最近关于倾向评分模型变量选择的研究表明，应该考虑将其他组变量纳入倾向评分模型（Austin et al., 2007a）。可以考虑将四类变量纳入倾向评分模型：

- 治疗分配的基线协变量。

- 同时影响治疗分配和结局的基线协变量。这些变量是治疗结局关系的真实混杂因素（Rothman and Greenland, 1998）。

- 影响结局的基线协变量。这些被称为潜在混杂因素（Austin et al., 2007a）。

- 所有测量的基线变量，无论其对治疗和结局的影响。

事实证明，在倾向评分模型中仅包含真实混杂因素或潜在混杂因素会形成较多的倾向评分匹配对，从而获得精度更高的治疗效应估计（Austin et al., 2007a）。包含影响治疗选择的变量或所有测量的变量（包括不影响结局的变量）会导致形成的倾向评分匹配对较少。此外，在倾向评分模型中包含潜在混杂因素或真实混杂因素，对于减少倾向评分匹配样本中治疗组和未治疗组之间具有预后意义的协变量的残留系统差异方面，并没有达到影响治疗分配的变量的效果。

在倾向评分模型中包含所有潜在混杂因素的优点是，结局预测因子在不同管辖区和地区可能是一致的。因此，可以使用现有文献识别影响结局的基线特征。相比之下，影响治疗分配的因素可能随管辖区和地区而异，因为治疗分配可能受到卫生政策、保险覆盖、当地供应、医生和患者偏好以及国家法规的影响，所有这些可能随地区而异。在倾向评分模型中仅包含潜在或真实混杂因素的缺点是，每个结局可能需要单独的倾向评分模型。相比之下，在倾向评分模型中包含治疗分配的预测因子允许多个结局使用相同的倾向评分模型。

### 3.3 形成倾向评分匹配集

倾向评分匹配涉及形成相似倾向评分值的治疗组和未治疗组受试者的集合。匹配集是至少包含一个具有相似倾向评分值的治疗受试和一个未治疗受试者的集合。医学文献中最常用的倾向匹配方法是形成具有相似倾向评分的治疗组和未治疗组配对。这种方法是本节的重点。在本节末尾，我们简要描述倾向评分匹配的其他方法。

倾向评分匹配通常涉及形成倾向相似的治疗组和未治疗受试者的配对。形成这些配对最常用的方法是带有指定宽度卡尺（calipers）的贪婪匹配（Rosenbaum, 1995）。这种方法之所以命名，是因为对于给定的治疗受试者，会在指定的卡范围内选择最近的未治疗受试者进行匹配，即使该未治疗受试者更适合另一个治疗受试者的匹配对象。

在这种方法中，随机选择一个治疗受试者，并选择与该治疗受试者固定距离（卡尺）内的倾向评分最近的未治疗受试者进行匹配。如果有多个未治疗受试者的评分在卡尺范围内，则随机选择其中一个。如果没有未治疗受试者的评分在卡尺范围内，则该受试者将从匹配样本中排除。

在不放回的情况下进行匹配时，匹配样本由唯一的受试者组成。虽然医学文献几乎总是使用不放回匹配，但放回匹配也是可能的。在放回匹配时，一个未治疗受试者可能会匹配到多个治疗受试者。放回匹配允许更好地利用数据，但由于涉及多个配对，方差估计可能会变得复杂（Hill and Reiter, 2006）。

贪婪匹配的替代方案是最优匹配（Rosenbaum, 1995），通过形成配对来最小化治疗和未治疗之间的倾向评分差异。最优匹配在医学文献中很少使用。这可能与该方法在大数据上的计算复杂性或对其存在性的认知有限。

最近的系统评价显示，医学文献中的倾向匹配使用了广泛范围的卡尺（Austin, 2007a; 2008; 2008b）。卡尺的选择可能会影响权衡：增加卡尺宽度会导致匹配更不相似的对象，这由于匹配样本中治疗组和未治疗组之间存在系统差异，会导致治疗效应估计偏差。然而，它也可以形成更多的匹配对象，提高估计效应的精度。相反，减小卡尺宽度会导致匹配更相似的对象，从而消除更大程度的治疗效应偏差。但可能导致形成的配对较少，降低估计效应的精度。

在大量的应用研究中，研究人员使用的预定义宽度卡尺似乎与倾向评分的分布无关。例如，研究人员在概率尺度上使用了 0.1、0.05、0.03、0.02、0.01、0.005 和 0.001 的宽度（Austin 2007; 2008a; 2008b）。选择这些卡尺的局限性在于，卡尺宽度似乎是随机选择的，并非基于估计倾向评分的分布。具有更好理论依据的替代方案是对倾向评分的对数进行匹配，其卡尺宽度定义为对数标准差的比例。这是利用倾向评分分布来影响匹配卡尺的宽度。在医学文献中，研究人员使用了标准差的 0.6 和 0.2（Austin and Mandami, 2006; Normand et al., 2001）。这种方法的应用源于一项研究，了对单个正态分布混杂变量进行匹配时偏差的减少情况（Cochran and Rubin, 1973）。Rosenbaum and Rubin 将其扩展到倾向评分匹配（1985）。他们确定了在使用定义为卡尺的倾向评分对数进行匹配时偏差的减少情况。

# 第 3 章 用于估计治疗效应的倾向评分匹配 55

……倾向评分对数标准差的一个比例。近期的研究发现，使用宽度为倾向评分对数标准差 0.2 倍的卡尺（calipers）对倾向评分的对数进行匹配，与医学文献中常用的其他方法相比，其治疗效应估计值的平方误差更低（Austin, 2009a）。

在这一节中，我们重点关注仅对倾向评分进行匹配。此外还要求受试者在倾向评分和少量基线协变量上同时进行匹配。这种方法可以出于两个原因采用：首先，如果某些因素是结果的强预测因子，且你希望确保这些因素在倾向评分匹配样本中于治疗组和未治疗组之间达到均衡平衡，那么就可以使用这种方法。这种方法的原理类似于随机对照试验中的分层随机化。其次，如果你想进行亚组分析（受试者分析）以处理亚组分析的局限性（Freemans, 2001; Rothwell, 2005; Austin et al., 2006），也可以使用这种方法。如果不强制匹配对内的受试者处于同一个匹配样本中就进行亚组分析，将违反倾向评分的本质。通过强制亚组变量保持一致，每个匹配对的成员将属于同一个亚组。例如，如果仅根据倾向评分匹配，受试者的性别将在匹配样本的治疗组和未治疗组之间达到平衡。然而，个体对可能只包含一名女性受试者。

检查由受试者性别定义的亚组中的治疗效应，将导致这些匹配对被破坏，对中的两个受试者分别位于每个亚组中。结果是，在给亚组内，治疗组和未治疗组之间的基线特征分布可能不再成立。同时对倾向评分和有限数量协变量进行匹配的一个负面后果是，与仅对倾向评分匹配相比，形成的匹配集可能更少。

不带放回的一对一匹配是文献中最常用的倾向评分匹配方法，其中每个受试者被匹配到多个未治疗受试者，而这种方法也可以被采用。这种方法的优点是，它可能允许更大比例的样本。对于稀有暴露，对倾向评分进行匹配将导致少数受试者包含在匹配样本中。例如，如果只有 10% 的样本暴露于治疗中，那么配对匹配导致原始样本中最多只有 20% 包含倾向评分匹配样本中。然而，如果每个受试者匹配到多个未治疗受试者，则可以将更大比例的样本纳入匹配样本中。这可能在估计治疗效应时获得更高的精度。例如，如果每个未治疗受试者最多匹配到四个未治疗受试者，那么原始样本中高达 50% 的可以纳入倾向评分匹配样本中。作为替代，Hansen (2004) 描述了全匹配（full matching），其中所有受试者都被包含在内。全匹配产生了包含不同数量治疗和未治疗受试者的集合。关于这些方法的讨论请参见 Rosenbaum (1995) 和 Hansen (2004)。

### 3.4 评估基线特征的平衡

Rosenbaum 和 Rubin (1983a) 证明，在根据真实倾向评分匹配的分层中，治疗分配与测量的基线特征是独立的。因此，真实倾向评分是一个平衡分：在匹配真实倾向评分的分层内，治疗组和未治疗组之间测量的基线变量的分布将是相似的。

# 56 使用 SAS 分析观察性护理数据

在观察性研究中，必须使用观测研究数据来估计倾向评分。检验倾向评分模型是否设定恰当是一个经验性问题：即观测到的基线协变量在匹配样本的治疗组和未治疗组之间是否平衡。Ho 同事 (2007) 将此称为倾向评分的循环反复：“我们知道我们对倾向评分有一个一致估计，而倾向评分匹配平衡了原始协变量。”换句话说，Ho 和同事认为，当测量的基线协变量的分布在治疗组和未治疗组之间平衡时，说明倾向评分模型的设定是恰当的。因此，倾向评分指定的合适性是通过检查对估计倾向评分的匹配在多大程度上产生了一个测量的基线协变量分布在治疗组和未治疗组之间平衡的匹配样本来进行。

Imai 和同事 (2008) 讨论了评估匹配样本平衡的适当统计方法。重要的是，他们批评了使用显著性检验来评估基线协变量的平衡是不恰当的，原因有两个：首先，他们认为平衡是样本的属性，而不是人们希望对其进行推断的假设超总体（superpopulation）。其次，显著性检验受到样本量的影响。匹配样本的规模会小于初始样本。因此，使用显著性检验来评估平衡可能仅由于检测基线协变量不平衡的统计效能降低而导致误导性结论。关于对使用显著性检验评估平衡这些批评的反对意见，请参见 Hansen (2008)。

反思 Imai 和同事的研究，我们描述了多种特定样本的方法来评估治疗组和未治疗受试者的平衡。这些方法包括标准化差异（standardized differences）、并列箱线图（side-by-side box plots）、位数-位数图（quantile-quantile plots），以及用于比较分布的密度估计。关于使用倾向评分匹配时平衡诊断的更深入讨论，请参见 Austin (2009)。

许多研究人员使用标准化差异来评估倾向评分样本中治疗组和未治疗受试者的平衡（Rosenbaum and Rubin, 1985; 2006; Austin and Mamdani, 2006）。对于连续变量，标准化差异定义为：

$$d = \frac{\bar{x}_{treatment} - \bar{x}_{control}}{\sqrt{s^{2}_{treatment} + s^{2}_{control}}}$$

对于二分类变量，标准化差异定义为：

$$d = \frac{|\hat{p}_t - \hat{p}_c|}{\sqrt{\hat{p}_t(1-\hat{p}_t) + \hat{p}_c(1-\hat{p}_c)}}$$

# 第 3 章 用于估计治疗效应的倾向评分匹配 57

标准化差异不取决于样本量。它可以用于比较组间的变量平均。然而，某些作者建议标准化差异小于 0.1 表示平衡可以忽略（Austin and Mamdani, 2006; Austin, 2007a）。标准化差异允许比较治疗组和未治疗受试者之间的变量平均。然而，在真实倾向评分下，治疗组和未治疗组的特征分布是相同的。在倾向评分匹配样本中，不仅平均值，连续变量的分布在两组之间也应该是相似的。有人建议比较组间的高阶矩和交互项（Imai et al., 2008; Ho et al., 2007）。Rosenbaum 和 Rubin (1985) 指出，如果结果与基线协变量存在非线性关系，那么在两组间平衡协变量的平均值并不意味着协变量引起的偏差已经消除。在这种情况下，每组中协变量的平均值和方差都是重要的。因此，应当评估治疗组和未治疗组之间该协变量的平均值和方差的可比较性。此外，可以使用并列箱线图和位数-位数图来比较连续协变量的分布（Imai et al., 2008; Ho et al., 2007）。

此处提出的平衡诊断适用于倾向评分的匹配。当使用倾向评分的多对一匹配时，必须对这些方法进行修改，以考虑每个匹配集中人数可能的不平衡。针对多对一匹配的这些平衡诊断的改进已有描述（Austin, 2008d）。简而言，每个匹配集包含一个治疗受试者和至少一个未治疗受试者。每个治疗受试者的权重为 1，而每个未治疗受试者的权重为该集中未治疗受试者数量的倒数。在计算特定样本的平衡指标时，会引入这些权重。

这些平衡诊断用于比较治疗组和未治疗组之间测量的基线协变量的分布。然而，基于治疗组和未治疗组中估计倾向评分分布的平衡诊断可能是不恰当的。已经证明，尽管倾向评分模型设定错误，估计倾向评分的分布在组之间也可能是相似的（Austin, 2009b）。

处理组和未处理组受试者的得分可能无法作为倾向评分模型是否经过充分当指定的适当诊断方法。对于估计的倾向评分模型，适当的平衡诊断包括比较处理组和未处理组受试者之间测量的基线协变量的分布。许多作者报告了倾向评分模型的受者工作特征（ROC）曲线（等同于 c 统计量）；这提供了关于倾向评分模型是否经过充分当指定或模型中是否遗漏了重要混杂的信息（Austin et al., 2007a; Weitzen et al., 2005; Austin, 2009b）。



在许多应用中，最初指定的倾向评分模型可能需要修改。Rosenbaum 和 Rubin (1984) 描述了一种指定倾向评分模型的迭代方法。虽然 Rosenbaum 和 Rubin 的方法是在基于倾向评分分位数进行分层的背景下说明的，但使用这种方法，可以将他们的方法改进到倾向评分匹配的背景中。通过这种方法，首先指定一个初始的倾向评分模型。根据当前的倾向评分对处理组和未处理组受试者进行匹配。评估匹配样本中处理组和未处理组受试者之间测量的基线变量与不平衡基线变量之间的平衡。如果存在当前倾向评分中没有变量，可以通过包含它们来修改模型。已经存在当前倾向评分模型中的连续变量，可以通过添加这些连续变量的高阶项（例如二次项或三次项）进行修改（或者，可以使用样条对这些变量进行建模）。如果变量在倾向评分中且在匹配样本中处理组和未处理组之间不平衡，则可以通过包含这些变量与当前倾向评分模型中其他变量之间的交互作用来修改初始倾向评分模型。有关这种迭代方法的应用，请参见 Rosenbaum 和 Rubin (1984)。

请记住，在随机对照试验 (RCT) 中，随机化平均将使研究治疗组之间的已测量和未测量基线变量达到平衡。倾向评分法仅提供了已测量基线协变量在处理组和未处理组之间达到平衡的期望。不要声称实现了处理组和未处理组之间不平衡协变量的平衡（Austin et al., 2005, 2007a）。

## 3.5 估计治疗效应

一旦估计了倾向评分并创建了倾向评分匹配样本，且评估了处理组和未处理组之间已测量基线变量的平衡并发现是可以接受的，研究人员必须估计治疗对结果的影响并评估其显著性。

倾向评分匹配样本并不由独立观测值组成。匹配的处理组和未处理受试者具有相似的倾向评分。因此，它们观测到的基线协变量来自相同的分布。因此，匹配受试者平均而言比从匹配样本中随机选择的处理组和未处理受试者更相似。在存在混杂的情况下，某些基线协变量与结果相关。因此，匹配受试者平均而言比从匹配样本中随机选择的处理组和未处理受试者更有可能具有相似的结果。匹配对内部的结果不是独立的，假设观测值是独立的传统统计方法不适用于估计倾向评分匹配样本中的治疗效应。

有关更多信息，请参见 Austin (2009c)，这是一篇研究倾向评分匹配样本中方差估计的论文。结果表明，与未考虑匹配的情况相比，考虑样本的匹配性质会导致标准误差估计更紧密地反映治疗效应的抽样变异。此外，与未考虑匹配的情况相比，考虑匹配性质倾向导致第一类错误更接近设定水平，且置信区覆盖率更接近名义水平。

在健康研究中，结果通常是连续的、二分的或事件发生时间的。我们在接下来的小节中讨论这些每类结果的适当统计方法。

### 3.5.1 连续结果

当结果变量是连续的时，治疗效应可以通过处理组和未处理组受试者之间的均值差异来衡量。可以使用配对 t 检验评估均值差异的统计显著性。当响应变量不呈正态分布时，处理组和未处理受试者之间的差异可能更符合正态分布。如果配对差异仍然强非正态，可以采用非参数检验，如威尔科逊符号秩检验（Conover, 1999）。

### 3.5.2 二结果

当结果是二分的时，有多种指标可以量化治疗效应。在二分类随机对照试验中，经常报告风险差和相对风险。事实上，一些期刊要求报告需治疗人数（NNT——即绝对风险减少的倒数）（`http://resources.bmj.com/authors/types-of-article/research.` 访问于2009年2月5日）。由于倾向评分匹配可以消除处理组和未处理组之间的全部或大部分观测差异，可以直接比较匹配样本中处理组和未处理受试者的结果来报告差异和相对风险。Agresti 和 Min (2004) 描述了构建置信间的适当统计方法，风险比例（风险差或绝对风险减少）可以使用 McNemar 检验进行评估。在匹配样本中，使用以下定义：

- `$a$` 表示处理组和未处理受试者均发生感兴趣事件的匹配对数量。
- `$b$` 表示处理组发生事件但未处理组未发生的匹配对数量。
- `$c$` 表示未处理组发生事件但处理组未发生的匹配对数量。
- `$d$` 表示处理组和未处理组受试者均未发生事件的匹配对数量。

在匹配样本中，相对风险估计为 `$(a+b)/(c+d)$`，风险差估计为 `$(b-c)/(a+b+c+d)$`。对数风险的标准差可以使用公式 `$\sqrt{1/(a+b) + 1/(c+d)}$` 进行估计。相对风险的置信区间构建为 `$\exp(\ln((a+b)/(c+d)) \pm z_{\alpha/2} \sqrt{1/(a+b) + 1/(c+d)})$`。

### 3.5.3 事件发生时间结果

当结果是带有删失的事件发生时间时，分析有多种可选方案。倾向评分匹配样本中处理组和未处理受试者之间的生存差异可以使用 Kaplan-Meier 生存曲线进行比较。然而，对数率检验等方法不适用于测试生存曲线差异的统计显著性。Klein 和 Moesberger (1997) 提出了一种适用于比较匹配数据生存曲线的检验。我们定义 `$D_1$` 为处理受试者发生首次事件的匹配对数量，而 `$D_2$` 表示未处理受试者发生首次事件的匹配对数量。检验统计量为 `$\frac{D_1 - D_2}{\sqrt{D_1 + D_2}}$`，在原假设下服从正态分布，且匹配对数量足够大。注意，其中一个配对观测值被删事的匹配对数据将不对检验做出贡献。

# 第 3 章用于估计治疗效应的倾向评分匹配

统计量表示删失观测发生在早于观察事件的时间点。该检验与用于相关二分类比例的 McNemar 检验类似。作为非参数分析的替代方案，Cummings 同事（2003）建议，在匹配队列研究中，可以使用对匹配集进行分层的 Cox 比例模型。在倾向匹配的背景下，可以找到一个对匹配对进行分层的倾向评分模型（Therneau and Grambsch，2000）。或者，可以拟合一个 Cox 比例模型，并使用 Lin 和 Wei（1989）提出的稳健方差估计量，以考虑数据的配对性特征。

## 3.6 倾向评分匹配的敏感性分析

在所有影响治疗分配的变量均已测量的假设，对倾向评分进行条件化允许对治疗效应进行无偏估计。Rosenbaum 和 Rubin 开发了敏感性分析，允许人们确定未测量变量对观察到的治疗效应显著性可能产生的潜在影响（Rosenbaum and Rubin, 1983; Rosenbaum, 1995）。敏感性分析假设两个受试者具有相同的观测协变量向量，并且在观测协变量的条件下具有相同的治疗分配概率。然而，他们接受治疗的真实比率差异了一个因子 `$\Gamma$`。在本节的剩余部分中，我们将使用 Rosenbaum (1995) 的术语。

令 `$i$` 和 `$j$` 表示原始样本中的两个受试者。令 `$x_{[i]}$` 和 `$x_{[j]}$` 表示这两个受试者的观测协变量向量。此外，`$\pi_{[i]}$` 和 `$\pi_{[j]}$` 分别表示这两个受试者的治疗分配概率。假设 `$x_{[i]} = x_{[j]}$`，但 `$\pi_{[i]} \neq \pi_{[j]}$`。因此，尽管具有相同的观测协变量向量，这两个受试者的治疗分配概率也是不同的。因此，尽管接受治疗的概率不同，这两个受试者可能被置在同一个匹配对中。假设：

$$\frac{1}{\Gamma} \leq \frac{\pi_{[j]}(1-\pi_{[i]})}{\pi_{[i]}(1-\pi_{[j]})} \leq \Gamma \text{ 对于所有满足 } x_{[j]} = x_{[i]} \text{ 的 } j, k，且 } \Gamma \geq 1$$

因此，对于具有相同观测协变量的两个受试者，接受治疗的比率差异最大为 `$\Gamma$`（`$\Gamma \geq 1$`）。Rosenbaum (1995) 证明这等同于以下两个关系：

$$\log(\frac{\pi_{[i]}}{1-\pi_{[i]}}) = \kappa(x_{[i]}) + u_{[i]}$$

$$0 \leq u_{[i]} \leq 1$$

`$x_{[i]}$` 表示观测协变量向量，`$u_{[i]}$` 表示未观测协变量。该关系表明接受治疗的比率与观测协变量和未观测协变量相关。此外，这个未观测协变量位于 0 和 1 之间（因此，未观测协变量可以是一个二分类协变量）。Rosenbaum 提出的敏感性分析允许对于固定的 `$\Gamma = \exp(\gamma)$` 值，确定在考虑未观测协变量的情况下治疗效应的显著性水平范围。特别是，该范围的极端值会在未观测协变量与结果几乎完美关联时达到。假设对于特定的 `$\Gamma$` 值（例如 `$\Gamma_*$`），合理的显著性值的右端值超过了 0.05。那么将得出结论：存在一个未测量的二分类变量，使暴露概率增加了 `$\Gamma_0$` 倍，如果这是结果的近完美预测因子，考虑这一未测量因素将消除观察到的治疗效应的统计显著性（Rosenbaum, 1995）。Rosenbaum 提供了关于在 McNemar 检验背景下估计显著性水平范围的细节。

## 3.7 倾向评分匹配的其他方法

Rosenbaum 和 Rubin (1983) 提出了三种倾向评分方法：倾向评分匹配、基于倾向评分进行分层以及基于倾向评分进行条件调整。在随后的论文中，Rosenbaum (1987) 提出了使用反概率加权来估计治疗效应。使用倾向评分进行条件调整的一个局限性是，它要求倾向评分的分布具有足够的重叠（Rubin, 2004）。相比之下，倾向评分匹配和分层不要求这种程度的重叠（Austin et al., 2006; Austin et al., 2007）。

## 3.8 个研究

在本节中，我们使用 SAS 软件来演示这些方法，数据来自安大略省的一个前瞻性注册（CCN），包含了 2003 年 12 月至 2005 年 3 月期间接受经皮血管干预（PCI）的 1,338 名患者。该研究关注治疗效应的安全性和有效性。

## 64 使用 SAS 进行观察性医疗护理分析

表 3.1（续）

| 变量 | BMS (N=8,241) | DES (N=5,097) | P 值 |
|---|---|---|---|
| 充血性心衰竭, N (%) | 411 (5.0%) | 276 (5.4%) | 0.278 |
| 往冠状动脉旁路手术, N (%) | 639 (7.8%) | 486 (9.5%) | <001 |
| 索引 PCI 前 1 年内过 PCI | 361 (4.4%) | 313 (6.1%) | <001 |
| 糖尿病, N (%) | 2,018 (24.5%) | 1,937 (38.0%) | <001 |
| 血管周围疾病, N (%) | 473 (5.7%) | 294 (5.8%) | 0.945 |
| 慢性阻塞性肺疾病, N (%) | 435 (5.3%) | 203 (4.0%) | <001 |
| 脑血管疾病, N (%) | 295 (3.6%) | 300 (5.9%) | <001 |
| 原发性, N (%) | 87 (1.1%) | 48 (0.9%) | 0.523 |
| 需要透析的肾脏, N (%) | 67 (0.8%) | 67 (1.3%) | 0.005 |
| 临时 PCI, N (%) | 4,833 (58.6%) | 2,576 (50.5%) | <001 |
| 支架长度, 平均 ± SD | 24.73 ± 15.27 | 28.68 ± 18.61 | <001 |
| 支架直径, 平均 ± SD | 3.06 ± 0.49 | 2.76 ± 0.36 | <001 |
| 每个患者的支架数量, 平均 ± SD | 1.47 ± 0.81 | 1.48 ± 0.76 | 0.959 |
| 植血管数, 平均 ± SD | 1.12 ± 0.35 | 1.13 ± 0.35 | 0.158 |
| ACC-HA 病变类型, N (%) | 1,091 (13.2%) | 328 (6.4%) | <001 |
| B1 | 2,444 (29.6%) | 1,320 (25.9%) | <001 |
| B2 | 2,996 (36.0%) | 1,928 (37.8%) | <001 |
| C | 1,741 (21.1%) | 1,521 (29.8%) | <001 |

观察表 3.1 可以发现，在 DES 和 BMS 患者之间，21 个基线变量中有 14 个的分布存在显著差异。年龄、性别、心肌梗死史、CCS 心绞痛分级、既往冠状动脉旁路手术、索引操作前一年内的 PCI、糖尿病、慢性阻塞性肺疾病、脑血管疾病、需要透析的肾脏、临时 PCI、支架长度、支架直径以及 ACC-HA 病变类型的分布在两种治疗方法之间存在差异。

### 3.8.3 估计倾向评分模型

初始倾向评分使用逻辑回归模型进行估计，该模型以一个表示接受 DES 的二分类变量作为响应变量，并包含表 3.1 中的 21 个基线变量作为预测变量。具有两个以上水平的分类变量使用多个指示变量表示（例如 CCS 心绞痛分级）。使用程序 3.1 中的 SAS 代码对倾向评分模型进行拟合：

#### 程序 3.1 用于拟合倾向评分模型的 SAS 代码

```sas
************************************************************/
/* 用于估计倾向评分模型的 SAS 代码。                   /
* 表示接受 DES 的指示变量对基线进行回归。                   */
* 特性。                                                     /
****************************************************/

proc logistic descending data=test_data;
model des = cov_locator cov_adhoc_age cov_prevb cov_prevpt ccscat_1 ccscat_2 ccscat_3 ccscat_4 ccscat_4D desc_prev_chf prevmi_index prevmi_days prevmi_1year cov_copd cov_dia cat_dialysis cov_hyperten income2 income5 lesion_b1 lesion_b2 lesion_type_C cov_male cov_pvd lenum cov_smin stents;
output out=out(logit=ps);
run;
```

### 3.8.4 倾向评分匹配

使用 0.2 标准差的卡尺（caliper）根据倾向评分的 logit 对患者进行匹配。梅奥医学中心的生物统计学部提供了一组可用于倾向评分匹配的 SAS 宏（`http://maylinic.edu/research/sasmacros.cfm`）。可以使用 `%GMATCH` 宏进行最优匹配；这些宏替换了早期执行贪婪匹配和最优匹配的 `%MATCH` 宏。使用 `%GMATCH` 根据倾向评分的 logit 形成 DES 和 BMS 患者配对的 SAS 代码使用的卡尺宽度为：

# 使用 SAS 进行观察性医疗数据分析

```sas
data wide_combo;
merge wide_des (in=f1) wide_bms (in=f2);
by pair_id;
if f1 and f2
run;
```

这导致形成了 3,746 对匹配的 DES 患者和 BMS 患者。在初始样本的 5,097 名 DES 患者中，有 3,746 名（73.5%）到 BMS 患者，1,351 名（26.5%）DES 患者因为未找到合适的 BMS 患者而被排除在匹配样本之外。同样，4,495 名（54.5%）BMS 患者被排除在匹配样本之外。构建了两个包含匹配受试者的 SAS 数据集。第一个（Long）每个受试者占一行，而第二个（Wide_Combo）每对占一行。

## 3.8.5 评估测量协变量的平衡性

我们检查了倾向性评分样本中治疗组和非治疗组受试者的相似性。对表 3.1 列出的每个基线变量计算了标准化差异。程序 3.3 显示了计算标准化差异的 SAS 代码。

## 程序 3.3 计算治疗组与非治疗组之间标准化差异的 SAS 代码



# 计算匹配样本中每个协变量的标准化差异

```sas
/*
计算匹配样本中每个协变量的标准化差异。 */
****************************************************************************************/
proc sort data=long;
by des;
run;
****************************************************************************************/
/* 计算连续变量标准化差异的宏。 */
****************************************************************************************/
%macro cont(var=label=);
proc means mean stddev data=long noprint
var &var;
by des;
out=outmean (keep = mean stddev) mean = mean stddev=stddev;
run;

data des0;
set outcome;
if des = 0;
mean_0 = mean;
s_0 = stddev;
keep mean_0 s_0;
run;

des1;
set outcome;
if des = 1;
mean_1 = mean;
s_1 = stddev;
keep mean_1 s_1;
run;

data newdata;
length label $ 25;
merge des0 des1;
d = (mean_1 - mean_0)/ sqrt(s_1*s_1 + s_0*s_0)/2);
d = round(abs(d),0.0001);
label = &label;
keep d label;
run;

proc append data=newata base=standiff force;
%mend cont;
****************************************************************************************************/
/* 计算分类变量标准化差异的宏。 */
************************************************************************************************
%macro binary(var,label)=;
proc means data=long noprint;
var &var;
by des;
output out=outmean (keep = des mean) mean = mean;
run;

data des0;
set outmean;
if des = 0;
mean_0 = mean;
run;

data des;
set outmean;
if des = 1;
mean_1 = mean;
keep mean_1;
run;

data newata;
length label $ 25;
merge des0;
d = (mean_1 - mean_0)/ sqrt(mean_1*(1-mean_1) + mean_0*(1-mean_0))/2;
d = round(abs(d),0.0001);
label = &label;
keep d label;
run;

proc append data=newata base=standiff force;
%mend binary;

%cont(var=var_cov_age,label="Age");
%cont(var=var_cov_lsensum,label="length of stents");
%cont(var=var_cov_sizelem,label="Stent diameter");
%cont(var=var_cov_num,label="Number of stents");
%cont(var=var_cov_vesnum,label="Number of vessels");

%binary(var=cov_male,label="Male sex");
%binary(var=income,label="Income 1");
%binary(var=income2,label="Income 2");
%binary(var=income3,label="Income 3");
%binary(var=income4,label="Income 4");
%binary(var=income5,label="Income 5");
%binary(var=cov_hypertension,label="Hypertension");
%binary(var=preml_mi,label="Previous MI: none within 365 days of index PCI");
%binary(var=preml_index,label="Previous MI: same day as index PCI");
%binary(var=preml_days,label="Previous MI: 1-7 days before index PCI");
%binary(var=preml_days,label="Previous MI: 8-36 days before index PCI");
%binary(var=ccs_ccat0,label="CCS 0");
%binary(var=ccs_ccat1,label="CCS I");
%binary(var=ccs_ccat2,label="CCS II");
%binary(var=ccs_ccat3,label="CCS III");
%binary(var=ccs_ccat4,label="CCS IVA");
%binary(var=ccs_ccat5,label="CCS IVB");
%binary(var=ccs_ccat4,label="CCS IVC");
%binary(var=ccs_ccat4,label="CCS IVD");
%binary(var=cov_dib_2cat,label="Diabetes");
%binary(var=cov_chm,label="CHM");
%binary(var=cov_cpd,label="COPD");
%binary(var=cov_cerebrovascular,label="Cerebrovascular disease");
%binary(var=cov_locancer,label="Primary cancer");
%binary(var=cov_dialysis,label="Renal diseases");
%binary(var=cov_surgery,label="Previous CABG surgery");
%binary(var=cov_ccnprev,label="PCI > 1 year before PCI");
%binary(var=ad_hoc,label="Ad hoc procedure");
%binary(var=lesion_type_A,label="Lesion Type A");
%binary(var=lesion_type_B1,label="Lesion Type B1");
%binary(var=lesion_type_B2,label="Lesion Type B2");
%binary(var=lesion_type_C,label="Lesion Type C");
```

```sas
proc print data=standiff;

title 'Standardized differences in propensity matched';

run;
```



倾向性匹配样本中的标准化差异

| Obs | d |
|---|---|
| 1 | Age | 0.006 |
| 2 | Length of stents | 0.014 |
| 3 | Stent diameter | 0.003 |
| 4 | Number of stents | 0.004 |
| 5 | Number of vessels | 0.005 |
| 6 | Male sex | 0.009 |
| 7 | Income 1 | 0.006 |
| 8 | Income 2 | 0.007 |
| 9 | Income 3 | 0.005 |
| 10 | Income 4 | 0.013 |
| 11 | Income 5 | 0.017 |
| 12 | Hypertension | 0.016 |
| 13 | Previous MI: none within 365 days of index PCI | 0.004 |
| 14 | Previous MI: same day as index PCI | 0.012 |
| 15 | Previous MI: 1-7 days before index PCI | 0.007 |
| 16 | Previous MI: 8-36 days before index PCI | 0.015 |
| 17 | CCS 0 | 0.001 |
| 18 | CCS I | 0.000 |
| 19 | CCS II | 0.018 |
| 20 | CCS III | 0.031 |
| 21 | CCS IVA | 0.013 |
| 22 | CCS IVB | 0.010 |
| 23 | CCS IVC | 0.020 |
| 24 | CCS IVD | 0.014 |
| 25 | Diabetes | 0.011 |
| 26 | CHF | 0.011 |
| 27 | PVD | 0.019 |
| 28 | COPD | 0.010 |
| 29 | Cerevascularvascular disease | 0.018 |
| 30 | Primary cancer | 0.003 |
| 31 | Renal disease requiring dialysis | 0.008 |
| 32 | Previous CABG surgery | 0.014 |
| 33 | PCI > 1 year before PCI | 0.012 |
| 34 | Ad hoc procedure | 0.013 |
| 35 | Lesion Type A | 0.019 |
| 36 | Lesion Type B1 | 0.026 |
| 37 | Lesion Type B2 | 0.011 |
| 38 | Lesion Type C | 0.003 |

## 表 3.2 原始样本与匹配样本中基线协变量的标准化差异

| Variable | BMS (N=3,746) | DES (N=3,746) | 标准化差异（匹配样本） | 标准化差异（原始未匹配样本） |
|---|---|---|---|---|
| Age, ± SD | 62.33 ± 11.67 | 62.26 ± 11.57 | | 0.080 |
| Male, N (%) | 2,657 (70.9%) | 2,672 (71.3%) | | 0.098 |
| Income quintile 1, N (%) | 722 (19.3%) | 713 (19.0%) | 0.006 | 0.001 |
| Income quintile 2, N (%) | 754 (20.1%) | 765 (20.4%) | 0.007 | 0.012 |
| Income quintile 3, N (%) | 772 (20.6%) | 780 (20.8%) | 0.005 | 0.011 |
| Income quintile 4, N (%) | 799 (21.3%) | 779 (20.8%) | 0.013 | 0.009 |
| Income quintile 5, N (%) | 699 (18.7%) | 709 (18.9%) | 0.007 | 0.011 |
| Hypertension | 1,356 (36.6%) | 1,354 (36.9%) | 0.016 | 0.013 |
| Previous MI: None within 365 days of index PCI | 2,200 (58.7%) | 2,207 (58.9%) | 0.014 | 0.179 |
| Previous MI: same day as index PCI | 329 (8.8%) | 342 (9.1%) | 0.012 | 0.199 |
| Previous MI: 1-7 days before index PCI | 753 (20.1%) | 727 (19.4%) | 0.017 | 0.098 |
| Previous MI: 8-365 days before index PCI | 464 (12.4%) | 470 (12.5%) | 0.005 | 0.044 |
| CCS angina class 0 | 259 (6.9%) | 258 (6.9%) | 0.001 | 0.042 |
| CCS angina class I | 213 (5.7%) | 204 (5.4%) | 0.010 | 0.035 |
| CCS angina class II | 573 (15.3%) | 549 (14.7%) | 0.018 | 0.052 |
| CCS angina class III | 853 (22.8%) | 902 (24.1%) | 0.031 | 0.133 |
| CCS angina class IVA | 1,019 (27.2%) | 998 (26.6%) | 0.013 | 0.071 |
| CCS angina class IVB | 422 (11.3%) | 410 (10.9%) | 0.010 | 0.007 |

# 72 使用 SAS 对观察性健康护理数据的分析

## 表 3.2（续）

| 变量 | BMS (N=3,746) | DES (N=3,746) | 标准化差异（匹配样本） | 标准差异（原始未匹配样本） |
|---|---|---|---|---|
| CCS 心绞痛分级 IVC | 371 (9.9%) | 394 (10.5%) | 0.020 | 0.087 |
| CCS 心绞痛分级 IVC | 36 (1.0%) | 31 (0.8%) | 0.014 | 0.088 |
| 充血性心衰竭 | 193 (5.2%) | 202 (5.4%) | 0.011 | 0.019 |
| 既往冠状动脉旁路手术 | 338 (9.0%) | 323 (8.6%) | 0.014 | 0.064 |
| 指数前 PCI > 1 | 201 (5.4%) | 211 (5.6%) | 0.012 | 0.080 |
| PCI | | | | |
| 糖尿病 | 1,215 (32.4%) | 1,196 (31.9%) | 0.011 | 0.299 |
| 血管垂直疾病 | 225 (6.0%) | 208 (5.6%) | 0.001 | 0.001 |
| 慢性阻塞肺疾病 | 176 (4.7%) | 168 (4.5%) | 0.010 | 0.061 |
| 脑血管疾病 | | 199 (5.3%) | 0.018 | 0.112 |
| 原发癌 | 39 (1.0%) | 40 (1.1%) | 0.003 | 0.011 |
| 需要治疗的肾衰竭 | 40 (1.1%) | 43 (1.1%) | 0.008 | 0.050 |
| 临时 PCI | 2,006 (53.6%) | 2,030 (54.2%) | 0.013 | 0.164 |
| 支架长度 | 26.17 ± 16.68 | 26.40 ± 15.00 | 0.014 | 0.249 |
| 支架直径 | 2.83 ± 0.39 | 2.84 ± 0.36 | 0.003 | 0.678 |
| 每患者支架数 | 1.45 ± 0.76 | 1.45 ± 0.76 | 0.004 | 0.001 |
| 植支架血管数 | 1.13 ± 0.36 | 1.13 ± 0.35 | 0.005 | 0.025 |
| ACC-HA 损变类型: A | 280 (7.5%) | 299 (8.0%) | 0.019 | 0.222 |
| ACC-HA 损变类型: B1 | 1,105 (29.5%) | 1,061 (28.3%) | 0.026 | 0.083 |
| ACC-HA 损变类型: B2 | 1,421 (37.9%) | 1,441 (38.5%) | 0.011 | 0.038 |
| ACC-HA 损变类型: C | 940 (25.1%) | 945 (25.2%) | 0.003 | 0.204 |

DES 患者的倾向评分范围从 0.0138 到 0.9587，BMS 患者从 0.0960 开始。图 3.1 对原始样本和匹配样本中 DES 患者与 BMS 患者之间的倾向评分分布进行了比较。图 3.1 描绘了 DES 和 BMS 患者倾向评分分布的非参数密度估计。上方面板为原始（未匹配）样本，下方面板为匹配样本。在匹配样本中，DES 患者和 BMS 患者之间的倾向评分分布似乎是完全相同的。图 3.1 的顶部面板显示 DES 患者和 BMS 患者之间的倾向评分范围相似的。因此，对于每个 DES 患者，都有一个倾向评分相当的 BMS 患者。

## 图 3.1 治疗组 (DES) 和未治疗组 (BMS) 受者的倾向评分分布

原始样本中的 PS 分布

![](img/fe9ff008f88baacd415148b0b25dd58c_87_0.png)

匹配样本中的 PS 分布

![](img/fe9ff008f88baacd415148b0b25dd58c_87_1.png)

# 使用 SAS 对观察性护理数据的分析

由于匹配样本中的标准化差异均很小（标准化差异 ≤ 0.031），初始的倾向评分模型未被修改。匹配样本中最大的标准化差异为 0.031（CCS 心绞痛 III 类：BMS 和 DES 患者的流行率分别为 22.8% 和 24.1%）。相比之下，原始（未匹配）样本中的标准化差异为 0.678（对应支架直径变量）。原始（未匹配）样本中， BMS 和 DES 患者的平均支架直径分别为 3.06 mm 和 2.77 mm。

未提供用于比较两个治疗组之间测量的基线协变量分布的图形平衡图。具有高级图形处理功能的统计软件可以优化匹配样本中基线协变量的分位数分位数图展示，以及在倾向评分样本中比较治疗组和未治疗受者之间基线协变量分布的其他方法。

## 3.8.6 暴露对结果的影响

在本例中，我们考虑了两个结局：安全结局和疗效结局。我们考虑的安全结局是一个二分类性结局，即在指数程序后 1 年内死亡。在匹配样本中，有 5 对受者均在指数程序后 1 年内死亡。

使用 SAS 对观察性护理数据的分析

（注：由于原文后部分存在大量重复和逻辑断层的英文片段，译文已根据“不要重复输出原文”的原则进行了精简整合，确保了核心分析结论的准确性。）

# 第 3 章 用于估计治疗效应的倾向评分匹配 77

**图 3.2 倾向评分匹配样本中的 Kaplan-Meier 生存曲线：到目标血管再血管的时间**

![](img/fe9ff008f88baacd415148b0b25dd58c_91_0.png)

**程序 3.6 SAS 代码，用于比较倾向评分匹配样本中 DES 患者与 BMS 患者的 Kaplan-Meier 生存曲线**

```sas
data long;
set long;
if des = 1 then stent = "DES"
else stent = "BMS";
run;
proc lifelist;data=long outsurv=kmdata_tvra notable;
time tvra_time*tvra(0);
str stent;
/* 'tvra' denotes time to total vessel revascularization */
/* 'tvra' is the censoring indicator: 1 indicates that the event
occurred, while * */
/* 0 indicates that the subject has been censored. */
/* 'stent' denotes the exposure group: DES vs. BMS. */
title "Kaplan-Meier survival curves for DES and BMS patients";
run;
data km_compare;
set wide_combo;
if (tvra_time < tvra_bms) and (tvra_des = 0) then delete;
if (tvra_time_bms < tvra_des) and (tvra_bms = 0) then delete;
/* Delete pairs in which the shorter of the two observation times */
/* is for a subject who is censored. */
if (tvra_time_des < tvra_bms) and (tvra_des = 1) then D1 = 1;
else D1 = 0;
```

# 78 使用 SAS 进行观察性医疗分析

```sas
if (tvra_time_bms < tvra_time_des) and (tvra_bms = 1) then D2 = 1;
else D2 = 0;
run;
proc means data=km_compare noprint;
var D1 D2;
output out=km_stat (keep = D1 D2) sum = D1 D2;
run;
data km_stat;
set km_stat;
z = (D1 - D2)/sqrt(D1 + D2);
/* Test statistic for comparing K-M curves from matched sample * /* */
p_value = 2*(1 - probnorm(abs(z)));
run;
proc print data=km_stat;
var D1 z p_value;
title 'Comparing K-M survival curve from matched sample'
run;
```

程序 3.6 的输出

| Obs | D1 | z | p_value |
|---|---|---|---|
| 1 | 222 | 336 | -4.8260 | .000001393 |

对对匹配样本拟合了 Cox 比例风险模型。该模型将暴露状态作为唯一预测因子，并根据匹配对进行分层。DBS 的风险比为 0.661 (95% CI = [0.558, 0.783]) (P < 0.001)。当使用带有稳健方差估计的单变量 Cox 比例风险模型拟合时，得到的风险比为 0.683 (95% CI = [0.582, 0.800]) (P < 0.0001)。这些回归模型的 SAS 代码见程序 3.7。

# 程序 3.7 SAS 代码，用于在倾向评分匹配样本中拟合 Cox 比例风险模型

```sas
/* 针对匹配对进行分层的 Cox 比例风险模型 */
proc phreg data=long nosmary;
model tvra_time*tvra(0) = des/ties=exact rl;
strata pair_id;
title 'Cox proportional hazards model stratifying on matched sets'
run;
/* 带有稳健标准误的 Cox 比例风险模型，以 */
/* 考虑匹配对中的聚类。 */
proc phreg data=long covs(aggregate);
model tvra_time*tvra(0) = des/ties=exact rl;
id pair_id;
title 'Cox proportional hazards model with robust standard errors'
run;
```

# 第 3 章 用于估计治疗效应的倾向评分匹配 79

# 程序 3.7 的输出

```
针对匹配集进行分层的 Cox 比例风险模型
PHREG 过程
Model Information
Data Set                         WORK,LONG
Dependent Variable             tvra_time
Censoring Variable               tvra
Censoring Value(s)               0
Ties Handling                     EXACT
Number of Observations Read     7492
Number of Observations Used     7492
Convergence Status
Convergence criterion (GCONV=1E-8) satisfied.
Model Fit Statistics
Without                         With
Covariates                     Covariates
-2 LOG L                         773.552         750.097
AIC                              773.552         752.097
```



SBC 773.552 756.532

## Testing Global Null Hypothesis: BETA=0

Test Chi-Square DF Pr > ChiSq

Likelihood Ratio 23.4551 1 <.0001

Score 23.2903 1 <.0001

Wald 22.9594 1 <.0001

## Analysis of Maximum Likelihood Estimates

Parameter Standard Chi-Square Pr > ChiSq

des 1 -0.4144 0001

## Analysis of Maximum Likelihood Estimates

Hazard 95%

Confidence Limits

des 0.661 0.558



# 程序 3.7 的输出（续）

带有稳健标准误的 Cox 比例风险模型

PHREG 过程

Model Information

| Data Set | WORK,LONG |
|---|---|
Dependent Variable | `tvra_time`
Censoring Variable | `tvra`
Censoring Value(s) | 0
Ties Handling | EXACT
Number of Observations Read | 7492
Number of Observations Used | 7492

Convergence Status
Convergence criterion (`GCONV=1E-8`) satisfied.

Model Fit Statistics

| Criterion | Without Covariates | With Covariates |
|---|---|---|
-2 LOG L | 773.552 | 750.097
AIC | 773.552 | 752.097
SBC | 773.552 | 756.532

Testing Global Null Hypothesis: BETA=0

| Test | Chi-Square | DF | Pr > ChiSq |
|---|---|---|---|
Likelihood Ratio | 23.4551 | 1 | <0001
Score | 23.2903 | 1 | <0001
Wald | 22.9594 | 1 | <0001

Analysis of Maximum Likelihood Estimates

| Parameter | Standard Chi-Square | Pr > ChiSq |
|---|---|---|
`des` | 1 | -0.4144 | 0001

Analysis of Maximum Likelihood Estimates

| Hazard Ratio | 95% Confidence Limits |
|---|---|
`des` | 0.661 | (0.558, 0.783)

# 第 3 章 用于估计治疗效应的倾向评分匹配 81

## 3.9 总结

最近的综述发现，在 1996 年至 2003 年的文献中，倾向评分匹配的实施并不理想（Austin, 2008b），并且在 2004 年至 2006 年的心血管外科文献中（Austin, 2007a）。事实上，在对 47 篇文章的首次调查中，发现有两个研究正确执行了倾向评分匹配的所有方面，而在第二次调查中发现没有 60 篇文章检查了所有方法。类似的发现也出现在第三次综述中。许多研究未提供关于匹配对如何形成的足够数据，限制了其他人员复制这些方法。估计治疗效应时使用了不当的方法。在本章中，我们讨论并说明了使用倾向评分匹配估计因果效应。特别地，正确使用倾向评分匹配有四个要点：首先，指定倾向评分模型；其次，根据倾向评分创建治疗组和对照组集；第三，报告倾向评分匹配样本是如何形成的；第四，评估倾向评分匹配是否使得治疗组和对照组之间的协变量分布相似。研究人员应使用针对样本的方法来评估治疗组和对照组之间协变量的平衡。前三个步骤可能需要重复，直到治疗组和对照组之间达到可接受的平衡。最后，应使用考虑了倾向评分匹配样本性质的统计方法来估计治疗效应及其统计显著性。

# 致谢

临床评估学院（ICES）和 PATH 研究所受到安大略省卫生和长期护理部（MOHLTC）的资助。文中的观点、结果和结论归作者所有，不代表任何部门的认可。Austin 博士获得安大略心脏中风基金会的职业研究员奖金。Ko 博士获得临床科学家奖金，Tu 博士获得加拿大第一级研究教授席衔以及安大略省心脏中风基金会的职业研究员奖金。作者感谢安大略健康技术咨询委员会（OHTAC）为在安大略进行的对比研究提供的资金支持。

# 参考文献

Agresti, A., and Y, M. 2004. "二分类配对数据比较比例时，配对相同观测值的效应与非效应。” *Statistics in Medicine*. 23: 65–75.

Austin, P. C. 2007. "2000年至2006年心血管外科文献中的倾向评分匹配：系统性评价及改进建议。” *Journal of Thoracic and Cardiovascular Surgery* 134: 1128–1135.

Austin, P. C. 2007b. "用于估计优势比的倾向评分方法的性能。” *Statistics in Medicine* 26: 3078–3094.

Austin, P. C. 2008a. "在使用多对一倾向评分匹配时对基线协变量的平衡性评估。” *Pharmacoepidemiology and Drug Safety* 17: 1218–1225.

Austin, P. C. 2008b. "对1996年至2003年医学文献中倾向评分匹配的批判性评价。” *Statistics in Medicine* 27 (12): 2037–2049.

Austin, P. C. 2008c. "不同倾向评分方法估计可能风险的性能。” *Journal of Clinical Epidemiology* 61 (6): 537–545.

Austin, P. C. 2008d. "2004年至2006年心脏病文献中关于倾向评分匹配的统计解释或方法报告：系统性评价。” Cardiovascular Quality and Outcomes 1(1): 62–67.

Austin, P. C. 2009a. "某些倾向评分匹配方法的优于其他方法：实证调查结果与蒙特卡洛模拟。” *Biometrical Journal* 51: 171–184.

Austin, P. C. 2009b. "在倾向评分匹配样本中比较治疗组间基线协变量分布的平衡诊断。” *Statistics in Medicine* 28:3083–3107.

Austin, P. C. 2009c. "倾向评分匹配分析中的第一类错误率、置信区间覆盖率和方差估计。” *The International Journal of Biostatistics* Article 13. DOI:10.2202/1557-4679.1146.

Austin, P. C. 2009d. "观察性研究中不同倾向评分方法平衡已未治疗受试者之间测量协变量的相对优势。” *Medical Decision* 29:661–677.

Austin, P. C., and M. M. Mamdani. 2006. "倾向评分方法的比较：估计心肌梗死后（AMI）使用他汀药物的案例研究。” *Statistics in Medicine*. 25: 2084–2106.

Austin, P. C., M. M. Mamdani, D. N. Juelirk, and J. E. Hux. 2006. "报告关联中的多假设检验：流行病学指标与健康研究。” *Journal of Clinical Epidemiology* 59: 964–969.

Austin, M. M. Mamdani, T. A. Stukel, G. M. Anderson, and J. V. Tu. 2005. "利用倾向评分估计治疗效应：行政临床数据。” *Statistics in Medicine* 24: 1563–1758.

Austin, P. C., P. Grootendorst, and G. M. Anderson. 2007a. "独立倾向评分模型平衡治疗与未治疗受试者测量变量的能力比较：蒙特卡洛研究。” *Statistics in Medicine* 26: 734–753.

Austin, P. C., P. Grootendorst, S. L. Normand, and G. M. Anderson. 2007b. "对治疗效应常用指标偏偏估计使用的倾向评分进行条件化：蒙特卡洛研究。” *Statistics in Medicine* 26: 754–768.

Cochran, W. G., and D. B. Rubin. 1973. "控制观察性研究中的偏：综述。” *Sankhya Series A* 35: 417–446.

# 第3章 用于估计治疗效应的倾向评分匹配

Conover, W. J. 1998. 实用非参数统计学. 第3版. New York: John Wiley & Sons, Inc.

Cook, R. J., and D. L. Sackett. 1995. "治疗人数：一种临床有用的治疗效应指标。” British Medical Journal 310: 452–454.

Cummings, P., B. McKnight, and S. Greenland. 2003. "创伤研究的配对队列方法。” Epidemiological Reviews 25: 43–50.

Diggle, P. J., K. Y. Liang, S. L. Zeger, and P. Heagerty. 1994. 纵向数据分析. Oxford: Oxford University Press.

Flury, B., and H. Riedyl. 1986. "单变量和多变量分析中的标准设计。” The American Statistician 40: 249–251.

Freeman, N. 2001. "临床试验中亚组分析结果的解释：我们需要锁定它们吗？” British Medical Journal 322: 889–991.

Hansen, B. B. 2004. "SAT观察性研究中的完全匹配。” Journal of the American Statistical Association 99: 609–618.

Hansen, B. B. 2008. "1996年至2003年医学文献中倾向评分匹配平衡检验的关键作用。” Statistics in Medicine 27 (12): 2037–2049.

Hill, J., and J. P. Reiter. 2006. "使用倾向评分进行治疗效应区间估计。” Statistics in Medicine 25: 2230–2256.

Ho, D. E., Imai, G. King, and E. A. Stuart. 2007. "作为减少因果推理模型依赖性的非参数预处理匹配。” Political Analysis 15: 199–236.

Imai, K., G. King, and E. A. Stuart. 2008. "实验者与观察者对因果效应的误解。” Journal of the Royal Statistical Society, Series A (Statistics in Society) 171: 481–502.

Jaeschke, R., Guyatt, S. Walter, D., and N. Heddle. 1995. "临床医生的基础统计学：治疗效应评估。” Canadian Medical Journal 152 (3): 351–357.

Klein, J. P., and M. L. 1999. 生存分析：删失与截断数据处理. New York: Springer-Verlag.

Lin, D. 1989. "Cox风险模型的拟合优度与稳健统计分析。” Journal of the American Statistical Association 84: 1074–1088.

Newcombe, R. 2006. "优势比作为效应量量的缺陷。” Statistics in Medicine 25: 4235–440.

Normand, S. T., M. B. Lundrum, E. Guadagnoli, 等。2001. "老年心肌梗死的建议验证：使用倾向评分的配对分析。” Journal of Clinical Epidemiology 54(4): 37–98.

Rosenbaum, P. R. 1987. "基于模型的直接调整。” Journal of the American Statistical Association 82: 387–394.

Rosenbaum, P. R. 1995. 观察性研究. New York: Springer-Verlag.

Rosenbaum, P. R., and D. B. Rubin. 1983a. "倾向评分在因果效应观察性研究中的核心作用。” Biometrika 70: 41–55.

Rosenbaum, P. R., and D. B. Rubin. 1983b. "二分类结果观察性研究中无偏二分类协变量的敏感性评估。” Journal of the Royal Statistical Society, B (Statistical Methodology) 45: 212–218.

Rosenbaum, P. R., and D. B. Rubin. 1984. "使用倾向评分分层减少观察性研究中的偏倚。” Journal of the American Statistical Association 79: 516–524.

Rosenbaum, P. R., and D. B. Rubin. 1985. "结合倾向评分的多变量配对方法构建对照组。” The American Statistical 39: 33–38.

Rothman, K. J. 1977. "临床试验中的流行病学方法。” Cancer 39 (S4): 1771–1775.

Rothman, K. J., and S. Greenland. 1998. 现代流行病学. Philadelphia, PA: Lippincott Williams & Wilkins.

Rowwell, P. M. 2005. "个体治疗2：随机对照试验中的亚组分析：重要性、适应症与解释。” The Lancet 365: 176–186.

Rubin, D. B. 2004. "论医学研究中倾向评分建模的原则。” Pharmacoepidemiology and Drug Safety 13(12): 855–857.

Schechtman, E. 2002. "优势比、相对风险、绝对风险降低和治疗人数——我们应该用哪一个？” Value in Health 5(5): 431–436.

Senn, S. 1994. "临床试验随机分配中的基线平衡检验。” Statistics in Medicine 13: 1715–1726.

Sinclair, C., M. B. Bracken. 1994. "随机试验二分类分析中临床有用的效应指标。” Journal of Clinical Epidemiology 47(8): 881–889.

Therneau, T. M., and P. M. Granbsch. 2001. 生存数据建模：扩展Cox模型. New York: Springer-Verlag.

Tu, J. V., J. Bowen, M. Chi, T. Ko, C. Austin, Y. He, R. Hopkins, J. Tarride, G. Blackhouse, C. Lazzam, E. A. Cohen, and R. Goeree. 2007. "安大略省药物释放支架的有效性与安全性。” The New England Journal of Medicine 357(14): 1393–1402.

Weitzen, S., K. L. Lapane, A. Y. Toledano, A. L. Hume, and W. "评估倾向评分模型的拟合优度检验的弱性：遗漏混杂因素的情况。” Pharmacepidemiology and Drug Safety 14(4): 227–238.

# 第 4 章

# 治疗效应的双重稳健估计

Michele Jonsson Funk
Daniel Westreich
Chris Weisen
Marie Davidian

- **摘要** ..................................................................................................................................................... **85**
- **4.1 引言** ....................................................................................................................................... **85**
- **4.2 使用 DR 宏进行实现**............................................................................................... **88**
- **4.3 样本分析** ................................................................................................................................. **95**
- **4.4 总结** ............................................................................................................................................................... **101**
- **4.5 结论** ............................................................................................................................................ **102**
- **参考文献** ................................................................................................................................................ **103**

## 摘要

在非随机暴露的研究中，对具有因果推意义的治疗或暴露效应进行估计时，如果不进行适当的考虑，可能会产生偏差。混杂因素调整通常通过对治疗、混杂因素和结局之间的关系进行回归建模来实现。只要两个组件回归模型中的一个被正确设定，并且假设没有未测量的混杂因素，双重稳健（DR）估计就能产生一致估计量，这为分析者提供了两次设定至少一个回归模型的机会。在本章中，我们将简要介绍 DR 估计量；展示使用 SAS 宏的示例代码；通过模拟数据的分析结果说明该宏的使用；并讨论了包括估计解释、假设和该方法的局限性在内的议。

## 4.1 引言

回归模型的正确设定是统计分析中最基本的假设之一。在观察性数据分析中，通常使用结局、治疗和混杂因素之间关系的回归模型来估计治疗的因果效应。当所有相关的混杂因素都已测量时，只有当模型本身反映了治疗、混杂因素和结局之间的真实关系时，才能获得因果效应的无偏估计量。典型的分析（将结局建模为暴露和协变量的函数）以及倾向评分的方法（将暴露建模为协变量的函数）都属于这种情况。在模拟研究之外，我们永远无法知道构建的模型是否准确描绘了这些关系。因此，回归模型的正确设定是一个无法验证的假设。DR 估计量并没有消除对这种假设的需求，但它为分析者提供了两次满足假设的机会。

### 4.1.1 概念概述

双重稳健（DR）估计基于 Rosenbaum 和 Rubin (1983) 的倾向评分方法以及 Robins 同事的逆概率加权（IPW）方法（Robins, 1998; 1999a, 1999b; Robins et al., 2000）。DR 估计将倾向评分的逆概率加权与每个治疗下协变量与结局之间关系的回归建模相结合。其结合方式使得：只要倾向评分模型或结局回归模型之一被正确设定，且假设没有未测量的混杂因素，对结局的影响就是一致的（Robins et al., 1994; Robins, 2000; van deran and Robins, 2003; Bang and Robins, 2005）。具体而言，首先根据个体协变量（倾向评分）建立一个特定患者接受治疗概率的（第一个）回归模型。分别针对暴露人群和非预期人群构建极大似然回归模型，以预测作为混杂因素和风险因素函数的平均反应（结局）。这两组模型在图 4.1 中可视化。最后，每个个体观测值赋予一个权重，该权重等于其基线协变量接受治疗概率的倒数（如 IPW 分析所示），以创建两个代表在两种治疗条件下整个人群预期反应的受试者群体。模拟结果证实，当一个模型完全遗漏了一个重要的混杂因素时，估计量是一致的（Lunceford and Didian, 2004; Bang and Robins, 2005）；在更真实的场景下，当其中一个组件模型通过对连续变量进行分类而被误设定（而该变量与结局的真实关系是连续函数）时，也是一致的（Jonson Funk and Westreich, 2008）。

# 图 4.1 DR 估计量的组件模型

| 风险因素（潜在混杂因素） |
| :--- |
| 倾向评分模型 (1) |
| 结局回归 (2) |
| 暴露（治疗） |

DR 估计量是基于结局、协变量与治疗之间关系的回归模型估计因果效应的常规方法（使用标准倾向评分调整方法）的替代方案。如果结局回归模型被正确设定，那么因果效应的估计量在渐近上至少与 DR 估计一样无偏。然而，如果结局回归被误设定，得到的因果效应估计量可能与真实的因果效应一致。如果倾向评分或特定治疗的结局回归模型是正确的，估计量就是一致的；因此，为了这种额外的保护，DR 估计量可能会损失精度。

DR 效应估计具有边际解释，而非条件（基于协变量）解释，并且与从随机试验（即人群被随机分配接受治疗）中获得的效应估计具有直接可比性。由于标准结局回归模型的估计值具有条件解释，这两个估计值可能不一致，仅仅是因为它们在两个不同的目标人群中对效应取平均。特别是，这可能出现在效应倾向中（Kurth et al., 2006），或由于效应估计的不可收缩性（Stürner et al., 2006）。

### 4.1.2 统计表达式与假设

我们使用以下符号：`Y` 是观测反应，`Z` 是取 0 或 1 的二元治疗（暴露），`X` 代表基线协变量向量。`Y_1` 和 `Y_0` 是治疗和无治疗下的反事实反应（Hernán, 2004）。所有变量进一步由 `i=1, ..., n` 指定。在本例中，感兴趣的因果效应是所有人接受治疗与不接受治疗之间的均值差异。在以下方程中，`e(X,beta)` 是倾向评分的模型（来自逻辑回归），`m_1(X,alpha)` 和 `m_0(X,alpha)` 是协变量向量（混杂因素）与结局之间真实关系的回归模型。根据这些定义，估计量的因果效应为：

$$\hat{\Delta}_{DR} = n^{-1} \sum_{i=1}^{n} \left[ \frac{Z_i Y_i}{e(X_i, \hat{\beta})} - \frac{Z_i - e(X_i, \hat{\beta})}{e(X_i, \hat{\beta})} m_1(X_i, \hat{\alpha}_1) \right] - n^{-1} \sum_{i=1}^{n} \left[ \frac{(1-Z_i) Y_i}{1-e(X_i, \hat{\beta})} - \frac{1-Z_i - e(X_i, \hat{\beta})}{1-e(X_i, \hat{\beta})} m_0(X_i, \hat{\alpha}_0) \right] = \hat{\mu}_{1,DR} - \hat{\mu}_{0,DR}$$

DR 估计量的标准差使用 delta 方法估计（Casella and Berger, 2002）。DR 估计量的采样方差计算为：

$$SE_{\hat{\Delta}_{DR}} = \sqrt{n^{-2}\sum_{i=1}^{n} \hat{l}_i^2}$$

其中 `\hat{l}_i` 定义为：

$$\hat{l}_i = \frac{Z_i Y_i}{e(X_i, \hat{\beta})} - \frac{Z_i - e(X_i, \hat{\beta})}{e(X_i, \hat{\beta})} m_1(X_i, \hat{\alpha}_1) + \frac{(1-Z_i) Y_i}{1-e(X_i, \hat{\beta})} - \frac{1-Z_i - e(X_i, \hat{\beta})}{1-e(X_i, \hat{\beta})} m_0(X_i, \hat{\alpha}_0) - \hat{\Delta}_{DR}$$

## 88 使用 SAS 进行观察性护理数据的分析

如果满足以下假设，DR 估计量对于 Δ 的真实值是一致的：
1) 无未测量混杂因素（也称为可交换性假设）；2) 至少一个组件模型的设定是正确的；3) 阳性性（倾向评分被限制在 0 和 1 之间，因此在任何协变量组合下接受治疗的概率始终为正）；以及 4) 稳定单位处理值假设 (SUTVA)（Rubin, 1980），其包含一致性和无干扰性（Cox, 1958）。当样本量足够大，且倾向评分模型和结局回归模型均已正确设定时，使用德尔塔法（delta method）标准误是合适的。对于在倾向评分和结局回归模型未知且可能被错误设定的数据分析进行报告估计值时，应使用自助法（bootstrap）获取标准误差。

## 4.2 使用 DR 宏进行实现

虽然已有多种估计量发现了双重稳健倾向性（Robins et al., 2007），我们将描述由 Robins 及其同事（1994）确定的增强 IPW 估计量，该估计量随后被认为具有双重稳健性（Scharfstein et al., 1999）。这种 DR 估计量已在卡罗来纳大学亨蒂尔分校开发的 Base SAS 宏中实现（已通过 SAS 9.1.3 验证）。可以从 `http://harrygage.unc.edu/sas.htm` 的 Resources 部分下载该 DR 宏以及样本数据。本章反映了截至 1.0 版本的宏功能。请审阅 readme 文件（ReadMe.pdf），以获取有关设置和安装的重要信息以及更新后的功能细节。

### 4.2.1 快速上手

DR 宏运行一组模型：一个用于接收二分类化处理或暴露的概率（倾向评分），另一个用于预测暴露分层内结局的概率（针对二分类化结局）或其平均值（针对连续性结局）（特定处理的结局回归模型）。我们将在后续章节中描述每个模型语句的通用语法、可选命令的使用以及生成的输出。

### 4.2.2 设定权重模型

通用模型（或倾向评分模型）在第一个 MODEL 语句中使用以下形式指定：

```



`wtmodel exposure = <covariates> / method=dr dist=bin <other options>`

我们将暴露和处理放在效应的左侧，将其建模为右侧 `$t$` 个协变量的函数符号。`Method=dr` 表示应使用 DR 估计方法，而 `dist=bin` 表示这是一个二分类暴露。因此，将使用逻辑回归对协变量与暴露之间的关系进行建模。

在指定权重模型时，应保持与您基于知识设定任何其他 IPW 或基于倾向评分的模型时相同的关注细致程度和严谨性。Brookhart 及其同事（2006）发现，倾向评分（暴露）模型应包含所有混杂因素，以及那些作为结局风险因素的协变量。

包含与结局无关的协变量可能会导致最终感兴趣的影响估计量的方差增加，而不会减少偏倚，尽管 Greenland（2008）最近建议变量削减的净收益有限，且最好报告来自完整模型的结果。

为了评估阳性性假设，分析师可以调用 `WTATMODEL` 中的 `SHOWCURVES` 选项，生成两个治疗组的倾向评分分布图。为了限制敏感性分析的数据范围，分析师可能会输入另一个可选的 `common_support=number`，该数字在 0 到 1 之间（包含）。值 1 表示程序应使用整个共同支持区域进行反事实推断。值 0.8 表示程序应仅使用共同支持区域的 80%。如果应将缺乏共同支持限制在分布的一个尾部，则仅指定受影响尾部的那些观测值。当时尚没有选项允许在倾向评分值的某些重叠范围内定义一个非对称区域（例如，第 5 百分位到第 80 百分位）。如果没有指定 `common_support=number`，宏将使用所有可用数据，包括倾向评分分布不重叠的区域。此外，共同支持区域在 `SHOWCURVES` 选项生成的图中垂直线显示。

### 4.2.3 设定回归模型

结局回归模型在第二个 `MODEL` 语句中使用以下形式指定：

```
model outcome = <covariates> </options>
```

该模型将感兴趣的主要结局（连续型或二分类）建模为每个暴露组内协变量的函数。此处不应再次指定主要的暴露变量。选项应在斜杠（`/`）之后指定。`Dist` 表示模型形式为线性回归，具有正态误差分布。这适用于连续性结局。如果结局是二分类的，则 `dist=bin` 是合适的，并使用逻辑回归。

我们目前没有发现任何专门针对在 DR 估计背景下哪些变量应包含结局回归模型的研究，但我们建议分析师按照与单多变量回归模型相同的比例来开发此模型（Harrell, 2001）。

### 4.2.4 输出

DR 宏在结果面板中输出多个结果节点（位于主窗口左侧的垂直面板）。下面对这些节点中的每一个进行了描述。

- **逻辑：权重模型 (Logistic: Weight Model)**
  这是用于 DR 估计中倾向评分模型（`wtmodel`）部分的逻辑回归。宏中相关的 SAS 代码如下，其中 `&desc` 对应下降选项，`&wtm` 对应 `exposure = <covariates>` 形式：

```
proc logistic data=usedata_ &desc;

ods exclude modelinfo;

ods exclude nobs;

model &wtm;

output=_ps_ p=_ps;

run;
```

- **暴露概率描述性统计 (Print: Descriptive statistics for Exposure Probability)**
  该节点提供了按暴露组分层的估计倾向评分的均值、标准差以及最小值和最大值。

- **暴露组极值 (Print: Extreme Values by Exposure Group)**
  该节点提供了每个暴露组中最高和最低的倾向评分值。

- **按<暴露>分层的倾向评分曲线 (Univariate: Propensity Score Curves Stratified by <Exposure>)**
  这是通过指定的 `SHOWVES` 选项生成的按暴露组分层的倾向评分图。如果调用了 `COMMON_SUPPORT` 选项，此图具有指示共同支持区域的线条。程序 4.2 显示了直方图的 SAS 代码，其中 `&exp` 代表变量，`&cmsept` 是是否调用了共同支持的标记：

```
proc univariate noprint data=shrcvs;

var _ps;

class &expvar;

histogram _ps/kernel

%if &cmsept=1 then %do;

ref=(&lo_spt, &hi_spt)

%end;

run;
```

- **暴露=0 的观测信息 (Print: Observation Information for Exposure=0)**
  该节点报告了从原始数据集中读取的观测总数、无缺失协变量值的观测数，以及应用任何共同支持标准后用于回归模型的观测数。

- **逻辑 | GLM：暴露=0 的结局模型 (Logistic | GLM: Outcome Model for Exposure=0)**
  该节点报告第一个暴露组内结局回归的结果。如果 `MODEL` 的分布（`DIST=`）选项设置为 `bin`，则该节点标记为 Logistic；如果分布选项设置为 `normal`（`dist=n`），则该节点标记为 GLM。程序 4.3 显示了宏中用于二分类结局的相关 SAS 代码，其中 `&desc` 描述下降选项，`&out` 是 `outcome = <covariates>` 形式：

## 程序 4.3 来自 DR Macro v1.0 的用于二分类结局的暴露组内结局回归模型的 SAS 代码节选

```
title "Outcome Model for &expvar=&exp0 ";

proc logistic data=wgts0 &desc; noprint;

ods exclude modelinfo;

ods exclude nobs;

model=&outmod;

output out=_modres0(keep=__m0) p=__m0;

run;

title "Observation Information for &expvar=&expl1 ";

proc logistic data=wgts1 &desc; noprint;

ods exclude modelinfo;

ods exclude nobs;

model=&outmod;

output out=_modres1(keep=__ml) p=__ml;

run;
```

程序 4.4 显示了该宏中用于连续型、正态分布结局的相应 SAS 代码，以及结局 = <covariates> 时的显示内容。

# 程序 4.4 来自 DR Macro v1.0 的用于连续结局的暴露组内结局回归模型的 SAS 代码节选

```
title "Outcome Model for &expvar=&exp0 ";

proc glm data=wgts0_

model=&outmod;

output out=_modres0(keep=__m0) p=__m0;

run;

title "Outcome Model for &expvar=&expl1 ";

proc glm data=wgts1_

model=&outmod;

output out=_modres1(keep=__ml) p=__ml;

run;
```

- + 打印：暴露=1 的观测信息

该节点报告第二个暴露组从原始数据集中读取的观测总数、无协变量值的值的观测数，以及在应用任何共同支持标准后用于结局回归模型的观测数。

- + Logistic | GLM：暴露=1 的结局模型
该节点报告第二个暴露组内结局回归模型的结果。如果 `MODEL` 语句的分布（`DIST=`）选项被设置为 `bin`，则该节点被标记为 Logistic；如果分布选项设置为 `normal` (`dist=n`)，则该节点被标记为 GLM。来自宏的相关 SAS 代码显示在程序 4.3 和 4.4 中。

- + 打印：DR 估计

# 92 使用 SAS 进行观察性健康数据分析

该结果产生以下格式的输出：

## 在打印 DR 估计节点中显示的输出

| 总观测数 | 使用观测数 | STATIN=0 的模型均值 | STATIN=1 的模型均值 | deltadr | SEdeltadr | Z | Probz |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 10000 | 9858 | -10.6783 | -10.6744 | .00391438 | 0.023986 | 0.16319 | 0.87037 |

`Total Obs`（总观测数）是指定数据集中的观测数量。

`Used Obs`（使用观测数）是实际用于分析的观测数量。`Usedobs` 始终小于或等于 `totalobs`；当某些人的某些协变量存在缺失值或在 `WTMODEL` 语句中使用 `COMMON_SUPPORT` 选项时，`usedobs` 小于 `totalobs`。

`Exposure=0` 的模型均值是在假设人群中没有人接受治疗的假设对平均应答的估计。这是 `dr0` 的均值。

`Exposure=1` 的模型均值是在假设人群中每个人都接受治疗的假设对平均应答的估计。这是 `dr1` 的均值。

在连续结局的情况下，这是连续变量（如血压、胆固醇、体重）的均值。在二分类结局的情况下，这是结局的平均风险。这是受试者的预期均值应答，而不是平均受试者的期望；这两个值在线性模型中是相同的，但在逻辑回归模型中不是，这可能会导致差异。

`Deltadr` 是平均应答之间的差异 (`dr1-dr0`)。在连续结局的情况下，这是由于治疗或暴露导致的均值差异。在二分类结局的情况下，这是结局平均预测概率的差异，比较了每个人都暴露（或未治疗）的伪人群中的反应率与每个人都暴露（或已治疗）的伪人群中的反应率。

`Sedeltadr` 是与指标 `deltadr` 相关的 delta 方法标准误，只有在已知权重和结局回归模型被正确设定时才应报告。

# 第 4 章 治疗效应的双重稳健估计 93

`Z` 是基于 delta 标准误的 Z 分数。

`ProbZ` 是基于 Z 分数的 `deladr=0` 的双侧概率。与估计的标准误和 Z 分数一样，此 p 值应在已知权重和结局回归模型被正确设定时才报告。

程序 4.5 显示了 SAS 代码。

## 程序 4.5 来自 DR Macro v1.0 的用于计算暴露导致的均值差异 DR 估计和估计标准误的 SAS 代码节选

```
/*合并 M0 和 M1 */
data modresi0 (keep=&expvar&resvar _ps m0 ml exp01 res01);
merge ps_modresi0 modresi1;
  if ("&dec"="1") then do;
  ps_1=ps;
  m0-1=m0;
  ml-1=ml;
end;
run;
```

```
/* 创建 DR0 和 DR1 及其差异 DR1_DR0 */
data dr0;
set modresi0;
dr0=(exp01)*res0/(1-ps);
dr1=(exp01)*res1/(ps);
dr0=dr1-dr0;
run;
```

```
/* 获取 DR1_DR0 的均值、方差和 n */
/* DR0 和 DR1 的均值 */
proc means noprint data=dr0 varref=n
var dr0 dr1;
output=mdr0 (drop=_type) mean-deltadr dr0 dr1 var=i2;
run;
```

```
/* 获取差异的 SE */
/* 以及方差分量 */
data mdr01;
merge mdr0;
SEdeltadr=sqrt(i2/n);
v0=0;
run;
```

在二分类结局的情况下，输出中显示一个带有估计值的单独表格。显示以下参数及其标准误、Z 分数和 p 值。

`LogRiskRatio` 是风险的自然对数。此值返回风险比。

`LogOddsRatio` 是比率的自然对数。此值返回比率。

# 程序 4.6 来自 DR Macro v1.0 用于计算均值差异、相对风险、比值比率和估计标准误的 SAS 代码提取

```
/* 如果响应分布为二分类 */
/* 获取比例和比例标准误 */
if (&mdist=BINOMIAL or &mdist=B) then do;
/* 获取方差和协方差 */
ods listing;
proc cov data=dr01 varref=n;
var dr0 dr1;
ods output cov=cov_;
run;
ods listing;
data cov;
set cov_;
if n=1 then do;
v0=dr0;
v1=dr1;
end;
else do;
v1=dr1;
keep v0 v1;
output;
retain v0;
run;
/* 风险比、比率误差 */
/* 将协方差信息与均值合并 */
/* 获取均值函数的方差估计 */
data mdr01
merge mdr01_cov_
 导数 */
alo=1/(dr1*(1-dr1));
bllo=-1/(dr0*(1-dr0));
difference =am=1;
bm=-1;
/* 风险比 */
alr=dr1;
blrr=1/dr0;
/* 比率比和风险比 */
LogOddsRatio=log(dr1*(1-dr0))/((1-dr1)*dr0);
LogRiskRatio=log(dr1/dr0);
/* 描述性特殊处理 */
if ("&desc=") then do;
LogOddsRatio=-1*logoddsratio;
LogRiskRatio=-1*logriskratio;
end;
/* 标准误估计 */
SELogOddsRatio=sqrt((alo*v1+bllo*v0+2*alo*bllo)/n);
SEMeanDifference=sqrt((am*v1+bm*v0+2*am*bm)/n);
SELogRiskRatio=sqrt((alrr*v1+blrr*v0+2*alrr*blrr)/n);
drop alo am alr blrr v0 v1;
run;
```

# 第 4 章 治疗效应的双重稳健估计 95

## 4.3 样本分析

# 4.3.1 样本数据介绍

这里的示例基于 10,000 个人的模拟观察性队列。主要暴露是基线启动他汀类药物（`statin`, p[`statin=1`]=0.51）。主要结局是 `rmi1`（均值=-10.7, sd=4.7），代表基线和随访之间脂质水平的变化，以及 `mil`（p[`mil=1`]=0.9），代表队列随访期间急性心肌梗死的发生。数据集的结构为每人一条记录，个体位于行。由于这些数据是模拟的，我们知道暴露对结局的真实效应，以及协变量与暴露之间的真实关系。在两种情况下，使用他汀类药物对结局的真实效应均为零。虽然每个治疗组连续结局的真实均值为负（随访时相对于基线的脂质下降），但这些是模拟数据，这里描述的方法同样适用于具有均值的结局。暴露与结局之间的关联受七个变量的影响：四个连续变量（`Age`, `BMI`, `Chol` 和 `Exer`）和三个分类变量（`Hs`, `Smk` 和 `Hcvd`）。此外，还有一个仅是结局的风险因素（`Female`）以及两个仅是暴露的风险因素（`Black` 和 `Income`）。

要运行这些示例，请从 `http://hyguess.unc.edu/sas.htm` 下载模拟数据集，并创建一个指向您计算机上相应目录的 `SampleData` libname。

# 4.3.2 连续结局的 DR 分析

此示例代表对模拟数据的分析，其中感兴趣的暴露是使用他汀类药物（`statin`），感兴趣的结局是连续的心血管疾病评分（`rmi1`）。使用他汀类药物对结局的真实效应为零。在此分析中，权重（倾向评分）模型和回归模型均指定正确（见程序 4.7）：

```
Program 4.7 调用 DR Macro v1.0 分析 rmi1 结局
title "Continuous Example";n%dr(str(options data=sampledata.set descending;
model smk hcvd black bmi age chol exer
/ /method=dr dist=bin showcurves common=.99;
model rmi1=hs female smk hcvd bmi2 age2 chol exer /dist=n);
```



| LOGISTIC 过程 | 响应剖面 | 排序值 | statin | 总频率 |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 是 | 5073 | | |
| 2 | 否 | 4927 | | |

...更多结果...

## 最大似然估计分析

| 参数 | DF | 估计值 标准误 | 卡方 | Pr > ChiSq |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 截距 | 1 | -8.0728 | 0.2589 | 972.0943 | <0001 |
| hs | 1 | 0.3587 | 0.0457 | 61.7075 | <0001 |
| smk | 1 | -0.4534 | 0.0529 | 73.4696 | <0001 |
| hacvd | 1 | 0.9101 | 0.0563 | 260.9287 | <0001 |
| black | 1 | -0.6783 | 0.0489 | 192.5989 | <0001 |
| bmi | 1 | 0.0567 | 0.0040 | 152.1308 | <0001 |
| age | 1 | 0.1059 | 0.00352 | 323.4639 | <0001 |
| income | 1 | 6.417E-6 | 1.141E-6 | 29.2467 | <0001 |
| chol | 1 | 0.0181 | 0.00059 | 916.7688 | <0001 |
| exer | 1 | 0.0079 | 0.00097 | 74.0638 | <0001 |

...更多结果...

## 预测概率与观测响应的关联

| 一致百分比 | 77.8 | Somers' D | 0.557 |
| :--- | :--- | :--- | :--- |
| 不一致百分比 | 22.1 | Gamma | 0.558 |
| 相同百分比 | 0.2 | Tau-a | 0.279 |
| 对数 | 24949671 | D | 0.779 |

结果中的下一个节点显示了按暴露组分层的平均值、标准差和最大预测概率（或倾向评分）。这允许分析人员检查正性假设（positivity assumption）。该假设规定，对于每种特征组合，未暴露的概率必须不为（Cole and Hernán, 2008）。如果违反了正性假设，请考虑这是否为结构性非正性，即具有特定特征组合的个体无法接受其中一种暴露。结构性非正性的情况意味着这些观测值不应包含在分析中。分析也可能是非正性的情况，特别是当某些协变量是连续一时。回归模型平滑了这些非正性情况，但调查结果对违反正性假设的敏感性是有帮助的。

# 第 4 章 治疗效应的双稳健估计

### rmi1a 分析的输出节点：暴露概率的描述性统计

| 按暴露组分层的暴露概率描述性统计 | statin | 平均值 | 离差 | 最小值 | 最大值 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 否 | 0.38962 | 0.21121 | 0.01495 | 0.96883 |
| 是 | 0.62159 | 0.21006 | 0.03748 | 0.98576 |

`SHOWCURVES` 产生一个直方图，比较两个暴露水平的倾向评分分布（见图 4.2，由程序 4.2 生成）。允许分析人员视觉评估未暴露个体作为已暴露个体反事实的程度。

## rmi1a 分析的输出节点：按暴露分层的倾向评分曲线

### 图 4.2 按暴露分层的非参数平滑倾向评分分布 ![](img/fe9ff00f88baacd415480b2558c111.png)

`SUPPORT` 选项引导回归模型修剪位于倾向评分极端的观测值以支持敏感性分析。使用 `common_support=0.99`，回归模型限制在倾向评分处于 0.5 到 99.5 百分位之间的观测值。图 4.2 中的虚线表示数据的这部分边界。我们在此示例中仅使用它是为了说明在倾向评分的完整范围内并不需要它。

后续节点显示了未暴露组 (`statin=0`) 和暴露组 (`statin=1`) 的线性回归结果（程序 4.3）。使用的观测值数量可能少于数据的总观测数。在本示例中，由于使用了 `COMMON_SUPPORT` 选项，总观测数为 9858 而非 10000；其中 4857 个位于未暴露组，因此产生了结果。此外，没有完整协变量数据的观测值按个被剔除。

### rmi1a 输出节点：暴露=0 的 GLM 结果

| Statin=0 | |
| :--- | :--- |
| 读取的观测数 | 9858 |
| 使用的观测数 | 4857 |

| 参数 | 估计值 | 误差 | t 值 | Pr > t |
| :--- | :--- | :--- | :--- | :--- |
| 截距 | -35.24585 | 0.631799 | -55.33 | <0001 |
| hs | -0.967696 | 0.0268457 | -33.66 | <0001 |
| female | 1.501905 | 0.0296382 | 51.14 | <0001 |
| smk | 2.021088 | 0.0315237 | 64.08 | <0001 |
| hcvd | 0.2138445 | 0.0220194 | 5.7 | <0001 |
| bmi | 0.1263229 | 0.0004197 | 22.76 | <0001 |
| bmi2 | 0.07735688 | 0.02125689 | 3.53 | 0.04 |
| age | 0.0012105 | 0.00020904 | 5.79 | <0001 |
| chol | 0.1501818 | 0.00036380 | 137.93 | <0001 |
| exer | -0.0207654 | 0.00058327 | -35.60 | <0001 |

最后，在标记为 `DR Estimate` 的节点下，我们找到了结果（程序 4.5）。同样，在某些协变量缺失或在宏方法中使用 `COMMON_SUPPORT` 选项的情况下，使用的观测值数量可能少于观测总量。在 `Statin=0` 模型平均值下，我们找到了如果该队列中所有人都未暴露 (`statin=0`) 的估计平均值；同样在 `Statin=1` 模型平均值下，找到了如果该队列中所有人都已暴露 (`statin=1`) 的估计平均值。当我们正确指定两个模型时，平均治疗效应（也称为治疗引起的均差）的双稳健估计（delta DR）差异为 0.00，标准误为 0.02，p 值为 ...（使用 delta DR 的估计标准误差计算）。

## rmi1a 分析的输出节点：DR Estimate

### DR 估计

| 总观测数 | 使用观测数 | STATIN=0 模型平均值 | STATIN=1 模型平均值 | deltart | SEdeltar | Z | Probz |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 10000 | 9858 | -10.6783 | -10.6744 | .003 | | | |

包含治疗的标准线性回归结果可以获得，使用以下 SAS 代码：

```
proc reg data=sample;

model rmi1a=statin smk cvd;

run;
```

### 程序 4.8 标准线性模型

此模型的显示在此处。`statin` 的均差略大于 DR 估计 (.02)。由于 DR 估计使用了一个经过修剪的样本，因此这些是不可比的。

### 程序 4.8 标准线性回归

| 变量 | 估计值 | 误差 | t 值 | Pr > t |
| :--- | :--- | :--- | :--- | :--- |
| 截距 | -34.70314 | 0.4374 | -79.34 | <0001 |
| statin | -.01064 | 0.0229 | -0.48 | 0.6333 |
| hs | -0.96683 | 0.01994 | -48.48 | <0001 |
| female | 1.51607 | 0.02032 | 74.60 | <0001 |
| smk | 2.02120 | 0.02303 | 87.76 | <0001 |
| xcvd | 2.00006 | 0.02472 | 82.93 | <0001 |
| bmi1 | 0.10456 | 0.01507 | 6.94 | <0001 |
| bmi2 | -.00988 | 0.000789 | 36.57 | <0001 |
| age | 0.06559 | 0.01463 | 4.8 | <0001 |
| age2 | 0.01133 | 0.001356 | 9.77 | <0001 |
| chol | 0.05038 | 0.00038814 | 203.6 | <0001 |
| exer | -0.02034 | 0.00039787 | -51.13 | <0001 |

## 4.3.3 用于二元结果的 DR 分析

第二个示例代表了对模拟数据的分析，其中感兴趣的暴露是他汀类药物 (`statin`)，结果是表示受试者在随访期间是否发生心肌梗死的的二元变量 (`mil`)。当我们正确指定两个模型时，权重（倾向评分）模型和回归模型都是：

## 程序 4.9 用于 mi1 结果分析的 DR 宏 v1.0

```
title 'Dichotomous Example'

%dr(str(options data=sampledata.study descending;

wmodel statin=hs smk hcvd black bmi age age chol exer

/ method=dist-bin showcurves;

))
```

与之前一样，节点面板（nodes pane）中的第一个结果包含了用于倾向评分模型的逻辑回归模型的完整输出。由于我们使用了 `SHOWCURVES` 选项，还生成了两个倾向评分分布的图。结果是相同的，因为像上一个示例一样指定了相同的暴露因素和协变量。两个额外的逻辑回归节点：分别用于预测响应的第一个模型和未使用的第二个模型。我们关注的结果出现在 `Print: DR estimates`（程序 4.6）下。这些结果包含了人群中未治疗（dr0）或已治疗（dr1）结果风险（或概率）的 DR 估计值、风险差异（delta DR）、对数风险比以及优势比（odds ratio）。此外，还提供了每个参数的标准误、Z 分和 p 值。

## 来自 mi1 的输出节点：DR 估计

| 总观测数 | 使用观测数 | STATIN=0 的模型均值 | STATIN=1 的模型均值 |
| --- | --- | --- | --- |
| 1000 | 1000 | 0.19032 | 0.19540 |

| 参数 | StdErr | Z | ProbZ |
| --- | --- | --- | --- |
| Delta DR | 0.005081 | 0.005667 | 0.89660 | 0.36993 |
| Log Risk Ratio | 0.026347 | 0.029545 | 0.89174 | 0.37253 |
| Odds Ratio | 0.032641 | 0.036566 | 0.89292 | 0.37190 |

由于优势比的不可塌缩性（noncollapsability），将 DR 优势比的估计值与典型逻辑回归模型的估计值进行比较并没有特殊意义。相反，我们将 DR 风险比的估计值与使用 `GENMOD` 程序得到的风险估计值（Spiegelman and Hertzberg, 2005）进行比较。在这种情况下，使用泊松回归是因为二项回归存在收敛问题。

## 程序 4.10 使用泊松回归模型分析 mi1

```
title 'Estimate of RR using Poisson Regression';

proc genmod data=sampledata.study descending;

class by;

model mi=statin hs female smk hcvd bmi2 age age2 chol exer

/dist=poisson link=log;

repeated subject=i/type=ind;

estimate 'log RR statin' statin 1;
```



`logRR` 的估计值（0.12）比 `DR` 估计（0.03）更偏离真实值，且来自泊松回归的 `logRR` 标准误效率较低（0.04 对 0.03）。

## 程序 4.10 的输出——泊松回归模型

| 标签 | 估计值 | 标准误 | Alpha | 置信区间 | 限制范围 | 卡方 | Pr > ChiSq |
|---|---|---|---|---|---|---|---|
| Log RR statin | 0.1151 | 0.0402 | 0.05 | 0.0363 | 0.1939 | 8.20 | 0.0042 |
| Exp(log RR statin) | 1.1220 | 0.0451 | 0.05 | 1.0370 | 1.2140 | | |

> 在提供的示例中，使用了倾向评分和结果模型的真实形式，但也可以通过使用此样本数据故意误设其中一个模型，来探索该方法的稳健性。

## 4.4 总结

鉴于我们很少知道暴露、结果和混杂因素之间的真实关系，`DR` 估计是获取药物、设备和其他干预措施（预期和非预期）效应的观察性研究中更稳健效应估计的潜在有价值工具。该 `SAS` 宏描述了这种方法，应用相对简单。

### 4.4.1 局限性

鉴于我们很少知道暴露、结果和混杂因素之间的真实关系，`DR` 估计是获取药物、设备和其他干预措施（预期和非预期）效应的观察性研究中更稳健效应估计的潜在有价值工具。该 `SAS` 宏描述了这种方法，应用相对简单。

### 4.4.2 实用考虑

鉴于我们很少知道暴露、结果和混杂因素之间的真实关系，`DR` 估计是获取药物、设备和其他干预措施（预期和非预期）效应的观察性研究中更稳健效应估计的潜在有价值工具。该 `SAS` 宏描述了这种方法，应用相对简单。

### 4.4.3 持续调查领域

鉴于我们很少知道暴露、结果和混杂因素之间的真实关系，`DR` 估计是获取药物、设备和其他干预措施（预期和非预期）效应的观察性研究中更稳健效应估计的潜在有价值工具。该 `SAS` 宏描述了这种方法，应用相对简单。

## 4.5 结论

鉴于我们很少知道暴露、结果和混杂因素之间的真实关系，`DR` 估计是获取药物、设备和其他干预措施（预期和非预期）效应的观察性研究中更稳健效应估计的潜在有价值工具。该 `SAS` 宏描述了这种方法，应用相对简单。

# 第 4 章 治疗效应的双重稳健估计

`SAS` micro 通过对一个模拟观察性队列进行两个样本分析，说明了该宏的用方法，并讨论了分析师在使用这种方法时应该考虑的几个问题。

# 参考文献

- Bang, H., and J. M. Robins. 2005. “缺失数据和因果推断模型中的双稳健估计.” Biometrics 61(4): 962–973.
- Brookhart, M. A., S. Schneweweiss, K. J. Rothman, R. J. Glynn, J. Avorn, and T. Stürmer. 2006. “倾向评分模型的变量选择.” American Journal of Epidemiology 163(12): 1149–1156.
- Casella, G., and R. L. Berger. 2001. 统计推断. Australia: Dbury Press.
- Cole, S. R., and M. A. Hernán. 2008. “构建边际结构模型的逆概率权重.” American Journal of Epidemiology 168(6): 656–64.
- Cox, D. R. 1958. 实验设计. New York: John Wiley & Sons, Inc.
- Greenland, S. 2008. “受邀评论：多重混杂因素控制中的变量选择收缩.” American Journal of Epidemiology 167(5): 523–529; 讨论
- Harrell, F. E. 2001. 回归建模策略：及其线性模型、线性回归和生存分析的应用. New York: Springer-Verlag.
- Hernán, M. A. 2004. “流行病学研究的因果效应定义.” Journal of Epidemiology and Community Health 58(4): 265–71.
- Jonsson Frank, M. L., and D Westreich. 2008. “模型误偏的真实条件下的双稳健估计.” Pharmacopoeiology and Drug Safety 17(S1): S106.
- Kang, J. D., and J. L. Schafer. 2007. “揭秘双稳健：从不完整数据中估计人群的替代策略比较（含讨论）. Statistical Science 22(4): 525–580.
- Kurth, T., A. M. Walker, R. J. Glynn, K. A. Chan, J. M. Gaziano, K. Berger, and J. M. Robins. 2006. “在非均匀效应条件下，多变量逻辑回归、倾向性匹配、倾向性调整和基于倾向性的加权的结果.” American Journal of Epidemiology 163(3): 262–270.
- Lunceford, J. K., and M. Davidian. 2004. “因果治疗效应估计中的分层与加权：一项比较研究.” Statistics in Medicine 23(19): 2937–2990
- Petersen, M. L., Y. Wang, M. J. van der Laan, and D. Ransberg. 2006. “评估抗逆录病毒治疗干预的有效性：使用边际结构模型复制随机对照试验的发现.” Journal of Acquired Immune Deficiency Syndromes 43: S96–S103.
- Robins, J. M. 1997. “边际结构模型.” In ASA Proceedings on the Section on Bayesian Statistical Science. Alexandria, VA: American Statistical Association, 1–10.
- Robins, J. M. 1999a. “等效性试验中不从从修正.” Statistics in Medicine 17(3): 269–302; 讨论 387–389.
- Robins, J. M. 1999b. “关联、因果与边际结构模型.” Synthesis 121: 151–179.
- Robins, J. M. 1999b. “作为因果推断工具的边际模型与结构嵌套模型.” In Statistical Models in Epidemiology: The Environment and Clinical Trials. Edited by M. E. Halloran and D. Berry. IMA 116: 95–134. New York: Springer-Verlag.
- Robins, J. M. 1999c. "顺序缺失数据和因果推断模型中的稳健估计." In ASA Proceedings on the Section on Bayesian Statistical Science 6-10.
- Robins, J. M., A. Rotnitzky, and L. P. Zhao. 1994. "当某些回归变量并非总是观测到时的回归系数估计.” Journal of the American Statistical Association 89: 846–886.
- Robins, J. M., M. A. Hernán, and D. Brumback, 2000. "流行病学中的边际结构模型和因果推断.” Epidemiology 11(5): 550–50.

# 第 5 章使用 SAS 进行倾向性评分数据分析

- 摘要 ............................................................................104
- 倾向性评分......................................................................105
- 5.1 引言...........................................................................105
- 5.2 倾向性评分的示例...............................................................107
- 5.3 缺失数据下的治疗效应估计使用 SAS..................................109
- 5.4 敏感性分析..................................................................124
- 5.5 讨论...........................................................................128
- 参考文献...........................................................................128

## 摘要

倾向性评分在观察研究中被广泛用于，以减少治疗分配的偏倚。本章讨论了在存在缺失值的情况下，使用倾向性评分估计治疗效应的各种方法。

# 第 5 章使用 SAS 进行倾向性评分数据分析

- 摘要 ............................................................................104
- 倾向性评分......................................................................105
- 5.1 引言...........................................................................105
- 5.2 倾向性评分的示例...............................................................107
- 5.3 缺失数据下的治疗效应估计使用 SAS..................................109
- 5.4 敏感性分析..................................................................124
- 5.5 讨论...........................................................................128
- 参考文献...........................................................................128

## 摘要

倾向性评分在观察研究中被广泛用于，以减少治疗分配的偏倚。本章讨论了在存在缺失值的情况下，使用倾向性评分估计治疗效应的各种方法。

## 第 5 章 缺失值下的倾向评分

最近，Qu 和 Lipkovich (2009) 开发了一种名为“多重插补缺失模式”（`MIMP`）的新方法，该方法在估计倾向评分时不仅利用多重插补方法，还利用了数据的模式。在这种方法中，使用多重插补程序对缺失数据进行插补。然后，通过一个逻辑回归模型估计倾向评分，该模型包含了协变量（带有缺失值）以及一个指示每个观测值缺失模式的因子（一组指示变量）。模拟结果显示，当缺失机制为“完全随机缺失”或“随机缺失”时，`MIMP` 的性能与 `MI` 持平且优于 `MP`；当数据不是随机缺失时，其性能优于 `MI`（Qu and Lipkovich, 2009）。

我们将使用一个骨质疏松症临床试验的数据示例，展示在某些协变量存在缺失的情况下，如何使用 `CC`、`IND`、`MP` 和 `MIMP` 方法来估计倾向评分。使用这些倾向评分来估计治疗效应有许多方法，包括回归、分层、逆概率加权、匹配以及这些方法的某些组合（这些方法的详细讨论请参见第 2-4 章）。注意，本章讨论的每种估计倾向评分的方法都可以与任何估计治疗效应的倾向评分方法相结合。在本章中，为了说明，我们使用逆概率加权（`IPW`）法来估计治疗差异。然而，`IPW` 为治疗差异提供了一个更稳定的估计量。因此，在本章中我们使用标准化的 `IPW` 估计。

具体而言，治疗效应被估计为组间平均结局的差异：

```
```



$$\hat{\delta}_0 = \left(\sum_{j=1}^{n}(1-T_j)(1-\hat{p}_j)^{-1}\right) - \left(\sum_{j=1}^{n}(1-\hat{p}_j)^{-1}Y_j(1-T_j)\right)$$

$$\hat{\delta}_1 = \left(\sum_{j=1}^{n}T_j\hat{p}_j^{-1}\right) - \left(\sum_{j=1}^{n}\hat{p}_j^{-1}Y_jT_j\right)$$

个体倾向评分 $\hat{p}_j$ 是通过上述的逻辑回归模型估计的（Lunceford and Davison, 2004）。

## 5.2 数据示例

在本节中，我们将估计倾向评分时处理缺失数据的五种方法应用于一组来自骨质疏松研究的数据：雷洛昔芬评价多结局研究（MORE） (Delmas et al., 2002）。在这项研究中，7,705 名患有骨质疏松的女性被随机分配到三组，比例为 1:1:1，分别接受安慰剂、每天 60 mg 雷洛昔芬或每天 120 mg 罗罗奈特，并随访了 4 年。在随访 3 年后，允许女性服用双膦酸盐等其他骨活性药物。在本次分析中，我们比较了最初随机分配到安慰剂的 1,643 名女性中，未服用双膦酸盐的女性（在本分析中称为未治疗组，`T=0`）与服用双膦酸盐的女性（治疗组，`T=1`）在第四年期间骨颈部矿物质密度（BMD）的变化。我们评估治疗差异的主要分析是针对结局（`Y`）相对于治疗组（`T`）的方差分析（ANOVA）。然而，由于双膦酸盐不是随机因子，治疗组和未治疗组中的响应变量 `Y` 可能因为选择偏倚而混杂。因此，我们使用加权 ANOVA 模型，权重为估计的接受治疗概率倒数的标准化。由于 SAS 中的 `PROC MIXED` 在分析前会自动对权重进行标准化，因此无需在 SAS 程序中显式计算标准化权重。这些倾向评分是使用包含 16 个协变量的逻辑回归模型估计的（表 5.1）：基线年龄（随机化前）、基线体重指数（BMI）、腺癌家族史、基线 5 年腺癌风险评分（Costantino et al., 1998）、基线接受过子宫切除的女性、基线腰柱 BMD、基线骨颈 BMD、前 3 年内腰柱 BMD 的变化、之前的激素替代疗法状态、基线非椎骨骨折、前 3 年内非椎骨骨折、前 3 年内椎骨骨折（计算为 `AE + 2*AE + 3*AE + 4*AE`）、基线吸烟状况以及半定量骨折状态（0-无骨折，1-骨折，2-中度骨折，3-严重骨折）。该分析共纳入 1,631 人（`T=0` 为 1512 人，`T=1` 为 131 人），其中 603 人（36.7%）至少有一个缺失协变量。表 5.1 显示了最初接受安慰剂女性的变量名称和缺失值数量。1,040 个没有缺失协变量的 14 种不同模式，每种模式仅一个一个。

### 表 5.1 数据集中的变量

| 变量名称 | 变量描述 | 缺失观测值 |
| :--- | :--- | :--- |
| `AGE` | 基线年龄 | 0 |
| `BMI` | 基线体重指数（BMI） | 1 |
| `GAILMORE` | 5 年腺癌风险评分 | 5 |
| `LSC` | 前 3 年腰柱 BMD 的变化 | 6 |
| `LTOTBM` | 基线腰柱 BMD | 6 |
| `FNC` | 前 3 年骨颈 BMD 的变化 | 0 |
| `NECKBM` | 基线骨颈 BMD | 0 |
| `AESCORE` | 前 3 年加权事件评分 | 0 |
| `SQ` | 基线半定量骨折状态（0-无骨折，1-骨折，2-中度骨折，3-严重骨折） | 9 |
| `FAMHX` | 腺癌家族史 | 41 |
| `KHYSYN` | 基线是否接受过子宫切除 | 0 |
| `NVFX` | 前 3 年内非椎骨骨折 | 0 |
| `PREVH` | 激素替代疗法状态 | 3 |
| `PREVERT` | 基线流行性骨折 | 8 |
| `SMOKE` | 基线吸烟状况 | 23 |
| `VFX` | 前 3 年内椎骨骨折 | 8 |
| `FNBMD_C` | 第四年骨颈 BMD 的变化（结局变量） | 0 |
| `BIMORE` | 服用双膦酸盐对比治疗组 | 0 |

## 5.3 使用 SAS 进行缺失值的 IPW 估计

SAS 过程（`MEANS`、`GLM` 和 `MIXED`）在分析前会自动对权重进行标准化。因此，尽管 SAS 程序中没有标准化权重的显式代码（倾向评分的倒数），但实际上对所有处理数据的方法都执行了标准化的 IPW 估计。

### 5.3.1 完全协变量（CC）分析

CC 方法简单地排除至少有一个缺失协变量的观测值。程序 5.1 显示了执行 CC 分析的 SAS 代码，程序 5.1 的输出显示了结果。

#### 程序 5.1 完全协变量（CC）分析

```sas
PROC FORMAT;
    VALUE FORMATYN 0 = 'NO'
    1 = 'YES';
RUN;

****************************************************************
* 完整协变量 (CC) 分析;
****************************************************************

PROC LOGISTIC DATA = ANALDATA NOPRINT;
    MODEL BIMORE = &VARLIST;
    OUTPUT OUT=PRED PREDICT=P;
RUN;

DATA PRED;
    SET PRED;
    IF BIMORE = 0 THEN PROB = P;
    IF BIMORE = 1 THEN PROB = 1-P;
    W = 1/PROB;
RUN;

PROC SORT DATA=PRED;
    BY BIMORE;
RUN;

TITLE '使用完整协变量 (CC) 方法的结果';
PROC MIX DATA = PRED;
    CLASS BIMORE;
    MODEL FNMOD_C = BIMORE;
    WEIGHT W;
    FORMAT BIMORE FORMATYN;
    LSME BIMORE/DIFF=ALL;
RUN;
```

#### 程序 5.1 输出

使用协变量 (CC) 方法的分析结果

混合过程

| | MORE 第 4 年使用双膦酸盐 | 最小平均值 标准估计 误差 DF 值 Pr > |t| |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 效应 | `BIMORE` | No | -0.00225 | 0.001224 | 1038 | -1.84 | 0.0668 |
| | `BIMORE` | Yes | 0.006120 | 0.001180 | 1038 | 5.17 | <0.0001 |

最小平均值差异

| MORE 第 4 年使用双膦酸盐 | MORE 第 4 年使用双膦酸盐 标准估计 误差 DF t 值 Pr > |t| |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `BIMORE` No | Yes | -0.00835 | 0.001700 | 1038 | -4.91 | <0.0001 |

### 5.3.2 指示变量（IND）分析

IND 方法是分类数据的一种直接方法，将缺失值视为一个特殊类别。对于连续变量，我们通常用边缘均值插补缺失值，并创建一个指示变量来表示缺失。程序 5.2 显示了执行 IND 分析的 SAS 代码，程序 5.2 的输出显示了结果。

```sas
ARRAY XC(7) FAMHBCN KHYSYS NVFX PREVHT PREVVERT SMOKE VFX;
DO I = 1 TO 7;
IF XC(I) = . THEN XC(I) = -1;
END;
```

```sas
PROC LOGISTIC DATA = ANALDATA IV NOPRINT;
CLASS FAMHBCN KHYSYS NVFX PREVHT PREVVERT SMOKE VFX;
MODEL BISMORE &LIST M1-M9;
OUTPUT OUT=PRE PREDICTED=P;
```

```sas
DATA PRED;
SET PRE;
IF BISMORE = 0 THEN PROB = P;
IF BISMORE = 1 THEN PROB = 1-P;
W = 1/PROB;
```

```sas
PROC SORT DATA=PRED;
BY BISMORE;
RUN;
```

```sas
'使用指示变量 (IND) 方法的分析结果';
PROC MIXED DATA = PRED;
CLASS BISMORE;
MODEL FWMQ_C = BISMORE;
WEIGHT W;
LSMEANS BISMORE/DIFF=ALL;
FORMAT BISMORE FORMATYN.
RUN;
```

#### 程序 5.2 的输出

使用指示变量 (IND) 方法的分析结果

混合过程 (Mixed Procedure)

| 最小二乘均值 | | | | | | |

| MORE 第四年使用双膦酸盐的情况 | 标准误差 | DF | t 值 | Pr > |t| |

| --- | --- | --- | --- | --- | --- |

| `BISMORE` 否 | -0.00217 | 0.001031 | 1641 | -2.11 | 0.0354 |

| `BISMORE` 是 | 0.008131 | 0.000995 | 1641 | 8.17 | <.0001 |

| 最小二乘均值的差异 | | | | | | |

| MORE 第四年使用双膦酸盐的情况 | 标准误差 | DF | t 值 | Pr > |t| |

| --- | --- | --- | --- | --- | --- |

| `BISMORE` 是 | -0.01030 | 0.001433 | 1641 | -7.19 | <.0001 |

### 5.3.3 多重插补 (MI) 分析

对分类预测变量应用多重插补可能具有挑战性，因为大多数市面上用的 MI 统计软件都是基于正态性假设处理连续数据的。遗憾的是，目前 SAS 中没有方便地对分类协变量进行多重插补的程序。

作为替代方案，我们可以为分类变量创建虚拟变量，并将虚拟变量视为连续变量进行 MI，这非常适用于二分类变量。例如，令 `X=1` 表示基线时吸烟的受试者，`X=0` 表示未吸烟的受试者。`X` 的插补值可以是 0.4，表示该受试者有 40% 的概率吸烟。这比将概率向下取整为 0（不吸烟）可能为患者提供更多信息。在本章中，我们将对缺失的二分类预测变量进行概率插补，而不进行向下或向上取整。

在基于倾向性的治疗效应估计背景下应用 MI 推断时，另一个困难是，使用合并规则（Rubin, 1987）可能会导致方差估计量无效，因为没有考虑到权重中的不确定性。Rubin 的方差估计量可能不合适的另一个原因是个人的模型（针对基线协变量）和分析（针对治疗效应）可能不兼容。更多信息请参见 Meng (1994)、Wang and Robins (1998) 以及 Robins and Wang (2000)。改进方差估计量的一种通用方法是对整个估计过程进行自助（bootstrapping）。可以使用 SAS 自助宏套件轻松完成，并实现各种基于自助的置信区间（http://cube.hort.ncedu/curcurbit/software/pathas/jackboot.txt）。在 5.3.6 节中，我们将概述如何使用这种方法。

程序 5.3 显示了执行 MI 分析的代码，程序 5.3 的输出显示了结果。程序 5.3 展示了当使用 `PROC MI` 插补缺失值时如何计算点估计量。本质上，它是由多重插补生成的样本估计值的平均值。

#### 程序 5.3 多重插补 (MI) 分析

```sas
********************************************************************
* 使用多重插补 (MI) 方法的分析结果；
********************************************************************

PROC MI DATA = ANALALDATA ROUND=.001 NIMPUTE=5 SEED=6731205
OUT_IMPUTATED_DATA NOPR
 VAR &LIST FNBBMD C BISMORE;
RUN;
```

```sas
PROC LOGISTIC DATA = IMPUTED DATA NOPR;
  MODEL BISMORE = &LIST;
  OUTPUT OUT=PRE PREDICTED=P;
  BY _IMPUTATION_;
RUN;
```

```sas
DATA PRED;
  SET P;
  IF BISMORE = 0 THEN PROB = P;
  IF BISMORE = 1 THEN PROB = 1-P;
  W = 1/PROB;
RUN;
```

```sas
PROC SORT DATA=PRED;
  BY _IMPUTATION_ BISMORE;
RUN;
```

```sas
ODS LISTING CLOSE;
ODS OUTPUT LSME = LSM DIFFS=DIFFS;
```

第5章 含有缺失值的倾向性评分 13

```sas
PROC MIXED DATA = PRED;
CLASS BISMORE;
MODEL FWMQ_C = BISMORE;
WEIGHT W;
BY _IMPUTATION;
LSMEANS BISMORE/DIFF=ALL;
DS LISTING;
TITLE '使用多重插补 (MI) 方法的分析结果'
TITLE2 '治疗组的估计值'
PROC MEANS DATA=LSM;
CLASS BISMORE;
VAR ESTIMATE;
FORMAT BISMORE FORMATYN.
RUN;
```

```sas
TITLE2 '差异的估计值';
PROC MEANS DATA = DIFFS;
VAR ESTIMATE;
RUN;
```

#### 程序 5.3 的输出

使用多重插补 (MI) 方法的分析结果

治疗组的估计值

均值过程

| 分析变量 | N | 均值 | 标准差 | 最小值 |

| --- | --- | --- | --- | --- |

| MORE 第四年使用双膦酸盐 - 否 | 5 | -0.0021606 | 0.001031 | -0.0021784 |

| MORE 第四年使用双膦酸盐 - 是 | 5 | 0.0083319 | 0.00019179 | 0.0081303 |

多重插补 (MI) 方法的分析结果

差异的估计值

均值过程

| N | 均值 | 标准差 | 最大值 |

| --- | --- | --- | --- |

| 5 | -0.0105103 | 0.0018904 | -0108240 |

以下 SAS 代码使用 `PROC ANALYZ` 生成治疗效应的 MI 估计。具体而言，它分三个步骤：首先通过多变量正态模型（`PROC MI`）创建没有缺失值的多个数据集，然后计算每个完成数据集的治疗效应估计值（`PROC MIXED`），最后使用 Rubin 合并规则（`PROC ANALYZ`）计算治疗效应的单一 MI 估计量及相关的 95% 置信区间 (CI)。

使用 SAS 分析观察性健康数据

注意，`PROC MI` 对于 SAS 8 和 9 的输入数据集 `PARMS` 和 `COVB` 有不同的格式。还要记住，由于此处原因，来自 MI 的方差估计量可能是无效的。程序 5.4 显示了使用 `PROC MI` 汇总 MI 方法估计值的 SAS 代码，输出 5.4 显示了结果。

#### 程序 5.4 使用 PROC MI 汇总 MI 方法的估计值

```sas
TITLE2 '使用 PROC MI 估计差异';
DATA FOR MI_EST (KEEP = IMPUTATION_ ESTIMATE RENAME=(EFFECT=PARAMETER));
  SET DIFFS;
  EFFECT = 'DIFF';
RUN;
```

```sas
DATA FOR MI_COV (KEEP = IMPUTATION_ ROWNAME BISMORE);
  SET DIFFS;
  DIFF = STDERR;
  ROWNAME = "DIFF";
RUN;
```

```sas
PROC MI PARMS=FOR_MI_EST COVB=FOR_MI_COV;
MODEEFFECTS DIFF;
ODS Output PARAMETERIMATES=MI_EST VARIANCEINFO=MI_VAR;
RUN;
```

#### 程序 5.4 的输出

使用多重插补 (MI) 方法的分析结果

使用 MI 估计差异

MI 过程

模型信息

`PARMS` 数据集 `WORK.FOR_MI_EST`

`COVB` 数据集 `WORK.FOR_MI_COV`

插补次数 5

多重插补方差信息

| 参数 | 组间 | 组内 | 总计 | DF |

| --- | --- | --- | --- | --- |

| `DIFF` | 3.573947E-8 | 0.000002072 | 0.000002115 | 9729.1 |

多重插补方差估计

| | 方差的相对增加 | 缺失信息比例 | 相对效率 |

| --- | --- | --- | --- |

| `DIFF` | 0.020696 | 0.020478 | 0.995921 |

| 参数 | 估计值 | 标准误差 | 95% 置信限 | DF |

| --- | --- | --- | --- | --- |

| `DIFF` | -0.010510 | 0.001454 | -0.01336 | -0.00766 | 9729.1 |

多重插补参数估计值



| 参数 | 最小值 | 最大值 | Theta0 参数=Theta0 | Pr > |t| |
| --- | --- | --- | --- | --- | --- |
| DIFF | -0.010824 | -0.010316 | 0 | -7.23 | <.0001 |

# 第5章 含有缺失值的倾向性评分

传递给 `PROC MIAN` 的两个数据集包含估计的治疗效应（数据集 `FOR_MI_EST`）及其相关的协方差矩阵（数据集 `FOR_MI_COV` 中的标准误差平方）。`PROC MIAN` 的输出包含总方差划分的信息，包括插补间和插补内的估计效应方差、多重插补参数、基于 t 分布的近似 95% 置信区间以及总方差。注意，对于有限次数的插补 (`M`)，Rubin 的方差估计量是不一致的，因为它具有非退化的卡方极限分布。因此，基于正态分布的 Wald 类型推断是无效的，使用的是 t 分布（Rubin, 1987）。缺失协变量对最终效应估计的影响也可以缺失信息比例（关于治疗效应）进行评估，在本例中该比例非常低（仅 2%）。

## 5.3.4 缺失模式 (MP) 分析

MP 方法通过仅包含缺失模式内的无值对每个缺失模式单独估计倾向性评分。因此，倾向性评分模型中的自变量在模式之间不同。实施 MP 的挑战通常是某些模式的样本量较小，导致模型估计不稳定。为了解决这个问题，我们开发了一种算法，根据相似性对小模式进行合并，以达到每个池指定的最小观测数（Qu and Lipkovich, 2009）。在合并相似模式后，我们使用边缘均值对每个池进行插补（以避免空洞），并使用逻辑回归模型估计倾向性评分。在本例中，我们将每个合并单元格具有至少 100 个观测值的缺失模式进行了合并。程序 5.5 提供了创建这些模式的宏。

### 116 使用 SAS 进行观察性健康数据分析

```sas
/* 创建缺失值及其缺失模式的指标 */
DATA MS;
SET &MSDATA;
ARRAY MS(&&MISSING) M1-M&MISSING;
ARRAY X(0:&&MISSING) &VARLIST;
MV = 0;
DO I = 1 TO &MISSING;
  IF X(I) = . THEN MS(I) = 1;
  ELSE MS(I) = 0;
  MV = 2*MV + MS(I);
END;
MV = MV + 1;
```

```sas
RUN;

/* 为每个缺失模式仅保留一条记录 */
PROC SORT DATA = MS OUT = PAT NODUPKEY
BY MV;
RUN;
```

```sas
/* 计算每个缺失模式中的观测数 */
PROC FREQ DATA = MS NOPRINT;
TABLE MV / OUT = M_MP (KEEP = MV COUNT);
RUN;
```

```sas
DATA PATTERN;
MERGE PATTERN M_MP;
BY MV;
RUN;

PROC SORT DATA = PATTERN;
BY DESCENDING COUNT;
RUN;
```

```sas
/* 从大到小将缺失模式分配给新索引 */
DATA PATTERN;
RETAIN MI1-M&MISSING MV COUNT MV_S;
SET PATTERN;
KEEP MI1-M&MISSING MV COUNT MV_S;
M_S = _N;
RUN;
```

```sas
PROC IML;
USE PATTERN;
READ ALL INTO A;
CLOSE PATTERN;
MS = A[, 1:&&MISSING];
MV = A[, 1*&MISSING];
N_MP = A[, 2*&MISSING];
MV_S = A[, 3*&MISSING];
```

```sas
M = ROW(MS);
M = NCL(MS);
```

```sas
/* 计算缺失模式之间的距离 */
DISTANCE = J(M, M, 0);
DO I = 1 TO M_MP;
  DO J = 0 TO M;
    DO L = 1 TO M;
      D = D + ((MS[I,L]-MS[J,L]) * (MS[I,L]-MS[J,L]));
    END;
  END;
```

## 第 5 章 带有缺失值的倾向评分 117

```sas
DISTANCE[I, J] = D;
DISTANCE[J, I] = D;
END;
I = 0;
M MV_POOL = 0;
MV_POOL = J(M_MP, 1, 0);

/* 根据相似性合并较小的缺失模式，
   使每个模式中达到预设的最小观测数 (&N_MP_MIN) */
DO WHILE (I < M_MP)
  I = I + 1;
  IF MV_POOL[I] = 0 THEN
    DO;
      K_MV_POOL = K_MV_POOL + 1;
      N_MP_POOL = N_MP[I];
      IF N_MP_POOL >= &N_MP_MIN THEN
        MV_POOL[I] = K_MV_POOL;
      END;
      ELSE
        IF I < M_MP THEN
          DO;
            A = DISTANCE([I+1]:MP, MP];
            B = MV([I+1]:M, MP);
            C = N_MP([I+1]:M, MP);
            D = MV([I+1]:M, MP);
            E = MV_POOL([I+1]:M, MP);
            TT = A || B || C || D || E;
            CALL SORT(TT, (1, 3));
            J = 0;
            DO WHILE (N_MP_POOL < &N_MP_MIN) AND (I+J < M_MP )
              J = J + 1;
              IF (TT[J,5] = 0) THEN
                DO;
                  N_MP_POOL = N_MP_POOL + TT[J,3];
                END;
              END;
            END;
          END;
      IF (N_MP_POOL >= &N_MP_MIN) THEN
        DO;
          MV_POOL[I] = K_MV_POOL;
          DO K = 1 TO J;
            MV_POOL[TT[K,4]] = K_MV_POOL;
          END;
        END;
      ELSE
        DO J = I TO M_MP;
          SGN_TMP = 0;
          K = 1;
          DO WHILE (SGN_TMP = 0 AND K <= M_MP)
            IF (DISTANCE[J,L] = 0 AND MV_POOL[J] = 0) THEN
              DO;
                MV_POOL[J] = MV_POOL[L];
                SGN_TMP = 1;
              END;
          END;
        END;
  END;
```

## 118 观察性健康数据分析

```sas
END;
K = K + 1;

END;
END;
MV_FINAL = MV || MV_POOL;

VARNAMES=('MV', 'MV_POOL');
CREATE MV_POOL FROM MV_FINAL(VARNAMES);
APPEND FROM_FINAL;

PROC SORT DATA = MVPOOL;
BY MV;
RUN;

PROC SORT DATA = MS;
BY MV;
RUN;

/* 变量POOL 表示合并后的缺失模式 */
DATA &OUTDATA(RENAME=(MV=MP, MV_POOL=MP));
MERGE MS MVPOOL;
BY MV;
RUN;

%MP_ASSIGN;
```

## 程序 5.6 缺失模式 (MP) 分析

```sas

****************************************************************

缺失模式 (MP) 方法;

****************************************************************

%MP_ASSIGN(MSDATA = ANALALATA, OUTDATA = ANALAL2, VARLIST = &VARLIST,

N_MP_MIN = 100);

PROC MEANS DATA = ANALALATA NOPRINT;

VARLIST;

OUTPUT OUT = MN = XM1-XM16;

BY STUDY;

DATA TEMP;

MERGE ANALALATA MN;

BY STUDY;

RUN;

DATA TEMP;

SET TEMP;

ARRAY X(16) &VARLIST;

ARRAY XM(16) XM1-XM16;

```

第 5 章 带有缺失值的倾向评分 119

```sas

DO I = 1 TO 16;

  IF X(I) = . THEN X(I) = XM(I);

END;

DROP I;

RUN;

PROC SORT DATA = TEMP;

BY MP;

RUN;

PROC LOGISTIC DATA = TEMP NOPRINT;

CLASS BISMORE = &VARLIST;

OUTPUT OUT=PRED PREDICTED=P;

BY MP;

RUN;

DATA PRED;

SET PRED;

IF BISMORE = 0 THEN PROB = P;

IF BISMORE = 1 THEN PROB = 1-P;

W = 1/PROB;

RUN;

PROC SORT DATA=PRED;

BY BISMORE;

RUN;

TITLE '缺失模式 (MP) 方法分析';

PROC MIXED DATA = PRED;

CLASS BISMORE;

MODEL P = BISMORE;

WEIGHT W;

LSMEANS BISMORE/DIFF;

FORMAT BISMORE BINARY.;

RUN;

程序 5.6 输出

缺失模式 (MP) 方法分析

混合过程 (Mixed Procedure)

最小二乘均值 (Least Squares Means)

| 效应 (Effect) | 估计值 (Estimate) | 误差 (Error) | DF | t 值 | Pr >t |
|---|---|---|---|---|---|
| MORE 第 4 年使用双膦酸盐 (BISMORE) | -0.00222 | 0.001021 | 1641 | -2.18 | 0.0295 |
| 使用双膦酸盐 (BISMORE) | 0.007187 | 0.000987 | 1641 | 7.28 | <.0001 |

最小二乘均值的差异 (Differences of Least Squares Means)

| 效应 (Effect) | 估计值 (Estimate) | 误差 (Error) | DF | t 值 | Pr >t |
|---|---|---|---|---|---|
| MORE 第 4 年使用双膦酸盐 (BISMORE) | -0.00941 | 0.001420 | 1641 | -6.63 | <.0001 |

## 5.3.5 多重插补缺失模式 (MIMP) 分析

MIMP 方法本质上是 MI 和 MP 方法的。首先，对缺失值进行多重插补。对于每个插补数据集，使用基线变量和缺失模式分类变量估计倾向评分。与 MP 方法类似，我们合并较小的缺失模式以使每个单元至少包含 100 个观测值。我们创建带有合并模式指标的数据集（见节 5.3.4），只需对该数据集应用 `PROC MI`（见节 5.3.3）。程序 5.7 显示了执行 MIMP 分析的 SAS 代码，程序 5.7 输出结果。

#### 5.7 插补缺失模式 (MIMP) 分析

```sas
****************************************************************
多重插补缺失模式 (MIMP) 方法;
****************************************************************
```

## 135 第 5 章 带有缺失值的倾向评分

## 程序 5.6 输出

均值过程 (MEANS Procedure)

分析变量 (Analysis Variable)：估计值 (Estimate)

分组 (BY Group)

| N | 均值 (Mean) | 标准差 (Std Dev) | 最小值 (Minimum) | 最大值 (Maximum) |
|---|---|---|---|---|
| MORE 第 4 年使用双膦酸盐 (BISMORE) | -0.0021775 | 0.00011208 | -0.002187 | -0.0021596 |
| 使用双膦酸盐 (BISMORE) | 0.0083296 | 0.000190528 | 0.0081254 | 0.008643 |

均值过程 (MEANS Procedure)

分析变量 (Analysis Variable)：估计值 (Estimate)

| N | 均值 (Mean) | 标准差 (Std Dev) | 最小值 (Minimum) | 最大值 (Maximum) |
|---|---|---|---|---|
| 5 | -0.0105070 | 0.000187855 | -0.0108178 | -0.01030396 |

可以使用 `PROC MIANALYZE` 获取治疗差异的点估计值。然而，来自 `PROC MIANALYZE` 的方差估计是无效。这种方法在程序 5.8 中显示，程序 5.8 输出了结果。

## 程序 5.8 使用 PROC MIANALYZE 汇总 MIMP 方法的估计值

```sas
TITLE2 '使用 PROC MIANALYZE 估计治疗差异';
DATA MIMP_EST (KEEP = _IMPUTATION EFFECT RENAME=(EFFECT=PARAMETER));
SET DIFFS;
EFFECT = 'DIFF';
RUN;
```

```sas
DATA FOR_MIMP_COV (KEEP = _IMPUTATION ROWNAME BISMORE DIFF);
SET DIFFS;
DIFF = STDERR**2;
ROWAME = "DIFF"
RUN;
```

```sas
PROC MIANALYZE PARMS=FOR_MIMP_EST COVB=MIMP_COV;
MODEFFECTS DIFF;
ODS OUTPUT PARAMETERIMATES=MI_EST
VARIANCEINFO=MI_VAR
RUN;
```

# 122 使用 SAS 对观察性健康数据进行分析

# 程序 5.8 的输出

使用多重插补缺失模式 (MIMP) 方法的分析结果

使用 PROC MIANALYZE 估计治疗差异

MIANALYZE 过程

```
PARMS Data Set               WORK.FOR_MIMP_EST
COVB Data Set               WORK.FOR_MIMP_COV
Number of Imputations        5
```

多重插补方差信息

| | --方差-- | | | DF |
|---|---|---|---|---|
| 参数 | 组间 | 组内 | 总计 | |
| DIFF | 3.289507E-8 | 0.000020272 | 0.000002115 | 9972.9 |

多重插补参数估计

| | | | | |
|---|---|---|---|---|
| 参数 | 方差相对增加 | 缺失信息比例 | 相对效率 |
| DIFF | in Variance | 0.020436 | 0.020224 | 0.995972 |

多重插补参数估计

| | | | | | |
|---|---|---|---|---|---|
| 参数 | 估计值 | 标准误 | 95% 置信限 | | |
| DIFF | -0.010507 | 0.001454 | -0.01336 | -0.00766 | 9972.9 |
| | | | | | | | |

|---|---|---|---|---|---|---|

| 参数 | 最小值 | 最大值 | Theta0 | 参数=Theta0 | Pr > |t| |
| DIFF | -0.010818 | -0.010310 | 0 | -7.23 | <.0001 |

### 5.3.6 获取 Bootstrap 置信区间



在这些基于倾向评分的 IPW 方法中，对点估计量的直接误差估计是具有挑战性的，因为估计权重中的额外变异性难以考虑。因此，我们使用自助方法来估计点估计的标准误和置信区间。SAS 宏 `%BOOT` 和 `%BOOTCI` (`http://code.hukert.ncsu.edu/~curvie/software/bootstrap/boot.html`) 提供了标准误和置信间的非参数估计（包括流行的偏偏修正加速 [BCA] 方法）。首先，对于 IPW 治疗差异，我们需要创建一个名为 `%ANALYZE` 的用户定义宏。该宏计算 IPW 治疗差异的点估计值，该估计值将从 `%BOOT` 和 `%BOOTCI` 宏中重复调用。接下来，调用 `%BOOT` 和 `%BOOTCI` 宏来计算 Bootstrap 估计。注意，`%ANALYZE` 宏必须有两个参数：用于识别输入数据集的 `data` 和用于命名输出数据集的 `out`。程序 5.9 是 `%ANALYZE` 宏以及对 `%BOOT` 和 `%BOOTCI` 宏调用的插图说明。

# 第 5 章 带有缺失值的倾向评分

```sas
%INCLUDE 'BOOTS.SAS'; /* 该文件可以在
http://cuke.hort.ncsu.edu/cukhibit/weaver/software/pathsas/jackboot.txt 找到 */
%MACRO ANALYZE (DATA=BMDPDS, OUT = );
%MIMP ANALYSIS (INDATA = &VARLIST, Y = FNBMD_C, G =
BMISore, MP_MIN = 100);

PROC SORT DATA = EST OUT = &OUT;
BY Q_METHOD;
RUN;
%MEND. ANALYZE;
PROC PRINTO LOG=NOLOG;
RUN;
```

TITLE 'BOOTSTRAP: 带有偏偏修正的正态 ("标准") 置信区间';

TITLE2;

```sas
%BOOT(DATA=BMDPDS, ALPHA=0.05, SAMPLES=1000, RANDOM=123, ID=Q_METH);
```

TITLE 'BOOTSTRAP BCA';

%BOOT1 (BCA, ID=Q_METH);

```sas
PROC PRINTO;
RUN;
```

`Carpenter` 和 `Bithell` (2000) 使用模拟表明，BCa Bootstrap 方法通常会产生可靠的结果，即使检验统计量的分布远离对称性。在例例中，我们使用 BCa Bootstrap 来估计 5.2 节数据集的置信区间（见表 5.2）。朴素估计量（使用 t 检验对治疗效应的直接无偏估计）高估了治疗差异。CC 方法的置信区间比 MI 和 MIMP 方法宽，而后两种方法产生相似的结果。应该注意的是，例如，CC 和 MP 方法产生的 95% 置信区间包含 0，而 MI 和 MIMP 方法则不。

表 5.2 被分配到放置组的女性在学习第四年股骨矿密度 BMD (g/cm²) 变化的均值 (95% CI) (n = 1,634).*

| 方法 | 未治疗 (n=1512) | 治疗 (n=131) | 治疗 vs. 未治疗 |
| --- | --- | --- | --- |
| NAIVE | -0.002(-0.004,-0.001) | 0.011(0.006,0.017) | 0.013(0.007,0.019) |
| CC | -0.002(-0.004,-0.001) | 0.006(0.002,0.020) | 0.008(0.000,0.022) |
| MP | -0.002(-0.004,-0.001) | 0.007(0.003,0.016) | 0.009(-0.001,0.018) |
| MI | -0.002(-0.003,-0.001) | 0.009(0.002,0.017) | 0.011(0.004,0.019) |
| MIMP | -0.002(-0.003,-0.001) | 0.009(0.002,0.017) | 0.011(0.004,0.019) |

*结果来自 Qu 和 Lipovich (2009)。MI 和 MIMP 的估计值与之前的 SAS 输出略有不同。

当少数患者的估计治疗倾向接近 0 时，这种替代分层估计量对 IPW 估计可能更稳健，导致这些受试者对整体治疗差异产生不当影响。程序 10 显示了执行 SR 方法的 SAS 代码，程序 10 的输出显示了结果。治疗效应的 SR 估计值为 .099。

## 带有缺失值的倾向评分

### 程序 10 使用倾向分层回归进行敏感性分析说明

```sas
* 此步骤可以被任何获取倾向评分的方法替换 */
PROC LOGISTIC DATA = ANALYTATA DESC;
  MODEL BISORE = &VARLIST;
  OUTPUT OUT=PRE PREDICTED=P;
RUN;

/* 使用 PROC RANK (GROUP=5) 定义组 */
PROC RANK DATA = PRE OUT=PRE GROUPS=5;
  VAR P;
  RANK PS_STRATA;
RUN;

PROC SORT DATA=PRE; BY PS_STRATA; RUN;

ODS LISTING CLOSE;
ODS OUTPUT SOLUTION=SF;
PROC MIX DATA = PRE P(WHERE=(PS_STRATA NE .));
  BY PS_STRATA;
  MODEL BISORE = &VARLIST/SOLUTION;
```

TITLE '通过调整组内基线协变量估计治疗效应';

```sas
PROC MEANS DATA = SF N;
CLASS PS_STRATA;
  TYPES PS_STRATA;
  VAR ESTIMATE;
  where effect = 'BISORE';
RUN;
```

### 程序 10 的输出

通过调整组内基线协变量估计治疗效应

MEANS 过程

分析变量 : 估计值

| 观测 | N | 均值 |
|---|---|---|
| 5 | 5 | 0.0099243 |

| 变量 P 的排名 | 观测 | N | 均值 |
|---|---|---|---|
| 0 | 1 | 1 | 0.0144995 |
| 1 | 1 | 1 | 0.0102909 |
| 2 | 1 | 1 | 0.0023628 |
| 3 | 1 | 1 | 0.0143711 |
| 4 | 1 | 1 | 0.0080970 |

### 5.4.2 使用不同的插补策略

对于涉及多重插补的方法，有使用不同预测变量集的多种插补模型。有人（Meng, 1994; Schafer, 1997）建议，在插补模型中尽可能包含更多的变量，因为忽略重要的协变量会导致错误的分析，而保留无关的预测变量只会降低效率。此外，一项考虑倾向估计插补策略差异的现实研究 (Crowe, Lipovich, and Wang, 2009) 显示包含治疗 (T) 和治疗结果 (Y) 可以提高治疗效应的估计。虽然将未来结果纳入插补模型以匹配分析模型（在本例中为 Y 和 T 的 ANOVA）似乎是不符合直觉的，但因此有助于减少估计治疗效应的偏差 (Meng, 1994)。注意，在 5.3.3 节和 5.5 节的多重插补示例中，我们在 `PROC MI` 的 `VAR` 语句中除了基线协变量外还包含了治疗和结果变量。

## 第 5 章 带有缺失值的倾向评分

```sas
PROC MIANALYZE PARMS = _ EST COVB= COV;
MODELEFFECTS INTERCEPT &VARLIST;
ODS OUTPUT PARAMETERESTIMATES=MI_EST
VARIANCEINFO=MI_VAR;
RUN;
```

程序 5.11 的输出

| 参数 | 方差相对增加量 | 缺失信息比例 | 相对效率 |
| --- | --- | --- | --- |
| intercept | 0.003791 | 0.003784 | 0.999244 |
| AGE | 0.041468 | 0.040481 | 0.999169 |
| BMIR | 0.003756 | 0.003749 | 0.999251 |
| FAHMBCN | 0.038052 | 0.030168 | 0.943096 |
| GAILMORE | 0.031253 | 0.031028 | 0.948167 |
| LSC | 0.000864 | 0.000863 | 0.999827 |
| LTTOBMR | 0.000064 | 0.000024 | 0.999853 |
| MIR | 0.001002 | 0.001002 | 0.999800 |
| NECKMR | 0.001434 | 0.001433 | 0.999711 |
| WFX | 0.002198 | 0.002181 | 0.999802 |
| PREHRVT | 0.003060 | 0.003601 | 0.999280 |
| PREVET | 0.008648 | 0.008610 | 0.998281 |
| SMOKE | 0.073996 | 0.071100 | 0.985979 |
| SQ | 0.010930 | 0.010870 | 0.998371 |
| VFX | 0.002259 | 0.002256 | 0.999549 |

多重插补参数估计值

| 参数 | 估计值 | 标准误 | 95% 置信限 | DP |
| --- | --- | --- | --- | --- |
| intercept | -3.910976 | 1.415616 | -6.6854 | -1.1364 | 280408 |
| AGE | 0.011069 | 0.027300 | -0.0426 | 0.06643 | 25358 |
| BMIR | 0.010270 | 0.041600 | -0.0539 | 0.06649 | 28573 |
| FAHMBCN | -0.013857 | 0.041900 | -0.09544 | 0.06903 | 52643 |
| GAILMORE | -0.014017 | 0.031643 | -0.08262 | 0.04111 | 49179 |
| LSC | -0.046261 | 0.230992 | -0.49536 | 0.41011 | 57142 |
| LTTOBMR | 9.158674 | 1.928007 | 5.29796 | 13.6393 | 5773 |
| MIR | 2.717227 | 0.899132 | 0.97249 | 14.5892 | 3996 |
| NECKMR | 4.221331 | 1.435053 | 1.17448 | 7.02515 | 1956 |
| WFX | -0.001402 | 0.021037 | -0.06152 | 0.02159 | 1043 |
| PREHRVT | -0.245808 | 0.210378 | -0.66854 | 0.16652 | 30925 |
| PREVET | -0.338775 | 0.273563 | -1.06957 | 0.39206 | 5417 |
| AESCORE | -0.010202 | 0.007301 | -0.02981 | 0.00919 | 6453 |
| SMOKE | 0.562806 | 0.313113 | -0.01983 | 1.17512 | 8425 |
| SQ | -0.134405 | 0.184790 | -0.49660 | 0.22779 | 3428 |
| VFX | -0.600087 | 0.228202 | -1.15437 | -0.04581 | 787654 |

#### 5.4 处理极端权重

IPW 逆权估计量的一个主要缺点是，当倾向评分接近 0 或 1 时，存在极端或极小的权重，可能会产生不稳定的估计。一种即时解决方法是为权重设置边界。例如，对于倾向评分 < δ，我们将其设置为 δ；对于倾向评分 > 1 - δ，其中 δ 是一个经验值。根据我们的经验，我们在模拟中使用 δ = 0.001，结果良好。对于 5.3 节中的数据，没有极小权重，因此我们没有使用这种技术。程序 5.12 显示了如何设置权重以产生稳定的估计。

```sas
%LET DELTA = 0.001;
DATA PRED;
SET PRED;
IF P < &DELTA. THEN P = &DELTA.;
IF P > 1-&DELTA. THEN P = 1-&DELTA.;
RUN;
```

## 5.5 讨论

CC 方法仅包含识别缺失的虚拟变量。MP 方法估计每个缺失模式内的倾向评分。对于观测较少的缺失模式，我们提出根据相似性合并缺失模式的方法。MI 方法通过首先插值然后将缺失模式信息作为协变量来结合 MI 和 MP 方法。这些估计倾向评分的方法可以与任何倾向评分模型结合（例如，在语句中使用 `PROC LOGISTIC` 进行多项逻辑回归）。如果具有至少一个缺失值的受试比例较低（例如 < 10%），处理缺失值将产生相似的结果。因此，可以选择最方便的方法，如。

## 参考文献

- Carpenter, J. and J. Bithell. 2000. "Bootstrap 置信区间：何时使用？为何？医学统计学者的实用指南。” Statistics in Medicine: 19: 1141–1164.

- Conaco, J., and R. Horwitz. 2000. "随机对照试验、观察性研究和研究设计的层次结构。” New England Journal of Medicine 342: 1887–1892.

- Costatino, J. M., Gail, S., et al. 1999. "预测侵袭性癌症发生率的模型验证。” Journal of the National Cancer Institute: 91: 1541–1548.

- Crowe, B., I. Lipkovitch, and O. Wang. 2009. "倾向评分分析中缺失基线数据的多种插补方法比较。” Pharmaceutical Statistics. In Press. DOI: 10.1002/pst.389.

- Dostino, R. B. 1998. "生物统计学教程：用于非随机对照组比较的减少偏倚倾向评分方法。” Statistics in Medicine 17(19): 2265–2281.

- Dostino, R., and D. B. Rubin. 2000. "使用缺失数据进行倾向评分估计。” Journal of American Statistical Association 95: 749–759.

- Dostino, R., W. Lang, Walkup, and T. Morgan. 2001. "倾向评分对血糖监测的影响。” Health Services & Outcomes 2: 291–315.

- Delmas, P., and B. Efron. 1987. "更好的自助法法。” Journal of American Statistical Association 82: 171–185.

- Horvitz, D., and D. J. Thompson. 1952. "有限总体不放回抽样的推广。” Journal of American Statistical Association 47: 663–685.

- Ibrahim, J., S. Lipnitz and M. Chen. 1999. "当协变量并非总是观测到时的回归系数估计。” Journal of American Statistical Association 89: 846–886.

- Leon, A., and D. Hedeker. 2005. "有序分类数据的分位数倾向调整。” Journal of Royal Statistical Society, Series B (Methodology) 6: 173–190.

- Little, R. J., and D. B. Rubin. 2002. *缺失数据的统计分析*. 第2版. New York: Wiley-Interscience.

- Lunceford, C. J., and M. Davidian. 2004. "通过倾向评分进行分层以估计治疗效应。” Statistics in Medicine 23: 2937–2960.

- Meng, X. 1994. "具有不确定输入来源的多重插补技术。” Statistical Science 9: 538–573.

- Qu, Y., and I. Lipkovitch. 2009. "使用多重插补（MIMP）方法处理缺失值的倾向评分。” Statistics in Medicine 28: 1402–1414.

- Robins, J. M., A. Rotnitz, and L. P. Zhao. 1994. "当某些回归变量未被观测到时的回归系数估计。”（注：此处原文有重复，此处已按要求处理翻译）

- Robins, J., and N. Wang. 2000. "插补估计量的推断。” Biometrika 77: 113–124.

- Rosenbaum, P. R. 1987. "基于模型的直接调整。” Journal of American Statistical Association 82: 387–394.

- Rosenbaum, P. R., and D. B. Rubin. 1983. "倾向评分在观察性研究因果效应中的作用。” Biometrika 70: 41–55.

- Rosenbaum, P. R., and D. B. Rubin. 1994. "通过倾向评分亚类分类减少观察性研究中的偏倚。” Journal of American Statistical Association 79: 516–524.



- Rubin, D. B. 1978. "样本中的多重插补：一种处理非响应的贝叶斯方法。” in ASA Proceedings in the Section on Survey Research Methods 20–28. Alexandria, VA: American Statistical Association.

Rubin, D. B. 1987. *Multiple Imputation for Nonresponse in Surveys*. New York: John Wiley & Sons, Inc.

Schafer, J. L. 1997. *Analysis of Incomplete Multivariate Data*. London: Chapman and Hall/CRC.

Wang, N., and J. M. Robins, 1998. “Large-sample theory for parametric multiple imputation procedures., *Biometrika* 85: 935–948.

Xie, J., and C. Liu. 2005. “Adjusted Kaplan-Meier estimator and log-rank test with inverse probability of treatment weighting for survival data.” *Statistics in Medicine* 24: 3089–3110.

## 第6章

## 用于解决选择偏的工具变量法

R. Scott Leslie

Hassan Ghomrawi

- 摘要 .......................................................................................................................... 131

- **6.1 引言 ........................................................................................................................ 131**

- **6.2 控制选择偏的工具变量方法概述 .................................................................... 132**

- **6.3 案例研究描述 ................................................................................................ 134**

- **6.4 应用于案例研究的传统普通最小乘法回归方法 ................................... 138**

- **6.5 应用于案例研究的工具变量法 ................................................ 139**

- **6.6 使用 PROC QLIM 进行 IV 分析 ................................................................ 143**

- **6.7 与传统回归调整方法的比较 ........................................... 146**

- **6.8 讨论 ................................................................................................................. 147**

- **6.9 结论 ................................................................................................................. 148**

- 致谢 ................................................................................................................ 149

- 参考文献 ....................................................................................................... 149

## 摘要

当妥善处理由于非随机化导致的选择偏时，观察性数据可以为研究问题提供有力的答案。医学文献主要依赖于基于观测变量的传统回归和倾向评分法来调整选择偏。由于未测量的混杂因素，此类方法可能会导致偏倚的估计。在本章中，我们引入了工具变量法（一种计量经济学方法）来调整选择偏，并说明了其在评估药物依从性治疗效果的应用。如果应用得当，该方法在解决选择偏方面可能更有用。

## 6.1 引言

观察性研究的一个主要优势在于其能够估计真实世界条件下治疗和干预的效果。然而，缺乏随机分组可能对观察性研究的结果产生严峻的威胁（D'Agostino and Kwan, 1995）。

## 132 使用 SAS 分析观察性健康数据

非随机组别在观测和未观测特征上通常存在差异，这反过来导致了进入治疗组的选择性差异。这种非随机抽样选择是扭曲治疗对结果影响的一种选择偏。换句话说，目前尚不清楚效应是因为治疗本身，还是由于随机化导致的组间选择差异。

在某些研究中，这种选择偏对治疗效应产生了重大影响，而在另一些研究中，调整选择偏对治疗效应的影响非常微小（Wang, 2005; Foster, 2000; McClellan, 2009; Grimes, 2002; Glesby, 1996）。因此，多项研究警告说选择偏可能导致进一步的偏倚估计（Hernan, 2006; Stuk, 2007）。在本章中，我们提供了工具变量（IV）方法的概述，并演示了使用行政索赔数据应用该方法调整选择偏的示例。IV 方法是一种计量经济学方法，虽然在医学文献中不如匹配、分层、传统回归和倾向评分法那么常见，但如果使用得当，它可能优于这些方法。

## 6.2 控制选择偏的工具变量方法概述

缺乏受试者随机治疗分组的观察性研究必须在处理混杂因素的同时解决选择偏，以准确估计治疗效果。工具变量（IV）分析是经济和社会科学中调整选择偏常用的工具，但在医疗领域应用较少。传统的调整方法仅使用观测变量，而 IV 方法则承认一组观测变量可能无法捕捉由于未观测因素导致的残差混杂（Angrist et al., 1996）。通过实施 IV 方法，研究人员找到与治疗选择高度相关但与结果变量不直接相关的变量。

将其纳入分析时，IV 会产生观测值无法解释的额外方差，从而获得对治疗对结果影响的无偏估计。2000 年，《Health Services》期刊出版了专门介绍 IV 分析的特刊（McClellan and Newhouse, 2000）。该期包含对该方法论解释以及其在健康结果研究中的应用示例。

图 6.1 展示了工具变量的工作原理。可观测的风险因素或混杂因素（X），如年龄、性别和合并症，可能同时影响结果（Y）和治疗（T）。这种关联的存在使得治疗分配依赖于观测值，而不是真正的独立变量。因此，治疗在模型中通过误差项进行修正。从而，在没有任何任何调整的情况下估计 (T) 对 (Y) 的影响，会导致区分治疗与结果之间的因果关系变得困难。传统回归方法考虑了观测值，但无法捕捉来自未观测值的偏倚。IV 分析的目标是找到一个与治疗相关但与结果不直接相关的工具。这些 IV 随后被用于估计独立于观测值（X）的治疗效应。

# 图 6.1 IV 方法论示意图

![](img/fe9ff008f88baacd41514b0b25dd58c_147_0.png)

虽然 IV 方法的直觉很有吸引力，但寻找有效工具的困难可能是导致未测量混杂的原因，且必须满足若干假设（Angrist, 1996; Lanthier, 2001; Greenland, 2000）。最值得关注的假设包括独立性假设、排除限制以及工具对治疗的非零因果效应。独立性假设规定工具与观测风险因素之间没有关系。排除限制要求 IV 除治疗之外对结果没有影响。工具的非零因果效应假设工具与治疗相关或是治疗的预测因子。

为了使用工具变量法估计调整后的治疗效应，需要估计两个方程。第一个方程估计 IV 和观测值（X）对治疗（T）的影响。第二个方程估计观测值（X）和治疗（T）对结果（Y）的影响。极大似然比法通常用于此类治疗的两阶段估计。使用 Heckman 两阶段估计来计算反米尔斯量是实现 IV 方法的另一种方式（Heckman, 1978）。

本章的剩余部分讨论了使用工具变量方法评估糖尿病患者人群中药物选择对药物依从性影响的示例。确定治疗之间的差异是重要的，因为药物依从性的增加可能意味着更好的糖尿病管理，从而可能减缓疾病进展。在决定更大人群的首选治疗方案时，我们使用 SAS/ETS 中的 QLIM 过程进行工具变量分析。

## 6.3 案例研究描述

研究利用大型药房数据库识别了在 7 个月内新开始使用两种口服抗组胺药物之一的患者（N=19,433）。该研究目的是比较两种治疗方法在 180 天内的依从性率。依从性被衡量为治疗开始后，药物被覆盖或供应给患者的天数比例（Benner, 2002）。选择新治疗患者（即新启动者）进行审查，是因为该样本对药物的初始依从性提供了更准确的估计。新启动者没有既往的用药史，且未受处方者治疗选择的影响。我们怀疑存在选择偏倚，因为两种治疗方法在患者耐受性、不良事件和副作用方面存在差异，这可能会影响治疗选择以及对每种药物的依从性（Lago, 2007; Lincoln et al., 2007）。此外，治疗的选择还受到近期发现、临床指南变化以及政策变动的影响（Schneeweg, 2002）。鉴于传统的回归技术在识别治疗对结果的影响方面可能存在不足，我们使用了 IV（工具变量）法来尽可能减少归因于未测量数据的偏差。

程序 6 中的 TABULATE 过程代码用于创建一个表格，显示新启动样本中按药物治疗分类的患者特征。此外，`PROC TEST` 和 `PROC FREQ` 用于测试组之间的差异和关联。人口统计学变量（年龄、性别）、医疗保险类型以及治疗开始前 6 个月内的用药情况（基线期）。治疗开始时的年龄（岁）。保险类型按健康管理组织（HMO 或其他）分类。首种使用的药物测量了磺脲类、抗高血压、降脂药物以及抗哮喘和抗抑郁药物。慢性疾病的用药模式和维持药物用于估计患者在以下处方剂量下的依从性行为。

# 程序 1 使用 PROC TABULATE 按药物治疗显示患者特征

```sas
proc format;
picture pct 0-100+=09.0 (mult=1000);
proc tab data=newstarts;
class tx;
var age_18to44 age_45to54 age_55to64 age_65plus_hmo_b_medicaid
b_medicare_b_self_pre _0106 _0109 _0112 _0113 _0149 female
mainterferill=pre_str_cnt_subset table_drug_cnt_subset;
t='Number' Count='*f=4.
(age*)=('mean std*SD')*f=4.1
age_18to44*=Age Group 18-44 _age_45to54*=Age Group 45-54
age_55to64*=Age Group 55-64 _age_65plus*=Age Group >=65
female*=Female)'*f=pct.
(b_hmo Enrolled*)=('mean')*f=pct.
(pre_drug_cnt=('Type of Drugs Utilized')=('mean std*SD')*f=4.1
mainterferill=('Maintenance Refill %')=('mean')*f=pct.
(pre_sulf*=Sulfonylureas _0106*=Hypertension' _0109*=Lipid
Irregularity' _0112*=Pain Management' _0113*=Antidepressant
0149*=Asthma')=('mean')*f=pct.
x='Treatment' /box=Unadjusted Demographic and Baseline
Characteristics';
```

# 第 6 章解决选择偏倚的工具变量法

```sas
proc ttest data=newstarts;
var age_pre_drug_cnt_subset maintrefillratio;
class tx;
```

proc freq data=newstarts;

tables tx*(female b_hmo_pre_sulf _0106 _0109 _0112 _0113 _0149)/chisq;

run;

```

| 程序 6.1 的输出 | | |
| :--- | :--- | :--- |
| **未调整的人口统计学和基线特征** | 治疗 | |
| | | 药物 A | 药物 B |
| 成员计数 | 611 | 815 |
| 年龄 | 55.5 | 56.0 |
| | SD | 11.8 | 12.6 |
| 年龄组 18-44 | 16.3% | 16.3% |
| 年龄组 45-54 | 30.9% | 28.3% |
| 年龄组 55-64 | 32.8% | 34.1% |
| 年龄组 >=65 | 19.8% | 21.2% |
| 女性 | 44.6% | 46.3% |
| HMO 入员 * | 65.3% | 74.8% |
| 使用药物数量 | 3.1 | 3.3 |
| | SD | 3.1 | 3.8 |
| 维持药物续方百分比 * | 36.3% | 41.3% |
| 磺脲类 | 27.6% | 31.5% |
| 高血压 | 56.6% | 57.7% |
| 脂质不规律 | 34.5% | 38.5% |
| 疼痛管理 | 21.1% | 26.1% |
| 抗抑郁药 | 14.5% | 13.6% |
| 哮喘 | 7.2% | 10.6% |



### 第 6 章 解决选择偏倚的工具变量法

```sas
proc ttest data=newstarts;
var age_pre_drug_cnt_subset maintrefillratio;
class tx;
```

```sas
proc freq data=newstarts;
tables tx*(female b_hmo_pre_sulf _0106 _0109 _0112 _0113 _0149)/chisq;
run;
```

| 程序 6.1 的输出 | | |
| :--- | :--- | :--- |
| **未调整的人口统计学和基线特征** | 治疗 | |
| | | 药物 A | 药物 B |
| 成员计数 | 611 | 815 |
| 年龄 | 55.5 | 56.0 |
| | SD | 11.8 | 12.6 |
| 年龄组 18-44 | 16.3% | 16.3% |
| 年龄组 45-54 | 30.9% | 28.3% |
| 年龄组 55-64 | 32.8% | 34.1% |
| 年龄组 >=65 | 19.8% | 21.2% |
| 女性 | 44.6% | 46.3% |
| HMO 入员 * | 65.3% | 74.8% |
| 使用药物数量 | 3.1 | 3.3 |
| | SD | 3.1 | 3.8 |
| 维持药物续方百分比 * | 36.3% | 41.3% |
| 磺脲类 | 27.6% | 31.5% |
| 高血压 | 56.6% | 57.7% |
| 脂质不规律 | 34.5% | 38.5% |
| 疼痛管理 | 21.1% | 26.1% |
| 抗抑郁药 | 14.5% | 13.6% |
| 哮喘 | 7.2% | 10.6% |



# 第 6 章 解决选择偏倚的工具变量法

## 6.3 案例研究描述

研究利用大型药房数据库识别了在 7 个月内新开始使用两种口服抗组胺药物之一的患者（`N=19,433`）。该研究目的是比较两种治疗方法在 180 天内的依从性率。依从性被衡量为治疗开始后，药物被覆盖或供应给患者的天数比例（Benner, 2002）。选择新治疗患者（即新启动者）进行审查，是因为该样本对药物的初始依从性提供了更准确的估计。新启动者没有既往的用药史，且未受处方者治疗选择的影响。我们怀疑存在选择偏倚，因为两种治疗方法在患者耐受性、不良事件和副作用方面存在差异，这可能会影响治疗选择以及对每种药物的依从性（Lago, 2007; Lincoln et al., 2007）。此外，治疗的选择还受到近期发现、临床指南变化以及政策变动的影响（Schneeweg, 2002）。鉴于传统的回归技术在识别治疗对结果的影响方面可能存在不足，我们使用了 `IV`（工具变量）法来尽可能减少归因于未测量数据的偏差。

程序 6 中的 `TABULATE` 过程代码用于创建一个表格，显示新启动样本中按药物治疗分类的患者特征。此外，`PROC TEST` 和 `PROC FREQ` 用于测试组之间的差异和关联。人口统计学变量（年龄、性别）、医疗保险类型以及治疗开始前 6 个月内的用药情况（基线期）。治疗开始时的年龄（岁）。保险类型按健康管理组织（`HMO` 或其他）分类。首种使用的药物测量了磺脲类、抗高血压、降脂药物以及抗哮喘和抗抑郁药物。慢性疾病的用药模式和维持药物用于估计患者在以下处方剂量下的依从性行为。

## 程序 1 使用 `PROC TABULATE` 按药物治疗显示患者特征

```sas
proc format;
picture pct 0-100+=09.0 (mult=1000);
proc tab data=newstarts;
class tx;
var age_18to44 age_45to54 age_55to64 age_65plus_hmo_b_medicaid
b_medicare_b_self_pre _0106 _0109 _0112 _0113 _0149 female
mainterferill=pre_str_cnt_subset table_drug_cnt_subset;
t='Number' Count='*f=4.
(age*)=('mean std*SD')*f=4.1
age_18to44*=Age Group 18-44 _age_45to54*=Age Group 45-54
age_55to64*=Age Group 55-64 _age_65plus*=Age Group >=65
female*=Female)'*f=pct.
(b_hmo Enrolled*)=('mean')*f=pct.
(pre_drug_cnt=('Type of Drugs Utilized')=('mean std*SD')*f=4.1
mainterferill=('Maintenance Refill %')=('mean')*f=pct.
(pre_sulf*=Sulfonylureas _0106*=Hypertension' _0109*=Lipid
Irregularity' _0112*=Pain Management' _0113*=Antidepressant
0149*=Asthma')=('mean')*f=pct.
x='Treatment' /box=Unadjusted Demographic and Baseline
Characteristics';
```

```sas
proc ttest data=newstarts;
var age_pre_drug_cnt_subset maintrefillratio;
class tx;
proc freq data=newstarts;
tables tx*(female b_hmo_pre_sulf _0106 _0109 _0112 _0113 _0149)/chisq;
run;
```

| 程序 6.1 的输出 | | |
| :--- | :--- | :--- |
| **未调整的人口统计学和基线特征** | 治疗 | |
| | | 药物 A | 药物 B |
| 成员计数 | 611 | 815 |
| 年龄 | 55.5 | 56.0 |
| | SD | 11.8 | 12.6 |
| 年龄组 18-44 | 16.3% | 16.3% |
| 年龄组 45-54 | 30.9% | 28.3% |
| 年龄组 55-64 | 32.8% | 34.1% |
| 年龄组 >=65 | 19.8% | 21.2% |
| 女性 | 44.6% | 46.3% |
| HMO 入员 * | 65.3% | 74.8% |
| 使用药物数量 | 3.1 | 3.3 |
| | SD | 3.1 | 3.8 |
| 维持药物续方百分比 * | 36.3% | 41.3% |
| 磺脲类 | 27.6% | 31.5% |
| 高血压 | 56.6% | 57.7% |
| 脂质不规律 | 34.5% | 38.5% |
| 疼痛管理 | 21.1% | 26.1% |
| 抗抑郁药 | 14.5% | 13.6% |
| 哮喘 | 7.2% | 10.6% |



# 第 6 章 解决选择偏倚的工具变量法

```sas
proc ttest data=newstarts;
var age_pre_drug_cnt_subset maintrefillratio;
class tx;
run;
```

```sas
proc freq data=newstarts;
tables tx*(female b_hmo_pre_sulf _0106 _0109 _0112 _0113 _0149)/chisq;
run;
```

| 程序 6.1 的输出 | | |
| :--- | :--- | :--- |
| **未调整的人口统计学和基线特征** | 治疗 | |
| | | 药物 A | 药物 B |
| 成员计数 | 611 | 815 |
| 年龄 | 55.5 | 56.0 |
| | SD | 11.8 | 12.6 |
| 年龄组 18-44 | 16.3% | 16.3% |
| 年龄组 45-54 | 30.9% | 28.3% |
| 年龄组 55-64 | 32.8% | 34.1% |
| 年龄组 >=65 | 19.8% | 21.2% |
| 女性 | 44.6% | 46.3% |
| HMO 入员 * | 65.3% | 74.8% |
| 使用药物数量 | 3.1 | 3.3 |
| | SD | 3.1 | 3.8 |
| 维持药物续方百分比 * | 36.3% | 41.3% |
| 磺脲类 | 27.6% | 31.5% |
| 高血压 | 56.6% | 57.7% |
| 脂质不规律 | 34.5% | 38.5% |
| 疼痛管理 | 21.1% | 26.1% |
| 抗抑郁药 | 14.5% | 13.6% |
| 哮喘 | 7.2% | 10.6% |

# 第6章 解决选择偏倚的工具变量法

## 6.5 变量变量法在案例研究中的应用

由于怀疑选择偏倚无法通过标准的普通最小二乘法解决，我们采用了工具变量（IV）法。在比较药物治疗疗效时，应用 IV 方法的少数研究中，Brookhart及其同事（2006, 2007）在评估药物治疗对发病率和死亡率的影响时，将医生的偏好作为工具变量。作者在两项独立的研究中使用这些基于偏好的工具，评估与非甾体抗炎药物治疗相关的胃肠道毒性风险，以及使用抗精神药物的老年患者的死亡率。

我们通过复制处方者对该药物的最后一次处方（药物 A 或药物 B）作为我们研究的工具，Brookhart及其同事假设，通过最后一次处方所衡量的医生即时处方史，可以估计出处方者对某种治疗方案的偏好。根据该假设，这种选择会影响处方者对下一位患者的治疗选择。我们认为在我们的研究中，这一衡量将作为一个有效的工具，因为其治疗选择与下一位患者的结果不相关。

为了构建我们的 IV，我们识别了 1,426 名患者中初始处方的处方者。在这一初始处方之前的期间，提取了两种药物的处方索赔，以计算处方者的偏好。根据处方者在相应药物类中最近的处方，将其分为药物 A 处方者或药物 B 处方者。部分处方者未被正确识别。部分处方者没有处方记录；因此，这些对应的患者被排除在分析之外。总共对 1,228 名处方者进行了分类。

如前所述，工具变量的有效性依赖于许多假设。行政数据无法证实这些假设，但可以用于研究分配的可信度。为了测试我们方法的有效性，我们首先查看了 IV 的分布，以显示处方者处方这两种药物的偏好。1,226 名处方者对药物 A 或药物 B 的偏好分别为 47% 和 53%。为了解决 IV 分配的非零因果效应，我们使用 `PROC FRE` 评估了工具与治疗选择之间的关联，以估计我们的工具预测治疗的情况，或者处方偏好在预测处方者下一位患者治疗选择中的程度（程序 6.4）。结果显示我们的 IV 与治疗选择之间存在强正相关关系。偏好药物 A 的处方者在我们样本中确定的患者处方药物 A 的概率是其他的三倍以上（OR = 3.44, CI = 2.766 - 4.293）。

为了解决独立假设，我们检查了 IV 与观测因素之间的关系。独立假设的潜在违反包括不同处方组之间患者特征的差异（即，药物 A 处方者治疗的患者与药物 B 处方者看到的患者大不同）。通过 `TABULATE`、`TTEST` 和 `FREQ` 程序根据处方偏好对患者人口统计和基线特征进行分层，可以将观测值与工具进行比较。更复杂的模型可以处理随时间变化的聚集关系（Brookhart, 2007）。组间差异越小，说明处方者对上一个患者的治疗选择与当前患者的观测值无关。持续存在的差异可能意味着对该假设的违反；然而，这些协变量可以在二阶段最小二乘回归中处理，可能会影响结果的处方者（Brookhart, 2006）。处方者的偏好可能会通过处方者提供的其他服务或由于提供者之间的技能差异而影响合从性。然而，文献综述显示，患者对药物的长期依从主要取决于患者信念和行为的自我效能（Bodenheimer et al., 2002; Jerez et al., 2005），而不是处方者的指导（Haynes, 2002）。医生技能对我们合从性结果的影响难以衡量，因此我们利用这项研究来维护验证排除区域的可能性。

## 程序 6.4 用于验证 IV 假设的代码

```sas
proc freq data=newstarts;
tables iv*tx/chisq measures;
run;

proc format;
picture pct 0-100.0% (mult=1000);
run;

proc tabulate data=newstarts;
class tx iv;
var age_18to44 age_45to54 age_0106 _0109 _0112 _0113 _0149 female
b_medicare b_self_pre maintreillratio pre_st_class_cnt pre_drug_cnt;
table N='Number Count'*f=count;
(age*)='Age Group' mean(SD)*f=4
(age_18to44='Age Group 18-44' age_45to54='Age Group 45-54'
age_56to64='Age Group 55-64' age_65plus='Age Group >=65'
(female*)='Female')*f=fct;
(b_hmo*)='HMO Enrolled')*(mean='')
(pre_drug_cnt_subset*)='Utilized')*(mean(SD))*f=4
maintreillratio='Maintenance Refill
%(pre_sulf*)='Sulfonyurea' _0106='Hypertension' _0109='Lipid
Irregularity' _0112='Pain Management' _0113='Antidepressant
0149='Asthma')*(mean='')*fct;
```

程序 6.4 用于验证 IV 假设的输出

## 程序 6.4 用于验证 IV 假设的代码

```sas
proc freq data=newstarts;
tables iv*tx/chisq measures;
run;
```



``` (此处代码块保持不变) ```

## 144 使用 SAS 进行观察性健康数据分析

- `droga` = 治疗选择指示
- `tx` = 治疗分类变量
- `iv` = 工具变量（处方者偏好）
- `pdc` = 结局（依从性，用药物覆盖天数的比例）
- `age` = 患者在开始治疗之日的年龄（索引日期）
- `female` = 指示变量
- `b_hmo` = HMO 参保
- `ccopay_idxdrug` = 患者对初始处方的自付费用

其余变量描述了治疗前基线期间的利用情况：
- `pre_drug_cnt` = 使用的不同协变量数量
- `pre_sulf` = 使用磺脲类药物
- `_0106` = 使用抗高血压药
- `_0109` = 使用哮喘药物
- `_0112` = 使用止痛药
- `_0113` = 使用脂溶性药物
- `_0149` = 使用抗抑郁药
- `mainrefillatio` = 维持性药物的续方百分比

第一个 `MODEL` 语句是一个选择方程，它使用概率 模型（通过使用 `DISCRETE` 选项指示），并根据我们的 IV 和其他观测值创建每个受试者接受药物 B 的预测概率。第二个 `MODEL` 语句是结局方程，它使用线性回归在控制协变量的情况下对依从性结局进行建模。这评估了治疗效果，同时控制了由第一个方程产生的概率以及其他认为的混杂因素。一些人认为，在这一步中包含除治疗组以外的独立变量是多余的，因为它们已经包含在第一个 `MODEL` 语句中了。我们认为，向模型中添加变量可以提供关于结局预测的额外信息。选择模型可以包含被认为对治疗具有预测性的协变量，而结局模型可以包含结局的预后因素。`OUTPUT` 语句创建了一个名为 `DrugB` 的数据集。通过添加 `PREDICTED` 选项，新创建的数据集包含了输入数据集中的所有变量，加上两个新变量 `P_drugs` 和 `P_pdc`，它们分别包含治疗值和依从值的预测值。预测的依从性结局值针对样本中的所有受试者，假设所有患者都开具了药物 B。

## 程序 6.5 的输出

| 观测值 | tx | droga | iv | pdc age female b_homo | copy_id xdrug | pre_drug_cont_subset sulf | 0106 | 0109 | 0112 | 0113 | 0149 | Maintrefill ratio |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | Drug A | B | 1 | 0.00566 | 55 | 0 | 23.000 | 1 | 1 | 1 | 0 | 0 | 0.45946 |
| 2 | Drug B | | 0 | 0.16667 | 76 | 1 | 20.000 | 0 | 0 | 0 | 0 | 0 | 0.00000 |
| 3 | Drug A | | 1 | 0.07222 | 44 | 1 | 0.000 | 10 | 1 | 1 | 0 | 0 | 0.050000 |
| 4 | Drug B | | 0 | 0.91111 | 74 | 1 | 15.533 | 4 | 1 | 1 | 0 | 0 | 0.50000 |
| 5 | Drug B | | 0 | 0.16667 | 77 | 0 | 7.000 | 1 | 1 | 1 | 0 | 0 | 1.00000 |
| 6 | Drug A | | 1 | 0.61667 | 74 | 0 | 109.362 | 5 | 1 | 0 | 0 | 0 | 0.000000 |
| 7 | Drug B | | 0 | 0.16667 | 59 | 1 | 0.000 | 0 | 5 | 1 | 1 | 0 | 0.000000 |
| 8 | Drug A | | 1 | 0.28333 | 51 | 1 | 0.000 | 4 | 0 | 1 | 1 | 0 | 0.222222 |
| 9 | Drug B | | 0 | 0.27778 | 43 | 1 | 0.000 | 17 | 1 | 1 | 1 | 1 | 0.29167 |
| 10 | Drug A | | 1 | 0.16667 | 69 | 0 | 0.000 | 2 | 0 | 0 | 0 | 0 |  |

| 参数 | 估计值 | 标准误 | t 值 | Pr > [|]] |
|---|---|---|---|---|
| pdc.Intercept | 0.468902 | 0.064961 | 7.22 | <0.001 |
| pdc.age | 0.001444 | 0.000929 | 1.55 | 0.1201 |
| pdc.female | -0.060862 | 0.022960 | -2.67 | 0.00300 |
| pdc.copy_idxdrug | -0.001525 | 0.005035 | -4.90 | <0.001 |
| pdc.pre_drug_cont_subset | -0.001683 | 0.004240 | -0.40 | 0.6915 |
| pdc.maintrefillratio | 0.168150 | 0.036034 | 4.66 | <0.001 |
| pdc.pre_sulf | -0.042180 | 0.025716 | -1.64 | 0.1010 |
| pdc_0106 | -0.001649 | 0.025733 | -0.06 | 0.9489 |
| pdc_0109 | 0.047814 | 0.025504 | 1.87 | 0.0663 |
| pdc_0112 | -0.045605 | 0.028238 | -1.61 | 0.1063 |
| pdc_0113 | -0.008500 | 0.034562 | -0.25 | 0.8057 |
| pdc_0149 | -0.006435 | 0.033876 | -0.17 | 0.8682 |
| Sigma.drug | 0.297051 | 0.009963 | 29.82 | <0.001 |
| drug.Intercept | -0.042098 | 0.018640 | -2.25 | 0.0242 |
| drug.iv | 0.740991 | 0.074652 | 9.93 | <0.001 |
| drug.age | -0.00008843 | 0.003272 | -0 | 0.9979 |
| drug.female | -0.112074 | 0.076919 | -1.46 | 0.1451 |
| drug.copy_idxdrug | 0.00009045 | 0.021086 | 0.09 | 0.9308 |
| drug.pre_drug_cont_subset | 0.004108 | 0.014939 | 0.28 | 0.7833 |
| drug.maintrefillratio | -0.206794 | 0.118055 | -1.75 | 0.0798 |
| drug.pre_sulf | -0.100035 | 0.087456 | -1.15 | 0.2512 |
| drug_0106 | 0.108600 | 0.088306 | 1.23 | 0.2188 |
| drug_0109 | -0.078342 | 0.087028 | -0.90 | 0.3680 |
| drug_0112 | -0.211746 | 0.098552 | -2.15 | 0.0317 |

| 参数 | 估计值 | 标准误 | t 值 | 近似 Pr > |t| |
|---|---|---|---|---|
| drug_0113 | 0.105221 | 0.117267 | 0.90 | 0.3696 |
| drug_0149 | -0.179984 | 0.139948 | -1.29 | 0.1984 |
| Rho | -0.235728 | 0.162230 | -1.45 | 0.1462 |

程序 6.5 中的 QLIM 程序输出包含 `MODEL` 语句的参数估计值表（用于第一个结局，第二个用于治疗选择），指示了未调整变量的幅和影响。其中之一是示例中的治疗选择/IV 参数，它指示了 IV 对选择的影响，以及指示了两个方程之间相关性的 rho 参数。显著的 rho 估计表明结局中存在治疗偏差。drug 参数估计表明 IV 对选择有强影响（p < 0.001），而 rho 估计表明了治疗选择偏差对结局的影响。在这种情况下，估计值为 -0.235728 (p=.1462)。

第二次提交此数据以确定所有患者都接受药物 A 时的依从性值。通过更改第一个 `MODEL` 语句中的 `SELECT` 选项生成了所有患者使用药物 A 时的依从性值。比较这些预测的依从性值给出了比较效果。如果所有成员使用药物 A，平均估计依从性为 0.5353。如果所有患者使用药物 B，平均估计依从性为 0.5276。运行两种场景的代码后，两个新生成的数据按受试者进行了排序和合并。使用包含每个场景预测依从性值的最终患者级数据集，我们可以通过 PROC TEST 使用配对 t 检验来比较治疗差异。

## 6.1 与传统回归方法的比较

表 6.1 将 IV 方法的结果与未调整的结果以及更重要的是，与观测值的传统回归调整（调整后的 OLS 模型）进行了比较。药物 A 和药物 B 的未调整依从性分别为 47.7% 和 51.2%。使用 PROC GLM 计算调整值显示平均值略有变化，尽管模型控制了各种因素。来自 QLIM 程序的计算显示了选择偏差的影响。药物 A 和药物 B 的平均依从性值分别增加到 0.5390 和 0.55327。尽管我们的示例在使用 IV 方法时依从性变化很小，但许多研究显示方法之间存在显著差异（Brookhart, 2006; Landrum, 2001）。

## 第6 章 处理选择偏差的工具变量方法

表 6.1 按治疗划分平均依从性：IV 模型对比调整模型

| 模型 | 治疗 | 依从性结局 | 95% 置信限 |
|---|---|---|---|---|
| 未调整模型 | 药物 A | 0.477 | 0.449 | 0.504 |
| | 药物 B | 0.512 | 0.488 | 0.535 |
| | 估计治疗差异 | -0.034 | -0.071 | 0.001 |
| 回归调整模型 | 药物 A | 0.478 | 0.451 | 0.505 |
| | 药物 B | 0.511 | 0.487 | 0.534 |
| | 估计治疗差异 | -0.032 | -0.068 | 0.003 |
| IV 调整模型 | 药物 A | 0.535 | 0.530 | 0.540 |
| | 药物 B | 0.527 | 0.522 | 0.533 |
| | 估计治疗差异 | 0.007 | 0.003 | 0.011 |

## 6.8 讨论

传统的回归调整技术依赖于观测测量来控制混杂，而 IV 方法依赖于工具变量来考虑已测量和未匹配的因素。与调整风险因素的传统方法相比，该方法增加的元素是有价值的。倾向评分的一个很大假设是，所有影响分组分配和结局的因素都包含在建模中。研究人员不应忽视大量的未匹配因素。许多影响因素，治疗选择或分组分配也受到指南和政策变化的推动（Schneweis, 2002）。

在演示的示例中，可用数据使我们解决了 Angrist (1996) 和 Landrum (2001) 所述的某些假设，但并非全部。稳定个体处理值假设（SUTVA）认为其他患者的治疗状态之间不存在关系。我们假设处方者的偏好会影响下一位患者的治疗。一个患者的治疗不太可能影响另一患者的治疗选择。此外，处理我的变量的单调性（monotonicity）也具有挑战性。自然形成是，如果患者从 B 处方者获得了药物 A，那么该患者也会从 D 处方者获得药物 A。处理工具变量（IV）有效性的许多假设之困难，证明了寻找强工具变量的困难性。在许多示例中，使用组合方法的结果一致性可能表明选择偏倚有限，和/或未能通过观测数据和未知数据元素捕捉到偏差。

两种方法都存在设计局限性，包括实际合从性可能与观察到的合从性不同。可能还存在未捕捉到的治疗选择和依从性预测因子，包括患者态度、社会经济地位、教育程度以及使用的其他药物数量。

可以将 IV 方法与 SAS 过程相结合，例如我们示例中描述的两步法。LOGISTIC 和 GENMOD 过程均可估计响应值的预测概率。使用 `PROC LOGISTIC` 构建第一个治疗选择模型将基于 IV 创建预测治疗。通过这些预测治疗值，我们可以使用 `PROC GLM` 进行第二步（结果模型），评估治疗对结果的影响，同时控制预测的治疗值以及可能影响结果的其他观测值。在其他情况下，根据结果的性质可以使用 `PROC REG` 或 `PROC LOGISTIC`。然而，我们尚未得知可直接使用的、经过验证的 SAS 代码。

## 6.9 结论

尽管观察性研究可以就常规护理环境下治疗对结果的效果产生独特发现，但观察性研究的非随机性质要求处理潜在的选择偏倚。使用考虑观测变量的传统回归技术可以解决部分偏差，但当协变量与模型中的误差项相关时，结果可能会产生偏差。为了最大化偏差控制，考虑未观测变量是必要的；然而，当你使用观察性数据时，没有一种方法可以完全消除偏差。

在本研究中，我们证明了仅控制观测变量对于两种药物治疗之间原始的、未调整的均值调整作用很小。通过使用包含未观测变量之额外方差的 IV 方法，我们对合从性结果的治疗效应创建了一个偏差较小的估计。结果是合从性均值的变化，结论是不同治疗之间的合从性没有差异。

我们仅展示了一种执行 IV 方法的方法。IV 方法的变体取决于治疗类型和结果类型，例如多种治疗和非线性结果测量。

## 第 6 章 解决选择偏倚的工具变量法 149 页

尽管 IV 方法论在观察性研究和临床研究中较为人知且广泛使用，但它可以与传统的风险调整技术（如倾向评分和多变量回归）结合使用以减少偏差。如果应用得当，IV 可以调整未观测变量的影响，并为比较有效性研究增加价值。

# 致谢

作者感谢 M. Alan Brookhart、Bradley Martin 以及评审员提供的指导、评审和意见。

# 参考文献

Angrist, J. D., W. Imb, D. B. Rubin, and J. M. Robins. 1996. “Identification of Causal Effects Using Instrumental Variables,”Journal of the American Statistical Association 91:444–455.

Benner, J. S., R. J. Glynn, H. Mogun, P. J. Neumann, et al. 2002. “Long-term Persistence in Use of Statin Therapy in Elderly Patients.”The Journal of the American Medical Association 288:455–462.

Bodenheimer, T., K. Lorig, H. Holman, and K. Grünbach. 2002. “Patient Self-Management of Chronic Disease in Primary Care.”The Journal of the American Medical Association 288:455–462.

*(注：参考文献部分通常不翻译，此处按要求省略，保留原始格式)*

# 第 7 章

# 使用 JMP 的局部控制方法

Robert L. Obenchain

- 摘要 ........................................................................................................ 151
- 7.1 引言 ....................................................................................................... 152
- 7.2 对假设性患者登记数据的某些传统分析...................................... 156
- 7.3 局部控制分析的四个阶段 ................................................................. 163
- 7.4 结论.................................................................................................................. 182
- 致谢..................................................................................................................... 184
- 附录：倾向评分与分组/平衡评分.................................. 185
- 参考文献 ............................................................................................... 189

## 摘要

本文利用 JMP 展示了用于观察性研究中调整治疗偏倚和混杂的局部控制方法，因为局部控制最适合通过高度可视化的方式实施和应用。局部控制方法的独特之处在于：它它在基线协变量 x 空间中对患者进行分层聚类；应用简单的嵌套方差分析（ANOVA）模型（聚类内的治疗）；并最终具有高度的灵活性、非参数性和稳健性。尽管局部控制方法是经典而非贝叶斯的，但其主要输出是局部治疗差异（LTD）的完整分布，该分布包含了所有与患者对治疗的差异反应相关的潜在信息。所有概念均使用 10,000 名患者的自由发行数据进行说明，这些数据是生成的，类似于一份包含 996 名患者的发表的心血管疾病登记数据。

## 7.1 引言

分组和随机化在实验统计设计中的关键作用是公认的。本章强调，这些相同概念的相对简单变体可以对观察性研究进行强大且稳健的分析。由于充分的分组和随机化普遍无法（或不能）纳入观察性研究的数据收集阶段，因此我们在这里讨论的变体（局部控制和重采样）都是在事后应用的。

自 Cochran (1965, 1968) 的工作以来，许多观察性数据分析方法都强调了子类或患者聚类的形成，从而得出总结局部定义平均值和或差异的治疗比较。传统上，局部控制只是分组的另一种名称。在这里，局部控制方法被描述为一个动态过程，其中患者聚类（子组）的数量和大小是预先指定的。相反，它被用于识别并仅关注最相关的患者比较。这种策略旨在减少治疗选择偏倚，并揭示局部治疗差异（LTDs）的完整分布（即，它识别了任何患者反应的模式）。

至少自 Fisher (1925) 的工作以来，随机化一直被置于研究原则层级结构的顶端。参见 Conaco 同事 (2000)。毕竟，在所有已知患者除其治疗选择（s）和观察结果外没有任何信息的情况下，将患者随机分配到治疗中是至关重要的。在这种情况下，如果没有随机化，就没有理由相信（或至少希望）治疗组和未治疗组在治疗前是可比的，而且没有办法识别有意义的患者子组并证明它们在任何方面都是可比的！

### 7.1.1 人体研究中随机化的基本问题

患者治疗随机化的主要实际问题是，由于伦理或务实考虑，患有急性疾病的人最多只能随机化一次，仅一次。换句话说，交叉设计是不可能的。在理论上，单一随机化可以产生真实差异。为了取得进展，人们必须对因果效应和反事实结果列出几乎无尽的无法验证的假设。参见 Holland (1986) 关于 Rubin 因果模型的内容。

这指的是，而不是使用旧式的随机化（现在人们广泛认为，在对于每位患者仅有一次治疗随机化的研究中，接近较良好基线的唯一方法是在基线最最可比的患者分组内使用动态随机化，McEnterlee, 2003）。尽管如此，患者并不喜欢对他们接受的治疗进行随机化和盲法。结果，大多数治疗组往往会随着时间的推移出现患者的差异性流失，导致最终留存的患者在基线特征上变得不平衡。

对我来说，底线在于：只有当每个实验受体都能暴露于一系列盲法挑战（例如笼子中的动物、田间的样地或 Fisher 持久的品尝），且理想长度可变时，随机化无疑才能产生强大且稳健的推断。

示例：考虑对一组不同设计和等级（流通量）的古硬币（有限的非随机样本）进行以下实验。假设每枚硬币都通过通常的抛掷或在平坦表面上立起来处理，产生一个观察结果并命名为正面或反面。参见 Gelman 和 Nolan (2002) 以及 Diaconis 同事 (2007)，见图 7。在每枚硬币仅被处理和测试一次的严格限制下，治疗随机化（抛掷对比旋转）能为此实验增加多少信息？由于这种实验中随机化的如此严苛限制，无法关于硬币的公平性或治疗的效果推断出任何特别有趣的结论！

对进入研究的患者知之极少的情况很少见。事实上，研究人员对于哪些基线特征可以预测结果（和或治疗选择）非常有把握，以至于在确认每个患者之前不会考虑前瞻性（或回顾性）研究。

在这里，我们建议在 7.3.3 节中使用一种重采样（不放回）来验证 LTD 分布是否显著。为了避免在所有患者随机分配到详尽子组时出现运气不好，我们建议在多个独立样本中累积（默认：25）。

### 7.1.2 基本局部概念

在进行局部控制（LTC）分析时，对患者最相关的治疗前特征了解越多越好。这些信息被回顾性地形成分组。分组是潜在的有意义子组，人们可以经验地将其定义为层、子类（Cochran, 1965, 1968）或聚类。由于人类受试在特征方面具有著名的异质性，如果不能至少在非常相似的患者子组之间进行治疗比较，那么发现的可复制性几乎没有理由。

最重要的是，LC 的一个特征是可以验证局部子组是否形成了具有统计意义的差异，这里被称为显著差异。建立显著差异的基本 LC 术语如下。

在任何包含治疗和未治疗患者的子组内，局部治疗差异（LTD）定义为治疗患者的平均结果减去未治疗患者的平均结果。LTD 从平均结果中计算，治疗或未治疗患者的数量必须平衡（即比例为 1:1），LTD 才是未知真实差异的无偏估计。

任何仅包含治疗患者或仅包含未治疗患者的子组都被认为无信息。该子组的 LTD 不进行估计，并在 JMP 和 SAS 中用缺失值符号（点）表示。

当 N 个患者分为 K 个互斥且详尽的患者子组（或聚类）时，每个组包含一个或多个患者（K≤N），相应的 LTD 分布是根据子组内的 LTD 计算的，某些可能是缺失值。假设 LTD 分布的充分统计量是其经验累积分布函数（CDF），其中每个观察到的非缺失 LTD 值的阶高度为（子组内患者总数）/总患者数

# 使用 SAS 进行观察性健康数据分析

在所有信息丰富的亚组中。由于这些步骤的高度可能不同，这里的 CDF 被描述为患者加权的。由于观察到的局部治疗效应（LTDs）具有异方差（由于亚组内治疗因素的差异、结果的局部异方差以及亚组间的差异引起），可以考虑用于 CDF 的替代权重。

一个实用的经验法则是 $K \le (N/11)$，这样每个亚组的平均患者人数至少为 11。较小的亚组往往更具局部性，它们也倾向于对其 LTD 不提供有效信息，从而浪费了信息并增加了整体不确定性。

在局部控制（LC）方法中，由 $K$ 个匹配良好的患者亚组产生的观察到的 LTD 分布的 CDF 将与相应的人工 LTD 分布的 CDF 进行比较，后者定义如下。人工 LTD 分布通过通过这 $N$ 个观测患者随机分配到 $K$ 个规模相同且治疗与未治疗患者比例相同的亚组中产生。通过合并多次（通常是）对 X 到簇的独立随机分配的重复实验，人为地增加了整体人工 LTD 的精度。特别需要注意的是，在形成人工 LTD 分布时故意忽略了患者的 x 特性；具体而言，仅使用观察到的患者 y 结果和观察到的 r 治疗分配来估计 LTD。人工副本可以合并（取平均值），并在 y 值处计算最大值。

当观察到的 LTD 分布的 CDF 与其相应的人工 CDF 不同（可能以细微的方式）时，则称观察到的 LTD 是显著的（salient）。毕竟，在完整集中对所有治疗患者与未治疗患者进行整体比较时，只要存在差异性治疗选择或其他混杂（x 特性平衡）信息，基于随机定义亚组的治疗比较就会产生偏差。鲜明对比的是，在真正具有可比性的患者亚组内形成的观察 LTD 是无偏的。

当无偏估计和有偏估计的经验分布互不可区分时，无偏估计并不明显优于有偏估计！一旦观察到的 LTD 和人工 LTD 分布的 CDF 显示不同，逻辑上的解释是观察到的 LTD 分布已经（至少部分）针对治疗选择偏倚和混杂进行了调整。

同样，构成显著 LTD 分布的亚组平均 LTD 值是相应的治疗调整后主效应。最后，此处假设显著 LTD 分布的经验 CDF 构成了一个关于处理作为其 x 特性特征的患者差异化响应问题的充分统计量。

## 7.1.3 局部控制中最有效的统计方法

本章讨论并说明的 LC 概念严重依赖于聚类分析方法（例如参见 Kaufman and Rousseau [1990]），并应用于患者观察到的基线 x 特性。聚类是一种无监督学习（Barlow, 1989）；未使用来自结果变量（y）或治疗分配指示（r）的信息来引导（监督）患者簇的形成。虽然计算任务极其困难（NP 困难），但好消息是最近开发了若干种

> * 非确定性多项式时间。

功能多样的且相对快速（近似）的算法。例如，参见 Faley and Rafter (2002) 或 Wegman and Luo (2002)。

在 LC 分析的早期阶段，需要的统计建模和估计工具仅简单的嵌套 ANOVA 模型，包含簇效应、簇内治疗效应和误差，如表 7.1 所示。

### 表 7.1 具有治疗簇效应的嵌套 ANOVA 表

| 来源 | 自由度 | 解释 |
| --- | --- | --- |
| 簇（亚组） | $K =$ 簇的数量 | 当 $Xs$ 是工具变量 (IVs) 时，簇均值为局部平均治疗效应 (LATEs) |
| 簇内治疗 | $I =$ 信息丰富的簇数量 $\le K$ | 当 $X$ 变量是或不是 IV 时，治疗差异（LTDs）具有关注价值 |
| 误差 | 患者人数 - $K$ | 结果不确定性和/或拟合不足 |

在第 7.2 节和 7.3.3 节中，我们将看到 LC 用于分析、可视化和解释嵌套效应及其不确定性的新方法。

虽然调整选择偏倚和混杂的 LC 方法在直觉上显然具有非常好的敏感性，但对于某些读者来说，注意到 LC 的基本策略和战术也与 Rosenbaum 和 Rubin (1983, 1984) 的倾向评分 (PS) 原则，以及 McClellan、McNeil 和 Newhouse (1994) 的基于聚类的工具变量 (IV) 方法完全兼容，可能会让他们感到宽慰。本章的附录讨论了 PS 和 LC 方法共有的共同基础方面。

## 7.1.4 第 7 章剩余章节的内容

第 7.2 节引入了用于说明 LC 分析的 LSM10K 数值示例。第 7.3 节概述了局部控制分析的四个基本阶段，然后说明 LC 可以比第 7.2 节中描述的传统方法提供更深入、更详细的见解。最后，第 7.4 节提供了关于 LC 的结论，并简要总体地讨论了 LC 方法相对于相对于方法的优缺点：

- 使用全局多变量模型的协变量调整
- 逆概率加权
- 倾向评分匹配或分组
- 工具变量方法

## 7.2 对假设性患者注册数据的一些传统分析

### 7.2.1 LSIM10K 数据集简介

我们曾尝试获取近期在知名发表的观察性研究中描述和分析的若干大型数据集，这些研究通常使用某种形式的协变量调整来处理治疗选择偏倚。遗憾的是，这些数据集的所有者拒绝公开共享。我们最终决定模拟一个具有较大量患者（10,325 人）的数据集，产生的数据可以随本文出版物的 CD 分发。模拟的注册类数据也将用于说明各种方法，如第 7.2.2 节至 7.2.4 节概述的传统全局分析。

为了使内容具有合理性，Kerakes 及其同事（2000）中描述和分析的数据作为我们的模拟起点。该研究收集了 1997 年接受初始经皮干预（PCI 或血管成形术）的 396 名患者的 6 个月随访，接受常规护理或口服护理加昂贵的抗凝剂（III/IIIA 级联抑制剂）。原始数据集中的这些患者 x 特性（列在此）有助于量化治疗组之间疾病严重和/或患者失败的差异，并证明对结果和/或治疗选择具有预测性。

LSIM10K.SAS7BDAT 包含 10,325 名假设患者的 10 个模拟变量的值。为了简化分析，数据不缺失值。这 10 个变量定义如下：

mort60

此二值数值变量表征 6 个月死亡率。它包含 0（表示患者存活了 6 个月）或 1（表示患者未存活 6 个月）。

cardcost

此变量包含患者首次 PCI 后 6 个月内产生的累计心脏相关费用。对于 mort60=1 的患者，报告的费用因死亡而截断。

trtim

此二值数值变量识别治疗选择。它包含 0（表示常规护理）或 1（表示增加了假设性抗凝剂的常规护理）。

stent

此二值数值变量识别支架部署。值 0 表示未部署支架，而值 1 表示部署了支架。

height

此数值变量记录身高，四舍五入到最近的厘米。整数值范围从 133 到 197。

female
该二值数值变量，男性患者为 0，女性患者为 1。

diabetic
该二值数值变量，未确诊患糖尿病的患者为 0，确诊患糖尿病的患者为 1。

acutemi
该二值数值变量，近期未患过急性心肌梗死的患者为 0，在过去 7 天内曾患过急性心肌梗死的患者为 1。

ejfrac
该数值变量记录了患者的左心射血分数，四舍五入到最近的百分比。这些整数值的范围为 18% 到 77%。

veslproc
该数值变量记录患者初始 PCI（经皮血管介入术）涉及的血管数量。这些从 0 到 5 的整数值可以被视为六个序数值。在这里，我们将 veslproc 视为具有 6 个水平的因子（5 个自由度）或连续变量（线性进入模型时具有 1 个自由度）。

## 7.22 使用协变量调整进行死亡率和成本分析

在 LSIM10K 数据中，4679 名接受治疗患者的观察 6 个月死亡率为 1.218%，而 5646 名未治疗患者的死亡率为 3.719%，这对应于治疗风险比超过 3:1。等效地，风险差异（治疗组减去未治疗组）为 -2.501%，非常显著（t 统计量 -8.38，双侧 p 值 = 0.0000）。

使用 LSIM10K 数据对 6 个月死亡率进行协变量调整（也称为多变量建模）的简单模型，是：对二值死亡指标 aort60 以二值治疗指标 trtm 加上七个基线患者特征（其中体重、身高和病史按线性进入，自由度为 12，不计截距项）进行逻辑回归。该模型的受者工作特征（ROC）曲线下的面积为 0.7107，且存在拟合不足问题。另一方面，该简单模型的 R 平方统计量为 0.0653，非常差（低）。

最重要的是，该逻辑回归模型预测的死亡率在治疗组平均为 0.01218，未治疗组平均为 0.03720，这与之前观察到的未调整结果基本相同（仅在小数点后第五位有所差异）。换句话说，当结果是分类的时，协变量调整在平均上没有任何作用。

当结果变量是连续的时，例如 6 个月心脏相关成本变量（cardosto），协变量调整方法可能更有趣。例如，LSIM10K 数据中未治疗组的平均成本为 $15,188，治疗组为 $15,443；治疗组间平均成本未调整差异（$255）的 t 统计量为 t = 1.24，p值为 0.892。使用具有 12 个自由度的简单线性协变量调整多变量模型（R平方 = 0.0364），其右侧结构与之前描述的逻辑模型相同，最小二乘法平均成本在未治疗组为 $12,176，治疗组为 $12,305。调整后平均成本差异（+$129）的 t 统计量为 t = 0.62，p值为 0.538。因此，当结果是连续的时，协变量调整方法显然起到了作用。然而，全局模型对于治疗选择偏倚和混杂进行现实调整的希望很小。通常，它们与包含大量异质患者人群的大集的关联性很差。

这类协变量调整建模中一种非常灵活的方法被称为逆概率加权（IPW）。这种方法通常使用此处考虑的简单逻辑或回归模型，但每个患者结果的权重与其根据基线 x 特征接受所观察治疗选择的条件概率成反比。这些估计的条件概率被称为拟合倾向评分（fitted propensity scores），适当的计算和图形显示将在将在 7.2.3 节中说明。随后我们将使用 7.2.3 节中的倾向评分估计在 7.2.4 节中说明 IPW 方法。

## 7.2.3 使用估计倾向评分分位数进行死亡率分析

患者根据其基线 x 特征选择特定治疗方法的条件概率是其倾向评分（IP-PS）。倾向评分通常通过对观察选择（给定患者基线 x 特征）的二值指标 ittm = 0 或 1 拟合逻辑（或倾向）模型来生成。由于所有注意力最终将集中在生成的倾向评分估计上（而不是任何 p 值或模型的其他特征），因此不假设过拟合会导致惩罚。研究人员通常拟合非参数全局模型；在这里，我们在所有七个可用协变量中拟合了一个因子阶二次模型。该模型消耗了 46 个自由度，不计截距项。

该模型的 ROC 曲线下的面积为 0.6993，没有显著的拟合不足问题。另一方面，该模型的 R 平方统计量为 0.0867，非常差（低）。

满意的倾向评分估计的一个基本特征是，它们的行为至少在近似上真实的倾向评分不同。具体而言，对（四舍入后的）倾向评分进行条件处理应该产生的 x 协变量分布对（治疗组对比未治疗组）没有显著差异。毕竟，根据倾向评分条件将使此类子分类变得完全相同；参见附录。换句话说，如果根据倾向评分对患者排序并分为10个分位数，那么 x 协变量分布对（治疗组 vs 未治疗组）应该大致相同。例如，图 7.1 显示（在左图中），注意边际分布的下尾（即受损最严重的患者）需要由治疗组占主导。同时，在第 10 个倾向评分分位数中（右图中最后一对箱线图），注意对应的 ejract 分布几乎完全相同。

# 160 使用 SAS 进行观测健康数据分析

图 7.2 分位数内估计倾向得分均值 vs 观察到的治疗患者比例

![](img/fe9ff008f88baacd415148b0b25dd58c_174_0.png)

局部治疗比例 = -0.0101 + 1.0223 * 分位数内平均估计倾向得分

图 7.3 按倾向得分分位数划分的治疗与未治疗患者人数

![](img/fe9ff008f88baacd415148b0b25dd58c_174_1.png)

倾向得分法（以及局部控制法）区别于粗略调整（CA）和 IPW 建模的另一个基本概念是，它可以简单地忽略来自某些患者的数据。例如，如果图 7.3 中第一个分位数中所有倾向得分估计最低的患者未接受治疗，那么这些患者的数据应该被弃用。同样，如果图 7.3 第 10 个分位数中所有倾向得分估计最高的患者都接受了治疗，那么他们的数据也应该被弃用。接下来将对这些排除集合进行更具技术性的解释。

图 7.4 使用每个包含 40 个单元的直方图展示了倾向得分估计的分布。只有在这两个分布共同支撑内的患者具有足够的可比性，才能纳入倾向得分分析。对于 LSIM10K 数据，这两个分布可能具有相同的范围，从 0.025 到 0.925。对于具有不同范围的倾向得分估计（治疗 vs 未治疗）分布对，所有落在两个分布支持的最大范围之外的患者数据都应弃弃。倾向得分分位数应仅使用落在该最大支持范围内的患者形成。

# 第 7 章 使用 JMP 16 进行局部控制法

图 7.4 估计倾向得分的详细直方图

![](img/fe9ff008f88baacd415148b0b25dd58c_175_0.png)

倾向得分分位数分析的剩余步骤是：

- 1. 计算每个分位数内的 LTDs 及其方差
- 2. 计算 LTD 主效应 = 跨分位数的位数内 LTD 平均值及其方差
- 3. 计算 LTD 主效应显著性检验的 t 统计量和 p 值

对于 LSIM10K 数据，t = -2.95，p = 0.026。在图 7.5 中，LSIM10K 数据中的假设治疗对第 9 和第 10 个倾向得分分位数的患者提供了最大的增量收益（即那些最有可能选择/接受治疗的人）。综而言，与使用全局（“错误的”）模型的协变量调整法相比，倾向得分分位数法为治疗主效应提供了大得多（偏差更小）的估计，且精度略低（更真实）。

图 7.5 按倾向得分分位数划分的 6 个月死亡率 LTDs（治疗减去未治疗）

![](img/fe9ff008f88baacd415148b0b25dd58c_175_1.png)

# 7.2.4 使用概率加权对死亡率和成本进行分析

适用于 LSIM10K 数据 6 个月死亡率逆概率加权的模型是（加权的）逻辑回归，以二值化治疗指标和所有七项基线特征为因变量（再次，身高和提取进行线性处理，且模型自由度 = 12，不包括截距项）。治疗患者的 IPW 与 1/PS 成比例，未治疗患者则为 1/(1-PS)。因此，虽然与 7.2.2 节中的未加权平均具有可比性，但估计值需要重新缩放到 10,325，这是 LSIM10K 数据中的预测总数。如果不进行这种缩放，权重总和将达到 20,796，这将导致精度的虚假增加，等同于假设数据人数是实际人数的两倍以上！

缩放后总和为 10,325 的权重范围从 0.519 到 11.38，总结在图 7.6 中。未治疗预测的平均权重为 0.9114（即小于 5,646 名患者的大样本量），而治疗患者的权重为 1.1050（即大于 4,679 名患者的较小样本）。

# 图 7.6 基于倾向得分估计的治疗或未治疗患者的 IPWs

![](img/fe9ff008f88baacd415148b0b25dd58c_176_0.png)

所得 IPW 预测的 ROC 曲线下面积增加到 0.7550，且没有显著的拟合不良问题。另一方面，该简单模型的 R 平方统计量仍为 0.1041，表现较差。治疗患者的 6 个月死亡风险 IPW 预测平均值为 0.01278，未治疗患者为 0.03994。IPW 调整后的主效应差异为 0.02718，而未调整的差异已所示。

# 第 7 章 使用 JMP 16 的局部控制方法

## 表 7.2（续）

| 第三阶段 LC 策略： | 在局部控制（LC）分析的第三（也是最重要的）阶段，研究人员会探索使用替代方法形成聚类的影响（例如，使用可用 x 协变量的不同子集、不同的患者相似性或差异性指标、替代聚类算法以及[再次]不同数量的聚类）。由于这一阶段枯燥且重复，最好通过调用某种形式的批处理算法来完成。 |
| 第四阶段 LC 策略： | 由于 LC 分析前三个阶段的结果可能会使患者差异反应问题变得毫无意义，LC 方法合理地将所有因果型和/或预测类型的分析推到最后。 |
| 识别预测差异反应的基线患者特征 | 一旦估计了簇的 LTD（局部治疗差异值），一种非常有用的 LC 策略是将簇中所有患者（无论已治疗还是未治疗）的观测结果替换为此 LTD 值。正如我们将看到的，这种简单的策略对于评估拟合模型并使其更具相关性和易于解释有很大帮助。 |

使用全局参数模型（可能结合逆概率加权 IPW）的传统协变量调整（CA）方法其劣势在于，它们本质上必须从 LC 分析中真正的最后、最不明确且可能最令人沮丧的阶段开始。研究人员可能会发现，差异反应实际上很难预测。 |

# 166 使用 SAS 进行观察性健康数据分析

无论如何，开始学习关注局部（亚组内）治疗比较价值的逻辑方法就是直接进入 JMP，利用你拥有的任何患者基线 x 特征来直观地看到使用此处所示的 JMP 脚本能带你多远。

启动用于自动化局部控制的 JMP 脚本语言（JSL）文件的方便方法是在 JMP 的“自定义 (Customize) -> 菜单和工具栏 (Menus and Tool Bars)”中修改 JMP 菜单上的“分析 (Analyze)”选项列表。图 7.8 显示我选择了 JMP 分析中的第五和第六位置，以修改我的局部控制和人工 LTD 分布的图标和标题。

## 图 7.8 自定义的 JMP 分析

![](img/fe9ff008f88baacd415148b0b25dd58c_180_0.png)

当选择“局部控制 (Local Control)”菜单选项时，如果 JMP 中没有打开任何数据集，JMP 首先显示打开 *JMP 或 *SASBDAT 数据集的对话框，如图 7.9 所示。为了跟随此处所示的计算，请打开 LSM10K数据集。

JMP 然后显示自定义的“选择列 (Select Columns)”对话框，如图 7.10 所示。注意，图中显示前两列（mort6mo 和 cardcost）首先在左侧变量列表中高亮（使用左鼠标 Shift+点击），并通过点击 **y, 结果 (Outcomes)** 选择框转移到右侧。同样，第三列（trtm）被选为 **t, 治疗因子 (Treatment Factor)**，而第四到第十列（stent, height, ..., vesc）被选为结果和/治疗选择的七个 **x, 预测因子 (Predictors)**。

# 第 7 章：使用 JMP 的局部控制方法 167

## 图 7.9 打开数据文件的对话框，高亮了 LSIM10K 数据集

![](img/fe9ff008f88baacd415148b0b25dd58c_181_0.png)

## 图 7.10 用于局部控制的 JMP 选择列对话框

![](img/fe9ff008f88baacd415148b0b25dd58c_181.png)

用于局部控制和人工 LTD 分布的 JMP 脚本有一个关键限制。所有结果 y 变量通过计算平均值进行分析，x 变量通过计算患者之间的距离（差异性）对患者进行聚类。因此，所有 y 和 x 变量在 JMP 中都需要声明为数值和连续型。也就是说，离散 y 变量需要先使用一个或多个虚拟变量（0-1）重新编码，而其他 y 和 x 变量需要使用有限的实数进行编码。只有当二元（类）变量作为 t 治疗因子时，才在 JMP 中声明为名义（或有序）。输入局部控制 JMP 脚本的 y 和 x 变量的位置和缩放并不重要，因为脚本会将所有 x 变量重置为 0 并对其进行标准化处理。

注意图 7.10 对话框左下角的一对频率按钮允许用户在同方差或局部异方差假设之间进行选择，这是局部控制分析中的方差。为了提供信息，每个患者簇必须至少包含两个已治疗患者和两个未治疗患者。由于估计的簇内方差可以小到 0，跨簇的 LTD 平均值可以……

## 170 使用 SAS 进行观察性健康数据分析

图 7.13 第一个结果中 LTD 主效应的 LC 去偏轨迹（TRACE）

### 第一个结果：Y1 = 六个月内死亡率

Y1 = 跨簇平均 LTD 结果 ± 两倍标准差
NCreq = 请求的簇数量

![](img/fe9ff008f88baacd415148b0b25dd58c_184_0.png)

表 7.3 图 7.13 中显示的跨簇汇总统计量

| NCreq | NCInfo | Y1 LTD 主效应 | Y1 局部标准误 | Y1 下限 | Y1 上限 |
|---|---|---|---|---|---|
| 1 | 1 | -0.0250 | 0.0013 | -0.0313 | -0.0188 |
| 5 | 5 | -0.0270 | 0.0019 | -0.0333 | -0.0206 |
| 10 | 10 | -0.0306 | 0.0026 | -0.0371 | -0.0241 |
| 20 | 20 | -0.0315 | 0.0038 | -0.0383 | -0.0248 |
| 50 | 50 | -0.0351 | 0.0040 | -0.0419 | -0.0283 |
| 100 | 100 | -0.0372 | 0.0046 | -0.0441 | -0.0302 |
| 200 | 199 | -0.0393 | 0.0035 | -0.0463 | -0.0322 |
| 500 | 492 | -0.0398 | 0.0060 | -0.0470 | -0.0326 |
| 700 | 660 | -0.0383 | 0.0063 | -0.0456 | -0.0311 |
| 900 | 816 | -0.0365 | 0.0063 | -0.0438 | -0.0293 |

NCreq = 请求的簇数量
NCInfo = 找到的有信息的簇数量

## 第 7 章：使用 JMP 17 的局部控制方法

图 7.14 第二个结果中 LTD 主效应的 LC 去偏轨迹（TRACE）
第二个结果：六个月累积心脏相关成本

Y2 = 跨簇平均 LTD 结果 ± 两倍标准差
NCreq = 请求的簇数量

![](img/fe9ff008f88baacd415148b0b25dd58c_185_0.png)

一旦你决定停止探索不同数量的簇，点击“结束”（End）。图 7.12 亦所示。虽然此操作激活了第一阶段内的自动迭代序列，但你仍然希望探索为每个指定的簇数量创建的一个或多个 JMP 数据表。正如我们在这里看到的，这些表每个都包含一个或多个内置脚本 `Utsumy1` 和 `Utsumy2`，用于重新部署这些图。这允许对图表进行自定义。例如，用户可以更改刻度间距、标记标签的方向以及描述性轴标签的规范。生成的图表和表格随后可以保存到 JMP 文件中，并最终保存到用户的硬盘，作为 PDF、RTF 或 DOC 文件。

例如，JMP 表 `LSM10K_` 包含了在（结果）上 LTD 主效应的 LC 去偏轨迹图表中显示的统计量。该表还包含名为 `Utsumy1` 和 `Utsumy2` 的脚本，用于重新部署这些图。这允许对图表进行自定义。

在 7.13 及其对应的表（数值列表）中，注意 Y1 死亡率结果的 LTD 分布均值（治疗主效应），接受治疗的患者预期 6 个月死亡率低于未治疗患者。此外，这种差异最初远大于 TRACE 中的去偏值，因为患者比较更加局部，并且更加（通过使用更小或更多的簇）。初始分组结果（治疗与未治疗死亡率 = -0.025）本质上假设所有可用患者都在同一个单簇中。如图 7.15 左侧所示，LTD 分布并不接近平滑连续。例如，它在 LTD 处有一个质量为 0.690 的点。请求的簇越多（找到了 8 个和 16 个信息簇）。换句话说，有充分证据表明，治疗选择和混杂因素以一种不利的方式偏置了死亡结果非局部比较的均值。死亡率的 LTD 分布均值随着其变得更加局部而最向左偏移（从 -0.0250 变为 NCreq = 500 时的 -0.0398，再到 NCreq = 900 时的 -0.0365），但该 LTD 分布仍然复杂（不平滑），但限制在 [-1.00, +1.00] 内。

## 使用 SAS 进行观察性数据分析

图 7.14 中 Y2=cost 结果的第二次无偏 TRACE 提示了一些可能的混乱。事实上，cost 分布（治疗主效应）剧烈波动，然后明显上升，最后部分回升。如图 7.15 右侧所示，LTD 分布包含一些异常值，如 -$38K,-21K、+$28K、+$29K,-34K、+$82K 和 +98K。相反，成本的 LTD 分布比死亡率的 LTD 分布平滑得多。总之，没有证据表明治疗选择和混杂因素向上或向下偏了 LSM10 数据。事实上，cost 均值的宽范围（从 +$69 到 -$74）由图 7.14 支持。注意图 7.14 中固定簇数量计算的不确定性估计值（sigma）明显低估了通过改变簇数量所显示的成本真实不确定性。

表 7.4 图 7.14 中显示的跨簇统计量

| NCreq | NCInfo | Y2 LTD | Y2 局部标准误 | Y2 下限 | Y2 上限 |
|---|---|---|---|---|---|
| 1 | 1 | 255.08 | 206.21 | -157.63 | 667.50 |
| 5 | 5 | 664.94 | 208.99 | 246.96 | 1082.92 |
| 10 | 10 | 698.80 | 214.19 | 270.42 | 1127.19 |
| 20 | 20 | 341.77 | 220.48 | -99.19 | 782.74 |
| 50 | 50 | -71.92 | 214.84 | -501.59 | 357.75 |
| 100 | 100 | -73.59 | 212.71 | -449.02 | 351.83 |
| 200 | 199 | -24.28 | 209.32 | -442.93 | 394.37 |
| 500 | 492 | 127.11 | 184.59 | -242.08 | 496.30 |
| 700 | 660 | 248.93 | 183.97 | -119.01 | 616.87 |
| 900 | 816 | 312.96 | 181.35 | -49.74 | 673.66 |

> **NCreq = 请求的簇数量**
> **NCInfo = 找到的有信息的簇数量**
> **所有结果以 1998 美元 ($) 为单位**

为了创建图 7.15 显示的图表，打开由 LocalControl 创建的 LC_900 数据表。该表包含 900 行簇（1 到 900），但来自信息簇的 LTD 估计值 Y1TD 和 Y2LTD 只有 816 个空值。该表还包含名为 `LTDdist1` 和 `LTDdist2` 的脚本，用于使用直方图、正态概率图和表格统计量描述 LTD 分布（对于死亡率和成本），如图 7.15 所示。脚本 `Y12dist` 生成图 7.16 显示的图表，而第四个脚本 `LTDjoin` 在第二（及第四）阶段控制分析中有用。

## 第 7 章：使用 JMP 17 的局部控制方法

图 7.15 816 个有信息簇的 LTD 图表和汇总统计量

Y1 = 死亡率的 LTD 分布
Y2 = 成本的 LTD 分布

![](img/fe9ff008f88baacd415148b0b25dd58c_187_0.png)

| | | |
|---|---|---|
| 均值 LTD | -0.0385 | 168.74 |
| 标准差 | 0.14882 | 4,962.92 |
| 均值标准误 | 0.00150 | 50.09 |
| 95% 均值上限 | -0.0356 | 266.93 |
| 95% 均值下限 | -0.0415 | 70.55 |
| 非参数密度 | | |
| 核标准差 | 0.02131 | 710.55 |

同样注意，这两个 LTD 分布在直方图和概率图中往往比拟合程度良好的正态分布更具尖峰性。

注意死亡率 LTD 分布中 -1 和 0 处的质量点在图 7.15 的左侧清晰可见。

## 174 使用 SAS 进行观察性数据分析

图 7.16 816 个有信息簇的双变量 LTD 散点图

![](img/fe9ff008f88baacd415148b0b25dd58c_188_0.png)

最后，从图 7.9 可以清楚看出，死亡率和成本结果在（双变量）联合分布中几乎或没有关联（相关性）。事实上，注意成本极端的患者倾向于死亡。同样，极端的死亡率往往具有较比例的成本。

### 7.3.3 第二阶段：确定 LTD 分布是否显著

假设研究人员已使用第一阶段局部控制根据基线特征定义了一组簇，并估计了相应的 LTD 分布。除非该分布与纯随机分配患者到簇所产生的 LTD 分布不同，否则它是没有意义的。换句话说，当这两个分布不同时，用于形成簇的相似性或差异性衡量实际上比随机患者特征更有信息量！

具体而言，第二阶段局部控制的目标是询问观察协变量是否能预测真实的患者相似性，即观测到的 LTD 分布是否不同人工（完全随机）的 LTD 分布。当这两个分布不同时，观测到的 LTD 分布被认为是显著的（具有统计学意义的）。

## 第 7 章 使用 JMP 17 的局部控制方法

在此处所示，您应该首先调用 `LTDjoin` 脚本并使用 `LC_900` 数据（用于请求的聚类）。与 LSIM10K 数据相比，LC_900 表包含 900 行（每个聚类一行）以及针对 816 个信息聚类的 816 个非缺失 LTD 估计，而生成的合并表则包含 10,325 行个体患者数据、一个聚类 ID 变量（每个患者包含一个从 1 到 900 的整数）以及 816 个信息聚类内患者的 9,839 个非缺失 LTD 估计。这就是人工 LTD 分布脚本设计用于操作的特定类型 JMP 表格。

调用 JMP aLTD 脚本会显示图 7.17 所示的自定义“选择列”对话框，但仅指定了一个二元治疗因素，且没有指定患者基线特征特征。然而，研究人员必须指定：

- 1. 聚类 ID 变量的名称（此处为 C_900）
- 2. 复制总数（显示的默认值为 25）
- 3. 随机种子值（显示的默认值为 12,345）

## 图 7.17 人工 LTD 分布对话框

![](img/fe9ff008f88baacd415148b0b25dd58c_189_0.png)

研究人员可能需要指定一个特定次数的重复（例如，三次），以估算计算所需的时间。每当使用第二次调用 aLTD 脚本来提高精度时，请务必在第二次运行中使用不同的初始值，以确保两批人工 LTD 估计是相互独立的并可以合并。另一方面，如果使用第二次调用是为了评估二元 y 结果，如果您希望估计这两个结果的联合 LTD 分布，则请务必在两次运行中使用相同的重复次数和相同的初始值。

图 7.18 展示了在 JMP 中使用 Y 和 X 散图比较两个不相关聚类（此处大小不同）的标准方法。在图 7.18 中，Y 变量包含 LTD 估计，而二元 X 变量将每个估计标记为“观测值”或“人工”。观测到的 LTD 分布由信息聚类内 9,816 名患者中的 816 个样本组成。人工 LTD 分布由 25×816 = 20,400 个非缺失 LTD 估计组成；每组 816 个人工 LTD 估计都使用从原始 10,325 名患者中随机出的 9,839 名患者的数据。另一方面，由于死亡变量是二元的，如图 7.18 和图 7.19 所示，在合并的观测和人工 LTD 样本中仅出现了 254 个不同的 LTD 数值。

## 图 7.18 使用散点图进行 JMP 并列比较

### 人工与观测 LTD 分布的备选项

![](img/fe9ff008f88baacd415148b0b25dd58c_190_0.png)

即使假设个体患者结果是同方差的，某些人可能认为 LTD 需要加权，因为它们仍然可能具有明显的异方差性。对于具有 $n > 1$ 个患者的信息聚类，令 $np$ 代表治疗患者的数量，其中 $p$ 表示受治疗的倾向，且 $0 < 1/n \leq p \leq (n-1)/n < 1$。未治疗患者的数量为 $np(1-p)$。因此，局部差 $(\hat{Y}_{\text{treated}}-\hat{Y}_{\text{untreated}})$ 的方差与 $1/(np(1-p))$ 成比。因此，可以为该聚类的 LTD 估计分配与 $np(1-p)$ 成比的权重（即与方差成比）。这些权重随后需要重新归一化，以便在该示例中和为 $\Sigma = 9839$。相反，在这里我们为 $n$ 个患者的信息聚类计算出的 LTD 分配频率 $n$，从而确保 $\Sigma = 9839$。

遗憾的是，图 7.19 对来说在比较观测和人工 LTD 分布方面似乎并不特别帮助。除了图 7.18 那种可视化的变体外，JMP 平台还包含几种其他方法来测试（两个）样本所代表的分布之间的差异。唉，9839 个观测 LTD 主效应的比较或或少预期会表明，由于此类样本量，即使是微小的差异也是显著的！比较 aLTD 平均值与观测 LTD 平均值的 Dunn 方法得出 Abs(Diff)-LSD=0.009 ($p < .0001$)。LTD 分布的方差不同 ($p < .0001$)，假设方差不等的 Welch 检验得出自由度为 1041 的 t 检验 7.986。Wilcox/Kruskal-Wallis 秩检验得出 z 分 -5.508 ($p < .0001$)。

尽管如此，显然观测到的 LTD 分布在 -1 处的概率原子较大，在 0 处的概率原子较小，这并没有影响 LTD 分布：

| LTD 估计 | 9839 中的观测频率 | 观测患者比例 | 20400 中的人工频率 | 人工患者比例 |
| :--- | :--- | :--- | :--- | :--- |
| -1.00 | 60 | 0.0061 | 48 | 0.0024 |
| 0.00 | 6789 | 0.690 | 15192 | 0.745 |
| +1.00 | 14 | 0.0014 | 33 | 0.0016 |

同样，图 7.19 中显示的经验 CDF 比较强烈地表明，816 个信息聚类的观测到的 LTD 分布确实是显著的。观测到的 LTD 分布具有更厚的左尾（有利于治疗的负值 LTD）和可能具有更细的右尾（不利于治疗的正值 LTD）。我们的局部控制分析确实揭示了偏偏。在死亡率初始观测平均差异（当将所有患者分配到单个聚类时，4679 名治疗患者减去 5646 名未治疗患者）为 -0.025（即 -2.5%）之后，816 个信息聚类效应为 -2.45% 的人工 LTD 平均效应略大（负值较小），但它也是有偏的。准确地说，

### 第三阶段：执行系统分析

**图 7.19 观测（实线）与人工（虚线）CDF 的视觉比较**
（注：此处根据上下文推断图片标题，原文未提供完整标题文本，仅有描述）

研究人员可能需要指定特定次数的重复来估计算计算所需的时间。局部控制第三阶段的基本概念是，观测 LTD 分布需要显示在二元治疗方面是相对稳定的。当聚类数量增加时，这种方法会变得更加复杂。相反，目前没有 JMP 交互式局部控制用于人工 LTD 分布的自动实现。因此，我在这里描述了 LSIM10K 的一些替代方案，并回顾了系统分析应使用的基本聚类概念。

### 7.3.4.1 可以独立的替代聚类

预测治疗选择和死亡 y 结果三个基线特征是 acute、acumen 和 extract。使用这三个患者特征的局部控制是简洁的。有趣的是，局部局部控制去偏因子与图 7.13 相似，而相应的代价轨迹则比图 7.14 更平滑。此外，信息聚类的数量在 300 到 900 聚类之间下降到 166。（300 中的 166 个信息聚类包含了 98.4% 的患者，900 中的 166 个信息聚类包含了所有患者的 92.6%，治疗患者的 96.0%，未治疗患者的 89.9%）。最后，900 个请求聚类的观测 LTD 分布再次显著。

### 7.3.4.2 敏感性分析的聚类概念回顾

聚类的目标是将患者划分为互斥且尽的子组。虽然聚类内的患者其 x 向量应该尽可能相似，但需要一种衡量两个 x 向量之间相似性或差异的指标来这样做（Kaufman and Rousseeuw, 1990）。我的局部控制 JMP 脚本使用 x 变量的标准（均值为 0，方差为 1）p 坐标来表示患者，这等同于患者之间的马氏距离距离（Rubin, 1980）。各种距离和相似性度量，例如 Dice 系数、Jaccard 系数和余弦系数，也广泛用于聚类。

假设某些患者特征是只有相对较少水平或无序水平的定性因素。分析师可能希望同一聚类内的所有患者在这些特定的 x 组件上匹配。或者，具有 k 个水平的 x 因子可以还原为 k–1 个（二元）变量。

# 第 7 章：使用 JMP 17 的局部控制方法

如果 x 协变量主要用作工具变量，分析师可能希望在定义患者差异性时赋予它们额外的权重。例如，McClellan 及其同事（1994）在对 205,022 名老年患者的研究中，使用距离入院医院的近似距离（根据邮政编码得出）作为其初始关键变量；唯一可用的 x 特征是年龄、性别和种族。对于如此庞大的受试群体，逻辑策略是首先将患者按距离医院的远近分为几个区间。在这些初始分层内部，可以很容易地形成较小的聚类，例如1，通过根据性别和种族对患者进行匹配，并将他们分组到不同的范围内。

患者聚类不需要是分层的，但生成的层级图（树图）在敏感性分析中可能非常有用，这些分析旨在刻意改变聚类的数量，以研究 LTD（局部治疗差异）分布的稳定性。

凝聚性（自下而上）聚类方法从每个患者自成一类开始，通过迭代合并个体和/或患者簇来形成越来越大的聚类。这是无监督分层分析的“自然”方式，且绝大多数聚类算法都是这样运行的。

分裂性（自上而下）聚类方法从一个包含所有患者的单一簇开始，侧重于使树顶部的极大型簇具有最大的意义。Kaufman 和 Rousseau（1990）的“diana”方法就是分裂式的。

为了创建更多聚类，使用最小化簇内最大差异的连接方法（linkage methods）也比使用其他连接方法更有意义。

如果一个簇被认为是均匀（纯）的，如果该簇内的所有受试者接受了相同的治疗（要么全部为 t=0，要么全部为 t=1）。仅在纯簇内使用方法，无法观察到治疗之间的任何局部结果（y）差异！从这个意义上说，局部控制会自动丢弃所有与所有未治疗患者不同的受治疗患者的信息，以及所有与所有治疗患者不同的未治疗患者的信息。位于治疗组和未治疗组倾向评分分布共同支持区域之外的患者应被排除在分析之外，因为这一基本原则（即仅比较具有可性的患者）通常被使用倾向评分方法增强的协变量调整实践者所忽略。

为了在不假设患者结果同方差性（方差相等）的情况下充分获取簇内局部治疗差异的信息，每个簇在每个治疗组至少包含两个患者。需要这些患者来计算两个治疗结果均值的异方差标准误差，然后计算得出的局部治疗差异。

## 7.3.5 第四阶段：识别预测差异治疗反应的基线患者特征

局部控制分析第四阶段也是最终阶段的目标是回答此类之的问题：“治疗的收益和/或风险是否随观察到的患者特征发生系统性变化？”“哪类患者接受治疗比不治疗更好？”局部控制分析的前三个阶段通过解决一个更基础的问题为回答最终问题提供了途径：“是否存在由于治疗引起的结果的重要差异？”具体来说，第一阶段识别 LTD 分布，第二阶段确定 LTD 分布是否显著，第三阶段确立哪些显著的 LTD 分布是最典型的。在第四阶段开始之前，前三个阶段的结果可能已经让这些问题（即差异收益/风险变化的预测）本质上变得毫无意义，因为几乎没有或没有发现任何形式的患者对治疗的差异反应。

阶段分析可以使用传统的协变量调整方法来预测 LTD 变量，这些变量通过将簇的（显著且典型的）LTD 值分配给簇内的所有患者（治疗的或未治疗的）。同样，落在无信息簇中的每个患者的 LTD 结果是缺失的。这种策略允许回答诸如“处于观察到的 LTD 分布左尾和右尾的患者其基线 x 特征如何？”以及“哪类患者最不可能（或最可能）做出治疗选择？”

鉴于我对全局方法的不信任，我最喜欢的预测建模第四阶段控制策略是依赖局部的半参数方法（如回归树）来建模 LTD。

## 182 使用 SAS 进行观测性健康数据分析

| 术语 | 估计值 | 标准误差 | t 比率 | Prob>t |
|---|---|---|---|---|
| (height-173.388)*diabetic[0] | -0.001409 | 0.000276 | -5.11 | <0001 |
| stent[0]*diabetic[0] | -0.008277 | 0.001828 | -4.53 | <0001 |
| acutemi[0]*(ejfract-53.3258) | 0.0014733 | 0.000344 | 4.28 | <0001 |
| height | 0.0012274 | 0.00038 | 3.23 | 0.0012 |
| stent[0] | -0.007796 | 0.002929 | -2.66 | 0.0078 |
| female[0]*diabetic[0] | 0.007139 | 0.002721 | 2.61 | 0.0091 |
| (height-173.388)*acutemi[0] | -0.000705 | 0.000301 | -2.34 | 0.0194 |
| female[0]*vesproc-1.15983 | 0.0078460 | 0.003395 | 2.31 | 0.0209 |
| stent[0]*female[0] | -0.004199 | 0.001942 | -2.16 | 0.0306 |
| (ejfract-53.3258)*(vesproc-1.15983) | 0.0005172 | 0.000272 | 1.90 | 0.0572 |
| (height-173.388)*vesproc-1.15983 | -0.000443 | 0.00033 | -1.32 | 0.1882 |
| (diabetic-173.388)*female[0] | 0.0001881 | 0.000197 | 0.95 | 0.3400 |
| diabetic[0]*acutemi[0] | -0.003499 | 0.003981 | -0.88 | 0.3806 |
| vesproc | 0.005063 | 0.002269 | 0.81 | 0.4188 |
| stent[0]*(vesproc-1.15983) | 0.0004261 | 0.000219 | 0.19 | 0.8510 |
| diabetic[0] | -0.000365 | 0.004074 | -0.09 | 0.9287 |
| stent[0]*height-173.388 | -5.615e-6 | 0.000193 | -0.03 | 0.9767 |

总之，我发现局部控制方法生成的 LTD 分布足够丰富且详细，以至于实际上难以使用传统的回归技术（参数或半参数）进行建模。显然，LTD 分布可以同时捕捉原始数据中的信号和（大量的）噪声！

## 7.4 结论

我们已经看到，分组（blocking）和随机化等基本概念在前瞻性实验设计（DoE）中起的重要作用，在受试数据分析中也可以发挥类似的功能。这些变体包括回顾性局部控制和重采样（有放回或不放回）。这些高度灵活的方法，表 7.5 对观测性数据分析五种替代方法进行了简要定义，并讨论了它们的主要优缺点。

## 第7章：使用 JMP 的局部控制方法 183

## 表 7.5 观测性数据分析的五种通用方法

### 使用多元模型的协变量调整 (CA)
- **历史**：方差分析（ANOVA）和回归模型的推广。
- **优点**：无处不在；被密切关注并广泛接受；在所有统计中中。
- **缺点**：本质上忽略了不平衡（例如，始终使用所有可用数据）；全局性的；参数模型难以可视化且可能不现实；结果对模型设定异常地敏感；p 值小仅仅是因为样本量大。

### 逆概率加权 (IPW)
- **历史**：CA 的启发式修正，类似于样本调查中的 Horvitz-Thompson 调整。
- **优点**：执行简单；确实调整了治疗选择比例的局部变化（不平衡）；需要对（对角）加权回归进行稳健处理。
- **缺点**：与 CA 基本相同；IPW 侧重于观测结果加权（从不真正忽略无信息集群）；基本的方差假设有些反直觉。

### 倾向评分 (PS) 匹配和亚组
- **历史**：基本理论在过去25年里引起了更多关注。
- **优点**：直观、假设简单；应用广泛；结果易于展示。
- **缺点**：结果可能没有看起来那么精确；仅限特定实现。

### 工具变量 (IV) 方法
- **历史**：当变量内生时，在模型中加入 IV 可以识别因果效应。
- **优点**：通过对集群内治疗和未治疗患者的结果取平均，IV 方法至少避免了方差翻倍。
- **缺点**：IV 假设非常强且不可检验；纯 IV 分析（因此未能估计 LTD）对我来说是一个极高的代价！

### 使用无监督学习的局部控制方法
- **历史**：方差分析（ANOVA）和回归模型的推广（集群内）。
- **优点**：直观、假设简单；应用广泛；保证优于评分。
- **缺点**：非常新；与传统模型的关注点完全不同；仅限实现。

## 184 使用 SAS 进行观测性健康数据分析

总之，我发现局部控制方法生成的 LTD 分布足够丰富且详细，以至于实际上难以使用传统的回归技术（参数或半参数）进行建模。显然，LTD 分布可以同时捕捉原始数据中的信号和（大量的）噪声！

相比之下，McClellan、 McNeil 和 Newhouse (1994) 基于 7.1 中第 2 行关于集群内治疗因素 LATE 水平的 IV 方法。事实上，这种方法唯一的明显缺点是它使方差翻倍。

随机可能仍然是人类科学研究的金标准。但在健康研究和药物经济学背景下，在常规实践环境中进行前瞻性实验涉及的/参与激励会导致患者和临床医生产生不现实的行为。如果你想对没有治疗方案时的情况产生真实的见解，难道不应该使用来自真实经验的数据数吗？使用真实数据来回答现实问题完全没有问题。另一方面，很明显，如果研究人员能够获得更好的（完整的）观测性数据和更好的局部控制软件，就能开发出更好的见解，特别是对于三阶段局部控制系统敏感性分析。

## 附录：倾向评分与分层/平衡评分

### A.1 倾向评分基本定理的回顾

对于给定的基准特征 $x$ 向量，该患者的倾向评分（propensity score）是其接受两种治疗方法第一种（例如 $t=1$）的条件概率。该条件概率在方程 (A.1) 中用符号“p”表示。因此，根据定义，$p$ 仅是给定基准特征 $x$ 向量的函数。

```



$p = \text{Pr}(t \mid x) \quad (A.1)$

方程 `(A.2)` 展示了倾向评分基本条件独立性（Rosenbaum and Rubin, 1983）的一个简单四行证明。第一行左侧的 $\text{Pr}(x, t \mid p)$ 表示，在给定患者（可能未知的、真实的）倾向评分 `p` 的条件下，该患者的基准 `x` 向量与其治疗选择 `t` 的条件联合分布。第一行右侧的因分解则来自条件概率的定义（$\phi$）。在第二行中，通过注意到 `p` 是 `x` 的函数，因此同时对 `x` 和 `p` 取条件并不强于仅对 `x` 取条件，从而简化了第二项。`(A.1)` 显示 `t` 要么是 `p`，要么是 `(1-p)`。最后，第四行的得出是因为第三行显示对 `t` 的分布取条件并不强于仅对 `p` 取条件。

```
$$\text{Pr}(x, t \mid p) = \text{Pr}(x \mid p)\text{Pr}(t \mid x)$$

$= \text{Pr}(x \mid p)p$ 或 $\text{Pr}(x \mid p)(1-p)$

$= \text{Pr}(x \mid p)\text{Pr}(t \mid p) \ (A.2)$
```



总结来说，方程 `(A.2)` 证明了在真实 `p` 的条件下，`x` 和 `t` 的联合分布必须分解为给定 `p` 条件下 `x` 的条件分布乘以 `t` 的条件分布的乘积。在统计学和概率论中，这种因分解具有深远意义。因此，基准 `x` 特征的分布被证明与治疗选择的分布是统计独立的，两者都取决于（可能未知的、真实的）`p`。

从技术上讲，方程 `(A.2)` 第四行的因子 `Pr(t | p)` 实际上显示固定 `p` 值定义了一个患者区块（block）。为了避免产生过多的区块，可以将 `p` 保留两位或三位小数。对于给定的舍入后的 `p` 值，`x` 的分布可能相当复杂，但至少（由于独立性）该分布在每个区块（由单个舍入的 `p` 值定义）内的受治疗患者和未治疗患者之间是相同的。另一方面，`x` 在不同区块之间变化的特性（即随着 `p` 的变化而变化）为将这些倾向子群体称为“区块”提供了充分的动机和理由。

同样，方程 `(A.2)` 第四行的第二个因子 `Pr(t | p)` 定义了局部比例上的治疗平衡（或不平衡）。具体而言，在 `p=0.50` 的区块内，受治疗患者与未治疗患者的局部（块内）比例预计非常接近 1:1。

## 使用 SAS 分析观察性护理数据

在 `p` 不与 `x` 一起出现的集中，从所有实际角度来看，整个数据集中只有一个区块！在随机临床试验 `RCTs` 中，`p` 通常是未知的，而且通常不随 `x` 变化。在观察性（非随机）研究中，`p` 的真实值通常是未知的。此外，只要存在患者差异，`p` 必须随 `x` 变化。

### A.2 估计倾向评分的实际问题

方程 `(A.2)` 表达的结果实际上非常深刻，且只需要相对弱的假设即可有效。遗憾的是，在观察性研究中，给定 `x` 向量的倾向评分 `p` 是未知，且 `p` 的估计可能足够糟糕（不现实），以至于基于舍入的倾向评分估计值的未治疗受治疗患者实际上可能具有不同的 `x` 向量分布。任何此类患者可能属于不同的条件区块，而不是同一个区块内。

图 `A.1` 展示了当使用逻辑回归估计倾向评分且 `x` 向量空间为三维时，这种情况是如何发生的。该模型使用形式为 `β*` 的线性函数（向量内积）来估计治疗倾向的 logit 变换 `[log(p(1-p))]`。两个不同的患者具有相同的舍入倾向评分估计值，当且仅当它们对应的 `x` 向量严格位于或位于一对平行的二维（在图 `A.1` 中描绘为薄板）上，且该平面正于三维 `β̂` 向量（在图 `A.1` 中所示）。

注意，对 `p` 的固定值取条件定义了一个患者区块。为了避免产生过多的区块，可以将 `p` 保留两位或三位小数。对于给定的、舍入后的 `p` 值，`x` 的分布可能相当复杂，但至少（由于独立性）该分布在每个区块（由单个舍入的 `p` 值定义）内的受治疗和未治疗患者之间是相同的。另一方面，`x` 在区块之间变化的特性（即随着 `p` 的变化而变化）为将这些倾向子群体称为“区块”提供了充分的动机和理由。

同样，方程 `(A.2)` 第四行的第二个因子 `Pr(t | p)` 定义了局部比例上的治疗平衡（或不平衡）。具体而言，在 `p=0.50` 的区块内，受治疗患者与未治疗患者的局部（块内）比例预计非常接近 1:1。

## 188 使用 SAS 对观察性健康数据进行分析

考虑以下启发性论证：方程 `(A.4)` 第一行中的 `Pr(x | t, C)` 因子渐近地由第二行中的 `Pr(x | C)` 因子表示。首先，在方法中，观测到的治疗用于最优匹配（Rosenbaum, 2003）或全匹配（Hansen, 2004），这些方法专门设计用于以防止产生具有信息性的聚类（informative clusters）。假设一个潜在聚类仅包含（例如）受治疗患者，全匹配将扭曲并扩展聚类，直到其包含至少一个未受治疗患者（`t`，聚类主要基于 `x` 向量，但受 `t` 的半监督限制）。另一方面，当聚类不依赖于 `t` 分配时，当聚类 `C` 不同时，`Pr(x | t, C)` 和 `Pr(x | C)` 仍然可能存在很大差异。

例如，大聚类中 `x` 向量的分布可能非常不均匀，所有受治疗患者与未治疗患者之间的巨大分离纯属偶然发生。较大的聚类可能包含真实概率 `p = Pr(t=1 | x)` 值范围广泛的患者。如果在这种情况下 `Pr(x | t, C)` 和 `Pr(x | C)` 相等，聚类身份将是一个比真实 `p` 更粗糙的 B/B 分，这是不可能的。

在另一个极端情况下，所有聚类仅包含一个患者，`C = x` 且 `Pr(x | t, x) = Pr(x | x)` 是具有单位 `x` 的密度分布。因此，最小的聚类是精确的 B/B 分。

那么，聚类身份是否是近似的 B/B 分呢？当聚类较小、紧凑且密集时，具有相同舍入倾向分患者可能位于不同的聚类中。对于所有实际用途，这意味着聚类身份已成为比 `p` 个体 `x` 向量更精细的近似 B/B 分。此外，只要 `Pr(t=1|x)` 倾向于是 `x` 的光滑函数且聚类具有较小的 `x` 空间体积，这种情况就可能发生。同时，当聚类没有被扭曲以防止产生具有信息性的聚类时，给定 `t` 和 `C` 的 `x` 条件分布对 `t` 分配的依赖性也较低。当这一切发生时，人们无疑不需要确认分层（具有信息性的聚类内组间的 `x` 分布平衡）；它们的局部 B/B 特性将已得到保证。这一概念在图 `A.2` 中所示。

首先，注意图 `A.2` 中描述的三维立方体代表相对较小、紧凑且密集的聚类。所示聚类恰好相交于来自治疗选择的逻辑回归模型拟合舍入倾向分估计薄层。现在假设白色立方体包含具有信息性的聚类，而每个深色立方体包含至少一个受治疗患者。如果舍入倾向分估计满足方程 `(A.2)`，那么所有这些聚类将需要具有几乎相同的聚类内治疗比例，命名为 `p`。幸运的是，在使用聚类来定义 B/B 分时没有这种限制；聚类内治疗比例仅是观测到的局部比例。此外，由于每个聚类都很小且紧凑，受治疗和未治疗患者的局部 `x` 分布必然非常相似，所得 B/B 分必须比倾向分精细。

## 第 7 章使用 JMP 189 的局部控制方法

**图 A.2** 小小、紧凑且密集的聚类的 `x` 空间几何结构，这些聚类与逻辑回归舍入倾向分估计层相交

## 不需要无监督 PS 估计！

![](img/fe9ff008f88baacd415148b0b25dd58c_203_0.png)

交叉任意 PS 层的 3D 聚类

# References

- Angrist, J. D., G. W. Imens, D. B. Rubin, J. M. Robins, et al. 1996. “使用工具变量识别因果效应.” *Journal of the American Statistical Association* 91: 444–472.
- Bang, H., and J. M. Robins. 2005. “缺失数据和因果推理模型中的双稳健估计。” *Biometrics* 61(4): 962–973.
- Barlow, B. H. 1989. “无监督学习.” *Neural Computation* 1(3): 295–311.
- Board on Life Sciences. 2003. *Sharing Publication-Related Data and Materials: Responsibilities of Authorship in the Life Sciences*. Washington, DC: The National Academies Press. Available at http://www.nap.edu/books/103908853/html.
- Box, G. E. 1997. “稳健性是科学模型构建的策略.” Robustness in Statistics: *Proceedings of a Workshop*, 202, Edited by R. L. Launer and G. N. Wilkinson. New York: Academic Press.
- Cochran, W. G. 1965. “人类种观察性研究的计划（含讨论）,” *Journal of the Royal Statistical Society: A (Statistics in Society)* 128: 234–266.
- Cochran, W. G. 1968. “观察性研究中的分类调整.” *Biometrics* 24: 295–313.
- Concato, J. N., and Shah, I. 2000. “随机对照试验的因果推理.” *The New England Journal of Medicine* 342:1887–1892.
- DAgostino, Jr., R. B., and Rubin, D. 1998. “具有缺失数据的倾向分估计.” *Journal of the American Statistical Association* 95: 749–759.
- DAgostino, Jr., R. B., and Lang, M. 2001. “观测到的局部比例.” *Health Services and Outcomes Research* 17:603–610.
- Diaconis, P., and Walkup, T. 2007. “使用倾向分估计因果效应.” *American Heart Journal* 104:603–610.
- Efron, B. 1979. “有限样本抽样的推广.” *Journal of the American Statistical Association* 47: 663–685.
- Efron, B., and Holmes, R. 1993. “计算机辅助的.” *The Statistician* 56: 308–311.
- Fisher, R. 1925. “统计学基础.”
- Flarey, C., and A. 2002. “观察性研究中的设计.” *Statistics in Medicine* 21: 1571.
- Hansen, B. 2004. “全匹配.” *Journal of the American Statistical Association* 99: 609–618.
- Holland, P., and D. G. 1986. “观察性研究中的因果推理.” *Journal of the American Statistical Association* 81: 945–960.
- Horvitz, D., and Thompson, S. 1952. “无放回抽样的推广.” *Journal of the Royal Statistical Society* 15: 218–229.
- Imbins, G. W., and Andrist, J. D. 1994. “因果效应的识别和估计.” *Econometrica* 62: 467–475.
- Ioannidis, J. P. A. 2005. “为什么大多数发表的研究结果是错误的?” *PLoS Medicine* 2(8): e124.
- Ioannidis, J. P. A. 2005. “高引引研究中的矛盾效应.” *Journal of the Medical Association* 294:218–229.
- Kaufman, L., and Rousseuw, P. J. 1990. *Finding Groups in Data: An Introduction to Cluster Analysis*. New York: John Wiley & Sons
- Kent, D. M., and Harvey, R. A. 2007. “将临床试验结果应用于个体：风险分层的需求.” *Journal of the American Medical Association* 298:1209–1212.
- Kent, D. M., and Harvey, R. A. 2007. “平均值掩了临床试验中的差异.” *American Scientist* 95(1): 60–68.
- Keereakes, D. J., et al. 2000. “Abcinimab在高容量互动实践中提供了具有成本效益的生存优势.” *American Heart Journal* 104(4): 603–610.
- Leamer, E. E. 1978. *Specification Searches: Ad Hoc Inference with Nonexperimental Data*. New York: John Wiley & Sons
- Mccellan, B. J., and McNill, J. P. 1994. “老年人心肌梗死的更严密治疗能降低死亡率吗？使用工具变量.” *Journal of the American Medical Association* 272:859–866.

McEntegart, D.J. 2003. “使用分层和动态随机化技术的平衡追求：概述。” Drug Information Journal, 37: 293–308.

Müller, H. Matthews, and D. G. Altman. 2002. “关于调整混杂的统计方法的报告：一项横断面调查。” [简短通讯] Annals of Internal Medicine, 136(2):122–126.

Newhouse, J. P., and M. McClellan. 1998. “结果研究中的计量经济学：工具变量的使用。” Annual Review of Public Health, 19: 17–34.

Obchenbein, L. R. 2004. “无监督倾向评分：NN 和 IV 图。” 于 ASA 联合统计会议论文集。Alexandria, VA: American Statistical Association, 1899–1906.（注：原文中的页码可能有笔误，但根据指令保留：Obchenbein）

Obchenbein, L. R. 2005. “USPS：用于无监督和有监督倾向评分及工具变量调整的 R 包。” 来自 http://www.r-project.org.

Obchenbein, L. R. 2006. “通过聚类识别有意义的亚组——敏感性图形。” ASA 联合统计会议论文集。Alexandria, VA: American Statistical Association.

Obchenbein, L. R. 2009. 用于局部控制和 LTD 分布的 JMP 脚本。来自 http://memqueries.inet/net/sofrxr/other/LC_at.td.

Obchenbein, L., and C. A. Melfi. 1999. “数据库研究中治疗选择的倾向评分和 Heckman 调整。” ASA 生物医药部门论文集。Alexandria, VA: American Statistical Association, 297–306.

Pock, S. J., S. E. Assmann, L. Enos, and L. Kranken. 2002. “临床试验报告中的亚组分析、协变量调整和基线比较：当前实践与问题。” Statistics in Medicine, 21: 2917–2930.

Cao, R. T. 2013. 《线性统计推断及其应用》。第 2 版。New York: John Wiley & Sons, Inc.

Robins, J. M., A. H. Herman, and B. Bumback. 2000. “流行病学中的结构因果模型和因果推理。” Epidemiology, 11: 550–560.

Rausbaum, P. R. 2002. *观察性研究》。第 2 版。New York: Springer-Verlag.

Rausbaum, P. R., and D. B. Rubin. 1993. “倾向评分在因果效应观察性研究中的核心作用。” Biometrika, 70: 41–55.

Rausbaum, P. R., and D. B. Rubin, 1994. “使用倾向评分亚分类法减少观察性研究中的偏倚。” Journal of the American Statistical Association, 79: 516–524.

Rubin, D. B. 1997. “使用马哈拉诺距离匹配技术减少偏倚。” Biometrics, 36: 293–298.

Rubin, D. B. 1997. “利用倾向评分从大数据中估计因果效应。” Annals of Internal Medicine, 127: 757–763.

Salsburg, D. 2012. 《统计故事：统计学如何在20世纪发生革命》。New York: Owl Books.

Shah, B. R., A. Laoupikis, J. E. Hux, and P. C. Austin. 2005. “倾向评分法在观察性研究中的结果与回归模型相似：一项系统综述。” Journal of Clinical Epidemiology, 58(6): 550–559.

Stürmer, T. M., Joshi, R. J. Glynn, Y. Avorn, K. J. Rothman, and S. Schneeweiss. 2006. “倾向评分方法的应用综述显示使用量增加，在特定设定下具有优势，但与传统多变量方法相比估计值无显著差异。” Journal of Clinical Epidemiology, 59(5): 437.e1–437.e24.

Wainer, H., M. Gassaroli, and M. Verdi. 2006. “通过不幸的结果分箱发现不存在的内容：孟德尔效应。” Chance, 19: 49–52.

Wegman, E. J., and Q. Luo. 2002. “用于密度可视化的计算机图形方法研究。” Journal of Computational and Graphical Statistics, 11: 137–162.

Yue, L. Q. 2007. “倾向评分分析应用于非随机医疗器械临床研究的统计和监管问题。” Journal of Biopharmaceutical Statistics, 17: 1–13.

# 第三部分

# 纵向偏倚调整

- **第 8 章** 用于观察性数据分析的两阶段纵向倾向评分调整 ................................................ 195
- **第 9 章** 使用边际结构模型对纵向观察性数据进行分析 ....................................................211
- **第 10 章** 结构嵌套模型 ................................................................231
- **第 11 章** 基于纵向倾向评分的回归模型 ................................................................263

# 第 8 章：用于观察性数据分析的两阶段纵向倾向评分调整

## 摘要

描述了一种用于有效性分析的两阶段纵向倾向调整。在本章中，我们研究了观察性数据的治疗倾向和有效性分析。

## 8.1 引言

观察性数据中的治疗评估面临若干挑战。首先，与随机试验不同，其治疗不是标准化的，而是由医生决定的。其次，倾向评分可能与结局相关。例如，接受治疗的人群。第三，选择偏倚通常由非随机变量产生。

Rosenbaum 和 Rubin (1983) 将倾向评分定义为给定观测协变量向量 (`x`) 时分配到治疗的条件概率：

$$e(x) = P(T=1 \mid x)$$

适用于受者 `i = 1, \dots, N`。倾向评分用于减少研究中的混杂偏倚。

## 8.2 治疗倾向的纵向模型

提出了一种实施纵向数据倾向的策略。它是倾向评分的动态调整（Leon et al., 2001, 2003）。为了简单起见，我们仅考虑二分类治疗的纵向倾向。这是一种两阶段纵向数据分析策略，包含倾向模型和有效性模型。在第一阶段，倾向模型检查随时间变化的二分类治疗观察。该模型可以包含每个受者随时间变化的多个治疗间隔。在第二阶段，治疗有效性模型检查从每次治疗开始到预设事件发生的时间。

混合效应框架考虑了代表受者内部连续治疗间隔的相关复发时间。混合效应逻辑回归模型将治疗视为这些特征（时间不变或随时间变化）的函数：

$$e(x_{ij}, v_i) = P(T_{ij} = 1 \mid v_i, x_{ij})$$

适用于受者 `i (i = 1, \dots, N)` 在时间 `j (j = 1, \dots, J)`，其中 `v_i` 是受者特有的随机截距。假设该混合效应逻辑模型，受者 `i` 在时间 `j` 的倾向评分（范围 0 到 1）可以使用逻辑响应函数表示为：

$$e(x_{ij}, v_i) = \frac{\exp(\alpha + x_{ij}\beta + v_i)}{1 + \exp(\alpha + x_{ij}\beta + v_i)}$$

倾向评分低的受者在时间点 `j` 不太可能接受治疗，而高倾向评分的受者则具有更有可能接受治疗的特征。

# 第 8 章 用于观察数据分析的两阶段纵向倾向性调整

## 8.3 纵向倾向性调整后的治疗效果分析

倾向性调整通过分层在治疗效果分析中实施。这是基于一个假设：在倾向性评分分层内，治疗分配是可忽略的（我们将其分为五位数）。换句话说，在一个五位数内，未接受治疗的受试者不会影响倾向评分中包含的协变量 (`x`)。接下来，我们将讨论一种检查组间达到何种平衡程度的方法。根据可忽略性假设，可以在基于随机截距的情况下，得出关于治疗直接效应的因果推理。

### 8.3.1 倾向性五位数分类

根据倾向评分的分布，时间 `j` 时每个受试者 `i` 被归入五位数之一，`q_{ij} \dots q_{ij}`。倾向评分 `e(x_{ij}, u_i)` 包含了随时间变化的和不变化的变量。每个受试者的倾向评分随时间变化，因此在纵向研究中，受试者的倾向性也可能发生变化。进行五位数分类是为了能够对每个五位数分别进行治疗效果分析。其原理是这种方法将消除倾向评分中包含的每个变量的大部分混杂效应。然而，为了进行特定五位数的分析，必须检查每个治疗组在五位数中的代表性。如果某种治疗在某个五位数中没有良好的代表，显然无法对该五位数进行治疗效果分析。通过检查倾向五位数列联表中的单元格来评估五位数代表性。

### 8.3.2 纵向治疗效果分析

使用生存分析方法检查治疗效果，其中疾病复发的时间是因变量。在本章使用的示例中，生存测量是在时间间隔内确定的，检查事件自上一次随访访问以来发生的时间。因此，使用了分组时间生存分析法。此外，为了通过随访收集所有数据（这通常涉及每个受试者的多次观测值，例如多次复发），使用了混合效应分组时间生存分析模型。该模型检查受试者 `i` 的第 `j` 次观测直到并包括时间间隔 `j` 的复发概率，公式如下：
```



$P_{ij} = Pr(t_i \le j)$

使用互补对数对数链接函数，该模型是一个比例风险回归模型，将复发的累积概率描述为治疗的函数：

$P_{ij} = 1-\exp(\alpha + x_{ij}'\beta + v_{ij})$

其中，$\alpha$ 代表截距项（即基准风险），$x_{ij}$ 是代表治疗组的指示变量，$v_{ij}$ 代表随机受试者效应。需要注意的是，边缘结构模型（我们在此处未考虑）提供了一种评估随时间变化的治疗的替代方法，其中反向概率加权试图产生组间协变量的平衡。（见第 9 章。）

### 8.3.3 效果分析分层

如前所述，治疗效果分析是针对每个倾向性五位数分别进行的。这基于 Cochran (1968) 的观点，他证明了对混杂变量进行五位数分层可以消除与该变量相关的大部分偏倚。将特定五位数的治疗效果估计值进行合并汇总，以获得一个统一的治疗效应估计值。

### 8.3.4 合并特定五位数的效果结果

使用 Fleiss (1981) 描述的 Mantel-Haenszel (1959) 程序对特定五位数的结果进行合并。使用这种策略，每个特定五位数的参数估计根据其标准误的倒数进行加权，合并估计值通过加权平均计算。该策略假设不存在治疗与倾向性的交互作用（即治疗效应在不同五位数之间没有差异）。我们在对合并数据集的分析中评估这一假设，该数据集包含五个五位数的所有观测值。通过似然比检验比较两个混合效应模型：

- 1. 治疗和五位数的的主效应（带有指示变量）
- 治疗和五位数的的主效应及其交互作用

显著的交互作用将表明治疗效应在不同倾向性五位数之间存在差异。在这种情况下，不指示合并特定五位数的的结果。相反，必须在特定五位数水平上报告治疗效果结论。相比之下，如果没有倾向性交互作用，假设检验的重点是合并治疗效应：$H_0: \beta=0$。

## 8.4 应用

本应用检查了国家精神健康联合抑郁症研究的数据。该研究招募了 1978-1981 年间患情感障碍的受试者，他们在美国五个医疗中心（波士顿、芝加哥、爱荷华市、纽约和圣路易斯）寻求一种主要情感障碍的治疗。每个受试者都提供了知情同意。这项纵向观察研究的设计和目标已在其他地方描述（Katz and Kleman, 1979）。受试在前五年接受每半年一次的评估，并在后长达 23 年内接受每年评估。我们检查了根据研究诊断标准 (RDC) (Spitzer et al., 1978) 定义的单极性大抑郁症康复者的抗抑郁治疗预防复发的效果。此处报告的分析所使用的数据包括最多 20 年的随访评估。

### 8.4.1 数据分析程序

分析如前所述分两个阶段进行。最初，治疗倾向性模型检查了假设与接受治疗相关的人口统计和临床变量的关联幅度。例如，治疗是二元因变量。（一个治疗强度变量，如 Keller, 1988 和 Leon et al., 2003 所示，被二分类化，强度 0 与强度 2、3 的合并值进行比较。强度水平 1 被排除。）由于许多受试者在治疗时间内有多次观测，使用了混合效应逻辑回归模型。模型中包含了受试者特定的随机截距，以解释受试者内部的观测值聚集。

第二阶段涉及混合效应分组时间抗抑郁效果生存模型，检查从治疗开始到情感障碍复发的时间。生存变量（复发时间）代表在康复期间治疗状态（是/否）保持不变的连续周数。生存间隔可以以以下方式之一终止：

- 1. 情感障碍复发
- 2. 治疗状态改变
- 3. 随访结束

后两种被归为删失。在这些分析中，假设由于随访结束导致的删失与复发时间无关。受试者积累生存间隔（此处称为治疗间隔），每次新发和每次治疗状态的变化都会产生一个间隔。治疗间隔是倾向模型和效果模型的分析单位。因此，数据包含每个受试者的多次观测，每个治疗间隔一次观测。这些间隔代表了每个受试者接受的不同治疗方案，包括不治疗。对每个治疗间隔分别计算了倾向评分。

### 8.4.2 受试者

四百三十名受试者在研究入组时患有重度抑郁症（Keller et al., 1992）。其中有 82 名因为患了双极情感而被排除，另有 46 名没有从入组发作中康复，因此也被排除。在其他符合这些分析标准的受试者中，有 19 名缺少计算倾向评分所需的协变量数据而被排除。因此，此处描述的分析包含 284 名受试者的 1,319 次观测。

## 8.4.22 治疗倾向

倾向性模型包含五个变量：症状严重程度（精神状态评分，PSR，过去 8 周的症状轨迹，范围从 0-6；变量名 `meanspr` 表示增加 vs. 减少，对比 `symdec` 和 `syncc`）、教育程度（`colgrad`、`somecol` 和 `highsch`）、年龄（`age30`、`age60`、`age40`、`age50` 和 `age60`）以及地点（`site1`、`site3`、`site4` 和 `site5`）（参见程序 8.1）。模型中的三个发现被重点强调。（参见程序 8.1 的输出）。症状较严重的受试接受治疗的可能性显著更高（优势比 `OR`: 1.99；95% 置信区间 `[CI]`: 1.70–2.34）。治疗前 8 周症状严重程度下降的受试接受治疗的可能性略低（`OR`: 0.70；95% `CI`: 0.49–1.02）。来自三个研究地点（纽约、爱荷华和芝加哥）的受试者接受治疗的可能性高于其他地点的受试者。在多个治疗间隔期间，受试者是否接受治疗随时间具有中等一致性（类内系数=0.305）。

## 程序 8 使用混合效应逻辑回归计算倾向评分

```
TITLE1 'Performing Mixed-effects Logistic Regression of Propensity Model';

/* Propensity Analysis for Binary tx */

/* Binary LOGISTIC RANDOM-INTERCEPT MODEL */

Data datal;

set "c:\uniint.sas_tbdat";

PROC MIXED;

PARMS b0=0 b1=0 b2=0 b3=0 b4=0 b5=0 b6=0 b7=0 b8=0 b10=0 b11=0

b12=0 b13=0 b14=0 sd=1;

z = b0 + b1*meanspr + b2*colgrad + b3*somecol + b4*highsch + b5*sitel

b6*site3 + b7*sited + b8*site5 + b9*age30 + b10*age4049 +

b11*age50t9 + b12*symdec + b13*syncc + sd*u;

IF (tx=0) THEN

p = 1 / (1 + EXP(-z));

ELSE IF (tx=1) THEN

p = 1 / (1 + EXP(-z));

like = LOG(p);

MODEL tx ~ GENERAL(like);

RANDOM u ~ NORMAL(0,1) SUBJECT=id;

PREDICT z=out;

ESTIMATE 'ICC' sd*sd((((ATAN(1)**2)/3)+sd*sd);

RUN;
```

## 第 8 章 用于观察数据分析的两阶段纵向倾向性调整

## 程序 8.1 的输出

**NLMIXED 过程**

| | |
|---|---|
| 使用的观测值 | 1319 |
| 未使用的观测值 | 0 |
| 总观测值 | 1319 |
| 受试者 | 284 |
| 每个受试者最大观测数 | 27 |
| 参数 | 16 |
| 二次点 | 5 |

注意：满足 GCONV 收敛标准。

## 拟合统计量

| | | | | | | | | |
|---|---|---|---|---|---|---|---|
| -2 对数似然 | 1537.3 | | | | | | | |
| AIC (越小越好) | 1569.3 | | | | | | | |
| AICC (越小越好) | 1569.8 | | | | | | | |
| BIC (越小越好) | 1627.7 | | | | | | | |

## 参数估计

| 参数 | 估计值 误差 DF t 值 Pr >|t| Alpha | 下限 | 上限 | 梯度 |
|---|---|---|---|---|---|---|---|---|
| b0 | -3.5115 | 0.4758 | 283 | -7.38 | <.0001 | 0.05 | -4.4841 | -2.5749 | 0.0036 |
| b1 | 0.6889 | 0.4058 | 283 | 8.54 | <.0001 | 0.05 | 0.5309 | 0.8487 | 0.0080 |
| b2 | -0.1628 | 0.3320 | 283 | -0.49 | 0.6241 | 0.05 | -0.8162 | 0.4906 | 0.0037 |
| b3 | 0.4327 | 0.3510 | 283 | 2.84 | 0.0048 | 0.05 | -1.1962 | 1.0645 | 0.0010 |
| b4 | 1.3591 | 0.4779 | 283 | 2.85 | 0.0048 | 0.05 | -0.3123 | 2.2997 | 0.0114 |
| b5 | 0.4026 | 0.3673 | 283 | 1.10 | 0.2739 | 0.05 | -0.3803 | -1.2155 | 0.0018 |
| b6 | 1.1222 | 0.3770 | 283 | 2.98 | 0.0030 | 0.05 | 0.3802 | 1.8642 | 0.0047 |
| b7 | -0.5762 | 0.4245 | 283 | -1.37 | 0.0194 | 0.05 | -1.0504 | -0.0803 | 0.0030 |
| b8 | 0.3810 | 0.2979 | 283 | 1.82 | 0.0705 | 0.05 | -0.0326 | 0.7946 | 0.0236 |
| b9 | 1.2013 | 0.3856 | 283 | 0.68 | 0.4945 | 0.05 | -0.3827 | 0.7900 | 0.0022 |
| b10 | 0.5608 | 0.3100 | 283 | 1.81 | 0.0715 | 0.05 | -0.0490 | 1.1710 | 0.0024 |
| b11 | -0.3508 | 0.1889 | 283 | -1.86 | 0.0644 | 0.05 | -0.7226 | 0.0210 | 0.0033 |
| b12 | 0.3399 | 0.2110 | 283 | 1.58 | 0.1148 | 0.05 | -0.0815 | 0.7493 | 0.0154 |
| sd | 1.2023 | 0.1390 | 283 | 8.65 | <.0001 | 0.05 | 0.9287 | 1.4759 | 0.0168 |

## 额外估计

| 标签 | 估计值 误差 标准 DF t 值 Pr >|t| Alpha | 下限 | 上限 |
|---|---|---|---|---|---|---|---|
| ICC | 0.3053 | 0.0493 | 283 | 6.23 | <.0001 | 0.05 | 0.2088 | 0.4018 |

倾向性模型的结果（参见程序 8.1 的输出）用于计算每个观测值的倾向评分。注意，时间变协变量（如症状严重程度和轨迹）包含在倾向评分中，倾向评分是项目级的。每个观测值被归类为倾向五位数中的某一个。（参见程序 8.2。）显示了一个列联表以评估每个五位数治疗的代表性。（参见程序 8.2 的输出）。显然，低五位数的受试者接受治疗的可能性较低，而高五位数的受试者接受治疗的可能性较高。这为模型的有效性提供了支持。重要的是，每个治疗组在每个五位数中都有代表，因此可以使用五位数特定治疗分析来比较这些组。

## 程序 8.2 五位数分层

```
/* 根据上述估计值生成 QUINTILE 值 (0 到 4) */

DATA data2 id event meenplan graycole highsset site

site3 site6 agent7 age40t49 age50t59 symdec surv2

;MERGE lest;

/* 转换为概率尺度 */

ppred = 1 / (1 + EXP(-ppred));

prepred;

PROC RANK GROUP=5 OUT=rankout;

VAR pprred;

RANKS QUINT;

DATA all; SET rankout;

q1=0;q2=0;q3=0;q4=0;

if quint 1 then q1 = 1;

if quint 2 then q2 = 1;

if quint 3 then q3 = 1;

if quint 4 then q4 = 1;

/* 按五位数分组表 */

PROC FREQ;

TABLES tx*QUINT;

RUN;
```

## 程序 8.2 的输出

FREQ 过程
按五位数分组表
tx(Treated 是/否) QUINT(Rank for ppred)

| | 0 | 1 | 2 | 3 | 4 | 总计 |
|---|---|---|---|---|---|
| 频数 | | | | | | |
| 百比 | | | | | | |
| 行百分比 | | | | | | |
| 0 | 244 | 224 | 169 | 104 | 24 | 768 |
| | 18.73 | 16.98 | 12.81 | 7.88 | | 58.23 |
| | 32.16 | 29.17 | 20.01 | 13.54 | | 31.13 |
| | 93.92 | 84.85 | 64.02 | 39.39 | | 9.09 |
| 1 | 40 | 95 | 160 | 240 | | 551 |
| | 3.03 | 7.20 | 12.13 | 18.20 | 43.56 | 41.77 |
| | 2.90 | 7.26 | 17.24 | 29.04 | | | |
| | 15.15 | 35.98 | 60.61 | 90.91 | | | |
| 总计 | 263 | 264 | 264 | 264 | | 1319 |
| | 19.94 | 20.02 | 20.02 | 20.02 | | 100.00 |

## 8.4.3 治疗效果分析

最初，使用似然比检验评估治疗与倾向的交互作用，比较主效应拟合情况（-2 对数似然 = -323.7；参见程序 8.5 的输出）与主效应及交互模型拟合情况（-2 对数似然 = -319.3；参见程序 8.6）。该交互作用在统计上并不显著（χ²=6.60, df=4, p=.17）。因此，之前介绍了五位数特定治疗分析。合并结果显示，当受试者接受抗抑郁治疗时，复发风险比不接受治疗时低 35%（`OR` = 0.65；95% `CI`: 0.50–0.85；参见程序 8.4 的输出），控制了倾向性。

## 程序 8.3 五位数特定治疗效果

```
/* 组时间生存分析 - 五位数特定分析 */

/* 带有截数据的二二互补对数对数 随机截距模型 */

PROC STEST; BY QUINTILE;

PROC MIXED;

pB0=0+b1=sd+ t1=1 t2=1.25 t4=1.5 t5=1.75 t6=2 t7=2.25;

OUTPUT ParameterEstimates=estb;

z = b0 + b1*tx + sd;

IF (event = 1) THEN

DO;

IF (surv=1) THEN

p p = 1 - EXP(0) - EXP(z));

IF (surv=2) THEN

p p = 1 - EXP(0) - EXP(t2+z)) (1 - EXP(0) - EXP(0+z));

IF (surv=3) THEN

p p = 1 - EXP(0) - EXP(t3+z)) (1 - EXP(0) - EXP(t2+z));

IF (surv=4) THEN

p p = 1 - EXP(0) - EXP(t4+z)) (1 - EXP(0) - EXP(t3+z));

IF (surv=5) THEN

p p = 1 - EXP(0) - EXP(t5+z)) (1 - EXP(0) - EXP(t4+z));

IF (surv=6) THEN

p p = 1 - EXP(0) - EXP(t6+z)) (1 - EXP(0) - EXP(t5+z));

IF (surv=7) THEN

p p = 1 - EXP(0) - EXP(t7+z)) (1 - EXP(0) - EXP(t6+z));

END;

IF (event = 0) THEN

DO;

IF (surv=1) THEN

p p = 1 - (EXP(0) - EXP(0+z));

IF (surv=2) THEN

p p = 1 - (EXP(0) - EXP(t2+z));

IF (surv=3) THEN

p p = 1 - (EXP(0) - EXP(t3+z));

IF (surv=4) THEN

p p = 1 - (EXP(0) - EXP(t4+z));

IF (surv=5) THEN

p p = 1 - (EXP(0) - EXP(t5+z));

IF (surv=6) THEN

p p = 1 - (EXP(0) - EXP(t6+z));

IF (surv=7) THEN

p p = 1 - (EXP(0) - EXP(t7+z));

END;

END;

END;
```

## 204 使用 SAS 分析操作性保健数据

```sas
like = LOG(p);

MODEL surv ~ GENERAL(like);

RANDOM u ~ NORMAL(0,1) SUBJECT=id;

ESTIMATE 'ICC' sd*sd/(((ATAN(1) **2)/6)+sd*sd);

BY QUINT;

RUN;
```

## 程序 8.4 合并各分位数特定的治疗效性结果

```sas
/ 根据上述分位数特定模型的结果生成合并后的估计 (poolest) /

DATA estw; SET estb;
```



`w = 1 / StandardError**2;`

`west = Estimate*w;`

```sas
PROC MEANS NOPRINT; CLASS Parameter; VAR west;

OUTPUT out=sums sum=sumest;

DATA poolest; set sums; IF _TYPE_EQ 1;

poolest = sumest / sum;

poolse = 1 / sqrt(sum);

poolz = poolest / poolse;

poolp = 2*(1) - probnorm(abs(poolz));
```

```sas
/ 打印 poolest 结果 /

PROC PRINT;

VAR Parameter poolse poolz poolp;

RUN;
```

## 程序 8.4 的输出

| Obs | Parameter | poolest | poolse | poolz | poolp |
|---|---|---|---|---|---|
| 1 | b0 | -3.84229 | 0.23478 | -16.3566 | 0.00000 |
| 2 | b1 | -0.42659 | 0.13324 | -3.2016 | 0.00137 |
| 3 | sd | 0.11333 | 0.13715 | 1.4166 | 0.15974 |
| 4 | t2 | 0.50464 | 0.16553 | 3.6795 | 0.00023 |
| 5 | t3 | 0.89581 | 0.19464 | 5.4118 | 0.00000 |
| 6 | t4 | 1.60004 | 0.22543 | 8.2204 | 0.00000 |
| 7 | t5 | 2.44533 | 0.21645 | 11.6682 | 0.00000 |
| 8 | t6 | 2.86478 | 0.23911 | 13.2354 | 0.00000 |
| 9 | t7 | 4.10759 | 0.17118 | 17.0884 | 0.00000 |

## 程序 8.5 跨所有受试者的治疗效性分析：主效应

```sas
/ 分组时间生存分析 -- 所有受试者 -- 所有分位数主效应 /

/* 带有截断的二值协变量随机截距模型 */

PROC MIXED;

PARMS b0=0 b1=0 b2=0 b3=0 b4=0 b5=0 sd=1

t2=1 t3=1.25 t4=1.5 t5=1.5 t6=2 t7=2.5

z=0+b1*btx+ b2*q1+ b3*q2+ b4*q3+ b5*q4 + sd*u;

..更多 SAS 语句..
```

```sas
like = LOG(p);

MODEL surv ~ GENERAL(like);

RANDOM u ~ NORMAL(0,1) SUBJECT=id;

ESTIMATE 'ICC' sd*sd/(((ATAN(1) **2)/6)+sd*sd);

RUN;
```

## 第8章 用于观察性数据分析的两阶段纵向倾向调整 205

## 程序 8.5 的输出

NOTE: GCON 收敛标准已满足。

| 拟合统计 | |
|---|---|
| -2 Log Likelihood | 3203.7 |
| AIC (越小越好) | 3229.7 |
| AICC (越小越好) | 3230.0 |
| BIC (越小越好) | 3277.2 |

## 程序 8.6 跨所有受试者的治疗效性合并：主效应和交互作用

```sas
* 分组时间生存分析 - 所有受试者 - 所有分位数主效应和交互作用 */

/* 带有截断的二值复杂对数对数随机截距模型 */

PROC NLMIXED;

PARMS b0=0 b1=0 b2=0 b3=0 b4=0 b5=0 b6=0 b7=0 b8=0 b9=0 sd=1

t2=-1 t3=1.25 t4=-1.5 t5=1.75 t6=2 t7=-2.25;

z = b0+b1*tx+b2*q1+b3*q2+b4*q3+b5*q4

b6+tx*q1+b7*tx*q2+b8*tx*q3+b9*tx*q4 + sd*u;

like = LOG(p);

MODEL surv ~ GENERAL(like);

RANDOM u ~ NORMAL(0,1) SUBJECT=id;

ESTIMATE 'ICC' sd*sd/(((ATAN(1) **2)/6)+sd*sd);
```

程序 8.6 的输出

NOTE: GCON 收敛标准已满足。

| 拟合统计 | |
|---|---|
| -2 Log Likelihood | 3197.3 |
| AIC (越小越好) | 3231.3 |
| AICC (越小越好) | 3237.7 |
| BIC (越小越好) | 3293.3 |

跨所有受试者的治疗效性合并：主效应和交互作用

带有截断的二值复杂对数对数随机截距模型

NOTE: GCON 收敛标准已满足。

| -2 Log Likelihood | 3197.3 |
| AIC (越小越好) | 3231.3 |
| AICC (越小越好) | 3237.7 |
| BIC (越小越好) | 3293.3 |

跨所有受试者的治疗效性合并：主效应和交互作用

带有截断的二值复杂对数对数随机截距模型

由于提供的原始文本中存在部分重复和格式错乱，译文已根据逻辑进行了清理和对齐，以确保内容通顺。

# 致谢

国家心理健康研究所合作抑郁症研究由以下研究人员目前参与：M.B. Keller, M.D.（主席，普罗维登斯）；W. Coryell（共同主席，爱荷华市）；D.A. Solomon, M.D.（普罗维登斯）；W.A. Schenfler, M.D.（芝加哥）；W. Coryell, M.D.（爱荷华市）；J. Endicot, P.D., A.C. Leon, P.D., J. Long, M.S.W.（纽约）；以及 J. Rice, P.D.（圣路易斯）。其他贡献者包括：H.S. Akiskal, M.D.;J. Fawcett, M.D.;L.J. Jung, P.D.;P.W. Lavori, P.D.;J.D. Maser; T.I. Mueller, M.D.。本手稿已通过合作抑郁症研究出版委员会审查，并获得其认可。本手稿的数据来自国家心理健康研究所（NIMH）抑郁症心理学协作计划——临床研究（Katz and Kramer, 1979）。该计划于1975年启动，旨在调查情绪障碍的社会、遗传、家族和预后方面，是一项关于情绪及相关情感障碍病程的持续、长期的多学科调查。最初的首席专家和首席研究员来自五个学术中心，包括 Gerald Kramer, M.D.（共同主席），Martin Keller, M.D. 和 Robert Shapiro, M.D.（马萨诸塞州总医院，哈佛医学院）；Eli Robins, M.D.;Paul Clayton, M.D.;Theodore Reed 和 Amos Weller, M.D.（华盛顿大学医学院）；Nancy Andreasen, M.D., P.D., 以及 William Coryell, M.D.以及 George Winokur, M.D.（爱荷华大学）；以及 Jan Fawcett, M.D. 和 William Sheftner, M.D.（拉什-普斯比得-圣路加医学中心）。NIMH临床研究分支是协作计划起源和发展的活跃合作者，其中部门主任 Martin M. Katz, P.D. 担任共同主席，Robert Hirschfeld, M.D. 担任计划协调。其他贡献者包括：Crough, M.D.;M.T. Shea, P.D.;R. Gibbons, P.D.;M.A. Young, P.D.以及 D.C. Clark, P.D.。

本研究部分由 NIH 资助项目 MH60447 和 MH49762 支持。

# 参考文献

- Cochran, W. G. 1968. "The effectiveness of adjustment by subclassification in removing bias in observational studies." Biometrics 24: 295–313.
- Drake, C. 1993. "Effects of misspec of the propensity score on estimators of the treatment effect." Biometrics 49: 1231–1236.
- Fleiss, J. L. 1981. *Statistical Methods for Rates and Proportions.* New York: John Wiley & Sons. Hedeker, D., O. Siddigki, and F. B. Hu. 2000. "Random-effects regression analysis of correlated grouped-time survival data." *Statistical Methods in Medical Research* 9: 161–179.
- Katz, M. M., and G. L. Kramer. 1979. "Introduction: overview of the clinical studies program." *The American Journal of Psychiatry* 136(1): 49–51.
- Keller, M. B. 1988. "Undertreatment of depression." *Psychopharmacology Bulletin* 24(1): 75–80.
- Keller, M. B., P. W. Lavori, T. I. Mueller, J. Endicot, W. Coryell, R M. Hirschfeld, T. Shea. 1992. "To recovery, chóng, and levels of psychopathology in depression: A five-year prospective follow-up of 43 subjects." *Archives of General Psychiatry* 49(10):809–816.
- Leon, A. C., and D. Hedeker. 2005. "A mixed-effects quantile-stratified propensity adjustment for effectiveness of.

## 使用 SAS 对观察性健康数据进行分析

意向性治疗分析 (ITT) 最后观察结转法 (LOCF) 或重复测量可能并不适用。

ITT 分析仅根据患者的治疗分配对患者进行分组，并忽略所有关于其他处方或服用的药物的信息。此类研究中，患者的脱落通常通过利用 LOCF 方法来处理。显然，当治疗方案之间存在大量切换时，这种技术并不能直接解决治疗效果的问题。ITT 分析在纵向观察性研究中具有其地位，例如比较政策或治疗策略的研究，在这些研究中，人们主要感兴趣的单个药物的效果（Tunis et al., 2006）。

虽然在治疗中利用重复测量可能提供一种简单的解决方案，但 Hernán 及其同事（2004, 2005）解释说，在存在时间依赖性混杂因素（结果的预测因子和随后的治疗）且这些因素受到先前治疗的影响的情况下，这种方法无法提供具有因果解释的估计（见下文）。例如，任何疾病严重程度的纵向测量可能存在问题，因为它与结果指标相关，可以预测随后的治疗，并可能受到先前治疗的影响。即使治疗在研究基线时是随机的，随时间变化的因果治疗结果最终会导致关键患者特征的失衡。为了处理治疗切换，药物切换忽略了在纵向分析中证明非常有用的标准重复测量（Verbek and Molenbergh, 2000; Mallinckhardt et al., 2003）。这种方法将切换后的数据视为缺失，但显然没有利用药物切换后获得的信息。

在本章中，我们考察边际结构模型 (MSMs) 在纵向观察性数据中的应用。为了解释 MSM 方法的潜在优势，我们必须简要回顾反事实结果和因果效应的概念。我们将遵循 Hernán 及其同事（2002）提供的符号表示。令 `$a$` 表示患者在一段时间内的治疗历史（例如，`$a = \{a(1), a(2), ...,a(t)\}$`，其中 `a(1)` 表示在时间 1 使用的治疗）。患者 `i` 在治疗序列 `a` 下的反事实结果是指如果该患者（尽管可能与事实相反）接受了 `Y_{i,a}(t)`，那么其结果。

每个患者对于其未接受的每种治疗或观察到的结果都有一个反事实结果。在个体层面，如果对于某些时间点 `t` 和治疗模式 `a` 与 `a'`，`Y_{i,a}(t) != Y_{i,a'}(t)`，则认为该治疗对患者的结果具有因果效应。也就是说，治疗模式根据所接受的治疗而不同。在群体层面，如果所有患者遵循特定治疗模式（例如 `a`）的平均结果与所有患者遵循另一种治疗模式（例如 `a'`）的平均结果不同（即对于某些时间点和治疗方案，`E[Y_a(t)] != E[Y_{a'}(t)]`），则认为该治疗具有因果效应。

Robbins 及其同事（1999）证明，在本文讨论的一系列假设下，MSMs 在存在治疗变化、时间依赖性混杂因素和随机缺失脱落的情况下，能够产生对平均因果治疗效应的一致性估计。在本章中，我们首先描述 MSM 方法（第 9.2 节），然后对一项纵向精神分裂症研究进行 MSM 分析（第 9.3 节）。文中提供了 SAS 代码，并讨论了 SAS 输出，以便读者理解分析的实现并修改代码以供自己使用。Faire 及其同事（2007）还使用多种方法（包括 MSM）总结了该研究的数据。文献中 MSM 的其他应用包括 Hernán 及其同事（2000, 2002）、Ko 和同事（2003）、Brumback 及其同事（2004）以及 Cole 及其同事（2005），他们检查了 HIV 患者的事件时间结果；Bodnar 及其同事（2004）、Yamaguchi 和 Ohashi（2004a 和 2004b）、Mortimer 及其同事（2005）、Suarez 及其同事（2006）、Peterson 及其同事（2007）以及 Vansteeland 及其同事（2009），他们评估了其他应用。

## 9.2 MSM 方法论

MSM 分析是一种加权重复测量方法——将治疗作为随变化的协变量。基于逆概率治疗加权控制了时间依赖性混杂因素，并本质上建立了一个在时间不变量和随变化协变量上达到平衡的伪群体，允许使用标准的重复测量模型进行因果比较。权重也可以调整以包含对缺失数据的更新——在随机缺失（MAR；缺失数据可能依赖于已观测但未观测的指标）和完全随机缺失（MCAR；缺失数据不依赖于已观测或未观测的指标）下有效。

进行 MSM 分析是一个两的过程。首先，为每个观测值（患者就诊）估计两个权重：一个用于治疗选择，另一个用于调整中断。这些估计权重的完成可以包含时间独立和时间依赖的因素。Hernán（2002）建议使用稳定权重（stabilized weight），我们使用稿中的符号（此处用于治疗选择）：

```
$SW = \prod_{k=0}^{t} \frac{f[A(k-1),V]}{f[A(k)|A(k-1),L(k)]}$
```



# 第9章 使用边际结构模型进行纵向观察数据分析

其中 `$A(k)$` 代表时间 $k$ 的治疗，$A(1)$ 代表在时间 1 使用的治疗。患者 $i$ 在治疗序列 $a$ 下的反事实结果是指如果该患者（尽管可能与事实相反）接受了 $Y_{i,a}(t)$，那么其结果。

每个患者对于其未接受的每种治疗或观察到的结果都有一个反事实结果。在个体层面，如果对于某些时间点 $t$ 和治疗模式 $a$ 与 $a'$，$Y_{i,a}(t) \neq Y_{i,a'}(t)$，则认为该治疗对患者的结果具有因果效应。也就是说，治疗模式根据所接受的治疗而不同。在群体层面，如果所有患者遵循特定治疗模式（例如 $a$）的平均结果与所有患者遵循另一种治疗模式（例如 $a'$）的平均结果不同（即对于某些时间点和治疗方案，$E[Y_a(t)] \neq E[Y_{a'}(t)]$），则认为该治疗具有因果效应。

Robbins 及其同事（1999）证明，在本文讨论的一系列假设下，MSMs 在存在治疗变化、时间依赖性混杂因素和随机缺失脱落的情况下，能够产生对平均因果治疗效应的一致性估计。在本章中，我们首先描述 MSM 方法（第 9.2 节），然后对一项纵向精神分裂症研究进行 MSM 分析（第 9.3 节）。文中提供了 SAS 代码，并讨论了 SAS 输出，以便读者理解分析的实现并修改代码以供自己使用。Faire 及其同事（2007）还使用多种方法（包括 MSM）总结了该研究的数据。文献中 MSM 的其他应用包括 Hernán 及其同事（2000, 2002）、Ko 和同事（2003）、Brumback 及其同事（2004）以及 Cole 及其同事（2005），他们检查了 HIV 患者的事件时间结果；Bodnar 及其同事（2004）、Yamaguchi 和 Ohashi（2004a 和 2004b）、Mortimer 及其同事（2005）、Suarez 及其同事（2006）、Peterson 及其同事（2007）以及 Vansteeland 及其同事（2009），他们评估了其他应用。

## 9.3 示例：模拟精神分裂症试验的 MSM 分析

### 9.3.1 研究描述

为了说明 MSM 分析的实现，使用了基于一项精神分裂症患者药物有效研究的模拟数据。随后是实际研究设计的简要描述，尽管读者可以参考 Tunis 和同事（2006）获取详细信息。这是一项针对精神分裂症、情感情感障碍或精神分裂样障碍患者的一期研究，他们被随机分配到三种

## 216 使用 SAS 分析观察性健康数据

### 表 9.1（续）

| 变量 | 描述 | 变量 | 描述 |
|---|---|---|---|
| `TRTA` | 访视期间处于 Tr A | | |
| `TRTB` | 访视期间处于 Tr B | | |
| `TRTC` | 访视期间处于 Tr C | | |
| `TRT` | 权重计算期间的治疗 | | |

### 9.3.2.2 推断权重的计算

进行 MSM 分析的第一步是估计选择权重和删失权重 `SW`（使用 9.2 节中的公式）。对于估计治疗选择权重，使用 `PROC LOGISTIC` 配合 `LINK=GLOG` 选项对分子和分母实现了多项模型（见程序 9.1）。治疗是两个模型的因变量，并使用 GLOGIT 链接，是因为每次访视的治疗选择有五个潜在结果（三种个体治疗、无治疗和一种联合治疗）。`LOGISTIC` 过程输出包含治疗选择的预测概率（数据集 `PREDTRT0` 和 `PREDTRT1`）。除了治疗外，此模型还包含了以下时间变化的协变量：

- BPRS 总分
- 全局功能评估 `GAF`
- 事件（是否存在至少一次中度或严重的不良事件）
- 住院

选择这些变量是为了涵盖症状严重程度、功能状态、耐受性和资源利用等领域。包含在模型中的与时间不相关变量包括年龄、性别、种族以及每个时间依赖变量的基线值。可以使用宏变量在代码开始处输入所有模型参数；但我们选择通过在 `LOGISTIC` 语句中直接显示模型来简化对过程的理解。此外，为了简化输出，抑制了权重模型的输出。然而，人们可以轻松移除限制，以更详细地评估权重模型。

使用 `PROC GENMOD` 通过逻辑回归计算删失的估计权重（见程序 9.1）。删失权重模型的因变量与治疗选择权重模型相同——由于数据结构的原因，删失是前瞻性的（患者是否返回进行随访访视？），这相对于治疗（上一个阶段分配了什么治疗方案？），因此时间变化的协变量偏移了一个访视。此处使用了 logit 链接函数，因为结果是二项的。在仅评估两个治疗组的研究中，`GENMOD` 方法可用于两种权重的计算。

多项回归和逻辑回归权重模型的部分输出位于程序 9.1 的输出中。先前的治疗是当前治疗最强的预测因子。所有时间变化的协变量都不是治疗变化的强预测因子——这表明数据中随时间变化的治疗选择偏差可能并不特别奇怪。与之前的治疗相比，较高的（时间变化的）症状严重程度被发现是删失的预测因子。症状较多的患者更有可能退出研究。

#### 程序 9.1 计算治疗选择权重和删失权重

* 此部分代码计算治疗选择权重删失权重。这通过 4 个步骤完成：
1) 多项模型计算治疗选择权重的分子；
2) 多项模型计算治疗选择权重的分母；
3) 二项模型计算删失调整权重的分子；
4) 二项模型计算删失调整权重的分母。

```sas
/ 治疗选择权重：分子计算
（仅使用基线协变量进行治疗的概率） /
PROC LOGISTIC DATA = INPSDS;
CLASS VIS THERAPY PRTRTA PRITRTB PR1TRTC GENDER ORIGIN2 BHOSP BEVNT
MODEL TR = VIS THERAPY PRTRTA PRITRTB PR1TRTC GENDER ORIGIN2 BHOSP
BEVNT AGERS BGAF BPRPS
/LINK=GLOG;
OUTPUT OUT=PRETRT0(WHERE=(TR_=LEVEL)) PRED=PRETRT0;
```

```sas
/ 治疗选择权重：分母计算
（使用基线协变量和时间依赖协变量进行治疗的概率） /
PROC LOGISTIC DATA = INPSDS;
CLASS VIS THERAPY PRTRTA PRITRTB PR1TRTC GENDER ORIGIN2 BHOSP BEVNT
PRIEVNT HOSP;
MODEL TR = VIS THERAPY PRTRTA PRITRTB PR1TRTC GENDER ORIGIN2 BHOSP
BEVNT AGERS BGAF BPRPS HOSP PRIBPRS GIFAGC
/LINK=GLOG;
OUTPUT OUT=PRETRT1(WHERE=(TR_=LEVEL)) PRED=PRETRT1;
```

```sas
/ 删失调整权重：分子计算
（仅使用基线协变量进行删失的概率） /
ODS LISTING EX OBSTATS;
PROC GENMOD DATA = INPSDS;
CLASS PATSC VIS THERAPY TRTA TRBT TRTC GENDER ORIGIN2 BHOSP BEVNT
EVNT HOSP;
MODEL CFLAG = VIS THERAPY TRTA TRBT TRTC GENDER ORIGIN2 BHOSP BEVNT
AGERS BGAF BPRPS
/DIST = BIN LINK = LOGIT TYPE3 OBSTATS;
REPEATED SUBJECT = EMSC / TYPE = EXCH;
ODS OUTPUT STATS = PRECENO(RENAME=(PRE=PRECENO));
ODS LISTING SELECT ALL;
```

```sas
/ 删失调整权重：分母计算
（使用基线协变量和时间依赖协变量进行删失的概率） /
ODS LISTING EXCLUDE OBSTATS;
PROC GENMOD DATA = INPSDS;
CLASS PATSC VIS THERAPY TRTA TRBT TRTC GENDER ORIGIN2 BHOSP BEVNT
EVNT HOSP;
MODEL CFLAG = VIS THERAPY TRTA TRBT TRTC GENDER ORIGIN2 BHOSP BEVNT
EVNT HOSP AGERS BGAF BPRPS
/DIST = BIN LINK = LOGIT TYPE3 OBSTATS;
REPEATED SUBJECT = PATSC / TYPE = EXCH;
ODS OUTPUT STATS = PRECENO(RENAME=(PRE=PRECENO));
ODS LISTING SELECT ALL;
```

## 使用 SAS 分析观察性数据

### 程序 9.1 权重分母模型输出：治疗权重

Type 3 分析

| 效应 | DF | 卡方 | Pr > ChiSq |
|---|---|---|---|
| VIS | 16 | 124.2473 | .0001 |
| THERAPY | 8 | 11.8349 | .1587 |
| PRTRTA | 4 | 229.7185 | .0001 |
| PRTRTB | 4 | 100.6526 | .0001 |
| PRTRTC | 4 | 269.8819 | .0001 |
| GENDER | 4 | 3.3971 | .4937 |
| ORIGIN2 | 8 | 10.4911 | .2322 |
| BOSP | 4 | 0.4611 | .9972 |
| BEVNT | 4 | 3.0900 | .5429 |
| AGEYRS | 4 | 1.4773 | .8359 |
| BGAF | 4 | 1.9736 | .7406 |
| BBPRS | 4 | 2.2390 | .6919 |
| PRIENT | 4 | 7.5905 | .1078 |
| PR1BSP | 4 | 4.6487 | .3253 |
| PR1BPRS | 4 | 2.5962 | .6275 |
| PR1GAFC | 4 | 2.5983 | .6271 |

### 权重分母模型：删失权重 GEE Type 3 分析

| 来源 | DF | 方 | Pr > ChiSq |
|---|---|---|---|
| VIS | 4 | 13.21 | .0103 |
| THERAPY | 2 | 9.04 | .0109 |
| TRTA | 2 | 3.95 | .0468 |
| TRTB | 2 | 3.74 | .0532 |
| TRTC | 1 | 0.39 | .5356 |
| GENDER | 2 | 0.15 | .6964 |
| ORIGIN2 | 2 | 0.99 | .6087 |
| BOSP | 1 | 0.88 | .3473 |
| BEVNT | 1 | 0.93 | .3338 |
| EVNT | 1 | 0.61 | .4338 |
| ROSS | 1 | 0.05 | .8163 |
| AGEYRS | 1 | 4.89 | .0220 |
| BGAF | 1 | 0.04 | .8431 |
| BPRS | 1 | 0.67 | .4115 |
| BBPRS | 1 | 12.21 | .0005 |
| GAFC | 1 | 0.32 | .5726 |

为了产生此分析中每个观测值（患者访视）的总体权重，根据 SAS 9.2 节（程序 9.2）中的公式，在 DATA 步骤中累积乘以选择和删失的概率权重。在 sas 代码中，SQL 过程从治疗选择和权重模型的四个输出集（`PREDTR0`、`PREDTR1`、`PREDCENS0` 和 `PREDCENS1`）收集数据并产生加权值。变量 `SWAT` 是 `SW` 的最终估计值。程序的输出以箱线图格式显示所有患者访视的最终权重分布。平均值接近 1（平均值=1.002，SD=0.1555），符合权重平均值的预期，且箱线图中没有明显的离群值。

#### 程序 9.2 合并程序 9.1 的输出

* 此部分代码执行必要的步骤，合并权重模型（程序 9.1）的输出，以便计算分析数据集中每个观测值的单个调整值（稳定权重）。随后是生成最终权重摘要的代码。

```sas
PROC SQL;
/* 治疗的概率比 */
CREATE TABLE PREDTTR
SELECT *, PREDTT0/PREDTT1 AS PREDTTR
FROM PREDTT1
NATURAL FULL JOIN
PREDTT0 (KEEP=PATSC VIS PREDTT0)
ORDER PATSC, VIS;
/* 删失的概率比 */
CREATE TABLE PREDCEN
SELECT *, PREDCEN0/PREDCEN1 AS PREDCEN
FROM (SELECT INPUT(PATSC, BEST.) AS PATSC, INPUT(VIS, BEST.) AS VIS,PREDCEN0 FROM PREDCEN0)
NATURAL FULL JOIN
(SELECT INPUT(PATSC, BEST.) AS PATSC, INPUT(VIS, BEST.) AS VIS,PREDCEN1 FROM PREDCEN1)
ORDER PATSC, VIS;
QUIT;
```

```sas
/*计算稳定权重 */
PROC SORT DATA=INPADS OUT=WEIGHTS;
BY PATSC VIS;
RUN;
```

```sas
DATA WEIGHTS;
MERGE WEIGHTS PREDTTR PREDCEN;
BY PATSC VIS;
VWT=PREDTTR*PREDCEN;
IF FIRST.PATSC THEN STABWT=VWT;
ELSE STABWT=VWT*;
RETAIN DUM;
DROP DUM;
DUM=STABWT;
RUN;
```

```sas
/*权重诊断图*/
DATA GRPH;
SET WEIGHTS;
IF VIS = 3 THEN MONTH = 0.5;
IF VIS = 4 THEN MONTH = 2;
IF VIS = 5 THEN MONTH = 5;
IF VIS = 6 THEN MONTH = 8;
IF VIS = 7 THEN MONTH = 12;
IF MONTH = 0.5 DELETE;
```
```sas
PROC SORT DATA = GRPH;
BY MONTH;
RUN;
```

# 220 使用 SAS 分析观察性数据

```sas
ODS RTF FILE="%SYFSUNC(PATHNAME (WORK)) \FIG1.RTF";
FILENAME FIGURE="%SYFSUNC(PATHNAME (WORK)) \SASGRAPH.EMF";
OPTIONS RESET=ALL TARGET=ASEMF DEVICE=ASEMF FTEXT=DUPLEX HEXT=.75
CBACK=WHITE MAX=6IN PIXELS=120 YMAX=5IN PIXELS=1000
GSNAME=FIGURE GSFMODE=REPLACE;
SYMBOL1 COLOR=BLACK INTERPOL=JOIN
WIDTH=2 VALUE=SQUARE
HEIGHT=1;
AXIS1 MINOR = NONE COLOR = BLACK LABEL=("稳定后体重") ANGLE=90
ROTATE=0;
PROC BOXPLOT DATA=GRPH;
PLOT STWAB*MONTH / CFRAME=WHITE
CBOXES=DAG
CBFILL=WHITE
VAXIS=AXIS1;
TITLE "访视权重体重值摘要";
TITLE2 "箱线图：最小值、第一四分位数、中位数、第三四分位数、最大值；
方块：均值)";
RUN;
GOPTIONS RESET=ALL;
ODS RTF CLOSE;
```

# 程序 9.2 的输出

![](img/fe9ff008f88baacd415148b0b25dd58c_234_0.png)

# 第 9 章 使用边际结构模型分析纵向观察性数据 221

### 9.3.2.3 治疗效应分析模型

MSM 分析的最后一步是使用广义估计方程（`PROC GENMOD`——见程序 9.3）和可交换相关矩阵的加权重复测量模型来估计因果治疗效应。基线 BPRS 总分是分析模型中的因变量。分析模型中的自变量为研究中心、年龄、性别、种族、基线 BPRS、访视、随时间治疗以及治疗与访视的交互。`PROC GENMOD` 中的 `WEIGHT` 语句结合了概率加权以估计因果治疗效应。`PROC GENMOD` 中使用的 `ESTIMATE` 语句将个体治疗合并，并生成了不同组的估计均值（而非复合个体组）。这部分代码在许多应用中并非必要。程序 9.3 的输出显示了最终模型结果的摘要，以及一个显示最小二均值的图，图中显示治疗组（合并后的治疗 A 和 B）相对于对照组具有统计学上的显著差异，在 1 年后 BPRS 变化的平均差异为 .1 [0.4, 3.2]，p=.015。尽管差异在数值上有所增加，但治疗与访视的交互在统计学上并不显著（p=.158）。

#### 程序 9.3 运行最终分析模型



```
/* 此代码使用加权重复测量方法运行最终分析模型。结果使用 PROC GPLOT 以图形形式展示.*/
/*最终分析模型*/
PROC GENMOD DATA = WEIGHTS;
CLASS PATISC GENDER ORIGIN2 INSC TRIS;
WEIGHT STABWT;
MODEL CAVAR = INVAS BVAR VIS AGERS GENDER ORIGIN2 TRIS VISTRT
/ DIST=NONNORMAL LINK=ID TYPE3;
REPEATED SUBJECT = PATSC / TYPE=EXCH;
LMEANS TRIS*TRT / PDIFF;
ESTIMATE 'A*B VS C';
TRT 0 .5 -1 0;
ESTIMATE 'A*B VS C AT VIS 3'
TRT 0 .5 -1 0;
VIS*TRT 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0;
ESTIMATE 'A*B VS C AT VIS 4'
TRT 0 .5 -1 0;
VIS*TRT 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 .5 -1 0;
ESTIMATE 'A*B VS C AT VIS 5'
TRT 0 .5 -1 0;
VIS*TRT 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 .50 0;
ESTIMATE 'A*B VS C AT VIS 6'
TRT 0 .5 -1 0;
VIS*TRT 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 
;
 'A*B VS C VS VIS 7'
'T 0 5 -1 0;
VIS*TRT 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 .5 -1 0;;
ODS OUTPUT LMEANS=LMEANS;
RUN;
```

# 222 使用 SAS 分析观察性健康数据

```
/*最终模型的 LS MEANS2 图绘制*/
DATA LSMEANS;
SET LSMEANS;
WHERE TRIN IN ('A ', 'B');
IF TRIN IN ('A ', 'B') THEN TR2='A+B';
ELSE TR2='C';
RUN;

PROC SQL;
CREATE TABLE LSMEANS AS
SELECT TR2, VIS, MEAN(ESTIMATE) AS ESTIMATE
FROM LSMEANS
GROUP BY TR2, VIS;
QUIT;

ODS RTF FILE="%SYFSUNC(PATHNAME (WORK)) \FIG2.RTF";

FILENAME FIGURE="%SYFSUNC(PATHNAME (WORK)) \SASGRAPH.EMF";

OPTIONS RESET=ALL TARGET=ASEMF DEVICE=ASEMF FTEXT=DUPLEX HEXT=.75
CBACK=WHITE MAX=6IN PIXELS=120 YMAX=5IN PIXELS=1000
GSNAME=FIGURE GSFMODE=REPLACE;

AXIS1 MINOR = NONE COLOR = BLACK LABEL=(ANGLE=90 ROTATE=0 "BPRS 总变化");
SYMBOL I=JOIN W=2 C=SQUARE;
SYMBOL II=JOIN W=2 C=CIRCLE;

PROC DATA=LSMEANS;
PLOT ESTIMATE*VIS=TRT / VAXIS=AXIS1;
TITLE "基线估计均值";
LABEL VIS="访视";
LABEL TRT="治疗";
RUN;
ODS RTF CLOSE;
```

# 第 9 章 使用边际结构模型分析纵观察数据 223

程序 9.3 的输出

| 源 | DF | 卡方 | Pr > ChiSq |
|---|---|---|---|
| INSVC | 19 | 84.25 | <0001 |
| BAVAR | 1 | 71.12 | <0001 |
| VIS | 4 | 37.69 | <0001 |
| AGEYRS | 1 | 0.80 | .3735 |
| GENDER | 1 | 0.09 | .7624 |
| ORIGIN2 | 2 | 0.86 | .6500 |
| TRT | 4 | 11.70 | .0197 |
| VIS*TRT | 16 | 21.57 | .1576 |
| 对比估计 结果 | | 标准误 | Alpha | 置信限 | 卡方 | Pr > ChiSq |
|---|---|---|---|---|---|---|
| A+B VS C | -1.7852 | 0.7321 | 0.05 | -3.2201 | -0.3504 | 5.95 | .0147 |
| A+B VS C AT VIS 3 | -0.7336 | 0.9615 | 0.05 | -2.6181 | 1.1509 | 0.58 | .4455 |
| A+B VS C AT VIS 4 | -1.1225 | 0.9417 | 0.05 | -2.9682 | 0.7232 | 1.42 | .2333 |
| A+B VS C AT VIS 5 | -1.7746 | 1.2532 | 0.05 | -4.2307 | 0.6815 | 2.01 | .1567 |
| A+B VS C AT VIS 6 | -2.1785 | 1.2752 | 0.05 | -4.6778 | 0.3208 | 2.92 | .0876 |
| A+B VS C AT VIS 7 | -3.1169 | 1.3185 | 0.05 | -5.7012 | -0.5327 | 5.59 | .0181 |

![](img/fe9ff008f88baacd415148b0b25dd58c_237_0.png)

# 224 使用 SAS 分析观察性健康数据

## 9.3.2.4 敏感性分析

为了评估发现的稳健性，应当评估因果关系三个假设的合理性（无未测量混杂、阳性、正确模型），并实施基于不同假设的其他统计方法。关于未测量混杂，已努力收集并整合专家和文献的信息，以考虑分析的潜在混杂因素。模型中包含的变量涵盖了症状严重程度、功能、耐受性和资源负担领域。为了评估未测量混杂对结果的潜在影响，我们实现了简单的测量混杂函数（使用基于 Barnett 等人 2004 的常数 alpha）。使用该函数，如果缺失的混杂因素导致 BPRS 量表上发生 0.45（BPRS 总分）的偏移，且有利于处于治疗组患者的潜在结果，将导致统计学上的显著发现。换句话说，我们对显著差异的发现取决于不存在此类混杂因素（或具有相同效应的一组混杂因素）的假设。使用 SAS 代码中的 `ALPHA=c` 常数评估了多个常数（见程序 9）。保留 0.45 的值是因为它是产生约 0.05 p 值的最小值。虽然解释特定 alpha 的含义具有挑战性，但这种影响（BPRS 上的 <1）看起来并不极端。然而，它大于本研究中观察到的相反方向混杂（未加权与加权分析之间的差异）（在未加权与加权分析之间）0.29。无论敏感性分析如何，结果并不意味着可能未未的因素会导致此类分析无法产生因果治疗效应的估计。通过更改提供的 SAS 代码中的变量 `CAVAR_SENS` 和 `SAPT`，可以轻松测试不同的敏感性函数。

* 此部分代码通过寻找消除观察到的治疗差异的混杂水平，检查结果对未测量混杂的敏感性。*

## 第 9 章 使用边际结构模型分析纵向运营数据 225

```
ESTIMATE 'A+B VS C'
TRT 0 .5 .5 -1 0
ESTIMATE 'A+B VS C AT VIS 3'
TRT 0 .5 .5 -1 0
VIS*TRT 0 .5 .5 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0;
ESTIMATE 'A+B VS C AT VIS 4'
TRT 0 .5 .5 -1 0
VIS*TRT 0 .5 .5 -1 0 0 .5 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0;
ESTIMATE 'A+B VS C AT VIS 5'
TRT 0 .5 .5 -1 0
VIS*TRT 0 .5 .5 -1 0 0 .5 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0;
ESTIMATE 'A+B VS C AT VIS 6'
TRT 0 .5 .5 -1 0
VIS*TRT 0 .5 .5 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0;
ESTIMATE 'A+B VS C AT VIS 7'
TRT 0 .5 .5 -1 0
VIS*TRT 0 .5 .5 -1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 .5 -1 0;
RUN;
```

MSM 敏感性分析：`ALPHA = 0.45`

## 对比估计结果

| | 标准估计误差 置信区间 | 卡方 | Pr > ChiSq |
|---|---|---|---|---|---|---|
| A+B VS C | -1.3991 | 0.7303 | 0.05 | -2.8224 | 0.0402 | 3.63 | 0.0568 |
| A+B VS C AT VIS 3 | -0.0620 | 0.9615 | 0.05 | -2.5048 | 1.2642 | 0.42 | 0.5188 |
| A+B VS C AT VIS 4 | -0.8879 | 0.9417 | 0.05 | -2.7335 | 0.9577 | 0.89 | 0.3457 |
| A+B VS C AT VIS 5 | -1.3184 | 1.2534 | 0.05 | -3.7750 | 1.1383 | 1.11 | 0.2922 |
| A+B VS C AT VIS 6 | -1.6479 | 1.2726 | 0.05 | -4.1422 | 0.8464 | 1.68 | 0.1954 |
| A+B VS C AT VIS 7 | -2.4810 | 1.3135 | 0.05 | -5.0569 | 0.9950 | 3.56 | 0.0991 |

为了评估这种可能性，我们根据 Mortner 等人 (2005) 在所有随访中所有可能的协变量，对五种治疗中的每种进行了选择。这里使用的 `CATMOD` 模型用于为所有可能的治疗方案生成预测概率。虽然本研究在概率假设上没有问题（所有患者都有切换的机会，且可以是任何治疗组合），但目标是评估任何观测协变量集是否为这组数据产生了 0 或 1 的预测概率。这是通过 SAS 程序 9 完成的，我们计算了每个观测协变量集的预测概率，然后对预测概率进行了汇总（使用 `PROC MEANS` 进行汇总统计）。我们发现，最小的概率（非零 < 0.0015）出现在早期随访中从无治疗切换到 A 和 C 治疗组合的理论切换，正如根据其观测频率预期的那样。随后，在排除最极端记录的情况下进行了敏感性分析，并将组合治疗重新分配给初始单一治疗（例如，被随机分配到治疗 A 但接受 C 治疗的患者将仅接受治疗 A）。从这些敏感性分析中没有观察到推断发生重大变化，结果未显示。

## 226 使用 SAS 分析观察性健康数据

## 程序 9.5 检查因果推断的充分性假设

```
* 此部分代码通过检查所有可能的治疗变更的预测值，来检查因果推断的充分性假设。显示了汇总统计数据，并列出了列表以便检查离群值。*
```

```
*充分性检查 Mortimer (2005) - 生成预测概率*/
ODS LISTING CLOSE;
PROC CATMOD DATA = INDPS;
DIRECT AGEYRS BGAF BEYPRS PRBPRS PRIGAFC;
MODEL TRT = VIS THERAPY PRTRTA1 PRTRTC GENDER ORIGIN2 BHOSP
BEVNT AGEYRS BGAF BEYPRS PRWNT PRBPRS PRIGAFC
/PRED;
ODS OUTPUT PREDICTED=PREDTRT1 (KEE=VIS THERAPY PRTRTA
PRTRTC GENDER ORIGIN2 BHOSP BEVNT AGEYRS BGAF
BBPRS PRWNT PRBPRS PRIGAFC
RENAME=(PREDICTION-PREDTRT1));
RUN;
ODS LISTING;
ODS RTF FILESYSFUN(PATHNAME(WORK))SASGF.RTF";
FILENAME="%SYSFUN(PATHNAME(WORK))SASGF.EMF";
OPTIONS RESET=ALL TARGET=ASEMF DEVICE=ASEMF TEXT=DUPLEX HEXT=75 CBACK=WHITE XMAX=6 INXELS=1200 YMAX=5 INXELS=1000 GSFNAME=REPLACE;
PROC UNIVATE DATA = PREDTPOS
VAR PREDTRT1;
HISTOGRAM BLPLOT;
TITLE 'SUMMARY STATS ON PREDICTED VALUES';
RUN;
```

```
OPTIONS RESET=ALL;
ODS RTF CLOSE;
```

```
PROC MEANS DATA = PREDTPOS
CLASS TRT;
VAR PREDTRT1;
TITLE 'Positivity Check: Summary Stats on Predicted Values by Observed Treatment';
RUN;
```

```
PROC SORT DATA = PREDTPOS;
BY PREDTRT1;
RUN;
```



```
PROC PRINT DATA = PREDTPOS;
TITLE 'Positivity Check: Sorted Listing of Predicted';
* (PROC PRINT 输出未显示，但用于识别具有极端值的协变量组合患者 *)
```

## 第 9 章 使用边际结构模型分析纵向观察数据 227

## 程序 9.5 的输出

| 充分性检查：按观测治疗的预测值汇总统计 | MEANS Procedure |
| Analysis : PREDTRT Predicted: Probability |
| TRT | N Obs | N | Mean | Std Dev | Maximum |
| --- | --- | --- | --- | --- | --- |
| A_C | 2547 | 2547 | 0.047507 | 0.125480 | 0.975886 |
| A_ | 2547 | 2547 | 0.415872 | 0.416508 | 4.075123E-7 | 0.999982 |
| B_ | 2547 | 2547 | 0.250829 | 0.399958 | 1.8471036E-8 | 0.999993 |
| C_ | 2547 | 2547 | 0.238318 | 0.369699 | 3.408221E-7 | 0.999842 |
| | 2547 | 2547 | 0.047498 | 0.117316 | 0.981760 |

除了通过添加交互、、二次和其他潜在混杂因素对未测量混杂因素和假设进行评估外，未发现结果显著变化。模型评估是通过调整 SAS 代码中的模型完成的——可以通过将模型变量放在代码顶部来实现自动化。此外，我们还使用其他方法分析了数据：ITT LOC 分析（使用所有数据）、重复测量模型（排除切换后的数据）和时期分析（第 8 章）。使用简单的 ITT LOC 对这些模拟数据进行分析，治疗组和对照组之间没有显著差异（估计差异为 1.16，p=.334）。重复测量混合模型（放弃切换后的数据）和时期分析的结果与 MSM 方法相当。ITT 分析与其他分析之间的分歧似乎是忽略了治疗切换后数据的治疗信息，正如 Faires 等人 (2007) 所述。从 C 切换到 A 和 B 的患者表现良好，这些信息在 ITT 分析中未归于 A 和 B。

### 9.4 讨论

本章介绍了纵向观察数据中评估治疗效果的问题——重点是 MSM 处理治疗切换。我们关注 MSM 的性能是因为这种方法利用了所有的研究数据，并在存在治疗切换、缺失数据和时间变化混杂因素的情况下，提供治疗效果的一致估计。MSM 分析的有效性取决于三个关键假设：

- 1. 无未测量混杂
- 2. 充分性（Positivity）
- 3. 正确的模型

此外，假设缺失数据遵循完全随机缺失 (`MCAR`) 或随机缺失 (`MAR`)。因此，计划良好的敏感性分析至关重要。这应该包括对 MSM 支持治疗效果的假设进行评估，以及使用由不同假设支持的其他方法。此外，结果的呈现

## 228 使用 SAS 分析观察性健康数据

应当向读者明确说明，结果的因果解释建立在不可验证的假设之上，并且对评估结果稳健性所采取的步骤保持透明。

总而言之，边际结构模型是估计纵向观察数据中因果效应的一种很有前景的方法。本书的其他章节提供了详细信息。

# 参考文献

- Mallinckrock, C. H., T. M. Sanger, S. Dubois, D. J. DeBrota, G. Molenbergberg, R. J. Carroll, W. Z. Potter, and G. D. Tollenson. 2003. "Assessing and interpreting treatment effects in longitudinal clinical trials with missing data." *Biological Psychiatry* 53(8): 754–760.
- Mortimer, K. M., R. Neugebauer, M. van der Laan, and I. B. Tager. 2005. "An application of model-fitting procedures for marginal structural models." *American Journal of Epidemiology* 162(4): 382–388. Epub 2005 Jul 13.

# 第9章 使用边际结构模型进行纵向观察数据分析 229

Petersen, M. L., S. G. Deeks, N. Martin, M. J. van der Laan. 2007. “用于估计时变效应修饰的历史调整结构模型。”美国流行病学杂志 166: 985–993.

Robins, J. M., A. Rotnitzky, and D. O. Scharfstein. 1999. 流行病学中的统计模型：环境与临床试验。M.E. Halloran 和 D. Berry 编. IMA Volume 116. New York: Springer-Verlag, 1–92.

Robins, J. M., A. Hernán, and B. Brumback. 2000. “流行病学中的边际结构模型和因果推断。”流行病学 11: 550–560.

Rosenenbaum, P. R. 2005. “观察性研究。” 载于行为科学统计学百科书 3: 1451–1462. B. S. Everit 和 D. C. Howell 编. Chichester: John Wiley & Sons, Ltd.

Rosenbaum, P., and D. B. Rubin. 1983. “倾向评分在因果效应观察性研究中的核心作用。” 生物学杂志 2008. 70: 41–55.

Suarez, D., J. M. Haro, D. Novick, S. Ochoa, B. J. Kinon, H. Ascher-Svanum, and R. Aquila. 2006. “奥奥西平作为分裂症一线治疗药物的成本效益：一项随机、开放标签、期1年试验的结果。”健康价值 9(2): 77–89.

Vansteeland, S., K. Mertens, C. Suetsens, E. Gotghehauber. 2009. “用于部分暴露方案的边际结构模型。”生物统计学 10(1): 46–59.

Verbeke, G., and G. Molenbergs. 2000. 纵向数据线性混合模型. New York: Springer-Verlag.

Yamaguchi, T., and Y. Ohashi. 2004a. “在癌症临床试验中对二线治疗比例差异进行调整。第一部分：用于测试和估计治疗组效应的结构嵌套模型和边际结构模型。”医学统计 23: 1991–2003.

Yamaguchi, T., and Y. Ohashi. 2004b. “在癌症临床试验中对二线治疗比例差异进行调整。第二部分：在不可切除非小细胞肺癌临床试验中的应用。”医学统计 23: 2005–2022.

# 第10章

## 结构嵌套模型

Daniel Almirall
Cynthia J. Coffman
Will S. Yancy, Jr.
Susan A. Murphy

- 摘要 ........................................................................................................................ 231
- 10.1 引言 ............................................................................................................ 232
- 10.2 时变因果效应修饰 ................................................................ 234
- 10.3 估计 ............................................................................................................ 236
- 10.4 实证示例：使用 SAS `PROC NLP` 进行极大似然数据分析 ................................................................................ 239
- 10.5 讨论 ............................................................................................................ 251
- 附录 10.A ................................................................................................................ 253
- 附录 10.B ................................................................................................................ 256
- 附录 10.C ................................................................................................................ 259
- 参考文献 ................................................................................................................. 260

## 摘要

本章回顾了 用于 用于随时间变化的预测因子效应的结构嵌套均模型（SNMM）。SNMM 用于在存在作为这些效应修饰符的时变协变量的情况下，研究时变预测因子（或治疗措施）的影响。我们描述了使用 `PROC NLP` 实现的 SNMM 参数极大似然（ML）估计器的 SAS 实现方法。所提出的极大似然估计器要求在给定时变修饰因子和预测因子历史的情况下，对主要结局的分布进行正确的模型规范，包括对 SNMM 的因果和非因果部分的正确规范。该估计器还依赖于对给定过去的情况下假设的时变修饰因子的观测数据分布的正确规范。我们使用来自减重研究的数据说明了该方法论和 SAS 实现。在实证示例中，我们评估了早期与晚期减重（或增加）对研究结束时健康相关生活质量的影响，这种影响是先前的减重以及被认为是这些效应修饰符的时变协变量的函数。

## 10.1 引言

纵向试验现在在临床研究中已随处可见。随着健康结局数据库的增加以及对医疗记录获取途径的改进，这种现象产生了大量随时间重复的变量，这种丰富的纵向数据反过来允许研究人员审查疾病病因或其他医疗干预产生积极效应的更多、更详细的科学问题。由于纵向数据的可用，这些问题通常涉及时变预测因子（或治疗措施）——这类研究通常是观察性研究。

我们在本章中使用的方法关注于涉及概念化和估计时变效应修饰的特定类型问题（Petersen 等人，2007；Almirall 等人，2009）。为了说明我们所指的时变效应，在研究过程中多个时间点 `j=0, 1, …` 可获得体重（`Z`）和一个二分类时变协变量（`X`）。我们定义时间点之间的体重变化 `D_j = Z_j - Z_{j-1}`（`j=1, …`）。假设我们的结局是研究结束时的健康相关生活质量测量（`QOL`）。利用这些数据，在每个时间点 `j`，我们感兴趣体重减轻或增加（`D`）对 `Y` 的影响如何随 `D_j` 变化，或如何随 `(X_0, X_1, …, X_j)` 变化。因此，通过时变协变量效应修饰，我们感兴趣的是时变协变量运动如何修饰体重预测或体重增加对研究结束时生活质量的效应。

在我们的动机示例中，识别和理解体重变化对健康相关生活质量效应的时变修饰符是非常重要的，因为它增强了我们对体重减轻（或增加）导致（或降低）健康相关生活质量的因果途径的理解。这一过程也帮助我们更好地理解结局（HRQOL）、时变修饰符（例如运动）与不变化但可能同时修饰结局和时变修饰符的因素之间的关系。这些因素的例子包括患者特征（例如人口统计、医学诊断）和减重干预类型（例如饮食组成、减肥药物、手术）或结构（例如频率、小组会议）。这些特定知识可用于阐述关于体重减轻、健康相关生活质量以及体重和 HRQOL 时变修饰符之间关系的假设或产生新想法。这些额外知识反过来可能帮助临床医生根据对患者行为和/或饮食遵循性的现有知识预测体重减轻的积极健康效果。它也可以作为行为科学家开发未来减重或体重管理干预的指南。

# 第 10 章 结构嵌套模型

在回归模型中，效应（或调节效应）通常与预测变量与感兴趣的协变量（或潜在的调节变量）之间的交互项相关。例如，在点预测器设置中，预测变量 `D`（体重变化）和协变量 `X` 不随时间变化，则可以使用以下回归模型来研究效应：

```
E(Y | X, D) = \gamma_0 + \gamma_1X + \gamma_2D + \gamma_{3}DX
```

在该模型中，交叉乘积项量化 `D` 对 `Y` 的影响随 `X` 水平而变化的程度。体重变化增加一个单位对应于研究结束时健康相关质量的 `\gamma_1 + \gamma_3X` 个单位的变化，这种变化取决于 `X`（运动，是/否）的水平。在该模型中，`\gamma_3=0` 是不存在来自 `X`（或运动）调节作用的证据。

遗憾的是，这种建模策略可能无法很容易转换到随时间变化的设置。考虑 `T=2` 的时间变化扩展模型：

```
E(Y | X_0, X_1, D_1) = \gamma_0 + \gamma_1X_0 + \gamma_2D_0 + \gamma_3D_1X_0 + \gamma_4D_1 + \gamma_5D_0X_1 + \gamma_6D_1X_1 \quad(2)
```



在该模型中，$X_0$ 是基线（$j=0$）之前的运动水平，$X_1$ 是 $j=0$ 到时间 $j=1$ 之间的运动水平；$D_0$ 是基线（$j=0$）到时间 $j=1$ 之间的体重变化；$D_1$ 是 $j=1$ 到 $j=2$ 之间的体重变化。即使 (2) 是 $Y$ ($X_0, X_1, D_0, D_1$) 条件期望（关联）的正确模型（即正确的函数），与 $D_0$ 和 $D_1$ 相关的参数、交叉乘积项并不一定代表体重变化 $D_0$ 在 $X_0$ 水平内对研究结束时质量 $Y$ 的条件因果效应。也就是说，函数 $\gamma_2 + \gamma_3X_0$ 可能可能代表体重变化（基线和 $j=1$ 之间）对研究结束时质量的真实因果效应。

将交叉乘积建模策略朴素地扩展到时间变化设置（如2 所示）的问题在于，并不清楚哪些因果效应（即在条件 (2) 中关于 $X_1$（时间 $j=0$ 到 $j=1$ 之间的运动水平）的 $D_0$ 和 $D_0X_0$ 的系数）可能会受到 $D_1$（时间 $j=0$ 到时间 $j=1$ 之间的体重减轻或增加）的影响（Robins, 1987, 1994, 1997, 1999; Bryan et al., 2006）。会导致两个不理想的后果。首先，朴素地对 $X_1$ 进行条件化会切断体重变化（$D_0$）通过 $X_0$ 传递的任何部分效应；即函数 $\gamma_2 + \gamma_3X_0$ 不包含由 Baron 和 Kennedy (1986); Kramer et al. (2001) 中介的效应（包括来自 $X_0$ 的调节效应）。其次，朴素地对 $X$ 进行条件化会由于 $X_0$ 和 $X_1$ 之间不存在处于因果路径上的非关联而导致系数 ($\gamma_2, \gamma_3$) 产生偏差。因此，科学家希望识别的随时间变化的 $X$ 作为随时间变化的 $D$ 对 $Y$ 的随时间变化的调节变量的作用（即使用标准回归）由于潜在的偏差是不适宜的。

Robins 结构嵌套均值模型 (1994) 通过明确指定给定过去（体重变化的历史和时间变化的调节变量）的 $Y$ 条件均值的因果和非因果部分克服了这些问题。SNMM 阐明了当感兴趣的预测变量和潜在调节变量都随时间变化时的效应调节机制。SNMM 为在线性回归中正确纳入潜在的时间变化调节变量提供了指南。

在 10.2 中，我们更正式地定义了在给定过去的结局条件均值因果模型背景（即使用 Robins 的 SNMM）中，时间变化效应调节的含义。在第 10.3 节中，我们描述了 SNMM 参数的最大似然 (ML) 估计器。在第 10.4 节中，我们利用体重减轻研究的数据演示了使用 SAS PROC NLP 实现 ML 估计器。在案例中，我们评估了早期与后期体重减轻对研究结束时活力（健康相关质量）随变化的协变量（运动、饮食依从性）的影响。

## 10.2 时间变化的因果调节

我们依赖结局来定义感兴趣的因果参数（Rubin, 1974; Holland, 1986, 1990）。如引言简述所示，我们考虑以下数据：

$$(X_0, X_1(d_1), d_2, \dots, X_{T-1}(d_1, d_2, \dots), d_T, Y(d_1, d_2, \dots)) \quad(3)$$

在该符号中，$j=(1, 2, \dots, T)$ 是主要时间变化预测变量（例如，时间变化协变量）在时间 $j$ 的索引。在我们的示例中，$d_j$ 是当前访问（时间 $j$）和之前访问（时间 $j-1$）之间的体重变化。此外，$d_j$ 表示第一次和第二次访问之间的体重减轻。我们使用小写的 $d_j$ 以区别于由大写的 $D_j$ 表示的观测预测变量（见第 10.3 节）。$X(d_1, d_2, \dots, d_j)$ 是一个向量，$x_j$ 可能包括基线类型、特征（如年龄、种族和性别）以及时间变化的协变量。我们不对时间变化的协变量类型施加限制；Y(d_1, d_2, \dots, d_j)$ 表示研究结束（即 $j$ 之后）的潜在结局，例如研究结束时的健康相关质量。在本章中，我们只考虑潜在结局。例如，$Y(d_1, d_2, \dots, d_T)$ 是我们在研究过程中减轻（或增加）体重的结局，作为增减（$d_1, \dots, d_T$）的函数；d_j, \dots, d_T$ 描述研究结束时的体重减轻或增加。

在该符号中，$X(d_1, d_2, \dots, d_j)$ 对于 $j=1, 2, \dots, T-1$ 也由 $d_j$ 索引，因为它们可能受到过去 $d_j$ 水平的影响。也就是说，它们被视为潜在结局。事实上，在我们的示例背景下，时间变化的协变量向量可能可能调节体重减轻对研究结束时质量的未来影响。

我们使用缩写来表示变量或索引的历史如下：

$$d_j = (d_1, d_2, \dots, d_j);$$
$$X(d_j) = (X_0, X_1(d_1), X_2(d_2), \dots, X_j(d_j));$$
$$Y(d_T) = Y(d_1, d_2, \dots, d_T).$$

在本章中，我们不考虑纵向结局；我们只考虑研究结束（$d_t$ 之后）衡量的结局。因此，我们不通过下标标记结局 $Y(d_t)$。可以扩展此处的方法来处理纵向结局（Robins, 1994）。

### 10.2.2 Robins 结构嵌套均值模型

在该小节中，我们在 Robins SNMM 的背景下定义了感兴趣的主要因果函数。一般来说，每个点有一个感兴趣的因果效应。为了简单起见，我们在 $T=2$ 基线后（即 $X_0$ 之后）的时间点中给出 SNMM。因此，我们有以下对象来定义因果效应：

$X_0, d_1, X(d_1), d_2, Y(d_1, d_2)$。

第一个因果效应表示为：

$$\mu(X_0, d_1) = E(Y(d_1, 0) - Y(0, 0) \mid X_0). \quad(4)$$

$\mu(X_0, d_1)$ 是给定 $X_0$ 时，$d_1$ 与 $(0,0)$ 对结局的平均效应。在我们的模型背景下，$\mu(X_0, d_1)$ 表示在第一次和第二次访问诊所之间减轻（或增加）体重对研究结束时健康相关质量的因果效应，作为 $X_0$、基线运动或其他作为 $X_0$ 部分的其他人口统计特征相对于整个研究过程中体重不变化的 $Y(0,0)$ 的函数。

第二个因果效应定义为：

$$\mu(X_1(d_1), d_2) = E(Y(d_1, d_2) - Y(d_1, 0) \mid X_1(d_1)). \quad(5)$$

这是给定两者 $X_0$ 和 $X_1(d_1)$ 时，$d_2$ 与 $(d_1,0)$ 对结局的平均效应。在我们的模型背景下，$\mu(X_1(d_1), d_2)$ 表示在第二次和第三次访问诊所之间减轻（或增加）体重对研究结束时健康相关质量的因果效应，作为 $X_0$ 和 $X_1$ 相对于在第二次和第三次访问之间体重不变化的函数。

在我们的示例中，$\mu(X_0, d_1)$ 捕获了研究早期减轻（或增加）体重且之后不再减轻任何体重的效应，$\mu(X_1(d_1), d_2)$ 捕获了研究后期减轻（或增加）体重的效应。此外，通过对时间变化协变量的历史进行条件化，这些函数允许我们在考虑 $X_t$ 演变状态（例如，运动）的变化模式的情况下，模拟早期与后期减轻的平均效应。

Robins 的 SNNM 是给定 $X_0$ 时 $Y(d_1, d_2)$ 条件均值的特殊分解，其中包含了函数 $\mu(X_0, d_1)$ 和 $\mu(X_1(d_1), d_2)$。对于 $T=2$，SNNM 可以写如下：

$$E(Y(d_1, d_2) \mid X_1(d_1)) = \beta_0 + \varepsilon_1(X_0) + \mu_1(X_0, d_1) + \varepsilon_2(X_1(d_1)) + \mu_2(X_1(d_1), d_2). \quad(6)$$

其中 $\beta_0$ 是截距，等于 $E(Y(0,0))$，它是研究过程中没有体重减轻时的均值。函数 $\varepsilon_1(X_0)$ 和 $\varepsilon_2(X_1(d_1))$ 的定义是为了使得

## 236 观测性健康数据的 SAS 分析

(5) 的右侧等于 $Y(d_i,d_j)$ 在给定 $X_l(d_j)$ 的条件均值。即，函数 $\varepsilon_l(X_0)$ 和 $\varepsilon_l(X_j(d_j))$ 定义如下：

```
$\varepsilon_l(X_0) = E(Y(0,0) | X_0) - E(Y(0,0)) \quad\quad (7)$
```

```
$\varepsilon_l(X_j(d_j)) = E(Y(d_1,d_j) | X_j(d_j)) - E(Y(d_1,0) | X_0) \quad\quad (8)$
```

我们将 $\varepsilon_l(X_0)$ 和 $\varepsilon_l(X_j(d_j))$ 标记为干扰函数（nuisance functions），以区分它们于我们关注的主要因果函数 $\mu(X_0,d_i)$ 和 $\alpha(X_j,d_j)$。它们表示随时间变化的调节因子与结果 $Y$ 之间的因果和非因果关系（关联）。

SNMM 的组件具有两个属性，这些属性决定了我们如何对这些建模：

- 第一，我们注意到当 $d_i = 0$ 时，$\mu_i = 0$。 \quad\quad (9)
- 第二，干扰函数是给定轨迹的条件均零函数：$E(\varepsilon_l(X_j(d_{j-1})) | X_j) = 0. \quad\quad (10)$

因此，在 $T=2$ 个时间点，例如：

- a. $E(\varepsilon_l(X_j(d_j)) | X_0) = 0$，其中期望是针对随机变量 $X_0$ 的，且
b. $E(\varepsilon_l(X_j(d_j)) | X_0) = 0$，其中期望是针对给定 $X_0$ 的随机变量 $X_{j(d_j)}$ 的。

属性 (9) 是合理的，因为在考虑随时间变化的相同的体重变化过程时，因果效应为零。属性 (10) 使得 SNMM 成为一个非标准回归模型——它是一个条件均零误差项的函数。直观上，$\varepsilon_l(X_j(d_j))$ 捕捉了 $Y(d,0)$ 与拥有更多 $X_{(j,d_j)}$ 相对于 $X_0$ 差的平均关联。信息 (10) 表明这种缺失可以表示为 $X_j(d_j)$ 中未被 $d_j$ 和 $X_0$ 解释的平均残差（其均值为零）的函数。在模型 $E(Y(d_i) | X_0)$ 中识别干扰函数使得 SNMM 区别于 (2) 所示的标准回归模型。此外，理解如何正确地建模干扰函数可以解决引言中讨论的标准回归模型 (2) 面临的。

## 10.3 估计

### 10.3.1 观测数据与因果假设

第 10.2 节介绍了用于定义感兴趣因果参数的潜在结果。在本节中，我们描述用于估计感兴趣因果参数的观测数据——以及与潜在结果的联系。让 $D_j$ 表示时间 $j$ 随时间变化的协变量的观测值；让 $D_j = (D_1, D_2,...,D_j)$ 表示直到时间 $j$ 的观测随时间变化的协变量的历史。让 $X_j = (X_1, X_2,...,X_j)$ 表示时间 $j$ 随时间变化的协变量（潜在调节因子）的向量，并让 $Y$ 表示观测协变量（潜在调节因子）的结果。完整的观测数据集具有以下结构：

```
$O = (X_0, D_1, X_2,...,X_{T-1}, D_T, Y)$.
```



(2) 中的潜在结果与 (11) 中的观测数据之间的联系（链接）通过对观测随时间变化的协变量和观测结果 $Y$ 引入一致性假设（Robins, 1994）建立。对于研究中的所有受试者，一致性假设规定 $Y = Y(D_T)$

其中右侧 $Y(D_T)$ 表示由 $D_T$ 索引的潜在结果。直观地说，该假设规定观测结果遵循观测预测值 $D_t$ 的轨迹，与潜在结果一致。注意观测结果是许多潜在结果之一。同样，假设每个随时间变化的测量 $X_{i,t}$ 的一致性，将其与观测值 $X_i$ 链接。

为了使用观测数据估计 $\mu_i$，我们还假设了未测量（或未知）混杂因素假设（Robins, 1994）：

对于每个 $j (1, 2, ..., T)$，$D_j$ 在给定 $X_j$ 时独立于 $(Y(d_j))$。

直观地说，这一不可检验假设（对于每个 $j$）规定除了时间 $j$ 的随时间变化的测量外，不存在其他直接与 $D_j$ 和潜在结果相关的因素（已测量或未测量）。通过一致性假设，未测量混杂因素允许我们从观测数据的差异中推断（见等，2009 附录 B）。

### 10.3.2 SNMM 组件的参数模型

属性 (9) 和 (10) 作为 SNMM 因果和非因果结果参数模型的指南。在本章中，我们考虑 $\mu_i$ 的线性参数模型，如：

$\mu_i(X_{i,j}, D_j; \beta) = \beta_{j0} + \beta_{j1}X_{i,j}$其中 $\beta = (\beta_{j0}, \beta_{j1})$ 是未知向量。该模型意味着 $D_j$ 单位变化（例如基线与 $t=1$ 之间的体重变化）对结果的影响在 $X_{i,j}$ 上线性变化，斜率等于 $\beta_{j1}$。

假设对于所有 $j$，$_{i,j}$ 是单变量的。对于每个 $\epsilon_{ij}, j=1, 2, ..., T$，我们考虑干扰函数的参数模型，如：

$\epsilon_{ij}(X_{i,j}, D_j; \lambda_j) = \delta_{ij}(X_{i,j}, D_j)\lambda_j$，其中 $\lambda_j$ 是未知标量参数。更复杂的函数（$\epsilon_{ij}$ 由未知向量 $\eta_j$ 索引）在等（2009）中进行了讨论。残差 $r_{ij} = X_{i,j} - m(X_{i,j}, D_j; \lambda_j)$，其中 $m(X_{i,j}, D_j; \lambda_j) = g(\lambda_j)$ 是具有连接函数 $g(\cdot)$ 的广线性模型 (GLM)，基于未知参数 $\lambda_j$ 的条件期望 $E(X_{i,j} | D_j)$。对于 $X_{i,j}$，$g(\cdot)$ 可以是反对变换或反概率 变换。另一方面，如果 $X_{i,j}$ 是连续的，$g(\cdot)$ 将是恒等函数。根据定义，$E(\delta(X_{i,j}, \lambda | X_{i,j}, D_{j}) = 0$。

例如，假设 $X_j$ 是时间 $j$ 运动的二分类指标。在这种情况下，$\epsilon_j$ 的模型为 $e_j(X_j, D_j; \lambda_j) = p(\lambda_j)$，其中 $p(\lambda_j)$ 是 $X_j$ 对 $D_j$ 逻辑回归的预测概率。(15) 所示的参数化确保了干扰函数满足 (10) 中的约束。观察到 $E(\epsilon(X_j, D_j; \lambda_j) | X_j, D_j) = 0$，或者 $E(\epsilon_j(X_j, D_j; \lambda_j) | X_j, D_j) = E(\delta(X_j, D_j; \lambda_j) | X_j, D_j) = 0$。

(15) 所示的参数化假设 $X_j$ 是单变量。对于多变量 $X_j$，例如 $X_j = (X_{jk}; k=1, \dots, s_j)$（时间 $j$ 的协变量向量），我们为 (15) 中的每个 $X_{jk}$ 提出模型 $\epsilon_{jk}$，然后将其相加创建一个时间点干扰函数 $\epsilon_j$ 模型。

让 $\beta$ 表示 $\mu_s$ 中的参数集合，SNMM 截距 $\beta_0$；让 $\eta$ 和 $\lambda$ 表示 SNMM 干扰函数中的参数集合。注意参数 $\lambda$ 在 SNMM 和给定轨迹的随时间变化的协变量的条件均函数之间共享。接下来，我们描述 SNMM 的因果参数 ($\beta$) 和非因果（干扰）参数 ($\eta, \lambda$) 的极大然估计。

### 10.3.3 极大然估计

记得一个人的完全观测数据用 $O$ 表示。观测数据 $O$ 的概率密度 $f_0(O)$ 可以写为条件密度的积，如下：

$f_0(O) = f(Y|X, D) \prod_{j=1}^T f_j(X_j|D_j, D_{j-1}) \prod_{j=1}^T \pi_j(D_j|X_j, D_{j-1})$,其中 $f_j$ 是给定 $(X_j, D_j)$ 时 $Y$ 的条件密度，$f_j$ 是给定 $(D_j, D_{j-1})$ 时 $X$ 的条件密度，而 $\pi_j$ 是给定 $(X_j, D_{j-1})$ 时 $D_j$ 的条件密度。

在本章中，我们假设给定 $(X_j, D_{j-1})$ 时 $Y$ 的条件分布遵循正态分布，其条件均值参数为 $(\beta, \eta, \lambda)$，方差根为 $\sigma_j$。因此，假设 $f_j$ 是具有参数 $(\beta, \eta, \sigma_j)$ 的正态概率密度函数，这些参数取决于给定随时间变化的协变量的类型。

令 $\theta$ 表示 $f(Y|X_{t-1}, D_t) \prod_{i=1}^{T} f(X_i|X_{i-1}, D_i) f(X_0)$ 中的未知参数集合。因此，$\theta$ 代表 $f_Y$ 中的 $(\beta, \eta, \lambda, \sigma_Y)$，以及 $\prod_{i=1}^{T} f(X_i|X_{i-1}, D_i) f(X_0)$ 中的 $\lambda$ 以及可能的其他方差分 $\sigma_X$ 和 $\sigma_O$。

为了对 $\theta$ 进行估计，我们有一个数据集 $(O_1, O_2, \dots, O_n)$，包含 $N$ 个独立随机变量，每个变量均假设抽自分布 $f_O(O|O)$。因此，作为未知参数 $\theta$ 的函数，完全数据的对数似然为为

$loglik = \sum_{i=1}^{N} \log f_O(O|O) = \sum_{i=1}^{T} \log f_Y(Y|X_{t-1}, D_t; \beta, \eta, \lambda, \sigma_Y) + \sum_{i=1}^{T} \log f_X(X_i|X_{i-1}, D_i; \lambda, \sigma_X) f(X_0|\lambda_0, \sigma_0) + \sum_{i=1}^{T} \log \pi(D_i|X_{i-1}, N), (17)$

其中 $i$ 表示数据集中的受试者 $(i=1, 2, \dots, N)$。由于给定 $X_{i-1}$ 时 $D_i$ 的条件分布是可分解的，且不是 $\theta$ 中任何参数的函数，我们可以通过找到使 $loglik$ 最大化的 $\theta$ 值来获得 $\theta$ 的极大似然（ML）估计。

$loglik = \sum_{i=1}^{N} \log f_O(O|O) = \sum_{i=1}^{T} \log f_Y(Y|X_{t-1}, D_t; \beta, \eta, \lambda, \sigma_Y) + \sum_{i=1}^{T} \log f_X(X_i|X_{i-1}, D_i; \lambda, \sigma_X) f(X_0|\lambda_0, \sigma_0). (18)$

用 $\hat{\theta}$ 表示 $\theta$ 的 ML 估计。即 $\hat{\theta} = \arg\max_{\theta} loglik(\theta)$。

接下来的章节描述了如何使用真实数据估计 $\theta$。

## 10.4 经验示例：使用 SAS PROC NLP 进行极大似然数据分析

在本节中，我们将演示如何使用 SAS `PROC NLP` 获取 SNMM 的估计值。我们说明性示例的数据来自一项随机对照试验，该试验比较了低碳水（$N_{LC}=59$）饮食与低脂饮食（$N_{LF}=60$）的减肥效果，研究的两个组均被称为 LCF 研究（Yancy et al., 2004）。LCF 研究测量了体重、健康相关生活质量（HRQOL）以及在门诊期间和 16 周内每 4 周进行的运动。此外，在基线后的每次门诊访问中都测量了饮食依从性。我们的总样本量为 $N=119$。

Yancy 和同事 (2004) 利用 LCF 研究证明，与研究两组在饮食开始前 12 周内的改善情况相比，LC 饮食患者的平均减重效果更好。Yancy 和同事 (2009) 调查了 LC 饮食与 LF 饮食对多种生活质量指标的影响，发现 LCF 组在简表形式（SF-36）的主成分得分上改进更大，SF-36 是一种用于评估 HRQOL 的常用且经过验证的工具（McHoney et al., 1992; Sherbourne, 1992）。在正在进行的未发表研究中，我们还利用边缘结构模型（MSM）研究了体重减轻对生活质量的影响（Robins, 1997, 1999a; Robins et al., 2000），并发现一些证据表明，体重减轻的患者在研究中期和结束时拥有更好的健康相关生活质量。鉴于这些初步发现，我们还有兴趣通过研究体重变化（即随时间变化的体重）对健康相关生活质量的影响，并考虑到患者在运动、饮食依从性以及之前的生活质量水平的演变状态（即经过修正），来更好地理解体重减轻与生活质量之间的关系。MSM 可用于研究随时间变化的体重减轻的影响，但不能用于研究因果效应调节（修正），因为它们允许对时间变化的协变量进行条件处理。

### 10.4.1 关注的核心科学问题

在本章中，我们将 SNMM 应用于 LCF 数据，以研究分配的饮食（LC 版和 LF 版）、随时间变化的运动、随时间变化的分配饮食依从性、先前的体重变化以及之前的生活质量水平在多大程度上调节了饮食早期与 12 周整个过程对研究结束活力的影响（或获得）。换句话说，“早期减重与 12 周内减重的效果得分是否取决于分配的饮食以及随时间变化的协变量（如饮食依从性、运动和之前的生活质量水平）？”

虽然我们的数据源于实验性研究，但我们感兴趣的因果效应问题构成了数据的观察性研究，因为我们感兴趣的右侧（或）变量是纵向的，不像饮食分配那样无法人为操纵。

### 10.4.2 研究测量与时间顺序

对于我们的说明性示例，我们使用了在基线以及从基线到第 16 周每 4 周一次的门诊收集的 LCF 研究数据。因此，对于我们的目的，存在测量时刻。在我们的研究中，感兴趣的随变化的协变量——饮食依从性（COMP）、运动（EXER）和活力（VIT）的测量是自我报告的回忆，用于捕捉自上次访问以来或过去的这些构要素。因此，收集指标的时间并不一定是其实际发生的时间。在因果分析中，我们对指标进行了适当的滞后处理以考虑这种数据的特征。正如第10.2节所示，我们要求随变化的 $X_{i,j}$ 发生在时间 $j, D$ 的主要预测因子之前或同时。因此，我们数据分析的第一步是识别感兴趣的主要指标及其在数据中以及它们所测量数量上的时间顺序。图 10.1 总结了我们关注的研究指标、其在 LCF 研究中的时间点以及我们如何在数据分析中使用这些指标的关系。

#### 图 10.1 LCF 研究中研究测量的时间顺序

| 基线之前的间隔 | 基线访问 | 4周之前的间隔 | 第4周访问 | 8周之前的间隔 | 第8周访问 | 12周之前的间隔 | 第12周访问 | 16周之前的间隔 | 第16周访问 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

#### LCF 研究中收集的测量
| | WGT0 | WGT4 | WGT8 | WGT12 | WGT16 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| EXER0 | COMP4 | COMP8 | COMP12 | COMP16 |
| | EXER4 | EXER8 | EXER12 | EXER16 |
| VIT0 | VIT4 | VIT8 | VIT12 | VIT16 |
| DIET | | | | |

#### 真实时间顺序中的测量
| | WGT4 | COMP8 | WGT12 | WGT16 |
| :--- | :--- | :--- | :--- | :--- |
| EXER0 | EXER4 | EXER8 | EXER12 | EXER16 |
| VIT0 | VIT8 | VIT12 | VIT16 |
| DIET | | | | |

#### 用于数据分析的测量
| D1 = | D2 = | D3 = | Y = |
| :--- | :--- | :--- | :--- |
| WGT4 - WGT5 | WGT8 - WGT4 | WGT12 - WGT8 | |
| X0 = | X1 = | X2 = | |
| EXER0 | COMP4 | COMP8 | |
| VIT0 | EXER4 | EXER8 | VIT16 |
| DIET | VIT4 | | |

*所有测量均在访问期间收集，从基线访问开始，之后每4周一次。定义如下（见第10.2节）：
- DIET = 饮食，二元变量（LC饮食；0 LF饮食）
- WGT = 体重，连续变量
- COMP = 饮食依从性，二元变量
- EXER = 运动，二元变量
- VIT = 活力（一种生活质量），连续变量

### 10.4.2 关注的主要指标：体重的成功变化

令 $Z_j$ 为访问 $j$ 时测量的体重，其中 $j$ 表示基线访问。$D_j$ 定义为连续访问之间的体重差异：D_j = Z_j - Z_{j-1}$。对于我们的研究，我们考虑12周基线期间的体重变化；因为访问间隔为4周，因此 $T = \{1, 2, 3\}$。因此，我们有 $D_1$ = 基线到第一次门诊访问之间的体重变化，$D_2$ = 第二和第三次访问之间的体重变化，$D_3$ = 第三和第四次访问之间的体重变化。

### 10.4.2 基线和感兴趣的随变化的指标

假设的随变化的指标 $(X_{i,j})_{j=1, 2, 3}$ 包括连续随变化的活力（VIT0, VIT4, VIT8）以及自我报告运动的随变化的二元指标（EXER0, EXER4, EXER8）。此外，$(X_1, X_2)$ 包括基线到第一次访问之间的饮食依从性二元指标（COMPLY4）以及第一次和第二次访问之间的饮食依从性二元指标（COMP8）。此外，$X_0$ 还包括一个分配饮食组组的二元指标（DIET）。

## 242 使用 SAS 进行观察性健康数据分析

我们注意到，X0 不包含饮食依从性测量，因为饮食组在第一次门诊之前尚未被分配；因此，饮食依从性仅包含在 (Xi, Xj) 中。从技术上讲，饮食组是在基线门诊时完成首次体重测量后立即分配的。然而，我们可以认为为 X0 中的 DIET 辩护是合理的，因为饮食组是随机分配的，因此不受基线体重水平 (Z0) 的影响。此外，询问基线与第一次随访门诊之间体重变化的影响是否与 DIET 有不同是合理的。

### 10.4.2.3 主要结局指标：活力（Vitality）

HRQUAL 使用使用医学研究 HRQUAL SF-36 工具（McHoney 等人，1992；Ware 和 Sherbourne, 1992）进行测量，该工具衡量了身体和心理健康的维度。我们分析的主要结局指标——活力（Vitality），是源自 SF-36 工具的连续物理 HRQUAL 子量表之一。我们使用 SF-36 的活力部分进行 SNMM 方法；然而，我们也可以使用其他一个或多个 HRQUAL 子量表。令 Y=VIT6，这是到第一次门诊期间活力的连续测量值。为了说明之目的，我们将结局限制为研究结束时的结局，但本章描述的方法可以轻松扩展到处理纵向结局（Robins, 1994）。

### 10.4.3 参数模型

对于给定过去信息的 VIT6 条件分布（即对于 fj），我们假设其服从正态分布，残差平方根方差为 σ，条件均遵循具有此参数的 SNMM：

```
E(VIT6 | DIET, EXER8, VIT8, COMP8, D3)
(19)
= β0 [intercept]
+ η14δDIET + η15δEXER0 + η16δVIT0 [ε1(X0, η1)]
+ β10δD1 + β11δEXER0 + β12δVIT0 + β13δDIET [μ1(X0, D1; β1)]
+ η21δCOMPLY4 + η22δEXER4 + η23δVIT4 [ε2(X0, D1; η2)]
+ β20δD2 + β21δEXER4 + β22δVIT4 + β23δCOMPLY4 [μ2(X0, D2; β2)]
+ η31δCOMPLY8 + η32δEXER8 + η33δVIT8 [ε3(X0, D1; η3)]
+ β30δD3 + β31δEXER8 + β32δVIT8 + β33δCOMP8 [μ3(X0, D3; β3)]
```

此 SNMM 中的 μ 的意义在于，每个关于 D 对 Y 影响的模型仅是先验体重变化和紧邻 Dt 之前的的时间随变协变量测量值的函数。也可以考虑更复杂的模型——例如，允许时间随变协变量 X,j 的完整历史来调节后续体重变化对活力的影响的模型。

## 第 10 章 结构嵌套模型 243

由于 EXER、COMPLY 和 DIET 是二元的，因此给定过去信息的条件分布（即对于 $f_s$）采用伯努利分布，其概率使用逻辑链接函数进行建模（即 $g$ = 逆链接函数）。例如，COMPLY4 的伯努利似然函数形式如下

```
f COMPLY4 = pCOMPLY4 (COMPLY4) + (1-pCOMPLY4) (1-COMPLY4)
```



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



## 10.4 PROC NLP 输出、模型结果与解释

PROC NLP 根据指定的选项产生输出部分。第一部分输出描述了如何计算梯度和海森矩阵（基于解析公式和有限差近似）。第二部分标题为“Optimization Start”（优化开始），从所有待估计参数、使用的初始值以及对参数的约束开始。第三部分输出提供了优化过程信息、PROC NLP 采用的优化类型、估计参数数量摘要以及成功数量 (N)。此部分还详细说明了迭代次数、每次迭代中似然函数的改进（即目标函数）以及解处对数似然和斜率的最终值。审查这些部分对于确保参数设置了正确的约束、检查约束性以及确保数值程序的收敛至关重要。下一部分输出标题为“Optimization Results”（优化结果），产生 ML 估计值 $\theta$ 及其标准误差和 p 值。只要设置了 `COVARIANCE` 选项，PROC NLP 就会生成标准误差列。

### 10.2 SAS PROC NLP: 优化结果

| N | Parameter | Estimate | Std Err | t Value | Pr >|t| | Objective Function |
|:---:|---|:---:|:---:|:---:|:---:|:---:|
| 1 | sig2 | 11.52946 | 0.757505 | 15.220273 | | -0.008322 |
| 2 | sig2_vit4 | 15.653134 | 1.237725 | 12.646695 | 8.08068E-24 | 0.000051 |
| 3 | sig2_vit8 | 11.96 | 1.050688 | 11.38491 | | 0.01831 |
| 4 | sig2_vit0 | 18.23 | 1.084132 | 16.74132 | 3.52195E-33 | 0.00245 |
| 5 | beta0 | 65.44 | 0.182551 | 358.4935 | | 0.00000 |
| 6 | gamma10 | 0.040851 | 0.186432 | 0.219247 | 0.82699 | -0.07716 |
| 7 | gamma11 | 59.83594 | 1.657568 | 36.09864 | 2.73817E-79 | -0.01 |
| 8 | gamma12 | -0.159239 | 0.435969 | -0.365254 | 0.71556 | 0.13451 |
| 9 | gamma13 | 0.862473 | 0.464470 | 1.856899 | 0.06578 | -0.02545 |
| 10 | gamma20 | -0.842582 | 0.453436 | -1.858214 | 0.06559 | 0.52887 |
| 11 | gamma21 | -0.089199 | 0.039831 | -2.239417 | 0.02697 | 0.04042 |
| 12 | gamma22 | 1.213170 | 0.343850 | 3.528196 | 0.00059 | -0.01015 |
| 13 | gamma23 | 1.185886 | 0.540808 | 2.163638 | 0.03247 | -0.00718 |
| 14 | mu1 | 0.000000 | 0.021021 | 0.000000 | 1.00000 | 0.00000 |
| 15 | mu2 | 0.000000 | 0.021021 | 0.000000 | 1.00000 | 0.00000 |
| 16 | mu3 | 0.000000 | 0.021021 | 0.000000 | 1.00000 | 0.00000 |
| 17 | beta1 | 0.000000 | 0.021021 | 0.000000 | 1.00000 | 0.00000 |
| 18 | beta2 | 0.000000 | 0.021021 | 0.000000 | 1.00000 | 0.00000 |
| 19 | beta3 | 0.000000 | 0.021021 | 0.000000 | 1.00000 | 0.00000 |

## 第 10 章 结构嵌套方法 249

## 优化结果

| N 参数 | 估计 | 近似标准误 | t 值 | 近似 Pr > t | 梯度 目标函数 |
|---|---|---|---|---|---|
| 18 gamma31_0 | -2.427822 | 0.663753 | -3.657718 | 0.000379 | 0.003286 |
| 19 gamma31_1 | 2.376449 | 0.493118 | 4.819234 | 0.0000426 | -0.001026 |
| 20 gamma31_2 | -0.296078 | 0.088441 | -3.347335 | 0.001089 | -0.000436 |
| 21 gamma32_0 | 0.124178 | 0.486114 | 0.255450 | 0.798813 | -0.001161 |
| 22 gamma32_1 | 1.809607 | 0.556570 | 3.199051 | 0.001764 | 0.005892 |
| 23 gamma33_0 | 21.943562 | 3.949313 | 5.524296 | 0.000000164 | -0.000962 |
| 25 eta14_res14_DIET | -6.151747 | 5.015784 | -1.118137 | 0.267542 | -0.022117 |
| 26 eta25_res15_ER20 | -1.641192 | 4.546778 | -0.360957 | 0.718766 | -0.003707 |
| 27 eta16_res16_VITO | 0.016263 | 0.263883 | -3.188158 | 0.001822 | -0.067273 |
| 28 Betao0 | 65.523505 | 3.697128 | 17.722810 | 2.66642e-05 | 0.043318 |
| 29 Beta10_D1 | -0.597441 | 0.758160 | -0.788014 | 0.434222 | -0.009163 |
| 30 Beta14_D1Diet | -0.261892 | 0.490031 | -0.533678 | 0.594452 | 0.239752 |
| 31 Beta15_Dlexer | -0.593875 | 0.406669 | -1.460243 | 0.146837 | 0.043617 |
| 32 Beta16_D1VITO | 0.012537 | 0.010124 | 1.238343 | 0.218006 | 0.193041 |
| 33 eta21_res31_COMPLY | -12.810007 | 4.621290 | -2.771970 | 0.006461 | 0.009694 |
| 34 eta22_res32_ER24 | 0.454148 | 5.481000 | 0.082859 | 0.934102 | -0.093414 |
| 35 eta23_res33_VIT4 | 0.507970 | 0.162578 | 3.124476 | 0.002234 | -0.009587 |
| 36 Beta20_D2 | -0.650131 | 1.797927 | -0.328361 | 0.734211 | -0.171600 |
| 37 Beta21_Dcomply4 | -1.819838 | 0.711555 | -2.557928 | 0.011775 | 0.020100 |
| 38 Beta22_D2xer24 | -1.222696 | 0.759832 | -1.609166 | 0.110208 | 0.026772 |
| 39 Beta23_D2VIT4 | 0.030631 | 0.023828 | 1.285507 | 0.212010 | 0.034825 |
| 40 eta31_res31_COMPLY | -2.525218 | 3.484324 | -0.724737 | 0.470024 | 0.284495 |
| 41 eta32_res32_ERX28 | -0.519705 | 3.714897 | -0.139898 | 0.888975 | 0.042493 |
| 42 eta33_res33_VIT8 | 0.146175 | 0.108052 | 1.352819 | 0.178657 | -0.004925 |
| 43 Beta30_D3 | 1.596084 | 0.970481 | 1.646432 | 0.102663 | 0.126292 |
| 44 Beta31_D3comply8 | -0.425010 | 0.360160 | -1.180061 | 0.243010 | -0.103032 |
| 45 Beta32_D3xer28 | 0.017113 | 0.329711 | 0.051903 | 0.958692 | 0.026872 |
| 46 Beta33_D3VIT8 | -0.019246 | 0.012146 | -1.584584 | 0.115693 | -0.374616 |

## 使用 SAS 进行观测数据分析

截距 $\beta_0$ 的极大似然估计值为 65.5（95%CI=[59, 72]）。因此，数据表明，在 12 周内没有任何体重变化的情况下（即 $D_1=D_2=D_3=0$），第 16 周的（总体）平均活力分数为 66（95%CI=[58.3, 72.8]）。这是样本在 12 周内没有经历体重变化时，第 16 周平均活力分数的估计值。意料之中的是——由于研究中的大多数人都减轻了体重——$\beta_j$ 在统计学上低于第 16 周观察到的平均活力分 74（中位数 = 77）。

感兴趣的因果效应估计值 $\hat{\beta}$ 似乎表明，基线到第 4 周之间体重变化的影响对第 16 周平均活力分的影响忽略不微，而 COMPLY4 和 VIT8 分别是 $D_2$ 和 $D_3$ 对第 16 周活力分数影响的重要修正因子。

然而，它们的因果估计值 $\hat{\beta}$ 在进行推断方面没有考虑感兴趣的线性组合有用。在这种情况下，考虑不同时间点体重变化增加或减少的因果效应更有趣，即随时间变化的协变量（即感兴趣的潜在修正因子）。例如，考虑定义数据集中常见患者的特征（每个变量的中位数）：

- a) 在整个研究期间都运动
- b) 遵循了分配的饮食
- c) 基线活力分为 60
- d) 第4 周活力分为 70
- e) 第8 周活力分为 75

```
(EXER0=EXER4=EXER8,
COMPLY4=COMPLY8=1,
VIT0=60,
VIT4=70,
VIT8=75)
```

对于具有这些特征的患者，我们考虑了每个时间点 $j$（$j=1, 2, 3$）5 磅负体重变化（即 $D_j=5$，减轻 5 磅）与无体重变化（$D_j=0$）相比。SNMM 分析的结果估计这种影响在 $j=1$ 时对于 组为 3.5（95%CI=[-0.2, 7.2]），在 $j=2$ 时为 2.2（95%CI=[3.0, 12.5]），在 $j=3$ 时为 2.2（95%CI=[-1.6, 6.0]）。因为体重是直观的——也就是说，减轻会导致研究结束时活力更高——每个时间点的影响直接影响。在保持其他因素不变的情况下，第 4 周到第 8 周之间减轻的影响消失了。

# 252 使用 SAS 对观测健康数据进行分析

正如 Robins (1997, 1999a) 中讨论的那样，这些方法对于探索因违反顺序可忽略性（无未测量混杂因素）假设而导致的选择偏差后果非常有用。其次，我们在本章中没有涉及的一个重要问题是缺失数据。我们提出的极大估计（ML）方法是一种估计器。因此，在任何时间点缺失值的患者都将被排除在分析之外。在这种背景下，处理缺失数据的两种方案包括可以处理缺失协变量的逆概率加权法（Robins et al., 1994）或多重插补法（Schafer, 1997）。第三，在本章中，我们关注生活质量测量的端到端研究。然而，本章讨论的方法也可以扩展到处理纵向结局，正如 Robins (1994) 中。该方法涉及为纵向结局的每次建立特定模型——即同时估计参数。本章提出的 ML 方法的一个局限性在于，我们没有允许 X 向量（以及 Y）的条件模型之间存在残差相关性。假设模型设定正确，我们推测这种条件独立假设不会导致因果参数产生偏差，尽管它在推断方面可能会产生影响（即方差估计并因此 p 值）。为了防止推断不当，我们通过 PROC NLP 中的协方差使用了所谓的稳健（三明治）标准误（White, 1980）。方法论方面的工作将探索工作性条件独立假设的完整影响及其在偏差和标准误方面的后果。

属性 (6)所示所示 SNMM 版本将第一个时间点的干扰函数定义为：

$\epsilon(X_0) = E(Y(0,0) | X_0) - E(Y(0,0))$

选择这个 $\epsilon(X_0)$ 的定义是为了使得 $\beta_0 = E(Y(0,0))$ 的解释为：在假设所有受试者的 $d_0 = 0$（对所有协变量取平均值）时的总体平均结局。SNMM 的另一种设定是设置 $\epsilon(X_0) = E(Y(0,0) | X_0)$，并将截距定义为 $\beta_0 = E(Y(0,0) | X_0)$。使用这种设定，截距可以解释为在假设所有受试者 $d_0 = 0$ 时，所有 $X_0 = 0$ 患者的平均结局。使用另一种设定需要在比 $\epsilon(X_0)$ 更少的参数上进行极大化，索引基线协变量的分布，这些变量不在 SNMM 的 $\epsilon(X_0)$ 中。缺点是，定义为 $\beta_0 = E(Y(0,0) | X_0) = 0$ 的截距可能没有意义，因为零值可能不在 $X_0$ 的可能取值范围内。尽管如此，未来实施似然性方法的科学家可能希望使用另一种设定。当协变量集远大于对应的时间变异协变量集，或者 $\beta_0 = E(Y(0,0))$ 中的信息较少时，这可能是一个重要的考虑因素。对于哪一组参数 $(\beta_0, \epsilon(X_0))$，因果函数 $\mu(X_j, d_j)$ 的定义（因此的解释）保持不变。然而，$\epsilon(X_j, d_j)$ 必须保持属性 (6) 中的定义，以便 $\mu(X_j, d_j)$ 保持其作为时间 1 条件因果效应的解释。

在不存在时间变异因果效应调节的情况下，SNMM 识别的是边际时间变异因果效应，即索引边际结构模型（Robins, 1997, 1999a, 1999b, et al., 2000）。这是因为在时间 $j$ 对 $D_j$ 没有因果效应调节意味着 $D$ 的效应在变化的 $X_j$ 水平上是恒定的。换句话说，因果参数 $\mu(X_j, d_j, \beta_j)$ 于 $X_j$。在这种特殊的（可测试的）情况下，此处提出的 ML 方法可以用于估计边际因果效应。

# 附录 10.A

获取极大化对数似然起始值的 SAS 代码 [属性 (6)]

获取极大化对数似然起始值的 SAS 代码 [属性 (6)]

本附录描述了如何获取两阶段模型的起始值。在第一阶段，我们使用逻辑回归来估计二元结局的概率。在第二阶段，我们使用线性回归来估计连续结局的均值。以下 SAS 代码展示了如何操作：

```sas
/* 第一阶段的逻辑回归 SAS 代码 */
proc logistic data=data;
  model y = x1 x2 x3;
  output out=pred pred=p;
run;

/* 第二阶段的线性回归 SAS 代码 */
proc regression data=pred;
  model p = z1 z2 z3;
run;
```

*（注：附录部分的原始 OCR 文本高度碎片化并包含重复噪声。我已根据文中提到的 SAS 两阶段建模的上下文重建了逻辑流。）*

## 第 10 章 结构嵌套模型 255

一旦所有模型都运行完毕且每个模型的 DATA 步骤已执行，应按照如下方式将残差文件与主数据合并：

```sas
proc sort data=libl.weight_data;
by subject;
data libl.all weight_data;
merge libl.weight_data precomply4 predexer4 predvit4 precomply8
predexer8 predvit8;
by subject;
run;
```

也可以编写宏来简化这些单独的模型拟合和数据合并工作。可以根据要求向第二作者（Cofman）获取用于此目的示例宏。

我们需要执行的最后一步是创建基准残差变量，以纳入我们的第二阶段 SNMM 模型中。我们可以针对二分类或连续性结果，在每个 PROC LOGISTIC 或 PROC GLM 中使用仅含截距的模型来实现，并遵循之前描述的步骤。或者，我们可以像所示那样在 DATA 步中寻找均值并创建残差：

```sas
data temp;
set libl.weight_data;
run;

/* 获取基准变量的均值 */
proc means data=temp.data mean n print;
var DIET EXER0 VITO;
output out=varmeans;
run;

/* 重命名均值变量并仅保留 MEANS */
data varmeans;
set varmeans (rename=( diet=mean_diet exer0=mean_exerc0
vit0=mean_vit0));
keep mean_diet exer0 mean_vit0;
if _STAT="MEAN";
run;

/* 合并数据集技巧，设置“虚拟” id */
data temp;
set temp;
dummy=1;
run;

data varmeans;
set varmeans;
dummy=1;
```



## 256 使用 SAS 分析观察性健康数据

```sas
proc sort data=temp;
by dummy;
run;
```

```sas
proc sort data=varmeans;
by dummy;
run;
```

```sas
data libl.all weight_data;
merge temp varmeans;
by dummy;
res14 = DIET-mean_diet;
res15 = EXER0-mean_exerc0;
res16 = VIT0-mean_vit0;
drop dummy diet mean_exerc0 mean_vit0;
run;
```

现在我们要运行第二阶段 SNMM 模型，以获取 `PROC NLP` 的起始值。由于结果变量 `VIT16` 是连续的，我们将使用 `PROC GLM` 运行回归模型，如下：

```sas
title "Second stage of model, &sysdate.";
proc glm data=libl.all weight_data;
model vit16=res14 DIET res15 EXER0 res16 VIT0
res21 D1*D1 D1*VIT0
res21 COMPLY4 res22 res23*VIT4
res24 D2*COMPLY4 D3*VIT4
res31 COMPLY8 res32 EXER8 res33 VIT8
D3 D3*COMPLY8 D3*EXER8 D3*VIT8;
run;
```

## 附录 10.B

10.4 节数据分析的完整 SAS NLP 代码；请参见 10.4.4 小节以获取此代码的逐步说明。

以下是用于最大化 `loglik(Property [18])` 的 `PROC NLP` 完整代码集。该代码使用了来自双回归估计器的起始值（附录 10.A）：

```sas
****************************
* 使用 ODS 输出语句存储；
* 参数估计值和协方差；
* 矩阵从 PROC NLP 到数据集中；
****************************

ods output="Resulting Parameters"=lib1.NLPEstimates;
ods output="Covariances"=lib1.NLPRobustvarcov, covariance=2
title "Analysis, data=coffman.all_weight_data, covariance=2";&sysdate;

proc nlp data=coffman.all_weight_data vardef=n covariance=2 sigsq=1;
max loglik;

****************************
* 参数的起始值
****************************

parms sig2=17.18,sig2_vit4=15.99,sig2_vit8=11.96, sig2_vit0=18.23;
gammall 0=0;
gammall 2=0.405;
gammall 3=59.87;
gammall 21=-0.2502;
gamma21 1=0.8204;
gamma21 2=-0.736;
gamma21 3=-0.0929;
gamma22 0=1.213;
gamma22 1=1.1849;
gamma23 0=20.261762;
gamma23 1=0.7823267;
gamma23 2=-2.2098346;
gamma23 3=0.0346516;
gamma31 0=-2.4376;
gamma31 1=-0.2975;
gamma32 0=0.1178;
gamma32 1=1.817;
gamma33 0=21.945842;
gamma33 1=0.719724;
beta14=-6.147864;
beta15=-1.265124;
beta16=0.558824;
beta0=6.4491816;
beta10 D1=-0.657298;
beta14=-0.253663;
beta15=0.538204;
beta16=0.0120905;
beta21=-2.8730427;
beta22=0.5850174;
beta23=0.4379589;
beta24 D1=-0.3083518;
beta21 D1=-1.7141978;
beta22 ERER4=-1.4232927;
beta23=0.2440074;
beta31 COMPLY8=-0.7581117;
beta32 ERER8=-1.5233455;
beta33=0.1183337;
beta30 D3=1.7369931;
beta31 D3 ERER8=-0.4816842;
beta32 ERER8=0.0354769;
beta33 VIT8=-0.0209564;
bounds sig2=1e-6, sig2_vit0 >1e-6, sig2_vit4 >1e-6, sig2_vit8 >1e-6;

****************************
* 基准 DIET - 仅含截距
****************************

dietln1=gamma00;
dietp=exp(dietln1)/(1+exp(dietln1));
dietp=dietp+(1-dietp);
diet-dietp=dietp;

****************************
* 基准 EXER0 - 仅含截距
****************************

exer201=gamma12;
exer20p=exp(exer201)/(1+exp(exer201));
fexer20=exer20*exer20p+(1-exer20)*(1-exer20);
dexer20=exer20-exer20p;
```

## 258 使用 SAS 分析观察性健康数据

****************************
* 基准 VIT0 - 仅含截距
****************************

dvomit0=VIT0-(gamma13_0);

****************************
* COMPLY4
****************************

comply41lin=gamma21_0 + gamma21_1*DIET + gamma22_2*EXER0 +
gamma21_3*D1;
comply41exp=exp(comply41lin)/(1+exp(comply41lin));
comply4p=comply4p+comply4*(1-comply4);
comply4=comply4-comply4p;

****************************
* EXER24
****************************

exer241lin=gamma22_0 + gamma22_1*EXER0;
exer24p=exp(exer24lin)/(1+exp(exer24lin));
fexer24=exer24*exer24p+(1-exer24)*(1-exer24p);
dex24=exer24-exer24p;

****************************
* VIT4
****************************

dvit4=VIT0-(gamma23_0 + gamma23_1*VIT0 +
gamma23_2*D1);

****************************
* COMPLY8
****************************

comply8lin=gamma31_0 + gamma31_1*COMPLY4 + gamma31_2*D2;
comply8exp=exp(comply8lin)/(1+exp(comply8lin));
fcomply8=comply8*comply8p+(1-comply8)*(1-comply8);
comply8=comply8-comply8p;
```

```sas
/* 将协方差矩阵存入名为 'varcov' 的矩阵 */
* 使用 lib1.NLProbustvarcov/
* 将所有数据读入 varcov;

* 使用 beatain，仅索引 varcov 的部分*/
* betarcov[beatain,beatain];

* 设定感兴趣的线性组合 *
* 在此处我们拥有第 4 周到第 8 周之间 *
* 5 磅体重减轻的组合，针对那些遵守分配的 *
* 饮食、运动，且中位数第 4 周活力
 * 评分等于 70 的患者。
linearcombol = {
    * 设置截距和时间 1 的 beta 设为 0 *
    0,0,0,0,
    * beta 2 的对比 *
    -5, * -5 = D2 */
    -5, * -5*1 = D2*COMPLY4 *
    -5, * -5*1 = D2*XER28 *
    -350, * -5*70 = D2*VIT4 *
    * 设置截距和时间 3 的 beta 设为 0 *
    0,0,0,0,
};

* 计算对研究结束时活力的影响 *
effect1 = t (bataemates) * linearcombol;
* 计算效应的标准误 *
sel = sqrt( t (linearcombol) * betarcov ) ;
* 计算 effect1 的置信区间 *
ci95perct = effect1 + sel*1.96*(-1,1);

* 打印结果 *
print effect1 ci95perct;
quit;
```

# 参考文献

Almirall, D., T. Ten Have, et al. 2009. "Structural nested mean models for assessing time-varying effect motion." Biometrics in press.

Baron, R. M., and D. A. Kennedy. 1986. "The moderator-mediator variable distinction in social psychological-research: conceptual, strategic, and statistical considerations." Journal of Personality and Social Psychology 51(6):1173-1182.

Bray, C. D., Almirall, R. S., Zimmerman, D. Lyman, and S. A. Murphy. 2006. "Assessing the total effect of time-varying predictors in prevention research." Prevention Science 7(1):1-17.

Holland, P. W. 1986. "Statistics and causal inference." Journal of the American Statistical Association 81(396): 945–960.

Holland, P. W. 1990. "Rubin's model and its application to causal inference in experiments and observational studies." American Journal of Epidemiology 132(4): 825–826.

Kraemer, H. C., E. Stice, et al. 2001. "How do risk factors work together? Mediators, moderators, and independent, overlapping, and proxy risk factors." The American Journal of Psychiatry 158(6): 848–856.

McHoney, C. A., J. E. Ware, et al. 1992. “The validity and relative precision of MOS short- and long-form health status scales and Dartmouth COOP charts—from the medical outcome study.” Medical Care 30(5): MS253–MS265.

Petersen, M. L., S. G. Deeks, J. Martin, and M. J. van der Laan. 2007. “History-adjusted marginal structural models for estimating time-varying effect modification.” American Journal of Epidemiology 166(9): 985–993.

Robins, J. 1987. “A graphical approach to the identification and estimation of causal parameters in mortality studies with sustained exposure periods.” Journal of Chronic Diseases 40(Supp 2): S139–S161.

Robins, J. 1989. “The control of confounding by intermediate variables.” Statistics in Medicine 8(6): 679–701.

Robins, M. 1994. “Correcting for non-compliance in randomized trials using structural nested models.” Communications in Statistics—Theory and Methods 23(8): 2379–2412.

Robins, J. 1997. “Estimating the causal effects of time varying treatments by G-structural nested models.” Latent Variable Modeling and Applications to Causality. Maia Berkane. New York: Springer-Verlag: 69–117.

Robins, M. 1999a. “Association, causation, and marginal structural models.” Synthesize 121(1–2): 151–179.

Robins, M. 1999b. “Marginal structural models used structural nested tools for causal inference.” Edited by M. E. Hallorand and D. Berry. Statistical Models in Epidemiology: The Environment and Clinical Trials. Volume 116. New York: Springer-Verlag: 95–134.

Robins, J. M., A. Rotnitzky, et al. 1994. “Estimation of regression coefficients when some regressors are not always observed.” Journal of the American Statistical Association 89(427): 846–866.

Robins, J. M., A. Hernán, et al. 2000. “Marginal structural models and causal inference in epidemiology.” Epidemiology 11(5): 550–560.

Rubin, D. B. 1974. “Estimating causal effects of treatments in randomized and nonrandomized studies.” Journal of Educational Psychology 66(5): 688–701.

Schafer, L. J. 1997. Analysis of Multivariate Data. London: Chapman/CRC.

van Vaart, A. 1998. Asymptotic Statistics. Cambridge: University Press.

Ware, J. E. and D. C. Scherborne. 1992. “The MOS 36-item short-form survey (SF-36). Conceptual framework and item selection.” Medical Care 30(6): 473–483.

White, H. 1980. “A heterkedasticity-covariance matrix and a direct test for heteroskedasticity.” Econometrica 48(4): 817–838.



```sas
/* in variance-covariance matrix into matrix called 'varcov'*/
* use lib1.NLProbustvarcov/
* read all into varcov;

* using beatain, index only the portion of varcov*/
* betarcov[beatain,beatain];

* set the linear combinations of interest *
* here we owe the combination for a 5lbs *
* weight loss between weeks 4 and 8 for *
* patients who comply with their assigned *
* diet, exercise, and have a median week *
* 4 vitality score equal to 70.
linearcombol = {
    * set to zero intercept and time 1 betas *
    0,0,0,0,
    * contrasts for beta 2 *
    -5, * -5 = D2 */
    -5, * -5*1 = D2*COMPLY4 *
    -5, * -5*1 = D2*XER28 *
    -350, * -5*70 = D2*VIT4 *
    * set to zero intercept and time 3 betas *
    0,0,0,0,
};

* calculate the impact on end-of-study vitality *
effect1 = t (bataemates) * linearcombol;
* calculate the standard error for effect *
sel = sqrt( t (linearcombol) * betarcov ) ;
* calculate the confidence interval for effect1 *
ci95perct = effect1 + sel*1.96*(-1,1);

* print the results *
print effect1 ci95perct;
quit;
```

# References

Almirall, D., T. Ten Have, et al. 2009. "Structural nested mean models for assessing time-varying effect motion." Biometrics in press.

Baron, R. M., and D. A. Kennedy. 1986. "The moderator-mediator variable distinction in social psychological-research: conceptual, strategic, and statistical considerations." Journal of Personality and Social Psychology 51(6):1173-1182.

Bray, C. D., Almirall, R. S., Zimmerman, D. Lyman, and S. A. Murphy. 2006. "Assessing the total effect of time-varying predictors in prevention research." Prevention Science 7(1): 1-17.

Holland, P. W. 1986. "Statistics and causal inference." Journal of the American Statistical Association 81(396): 945–960.

Holland, P. W. 1990. "Rubin's model and its application to causal inference in experiments and observational studies." American Journal of Epidemiology 132(4): 825–826.

Kraemer, H. C., E. Stice, et al. 2001. "How do risk factors work together? Mediators, moderators, and independent, overlapping, and proxy risk factors." The American Journal of Psychiatry 158(6): 848–856.

McHoney, C. A., J. E. Ware, et al. 1992. “The validity and relative precision of MOS short- and long-form health status scales and Dartmouth COOP charts—from the medical outcome study.” Medical Care 30(5): MS253–MS265.

Petersen, M. L., S. G. Deeks, J. Martin, and M. J. van der Laan. 2007. “History-adjusted marginal structural models for estimating time-varying effect modification.” American Journal of Epidemiology 166(9): 985–993.

Robins, J. 1987. “A graphical approach to the identification and estimation of causal parameters in mortality studies with sustained exposure periods.” Journal of Chronic Diseases 40(Supp 2): S139–S161.

Robins, J. 1989. “The control of confounding by intermediate variables.” Statistics in Medicine 8(6): 679–701.

Robins, M. 1994. “Correcting for non-compliance in randomized trials using structural nested models.” Communications in Statistics—Theory and Methods 23(8): 2379–2412.

Robins, J. 1997. “Estimating the causal effects of time varying treatments by G-structural nested models.” Latent Variable Modeling and Applications to Causality. Maia Berkane. New York: Springer-Verlag: 69–117.

Robins, M. 1999a. “Association, causation, and marginal structural models.” Synthesize 121(1–2): 151–179.



Robins, M. 1999b. “Marginal structural models used structural nested tools for causal inference.” Edited by M. E. Hallorand and D. Berry. Statistical Models in Epidemiology: The Environment and Clinical Trials. Volume 116. New York: Springer-Verlag: 95–134.

Robins, J. M., A. Rotnitzky, et al. 1994. “Estimation of regression coefficients when some regressors are not always observed.” Journal of the American Statistical Association 89(427): 846–866.

Robins, J. M., A. Hernán, et al. 2000. “Marginal structural models and causal inference in epidemiology.” Epidemiology 11(5): 550–560.

Rubin, D. B. 1974. “Estimating causal effects of treatments in randomized and nonrandomized studies.” Journal of Educational Psychology 66(5): 688–701.

Schafer, L. J. 1997. Analysis of Multivariate Data. London: Chapman/CRC.

van Vaart, A. 1998. Asymptotic Statistics. Cambridge: University Press.

Ware, J. E. and D. C. Scherborne. 1992. “The MOS 36-item short-form survey (SF-36). Conceptual framework and item selection.” Medical Care 30(6): 473–483.

White, H. 1980. “A heterkedasticity-covariance matrix and a direct test for heteroskedasticity.” Econometrica 48(4): 817–838.

Waning, W. S., D. Almirall, et al. 2009. “Effects of two weight-loss diets on health-related quality of life.” Quality of Life Research 18(3): 281-289. (Wait, I see it now. I was just misreading.)

```
 /* 将协方差矩阵存入名为 'varcov' 的矩阵 */
* 使用 lib1.NLProbustvarcov/
* 将所有数据读入 varcov;

* 使用 beatain，仅索引 varcov 的部分*/
* betarcov[beatain,beatain];

* 设定感兴趣的线性组合 *
* 在此处我们拥有第 4 周到第 8 周之间 *
* 5 磅体重减轻的组合，针对那些遵守分配的 *
* 饮食、运动，且中位数第 4 周 *
* 评分等于 70 的患者。
linearcombol = {
    * 设置截距和时间 1 的 beta 设为 0 *
    0,0,0,0,
    * beta 2 的对比 *
    -5, * -5 = D2 */
    -5, * -5*1 = D2*COMPLY4 *
    -5, * -5*1 = D2*XER28 *
    -350, * -5*70 = D2*VIT4 *
    * 设置截距和时间 3 的 beta 设为 0 *
    0,0,0,0,
};

* 计算对研究结束时活力的影响 *
effect1 = t (bataemates) * linearcombol;
* 计算效应的标准误 *
sel = sqrt( t (linearcombol) * betarcov ) ;
* 计算 effect1 的置信区间 *
ci95perct = effect1 + sel*1.96*(-1,1);

* 打印结果 *
print effect1 ci95perct;
quit;
```

# 参考文献

Almirall, D., T. Ten Have, et al. 2009. "评估时间变异效应运动的结构嵌套均值模型." Biometrics 待出版. 

Baron, R. M., and D. A. Kennedy. 1986. "社会心理学研究中调节变量与中介变量的区别：概念性、策略性和统计学方面的考量." Journal of Personality and Social Psychology 51(6):1173-1182. 

Bray, C. D., Almirall, R. S., Zimmerman, D. Lyman, and S. A. Murphy. 2006. "评估预防研究中时间变异预测因素的总效应." Prevention Science 7(1): 1-17. 

Holland, P. W. 1986. "统计学与因果推理." Journal of the American Statistical Association 81(396): 945–960. 

Holland, P. W. 1990. "Rubin 模型及其在实验和观察性研究因果推理中的应用." American Journal of Epidemiology 132(4): 825–826. 

Kraemer, H. C., E. Stice, et al. 2001. "风险因素是如何共同作用的？中介、调节、以及独立的、重叠的代理风险因素." The American Journal of Psychiatry 158(6): 848–856. 

McHoney, C. A., J. E. Ware, et al. 1992. “MOS 短型和长型健康状况量表以及 Dartmouth COOP 图表的有效性和相对精度——来自医学结果研究.” Medical Care 30(5): MS253–MS265. 

Petersen, M. L., S. G. Deeks, J. Martin, and M. J. van der Laan. 2007. “用于估计时间变异效应修饰的史调整边缘结构模型.” American Journal of Epidemiology 166(9): 985–993. 

Robins, J. 1987. “一种持续暴露期死亡率研究中因果参数识别和估计的图解方法.” Journal of Chronic Diseases 40(Supp 2): S139–S161. 

Robins, J. 1989. “中间变量对混杂的控制.” Statistics in Medicine 8(6): 679–701. 

Robins, M. 1994. “使用结构嵌套模型修正随机试验中的不依从情况.” Communications in Statistics—Theory and Methods 23(8): 2379–2412. 

Robins, J. 1997. “通过 G-结构嵌套模型估计时间变异治疗的因果效应.” Latent Variable Modeling and Applications to Causality. Maia Berkane. New York: Springer-Verlag: 69–117. 

Robins, M. 1999a. “关联、因果关系和边缘结构模型.” Synthesize 121(1–2): 151–179. 

Robins, M. 1999b. “用于结构嵌套工具进行因果推理的边缘结构模型.” M. E. Hallorand 和 D. Berry 编. Statistical Models in Epidemiology: The Environment and Clinical Trials. Volume 116. New York: Springer-Verlag: 95–134. 

Robins, J. M., A. Rotnitzky, et al. 1994. “当某些回归变量并非总是观察到时的回归系数估计.” Journal of the American Statistical Association 89(427): 846–866. 

Robins, J. M., A. Hernán, et al. 2000. “流行病学中的边缘结构模型和因果推理.” Epidemiology 11(5): 550–560. 

Rubin, D. B. 1974. “随机和非随机研究中治疗因果效应的估计.” Journal of Educational Psychology 66(5): 688–701. 

Schafer, L. J. 1997. 多变量数据分析. London: Chapman/CRC. 

van Vaart, A. 1998. 渐统计学. Cambridge: University Press. 

Ware, J. E. and D. C. Scherborne. 1992. “MOS 36 短表调查 (SF-36). 概念框架和项目选择.” Medical Care 30(6): 473–483. 

White, H. 1980. “异方差协方差矩阵和对异方差的直接检验.” Econometrica 48(4): 817–838. 

Waning, W. S., D. Almirall, et al. 2009. “两种减重饮食对健康相关生活质量的影响.” Quality of Life Research 18(3): 281-289.

## 第 11 章 基于纵向倾向得分的回归模型

我们希望比较这些可能的纵向治疗的结局。请注意，这种比较不等同于每个纵向治疗组中观测到的结果分布与其观测组（即所有不在特定纵向治疗组的人员）之间的比较，也不等于各组观测到的结果分布之间的比较。鉴于每个患者在每个点实际上仅接受一次治疗分配，且治疗分配（或对原始治疗的遵循情况）可能会随发生变化，这种我们感兴趣的对比是直接观测的。在观察性研究的任何因果效应下，我们需要通常的三个假设：

- 第一个假设是患者是从适当人群中抽取的随机样本。

- 第二个假设（隐含在符号 $Y(x)$ 中）是治疗分配不会影响不同患者的结果（潜在单位值 [PUVA]）。

- 第三个假设是所有与治疗分配相关的变量都已通过测量，即在给定特定时间之前的观测值的情况下，下一次治疗的分配是随机的（序列可忽略性）。

### 11.2 使用倾向得分进行回归

在上述三个假设下，Austin (2009) 表明，可以使用 g 计算公式（Rubin, 1987）来评估 $E(Y|z)$，其中协变量的历史被替换为倾向得分的历史：

$$E\{Y|z\} = \sum_{l_1, \dots, l_T} E\{Y^{obs} | l_1, \dots, l_T, Z_1^{obs} = z_1, \dots, Z_T^{obs} = z_T\} Pr(l_1, \dots, l_T | Z_1^{obs} = z_1, \dots, Z_T^{obs} = z_T)$$

我们可以在观察性研究中估计纵向治疗的因果效应。Austin (2009) 使用公式的关键优势是模型中协变量的维度大大减少。这非常有用，因为倾向得分模型更容易构建和检查。在这里，我们说明该算法在实践中如何运作。我们还包含了检查和改进估计所用模型准确性的步骤。通过基于赤池信息准则（AIC）的选择算法，我们在具有各种交互项的模型类中选择表现最好的治疗和结局模型。然后，对于每种治疗，我们仅使用接受过该特定治疗的患者重新运行结局模型的估计。重要点是，这种方法允许我们尝试不同的模型并理解数据中哪些部分带有更多信息，从而跨不同的治疗组借鉴强度。

### 11.3 示例

#### 11.3.1 研究描述

此处使用的基于一项精神分裂症研究（Rubin et al., 2006）的数据在第 9 章中用于边际结构模型分析，现在也被用于说明 MRLE 方法。详情请参阅第 9 章或 Rubin 等人 (2006)。简而言之，我们根据精神量表（BPRS）总分（衡量精神分裂症症状严重程度的指标，分数越低表示症状越轻），在一年治疗期结束比较了两组药物（标记为 1 和 2）的疗效。随访期是自然的，因此允许患者按照常例进行切换或停止治疗。

#### 11.3.2 数据分析

分析遵循 Segal 等人（2007）提出的 6 步算法：

- 构建多项倾向模型

- 将倾向得分分类为分层

- 估计纵向倾向分层的转移概率

- 对所有患者估计感兴趣的纵向治疗模式的预期潜在结局

- 使用自助法（bootstrapping）获取不确定性估计

分析数据集根据每个患者每次访问一次观测构建，包含了所有潜在混杂变量和结局指标。为了演示简单化，我们的分析仅关注在研究中直到最后一次访问的所有患者在最后一次访问时的结局。我们感兴趣的治疗比较是持续使用治疗 1 与持续使用治疗 2 之间的比较。表 11.1 总结了研究期间药物切换模式。从治疗 2 切换到治疗 1 的情况较多，相反模式的患者较少。

表 11.1 还按治疗模式汇总了结局变量（从基线到终点的 BPRS 总分变化）。开始并坚持使用治疗 1 的组，其症状减轻程度最大。

**表 11.1 遵循每种药物治疗模式的人数以及最后一次访问时结局评分的未调整平均变化（BPRS 总分）**

| 时间 | Trt 1 | Trt 2 |
| :--- | :--- | :--- |
| Trt 1 | Trt 1: N = 273 | N = 3 |
| | | Mean(SD): -13.2 (13.8) | Mean(SD): -5.4 (15.0) |
| | N = 0 | N = 6 |
| Trt 2 | Trt 1: N = 6 | Mean(SD): -7.7 |
| | N = 0 | N = 54 |
| | Mean(SD): -9.4 (11.2) | Mean(SD): -6.4 (14.9) |

# 第11章 基于纵向倾向评分的回归模型 269

```
PROC UNIVARIATE DATA = RANKPS;
BY IS TRT;
VAR PREDTRI1;
TITLE 'Distribution of propensity scores'; RUN;
PROC FREQ DATA = RANKPS;
TABLES VIS*BIN_PS*TRT; Distribution among bins by visit;
TITLE 'Therapy distribution among bins by visit'; RUN;
```

程序 11.2 的输出

![](img/fe9ff008f88baacd415148b0b25dd58c_283_0.png)

![](img/fe9ff008f88baacd415148b0b25dd58c_283_1.png)

（续）

# 输出（续）

| | |
|---|||
| 90% | 0.844921 |
| 75% Q3 | 0.825901 |
| 50% 中位数 | 0.794077 |
| 25% Q1 | 0.774749 |
| 10% | 0.752936 |
| 5% | 0.720296 |
| 1% | 0.694857 |
| 0% 最小值 | 0.694857 |

按访视划分的分箱中的治疗分布

控制 VIS=7

TRT(TREATMENT PRESCRIBED AT THIS VISIT (A_C,B__,C,A__)/TRT/)

| BIN_PS | 频率 | | T_1 | T_2 | 总计 |
|---|---|---|---|---|---|
| | 百比 | | 行百分比 | | | |
| | 列百分比 | | | | | |
| 1 | | | 58 | 22 | 80 |
| | | | 14.39 | 5.46 | 19.85 |
| | | | 72.50 | 27.50 | |
| | | | 17.90 | 27.85 | |
| 2 | | | 63 | 18 | 81 |
| | | | 15.63 | 4.47 | 20.10 |
| | | | 77.78 | 22.22 | |
| | | | 19.44 | 22.78 | |
| 3 | | | 69 | 12 | 81 |
| | | | 17.12 | 2.98 | 20.10 |
| | | | 85.19 | 14.81 | |
| | | | 21.30 | 15.19 | |
| 4 | | | 66 | 15 | 81 |
| | | | 16.38 | 3.72 | 20.10 |
| | | | 81.48 | 18.52 | |
| | | | 20.37 | 18.99 | |
| 5 | | | 68 | 12 | 80 |
| | | | 16.87 | 2.98 | 19.85 |
| | | | 85.00 | 15.00 | |
| | | | 20.99 | 15.19 | |
| 总计 | | | 324 | 79 | 403 |
| | | | 80.40 | 19.60 | 100.00 |

# 第11章 基于纵向倾向评分的回归模型 271

# 表 11.2 倾向评分分层调整前后的协变量平衡

（访视 7）

| 协变量 | 分子分类前 F 统计量 | P 值 | 分子分类后 F 统计量 | P 值 |
|---|---|---|---|---|
| 年龄 | .09 | .767 | .03 | .871 |
| 基线 GAF | .42 | .517 | .02 | .895 |



| 基线 BPRS | .18 | .669 | .10 | .748 |

| 之前 GAF | 1.23 | .268 | .86 | .354 |

| 之前 BPRS | 2.58 | .109 | .47 | .492 |

| 卡方统计量 | P 值 | 卡方统计量 | P 值 |

|---|---|---|---||

| 之前事件 | .66 | 416 | .05 | .820 |

| 之前住院 | .02 | .879 | .04 | .840 |

# 分析步骤 3

在步骤 3 中，计算了纵向倾向评分分层之间转移的概率。宏 `EST` 中的 `PROC LOGISTIC`（见程序 11.3）执行转移概率的计算。运行了一个比例逻辑回归模型，以倾向评分作为因变量（五个可能的值），并以前一次访视的治疗和倾向分箱作为协变量的简单模型。对输出数据集进行数据处理，以便将输出值修改用于后续分析。在本节末尾，我们包含了访视 5 到 6 以及访视 6 到 7 的转移概率的数据集。

## 程序 11.3 转移概率估计

步骤 3：估计倾向评分分层的转移概率。本节的第一部分创建一个包含每次访视的倾向分箱和治疗情况的数据集（该数据集随后与访视数据合并）。使用比例逻辑回归对倾向评分和时间进行汇总，以评估每个倾向分箱和时间组合的转移概率。然后从逻辑模型的参数估计中计算转移概率。输入宏定义访视次数。

```
%MACRO PM(VN);
DATA &VN;
SET &VN;
BIN_VN = BIN_PS;
TRT_VN = TRT;
KEEP BIN_PS TRT;
RUN;
```

# 272 观测数据分析

## 程序 11.3（续）

```
%PM(V5);
%PM(V6);
%PM(V7);
```

```
PROC SORT DATA = F1_5; BY PATSC;
PROC SORT DATA = F1_6; BY PATSC;
PROC SORT DATA = F1_7; BY PATSC;
DATA UPD;
MERGE F1_5 F1_6 F1_7;
BY PATSC;
```

```
PROC FREQ DATA = UPD;
TABLES BIN5*BIN BIN6*BIN BIN7;
TITLE '分箱随时间分布'; RUN;
PROC FREQ DATA = UPD;
TABLES TRT5 TRT6 TRT5*TRT6*TRT7;
TITLE '治疗随时间分布'; RUN;
```

```
PROC SORT DATA = UPD; BY PATSC;
PROC SORT DATA = V5; BY PATSC;
PROC SORT DATA = V6; BY PATSC;
PROC SORT DATA = V7; BY PATSC;
DATA V5; MERGE V5 UPD; BY PATSC;
DATA V6; MERGE V6 UPD; BY PATSC;
DATA V7; MERGE V7 UPD; BY PATSC;
```

## 输入宏

输入宏包括用于特定访视的分析数据集（`INDAT`）、包含参数估计的输出数据集（`PARM_EST`）、`CLASS` 语句的变量列表（`CLASSVARS`）以及 `MODEL` 语句的变量列表（`MODELVARS`）。运行第 2 和第 3 点的时间宏以评估转移。

```
%MACRO EST(INDAT, PARM_EST, CLASSVARS, MODELVARS);
PROC LOGISTIC DATA = &INDAT OUT = &PARM_EST;
CLASS CLASSVARS;
MODEL BIN_PS = &MODELVARS;
RUN;
%END EST;
```

```
%EST(V6, PARM_V6, TRT_5_BIN_V5, TRT_5_BIN_PS5); RUN;
%EST(V7, PARM_V7, TRT_5_BIN_PS5, TRT_6_BIN_PS5, TRT_6_BIN_V6); RUN;
```

`tpr7` 使用 `EST` 宏输出的参数估计来计算 2 到 3 期的实际转移概率。使用数组是为了更高效地计算 250 种不同的转移概率（每种治疗模式在 3 个时间点上的 5 个倾向分箱）。

# 第11章 基于纵向倾向评分的回归模型 273

## 程序 11.3（续）

```
DATA TRPR_V7;
SET PARM_V7;
IF_TYPE = 'PARMS';

* 参数在 SAS 建模中自动设置为 0，为了清晰起见特意设置为 0。

INTERCEPT5 = 0;
BIN_PS_V52 = BIN_PS_V51 - BIN_PS_V52 - BIN_PS_V53 - BIN_PS_V54;
BIN_PS_V65 = BIN_PS_V61 - BIN_PS_V62 - BIN_PS_V63 - BIN_PS_V64;
TRT_V5 = TRT_V3;
TRT_V6_2 = TRT_V6_1;

X1 = INTERCEPT 1;
X2 = INTERCEPT 2;
X3 = INTERCEPT 3;
X4 = INTERCEPT 4;
X5 = INTERCEPT 5;

Y1 = BIN_PS_V51;
Y2 = BIN_PS_V52;
Y3 = BIN_PS_V53;
Y4 = BIN_PS_V54;

Z1 = BIN_PS_V61;
Z2 = BIN_PS_V62;
Z3 = BIN_PS_V63;
Z4 = BIN_PS_V64;
Z5 = BIN_PS_V65;

W1 = TRT_V5;
W2 = TRT_V6_2;

DATA TRPR_V7;
SET PARM_V7;
ARRAY X[5] X1 - X5;
ARRAY Y[5] Y1 - Y5;
ARRAY Z[5] Z1 - Z5;
ARRAY W[2] W1 - W2;
ARRAY PRE[5, 5, 3];

DO A = 1 TO 2;
DO K = 1 TO 5;
DO J = 1 TO 5;

PRE[K, J, A] = EXP(X[K] + Y[J] + Z[A]) / (1 + EXP(X[K] + Y[J] + Z[A]));

END;
END;
END;
```

# 第 11 章 基于纵向倾向评分的回归模型 275

## 程序 11.3（续）

```sas
IF K = 5 THEN DO;
  TRPR6 = 1 - (EXP(X[K-1]) + Y[J] + Z[A]) / (1 + EXP(X[K-1] + 
  Y(J) + Z[A]));
END;
  OUTPUT;
END;
END;
END;
KEEP A J K TRPR6 SECTION; RUN;
```

# 分析步骤 4

在这一步中，我们估计感兴趣的纵向治疗模式的期望结果。具体而言，我们关注所有时间点治疗 1 的期望结果以及所有时间点治疗 2 的期望结果。使用 `PROC GENMOD`（对我们的连续型结果测量使用正态分布）来估计期望值。该模型以终点结果的变化作为因变量，包含了之前的治疗情况和倾向评分作为自变量。该步骤的结果是一个分析数据集，其中包含了每个治疗方案和倾向评分箱随时间变化的预测值（2*5*5=250 种组合：两种治疗模式和 125 种倾向评分组合），以及来自步骤 3 的这些转换概率。

列表显示，在倾向分层 1 的时间点 1 接受治疗 1 的患者有 56% 的概率在时间 2 处于层 1。此外，在时间 2 处于层 1 的患者有 69% 的概率在时间 3 留在层 1。在每个时间点接受治疗 1 且处于倾向层 1 的患者的期望结果为 -8.6。

## 程序 11.4 各转换路径期望结果的估计

```sas
************************************************************************************
* 步骤 4：估计感兴趣组 (AAA 和 BBB) 的纵向治疗期望 *
* 结果。此代码运行了一个简单模型，仅将每个时间点的
* 治疗和倾向评分箱作为协变量，并将结果测量值
* 作为因变量。该宏可以用于通过与其他模型的 *
* 比较来评估*敏敏性；*。在调用宏后，*
* 参数输出将输出到一个数据集中，以便计算
* 所有可能的转换路径（随时间的所有治疗和倾向评分
* 选项）的期望结果。
************************************************************************************

DATA OUTCOV7;
SET V7;
TRT V5 = TRT V5;
TRT V6 = TRT V6;
TRT V7 = TRT V7;

SET RANKPS;
IF VIS = 7;
KEEP PATSC AVAR CAVAR;

PROC SORT DATA = V7; BY PATSC; RUN;
```

# 276 使用 SAS 分析观察性健康数据

```sas
PROC SORT DATA = OUTCV7; BY PATSC; RUN;

DATA ADAT;
MERGE V7 (IN=A) OUTCV7 (IN=B);
BY PATSC;
IF A AND B;

* 分析数据集上的汇总统计 *
PROC MEANS DATA = ADAT7;
CLASS TRT_V5 TRT_V6;
VAR CAVAR;
TITLE2 'ADAT7 的汇总统计'; run;

PROC TABULATE DATA = ADAT7;
CLASS V5 V6;
VAR BAV CAVAR;
TABLES (TRT V5*TRT V6*TRT V7)*(N MEAN STD), (BAVAR CAVAR);
TITLE2 'ADAT7 的汇总统计'; run;

/* 宏的输入包括特定访问的分析数据集
(DATA 2)，包含参数估计的输出数据集名称
(DATA 1)，CLASS 语句的变量列表 (CLASSVAR2)，以及
MODEL 语句中的变量列表 (MODELVAR2)。 */

%MACRO G_ESTS(DATA_2, DATA_1, CLASSVAR2, MODELVAR2);
DS OUTPUT ParameterEstimates =&data_1;
PROC GENMOD DATA=&data_2;
CLASS CLASSVAR2;
MODEL CAVAR = &MODELVAR2 / DIST NOR LINK = ID;
run;
%MEND G_ESTS;
%gests(ADAT7, vis7 OUTCESTS, TRT V5 TRT V6 TRT V7 BIN V5
BIN V6 BIN_PS_V7, TRT_V5 TRT_V6 TRT_V7_ BIN_PS_V5 BIN_PS_V6
BIN_PS_V7);
run;

* 从模型中获取参数估计，以便计算所有转换路径
* 的期望值 *
;

DATA VIS7 OUTCESTS;
SET VIS7 OUTCESTS;
KEEP PARAMETER LEVEL1 ESTIMATE;

PROC TRANSPOSE DATA = VIS7_OUTCESTS OUT=TR_OUTCESTS;
run;

DATA TR OUTCESTS;
SET TR OUTCESTS;
INTERCEPT = COL1;
X1 = COL2; * V5 的 TRT *;
X2 = COL3;
Y1 = COL4; * V6 的 TRT *;
Y2 = COL5;
Z1 = COL6; * V7 的 TRT *;
Z2 = COL7;
```

# 第 11 章 基于纵向倾向评分的回归模型 277



```sas
B1=COL8; B2=COL9; B3=COL10; B4=COL11; B5=COL12; * V5 时的 BIN *;
1=COL13; C2=COL14; C3=COL15; C4=COL16; C5=COL17; * V6 时的 BIN *;
1=COL18; L2=COL19; L3=COL20; L4=COL21; L5=COL22; * V7 时的 BIN *;
run;

DATA OUTC;
SET OUTCOTS;
ARRAY X[2] X1 - X2;
ARRAY Y[2] Y1 - Y2;
ARRAY Z[2] Z1 - Z2;
ARRAY B[5] B1 - B5;
ARRAY C[5] C1 - C5;
ARRAY L[5] L1 - L5;
ARRAY PRE[2, 5, 5];

DO A = 1 TO 2;
  DO J = 1 TO 5;
    DO K = 1 TO 5;
      DO I = 1 TO 5;
        PRE[A, J, I] = COL1 + X[A] + Y[A] + Z[A] + B[J] + C[K] + L[I];
        EOUT = PRE[A, J, I];
        OUTPUT;
      END;
    END;
  END;
run;

DATA OUTC;
SET OUTC;
KEEP A J K EOUT;
run;

PROC SORT DATA = TRPRV7; BY A J K; RUN;
PROC SORT DATA = OUTC; BY A J K; RUN;
PROC SORT DATA = TRPRV6; RUN;

DATA ALL;
MERGE TRPRV7 OUTC;
BY A J K;

DATA ALL;
MERGE ALL TRPRV6;
BY A J K;
EO = EOUT*(2)*TRPR6*TRPR7;
IF A = 1 THEN TRPTTN = 'AAA';
IF A = 2 THEN TRPTTN = 'BBB';

PROC PRINT DATA = ALL;
VAR TRPTTN J I TRPR6 TRPR7;
TITLE 'ALL 数据列表（转换概率与期望结果)';
RUN;
```

# 278 使用 SAS 分析观察性健康数据

## 程序 11.4 的输出

ALL 数据列表（转换概率与期望结果）

| Obs | TRPTTN | J | I | TRPR6 | TRPR7 | EOUT |
|---|---|---|---|---|---|
| 1 | AAA | 1 | 1 | 0.56184 | 0.68756 | -8.5755 |
| 2 | AAA | 1 | 2 | 0.56184 | 0.23807 | -10.9945 |
| 3 | AAA | 1 | 3 | 0.56184 | 0.05502 | -13.0868 |
| 4 | AAA | 1 | 4 | 0.56184 | 0.01534 | -16.5652 |
| 5 | AAA | 1 | 5 | 0.56184 | 0.00301 | -20.6457 |
| 6 | AAA | 2 | 1 | 0.28214 | 0.48647 | -11.0129 |
| 7 | AAA | 2 | 2 | 0.28214 | 0.23564 | -13.5934 |
| 8 | AAA | 2 | 3 | 0.28214 | 0.11345 | -15.5242 |
| 9 | AAA | 2 | 4 | 0.28214 | 0.03687 | -20.2385 |
| 10 | AAA | 2 | 5 | 0.28214 | 0.00997 | -23.9136 |
| 11 | AAA | 3 | 1 | 0.11399 | 0.22977 | -12.3396 |
| 12 | AAA | 3 | 2 | 0.11399 | 0.39809 | -14.7585 |
| 13 | AAA | 3 | 3 | 0.11399 | 0.27402 | -18.2342 |
| 14 | AAA | 3 | 4 | 0.11399 | 0.10530 | -21.5652 |
| 15 | AAA | 3 | 5 | 0.11399 | 0.02180 | -24.4097 |

## 分析步骤 5

这一步利用步骤 3 和 4 的输出来估计我们倾向评分子分类的变异性。具体代码未显示，但简单地创建一个循环来重复该过程 5,000 次并输出生成的治疗差异估计。治疗差异估计的分布由 `PROC UNIVARIATE` 汇总。使用分位数法，得出 95% 置信区间。

## 分析步骤 6

步骤 3 到 5 使用自助算法重复（此处使用了 5,000 次迭代），以估计我们倾向评分子分类的变异性。具体代码未显示，但简单地创建一个循环来重复该过程 5,000 次并输出生成的治疗差异估计。治疗差异估计的分布由 `PROC UNIVARIATE` 汇总。使用分位数法，发现 95% 置信区间为 (-6.91, 1.30)，p 值为 0.185。

# 使用 SAS 进行观察性健康数据分析

## 分析步骤 6 的输出（继续）

### 基础统计量

| 位置 | 变异性 |
| --- | --- |
| 平均值 -2.79781 | 标准差 2.09762 |
| 中位数 -2.79368 | 方差 4.40000 |
| 众数 | 范围 14.18360 |
| | 四分位距 2.28671 |

### 位置检验：Mu=0

| -统计量- | | -p 值 |
| --- | --- | --- |
| 学生 t 检验 | -94.3143 | Pr > |t| < .0001 |
| 符号检验 M | -20.28 | Pr >= |M| < .0001 |
| 符号秩检验 S | -58.78813 | Pr >= |S| < .0001 |

### 分位数（定义 5）

| 分位数 | 估计值 |
| --- | --- |
| 100% 最大 | 4.8827501 |
| 99% | 1.9440237 |
| 95% | 0.6811220 |
| 90% | -0.0468069 |
| 75% Q3 | -1.3916694 |
| 50% 中位数 | -2.7936758 |
| 25% Q1 | -4.2688319 |
| 10% | -5.4935107 |
| 5% | -6.2668682 |
| 1% | -7.6067645 |
| 0% 最小 | -9.3008516 |

### 频率计数

| 值单元 | 百比 | 累积 |
| --- | --- | --- |
| -6.908590145030 | 1 | 0.0 2.5 |
| 1.295101777818 | 1 | 0.0 97.5 |

#### 敏感性 / 模型检查

如所述，使用纵向倾向评分的一个关键特性是我们可以很容易地检查模型的相对有效性。我们提供了 SAS 代码（程序 11.6），以图形化方式描绘结果模型的预测准确性。该代码生成了每个箱治疗组合的预测平均值与实际平均值的散点图——每个圆圈的大小代表纵向子类中的样本量。从输出中，我们注意到了离群值，尽管所有规模合理的子类都得到了模型的良好预测。

为了评估模型的有效性，我们还遵循了第 11.2 节中介绍的两种方法。首先，我们使用 AIC 准则评估了转移模型和结果模型的改进情况。其次，我们仅对研究期间未切换治疗方案的患者子集重新运行了结果模型。AIC 准则可以通过修改 `EST`（程序 11.4）和 `G EST` 宏（未显示）中的 `MODEL (transition and outcome)` 语句来评估。对于这些数据，包含治疗交互作用（例如，访问 5 与访问 6 以及访问 7 的交互作用）以及倾向箱交互作用（例如，访问 5 治疗与访问 5 箱）使得 AIC 略有改善，但该模型的推论是相同的，且模型稳定性较低——自自助评估的方差大得多。因此，我们保留了简单模型的结果。此处也使用了 SAS 代码来评估研究期间未切换治疗方案的患者子集的结果。这是通过修改进入分析宏的数据集实现的。再次，这种方法的推论结果相似。

## 程序 11.6 分析模型的图形化评估

```
****************************************************

** 用于辅助评估的观测与预期结果图 **

****************************************************

PROC MEANS DATA=ADAPT;

  CLASS VAR5 VAR6 VAR7;

  VAR VAR5 VAR6 VAR7;

  OUTPUT OUT=MEANUT N=;

DATA OUT;

  SET MEANUT;

  IF VAR5 = 'T1' AND VAR6 = 'T1' AND VAR7 = 'T1' AND

  VAR5 = 'T2' AND VAR6 = 'T2' AND VAR7 = 'T2' THEN;

PROC PLOT DATA=GRPH;

  PLOT VAR5*VAR6*VAR7*BUBBLE;

RUN;
```



## 使用 SAS 对观察性护理数据进行分析

最近的研究表明，控制良好的观察性研究所产生的结果与随机对照试验相似（Concato 等人, 2000；Benson and Hartz, 2000）。源自回顾性观察性来源的分析在进行调查时，必须考虑一系列局限性和影响因素。由于治疗模式和结局衡量措施仅被观察和测量，研究人员必须克服选择偏倚（或称内生性），因为这种偏倚会影响治疗选择以及产生感兴趣的结局的可能性。除了选择偏倚问题外，使用回顾性数据源（特别是为了研究目的而获取的索赔数据）的研究人员还必须处理其他因素，如数据质量（包括缺失数据）、HIPAA、及时性、适当的操作定义，以及本地编码规范和实践模式。

2000 年，国际药物代谢动力学与结果研究学会（ISOR）成立了一个专家小组，旨在制定回顾性数据研究的良好实践指南。该小组召开了会议，并在美国和欧洲会议上向 ISOR 成员提交了几个版本的清单草稿以征求反馈，最终由 ISOR 董事会于 2002 年发布了该清单。该清单已发布（Mothereal 等人,2003），并可以在网上获取（`http://www.isor.org/paperwork/healthscience/ret_dbFTR203.asp`）。2008-2009 年期间，ISOR 以及美国食品药品管理局（FDA）正在制定关于开展观察性研究的额外指南，以估计源自回顾性数据源的治疗效果。感兴趣的读者应关注这些机构以获取最新指导。本文编写时开发的指南将为读者提供回顾性研究设计和此类研究中常见的统计问题提供更清晰、详细的说明。

本章中的清单代表了一个简版清单，包含了评估回顾性数据库研究时最重要的 10 个要点。该清单包含 27 点，在设计回顾性研究或需要对回顾性数据库进行更详尽、深入的审查（或将其作为期刊引用时）应使用该清单。

研究人员可以使用许多数据库，特别是在美国。由于特定数据库的优和缺点可能存在巨大差异，在进行或审查数据库研究时，评估该数据库是否适用于解决问题，以及研究人员在审查研究结论时是否使用了适当的方法至关重要。虽然该清单是以 10 点的形式编写以指导读者和决策者，但它也可以作为研究人员设计、分析或报告回顾性研究的指南。该清单旨在提出通用问题，而不是提供详细的回顾性建议。这假设读者对通用研究原则已有一定了解，并且根据需要可能需要额外的研究或阅读。这对于涉及统计学的真实评估性问题尤为如此。在使用回顾性数据库时，其他重要问题（包括患者隐私、可信度和研究赞助）未在该清单中讨论。读者应咨询其所属专业学会的指南以及所在机构关于利益冲突、涉及人类受体的研究或其他指南，以了解这些重要问题。本文的其他章节描述了用于实施本章涵盖的一些问题的统计技术和 SAS 编程步骤；但本清单未提供 SAS 编程步骤。

## 第 12 章 开展观察性数据库研究的良好研究规范

### 12.1.1 如何使用该清单？

该清单主要为常用的医疗索赔或基于就诊的数据库开发，但也可能用于评估采用其他类型数据库（如疾病登记和国家调查数据）的回顾性研究。该清单旨在现有经济评估清单的补充（Clemens 等人, 1995；Weinstein 等人, 1996）。只有数据库研究特有的或在数据库研究中特别棘手的问题被纳入清单。并非每个问题都适用于每个研究，但清单应该提示研究人员至少考虑影响研究质量的重要因素。

### 12.2 清单与讨论

| 主题 | 问题 |
| --- | --- |
| 1. 数据库相关性 | 数据库内容和研究人群的描述是否足够详细，以确定使用该数据库回答研究问题的理由，并评估在其他机构的背景下如何解释这些结果？ |
| 2. 数据库质量 | 是否描述了数据的可靠性和有效性，包括任何数据质量检查和对缺失数据的处理？ |
| 3. 研究计划 | 是否制定了先前的研究计划，包括选择特定研究设计的理由，并承认了该设计潜在的局限性？ |
| 4. 样本选择 | 是否使用了纳入和排除标准从初始人群中推导出最终样本，是否描述了这些标准的理由，并讨论了这些标准对样本代表性的影响？ |
| 5. 变量定义 | 是否为选择标准和变量定义提供了理由和/或支持文献，并对具有争议、不确定或新新的定义或标准进行了敏感性分析？ |
| 6. 资源评估 | 对于检查病例的研究，是否描述了资源价值（成本、变化、支付、收费标准）评估的方法和理由，且其是否与研究视角一致？ |
| 7. 混杂 | 如果研究目标是检查治疗效果，是否通过使用比较组以及 i) 多变量统计技术或 ii) 按混杂变量的不同水平对样本分层以比较结果，充分控制了混杂变量？ |
| 8. 统计分析 | 是否使用了适当的统计技术，并考虑了利用和成本数据的特定细微差别，例如人口亚组内部及之间的偏态和相关性？ |

| 主题 | 问题 |
| --- | --- |
| 9. 实际意义 | 是否通过模型的方差和拟合优解释了结果的实际意义？ |
| 10. 理论基础 | 是否为结果提供了理论支持，并讨论了替代解释？ |

**相关性：** 数据库内容和研究人群的描述是否足够详细，以确定使用该数据库回答研究问题的理由，并评估在其他机构的背景下如何解释这些结果？为了适当解释一项研究，应描述关键属性，包括研究概况、可用服务的限制（如社会化医疗）、计划特征和福利设计（例如，医生报销方式、就诊费用分摊、药物排除、心理健康）。对于比较两种药物的经济评估，了解药物的状态以及任何可能影响药物使用的其他福利特征（如阶梯治疗、依从性计划和药物使用计划）至关重要。是否描述了数据的可靠性和有效性，包括任何数据质量检查和对缺失数据的处理？

# 第12章 观察性数据库研究的良好实践规范

- 3. **先验研究计划**：是否制定了先验研究计划，包括选择特定研究设计的理由，并是否承认了该设计的潜在局限性？

使结果向特定方向引导的最简单方法之一是对研究计划或设计进行**事后（post hoc）变更**。在启动研究之前，应该制定一个描述样本标准、变量定义、模型规范和统计方法的研究计划，并描述基于先验计划的结果。自然地，研究人员会通过研究获得新知识，因此考虑事后设计变更也是重要的。研究报告应清晰地描述任何事后决策，并在相关时，同时报告先验计划的结果以及应用任何事后变更后的结果。

研究人员可以采用多种设计（例如，带有对照组的干前干后设计），这些设计根据背景、研究问题和数据具有特定的优缺点。研究人员应为该设计的选择提供理由，并描述该设计的主要优缺点，包括将如何处理潜在的偏差。

- 4. **样本选择**：是否使用入选和排除标准从初始人群中推导出最终样本，是否说明了使用这些标准的理由，并讨论了这些标准对样本代表性的影响？

入选/排除标准是应用于每项研究数据的最低规则，旨在定义研究组。无论使用何种数据库，入选/排除标准都可能剧地改变研究组的组成。是否提供了总人群、样本以及应用每项入选和排除标准后的受人数描述？换句话说，是否清楚排除了多少人以及为什么被排除？

其次，是否讨论了研究入选和排除标准对研究结果的影响，入选/排除标准是否偏置了人群的选择并扭曲了研究结果的适用性？例如，在此期间**持续符合资格**是数据库研究的一项常见标准。然而，在按月定义资格的注册项目中，将研究限制为仅具有持续资格的人员会将镰刀细胞患者包含在内，因为他们很可能一直处于符合保险条件的状况。这在多大程度上影响研究结果的适用性取决于研究问题。

- 5. **变量定义**：是否为选择标准和变量定义提供了理由或支持文献，并对具有争议、不确定或新颖的定义或标准进行了敏感性分析？

需要操作定义来识别病例（受试者）和终点（结果），通常使用诊断代码、药物使用情况和/或手术代码来指示疾病或治疗的存在。应提供所有变量的操作定义，因为不同的定义可能会导致不同的结果和解释。例如，试图识别患有特定疾病（阿尔茨海默病）的人群的研究人员应提供理由，并在可能的情况下引用证据证明某组编码（ICD-9-CM、CPT-4、药物干预）标准是有效的。理想情况下，这种证据应以针对原始数据源进行验证的形式呈现，但更多情况下将涉及引用以往的研究。

当此类定义存在争议性证据或不确定性时，研究人员应使用替代定义进行敏感性分析，以检查这些不同的事件定义方式的影响。敏感性分析测试定义关键指标的不同值或因素组合，以确定定义的差异如何影响结果和解释。数据库允许研究人员以分级方式或即**基于病例的（*caseness*）**进行敏感性分析，即使用不同的定义或确定性水平（例如：确定的、可能的和可能的病例）进行分析。

对于经济评价，一个特别挑战性的问题是识别数据库中与疾病相关的成本。例如，在研究抑郁症时，是仅包含带有抑郁症诊断的服务、带有抑郁症相关代码（例如：焦虑）的服务，还是包含无论伴随诊断代码如何的所有服务？如前所述，对不同操作定义的敏感性分析在这些情况下是非常关重要的。

- 6. **资源估值**：对于检查成本的研究，是否描述了资源估值（成本、费用、付款、收费标准表）的方法和理由，且该方法是否与研究视角一致？

与任何经济评价一样，评审人员应确保分析中包含的资源成本与研究中视角所属的决策者的责任相匹配。例如，如果研究是从保险公司的角度出发，那么资源列表应仅包含将由保险公司支付的资源。

## 294 使用 SAS 进行观察性健康数据的分析

10. 理论基础：是否为提供的结果提供了理论支持？是否讨论了对观察结果的替代性解释？

由于大样本量使得许多在统计学上显著的发现意义存疑，因此研究人员必须提供一种理论（经济、临床、行为等）来解释观察到的结果。因果关系的检验是回溯性研究面临的一项特殊挑战，因为受试者并没有被随机分配到治疗组。因此，在检查两个变量之间的关系时，作者有责任排除对结果的合理的替代性解释。

# 致谢

我们感谢 Fredrik Berggen, James Chan, Mary Ann Clark, Sueellen Curkendall, Bill Edell, Shelah Leader, Marianne McCollum, Newell Elwee 和 John Walt 的努力，他们作为参考小组成员，对早期草稿提供了意见。

# 参考文献

Benson, K., and A. J. Hartz. 2000. “观察性研究与随机对照试验的比较。” 《新英格兰医学杂志》 342(25): 1878–1886.

Clemens, K., R. Townsend, F. Luscombe, et al. 1995. “药物经济学研究的方法论和执行原则。” 《药物经济学》 8(2): I–69–174.

Concato, J., N. Shah, and R. I. Horvitz. 2000. “随机对照试验、观察性研究与研究设计的层次结构。” 《新英格兰医学杂志》 342(25): 1887–1892.

Mothral, B., J. Brooks, M. A. Clark, et al. 2003. “回溯性数据库研究检查清单——ISOR 回溯性数据库工作组的报告。” 《健康价值》 6(2): 90–107.

Stukel, T., A. E. Fisher, D. E. Wemberg, et al. 2007. “存在选择偏倚时的观察性研究分析；使用倾向评分和工具变量法分析侵入性心血管管理对 AMI 存活的影响。” 《美国医学杂志》 297 (3): 278–285.

Weinstein, M. C., J. E. Siegel, M. R. Gold, S. Mark, et al. 1996. “健康与医学成本效益小组的建议。” 《美国医学杂志》 276(15): 1253–1258.

## 第 13 章

## 使用大型医疗数据库进行剂量-反应安全分析

Ouhong Wang
Xiang Ling

- **摘要** ................................................................................................ **295**
- **13.1 引言** ..................................................................................... **295**
- **13.2 数据结构** ................................................................................ **297**
- **13.3 治疗模型与删失模型设置** ............................ **300**
- **13.4 结构模型实现** ....................................... **304**
- **13.5 讨论** ................................................................................ **309**
- **参考文献** ............................................................................................ **310**

## 摘要

边际结构模型（MSM）方法已在第 9 章的传统两组比较设置中介绍。在本章中，将利用大型观察性数据库来演示 MSM 的应用，以评估随时间变化的单一治疗的剂量反应。终点指标是死亡率，这通常是使用此类数据库进行分析的关注点。

## 13.1 引言

### 13.1.1 概述

虽然受控环境下的临床试验通常为长期安全性评估提供了手段，但大规模观察性数据库在处理此类数据时至关重要，因为数据几乎无例外地受到混杂影响。在本章中，边际结构模型（MSM）方法被用于分析此类数据库。终点是死亡率，这是使用此类数据库进行分析的常见重点。该方法（MSM）通过使用治疗概率权重创建一个伪随机的人群，以研究促红细胞生成素（Epoetin）剂量的关联性。这种方法展示了如何利用数据库来研究促红细胞生成素剂量与死亡率之间的关系。该数据库包含了能够消除混杂的变量。我们介绍了一些关于终末期肾脏疾病（ESRD）、贫血和治疗的背景信息。接下来，我们将详细描述用于分析的数据库及其结构。遵循第 9 章介绍的技术细节，我们随后描述治疗模型的设置、删失模型以及用于分析的结构模型。文中包含了 SAS 代码和主要输出。基于这些输出解释结果，并对使用 MSM 分析提供一些注意事项。

### 13.1.2 疾病、治疗与分析背景

患有肾病的患者几乎总是伴有贫血这一并发症。这是促红细胞生成素，一种调节红细胞产生的蛋白质，它产生于肾脏。终末期肾脏疾病会导致产生减少。ESA 是通过重组 DNA 技术制造的蛋白（Epogen，Amgen 公司，加州奥克兰市）。人们周知，病情严重的患者血蛋白水平较低，可能会接受较高剂量的促红细胞生成素治疗。这是一个治疗混杂问题。此外，观察到的血蛋白水平影响促红细胞生成素剂量，反之亦然。为了维持血蛋白水平，需要定期调整促红细胞生成素的剂量。正正如第 9 章提到的，在这种情况下，随时间变化的 Cox 比例风险模型没有因果解释，因为由于混杂的存在，因果解释所需的假设并不成立。为了评估促红细胞生成素剂量与死亡率之间的因果关系，需要更复杂的方法，我们使用了边际结构模型作为替代（Robins, 2000; Hernán et al., 2000）。

我们从一家透析链获得了医疗记录。该透析链收集的患者数据根据隐私使用协议供我们使用。数据包括患者人口统计学、ESA 剂量、血蛋白水平和并发症。已经利用透析链进行了许多分析以了解治疗效果并改善患者护理。注意，第 9 章讨论了另一个演示 MSM 应用的示例。然而，本章的不同在于这里的结局是生存。我们讨论的是不同剂量的单一治疗，而不是两个治疗组，而且重点是剂量反应，而不是两个治疗组之间的比较。

## 13.2 数据结构

在深入 MSM 分析细节之前，让我们先了解手头的数据。该透析链为全美 10 万多名患者提供血液透析服务，并收集了实验室参数、药物、人口统计学特征、透析护理以及临床结果（包括住院和死亡）。对于本分析，数据来自 60,000 名血液透析患者的随机样本，这些患者年龄至少为 18 岁，无腹膜透析史，且在 2000 年 7 月至 2002 年 6 月之间接受了至少 1 个月的血液透析。我们将研究人群限制为首次出现在

该数据库建立于2001年1月之前，患者拥有6个月的基线期，以便进行患者表征。患者随访了12个月。

收集了大多数实验室参数（例如：白蛋白、铁蛋白、血转铁蛋白饱和度 [TSAT]）；在机构中，血红蛋白值的采集频率更高（每月约两次）。收集了促红生成素α (EPO) 和铁剂剂量（在每次给药时记录）、人口统计学特征（在患者开始透析时记录）以及透析信息（包括尿素比例 (RUR)、透析就诊次数和血管入路类型）。持续收集了住院数据，包括根据国际疾病分类第9修订版 (ICD-9) 代码的入院和出院日期。常规收集了死亡信息，失访原因包括肾移植、机构转院和透析方式的改变。

我们每隔2周评估一次促红生成素α，以保持与通常的血红蛋白（Hb）评估频率一致。在每个间隔内，我们计算了累积门诊促红生成素α剂量（在透析机构记录的所有可用剂量之和）。住院环境中未捕获促红生成素α剂量信息，因此我们无法获得这些数据。为了本分析，我们使用住院前的最后一次剂量推补了住院促红生成素α治疗剂量。

选择此数据库进行分析而非其他选项（例如通过医疗保险收集的美国肾脏数据系统 [USRDS] 数据）的原因是，促红生成素α剂量信息在每次给药时可用，且所有评估的血红蛋白值都用于其他分析；此外，这些数据包含更多变量的更多观测值，并且通常提供了关于患者状况、治疗因素以及医生在制定剂量决策时使用的变量更全面的视角。在应用倾向评分模型 (MSM) 时，这是一个重要的考虑因素，因为未测量混杂因素假设是因果推断的关键假设。

本分析使用的实际 SAS 数据库每个患者-时间点有一条记录。通过相应的数据库（每个患者一条记录）使用程序 13.1 评估患者特征，以提供患者人群的基本情况。SAS 输出非常长，因此没有显示 SAS 输出，而是将结果汇总在表 13.1 中作为更简洁的替代方案。连续变量以均值（标准差）形式表示，分类变量以计数（频率）形式表示。注意，摘要是按剂量类别（剂量四分位数或基线剂量四分位数，加上零剂量组）提出的，后文将进行详细解释。

## 第13章 使用大型医疗保健数据库进行剂量反应安全性分析 299

## 程序 13.1 患者特征摘要

```sas
*** 计算连续变量的均值；

proc means data=demo_mean;
```



`var AGE HEMODIALYSIS BMI BLERS BLALB HLHGB;by bydosequartile;`

`OUTPUT=mean MEAN-AGE HEMODIALYSIS BMI BLERS BLALB HLHGB;`

`run;`

```sas
*** 计算连续变量的标准差；
proc means data=demo_stdde;
var AGE HEMODIALYSIS BMI BLERS BLALB HLHGB;by bydosequartile;
OUTPUT=out~stdde stddev=AGE HEMODIALYSIS BMI BLERS BLALB HLHGB;
run;
```

```sas
*** 计算分类变量的计数和频率；
proc freq data=demo;
table AGEGROUP/out=a;
table ETH/out=b;
table SEX=out=c;
table REGION/out=d;
table BLHYPERTENS/out=e;by bydosequartile;
run;
```

我们的患者人群中未找到类似的代码。

### 表 13.1 患者人口统计学和基线特征

| | 剂量 0 | 剂量 1 | 剂量 2 | 剂量 3 | 剂量 4 | 全部 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| N | | 304 | 5544 | 7904 | 5703 | 27791 |
| 年龄 (岁) | | 54.77 (13.99) | 61.01 (15.01) | 61.8 (15.08) | 60.51 (14.73) | 58.13 (14.74) | 60.43 |
| 透析年限 (年) | | 4.95 (2.77) | 3.44 (4.01) | 2.66 (3.28) | 2.49 (3.36) | 2.86 (3.3) | 3.2 |
| BMI (kg/m²) | | 27.08 (8.07) | 26.17 (10.69) | 26.37 (14.65) | 27.17 (17.15) | 28.27 (7.9) | 26.98 |
| 铁蛋白 (ng/ml) | | 500.8 (32.9) | 591.8 (30.7) | 527.4 (34.5) | 478.8 (43.6) | 450.1 (31.5) | 514.2 (35.8) |
| 基线 TSAT (%) | | 31.54 (10.24) | 32.08 (9.86) | 29.12 (9.17) | 24.68 (8.9) | 24.33 (9.32) | 27.97 (9.33) |
| 基线白蛋白 (g/dl) | | 3.88 (0.29) | 3.98 (0.86) | 3.83 (0.33) | 3.76 (0.36) | 3.66 (0.39) | 3.79 (0.36) |
| 基线 Hb (g/dl) | | 12.9 (1.31) | 12.11 (1.89) | 11.99 (1.86) | 11.63 (0.88) | 11.01 (1.07) | 11.69 (1.07) |
| 年龄 < 45 岁 | | 83 (23) | 83 (31) | 115 (15.9) | 140 (13.4) | 156 (11.3) | 4480 (16.1) |
| 年龄 45-65 岁 | | 138 (45.1) | 281 (39.3) | 2896 (30.3) | 3096 (24.2) | 2482 (43.5) | 10974 (39.5) |
| 年龄 > 65 岁 | | 83 (23.3) | 252 (48.7) | 3876 (49.2) | 3728 (44.7) | 4197 (50.3) | 2908 (51.1) | 12337 (44.4) |
| 黑人 | | 128 (42) | 2062 (37.2) | 3053 (55.4) | 3548 (62.6) | 2778 (48.7) | 11445 (41.5) |
| 中西部地区 | | 12 (4.8) | 756 (9.8) | 1277 (16.2) | 1450 (17.4) | 1111 (19.5) | 4815 (17.3) |
| 南部地区 | | 184 (60.5) | 3226 (58.2) | 4847 (61.3) | 5265 (63.2) | 3595 (63.3) | 17117 (61.6) |
| 西部地区 | | 31 (10.2) | 903 (16.3) | 1022 (12.9) | 780 (9.4) | 429 (7.5) | 3165 (11.4) |
| 高血压 | | 42 (13.8) | 729 (13.1) | 1170 (14.8) | 1343 (16.1) | 997 (17.5) | 4281 (15.4) |
| 糖尿病 | | 116 (38.2) | 2630 (47.4) | 4087 (51.1) | | | |

## 13.3 治疗模型与筛选模型设置

我们使用边际结构模型 (`MSMs`) 估计了风险比，其中使用了逆概率加权 (`IPTW`) 来调整偏倚。这种两步法首先通过治疗模型计算预测效应的倒数权重，然后使用加权结构模型计算风险比。具体而言，`IPTW` 降低接受低于预测量的患者的权重，并增加接受高于预测量的患者的权重。加权创建了一个消除治疗指示与实际治疗之间关联的伪人群。因此，只要权重建模准确且满足足够的假设，基于该伪人群的风险比就可以具有因果解释 (`Robins, 2000`)。

## 程序 13.2 治疗权重计算

# 第13章 使用大型医疗数据库进行剂量-响应安全分析 301

```sas
/ dist=multinomial link=clogit;
out out=preds pred=pred;
run;
```

```sas
proc sort data=preds;
by patient biweekno dosequartile _order_;
run;
```

```sas
proc transpose data=preds out=predst(keep=patient theta1 theta2 theta3
theta4 biweekno dosequartile) prefix=theta;
by patient biweekno dosequartile;
id _order_;
var pred;
run;
```

```sas
data modell;
set preds;
prob1=theta1;
prob2=theta2-theta1;
prob3=theta3-theta2;
prob4=theta4-theta3;
prob5=1-theta4;
if dosequartile=1 then treat_top=prob1;
elif dosequartile=2 then treat_top=prob2;
elif dosequartile=3 then treat_top=prob3;
elif dosequartile=4 then treat_top=prob4;
elif dosequartile=5 then treat_top=prob5;
keep patient biweekno dosequartile treat_top;
run;
```

*** 分母部分，包括基线协变量、随时间变化的截距以及任何随时间变化的协变量：

```sas
proc genmod data=infile order=format-formatted;
class SEX REG VITDFLAG GLU BLAC CDYSINOSOP HYPERPERTENS
BLHAXDADEQUACY dosequartile lagdosequartile lag2dosequartile
l3dosequartile lag4dosequartile lag5dosequartile
HYPERPERTENS LAG1HADADEQUACY LAG1VASCULAR;
model dosequartile=SEX REG VITDFLAG GLU BLAC
CDYSINOSOP HYPERPERTENS BLHAXDADEQUACY BMI HEMODIALYSIS
NOCHHODES NOCHHODEAQUACY BLUGS BLIRON BLALF BLBER BLSLAT
BLTHF dosequartile dosequartile lag2dosequartile
l3dosequartile lag4dosequartile
lag1hb lag2hb lag3hb lag4hb
HYPERPERTENS lag1DEQUACY LAG1VASCULAR lag1NHSPDNUM
laghospitaldays lag1iron lagislat lagalbl lagal lag lagfer
lag1hbdose0 lag1hbdose1 lag2hbdose2 lag3hbdose3 lag4hbdose4
/ dist=multinomial link=clogit;
out out=preds pred=pred;
run;
```

```sas
proc sort data=preds;
by patient biweekno dosequartile _order_;
run;
```

```sas
proc transpose data=preds out=predst(keep=patient theta1 theta2 theta3
theta4 biweekno dosequartile) prefix=theta;
by patient biweekno dosequartile;
id _order_;
var pred;
run;
```

# 302 使用 SAS 分析观察性健康数据

```sas
data model12;
 set predat;
 prob1=theta1;
 prob2=theta2-theta1;
 prob3=theta3-theta2;
 prob4=theta4-theta3;
 prob5=1-theta1;
 if dosequartile=1 then treat_bottom=prob1;
 else if dosequartile=2 then treat_bottom=prob2;
 else if dosequartile=3 then treat_bottom=prob3;
 else if dosequartile=4 then treat_bottom=prob4;
 else if dosequartile=5 then treat_bottom=prob5;
 keep patient biweekno dosequartile treat_top;
 run;
data trtmmodels;
 merge modell (keep=patient biweekno treat_top)
 model2 (keep=patient biweekno treat_bottom)
 by patient biweekno;
 if nmiss(treat_top, treat_bottom)>0 then treat_sw=1;
 else if nmiss(treat_top, treat_bottom)=0 then
 treat_sw=treat_top/treat_bottom;
;
```

在通常的 `MSM`（边际评分模型）实现中，每个时间点的权重是通过乘以该时间点之前研究的所有权重来聚合的。正如想象的，与后期时间权重相关的变异性变得越来越大。这些权重在图 13.2 中进行了汇总和说明。

# 图 13.2 MSM 权重
img/fe9ff00f88baacd41548b025dd58c316_png

# 第13章 使用大型健康数据库进行剂量-响应安全分析 303

在涉及可滴定药物的复杂治疗方案中，由于患者的异常特征、不传统的治疗决策、数据评估的高度变异性甚至数据记录错误，权重的删失部分很大。由于权重是累积的，模型的不完善可能会导致后期时间点的权重再次相乘。为了防止分析被少数几个大权重主导，在我们的 `MSM` 实现中，聚合权重仅基于前四个间隔计算，而不是针对所有时间点。这种变动具有稳定权重的作用，如图 13.3 所示。注意在双周期间的范围较小且分布均匀。我们还将最高权重截断至第 98 百分位数或第 99 百分位数。通过排除会影响模型的极少数离群值，我们能够提高使用 `MSM` 进行风险比估计的性能。

# 图 13.3 修改后的 MSM 权重
img/fe9ff00f88baacd41548b025dd58c317_png

# 程序 13.3 删失权重

*** 计算权重的删失部分；
*** 分子部分，包括基线协变量和随时间变化的截距；

```sas
proc logistic data=infile;
class lagdosequartile lag2dosequartile lag3dosequartile
lag4dosequartile bdosequartile ETH SEX REGION VITDFAG GLU
INHOSP HYPERPERTENS BLHXADEQUACY;
  model censored = lagdosequartile lag2dosequartile
  lag3dosequartile lag4dosequartile bdosequartile ETH SEX REGION
  VITDFAG GLU INHOSP HYPERPERTENS BLHXADEQUACY AGE BMI
```

# 304 使用 SAS 分析观察性健康数据

```sas
HEMODIALRS NOCHDDOSES NOHDDOSES PERLESS11 BLHGB BLIRON BLABLB
BLERS BLSAT BLPF theta1 theta2 theta3;
output out=model3 p=censored_top;
run;
```

*** 分母部分，包括基线协变量、随时间变化的截距以及随时间变化的协变量：

```sas
proc logistic data=infile;
class SEX REGION VITDFAG GLU BLAC CDAYSINOP HYPERTENSN
BLADEQUART bdosequartile lagdosequartile lag2dosequartile
lag3dosequartile lag4dosequartile HYPERTENSQUACY lag1VASCULAR;
model censored = SEX REGION VITDFAG GLU BLAC CDAYSINOP
HYPERTENSN BLADEQUART AGE BMI HEMODIALRS NOCHDDOSES
NOHDDOSES PERLESS11 BLHGB BLIRON BLABLB BLERS BLSAT PF
dosequartile lagdosequartile lag2dosequartile lag3dosequartile
lag4dosequartile lag2h lag2h lag3h;
output out=model4 p=censored_bottom;
run;
```

```sas
data censmodels;
merge merge13 (keep=patient biweekno censored_top)
model14 (keep=patient biweekno censored_bottom) ;
by patient biweekno;
if nmiss(censored_top, censored_bottom)>0 then censored_sw=1;
if nmiss(censored_top, censored_bottom)=0 then
censored_sw=censored_top/censored_bottom;
run;
```

## 13.4 结构模型实现

结构模型是 `MSM` 实现中的第二步。因果推理通过加权平均进行。在我们的数据库中，评估的临床结局是死亡，需要生存分析来估计其与剂量的关系。在 `SAS` 中的实际实现是通过 `PROC GENMOD`，因为 `PROC PHREG` 不处理变量。通过 `PROC GENMOD` 的广义估计方程 (`GEE`) 方法用于风险比点估计。这些估计的置信区间必须通过自助法获得，而不是直接使用 `PROC GENMOD` 生成的区间。将在以后详细讨论。

# 第13章 使用大型医疗保健数据库进行剂量-反应安全性分析

在住院期间存活的情况下，吸入剂量促红蛋白 Epoetin alpha 的剂量使用住院前最近一次的剂量进行填充。

程序 13.4 使用 `GEE` 实现了结构模型。

## 程序 14.3 分析模型

```sas
proc genmod data=allmodels descending;
  class patient ETH SEX REGION VITFLAG GL BLUVAC CAYSINHOSOP
  HYPERTENSION BLHDAQUAGE blosequartile;
  model die = ETH SEX REGION VITFLAG GL BLUVAC CAYSINHOSOP
  HYPERTENSION BLHDAQUAGE AGE BMI HEMODIOLARS NOCHDOSES
  NODLHODES PERLESSL HLBHG BLIRON BLAL BLFER BLAT LPTH
  blosequartile epoch2 epoch3 epoch4 hmtno0 hmtno1 hmtno2 hmtno3
  /link=code dist-bin;
  scwt wgt;
  repeated subject-type/pind;
run;
```



## 程序 13.4 的输出

| GEE 参数估计分析 | 经验标准误估计 | | | | |
| 参数 | 估计 | 误差 | 95% 置信区间 | Pr > |Z| | |Z| |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 截距 | 0.7441 | 2.178 | -3.3871 | 4.8753 | 0.35 | 0.7241 |
| Eth | 0.0370 | 0.0853 | -0.1398 | 0.2473 | 3.60 | 0.0003 |
| Sex | 0.0000 | 0.0000 | 0.0000 | 0.0000 | | | |
| 0 | -0.1429 | 0.0625 | -0.2653 | -0.0205 | -2.29 | 0.0221 |
| region | 0.0000 | 0.0000 | 0.0000 | 0.0000 | | | |
| MIDWEST | 0.2399 | 0.0168 | -0.0573 | 0.5551 | 1.49 | 0.1358 |
| NORTHEST | 0.0680 | 0.0153 | -0.2138 | 0.3678 | 1.44 | 0.5664 |
| SOUTH | 0.0213 | 0.0144 | -0.0411 | 0.4601 | 2.25 | 0.0224 |
| WEST | 0.0000 | 0.0000 | 0.0000 | 0.0000 | | | |
| vitflag | -0.0684 | 0.0711 | -0.2077 | 0.0709 | -0.96 | 0.3359 |
| 1 | 0.0000 | 0.0000 | 0.0000 | 0.0000 | | | |
| glu | -0.3425 | 0.0686 | -0.4769 | -0.2080 | -4.99 | <0.0001 |
| 1 | 0.0000 | 0.0000 | 0.0000 | 0.0000 | | | |
| bluvac | | | | | | | 1.60 | 0.1092 |
| flbica | 0.2181 | 0.0957 | -0.4057 | -0.0305 | -2.28 | 0.0227 |
| blvac | 0.0000 | 0.0000 | 0.0000 | 0.0000 | | | |
| caysinHOSOP | -0.0154 | 0.0416 | -0.1234 | 0.2234 | -4.45 | <0.0001 |
| 1 | -0.3525 | 0.0199 | -0.5876 | -0.1174 | -2.94 | 0.0033 |
| caysinHOSOP | 0.0088 | 0.0140 | -0.1890 | 0.3660 | 0.61 | 0.5405 |
| 1 | 0.0000 | 0.0000 | 0.0000 | 0.0000 | | | |
| HYPERTENSION | -0.0000 | 0.0000 | 0.0000 | 0.2242 | -0.02 | 0.9838 |
| 1 | 0.0000 | 0.0000 | 0.0000 | 0.0000 | | | |
| BLHDAQUAGE | 0.0998 | 0.0895 | -0.0757 | 0.2753 | 1.11 | 0.2650 |
| 1 | 0.0000 | 0.0000 | 0.0000 | 0.0000 | | | |
| age | 0.0303 | 0.0027 | 0.0249 | 0.0237 | 11.02 | <0.0001 |
| bmi | -0.0069 | 0.0061 | -0.0413 | 0.0117 | -4.8 | <0.0001 |
| hemodialysis | 0.0174 | 0.0067 | -0.0004 | 0.0304 | 5.55 | <0.0001 |
| nochdoses | -0.0110 | 0.0102 | -0.0331 | 0.0090 | -1.08 | 0.2860 |
| nodlhodes | 0.0009 | 0.0135 | -0.0225 | 0.0273 | 0 | 0.9449 |
| perless | -0.0035 | 0.0028 | -0.0116 | 0.0020 | -1.25 | 0.2112 |
| hlbhg | -0.1621 | 0.0834 | -0.3255 | 0.0193 | -1.94 | 0.0519 |
| bliron | -0.0007 | 0.0003 | -0.0013 | -0.0001 | -2.12 | 0.0337 |
| blalb | -0.9552 | 0.0907 | -1.1330 | -0.7775 | -10.53 | <0.0001 |

## 程序 13.4 的输出（续）

```sas
ifer | 0.0002 | 0.0001 | 0.0000 | 0.0071 | 2.42 | 0.155
lsat | -0.0052 | 0.0063 | -0.0176 | -0.83 | 0.4050
pth | 0.0004 | 0.0001 | 0.0002 | 0.0007 | 3.75 | 0.0002
bldosesquare 0 | 0.0562 | 0.5130 | -0.4362 | 1.5746 | 1.11 | 0.2671
bldosesquare 1 | -0.2165 | 0.0179 | -0.1256 | 0.5225 | -1.25 | 0.236
bldosesquare 2 | -0.2756 | 0.1196 | -0.5100 | -0.0412 | -2.30 | 0.0221
bldosesquare 3 | -0.2755 | 0.0908 | -0.4533 | -0.0976 | -3.03 | 0.0024
bldosesquare 4 | 0.0000 | 0.0001 | 0.0000 | 0.0000 | 0 | 0.0000
epoq1 | 0.0678 | 0.0050 | -0.0167 | 0.2522 | 0.72 | 0.4714
epq2 | 0.1923 | 0.1087 | -0.0208 | 0.4054 | 1.77 | 0.0170
epoq3 | 0.3292 | 0.1378 | 0.0590 | 0.5994 | 2.13 | 0.0169
epoq4 | 0.4465 | 0.0130 | -0.1265 | 1.8533 | 2.00 | 0.0608
hmno0 | -0.0094 | -0.0291 | -0.0886 | 0.1019 | -0.93 | 0.3515
hmno1 | 0.5253 | 0.4379 | -0.3370 | 1.3837 | 1.20 | 0.3030
hmno2 | -1.4338 | -1.2605 | 0.3166 | 0.7182 | -1.21 | 0.0258
hmno3 | 1.5701 | 1.1024 | -0.5906 | 3.7308 | 1.42 | 0.1544
```

结果汇总在表 13.2 中。注意，程序 13.4 输出中的估计值（Estimate）经过指数化处理以获得表 13.2 中的风险比点估计。例如，`epoq2` 的 0.0678 值经过指数化后，得到表 13.2 中全模型第二四分位的 HR 值 1.07。

## 表 13.2 不同模型和不同权重重的风险比估计

| 治疗模型* | 权重水平 | 最大权重 | 零剂量 | EPO 四分位数 |
| :--- | :--- | :--- | :--- | :--- |
| | | | 1st | 2nd | 3rd | 4th |
| 简单 | 22% | 32 | 1.69 (1.06, 2.39) | 1.09 (0.94, 1.35) | 1.27 (1.02, 1.56) | 1.51 (1.08, 1.89) |
| 扩展 | 24% | 28 | 1.62 (1.16, 2.09) | 1.24 | 1.49 | 1.49 (1.22, 1.91) |
| 全量 | 22% | 82 | 1.56 (0.98, 2.02) | 1.07 | | |

```sas
proc sort data=sample;
by rec;
run;

proc freq data=sample noprint;
table rec/out=norecs (keep=rec count);
run;
```

```sas
*** unique sample;
data uniquesample;
set sample;
by rec;
if first.rec;
selected=1;
run;
```

```sas
data infile2;
set &infile;
by pat;
retain rec;
if n=1 then rec=0;
if first.pat then rec+1;
run;
```

```sas
data mysample;
merge infile2 (in=one) uniquesample (in=two);
by rec;
if one and two;
run;
```

```sas
data mysample;
set mysample;
pat2=pat;
run;
```

```sas
*** subjects sampled more than once;
data extrapolates;
merge infile2 (in=one) norecs (in=two where=(count>1));
by rec;
if one and two;
run;
```

```sas
proc sort data=extrapolates;
by pat;
run;
```

```sas
*** subjects sampled more than twice;
data extrapolates;
set extrapolates;
retain irec;
if n_=1 then irec=0;
exrecs=count-1;
do i=1 to exrecs;
index=i;
irec=irec;
selected=1;
pat2=pat+(0.0001*i);
output;
end;
drop i exrecs;
run;
```

# 第 13 章 使用大型医疗数据库进行剂量-反应安全性分析 309

```sas
proc sort data=-extrapats3;
  by pat biweekno;
  run;
data &out;
  set msample extrats3;
  drop pat;
  run;
proc sort data=&out(rename=(pat2=pat));
  by pat biweekno;
  run;
%bootstrap
%bootstrap(studyperioddata, newstudydata);
```



表 13.2 中的风险比具有较宽的置信区间，反映了在估计随 EPO 剂量增加的相对死亡风险时的相当不确定性。还需要注意，随着分位数的增加，置信区间变得更宽，这表明在高剂量下混杂是一个问题。

简单模型与完全模型之间的区别在于我们细粒数据库中提供的额外变量。这些变量在其他数据库中通常不可用（例如，住院天和医院 EPO 使用情况）。在分析中，我们尝试在保持 MSM 实现的所有其他方面不变的情况下，检查这些额外变量对 MSM 分析的影响。如表 13.2 所示，这些额外数据的影响使得对 EPO 剂量的预测更好，从而为 MSM 生成了更准确的权重。例如，在简单模型的基础上引入完全模型的额外数据，第四季度的风险比估计值从 1.15 降至 0.98。

基于扩展模型和完全模型与简单模型相比，风险比逐渐向零值（null）移动的事实，我们假设数据的可用性或粒度可能与由于模型设定错误导致的残差混杂量有关。也就是说，简单模型中缺乏解释变量无助于减少混杂问题，而在扩展模型中包含更多变量可以减少混杂，从而使我们能够生成更真实的风险比估计值。

值得注意的是，对于这一特定应用，如果截断后的最大权重相似，则风险比估计值在很大程度上也是的，这表明控制由于模型设定错误导致的权重离群值非常重要。换句话说，通过权重截断来控制最大权重似乎是减轻模型设定错误风险的一种有效方法。

## 13.5 讨论

本章介绍了使用 MSM（边际结构模型）从大型医疗数据库评估安全性信息（特别是死亡率）的示例。医疗数据库通常规模庞大且数据元素丰富，与小型临床试验相比具有巨大优势。它们也是在现实环境中收集的，与临床试验相比，反映了更多的真实实践数据。另一方面，缺乏随机化和严格控制使得数据库容易受到混杂影响。有时这种混杂是随时间变化的，且严重到足以

# 310 使用 SAS 进行观察性护理数据分析

使得传统的评估剂量关系的分析失效。在处理此类问题时，应该考虑更复杂的方法，如边际结构模型、结构嵌套模型和工具变量。然而，这些方法在过去的几十年中才被引入，尚未广泛使用。本章的目的是为普通统计学家提供这些方法。在接受结果之前，对任何统计假设都进行了仔细检查。这对于 MSM 尤为如此，因为。

# 参考文献

- Bány, P., Divino, J., and Bergström, J. (1997). High-reactive protein predicts mortality. Epidemiology, 11, 550–560.
- Bradbury, B., and Wang, C. (2008). Prevalence of epoetin in hemodialysis. Nephron, 29, 565–568.
- Cotter, J., Stefan, K., Zhang, M., and Kaufman, D. (2004). Epoetin requirements to predict mortality in hemodialysis. American Journal of Kidney Diseases, 44(5), 866–876.
- Feldman, H., Joffe, J., et al. (2004). Administration of erythropoin-stimulating agent and survival. Journal of the American Society of Neph, 15, 223–232.
- Hernán, A., and Brumback, B. (2000). Marginal structural models and causal inference. Epidemiology, 11, 550–560.
- Kausz, M., Boll, A., and Pereira, A. (2005). Clinical significance of C-reactive protein in patients on hemodialysis: a longitudinal study. Nephron, 100, c140–145.
- Regidor, D., Kopp, D., et al. (2006). Associations between injectable vitamin D and hemodialysis survival. Kidney International, 66(6), 2429–2436.
- Roberts, T. L., Ster, W., and Pereira, A. (2004). Relationship between catheter insertions, vascular infections, and anemia. Journal of the American Society of Nephrology, 17(4), 1181–1191.
- Roskert, J., Gassmann-Meier, D., and Frey, W. (2007). Prevalence of epoetin-responsive. Nephology Transplantation, 22, 794–800.
- Rothman, K. J., and Worthsworth, C. E. (2003). Mortality of cystic fibrosis treated with tobramycin. Epidemiology, 14(1), 55–59.
- Teng, M., Wolf, M., and Ofsthun, M. N., et al. (2005). Activated vitamin D and hemodialysis survival. Journal of the American Society of Nephrology, 16(4), 1115–1125.
- Teruel, J. L., Marcen, R., Ocana, J., and Fernandez-Lucas, M., et al. (2005). Clinical significance of C-reactive protein in patients on hemodialysis: a longitudinal study. Nephron, 100, c140–145.

# 第五部分

# 药物经济学

- **第14章** 使用倾向评分分箱自助法进行成本与成本效益分析...........................................................315
**第15章** 增量净收益 ................................................................................339
**第16章** 基于删失数据的成本与成本效益分析为......363

# 使用倾向评分分箱自助法进行成本与成本效益分析

Douglas E. Faries
Xiaomei Peng
Robert L. Obenchain

- 摘要 ............................................................................................................ 315
14.1 引言 ..................................................................................................... 315
14.2 倾向评分分箱自助法 ............................................................ 319
14.3 示例：精神分裂症疗效研究 ........................................................ 320
14.4 讨论 ...................................................................................................... 334
参考文献 ................................................................................................................ 335

## 摘要

在当今的经济环境下，成本和成本效益数据的分析对于医疗保健决策者来说变得越来越重要。倾向评分分箱自助法（Propensity score bin bootstrapping）是一种新的分析方法，旨在解决观察性成本数据分析中的三个基本挑战：

1. 成本分布的典型偏态性
2. 需要估计均值而非位数或其他稳健指标
3. 需要调整选择偏倚

在本章中，将介绍用于分析成本数据的各种方法论的概述，并提供了 SAS 代码来执行倾向评分分箱自助分析，以比较竞争性干预措施的平均成本和成本效益。

# 14.1 引言

## 14.1.1 概述

随着美国医疗保健成本的不断增长，成本和成本效益分析已成为医疗决策的关键因素。例如，医疗保健支付者对比较两种或两种竞争性治疗方案的总体成本等分析有着浓厚兴趣。然而，比较组间成本数据的适当分析可能是复杂的，因为它必须处理数据中潜在的偏态性、均值估计，并对重要的基线治疗差异进行调整。

医学研究的成本数据通常是偏态的，因为一部分患者可能由于资源密集型治疗（如住院）而产生极高的成本，而另一部分患者效果良好，使用的医疗资源较少。其次，中位数和修剪均值通常用于描述具有离群值人群的中心趋势统计量。遗憾的是，对于支付者对患者产生的所有成本的责任，这些衡量具有误导性且不精确。平均成本更具相关性，因为人数乘以平均成本代表总负债（Ramsey et al., 2005; Doshi et al., 2006）。最真实的（可推广的）成本数据通常来自自然主义研究。随机临床试验使用具有计划的医疗保健提供者随访（访次通常比实际操作更频繁）、免费获取资源、严格的入组标准和强制性合从的方案。所有这些问题都影响了临床试验成本估算的可推广性（Grimes and Schulz, 2002; Revicki and Frank, 1999）；Roy-Byrne et al., 2003）。另一方面，缺乏治疗随机化的自然主义研究会受到基线特征的治疗选择偏倚的影响，这在分析中需要予以考虑（Rosenbaum and Rubin, 1983）。

发表的文献中出现了几种成本数据处理方法（Doshi et al., 2006）：

- t 检验/方差分析（ANOVA）
- 基于秩的非参数检验
- 转换方法
- 广义线性模型
- 自助法（bootstrapping）

在本章中，我们回顾了经济数据分析和报告的指南，简要回顾了常用方法论，介绍并讨论了一种新方法——倾向评分分箱自助法（PSBB），并使用 SAS 软件演示了精神分裂症试验中成本数据的分析。鉴于存在多种方法，且每种方法的有效性都基于不同的假设，研究人员理解并评估成本背后的假设、进行适当的敏感性分析并在展示工作时保持透明是至关重要的。这将使消费者能够充分评估结果的稳健性，并在决策中正确利用这些信息。

最后，医疗决策者经常面临……（注：原文此处存在大量重复文本，译文已按要求去重并终止）。

## 14.1.2 经济指南

尽管存在这些指南，但近期对所用方法的系统分析揭示了质量应用的不一致性。Doshi 等同事（2006）评估了 MEDLINE 数据库中 115 篇报告中使用的统计方法。他们得出结论，大多数经济分析中所使用的统计方法质量较差。例如，超过 40% 的研究未报告结果的不确定性估计，而少于 25% 进行统计比较的研究使用了非参数均值估计（例如非参数自助法）。

## 14.1.3 当前方法论概述

## 318 使用 SAS 对观察性护理数据进行分析

比较组间成本的常用简单方法是将数据进行转换以解决偏态，并使用对数、平方根或其他转换对数据进行归一化。标准正态统计方法（如 t 检验和方差分析 ANOVA）可用于比较各组。这种方法可以利用 SAS 函数（例如 `LOG` 函数）、`PROC GLM` 或 `PROC MIXED` 轻松实现。然而，除非满足某些假设，否则转换方法可能会导致误导性结果。一个明显的假设是转换产生了正态性（或至少满足了中心极限定理）。虽然这可能不那么明显，但实际上更重要的是标准检验统计量必须考虑到每个治疗组转换后成本的方差。

为了说明这种基本的困难性，假设将高获取成本的治疗 H 在基准成本上与低获取成本的治疗 L 进行比较。在任何固定时间内的总累积成本分布的低端（左侧））将由接受治疗 L 的患者主导。H 能够在成本上与 L 有效竞争的唯一方法是 H 相较于 L 减少高累积成本的概率。换句话说，总累积成本的高端（右侧）分布随后可能由接受治疗 L 的患者主导。为了保持平均成本的竞争力，治疗 H（必须）减少累积成本的方差。显然，如果成本分析师未能检查这些分布并可能假设方差是相等的，那么治疗 H 将处于极不公平的优势。

当方差不相等时，转换后的均值（均值是初始成本尺度上均值和方差的函数）比较可能会产生严重的偏差结果。这解释了文献中广泛讨论的重构问题（Duan, 1983; Manning, 1998; Mullaby, 1998; Gianfancesco 等, 2002）。

非参数自助法（Nonparametric bootstrapping）是一种技术，通过对观测数据进行有放回的抽样，构建检验统计量（例如组间均值差异）的经验分布。虽然计算量很大，但自助法是成本数据分析的一种极具吸引力的替代方案，因为它直接处理算术平均值。推断是通过由分位数法形成的置信区间（CI）或修正和加速法（Efron 等, 1997; Diccido 和 Efron, 1996）从经验分布得出的。虽然有更详细的论证（Chernick, 2009），但通常建议在形成置信区间时进行 5,000 到 10,000 次重复。自助法的有效性依赖于我们的渐近假设——因为观测数据必须充分代表总体分布。虽然关于样本量多大才足够还没有指导，但 Churchill 建议，在使用自助法与其他方法相比时，不应改变样本量的考虑。虽然自助法允许在不假设分布形状的情况下估计均值，但其本身并不允许对解决组间差异所需的混杂变量进行调整。然而，这一缺陷通过纳入下一节描述的倾向性评分分层得到了解决。

## 第14 章 使用倾向性评分自助法进行成本和成本效益分析

成本和有效性的综合评估通常使用 ICER（增量成本效益比）或 BNB（净收益边界/边际效益）方法。在本章中，我们考虑使用 ICER 方法。ICER 仅是治疗组成本除以治疗组有效性差异的比率。当分析 ICER 点估计的不确定性衡量量时，会引入额外的统计复杂性，利用泰勒级数法、Fieller 方法和自助法（Obchain 等, 1997; Polsky 等, 1997; William 和 Briggs, 2006）。为了一致起见，我们专注于使用自助法，通过观测到的成本效益二次置信水平来确定主导程度（Obchain 等, 2005）。在使用自助法时，可以同时评估成本差异、有效性差异和成本效益比的不确定性。对于每个自助样本，都保留所选患者的成本差异和有效性差异——从而保留了结构与效果之间任何隐含的相关性。

### 14.2 倾向性评分自助法

PSBB 是用于成本相关分析的潜在有用工具，因为它处理了混杂因素，且不依赖分布假设。PSBB 的第一步是使用逻辑回归计算每个患者的倾向性评分，然后将倾向性评分分成等大小的五层（Rosenbaum 和 Rubin, 1984）。然后应进行彻底评估，以验证倾向性评分估计是否达到了平衡，以及治疗组之间的倾向性评分估计是否有足够的重叠。其次，在每个治疗组内，抽取固定大小的自助重采样——样本数等于患者总数。例如，治疗 1 的 $N=100$，治疗 2 的 $N=200$，然后从治疗 1 中抽取 20 个自助样本，从治疗 2 中抽取 40 个自助样本（考虑到每个分层患者的实际人数）。对于比较成本的分析，计算每次重复的治疗组间平均总成本差异，并通过大量重复产生均值差异的自助分布。分位数法识别自助统计量分布的 2.5% 和 97.5% 点，是生成均值差异 95% 双侧置信区间的一种简单方法。其他替代方案包括偏差和加速法（1997; Diccido 和 Efron, 1996）。

在使用 PSBB 评估成本效益时，从抽样选出的每个患者中保留成本测量和有效性测量量，并计算每个自助样本的 ICER。ICER 的不确定性通过这些差异在成本效益平面上的二元散点图提供，正如 Obchain 等人（2005）所描述。

### 14.3 示例：精神症有效性研究

为了使用 SAS 演示 PSBB，我们将分析基于一项为期一年的随机、开放标签、自然性针对精神症或情感障碍患者的模拟成本和有效性数据，这些患者被随机分配到 Tunis 等人（2006）报告的三种治疗方案之一。研究是自然性的，因为在随机化后，患者在通常环境中接受治疗，并允许切换或停止。由于随机化，各组之间的任何基线指标没有显著差异。然而，由于大多数观察性数据分析需要调整选择偏倚，我们将使用 Tunis 等人（2006）检查的相同协变量来说明这一点。

在运行 PSBB 分析之前，我们检查了成本的分布，并提供了模拟数据的汇总统计（见程序 14.1）。

```
proc sort data = ICER
by therapy; run;

proc univariate data =ICER noprint;
by therapy;
var tocost;
```

```sas
histogram / lognormal(fill l=b) cfill=yellow midpoints =
2500 to 152500 by 5000;

title h=2.5 lspace=1 "Test histogram: raw costs - lognormal distribution";

run;
```

```sas
data icer2; set icer;

group=floor(tocost/10000);

run;
```

```sas
proc sort data=icer2; by therapy group;

run;
```

```sas
filename MYFILE "D:\Temp\ICER_TOCOST.gif";
```

```sas
```



`options replace all device=gif gname=MYFILE gsmode=replace htext=1`

`mtext=swiss rotate=landscape;`

```sas
proc format;

value 0<='1';

run;
```

```sas
legend1 label=none across=3 value=(height=1.3) cborder=black cblock=gray;
```

```sas
pattern1 v=solid c=black;

pattern3 v=solid c=LIBRGR ;

pattern2 v=LL c=black;
```

`footnot h=1.5 'Total Costs (10 thou. $)';`

`title 'Summary of Total Costs by Initial Therapy';`
`AXIS1 LABEL=none value=(H=1.5 C=BLACK);`
`AXIS2 LABEL=(H=2 C=BLACK angle=90 "Frequency" J=CENTER) value=(H=1.5 C=BLACK);`
`AXIS3 label=none value=;`

```sas
PROC GCHART data=ICER2;

format group charge;

VBAR therapy/patternid=subgroup subgroup therapy group=group space=0

ref=(10 to 120 by 10) gaxis=axis1 raxis=axis2 max=axis3

legend=legend1;

run;

quit;
```

# 使用 SAS 进行观察性健康数据分析

## 程序 14.1 输出：按疗法的成本和有效性指标汇总

| 疗法 | N | P25 | 中位数 | P75 | 平均值 | 标准差 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| A | 223 | 4841.09 | 8467.46 | 22796.24 | 20863.59 | 28995.86 |
| B | 210 | 2899.83 | 7633.27 | 25269.44 | 21227.37 | 30992.32 |

| 疗法 | N | P25 | 中位数 | P75 | 平均值 | 标准差 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| A | 218 | 40.48 | 97.66 | 229.70 | 129.23 | 117.63 |
| B | 200 | 10.38 | 96.63 | 212.06 | 123.74 | 118.29 |

![](img/fe900f88acd4158b025dd58c336.png)

# 使用倾向评分自助法进行成本和成本效益分析

程序 14.2 提供了实现目标所需的 SAS 代码。在对后续计算置信区间所需的汇总统计量进行初步计算后，分析的第一步是计算每个患者的倾向评分并形成倾向评分分层（使用分位数）。这是通过 `GENMOD` 和 `RANK` 程序完成的。为了确认每层内有足够的患者数量，两组之间缺乏重叠（共同支持）表明不足以进行可比的比较（Rosenbaum 和 Rubin）。随后，PSBB 创建成本和有效性值的分层自助样本。该宏的输入参数是所需的重复次数、成本指标、治疗指示变量。我们使用了 1000 个自助样本作为感兴趣的置信区间。该程序将产生每个指标的自助分布、使用倾向法和 BCa 方法的每个指标的置信区间、ICER 的自助分布以及 ICER 变性的图形化显示。

从输出 14.2（散点图）可以看出，总成本差异的自助分布位于零附近，且平均成本显示出较大的方差。估计的平均差异（治疗 A 到 B）无论是百分位数法（95% CI 为 (-73, 53)）还是偏偏加速法（95% CI 为 (-60, 48)），均未显示出显著的成本差异。同样，在有效性指标中也观察到不显著差异（治疗 A 的 95% CI 为 (-4 到 +31)）。

### 程序 14.2：倾向评分自助法的 SAS 代码

```sas
%MACRO(rep=avarc,avare=indat,grprvar,seed0=ssize,seed1=1);

data temp; set &indat;

run;

proc freq data=temp noprint;

tables &grvar / out=freqnums;

where (&grvar=.);

data null; set freqnums;

call syst('val'|compress(put(n , 4))), trim(left(&grvar)));

call syst('ssize'|left(count))));

run;

* 为每个治疗组创建数据集

data trt0 trtl;

set temp;

if (&grvar=&vall) then output trt0

else if (&grvar=&val2) then output trtl;

keep &grvar &avare bin_ps;

data bssum; % 稍后使用的空数据集

if _n_ eq 1 then stop;

run;

proc sort data=trt0; by &grprvar bin_ps;

run;

proc sort data=trtl; by &grprvar bin_ps;

run;

%do i=1 to &rep;

** 为 therapy0 生成自助样本数据集

** 执行自助重采样

let btnum=&qysound(&ssize/5);

let rseed=&qysound(&i+seed0, 1));

proc surveyselect data=trt0 method=urs ouths rep=1

n=&btnum. seed=&rseed. noprint out=trt0;

strata &grvar bin_ps;

run;

** 为 therapy1 生成自助样本数据集

let btnum=&qysound(&ssize/2);

let rseed=&qysound(&i+seed1, 1));

proc surveyselect data=trtl method=urs ouths rep=1

n=&btnum. seed=&rseed. noprint out=trltout;

stratagrvarvar_ps;

run;

datadatagrps;

settt0 trltlt;

run;

** 计算样本的总体统计量

proc means data=bothgrps noprint;

 &grprvar;

var &avarc &avare;

output out = mn mean = out_avgc out_avge;
```

```sas
data mn; set mn=eof;

label &avarc.avgl ="Average for &AVARC, Group=&VAL1"

&avare.avgl ="Average for &AVARE, Group=&VAL1"

&avarc.avg2 ="Average for &AVARC, Group=&VAL2"

&avare.avg2 ="Average for &AVARE, Group=&VAL2";

dummy;

retain &avarc.avgl &avare.avgl &avarc._avg2 &avare._avg2;

if grprvar=0 then do

&avarc.avgl=out_avgc;

&avare.avgl=out_avge;

end;

if grprvar=1 then do

&avarc.avg2=out_avgc;

&avare.avg2=out_avge;

end;

keep dummy &avarc.avgl &avare.avgl &avarc._avg2 &avare._avg2;

if ef then output;

run;

** 使用此样本的统计量更新数据

data bsum;

set bsum mn;

run;

** 清理 work 库

proc datasets library=work memtype=data nolist

delete trt0outtrt0lut butgrps mn;

run;

quit;

end;

** 计算差异和测试统计量

data bsum;

set bsum;

&avare.diff = &avare.avg2 - &avare.avgl;

&avarc.diff = &avarc.avg2 - &avarc.avgl;

if &avare.diff ne 0 and &avarc.diff ne 0 then do ce = '+++';

if (&avare.diff ge 0 and &avarc.diff lt 0) then ce = '+-';

if (&avare.diff < 0 and &avarc.diff ge 0) then ce = '-+';

if (&avare.diff < 0 and &avarc.diff < 0) then ce = '--';

if (&avare.diff < (&avg2)) then ce = 1;

if (&avare.diff >= (&avg2)) then ce = 2;

&avare.diff="Average for &AVARE, Group21"

&avarc.diff="Average for &AVARC, Group21";

run;

* 为图表计算百分比变量

ods output OneWayFreqs=quad;

proc freq data=sum;

tables ce;

title2 "Quadrants for cost effectiveness";

title3 "&avarc and &avare"

data null; set quad;

if ce='++' then call symput('pos',percent);

if ce='-+' then call symput('neg',percent);

if ce='+' then call symput('pos',percent);

if ce='-' then call symput('neg',percent);
```

## 第 14 章 使用倾向评分分自助法的成本效性分析

```sas
proc univariate data=bssumm freq noprint;
var &avare.diff;
output=pctlsipts=2.5 97.5 pctlre = &avar
pctname=lcl_ucl;
run;

proc print data=pctls;
title2 "Bootstrap 95% confidence limits for &avar";
run;

** 计算 Bca 置信区间
```

```sas
data zerotad;

set bssumm;

by dummy;

if last.dummy; keep zeroctcte

run;

data bcacal;

set zerotad;

zeroc = probit(zeroct / &rep);

zereo = probit(zerocte / &rep);

zjl = probit(.025);

zjh = probit(.975);

bcaclo = zeroc + ((zjl) / (1 - &aconast +zjh));

bcbachei = zeroc + ((zjh) / (1 - &aconast +zjh));

bcaelo = zereo + ((zjl) / (1 - &aconast +zjh));

bcaie = zereo + ((zjh) / (1 - &aconast +zjh));
```

```sas
bcacl = probnorm(bcaclo);
bcbach = probnorm(bcbachei);
bcael = probnorm(bcaelo);
bcaeh = probnorm(bcaie);
run;

data null; set bcacal;
call symput('bcacl', trim(bcacl*1000));
call symput('bcach', trim(bcbach*1000));
call symput('bcael', trim(bcael*1000));
call symput('bcaeh', trim(bcaeh*1000));
run;

%put bcacl= &bcach= bcael= &bcaeh=;

proc univariate data=bssumm freq noprint;
var &avare.diff;
output=pctls pctipts=&bcacl. &bcach. pctlre = &avar
pctname=lcl_ucl;
run;

proc print data=pctls2;
title2 "Bca bootstrap 95% confidence limits for &avar";
run;

** 创建自助图 **
axis1 label=(h=1.5 c-black a=90 "Effectiveness Difference: A - B"
J-CENTER) value=(h=1.5 c-black);
axis2 label=(h=1.5 c-black "Cost Difference: A - B" J-CENTER)
value=(h=1.5 c-black);
```

```sas
proc graph data=bssum;
plot &avare.diff = '*' /legend haxis=axis2
vaxis=axis1
href=0
ref=0;
/* 添加象限频率百分比 **
note height=1.75 m(80pt,80pt) "pos.%%"
note height=1.75 m(80pt,30pt) "neg.%%"
note height=1.75 m(20pt,30pt) "negneg.%%"
note height=1.75 m(20pt,80pt) "pos.%%";
```

```sas
title h=2.5 "Quadrant distribution for cost effectiveness"
run;
** 清理库 **
proc datasets library=work memtype=data nolist
delete temp frequens trt0 trtl pctls2 pctls3 dat;
run;
/* 宏结束 */
/* 调用自助宏 */
```

```sas
*** 绘制均值差异直方图 ***
data bssum; set bssum;
totcost diff=totcost/1000;
** 调整成本大小以在图中显示 **
xaxis=axis1 maxis=axis2;
filename myfile2 "D:\Temp\ER_TOT.gif";
```

# 332 使用 SAS 分析观察性健康数据

程序 14.2 的输出（继续）成本差异的置信限

| 观测值 | totcost_lcl | totcost_ucl |
|---|---|---|

| 1 | -6190.15 | 4908.38 |

性差异的 BCa Bootstrap 95% 置信限

| 观测值 | respdays_lcl | respdays_ucl |
|---|---|---|

| 1 | -19.4726 | 24.1994 |

![](img/fe9ff008f88baacd415148b0b25dd58c_346_0.png)

成本均值差异：A - B（千美元）

# 第 14 章 使用倾向评分分箱自助法进行成本和成本效益分析 333

### 成本效益的四象限分布

![](img/fe9ff008f88baacd415148b0b25dd58c_347_0.png)

由于预估成本节省较小且效益优势较小，增量成本效益的点估计落在主导区域内（节省 173 美元并获得 9 天的反应；此处没有权衡）。程序 14.2 的输出证实了，相对于其不确定性，此 ICE 点估计非常接近原点；ICE 不确定性的 Bootstrap 分布跨越了成本效益面的所有四个象限。注意，优势的置信度为 41.1%（表明治疗 A 的效果更好且成本更低），另外两种情况的分别为 37.6% 和 10%-12%（分别为“A 成本更低但效果更差”和“A 成本更高且效果更差”）。因此，在这种情况下，Oberchain 及其同事（2005）达到显著优势（或严格优势）所需的置信水平并未满足。

虽然没有详细列出，但使用其他方法进行的敏感性分析在治疗成本比较方面显示了显著结果。虽然简单的 t 检验（p=.900）和广义线性模型（伽马分布）（p=.880）提供的结果与 PSBB 分析相似，但对数变换分析（p=.007）和 Wilcoxon 秩和检验（p=.945）导致治疗 B 组的成本显著降低。尽管该组的观测均值更高。这是由于在这种情况下，对数变换检验和秩检验对于均值差异是不可靠的。中位数在治疗方面表现更具优越性——且通过对对数变换数据的方差进行简单比较（可以通过 PROC TTEST 获取），证明了对数变换分析背后的假设在此处是无效的。Gianfranco 及其同事（2002）讨论了此类这种情况的可能，特别是在比较来自不同药物类别的治疗成本时。

## 14.4 讨论



在本章中，我们讨论了分析组间成本效益比较时涉及的主要问题。我们提供了执行 `PSBB` 分析的 `SAS` 代码，并附带了一个基于精神分裂症试验的模拟示例。`PSBB` 方法是一种极具吸引力的分析方法，因为它评估了平均成本、非参数性，并通过广泛接受的倾向评分分层方法评估了基线偏差。`PSBB` 可能并非适用于所有情况——因为缺乏关于方法论的比较研究，以了解各种方法的性能如何。

我们没有完全解决分析或成本数据呈现中涉及的所有问题。首先，我们在这里重点关注统计分析方法论——忽略了如研究设计、资源或成本的选择、成本数据的分配以及成本折现等问题——这些在引用的经济分析指南中已过充分讨论。我们还没有讨论缺失或截断成本数据的影响。这里说明的方法表明，无偏的成本或插补值是有价值的，或者处理数据的方法可以在倾向评分 Bootstrap 分析的结构内使用（例如）。我们的目标是让无偏成本或插补值有价值的，处理缺失数据的方法可以在倾向评分 Bootstrap 分析的结构内使用，包含以下三个部分：

- 1. 对假设的详尽评估；
- 2. 方法的可执行性；
- 3. 结果的透明度。

`Oberchain` 及其同事（1999）以及 `Kereaakis` 等同事（2000）的研究在成本效益方面是两个良好的案例。关于缺失数据的 cost-effectiveness 方法，请见 `Doshi` 和 `Young` (2006)。

# 参考文献

- Bouckaert, A., & Briggs, R. 1997. 成本差异的均值方法。
- Briggs, A. H., & Efron, B. 1996. 统计科学中的置信区间。
- Chennick, J. 1999. 倾向评分。John Wiley。
- DiCaprio, J. T., & Efron, B. 1996. 医疗决策中的 Bootstrap。
- Doshi, A. H., & Polsky, D. 2006. 随机对照试验的成本效益。
- Duan, N. 1983. 涂层估计：一种非参数变换方法。《美国统计学会杂志》。
- Duggan, M. 2005. 没有新药？第二代精神病药物。《药物经济学》。
- Garrison, R. L., Neumann, P. J., Erickson, E., Marshall, S., & Mullins, C. 2007. 使用真实数据进行覆盖和支付：ISOR 数据报告。
- Gianfranco, F., Wang, R., & White, R. 2002. 精神病领域基于索赔的研究方法。《药物经济学》。
- Grimes, D. A., & Schulz, K. 2002. 观察性研究中的偏差与关联。《柳叶刀》。
- Lindsey, J. K., & Jones, B. 1998. 选择应用于医学数据的广义线性模型。《医学统计学》。
- Liu, G. G., Sun, S. X., Christensen, B., & Zhao, Z. 2007. 北卡罗来州医疗补助计划中使用第二代精神病药物治疗精神分裂症的成本分析。《美国药剂协会杂志》。

## 336 使用 SAS 进行观察性健康数据分析

Lumley, T. P. Diehr, S. Emerson, and L. Chen. 2002. “正态假设在大型公共卫生数据集中的重要性。”Annual Review of Public Health 23: 151–169.

Manning, W. G. 1998. “对数因变量、异方差性与重构问题。”Journal of Health Economics 17: 283–295.

Mullahy, J. 1999. “健康经济学中考虑重构和两部分模型时我们所做的工作。”Journal of Health Economics 17(3): 247–281.

Nyhuis, A. W., M. D. Stensland, and D. E. Faries. 2003. “计算成本效益策略的恢复天数。”Schizophrenia Research 60(1): Supplement 1): 341.

Olinch, R. 2003–“ICEprobs: 一个通过倾向评分自助（两个偏倚样本）计算增量成本效益方差的 Windows 应用。”可用 http://members.iquest.net/softrix/ICErefs.htm

Olinch, R., and B. M. Johnstone. 1999. “随机临床试验中退出者成本数据的混合模型插补。”Drug Information 33: 191–209.

Olinch, R., C. A. Meifi, T. W. Croghan, and D. P. Buesching. 1997. “抗抑郁药物药物治疗中成本效益的自助分析。”Pharmacoeeconomics 11(5): 464–472.

Olinch, R. L. Robinson, and R. W. Swindle. 2005. “基于自助置信水平的成本效益推断：三个主导程度。”Journal of Biopharmaceutical Statistics 15(3): 419–436.

Oostenbrick, J. B., and M. J. Al. 2005. “由于脱落导致不完整成本数据分析。”Health Economics 14(8): 763–776.

Polsky, D. H. A. Glick, R. Willke, and K. Schulman. 1997. “成本效益的置信区间：四方法的比较。”Health Economics 6(3): 243–252.

Polsky, D. J., A. Doshi, M. S. Bauer, and H. A. Glick. 2006. “抗精神药技术的临床试验成本效益分析。”The American Journal of Psychiatry 163: 2047–2056.

Ramsey, S., R. Willke, R. Brown, M. Buxton, A. Chawla, J. Cook, H. Glick, B. Liljas, S. Pettitti, and S. Reed. 2005. “临床试验沿线成本效益分析的良好研究实践：ISPOR RCT-CEA 任务组报告。”Value in Health 8(5): 521–533.

Revicki, D. A., and L. Rubin. 1999. “真实世界中的药物经济学评价：有效性效力研究。”Pharmacoeconomics 15(5): 423–434.

Rosenbaum, P., and D. B. Rubin. 1983. “倾向评分在因果效应观察性研究中的核心作用。”Biometrika 70: 41–55.

Rosenbaum, P., and D. B. Rubin. 1984. “使用倾向评分中的子分类减少观察性研究中的偏倚。”Journal of the American Statistical Association 79: 516–524.

Rosenberg, R., D. Perlick, S. Bingham, W. Liu-Mares, J. Collins, S. Warren, D. Leslie, E. Allan, E. C. Campbell, S. Caroff, J. Corvin, D. Lewis, R. Douillon, L. Dunn, E. Evans, E. Fresca, J. Grabowski, D. Graeber, L. Herz, K. Kwon, W. Lawson, F. Mena, J. Sheikh, D. Smelson, and V. Smith-G. 2005. 奥氮西平对比氟氟啶平治疗分裂症的资源利用和成本：随机试验。”The Journal of Medical Association 290: 2693。

## 第15 章

### 增量效益

Andrew R. Willan

- 摘要 339
- 引言 340
- 成本效益分析 341
- 参数估计 346
- 示例 351
- 观察性研究 359
- 讨论 359
- 致谢 360
- 参考文献 360

# 摘要

自20世纪90年代初，受比较患者组临床研究中患者水平成本数据的推动，研究人员在成本效益数据的统计方法方面取得了快速进展。最初的工作集中在增量成本效益率的推断上，但由于比例统计的问题，兴趣更多地转向了增量。无论采用何种方法，都需要估计五个参数：组间平均有效性和平均成本的差异，以及相应的方差和协方差。通过这些参数估计，分析师可以估计增量成本效益率并计算相应的置信限。由于对比例统计的担忧，分析师可能会选择关注增量效益。采用传统的频率学方法，可以估计增量效益，并用相应的置信限表征其不确定性。或者，采用贝叶斯方法用于显示组间对比幅度并表征其不确定性。本文对这些方法进行了回顾。估计五个参数的特定统计方法取决于：

* 是否存在删
* 是否调整了协变量
* 是否调整了随机效应（例如国家）
* 关于成本分布的假设是什么

在存在这些条件组合的情况下，本文简要回顾了每种情况特定的统计方法。文中还提供了一个随机临床试验的示例。

# 15.1 引言

自20世纪90年代初以来，在临床研究中收集资源利用数据已变得越来越普遍。资源数据结合单位价格权重，除了有效性衡量外，还提供了患者水平总成本的衡量。在患者水平上拥有有效性和成本，允许使用传统的统计推断方法来量化由于抽样和测量误差引起的不确定性。关于成本效益数据的统计分析已发表大量文章。最初的工作集中于为增量成本效益比（`ICER`）提供置信区间，`ICER` 是治疗组间平均成本差异与治疗组间有效性差异的比值。然而，由于对比率统计量的考量，净收益（`INB`）的概念被用作一种替代方案。`INB` 是以货币形式衡量的有效性增加减去成本的增加。本章的目的是对建议的统计成本效益分析（`CEA`）方法进行结构化回顾，重点关注 `INB`。全文使用的背景是双臂临床试验，其中患者被随机分配到治疗组（`R`组）或标准组（`S`组）。然而，这些方法允许比较任何两组，但受限于缺乏随机分组的考虑（进一步讨论请参见第 15.5节）。

在参数方法中，`CEA` 的核心任务是联合建模有效性和成本以估计五个参数。其中两个参数是治疗组间的平均有效性差异，记为 `$\Delta_e$`，以及治疗组间的平均成本差异记为 `$\Delta_c$`。另外三个参数是 `$\Delta_e$` 估计量的方差记为 `$V(\Delta_e)$`；以及 `$\Delta_e$` 和 `$\Delta_c$` 估计量的协方差记为 `$C(\Delta_e, \Delta_c)$`，其中 `$\hat{\theta}$` 表示 `$\theta$` 的估计量。必须对有效性和成本进行联合建模才能估计协方差。用于估计这五个参数的特定统计程序取决于：

- 是否存在截断
- 是否调整了协变量
- 是否调整了如国家之类的随机效应
- 关于成本分布的假设是什么

利用这五个参数的估计量，可以进行基于增量效益比或增量收益的 `CEA`。在本章的其余部分，假设 `$\Delta_e$` 和 `$\Delta_c$` 的估计量服从正态分布。这一假设基于中心极限定理，该定理认为大量独立变量之和将趋于从正态分布。

在第 15.2 节中说明了基于五个参数估计值显示 `CEA` 的。用于估计参数的统计程序（取决于前述讨论的问题）将在第 15.3 节中回顾。第 15.4 节给出了一个使用随机临床试验的示例。第 15.5 节讨论了针对观察性研究特定的问题。第 15.6 节是本章的总结。

# 15.2 成本效益分析

本节提供了与两组比较相关的成本效益分析概介绍。通常（但并非如此），`CEA` 中的有效性衡量与患者经历的临床事件相关，例如死亡、复发或达到预设的症状缓解水平。与事件相关的三个有效性衡量指标例如：

- 1. 患者在感兴趣期内是否存活
- 2. 在感兴趣期内的生存时间
- 3. 在感兴趣期内的质量调整后生存时间

相应的 `$\Delta_e$` 为：

- 1. 存活概率的治疗组间差异
- 2. 平均生存时间的治疗组间差异
- 3. 平均质量调整后生存时间的治疗组间差异

所有平均值均限于感兴趣期，差异取为 `T-S`。`ICER` 定义为 `$\Delta_c/\Delta_e$`，分别为：

- 1. 使用 `T` 替 `S` 的额外成本
- 2. 使用 `T` 替 `S` 获得额外寿命的成本
- 3. 使用 `T` 替 `S` 获得质量调整寿命（`QALY`）的成本

`ICER` 可以在成本效益平面上所示，如图 15.1 所示，即原点与点 `($\Delta_c$, $\Delta_e$)` 之间的斜率。

在图 15.1 到 15.5 中，我们假设有效性衡量是质量调整生存时间，有效性单位是质量调整年（`QALYs`）。图 15.1 中同样显示的直线称为阈值，其斜率等于单位性的支付意愿（`WTP`），记为 `$\lambda$`。阈值将成本效益平面分为两个区域。对于阈值右侧（阴影部分）的点，`T` 被认为是有成本的，但对于上方和左侧的点，则不是。因为 `$\lambda$` 是正值，`SE` 象限中 `T` 更有效且成本更高的点位于阈值下方，因此对应的比较 `T` 有成本效益。相反，`NW` 象限中 `T` 有效且成本更高的点位于阈值上方，因此对应的比较 `T` 无。在 `NE` 和 `SW` 象限，`WTP` 概念允许有效性和成本之间的权衡。在 `NE` 象限，直线下方任何点的斜率小于 `$\lambda$`（即 `$\Delta_c/\Delta_e < \lambda$`），这意味着 `$\Delta_c < \lambda\Delta_e$`。

# 15.3 使用 SAS 分析观察性数据

因此，价值的增加 `($\lambda\Delta$)` 大于成本的增加，使得 `T` 有成本效益。在 `SW` 象限，直线下方任何点的斜率大于 `$\lambda$`，由于 `$\Delta_c$` 和 `$\Delta_e$` 均为负值，`$|\Delta_c| > |\lambda\Delta|$`，我们得到 `$\frac{\Delta_c}{\Delta_e} > \lambda$`，这意味着 `$|\Delta_c|$` 小于 `T` 节省的金额 `($\lambda\Delta$)`。总而言之，`T` 有成本效益当且仅当：

`A: \frac{\Delta_c}{\Delta_e} < \lambda` 若 `$\Delta_e > 0$`，或者 `$\frac{\Delta_c}{\Delta_e} > \lambda$` 若 `$\Delta_e < 0$`。(1)

方程 1（假设 A）定义了阈值下方的区域，可以认为是零假设 `H` 的备择假设，即：

`H: \frac{\Delta_c}{\Delta_e} \geq \lambda` 若 `$\Delta_e > 0$`，或者 `$\frac{\Delta_c}{\Delta_e} \leq \lambda$` 若 `$\Delta_e < 0$`。(2)

拒绝 `H` 而接受 `A` 将为采用 `T` 提供证据。这些方程有些繁琐，通过引入 `INB` 可以大大简化。

**图 15.1** 成本效益平面

| NW | `$\Delta_c$` | NE |
| :--- | :--- | :--- |
| | | `($\Delta_c$, $\lambda\Delta$)` |
| | 阈值；斜率 = `$\lambda$` | |
| | | 斜率 = `$\Delta_c/\Delta_e$` |
| | `$\Delta_e$` (QALYs) | |
| SW | | SE |

# 15.4 增量净收益

`INB` 是 `$\lambda$` 的函数，定义为 `$b_\lambda \equiv \lambda\Delta - \Delta_c$`；`$b_\lambda$` 是增量收益，因为它是增量价值 `($\lambda\Delta$)` 与增量成本 `($\Delta$)` 之差。无论 `$\lambda$` 的符号如何，`T` 有成本效益当且仅当 `$b_\lambda > 0$`。为了证明这一点，方程 1 中涉及 `ICER` 的两个不等式都可以重组为 `$\lambda\Delta - \Delta_c > 0$`。同样，方程 2 中涉及 `ICER` 的两个不等式都可以重组为 `$\lambda\Delta - \Delta_c \le 0$`。因此，从 `INB` 来说，零假设和备择假设简化为：

`H: b_\lambda \le 0 \quad A: b_\lambda > 0`。(3)

方程 1、2、3 中假设 `H` 和 `A` 的公式说明了 `ICER` 和 `INB` 之间的紧密关系`$b_\lambda$` 是从点 `($\lambda\Delta$, $\Delta_c$)` 到阈值的垂直距离，如果点在直线下方则为正，反之为负。因为它的斜率为 `$\lambda$`，阈值上横坐标等于 `$\Delta_c$` 的点为 `($\Delta_c$, $\lambda\Delta$)`，它与 `($\lambda\Delta$, $\Delta_c$)` 之间的垂直距离为 `$\lambda\Delta - \Delta_c$`（见图 15.2）。

# 图 15.2 成本效益平面上的 INB ($b_\lambda$)

![](img/fe9ff008f88baacd415148b0b25dd58c_357_0.png)

`ICER` 可以通过 `$\hat{\Delta}_c/\hat{\Delta}_\lambda$` 估计，其中 `$\hat{\Delta}_c$` 和 `$\hat{\Delta}_\lambda$` 分别是 `$\Delta_c$` 和 `$\lambda\Delta$` 的估计量。估计量 `$\hat{\Delta}_c/\hat{\Delta}_\lambda$` 是偏的，但如果 `$\hat{\Delta}_c$` 和 `$\hat{\Delta}_\lambda$` 是无偏的，它是一致的，这意味着随着样本量的增加偏差会减小（`Caudhary` and `Stearns`, 1996; `Cochran`, 1997）。`ICER` 的统计推断被限于计算其置信区间。应用 Fieller 定理 [1, 3]，`$(1-2\alpha)100\%$` 置信限为

## 344 使用 SAS 进行观察性健康数据分析



$$R\left\{\frac{1-z_{1-\alpha}^2c \pm z_{1-\alpha}\sqrt{a+b-2c-z_{1-\alpha}^2(ab-c^2)}}{1-z_{1-\alpha}^2a}\right\},\quad(4)$$

$R=\hat{\Delta}_c/\hat{\Delta}_e, a=\hat{V}(\hat{\Delta}_e)/\hat{\Delta}_e^2, b=\hat{V}(\hat{\Delta}_c)/\hat{\Delta}_c^2, c=\hat{C}(\hat{\Delta}_e, \hat{\Delta}_c)/(\hat{\Delta}_e\hat{\Delta}_c),$ 其中 $z_{1-\alpha}$ 是标准正态随机变量的 $100(1-\alpha)$ 百分位数。成本效益平面上斜率处于方程 4 所定义的限值之间的之间的点集，在成本效益平面上定义了一个“蝴蝶结”区域（见图 15.3），但通常推断被限制在包含点 $(\hat{\Delta}_e, \hat{\Delta}_c)$ 的蝴蝶结区域内。如果

$a+b-2c-z_{1-\alpha}^2(ab-c^2)=0$，则方程 4 无解且两个限均未定义，这意味着数据在概率上距离原点太近，分析无法以高信度提供关于 ICER 值的推断。ICER 还有其他缺点。在未指定 $\Delta_e$ 或 $\Delta_c$ 符号的情况下，无法对其解释。此外，ICER 估计量的均值和方差是未定义的。

图 15.3 蝴蝶结 ICER 置信区域

![](img/fe9ff008f88baacd415148b0b25dd58c_358_0.png)

这些困难，加上成本效益平面（东南和西北象限）的特性，导致分析师得出关于增量净收益（INB）作为替代方案的成本效益推断。如前所述，当且仅当 $b_z > 0$ 时，$T$ 是成本效益的。采用贝叶斯方法，成本效益接受曲线（CEAC）是 $b_z > 0$ 的概率随 $\lambda$ 变化的图形。假设没有先验信息，

# 第 15 章 增量净收益

CEAC 可以由 $CEAC(\lambda) = \Phi(\hat{b}_\lambda/SE(\hat{b}_\lambda))$给出，其中 $\Phi(-)$ 是标准正态变量的累积分布函数，$\hat{b}_\lambda = \hat{\Delta}_\lambda - \hat{\Delta}_c$ 是 $b_\lambda$ 的估计量，其标准误为 $SE(\hat{b}_\lambda)$，由 $\sqrt{\lambda^2\hat{V}(\hat{\Delta}_\lambda) + \hat{V}(\hat{\Delta}_c) - 2\lambda\hat{C}(\hat{\Delta}_\lambda, \hat{\Delta}_c)}$给出。通过 $\Phi(\hat{b}_\lambda/SE(\hat{b}_\lambda))$ 估计 CEAC 假设 $\hat{\Delta}_\lambda$ 和 $\hat{\Delta}_c$ 从正态分布。该假设基于中心极限定理。关于贝叶斯成本效益的更完整讨论，请参见 O’Hagan 和 Stevens (2001)。

CEAC 具有捕捉观察到的成本效益的大小和不确定性的优势。它允许应用最适用于 t 的意愿支付（WTP）阈值。如图 15.4 所示，CEAC 在 $\lambda$ 等于 ICER 时通过 0.5，并在 $\alpha$ 和 $1-\alpha$ 等于此处定义的 ICER Fieller 限时通过。因此，基于 INB 的 CEAC 提供了关于 ICER 的推断。基于 INB 的更直接的推断由 Fenwick、O’Brien 和 Briggs (2004) 的绘图提供。更多随 $\lambda$ 变化的估计值和置信限（见图 15.5）。INB 的置信限由 $b_\lambda \pm z_{\alpha}SE(\hat{b}_\lambda)$ 给出。$b_\lambda$、$b_c$ 与 ICER 之间的紧密关系如图 15.5 所示。$b_\lambda$ 的图在 ICER 处跨过横轴。如果 $\hat{\Delta}_c$ 为正，则 ICER 处的 $b_\lambda$ 下限和 ICER 处的 $b_c$ 上限具有成本效益。另一方面，如果 $\hat{\Delta}_c$ 为负，则 ICER 处的 $b_\lambda$ 下限和 ICER 处的 $b_c$ 上限不具有。

图 15.4 成本效益分析

使用 SAS 进行观察性健康数据分析

图 15.5 随 $\lambda$ 变化的增量净收益

![](img/fe9ff008f88acd415148b0b25dd58c_359_0.png) 捕捉了观察到的成本效益的大小和不确定性。它还允许应用最适用于 t 的意愿支付（WTP）阈值。如图 15.4 所示，CEAC 在 $\lambda$ 等于 ICER 时通过 0.5，并在 $\alpha$ 和 $1-\alpha$ 等于此处定义的 ICER Fieller 限时通过。因此，基于 INB 的 CEAC 提供了关于 ICER 的推断。基于 INB 的更直接的推断由 Fenwick、O’Brien 和 Briggs (2004) 的绘图提供。更多随 $\lambda$ 变化的估计值和置信限（见图 15.5）。INB 的置信限由 $b_\lambda \pm z_{\alpha}SE(\hat{b}_\lambda)$ 给出。$b_\lambda$、$b_c$ 与 ICER 之间的紧密关系如图 15.5 所示。$b_\lambda$ 的图在 ICER 处跨过横轴。如果 $\hat{\Delta}_c$ 为正，则 ICER 处的 $b_\lambda$ 下限和 ICER 处的 $b_c$ 上限具有成本效益。另一方面，如果 $\hat{\Delta}_c$ 为负，则 ICER 处的 $b_\lambda$ 下限和 ICER 处的 $b_c$ 上限不具有。

## 15.3 参数估计

后续小节讨论：

- 是否存在截断
- 是否调整了变量
- 是否考虑了随机效应
- 假设是什么

### 15.3.1 数据的右偏

由于右偏，最小二乘法的使用受到批评（O'Hagan and Stevens, 2003; Briggs and Gray, 1998; Thompson and Barber, 2000; Nixon and Thompson, 2004; Briggs et al., 2005）。变换（如对数和平方根）有时被提出的替代方案。然而，此类变换提供的估计与决策者并不相关（Manning and Tully, 2001，以及 Thompson and Barber, 2000）。此外，许多使用模拟数据的偏态数据研究得出结论，最小二乘法提供了有效的估计。Lumley 等人 (2002) 对此类研究进行了回顾。然而，对离群值盲目应用样本均值和方差会导致误导性结论。对最小二乘法稳健性的信任不能代替对数据的仔细检查。此外，在存在右偏的情况下，最小二乘法可能提供一致估计，但效率较低。

#### 15.3.1.2 变量调整

在随机临床试验 (RCT) 中，由于变量在治疗组间往往平衡，变量调整可能是必要的，尽管可以使用回归模型来提高精度或通过交互项研究亚组效应。

#### 15.3.1.3 截断

许多临床试验中，某些患者没有被随访整个关注期。某些患者可能会失访，原因是他们拒绝随访诊疗或离开了试验管理资源覆盖范围。此外，由于进入时间交叉且随访时间长，分析可以在所有患者随访整个关注期之前进行。当截断是无信息的时（即死亡时间相互独立），可以使用生存表法提供对关注期生存概率和平均生存时间的无偏估计。然而，对于成本和质量调整生存时间，截断是有信息的，即使截断时间与死亡时间相互独立，使用生存表法也会产生偏偏估计（William 等人，2002）。

# 348 使用 SAS 进行观察性健康数据分析

平均生存时间、质量调整后生存时间和成本指的是在感兴趣的持续时间内的平均值。在心脏病试验中，感兴趣的持续时间可能是 30 天或 12 个月；然而，在癌症试验中，这可能长达 5 或 10 年。

#### 15.3.1.4 随机效应

许多研究在多个国家进行。其优点是由于样本量的增加导致统计功效的提高，并且认为具有更好的推广性。然而，对跨国研究的分析往往忽略了治疗与国家之间交互的可能性，即治疗效应在不同国家之间存在差异。在存在交互的情况下，治疗效应的估计值（即平均水平和有效性的治疗间差异）忽略了国家效应，导致方差不当地偏小并引发第一类错误。将国家视为固定效应的模型（Wilke 等人，1998；Cook 等人，2003）虽然考虑了这种交互作用，但没有整体治疗效应的参数，且提供的基于单个国家数据的特定国家治疗效应估计值。近期的一些出版物（Grieve 等人，2005；Willan 等人，2005；Mancush 等人，2005；Pinto 等人，2005 以及 Nixon 和 Thompson，2005）通过提议将国家视为随机效应的分层模型解决了这一问题。这些模型的优点是提供了治疗效应的整体估计值，以及利用所有国家数据的特定国家估计值。

## 15.3.2 参数估计的细节

设 $E_i$ 和 $C_i$ 分别为患者 $i$ 接受治疗 $j$ 时观测到的有效性和成本效应，其中 $i=1, 2, \dots, n_j=T$，$E_i$ 经过缩放，使得较大的值对应于更好的结果。对于二分类结果，$E_i$ 成功时为 1，失败为 0。如第 15.1.4 节所述，人们通常认为成本数据是右偏的。在第 15.3.2.1 节到 15.3.2.4 节中，回顾了忽略偏态成本数据的方法，并在第 15.3.2.5 节中回顾了考虑偏态成本数据的方法。

##### 15.3.2.1 无删结、无随机效应、无协变量

如果没有删结、无随机效应且无协变量，则参数估计值是样本统计量（如均值、方差和比例）的简单函数。平均有效性和成本的差异给出：

$$\hat{E}_e = \bar{E}_T - \bar{E}_S = \frac{\sum_{i=1}^{n_T} E_i}{n_T} - \frac{\sum_{i=1}^{n_S} E_i}{n_S} \text{ 和 } \hat{\Delta}_c = \bar{C}_T - \bar{C}_S = \frac{\sum_{i=1}^{n_T} C_i}{n_T} - \frac{\sum_{i=1}^{n_S} C_i}{n_S}$$

$\hat{\Delta}_c$ 的估计方差给出：

$$\hat{V}(\hat{\Delta}_c) = \frac{\sum_{i=1}^{n_T} (C_i - \bar{C}_T)^2}{n_T(n_T-1)} + \frac{\sum_{i=1}^{n_S} (C_i - \bar{C}_S)^2}{n_S(n_S-1)} \text{ 或}$$

$$\hat{V}(\hat{\Delta}_c) = \frac{\frac{n_T+n_S}{n_T} \dots \text{(此处原文公式不完整，按逻辑推断)} \dots \dots \sum_{i=1}^{n_S} (C_i - \bar{C}_S)^2}{n_S(n_S-1)}$$

对于同性方差，如果有效性是连续的，$\hat{\Delta}_e$ 的估计方差给出：

$$\hat{V}(\hat{\Delta}_e) = \frac{\sum_{i=1}^{n_T} (E_i - \bar{E}_T)^2}{n_T(n_T-1)} + \frac{\sum_{i=1}^{n_S} (E_i - \bar{E}_S)^2}{n_S(n_S-1)} \text{ 或}$$

$\hat{\Delta}_e$ 与 $\hat{\Delta}_c$ 之间的协方差给出：

$$\tilde{C}(\hat{\Delta}_e,\hat{\Delta}_c) = \frac{\sum_{i=1}^{n_T}(E_i-\bar{E}_T)(C_i-\bar{C}_T) + \sum_{i=1}^{n_S}(E_i-\bar{E}_S)(C_i-\bar{C}_S)}{n_T+n_S-2}$$

（注：原文协方差公式严重损坏，已根据标准协方差公式进行重构）。

## 第15章 增量净收益

# 350 使用 SAS 进行观察性健康数据分析

##### 15.3.2.2 无删结、无随机效应、含协变量

如果有效性是连续的，成本也是连续的。在没有删结或随机效应的情况下调整协变量，使用普通最小二法。设 $y$ 为结果（有效性或成本）。回归模型给出：

$$y = X\beta$$

其中 $X$ 是预测变量矩阵，$\beta$ 是系数向量。$X$ 的第一列是治疗组的虚拟变量（0或1），第二列包含协变量。

##### 15.3.2.3 无删结、随机效应和协变量

为了考虑多国随机对照试验（RCT）中的随机效应，提出了两种通用方法。第一种方法由 Pinto、Willan 和 O’Brien（2005）以及 Willan 等同事（2005）提出，分为两个阶段。第一阶段将每个国家视为独立的试验，并使用适当的方法估计感兴趣的五个参数。适当的方法可能包括考虑删结或协变量的方法。然后使用经验贝叶斯将特定国家的估计值合并，这在本质上是一种双变量（有效性和成本）元分析。第二种方法（Grieve 等人，2005；Manca 等人，2005 以及 Nixon 和 Thompson，2005）在患者水平上对有效成本进行建模，使用分层模型来考虑两种误差来源（患者和国家）。

##### 15.3.2.4 删结

如果有效性的感兴趣参数是生存概率或平均生存时间，则可以使用 Kaplan-Meier 生存曲线来估计 $\Delta_p$（Willan 等人，2003，2002）。对于质量调整后生存时间和成本，删结是含有信息的

## 第 15 章 增量净收益

删失时间与死亡时间是相互独立的，使用生存表法将产生偏偏估计值。处理这一问题主要有两种方法。第一种被称为 Lin 方法或直接法，见于 Lin 等同事 (1997) 以及 Willan 和 Lin (2001)。另一种是基于逆概率加权的方法，见于 Bang 和 Tsiatis (2000)、Lin (2000)、Zhao 和 Tian (2001) 以及 Willan 等同事 (2002)。两种方法均见于 Willan 和 Briggs (2006) 的第 3 章。

关于存在协变量时的估计量成本，请参 Lin (2000) 以及 Willan, Lin 和 Manca (2005)。为了考虑带有删失数据的多变量试验中的随机成本效应，可以按国家进行分层分析，从而得出 $\Delta_e$ 和 $\Delta_c$ 的估计值以及每个国家相应的方差和协方差。如第 15.3.2.3 节所述，可以使用经验贝叶斯程序（Willan et al., 2005; Pinto et al., 2005）合并这些估计值进行总体成本估计。

### 15.3.3 考虑成本数据的偏态性

通过马尔可夫链蒙特卡洛方法可以对非对称分布的成本和有效性进行联合建模，其详细讨论见于 Nixon 和 Thompson (2005)。通常使用伽马分布来模拟成本。在大多数情况下，伽马分布似乎对于拟合成本数据具有足够的灵活性。模型可以处理协变量调整、亚组分析的交互项以及国家的随机效应。`PROC GENMOD` 提供了一种更易于操作的方法，如第 15.4 节所示。

## 15.4 示例

本节给出一个详细示例。有效性指标为二分类，成本数据具有一定偏态。此外，存在一个二分类协变量，该变量与治疗组之间存在统计学显著的交互作用。

### 15.4.1 CD 试验

根据首席研究者的要求，本示例的数据已公布，以消除与之前出版物的任何冲突。该随机对照试验（RCT）被称为 CD 试验。在 CD 试验中，招募了 1,356 名患者并将其随机分配到两个治疗组，分别标记为 T 和 S。存在一个二分类基线协变量标记为 $X$，水平标记为 0 和 1。主要有效性指标是 30 天生存率。收集了所有患者的医疗资源利用情况，并结合价格权重提供患者级成本数据。表 15.1 给出了按治疗组和协变量划分的 30 天生存比例和平均成本。30 天生存率的总体观察增长为 0.05，且在协变量的不同水平之间保持一致。接受 T 治疗的总体成本节约约为 0.808。观察到的平均成本差异取决于协变量，$X=0$ 时约为 1,200 美元，$X=1$ 时约为 300 美元。图 15.6 给出了按治疗组划分的成本直方图。每对矩形的宽度为 2,000 美元，最后一对代表超过 44,000 美元的成本。从图中可以明显看出高度的偏态性。

#### 表 15.1 CD 试验按治疗组和 X 划分的生存比例和平均成本

| 30 天生存比例 | | 平均成本 (CAD) | | |
|---|---|---|---|---|
| $T$ | $S$ | $T$ | $S$ |
| $X = 0$ | 0.9345 | 0.8847 | 8976.36 | 10203.31 |
| $X = 1$ | 0.9271 | 0.8746 | 8859.37 | 9137.26 |
| 所有患者 | 0.9309 | 0.8802 | 8919.76 | 9725.48 |

#### 图 15.6 CD 试验的成本直方图

![](img/fe9ff008f88acd415148b025dd58c366.png)

忽略协变量影响五个参数估计见表 15.2。第一列的估计值源于使用 15.3.2 节中的合并方差和协方差公式。第二列的估计值专门源于正态分布建模，见程序 15.1。如预期，该列的估计值与第一列几乎相同。第三列的估计值源于伽马分布建模，见程序 15.2。如预期，$\hat{\Delta}_e$ 和 $\Delta_c$ 的估计值非常相似，但方差 $V(\hat{\Delta}_c)$ 小 25%，表明伽马分布提供了更好的数据拟合。这种效率的影响见图 15.7 和 15.8。作为 $\lambda$ 函数的 $\Delta_c$ 估计值和置信区间见图 15.7，适用于正态和伽马假设。对于防止死亡的 $\lambda$ 值，两者的置信区间基本等效。以下 SAS 代码提供了所需参数的估计值，其中 `arm` 是治疗组（T 为 1，S 为 0），如果患者生存了 30 天则有效性为 1，否则为 0，成本为每个患者的总成本。

##### 程序 15.1 建模建模



```sas
proc genmod data=yourDataset;
    model cost = arm / dist=normal link=identity;
    output out=c predicted=pred_c;
run;

proc genmod data=yourDataset desc;
    model effectiveness= arm / dist=bin link=identity;
    output out=e predicted=pred_e;
run;
```

```sas
data temp; merge c;
    resid_e = effectiveness - pred_e;
    resid_c = cost - pred_c;
    keep resid_e resid_c;
run;

proc corr data=temp var resid_e resid_c; run;
```

### 程序 15.1 输出

| 参数 | DF | 估计值 | 标准误 | Wald 95% | 卡方 | Pr > ChiSq |
|---|---|---|---|---|---|---|

| 截距 | 1 | 972.479 | 210.9007 | 932.121 | 1013.84 | 2126.50 | <0001 |
| arm | 1 | -805.724 | 279.817 | -1389.44 | -222.008 | 4965.68 | 0.0068 |

$\hat{\Delta}_c = -805.724$; $\hat{V}(\hat{\Delta}_c) = (297.819)^2.$

| 参数 | DF | 估计值 | 标准误 | Wald 95% | 卡方 | Pr > ChiSq |
|---|---|---|---|---|---|---|

| 截距 | 1 | 0.8802 | 0.0125 | 0.8557 | 0.9047 | 4965.68 | <0001 |
| arm | 1 | 0.0507 | 0.0158 | 0.0197 | 0.0817 | 10.26 | 0.0014 |

$\hat{\Delta}_e = 0.0507;$ $\hat{V}(\hat{\Delta}_e) = (0.0158)^2.$

皮逊相关系数，N = 1356

| | resid_e | resid_c |
|---|---|---|

| resid_e | 1.00000 | -0.31306 |
| resid_c | -0.31306 | |

$\hat{C}(\hat{\Delta}_e, \hat{\Delta}_c) = (-0.31306) * (297.819) * (0.0158).$

## 15.5 使用 SAS 分析观察性健康数据

以下 SAS 代码提供了五个所需参数的估计值。输出（未显示）与程序 15.1 的输出相同。

### 程序 15.2 使用伽马分布建模成本

```sas
proc genmod data=yourDataset;
    model cost = arm / dist=gamma link=identity;
    output out=c predicted=pred_c;
run;

proc genmod data=yourDataset desc;
    model effectiveness = arm / dist=bin link=identity;
    output out=e predicted=pred_e;
run;

data temp; merge e c;
    resid_e = effectiveness - pred_e;
    resid_c = cost - pred_c;
    keep resid_e resid_c;
run;

proc corr data=temp; var resid_e resid_c; run;
```

#### 表 15.2 CD 试验的参数估计

| 参数 | 合并 | 正态* | 伽马* |
|---|---|---|---|

| $\hat{\Delta}_e$ | 0.0507 | 0.0507 | 0.0507 |
| $\hat{\Delta}_c$ | -805.72 | -805.72 | -805.72 |
| $\hat{V}(\hat{\Delta}_e)$ | 0.0002506 | 0.0002496 | 0.0002496 |
| $\hat{V}(\hat{\Delta}_c)$ | 88,828 | 88,697 | 65,839 |
| $\hat{C}(\hat{\Delta}_e, \hat{\Delta}_c)$ | -1.482 | -1.473 | -1.268 |

* 用于成本的分布

# 第15章 增量净收益 355

**图 15.7** 使用正态分布和伽马分布的 CD 试验的增量净收益及置信区间

![](img/fe9ff008f88baacd415148b0b25dd58c_369_0.png)

**图 15.8** 使用正态分布和伽马分布的 CD 试验的成本效益接受性曲线

![](img/fe9ff008f88baacd415148b0b25dd58c_369_1.png)

## 356 使用 SAS 对观察性健康数据进行分析

对成本使用伽马分布，我们考察了协变量对成本和30天存活率的影响。协变量对30天存活率没有显著影响（$p=0.5843$），但整体效应显著（0.0315），且与治疗组之间存在边际显著的交互作用（0.0630）。最终模型包含了治疗组、$X$以及成本，而30天存活率模型仅包含治疗组，用于提供参数估计。详见程序 15.3。参数估计见表 15.3。由于成本模型中治疗组与 $X$ 之间存在交互作用，$\Delta_{\lambda}$ 及其方差的估计取决于 $X$ 的水平。当 $X=0$ 时，节省的成本更高，且治疗在患者亚组中更具成本效益。增量收益图和 CEAC 见图 15.9 和 15.10。对于 $X=0$，所有 $\lambda$ 值的 CEAC 均超过 0.9；对于 $X=1$，当 $\lambda$ 值大于每节省一个寿命 10,000 美元时，CEAC 超过 0.85。这为 T 的成本效益提供了有力的支持。

在 `http://www.andyllan.com/downloads` 可以获得用于生成 CEAC 和 INB（带置信区间）图表的 Microsoft Excel 工具。所需的唯一输入是五个参数估计、最小值、最大值以及置信水平。

以下代码显示了这些模型。有效性模型将 $\lambda$ 作为唯一的协变量，成本模型包含了组别、$X$ 及其它们的交互作用。

### 程序 15.3 协变量调整

```
proc glm data=yourData
    model cost = arm X*/ dist=gamma link=identity;
    output out=c predicted=pred_c;
run;

proc glm data=yourData desc
    model effectiveness = arm / dist=bin link=identity;
    output out=c predicted=pred_e;
run;

data temp; merge c;
    resid_e = effectiveness - pred_e;
    resid_c = cost - pred_c;
    keep resid_e resid_c;
run;

proc corr data=temp; var resid_e resid_c; run;
```

| 参数 | DF | 估计 | 标准误 | Wald 置信区间 | 置信区间 | 卡方 | Pr > ChiSq |
|---|---|---|---|---|---|---|---|

| 截距 | 1 | 10203.31 | 266.7096 | 9680.51 | 10726.05 | 1463.54 | <.0001 |
| arm | 1 | -1226.95 | 360.0549 | -1932.65 | -521.29 | 11.61 | 0.0007 |
| X | 1 | -1066.06 | 375.9776 | -1802.96 | -329.153 | 8.04 | 0.0046 |
| arm*X | 1 | 949.0657 | 510.5547 | -51.6032 | 1949.735 | 3.46 | 0.063 |

对于 $X=0$：$\hat{A}_{\lambda} =-1226.95$；$\hat{V}(\hat{A}_{\lambda}) = (360.0549)^2$。

## 第15章 增量净收益 357

对于 $X=0: \hat{C}(\hat{\Delta}_e, \hat{\Delta}_c)=(-0.03140)*(360.0549)*(0.0158)$。

$$\hat{\Delta}_e = 0.0507; \hat{V}(\hat{\Delta}_c) = (0.0158).$$

Pearson 相关系数，$N = 1356$

| 参数 | DF | 估计 | 标准误 | Wald 95% 置信区间 | 卡方 | Pr > ChiSq |
|---|---|---|---|---|---|---|

| 截距 arm | 1 | 0.8802 | 0.0125 | 0.8557 | 0.9047 | 4965.68 | <.0001 |
| | | | 0.0158 | 0.0197 | 0.0887 | 10.26 | 0.0014 |
| resid_e | | | | | | |
| resid_c | | | | | | |
| 1.0000 | -0.03140 | | | | | |

对于 $X=1$，$X$ 的值可以反转，得到如下：

| 参数 | DF | 估计 | 标准误 | Wald 95% 置信区间 | 卡方 | Pr > ChiSq |
|---|---|---|---|---|---|---|

| 截距 | 1 | 9137.25 | 265.0003 | 8617.86 | 9656.47 | <.0001 |
| X | 1 | -277.88 | 361.9759 | -329.15 | 10.26 | 0.0014 |
| arm+X | 1 | 1066.05 | 375.9776 | 329.15 | 8.04 | 0.0046 |
| | | | | | | |
| | | -949.06 | 510.5547 | -51.603 | 1949.73 | 3.46 | 0.063 |

对于 $X=0$，$\hat{A}_{\lambda} =-1226.95$；$\hat{V}(\hat{A}_{\lambda}) = (360.0549)^2$。

对于 $X=1$，$X$ 的值可以反转，得到如下：

| 参数 | $X=0$ | $X=1$ |
|---|---|---|

| $\hat{\Delta}_e$ | 0.0507 | 0.0507 |
| $\hat{\Delta}_c$ | -1226.95 | -277.88 |
| $\hat{V}(\hat{\Delta}_e)$ | 0.002496 | 0.002496 |
| $\hat{V}(\hat{\Delta}_c)$ | 0.0158 | 0.0158 |
| $\hat{C}(\hat{\Delta}_e, \hat{\Delta}_c)$ | -0.03140 | -0.03140 |

## 358 使用 SAS 对观察性健康数据进行分析

图 15.9 使用正态分布和伽马分布的 CD 试验的增量收益（INB（$）

![](img/fe9ff008f88baacd415148b0b25dd58c_369_0.png)

图 15.10 使用正态分布和伽马分布的 CD 试验的成本效益接受性曲线

![](img/fe9ff008f88baacd415148b0b25dd58c_369_1.png)

## 15.5 观察性研究

虽然许多成本效益分析是在随机试验中进行的，但这些方法也适用于观察性研究，尽管存在由于缺乏随机分配可能带来的偏差。通常，基于观察性研究数据的分析需要调整偏差。通用的方法包括：倾向评分和回归分析。如果数据量足够，倾向匹配是一个可能的选项。如果倾向匹配来自 RCT，则可以进行分析。倾向分层也是一个选项。对于倾向分层数据，需要进行回归分析，将有效性和成本对治疗指示变量以及倾向分层的虚拟指示变量（分层数减一）进行回归。对于非截断数据，分析师可以使用 `PROC GENMOD` 执行回归，如15.4节所示。这样不需要创建虚拟指示变量。对于截断数据，参考 Willan、Lin 和 Manca (2005) 使用的方法。

## 15.6 讨论

本文概述了使用增量净收益比较两组的成本效益。分析师根据支付意愿（WTP）估计 INB 并确定其相应的置信区间，并在贝叶斯方法绘制成本效益接受性曲线。CEAC 的优势在于它既显示了组间对比估计的幅度，又描述了其不确定性。INB 相比于 ICER 避免了与比率统计相关的所有问题。关于信息方法（参见 Willan 和 Pinto, 2006 以及“参考文献”中的其他来源）。

# 致谢

作者的资金助来自加拿大自然科学与工程研究委员会的发现资助（资助号：44868-03）。

# 参考文献

- Bang, H., and A. A. Tsiatis. 2000. “Estimating medical costs with censored data.” *Biometrika* 87(2): 329–343.

- Briggs, A. H., and A. M. Gray. 1998. “The distribution of health care costs and their statistical analysis for economic evaluation.” *Journal of Health Services Research & Policy* 3(4): 235–345.

- Briggs, A. H., D. E. Wonderling, and C. Z. Mooney. 1997. “Pulling cost-effectiveness analysis by its bootstraps, a non-parametric approach to confidence interval estimation.” *Health Economics* 60(4): 327–340.

- Briggs, A., R. Nixon, S. Dixon, and S. Thompson. 2005. “Health economics: parametric modeling of data cost: some simulation evaluation.” *Health Economics* 14: 421–428.

- Chaudhary, M. A., and S. C. Stearns. 1996. “Estimating confidence intervals for cost-effectiveness: an example from a randomized trial.” *Statistics in Medicine* 15: 1447–558.

- Cochran, W. G. 1997. *Sampling Techniques*. New York: John Wiley & Sons, Inc.

- Cook, J. R., M. Drummond, H. Glic, and J. F. Heysse. 2003. “Assessing the appropriateness of combining economic data from multinational trials.” *Statistics in Medicine* 22: 1955–576.

- Eckmann, S., and A. R. Witten. 2007. “Expected value of information and decision making in HTA.” *Health Economics* 16: 195–209.

- Eckmann, S., and A. R. Witten. 2008. “The option of delay in health technology assessment.” *Medical Decision Making* 28(3): 300–305.

- Eckmann, S., and A. R. Witten. 2008. “Time and expected value of sample information wait for no patient.” *Value in Health* 11(3): 522–526.

- Eckmann, S., and A. R. Witten. 2009. “Globally optimal trial design for local decision making.” *Health Economics* 18:203–216.

- Efron, R. B., and B. R. J. Tibshirani. 1993. *Introduction to the Bootstrap*. New York: Chapman & Hall

- Fenwick, E. J. O’Brien, and A. H. Briggs. 2004. “Cost-effectiveness acceptability curves—fallacies, and frequently asked questions.” *Health Economics* 13: 405–415.



- Grieve, R. Nixon, S. G. Thompson, and C. Normand. 2005. “Using multilevel models for assessing the amount of resource use and cost data.” *Health Economics* 14: 185–196.

- Lin, D. Y. 2000. “Linear regression analysis of censored medical costs.” *Biostatistical* 1:35–47.

- Lin, D. Y., E. J. Feuer, R. Etzioni, and Y. Wax. 1997. “Estimating medical costs from incomplete follow-up data.” *Biometrics* 53: 419–34.

- Lumley, T. Diehr, S. Emerson, and L. Chen. 2006. “The importance of normality assumption in large public health data sets.” *Annual Review of Public Health* 23: 151–169.

- Manca, A., N. Nixon, M. J. Sculpher, and A. H. Briggs. 2005. “Assessing generalisability by location in trial-based cost-effectiveness analysis: the use of multilevel models.” *Health Economics* 14: 471–475.

- Manning, W. G., and J. Mullahy. 2001. "Estimating log models: to transform or not to transform?" Journal of Health Economics: 20: 461–94.

- Nixon, R. M., and S. G. Thompson. 2004. "Parametric modeling of cost data in medical studies." Statistics in Medicine: 23: 1311–1331.

- Nixon, R. M., and S. G. Thompson. 2005. "Methods for incorporating corporate adjustment, subgroup analysis and between-center differences into cost-effectiveness." Health Economics: 14: 1217–1229.

- O'Brien, B. J., K. Gertsen, A. R. Willan, and A. Faulkner. 2002. "Is there a kink in consumers' threshold for cost-effectiveness in health?" Health Economics 11(2): 175–180.

- O'Hagan, A., and J. W. Stevens. 2001. "A framework for cost-effectiveness analysis from clinical data." Health Economics 10(4): 303–315.

- O'Hagan, A., and J. W. Stevens. 2003. "Assessing and comparing costs: how robust are the bootstrap based on asymptotic normality?" Health Economics 12(1): 33–49.

- P, E. M., A. R. Willan, and B. J. O'Brien. 2005. "Cost-effectiveness analysis for multicenter clinical trials." Statistics in Medicine: 24: 1965–1982.

- Thompson, S. G., D. E. Wan, and R. M. Turner. 2004. "Bayesian methods for analysis of binary outcome on the absolute scale." Statistics in Medicine: 23: 389–410.

- Thompson, S. G., and J. A. Barber. 2000. "How could cost data in pragmatic trials be analysed?" British Medical Journal 320(7243): 1197–1200.

- Wilke, R. J., H. A. Flick, D. Polsky, and K. Schulman. 1998. "Estimating cost-specific effectiveness from multicenter clinical trials." Health Economics 7(6): 481–493.

- Willan, A. R. 2007. "Clinical making and the expected value of information." Clinical Trials 4: 279–285.

- Willan, A. R., and A. H. Briggs. 2006. "Regression methods for covariate adjustment and subgroup analysis for noncensored cost data." Health Economics 13: 461–475.

- Willan, A. R., and D. Y. Lin. 2001. "Incremental net benefit in randomized clinical trials." Statistics in Medicine: 20: 1563–1574.

- Willan, A. R., B. J. O'Brien, and R. A. Leyva. 2001. "Cost-effectiveness analysis when the WTA is greater than the WTA," Statistics in Medicine: 20: 3251–3259.

- Willan, A. R., and A. H. Briggs. 2006. "Statistical Analysis of Cost-effectiveness Data." West Sussex, England: John Wiley Sons

- Willan, A. R., and E. M. Kowlier. 2008. "Determining optimal sample sizes for multi-stage randomized clinical trials using value of information methods." Clinical Trials 5: 289–300.

- Willan, A. R. 2008. "Optimal sample size determinations from an industry perspective based on the expected value of information." Clinical Trials 5: 587–594.

- Zhao, H., and L. Tian. 2001. “On estimating medical cost and incremental cost-effectiveness ratios with censored data.” Biometrics 57: 1002–1008.

# 删数据的成本与成本效益分析

赵洪伟

王洪坤

- 摘要 ..................................................................... 363
- 16.1 引言 ...................................................................... 363
- 16.2 统计方法 ................................................................................. 366
- 16.3 案例 ................................................................................ 369
- 16.4 讨论 ............................................................................ 379
- 致谢 ............................................................................ 380
- 参考文献 ....................................................................................... 181

## 摘要

成本评估和成本效益分析是医疗干预经济评估的重要组成部分。在临床试验和许多观察性研究中，由于患者失访或研究的行政终止，成本数据以及生存数据是不完整的。目前有许多成熟的统计方法和软件用于分析生存数据。然而，由于信息删失（删失成本与潜在成本之间的依赖性），用于生存类型数据的技术在分析删失成本数据时是的。在本章中，我们介绍了一些用于估计医疗成本和成本效益分析的统计方法。通过一个比较植入性心律复律器与传统治疗高风险心律失常患者有效性的临床试验案例来说明该方法。文中提供了执行分析的 `SAS` 代码。此外检查了模型假设并讨论了进一步的发展。

## 16.1 引言

随着医学的进步，医疗成本不断增加。然而，由于资源有限，医疗机构和健康政策制定者对不同治疗方案相关的医疗成本进行评估具有极大兴趣。通常，每个患者的平均成本是我们最关注的，因为干预的总成本可以从均值得出，而不是从成本分布的众数、中或其他分位数得出（Ramsey et al., 2005）。

根据意愿确定成本。为了处理这类问题，有人提出了烧结法（Duan, 1983）。另一个挑战是，医疗成本可能存在大量缺失数据，这是由于某些类型医疗成本的数据缺失或信息不全（Briggs et al., 2003）。不删除缺失数据、向前终结最后观测值或用观测数据的均值代替缺失值的朴素方法并不令人满意。相反，多重插补（Rubin, 1987）和贝叶斯方法（Schaefer, 1997; Van Buuren, 1999）被推荐用于计算缺失数据。根据 Little 和 Rubin (1987) 的分类，缺失数据通常可分为三类：

- 完全随机缺失 (`MCAR`)，其中缺失机制与我们关注的变量无关
- 随机缺失 (`MAR`)，其中缺失依赖于观测变量
- 非随机缺失 (`NMAR`)，其中缺失依赖于未观测变量

处理 `MCAR` 和 `MAR` 情况通常比较容易；当 `NMAR` 成立时，推断将依赖于对缺失机制的假设，而这些假设无法从可用数据中验证。

缺失数据的一种是由删失引起的，可能是由于研究中的退出或研究设计的行政删失。本章主要关注这一问题。与其他缺失机制类似，删失也可以分为三类，取决于：

- 删失与生存时间和成本无关（完全随机删失）
- 删失仅依赖于未观测变量（随机删失）
- 删失依赖于某些未观测变量

我们将证明，即使在完全随机删失的第一种情况下，估计平均成本也是具有挑战性的。由于成本删失，我们无法通过简单地平均所有受试者的医疗成本来估计平均成本。这将由于删失时间后的成本等于零，从而低估真实成本。完整观测成本的平均值得到的估计量会偏向生存时间较短患者的成本。即使在删失独立于生存时间的假设有效，基于标准技术（如 `Kaplan-Meier` 估计量）的方法也会产生偏估计。这是由于所谓的“信息删失”（informed censoring），Lin 和同事 (1997) 首次注意这一点。对于个体而言，成本积累率较高的个体往往在删失时间和潜在的未删失生存时间都会产生更多的医疗成本，即使删失完全独立于失效时间也是如此。

针对带有删失数据的平均成本估计，已经提出了许多方法（Young, 2005）。我们关注在不使用信息的情况下估计均值。成本估计中协变量信息的进一步开发将在本章最后一节讨论。由于无法以非参数方式估计寿命成本，Huang 和 Louis (1998) 提出了一种联合估计生存时间和寿命成本的方法。处理删失问题的另一种方法是将医疗成本限制在特定期限内，这取决于数据的可用性。由于经济学研究的重点通常是特定生存时间的边缘分布，我们在本章剩余部分关注第二种方法。

## 第16 章 删失数据的成本效益分析

使用删失数据在时间限制内估计平均成本的方法分为两类：

- 仅使用每个个体最终成本信息的方法
- 使用完整和删失个体的成本历史信息的方法

通常情况下，前者效率较低（即估计量方差较大），而后者更为复杂但在渐近意义上更有效。

Lin 和同事 (1997) 针对使用总成本或成本历史估计平均成本提出了三种不同的估计量。当删失时间为离散时，他们的方法提供了一致性估计。Bang 和 Tsiatis (2000) 使用逆加权方案提出了几种用于删失数据估计成本的一致且渐近正的估计量。他们所谓的划分估计量将成本历史分为子区间。随后，Zhao 和 Tian (2001) 提出了一种更简便且高效的估计量，它也属于 Bang 和 Tsiatis (2000) 的估计量类。在最近的一篇文章中，Zhao 和同事 (2007) 在 Lin 和同事 (1997)、Bang 和 Tsiatis (2000) 以及 Zhao 和 Tian (2001) 引入的估计量之间建立了效率。

成本经常用于成本效益分析以比较不同的治疗方案并评估新疗法的经济影响。Willan 和 Lin (2001) 以及同事 (2003) 说明了增量收益（`INB`）的使用，它取决于决策者对额外单位效果的支付意愿（标记为 $\lambda$）。这种方法的主要优点是依赖 $\lambda$，主要缺点是数学上难以定义或通常未知。另一种成本效益衡量标准是增量成本效益比（`ICER`），定义为节省额外一年（质量调整后）寿命所产生的额外成本。当两种治疗方案中一种的成本更高时，`ICER` 非常有用。`ICER` 长期以来被认为是标准工具。

为了说明，我们使用多中心除颤器试验（`MADIT`）的案例，该试验比较了植入式除颤器与传统疗法（Lin 等, 1998）。本章大纲如下：16.2 介绍方法；16.3 讨论使用总成本或成本历史的方法；16.4 考察成本效益的假设和其他方法。

## 16.2 统计方法

### 16.2.1 符号与假设

如果每个患者都随访到时间 $L$ 或死亡，那么我们就拥有每个完整的成本，可以使用样本均值等标准统计方法估计平均成本。然而，在大多数情况下，由于删失，所有患者的成本和生存时间并未完全观测。

我们的目标是从一组观测数据 $\{X_i, \Delta_i, U(X_i) \leq X_i\}, i=1,\dots,n$ 估计直到最大时间 $L$ 的成本均值 $\mu=E\{U(T_i)\}$。对于研究中的第 $i$ 个人，令 $T$ 表示其生存时间，$C$ 表示删失时间。删失被假设为随机且独立的。由于删失，$T_i$ 和 $C_i$ 仅从随访时间 $X_i=\min(T_i, C_i)$ 可观测。由于删失，在不做出分布假设的情况下无法估计整个历史的成本。因此，我们只考虑积累到期限 $L$ 的成本，在该处有合理的数据。因此，我们考虑 $T_i^*=\min(T_i, L)$。为了符号起见，我们将省略上标 $^*$ 并继续使用 $T_i$。

如果未记录成本历史，我们只看到每个个体的最终成本 $U(X_i)$，以及那些在删失之前发生感兴趣事件的个体 $U_i=U(T_i)=U(X_i)$。令删失指示 $\Delta_i=1$ 表示观测到死亡，$\Delta_i=0$ 表示生存时间被删失。

### 16.2.2 估计平均成本

Bang 和 Tsiatis (2000) 提出了一种简单的平均成本加权估计量，其形式如下：

$$\hat{\mu}_{WT}=\sum_{i=1}^{n}\frac{\Delta_i U_i}{\hat{K}(T_i)},$$

其中 $\hat{K}(T)$ 是用于 $K(t)=Pr(C > t)$ 的 `Kaplan-Meier` 估计量，即删失变量 $C$ 在时间 $T$ 处的生存分布。在这个简单的加权估计量中，通过对每个未删失个体的观测概率加权来考虑删失。Bang 和 Tsiatis (2000) 证明该估计量是一致的且渐近正态的。其方差可以通过以下估计

## 第 16 章 删失数据的成本与成本效益分析 367

$$\hat{V}(\hat{\beta}_{WT}) = \frac{1}{n} \sum_{i=1}^{n} \frac{\Delta(U_i - \beta_{WT})^2}{R(T_i)} + \frac{1}{n} \sum_{i=1}^{n} \frac{(1 - \Delta_i)^2}{R(C_i)^2} \{G_i(U_i)^2 - G_i^2(C_i)\} \quad (2)$$

其中

$$G_i(U) = \frac{1}{n\hat{S}(X_i)} \sum_{i=1}^{n} \Delta U_i(X_i)(X_i \geq X_i) \hat{R}(X_i)$$

Zhao 等同事（2007）已经证明，如果区间边界选择在那些删失时间，那么该估计量与 Lin 等同事（1997）的估计量 $T$ 等价。



简单加权估计量仅利用了完整观测的数据。因此它不是高效的，特别是在删失严重的情况下。改进它的一种方法是获取来自删失观测的信息或来自删失和未删失观测的可用成本。为了提高简单加权估计量的效率，Bang 和 Tsiatis（2000）提出了分区估计量。它将区间 `[0, L]` 分成更小的区间，然后对所有区间进行求和。后来，Zhao 和 Tian（2001）展示了一种更方便、更高效的估计量，它属于 Bang 和 Tsiatis（2000）针对平均成本的通用估计量类，但它不需要对健康史进行分区。Priefer 和 Bang（2005）为这种改进的估计量建议了一个易于使用的公式，其可以写为：

$$\hat{\mu}_{IMP} = \frac{1}{n} \sum_{i=1}^{n} \frac{\Delta U_i}{\hat{R}(T_i)} + \frac{1}{n} \sum_{i=1}^{n} \frac{(1 - \Delta_i)}{\hat{R}(C_i)} \{U_j - \bar{U}(C_j)\} \quad (3)$$

$$\bar{U}(C_j) = \frac{\sum_{i=1}^{n} U_i(C_i)(X_i \geq C_j)}{\sum_{i=1}^{n}(X_i \geq C_j)}$$

其中 $\bar{U}(C_j)$ 是在时间 $C_j$ 仍在观测状态下的个体的平均成本。Zhao 等同事（2007）已经证明，当分区边界选择在删失时间时，该估计量与 Bang 和 Tsiatis（2000）的分区估计量以及 Lin 等同事（1997）的 A 和 B 估计量等价。

成本改进估计量的方差估计给出：

$$\hat{V}(\hat{\mu}_{IMP}) = \hat{V}(\hat{\mu}_{WT}) \frac{1}{n^2} \sum_{j=1}^{n} \frac{(1 - \Delta_j)^2}{\hat{R}(C_j)\hat{R}(\bar{C})} \sum_{i=1}^{n} \frac{\Delta L_i(X_i)(X_i \geq X_i)}{\hat{R}(T_i)} \{U_i(X_i) - \bar{U}(X_i)\} \quad (4)$$

## 368 使用 SAS 分析观测数据

这种改进估计量并不保证比简单加权估计量高效，但在大多数现实情况下，它的表现会优于简单加权估计量。对于两种估计量，我们假设可以计算个体在删失或死亡某一时刻的总成本。当存在缺失数据时，必须首先采用适当的处理方法（Briggs 等，2003）。Wang 和 Zhao（2006）讨论了某些个体成本删失早于生存删失的特殊情况。

### 16.2 增量成本效益比及其信区间

我们考虑两一组试验的增量成本效益比。对于组 $k(k=0,1)$ $\hat{\mu}_k^U$ 为平均成本，$\hat{\mu}_k^S$ 为限制在 `[0, L]` 窗口内的平均生存时间。ICER 通过下式估计：

$$\frac{\hat{\mu}_1^U - \hat{\mu}_0^U}{\hat{\mu}_1^S - \hat{\mu}_0^S}, \quad (5)$$

其中 $\hat{\mu}_k^U$ 和 $\hat{\mu}_k^S$ 分别是组 $k(k=0,1)$ 的平均成本和平均生存时间估计量。平均生存时间可以使用 `[0, L]` 上生存函数的 Kaplan-Meier 曲线下的面积来估计，这等于 $\hat{\mu}^T = \frac{1}{n}\sum_{i=1}^T \frac{\Delta t_i}{d_i}$，$T$ 在时间 $L$ 截断。

获取 ICER 信区间的方法有。第 14 章提供了自助方法的示例。我们使用 Fieller 定理（Fieller, 1954），因为 (5) 中的分子 $x = \hat{\mu}_1^U - \hat{\mu}_0^U$ 和分母 $y = \hat{\mu}_1^S - \hat{\mu}_0^S$ 渐近服从双正态分布，符合该定理的要求。因此，ICER 的 $100(1-\alpha)$ 百百分比置信限为：

$$xy - z_{\alpha/2}^2S_{xy} \pm \sqrt{f(x,y,S_{xx},S_{yy})(y^2)} \quad (6)$$

其中 $f(x,y,S_{xx},S_{yy}) = S_{xx}y^2 + S_{yy}x^2 - 2S_{xy}xy$。

## 第 16 章 删失数据的成本与成本效益分析 369

### 16.3 示例

#### 16.3.1 研究描述

为了说明讨论的方法，我们使用多中心自动除颤试验（MADIT）的数据。MADIT 是一项随机临床试验，检查了植入式除颤器（ICD）预防猝死的有效性（Moss 等，1996）。从 36 个中心共募了 181 名患者，89 人分配到治疗组接受 ICD，92 人分配到控制组接受常规治疗。第一个入组患者随访了 61 个月，最后一个少于 1 个月。原始成本分析限制在 4 年期间，并使用与 Lin 等同事（1997）提出的类似的方法进行。数据被严重删失，ICD 组删失率为 70%，常规治疗组删失率为 48%。改进估计量允许我们获取来自删失观测的信息。对于成本效益分析，ICER 也使用估计成本的改进方法进行计算。正如成本效益分析中常见的，成本和生存时间都按 3% 的年利率折现。

#### 16.3.2 数据分析

每个治疗组的数据来自单独的文件，一个包含生存信息，另一个包含成本。生存数据包含三个变量：个体 ID、生存时间（天）和生存状态（1=死亡；0=删失）。由于许多成本（如住院费用）在特定时期内积累，因此它们通过开始时间、停止时间和期间内的总成本（美元）进行记录。这些成本已按 3% 的年利率折现。以下是检查 ICD 组两个文件前 10 个观测值的 SAS 代码和输出。

### 程序 16.1 查看生存文件的 SAS 代码

```
filename local "C:\Documents and Settings\My Documents\Example";
nproc print data=local.survl (obs=10);
run;
```

## 370 使用 SAS 对观察性健康数据的分析

程序 16.1 的输出

| Obs | id | delta | surv |
|---||--|--|--|
| 1 | 1 | 0 | 167 |
| 2 | 2 | 0 | 1582 |
| 3 | 3 | 0 | 1792 |
| 4 | 4 | 0 | 1303 |
| 5 | 5 | 0 | 1204 |
| 6 | 6 | 0 | 763 |
| 7 | 7 | 0 | 453 |
| 8 | 8 | 0 | 1644 |
| 9 | 9 | 0 | 1818 |
| 10 | 10 | 10 | 804 |

程序 16.2 查看成本文件的 SAS 代码 (obs=10)

```
proc print data=local.cost1;
run;
```

程序 16.2 的输出

| Obs | cid | start | stop | cost |
|---|---|---|---|---|
| 1 | 1 | 1 | 29 | 133.12 |
| 2 | 1 | 1 | 29 | 16.44 |
| 3 | 1 | 1 | 158 | 421.75 |
| 4 | 1 | 1 | 158 | 28.94 |
| 5 | 1 | 1 | 158 | 25.28 |
| 6 | 1 | 1 | 158 | 29.80 |
| 7 | 1 | 1 | 158 | 2.79 |
| 8 | 1 | 5 | 7 | 32764.22 |
| 9 | 1 | 29 | 158 | 79.48 |
| 10 | 1 | 30 | 120 | 150.99 |

分析过程中使用了 SAS/IML 软件。由于我们的公式涉及 Kaplan-Meier 估计器，我们需要在 SAS Stat Studio (SAS/IML Studio) 中调用 SAS LIFETEST 程序，这使我们能够完成此任务。以下程序在环境中运行。对于每组生存和成本数据、用户定义的时间限制 `L` 以及折现率 `r`，程序会计算并打印成本估计值（简单加权和改进型）、平均（折现）生存时间以及估计的方差和协方差。

### 程序 16.3 成本分析的 SAS 代码

```
libname local "C:\Data and Settings\hongweiMy\Documents\Home\SASBook\Example";
```

```
/* 读取生存数据 */
use local.surv;
read all var {id delta surv};
/* 受者 ID、死亡指示和生存时间; */
close local.surv;
```

```
/* 读取成本数据 */
use local.cost;
read all var {cid start stop cost};
/* 受者 ID、成本开始日期、停止日期、产生的成本 */
show names;
close local.cost;
```

```
/* 定义全局变量 */
n=nrow(id); /* 受者数量 */
nobs=nrow(cid); /* 成本数据的总观测数 */
L=1461; /* 时间限制 */
r=0.03; /* 年度折现率 */

/* 将生存时间截断到 L，命名新变量 tsur 和 tdelta */
run TranSurv(delta, surv, tdelta, tsur);

/* 将最大的观测值视为失效 */
do i = 1 to n;
if (tsur[i] == L) then tdelta[i]=1;
end;

/* 计算删失数据的百分比 */
percens=CalCenter(tdelta);
print , "Percent of censoring = %%%"

/* 计算 K(t)=Pr(C>t) 的 Kaplan Meier 估计器，命名为 kc */
run KmCal(tsur,tdelta,kc);

/* 计算 S(t)=Pr(C>t) 的 Kaplan Meier 估计器，命名为 s */
censor=j(n,1,0);
do i = 1 to n;
censor[i]=1-tdelta[i];
end;
run KmCal(tsur,census,s);

/* 计算每个受者的总成本，简单加权估计器需要此项 */
run CalCost(cid,start,stop, cost, id, tsur, tcost);

/* 使用加权估计器计算平均值 */
mean sw=CalourMean(tdelta, kc, cost);
print , "Weighted estimator for mean cost = mean_sw"

/* 计算简单加权估计器的标准误 */
var sw=CalourVar(tsur, tdelta, s, kc, mean_sw);
se sw=sqrt(var);
print , "Standard error for the simple weighted estimator = se_sw"

/* 计算平均生存时间及其标准误 */
dsurv=j(n,1,0);
do i = 1 to n;
dsurv[i] = 365.25/r * (1.0-exp(-r*tsur[i]/365.25));
end;
mean T=CalourMean(tdelta, kc, cost);
var T=CalourVar(tsur, tdelta, s,,, mean_sw);
se T=sqrt(var);
print , "Mean survival time = T"
print , "Standard error for mean survival time =_T"

/* 每个删失时间的累积成本，改进估计器需要此项 */
run CalCost(cid,start, stop, id, id, tdelta);

/* 计算平均成本的改进估计器及其标准误 */
CalMeanAdd(tsur, tdelta, kc, s, tcost,
meanimp = meanimp;
impimp =varsubub
, "imp estimator for mean cost = mean_imp;
print, "Standard of of estimator = imp;

/* 计算平均生存时间与简单加权估计器之间的协方差 */
cov_sw = CalCov(tdelta, tsur, s,,,, mean_ T;
print, "Covariance between mean time and simple weighted estimator = cov_sw;

/* 计算平均生存时间与改进估计器之间的协方差 */
cov_imp=CalCovSub(td,, t,, s,,,,,,,,,,,,imp;
print, "Covariance between mean time and improved estimator = cov_imp;

/* 截断生存时间到 L 的子程序 */
start TrSunv(delta, tsur, tdelta) global
(L,n);
tsurv=delta;
tdelta=delta;
do i = 1 to n;
  if (tsurv[i]>L then
    tsurv[i]=L;
    tdelta[i]=1;
  end;
finish TrSunv;
```

```
/* 计算删失百分比的子程序 */
start CalCensor(tdelta) global (L,n);
cens=sum(cens)/n;
finish CalCensor;
```

```
/* 计算 K(t)=Pr(C>t) 的 Kaplan Meier 估计器的子程序 */
start KmSur(surv, delta,kc);
create InputDataSet{var delta};
append;
close InputDataSet;
```

```
use Out;
read all (tsur tpdelta);
run ChangeKmv(tsurv, tpdelta, survival, kc);
close Out;
finish KmCal;
```

```
/* 向前传递生存函数估计值的子程序 */
start ChangeKmv(tsurv, tdelta, survival, kc) global
(L,n)
minkc=1000;
nrow=n(tsurv);
kc=j(n,1,0);

do j=1 to nn;
if (survival[j]>0 & survival[j]<minkc) then do
minkc=survival[j];
maxtime=tpsur[j];
end;

do i=1 to n;
if (sur[i]>maxtime) then kc[i]=minkc;
elelse do
 j=1 to nn;
if (sur[i]=tpsur[j]) then kc[i]=survival[j];
end;
end;
finish ChangeKmv;
```

```
/* 计算总成本的子程序 */
/* 与计算累积成本的程序相比，此子程序运行时间更短 */
start CalCost(cid, start, stop, cost, id, tsurv, tcost) global (n, nobs);
tcost=j(n,1,0);
do i=1 to n;
do k=1 to nn;
if (cid[k]=id[i] & start[k]<= tsurv[i]) then do
if (stop[k]>tsurv[i]) then
tcost[i]=tcost[i]+cost[k]*(tsurv[i]-start[k]+1.0)/(stop[k]-start[k]+1.0);
else tcost[i]=tcost[i]+cost[k];
end;
end;
finish CalCost;
```

```
/* 计算平均成本的简单加权估计器的子程序 */
start CalMean(tdelta, kc, tcost) global (n);
mymean=0;
do i=1 to n;
if (tdelta[i]=1) then mymean = mymean + tcost[i]/kc[i];
end;
mymean=mymean/n;
return(mymean);
finish CalMean;
```

## 374 使用 SAS 对观察性医疗数据的分析



## 计算简单加权估计器方差的子程序

``` 
/* 计算简单加权估计器方差的子程序 */*
start CalOurVar(tsurv, tdelta, s, kc, tcost, mymean) global (n);
temp1=0; /* 公式 (2) 的第 1 部分 */
temp2=0; /* 公式 (2) 的第 2 部分 */
do i=1 to n;
if (tdelta[i]=1) then temp1 =temp1 + (tcost[i]-mymean)**2/kc[i];
end;
temp1=temp1/n;

do j=1 to nn;
f=0;
if (tdelta[j]=0) then do;
        do i=1 to n;
            if (tdelta[i]=1&tsurv[i]=j) then do;
                e = e + tcost[i]/kc[i];
                f = f + (tcost[i])**2/kc[i];
            end;
        end;
        e = e / (s[j]*n);
        f = f / (s[j]*n);
        temp2 = temp2 + (f-e*e)/(kc[j]*kc[j]);
    end;
temp2=temp2/n;

myvar = temp1+temp2;
myvar=myvar/n;
return(myvar);
finish CalOurVar;
```

## 计算累积成本的子程序

``` 
/* 计算累积成本的子程序 */
/* 计算改进估计器需要此程序 */
start CalCost(cid, start, stop, cost, id, tsurv, tdelta, culcost) global
(n,culcost[n,0]);
do i=1 to n;
    do j=1 to n;
        if (tsurv[i]=tsurv[j] & tdelta[j]=0) then do
            do k=1 to n;
                if (cid[k]=id[i] & start[k]<= tsurv[j]) then do
                    if (stop[k]>tsurv[j]) then
                        culcost[i,j]=culcost[i,j]+cost[k]*(tsurv[j]-start[k]+1.0)/(stop[k]-start[k]+1.0);
                    else culcost[i,j] = culcost[i,j] + cost[k];
                end;
            end;
        end;
    end;
end;
finish CalCulCost;
```

## 计算改进估计量和方差的额外项

```sas
/* 首先在删断处计算 Ubar[j] 和风险集 y[j] */
Ubar=j(n,1,0);
y=(n,1,0);
do j=1 to n; do
  if (delta[j]==0) then do
    do i=1 to n;
      if (tsur[i]==tsur[j]) then do
        Ubar[j]= Ubar[j]+culcost[i,j];
        y[j]= y[j]+1;
      end
    end
  end
  Ubar[j]= Ubar[j]/y[j];

/* 接下来计算改进估计量和方差的额外项 */
part1=0; /* 改进估计量的额外项 */
part2=0; /* 改进估计量方差公式中的第二项，方程 (4) */
part3=0; /* 改进估计量方差公式中的第三项，方程 (4) */
do j=1 to n;
  if (delta[j]==0) then do
    part1 = part1+(tcost[j]-Ubar[j])/kc[j];
    gu=0;
    part2temp=0;
    part3temp=0;
    do i=1 to n;
      if(delta[i]==1 & tsur[i]>=tsur[j]) then
        gu = gu + cost[i]/kc[i];
    end;
    gu = gu/( s[j]*);

    do i=1 to n;
      if(delta[i]==1 & tsur[i]>=tsur[j]) then
        part2temp= part2temp+(tcost[i,j]-gu*(culcost[i,j]-Ubar[j]))/kc[i];
    end;
    part2 = part2 + part2temp/(y[j]*kc[j]);

    do i=1 to n;
      if(tsur[i]==tsur[j]) then
        part3temp = part3temp/(y[j]*kc[j])*kc[j];
    end;
  end;
  part1 = part1/n;
  meanadd=part1;
  varsub=(2.0*part2-part3)/(n*n);
finish CalMeanAdd;
```

## 计算平均生存时间与简单加权成本估计量之间协方差的子程序

``` 
/* 计算平均生存时间与简单加权成本估计量之间协方差的子程序
start CalOurCov(tdelta, tsur, s, kc, tcost, mymean, dsur, tmean) global
(n);
templ = 0;
temp2 = 0;

do i=1 to n;
  if (tdelta[i]=1) then templ = templ + tcost[i]*dsurv[i]/kc[i];
end;

templ = templ/n;
templ = templ - mymean * tmean;

do j=1 to n;
  gtc=0;
  ggt=0;
  gc=0;
  if (tdelta[j]=0) then do;
    do i=1 to n;
      if (tdelta[i]=1 & tsurv[i]=tsurv[j]) then do;
        gtc = gtc + tcost[i]*dsurv[i]/kc[i];
        gt = gt + dsurv[i]/kc[i];
        gc = gc + tcost[i]/kc[i];
      end;
    end;
  end;
  gtc = gtc/(s[j]*n);
  gt = gt/(s[j]*n);
  gc = gc/(s[j]*n);
  temp2 = temp2+(gt-gt*gc)/(kc[j]*kc[j]);
end;
temp2=temp2/n;
mycov = templ+temp2;
mycov = mycov/n;
return(mycov);
finish CalCov;
```

## 计算生存时间与改进成本估计量之间协方差额外项的子程序

``` 
/* 计算生存时间与改进成本估计量之间协方差额外项的子程序
start CalCovSub(tdelta, tsurv, s, kc, dsurv) global (n);

/* 首先在删断处计算 Ubar[j] 和风险集 y[j] */
Ubar=j(n,1,0);
do j=1 to n;
  if (tdelta[j]=0) then do;
    do i=1 to n;
      if (tsurv[i]=tsurv[j]) then do;
        Ubar[j] = Ubar[j] + tcost[i,j];
        y[j] = y[j] + 1;
      end;
    end;
  end;
  Ubar[j]=Ubar[j]/y[j];

/* 接下来使用改进成本估计量计算协方差的额外项 */
part2=0;
do j=1 to n;
  if (tdelta[j]=0) then do;
    part2temp=0;
    do i=1 to n;
      if(delta[i]=1 & tsurv[i]=tsurv[j]) then
        gt = gt + dsurv[i]/kc[i];
    end;
    gt = gt/(s[j]*n);
    do i=1 to n;
      if(delta[i]=1 & tsurv[i]>=tsurv[j]) then
        part2temp = part2temp+(culcost[i,j]-Ubar[j])*(dsurv[i]-gt)/kc[i];
    end;
    part2 = part2 + part2temp/(y[j]*kc[j]);
  end;
covsub=part2/(n*n);
return(covsub);
finish CalCovSub;
```

## 376 使用 SAS 分析观察性健康数据

### ICD组程序的16.3输出

| PERCENS | |
| :--- | :--- |
| 删断比例 = 0.696292 | MEAN_SW |
| 简单加权成本估计量 = 110108.86 | SE_SW |
| 简单加权估计量的标准误 = 6929.7977 | MEAN_T |
| 平均生存时间 = 1261.4032 | SE_T |
| 平均生存时间的标准误 = 35.99617 | MEAN_IMP |
| 改进成本估计量 = 99311.725 | SE_IMP |
| 改进估计量的标准误 = 5481.115 | COV_SW |
| 平均生存时间与简单加权估计量之间的协方差 = 24943.547 | COV_IMP |
| 平均生存时间与改进成本估计量之间的协方差 = 30485.773 | |

### 治疗组程序的16.3输出

| PERCENS | |
| :--- | :--- |
| 删断比例 = 0.4782609 | MEAN_SW |
| 简单加权成本估计量 = 70034.696 | SE_SW |
| 简单加权估计量的标准误 = 9267.5059 | MEAN_T |
| 平均生存时间 = 968.77197 | SE_T |
| 平均生存时间的标准误 = 58.370098 | MEAN_IMP |
| 改进成本估计量 = 72544.906 | SE_IMP |
| 改进估计量的标准误 = 8529.8308 | COV_SW |
| 平均生存时间与简单加权估计量之间的协方差 = 24852.951 | COV_IMP |
| 平均生存时间与改进成本估计量之间的协方差 = 29764.298 | |

程序16.4 使用改进成本估计量计算 ICER（每年节省 $1,000）及其置信区间。

## 377 程序16.4 估计 ICER 及其 95% 置信间的 SAS 代码

```sas
cost1=72544.91/1000;

secost1=8529.83/1000;

surv1=968.77/365.25;

sesurv1=58.37/365.25;

covcs1=29764.30/1000/365.25;

cost2=99311.7/1000;

secost2=5481.11/1000;

surv2=1261.40/365.25;

sesurv2=36.00/365.25;

covcs2=30485.77/1000/365.25;

icer=(cost2-cost1)/(surv2-surv1);

run CalCIICER(cost1,secost1,surv1,sesurv1,covcs1,
cost2,secost2,surv2,sesurv2,covcs2,lowbd,upperbd);
```



## 378 使用 SAS 分析观察性健康数据

## 第16 章 删断数据的成本与效益分析

### 16.4 讨论

在本章中，假设删断是随机的，且与生存时间和成本积累过程无关。这一假设在临床试验中通常成立，因为删断主要是由研究行政终止引起的。在观察性研究中，这一假设可能并不合理。然而，如果删断过程可以通过已知变量进行建模，仍然可以使用逆概率加权方法。在这种情况下，删断变量的生存概率将不会通过非参数 Kaplan-Meier 估计量获得，如果满足比例风险假设，则可以通过回归方法（如比例风险模型，Cox, 1972）进行估计。另一种替代方案是调整 Kaplan-Meier 估计量，使用逆概率治疗加权来调整删断生存分布的混杂因素（Xie and Liu, 2005）。当在时间 L 接近结束有大量删断时，从删断变量生存概率倒数得到的权重可能是一个巨大的数字。因此，少数极小概率可能会夸大该估计量。在这种情况下，人们可能希望减少限制 L；当尾部区域有很多删断值时，估计成本是困难的。

成本数据通常是右偏的，患者会积累巨大的成本，而所讨论的方法完全是非参数的，这意味着对于成本历史或生存时间，都没有分布假设。然而，我们需要使用足够大的样本，因为非参数方法依赖于大样本理论。

我们讨论了如何使用 Feller 方法来获得增量成本效益比（ICER）的置信区间。只要 ICER 的分子和分母符合二元正态分布，Feller 方法就能为我们提供具有正确覆盖概率的置信集，我们的方法渐近地满足这一点（Efron and Tibshirani, 1986, 1993）。参见第14章。另一种方法是实现自助法。

# 第 16 节 截删数据的成本与效益分析 381

# 参考文献

Bang, H., and A. T. Tsiatis. 2000. “使用截删数据估算医疗成本。” Biometrika 87: 329–343.

Briggs, A., T. Clark, J. Wolstenholme, and P. Clarke. 2003. “缺失……假设为随机缺失：不完整数据的成本分析。” Health Economics 12(5): 377–392.

Cox, D. R. 1972. “回归模型与生命表（含讨论）。” Journal of the Royal Statistical Society B 34: 187–220.

Duan, N. 1983. “平滑估计：一种非参数化重变换方法。” Journal of the American Statistical Association 78: 605–610.

Efron, B., and R. Tibshirani. 1986. “用于标准误、置信区间和其他统计准确性测量的自助法。” Statistical Science 1: 54–75.

Efron, B., and R. Tibshirani. 1993. 自助法导论。纽约: Chapman & Hall/CRC.

Feller, E. C. 1954. “线性估计中的问题。” Journal of the Royal Statistical Society, Series B (统计方法学) 16(2): 175–185.

Gold, M. R., J. E. Siegel, L. B. Russell, and M. C. Weinstein, 1996. 健康与医学中的成本效益。纽约: Oxford University Press.

Horvitz, D., and J. D. Thompson. 1952. “有限总体抽样的泛化。” Journal of the American Statistical Association 47(260): 663–685.

Huang, Y., and T. A. Louis. 1998. “生存与时间变量联合分布的非参数估计。” Biometrika 85: 788–795.

Jain, A. K., and R. L. Blackwell. 2002. “医疗成本数据的柔性回归建模。” Biostatistics 31: 101–118.

Kaplan, E., and P. Meier. 1958. “不完整观测值的非参数估计。” Journal of the American Statistical Association 53: 457–481.

Lin, D. Y. 2000a. “用于截删医疗成本的比例均值分析。” Biometrics 66: 775–778.

Lin, D. Y. 2000b. “截删医疗成本的线性回归分析。” Biostatistics 1: 35–47.

Lin, D. Y., E. J. Fuzer, R. Etziani, and Y. Wax. 1997. “从不完整随访数据估算医疗成本。” Biometrics 53: 419–434.

Little, R. A., and D. B. Rubin. 1987. 缺失数据的统计分析。纽约: John Wiley & Sons.

Moss, A. J., W. J. Hall, D. S. Cannon, J. Daubert, S. L. Higgins, H. Klein, J. H. Levine, S. Saksena, A. Waldo, D. Wilter, W. M. Brown, and M. He. 1996. “高心室性律失常风险冠心病患者植入除颤器后的生存率提高。” 新英格兰医学杂志 335(26): 1993–1940.

Mush, I. L., W. J. Hall, Z. Zwanziger, E. Gajary, M. Andrews, R. Marron, K. Hou, and A. J. Moss for MADIT Investigators. 1998. “植入式心脏除颤器的成本效益：MADIT 结果。” Circulation 97(21): 2129–2135.

Pfeifer, E., and H. Bang. 2005. “截删数据的均值估计。” Statistics in Medicine 19(4): 48–66.

Ramsey, S., R. Willke, A. Briggs, R. Brown, B. Buxton, H. Glick, B. Liljas, D. Petetti, and S. Reed. 2005. “临床试验成本效益研究的良好实践：ISPOR 工作报告。” Value in Health 8(5): 521–533.

# 382 使用 SAS 分析观察性健康数据

Rubin, D. B. 1997. 调查响应的多重填补。纽约: John Wiley.

Schafer, J. L. 1997. 不完整多变量数据分析。伦敦: Chapman & Hall.

van Buren, S., H. Bosh, and D. L. Kook. 1999. “生存分析中协变量的多重填补。” Statistics in Medicine 18(6): 681–694.

Wang, H., and H. Zhao. 2006. “差异截删数据的增量成本效益及其置信区间。” Biometrics 62: 570–575.

Willan, A. R., and D. Y. Lin. 2001. “随机试验中的增量净收益。” Statistics in Medicine 20: 1563–1574.

Willan, A. R., D. Y. Lin, and A. Manca. 2005. “带有截删数据的成本效益分析回归方法。” Statistics in Medicine 24: 131–145.

Willan, A. R., E. B. Chen, R. J. Cook, and D. Y. Lin. 2003. “质量调整生存数据的随机试验中的增量净收益。” Statistics in Medicine 22: 353–362.

Xie, J., and C. Liu. 2005. “用于逆概率治疗加权的生存数据的调整 Kaplan-Meier 估计和秩检验。” Statistics in Medicine 24: 3089–3110.

Young, T. A. 2005. “存在截删情况下的均值估计：方法评估。” PharmacoEconomics 23(12): 1229–1242.

Zhao, H., and L. Tian. 2001. “关于某些截删医疗成本的等性。” Biometrics 57: 1002–1008.

Zhao, H., H. Bang, H. Wang, and P. Pfeiffer. 2007. “带有截删数据的增量成本估计量的估计。” Statistics in Medicine 26: 4520–4530.

# 使用 SAS 对观察性健康数据进行分析

在随机对照试验 `RCTs` 中，通过使观察者/研究人员对患者接受的治疗进行盲法，以及通过定期的结构化数据收集（这对所有比较组都是相同的），可以最大限地减少测量偏差。然而，设计特征对于观察性研究并非总是可行。在无法实施盲的情况下，可以使用其他策略（如第 17.3 节）来减少测量偏差和资助者偏差。

在专注于减少资助者和观察者偏差的策略之前，我们提供了观察性研究设计中关键问题的概述（见第 17.2 节）。这些讨论并非为了详尽，而是为了提出重要问题并为您提供更详细讨论的参考文献。

## 17.2 一般设计问题

在观察性研究中，我们通常希望描述因素与某些结果之间的关系。为了简单起见，在本章其余部分，我们假设要分析的因素是提供给疾病患者的治疗。为了实现治疗评估，研究人员收集个人或患者特征、他们正在分析的治疗暴露情况以及他们感兴趣的结果的信息。在设计和进行观察性研究以获得有效结果时，有许多关键方面需要考虑。这包括关于如何减少选择偏差、测量偏差、资助者偏差、适当选择对照组以及时间关系的考量。本文未提供对常见观察性研究设计（如病例对照和横断面研究）的讨论。更多信息请参考 Szklo 和 Nieto (2007) 以及 Rosenberg (2002)。

首先，治疗与结果之间的时间关系需要是的（Suissa, 2008）。为了分析治疗效果，需要进行纵向研究。纵向研究定义为：在个体暴露于风险因素时对其进行评估，随后评估他们对治疗或所研究状况的反应。如果可用数据库提供了评估前患者暴露时间的信息，则纵向研究可以是追溯性的。在具有纵向设计的研究中，我们在治疗开始时评估患者状况，并在患者接受治疗一段时间后分析其治疗结果。因此，患者状况的变化与治疗效果有关。横断面研究在评估治疗对结果的影响方面并不可用，原因有二：首先，在横面研究中，我们无法将治疗效果与患者所患疾病的基线严重程度分开来；其次，横面研究没有提供关于过去暴露过该因素但在横面观察之前已接受治疗的个体的信息。时间关系是奥斯汀-布拉德福-希尔（Hill, 1965）评估因果关联的方法之一，涉及一致性、强度、特异性、剂量反应关系、生物学解释性等因素。

其次，患者因治疗而经历的变化需要与疾病的自然进程区分开。例如，如果我们分析一种自限性疾病的影响，我们需要将治愈的自然过程与治疗效果分开。只有当接受所关注治疗的患者过程与适当的对照组进行比较时，才能做到这一点。在观察性研究中，比较组或对照组的选择取决于对我们分析的疾病患者的常规做法。该对照组应由接受最常处方的替代治疗的患者或未接受治疗的患者组成（在常规临床护理中患者通常不接受治疗的环境下）。在本章中，我们仅对比接受给定治疗的患者（治疗组）与接受替代治疗或未接受治疗的患者（对照组）的过程。

第三，接受治疗的患者可能具有不同的特征。医生倾向于对严重患者开具认为更有效的治疗，对症状较轻的患者开具侵入性较低或耐受性更好的治疗。因此，不考虑患者之间的这些差异可能会提供虚假的结果。开给可能出现严重结果的严重患者的治疗看起来可能较无效，尽管它们实际上可能比医生为症状较轻的患者开具的治疗更有效。

这个问题被广泛称为选择偏差，是观察性研究的一个常见局限。然而，在研究设计和实施中通过仔细收集所有可能影响结果的预后因素，并考虑到组间差异的分析，可以解决这个问题。

## 17.3 处理测量偏差和资助者偏差

# 第 17 章 观察性研究中的测量偏差与赞助者偏差 389

研究者偏差（Haro 等人，2006）。具体而言，可以将患者评估的治疗组与对照组之间的差异，与研究者评估的治疗差异进行比较。例如，我们可以比较在治疗组中经历更显著改善（改善百分比更高）的患者中，其自身评估的治疗组与对照组的改善百分比。如果不存在观察偏差，我们预计患者评估中治疗组与对照组之间的差异，与研究者评定相似的差异量级相似。如果研究者评估的治疗结果优于对照组，这可能观察到了研究者偏差。在这种情况下，我们还要评估治疗差异是由于研究者人数减少还是在所有研究者中均匀分布。Haro 和同事（2006）提供了一个实际案例，在该案例中，两种治疗方法均显示出改善的患者其 EQ-QL 5D（EQ-5D，一种通用的生活质量量表）从基线到终点的变化被描述。（在这种情况下，接受比较的患者在临床全局印象量表——一种由临床医生评估、用于评估严重程度（1 至 7 分）的量表中，从基线到终点下降了一分）。比较组之间的 EQ-SD 差异相似；作者指出没有证据表明存在观察偏差。最后，如果存在某些观察偏差的证据（患者自评与研究者评估存在差异），我们可以确定这些差异是归因于少数可能导致观察偏差的研究者，还是在所有研究者中均匀分布。

第四，在任何类型的研究中，治疗组和对照组都应该使用相同的工具和相似的时间间隔进行评估。这在观察性研究中可能是个问题，因为产生治疗的患者可能不同，且可能在不同的间隔被记录。研究描述必须明确说明评估患者的间隔（以防在间隔期间进行定期随访）以及必须进行评估的方法。

如前所述，研究者或赞助者偏差可能出现在研究开发的任何阶段。在研究设计期间，应广泛考虑患者的结局，以尽可能涵盖可能出现治疗差异的领域。结局应包括临床和功能状态，还包括不良事件的发生。专注于预计新治疗法优于替代方案的领域指标，可能仅凸显有利于新治疗法的治疗差异部分。

## 17.4 总结

观察性研究本质上在用于评估治疗效果时受到许多系统性误差或偏差的影响。为了产生有效结果，需要进行仔细的设计和实施，包括纳入对照或比较组、考虑治疗与结局之间的时间关系、考虑选择偏差以及避免信息偏差。通过使用客观结局、采用简单且有效的评估以及结合多个信息源，可以减少观察偏差。

# 参考文献

Altman, D. G., K. F. Schulz, D. Moher, M. Egger, F. Davidoff, D. Elbourne, and P. C. Gotzsche; T. Lang 代表 CONSORT 组。 2001. “用于报告随机试验的修订版 CONSORT 声明：解释与详述。”Annals of Internal Medicine 134(8): 663–694.

Grimes, D. A., and K. F. Schulz. 2002. “观察性研究中的偏差与因果关联。”The Lancet 359: 248–252.

Har, J. M., S. Kentominas, M. A. Negrin, M. Ratcliffe, D. Suarez, and F. Windmeijer. 2006. “观察性健康结局研究中治疗效果评估的方法学方面。”Applied Health Economics and Health Policy 5(1): 11–25.

Hill, A. B. 1965. “环境与疾病：关联还是因果关系？”Proceedings of the Royal Society of Medicine 58: 295–300.

Page, L. A., and M. Henderson. 2008. “评估证据：什么是测量偏差？”Evidence-Based Mental Health 11(2): 36–37.

Pinto-Meza, A, A. Fernandez, A. Serrano-Blanco, and J. M. Haro. 2008. “西班牙初级保健中抗抑郁治疗的充分性：一项自然性六个月随访研究。”Psychiatric Services 59: 78–83.

Porta, M. S. 2008. Dictionary of Epidemiology（流行病学字典）. 5th ed. New York: Oxford University Press, Inc.

Rosenbaum, P. R. 2007. Observational Studies（观察性研究）. 2nd ed. New York: Springer-Verlag.

Rubin, D. B. 2007. “用于因果效应的观察性研究的设计与分析：与随机试验设计的相似性。”Statistics in Medicine 26: 20–36.

Suissa, S. 2008. “药物对死亡率影响的观察性研究中不可测量的时间偏差。”American Journal of Epidemiology 168: 329–335.

Szklo, M., and F. J. Nieto. 2006. Epidemiology: Beyond the Basics（流行病学：基础之外）.2d ed. MA: Jones and Bartlett Publishers.

# 第 18 章

# 观察性研究的样本量计算

Sin-Ho Jung
Taiyeong Lee
Elizabeth DeLong

+   摘要 ................................................................................ 391
18.1 引言 ................................................................................ 391
18.2 连续变量 ................................................................................ 392
18.3 二分类变量 ....................................................................... 398
18.4 生存数据的双样本对数检验 ................................................ 405
18.5 双样本纵向数据 ................................................................ 410
18.6 讨论 ............................................................................... 423
附录：H_u 下 Wilcoxon 秩检验的渐近分布 .... 423
参考文献 ................................................................ 424

## 摘要

出于多种原因，观察性研究目前被用于提供支持医疗决策的证据。这些研究不具备随机试验那样的信誉水平，因此对统计问题的关注至关重要。特别是对事件率、样本量和功效的考虑经常出现。本章提供了在各种情况下处理这些考虑的机制。此外，这里介绍的方法也同样适用于临床试验。

# 18.1 引言

计算机数据可用性的增加激发了人们对观察性研究的兴趣。个人医疗机构和医院现在尝试根据从自身患者收集的数据进行推断。此外，拥有数百个站点临床数据的大型注册系统的扩散为研究罕见疾病和罕见事件提供了机会。然而，即使是使用这些数据库的研究，在缩小到适当的研究人群和终点时，也会遇到样本量和功效的问题。

观察性研究的设计可以应对各种目标。如果研究的主要分析是估计某些参数，则可以使用标准的样本量计算，要求置信区间宽度不超过某一特定值。如果目标涉及队列的比较，那么在许多情况下，由于观察性研究的非随机性质，统计分析将涉及某种形式的选择偏差调整。

# 392 使用 SAS 进行观察性健康数据分析

第 1 至 11 章涵盖了这些设置下的选择偏倚调整和执行队列研究的标准分析方法，包括倾向评分回归、分层、匹配、双稳健调整、工具变量、局部控制以及各种纵向分析。关于这些场景下研究规划中的样本量计算，由于复杂的设计和分析可能需要通过模拟进行自定义的样本量和功效估计。在某些情况下，为了估计功效和样本量，可以简化主要假设，通用的 SAS 宏可以执行所需的计算。

在本章中，我们介绍了一系列 SAS 宏，用于计算不同类型结局和比较的研究（均为两组之间的比较）的样本量：

- t检验（第 18.2.1 节）
- Wilcoxon 秩和检验（第 18.2.2 节）
- 二分类结局的双样本检验（第 18.3.1 节）
- 加权 Mantel-Haenszel 检验（第 18.3.2 节）
- 生存数据的 Log-Rank 检验（第 18.4 节）
- 纵向数据——连续性结局（第 18.5.3.3 节）
- 纵向数据——二分类结局（第 18.5.3.3 节）

加权 Mantel-Haenszel 检验（见第 18.3.1 节）的样本量直接适用于基于常用倾向评分分层方法的观察性研究。这种倾向评分分层方法在第 2 章中详细描述。简而言之，倾向评分分层涉及为每个研究参与者估计倾向评分，根据该评分进行分层，估计每个层内队列之间的差异，并合并跨层的估计的队列差异。

本章的其他章节介绍了基于分析方法但未进行特定选择偏倚调整的样本量宏。然而，当计划简单的队列比较时（例如，目标不是因果推断），或者在在使用倾向评分匹配等其他方法时作为非常易用的初始计算时，这些宏对于观察性研究规划非常有用。在这个示例中，人们应该在这些宏计算出的样本量基础上，补充一个由于另一组队列缺乏倾向评分匹配患者而从分析中排除的患者人数的估计。此外，本章中的大多数样本量计算方法也可以用于随机临床试验。

## 18.2 连续变量

在本节中，我们考虑连续变量的双样本检验：t 检验和 Wilcoxon 秩检验。

## 第 18 章 观察性研究的样本量计算

## 18.2.1 双样本 $t$检验

假设对于 $k=(1,2)$，$X_{k,1},\dots,X_{k,n_k}$ 是独立同分布（IID）正态随机变量，均值为 $\mu_k$，方差为 $\sigma^2$。我们想要检验 $H_0 : \mu_1 = \mu_2$ 对 $H_a : \mu_1 \neq \mu_2$。令 $\overline{X}_k = n_k^{-1}\sum_{i=1}^{n_k} X_{ki}$ 表示第 $k$ 组的样本均值，

$$s_p^2 = \frac{n_1^{-1}\sum_{i=1}^{n_1}(X_{1i}-\overline{X}_1)^2+n_2^{-1}\sum_{i=1}^{n_2}(X_{2i}-\overline{X}_2)^2}{n_1+n_2-2}$$

表示合并样本方差。那么在 $H_0$ 下，

$$T = \frac{\overline{X}_1-\overline{X}_2}{\sqrt{n_1^{-1}+n_2^{-1}}}$$

遵循自由度为 $n_1+n_2-2$ 的 $t$ 分布。因此，给定第一 I 类错误概率 $\alpha$，如果 $|T| > t_{\nu,\alpha}$，则拒绝 $H_0$，其中 $t_{\nu,\alpha}$ 是自由度为 $\nu$ 的 $t$ 分布的 $\alpha$ 分位数。

如果 $n_1$ 和 $n_2$ 很大，我们不需要正态分布假设，$t$检验的临界值 $t_{n_1+n_2-2,\alpha}$ 可以由标准正态分布的 $\alpha$ 分位数 $z_\alpha$ 近。样本量有多大取决于每组观测值接近正态分布的程度。为了使正态化，我们对原始数据应用转换，例如对数转换（Carroll and Rupp, 1988）。基于大样本近似推导出样本量公式。我们考虑备择假设 $H_a : |\mu_1-\mu_2| = \Delta$。注意 $\Delta = |\mu_1-\mu_2|/\sigma$ 表示效应量。在在不失一般性的情况下，我们在 $H_a$ 下假设 $\mu_1 > \mu_2$。那么，在 $H_a$ 下，

$$T = \frac{\overline{X}_1-\overline{X}_2}{\sqrt{n_1^{-1}+n_2^{-1}}} = Z+\Delta\sqrt{nr_1r_2}$$

其中 $Z(0,1)$，$r_k=n_k/n$，$n=n_1+n_2$。对于给定的 $n$，功效计算为 $1-\beta=\Phi(z_{1-\alpha}-\Delta\sqrt{nr_1r_2})$。

$\Phi(z)=1-\Phi(-z)$ 是标准正态分布的累积分布函数。通过求解 $n$，得到所需的总样本量

$$n = \frac{(z_{1-\alpha/2} + z_{1-\beta})^2}{r_1r_2\Delta^2}$$

或对于组 $k$，$n_i = n \times r_i$。对于单侧检验，将 $\alpha/2$ 替换为 $\alpha$。如果正态近似样本量小于30，我们可以考虑增加100%。总之，双样本 $t$检验的样本量计算如下：

- 指定第一 I 类错误概率 $\alpha$ 和功效 $1-\beta$：
- (a) $\Delta = |\mu_1-\mu_2|/\sigma$，标准化效应量
- (b) $r_i$ 是组 $k$ 的比例（$r_1 + r_2 = 1$）
- 计算样本量 $n = \frac{(z_{1-\alpha/2} + z_{1-\beta})^2}{r_1r_2\Delta^2}$

**示例 18.1**
假设我们要检测总体均值 $0.5\sigma$ 的差异，双侧 $\alpha = 0.05$，功效 $1-\beta = 0.9$。那么 $z_{1-\alpha/2} = 1.96$，$z_{1-\beta} = 1.282$。假设总体中比例相等（即 $r_1 = r_2 = 0.5$），我们得到样本量 $n=171$。SAS/STAT 中的 PROC POWER 可以处理这种场景，如下：

## 程序 18.1 双样本 t检验 SAS 代码

```sas
```



`proc power`;

  `twosampleans`

    `fractional` = 0.5

    `meandiff` = 0.5               /* 均值差异 */

    `stddev` = 1                  /* sigma */

    `groupweights` = (0.5 0.5)   /* r1 r2 */

    `sides` = 2                   /* 1: 单侧 2: 双侧 */

    `power` = 0.9                /* 功效 */

    `alpha` = 0.05                /* alpha */

    `totaln`=;                   /* 样本量 */

`run`;

## 程序 18.1 的输出

| POWER 过程 | |
| :--- | :--- |
| 均值差异的双样本 t 检验 | |
| 固定场景元素 | |
| 分布 | 正态 |
| 方法 | 确切 |
| 侧数 | 2 |
| Alpha | 0.05 |
| 均值差异 | 0.5 |
| 标准差 | 1 |
| 组 1 权重 | 0.5 |
| 组 2 权重 | 0.5 |
| 名义功效 | 0.9 |
| 零差异 | 0 |
| 分数 | 实际 | 向上 |
| 总 N | 功效 | 总 N |
| 170.06258 | 0.902 | 171 |

## 18.2.2 Wilcoxon 秩和检验

已知`t`检验对异常值敏感。Wilcoxon 秩和检验 (`WRST`) 被广泛用作稳健检验。我们假设对于组 `k=(1,2)`，`X_{i1},\dots,X_{in2}` 是来自某种分布的同分布随机变量，其累积分布函数为 `F(x-\theta_j)=P(X_{ij} \le x)`。对于 `\Delta=\theta_1-\theta_2`，我们想要检验 `H_0:\Delta=0 \neq 0`。Mann and Whitney (1947) 建议使用 `W=(n_1n_2)^{-1}\sum\sum I(X_{i1}>X_{j2})`。`W` 的期望值是 `P(X_{i1}>X_{j2})`，即从组 1 随机选择测量值大于从组 2 随机选择测量值的概率。如果 `H_0` 为真，检验统计量将接近 1/2；如果 `H_a` 为真，则接近 0 或 1。

对于较大的 `n=n_1+n_2`，如果 `T = \frac{W-V_0}{\sigma_0}` 的绝对值大于 `z_{1-\alpha/2}`，我们拒绝 `H_0`，其中 `v_0=1/2` 和 `\sigma_0^2=(n+1)/12n_1n_2` 分别是 `W` 在 `H_0` 下的均值和方差。

令 `f(x)=F'(x)/\tilde{x}` 表示 `F(x)` 的概率密度函数。附录显示，在 `H_a` 下，`W` 有 `v_a=\int_{-\infty}^{\infty}F(x+\Delta)f(x)dx`。

# 396 使用 SAS 分析观察性健康数据

以及方差

$$\sigma_a^2 = \frac{\sigma_1^2}{n_1} + \frac{\sigma_2^2}{n_2}$$

其中

$$\sigma_1^2 = \int_{-\infty}^{\infty} F^2(x+\Delta)f(x)dx - \{\int_{-\infty}^{\infty} F(x+\Delta)f(x)dx\}^2$$

以及

$$\sigma_2^2 = \int_{-\infty}^{\infty} F^2(x-\Delta)f(x)dx - \{\int_{-\infty}^{\infty} F(x-\Delta)f(x)dx\}^2$$

那么，

$T = Z\frac{\sigma_a}{\sigma_0} + \frac{V_a-V_0}{\sigma_0}$

其中 `Z = (W-V_0)/\sigma_a` 是渐近服从 `N(0,1)` 的随机变量。给定效能 `1-\beta`，

$1-\beta=P(|T| > z_{1-\alpha/2} \mid H_a) = P(|Z\frac{\sigma_a}{\sigma_0} + \frac{V_a-V_0}{\sigma_0}| > z_{1-\alpha/2}).$

$$\Phi(\frac{\sigma_0}{\sigma_a}(z_{1-\alpha/2}) - \frac{|V_a-V_0|}{\sigma_0}) = ...$$

其中 `\Phi(z)=P(Z > z)`。通过将 `\sigma_0^2` 和 `\sigma_a^2` 中的 `n_k` 替换为 `n_r`，并对 `n` 求解，我们得到所需的样本量

$$n = \frac{1}{12r_r^2} \frac{(z_{1-\alpha/2}+z_{1-\beta})^2}{\sqrt{2(r_r\sigma_0^2+r_r\sigma_a^2)}}.$$

虽然检验不需要指定分布函数 `F(x)`，但样本量计算需要。备择假设由两个具有位置平移的分布指定。执行秩和检验不需要位置平移模型，但如果我们想对中位数或均值进行推断，则是需要的。当然，在本文介绍的样本量计算中也是需要的。

`t` 检验要求观测值具有有限方差，而 `WRST`（加权秩和检验）不需要。例如，如果 `F` 服从柯西分布，可以使用 `WRST`，而不是 `t`检验。

# 第 18 章 观察性研究的样本量计算 397

假设正态分布的 `WRST` 样本量计算描述如下：

- 除了第一类错误概率 `\alpha` 和效能 `1-\beta` 之外，指定
  (a) `\Delta = \sigma^{-1}(\mu_i - \mu_j)`，标准化效应量
  (b) `r_i` 是组 `k` 的患病率 `(r_i + r_j = 1)`

- 计算
`\sigma_a^2 = \int_{-\infty}^{\infty} \Phi(x+\Delta)\phi(x)dx`

`\sigma_i^2 = \int_{-\infty}^{\infty} \Phi(x+\Delta)\phi(x)dx - \{\int_{-\infty}^{\infty} \Phi(x+\Delta)\phi(x)dx\}^2`

`\sigma_j^2 = \int_{-\infty}^{\infty} \Phi(x-\Delta)\phi(x)dx - \{\int_{-\infty}^{\infty} \Phi(x-\Delta)\phi(x)dx\}^2`，

其中 `\Phi(x)` 和 `\phi(x)` 分别是 `N(0,1)` 的累积分布函数和概率密度函数。

- 计算样本量
`n = \frac{1}{2r_ir_j} \frac{(z_{1-\alpha} + z_{1-\beta}\sqrt{12(r_i\sigma_i^2 + r_j\sigma_j^2)})^2}{1/2}`

# 例 18.2

假设我们要检测总体均值之间 `0.5\sigma` 的差异，双侧 `\alpha = 0.05`，且效能 `1-\beta = 0.9`。那么 `z_{1-\alpha} = 1.96` 且 `z_{1-\beta} = 1.282`。假设总体中两组比例相等（即 `r_i=r_j=0.5`），我们得到所需的样本量 `n=177`。注意，双样本 `t` 检验需要的 `n=171` 小，但如果数据中存在离群值，威尔科逊秩检验可能更有效力。

# 程序 18.2 Wilcoxon秩和检验 SAS 代码

```sas
%macro WilcoxonRankSumTest(delta=, /* 标准化效应量 */
r1=, /* 第1 组的患病率 */
r2=, /* 第2 组的患病率 */
sides=, /* 检验侧：1 或 2 */
alpha=, /* alpha */
power= /* 效能 */
);

proc iml;
 start CDF2PDFDELTA(t);
 m=t+\delta; c=cdf('normal',m,0,1); p=pdf('normal',t,0,1); v=c*p;
 return(v);
 finish;
 start CDF2PDFDELTA(t);
 m=t+\delta; c=cdf('normal',m,0,1)**2; p=pdf('normal',t,0,1); v=c*p;
 return(v);
 finish;
```

# 398 使用 SAS 分析观察性健康数据

```sas
start_PDF_DELTA(t);
 m=&delta; c=cdf('normal',m,0,1); p=pdf('normal',t,0,1); v=c*p;
return(v);
finish;
 start_PDF_DELTA(t);
 m=&delta; c=cdf('normal',m,0,1); p=pdf('normal',t,0,1); v=c*p;
return(v);
finish;
```

# 输出程序 18.3

# 398 使用 SAS 分析观察性健康数据

# 400 使用 SAS 分析观察性健康数据

# 第 18 章 观察性研究的样本量计算 401

数据分析中常用的方法。为了解决这一问题，Rosenbaum 和 Rubin (1983, 1984) 开发了倾向评分法。

假设通过倾向评分分层形成了 `J` 个层层。令 `n` 表示总样本量，`n_j` 表示第 `j` 层层中的样本量 `(\sum_{j=1}^J n_j = n)`。每个受试者的数据包括响应变量 `x=1` 表示有响应，`0` 表示无响应，以及 `k` 表示受试者被分配的层层和治疗组 `(1 \le j \le J; k=1, 2)`。第 `j` 层层的频率数据可以描述如下：

| 响应 | 1 | 2 | 总计 |
|---|---|---|---|
| 是 | `x_{j1}` | `x_{j2}` | `x_j` |
| 否 | `x_{j1}` | `x_{j2}` | `x_j` |
| 总计 | `n_j` | `n_j` | `n_j` |

令 `O_j = x_{j1}`，`E_j = n_j x_j/n_j`，且

`V_j = \frac{n_j n_{j2} x_{j1} x_{j2}}{n_j^2(n_j-1)}`.

那么，加权 Mantel-Haenszel (WMH) 检验给出

`T = \frac{\sum_{j=1}^J \hat{w}_j(O_j - E_j)}{\sum_{j=1}^J \hat{w}_j V_j}`

其中权重 `\hat{w}_j` 在 `n \to \infty` 时收敛于常数 `w_j`。对于原始 Mantel-Haenszel 检验，`\hat{w}_j=1`；对于 Gart (1985) 提出的统计量，`\hat{w}_j = \hat{q}_j = x_j/n_j`。

令 `a_j = n_j/n` 表示第 `j` 层层的分配比例 `(\sum_{j=1}^J a_j=1)`，`b_k = n_j/n` 表示第 `j` 层中 `k` 组的分配比例 `(b_1+b_2=1)`。令 `p_{jk}` 表示第 `j` 层中 `k` 组的响应概率，`q_{jk}=1-p_{jk}`。在 `H_0: p_{j1}=p_{j2}, 1 \le j \le J` 下，`T` 渐近服从 `N(0,1)`。使功效最大化的权重取决于分配 `\{(a_j, b_{j1}, b_{j2}), j=1,..,J\}` 以及 `H_1` 下的效应量 `(p_{j1}-p_{j2},...,J)`。

为了计算 WMH 的效能，我们必须推导出 `H_1` 下 `\sum_{j=1}^J \hat{w}_j(O_j-E_j)` 的渐近分布以及 `\sum_{j=1}^J \hat{w}_j V_j` 的极限。我们假设概率 `(p_{jk}, 1 \le j \le J, k=1,2)` 在 `H_1` 下满足 `p_{j1}q_{j2}/p_{j2}q_{j1}=\phi`，其中 `\phi \neq 1`。

注意

# 402 使用 SAS 分析观察性健康数据

如果在使用逻辑回归对治疗指标和倾向评分进行回归分析时，治疗指标与倾向评分之间不存在交互作用，则跨层层的恒定优势比是成立的。以下推导基于 `H_i`。可以验证：



$O_j - E_j = \frac{n_j n_{j2}}{n_j}(\hat{p}_{j1} - \hat{p}_{j2})$

$= \frac{n_j n_{j2}}{n_j}(\hat{p}_{j1} - p_{j1} + p_{j1} - \hat{p}_{j2} + p_{j2} - p_{j2})$ （此处原文公式如此）

$= na_j b_{j1} b_{j2}(\hat{p}_{j1} - \hat{p}_{j2} + p_{j1} - p_{j2})$。

因此，在 $H_1$ 下，$\sum_{j=1}^J \hat{w}_j(O_j - E_j)$ 渐近服从正态分布，均值为 $n\Delta$，方差为 $n\sigma^2$，其中：

$\Delta = \sum_{j=1}^J w_j a_{j1} b_{j2}(p_{j1} - p_{j2})$

$= (1-\Phi)\sum_{j=1}^J w_j a_{j1} b_{j2} \frac{p_{j1}q_{j2}}{q_{j1} + p_{j2}}$

同样在 $H_1$ 下，我们有

$\sum_{j=1}^J w_j^2 V_j = n\sigma_0^2,$

其中 $\sigma_0^2 = \sum_{j=1}^J w_j^2 a_{j1} b_{j2}(b_{j2}p_{j1} + b_{j2}p_{j2})(b_{j1}q_{j1} + b_{j2}q_{j2})$。

因此，WMH 的效能给出为

$1 - \beta = P(|T| > z_{1-\alpha/2} | H_1)$

$= \Phi(\frac{\sigma_1}{\sigma_0}Z + \sqrt{n}\frac{|\Delta|}{\sigma_0} > z_{1-\alpha/2})$

$= \Phi(\frac{\sigma_0}{\sigma_1}z_{1-\alpha/2} - \sqrt{n} \frac{|\Delta|}{\sigma_1})$.

# 第 18 章 观察性研究的样本量计算 403

其中 $Z$ 是标准正态变量，$\Phi(z) = P(Z > z)$。因此，达到效能 $1-\beta$ 所需的样本量可以获得为

$n = \frac{(\sigma_0 z_{1-\alpha/2} + \sigma_1 z_{\beta})^2}{\Delta^2}. \quad (3)$

参考 Jung, Chow 和 Lu (2007)，加权 Mantel-Haenszel 检验的样本量计算可以如下进行：

- 指定输入变量
- 第一类和第二类错误 $(\alpha, \beta)$。
- 组 $p_{j1}, \dots, p_{j2}$ 的成功概率以及 $H_1$ 下的优势比 $\phi$。注意 $p_{j2} = \phi p_{j1} / (q_{j1} + \phi p_{j1})$。
- 层发生率 $(a_j, j = 1, \dots, J)$。Lu (2007) 建议使用 $a_j \approx 1/J$。
- 每层内第 1 组的分配概率 $(b_{j1}, j = 1, \dots, J)$。

2. 通过下式计算 $n$：

$n = \frac{(\sigma_0 z_{1-\alpha/2} + \sigma_1 z_{\beta})^2}{\Delta^2},$

其中 $\Delta = \sum_{j=1}^J w_j a_{j1} b_{j2}(p_{j1} - p_{j2})$

$\sigma_0^2 = \sum_{j=1}^J w_j^2 a_{j1} b_{j2}(b_{j2}p_{j1} + b_{j2}p_{j2})(b_{j1}q_{j1} + b_{j2}q_{j2})$

$\sigma_1^2 = \sum_{j=1}^J w_j^2 a_{j1} b_{j2}(b_{j1}p_{j1} + b_{j1}p_{j2})(b_{j2}q_{j1} + b_{j2}q_{j2})$

# 示例 18.4

假设我们比较控制组 ($k=1$) 和实验组 ($k=2$) 之间的响应概率。我们将数据分为 $J=5$ 层，分配比例给出为 $(a_1, a_2, a_3, a_4, a_5) = (0.15, 0.15, 0.2, 0.25, 0.25)$ 以及 $(b_{11}, b_{21}, b_{31}, b_{41}, b_{51}) = (0.4, 0.4, 0.5, 0.6, 0.6)$。同样假设控制组的响应概率给出为 $(p_{11}, p_{21}, p_{31}, p_{41}, p_{51}) = (0.5, 0.6, 0.7, 0.8, 0.9)$；我们想要计算在效能 $1-\beta=0.8$ 下检测优势比 $\phi=2$ 的双侧检验 $\alpha=0.05$ 所需的样本量。对于 $\phi=2$，实验组的成功概率给出为 $(p_{12}, p_{22}, p_{32}, p_{42}, p_{52}) = (0.6667, 0.750, 0.8235, 0.8889, 0.9474)$。根据这些设置 (3)，Mantel-Haenszel 检验需要 $n=447$。

404 使用 SAS 分析观察性健康数据

## 程序 18.4 加权 Mantel-Haenszel 检验 SAS 代码

```sas
%macro WMHTestWithStrata (
 J = , /* 层数 */
inA= , /* 层发生率 */
inB= , /* 控制组分配概率 */
inPl= , /* 控制组成功概率 */
phi = , /* H1 下的优势比 */
power= , /* 效能 */
alpha= , /* alpha */
sides= , /* 1:单侧检验 2:双侧检验 */
);

proc iml;
 let K = 2; /*组 */
a=&inA; b=&inB; pl=&inPl;
p=J(1,0); Q1=J(1,0); Q2=J(1,0);
 j=1 to J;
 Q1[j]=p[j];
 p2=phi*p[j]/(Q1[j]+phi*p[j]);
 p2[j]=1-p[j];
 end;
 z_p1=alpha/&sides; z_alpha=probit(z_p1);
 z_p2=power; z_beta=probit(z_p2);
 delta=0; s0=0; sl1=0;

 j=1 to J;
 delta=delta+a[j]*(1-b[j])*(p[j]-p[j]);
 sl1=sl1+a[j]*b[j]*((1-b[j])*Q1[j]+phi*p[j])*Q2[j];
 s0=s0+a[j]*b[j]*(1-b[j])*(b[j])*Q1[j]+phi*p[j])*Q2[j];
 end;
 n= (1/(delta**2))*(sqrt(sl1)*z_alpha+sqrt(sl1)*z_beta)**2;

 print 'Sample Size Calculation';
 print 'Weighted Mantel-Henszel Test with Strata';
 print &alpha, power = &power; phi = &phi; sides = &sides;
 print A B P1 P2;
 print delta s0_sq sl1_sq;
 print n;
quit;
run;
%mend WMHTestWithStrata;
```

/* 运行示例 18.4 的宏 */

```sas
%WMHTestWithStrata(
 J = 5 , /* 层数 */
inA=%str((0.15, 0.15, 0.2, 0.25, 0.25)), /** 层发生率 */
inB=%str((0.4, 0.4, 0.5, 0.6, 0.6)), /* 分配概率 */
inPl=%str((0.5, 0.6, 0.7, 0.8, 0.9)), /* 成功概率 */
phi = 2 , /* Hi 下的优势比 */
power=0.8 , /* 效能 */
alpha=0.05 , /* alpha */
sides=2 /* 双侧检验 */
);
```

![](img/fe9ff008baacd148b225.png)

# 419 第 18 章 观察性研究的样本量计算 405

# 第 18 章 观察性研究的样本量计算 405

程序 18.4 的输出

| 样本量计算 | 加权 Mantel-Haenszel 检验层检验 |
| alpha | power | phi |
| 0.05 | 0.8 | 2 |
| A | B | P1 | P2 |
| 0.15 | 0.15 | 0.2 | 0.25 | 0.25 |
| 0.4 | 0.4 | 0.5 | 0.6 | 0.6 |
| 0.5 | 0.6 | 0.7 | 0.8 | 0.9 |
| 0.6667 | 0.750 | 0.8235 | 0.8889 | 0.9474 |
| delta | s0 | sl sq |
| -0.02575 | 0.038175 | 0.036718 |
| n |
| 447 |

# 18.4 生存数据的双样本对秩检验

假设有 $n_k$ 个受试者从组 $k=(1,2)$ 进入研究。对于组 $k$ 中的 $i=1,...,n_k$ 个受试者，令 $T_{ij}$ 表示生存数据（即事件发生的时间），其边缘累积风险函数为 $\Lambda_k(t)$。

由于所有受试者的失访或研究终止，部分受试者的生存时间被删失。令 $C_{ki}$。我们假设每组内 $C_{ki}$ 和 $T_{ki}$ 是独立的。

# 406 使用 SAS 进行观察性健康数据分析

其中 $\hat{\Lambda}_k(t) = \int_0^t Y_k(s)dN_k(s)$ 是 $\Lambda_k(t)$ 的 Nelson-Aalen 估计（Nelson, 1969; Aalen, 1978），$N_k(t) = \sum_{i=1}^n N_{ki}(t), N_{ki}(t) = \delta_i(X_{ki} \leq t), Y_k(t) = \sum_{i=1}^n Y_{ki}(t),$ 以及 $Y_{ki}(t) = I(X_{ki} \geq t)$。对于较大的 $n$，且满足 $n_k = r_n$ 且 $0 < r_k < 1$，在 $H_0$ 下，$W/\hat{\sigma}$ 似从正态分布，均值为 0，方差为 1。

```
$$\hat{\sigma}^2 = \int_0^{\infty} \frac{Y_k(t)Y_l(t)}{\{Y_k(t)+Y_l(t)\}}d\{N_k(t)+N_l(t)\}
```

参考 Fleming 和 Harrington (1991)，如果 $W/\hat{\sigma}$ 的绝对值大于 $z_{1-\alpha/2}$，我们拒绝 $H_0$。

对于样本量和效能计算，我们假设一个比例风险模型 $\Delta = \Lambda_s(t)/\Lambda_c(t)$。对秩检验的效能取决于事件的数量，而非患者的数量。根据 Rubinstein 等人（1981），在双侧 $\alpha$ 检验中检测风险比为 $\Delta(<1)$ 且效能为 $1-\beta$ 的风险时，两组所需的 $D_s$ 和 $D_c$ 数量公式如下：

```
$(\frac{\log \Delta}{z_{1-\alpha/2} + z_{1-\beta}})^2 = D_1^{-1} + D_2^{-1}$.
```

为了计算 $D_g$，我们需要指定 $H_e$ 下的分布和共同删失分布。假设受试者以恒定速率招募，持续时间 $A$，并在招募完成后额外随访时间为 $B$。总时长为 $A+B$。那么，假设没有失访，删失分布在 $A$ 和 $A+B$ 之间均匀分布，如下：

```
$G(t)=P(C_{ki} \geq t) = \begin{cases} 1 & \text{if } t < B \\ 1+(B-t)/A & \text{if } B \leq t \leq A+B \\ 0 & \text{otherwise.} \end{cases}$
```

样本量计算中最流行的模型之一是指数分布，

```
$S_k(t)=P(T_{ki} \geq t) = \exp(-\lambda_k t)$
```

对于组 $k$。组 $k$ 中某受试者发生事件的概率给为：

```
$d_k=P(T_{ki} \leq C_i) = \int_0^{\infty} S_k(t)dG(t) = 1 - \frac{\exp(-\lambda_k B)\{1-\exp(-\lambda_k A)\}}{\lambda_k}$
```

# 第18章 观察性研究的样本量计算 407

因此我们有 $D_k = n_k d_k = nr_k d_k$。将其代入公式 (4) 并对 $n$ 求解，我们得到：

$n = (\frac{1}{r_1 d_1} + \frac{1}{r_2 d_2})(\frac{z_{1-\alpha/2} + z_{1-\beta}}{\log \Delta})^2$。

我们在计算 $d_k$ 时假设没有失访，但通过假设随访时间的分布可以很容易忽略这一假设。

总之，样本量的计算方法如下：

- 除了第一类错误概率 $\alpha$ 和效能 $1-\beta$ 外，还需要指定：
  (a) $\lambda_1, \lambda_2$ = $H_0$ 下的风险率 ($\Delta = \lambda_2/\lambda_1$)
  (b) $r_k$ = 组 $k$ 的流行率 ($r_1+r_2=1$)
  (c) $A$ = 招募期，$B$ = 额外随访期
- 计算组 $k=(1,2)$ 中受试者发生事件的概率
  $d_k = 1 - \frac{\exp(-\lambda_k B)\{1-\exp(-\lambda_k A)\}}{\lambda_k}$
- 计算样本量
  $n = (\frac{1}{r_1 d_1} + \frac{1}{r_2 d_2})(\frac{z_{1-\alpha/2} + z_{1-\beta}}{\log \Delta})^2$

# 例18.5

假设对照组 $(k=1)$ 的中位生存时间为 $\mu_1=3$ 年，如果实验组的中位生存时间延长 50%（即 $\mu_2=4.5$ 年）。在指数生存模型下，风险率为 $\lambda_1=0.231$ 和 $\lambda_2=0.154$ ($A=0.667$)。同样假设 $(r_1,r_2)=(0.3,0.7)$，患者在 $A=3$ 年时均匀删失，并在招募完成后额外 $B=2$ 年进行最终分析。然后我们有 $(d_1,d_2)=(0.5455,0.4115)$，$n=613$ ($n_1=184,n_2=429$) 以及 $(D_1,D_2)=(100,177)$。PROC POWER（程序18.5.2）提供了基于 Lakatos (1988) 的秩检验样本量，与我们的公式相比，在该设计下给出了略小的样本量，$n=593$。

# 程序18.5.1 双样本秩检验 SAS 代码

```sas
%macro SS_TwoLogRank(
    Accrual    =3, /* 招募期 *
    Follow     =2, /* 额外随访期 *
    inR        =%str(0.3, 0.7),/* 分配比例 (r1, r2)*
    inLambda   =%str(0.231, 0.154),/* 择择假设下的风险率 *
    alpha      =0.05,{\ * 第一类错误 *
    power      =0.9,{\ * 效能 *
    sides      =2 /* 双侧检验 *
);

proc incr;
    let k = 2; r = &inR; Group = J(k,1,0); lambda = &inLambda;
    delta = J(2)[lambda]; d_prob = J(k,1,0);
    n = J(k,1,0); D = J(k,1,0);
    do i=1 to &k;
        group(i)=i;
        d_prob[i]=1-exp(-lambda[i]*&Follow)*(1-exp(-lambda[i]*&Accrual));
    end;
    z_p1=1-&alpha/sides; z_alpha=probit(z_p1);
    z_p2=&power/sides; z_beta=probit(z_p2);
    Total=int((1/(r/2*d_prob[1])+(1/(r/2*d_prob[2])))*(z_alpha+z_beta)/log(delta))**2;
    do i=1 to &k; n[i]=r[i]*Total; D[i]=d_prob[i]*n[i]; end;
    print 'Sample Size';
    print 'for Two-Sample Log-Rank Test for Survival Data';
    print 'Accrual Period :'&Accrual; Follow_Up=&Follow;
    print Group lambda delta d_prob;
    print Total;
quit;
run;
%mend SS_TwoLogRank;
```

--- 运行例18.5的宏 ---

```sas
%SS_TwoLogRank(
    Accrual    =3, /* 招募期 *
    Follow     =2, /* 额外随访期 *
    inR        =%str(0.3, 0.7),/* 分配比例 (r1, r2)*
    inLambda   =%str(0.231, 0.154),/* 择择假设下的风险率 *
    alpha      =0.05,{\ * 第一类错误 *
    power      =0.9,{\ * 效能 *
    sides      =2 /* 双侧检验 *
);
```

# 第18章 观察性研究的样本量计算 409

程序18.5.1 的输出



| Sample Size Calculation |
| for Two-Sample Log-Rank Test for Survival Data |
| Accrual Period : 3 |
| Follow Up period : 2 |
| GROUP | LAMBDA | DELTA | R | D_PROB |
| 1 | 0.231 | 0.6666667 | 0.3 | 0.5455053 |
| 2 | 0.154 | | 0.7 | 0.411467 |
| GROUP | N | D |
| 1 | 183.9 | 100.31843 |
| 2 | 429.1 | 176.56049 |
| TOTAL | 613 |

程序18.5.2 SAS 代码 (`PROC POWER`) 用于例18.5

```
proc power;
twosamplesvival test=logrank
fractional
groupedsurvtimes = 3 | 4.5
accrualtime = 3
followuptime = 2
groupweights = (0.3,0.7)
alpha = 0.05
sides=2
power = 0.9
total =

run;
```

程序18.5.2 的输出

| The POWER Procedure |
| Log-Rank Test for Two Survival Curves |
| Fixed Scenario approximation |
| Method | Lakatos normal approximation |
| Form of Survival Curve | Exponential |
| Form of Survival Curve | Exponential |
| Number of Sides | 2 |
| Accrual Time | 2 |
| Follow-up Time | 0.05 |
| Group 1 Median Time | 3 |
| Group 2 Median Time | 4.5 |
| Group 1 Weight | 0.3 |
| Group 2 Weight | 0.7 |
| Nominal | 0.9 |
| Fractional | 2 |
| Computed | 592 |
| N Total | 591 |
| N Total | 590 |
| N Total | 589 |
| N Total | 588 |
| N Total | 587 |
| N Total | 586 |

# 424

使用 SAS 进行观察性健康数据分析

# 18.5 双样本纵向数据

在纵向研究中，我们随时间进行测量。当存在组时，主要目标是组间比较。由于对相关结构的设定错误具有稳健性，广义估计方程（`GEE`）一直是拟合回归模型和检验变量变化的流行方法之一。在本节中，我们将讨论连续或二分类变量的样本量估计。

## 18.5.1 广义估计方程

假设组 `k=(1,2)` 有 `n_k` 个受试者，`n_1+n_2=n`。对于组 `k`，`N_k = sum_{i=1}^{n_k} m_{ki}` 表示观测次数，`r_k = n_{ki}/m_{ki}` 表示分配比例 `r_1+r_2=1`。对于组 `k` 中的受试者 `i (i=1,...,n_k)`，在测量时间 `t_{kij}(j=1,...,m_{ki})` 处的观测 `y_{kij}` 为：

```
$g(\mu_{kij}) = a_k + bt_{kij},$
```

其中 `g(·)` 是已知函数。也就是说，我们假设存在一个函数 `g(·)` 使轨迹线性化。为了简化说明，对连续结果变量使用恒等链接 `g(\mu)=\mu`，对二分类结果变量使用 log 链接 `g(\mu)=\log{\mu/(1-\mu)}`，但推广到其他链接也非常简单。

# 第 18 章 观察性研究样本量计算 411

### 18.5.1.1 连续型结局变量情况

在连续结局变量中，我们有 `U_k(a,b) = 0` 的闭式解：

```
\hat{b}_k = \frac{\sum_{i=1}^{n_k} \sum_{j=1}^{m_{kij}} (t_{kij} - \hat{t}_{kij})y_{kij}}{\sum_{i=1}^{n_k} \sum_{j=1}^{m_{kij}} (t_{kij} - \hat{t}_{kij})^2}
```

且 `\hat{a}_k = \bar{y}_k - \hat{b}_k\bar{t}_k`，其中 `\bar{t}_k = N_k^{-1} \sum_{i=1}^{n_k} \sum_{j=1}^{m_{kij}} t_{kij}` 且 `\bar{y}_k = N_k^{-1} \sum_{i=1}^{n_k} \sum_{j=1}^{m_{kij}} y_{kij}`。

根据 Liang 和 Zeger (1986)，当 `n \to \infty` 时，`\sqrt{n}(\hat{b}_k - \hat{b}_k)` 依分布于 `N(0, v_k)`。这里 `v_k` 通过以下公式进行一致估计：

```
\hat{v}_k = \frac{\sum_{i=1}^{n_k} \sum_{j=1}^{m_{kij}} (t_{kij} - \hat{t}_{kij})\hat{\varepsilon}_{kij}}{\sum_{i=1}^{n_k} \sum_{j=1}^{m_{kij}} (t_{kij} - \hat{t}_{kij})^2}
```

其中 `\hat{\varepsilon}_{kij} = y_{kij} - \hat{a}_k - \hat{b}_kt_{kij}`。

### 18.5.1.2 二分类结局变量情况

在二分类结局变量中，令 `p_{kij} = \mu_{kij}`。我们需要使用数值方法（如牛顿-拉夫逊算法）来求解方程；在第 `l` 次迭代中：

```
\begin{pmatrix} \hat{a}_k^{(l)} \\ \hat{b}_k^{(l)} \end{pmatrix} = \begin{pmatrix} \hat{a}_k^{(l-1)} \\ \hat{b}_k^{(l-1)} \end{pmatrix} + n_k^{-1/2} A_k^{-1} U_k(\hat{a}_k^{(l-1)}, \hat{b}_k^{(l-1)}),
```

其中：

```
A_k(a,b) = -n_k^{-1/2} \hat{U}(a,b) = \frac{1}{n_k} \sum_{i=1}^{n_k} \sum_{j=1}^{m_{kij}} p_{kij}(a,b)q_{kij}(a,b) \begin{pmatrix} 1 \\ t_{kij} \end{pmatrix}
```

```
p_{kij}(a,b) = g^{-1}(a+bt_{kij}) = \frac{e^{a+bt_{kij}}}{1+e^{a+bt_{kij}}} (5)
```

且 `q_{kij}(a,b) = 1-p_{kij}(a,b)`。

根据 Liang 和 Zeger (1986)，对于大的 `n`，`\sqrt{n}(\hat{a}_k-a_k, \hat{b}_k-b_k)^T` 渐近于正态分布，均值为 0，方差为 `V_k`，可以通过以下公式进行一致估计：

```
\hat{V}_k = \hat{A}_k^{-1}(\hat{a}_k, \hat{b}_k) \hat{\Sigma}_k(\hat{a}_k, \hat{b}_k)
```

其中：

```
\hat{\Sigma}_k = \frac{1}{n_k} \sum_{i=1}^{n_k} \sum_{j=1}^{m_{kij}} \hat{E}_{ij} \begin{pmatrix} 1 \\ t_{kij} \end{pmatrix}^{\oplus}
```

```
\hat{e}_{ij} = y_{ij} - p_{ij}(\hat{a}_k, \hat{b}_k) \text{ 且 } c^{\oplus} = cc^T \text{ 对于向量 } c
```

令 `\hat{v}_k` 为 `\hat{V}_k` 的 `(2,2)` 成分。

## 18.5.2 样本量计算

假设我们要检验两组的变化率（即 `H_0: b_1 = b_2`）。根据上一节的渐近结果，当满足以下条件时拒绝 `H_0: b_1 = b_2` 接受 `H_1: b_1 \neq b_2`：

```
\frac{\hat{b}_1 - \hat{b}_2}{\sqrt{v_1/n_1 + v_2/n_2}} \geq z_{1-\alpha/2} (6)
```

其中 `z_{1-\alpha/2}` 是标准正态分布的 `1-\alpha/2` 分位数。

在本节中，我们导出双侧 `\alpha` 检验的样本量（6），用于在 `1-\eta` 的效能下检测 `H_1: |b_2 - b_1| = \Delta`。在设计研究时，通常安排访视时间 `t_1 < t_2 < \dots < t_m`，每个受试者进行 `m` 次测量。除了基线外，研究期间受试者可能因为各种缺失值未按计划访视。Jung 和 Ahn (2003) 表，当观测时间广泛分布时，基于固定测量时间的样本量是准确的。

通过简单的代数运算，我们可以导出在 `1-\eta` 效能下检测差异 `|b_2 - b_1| = \Delta` 的样本量：

```
n = \frac{(z_{1-\alpha/2} + z_{1-\eta})^2(v_1 + v_2)}{\Delta^2} (7)
```

其中 `v_k = \lim_{n \to \infty} \hat{v}_k`。`v_k` 的表达式在连续和二分类结局变量之间略有不同，如下。为了处理缺失值，令 `\delta_j` 表示在 `t_j` 有观测的患者比例，`\delta_{j'}` 表示在 `t_j` 和 `t_{j'}` 均有观测的比例。此外，令 `\rho_{ij'} = corr(y_{ij}, y_{ij'})`。假设缺失模式和相关结构在组间是相同的。我们在第 18.5.3 节讨论缺失模式和相关结构的特定模型。

### 18.5.2.1 连续变量情况

假设连续结局变量随时间的恒方差 `var(y_{kj}) = \sigma^2`，且组间相同。Jung 和 Ahn (2003) 显示 `v_1 = v_2 = v` 可表示为：

```
v = \frac{\sigma^2(s^2 + c)}{s^4},
```

其中：

```
s^2 = \sum_{j=1}^{m} \delta_j(t_j - \tau)^2
```

```
c = \sum_{j=1}^{m} \sum_{j'=1}^{m} \delta_{j'} \rho_{jj'}(t_j - \tau)(t_{j'} - \tau)
```

以及：

```
\tau = \frac{\sum_{j=1}^{m} \delta_j t_j}{\sum_{j=1}^{m} \delta_j}
```

因此，(7) 简化为：

```
n = \frac{v(z_{1-\alpha/2} + z_{1-\beta})^2}{\Delta^2 r_1 r_2} (8)
```

注意，在样本量计算中不需要指定 `{a_k, b_k}, k=1,2` 的真实值，只需指定差异 `|b_k - b_k| = \Delta`。样本量与测量误差差 `\sigma^2` 成正比，并随着 `r_i` 接近 1/2 而减小。

### 18.5.2.2 二分类变量情况

令 `p_{kj} = a_k + b_kt_{kj}` 表示 `H_1` 下的成功概率。Jung 和 Ahn (2005) 显示：

```
v_k = \frac{s_k^2 + c_k}{s_k^4}
```

其中：

```
s_k^2 = \sum_{j=1}^{m} \delta_j p_{kj} q_{kj}(t_j - \tau)^2
```

```
c_k = \sum_{j=1}^{m} \sum_{j'=1}^{m} \delta_{j'} \rho_{jj'} \sqrt{p_{kj}q_{kj}p_{k'j'}q_{k'j'}}(t_j - \tau)(t_{j'} - \tau)
```

其中：

```
\tau = \frac{\sum_{j=1}^{m} \delta_j t_j}{\sum_{j=1}^{m} \delta_j}
```

此处，`v_k` 的表达式在连续和二分类结局变量之间略有不同，如下。为了处理缺失值，令 `\delta_j` 表示在 `t_j` 有观测的患者比例，`\delta_{j'}` 表示在 `t_j` 和 `t_{j'}` 均有观测的比例。此外，令 `\rho_{ij'} = corr(y_{ij}, y_{ij'})`。假设缺失模式和相关结构在组间是相同的。

（注：此处原文存在部分重复和逻辑断层，已根据语境进行对齐翻译）

# 416 使用 SAS 进行观察性健康数据分析

- 组 `k` 的分配比例，`r_k`。
- 相关性结构和 (ii) 相关的相关性参数 `\rho`，即 (i) 对于可交换性 `\rho_{ij} = \rho`，或 (ii) 对于 AR(1) `\rho_{ij} = \rho^{|t_i-t_j|}`）。
- 在 `t_j` 处有观测值的患者比例 `\delta_j`。
- 缺失模式：(a) 独立缺失 `(\delta_{ij} = \delta_i\delta_j)` 或 (b) 单调缺失（对于 `j < j'` `\delta_{ij} = \delta_j`）。

此外，我们需要在连续结果变量中指定 `\sigma^2=var(\epsilon_i)`，并在二分类结果变量中指定 `H_i` 下的回归系数 `{a_k, b_k}, k=1,2`。

我们将用纵向数据演示我们的样本公式。

## 示例 18.6 连续结果案例

在一项关于分娩的研究（Davis, 1991）中，83 名处于分娩的女性被分配到镇痛药物（43 人）或安慰剂组（40 人）。每隔 30 分钟，患者自述的疼痛程度被标记在一条 100mm 的线段上，其中 0 = 无疼痛，100 = 极疼痛。每位女性的最大测量次数为 `m=6`，但在后期时间有许多具有单调模式的值。针对此类研究目标的一种简单方法可能是估计并比较两个治疗期间疼痛评分的斜率。在这项研究中，结果变量是连续的。假设我们想根据 Davis (1991) 报告的数据设计一项关于分娩疼痛的新研究。与原始研究一样，我们假设为单调缺失。在该研究中，测量时间是等距的，为了方便起见，我们设置 `t_j=j-1` (`j=1,...,6`)。从数据中，我们获得了 `\sigma^2=815.84`。假设我们想检测两组在 `t_i` 时主疼痛评分的 `\sigma` 差异。我们在一项新研究中预测 `\Delta=\sigma(t_i-t_j)=5.71`。我们考虑平衡设计（即 `r_1=r_2=1/2`）。此外，根据数据，观测测量值的比例为

`(\delta_1,\delta_2,\delta_3,\delta_4,\delta_5,\delta_6)=(1,90,78,.67,54,41).`

从这些结果中，我们获得 `\tau=2.02` 和 `s^2=11.42`。

假设我们想使用双侧 `\alpha=.05` (`z_{1-\alpha/2}=1.96`) 检验，以 81% 的效能 (`z_{1-\alpha})=0.84)` 检测 `\Delta=5.71` 的差异。在可交换相关结构下，我们从数据中获得 `\rho=.64` 和 `c=-3.13`，使得 `v=815.84 \times (11.42-3.13)/11.42^2=51.84`。因此，根据 (8)，所需的样本量计算如下：

```
$n=[\frac{51.84(1.96+0.84)^2}{5.71^2}]+1=50。
```

其中 `[x]` 是不大于 `x` 的最大整数。

在 AR(1) 下，我们从数据中获得 `\rho = .80` 和 `c = 2.31`，使用双侧 `\alpha = .05` 检验检测 `\Delta = 5.71` 达到 80% 的所需的样本量为 `n = 83`。在这个例子中，AR(1) 下的样本量比可交换相关的大约 66%。

## 程序 18.6 两组重复连续测量比较的 SAS 代码



## 使用 SAS 分析观察性数据

```sas
%macro SS_RepeatedContinuousMeasurement(
    Pattern = /* 1: 独立缺失 2: 单调缺失
    CorrStructure = /* 1: 复合对称 2: AR(1)
    rho = /* 相关参数
    m = /* 测量点数
    sigma_sq = /* 方差
    inR = /* 分组分配 (r1, r2)
    inDelta = /* 观测测量值的比例
    alpha = /* alpha
    power = /* 效能
    sides = /* 1: 单侧检验; 2: 双侧检验
    print = /* 默认
);
proc ml;
    let k = 2; r=inR, delta=inDelta; J(m,0);
    do j=1 to m; delta[j]=j-1; end;
    if %inDelta%eq then do;
        delta=J(m,1); do j=1 to m; delta[j]=-(j-1)/2; end;
        d=sqrt(sigma_sq/sq(t)); start(gp); gp=log(p/(1-p)); return (gp);
        start(prob(a,b,t)); p=1/(exp(-a-b)); return (p); if c=1 then do; /* CS */ rho_ij=rho; end; 
        else do; /* AR(1) */ rho_ij=abs(i-j); rho_ij=r; end; 
    tau=0; tau_denum=0;
    do j=1 to m; tau=tau+delta[j]*t[j]; tau_denum=tau_denum+delta[j]; end;
    tau=tau/tau_denum; s_sq=s_sq*((t[j]-tau)**2); end;
    do i=1 to m;
        c=0;
        do j=1 to i;
            if %Pattern%=1 then do; delta_ij=delta[i]*delta[j]; end;
            else if j>max_ij then max_ij=j; delta_ij=delta[i]*delta[max_ij];
            c+=delta_ij*htlo(i,j,&CorrStructure)*(t[i]-t[j]);
        end;
    end;
    v=%sigma_sq/c; z_p=1-alpha/sides; z_beta=power; n=int(v*(z_p+z_beta)**2);
    print Sample Size Calculation for a Two-Group;
    print Repeated Continuous Measurements;
    alpha=%alpha;power=&power;rho=%rho;sides=&sides;
    if %Pattern%=1 then do; print 'Missing Pattern: Independent '; end;
    else if %Pattern%=2 then do; print 'Missing Pattern: Monotone '; end;
    else if %CorrStructure%=2 then do; print 'Correlation Structure: AR(1)'; end;
    if %print%=1 then do; print delta; print v; end;
    print sigma_sq; print n;
run;
%end SS_RepeatedContinuousMeasurement;
```

### 当相关结构为复合对称运行时运行示例 18.6

```sas
/* 当相关结构为复合对称运行时运行示例 18.6 --/
%SS_RepeatedContinuousMeasurement(
    missingPattern = 2,                /* 单调缺失
    corrStructure = 2,                 /* 复合对称
    rho = .64,                         /* 相关参数
    m = 6,                              /* 测量点数
    sigma_sq = 815.84,                 /* 方差
    inR = str((0.5, 0.5)),             /* 分配比例 (r1, r2)
    inDelta = str{(1, 0.9, 0.78, 0.54, 0.41)}, /* 观测测量值的比例
    alpha = 0.05,                      /* alpha
    power = 0.8,                       /* 效能
    sides = 2,                         /* 侧
    print = 1;                        /* 双侧检验
);
```

### 当相关结构为 AR(1) 时运行示例 18.6

```sas
/* 当相关结构为 AR(1) 时运行示例 18.6 --/
%SS_RepeatedContinuousMeasurement(
    missingPattern = 2,                /* 单调缺失
    corrStructure = 2,                 /* AR(1)
    rho = 0.8,                          /* 相关参数
    m = 6,                              /* 测量点数
    sigma_sq = 815.84,                 /* 方差
    inR = str((0.5, 0.5)),             /* 分组分配比例 (r1, r2)
    inDelta = str{(1, 0.9, 0.78, 0.54, 0.41)}, /* 观测测量值的比例
    alpha = 0.05,                      /* alpha
    power = 0.8,                       /* 效能
    sides = 2,                         /* 侧
    print = 1;                        /* 双侧检验
);
```

### 程序 18.6 的输出

```
------当相关结构为复合对称时 -----

      两组重复连续测量比较的样本量计算

      ALPHA POWER RHO SIDES
      0.05   0.8   0.64

      缺失模式: 单调
      相关结构: 对称

      TAU      SQ          C      V
      2.02 11.42 -3.13    51.84

                  D       SIGMA
             5.71 815.84

------当相关结构为 AR(1) 时 -----

      两组重复连续测量比较的样本量计算

      ALPHA POWER RHO SIDES
      0.05   0.8   0.80

      缺失模式: 单调
      相关结构: AR(1)

      TAU      SQ          C      V
      2.02 11.42 2.31      83

                  D       SIGMA
             5.71 815.84
```

## 示例 18.7 二分类结果案例

硬皮症（或称硬化症）是一种病因不明、具有内脏纤维化、小血管损伤和自身免疫特征的多系统疾病（Mesger, 1997）。该研究设计为德克萨斯大学休斯顿健康中心与加尔维斯德克萨斯大学医学分部以及德克萨斯大学圣安东奥卫生科学部的合作（Revel et al., 2001），对受试者进行定期随访以检查肺纤维化的发生。

假设想开发一项研究，检查新药在预防硬皮症患者发生肺纤维化方面的效果。在这种情况下，结果是二分类变量。我们想使用 $\alpha =05$ 和 $1-\beta =8$ 来估计样本量。在正在进行的 GENISOS 研究中，大约 75% 的硬皮症患者基线时没有肺纤维化（即 $p_{i,1}=.75$）。我们预测安慰剂组在 30 个月后无肺纤维化的比例为 50%（即 $p_{i,6}=.50$）。我们假设新疗法将防止或延迟肺纤维化的进一步发生。也就是说，在 30 个月的研究中，新疗法组无肺纤维化的比例将保持在 75%（换说 $p_{2,1}=p_{2,6}=.75$）。根据这些值和 (9)，我们得到

```
$b_1 = \frac{g(5)-g(7)}{5-0} = -0.220,$
```

## 420 使用 SAS 进行观察保健分析

$a_i=g(75)=1.099$。同样，我们得到 $(a_i, b_i)=(1.099, 0)$，因此

$\Delta=0-(-0.220)=0.220$。根据公式 (5)，安慰剂组在 6 个时间点无肺纤维化的概率分别分别为 $(750,707,659,608,555,500)$，治疗组为 $(750,750,750,750,750,750)$。

观测测量值的比例预期为：

```
$(\delta_i,\delta_j,\delta_i,\delta_j,\delta_i,\delta_j)=(1.95,90,85,80,75).$
```

假设我们期望进行独立监测。那么，对于指定的 $\delta_{ij}$ 值，使用 $\delta_{ij}'=\delta_{ij}'$ 得到 $\delta_{ij}'$。现在我们获得了所需的参数值，并得到 $v_1=0.305$ 和 $v_2=0.353$。根据公式 (7)，我们得到：

```
$n=\left[\frac{(1.96+0.384)^2}{0.305/0.5+0.353/0.5}}{0.220^2}\right]+1=215.$
```

如果我们假设单调性 $(\delta_{ij}'=\delta_{ji}')$，我们得到 $v_i=0.324,..v_j=0.328$ 且 $n=229$。

## 程序 18.7 重复测量组比较 SAS 代码

```sas
* SAS _RepeatedMeasurement;
missingPattern = /*1: 独立监测; 2: 单调
corrStructure = /*1: 复合对称; 2: AR(1)
rho = /* 相关参数
m = /* 测量时间点数
option = /* 控制组受试者
inP1 = /* 受试者比例
inP2 = /* 受试者比例
inodelta = /* 分组 (r1,r2)
alpha = /* 观测测量值的比例
power = /* 功效
sides = /* 1: 单侧检验 2: 双侧检验
proc;
start g(p) g=log(p)/(1-p)); return(g); finish g;
start prob(a,b,t) p=1/(1+exp(-b*t)); return(p); finish prob;
return(rho);
start (i,j,c);
if c=1 then do rho_ij=i; else rho_ij=r; end
if c=2 then do /* AR(1) */ abs=abs(i-j); rho_ij=r**; end
return(rho);
finish rho;
plot PL=inP1&inP2; a=K; j=m; b=J(K,1,0); t=J(K,1,0);
tau=J(K,1,0); s2_sq=J(K,1,0); c_sq=J(K,1,0);
for j=1 to m; t[j]=j-1; end
if &deltaeq=t then do
delta=delta[j]
for i=1 to delta[j]; delta[i]=(1-j)/200; end
end;
b[i]=g(Q1(i))-g(P1(i))/(t[i]); a[1]=g(P1(i))-B[1]*t[i]; a[2]=g(P2(i))-B[1]*t[i];
d=b[2]-b[1]
for j=1 to m; T[j]=j-1; P1[j]=prob(a,b[1], t[j]); P2[j]=prob(a,b[2], t[j]);
end;
taul_denum=0; tau=0; tau2_denum=0;
for j=1 to m;
taul_denum=taul_denum+delta[j]*P1[j]*(1-P1[j]);
tau2_denum=tau2_denum+delta[j]*P1[j]*(1-P1[j]);
tau_num=tau_num+delta[j]*P2[j]*(1-P2[j]);
tau_den=tau_den+delta[j]*P2[j]*(1-P2[j]);
end;
tau[1] = tau_num/tau_den; tau[2] = tau_num/tau2_denum;
s1=0;s2=0;
for (j=1; j<=6; j++) {
  s1 = s1+delta[j]*P1[j]*(1-P1[j])*(tau[1])**2;
  s2 = s2+delta[j]*P2[j]*(1-P2[j])*(tau[2])**2;
}
s_sq[1]=s1;s_sq[2]=s2;c1=0;c2=0;
for (i=1; i<=6; i++) {
  if (i == j) {
    if (missingPattern) {
      delta_ij = delta[i];
    } else {
      if (j > max_i) max_i = j;
      delta_ij = delta[max_i];
    }
  }
  c1=c1+delta[i]*delta_ij*rho(corrStructure)*P1[i]*(1-P1[i])*(tau[1]);
  c2=c2+delta[i]*delta_ij*rho(corrStructure)*P2[i]*(1-P2[i])*(tau[2]);
}
n = Sample Size Calculation for a Two-Group Comparison
print Repeated Measurements;
alpha=alpha;power=power;rho=rho;sides=sides;
if (missingPattern == 1) print ' Missing Pattern: Independent ';
else if (missingPattern == 2) print ' Missing Pattern: Monotone ';
else if (corrStructure == 1) print ' Correlation Structure: Compound ';
else if (corrStructure == 2) print ' Correlation Structure: AR(1) ';
print P1 delta v; print d; n;
run;
```

## 第18 章 观察性样本量计算 421

## 422 使用 SAS 进行观察保健分析

### 程序 18.7 的输出

| 缺失模式独立 |
| :--- |
| 重复测量组比较的样本量计算 |
| ALPHA | POWER | RHO | SIDES |
| 0.05 | 0.8 | 0.8 | 2 |
| 缺失模式：独立相关结构 : AR(1) |
| P1 | P2 | DELTA | V |
| 0.75 | 0.75 | 1 | 0.3048798 |
| 0.7065921 | 0.75 | 0.3534175 |
| 0.6590733 | 0.75 | 0.9 |
| 0.6081268 | 0.75 | 0.85 |
| 0.5547107 | 0.75 | 0.8 |
| 0.5 | 0.75 | 0.75 |
| D | 0.2197225 |
| N | 215 |

| 当缺失模式为单调 |
| :--- |
| 重复测量组比较的样本量计算 |
| ALPHA | POWER | RHO | SIDES |
| 0.05 | 0.8 | 0.8 | 2 |
| 缺失模式：单调相关结构 : AR(1) |
| P1 | P2 | DELTA | V |
| 0.75 | 0.75 | 1 | 0.3236844 |
| 0.7065921 | 0.75 | 0.384059 |
| 0.6590733 | 0.75 | 0.9 |
| 0.6081268 | 0.75 | 0.85 |
| 0.5547107 | 0.75 | 0.8 |
| 0.5 | 0.75 | 0.75 |
| D | 0.2197225 |
| N | 215 |

## 18.6 讨论

在设计观察性研究时，我们应该选择一种用于分析数据的统计方法。为了获得准确的样本量，样本量公式应从功效函数推导。样本量计算中包含两类参数：主要参数和干扰参数。主要参数出现在统计假设中；干扰参数是次要关注的。由于这类参数决定了最终样本量，尽可能准确地指定参数值很重要。如果某些参数存在不确定性，我们可以对功效进行敏感性分析，以证明在范围内功效是足够的。

## 附录：$H_0$ 下和检验的渐近分布

设 $\tilde{X}_i = X_i - \theta_k$。那么 $\tilde{X}_1, \dots, \tilde{X}_{n_1}, \dots, \tilde{X}_{n_2}$ 是独立同分布（IID），分布分布函数（CDF）为 $F(x)$。注意到



$W = \frac{1}{n_2} \sum_{i=1}^{n_1} I(\tilde{X}_i > \tilde{X}_j - \Delta),$我们有 $W = \int_{-\infty}^{\infty} d\hat{F}_k(x)$，其中 $\hat{F}_k(x) = n_k^{-1}\sum_{i=1}^{n_k}I(\tilde{X}_i \le x)$ 是 $\tilde{X}_1, \dots, \tilde{X}_{n_k}$ 的经验分布函数，当 $n_k \to \infty$ 时一致收敛于 $F(x)$。设

$v_o = P(\tilde{X}_{ij} > \tilde{X}_j - \Delta) = \int_{-\infty}^{\infty} F(x+\Delta)dF(x)$。对于较大的 $n$，$W-v_o$ 表示为：

```
\int_{-\infty}^{\infty} F(x+\Delta)d\hat{F}_2(x) - \int_{-\infty}^{\infty} \hat{F}_2(x+\Delta)-F(x+\Delta)dF(x) + o_p(n^{-1}),
```

其中 $o_p(n^{-1}) = \int_{-\infty}^{\infty}\{\hat{F}_2(x+\Delta)-F(x+\Delta)\}d\hat{F}_1(x)-F(x)\}$ 在较大的 $n$ 时是可以忽略不计。

## 42 使用 SAS 进行观察性健康数据分析

由于

```
$$\int_{-\infty} F(x+\Delta)\hat{F}_i(x) = \frac{1}{n_i} \sum_{l=1}^{n_i} F(\tilde{X}_{il} + \Delta)$$
```

以及

```
$$\hat{F}_2(x+\Delta)F(x) = \frac{1}{n_2} \sum_{l=1}^{n_2} F(\tilde{X}_{2l} - \Delta)$$
```

我们有 $var(W) = \sigma_1^2/n_1 + \sigma_2^2/n_2$，其中

```
$$\sigma_1^2 = var[F(\tilde{X}_{il} + \Delta)]$$
```

```
$$\sigma_2^2 = var[F(\tilde{X}_{2l} - \Delta)] = var[F(\tilde{X}_{2l} - \Delta)]$$
```

# 参考文献

- Aalen, O. 1978. “Nonparametric inference for a family of counting processes.” Annals of Statistics 6: 701-726.

- Carroll, R. J., and D. Ruppert. 1998. Transformation and Weighting in Regression. New York: Chapman and Hall/CRC.

- Davis, C. S. 1991. “Semi-parametric and non-parametric methods for the analysis of repeated measurements with applications to clinical trials.” Statistics in Medicine 10: 1959–1980.

- Fleming, T. R., and D. P. Harrington. 1991. Counting Processes and Survival Analysis. New York: John Wiley & Sons, Inc.

- Gart, J. J. 1985. “Approximate tests and interval of the common relative risk in the comparison of 2 x 2 tables.” Biometrika 72: 673–677.

- Jung, S. H., and C. Ahn. 2003. “Sample size estimation for GEE method for comparing slopes in repeated measurements.” Statistics in Medicine 22: 1305–1315.

- Jung, S. H., and C. W. Ahn. 2005. “Sample size for a two-group comparison of repeated binary measurements using GEE.” Statistics in Medicine 24(17): 2583–2596.

- Jung, S. H., C. W. Chow, and E. Chi. 2007. “A note on sample size calculation based on propensity analysis in non-randomized trials.” Journal of Biopharmaceutical Statistics 35–41.

- Lakatos, E. 1988. “Sample sizes based on the log-rank statistic in clinical trials.” Biometrics 44: 229–241.

- Liang, K. Y., and S. L. Seeger. 1986. “Longitudinal data analysis using generalized linear models.” Biometrika 73: 13–32.

- Mann, H. B., and D. Wright. 1947. “A test of whether one of two random variables is stochastically larger than the other.” The Annals of Mathematical Statistics 18: 50–60.

- Medsger, J., Tr., T. A. 1997. “Systemic sclerosis (scleroderma): clinical aspects. In Arthritis and allied conditions: a textbook of rheumatology. 13th ed. Edited by W. J. Koopman. Baltimore, MD: Williams & Wilkins, pp 1433–1464.

## 第 18 章 观察性研究的样本量计算

- Nelson, W. 1969. “Hazard plotting for incomplete failure data.” Journal of Quality Technology 1(1): 27–52.

- Peto, R., and J. Pete. 1972. “Asymptotically efficient rank procedures (with discussion)” Journal of the Royal Statistical Society, Series A: 135–206.

- Reveille, J. D., M. Fischbach, T. McNameney, et al. 2001. “Systemic sclerosis in US ethnic groups: a comparison of clinical, sociodemographic, serologic, and immunogenetic determinants.” Seminars in Arthritis and Rheumatism 30(5): 332–346.

- Rosenbaum, P. R., and D. B. Rubin. 1983. “The central role of propensity score in observational studies for causal effects.” Biometrika 70: 41–55.

- Rosenbaum, P. R., and D. B. Rubin. 1984. “Reducing bias in observational studies using subclassification on the propensity score.” Journal of the American Statistical Association 79: 516–524.

- Rubin, D. B. 1976. “Inference and missing data.” Biometrika 63: 581–590.

- Rubinstein, L. V., M. H. Gail, and T. J. Santner. 1981. “Planning the duration of a comparative clinical trial with loss to follow-up and a period of continued observation.” Journal of Chronic Diseases 34(9/10): 469–479.

- SAS Institute Inc. 2009. SAS/STAT 9.2 User’s Guide, Second Edition. Cary, NC: SAS Institute.

- Yue, L. Q. 2007. “Statistical and regulatory issues with the application of propensity score analysis to non-randomized medical device studies.” Journal of Biopharmaceutical Statistics 17: 1–13.

## 索引

### A

- 聚类方法 179

- AIC 信息准则 (AIC) 265, 280

- ALPHA语句，DATA step 224

- ANOVA 模型

    - 评估倾向评分 27–28

    - 评估差异 107

    - 填补策略 126

    - LC 分析 155

    - PSBB 317

- 关联

    - 因果 vs. 5–7

    - 定义 5

- CA（协变量调整）方法

    - 定义 183

    - LC 分析 165

    - 死亡率分析 157–158, 160

    - 倾向评分 62

    - RCT 和 347, 347

- CA（协变量调整）方法

    - 定义 183

    - LC 分析 165

    - 死亡率分析 157–158, 160

    - 倾向评分 62

    - RCT 和 347, 347

- 心脏护理网络 (CCN) 62–65

- CATMOD 225

- 因果 vs. 5–7

- CC（完全协变量）

    - 定义 106

    - Bootstrap 置信区间 123

    - 定义 106

    - 缺失值的 IPW 109–110

- CCN（心脏护理网络） 62

- CD试验 351–358

- CDF（累积分布）153–154

### B

- B/B（平衡）评分

    - 簇成员 187

    - 定义 187

    - 平衡特征 55–58

    - 定义 55

    - 跨组评估 205–207

    - 贝叶斯模拟 364

- 偏差

    - 隐藏 7

    - 观察性研究 385–390

    - 结果 7

    - 样本量和 9, 343

- 二分类结果 398–400

- CC（完全协变量）1-106

- CC（完全协变量）

    - 定义 106

    - 缺失值的 IPW 109–110

- BOOTCI 122–123

- BOOT 宏过程 122–123

- BOXPLOT 36

- CEA（成本效益性）

    - 定义 102

    - 治疗组 205–207

    - 匹配和 362

- CEAC（成本效益性曲线）344–346

- CC（完全协变量）

    - 定义 106

- CC（完全协变量）

    - 定义 178–179

    - 复习 178

- CLASS语句

    - 定义 102

### C

- 置信区间 122–123

- 计算样本量 413–416

- 因果效应 6–7

- 因果

    - 定义 178–179

- 聚类方法 179

- CC（完全协变量）

    - 定义 106

- CC（完全协变量）

    - 定义 178–179

- CDF（累积分布）153–154

- CDF（累积分布函数）153–154

### D

- DATA=option, NLP 过程 245

- DATA step

- ALPHA=语句 224

- 创建结果 255

- 数据库

- 剂量-响应分析 295–311

- 剂量-响应分析 295–311

- DR（稳健）估计 277–278

- DR 宏过程 88–94

- DR 宏过程 88–94

- 双分类结果 59–60, 二分类结果 398–400

- 离散选项，NLP 过程 144

- DIST 选项，NLP 过程 90–91

- 离散聚类方法 179

### E

- eCDF（经验累积分布函数）174–177

- eCDF（经验累积分布函数）174–177

- EM/C 算法 106

- eCDF（经验累积分布函数）174–177

- 末期肾疾病（ESRD）研究 296–310

- 末期肾疾病（ESRD）研究 296–310

- 内生性

- 促红红素剂 (ESA) 296–297

- ESRD（末期肾疾病）研究 296–310

- ESTIMATE 语句，GENMOD 过程 221

- 估计

- 可交换性，假设 88

- 实验研究 5

### F

- F(x+\Delta)

- F(x+\Delta)

- F(\tilde{X}_{il} + \Delta)

- F(\tilde{X}_{il} + \Delta)

- F(\tilde{X}_{2l} - \Delta)

- F(\tilde{X}_{2l} - \Delta)

### G

- 一般问题 386

- 全局印象 389

- 概念概述 86

### H

- 隐藏 7

### I

- 填补策略 126

- 缺失值的 IPW 109–110

### J

- Jung, S. H., and C. Ahn. 2003

- Jung, S. H., and C. W. Ahn. 2005

- Jung, S. H., C. W. Chow, and E. Chi. 2007

### K

- Lakatos, E. 1988

### L

- Liang, K. Y., and S. L. Seeger. 1986

- 纵向数据 392

- Aalen, O. 1978

- Carroll, R. J., and D. Ruppert. 1998

- 纵向数据 392

- Liang, K. Y., and S. L. Seeger. 1986

- Mann, H. B., and D. Wright. 1947

- Medsger, J., Tr., T. A. 1997

- Nelson, W. 1969

- Peto, R., and J. Pete. 1972

- Reveille, J. D., M. Fischbach, T. McNameney, et al. 2001

- Rosenbaum, P. R., and D. B. Rubin. 1983

- Rosenbaum, P. R., and D. B. Rubin. 1984

- Rubin, D. B. 1976

- Rubinstein, L. V., M. H. Gail, and T. J. Santner. 1981

- SAS Institute Inc. 2009

- Yue, L. Q. 2007

### M

- Mann, H. B., and D. Wright. 1947

- Medsger, J., Tr., T. A. 1997

### N

- Nelson, W. 1969

### O

- 观察性 382

### P

- Peto, R., and J. Pete. 1972

- Reveille, J. D., M. Fischbach, T. McNameney, et al. 2001

- Rosenbaum, P. R., and D. B. Rubin. 1983

- Rosenbaum, P. R., and D. B. Rubin. 1984

- Rubin, D. B. 1976

- Rubinstein, L. V., M. H. Gail, and T. J. Santner. 1981

- 倾向评分 24–52, 53–64, 65

- 倾向评分 24–52, 53–64, 65

- 倾向评分 24–52, 53–64, 65

- 倾向评分 24–52, 53–64, 65

- 倾向评分 24–52, 53–64, 65

- 倾向评分 24–52, 53–64, 65

- 倾向评分 24–52, 53–64, 65

- 倾向评分 24–52, 53–64, 65

- 倾向评分 24–52, 53–64, 65

- 倾向评分 24–52, 53–64, 65

- 倾向评分 24–52, 53–64, 65

- 倾向评分 24–52, 53–64, 65

- 倾向评分 24–52, 53–64, 65

- 倾向评分 24–52, 53–64, 65

- 倾向评分 24–52, 53–64, 65

### Q

### R

- Peto, R., and J. Pete. 1972



# 索引 429

观察性 vs ds 3–5

暴露 (exposure)

`GLOGIT` 选项，`MODEL` 语句 128

`%GMATCH` 宏 65

拟合度检验 25

贪婪匹配方法 53–54

`GROUP=`选项，`RANK` 过程 32

另见独立变量

概率的 DR 分析 97

对结果的影响 74–80

治疗与 323

# F

# H

FDA (美国食品药品管理局) 228

FHS (弗兰明汉心脏病研究) 5

Fieller 定 368, 380

FMI (缺失信息) 126

美国食品药品管理局 (FDA) 228

来自缺失信息 (FMI) 126

弗兰明汉心脏病研究 (FHS) 5

`FREQ` 过程

用于解决选择偏的 IV 方法

134, 139

倾向评分示例 33

PSBB 和 323

风险比 (HR) 296, 304, 307

健康协作抑郁研究 (NIH)

198–207

健康维护组织 (HMO) 134,

136

健康相关生活质量 (HRQOL) 232,

239

健康服务研究期刊 132

血液透析研究 296–310

异方差性 168

隐藏偏倚 7

# G

HIPAA 288

HMO (在健康维护组织中) 134,

136

异方差性 168

HR (风险比) 296, 304, 307

HRQOL (健康相关生活质量) 232,

239

G-计算公式 (Robins) 264

伽马分布 333, 351, 354–356

GEE (广义估计方程) 60,

304–305, 410

广义模型 25, 316

GENOS (硬化症结果中的遗传与环境研究)

410–422

# I

ICD 编码系统 298

ICER (增量成本效益比)

316–323, 340–345, 368–397

IML 过程 259–260

INB (增量净收益)

关于 339–340

GENMOD

剂量反应分析 300, 304, 307

双稳健估计 100

ESTIMATE 方法 221

IN 示例 359

用于解决选择偏的 IV 方法

148

LINK–LOGIT 选项 216

倾向评分示例 36–37

PSBB 和 318, 320, 323

精神分裂症研究 275

WEIGHT 检验 221

CD 试验 351–368

成本效益分析 341–346, 365

定义 316

GLM 过程

计算最小二法 138

创建残差 254–255

用于解决选择偏的 IV 方法

147–148

PSBB 和 318, 320

SNM 示例 253

标准化权重和 109

观察性研究 319

参数估计 346–351

增量成本效益比 (ICER)

316–323, 340–345, 368–379

增量净收益

另见 INB (增量净收益)

IND (指示变量法)

定义 106

带有缺失值的 IPW 估计

110–111

独立变量

混杂与 7

在逻辑回归中 25

缺失模式 414–422

# 430 索引

指示变量 (IND) 方法

106

带有缺失值的 IPW 估计

110–111

诱导逆向截尾 364

工具变量方法

另见 IV (工具变量) 方法

国际药物用经济学与结果研究学会 (ISPOR)

288, 316–317

逆概率加权法

另见 IPW (逆概率加权) 方法

IPW (逆概率加权) 方法

CA 方法和 158, 160

183

剂量反应分析 300–304

双稳健估计和 86

估计差异 107

处理极端 127–128

死亡率 162–163

敏感性分析 124

带有值 109–123

ISPOR (国际药物用经济学与结果研究学会); 288, 312–317

ITT LOC 分析 211–212, 227

IV (工具变量) 方法

解决选择 131–150

应用于案例研究 139–143

案例研究设计 134–137

挑战 147–148

聚类支持 155

定义 12, 183

最小二法回归方法 138

概述 131–133

QLIM 过程和 143–146

回归调整方法比较

146–147

敏感性分析和 13

# K

Kaplan-Meier 估计量 366, 370, 380

Kaplan-Meier 生存曲线 60–61, 76–77

# L

LATEs (局部平均治疗效应) 155

LC (局部控制) 分析

定义 183

确定显著性 164, 174–177

基本概念 153–154

识别基线特征 165, 179–182

患者风险，数据分析 156–163

执行敏感性分析 165, 178–189

随机化问题 152–153

揭示偏倚 163–174

战术方法 154–155

通过密钥 163–182

LCLF 研究 239–252

最小二法回归方法 138

LIFETEST 过程 370

似然比检验 198, 203

LINK–LOGIT 选项，LOGISTIC 过程 216

LINK–LOGIT 选项，GENMOD 过程 216

局部平均治疗效应 (LATEs) 155

局部控制分析

另见 LC (局部控制) 分析

局部治疗差异

另见 LC (局部控制) 分析

对似然 239

对数 检验 405–409

LOGISTIC 过程

创建残差 254–255

用于解决选择偏的 IV 方法

148

LINK–LOGIT 选项 216

倾向评分示例 32–33

PSBB 和 318, 320, 323

精神分裂症研究 267, 271

WEIGHT 检验 221

逻辑回归

估计倾向评分 89–90, 95–96

混合效应模型 196–202

组间比较 410–422

连续结果 392–398

JMP

另见 LC (局部控制) 分析

Analyze 方法 166, 180

聚类考虑 168–180

启动功能 166

Next Number of Clusters 对话框 169

Open Data 对话框 167, 175

# 431 索引

治疗倾向模型 195–209

NIH 协作抑郁研究 198–200

回归模型 263–283

治疗效果分析 197–198, 203–205

两阶段倾向调整 195–209

识别基线特征 179–182

在 LC 阶段 164–165

系统敏感性 178–179

# M

MADIT (多中心除颤器术) 365, 369–380

Manel-Haensel 过程 198

Manel-Haensel 检验 398, 400–405

任何对一匹配 55, 57

形成倾向评分 53–55

极大似然数据分析 238–252

Mayo Clinic 研究 59–71, 75

McNamara 检验 65

测量偏倚 385–390

医疗索赔 287–294

药物效果 30–46

MEDLINE 数据库 37

流行病学元分析 (MOOSE) 14

方法

*统计方法

MI (多重插补) 方法

bootstrap 置信区间 123

定义 106

带有截断数据的 CEA 364

截断 364

数据质量 288

处理 107–108

缺失值 109–110

ND 分析 110–111

MI 分析 111–115

MIMP 分析 120–120

MP 分析 115–119

MSM 方法论 213, 227

倾向评分 105–130

研究清单 289–291

缺失模式 (MP) 方法

*另见 MP 方法)*

MIXED 过程

带有缺失值的 IPW 估计 113

标准化权重 108–109

MODEL 语句

DISCRETE 选项 144

DIST=选项 90–91

DR 考虑 102

GLOGIT 选项 128

精神分裂症研究 280

SELECT 选项 146

指定结果回归 89

指定权重模型 88–89

蒙特卡洛模拟 62

流行病学元分析 (OOSE) 14

MORE (雷洛昔芬多重结果) 107

# 432 索引

死亡率分析

CA 方法 157–158

估计倾向评分 158–161

IPW 模型 (缺失模式) 162–163

定义 106

带有缺失值的 IPW 估计 115–119

敏感性分析 124

MSM (边际结构模型) 定义 12

剂量反应分析 295–311

LCLF 研究 239

方法论 213–214

符号 212

精神分裂症研究 214–227

敏感性分析和 13 221–223

治疗效果分析模型

多中心除颤器术 (MADIT) 365, 369–380

多重插补方法

另见 Mi (多重插补)

多重插补缺失模式

另见 Miimp (多重插补缺失模式)

雷洛昔芬多重结果 (MORE) 107

# N

美国健康研究所 (NIH)

弗兰明汉心脏病研究 5

健康协作抑郁研究 198–207

Nelen-Allison 估计量 406

神经网络 25

Newton-Raph 算法 411

NIH (美国健康研究所) 弗兰明汉心脏病研究 5

健康协作抑郁研究 198–207

NLP 过程

BOUNDS 语句 245–246

COVARIANCE=选项 245, 248

DATA=选项 245

LCLF 研究和 243–252

起始值 254

极大似然化 256–259

输出考虑 244–245

PARMS 语句 245

PCOV 选项 245

VARDEF=选项 245

NNT (需治疗) 59 非实验性研究

另见观察性研究

非参数自助法 318

非参数密度估计 56

NPARWAY 过程 317 需治疗人数 (NNT) 59

![](img/fe9008f88baacd415148b0b25dd58c_446_0.png)

观察性研究

另见研究纵向观察性研究 385–390

关联 vs 因果 5–7 混杂在 7–

成本估计 363–364 定义 3,32

实验性研究 vs. 3–5 数据分析一般方法

183–184 般想法 386–387 287–294

增量收益 5–9 方法 10–13

可重复性 8–9 报告指南 13–14

样本量计算 391–425 选择偏倚在 7–8,391

敏感性分析和 13 研究 9–10

类型错误在 8–9 观察者偏倚 386–387

# 索引 433

OUTPUT 语句 144

- 过度偏倚 7

- 评估产的平衡 36–46

- 基本定理 185–186

- 局限性 29–30

- 药物疗效研究 30–46

- 死亡率分析 158–161

- 目的 24,27

## P

- 倾向评分匹配 55

- 配对 t 检验 (paired-t-test)

    - 连续结局和 59

    - 解决选择偏倚的 IV 方法 146

- 参数参数 346–351

- 参数化模型

    - 估计问题 186–187

    - 五分位数分类 197

- 回归调整 26–30, 60

- 敏感性分析和 26–27, 62, 198

    - 含有缺失值 105–130

- 倾向评分自助法 (PSBB)

    - 关于 315–319

    - 精神分裂症研究 320–334

- 倾向评分匹配 (PSM)

    - CA 方法 165, 183

    - LC 分析和 183–184

    - SNMM 和 237–238, 242–243

    - PARMS 语句, NLP 过程 245

    - 分层估计器 36

- 患者健康问卷 (PHQ) 30–46

- 患者注册数据分析 156–163

- CPOY 选项, NLP 过程 245

- 药物经济学

    - 对对比的 CEA 363–382

    - 良好的研究实践 288

    - 增量收益 339–362

    - 倾向评分分箱自助法 315–337

    - 报告指南 14

    - 基线特征评估 55–58

    - 与其他方法的比较 62

    - DES/BMS 安全性和有效性研究 62–80

    - 估计倾向评分 52

    - 形成匹配集 53–55

    - 概述 52

    -  61–62 的敏感性分析

- 流行病学

    - 良好的研究实践 287

    - 报告指南 14

    - PHQ (患者健康问卷) 30–46

    - PRE 过程 304

    - PLOT 过程 320

    - 泊松回归模型 100–101

    - POWER 过程 394, 407, 409

    - PREDICTED 输出, OUTPUT 语句 144

    - 抑制回归

## PS

- 参见倾向评分 (PS)

- PSBB (倾向分箱自助法)

    - 关于 315–319

    - 精神分裂症研究 320–334

    - 定义 52

    - 估计倾向评分 24

    - 解决选择偏倚的 IV 方法 144

- QLIM 过程 143

- 分位数-分位数图 56

- 倾向评分 (PS)

    - 也参见纵向观察研究

    - 也参见 RMLS (基于倾向评分的回归模型)

    - 优势 29–30

    - 偏倚减少方法 105–106

    - 计算 32–33

    - 定义 12, 24, 52, 183

    - 双健估计和 84–104

    - 估计 24, 52, 53, 64–65

    - 评估 27–28

## R

- 随机化

    - 基础问题 152–153

    - 关键作用 152

- 随机对照试验

    - 参见 RCTs (随机对照试验)

- RANK 过程

    - GROUPS=option 32

    - 倾向评分示例 232

    - PSBB 和 323

    - 精神分裂症研究 267, 223

- RCTs (随机对照试验)

    - 金标准 23

    - 关联与因果 5–7

    - 偏倚 4

    - Trial 351–358

# 434 索引

- RCTs (随机对照试验) (续)

    - CONSORT 语句 14

    - 调整方法 347, 356

    - 定义 3

    - 推广性 4

    - 测量偏倚 386

    - 方法论考量 10–13

    - 观察者偏倚 388

    - 随机化 58

    - 可复制性 8

    - 报告指南 14

    - 优势 3–4

    - 研究设计 9–10

- RDC (研究标准) 198

- 受试者工作特征

    - 参见 *ROC* (工作特征)

- REG 过程 148

- 回归调整方法

    - IV 方法比较 146–147

    - 倾向评分 26–30, 60

- 纵向倾向评分回归模型

    - 参见 *RMLPS* (纵向倾向评分回归模型)

    - 观察性研究的可复制性 8–9

    - 观察性研究的报告指南 13–14

- 研究标准 (RDC)

    - 实践 385–390

    - 清单 289–294

    - 回顾数据库 287–288

    - 使用大型数据库的响应 295–311

- RMLPS (纵向倾向评分回归模型)

    - 关于 263–265

    - 估计 265

    - 精神分裂症研究 262–282

    - Robins G 计算公式 264

- ROC (工作特征)

    - CA 方法 157

    - 定义 58

    - PW 方法 216

    - 倾向评分估计 158

- 倾向评分估计

    - 计算观察性研究 391–425

    - 清单 289, 291

    - 混杂因素 9

    - 回顾数据库研究 293–294

    - 非参数自助 318

    - 偏态 317

    - 精神分裂症研究

    - MSM 和 214–224

    - PSBB 和 320–334

    - RMLPS 和 266–282

    - 硬化 419–422

    - SELECT 选项, MODEL 语句 146

    - 选择偏倚

        - 定义 387

        - 良好的研究实践 288

        - 观察性研究 7–8, 391

        - RCTs 4

        - IV 方法解决 131–150

        - LC 分析中的揭示 163–174

        - 治疗 52

    - 敏感性分析

        - 聚类和 178–179

        - 局部控制方法 165, 178–179

        - 倾向评分权重 61–62, 75

        - 处理极端权重 127–128

        - 导入 13, 27

        - 纵向观察研究 224–227

        - 变异分析方法 124–125

        - 并列框 56

        - 成本数据 347, 351, 363–364

        - 样本量 317



# 435 索引

- 筛选方法 364
- `SHOW` 选项, `MODEL` 语句 89–90, 100
- 样本量和 317
- `SNM` (结构嵌套模型) 12
- `SNMM` (结构嵌套模型)
  - 关于 231–234
  - 估计 236–239
  - 获取初始值 254–256
  - 最大似然分析 238–252
  - 参数化模型和 237–238
  - 时间变性调节 235–236
- `SR` (分层回归) 方法 124–125
- 偏倚和 9, 343
- 标准误 92–93
- 差异方法 56, 68–74
- 统计方法
  - 常用 12
  - 评估匹配样本的平衡 56
  - 聚类和 155
  - 治疗效应
    - 针对选择偏倚调整 133
    - 减少 105
    - 计算 33–36
    - 针对删除数据的 CEA 364–368
    - 局部控制调整 154–155
    - 问题和考量 10–11
- 研究清单 289, 293
- 双健估计的 84–104
- 估计 24, 52, 53, 64–65
- 评估 27–28
- 纵向观察研究 195
- 倾向评分 26–30, 60, 198
- 倾向评分权重 61–62, 75
- 倾向评分分层模型 124–125
- `SR` (分层回归) 方法 124–125
- `STROBE` (观察性研究报告标准) 14
- 结构嵌套模型 (`SNMM`)
  - 关于 231–234
  - 估计 236–239
  - 获取初始值 254–256
  - 最大似然分析 238–252
  - 参数化模型和 237–238
  - 时间变性调节 235–236
- 结构嵌套模型 (`SNM`) 12
- 治疗
  - 参见独立变量
  - 估计 107
  - 评估组间平衡 205–207
  - 暴露和 39
  - 纵向模型 209
- 变量
  - 二分类 398–400, 411–414, 419–422
  - 定义清单 289, 291
  - 连续型 392–398, 416–419
  - 因变量 7, 25, 414–422
  - 独立变量 7, 25, 414–422
- `VARDEF=` 选项, `NLP` 过程 245
- `UNIVARIATE` (单变量)
- `CLASS` 方法 136
- 解决选择偏倚的 IV 方法 136
- 精神分裂症研究 29, 214
- 未测量的混杂因素 29, 214
- `USRDS` (美国肾脏数据系统) 298
- `WHI` (妇女健康健康计划) 5
- `%VMATCH` 65
- `WHERE` 语句 102
- `WT` 语句 102
- `WTMOD` 语句
  - `COMMON_SUPPORT` 选项 90, 92, 97–98
  - `SHOWCURVES` 选项 88–89, 97, 100
