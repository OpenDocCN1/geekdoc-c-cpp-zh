

由 Terminal Time 的机制为该受众制作历史叙述。接着是第一个提问环节，在此期间，“确立一个初始意识形态主题（来自性别、种族、技术、阶级、宗教的集合）和一个叙事弧（例如，这是一个进步还是衰落的叙事）”（Mateas, Vanouse, and Domike 2000）。下一阶段是生成并展示涵盖 1000-1750 年（公元）的故事部分，耗时六分钟。接着，第二组问题对第一组中选定的意识形态主题进行细化，并可能引入一个子主题（例如，种族带有阶级子主题，或技术带有宗教子主题）。然后生成并展示故事的下一部分，涵盖大约 1750–1950 年（公元），同样耗时六分钟。接着是最后一组问题，进一步细化主题，并引入反转的可能性（例如，衰落叙事可能变成进步叙事）。接着是生成并展示故事的最后阶段，涵盖大约从 1950 年（公元）到千禧年末。

随着每个叙事阶段的进行，意识形态模型不仅受观众反馈进一步塑造，而且在运作中也变得更加粗犷。这一点，加上观众对更近期历史的更大熟悉程度，导致故事中夸张的意识形态倾向在 Terminal Time 表演的二十分钟内变得越来越明显。在表演接近尾声时，这最终体现在诸如上面引用的关于中国入侵西藏的赞颂性描述等故事片段中。在那个特定案例中，起作用的意识形态目标是 Terminal Time 的创作者所称的属于“反宗教理性主义”的目标。

Terminal Time 中意识形态的表征基于为 Politics 系统开发的表征——而 Politics 系统本身是 1950 年代至 1970 年代由 Robert Abelson 及其合作者创建的意识形态机器的继任者（在第 4 章中讨论过）。在 Terminal Time 中，意识形态被表示为一组目标树——具体来说，是故事通过其千年历史将要展示的修辞目标。虽然初始观众投票产生的是 Terminal Time 作者最初设计的目标树之一，但进一步的提问可能会添加、删除或更改目标。例如，在第二轮提问期间，可以通过将一个树中的目标与另一个树中的目标相结合来引入一个子主题。

下面是一个 Terminal Time 创作示例——具体来说，是任何修改之前存在的反宗教理性主义目标树。请注意，因为“show-thinkers-persecuted-by-religion”是两个高级目标的子目标，它可以同时满足这两个目标。

```
show-religion-is-bad
show-religion-causes-war
show-religion-causes-crazy-self-sacrifice
show-religion-causes-oppression
show-religion-causes-self-abuse
show-thinkers-persecuted-by-religion
show-halting-rationalist-progress-against-religion
show-thinkers-opposing-religious-thought
show-thinkers-persecuted-by-religion
(Mateas, Vanouse, and Domike 2000, 239)
```

在他们的论文中，Mateas, Vanouse, and Domike 写道，在 Terminal Time 中，“九个主要意识形态家使用总共 222 个修辞目标来表示。” Terminal Time 的作者将这些意识形态模型的制作视为创作，即创作一件艺术品。但这并不总是 AI 社区理解他们工作的方式。正如 Mateas 所报告的：

第一次向技术受众展示 Terminal Time 时，有人提出了几个问题，询问我是否在模拟真正的历史学家的工作方式。隐含的假设是，这种系统的价值在于其对人类行为的真实模型。事实上，Terminal Time 的架构结构是作品概念的一部分，不是作为人类行为的现实肖像，而是作为某些制度化的纪录片制作过程的漫画，（2002, 57–58）

鉴于我之前在 AI 中关于拟人化模型的讨论，Terminal Time 受到这样的接待或许并不意外。为了理解 Terminal Time 及其背后的理念，确实需要考虑人类历史和意识形态模型如何与系统交互。然而，寻找人类模型的地方不在于系统本身。相反，Terminal Time 依赖于这些模型存在于一个非常拟人化的位置：观众之中。

## 事件知识

为了使 Terminal Time 的事件对系统可访问，它们需要以正式化的方式表示。Terminal Time 解决这个问题的方法是建立在一种名为“Upper Cyc Ontology”的日常知识表示之上（这是一项雄心勃勃的、正在进行中的尝试，旨在解决之前在 Minstrel 语境下讨论的根本问题）。为了 Terminal Time 的目的，Cyc Ontology 采取的方法既构建了其自身术语的创作方式（作为知识库中的断言，该知识库还包括 Upper Cyc 的术语，并为其术语定义提供了较低层级的基础）。

Terminal Time 的历史事件涵盖一系列抽象层级。例如，它们包括第一次十字军东征、巴克莱特的发明以及启蒙哲学的兴起。以下是事件如何为 Terminal Time 创作的一个示例。具体来说，这是一个事件的表示，即乔尔丹诺·布鲁诺的故事：

```
:: Giordano Bruno
(Sisa %GiordanoBrunoStory %HistoricalEvent)
(Sisa %GiordanoBrunoStory %IdeaSystemCreationEvent)
(Sisa %GiordanoBrunoStory %Execution)
(%circa %GiordanoBrunoStory (%DateRangeFn
  (%CenturyFn 16) (%CenturyFn 17)))
(SevenOccursAt %GiordanoBrunoStory
  SContinentOfEurope)
(SperformedBy %GiordanoBrunoStory %GiordanoBruno)
(SoutputsCreated %GiordanoBrunoStory
  %GiordanoBrunoIdeas)
(Sisa %GiordanoBrunoIdeas
  SPropositionalInformationThing)
(Sisa %GiordanoBrunoIdeas SSomethingExisting)
(%conflictingMOs %GiordanoBrunoIdeas
  %MedievalChristianity)
(Sisa %GiordanoBrunoIdeas %IdeaSystem)
(SperformedByPart %GiordanoBrunoStory
  %TheRomanCatholicReligiousOrg)
(SubjectActedOn %GiordanoBrunoStory
%GiordanoBruno)
(Mateas, Vanouse, and Domike 2000, 238)
```

在上述表示中，以 "%" 开头的术语在 Upper Cyc Ontology 中定义，而未以 "%" 开头的术语则在 Terminal Time 本体论中以 Upper Cyc Ontology 的术语定义。该事件表示的英文释义如下：

乔尔丹诺·布鲁诺的故事是一个发生在 16 和 17 世纪的历史事件，涉及创建一个新的思想系统和一次处决。在此事件中创建的思想系统与中世纪基督教的思想系统相冲突。乔尔丹诺·布鲁诺和罗马天主教会的一部分都是此事件的执行者。乔尔丹诺·布鲁诺在此事件中被施加作用（他被处决）。（同上）

为了让 Terminal Time 的意识形态家利用此类事件，必须能够确定该事件可以被旋转以支持当前的修辞目标之一。Terminal Time 系统通过测试事件的适用性来识别候选事件。这些测试通过一个用 Lisp 编写的“推理引擎”来执行。以下是“show-thinkers-persecuted-by-religion”的测试：

```
(%and
  (Sisa ?event %IdeaSystemCreationEvent)
  (Sisa ?event %Execution)
  (OutputsCreated ?event ?newIdeas)
  (%conflictingMOs ?newIdeas ?relBeliefSystem)
  (Sisa ?relBeliefSystem $Religion))
(ibid., 239)
```

正如 Mateas, Vanouse, and Domike 所指出的，这并非寻找所有宗教迫害思想家实例的一般测试。例如，它假设处决是唯一的迫害类型。同样，Terminal Time 对乔尔丹诺·布鲁诺故事的表示也不是唯一可能的表示。Terminal Time 的作者指出，在其他情况下，可能希望将布鲁诺的著作和处决表示为独立事件，而不是一个复合事件。

但再次强调，Terminal Time 并不试图创建历史学家行为的现实模拟，或创建一个“真正理解”历史的系统，或本身成为一个创造性系统。相反，它是一件创作的艺术品。

如果作者希望——在某个时刻——系统能够识别宗教团体迫害思想家但不涉及处决的实例，以便在其故事中使用这些事件，那么测试可以扩展以匹配新的事件类别。截至 2000 年，作者报告称系统包括“134 个历史事件和 1568 个知识库断言”（不包括 Upper Cyc Ontology 中的那些断言）。鉴于所有可能涉及宗教迫害思想家的事件示例（在 134 个中）也都包含处决，因此不需要更广泛的测试。但任何参与为 Terminal Time 创作历史事件数据的人都必须意识到以后将评估它们的测试。事实上，除非与 Terminal Time 系统中当前的测试相关联，否则创作历史事件毫无意义，因为不匹配任何测试的事件永远不会在故事中被使用。因此，事件的创作与测试的创作紧密耦合。

