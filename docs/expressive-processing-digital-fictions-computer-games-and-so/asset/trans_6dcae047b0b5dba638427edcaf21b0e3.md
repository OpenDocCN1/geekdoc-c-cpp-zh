

## 远离写作

从模板驱动的方法转向“真正”面向结构的自然语言生成（NLG）领域，也就意味着进一步远离写作。这一点在两个层面上都成立。提供给系统的信息也更远离写作。此外，由于所提供信息的差异，作者传统上用来塑造系统表面输出的技术——修订——变得与传统的文本编辑截然不同。这些事实很可能是比模板更复杂的NLG技术很少被作家采用的部分原因。

在他们的文章《构建应用自然语言生成系统》中，Ehud Reiter 和 Robert Dale（1997）概述了NLG系统的六种基本活动，以一个回答铁路旅行问题的系统为例。内容确定是获取NLG系统将转化为文本的语义信息，并创建后续步骤将使用的一组消息的过程（在示例中，即路线上的下一班火车、其出发时间以及每天有多少班火车行驶该路线）。话语规划将消息结构化，通常形成计算机科学中无处不在的树形结构之一（在示例中，下一班火车的身份及其出发时间成为“下一班火车信息”节点的叶子——它们之间存在“阐述”关系——并通过树根处的“序列”关系与“列车数量”信息相连）。句子聚合则是决定哪些消息应被分组为句子的过程，通常依赖树形数据（在示例中，指出这两个叶子可以合并，使下一班火车的名称和出发时间出现在同一个句子中）。词汇化是确定将用于表达特定概念和关系的词语和短语的活动。词汇化对于多语言输出的系统尤为重要，但也可以是明确提供变化（防止输出单调）或对用词选择进行决策的好地方（在示例中，建议depart可能比leave更正式）。指代表达生成在某些方面与词汇化密切相关，因为它是选择用于指代消息中实体的词语或短语。然而，它更关注上下文，特别是迄今生成的文本的上下文（在示例中，这是关于何时适合使用"it"、"this train"和"the Glasgow train"等表达来指代先前提到的火车的问题）。语言实现是应用语法规则，将先前过程的输出形成在句法、形态和正字法上正确的文本中。（在示例中，系统生成句子"There are 20 trains each day from Aberdeen to Glasgow." 实现器的句法组件添加了"from"和"to"以标记火车的出发地和目的地，形态组件从词根"train"生成了复数形式"trains"，正字组件将首字母大写并在句末添加了句号。）

从实际情况来看，NLG系统通常并不为这六种活动设置六个不同的组件。Reiter和Dale指出，最常见的架构实际上由一个三阶段流水线组成：文本规划（内容确定和话语规划）、句子规划（句子聚合、词汇化和指代表达生成）以及语言实现（句法、形态和正字处理）。Reiter和Dale在此的描述与其他NLG权威（如Eduard Hovy）的观点一致，后者在《MIT认知科学百科全书》中的摘要使用了近乎相同的术语：文本规划、句子规划和句子实现（Wilson和Keil 1999）。

这一概述还凸显了另一个可能的原因：很少有作家——事实上，很少有来自任何背景的数字媒体从业者——使用过传统的NLG技术。正如从Tale-Spin/Mumble到当今系统的设计所见，这些系统通常基于消息先于语言的假设来构建。它们的架构旨在使明确定义的消息能够被“实现”为文本。然而，对许多作家来说，创意写作是无法以其他方式表达的内容的实践。其消息并不先于文本，而是通过其语言的具体特征而产生。

Terminal Time、Brutus以及那些更直接参与NLG传统的系统，以不同方式应对这一创作困境。

## 终端时间模板

观察Terminal Time的NLG方法可以发现，该系统之所以能产生令人满意的媒体体验，部分原因在于它是一个灵活的文本容器，可以使用传统写作技巧进行制作。其方法本质上是面向模板的NLG，尽管底层系统的设计更为通用和强大，可以进一步挖掘。然而，就目前而言，Terminal Time的作者通常在句子层面为历史事件制作叙述。

在任何特定的Terminal Time表演中，面向受众的意识形态模型的当前形态将决定哪些事件会被描绘以及如何进行侧重。每个历史事件的文本都必须适当地描述该事件，既要给出其轮廓，又要根据当前的修辞目标调整描述。此外，由于Terminal Time的设计是让同一受众在短时间内观看两次，因此如果同一事件（出于相同的修辞目标）能以非重复的方式进行叙述，那就很有用。例如，以下是一个针对阶级问题的Terminal Time入门叙述的NLG规则：

```
(defn-rule name: generate
:context 'feudal-agrarian-first-period-intro
:body (seq
(terminal
(string "1000 years ago. Europe was emerging from the Dark Ages.")
(keywords (daily-life europe european peasant)))
(terminal
(string "As the new millennium dawned,
the seeds had been sewn for a just
and humane social order.")
(keywords (farming daily-life europe)))
(rule :detail)
(terminal
(string "The new millennium's fragile seeds of economic freedom were cultivated in the feudal agrarian economies.")
(keywords (daily-life farming europe))
(rule :conclusion))
(Mateas 2007)
```

由“string”引导的三个句子构成了叙述的主干。它们按顺序由合成的旁白声音朗读，并伴随标记了下一行指定关键词的视频片段。变化由以“:rule”开头的两行提供——一行用于补充细节，另一行用于结论。Terminal Time可以插入的可能细节句子范围从“农民和小商贩在和谐的当地以物易物经济中一起工作”到“与20世纪美国的资本主义暴食相比，这些农业社区的财富只略微集中”（附带相应的视频关键词）。可能的结论之一是：“工人欠他的土地所有者劳动，但不能被赶出他的家。”另一方面，不同的意识形态模型将导致对这些情况的略有不同的描述，例如可以得出这样的结论：“工人欠他的土地所有者劳动，并以此换取了拥有自己家园的权利。”

在叙述欧洲的农业过去时，Terminal Time基本上根据其意识形态模型的当前形态为叙述提供平行结构。然而，Terminal Time的作者选择将其他事件的不同叙述交织在一起。例如，以下是关于太空时代的入门叙述的NLG规则：

```
(defn-rule
 :name generate-rocket-science-intro
 :context %RocketScience
 :body (:seq
  (:terminal
   (:string "Beginning in (%date 1957) with
   the launch of the Russian satellite Sputnik
   atop an Intercontinental Ballistic Missile,
   human beings left the planet
   earth and began exploring space.")
   (:keywords (satellites rockets
   communism outer-space)))
  (:terminal
   (:string "This"
   ((%rhet-goal :show-the-
   hollowness-of-science)
   "mechanistic")
   "hymn to science reached its crescendo with
   the moon landing in (%date 1969).")
   (:keywords (moon rockets america outer-space
   technological-instruments astronomy)))))))
(Mateas 2007)
```

在此规则中，如果此事件被用于支持修辞目标“show-the-hollowness-of-science”，则单词“mechanistic”会被插入到第二个句子中。如果是，进一步的规则将产生一个后续句子

