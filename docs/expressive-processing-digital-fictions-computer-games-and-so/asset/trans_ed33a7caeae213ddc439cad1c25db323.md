

新关键字与目前已找到的最高级关键字进行比较。如果新单词的级别更高，它会被添加到栈顶；否则，它会被添加到栈底。在扫描文本中的关键字结束时，最高级关键字位于栈顶。

关键字扫描完成后，下一步是找到一个与听众输入内容的替换后版本（除去因逗号或句号而丢弃的部分）相匹配的“分解规则”。分解规则与关键字相关联，因此此搜索从弹出栈顶关键字开始。（我很快将讨论如果栈中没有内容时会发生什么。）Eliza 会尝试与该关键字关联的分解规则，寻找一个与通配符“0”（相当于“任意数量的单词，包括零个单词”）相结合的适当单词模式。例如，如果关键字是“you”，则第一个分解规则是：(0 | remind you of 0)

这不会匹配上面的示例短语“I are very helpful”。第一条规则只会匹配类似“With that last statement I remind you that I are a machine”的替换后短语，或者（因为 0 可以表示零个单词），“I remind you of the happier days of your childhood”。然而，针对“you”关键字的下一条分解规则会匹配前面使用的示例短语：(0 | are 0)

一旦找到匹配项，分解规则就会做其名称所指的事：它将短语分解为各个部分。这种分解基于规则中的单词数量和 0 的数量。例如，“I are very

6. 问号未被使用，因为在 Weizenbaum 使用的计算机系统上，它们被解释为“行删除”。

helpful”将变为：(1) 空 (2) | (3) are (4) is very helpful.

此时，剩下的就是决定要对听众说什么。每个分解规则可以有一组与之关联的重组规则。一个重组规则示例（针对分解“0 I am 0”）是：(What makes you think I am 4)

这将产生回复：“What makes you think I am very helpful.” 一旦在 Eliza 的任何运行中使用过，重组规则就会被标记，以便在重复任何规则之前，先循环使用与特定分解关联的所有重组规则。

这是 Eliza 方法的主要部分。还有一些改进，例如允许脚本在关键字之间共享规则的技术（例如，mother 和 father）。但由此，Eliza 中起作用的主导操作逻辑应该很清楚：转换。Eliza 的每句话都是对听众最近陈述的多步转换的结果。

这些转换中的许多都包含被转换陈述的逐字部分，如上所述。其他则是更间接的转换，例如将“Perhaps I could learn to get along with my mother”翻译为“Tell me more about your family.” 然而，真正的翻译困难在于，当听众最近的文本中找不到任何关键字——这是 Eliza 转换逻辑的核心方面——时。例如，当 Eliza/Doctor 问“What else comes to mind when you think of your father”，并收到回复“Bullies”时，就是这种情况。

在这种情况下，一组可能的转换可以基于名为“none”的特殊关键字在脚本中定义。在 Doctor 中，这些是诸如“Please go on”和“I see”之类的无内容短语。然而，与 Eliza 的一些最令人惊讶的时刻来自另一个名为“memory”的特殊结构。该结构与特定关键字结合使用。在 Doctor 的例子中，它与关键字“my”和分解“0 your 0”一起使用。选择此关键字时，会以通常方式生成回复。此外，还可以创建另一个重组并存储在队列中，以便在未找到关键字时稍后使用。在 Doctor 中，这些重组是“Lets discuss further why your 3”、“Earlier you said your 3”和“Does this have anything to do with the fact that your 3”——我们在上面看到了最后一个，其中 3 是“boyfriend made you come here”。换句话说，上面对话中的惊人笑点只不过是一种后备方案，是 Eliza 在最近的回复没有可识别关键字时可以采取的默认操作。

这里我们可以看到是什么促使 Weizenbaum 写道：“一旦某个特定程序被揭开面纱，一旦其内部工作原理用足够通俗的语言解释以引发理解，其魔力就会瓦解；它被揭示为仅仅是一组过程，每个过程都相当容易理解”（1966, 36）。但是，当我们与一段软件交互时，我们不一定能获得这种理解，我们无法清楚地了解它内部实际是如何运作的。就 Eliza/Doctor 而言，萨根博士和我并非孤例：其听众常常对其内部工作原理产生错误的想法。他们假设，既然与程序交互的表面外观可能类似于连贯的对话，那么内部软件必定复杂。有些人认为它一定是

7. 这是珍妮特·默里在 *全息甲板上的哈姆雷特* 中报道的故事版本。
除了这个版本，还有许多明显是伪造的版本流传，包括一个 Weizenbaum 是事件参与者的版本。这个版本本身不可能是……
注释继续在本章末尾。

某种接近虚构的 HAL 的东西：一种足够智能以理解和产生任意人类语言的计算机程序。这种情况发生得如此频繁，并且如此引人注目，以至于在计算机科学圈子里，人们开始为这种误解使用一个特定术语，即本章前面提到的：Eliza 效应。

## 为什么 Eliza 有效

关于 *Eliza/Doctor* 有效性的故事有很多。Weizenbaum 自己告诉我们：“我的秘书，她看着我在这个程序上工作了很多个月，因此肯定知道它仅仅是一个计算机程序，开始与它交谈。仅与它交换了几句话之后，她就让我离开房间”（1976, 6）。还有一个反复讲述的故事，有许多版本，关于老板以为自己在与下属沟通，但实际上却在与 *Eliza/Doctor* 交谈：

副总裁：Do you think I can use the computer this morning?
Teletype: WHY DO YOU ASK?
副总裁：I might be able to make some additional telecomp (computer system) sales.
Teletype: WHY AREN'T YOU SURE?
副总裁：My prospective customers have never seen a demonstration of the system.
Teletype: DOES THIS MEAN VERY MUCH TO YOU?
副总裁：Of course it does.
Teletype: YOU SEEM VERY POSITIVE ABOUT THAT.
副总裁：This is ridiculous.
Teletype: WHAT DO YOU MEAN THIS IS RIDICULOUS?
(Murray 1997, 7).

作为一名高中生，我发现 *Eliza/Doctor* 之所以能创造出有效的初始幻觉，与上述故事中那位标志性的“情感化”秘书和“糊涂”老板产生作用的原因相同。首先，我们都习惯于纯文本计算，以及在那个环境中与他人交谈。其次，Eliza/Doctor 在进程和数据之间实现了非常好的匹配。初次拜访治疗师的情境、重组和无回应中的巧妙编写，以及精心挑选的关键字，都尽可能地利用了 Eliza 转换过程提供的简单语言技巧。（事实上，除了 Doctor 之外还创建了其他 Eliza 脚本，但没有哪个脚本变得像它那样广为人知或普及。）第三，就我自己、秘书和老板而言，这是我们第一次接触计算机角色。但所有这三个原因都只是 Eliza/Doctor 对一个更普遍现象的具体细微差别：当一个系统被呈现为智能，并似乎表现出智能行为时，人们有着令人不安的强烈倾向将其视为智能。⁸

8. 马克·J·纳尔逊在本书的基于博客的同行评审中，敦促我澄清这一点不仅适用于计算机系统——正如本章后面将展示的一个例子：哈罗德·加芬克尔的是/否治疗实验。

这一现象挫败了 Weizenbaum 的职业生涯。他开始将工作重点放在导致 Eliza 效应名称的概念错位上，具体是探讨它如何“在相当正常的人身上引发强大的妄想性思维”（1976, 7）。Weizenbaum 写了一本书，致力于证明计算机的内部并非神奇，当我们假设人类如此机械化以至于我们的智能可以或应该被计算机匹配时，我们是在自讨苦吃。从某种意义上说，他从一名计算机科学家转变为最早审视计算机文化的知识分子批评家之一。

