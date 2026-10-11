
- Birrwistle, G., O-J. Dahl, B. Myhrhaug, and K. Nygaard. *SIMULA Begin*. Student-litteratur (Lund, Sweden), 1979. ISBN 9144062125.

- Holmevik, J. R. “Compiling SIMULA: A Historical Study of ‘Technological Genesis’” *IEEE Annals of the History of Computing*, Vol. 16 No. 4, 1994, pp. 25–37.

- Krogdahl, S. “The Birth of Simula.” Proceedings of the HiNC 1 Conference in Trondheim, June 2003 (IFIP WG 9.7, in cooperation with IFIP TC 3).

- Nygaard, Kristen, and Ole-Johan Dahl. “The Development of the SIMULA Languages.” *ACM SIGPLAN Notices*, Vol. 13 No. 8, 1978. Special Issue: History of Programming Languages Conference.

- SIMULA Standard. *DATA Processing – Programming Languages – SIMULA*. Swedish Standard, Stockholm, Sweden (1987). ISBN 9171622349.

### 22.2.5 C

1970 年，人们“众所周知”地认为，严肃的系统编程——特别是操作系统的实现——必须用汇编代码完成，且无法可移植地实现。这与 Fortran 出现之前科学编程的情况类似。几个个人和团体开始挑战这一正统观念。从长远来看，C 编程语言（第 27 章）是这些努力中成功得最多的。

Dennis Ritchie 在新泽西州默里山（Murray Hill）贝尔电话实验室计算机科学研究中心设计并实现了 C 编程语言。C 语言的美妙之处在于它是一门刻意保持简单的编程语言，非常贴近硬件的基本方面。目前大多数复杂性（其中大部分因兼容性原因在 C++ 中重新出现）是在其原始设计之后添加的，并且在某些情况下是在 Dennis Ritchie 反对的情况下添加的。C 的成功部分归功于其早期的广泛可用性，但其真正的优势在于语言特性到硬件设施（参见 §25.4–5）的直接映射。Dennis Ritchie 简洁地将 C 描述为“强类型但弱检查的语言”；也就是说，C 具有静态（编译时）类型系统，使用对象的方式与其定义不同的程序是不合法的。然而，C 编译器无法检查这一点。当 C 编译器需要在 48K 字节内存中运行时，这是有道理的。C 开始被使用后不久，人们开发了一个名为 lint 的程序，独立于编译器验证对类型系统的合规性。

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_868_0.png)

与 Ken Thompson 一起，Dennis Ritchie 是 Unix 的联合创始人，Unix 无疑是历史上具有影响力的操作系统。C 曾经——并且现在——与 Unix 操作系统相关联，并通过 Unix 与 Linux 和开源运动相关联。

在长达 40 年的时间里，Dennis Ritchie 在贝尔实验室计算机科学研究中心工作。他是哈佛大学的毕业生（物理学专业）；他来自哈佛大学的博士（应用数学）学位从未被授予，因为他要么忘记了，要么拒绝支付一小笔（60 美元）注册费。

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_869_0.png)

在早期阶段（1974–79 年），贝尔实验室的许多人都影响了 C 语言的设计及其推广。Doug McIlroy 是每个人最喜欢的批评者、讨论伙伴和创意大师。他对 C、C++、Unix 以及更多领域都产生了影响。

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_869_1.png)

Brian Kernighan 是一位杰出的程序员和作家。他的代码和文字都是清晰简洁的典范。本书的风格部分源自其代表作 *《C 程序设计语言》*（以其合著者 Brian Kernighan 和 Dennis Ritchie 的姓氏首字母缩写 “K&R” 而闻名）中的教程章节。

仅有好的想法是不够的；要在大规模上发挥作用，这些想法必须简化为最简形式，并以目标受众中大量人员易于理解的方式清晰地表达出来。冗长是此类思想展示中最糟糕的敌人之一；晦涩难懂和过度抽象也是如此。纯粹主义者通常对这种普及化结果嗤之以鼻，更喜欢以只有专家才能理解的方式呈现的“原始结果”。我们并不如此：让一个新手理解一个不平凡但有价值的想法是困难的，这对专业能力的提升至关重要，并对整个社会有价值。

多年来，Brian Kernighan 参与了许多具有影响力的编程和出版项目。两个例子是 *AWK*——一种早期脚本语言，以其作者 Aho、Weinberger 和 Kernighan 的姓氏首字母命名——以及 *AMPL*（“一种数学规划语言”）。

Brian Kernighan 目前是普林斯顿大学的教授；当然，他也是一位优秀的教师，擅长将原本复杂的主题讲得清晰明了。在超过 30 年的时间里，他在贝尔实验室计算机科学研究中心工作。贝尔实验室后来变成了 AT&T 贝尔实验室，再后来分裂为 AT&T 实验室和 Lucent 贝尔实验室。他是多伦多大学的毕业生（物理学专业）；他的博士是普林斯顿大学电气工程专业的。

C 语言的家谱看起来像这样：

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_870_0.png)

C 语言的起源在于英国从未完成的 CPL 项目、Martin Richards 在从剑桥大学休假期间访问 MIT 时开发的 BCPL（Basic CPL）语言，以及 Ken Thompson 开发的一种称为 *B* 的解释型语言。后来，C 语言由 *ANSI* 和 *ISO* 标准化，并且受到了 C++ 的许多影响（例如函数参数检查和 const 常量）。

CPL 是剑桥大学和伦敦帝国理工学院之间的一个合作项目。最初，该项目在剑桥进行，因此“C”官方代表“Cambridge”。当帝国理工学院成为合作伙伴时，“C”的官方解释变成了“Combined”。实际上（或者我们被告知如此），它始终代表“Christopher”，以 CPL 的主要设计者 Christopher Strachey 命名。

# 参考文献

- Brian Kernighan 的个人主页：http://cm.bell-labs.com/cm/cs/who/bwk 和 www.cs.princeton.edu/–bwk/。

- Dennis Ritchie 的个人主页：http://cm.bell-labs.com/cm/cs/who/dmr。

- ISO/IEC 9899:1999. 编程语言 – C。（C 语言标准。）

- Kernighan, Brian，和 Dennis Ritchie。 *《C 程序设计语言》*。Prentice Hall, 1978。第二版，1988。ISBN 0131103628。

- 贝尔实验室计算机科学研究中心成员列表：http://cm.bell-labs.com/cs/alumni.html。

- Richards, Martin。 *《BCPL – 语言及其编译器》*。剑桥大学出版社，1980。ISBN 0521219655。

- Ritchie, Dennis。“C 编程语言的发展。” *《ACM 编程语言历史会议论文（HOPL-2）》*。 *《ACM SIGPLAN 通告》*，第 28 卷第 3 期，1993 年。

- Salus, Peter。 *《UNIX 的二十五年》*。Addison-Wesley, 1994。ISBN 0201547775。

### 22.2.6 C++

C++ 是一种通用编程语言，偏向于系统编程，它：

- 是更好的 C

- 支持数据抽象

- 支持面向对象编程

- 支持泛型编程

它最初由 Bjarne Stroustrup 在新泽西州默里希尔的贝尔电话实验室计算机科学研究中心设计和实现，也就是说，就在 Dennis Ritchie、Brian Kernighan、Ken Thompson、Doug McIlroy 和其他 Unix 大师的走廊对面。

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_872_0.png)

Bjarne Stroustrup 在家乡丹麦奥胡斯的大学获得了硕士学位（主修数学，辅修计算机科学）。然后他去了剑桥，在那里为 David Wheeler 工作并获得了博士学位（计算机科学）。C++ 的主要贡献在于：

- 让抽象技术对主流项目变得可负担且易于管理

- 在效率至关重要的应用领域率先使用面向对象和泛型编程技术

在 C++ 出现之前，这些技术（通常被粗糙地归类为“面向对象编程”标签之下）在行业中大多默默无闻。正如 Fortran 出现前的科学编程和 C 出现前的系统编程一样，这些技术在现实世界中被认为太昂贵而不被使用，对“普通程序员”来说也过于复杂而无法掌握的观点是“众所周知”的。

C++ 的工作始于 1979 年，并于 1985 年导致商业发布。在最初的设计和实现之后，Bjarne Stroustrup 与贝尔实验室及其他地方的朋友一起进一步开发，直到 1990 年正式启动标准化。自那以后，C++ 的定义先由 ANSI（美国国家标准机构）开发，自 1991 年起由 ISO（国际标准化组织）开发。Bjarne Stroustrup 作为负责新语言功能的小组主席，在该工作中发挥了主要作用。第一个国际标准（C++98）于 1998 年通过，第二个标准于 2011 年通过（C++11）。下一个 ISO 标准将是 C++14，再下一个有时被称为 C++1y，可能会成为 C++17。

在 C++ 最初十年的发展之后，最显著的发展是 STL——标准库中用于容器和算法的设施。这是数十年来工作的成果——主要由 Alexander Stepanov 完成——旨在受数学之美和实用性的启发，产生最通用和高效的软件。

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_873_0.png)

Alex Stepanov 是 STL 的发明者和泛型编程的先驱。他是莫斯科大学的毕业生，曾使用多种语言（包括 Ada、Scheme 和 C++）从事机器人、算法和其他领域的工作。自 1979 年以来，他一直在美国学术界和工业界工作，特别是在 GE Labs、AT&T 贝尔实验室、惠普、Silicon Graphics 和 Adobe。

C++ 的家谱看起来像这样：

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_873_1.png)

“C with Classes”是 Bjarne Stroustrup 对 C 和 Simula 想法的初步综合。随着其继任者 C++ 的实现，它立即消亡了。

语言讨论往往聚焦于优雅和高级功能。然而，C 和 C++ 并没有以这种方式成为计算历史上最成功的两种语言。它们的优势在于灵活性、性能和稳定性。主要软件系统存活数十年，通常耗尽其硬件资源，并经常遭受完全意想不到的需求变化。C 和 C++ 能够在这种环境中蓬勃发展。我们最喜欢的 Dennis Ritchie 语录是：“有些语言是为证明一个观点而设计的；其他语言是为解决一个问题而设计的。” 通过“其他”，他主要指的是 C。Bjarne Stroustrup 喜欢说：“甚至我也知道如何设计一种比 C++ 更漂亮的语言。” C++ 的目标——就像 C 一样——不是抽象的美（尽管当我们能享受到时我们强烈欣赏它），而是实用性。

# 参考文献

- Alexander Stepanov 的出版物：www.stepenovpapers.com。

- Bjarne Stroustrup 的个人主页：www.stroustrup.com。

- ISO/TEC 14882:2011。 *《编程语言 – C++》*。（C++ 标准。）

- Stroustrup, Bjarne。“C++ 的历史：1979–1991。” *《ACM 编程语言历史会议论文（HOPL-2）》*。 *《ACM SIGPLAN 通告》*，第 28 卷第 3 期，1993 年。

- Stroustrup, Bjarne。 *《C++ 的设计与演化》*。Addison-Wesley, 1994。ISBN 0201543303。

- Stroustrup, Bjarne。 *《C++ 编程语言，第四版》*。Addison-Wesley, 2013。ISBN 978-0321563842。

- Stroustrup, Bjarne。 *《C++ 之旅》*。Addison-Wesley, 2013。ISBN 978-0321958310。

- Stroustrup, Bjarne。“C 和 C++：兄弟姐妹”；“C 和 C++：兼容性的案例”；以及“C 和 C++：兼容性案例研究。” *《C/C++ 用户期刊》*，2002 年 7 月、8 月和 9 月。

- Stroustrup, Bjarne。“在现实世界中演化一门语言：C++ 1991–2006。” *《第三届 ACM SIGPLAN 编程语言历史会议（HOPL-III）论文》*。加州圣迭戈，2007 年。http://portal.acm.org/toc.cfm?tid=1238844。

### 22.2.7 当下

当前使用哪些编程语言以及用于什么用途？这是一个真正难以回答的问题。当前语言的家谱是——即使以最简化的形式——有点拥挤和混乱：

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_875_0.png)

事实上，我们在网页上（以及其他地方）发现的大多数统计数据，其准确性几乎不比谣言好多少，因为它们测量的是与使用情况仅有弱相关性的指标，例如包含某编程语言名称的网络帖子数量、编译器出货量、学术论文、图书销量等。所有这些指标都偏向新事物而非既有标准。那么，什么是程序员？是每天使用编程语言的人吗？只是为了学习而编写小程序的算什么？只是谈论编程的教授算什么？几乎每年写一次程序的物理学家算什么？一个职业程序员——按定义几乎总是——每周使用多种编程语言，是算很多次还是只算一次？我们看过这些统计以各种方式回答过上述每一个问题。

然而，我们觉得有义务给你们一个观点，因此在2014年，全世界大约有1000万职业程序员。对于这个观点，我们依赖于IDC（一家数据收集公司）、与出版商和编译器供应商的讨论，以及各种网络来源。尽管大家可以随意质疑，但我们知道在任何尚算合理的程序员定义下，这个数字大于100万且小于1亿。他们使用哪种语言？Ada、C、C++、C#、COBOL、Fortran、Java、PERL、PHP、Python 和 Visual Basic 可能（仅仅是可能）占据了所有程序的90%以上。

除了这里提到的语言，我们还可以列出几十种甚至上百种。除了试图对有趣或重要的语言保持公平外，我们看不到继续列举的意义。请自行查找所需信息。专业人士熟悉多种语言，并会根据需要学习新语言。对于所有人和所有应用来说，并没有“唯一的正确语言”。事实上，我们能想到的所有主要系统都使用多于一种语言。

### 22.2.8 信息来源

上述每种语言的描述都有一个参考列表。以下是涵盖多种语言的参考资料：

*更多语言设计师的链接/照片*

www.angelfire.com/tx4/cus/people/.

*一些语言示例*

http://dmoz.org/Computers/Programming/Languages/.

*教材*

- Scott, Michael L. *Programming Language Pragmatics*. Morgan Kaufmann, 2000. ISBN 1558604421.

- Sebesta, Robert W. *Concepts of Programming Languages*. Addison-Wesley, 2003. ISBN 0321193628.

*历史书籍*

- Bergin, T.J., and R. G. Gibson, eds. *History of Programming Languages – II*. Addison-Wesley, 1996. ISBN 0201895021.

- Hailpern, Brent, and Barbara G. Ryder, eds. *Proceedings of the Third ACM SIGPLAN Conference on the History of Programming Languages (Hopl-III)*. San Diego, CA, 2007. http://portal.acm.org/toc.cfm?id=1238844.

- Lohr, Steve. *Go To: The Story of the Math Majors, Bridge Players, Engineers, Chess Wizards, Maverick Scientists and Iconoclasts–The Programmers Who Created the Software Revolution*. Basic Books, 2002. ISBN 978-0465042265.

- Sammet, Jean. *Programming Languages: History and Fundamentals*. Prentice Hall, 1969. ISBN 0137299885.

- Wexelblat, Richard L., ed. *History of Programming Languages*. Academic Press, 1981. ISBN 0127450408.

## 复习题

1. 历史有哪些用途？

2. 编程语言有哪些用途？请举例。

3. 列出一些编程语言客观上具有良好特性的基本属性。

4. 抽象意味着什么？更高层次的抽象又意味着什么？

5. 我们对代码的四个高层次理想是什么？
