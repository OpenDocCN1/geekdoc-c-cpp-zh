# 并行编程语言比较研究：萨利申问题（超级计算专题专题，第 6 卷）










# 第 6 

丛主编辑：

- G. RODRIGUE
加州大学戴维斯分校
劳伦斯利弗摩尔国家实验室
美国加利福州利弗摩尔

- G. MICHAEL
劳伦斯利弗摩尔国家实验室
美国加利福州利弗摩尔



计算机研究小组
劳伦斯利弗摩尔国家实验室
美国加利福州利弗摩尔












# 丛书介绍

大规模计算是一个日益增长的研究领域，它对科学、工程和现代工业技术的进步起着至关重要的作用。计算正迅速成为探索新问题最频繁使用的技术。在过去的几年里，计算机建模的引入产生了十年前无法想象的成果。它们是许多领域中不可或缺的工具；从气候研究到化学动力学，从自动化制造到密集重症监护室的运行。科学过程的计算机仿真在许多情况下可以替代实际实验。这些仿真成本更低，并且能够解决更广泛的问题。计算机仿真还提供了从实验无法获得的物理问题的理解。

许多类型的研究问题现在正日益依赖计算机模型，数值实验正逐渐与更传统的研究方法并存。除了理论和实验之外，科学现在还有了一个计算维度。

研究复杂性的增加导致了对更大、更快的计算机的需求；即超级计算机。在这一过程中，超级计算机本身刺激了计算方法的重新开发。一个领域的结果被快速应用于另一个领域。其结果使超级计算变成了一场多学科的冒险。在所有大学、实验室和工业领域，都能找到来自不同兴趣和背景的超级计算科学家。

在超级计算中，工程与物理科学的学术领域与数学、计算机科学和计算机工程的学术领域之间存在大量交叉。这些领域中使用的科学术语各不相同，在超级计算科学取得进展之前，需要对其进行翻译或理解。

尽管许多进步在很多情况下让过去变得更容易，但它并没有跟上过去十年对计算机需求的剧增，以及计算机硬件日益增长的复杂度。

《超级计算特别专题》（Special Topics in Supercomputing将将两个方向开展。首先，考虑到超级计算研究不断开启新方向，该丛书的一部分将致力于刚刚开始固化为明确研究领域的主题。这些卷包含了该领域当前领军者的稿件。

其次，《超级计算特别专题》将作为系列的一部分，包含关于超级计算新领域和成熟领域的专著和论文集。随着超级计算的某些主题开始在坚实的理论基础的基础上固化，它们将由该领域丰富的作者汇编成专著或教科书。另一方面，超级计算的一些领域非常新，尚无法收集足够的稿件来撰写一本完整的书。这些主题将包含在该丛书的论文集中。

这项事业的希望是让超级计算得到更广泛的理解，并在那些由于信息不足而尚未渗透的领域变得更易于获取。

G. Rodriguez

# 前言

随着执行速度达到单 CPU 计算机的物理极限，我们获得更大计算能力的唯一希望就是并行系统。一个研究密集的领域是并行编程语言。研究人员提出了无数新的编程语言、对现有语言的扩展以及编程工具。遗憾的是，这些研究主要局限于学术界，很少来自用户社区的投入。各种方法之间的差异、相似性、优点、缺点以及适当的问题领域是微妙的，且往往被充分理解。鉴于这种混乱，对并行语言进行知情的比较是困难的。

在书中，我们使用了一个语言和计算社区都能理解并欣赏的比较基准。我们根据四个问题的解决方案比较了八种并行编程语言。每一章都包含了该语言哲学、语义和语法的描述，以及对每个问题的解决方案。这些章节由知名专家编写；在某些情况下，作者就是该语言的设计者。我们相信，通过讨论解决方案而不是语言特征或理论属性，我们桥起语言专家与用户之间的鸿沟。

本书适合并行编程语言研究生课程的补充教材。由于本书是从计算的角度研究语言的，因此计算机科学和计算科学的研究生都将受益。

我们邀请其他并行语言的倡者在其他论坛发表他们对“萨利申问题”的解决方案。本书仅包含并行编程语言的一个子集。我们希望看到所有类语言的解决方案，并且每类尽可能多的实例。如果语言存在真实的实现，我们建议作者讨论性能。在大多数应用程序程序员看来，语言的优劣取决于其应用性能。我们还鼓励所有领域的科学家提出尚未包含在计算模型中的新问题。我们希望这套问题将成为比较并行编程语言的标准，就像利弗摩尔循环和 Linpack 被用于评估计算机系统一样。

John Feo







Kenneth W. Dritz 9








本页特意留白


## Salishan 问题

John Feo
计算研究小组，L-306
劳伦斯·利弗摩国家实验室
加州利弗摩尔 94550

## 1. 引言

并行编程语言的比较往往是基于理论标准而非实践标准。传统研究从参数传递、求值顺序、对并发的支持、同步与通信方法，以及对特定数据结构（如数组、列表或树）的操作支持等方面对并行语言进行了比较。通常，这些研究使用假设或琐碎的程序示例来说明语言特性。它们很少讨论不同方法如何影响真实应用程序的开发，留给读者去推断语言特性对他们解决的问题的影响。

我们参加过多少次会议，演讲者在上面乏味地喋了四十分钟，描述另一种并行语言的语法，然后展示阶乘、斐波那契或八皇后问题的代码？讲师让应用程序程序员几乎无法感知该语言的真实优缺点，不知道该语言可以和不能高效地表达哪些类型的并行程序，甚至不知道该语言是否能够表达特定的算法。通过只描述树木而非森林，并且不使用相关的例子，演讲者往往无法说服听众尝试这种新语言。

因此，并行编程语言的发展主要局限于学术界，很少来自用户社区的投入。后者对用于推广这些语言的学术论点感到困惑。他们认为语言设计者更感兴趣的是设计深奥的语言属性，而不是支持大规模应用程序所需的功能。另一方面，应用程序程序员在考虑新想法和新编程风格方面很缓慢。他们不愿尝试新语言，从而错过了影响设计的机会。他们继续使用顺序语言进行编写，并梦想自动并行化编译器能将他们“过时的旧代码”转换，以适应每一类新的并行机器。

意识到语言社区与应用社区之间长期存在的鸿沟，1988 年 Salishan 高速计算会议包含了四个关于并行编程语言的环节。该会议是由劳伦斯·利弗摩尔国家实验室和洛斯阿拉莫斯国家实验室赞助的年度会议。在俄勒冈州格伦尼德海滩（Glenened Beach）的 Salishan Lodge 。会议为高速超级计算机的架构师和用户提供了交流和影响彼此工作的平台。参与者包括来自学术界、工业界国家实验室的计算机和物理科学家。

为了避免“典型的”编程语言演讲，程序委员会采用了一种受控格式 [3]。它定义了四个非平凡问题（*Salishan 问题*），并邀请了五位演讲者用不同的并行语言提出这些问题的解决方案。委员会将这些问题的解决方案作为比较的基础。这些问题涵盖了各种编程模型和数据结构，包括：动态任务、同步任务、异步任务、嵌套循环并行、数组、流和递归树结构。

## Salishan 问题

每位演讲者有十五分钟的时间来描述他们的语言以及他们对每个问题的解决方案。演讲者被指示要讨论哲学而非语法。他们被告知要联系好与坏、易与难、该语言很好地表达哪些类型的应用，以及哪些类型表达得较差。由于某些语言缺乏真实的实现，性能不是一个问题。考虑到 Salishan 听众“直言不讳”的特点，很少有演讲者能完全全其责。总来说，这些环节在日落落套房的晚间招待会上引发了大量的讨论。

这本书是成功的结果。它包含了八章，每章都描述一种不同的并行编程语言及其对 Salishan 问题的解决方案。这些语言是：Ada、C*、Haskell、Id、Occam、Program Composition、Scheme 和 Sisal。

Ada 由国防部开发是一种是一种命令式编程语言，旨在支持现代软件工程技术。C* 和 Occam 是并行体系的语言抽象。前者支持数据并行、SIMD 计算，而后者支持通信顺序进程（CSP）。Haskell、Id 和 Sisal 是函数式语言。基于数学原理，它们隐藏了并行处理的细节（并发、通信和同步）。Sisal 是 Lisp 的派生语言，同时包含了函数式和命令式结构。在某些大学，它是教给学生的第一种编程语言。PCN 是一种用于组合一组基础语言编写的程序的表示法。它提供了一个从规范到目标机器高效源代码的开发问题的框架。

解决方案，而非语言的特性，构成了比较的基础。我们鼓励读者仔细研究每个解决方案。同时理解代码和设计过程是至关重要的。在下一节中，我们将给出给作者的说明。

我们要求所有演示 Salishan 问题解决方案的作者遵循这些说明。在第 3、4、5 和 6 节中，我们定义了四个 Salishan 问题。

# 2 给作者的说明

你应该从讨论开发你语言的原因开始，讨论它可以和不能表达的计算类型和并行形式，以及从程序员的角度来看它的优缺点。你应该提供足够的内容，让不熟悉你语言的熟练读者也能理解你的解决方案。然后，你应该为每个问题给出一个解决方案并对该解决方案进行批判性分析。

你可以自由选择任何你算法，但警告你，低效的算法会让语言看起来很糟糕。读者会推断该语言无法表达更高效的算法，或者该语言的特性自然导致了低效的解决方案。务必讨论问题的哪些方面容易表达，哪些困难。再次，使用你语言的“最佳”算法。

你应该编写完整的解决方案；不要将非标准操作隐藏在库函数中。例如，如果你的语言没有流，但你想在解决方案中使用流，请给出你的语言中定义流的语句以及你使用的流操作的代码。设计每个问题的例程，就像在为库设计一样。不要包含输入输出。

最后一点：你必须同时展示好与坏。没有完美的编程语言，也没有完美的解决方案。所有语言都有缺陷，并且对解决方案空间实施了限制。**我们坚持你讨论这些问题。**





## 3. 海明问题（扩展）

给定一个未知大小的质数集合 (a, b, c, . . .) 和一个整数 $n$，按递增顺序且不重复地输出所有形式如下的整数

```
$a^d \cdot b^l \cdot c^k \cdot \dots \leq n$
```

观察到，如果 $r$ 在输出流中，那么

```
$a \cdot r, b \cdot r, c \cdot r, \dots \leq n$
```

等待，原文是：
```也在输出流中。

该问题测试了语言表达递归流计算和生产者/消费者并行的能力，以及支持动态任务创建的能力。

## 4. 石烷问题

给定一个整数 $n$，输出所有 $i \leq n$ 的石烷分子的化学结构，要求不重复并按大小递增顺序输出。包含所有异构体，但不包含重复。石烷分子的分子式为 $C_iH_{2i+2}$。你可以为选择的分子选择任何表示方法，只要它们能清晰地区分异构体即可。

该问题在 [4] 中被讨论过，但解决方案效率低下。基于自由树和定向树理论 [2] 存在更高效的算法。该问题涉及递归树结构的表示、这些结构的创建与处理、嵌套循环并行，以及如果使用 Turner 的解决方案，还涉及模式匹配和集合操作。

## 5. 诊所

给定一组患者、一组医生和一名接待员，模拟以下交互：初始状态下所有患者都是健康的，所有医生都在一个 FIFO（先进先出）队列中等待病患。在随机时间，患者会生病并进入一个 FIFO 队列等待其中一位医生的治疗。接待员处理这两个队列，按照先进先出的方式将患者分配给医生。一旦医生和患者配对，医生就会诊断疾病并在随机时间内治愈患者。随后，患者被释放，并重新回到医生队列等待另一位患者。该问题的输出未明确规定。该问题改编自 [3]。

这既不是事件驱动的也不是时间驱动的仿真。没有全局知识，对将发生的事件没有预知，没有全局时钟，也没有全局通信。你可以使用任何想要的方法来决定患者何时生病以及患者看诊多久。患者、医生和接待员之间的互动应当符合实际情况。我们的目的是测试每种语言编写一组具有循环依赖的并发异步进程的能力。

## 6. 天线矩阵求解器

求解线性方程组

```
Ax = b
```

不使用主元法，其中 $A$ 是一个 $n \times n$ 的天线矩阵。天线矩阵在第 $i$ 行到 $l$ 行（$1 \le k \le i$）非零，在第 $j$ 列的第 $k$ 行到 $j$ 行（$1 \le k \le j$）非零，$k$ 的值存储在两个向量中：$row$ 和 $column$。例如，如果

## 萨利申问题

| 1 | 0 | 0 | 1 | 0 | 0 |
| 0 | 1 | 0 | 1 | 0 | 0 |
| 0 | 1 | 1 | 1 | 1 | 0 |
| 0 | 0 | 0 | 1 | 1 | 0 |
| 0 | 1 | 1 | 1 | 1 | 0 |
| 0 | 0 | 0 | 1 | 1 | 0 |
| 0 | 0 | 0 | 0 | 0 | 1 |

$row = [1, 2, 2, 4, 4, 7]$ 且 column = $[1, 2, 3, 1, 3, 7]$。你可以假设你用于 A, b, row 和 column 的任何一种输入形式。

该问题最初在 [1] 中被讨论，并由 Alan Hindmarsh 向我们提出。我们包含这个问题是为了测试每种语言定义包含非本质元素（即零）的数组结构的能力，并在给定这些结构的基础上，高效地支持并行迭代数组计算（即避免涉及零的计算）。

## 致谢

我非常感谢对本书做出贡献的作者。他们的工作非常出色。我特别感谢他们遵循指示并按要求解决了问题。如果他们是警察，他们会解决另一个问题——他们想解决的问题，而不是被要求解决的问题。还要感谢 1988 年萨利申会议程序委员会尝试新事物。语言和应用程序编程社区必须共同努力开发下一代编程语言。他们必须相互交流。

这项工作由美国能源部能源研究办公室的应用数学计划部分支持，合同编号 W-7405-Eng-48，用于劳伦斯·利弗莫尔国家实验室。

## 免责声明

本报告是作为美国政府资助的工作报告编制的。美国或美国能源部或其任何员工、承包商、分包商或员工均不对所披露的任何信息、设备或过程的准确性、完整性或可用性做出任何明示或暗示保证，不承担任何法律责任或义务，也不代表其使用不会侵犯私人权利。

对公司或产品名称的引用并不意味着加州大学或美国能源部对产品的认可或推荐，也不排除其他可能合适的产品。

本报告包含的观点、意见和/或发现是作者的，除非另有文件指定，否则不应被视为陆军的官方立场、政策或决策。

## 参考文献

- 1. Eisenstat, S. C. and A. H. Sherman. Subroutines for envelope solution of sparse linear systems. Research Report 35, Yale University, New Haven, CT, October 1974.
- 2. Knuth, D. The Art of Computer Programming, Vol. 1: Fundamental Algorithms. Addison-Wesley, Reading, MA, 1973.
- 3. McShea, M. K. Evaluation of Parallel Programming Languages. M.A. thesis, Department of Computer Science, The University of Texas at Austin, 1986.
- 4. Turner, D. The semantic elegance of applicative languages. In Proceedings of the Conference on Functional Languages and Computer Architecture, Portsmouth, NH, October 1981, 85–92.





# Ada

Ada 程序是严格串行的，除非显式使用任务（tasking）来表示并发性。（然而，Ada 9X 可能允许某种程度的隐式并行，例如可以利用向量架构。）如果提供了多处理器或分布式实现的 Ada，那么并发性——只要使用得当——可以提供一些速度加速。然而，并发更重要的作用是作为一种认知工具，类似于递归；在这一作用上，它可以简化某些算法的表达式——特别是对于它非常擅长的非确定性算法。（在不需要顺序的地方通过指定顺序来未能利用非确定性是属于过度规范；这可能导致效率低下，或者在某些情况下导致不完备。）在硬件允许的情况下，实现速度加速的目标应该是次要的；事实上，编写并发的 Ada 程序时，可以在不考虑其最终运行的硬件的情况下进行编写，因为它们实际上（在没有速度加速的情况下）运行在单处理器上，在那里，Ada 的实现通过在各个 Ada 任务之间进行交替执行或时间分片，来实现并发的幻觉。

Ada 中的任务汇会（rendezvous）模型比监视器（monitors）[6] 的层次更高，一些研究人员青睐监视器，是因为它们可以使用轻量级硬件锁高效地实现。当然，汇会机制的实现通常在内部使用锁和锁定操作，而这对应用程序程序员来说是不可见的。在 Ada 程序中实现监视器范式（因其逻辑属性而受到欢迎）可以通过汇会机制轻松实现。遗憾的是，由于 Ada 任务完整语义的丰富，汇会机制的实现不足以让用 Ada 编写的监视器与其它语言中直接通过锁和锁定操作手工构建的监视器竞争，或与其它语言中提供的原生操作（不具备 Ada 的所有语义丰富性）相竞争。然而，编译器供应商正日益使他们的编译器足够智能，能够识别何时汇会（不带语言中更昂贵的特性）被用于监视器比喻中，通过实现所谓的“Habermann-Nassi 优化”[5]，它们在那种情况下专门化代码生成，以匹配其它语言中最好的监视器实现。尽管如此，预计 Ada 9X 将引入新功能，以提供并发任务对共享数据进行高效的互斥访问。

任务是一种 Ada 的程序单元，类似于过程（procedure），区别在于它有独立的控制线程且不能有形式参数。与其他程序单元一样，任务分为两个独立的部分——规范（specification）和体（body）。任务的规范用于定义任务与其他交互的单元之间的可见接口，而其体表达了它的逻辑行为。任务可以定义为单个对象（单任务）或类型；对于后者，可以创建任意数量的同类型对象，可能作为复合对象（如数组）的组件¹。任务与其他对象一样可以通过进入声明的作用域或评估分配器（Ada 中动态分配的机制）来创建；它们在创建时开始执行。²例如，在医生室问题中，前台接待被建模为单任务；患者被建模为某种适当任务类型的任务数组；而医生则被建模为使用分配器单独创建的另一种任务类型的对象。（使用两种不同技术来管理这些集合的原因在问题解决方案中讨论。）

在不相交的数据集上工作且从不协作的任务是有趣的。更典型的是，任务要么共享全局数据并对它们的引用进行同步（串行化），要么完全拥有自己的数据，并依靠其他任务与其交互时的队列和互斥来对数据的引用进行串行化。在后者的情况下，值通常在交互的任务之间传输。交互的同步和通信方面在汇会机制中体现。

一旦创建，任务就会与程序的其余部分并行执行，直到它们终止或到达某种同步点——例如，由与另一个任务的汇会决定的点。

在最简单的汇会类型中，“调用任务”对“被调用任务”的入口（entry）进行入口调用。（任务的入口在它的规范中声明。）入口调用的语法与过程调用相似，但所涉及的名称是一个扩展名称（例如 `t.e`），它结合了被调用任务的名字 (t) 和其内部任何入口 (e) 的名称。像过程调用一样，入口调用可以可选包含实际参数，因此它可以向被调用任务传递值并从其那里接收值。

被调用任务在简单汇会中的作用由接受 语句（accept statement）表示，这是一个可执行语句，其语法如图 1 所示³

```
accept <entry-name> [[<formal-parameter-list>]] [do
<statement-list>]
```

图 1 - accept 语句的语法

如果 accept 语句具有形式参数，其作用域延伸到语句的末尾（即图 1 中的分号）。汇会的语义如下：两个执行汇会部分的任务中的第一个（即调用任务中的入口调用或被调用任务中的 accept 语句）将变为挂起，直到另一个任务执行其相应部分。在此时，如果存在语句列表，调用任务将挂起（如果它尚未挂起），而被调用任务执行语句列表；当然，语句列表可以读取模式为 `in`、`out` 或 `in out` 的形式参数（其值是从调用任务传输的），并存储到模式 `out` 或 `in out` 的形式参数中。最后，当到达语句列表末尾（或在不存在列表时），两个任务继续并行运行——调用任务执行其入口调用之后的语句，被调用任务执行其 accept 语句之后的语句。在调用方，此前与 `out` 或 `in out` 模式的形式参数关联的实际参数，从现在起拥有它们在汇会期间收到的新值。

如果多个任务调用某个任务的给定入口，调用将按先先出（FIFO）顺序队列，每次对该入口执行 accept 语句都会从队列中移除旧调用。

可以构造条件入口和接受 语句（如果对应项尚未执行，则采取另一种路径）以及超时入口调用和接受 语句（如果对应项在指定时间内未执行，则超时并采取另一种路径），但我们的问题解决方案不需要它们。此外，任务的入口可以聚合入口族（entry families），它们的行为类似于入口数组，并允许计算入口调用或接受 语句中命名的入口的标识（例如通过其下标表达式的值）；问题解决方案也不需要入口族。

最后，可以使任务接受多个备选入口的任何一个调用。为了实现这种效果，被调用任务执行所谓的选择等待（selective wait），其语法在图 2 中（通过骨架示例所示）。当任务到达选择等待时，如果 accept 语句命名的一个或多个入口已被调用，则会选择一个调用（方式由语言定义），并与调用任务的任务执行汇会；汇会结束时，参与汇会的 accept 语句之后的语句列表（如果有）将与调用任务并行执行。




```
select
<accept-statement>
[statement-list>
or
<accept-statement>
[statement-list>
or
  ..
end select;
```

图 2 - 如果没有任务调用接受语句中命名的任何条目，执行选择性等待（selective wait）的任务将继续执行

另一方面，如果是条件监控器等待（monitor wait），执行选择性等待的任务将挂起，直到某个任务调用了这些条目之一，此时它将与该任务进行会合（rendezvous）。可以使用其他选项为选择性等待添加条件或定时行为。

选择性等待的分支被称为选择性等待备选（selective wait alternatives），有多种。图 2 所示的是接受备选（accept alternatives）。任何选择性等待备选都可以由一个包含布尔表达式的保护语句（guard）前缀。当任务到达选择性等待时，会首先评估所有的保护语句。保护语句求值为真的的备选，或者没有保护语句的备选，被称为被称为“开放的”（open）。只有开放的备选会在选择性等待的执行过程中被进一步考虑。保护语句中的布尔表达式通常涉及任务局部的“状态”变量。使用保护语句是实现监控器的关键要素，监控器可以挂起一个监控请求，当该操作在某些其他任务执行互补的监控操作之前无法执行时。（此类监控器的示例可能是一个从任务集合中缓存项目的缓冲区。当缓冲区为空时，无法执行从缓冲区向请求任务投递项目的操作；它必须等待其他任务先执行将项目放入缓冲区的互补操作。保护语句将用于在缓冲区为空时阻止接受请求交付项目的条目调用。）

这种等待与多个其他任务中的任何一个进行交互的能力，对于“诊所问题”解决方案的运行至关重要。在该问题，接待员必须等待空闲医生对病人的请求，或患者关于他们生病并需要医生的通知。这些交互可能以任意且不可预测的顺序发生，接待员必须在每次发生时做出响应。保护语句在该解决方案中也起着至关重要的作用；它们被用于推迟接待员与空闲医生的交互，直到它知道存在病患。该问题解决方案的大部分预期行为，包括医生和患者排队直到能够配对，都是从 Ada 任务特性的语义免费获得的。

Ada 中任务的终止本身是一个深奥的主题，我们在这里只给出可能性的简要概述。任务终止的一种方式是到达执行的末尾（但在该点，它们将等待直到它们的所有子任务（如果有）都终止）。另一种方式通过另一种类型的选择性等待（终止备选）表示，这种方式更适合像监控器这样的任务，它们只要还需要这些服务，就会重复地为其他任务执行服务。非正式地说，后一种机制允许服务任务在终止，而不是等待未来的条目调用，当不再可能从任何可能与其交互的任务处接收条目调用时——也就是说，当所有任务都已终止，或者同样陈述了终止意愿而不是接受另一个调用时。通常，当一个任务通过这种机制终止时，其他任务（它可能与之交互的任务）也会同时终止，因此这种机制被称为“分布式终止”（distributed termination）。分布式终止在问题解决方案中并没有被使用。

# Ada

尽管已经提到了任务（tasks）和过程（procedures）在形态上的相似性，但将整个任务看作并行执行的最小单元显然是不正确的。任务通常在挂起和执行之间交替，而执行周期可以根据当前应用程序的需求灵活调整大或小。如果认为 Ada 任务以固定方式绑定到处理器或多处理器系统的节点，且这些处理器或节点频繁变为阻塞，也是一个错误。Ada 实现通常维护一个符合执行（未挂起）的 Ada 任务队列，当每个处理器的上一个任务终止或挂起时，会从队列中取一个任务。在某些情况下，处理器注意力从一个任务到另一个任务的重定向甚至可以在没有上下文切换的情况下完成（例如，使用 Habermann-Nassi 优化）。

对 Ada 的常见批评之一是与其他语言相比它过于冗长。在这种背景下，例如，在任务的规范（specification）和体（body）中，任务条目参数配置（parameter profiles）的重复。（子程序的规范和体中也存在相同类型的重复。）这种特定的重复可以归因于“子程序重载”（subprogram overloading）这一强大语言功能的要求，它在抽象设计中起着重要作用。总来说，Ada 的冗长有时是冗余的结果，这种冗余既约束了程序的威力又增加了程序的安全性（通过实现广泛的编译时检查）。由于其所代表的意义，大多数 Ada 程序员很快学会接受这种冗长是资产而非障碍。

Ada 似乎是一个表达诊所问题解决方案的良好语言，因为问题中的参与者以及它们之间的交互直接映射到 Ada 的可用功能。各种参与者之间的两两交互让人想起了会合（rendezvous）本身；预期的队列行为是免费获得的；而信号的合并（可以说的话）是由选择性等待提供的。Hamming 问题四个解决方案中的前两个在 Ada 中似乎也很有吸引力，因为有了流（stream）的抽象——虽然它不是内置在语言中的，但在 Ada 中很容易编程。这些解决方案与书中的其他语言相比相当，在那些语言中，流要么是内置的（如 SISAL [9]），要么作为之前编写的可重用抽象可用。Hamming问题的剩余解决方案似乎不那么吸引人，但仅是因为它们比通常的解决方案复杂得多。

# 1.2. 数据结构与抽象特征

在用于定义复杂数据结构和抽象并使其具有可重用性的特征中，包（packages）、泛型（generic units）、私有类型（private types）、访问类型（access types）、带有区分部分的记录类型（record types with discriminant parts）或变体部分的类型（variant parts）以及运算符重载（operator overloading），这些特征提供了这些潜在优势的表面。解决方案在开发过程中自然暗示了它们的使用。

包是 Ada 中的四种程序单元类型之一，其他是子程序（函数或过程）、任务和泛型单元。包包含了为了一起使用的声明。例如，数学库通常构造为一个包含数学子程序的包。抽象通常组织为声明了类型（通常是私有类型）以及适用于这些类型的操作包。像程序单元一样，包的规范有规范和体。包规范中被称为可见部分的部分是导出给用户或客户端的。包体包含在其规范中出现的单元的体；它还可以包含其他类型、对象的声明（这些声明仅在包内部可见）。某些包不需要体。

单独作为编译单元的包规范定义库包；单独作为编译单元的子程序和泛型单元也定义库单元。[任务不能单独出现，必须始终在另一个程序单元内部。这一规则与分布式任务的语义有关。]库单元在成功编译后进入程序库，此后对潜在客户端可用。客户端——即需要库单元提供的设施的编译单元——在它的上下文句（context clause）中引用库单元，该句包含一个或多个可选的使用（uses）。（我们说编译单元“with”该库单元。在本章中，我们也说编译“in the context of”该库单元。）库单元的客户端可以在库单元体编译之前进行编译；此外，当库单元体在最初编译后更改时，客户端不需要重新编译。例如，库包的规范包含了编译对导出的类型、对象和子程序的引用所需的所有接口信息。因此，只要接口保持不变，抽象的具体实现的更改不需要抽象的客户端重新编译。

Hamming 问题的解决方案组织为一个库包；该包导出一个类型、一个内部包和一个解决该问题的过程。为了解决 Hamming 问题，用户编写一个“with” Hamming 问题包的程序单元，然后




20 K. W. Dritz

调用其导出的过程。为了与该过程接口，用户还需要声明哈明问题（Hamming's problem）包及其内部包导出的类型的某些对象。

烷烃（paraffins）问题的解决方案组织方式略有不同，分为三个部分：一对库包（一个用于基团，另一个用于分子），它们导出类型和操作，以及一个解决该问题的库函数。为了解决烷烃问题，用户编写一个程序单元来“with”（使用）并调用该函数。为了与该函数接口，用户也需要“with”分子包并声明由其导出的类型的某些对象。根据用户应用程序的其他需求，用户可能还希望“with”基团包。

泛型单元（Generic units，可能是泛型包或泛型子程序）通过允许各种方式对包或子程序进行参数化，有力地支持了重用性目标。它们作为模板，通过实例化过程获得普通的包或子程序，在实例化过程中，泛型实际参数与泛型单元的泛型形式参数相关联。泛型单元可以使用类型、计算值（在泛型单元内部起别名）、变量（提供泛型单元内部外部变量之间的别名）以及子程序进行参数化。泛型实际参数被“导入”到泛型单元中；某些由泛型包导入的内容可能会通过从实例化获得的普通包重新导出。

医生诊所（doctor's office）问题的解决方案组织为一个泛型库过程，该过程导入了一对函数。为了解决医生诊所问题，用户编写一个程序单元来“with”该泛型过程，用一对函数名（由用户提供）对其进行实例化，这两个函数提供了患者健康期和医生治愈时间的概率分布，并调用生成的普通过程。通过子程序进行参数化也 

# Ada

21

在烷烃问题的解决方案中起着次要作用，在其中使用了泛型过程（既作为库单元也从内部使用）。目前，泛型单元必须通过这种方式用另一个子程序来参数化子程序，但预计 Ada 9X 提供提供不使用泛型单元的方法。

天际矩阵（skyline matrix）问题的解决方案组织为一个泛型库包，该包导入了一个浮点类型和一个正整数值。为了解决天际矩阵问题，用户编写一个程序单元“with”该泛型包，用一个浮点类型（从而将问题定制为所需的精度）和一个给出问题阶数的正整数对其进行实例化，声明由生成的普通包导出的类型的矩阵和向量，使用该包导出的操作操纵矩阵和向量，并调用函数（也由包导出）来求解矩阵方程。

在 Ada 中，类型被视为一组值的集合和一组对这些值进行的操作。类型的操作可以由用户以子程序的形式进行声明，并通过名称或（预定义的）运算符符号指定。此外，符合类型性质的操作被隐式声明并随类型一起导出。例如，浮点类型的声明隐式声明了对该类型值的算术操作；另一个例子是数组类型的声明隐式声明了通过下标进行组件选择作为该类型的操作。用户可以声明私有类型（private types），其意义在于某些操作是由类型声明隐式导出的；本质上，类型的实现细节对客户端是隐藏的。私有类型定义在包规范的可见部分。在包规范的另一部分（称为私有部分）给出了相应的全类型（full type）声明。除了为所有私有类型隐式导出的少数操作外，包客户端可用的其他操作是在包的可见部分以子程序形式显式导出的。与全类型声明相关的操作由它隐式声明，并在包体中可见，但对包客户端不可见。私有类型的使用通常与泛型的使用相结合以构建强大且安全的抽象。我们在解决方案中私有类型的使用仅限于第 5.2 节末尾关于与天际矩阵相关的某些可能性的简要讨论。
然而，在几个问题解决方案中，我们假设存在提供通用有用抽象的泛型库包，并且确实会使用私有类型。

 Ada 中的动态存储分配（Dynamic storage allocation）适用于需要构建复杂列表或树结构的应用程序。一种名为*分配器*（allocator）的操作动态地获取对象的存储空间并返回指向新分配对象的指针。指针值是一种称为*访问类型*（access types）的类型的值。访问类型的声明规定了访问类型的值所指向对象的类型，维护了 Ada 的强类型原则。我们在解决方案中以多种方式使用访问类型。在烷烃问题中，我们将分子和基团构建为链接记录的树，并将给定大小的记录存储在链列表中。在医生诊所问题中，我们将医生表示为某些任务类型的动态分配任务，每个任务都通过指针访问，指针用于向接待员和治疗的患者标识该任务。在天际矩阵问题中，我们动态分配天际矩阵的行和列，以容纳天际线内部的组件，而不浪费外部零组件的空间；事实上，一个天际矩阵表示为指向下三角行向量的指针数组以及另一个指向上三角列向量的指针数组。

记录类型（record types）的两个特征在 Ada 的数据结构和抽象中起着作用：判别部分（discriminant parts）和变体部分（variant parts）。记录类型可以带有*判别部分*，它以某些方式对类型进行参数化。

# Ada

23

记录定义中的判别部分提供了称为判别符（discriminants）的特殊组件的名称和类型，其他组件可能依赖于此。在不详细说明的情况下，我们简单说记录类型的判别符可以用来表示其他作为记录组件的边界，并结合部分，它们可以用于确定记录中存在哪些交替组件。因此，带有判别部分的类型对象在布局方面是自描述的。根据它们的声明和创建方式，此类对象可以被限制为永久具有相同的布局（即判别符一旦初始化就不可更改），或者允许在赋值结果下更改布局，只要在类型给出的判别符允许值范围内。在问题解决方案中，我们仅有限地使用了这一功能。在烷烃问题中，我们使用判别符和变体部分为烷烃基团定义了具有两种布局的记录类型，烷烃分子的记录类型也可以有两种布局。在天际矩阵问题中，我们使用判别符来持有作为数组的记录组件的边界。在两种情况下，记录类型的对象都是带有限制布局的动态分配的。

解决方案中最后一个感兴趣的特征是*子程序和运算符重载*（subprogram and operator overloading），指的是允许声明具有相同标识符（可以是名称或预定义的运算符符号）但参数/结果特征不同的多个不同子程序。由特定名称或运算符符号指定的子程序在编译期间通过重载解析确定，这取决于参数/结果类型和其他上下文信息。该特性通过允许将熟悉的名称或运算符符号扩展到新的数据类型来支持抽象。我们在天际矩阵问题的解决方案中使用运算符重载为向量定义了一个内积函数，使用了习惯的*中缀*（infix）运算符符号。




24 K. W. Dritz

（它被预定义为标量的乘法运算符）；因此，我们重载了 `*` 运算符。（我们还将命名参数关联与更传统的位置参数关联相结合，特别是当这种结合能让子程序调用或泛型实例化读起来像一个英语短语时。）

在随后的问题解决方案中，我们对语言特性的讨论仅限于让不熟悉该语言的读者能够理解这些特性的影响、优势和局限性，以及其对当前应用的所需的深度。然而，我们并未尝试描述所有用到的特性。

## 2 汉明问题（扩展）

该问题如下：给定一个有限的递增素数序列 $p_1, \dots, p_k$ 和一个整数 $n$，按大小递增顺序且不重复地输出所有小于或等于 $n$ 的形式如下的整数：

```
$\prod_{i=1}^{k} p_i^{e_i}$
```

其中 $e_t \ge 0$。提示指出，如果 $m$ 在输出序列中，那么只要 $m \cdot p_b$ 小于或等于 $n$，它也在序列中。

这里给出了四种不同任务程度的汉明问题解决方案。第一个是直观的，没有使用任何不必要的特性；第二个是第一个的微小变，它以一种相当人工的方式使用任务来消除不必要的确定性，并意外地引入了少量的并发。第三种实现了一种完全不同的算法，并以更函数的方式使用任务；第四种是第三种的扩展，通过复制任务来实现更大的并行性。虽然第四种解决方案也代表了对其前身版本的人工改进，但其改进的目标和方法与第二种解决方案所体现的不同。

### 2.1. 第一种解决方案：常用的串行算法

解决此问题的常用方法涉及多个并行的未来输出值流，每个流对应一个素数。在“主循环”的每次迭代中，一个值被添加到每个流的末尾，产生一个新的输出值，并从流的头部移除一个值。更准确地说，每循环一次循环：

- 将上一个输出值与该流关联的素数的乘积添加到每个流的末尾；
- 确定所有流头部值中的最小值，它将成为下一个输出值；
- 移除每个头部匹配该最小值的流。

Ada 中没有预定义的流（streams），但我们假设作为一个库单元存在一个名为 `streams` 的泛型包，它提供了一个名为 `stream` 的抽象数据类型，并带有对该类型对象的适当操作。由于我们需要正整数流，我们使用预定义类型 `integer` 的预定义子类型 `positive` 来实例化泛型包，以获得一个我们称为 `positive_streams` 的包；其类型正是我们所寻找的。我们不关心泛型包的实现（它可能使用指针和链表），为了简洁起见，我们省略了它的规范。我们假设 `stream` 类型对象的初始状态为“空”，允许我们省略对流的显式初始化；这是一个合理的假设，因为访问对象（即指针）在 Ada 中会自动初始化为空。在本次应用中，我们只需要流的以下操作，我们假设这些是由泛型包提供的：一个 `append` 过程用于向流的末尾添加一个值；一个 `head` 函数用于返回非空流头部的值而不移除它；以及一个 `behead` 过程用于移除并丢弃非空流头部的值。可以假设 `head` 和 `behead` 应用于空流时会抛出某些异常。我们不需要 `is_empty` 谓词；由于我们只将 `head` 和 `behead` 应用于非空流，我们可以保证永远不会抛出异常。

我们的汉明问题的第一个解决方案以包 `hamnings_problem` 的形式给出，它导出了正整数无约束数组（不带边界的数组）类型、一个与正整数流相关的类型和操作包，以及一个在给定最大值和升序排列的素数数组时计算并交付所需值序列的过程。数组类型和流类型及操作包与该过程一起导出，以便它们用于构建和处理该过程的输入输出（我们选择通过将输出值序列附加到一个 `in out` 参数来交付，该参数最初是作为空流传递的）。`hamnings_problem` 包的规范如图 3.6 所示。

```ada
with streams;
package hamnings_problem is
type positive_array is array (integer range <>) of positive;
positive_streams is new streams (positive);
use positive_streams;
  procedure solver (n :in positive;
                   primes :in positive_array;
                   outputs :in out stream);
end;
```

> 图 3 - `hamnings_problem` 包的规范

`hamnings_problem` 包的体如图 4 所示。`min` 和 `max` 函数在 Ada 中没有预定义，但我们假设作为一个库单元存在一个名为 `min_and_max` 的泛型包，我们用子类型 `positive` 对其实例化。实例结果是一个我们称为 `positive_min_and_max` 的包；它导出了针对正整数的 `min` 和 `max` 函数。我们在这里不关心泛型包的实现，为了简洁，我们甚至省略了它的规范。

```ada
with min_and_max;
package body hammings_problem is
  package positive_min_and_max is new min_and_max (positive);
  use positive_min_and_max;
  procedure solver (n      : in positive;
                    primes  : in positive_array;
                    outputs : in out stream) is separate;
```

图 4 - `hamnings_problem` 包的体（第一种解决方案）

`solver` 过程的体由一个存根持有，而 `solver` 的正体是 `hamnings_problem` 的子单元。这允许我们保持编译单元较小。现在对经济性的需求并不迫切，但展示的解决方案确实从这种做法中受益。`solver` 的正体作为一个独立的编译单元如图 5 所示。

图 5 所示的解决方案有些浪费，因为它将超过 $n$ 的值附加到流，尽管这些值从未成为输出序列的一部分；当主循环终止时，它们仍然留在流中。更糟糕，它缺乏健壮性，因为此类值的计算理论上可能会溢出，导致程序停滞。这些问题可以很容易地修正，但算法的简单性会被增加的细节所掩盖。

28 K. W. Dritz

```ada
separate (hamnings_problem)
procedure solver (n : in positive;
  primes : in positive_array;
  outputs : in out stream) is
  infinity : constant positive := n + 1;
  pipes : array (primes'range) of stream;
  i : positive := 1;
  new_i : positive;
begin
  while i <= n loop
    append(i, to => outputs);
    new_i := infinity;
    for k in primes'range loop
      append(primes(k), to => pipes(k));
      new_i := min(new_i, head(pipes(k)));
    end loop;
    i := new_i;
    for k in primes'range loop
      if head(pipes(k)) = i then
        behead(pipes(k));
      end if;
    end loop;
  end loop;
end;
```

```5 - `solver` 过程的正体（第一种解决方案）

### 2.2. 第二种解决方案：并行处理流

在主循环的每次迭代中，之前的解决方案按顺序遍历流。当然，访问流的顺序是有意义的，而且事实上它们可以并行处理。因此，该解决方案实际上是过度规范的。

对于我们的第二种解决方案，`solver` 过程修改后的正体如图 6 所示，而 `hamnings_problem` 包的规范和体保持不变。





# Ada

```ada
separate (hammings_problem)
procedure solver (n : in positive;
  primes : in positive_array;
  outputs : in out stream) is
  task type stream_processor is
    entry install_prime (a_prime : in positive);
  end;
  task min_finder is
    entry bid (a_head : in positive);
    entry wait_for_min;
  end;
  infinity : constant positive := n + 1;
  pipes : array (primes'range) of stream_processor;
  : positive := 1;
  task body stream_processor is separate;
  task body min_finder is separate;
```

```ada
begin
  for k in primes'range loop
    pipes(k).install_prime (primes(k));
  end loop;
end;
```

图 6 - solver 过程的正确主体（第二方案）

现在分配了一个单独的任务用于处理每个流。流的 pipes 数组被一个（同名的）数组取代，其组件的类型为名为 `stream_processor` 的类型；该数组中的每个任务都使用相应的质数声明并处理单个流。还有一个额外的任务 `min_finder`，用于在适当的时间找到所有流头部的最小值。`stream_processor` 任务类型和 `min_finder` 单个任务的主体位置由存根占据；它们的正确主体是 `solver` 的子单元，将在稍后显示。

`stream_processor` 任务的 `pipes` 数组在执行 `solver` 时创建（具体是在其声明部分的详细化处理期间）。`solver` 的语句列表初始化每个任务与其对应的质数，然后在（在末尾）等待所有任务终止，最后返回给调用者。

`stream_processor` 任务在每次循环执行时，都会将其各自的流头部作为可能的最小值向 `min_finder` 竞价，然后等待 `min_finder` 将这些竞价放入 `i` 中（变量 `i` 扮演的角色与之前相同，但现在对所有任务是全局的）。实现 `stream_processor` 任务行为的代码见图 7。

```ada
separate (hammings.problem.solver)
task body stream_processor is
  my_prime : positive;
  my_stream : stream;
begin
  accept install_prime (a_prime : in positive) do
    my_prime := a_prime;
  end
  while i <= n loop
    append (i*my_prime, to => my_stream)
    min_finder.bid (head (my_stream));
    min_finder.wait_for_min;
    if head (my_stream) = i then
      behead (my_stream);
    end
  end;
```

图 7 - `stream_processor` 任务类型的正确主体

用于与 `min_finder` 进行通信和同步的对等（rendezvous）像一个“屏障”，防止 `stream_processor` 任务继续移动到其流头部，直到所有任务都已将其流头部的值通信给 `min_finder`，并且 `min_finder` 找到了它们中的最小值。实现 `min_finder` 任务行为的代码见图 8。

# Ada

```ada
separate (hammings_problem.solver)
task body min_finder is
new_i : positive;
begin
while i <= n loop
  append (i, to => outputs);
  new_i := infinity;
  for k in primes'range loop
    accept bid (a_head : positive) do
      new_i := min(new_i, a_head);
    end;
  end loop;
  i := new_i;
  for k in primes'range loop
    accept wait_for_min;
  end loop;
end loop;
end;
```

图 8 - `min_finder` 任务的正确主体

第二个方案不能被预期产生任何显著的加速，因为同步点之间的并行工作粒度相对于同步开销来说太小了。屏障所代表的串行瓶颈在第一个方案中也有对应物，它本身并没有让情况变得糟糕。第二个方案的主要价值在于说明如何使用“询问”（asking）用完全非确定的排序来替换不必要的确定性排序，而这种排序仅满足算法的相关数据流属性。（`min_finder` 中的 `for` 循环仅用于计算要执行的对等次数，而不是为了对它们排序；循环变量在循环内部没有被引用。）

### 2.3. 第三种方案：并发的奇新用法

在 Ada 的理想化实现中，如果对等（rendezvous）不产生开销，第二个方案产生的加速预计随质数的数量而扩展；如果处理器比质数多，多余的处理器将无法被利用。接下来要描述的完全不同的方法能够与独立参数成比例地扩展；因此，它可以始终能够使用所有可用处理器。（我们将实际扩展的细节留给第四种方案，这里只展示基本算法。）

我们的第三种方案使用一个单一的未来输出值循环流；该流之所以是循环的，是因为从其头部移除的一些值会被放回流的尾部。在主循环的每次迭代中，流头部的值被移除并放入 `outputs` 流中；它还被触发另一个任务（称为 `products_generator`）生成一系列自身与所有质数的乘积序列。同时——即在乘积正在生成时——未来输出值循环流的剩余部分被读取，并在它们可用时与乘积流合并（两个流都是升序的），生成的数值序列被重定向回循环流（即附加到其尾部）。

在这一方案中，与之前的方案相比，我们不生成任何大于 $n$ 的乘积。使用常量 `infinity`（定义为 $n+1$ 且之前用于其他用途）作为乘积流和未来输出循环流的结束标记是方便的（其中它将上一次迭代产生的最后一个值与下一次迭代产生的第一个值隔开）。循环流初始化为 1，随后是结束标记；循环流随迭代增长并最终收缩，直到只剩下结束标记（即，主循环中从循环流读取结束标记时）。

# Ada 33

![](img/68e0e7cd6167f4d693a9b7458d12.png)

图 9 - 解决问题的创新算法数据流

该算法的数据流特征见图 9。`products_generator` 任务按照自己的速度运行，可能在需要之前就生成乘积（在这种情况下它们留在乘积流中），或者生成得太慢，导致在需要时乘积流为空。因此，之前假设的流抽象对于此应用是不够的；不同任务写入该流这一事实是其适用性的线索。我们现在要求在尝试读取另一个任务写入的流时挂起，以将其与之前的类型区分。。事实上，我们现在假设有一个库单元名为 `buffers` 的泛型包，提供一个名为 `buffer` 的抽象类型以及该类型的相应操作。由于我们需要正整数缓冲区，我们使用 `positive` 实例化 `buffers` 以获得一个我们称为 `positive_buffers` 的包；其缓冲区类型正是我们需要的。正如处理流一样，我们假设缓冲区对象的初始状态是“空”，从而允许我们省略显式初始化缓冲区。为了简便，我们省略了泛型包的主体。然而，我们注意到可以将之前的 `head` 和 `out` 操作合并为一个名为 `read` 的过程，该过程等待缓冲区非空，然后移除并交付其头部项。我们将 `append` 的缓冲区模拟称为 `write`，以保持我们的抽象分离。最后，我们注意到 `buffers` 的实现我们确实使用任务来实现所需的挂起；事实上，该类型可以实现为具有监视器行为的任务。

在第三种方案中，我们仅对 `solver` 的输出保留流的使用，而在其他地方使用缓冲区。理论上，循环“流”可以是流而不是缓冲区，因为它被同一个任务读取和写入；我们选择将其实现为缓冲区，是为了预测第四种方案（在那种方案中，相应的对象必须是缓冲区），以避免强调当前方案与变体之间的差异。正如第二个方案一样，`hamnings_problem` 包的规范保持不变，但这次我们对其主体做了细微调整：纯出于风格考虑，我们选择在那里实例化 `buffers` 泛型包。`hamnings_problem` 包的修订后主体见图 10。

`solver` 过程的修订后主体见图 11。`products_generator` 任务被创建并在每次通过主循环执行结束时随后终止。通过轻微的重新设计，我们可以安排只创建一次，将其处理封装在循环中，并将该循环与 `solver` 中的主循环同步，并在适当的时间终止。那种重新设计将使用对等来进行同步，并对 `products_generator` 任务进行分布式终止。但由于简单性更




# Ada

在这些解决方案中，相比效率，我们更重要，因此我们选择了语义上更简单的方法。

```
with min_and_max, buffers;
package body hammings_problem is
  package positive_min_and_max is new min_and_max (positive);
  package positive_buffers is new buffers (positive);
  use               positive_min_and_max, : in positive_buffers;
  procedure solver (n               : in positive;
                    primes         : in positive_array;
                    outputs         : in out stream) is separate;
```

图 10 - hammings_problem 包的主体（第三种解决方案）

### 2.4. 第四种解决方案：数据流循环展开

“循环展开”技术可以通过一种独特的方式应用于图 9 中的数据流循环：通过将值从循环流中移除到将其重新放回流中这之间的所有值处理过程视为单一的“阶段（stage）”处理；通过将一个处理阶段封装在一个任务（task）中；将其复制任意次数；并在任务之间（即阶段之间）插入缓冲区（而不是流）。通过将处理过程分散到更多的任务中，其结果（其数据流特征如图 12 所示）实现了可能更大的并行性——这主要是因为可以同时生成多个产品流，并将其与未来输出的循环流合并。需要注意的是，未来输出值的“循环流”现在分散在整个数据流循环中，某些值位于每个任务间的缓冲区和每个任务的局部变量中，且只有一个结束标记位于循环附近的某处。尽管现在有许多任务向输出流追加内容，但由于随着未来输出流的“前端”从一个阶段推进到下一个阶段，每次只有一个任务执行操作，因此这种行为不会产生同步问题。

# 36

# K. W. Dritz

```
separate (hammings_problem)
procedure solver (n : in positive;
  primes : in positive_array;
  outputs := in out stream) is
  infinity : constant positive := n + 1;
  recirc : buffer;
  i : positive;
begin
  write (i, to => recirc);
  write (infinity, to => recirc);
  loop
    read (i, from => recirc);
    exit when i = infinity;
    append (i, to => outputs);
    declare
      j, p : positive;
      products : buffer;
      task products_generator;
      task body products_generator is
      begin
        for k in primes'range loop
          exit when i > n/primes(k);
          write (i*primes(k), to => products);
        end loop;
        write (infinity, to => products);
      end;
    begin
      read (j, from => recirc);
      read (p, from => products);
      loop
        if j < p then
          write (j, to => recirc);
          read (j, from => recirc);
        elsif j > p then
          write (p, to => recirc);
          read (p, from => products);
        else
          write (j, to => recirc);
          exit when j = infinity;
          read (j, from => recirc);
          read (p, from => products);
        end if;
      end loop;
    end;
  end loop;
end;
```

图 11 - solver 过程的主体（第三种解决方案）

# Ada

![](img/68e0c8e7cd61671f4d693a9b7458d12d_47_0.png)

输出流

结束标记后的第一个值

STAGE 任务

图 12 - 使用循环展开求解汉明问题的新型算法中的数据流

第四种解决方案的代码（即带有数据流循环展开的新型算法变体）分布在两个图中。图 13 显示了修改后的 solver 过程正体，其中 stage 任务类型的主体由一个主体存位符（body stub）表示。图 14 显示了 stage 的正体。

我们为 solver 增加了一个额外参数 `m`，它是循环展开的深度（阶段数量）；为了节省空间，我们省略了由于此添加而对 `hamdings_problem` 包规范和主体进行的细微更改。理想情况下，`m` 的值应该与可用处理器的数量成比例增加，其速率可能最好通过实验来确定（这取决于每个阶段的任务消耗了多少处理器的性能，以及等因素）。

# 38

# K. W. Dritz

```
separate (hammings_problem)
procedure solver (n, m : in positive;
  primes : in positive_array;
  outputs : in out stream) isntask type stage is
  entry identify_self (k : in positive);
end;
  infinity : constant positive := n + 1;
  stages : array (1 .. m) of stage;
  sbuffers : array (1 .. m) of buffer;
  done : array (1 .. m) of boolean := (others => false);
task body stage is separate;
begin
  write (1, to => sbuffers(1));
  write (infinity, to => sbuffers(1));
  for k in stages'range loop
    stages(k).identify_self (k);
end;
```

> 图 13 - solver 过程的正体（第四种解决方案）

在这一解决方案中，大部分工作由 solver 的依赖任务完成。在“启动”第一个阶段并向每个阶段识别其在数据流循环中的位置后，solver 在（其末尾）等待其依赖任务终止然后返回给其调用者；当它最终这样做时，输出流已经完成。

如图 14 所示，每个阶段的第一个动作是从 solver 接收其在数据流循环中的位置。它计算其后继者的位置。这些位置当然是 solver 声明的数组中的索引，因此这些数组中最后一个组件的后继者是第一个组件。每个阶段使用其自己的索引及其后继者的索引来确定哪个是其输入缓冲区，哪个是输出缓冲区。

```
separate (hammings_problem.solver)
task body stage is
ni, self, successor : positive;
begin
  accept identify_self (k : in positive) do
    self := k;
  end;
  successor := self mod m + 1;
  loop
    read (i, from => sbuffer(self));
    exit when i = infinity;
    append (i, to => outputs);
    declare
      j, p : positive;
      products : buffer;
    task products_generator;
    task body products_generator is
      begin
        for k in primes'range loop
          exit when i > n/primes(k);
          write (i*primes(k), to => products);
        end loop;
        write (infinity, to => products);
      end;
      begin
        read (j, from => sbuffer(self));
        read (p, from => products);
        loop
          if j < p then
            write (j, to =>buffer(self));
            read (j, from => sbuffer(self));
          elsif j > p then
            write (p, to =>buffer(self));
            read (p, from => products);
          else
            write (j, to =>buffer(self));
            exit when j = infinity;
            read (j, from => sbuffer(self));
            read (p, from => products);
          end if;
      end loop;
      end;
      done(self) := true;
      if not done(successor) then
        write (infinity, to => sbuffer(successor));
      end if;
    end;
```

图 14 - stage 类型的正体

40 K. W. Dritz

当一个阶段在主循环中从输入缓冲区读取结束标记时，它会将自己的 `done` 数组分量设置为 true，根据需要传播结束标记，然后终止。从一个阶段到其后继者的结束标记传播，如果后继者尚未从输入缓冲区读取结束标记（如 `done` 数组分量所示）。如果不以这种方式传播结束标记，阶段将等待永远不会到达输入而死锁，solver 也不会终止。但结束标记（前面没有未来输出）已经绕过了数据流循环，所有的阶段都将终止，不再需要进一步传播。

## 3 烷烃问题

烷烃分子的分子式为 $CnH_{2n+2}$。问题如下：给定一个整数 $n$，按大小顺序输出 $i \le n$ 的烷烃分子结构表示，包括所有异构体但不包含重复。

烷烃问题旨在揭示应用语言的优势。Turner 在应用语言 KRC 中的原始解决方案 [10] 大量使用了抽象和高阶函数来产生紧凑优雅的程序，但是以牺牲效率为代价的。他的程序旨在通过附加适当大小的烷烃基团来产生所有给定大小的烷烃分子。





## Ada 41

在对领先碳原子进行调整时，最初并没有考虑到这一简单过程会产生每个不同烷烃异构体的许多不同表示形式（不同的取向）。由于问题要求为每个异构体只产生一种表示形式，Turner 的解决方案过滤掉了重复项。每当生成一个新的烷烃分子时，都会测试其与所有之前保留的分子的唯一性。唯一性测试包括检查每个之前保留的分子是否属于新生成分子的所有结构等效重取向的集合。后者通过计算包含新生成分子的集合在各种等价保持变换（旋转、反转以及附在分子每个碳原子上的烷烃基团的交换）下的闭包来实时获取。为了使这一过程可行，必须有隐式或显式的垃圾回收在工作。KRC 解决方案之所以简洁，部分是因为垃圾回收是隐式的，部分是因为在发现新的重复项时，并没有优先考虑避免重复计算。Turner 采用的策略还受到 KRC 另一个特征——惰性求值的影响——它通过推迟集合元素的计算直到需要时，至少部分地回收了丢失的效率（通常在闭包尚不完整时就能发现重复项）。

面对在不具备 KRC（或其他替代语言）强大且方便特性的语言中解决此问题的程序员，会有强烈的动机放弃 Turner 的解决方案——如果编写显式垃圾回收没有吸引力，且如果严格求值和重复计算在效率上是不可接受的——并寻找一种从一开始就避免重复项的烷烃分子生成策略。Ada 解决方案，像本书中的大多数其他方案一样，遵循了这种策略。

烷烃分子可以被视为一棵自由树 [8]，第 362-363 页，其顶点对应碳原子，边对应碳-碳键。因此，大小为 $i$（即具有 $i$ 个碳原子）的独特烷烃异构体对应于具有 $i$ 个顶点的结构不同的自由树。我们的程序将烷烃分子表示为有向的、有序树（我们在此处将这些顶点称为节点），而不是自由树——我们避免重复项策略的核心在于：烷烃分子自由树表示的顶点与其在程序中对应的有向有序树表示的节点之间的映射。

显而易见，树表示中某个顶点的无序邻居将成为程序中所用表示中其映射到的节点的子节点。改变子节点的顺序会导致相同烷烃分子的不同表示形式——即结构等效的烷烃分子。我们通过对一个节点的子节点使用唯一的（字典序的）排序来避免这种重复项的产生。请注意，虽然自由树的顶点的邻居可能少于四个（即当它们被附上时），但程序树中对应的节点要么有四个子节点（根节点的情况），要么有三个子节点和一个祖先节点（非根节点的情况）。还要注意，某些子节点代表氢原子；在程序中，氢原子附着在碳原子上的位置是显式的。

同样显而易见的是，自由树的有向边将成为程序树中节点之间的定向链接，而将某个顶点再次映射到根节点会导致相同烷烃分子的不同表示形式。我们通过引用自由树的质心定理（见 [8]，第 387 页）来避免这种重复项：奇数大小的自由树有一个质心（高度最小的顶点，其中顶点的高度是其最大子树的大小），而偶数大小的自由树只有一个质心或一对相邻的质心。我们通过选择质心作为程序树中的根节点，对单质心烷烃分子的表示进行规范化处理。在双质心烷烃分子的情况下，我们使用对应于两个质心之间的碳-碳键的任何节点作为根节点。它恰好有两个子节点，对应于两个质心；它们当然按照我们的方式进行字典序排序。

总结，我们的策略通过规范化地选择根节点并进行字典序排序来避免重复项。奇数大小的烷烃分子和偶数大小的单质心烷烃分子在这里被称为“碳中心烷烃”（CCPs）；它们的树的根节点对应碳原子并有四个子节点，每个子树的根代表一个烷烃基团。大小为 $i$ 的 CCP 的基团大小小于或等于 $(i-1) / 2$ 的地板值，且总大小为 $i-1$。偶数大小的双质心烷烃分子在这里被称为“键中心烷烃”（BCPs）；它们的树的根节点对应于碳-碳键并有两个子节点，每个子树的根代表一个烷烃基团。对于它们来说，大小为 $i$ 的 BCP 的根节点大小正好等于 $i/2$，因此总大小为 $i$。（对于它们来说，大小 $i>0$ 的烷烃基团的根节点对应碳原子并有三个子节点，子树的根代表一个烷烃基团是递归的）。因此，烷烃基团的数据结构是三个烷烃基团，每个基团的大小小于或等于 $i-1$，且总大小为 $i-1$。大小为 0 的烷烃基团是氢基团；其根节点对应氢原子且没有子节点。在程序中，所有三类对象都是通过相同的过程构建的，该过程相当于向某些其他节点附上若干个（两个、三个或四个）适当大小的烷烃基团。对附着基团最大大小的限制确保了 CCP 的根节点对应于质心，同样确保了 BCP 根直接后代的节点对始终对应于相邻的质心；这一属性加上附着基团的字典序，保证了重复项的避免。）

### 3.1. 串行解决方案

为了简单起见，我们在本节中开发了一个解决烷烃问题的完全串行解决方案；在下一节中，我们将讨论该问题提供的并行机会，并通过通过对串行解决方案的一小部分进行直接修改来获得一个并行解决方案。

在顶层，我们的串行解决方案是一个函数形式 `parffins`（如图 15 所示），它接受一个正整数 $n$，并返回一个索引值为 1 到 $n$ 的数组，其第 $t$ 个组件是大小为 $l$ 的唯一烷烃异构体的列表。该函数是在上下文从句中命名的两个库包定义的基团和分子的某些应用程序相关类型的文中编译的。显然，该函数需要此类类型；推测该函数所属的更大应用也是如此。（类型包的规范和体部如图 16 至 19 所示。）`parffins` 函数首先创建并在内部的局部数组 `r_array` 的组件中存储大小从 0 到 $n/2$ 的烷烃基团列表（Ada 中的整数除法向零截断，对于正操作数，这等同于提供商的地板值）；$n/2$ 是大小为 $n$ 的烷烃分子所需最大基团的大小。基团按大小顺序创建，因为构建较大的基团需要较小的基团。接下来，该函数按顺序创建大小从 1 到 $n$ 的烷烃分子列表，将 `m_array` 的第 $t$ 个组件存储为大小为列表




# Ada
# 45

首先是 CCPs，然后（对于偶数尺寸）最后，它返回 BCPs。m_array。（函数的内容将进一步讨论。）

```ada
with radicals, molecules;
  use radicals, molecules;
  function paraffins (n : positive) return array_of_molecule_lists is
  type array_of_naturals is array (positive range <>) of natural;
  use radical_lists, molecule_lists;
  r_array : array_of_radicals_lists (0 .. n/2);
  m_array : array_of_molecule_lists (1 .. n);
generic
  with procedure apply_to_each (tuple : in array_of_radicals);
  procedure enum_rad_tuples (p : in array_of_naturals);
  procedure enum_radicals (p : in array_of_naturals) is separate;
  procedure generate_radicals_of_size (i : positive) is separate;
  procedure generate_bcps_of_size (i : positive) is separate;
begin
  append (hydrogen_radical, to => r_array(0));
  for i in 1 .. n/2 loop
    generate_radicals_of_size (i);
  end loop;
  for i in 1 .. n loop
    generate_ccps_of_size(i);
    if mod i 2 = 0 then
      generate_bcps_of_size (i);
    end if;
  end loop;
  return m_array;
end;
```

> 图 15 - paraffins 函数的自说明体（串行版本）

让我们看看声明解决方案中使用的依赖于问题的包。`radicals` 包的规范如图 16 所示。自由基是树，其节点类型为 `radical_node`，这是一个记录类型（record type），带有一个判别器，用于指示该节点表示氢自由基（没有子节点）还是碳基自由基（有三个子节点）。`radical` 类型是一个访问类型，其指定类型为 `radical_node`；因此，一个自由基由其根节点表示，如果该节点不是退化的，则包含指向其子节点的指针等。还声明了一个提供自由基数组的无约束数组类型，以及其中几个具有固定组件数量的约束子类型；其中一个

```ada
with lists;
package radical_kind is (hydrogen, carboniferous);
type radical_node (kind : radical_kind);
type radical is access radical_node;
type array_of_radicals is array (positive range <>) of radical;
type two_radicals is array_of_radicals (1 .. 2);
type three_radicals is array_of_radicals (1 .. 3);
type four_radicals is array_of_radicals (1 .. 4);
type radical_node (kind : radical_kind) is record
case kind is
when hydrogen =>
null;
when carboniferous =>
  carbon_neighbors := three_radicals;
end case;
package radical_lists is new lists (radical);
ubtype radical_list is radical_lists.list;
type array_of_radical_lists is
array (natural range <>) of radical_list;
function hydrogen_radical returns radical;
function radical_made_from (subradicals : three_radicals)
return radical;
```

图 16 - `radicals` 包的规范

其中一个被用于 `radical_node` 的声明中。自由基的链表通过用类型 `radical` 实例化名为 `lists` 的泛型包获得，由于其在不同应用中的实用性，我们假设它是可用的与应用程序无关的库单元；`radicals` 的规范在其上下文中被编译。我们在这里不显示它的定义，只是注释说我们假设它导出至少一个名为 `list` 的类型；`head`、`tail` 和 `is_empty` 函数；以及一个 `append` 过程。我们进一步假设 `lists` 初始是空的。还声明了另一个提供链表数组的无约束数组类型，最后声明了两个函数——一个用于分配并返回表示氢自由基的 `radical_node` 类型对象的指针，另一个用于分配并返回表示碳基烷烃的 `radical_node` 类型对象的指针，该烷烃是由指向其子节点的 `radical_node` 类型对象的指针构成的。

`radicals` 包的体如图 17 所示；它包含了在其规范中声明的构建自由基函数的体。这些函数足够简单，不需要解释。

```ada
package body radicals is
function hydrogen_radical return radical is
begin
  return new radical_node' (kind => hydrogen);
end;
function radical_made_from (subradicals : three_radicals)
return radical is
begin
  return new radical_node' (kind => carboniferous,
  carbon_neighbors => subradicals);
end;
```

图 17 - `radicals` 包的体

`molecules` 包的规范如图 18 所示。分子是树，其根节点类型为 `molecule_node`，这是一个记录类型，带有一个判别器，用于指示该节点表示 BCP（有两个子节点）还是 CCP（四个子节点）。`molecule` 类型是一个访问类型，其指定类型为 `molecule_node`；因此，一个分子由指向其根节点的指针表示，其包含指向其子节点的指针等。注意，`molecule_node` 和 `molecule` 类型与 `radical_node` 和 `radical` 类型不同，它们不是递归类型。也就是说，分子的子节点不是分子而是自由基。为了实现与自由基相关的类型的可见性，我们在编译规范时在 `molecules` 的上下文中包含了（即 `with radicals`）。分子的链表通过用类型 `molecule` 实例化之前讨论的 `lists` 泛型包获得。还声明了一个提供分子链表数组的无约束数组类型，最后声明了一个函数——一个用于分配并返回表示 `molecule_node` 类型对象的指针，该对象是由指向其子节点的 `radical_node` 类型对象的指针构成的。

```ada
with radicals, lists;
  use radicals;
package molecule is
  type molecule_kind (kind : bond_centered, carbon_centered);
type molecule_node (kind : molecule_kind) is record
  case kind is
    when bond_centered =>
      bond_neighbors : two_radicals;
    when carbon_centered =>
      carbon_neighbors : four_radicals;
  end case;
end record;
type molecule is access molecule_node;
package molecule_lists is new lists (molecule);
ubtype molecule_list is molecule_lists.list;
type array_of_molecule_list is
  array (positive range <>) of molecule_list;
function molecule_made_from (radicals : array_of_radicals)
  return molecule;
```

图 18 - `molecules` 包的规范

# Ada 47
# 48
# K. W. Dritz

`molecules` 包的体如图 19 所示；它包含了在其规范中声明的构建分子函数的体。它非常简单，不需要解释。

```ada
package body molecule is
function molecule_made_from (radicals : array_of_radicals)
return molecule is
begin
  if radicals'length = 2 then
    return new molecule_node(kind => bond_centered,
      bond_neighbors => radicals);
  else -- Must be 4.
    return new molecule_node(kind => carbon_centered,
      carbon_neighbors => radicals);
  end if;
end;
```

图 19 - `molecules` 包的体

读者应该暂时回到 `paraffin` 的体（图 15）。在 `paraffin` 函数之前的上下文中，`use` 子句的作用是为在 `radicals` 和 `molecules` 中声明的名称提供直接可见性。这些名称包括 `radical_lists` 和 `molecule_lists`，即在 `radicals` 和 `molecules` 中通过实例化 `lists` 获得的包。然而，可见名称并不包括列表操作的操作（`head`、`tail`、`append`、`is_empty`），因为这些操作没有在 `radicals` 或 `molecules` 中声明。第二个 `use` 子句（即函数声明部分中的一个）的作用是为这些操作提供直接可见性。注意 `radical_lists` 和 `molecule_lists` 导出了相同的程序名称。编译器如何知道 `paraffin` 中稍后出现的 `append` 名称来自于这些包中的哪一个？答案是重载 `append` 过程根据调用中实际参数的类型通过重载解析来区分；对 `head`、`tail`、`is_empty` 以及其他调用的也是如此。




## K. W. Dritz

将其附加到解决方案的其他部分。然而，对于 `radical_lists` 和 `molecule_lists` 导出的 `list` 类型，并没有发生这种重载解析；事实上，相同类型名称的这两个出现会相互抵消，在简单的名称 `list` ining 或其子单元中都无法直接看到。这就是为什么我们在基团的规范中将子类型 `radical_list` 声明为与 `radical_lists` 导出的 `list` 类型同义，并在分子的规范中将子类型 `molecule_list` 声明为与 `molecule_lists` 导出的 `list` 类型同义。因此，在 ining 及其子单元中，我们根据情况使用 `radical_list` 或 `molecule_list` 名称，而不是使用歧义的（甚至无法直接看到的）`list` 名称.¹¹1¹

我们现在转向构建石烷基团、BCPs 和 CCPs 的实际工作。

大小为 $i$（$i > 0$）的基团生成方法是：首先列出所有 $i-1$ 的有序、非递减的三元划分。这些划分按自然顺序列举。（例如，7 的有序、非递减三元划分枚举顺序为 (0,0,7), (0,1,6), (0,2,5), (0,3,4), (1,1,5), (1,2,4), (1,3,3), (2,2,3)。）每个划分都提供了需要（按顺序）附加到碳原子上以获得大小为 $i$ 的基团的三个亚基团的大小；由于这些亚基团中任何一个的最大大小均为 $i-1$，可以保证它们在之前已经创建了（记住，基团是按大小顺序创建的）。随着每个划分的列举，我们从属地列举所有具有指定大小的、字典序基团三元组。每个这样的三元组都提供了需要（按顺序）附加到碳原子上以获得大小为 $i$ 的基团的实际亚基团。整个过程按字典顺序生成大小为 $i$ 的基团。

大小为 $i$ 的 CCPs 通过相同的过程生成，但参数不同。首先，我们列举所有 $i-1$ 的有序、非递减的四元划分，其元素的大小不大于 $\lfloor\{\iota - 1\} / 2\rfloor$。每个划分都提供了需要（按顺序）附加到碳原子上以获得大小为 $\iota$ 的 CCP 的四个基团的大小；这些基团保证在之前已经创建了（记住，基团是在分子之前创建的）。随着每个这样的划分的列举，我们从属地列举所有具有指定大小的、字典序基团四元组。每个这样的四元组都提供了需要（按顺序）附加到碳原子上以获得大小为 $\iota$ 的 CCP 的实际基团。

理论上，我们不需要列举划分来获取 $\iota$ 的 BCP 组成基团的大小；因为我们唯一需要的划分是 $(\frac{\iota}{2})$，它可以通过构建其唯一的元素来获得。然而，我们可以重用用于生成基团和 CCPs 的软件组件，通过向它们提供参数来列举所有 $\iota$ 的、具有最小和最大大小均为 $\frac{\iota}{2}$ 元素的有序、非递减划分；当然，这只有一个。该划分提供了需要（按顺序）附加到碳碳键上以获得大小为 $\iota$ 的 BCP 的两个基团的大小。从属地，我们列举所有具有指定大小的字典序基团二元组。每个这样的二元组都提供了需要（按顺序）附加到碳碳键上以获得大小为 $\iota$ 的 BCP 的实际基团。

根据前面的讨论，很清楚我们解决方案的核心组件是一个程序，该程序列举将给定整数划分为给定数量元素的有序非递减划分，每个元素都受到给定最小值和最大值的限制。这表明需要需要四个形式参数。实际上，还需要第五个参数：封装在列举每个划分时应用其上的操作的程序名称（该操作是列举由划分给出的大小的基团元组的操作）。由于目前在 Ada 中只有通过使用泛型单元（generic units）才能实现参数化，我们将划分枚举程序制成了泛型程序。它被称为 `enum_partitions`，其规范如图 20 所示。由于名为 `apply_to_each` 的泛型形式子程序的声明必须提到一种类型——即用于将枚举的划分传递给与 `apply_to_each` 关联的实际子程序的类型——我们将该类型变为另一个泛型形式参数，命名为 `array_type`。通过这样做，划分枚举程序需要是独立的；`apply_to_each` 位于全局作用域中。因此，泛型程序 `enum_partitions` 有四个形式参数。`enum_partitions` 的主体将在稍后显示。

```ada
generic
  type array_type is array () of natural;
  procedure apply_to_each (p : array_type);
procedure enum_partitions (
  sum_of_elements : natural;
  nbr_of_elements : natural;
  min_element     : natural;
  max_element     : natural
) is array_type => array_type;
```
图 20 - 泛型 `enum_partitions` 程序的规范





# Ada

55

```
with enum_partitions;
separate (paraffins)
procedure generate_ccps_of_size (i : in positive) is
  procedure make_and_append_ccp (quad : in four_radicals) is
  begin
    append (molecule_made_from(quad), to => m_array(i));
  end;
  procedure enum_rads_for_ccps is
    new enum_rad_tuples (apply_to_each => make_and_append_ccp);
  procedure enum_partitions_for_ccps is
    new enum_partitions (array_type => array_of_naturals,
      apply_to_each => enum_rads_for_ccps);
  begin
    enum_partitions_for_ccps (sum_of_elements => i-1,
      nbr_of_elements => 4,
      min_element => 0,
      max_element => (i-1)/2);
  end;
```

Figure 22 - generate_ccps_of_sizesize过程的正体

```
with enum_partitions;
separate (paraffins)
procedure generate_bcps_of_size (i : in positive) is
  procedure make_and_append_bcp (pair : in two_radicals) is
  begin
    append (molecule_made_from(pair), to => m_array(i));
  end;
  procedure enum_rads_for_bcps is
    new enum_rad_tuples (apply_to_each => make_and_append_bcp);
  procedure enum_partitions_for_bcps is
    new enum_partitions (array_type => array_of_naturals,
      apply_to_each => enum_rads_for_bcps);
  begin
    enum_partitions_for_bcps (sum_of_elements => i,
      nbr_of_elements => 2,
      min_element => i/2,
      max_element => i/2);
  end;
```

Figure 23 - generate_bcps_of_sizesize过程的正体

我们展示的可执行语句总数仍然少得惊人。我们解决方案大部分的可执行语句可以在泛型过程 `enum_partitions` 和 `enum_rad_tuples` 的主体中找到，这些是我们解决方案中待呈现的所有部分。`enum_partitions` 的主体（如前所述，它被设计为一个与应用程序无关的库单元）如图 24 所示。`enum_partitions` 中的代码：

```
with min_and_max;
procedure enum_partitions (sum_of_elements : in natural;
  nbr_of_elements : in positive;
  min_element : in natural;
  max_element : in natural) is
  package integer_min_and_max is new min_and_max (integer);
  use array (1 .. nbr_of_elements) of
    procedure recursively_partition (level : natural
      constant natural = nbr_of_elements - level;
      remaining_levels : natural;
      prev_element : natural) is
    begin
      if remaining_levels > 0 then
        for element in
          max(remainder - max_element*remaining_levels, prev_element)..
          min(remainder - min_element*remaining_levels,
              remainder / (remaining_levels + 1))
          loop
            p(level) := element;
            recursively_partition (level + 1, remainder - element, element);
          end loop
      else
        p(level) := remainder;
        apply_to_each (p);
      end if;
    end;
  begin
    recursively_partition (1, sum_of_elements, enum_partitions)
  end;
```

Figure 24 - enum_partitions 泛型过程的主体

# Ada 57

虽然较为复杂，但并不深奥。一个内部过程 `recursively_partition` 被调用来分配划分的第一个元素；它递归地调用自己分配后续元素，直到到达最后一个元素。在每个递归层级，它计算¹³ 该层级接受的元素值范围（可能是空的），并循环¹⁴遍历这些值（每个值依次升到下一个更高的层级）。在最高层，当划分被枚举出来时，它将通过参数传递的操作应用于该划分。

剩余的泛型过程 `enum_radtuples`（`paraffins` 的子单元）的正体如图 25 所示。它的结构与 `enum_partitions` 类似。一个内部过程 `recursively_enumerate` 被调用来分配基元组的第一个元素；它递归地调用自己分配后续元素，直到到达最后一个元素。在每个递归层级，它确定该层级可用于分配的基团列表，并循环遍历这些值（每个值升到下一个更高的层级）；该列表是该层级所需尺寸基团的完整列表，除非该层级与上一层级的大小相同，在这种情况下，该列表是上一层列表的剩余部分，从上一层分配的基团开始¹⁵。在最高层，当一个元组被枚举出来时，它将通过参数传递的操作应用于该元组。

最后，值得强调的是，我们构建表示基团和分子的树共享了组件。因此，基团的子基团并不独立于它们自身作为顶级基团的出现，也不独立于子基团的其他出现而占据存储。创建新节点不需要复制被多次指向的子基团。事实上，每个基团都被指向了（见下）：

```
separate (paraffins)
procedure enum_radtuples (p : array_of_naturals) is
  radical_tuple : array_of_radicals (1 .. p'length);
  procedure recursively_enumerate (level : positive;
                               remainder : radical_list;
                               prev_element : natural) is
  levels_radical_list : radical_list;
  begin
    if level = 1 then
      levels_radical_list := remainder;
    else
      levels_radical_list := tail(prev_element);
    end if;
    while not is_empty(levels_radical_list) loop
      radical_tuple(level) := head(levels_radical_list);
      if level < p'length then
        recursively_enumerate (level + 1, tail(levels_radical_list), prev_element);
      else
        apply_to_each (radical_tuple);
      end if;
      levels_radical_list := tail(levels_radical_list);
    end loop;
  end;
begin
  recursively_enumerate (1, array(p), 0);
end;
```

Figure 25 - enum_radtuples 泛型过程的主体

# Ada 59

### 3.2. 并行解决方案

有很多方法可以引入显式并行（如果需要的话），以获得加速。明显而直接的方法是并行执行构建分子的循环（例如通过每个独立的任务），尺寸 $i$ 的基团列表与其他尺寸的列表完全独立。然而，没有必要等待所有基团列表完成后才开始分子列表。由于尺寸 $i$ 的分子涉及不大于 $(i-1)/2$ 的基团，一旦尺寸 $i$ 的基团完成，就可以开始尺寸 $2i$（如果 $i > 0$）和 $2i+1$（如果 $2i < n$）的分子生成。利用这一观察的并行版本函数如图 26 所示。函数声明部分的唯一新增是任务类型 `worker_task` 的规范和存根，其正体见下一图。函数语句列表块语句声明了一个 `worker_task` 类型的数组 `molecule_list_generator`，所有这些任务在继续之前都会等待与 `start_on_size` 的会合。然后块语句按顺序创建基团列表，每完成一个，就信号一个或两个任务开始它们的分子列表；它在该点不等待任务完成。每个任务在完成之前继续进行任何进一步交互。块语句在结尾等待其所有的依赖任务都完成；然后最后执行返回语句。

```task worker_task is
  entry start_on_size (size : in positive);
begin
  loop
    accept start_on_size (size) do
      generate_ccps_of_size (size);
      if size mod 2 = 0 then
        generate_bcps_of_size (size);
      end if;
    end;
  end loop;
end;
```

Figure 27 - worker_task 任务的正体





## 60 K. W. Dritz

我们的程序并不那么适应这一点，但可以想象出一些简单的更改，有助于进一步增强性能。

```ada
with radicals, molecules;
use radicals, molecules;
function paraffins (n : positive) return array_of_molecule_lists is array_of_naturals is array (positive range <>) of natural;
use radicals, molecule_lists;
r_array : array_of_radical_lists (0 .. n/2);
m_array : array_of_molecule_lists (1 .. n);
generic
  with procedure apply_to_each (tuple : in array_of_radicals);
  procedure enum_rad_tuples (p : in array_of_naturals);
  task type worker_task is
    entry start_on_size (i : positive);
  end;
  procedure enum_tuples (p : in array_of_naturals) is separate;
  procedure generate_radicals_of_size (i : positive) is separate;
  procedure generate_ccps_of_size (i : positive) is separate;
  procedure generate_bcps_of_size (i : positive) is separate;
  task body worker_task is separate;
begin
  molecule_list_generator : array (1 .. n) of worker_task;
  begin
    append (hydrogen_radical, to => r_array(0));
    molecule_list_generator(1).start_on_size (1);
    for i in 1 .. n/2 loop
      generate_radicals_of_size (i);
      molecule_list_generator(2*i).start_on_size (2*i);
      if 2*i < n then
        molecule_list_generator(2*i+1).start_on_size (2*i+1);
      end if;
    end loop;
  end;
  return m_array;
end;
```

图 26 - paraffins 函数自说明体（并行版本）

## Ada 61

应用式语言相对于 Ada 有一个明显的优势——即像我们在这里所利用的并行化机会（以及在更微观尺度上的其他机会），是根据当前问题数据流属性允许的程度被隐式且自动地利用。

```ada
separate (paraffins)
task body worker_task is
  my_size : positive;
begin
  accept ccps_of_size (i : positive) do
    my_size := i;
  end;
  generate_ccps_of_size (my_size);
  if my_size mod 2 = 0 then
    generate_bcps_of_size (my_size);
  end if;
end;
```

图 27 - worker_task 任务的正确体

## 4. 诊室问题

给定一组患者、一组医生和一名接待员，该问题是建模以下交互。初始状态，所有患者都是健康的，所有医生都在队列中等待治疗病患。在随机时间，患者会生病并进入队列等待其中一名医生的治疗。接待员处理这两个队列，按照先进先出（FIFO）的方式将患者分配给医生。一旦医生和患者配对成功，医生就会进行诊断疾病，并在随机选择的时间段内治愈患者。然后，医生和患者回到接待台，由接待员记录相关信息。患者被释放，直到其再次生病，而医生返回队列等待另一个患者。可以使用任何分布函数来表示患者的健康时间和医生的治疗时间，但建模医生的代码不能知道患者的分布函数，反亦然，且接待员对两者都不应该。

诊室问题似乎是为 Ada 量身定制的；事实上，解决方案非常简洁，以至于被我们对此讨论完全掩盖了。该解决方案使用一组任务，通过交互方式模拟了问题描述中定义的患者、医生和接待员之间的交互；事实上，有一个接待员任务，并且每个患者和每个医生各有一个任务。在 Ada 中构建模型时遇到了差异；特别是 Ada 允许建模接待员的任务直接响应由患者或医生任务发起的交互，而不考虑哪个先发生。其他一些语言难以异步响应来自不同异构源的信号。

### 4.1. 替代方案的特点

这个问题可以通过两种截然不同的方式解决。可以编写一个“实时程序”，其中通过暂停患者（或在后者的情况下患者和医生）任务与实际时间成正比的长度，来模拟健康和生病周期。或者，可以编写一个“离散事件模拟程序”，其中跳过了到下一个调度“事件”（例如健康期的结束）的时间。在前者，交互任务的大部分时间都花在等待一个延迟或另一个延迟的过期；由于它们通常是同时运行的，整个程序的运行效率非常低。后者要高效得多，因为每当所有任务本应处于等待时，会立即重置为下一个延迟即将到期的时刻。因此，整个程序永远不会处于“等待状态”，其总持续时间不取决于模拟等待的长度，而是取决于模拟的非等待 Ada 事件的数量以及建模每个此类事件所需的计算资源。

这两种方法的共同点是，在任务执行下一个操作之前，需要将它们挂起一段时间。（在实时程序中，任务挂起一段预定的时间；在离散事件模拟中，任务挂起一段无法预知的时间）。因此，从每个任务的逻辑行为来看，两种方法之间的区别很小：任务相互交互，并由于延迟过期或汇合而偶尔挂起。由于任何方法都能充分演示要建模的交互，我们选择了简单的（尽管效率较低的）实时程序方法。离散事件模拟将增加有序队列管理器的复杂性，这对于确定任务之间的交互既不是必要的也不是工具性的。实时程序可以在所有找到 `delay` 语句的地方进行更改，而离散事件模拟仅需通过系统的局部更改并添加有序队列管理器；由于空间限制省略了细节。

问题陈述没有说明诊室建模何时或如何结束；推测，此类细节只会使问题变得复杂。在本质上，我们通过忽略退出问题简化了解决方案；建模的交互持续进行。当然，退出可以在之后设计。

### 4.2. 解决方案的结构

这里提出的解决方案以名为 `doctors_office` 的通用过程的形式存在。该通用过程由两个函数参数化，这些函数是随机生成器，用于选择每个患者享受的健康时长以及中间的随机诊断和治愈时长（一旦患者分配给医生）。通用过程的规范如图 28 所示。要使用此机制，需要实例化通用过程并提供随机生成器的名称，以获得一个非通用的过程，然后用两个代表患者和医生数量的实际参数调用它。

```ada
generic
  with function random_healthy_period return duration;
  with function random_treatment_period return duration;
procedure doctors_office (number_of_patients : in natural;
                         number_of_doctors : in natural);
```

图 28 - doctors_office 通用过程的规范

在解决方案中，我们使用预定义的固定点类型 `duration` 作为随机生成器的结果，因为这是 `delay` 语句的操作数所需的类型。我们使用预定义整数类型的预定义子类型 `natural` 表示患者和医生的数量。通用过程的体如图 29 所示。任务类型 `patient_task` 和 `doctor_task` 以及单个任务 `receptionist` 的体由体存根持有，其对应的正体将在稍后显示。





# Ada

65

```ada
procedure doctors_office (number_of_patients : in natural;
number_of_doctors : in natural) is
task type patient_task;
type doctor_task;
type doctor is access doctor_task;
task type doctor_task is
  entry identify_self (myself : in doctor);
  entry patient_visiting_for_treatment;
end;
task receptionist is
  entry patient_becoming_patient (d1 : in doctor);
  entry patient_requesting_doctor (d2 : out doctor);
end;
patient : array (1 .. number_of_patients) of patient_task;
new_doctor : doctor;
task body patient_task is separate;
task body doctor_task is separate;
task body receptionist is separate;
begin
  for i in 1 .. number_of_doctors loop
    new_doctor := new doctor_task;
    new_doctor.identify_self (new_doctor);
  end loop;
end;
```

图 29 - doctors_office 泛型过程的主体

注意患者集合的集合方式与医生集合的集合方式不同。在我们的解决方案中，患者执行入口调用¹⁷ 但不需要接受这些调用；由于没有任务请求患者的入口，因此任何单个患者的身份都不会被需要。分配所需数量患者最简单且直接的方法是声明一个具有适当边界的 `patient_tasks` 数组；该数组的被订阅组件从未被引用。相反，医生既执行也接受入口调用，因此有需要识别单个医生。我们选择通过单独逐一分配每个医生来识别它们，获取指向新分配的 `doctor_task` 的指针，然后将该值传递给任务本身（通过其 `identify_self` 入口），将其保存在任务本地变量中；在外部不保留所有医生的集合记录，因为不需要。当医生变得空闲并请求一个患者进行治疗时，它会将自己的身份传递给接待员。只有当某个患者生病时，接待员才会接受来自医生的此类调用，此时它会将医生的身份传递给患者，患者与医生交互以接受治疗。

在对所有医生进行分配和初始化后，所有后续操作都发生在 `doctors_office` 的依赖任务内部；因此，在返回给调用者之前，`doctors_office` 等待（在其结束处）所有依赖任务终止。由于它们永远不会终止，在此实现中，`doctors_office` 永远不会返回。

### 4.3. 患者的行为

实现患者行为的代码如图 30 所示。患者的行为非常简单。患者重复地享受一段随机的健康期，检查接待员（宣布生病），向接待员请求医生的服务，在有医生可用时被分配一名医生，并拜访医生接受治疗。

```ada
separate (doctors_office)
task body patient_task is
  assigned_doctor : doctor;
begin
  loop
    delay random_healthy_period;
    receptionist.patient_becoming_sick;
    receptionist.patient_requesting_doctor (assigned_doctor);
    assigned_doctor.patient_visiting_for_treatment;
  end loop;
end;
```

> 图 30 - patient_task 任务类型的正确主体

问题描述中说，在治愈后，患者和医生应返回接待员；患者在此处没有这样做，仅仅是因为在那个点，接待员不需要代表患者采取任何相关操作（影响医生或患者）。取决于对接待员的记录保存的要求，与其进行额外的交互可能是理想的。

正如我们在检查接待员的详细行为时将看到的，患者向接待员通报生病的调用不会导致患者无限挂起；它可能会导致短暂的挂起（即，如果接待员当前正忙碌），类似于等待监视器锁。需要注意的是，接待员的设计使得它在每次通过其循环时，都都能接收来自患者对其 `patient_becoming_sick` 入口的调用。另一方面，患者在随后的立即调用接待员的 `patient_requesting_doctor` 入口时，很有可能会被挂起，因为接待员可能处于处于正在执行（或可以执行）该入口的 `accept` 语句的状态。医生的可用是执行该 `accept` 语句的前提条件。最终，一个医生将变得空闲来治疗患者（患者挂起不仅是直到医生可用，而且直到患者之前对医生的所有请求都得到满足），此时患者对 `patient_requesting_doctor` 的入口调用将导致与接待员的会合，接待员将把可用医生的身份传递给患者。在完成与接待员的 `patient_requesting_doctor` 会合后，患者将直接调用分配的医生的 `patient_visiting_for_treatment` 入口，在会合中保持挂起直到治疗完成。

### 4.4. 医生的行为

实现医生行为的代码如图 31 所示。医生在接收并存储自己的身份后，重复的行为是向接待员宣布其治疗患者的可用性，然后（一旦有患者来寻求治疗）以耗费随机时间的治疗的形式提供服务。问题描述说，医生（以及其患者）在治疗结束时返回接待员；至少医生返回接待员的行为我们的解决方案得到了充分的建模，因为在治疗患者后向接待员信号其再次空闲。

```ada
separate (doctors_office)
task body doctor_task is
  self : doctor;
begin
  accept identify_self (myself : doctor) do
    self := myself;
  end;
  loop
    receptionist.doctor_requesting_patient (self);
    accept patient_visiting_for_treatment do
      delay random_treatment_period;
    end;
  end loop;
end;
```

图 31 - doctor_task 任务类型的正确主体

正如我们在检查接待员的详细行为时将看到的，医生在调用接待员请求患者时很有可能会挂起，因为接待员并不总是接收此类调用；这发生在没有患者生病时，它是所需行为的重要组成部分。最终，患者会到来（医生挂起不仅直到患者出现，而且直到医生对患者的所有请求都得到满足），此时医生的 `doctor_requesting_patient` 入口调用将导致与接待员的会合，接待员将接收医生的身份。接待员将该身份传递给患者（在对应的 `patient_visiting_for_treatment` 入口）。因此，在完成与接待员的会合后，医生将无延迟地治疗患者。

### 4.5. 接待员的行为

实现接待员的行为如图 32 所示。接待员的行为微妙但直接。接待员重复地只是等待并处理患者生病的通知或空闲医生对治疗患者的请求。接待员在每次通过循环时处理一个患者的通知或医生的请求，在必要时等待其到达。它总是接收通知，但只有在满足某些条件时才接收请求。具体而言，只有在有可用患者满足请求时（即，只有当患者生病时），它才会接受医生对治疗患者的请求。如果在循环的某次迭代中没有患者等待治疗，那么接待员将保持挂起直到收到生病患者的通知，即使此时存在医生对治疗患者的未处理请求。





## K. W. Dritz

对两个入口调用的等待通过在循环内部编写选择性等待（selective wait）来实现。此外，选择性等待的两个接受备选方案中的第二个受到了保护，以确保在循环的某些迭代中（特别是那些保护条件为假的迭代），对受保护入口的调用将不会被接受并将保持在队列中。当保护条件为真时（即第二个选择性等待备选方案“开放”，且对两个入口的调用都已经发出），则任何一个入口调用都可以被接受；未被接受的那个将保持挂起状态，并在选择性等待的后续执行（即循环的后续迭代）中被接受。逻辑行为和程序的正确性对这种选择的不确定性并不敏感，这让我们确信正在使用恰好的特性。

```ada
separate (doctors_office)
task body receptionist is
  sick_patients : natural := 0;
begin
  select
    accept patient_becoming_sick;
      sick_patients := sick_patients + 1;
  or
    when sick_patients > 0 =>
      accept doctor_requesting_patient (d1 : in doctor) do
        accept patient_requesting_doctor (d2 : out doctor) do
          d2 := d1;
      end;
      sick_patients := sick_patients - 1;
  select;
end loop;
end;
```

图 32 - 接待员任务的正确主体

需要注意的是，选择性等待中只需要代表两个通道的两个选择性等待备选方案，而不是为每个医生和每个患者都准备一个。接待员以相同的方式处理与所有医生的交互，与所有患者的交互也是如此。这两个选择性等待备选方案用于区分其他任务可能与接待员交互的两个原因，而不是为了识别交互的任务身份。当需要医生的身份时，该身份将由医生在交互过程中作为数据传递。

如果有多个患者生病并请求医生，他们的入口调用将由 Ada 以先先出（FIFO）的顺序保持在队列中，每当执行一次对入口的 `accept` 语句时，就会从 `patient_requesting_doctor` 入口的队列中取出一个调用。因此，患者按照问题描述中要求的请求医生的顺序被处理。同样，如果多个医生试图从接待员处请求患者，他们的调用将由 Ada 以 FIFO 顺序保持在队列中，每当执行一次对入口的 `accept` 语句时，就会从 `doctor_requesting_patient` 入口的队列中取出一个调用。问题描述没有指定多个可用医生中的哪一个应该治疗患者，因此我们对可用医生进行的 FIFO 分配只是许多可行方法之一；这种分配是最容易提供的，因为是免费的。注意，此问题所需的所有队列操作都是由 Ada 隐式完成的，不需要显式地维护任何队列。

当接待员接受来自请求患者的医生的入口调用时（仅在已知患者生病时才会这样做），并且仍在与医生进行会会（rendezvous），它也会接受来自请求医生的患者的入口调用（与其会会）。因此，接待员充当了中介，信息——可用医生的身份——通过它传递给患者。请注意，如果接待员在不知道患者生病的情况下接受了可用医生的入口调用（例如，如果第二个等待没有受保护），那么接待员可能会在 `patient_requesting_doctor` 的 `accept` 语句处挂起，而且如果没有患者生病（即没有患者任务调用该入口），它确实会挂起。虽然这达到了让请求患者的医生在没有患者生病时挂起的预期效果，但该请求永远无法满足，因为接待员无法记录患者的生病。事实上，程序将死锁。在第二个选择性等待上使用保护条件避免了这一点，同时在没有患者生病时仍让请求患者的医生挂起。

总之，接待员任务的特点是包含一个带有选择性等待的循环，允许任务反复地等待并响应多个备选事件中的任何一个。使用保护条件（Guards）使其对某些事件的发生不接受，同时保持对其他事件的接受；而后者的事实决定了其对前者的接受性。这是 Ada 中一种常见且重要的任务范式。值得注意的是接待员任务中嵌套的 `accept` 语句的使用，这说明了通过任务构造的适当耦合可以实现的威力。

## 5. 天线矩阵问题

该问题是求解矩阵方程 $Ax = b$，其中 $A$ 是阶数为 $n$ 的天线矩阵（skyline matrix），$x$ 和 $b$ 是阶数为 $n$ 的向量。天线矩阵是方阵，其次对角线行具有不同数量的前导零，它们的特殊结构暗示了使用“锯齿数组”（ragged arrays）——即行或列边界不相同的二维数组。该问题的主要目的是测试该语言是否具有锯齿数组。

我们使用 Doolittle 的 LU 分解法（Crout 方法的变体，其中 $U$ 是单位三角矩阵）来解决这个问题。

### 5.1. 普通矩阵的解

我们在图 33 中给出名为 `matrices` 的通用包的规范，它导入了一个浮点类型和一个正数 $n$，并导出了阶数为 $n$ 的向量和矩阵的类型及子程序（分别称为 `n_vector` 和 `nxn_matrix`），其组件为给定的浮点类型。导出的函数 `solve` 解决了矩阵问题。为了获得不同大小的矩阵，需要该包的不同实例化。通过仅为二维数组定义无约束类型，可以避免多次实例化的需要，要求用户在对象声明中提供适当的边界。

```ada
generic
type float_type is digits nn : in positive;
package matrices is
  type vector is array (positive range <>) of float_type;
  subtype n_vector is vector (1 .. n);
  type nxn_matrix is array (1 .. n, 1 .. n) of float_type;
  function row (row_index : positive;
    of_matrix : nxn_matrix;
    from : positive;
    to : natural) return vector;
  function col (col_index : positive;
    of_matrix : nxn_matrix;
    from : positive;
    to : natural) return vector;
  function "*" (left, right : vector) return float_type;
  function solve (a : nxn_matrix; b : n_vector) return n_vector;
end;
```

图 33 - `matrices` 通用包的规范





# Ada

通过为这些数组提供受限类型或子类型，我们消除了检查边界匹配的需求从而简化了代码。我们为一维数组提供了一个无约束类型（命名为 `vector`），作为 `row` 和 `col` 函数的结果类型（这两个函数分别返回部分行和列），以及 `*`（内积）运算符的操作数类型（该运算符接受部分行和列作为操作数）。我们没有使用原始类型，因为我们希望用户能够利用 `nx_matrix` 是二维数组这一事实——例如，通过普通的下标表示法来引用此类对象的组件。此外，辅助的 `row` 和 `col` 函数以及仅供 `solve` 函数使用的 `*` 运算符本可以定义在 `matrices` 的体中；但我们在它的规范中定义了它们，因为它们可能在用户的应用程序其他地方有用。

`matrices` 的体如图 34 所示。辅助函数的完整体已包含在内，但 `solve` 函数体体较大，在这里仅由一个体占位符表示，其正体将在下一张图中。

`row` 和 `col` 函数被设计为返回部分行或部分列，从位置 `from` 扩展到位置 `to`。（注意：Ada 允许空数组——即没有组件的数组；当 `to < from` 时，`row` 和 `col` 返回空向量，正如我们在 Doolittle 方法的实现中多处所做。）在实现向量 `*`（内积）运算符的函数中，为了演示方便，隐含地假设两个操作数 `left` 和 `right` 是相同的。两个空向量的内积定义为零。

```ada
package body matrices is is
function row (row_index : positive;
  of_matrix : nxn_matrix;
  from : positive;
  to : natural) return vector is
  result : vector (from .. to);
begin
  for i in from .. to loop
    result(i) := of_matrix(row_index,i);
  end loop
  return result;
end;
function col (col_index : positive;
  of_matrix : nxn_matrix;
  from : positive;
  to : natural) return vector is
  result : vector (from .. to);
begin
  for i in from .. to loop
    result(i) := of_matrix(i,col_index);
  end loop
  return result;
end;
function "*" (left, right : vector) return float_type is
  sum : float_type := 0.0;
begin
  for i in left'range loop
    sum := sum + left(i) * right(i);
  end loop
  return sum;
end;
function solve (a : nxn_matrix;
  b : n_vector) return n_vector is separate;
end;
```

图 34 - matrices 通用包的体

Doolittle 方法的核心显然位于 `solve` 函数中，其正体如图 35 所示。与往常一样，形状为下三角和上三角的 `l` 和 `u` 矩阵共享一个 $n$ 阶矩阵 `lu` 的存储空间。（`l` 和 `u` 的名称都与 `lu` 别名，在算法中仅起说明性作用。）`u` 的对角线是 `lu` 的对角线；`l` 是单位三角，其对角线全为 1 且不存储。三角形 `l` 和 `u` 在我们版本的 Doolittle 方法的分解步骤中计算，通过交替填充不断增高的 `l` 行和 `u` 列来完成。注意看对部分行和部分列使用简单抽象以及对内积使用熟悉的表示法如何使得算法的表达变得清晰简洁。为了演示方便，此处未提供奇异性测试，也没有为奇异性做任何处理。

```ada
separate (matrices)
function solve (a : nxn_matrix; b : n_vector) return n_vector is
  x, y : n_vector;
  lu : nxn_matrix;
  l : nxn_matrix renames lu;
  u : nxn_matrix renames lu;
begin
  -- 分解步骤 (计算 l 和 u)。
  for i in 1 .. n loop
    for j in 1 .. i-1 loop
      l(i,j) := (a(i,j) - row(i,l,1,j-1) * col(j,u,1,j-1)) / u(j,j);
    end loop;
    for j in 1 .. i loop
      u(j,i) := a(j,i) - row(j,l,1,j-1) * col(i,u,1,j-1);
    end loop;
  -- 前向替换步骤 (计算 y)。
  for i in 1 .. n loop
    y(i) := b(i) - row(i,l,1,i-1) * y(1..i-1);
  end loop;
  -- 后向替换步骤 (计算 x)。
  for i in reverse 1 .. n loop
    x(i) := (y(i) - row(i,u,i+1,n) * x(i+1..n)) / u(i,i);
  end loop;
  -- 返回结果。
  return x;
end;
```

图 35 - 矩阵矩阵 `solve` 函数的正体

## Ada 77

应当指出，`nx_matrix` 类型本可以是边界为 `1..n` 的一维数组（完全准确地说，我们应该说它们是二维数组的一维截面的记录）。通过对列向量使用切片符号（slicing notation），可以很容易获取部分列。例如，后向替换步骤中需要的行始终延伸到行的末尾，即 `u(i..n)`。

### 5.2. Skyline 矩阵的求解

普通矩阵的解现在被修改为利用 Skyline 矩阵（天际线矩阵）的特殊属性。首先，我们将通用包替换为名为 `skyline_matrices` 的包，其规范如图 36 所示。我们现在不再使用 `nxn_matrix` 类型，而是定义了一个 `nxn_skyline_matrix` 类型，它是包含两个组件的记录，每个组件都是一个指针数组：`lower` 组件是一个指向下三角行指针的向量（vector），而 `upper` 组件是一个指向上三角列指针的向量。

我们舍弃了 `col` 函数，并对 `row` 函数进行了简要简化（即通过更改其参数）。我们不再需要 `col` 函数，因为我们需要引用的所有列都在上三角中，而且现在它们只是一维数组，而不是二维数组的一维截面（完全准确地说，我们应该说它们是包含一维数组的记录）。遗憾的是，Doolittle 方法中引用的行并不是都是下三角；如果是的话，我们可以出于类似原因取消 `row` 函数。后向替换步骤引用 `u` 的行。该行跨越了代表 `lu` 上三角的列向量，其某些组件可能位于 `lu` 的 Skyline 包之外。因此，保留 `row` 仅是为了从上三角中提取行，并针对该目标进行了专门。由于 `row` 被要求从 Skyline 矩阵的上三角中提取行，我们不再向它传递整个 Skyline 矩阵；我们只需传递代表其列的指针向量即可。我们不再需要作为参数传递行的上边界。

每个行或列都由 `bounded_vector` 类型的对象表示，该类型是一个包含一个组件 `e` 和两个判别符 `lo, hi` 的记录。组件 `e` 是一个无约束数组（其定义未变），受 `lo` 和 `hi` 边界的限制——因此每个对象在包含向量的边界方面都是自描述的。边界在分配对象时提供，并在对象的整个生命周期内保持不变。

现在转向 `skyline_matrices` 的体（图 37），我们注意到它与前身相比的以下变化：


80

K. W. Dritz

# generic

```
```
```

图 36 - skyline_matrices 泛型包的规范

- row 函数的主体返回一个行向量，其中每个位置都包含天际线矩阵的一个分量，其上三角部分作为参数传递（如果在天际线包络内）或为零（如果在包络外）。如果该向量位于任一端，其边界可以缩短，但这种优化似乎并不划算。
- *** 运算符（内点积函数）现在可以接收一对长度不同的向量；由于缺失的分量为零，它们对内积没有贡献，且循环可以从两个向量下界的较较大值扩展到它们上界的较小值。

```
with min_and_max;
package body skyline_matrices is
  package natural_min_and_max is new min_and_max (natural);
use
  natural_min_and_max;
  function row (row_index : positive;
    of_cols : vector_ptrs;
    from : positive) return vector is
  result : vector (from .. n);
begin
  for i in from .. n loop
    if row_index >= of_cols(i).lo then
      result(i) := of_cols(i).e(row_index);
    else
      result(i) := 0.0;
    end if;
  end loop;
  return result;
end;
function "*" (left, right : vector) return float_type is
  sum : float_type := 0.0;
begin
  for i in max(left_first, right_first) ..
    min(left_last, right_last) loop
    sum := sum + left(i) * right(i);
  end loop;
  return sum;
end;
function solve (a : nxn_skyline_matrix;
  b : n_vector) return n_vector is separate;
```

图 37 - skyline_matrices 泛型包的主体

solve 函数的修订后的主体如图 38 所示。一个微小的变化是 l 和 u 现在分别与 lu 的下三角和上三角部分同名，而不是像之前那样与整个 lu 对象同名。这简化了我们为了表示 lu 的分量、行或列而要求的表达式（例如，我们写 l(i).e(j) 来表示 lu 下三角的第 (i, j) 分量）。

# 82 K. W. Dritz

可以为 a 的下三角和上三角提供类似的重命名声明，但 solve 中对 a 的引用很少，因此节省的开销并不显著。solve 函数包含了两个之前要求的步骤：一个是在分解步骤中填充之前分配局部 lu 天际线矩阵的行和列，另一个是在返回结果之前释放内存。根据 Doolittle 方法，lu 的天际线包络与 a 的包络是相同的。因此，我们分配 lu 的第 i 行使其具有与 a 的第 i 列相同的下界，且上界为 i-1（记住下三角在对角线稍处就停止了）；同样，我们分配 lu 的第 i 列使其具有与 a 的第 i 列相同的下界，且上界为 i（上三角包含对角线）。

在分解步骤中，我们看到两个内部循环现在从正在填充的行或列的第一个非零分量的索引开始，而不是从 1 开始，因为前面的分量（天际线包络之外的分量）不存在。回代步骤包含了对 row 函数最后的引用。

我们对天际线矩阵的解决方案显然通过不存储天际线矩阵包络外的零节省了空间。它通过不计算这些零节省了时间。惊讶的是，它在另一个方面也比普通矩阵的解决方案更高效：它调用更少的子程序来获取（部分）行或列，并在此拷贝更少的数据。

# Ada

# 83

```
with unchecked_deallocation;
separate (skyline_matrices)
function solve (a : nxn_skyline_matrix;
    b : n_vector) return n_vector is
  x, y : n_vector;
  lu : nxn_skyline_matrix;
  l1 : vector_ptrs renames lu.lower;
  u : vector_ptrs renames lu.upper;
  procedure free is
    begin
    new unchecked_deallocation (bounded_vector, vector__ptr);
    for i in 1 .. n loop
        l1(i) := new bounded_vector (lo => lower(i).lo, hi => i-1);
        u(i) := new bounded_vector (lo => upper(i).lo, hi => i);
    end loop;
    -- Factorization step (compute l1 and u)
    for i in 1 .. n loop
        for j in l1(i).lo .. i loop
            l1(i).e(j) := (a.lower(i).e(j) - l1(i).e(i).lo..j-1) * u(j).e(u(j).lo..j-1)) / u(j).e(j);
        end loop;
        for j in u(i).lo .. n loop
            u(i).e(j) := a.upper(i).e(j) - l1(j).e(j).lo..j-1) * u(j).e(u(j).lo..j-1)) / u(j).e(j);
        end loop;
```
（注：此处原文包含大量 OCR 识别错误和重复逻辑，翻译时已根据上下文逻辑进行了处理，去除了乱码部分）

# 94

K. W. Dritz

solve 函数的修订后的主体如图 38 所示。一个微小的变化是 l 和 u 现在分别与 lu 的下三角和上三角部分同名，而不是像之前那样与整个 lu 对象同名。这简化了我们为了表示 lu 的分量、行或列而要求的表达式（例如，我们写 l(i).e(j) 来表示 lu 下三角的第 (i, j) 分量）。可以为 a 的下三角和上三角提供类似的重命名声明，但 solve 中对 a 的引用很少，因此节省的开销并不显著。solve 函数包含了两个之前要求的步骤：一个是在分解步骤中填充之前分配局部 lu 天际线矩阵的行和列，另一个是在返回结果之前释放内存。根据 Doolittle 方法，lu 的天际线包络与 a 的包络是相同的。因此，我们分配 lu 的第 i 行使其具有与 a 的第 i 列相同的下界，且上界为 i-1（记住下三角在对角线稍处就停止了）；同样，我们分配 lu 的第 i 列使其具有与 a 的第 i 列相同的下界，且上界为 i（上三角包含对角线）。

在分解步骤中，我们看到两个内部循环现在从正在填充的行或列的第一个非零分量的索引开始，而不是从 1 开始，因为前面的分量（天际线包络之外的分量）不存在。回代步骤包含了对 row 函数最后的引用。

我们对天际线矩阵的解决方案显然通过不存储天际线包络外的零节省了空间。它通过不计算这些零节省了时间。惊讶的是，它在另一个方面也比普通矩阵的解决方案更高效：它调用更少的子程序来获取（部分）行或列，并在此拷贝更少的数据。

# Ada

# 85

天际线情况下，在第一次尝试向分量存储非零值时，分配行（如果分量在下三角）或列（如果在上三角）的责任——（注意在 Ada 中指针被初始化为 null，这使得很容易检测到行或列已分配）。与此结合，row 和 col 函数必须准备好在参数行或列尚未分配时返回空数组。虽然分配行和列的责任可以构建在与矩阵类型导出的分量存储过程中，但没有方法可以处理矩阵行和列（在天际线情况下）的“自动”释放并离开矩阵对象声明的作用域。当然，Ada 允许此类动态分配的存储自动回收（在这种情况下，当 solve 返回时）；这在 Ada 中并没有通常实现。如果不是显式释放；但正如我们在本章前面提到的，需要这种垃圾收集，一个释放矩阵的程序可以与类型一起导出，并在 solve 返回之前导入并调用。对于普通矩阵，释放程序将将什么都不做，而对于天际线矩阵，它将具有图 38 所示的行为。如果我们愿意与矩阵类型导出额外的操作，实际上可以节省计算并然后丢弃天际线包络外零的开销。


外络线（在 skyline 情况下）。1 和 $u$ 的行和列仍然由上述讨论的组件存储过程进行分配。因此，在分解步骤中，我们不会请求 $lu$ 的行和列的下界（因为它们尚未被分配）；相反，我们会请求 $a$ 的行和列的下界。对于正规矩阵的情况，当然，这些查询函数将被设计为始终返回 1。显然，作为可重用抽象的一部分，此类函数并不十分优雅，但它们确实允许我们在 skyline 情况下保留一些速度优势。

最后，在 `matrices` 单元中，矩阵类型真的应该被声明为 `limited private`（受限私有），而不仅仅是 `private`。赋值操作和预定义的相等比较操作是为 `private` 类型隐式声明的少数操作，它们在 `limited` 类型中是不隐式声明的，且这些操作对我们可能非常重要。当在抽象的实现中使用指针时，我们需要确定赋值和相等比较是否有意义。在我们的情况下，它们没有意义。将一个 skyline 矩阵赋值给另一个将只会拷贝包含的指针值；而不会复制行和列；因此，目标将与源值的行和列相同。因为源的行和列在赋值后，其其一的变化会影响另一个。同理，两个具有不同但相等的行列的 skyline 矩阵将不相等，因为预定义的相等比较操作只会比较指针值。在某些应用中，存储共享是期望的，但在这里不需要。在可重用的抽象中，抑制无意义操作的隐式声明非常重要，这样抽象就不会被误用。在 `matrices` 中将矩阵类型声明为 `limited private` 将实现这一点。（在第 5.2 节中，我们没有担心不将矩阵类型设置为 `limited` 的风险，因为正如我们在那里所说的，我们特别希望用户能够利用对其实实现的了解，这要求我们放弃使用 `private` 类型，因此也放弃了 `limited` 类型；我们含蓄假设用户不会通过例如赋值或比较 skyline 矩阵来误用这些知识。）尽管在 `solve` 中不需要矩阵的赋值和相等比较，但如果 `matrices` 的设计者真的打算让两个版本在各种应用程序中被重用，那么设计者就不应做出这样的假设。因此，`matrices` 的设计者将被通过子程序或运算符重载，显式地提供这些操作作为矩阵抽象的一部分；当然，`matrices` 的设计者也可以确保这些操作在 skyline 情况下具有预期的行为。这些考虑决定了 `solve` 导入矩阵类型时使用的通用形式类型必须声明为 `limited private`，但这是可能的，因为 `solve` 不需要矩阵类型的赋值操作或预定义的相等比较操作。

# 致谢

本章的准备工作由美国国防部战略防御计划组织（Strategic Defense Initiative Organization）支持，项目编号为 PMA E2304。

# 脚注

- 1. 任务无法进行参数化的特性在相似任务被聚合到数组中并设置为处理问题的不同部分时尤为有用——这是我们在随后的几个问题解决方案中反复采用的策略。目前，必须使用汇会机制（rendezvous mechanism）与任务进行通信，以给它们一些自己的“身份”。对于 Ada 9X，已经提出了用于任务参数化的机制；这些机制有望消除我们解决方案中的部分任务通信，从而简化它们。

- 2. 这是一个简化的处理，但对于本引言来说是恰当的。

- 3. 在我们的代码示例中，Ada 关键字（即保留字）将加粗。这将很好地将它们与标识符区分开来，且两者都可以小写。出现在普通正文中的 Ada 关键字也将加粗——每当认为某种标点符号合适时如此。

- 4. 我们所说的“可重用”是指尽可能通用，以便它可以被用于各种需要相同通用行为的应用程序，而不论无关细节的差异。在 Ada 中，重用性主要通过通用单元（generic units）特别是通用包（generic packages）的定义和实例化来实现。任意类型的流是可重用抽象的明显候选者；尽管流中包含的值类型可能会随着不同的应用程序而变化，甚至可能随着单个应用程序中不同的流而变化，但对流的操作是独立于该类型的。我们刻意不显示如何在 Ada 中编写一个通用的 "streams" 包，因为很可能在一个成熟的工作环境中，设计解决 Hamming 问题的程序员会发现，之前有人曾对流抽象的需求，并且一个导出所需类型和操作（可能具有与我们使用的不同的名称）的通用包已经存在于本地库中。这样的库可以被认为是是对语言的扩展。

- 5. 本章中使用的所有被“假设存在”的库单元实际上都是为了测试解决方案而编写并使用的。

- 6. 我们对 Hamming 问题的解决方案中使用和生成的所有整数值都大于零，但对于无约束数组类型 `positive_array` 对象的下标，没有做出这种正数的假设（因为这不是强制要求的）。因此，正如我们所做的那样，使用子类型 `positive` 而不是 `integer` 类型作为我们所有的变量或其组件是恰当的；这样做增加了程序的安全性，作为结果，过程 `solver` 无法被带有具有非正值的标量实际参数或具有非正值组件的复合实际参数进行调用，如果允许这样做，这将导致模糊的失败。我们最大限程度地应用了这一推理，尽管实际上，只需通过将 `solver` 的形式参数声明为（或具有）子类型 `positive`，并将将其他每一个整数变量或组件（包括流的组件）声明为 `integer` 类型，就可以实现必要的安全性。（由于我们可以证明，如果调用 `solve` 的实际参数或其组件都是正数，那么解决方案产生的所有整数值都将是正数。）

- 7. 在数据流属性的范围内，不同的运行顺序显然是由计算负载的概率特性引起的。

- 8. 很好，几乎如此；其中一个将执行 `min_finder`。

- 9. 实际上，Ada 允许隐式垃圾回收，但它提供了显式释放分配存储的机制。如果我们发现垃圾回收被常规实现，我们可能会受到按照 Turner 的精神获得一个解决方案；实际上，它在 Ada 系统很少被实现。

- 10. 我们的字典序排序是：如果第一个小于第二个，或者它们的大小相同且第一个在相同大小的半径列表中出现不晚于第二个，则它们是字典序的。

- 11. 实际上，在这些地方使用的任何一个名称仅位于通用过程 `enum_rad_tuples` 的适当正文中，它是 `paraffin` 的一个子单元；参见图 25。

- 12. 这个无约束数组类型在父单元 `paraffin` 中声明。我们在上一个段中解释了 `enum_partitions` 如何被赋予通用形式 `array_type`，并在这里与 `array_of_naturals` 关联。另一个通用过程 `enum_rad_tuples` 同样需要 `array_of_naturals`；然而，由于该通用过程本身就是针对特定问题的，并且因如此嵌套在 `paraffin` 内部，它通过嵌套获得了 `array_of_naturals` 的可见性，而不需要通过通用参数关联导入 `array_of_naturals`。

- 13. 此计算需要 `min` 和 `max` 函数，这些函数是通过对解决 Hamming 问题中使用的相同的应用程序无关通用库包 `min_and_max` 使用预定义类型 `integer` 进行通用实例化得到的。


integer 被用作通用实际参数，而不是它的子类型（如 positive 或 natural），因为当前 `min` 和 `max` 调用中的中的参数表达式可能会产生负值。

+   14. 递归每一层中的循环与某些解决方案中发现的静态嵌套循环以及缺乏递归的情况形成了对比；它的优势在于能够模拟任意层次的嵌套。当然，这种策略的动机是编写一个单一通用过程，以适用于该问题所需的二分、三分和四分划分。

+   15. 这是交付字典顺序排序根数元组的需求所导致的一个微妙结果。

+   16. 诚然，这种策略没有良好的负载均衡特性。可以使用更少的任务来完成，因为在另一个任务创建大尺寸分子列表的时间内，一个任务可以顺序创建多个小尺寸的分子列表。

+   17. 为了在本节剩余部分方便，当我们使用相同的词指代我们的程序单元时，将 `patient_task` 类型的对象称为“patients”，将 `doctor_task` 类型的对象称为“doctors”，将唯一的接待员任务称为“receptionist”。我们偶尔也使用相同的词来指代我们建模的人，例如在讨论问题描述时。

+   18. 1988 年会议期间演示的解决方案要简单得多；它确实包含了显式的出队操作（dequeing）。

+   19. 由于无法定义具有非驻留步长的数组，因此提供横截的最接近的方法是定义一个函数，通过将矩阵的分量拷贝到单位步长向量中来返回矩阵的（部分）行或列。幸运的是，这在这里足够了。

+   20. 除了一个给定矩阵及其分量索引获取矩阵分量的函数外，矩阵抽象还必须提供一个存储到矩阵分量的过程——给定矩阵、其分量索引以及要存储的值。

## Ada 91

21. Ada 9X 可能会引入对象或类型的“终结化”（finalization），这将优雅地解决此问题。

## 参考文献

+   1. Ada 9X Project. Ada 9X Requirements. Office of the Under Secretary-of Defense for Acquisition, Washington, D.C., January 1990.

+   2. Booch, G. Software Engineering with Ada. Benjamin/Cummings, Menlo Park, CA, 2nd Edition, 1987.

+   3. Cohen, N. H. Ada as a Second Language. McGraw-Hill, 1986.

+   4. Fox, L. An Introduction to Numerical Linear Algebra. Clarendon Press, Oxford, 1964.

+   5. Habermann, A. N. and I. R. Nassi. Efficient Implementation of Ada Tasks. CMU Report CMU-CS-80-103; Carnegie Mellon University, Pittsburgh, PA, January 1980.

+   6. Hoare, C. A. R. Monitors: An Operating System Structuring Concept. Communications of the ACM, 17(10):549–557, October 1974.

+   7. Hoare, C. A. R. Communicating Sequential Processes. Communications of the ACM, 21(8):666–667, August 1978.

+   8. Knuth, D. E. The Art of Computer Programming, Volume I. Addison-Wesley, 1968.

+   9. McGraw, J. et al. SISAL: Streams and Iteration in a Single-Assignment Language, Language Reference Manual, Version 1.1, LLNL Report M-146, Lawrence Livermore National Laboratory, Livermore, CA, July 1983.

+   10. Turner, D. A. Semantic Elegance of Algebraic. In Proc. Conf. on Functional Programming Languages and Computer Architecture, Portsmouth, NH, October 1981, 85–92.

+   11. U.S. Department of Defense. Requirements for High Order Programming Languages, Steelman. U.S. Government Printing Office, Washington, D.C., June 1978.

+   12. U.S. Department of Defense, Ada Joint Program Office. Reference Manual for the Ada Programming Language, ANSI/MIL-STD-1815A. U.S. Government Printing Office, Washington, D.C., 1983 (adopted by ISO as ISO/8652-1987, Programming Languages—Ada).

并行编程语言的比较研究：
Salishan 问题 / J.T. Feo (编辑)
© 1992 Elsevier Science Publishers B.V. 版权所有。

# C* 并行编程语言

David L. Andrews
CASE Center, Syracuse University
Syracuse, NY 13244

Eric Barszcz
Nasa Ames Research Center
Moffettett Field, CA 94035

## 1. 背景

C* 是 C 语言的扩展，专为 Thinking Machines SIMD（单指令多数据）计算机 Connection Machine2 [1] 设计。该语言假设一个冯·诺依曼风格的前端计算机（如 VAX3）与一组相同的处理器协同工作，每个处理器都有本地内存，如图 1 所示 [3]。数组中的处理器同时执行相同的指令流，同时之间进行数据通信，C 共享以下特征：

1) 统一地址空间，
2) 顺序执行，以及
3) 指针算术。

C* 大部分并行能力源于将现有运算符和语句应用于新的并行数据类型。例如，在两个多路操作数 `a` 和 `b` 上指定的算术操作 `a * b` 将导致所有处理元素执行乘法。此外，如果启用了 16k 处理元素并包含 `a` 和 `b`，将同时执行 16k 次乘法。C* 保留了数组与指针之间的互换性，这是 C 语言的核心特征。所有处理器间的通信都通过赋值和指针间接表示。并行执行不需要新的表达式运算符，尽管引入了两个计算并行操作数最大值或最小值的运算符。

### 1.1. 语言设计

C* 编程语言遵循单指令流的 SIMD 哲学，并提供了独立于处理元素数量的简单控制机制。这些扩展基于仅三个新特性：

- 一个用于识别并行数据的多路（poly）类型属性
- 一个用于组织并行数据的域（domain）特性，在语法和语义上与 C `struct` 相似
- 一个用于激活和停用并行执行的选择性语句（selection statement）

### 1.2. 顺序与并行数据表示

数据在 C* 中表示为标量或并行。标量数据通过关键字 `mono` 识别，并存在以前端主机的的内存中。并行数据通过关键字 `poly` 识别，存在于处理器数组的本地处理器内存中。在域内声明的数据默认为 `poly`，而在域外声明的数据默认为 `mono`。关键字 `domain` 用于两种不同的语境：

1) 类似于 C 关键字 `struct` 用于声明，以及 2) 用于限定 C* 程序部分的的作用范围，指明包含该域类型操作数的处理器需要被激活。

```
mono int uno; /** 存在于主机内存中的标量整数 */
```

```
poly int ddata; /** 存在于处理器本地内存中的多个整数 */
```





```c
mono int *poly ddata; /** 数组上的多个指针
处理器所有指针都指向主机
内存中的一个标量
//*/
```

```c
poly int *poly ddata; /** 数组上的多个指针
处理器指向数组处理器中
已存在的并行
数据处理器 //*/
```

### 1.3. 基础计算的表示

所有的 C 代码分为两类：标量（scalar）和并行（parallel）。属于某个域（domain）的代码是并行代码，执行在处理器阵列上。所有其他代码都是串行的（serial），并执行在前端主机处理器上。这两种类型的代码使用相同的语法，仅通过语法上下文进行区分。所有的标准 C 表达式运算符和所有的 C 语句类型都可以以与串行代码相同的方式在并行代码中使用。

### 1.4. 并行计算的表示

许多数据处理器对同一条指令的同步并行执行仅在每个执行该指令的处理器包含相同的内存布局时才可能发生。描述数据处理器内存的 C* 结构类型称为域（domain）。下面显示了两个域 `Enum` 的示例域声明。域相关的内存布局如图 2 所示。

```c
/** 示例声明 **/
domain Enum {
  int number;
  domain Enum dptr;
};
```

```c
/** 示例声明 **/
domain Paraffin {
  char *wax;
  int a;
} Pe_Paraffin[100];
```

# C*

![](img/68e0c8e7cd61671f4d693a9b7458d12d_107_0.png)

图 2 - 域 `Enum` 的内存和指针配置。

**domain** Enum 声明了一个整数和一个指针，它们存在于所有在 **domain** Enum 中执行的处理元素的本地内存中，如图 2 所示。**domain** Paraffin 声明了一个字符指针和一个整数，它们存在于分配给在 **domain** Paraffin 中执行的 100 个处理器的每个本地内存中。域内声明的任何字段的特定实例都可以通过指定处理器阵列索引以及使用用于访问结构体字段的 C 语法来访问。例如，`Pe_Paraffin[50].wax` 指定了位于（逻辑）处理器 50 本地内存中的字符字符串 wax。

### 1.4.1. 新运算符

C* 充分利用了编译时串行和并行数据之间的区别，通过重载扩展了有的 C 运算符以对并行数据进行操作。仅添加了两个新运算符：最小运算符 `<` 和最大运算符 `>`。新运算符与扩展后的标准 C 运算符集合一起，允许以以下方式在处理器之间进行数据移动：

- 读取（reading）：从特定的数据处理器获取一个值到前端
- 写入（writing）：从前端将一个值存储到特定的数据处理器中
- 复制（replication）：从前端广播一个值到所有并行处理器
- 归约（reduction）：从所有并行处理器读取值，交付组合后的结果
- 排列（permutation）：在规则和不规则模式下数据处理器之间进行通信

作为归约操作的一个简单示例，考虑以下代码片段：

```c
/** 类似于结构体 **/
domain Pebble_Beach {
    int hole_score; /** 并行变量 **/
} Pebble_Beach_hole[18];
main() {
    /** 重置回合分数 **/
    int round_score = 0;
    /** 激活 Pebble_beach_hole 的所有 18 个 PE **/
    [domain Pebble_Beach].{
        /** 求和归约到前端 **/
        round_score += hole_score;
    }
}
```

分配给域 `Pebble_Beach` 的代码仅由 `Pebble_Beach` 的处理器执行。变量 `round_score` 声明在域之外，默认是一个位于主机前端的标量值。熟悉的 C 语法 `+=` 将值赋值给 `round_score`；即其当前值加上 `hole_score` 的值，但 `hole_score` 是域内的变量。

域内声明的任何字段的特定实例都可以通过指定处理器阵列索引以及使用用于访问结构体字段的 C 语法来访问。例如，`Pe_Paraffin[50].wax` 指定了位于（逻辑）处理器 50 本地内存中的字符字符串 wax。

（注：此处提供的原始文本似乎存在部分重复或逻辑断层，翻译已根据指令“不要重复输出原文”的原则对有效内容进行了处理。）

C* 充分利用了编译时串行和并行数据之间的区别，通过重载扩展了有的 C 运算符以对并行数据进行操作。仅添加了两个新运算符：最小运算符 `<` 和最大运算符 `>`。新运算符与扩展后的标准 C 运算符集合一起，允许以以下方式在处理器之间进行数据移动：

字体 读取（reading）：从特定的数据处理器获取一个值到前端
- 写入（writing）：从前端将一个值存储到特定的数据处理器中
- 复制（replication）：从前端广播一个值到所有并行处理器
- 归约（reduction）：从所有并行处理器读取值，交付组合后的结果
- 排列（permutation）：在规则和不规则模式下数据处理器之间进行通信

...（省略重复的逻辑段落）...

### 1.5. 处理器选择

处理器通过进入域被激活。使用熟悉的 C 运算符在域内进行操作。假设我们想要找到 `hole_score` 的最大值。C* 提供的 `>` 运算符执行操作如下：

```c
domain Enum {
  int number;
}
```




102

D. L. Andrews 和 E. Barszcz

| | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|---|
| **a** | a^0 | a^1 | a^2 | a^3 | a^0 | a^1 | a^2 | a^3 | a^0 | a^1 |
| **b** | b^0 | b^0 | b^0 | b^1 | b^1 | b^1 | b^0 | b^0 | b^0 | b^1 |
| **c** | c^0 | c^0 | c^0 | c^0 | c^0 | c^0 | c^0 | c^1 | c^1 | c^1 |

（注：c 行根据 OCR 结果延续）

图 3 - 汉明问题的处理器内存布局

通过将集合 `Conv` 的元素与素数的幂集进行卷积，可以为下一个素数获得一组新的部分值。在对所有素数执行此操作后，集合 `Conv` 将包含未排序的元素，这些元素是扩展汉明问题的解。列表可以在 Connection Machine 上快速排序，以获得升序的扩展汉明问题的解。图 3 显示了每个处理器中素数值的分布，每个处理器接收素数的唯一组合并计算一个单一的卷积输出点。

C* 程序首先从 `Primemult` 域的素数列表中计算每个输入素数输入的部分结果。在每个处理器中，计算一个唯一的 `a^i` (`i=0...j≤N`) 并将其置于本地内存中。所有 `a^s` 的计算在 `log2(log2N)` 时间内完成，如图 4 所示，并在 C* 中表示为

```c
/* initialize variables *//
pwrto = 0;
/** within domain Primemult **/
/** compute each PE's address **/
int addr = (int) (this - &Prime_Procs[0])
while (( max >= prime_number) <= N) {
```

# C*

103

| | Pe[0] | Pe[1] | Pe[2] | Pe[3] | Pe[4] | Pe[5] | Pe[6] | ... |
|---|---|---|---|---|---|---|---|---|
| a | a | a | a | a | a | a | ... |
| a² | a² | a² | a² | a² | a² | a² | ... |
| a² | a³ | a³ | a⁴ | a⁴ | a⁴ | a⁴ | ... |

图 4 - a**i** 值的计算，其中 a**i** < N

```c
if (addr >= pwrto)
    prime_number *= Prime_Procs[addr-pwrto].prime_number;
    pwrto = 2;
} // end while */
```

`>=?` 运算符返回所有启用处理元素内存位置 `prime_number` 中的最大值。当计算出的 `aⁱ` 大于整数 `N` 时，循环将退出，从而允许 `N` 和 `prime_number` 使用任意值，而无需指定循环限制。计算出的 `aⁱ` 值取决于仅查询那些计算出的素数值小于或等于 `N` 的处理元素，并对它们的地址使用 `>=?` 运算符。

在每个素数扩展后（`a⁰, a¹, a², ... ≤ N`），这些值分布在 `PrimeExpand` 域的处理器数组中，如图 5 所示。执行此操作的 C* 代码如下：

```c
/** maxpe == number of primes < N **/
/** rep == current size of the set Conv **/
modaddr = offset;
for (indx = 0; index <= maxpe; indx++) {
    frontprime = Prime_procs[indx].primenum;
```

104 D. L. Andrews 和 E. Barszcz

```c
if (modaddr < (index*rep + rep) && modaddr >= rep*index)
    temp *= frontprime;
```

其中每个待分布的 `a^l` 值首先从 `Primemult` 域中的处理器 `Prime_Procs[index]` 传输到前端，并广播到 `PrimeExpand` 域中指定的处理器范围内，该范围由图 5 所示的

```c
if (modaddr < (index*rep + rep) && modaddr >= rep*index)
```

语句指定。注意，在程序中，计算出的乘积值相对于 `N` 进行检查以确定该值是否超过了我们的限制。在所有素数输入、在 `Primemult` 域中扩展、分布并在 `PrimeExpand` 域中更新部分值后，可以通过条件性选择乘积值小于 `N` 的处理器，在单个条件操作中识别出所有小于 `N` 的感兴趣的值。选定的值随后传递给排序程序，按升序返回值。

`Primemult` 域在 `O(log₂N)` 内执行每个 `a^i` (`i = 0, 1, ... j, l ≤ N`) 的乘法。`PrimeExpand` 域在 `O(L • log n)` 内执行 `Primemult` 域计算出的 `a` 的分布以及所有 `L` 个输入素数的乘法，其中 `L` 由最小素数给出。计算出的值使用 Batcher 排序，复杂度为 `O(log²M)`，`M = (log₂N • log₂N • ...)` 是集合 `Conv` 的基数。因此，算法的最坏情况计算复杂度由执行所有 `L` 个输入素数乘法的步骤给出，为 `O(L • logαN)`。

图 5 - 计算出的素数的分布

此外，这种高效的算法很容易在 C* 中表示。素数值从文件流入并以 `EOF`（文件结束）终止，通过 `while` 循环识别，允许输入任意长度的素数列表。

3. 汉明问题

在 C* 中开发的求解汉明问题的算法基于 Turner [4]。每个分子由整数列表表示。列表中的每个整数代表一个子分子。例如，甲烷表示为 `[1, 3]`，而丙烷的几种表示方式之一为 `{3, 3, 1}`。以下函数生成包含所有分子的列表：

```c
para n = {[x,3] | x <- para (n-1)}
quotient f = a: {b |
para = 0
para (n) = {[a,b,c] | i, j,k < [0, ..., n-1]; i+j+k = n-1;
a <- para i; b <- para j; c <- para (n-1)}
```

C* 算法通过在 `Enum` 域并行计算所有 `para(n)` 开始。这是通过形成所有组合 `[a,b,c] | 0 ≤ a,b,c ≤ n-1` 并根据相对地址完成的。以下代码执行此操作：

```c
index = n; /** para(n) **/
offset = (int) (this - &Enum[0]);
if (offset <= max_size) { /** max_size = i **/
a = offset % index; /** a address **/
mod_b = offset / index; /** b address **/
b = mod_b % index; /** b address **/
c = index-1-a-b; /** b address **/
} /* end if */
```

# C*

107

| Pe | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | . | 1 | 2 | 4 | 5 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| (a, b, c) | 0 | 0 | 1 | 1 | 0 | 1 | 0 | 2 | 1 | 0 | | 1 | 3 | 2 | 1 | 0 |
| | 0 | 0 | 0 | 1 | 0 | 0 | 2 | 0 | 0 | | 3 | 0 | 1 | 0 |

图 6 - 枚举的处理器内存布局。执行并行枚举所需的处理元素由运行时定义的 `max_size` 给出该代码的执行情况如图 6 所示。C* 算法的下一步是对 `[aᵢ bⱼ cᵏ]` 执行直方图，表示形成 `para(n)` 的子分子。所有处理器通过在 `Hamming` 域执行以下代码并行执行直方图：

```c
para[a] += 1; para[b] += 1; para[c] += 1;
```

图 7 显示了该操作在 `1 ≤ N ≤ 5` 时的结果。`para[r]` 现在表示 `[aᵢ bⱼ cᵏ]` 中等于 `r` 的数字；即 `para[0]` 等于零的个数，`para[1]` 等于一的个数，以此此类推。在 `[aᵢ bⱼ cᵏ]` 有三个数字的情况下，任何 `para[i]` 可以取的最大值是 3。

通过使用指针间接从 `PrimeExpand` 域复制每个处理器的数组在 `PrimeExpand` 域中扩展数组。每个数组复制到 `PrimeExpand` 的次数相当于形成烷烃分子的可能组合数。图 7 显示 `n=2` 时有两种子分子组合。所有包含 `n=2` 作为子分子的烷烃其 `para[2]` 均非零。执行此操作的代码给出：

D. L. Andrews 和 E. Barszcz

| Pe | n | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 2 | 1 | 2 | 0 | 1 | 1 | 2 | 0 | 1 | | | | | |
| 1 | 1 | 2 | 3 | 0 | 1 | 2 | 0 | 2 | | 1 | 0 | | | |
| 2 | | 0 | 1 | 0 | 1 | 2 | 0 | | 1 | 0 | 0 | | | |
| 3 | | | 0 | 1 | 0 | 1 | 0 | | 1 | 0 | 0 | | | |
| 4 | | | | | 0 | 0 | 1 | | | 0 | 1 | | | |
| 5 | | | | | | | | | 0 | 0 | 1 | | |

图 7 - Para Array 配置

```c
[domain Paraxpand). {
mono int index;
mono int upper;
domain Paraffin *transptr;
base = 0;
pe_num = this - &Pxpnd_Pe[0]; /** relative Pe **/
for(index = 0; index < count; index++) {
  /** count = # pe's **/
  /** pointer to domain Paraffin **/
  ntransptr = &Paraffin[index];
  if(pe_num == 0) { /** first elements pointer **/
  /** expand set in domain Paraffin **/
  upper = transptr -> expand;
  if((pe_num < base + upper) && (pe_num >= base)) {
    rep = index;
    /** pelem = 1, 0 < i < N **/
    carbon_number = transptr -> pelem;
    for(loop = 0; loop < N; loop++)
      array[loop] = transptr -> para[loop];
  }
} /* end if */
```





## C* 109

```
base += upper;
}
}
```

注意，在 Paraxpand 域中，使用 poly 指针 transptr 在两个域之间正在发生并行读取。一个 for 循环遍历 para 的元素，一次将一个元素传输到 Paraxpand 域。Paraxpand 域中扩展后的 para 数组如图 8 所示。

在 Paraxpand 域中扩展 para 数组后，每个 para 数组中的每个 para n (para[0]) 将是聚石烷分子表示中的第一个整数。第二个条目 (para[1]) 表示表示中 3 的数量。所有其他条目均通过递归替换找到。作为递归替换的示例，如果 para 数组在 para[2] 中有一个条目，例如图 8 中的处理器 2，则对于 n = 2 的子分子表示将附加到该分子的表示上。如果该条目大于 1，例如图 8 中 para[2] 的处理器 8，则将子分子按该次数复制到该分子的表示中。

C* 算法在 Paraxpand 域内通过一个顺序循环执行执行上述操作。每个处理器在 polymer 数组中构建一个聚石烷分子。执行此操作的代码列如下，并在图 9 中图形所示。

```c
/* 循环所有可能的碳数 **/
for(k=2; k<N; k++) {
[domain Paraxpand].(

  if((parray[k] != 0) && (carb_num > k)) {
  /** 替换 k -> k+1, k+2, ... N **/
  pfpntr = &Ppxnd_pe[target]; // poly pointers **/
  /** k 分子中的整数数量 **/
  ddize = pfnptr -> length;
```

## 110 D. L. Andrews 和 E. Barszcz

| | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| n | 2 | 3 | 4 | | | | | | | | | | | 6 | |
| p | 0 | 2 | 0 | 1 | 2 | 2 | 0 | 1 | 1 | 2 | 2 | 2 | 0 | 0 | 1 | 1 | 1 | 1 | |
| a | 1 | 2 | 0 | 3 | 1 | 0 | 2 | 0 | 1 | 1 | 0 | 0 | 0 | 2 | 0 | 1 | 1 | 1 | |
| r | | | 0 | 1 | 0 | 1 | 0 | 2 | 0 | 1 | 1 | 0 | 0 | 0 | | | | | |
| a | | | | | 0 | 0 | 1 | 0 | 0 | 1 | 0 | 0 | 0 | 1 | 1 | 1 | 0 | 0 | 0 | |
| 3 | | | | | | | | 0 | 0 | 0 | 0 | 1 | 1 | 1 | 0 | 0 | 0 | 1 | 1 | |
| 4 | | | | | | | | | | | | | | | | 0 | 0 | 0 | 0 | 0 | |
| 5 | | | | | | | | | | | | | | | | | | | |

图 8 - Paraxpand 域中扩展的 para 数组

```c
** m 是 poly; 每个人复制 dsize 个整数 */
for(m=0; m < dsize; m++) {
  /** 获取 k 个碳的聚合物 ***/
  parffin[m] = pfnptr -> polymer[m];

  /** pe 复制 polymer array[k] 次 */
  for(m=0; m < array[k]; m++) {
    /** 附加 k cnt polymer **/**
    polymer[length + cnt] = paraffin[cnt];
    length += dsize; /** 更新你的长度 ***/
  }
}
```

上述代码中的变量 `length` 存储每个碳分子的当前整数数量。每个对自己的 polymer 数组执行更新的处理器都需要读取 `length` 以及目标处理器的 polymer 数组，以确定数组中当前整数的数量。然后，每个处理器设置临时变量 `dsize` 等于目标处理器，并将 polymer 数组按顺序复制到虚拟数组 `parffin` 中。然后，将虚拟数组 `parffin` 按 `array[k]` 次附加到当前 polymer 数组上。

| | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| | 2 | 3 | | 4 | | | | | | 5 | | | | | |
| | | | | | 2 | 2 | 0 | 1 | 1 | | 2 | 2 | 2 | | |
| p | 1 | | | | | 2 | 2 | 0 | 1 | 1 | 0 | 0 | 0 | | |
| a | 2 | | | | | | 2 | 2 | 0 | 1 | 0 | 0 | 0 | 0 | | |
| r | 3 | | | | | | | 2 | 0 | 0 | 0 | 0 | 0 | 0 | | |
| a | 4 | | | | | | | 0 | 0 | 1 | 0 | 0 | 0 | 1 | 1 | | |

| | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| | 2 | 3 | | 4 | | | | | | | 5 | | | | | |
| | | 2 | 3 | 1 | 2 | 2 | 3 | 1 | 1 | | 2 | 2 | 2 | | | |
| polymer | | | 3 | 5 | 3 | 2 | | | | 3 | 3 | | | | | |
| array | | | | 3 | 5 | 3 | 2 | | | | | | | | | |

| | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| | 2 | 3 | | 4 | | | | | | | 5 | | | | | |
| | | | | | 2 | 2 | 0 | 1 | 1 | | 2 | 2 | 2 | | | |
| p | 1 | | | | | 2 | 2 | 0 | 1 | 1 | 0 | 0 | 0 | | | |
| a | 2 | | | | | | 2 | 2 | 0 | 1 | 0 | 0 | 0 | 0 | | |
| r | 3 | | | | | | | 2 | 0 | 0 | 0 | 0 | 0 | 0 | | | |
| a | 4 | | | | | | | 0 | 0 | 1 | 0 | 0 | 0 | 1 | 1 | | | |

| | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| | 2 | 3 | | 4 | | | | | | 5 | | | | | | |
| | | | | | 2 | 2 | 0 | 1 | 1 | | 2 | 2 | 2 | | | |
| p | 1 | | | | | 2 | 2 | 0 | 1 | 1 | 0 | 0 | 0 | | | |
| a | 2 | | | | | | 2 | 2 | 0 | 1 | 0 | 0 | 0 | 0 | | | |
| r | 3 | | | | | | | 2 | 0 | 0 | 0 | 0 | 0 | 0 | | | |
| a | 4 | | | | | | | 0 | 0 | 1 | 0 | 0 | 0 | 1 | 1 | | | |

| | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| | 2 | 3 | | 4 | | | | | | 5 | | | | | | | |
| | | | | | 2 | 2 | 0 | 1 | 1 | | 2 | 2 | 2 | | | | |
| p | 1 | | | | | 2 | 2 | 0 | 1 | 1 | 0 | 0 | 0 | | | | |
| a | 2 | | | | | | 2 | 2 | 0 | 1 | 0 | 0 | 0 | 0 | | | | |
| r | 3 | | | | | | | 2 | 0 | 0 | 0 | 0 | 0 | 0 | | | | |
| a | 4 | | | | | | | 0 | 0 | 1 | 0 | 0 | 0 | 1 | 1 | | | | |

| | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| | 2 | 3 | | 4 | | | | | | 5 | | | | | | | | |
| | | | | | 2 | 2 | 0 | 1 | 1 | | 2 | 2 | 2 | | | | | |
| p | 1 | | | | | 2 | 2 | 0 | 1 | 1 | 0 | 0 | 0 | | | | | |
| a | 2 | | | | | | 2 | 2 | 0 | 1 | 0 | 0 | 0 | 0 | | | | | |
| r | 3 | | | | | | | 2 | 0 | 0 | 0 | 0 | 0 | 0 | | | | | |
| a | 4 | | | | | | | 0 | 0 | 1 | 0 | 0 | 0 | 1 | 1 | | | | | |
| | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | || | 2 |  | | 0 | 0 | 1 | 0 | 0 | 0 | 1 | 1 | | | |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---| | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | |
| p | 1 | | | | | 2 | 2 | 0 | 1 | 1 | 0 | 0 | 0 | | | | | | |
| a | 2 | | | | | | 2 | 2 | 0 | 1 | 0 | 0 | 0 | 0 | | | | | | |
| r | 3 | | | | | | | 2 | 0 | 0 | 0 | 0 | 0 | 0 | | | | | | |
| a | 4 | | | | | | | 0 | 0 | 1 | 0 | 0 | 0 | 1 | 1 | | | | | | |
| | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | | | | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | | | |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---| | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | |
| | 2 | 3 | | 4 | | | | | | 5 | | | | | | | | | |
| | | | | | 2 | 2 | 0 | 1 | 1 | | 2 | 2 | 2 | | | | | | |
| p | 1 | | | | | 2 | 2 | 0 | 1 | 1 | 0 | 0 | 0 | | | | | | |
| a | 2 | | | | | | 2 | 2 | 0 | 1 | 0 | 0 | 0 | 0 | | | | | | |
| r | 3 | | | | | | | 2 | 0 | 0 | 0 | 0 | 0 | 0 | | | | | | |
| a | 4 | | | | | | | 0 | 0 | 1 | 0 | 0 | 0 | 1 | 1 | | | | | | |
| | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | | | | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | | | |
| | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | |

## 112 D. L. Andrews 和 E. Barszcz

C* 算法在 Paraxpand 域内通过一个顺序循环执行上述操作。每个处理器在 polymer 数组中构建一个聚石烷分子。执行此操作的代码列如下，并在图 9 中图形所示。

```c
/* 循环所有可能的碳数 **/
for(k=2; k<N; k++) {
[domain Paraxpand].(

  if((parray[k] != 0) && (carb_num > k)) {
  /** 替换 k -> k+1, k+2, ... N **/
  pfpntr = &Ppxnd_pe[target]; // poly pointers **/
  /** k 分子中的整数数量 **/
  ddize = pfnptr -> length;
```

注意，在 Paraxpand 域中，使用 poly 指针 transptr 在两个域之间正在发生并行读取。一个 for 循环遍历 para 的元素，一次将一个元素传输到 Paraxpand 域。Paraxpand 域中扩展后的 para 数组如图 8 所示。

在 Paraxpand 域中扩展 para 数组后，每个 para 数组中的每个 para n (para[0]) 将是聚石烷分子表示中的第一个整数。第二个条目 (para[1]) 表示表示中 3 的数量。所有其他条目均通过递归替换找到。作为递归替换的示例，如果 para 数组在 para[2] 中有一个条目，例如图 8 中的处理器 2，则对于 n = 2 的子分子表示将附加到该分子的表示上。如果该条目大于 1，例如图 8 中 para[2] 的处理器 8，则将子分子按该次数复制到该分子的表示中。

上述代码中的变量 `length` 存储每个碳分子的当前整数数量。每个对自己的 polymer 数组执行更新的处理器都需要读取 `length` 以及目标处理器的 polymer 数组，以确定数组中当前整数的数量。然后，每个处理器设置临时变量 `dsize` 等于目标处理器，并将 polymer 数组按顺序复制到虚拟数组 `parffin` 中。然后，将虚拟数组 `parffin` 按 `array[k]` 次附加到当前 polymer 数组上。

## 4. 医生

C* 算法允许多个患者同时生病并请求服务。如果多个患者同时生病，他们将根据相对处理器编号在队列中排序。接待员会对特定时间进入诊所的所有病人进行排序，并将注意力转向将等待的患者与可用医生进行匹配。

并行查询所有医生以确定他们是忙碌还是可以接收新患者。目前忙碌的医生（由其忙碌标志 = BUSY 且随机治愈时间大于 0 表示）并行减少其时间。可用医生的数量可以通过还原操作轻松地找到：

```c
wait_doc = 0;
wait_doc += not_busy;
```

在 Doctor 域中。wait_doc 必须初始化，否则之前的 wait_doc 值将会被并行还原。

在算法开始时，所有患者生成一个随机生病时间。在每个模拟步骤中，随机时间会减少。当生病时间减少到零时，患者进入诊所接受治疗。用于减少随机时间的代码为：

```c
else if ((sick == NOT_SICK) && (lambda > 0)) {
    lambda -= 1;
    if(lambda == 0) sick = SICK;
}
```

处理器的数量由患者和医生决定。Patient 中的整数变量和 Doctor 中的 cure_time 分别代表生病的随机时间和治愈时间。

```c
domain Doctor {
int sick;
int not_busy;
int lambda;
int cure_time;
int wait;
int doctor_num;
int Patient_num;
int patient_ptr;
} Patient_Pe
int patient_id;
[size_of_population]; Doctor_Pe[number_of_doctors];
```

接待员将所有新患者 (lambda = 0) 等待队列，并设置每个患者的 wait 字段等于其在队列的位置。接待员通过将患者的生病标志设置为 QUEUED 来通知患者已进入队列。





## D. L. Andrews 和 E. Barszcz

下一个患者将被分配给处理器编号最低的下一个可用医生。

值得注意的是，上一步代表了仿真中的一个人为（尽管是现实的）瓶颈。C* 的语法允许将尽可能多的患病患者分配给尽可能多的可用医生，且全部并行进行。

回到问题本身，选择等待时间最短的患者（代表其在患病队列中的位置），并分配给相对地址最小的下一个可用医生。然后，选中的医生会生成新的治疗方案并将其标记为忙碌。选择患者的代码如下所示：

```c
[domain Patient] {
  patient_num = (this - &Patient_Pe[0]);
  whosnext = PATIENTS; /* 重置 ****/
  if(sick == QUEUED) { /* 选择下一个队列患者 */
    whosnext <= wait; /** 选择下一个队列位置 **/
    next_patient = PATIENTS; /** 重置 **/**
    if(wait == whosnext) { /** 选择患者 **/
      next_patient <= patient_num;
      /** 选择已治愈的患者 **/
      Patient_Pe[next_patient].sick = BEING_CURED;
    }
  }
}
```

所有医生都并行查询，通过条件语句判断它们是否完成了对患者的治疗：

```c
((cure_time == CURED) && (not_busy == BUSY))
```

在 `domain Doctor` 内，所有成功通过上述条件的医生都会重置其患者的 `sick` 标记，表示患者不再患病，并重置自己的 `not_busy` 标记，并行执行这两个操作。

## C* 115

整个仿真可以用 C* 表达。患病患者与医生的匹配是通过两个域之间的指针间接完成的。算法的最坏情况计算复杂度由 `domain Patient` 中用于将患者放入队列的 `for` 循环决定，等于每个仿真时间步中需要入队列的患者数量。语法允许清晰地表达患者患病和治愈患者这两个异步事件，每个事件都发生在指定的域内。此外，该仿真对于不同数量的患者和医生具有良好的扩展性。代码的唯一更改是重新声明患者域和医生域的大小。

## 5. Skyline 矩阵求解器

Skyline 矩阵求解器的目标是求解线性方程组：

$Ax = b$

在不使用主元的情况下，其中 $A$ 是一个 $N \times N$ 的 skyline 矩阵，$x$ 和 $b$ 是向量。Skyline 矩阵在第 $i$ 行的第 $j$ 到 $i$ 列（$1 \le j \le i$）是非零元素，在第 $j$ 列的第 $i$ 到 $j$ 行（$1 \le i \le j$）也是非零元素。

向量 $I$ 定义对角线下的 skyline，向量 $J$ 定义对角线上的 skyline。使用的 C* 算法是并行高斯消元的变体，其中 $I$ 和 $J$ 被用掩码以避免对零元素进行不的操作。假设 $A$ 的输入格式是一个结构线性数组，仅包含非零元素及其 $i, j$ 索引。

与 $C$ 不同，$C^*$ 目前不支持“锯齿数组”（ragged arrays）。因此，为了避免存储零元素，所有非零元素都存储在线性数组中。在密集并行高斯消元中，计算期间需要 $i, j$ 数组索引来指定行。

116 D. L. Andrews 和 E. Barszcz

图 10 - 用于操作的高斯消元和列。索引可以在每次需要时重复计算，也可以在程序开始计算一次并存储。

对于求解 skyline 矩阵，一次性计算每个非零元素的 $i, j$ 索引并将其与元素一起存储更为简单且计算效率更高。

密集并行高斯消元的前向消元步骤如图 10 所示。执行此密集并行高斯消元的 C* 代码如下：

```c
/* 前向消元 */
for (k=0; k<N; k++) {
    [domain Matrix]; 
    /* 动态计算 i,j 索引 */
    int offset = (int) (this - &A[0][0]);
    int i = offset / N;
    int j = offset % N;

``````c
/* 并行计算所有行主元 */
/* 将列下方每个元素 */
* 主元除以主元 */
if ((i > k) && (j == k))
    a = a / A[i][k].a;
/* 通过以下更新第 k 行下方的元素 */
* (row(i) = row(i) - (row(k) * rowpivot(i))) *
if ((i > k) && (j > k))
    a = A[i][k].a * A[k][j].a;
}
domain RHS,{
/* 动态计算 i 索引 */
int i = (int)(this - &B[0]);
/* 同时更新 RHS 的所有 */
* k 行下方的元素 */
if (i > k) b = b - (A[i][k].a * B[k].b);
}
/* 反向替换 */
for (k=(N-1); k>0; k--) {
/* 计算第 k 个元素 */
x[k] = B[k].b;
domain RHS,{
/* 动态计算 i 索引 */
int i = (int)(this - &B[0]);
/* 同时更新 RHS 的所有 */
* k 行下方的元素 */
if (i > k) b = b - (A[i][k].a * B[k].b);
}
```

上述代码与更高效的解决方案之间的区别是：

```c
/* 选择下一个队列患者 */
whosnext <= wait; /** 选择下一个队列位置 **/
next_patient = PATIENTS; /** 重置 **/**
if(wait == whosnext) { /** 选择患者 **/
  next_patient <= patient_num;
  /** 选择已治愈的患者 **/
  Patient_Pe[next_patient].sick = BEING_CURED;
}
```

上述代码与更高效的解决方案之间的区别是：

最近修订中关键字的定义。注意 $I$ 和 $J$ 被用于屏蔽操作。

语法允许清晰地表达患者患病和治愈患者这两个异步事件，每个事件都发生在指定的域内。此外，该仿真对于不同数量的患者和医生具有良好的扩展性。代码的唯一更改是重新声明患者域和医生域的大小。

Skyline 矩阵求解器的目标是求解线性方程组 $Ax = b$ 在不使用主元的情况下，其中 $A$ 是一个 $N \times N$ 的 skyline 矩阵，$x$ 和 $b$ 是向量。Skyline 矩阵在第 $i$ 行的第 $j$ 到 $i$ 列（$1 \le j \le i$）是非零元素，在第 $j$ 列的第 $i$ 到 $j$ 行（$1 \le i \le j$）也是非零元素。

向量 $I$ 定义对角线下的 skyline，向量 $J$ 定义对角线上的 skyline。使用的 C* 算法是并行高斯消元的变体，其中 $I$ 和 $J$ 被用掩码以避免对零元素进行不的操作。假设 $A$ 的输入格式是一个结构线性数组，仅包含非零元素及其 $i, j$ 索引。

与 $C$ 不同，$C^*$ 目前不支持“锯齿数组”。因此，为了避免存储零元素，所有非零元素都存储在线性数组中。在密集并行高斯消元中，计算期间需要 $i, j$ 数组索引来指定行和列。索引可以在每次需要时重复计算，也可以在程序开始计算一次并存储。对于求解 skyline 矩阵，一次性计算每个非零元素的 $i, j$ 索引并将其与元素一起存储更为简单且计算效率更高。

密集并行高斯消元的前向消元步骤如图 10 所示。执行此密集并行高斯消元的 C* 代码如下：

```c
/* 前向消元 */
for (k=0; k<N; k++) {
    [domain Matrix]; 
    /* 动态计算 i,j 索引 */
    int offset = (int) (this - &A[0][0]);
    int i = offset / N;
    int j = offset % N;

``````c
/* 并行计算所有行主元 */
/* 将列下方每个元素 */
* 主元除以主元 */
if ((i > k) && (j == k))
    a = a / A[i][k].a;
/* 通过以下更新第 k 行下方的元素 */
* (row(i) = row(i) - (row(k) * rowpivot(i))) *
if ((i > k) && (j > k))
    a = A[i][k].a * A[k][j].a;
}
domain RHS,{
/* 动态计算 i 索引 */
int i = (int)(this - &B[0]);
/* 同时更新 RHS 的所有 */
* k 行下方的元素 */
if (i > k) b = b - (A[i][k].a * B[k].b);
}
/* 反向替换 */
for (k=(N-1); k>0; k--) {
/* 计算第 k 个元素 */
x[k] = B[k].b;
domain RHS,{
/* 动态计算 i 索引 */
int i = (int)(this - &B[0]);
/* 同时更新 RHS 的所有 */
* k 行下方的元素 */
if (i > k) b = b - (A[i][k].a * B[k].b);
}
```

上述代码与更高效的解决方案之间的区别是：

```c
/* 选择下一个队列患者 */
whosnext <= wait; /** 选择下一个队列位置 **/
next_patient = PATIENTS; /** 重置 **/**
if(wait == whosnext) { /** 选择患者 **/
  next_patient <= patient_num;
  /** 选择已治愈的患者 **/
  Patient_Pe[next_patient].sick = BEING_CURED;
}
```

上述代码与更高效的解决方案之间的区别是：

最近修订中关键字的定义。注意 $I$ 和 $J$ 被用于屏蔽操作。

语法允许清晰地表达患者患病和治愈患者这两个异步事件，每个事件都发生在指定的域内。此外，该仿真对于不同数量的患者和医生具有良好的扩展性。代码的唯一更改是重新声明患者域和医生域的大小。

## 附录

********************/
/**  Hamming 的问题  **/
********************/

```c
#include <stdio.hs>
void Batcher(int);

#define MAXSIZE 150
#define BIGSIZE 4096

domain Primemult {
    int primenum;
} Prime_Procs[MAXSIZE];

domain PrimeExpand {
    mono int intx, jdx;
    mono int frontprime;
    int product = 1;
    int Origin;
    int Location;
} Prime_Procs[BIGSIZE];

main(int argc, char *argv[]) {
    int N;
    char *argv[11];
    int maxoffset = 0;
    int maxpe = 0;
    int rep = 1;
    int prime;
    FILE *fp;
    fp = fopen("primelist.dat","r"); // /** 质数输入文件 */
    sscanf(fp,"%d\n%d",&N)==1; // /** 读取值 N **/
    while (sscanf(fp,"%d\n%d",&prime)==1) { /** 主 while 循环 **/
        printf("%d\n", prime);
        [Primemult];{
            mono int max = 0;
            mono int maxaddr = 0;
            mono int prwto = 1;
            primenum = prime;
            int addr = (int)(this - &Prime_Procs[0]);
            while (max > primenum) <= N () { // /**扩展质数 */
                if (addr == prwto) {
                    primenum = Prime_Procs[addr-prwto].primenum;
                    prwto *= 2;
                }
            } /** 结束 while ***
    **** 找到 <= N 的 pe 数量以后用用 ***
    if (primenum <= N) {
```
```





## C* 121

```c
maxaddr>= addr;
Prime Procs [maxaddr + 1].primenum = 1; /* 设置 b**0 **/
maxaddr += 1;
maxpe = maxaddr;
maxoffset *= {maxaddr+1};
} /** [domain.primenum] 结束 /**/
```

```c
/*** 在 domain domain 中执行质数乘法 ***/
[domain PrimeExpand].{
    int offset = (int) -Prime_Execs[0];
    int modoff = offset % (maxoffset);
    /*** 将目标数字放在前端 ***
    for (int idx = 0; idx < maxpe; idx++) {
        int frontprime = Prime_Procs[idx].primenum;
        if (modoff < (idx + rep) % modaddr >= rep*idx) {
            product *= frontprime;
        }
    } **** for 结束 ***/
    rep = offset;
} /** domain PrimeExpand 结束 ***/
} /** while 循环结束 ***/
```

```c
fclose(fp); /** 关闭文件 **/
```

```c
/*** 批量排序值 *******/
Batch(rep); /** 批量排序程序 ***/
/*** 选择并输出解 ******/
[domain PrimeExpand].{
    for(int j = 0; j < (maxoffset-1); j++) {
        if (Prime_Execs[j].product <= N) {
            printf("Prime_Execs[%d]=%d\n", j, jdx, Prime_Execs[j].product);
        }
    } /** for 结束 **/
} /** domain PrimeExpand 结束 ***/
```

****************************************************/
/*** 石蜡枚举问题 (Paraffin Enumeration Problem) **/
****************************************************/

```c
#include <stdio.h>
#include <math.h>

#define N 10

domain Enum /** 还原使用的临时整数 **/
mono int enumenum;
mono int boolflag;
mono int elem;
/** (x,y,z) **/
```

## D. L. Andrews 和 E. Barszcz

```c
int x;
int y;
int z;
int flag;      /** flag = {0,1} 用作布尔 **/
}EnumPe[1024];
```

```c
domain Paraffin {
mono int pminaddr;
int pelem;
int expand = 1;
/** {a,b,c } **/
int a;
int b;
int c;
int para[N];
}ParaPe[1024];
```

```c
domain Paraxpand {
/** mono int 全部用于循环和临时变量 **/
mono int base = 0;
mono scalarbase;
/** m = 用于从 domain Paraffin 转移数组的循环索引 **/
int m;
int pe_num;      /** pe_num 是相对地址 **/
int rep;         /**拷贝数组的临时变量 = 多合物长度 **/
int size;       /** 用于拷贝数组的“索引”临时变量 **/
int cnt;
int length;      /** 碳数量 **/
int carb_num = 0; /** 当前聚合物数组的大小 **/
int mod;
int base;       /** pe 的模地址 **/
int thispe;      /** 临时存储 **/
int thispe = {0,1} 用作布尔标志 **/
int array[N];
int paraffin[N];
int polymer[30];
int carb_count[N];
domain Paraxpand *pfnptr; /** 指向 domain Paraffin 的聚指针 **/
domain Paraxpand *tranptr; /** 指向 domain Paraxpand 的聚指针 **/
}Pxpde[1024];
```

```c
main() {
int max_size;    /** max_size = 可能的排列数 **/
int index;
int this_rep;
int upper;
int total_expand;
int x;
int car_base[N];
int exp[N];
/** 前端临时存储 **/
int listx[1024];
```

```c
int listy[1024];
int listz[1024];
int Enum[1024];
int tempx;
int tempo;
int count = 0; /* 前端数组的索引 **/
int loop {

for(index = 2; index <= N; index++){
 max_size = pow(index,3); /* 最大枚举数 **/
[domain Enum].{
 int mody;
 mono int next = 0; /* 初始化所有标志为零 **/
 int offset = (int)(this - &Enum[0]);
 if (offset < max_size) { /* <= maxsize 的值的索引 **/
 x = offset / index; /* 模地址 a **/
 mody = offset % index;
 y = mody % index;
 z = Index-1-x-y;
 } // if 结束
enum = 0;
 if (x + y) <= (x+y) == (index-1) {
enum += (poly)1;
 next < offset? { /* 找到第一个值 **/
 flag = 1; /* 初始化 PE 标志 **/
 boolflag; /* 初始化全局标志 **/
 while(boolflag) == 1) {
 /* 向前端加载 (x,y,z) **/
 listy[count] = Enum[next].x;
 listz[count] = Enum[next].y;
 listx[count] = Enum[next].z;
 Enum[count] = index; /* 枚举 **/
 for(elem=0; elem<elem+) { /* 旋转值 **/
 if(listx[count] == x) && (flag == 1) {
 /* 检查所有 x **/
 if(list[count] == y && listz[count] == z) {
랴[count] = z; listz[count] = y;
 flag = 0; /* 设置 PE 标志 **/
 } // if (x[count] = x) 结束 **/
 tempx = listx[count]; /* 临时存储 **/
 tempy = listy[count]; /* 临时存储 **/
 listy[count] = listz[count]; /* 旋转 z **/
 listx[count] = tempy; /* 旋转 y **/
 listz[count] = tempx; /* 旋转 x **/
 } // 循环3次 **/
if(flag == 1) {
 /* 重置指针 **/
 next = 0; offset;
 next; /* 选择下一组 (x,y,z) **/
 }
 count += 1; /* 增加计数 **/
boolflag = 0; /* 重置全局标志 **/
boolflag >= flag;
} /** while 结束 **/
} /** x+y+z =N-1 的组合 **/
} /** domain Enum 结束 **/
} /** for 结束 **/

```c
domain Paraffin. /** 所有的迭代并更新 **/
int paraoffset = (this - &ParaPe[0]); /** 偏移 **/
// 将值顺序读取到 Paraffin **/
for(loop = 0; loop < count; loop++) {
ParaPe[loop].i = list[loop];
ParaPe[loop].b = list[loop];
ParaPe[loop].c = list[loop];
ParaPe[loop].pelem = Enum[loop];
} /** 读取值结束 **/
```

```c
para[a] += 1;
para[b] += 1;
para[c] += 1;
for(loop = 2; loop < N; loop++) {
exp[loop] = 0;
if(pelem == loop) exp[loop] += expand; /** 查找 pe **/
if(pelem > loop) && (pelem > 0) exp *= exp[loop];
} /** 长度结束 **/
if(paraoffset < count) {
total_expand = 0; /** 重置计数 **/
total_expand += expand;
} /** if 结束 **/
} /** domain Paraffin 结束 **/
```

```c
domain Paraxpand.
pe_num = (int)(this - &PpxPe[0]);
for(index = 0; index < count; index++) {
transptr = &ParaPe[index];
if(pe_num == 0) { /** 选择第一个元素指针 **/
upper = transptr -> expand;
if((pe_num <= base + upper) && (pe_num >= base) {
rep = index; /** 标记重复次数 **/
carb_num = transptr->pelem; /** 元素数量 **/
for(loop = 0; loop < N; loop++) {
parray[loop] = transptr -> para[loop];
} /** if 结束 **/
base += upper; /** 更新基地址 **/
} /** for 结束 ***
} /** domain Paraxpand 结束 **/
```

```c
/** 初始化第一个条目 **/
[domain Paraxpand].
length = 0;
if(array[0] != 0) {
polymer[0] = array[0];
length = 1;
} /** 初始化第一组结束 **/
for(m=0; m < array[1]; m++)
polymer[length++] = 3; /** 初始化第二组结束 **/
} /** Paraxand 结束 ***

```c
*** 递归步骤更新石蜡表示 **/
for(k=2; k<N; k++) { /** 遍历所有值 **/
    domain[Paraxand];
    pe_num = (int)(this) - &Pnd_Pe[0]);
...




# C*

# 127

****************************************************************/**
/** 医生诊所问题 **/
/****************************************************************/

```c
#define PATIENTS 20
#define DOCTORS 5
#define NOT_BUSY 1
#define BUSY 0
#define SICK 1
#define NOT_SICK 0
#define QUEUED -1
#define TREATING 2
#define CURED 0
#define simulation_time 50

#include <stdio.h>
#include <stdlib.h>
```

```c
domain Patient {
    int sick = NOT_SICK;
    int lambda = 0;
    int wait;
    int patient_num;
} Patient_Pe[PATIENTS];
```

```c
domain Doctor {
    int not_busy = NOT_BUSY;
    int cure_time = CURED;
    int doctor_num;
    int patient_id;
    domain Patient *patient_ptr;
} Doctor_Pe[DOCTORS];
```

```c
main() {
    int number_sick; /*** 生病人数量 **/
    int cnt = 0;
    int i;
    int next_patient;
    int whosnext;
    int wait_doc;
    int next_doc;
    int loop;
```

```c
**** 用于打印结果的变量 ***
int max_alloc = PATIENTS;
int sick_count = 0;
int Sick_List[100];
int Time_List[100];
int doc_finish;
int num_cured;
int cure_count = 0;
```

```c
int Doctor_Cured[100];
int Patient_Cured[100];

for(loop = 0; loop < simulation_time; loop++) { /** 无限循环 **/
[domain Patient]; {
    /** sick = 1;
    patient_num = (int) (this - &Patient_Pe[0]);
    /** 处理随机时间的生成 ***/
    if((sick != NOT_SICK) && (lambda == 0)) {
        /** 在此处插入你喜欢的随机数生成程序 **/
        lambda = rand();
    }
    else if(sick != NOT_SICK) && (lambda > 0)) {
        /** 并行递减所有健康计数 **/
        lambda = 1;
        if(lambda == 0) sick = SICK;
        /** 检查是否有新的就诊人员 ***/
        number_sick = 0; /** 重置 **/
        if(sick != SICK) /** 重置 sick += (poly)[1]; /** 计数病人 #/**
        /** 如果有新患者，放入队列 ***/
        for(i=0; i < number_sick; i++) {
            next_patient = PATIENTS; /** 重置 **/
            if(sick != SICK) && next_patient < patient_num) {
                Patient_Pe[next_patient] = QUEUED;
                Patient_Pe[next_patient].wait += 1 + cnt;
                /** 收集前端统计信息 **/
                Sick_List[sick_count] = next_patient;
                Time_List[sick_count++] = loop;
            }
        }
        /** 更新病人人数 **/
        cnt += number_sick;
    }
}

**** 检查医生 *****/
*** 医生在茶休息 **/
[domain Doctor]. {
    /** 更新医生的治愈时间 **/
    if((cure_time > 0) && (wait_busy != BUSY)) cure_time -= 1;
    /** 更新非忙碌医生 ***/
    wait_doc = 0;
    wait_doc += not_busy;
}

/** 检查是否有在队候患者 ***/
if((cnt != 0) && (wait_doc != 0)) {
    /** 选择下一个医生 ***/
    [domain Doctor]. {
        doctor_num = (int) (this - &Doctor_Pe[0]);
        next_doc = DOCTORS;
        if(not_busy != NOT_BUSY) next_doc <= not_num;
    }
}
```

# C*

```c
/** 在队列中选择下一个患者 ***/
[domain Patient];
patient_num = (int)(this - &Patient_Pe[0]);
whosnext = PATIENTS;
if(sick == QUEUED ||
  whosnext <= wait) {
  next_patient = PATIENTS;
  if(wait == whosnext) next_patient <= patient_num;
  Patient_Pe[next_patient].sick = TREATING;
/** 将患者分配给医生 /**
[domain Doctor].{
  Doctor_Pe[next_doc].not_busy = BUSY;
  Doctor_Pe[next_doc].patient_id = next_patient;
  Doctor_Pe[next_doc].cur_time = rand();
  printf("Doctor<%d> <- Patient <%d> at time[%d]\n",
    next_doc, next_patient, loop);
/** 更新队列中剩余的人数 ***/
  cnt -= 1;
} // end if //
*** 检查已治愈的患者并更新治愈时间 ***
[domain Doctor].{
  /** 查找此时治愈的人数 **/
  if((cur_time == CURED) && (not_busy == BUSY)) {
    num_cured = 0;
    num_cured += (poly)1;
    for(i=0; i < num_cured; i++) {
      if((cur_time == CURED) && (not_busy == BUSY)) {
        /** 重置 **/
        doc_finish = DOCTORS;
        doc_finish <= doctor_num;
        Doctor_Pe[doc_finish].finish_ptr =
          &Patient_Pe[doc_finish].patient_id;
        Doctor_Pe[doc_finish].finish_ptr = NOT_SICK;
        Doctor_Pe[doc_finish].not_busy = BUSY;
        Patient_Cured[cure_count++] =
        finish_id;
      }
    }
  }
for(i=0; i <count_count++) { {
  printf("(" order of\\t\\n



("printf




for
i=0 < cure_count; i++) {
  printf("%d <d\n", Doctor_Cured[i], Patient_Cured[i]);
} // end main

# D. Andrews and E. Bars

```c
********************
/** Skyline 矩阵 **/
********************

#include <stdio.h>

#define N 4
#define BIG 10

domain Matrix { float a; int i; } A[N][N];
domain RHS { float b; int i; } B[N];
domain Skyline { float s; int i; } SKY[BIG];
domain Vector { float element; int start; } I[N], J[N];

void main(int argc, char *argv[])
{
    int k, l, m;
    float x[N], element;
    float rowsum; /* 需要并行归约 */
    int NonZeros;
    float Pivot;
    FILE *fp;

    fp = fopen(argv[1], "r");

    /* 读取矩阵 */
    for (k=0; k<N; k++)
    for (l=0; l<N; l++) {
        fscanf(fp, "%f", &element);
        A[k][l].a = element;
    }

    /* 初始化 RHS */
    for (k=0; k<N; k++) {
        int offset = (int) (this - &B[0]);
        i = offset / N;
        j = offset % N;
    }

    /* 初始化 RHS 的值 */
    for (k=0; k<N; k++) {
        rowsum = 0.0;
        if (i == k) rowsum += A[k].a;
        B[k].b = rowsum;
    }

    /* 将矩阵转换为 Skyline 格式 */
    NonZeros = map();

# C*

```c
printf("NonZeros %d\n", NonZeros);
/* 前向消元 */
for(k=0; k<(N-1); k++) {
    [domain Skyline];
    /* 寻找主元 */
    if ((i == k) && (j == k)) Pivot = s;
    /* 计算行主元 */
    if ((i > k) && (j >= k)) && ((I[i].start <= k)) {
      s = s / Pivot;
      I[i].element = s;
    }
    /* 保存行 k */
    if(((i == k) && (j > k)) && (J[j].start <= k)) J[j].element = s;
    /* 并行更新元素 */
    if ((i > k) && (j > k)) {
      if ((I[i].start <= k) && J[j].start <= k)
        s = s - (I[i].element * J[j].element);
    }
    [domain RHS];
    if (i > k) b = b - (I[i].element * B[k].b);
}
/* 反向替换 */
for(k=N-1; k>=0; k--) {
    [domain Skyline];
    if((i <= k) && (j == k)) && (J[k].start <= k)) J[i].element = s;
    x[k] = B[k].b / J[k].element;
    [domain RHS];
    if ((i < k) && (J[k].start < k)) b = b - (J[i].element * x[k]);
}
```

```c
int map(
  int k, l, m;
  [domain Vector]. { start = -1; }
  /* 将每个非零元素分配到 Sky 中的位置 */
  /* 如果能找到一种巧妙的方法来实现这样做 */
  /* 并行的话，尽管去尝试... */
  m = 0;
  for (k=0; k<N; k++)
    for (l=0; l<N; l++)
      if (A[k][l].a != 0.0) {
        Sky[m].s = A[k][l].a;
        Sky[m].i = A[k].i;
        Sky[m].j = A[k].j;
        m++;
        if (I[k].start == -1) I[k].start = l;
        if (J[l].start == -1) J[l].start = k;
      }
    return(m);
}/* map 结束 */
```




# P. Hudak 和 S. Anderson

Haskell 是一种通用的纯函数编程语言，展示了编程语言研究中的许多最新创新，包括高阶函数、非严格函数和数据结构、静态多态类型、用户可定义的代数数据类型、模式匹配、列表推导式、模块系统以及丰富的原始数据类型（包括任意精度和固定精度整数，以及复数、有理数和浮点数）。此外，它具有几个提供额外表达能力的新颖特性，包括使用类型类概念的优雅重载形式、统一了两种主要的函数 I/O 模型的灵活 I/O 系统，以及允许使用“数组推导式”构建纯函数单体数组的数组数据类型。

读者会注意到，我们没有将 Haskell 描述为并行编程语言；事实上它确实不是。然而，近年来许多研究都集中在并行机器上实现函数式语言，包括构建特殊用途硬件（如数据流和归约机制）。我们对这些问题将不作多言，只需指出这些所提问题的解决方案具有显著的内在并行性。

由于空间限制，我们无法完整描述 Haskell；我们的目标只是通过对 1988 年 Salishan 高速计算会议上提出的四个语言会问题提供解决方案，让读者对该语言有一定的了解。读者可以参阅 Haskell Report [7] 以获取该语言的完整定义。当然，学习这里提出的解决方案将让读者对在任何一种现代函数式语言中编程的感觉有所了解；事实上，给出的所有解决方案都运行在我们在耶尔大学设计并实现的函数式语言 Alfi 的实现上。

## 2 Haskell 简要概述

在本节中，我们将描述足够的 Haskell 语法，以便理解后文给出的程序。因此，Haskell 的很大部分将完全不被描述，最显著的是用户定义的数据类型、模块和 I/O。此外，本文使用的语法对应于会议时的设计；自那时起，已经进行了一些更改。

Haskell 是一种“等式化”语言，类似于 Miranda2、Hope 以及其他几种现代函数式语言。函数由一组方程定义，这些方程对参数进行 `[a,b,c]` 模式匹配。列表写作 `[]` 表示空列表。可以通过编写 `a:as` 在列表头部添加一个元素。两个列表可以通过列表 `ll++ls` 拼接在一起。这里是模式匹配的示例：

```
member x = False
(y:ys) = if x==y then True
                else member x ys
```

第二行上的“撇号标记”是前一行初始子序列的简便缩写（使得两个方程的元数相同）。

函数 `f x = x+1` 也可以用表达式 `\x -> x+1` “匿名”地定义，因此 `(\x -> x+1) 2` 返回 3。

列表推导式是定义列表的简洁方式，通过示例解释效果最好：

```
[ (x,y) | x<-xs, y<-ys ]
```

它构建了一个包含所有第一个元素来自 `xs`、第二个元素来自 `ys` 的对的列表。也可以定义“无限列表”，得益于惰性求值，程序其他部分所需的列表部分实际上会被计算。因此，无限 1 列表可以通过方式定义：

```
ones = 1 : ones
```

记法 `[a..b]` 表示从 a 到 b（包含边界）的整数列表，`[a..]` 是从 a 开始的无限升序整数列表。

列表上定义了许多标准实用函数。除了之前定义的 `member` 之外，我们在本文需要的函数如下：

```
-- 当 pred 为真时，取列表元素
takewhile pred [] = []
  (a:as) = if (pred a) then
    (a : awhile pred as)
  else
    []
```

```
-- 从左侧折叠列表
foldl f [] = a
  (x:xs) = foldl f (f a x) xs
```

```
-- 从右侧折叠列表
foldr f [] = a
  (x:xs) = f x (foldr f a xs)
```

```
-- 从两个列表对形成对列表
zip [] bs = []
  as [] = []
  (a:as) (b:bs) = (a,b) : zip as bs
```

```
-- 去除列表重复项
nodups [] = []
  (x:xs) = x : nodups [ y | y <- xs, y /= x ]
```

# Haskell

在 Haskell 中，函数应用始终具有最高优先级的中间操作符，因此

```
a : awhile pred
```

被解析为

```
a : (while pred as)
```

注意 `zip` 中元组的使用，元组在 Haskell 中通过编写以下方式构造有限长度：

```
(a, b, ..., c)
```

（括号是强制的）；元组可以像列表一样进行模式匹配。最后，注意对于 `foldl` 和 `foldr` 满足以下关系：

```
foldl f a [x1, x2, ..., xn] => (f ... (f a x1) x2) ... xn
foldr f a [x1, x2, ..., xn] => (f x2 ... (f x a) ... )
```

Haskell 还有数组以及用于操作它们的特殊语法。二维数组 `a` 通过表达式 `a!(i, j)` 在位置 `(i, j)` 索引。新数组使用“数组推导式”构建；推导式指定了矩阵的索引/值对。例如：

```
array ((1,1), (n,n))
[(i,j), k*a(i,j) | i<-{1..n], j<-{1..n} ]
```

返回一个被标量 `k` 乘以矩阵。

对 Haskell 的这种描述非常简洁，但足以让后文给出的程序自说明白。然而，具有一种函数式语言的经验将是有益的。

## 3 Hamming 问题（扩展）

在 Haskell 中解决此问题的自然方法是生成一个无限增长序列，然后过滤掉小于 `n` 的数字。但我们如何创建无限序列？首先，让我们定义一个乘以流中每个元素的函数：

```
scale xs = [ p*x | x<-xs ]
```

现在注意问题的构造方法是归纳定义：

* 1 在输出序列中。
* 对于每个素数 `p`，如果 `k` 在输出序列中，那么 `k • p` 也在其中。

我们可以构建这样的数据流图，如图 1 所示，其中重复模式被突出显示。将框的功能封装在 `f` 中，并使用 `foldl`：

```
hamming primes = 1 : foldl f [] primes
  f xs p = h where
    h = merge (scale (1:h)) xs
```

在这种情况下，`merge` 简单定义为：

```
merge (a:as) (b:bs) = if a < b then a : merge as (b:bs)
else b : merge (a:as) bs

[] bs = bs
as [] = as
```

当 `merge` 按升序合并流列表时。不幸的是，`merge` 还必须删除重复项，因为这个简单的定义会构造特定数字的所有排列。例如，它会生成十二：2 • 2 • 3，2 • 3 • 3 和 3 • 2 • 2。

这显然是低效的，我们更倾向于避免额外乘法的解决方案。问题源于子流是递归地从整个列表 `h` 生成的。我们真正想要某种“追尾”的东西，以避免生成所有组合。图 2 中的数据流图实际上正是如此——注意每次 `merge` 的结果都被反馈到自身，从而避免了重复。

结果就是：

```
takewhile (\x -> x < n) (hamming primes)
```

使用引言中定义的实用函数 `while`。

这里是在我们的 Alfi 实现上运行的示例输出转录：





# Haskell

```haskell
take (\x -> x < 46) (hamming [2,3,5]);
Result: [1,2,3,4,5,6,8,9,10,12,15,16,18,20,24,25,27,30,32,36,40,45]
```

## 4. 蜡烛问题

该问题在 [8] 中得到了讨论。在参考文献中，它是使用函数式语言 Miranda 解决的，而 Miranda 正好与 Haskell 相似。因此我们的任务已经完成了！虽然有更高效算法可以解决这个问题，但它们对理解 Haskell 没有提供更多的见解。因此，我们将在 Haskell 中重写 Turner 的 KRC 解决方案并进行一些简化，并参考上面的蜡烛进行详细描述：

```haskell
main = foldr (++) [] (map paraffin [..])

affin n = quotient equiv ["x","H","H","H"] | x <- para (n-1) - []

para = ["H"] : map genpara [..]
genpara n = [ [a,b,c] |
  i <- [0..(n-1)/3], j <- [i..(n-1-i)/2],
  a <- para!!i, b <- para!!j, c <- para!!(n-1-i-j)]
```

```haskell
equiv a b = member (equivclass a) b
equivclass x = closure_under_laws [invert
```

```haskell
invert [[a,b,c,d],e,f] = [a,b,c,d,e,f]
("H":x) = "H":x
```

```haskell
rotate [a,b,c,d] = [b,c,d,a]
swap [a,b,c,d] = [b,a,c,d]
```

```haskell
closure_under_laws fs xs = xs ++ closure' fs xs
closure' fs xs ys =
closure'' fs xs (nodups) [a | f <- fs,
```

```haskell
a <- map f ys, not (member a xs)]
closure' fs xs [] = []
ys = ys ++ closure' fs (xs ++ ys) ys
```

```haskell
quotient f [] = []
(a:x) = a : [b | b <- quotient f x , not (f a b)]
```

## 5. 医生诊室

在四个问题中，这可能是定义最模糊的一个。主要的困难在于第一句中“模型（model）”这个动词的具体含义。也许最常见的建模类型是对实际时间/事件对的模拟，这正是下面由 Joe Fasel 编写的第一个解决方案所呈现的。然而，这种解决方案完全消除了问题的非确定性和异步性（因为它们正在被模拟），这与问题描述最后一句中关于“具有非确定性”的陈述有些冲突。因此，我们还提供了一个使用显式非确定性的解决方案。遗憾的是，非确定性不是 Haskell 标准的一部分，因此我们假设有一个名为 `choose` 的原始操作符，它能从列表中非确定性地选择一个元素。

这两个解决方案截然不同，反映了 Haskell 非常不同的特性。

### 5.1. 时间/事件模拟

这种医生诊室模型以输入患者数量、医生数量、患者生病的初始时间列表，以及两个无限持续的时间列表（代表患者保持健康的时间分布和医生治愈患者所需的时间分布）。它返回一个无限元组列表，包含每次就诊的以下信息：

(患者, 生病时间, 医生, 开始治疗时间, 治愈时间)

也就是说，患者编号、患者生病并进入患者队列的时间、分配的医生编号、患者被分配到医生的时间，以及医生完成患者治疗的时间。

该解决方案的风格是创建相互递归的时间/事件对流，在适当的位置将它们合并在一起，同时保持时间顺序。主要的事件流是患者 (patientQ)、医生 (doctorQ) 和治愈的人 (cured)，如下所示。`insert` 和 `makeQ` 是处理时间-事件对队列的工具。

```haskell
n m initialWellDist WellDist CureDist = cured

where insert y [] = [y] -- 将 y 插入时间排序的队列
  insert (p',t') rest ((p,t):xs) | t' < t = rest
  | otherwise = (p,t) : insert (p',t') xs

makeQ (x:xs) yys -- 初始队列（有序），  -- 后续条目（无序）
  x = makeQ (insert y xs) where y:ys = yys
```

```haskell
patientQ
  makeQ (foldr insert [] (zip [1..n] initialWellDist))
  (p,c+x) | ((p,s,d,t),x) <- zip cured WellDist
```

```haskell
doctorQ
  -- (医生，可用时间)
  makeQ [(d,0) | d <- [1..m]]
  (d,c) | (p,s,d,t,c) <- cured
```

```haskell
cured
  = [(p,s,d,t+x) where t = max s a
  | (p,s), (d,a), x) <- zip3 patientQ doctorQ cureDist
```

### 5.2. 异步过程模型

在接下来的解决方案中，“世界”被建模为一个六元组：

- healthy_people, -- 健康人数列表
- sick_people, -- 生病人数队列
- being_cured, -- 正在治的病人/医生对
- cured_people, -- 已治愈的人/医生对队列
- doctor_Q, -- 可用医生队列
- 接待员记录的相关记录

这种表示方法实际上比上一个更详细，因此也更真实。特别是，增加了一个记录簿以及一个用于存放在治疗结束后向接待员汇报的医生/患者对的队列（这个队列在规范中没有提到，但看起来更真实）。世界的初始状态是显而易见的：

```haskell
initial_world = 
([[1..n], -- 每个人都是健康的
{}, -- 没有人生病了
{}, -- 没有人正在被治疗
{}, -- 没有人刚刚被治愈
[1..m], -- 每个医生都是空闲的
```

世界的动态通过“过程”捕捉，这些过程接收一个世界并输出一个新的世界。医生诊室的模拟通过从初始世界开始并迭代选择一个过程来更新世界来进行。结果是：

```haskell
Haskell 143
```





# Haskell

数组实例是单块式处理的，而不是增量式的。也就是说，整个最终数组是在一个单块式的声明中指定的，这产生了一种更符合函数式编程哲学的声明式阅读方式。下面将介绍这种风格的解决方案。

## 6.1. 单块式数组解决方案

轮廓问题很好地说明了 Haskell 数组的某些特殊优势。特别是，数组规范可以清晰、直接地从问题的原始数学定义推导出来。核心数据依赖是清晰的，而不是被无关的互操作操作顺序所掩盖。数组的递归定义（包括多个数组的互递归定义）允许优雅的规范和高效的实现。Haskell 数组允许对任何数组不同区域的元素进行单独定义，这允许了类似于从 Fortran 循环中提升计算的优化，这些优化清晰地响应了数学函数的域规范。

增量式解决方案本质上是 Sherman 代码的转录版本，我们没有包含关于数据表示或算法的描述。对于单块式解决方案，我们将从最基础的开始，通过规范的成对细化来开发最终程序。

### 6.1.1. Sherman 稀疏矩阵包络格式简介

Sherman 的包络格式在稀疏线性系统 $A \cdot x = b$ 的方程和变量排序使得 A 的大部分非零元素靠近主对角线时效果最好。下三角的每一行 $i$ 被存储为从该行最左侧非零元素到对角线前最后一列 $j = i - 1$ 的包络。同样，上三角的每一列 $j$ 被存储为从该列上方非零元素到对角线前最后一行 $i = j - 1$ 的包络。主对角线本身存储为长度为 $n$ 的 1 维向量。

Sherman 将稀疏矩阵表示为五元组 $(n, pl, d, pu, irl, iru)$，其中：

- n = A 的阶数。
- $pl, d, pu$ = 1 维浮点向量，分别表示下三角连续存储的行包络、主对角线元素和上三角连续存储的列包络。
- $irl = iru =$ 长度为 $n$ 的 1 维整数向量，指向 $pl$ 和 $pu$ 的基地址。

基地址向量需要一些解释。对于访问下三角 $pl$，假设我们定义了向量：

- $fl!i = =$ 第 $i$ 行第一个非零元素的列索引。
- $begin\_l!i =$ 第 $i$ 行第一个非零元素在 $pl$ 中的索引。

然后我们通过以下方式访问下三角中的 $a!(i, j)$:

```
pl!(begin_l!i + j - fl!i) = a!(i, j)
```

但值

```
begin_l!i - fl!i
```

对于行 $i$ 中的每一个 $j$ 都是相同的。在随后的章节中，我们将看到计算下三角或上三角因子的元素 $(i, j)$ 需要一个内积求和，该求和沿着下三角行 $i$ 和上三角列 $j$ 。对于顺序程序，最好将此求和设为内层循环，以保持引用局部性，从而获得良好的缓存和虚拟内存命中率。因此，我们希望将此循环不变的计算移出内层循环，用 $O(n)$ 次评估替换对表达式

```
begin_l!i - fl!i
```

的 $O(n^2)$ 次评估。我们还通过将两个长度为 $n$ 的向量替换为一个长度为 $n$ 的向量来节省表示空间。

```
irli = begin_l1! - fli
pl!(irli + j) = a(i,j)
```

$irli$ 的值可以被视为 $pl$ 中行 $i'$ 的包络的基地址。“第一个非零”函数 $fl$ 可以作为对行 $i$ 中所有 $j$ 求和的限制，但可以从 $irli$ 轻松恢复。上三角的列导向包络以类似的方式存储。

### 6.1.2. “第一个非零”函数

我们将展示行 $i$ 的非零函数 $fl$ 如何从 $irl$ 恢复，用于行 $i$ 中所有 $j$ 求和。上三角的列导向包络以类似的方式存储。类似的函数 $fu$ 可以从上三角的列导向包络推导出来。设 $env\_len\_i(i)$ 为 $i$ 行第一个非零元素在 $pl$ 中的索引。然后我们通过以下访问下三角中的 $a!(i, j)$:

```
pl!(begin_l!i + j - fl!i) = a!(i, j)
```

但值

```
begin_l!i - fl!i
```

对于行 $i$ 中的每一个 $j$ 都是相同的。在随后的章节中，我们将看到计算下三角或上三角因子的元素 $(i, j)$ 需要一个沿着下三角行 $i$ 和上三角列 $j$ 运行的内积求和。对于顺序程序，最好将此求和设为内层循环以保持引用局部性，从而获得良好的缓存和虚拟内存命中率。因此，我们希望将此循环不变的计算移出内层循环，用 $O(n)$ 次评估替换对表达式

```
begin_l!i - fl!i
```

的 $O(n^2)$ 次评估。我们还通过将两个长度为 $n$ 的向量替换为一个长度为 $n$ 的向量来节省表示空间。

```
irli = begin_l1! - fli
pl!(irli + j) = a(i,j)
```

$irli$ 的值可以被视为 $pl$ 中行 $i'$ 的包络的基地址。“第一个非零”函数 $fl$ 可以作为行 $i$ 中所有 $j$ 求和的限制，但可以从 $irli$ 轻松恢复。上三角的列导向包络以类似的方式存储。

我们将展示行 $i$ 的非零函数 $fl$ 如何从 $irl$ 恢复，用于行 $i$ 中所有 $j$ 求和。上三角的列导向包络以类似的方式存储。类似的函数 $fu$ 可以从上三角的列导向包络推导出来。设 $env\_len\_i(i)$ 为第 $i$ 行第一个非零元素在 $pl$ 中的索引。然后我们通过以下方式访问下三角中的 $a!(i, j)$:

```
pl!(begin_l!i + j - fl!i) = a!(i, j)
```

但值

```
begin_l!i - fl!i
```

对于行 $i$ 中的每一个 $j$ 都是相同的。在随后的章节中，我们将看到计算下三角或上三角因子的元素 $(i, j)$ 需要一个沿着下三角行 $i$ 和上三角列 $j$ 运行的内积求和。对于顺序程序，最好将此求和设为内层循环以保持引用局部性，从而获得良好的缓存和虚拟内存命中率。因此，我们希望将此循环不变的计算移出内层循环，用 $O(n)$ 次评估替换对表达式

```
begin_l!i - fl!i
```

的 $O(n^2)$ 次评估。我们还通过将两个长度为 $n$ 的向量替换为一个长度为 $n$ 的向量来节省表示空间。

```
irli = begin_l1! - fli
pl!(irli + j) = a(i,j)
```

$irli$ 的值可以被视为 $pl$ 中行 $i'$ 的包络的基地址。“第一个非零”函数 $fl$ 可以作为行 $i$ 中所有 $j$ 求和的限制，但可以从 $irli$ 轻松恢复。上三角的列导向包络以类似的方式存储。

我们将展示行 $i$ 的非零函数 $fl$ 如何从 $irl$ 恢复，用于行 $i$ 中所有 $j$ 求和。上三角的列导向包络以类似的方式存储。类似的函数 $fu$ 可以从上三角的列导向包络推导出来。设 $env\_len\_i(i)$ 为第 $i$ 行第一个非零元素在 $pl$ 中的索引。然后我们通过以下方式访问下三角中的 $a!(i, j)$:

```
pl!(begin_l!i + j - fl!i) = a!(i, j)
```

但值

```
begin_l!i - fl!i
```

对于行 $i$ 中的每一个 $j$ 都是相同的。在随后的章节中，我们将看到计算下三角或上三角因子的元素 $(i, j)$ 需要一个沿着下三角行 $i$ 和上三角列 $j$ 运行的内积求和。对于顺序程序，最好将此求和设为内层循环以保持引用局部性，从而获得良好的缓存和虚拟内存命中率。因此，我们希望将此循环不变的计算移出内层循环，用 $O(n)$ 次评估替换对表达式

```
begin_l!i - fl!i
```

的 $O(n^2)$ 次评估。我们还通过将两个长度为 $n$ 的向量替换为一个长度为 $n$ 的向量来节省表示空间。

```
irli = begin_l1! - fli
pl!(irli + j) = a(i,j)
```

$irli$ 的值可以被视为 $pl$ 中行 $i'$ 的包络的基地址。“第一个非零”函数 $fl$ 可以作为行 $i$ 中所有 $j$ 求和的限制，但可以从 $irli$ 轻松恢复。上三角的列导向包络以类似的方式存储。

我们将展示行 $i$ 的非零函数 $fl$ 如何从 $irl$ 恢复，用于行 $i$ 中所有 $j$ 求和。上三角的列导向包络以类似的方式存储。类似的函数 $fu$ 可以从上三角的列导向包络推导出来。设 $env\_len\_i(i)$ 为第 $i$ 行第一个非零元素在 $pl$ 中的索引。然后我们通过以下方式访问下三角中的 $a!(i, j)$:

```
pl!(begin_l!i + j - fl!i) = a!(i, j)
```

但值

```
begin_l!i - fl!i
```

对于行 $i$ 中的每一个 $j$ 都是相同的。在随后的章节中，我们将看到计算下三角或上三角因子的元素 $(i, j)$ 需要一个沿着下三角行 $i$ 和上三角列 $j$ 运行的内积求和。对于顺序程序，最好将此求和设为内层循环以保持引用局部性，从而获得良好的缓存和虚拟内存命中率。因此，我们希望将此循环不变的计算移出内层循环，用 $O(n)$ 次评估替换对表达式

```
begin_l!i - fl!i
```

的 $O(n^2)$ 次评估。我们还通过将两个长度为 $n$ 的向量替换为一个长度为 $n$ 的向量来节省表示空间。

```
irli = begin_l1! - fli
pl!(irli + j) = a(i,j)
```

$irli$ 的值可以被视为 $pl$ 中行 $i'$ 的包络的基地址。“第一个非零”函数 $fl$ 可以作为行 $i$ 中所有 $j$ 求和的限制，但可以从 $irli$ 轻松恢复。上三角的列导向包络以类似的方式存储。

### 6.1.3. L • U 在密集数组格式下的分解

特别是，数组规范可以清晰、直接地从问题的原始数学定义推导出来。核心数据依赖是清晰的，而不是被无关的互操作操作顺序所掩盖。数组的递归定义（包括多个数组的互递归定义）允许优雅的规范和高效的实现。Haskell 数组允许对任何数组不同区域的元素进行单独定义，这允许了类似于从 Fortran 循环中提升计算的优化，这些优化清晰地响应了数学函数的域规范。

增量式解决方案本质上是 Sherman 代码的转录版本，我们没有包含关于数据表示或算法的描述。对于单块式解决方案，我们将从最基础的开始，通过规范的成对细化来开发最终程序。

### 6.1.1. Sherman 稀疏矩阵包络格式简介

Sherman 的包络格式在稀疏线性系统 $A \cdot x = b$ 的方程和变量排序使得 A 的大部分非零元素靠近主对角线时效果最好。下三角的每一行 $i$ 被存储为从该行最左侧非零元素到对角线前最后一列 $j = i - 1$ 的包络。同样，上三角的每一列 $j$ 被存储为从该列上方非零元素到对角线前最后一行 $i = j - 1$ 的包络。主对角线本身存储为长度为 $n$ 的 1 维向量。

Sherman 将稀疏矩阵表示为五元组 $(n, pl, d, pu, irl, iru)$，其中：

- n = A 的阶数。
- $pl, d, pu$ = 1 维浮点向量，分别表示下三角连续存储的行包络、主对角线元素和上三角连续存储的列包络。
- $irl = iru =$ 长度为 $n$ 的 1 维整数向量，指向 $pl$ 和 $pu$ 的基地址。

基地址向量需要一些解释。对于访问下三角 $pl$，假设我们定义了向量：

- $fl!i =$ 第 $i$ 行第一个非零元素的列索引。
- $begin\_l!i =$ 第 $i$ 行第一个非零元素在 $pl$ 中的索引。

然后我们通过以下方式访问下三角中的 $a!(i, j)$:

```
pl!(begin_l!i + j - fl!i) = a!(i, j)
```

但值

```
begin_l!i - fl!i
```

对于行 $i$ 中的每一个 $j$ 都是相同的。在随后的章节中，我们将看到计算下三角或上三角因子的元素 $(i, j)$ 需要一个沿着下三角行 $i$ 和上三角列 $j$ 运行的内积求和。对于顺序程序，最好将此求和设为内层循环以保持引用局部性，从而获得良好的缓存和虚拟内存命中率。因此，我们希望将此循环不变的计算移出内层循环，用 $O(n)$ 次评估替换对表达式

```
begin_l!i - fl!i
```

的 $O(n^2)$ 次评估。我们还通过将两个长度为 $n$ 的向量替换为一个长度为 $n$ 的向量来节省表示空间。

```
irli = begin_l1! - fli
pl!(irli + j) = a(i,j)
```

$irli$ 的值可以被视为 $pl$ 中行 $i'$ 的包络的基地址。“第一个非零”函数 $fl$ 可以作为行 $i$ 中所有 $j$ 求和的限制，但可以从 $irli$ 轻松恢复。上三角的列导向包络以类似的方式存储。

### 6.1.2. “第一个非零”函数

我们将展示行 $i$ 的非零函数 $fl$ 如何从 $irl$ 恢复，用于行 $i$ 中所有 $j$ 求和。上三角的列导向包络以类似的方式存储。类似的函数 $fu$ 可以从上三角的列导向包络推导出来。设 $env\_len\_i(i)$ 为第 $i$ 行第一个非零元素在 $pl$ 中的索引。然后我们通过以下方式访问下三角中的 $a!(i, j)$:

```
pl!(begin_l!i + j - fl!i) = a!(i, j)
```

但值

```
begin_l!i - fl!i
```

对于行 $i$ 中的每一个 $j$ 都是相同的。在随后的章节中，我们将看到计算下三角或上三角因子的元素 $(i, j)$ 需要一个沿着下三角行 $i$ 和上三角列 $j$ 运行的内积求和。对于顺序程序，最好将此求和设为内层循环以保持引用局部性，从而获得良好的缓存和虚拟内存命中率。因此，我们希望将此循环不变的计算移出内层循环，用 $O(n)$ 次评估替换对表达式

```
begin_l!i - fl!i
```

的 $O(n^2)$ 次评估。我们还通过将两个长度为 $n$ 的向量替换为一个长度为 $n$ 的向量来节省表示空间。

```
irli = begin_l1! - fli
pl!(irli + j) = a(i,j)
```

$irli$ 的值可以被视为 $pl$ 中行 $i'$ 的包络的基地址。“第一个非零”函数 $fl$ 可以作为行 $i$ 中所有 $j$ 求和的限制，但可以从 $irli$ 轻松恢复。上三角的列导向包络以类似的方式存储。

### 6.1.4. L • U 在密集数组格式下的分解

为了清晰，我们在列表推导式中引入了一些新语法。在数组函数的列表推导式参数中，(i, x) 对可以写成 i = x 的形式，类似于 Haskell where 中的声明。例如：

```
array ((1,1), (N,N))
[(i,j) = k * a!(i,j) | i <- [1..N], j <- [1..N]]
```

从上一节的方程中，我们可以写一个函数式程序来计算 L 和 U。让我们定义一个高阶函数来表示数学求和符号：





# Haskell 153

sum i j accum f = if j < i then accum
              else sum (i + i) j (accum + (f i)) f

让我们定义一个函数 1，它给定索引 (i, j) 计算 L 中的元素值：

```
l (i,j) = a!(i,j) - (sum 1 (j-1) 0 1_exp)
where 1_exp k = L!(i,k) * U(k,j)
```

这个对 1 的定义与 Fortran 中的 DO 循环非常相似，并且可以进行高效的编译。

相反，我们将使用一种替代的 sum 的定义，它作用于列表上。

```
sum xs = suml 0 xs = accum
where suml accum []
suml accum (x:xs) = suml (accum + x) xs
```

配合列表推导式参数使用，这个版本为编写 `1 i` 提供了一种更具可读性的方式，并且更接近数学求和符号。

```
l (i,j) = a!(i,j) - sum [ L!(i,k) * U(k,j) | k <- [1..j-1]]
```

我们可以将列表视为一个多集，将 sum 视为集合中元素的求和（尽管严格来说，浮点加法不满足结合律）。诸如 Wadler 的无列表（listlessness）和压缩变换等技术可以确保这种表达式转换为语义等的表达式，其中列表被消除；该表达式可以像 DO 循环一样高效地编译 [9.10]。

这个对 1 的定义适用于

```
i <- [2..n], j <- [1..i-1]
```

# 154 P. Hudak 和 S. Anderson

跳过第一行，因为 l(1,1) 在对角线上，而我们希望单独定义对角线元素。

d 的定义计算 L 的对角元素，是 l 定义的简化版本（因为 i=j），适用于 i < [1..n]。

U 的定义与 L 几乎相同，但求和在 k=i-1 处停止。然后整行被 1./d!i 缩放，以将 U 的对角线归一化为 1.0。U 的定义适用于

i <- [1..n], j <- [i+1..n]

或者等价于

j <- [2..n], i <- [1..j-1]

参见本节末的完整程序。

每个元素 d! 在同一行的每个 u!(i,j) 定义中都作为除数出现（总共 (n-n)/2 次除法），同时也出现在 L•U•x=b 回代阶段同一行 x!i 的定义中（n 次除法）。由于除法与乘法相比开销很大，我们转而存储每个 d! 的倒数，将 O(n²) 次除法替换为 n 次除法和 O(n²) 次乘法。这是使用数组存储昂贵的共享计算的经典示例。

L 和 U 的定义在数学定义上和 Haskell 数组定义上都是互递归的。我们不需要存储 L 的上三角或 U 的下三角（它们为 0），因此我们可以将所有基本结果存储在单个 n² 数组中。我们可以递归地定义矩阵

```
lu = (L - D) + D¹ + (U - I)
```

以稠密矩阵格式（其中 D=L 的对角线，D¹=D 的逆矩阵）：

# Haskell

pla a = lu
where
((1,1), (n,n)) = bounds a
lu = array ((1,1), (n,n))
  [ (i,j) = i j | i <- [2..n], j <- [1..i-1] ] ++
  [ (i,i) = d | i <- [1..n] ] ++
  [ (i,j) = u j | i <- [1..n-1], j <- [i+1..n] ]
ij = a!(i,j) - sum lu!(i,k) * lu!(k,j) | k <- [1..j-1]
d i = *
where s = lu!(i,i) - sum lu!(i,k) * lu!(k,j) | k <- [1..i-1]
uj = lu!(i,i) *
  ( a!(i,j) - sum lu!(i,k) * lu!(k,j) | k <- [1..i-1] )

### 6.1.5. 惰性数组和严格数组

注意，数组推导式中的域规范完全对应于数学函数定义给出的域规范。这些域规范不应被视为循环结构：它们对于数组 lu 中元素的求值顺序没有说明任何信息。

事实上，我们可以让 lu 成为一个惰性数组。惰性数组中的每个元素都用一个悬值（thunk）表示，只有在需要时才会被求值。诸如下的域规范

i <- [2..n], j <- [1..i-1]

并不说明数组 lu 元素的求值顺序。惰性数组中的每个元素由一个悬值表示，只有在需要时才会被求值。





### 6.1.7. 使用包表示法的 L • U 分解

最后，让我们将定义从稠密格式转换为包格式。令输入矩阵 `a` 表示为元组

```
(n,old_pl,old_d,old_pu,irl,iru)
```

结果矩阵 `lu` 表示为

```
(n,new_po,new_d,new_pu,irl,iru)
```

辅助向量 `iru` 和 `irl` 对于输入矩阵 `a` 和输出矩阵 `lu` 而言是相同的。`a` 中的零元素在 `lu` 中变为非零元素，被称为“填充”（fill-in）。填充只会发生在包（envelope）内部；`a` 的包之外的所有零元素都保证保留在 `lu` 中，因此在在 `lu` 的包之外；因此，`a` 和 `lu` 具有相同的包结构，由向量 `iru` 和 `irl` 表示。

`new_d` 的向量边界简单为 `(l,n)`。我们可以通过获取向量边界 `(bounds pl)` 获取 `new_pl` 的新向量边界，同样地对于 `new_pu` 也是如此。或者，我们可以观察 `pl` 最后一个元素的索引为

```
irl!n + n - 1
```

对输入矩阵 `a` 引用的示例替换如下：

- 当 `i <- [2..n], j <- [(fu i)..(i-1)]` 时，`a!(i,j)` 变为 `old_pl!(irl!i + j)`
- 当 `i <- [1..n]` 时，`a!(i,j)` 变为 `old_d!(i)`
- 当 `j <- [2..n], i <- [(fu j)..(j-1)]` 时，`a!(i,j)` 变为 `old_pu!(i + iru)`

对 `lu!(i, j)` 的 l, d, 和 u 区域的引用也可以进行类似的替换。下三角的定义变为：

# P. Hudak & S. Anderson

```
1 (i,j) = s
where
kmin_1 = max (fl i) (fu j)
l1_exp k = new_pl!(irl!i + k) * new_pu!(k + iru!j)
accum_init = old_pl!(irl!i + j)
s = a_init - sum [l1_exp k | k <- [kmin_1..j-1]]

new_pl = array (bounds old_pl)
[irl!i+j = 1 (i,j), j <- [2..n], j <- [(fl i)..i..j] ]
[ irl!i + j = old_pl!(irl!i + j)
i <- [2..n], j <- [(fl i)], j < i]
```

有很多有很多公共子表达式消除的机会。对于给定的元素 `(i, j)`，求和中的每一项 `k` 都使用相同的基地址值 `irl!i` 和 `iru!j`，我们可以为每项节省两次向量查找。

还要注意，对于给定的行 `i`，表达式 `irl!i` 和 `(fl i)` 同时出现在 `(i, j)` 的定义和 `new_pl` 的数组推导式中。通过将这两个表达式从 `(i, j)` 的定义中抽象出来并在数组推导式的层级计算它们，我们不仅在程序的这两个部分之间共享了它们，还确保这些表达式对于给定的行只计算一次，而不是为行中的每个元素重新计算。

这是我们 L • U 分解的最终完整版本，提供了下三角的代码。

# Haskell

```
plu (n, old_pl, old_d, old_pu, irl, iru) =
(n, new_pl, new_d, new_pu, irl, iru)
where
1 (i,j) irli fli = s
where
kmin_l = max fli (fu j)
iruj = iru!j
l1_exp k = new_pl!(irli + k) * new_pu!(k + iruj)
a_init = old_pl!(irli + j)
s = a_init - sum [l1_exp_k | k <- [kmin_l..j]]
new_pl = array (bounds old_pl)
[irli + j) = 1 (i,j) irli fli
| i <- (2..n),
irli <- [irli!i],
fli <- [fli i],
j <- [fli+i..i-1] ] ++
(irli + j) = old_pl!(irli + j)
| i <- [2..n),
irli <- [irli!i],
fli <- [fli i],
j <- [fli j], fli k < i]
```

[1,2] 讨论了列表推导式的扩展，它能更清晰优雅地处理生成器的嵌套和循环不变子表达式。

如果编译器将 `i` 视为外层循环索引并将 `j` 视为内层循环索引，我们就实现了等同于 Fortran 中提升循环不变计算的。。在该程序片段中，仍有一些提升公共子表达式的机会，但我们已经利用了所有提升循环不变表达式的机会。

### 6.1.8. L • U • x = b 求解阶段

我们将讨论两个回代求解（backsolve）阶段的版本，一个版本使用列优先的 U，另一个使用重组后的行优先的 U。

# P. Hudak and S. Anderson

$A \cdot x = L \cdot U \cdot x = b$ 等价于求解下三角系统 $L \cdot y = b$，使用中间解 $y$ 作为右侧来求解上三角系统 $U \cdot x = y$。

```
l!(1,1) * (y 1) = b!1
l!(2,1) * (y 1) + l!(2,2) * (y 2) = b!2
...
l!(n,1) * (y 1) + . . + l!(n,n) * (y n) = b!n
```

记得我们以 `d!i` 的名存储每个 `i` 的对角线元素的逆。对于一个典型的行 `i`，这个方程组可以重写为函数：

```
y_vec = array [ i = y | i <- [1..n] ]
y i = s * d!i
where
s = b!i - sum [l!(i,j) * y_vec!j | j <- [1..i-1]]
```

最后求解上三角系统 $U \cdot x = y$，记得 $U$ 是单位对角线。假设矩阵处于稠密格式，整个函数对 `l!(i,j)`、`d!i` 和 `u!(i,j)` 进行适当的替换：

```
lu = (L - D) + D^{-1} + (U - I)
plub b = x_vec
where
y i = s * lu!(i,i)
s = b!i - sum [lu!(i,j) * x_vec!j | j <- [1..i-1]]
x i = y_vec!i - sum [lu!(i,j) * x_vec!j | j <- [i+1..n]]
y_vec = array (1,n) [ i = x | i <- [1..n] ]
```

# Haskell

现在让我们保持稠密格式，但引入“第一个非零”函数 `fl` 和 `fu`，以避免对 `l!(i,j)` 或 `u!(i,j)` 在包之外（因此为零）的项进行乘法和减法。对于下三角系统，这种变化是微不足道的，因为求和是沿行进行的。对于 `i <- [2..n]`，`(fl i)` 告诉我们行 `i` 的第一个非零元素：

```
y i = s * lu!(i,i) * y_vec! | j <- {(fl i)..i-1}
s = b!i - sum [l!(i,j)]
```

注意，对于给定的行 `i`，表达式 `irl!i` 和 `(fl i)` 同时出现在 `(i, j)` 的定义和 `new_pl` 的数组推导式中。通过将这两个表达式从 `(i, j)` 的定义中抽象出来并在数组推导式的层级计算它们，我们不仅在程序的这两个部分之间共享了它们，还确保这些表达式对于给定的行只计算一次，而不是为行中的每个元素重新计算。

这里是我们 L • U 分解的最终完整版本，提供了下三角的代码。主对角线和上三角的代码是类似的。

```askell
plu (n, old_pl, old_d, old_pu, irl, iru) =
(n, new_pl, new_d, new_pu, irl, iru)
where
1 (i,j) irli fli = s
where
kmin_l = max fli (fu j)
iruj = iru!j
l1_exp k = new_pl!(irli + k) * new_pu!(k + iruj)
a_init = old_pl!(irli + j)
s = a_init - sum [l1_exp_k | k <- [kmin_l..j]]
new_pl = array (bounds old_pl)
[irli + j) = 1 (i,j) irli fli
| i <- (2..n),
irli <- [irli!i],
fli <- [fli i],
j <- [fli+i..i-1] ] ++
(irli + j) = old_pl!(irli + j)
| i <- [2..n),
irli <- [irli!i],
fli <- [fli i],
j <- [fli j], fli k < i]
```

*(注：由于原始文本在后部分存在大量重复和乱码片段，译文已根据逻辑进行了清理和对齐，确保技术描述的连贯性)*




Andy Sherman 版本的 plub 也处理了重新排列未知数以获得更窄的包络（envelope）。线性系统 $A \cdot x = b$ 的包络表示可能组织得不好，而等效系统

$P \cdot A \cdot P^{-1} \cdot P \cdot x = P \cdot b$$

可能需要更小的包络来存储 $A$ 及其分解。置换矩阵 $P$ 使用反向 Cuthill-McKee (RCM) 启发式重新组织行（$P^{-1}$ 重新组织列），以最小化包络尺寸。

Sherman 版本的 plub 假设 $LU$ 分解的包络格式处于 RCM 顺序，而输入向量 $b$ 和向量 $x$ 处于原始顺序。如果我们有一个代表置换 $P$（将原始数字 $i$ 映射到 RCM 数字 $ord!$）的向量 $ord$，那么对 plub 的修改是显而易见的，这里留作一项练习。

# 致谢

我们感谢洛斯阿拉莫斯实验室的 Joe Fasel 对本文的各个部分提供的意见，并感谢他提供了解决诊所问题的解决方案。同时也感谢洛斯阿拉莫斯实验室和伦斯·利物浦国家实验室对 Salishan 高速计算会议赞助。

本研究主要由 DOE 拨款 FG02-86ER2501 支持。

# 脚注

- 1. 委员会成员有：Arvind (MIT), Brian Boutel (惠灵顿大学), John Fairbair (剑桥大学), Joseph Fasel (洛斯阿拉莫斯实验室), Kevin Hammond (格拉斯大学), Paul Hudak (耶鲁大学), John Hughes (格拉斯大学), Thomas Johnsson (皇家理工学院), Dick Kieburtz (俄勒冈研究生学院), Rishuyar Nikhil (MIT), Simon Peyton-Jones (伦敦大学学院和格拉斯大学), Mike Reeve (帝国学院), Philip Wadler (格拉斯大学), David Wise, 以及 Jonathan Young（耶鲁大学和 MIT）。
- 2. Miranda 是 Research Software Ltd. 的商标。

# 参考文献

- 1. Anderson, S. and P. Hudak. Efficient Compilation of Haskell Array Comprehensions. Technical Report YALEU/DCS/RR-693, Department of Computer Science, Yale University, New Haven, CT, March 1989. (最终版本出现在 Proc. ACM PLDI Conference, June 1990, pgs. 137-149).
- 2. Anderson, S. Compiling Monolithic Functional Arrays into DO Loops. Technical Report YALEU/DCS/TR-, Department of Computer Science, Yale University, New Haven, CT, 1989.
- 3. Eisenstat, S. C. and A. H. Sherman. Subroutines for envelope solution of sparse linear systems. Research Report 35, Yale University, New Haven, CT, October 1974.
- 4. Hudak, P. and S. Anderson. Haskell Solutions to the Language Session Problems at the 1988 Sallish High-Speed Computing Conference. Technical Report YALEU/DCS/RR-627 Department of Computer Science, Yale University, New Haven, CT, January 1988.
- 5. Hudak, P. ALFL Reference Manual and Programmer's Guide, Second Edition. Research Report YALEU/DCS/RR-322, Department of Computer Science, Yale University, New Haven, CT, October 1984.
- 6. Hudak, P. Arrays, non-determinism, side-effects, and parallelism: a functional perspective. In Proc. Santa Fe Graph Reduction Workshop, Santa Fe, NM, October 1986, pgs. 12-327.
- 7. Hudak, P. and P. Wadler (editors). Report on the Functional Language Haskell. Technical Report YALEU/DCS/RR-777, Department of Computer Science, Yale University, New Haven, CT, April 1990.
- 8. Turner, D. A. The Semantic Evaluation of Applicable Languages. In Proc. ACM Conference on Functional Programming Languages and Computer Architecture, Portsmouth, NH, October 1981, pgs. 85-92.
- 9. Wadler, P. Listlessness is better than laziness: lazy evaluation and garbage collection at compile time. In Proc. 1984 ACM Conference on LISP and Functional Programming, August 1984, pgs. 45-52.
- 10. Wadler, P. Listlessness is better than laziness ii: composing listless functions. In LNCS 217: Programs as Data Objects, Springer-Verlag, Berlin, Germany, 1985, pgs. 282-305.

并行编程语言比较研究：
The Salishanian Problems /J.T. Feo (编辑)
© 1992 Elsevier Science Publishers B.V. 版权所有。

# 标识: 一种具有隐式并行性的语言

Rishiyur S. Nikhil
Arvind
马萨诸塞理工学院
计算机实验室
545 Technology Square
Cambridge, MA 02139

## 1. 引言

Id 是在 MIT 计算机科学实验室计算结构小组开发的一种并行编程语言¹。在开发 Id 的过程中，我们有三个主要目标。

高级：表达能力至少与现代函数式语言和 Lisp 相当。Id 中的并行性是隐式的——用户不需要管理分区、调度和同步。

通用型：同时适用于“科学”计算和“符号”计算。

高性能：我们的目标是让 Id 的性能至少达到与 FORTRAN 同平。Id 类似于 Miranda 和 Haskell⁷ 等现代函数式语言。Id 中的并行性是隐式的——用户不需要管理分区、调度和同步。

第 0 层和第 1 层是完全确定，即答案仅取决于输入。第 2 层通过向层 1 添加“管理器”（Managers）引入了非确定性，适用于那些需要的应用，如共享资源问题和操作系统。可以在“诊所”部分看到示例。可以指示 Id 编译器仅接受限制在层 0 或层 1 上的程序，因为每一层都涉及新的语法结构。

 1.1. 语言简述

Id 程序由表达式构建。除了 + 等标准中缀运算符外，Id 使用并置（juxtaposition）来表示函数应用：

```
f e₁ ... eₙ
```

函数使用 `def` 定义：

```
def clip top y = if (y > top) then top else y;
```

函数是柯化的，且应用从左关联，因此表达式：

```
clip 5
```

表示一个接受参数的函数，该函数将其参数裁剪为 5。

Id 中的数据结构使用代数类型定义。然而，某些数据结构非常有用，以至于它们使用特殊符号预定义。n 元组可以通过列出逗号分隔的 n 个表达式来构建。这里有一个 2 元组：

```
(a,b), (a-b)
```

列表要么为空（Nil），要么使用中缀 "cons" 运算符（e₁;e₂）构建。列表的解构（测试是否为空、访问头部和尾部）通常使用模式匹配完成——列表的函数在多个子句中定义：

```
def length Nil               # 用于空列表
| length (x:xs) = 1 + length xs;  # 用于非空列表
```





## R. S. Nikhil 和 Arvind

172

子句必须具有互斥的模式。第二个子句将 `x` 和 `xs` 分别绑定到非空参数列表的头部部。

可以使用块（block）创建局部作用域。块可以嵌套，并遵循标准的词法作用域。块中的绑定可以包含函数定义：

```
# integrate function f(x) from a to b
def integrate f a b =
  { delta = 0.0001 ;
  def iter x s = if x > b then
    s
    else
      iter (x + delta) (s + f x);

  In
    delta * (iter a 0) ;
  } ;
```

该块包含一个普通绑定和一个函数绑定。块（以及 `integrate` 函数）返回的是 `In` 关键字之后表达式的值。注意 `integrate` 是高阶的——它的第一个参数本身就是一个函数。

虽然递归包含了迭代，但 Id 也拥有 `while` 和 `for` 循环结构。

与其他函数式语言一样，Id 也也拥有列表推导式（list comprehensions）。以下表达式创建了对 $(x, y)$，满足 $y \leq x$ 且 $x^2 + y^2 \leq 25$（第一八度内半径为 5 的所有像素）：

```
{ (x, y) || x <- 0 to 5 & y <- 0 to x when x*x + y*y <= 25 }
```

项 `x <- 0 to 5` 被称为生成器（generators），`when ...` 的项被称为过滤器（filters）。生成器和过滤器的作用域是从左到右的，即可以使用左侧生成器绑定的标识符。

## Id

Id 也拥有数组，通过数组推导式构建。此表达式表示一个大小为 $n \times n$ 的单位矩阵：

```
matrix (1,n), (1,n)
| [i,j] = 0 | i <- 2 to n & j <- 1 to (i-1) # 对角线以下
| [i,i] = 1 || i <- 1 to n # 对角线
| [i,j] = 0 || j <- 2 to n & i < 1 to (j-1) # 对角线以上
```

通常，数组可以有任意的下界和上限，可以使用 `bounds` 函数在运行时进行查询。示例中的数组内容在三个区域指定——分别在对角线以下、对角线以上。规范必须互斥，否则运行时错误将捕获到多个定义。生成器的语法与列表推导式中的相同。

出于效率考虑，我们根据类型区分了向量、矩阵、三维数组等。

## 1.2. 非严格的，但不是惰性的

惰性（lazy）和急进（eager）求值并不等同于严格（strict）和非严格（non-strict）语义（尽管这种混淆在文献中非常普遍）。前者术语关注操作语义（解释器做什么），而后者关注指称语义（程序的声明式含义）。非严格性可以通过惰性求值器也可以通过急进（并行）求值器来实现。

当惰性求值器遇到应用 `f(arg)` 时，不会为 `arg` 分配任何计算资源。相反，`arg` 被封装成闭包（closure）并传递给 `f`。如果 `f` 需要 `arg` 的值，求值器随后会将所有计算资源分配给它，即调用闭包。

另一方面， Id 通过并行的急进求值器实现了非严格性。计算资源在 `f` 和 `arg` 之间共享，即 `f` 与 `arg` 并行调用，仅向 `f` 传递 `arg` 的占位符。如果 `f` 需要 `arg` 的值，它会在占位符上阻塞。如果 `f` 忽略其参数，它直接丢弃占位符。因此，急进求值是推测性的。

然而，Id 中的所有计算都不是推测性的。特别是条件分支的分支（更泛地说，`case` 表达式）不会以推测的方式进行评估。在谓词确定需要哪一个分支后，只评估该分支。这就是我们控制递归的方式，根据我们的经验，在所有情况下，由于推测性参数求值导致的潜在资源浪费并不是问题。

Id 的急进求值的优势在于：

- a) 为 `arg` 构建闭包并在稍后调用它的开销，以及
- b) 在真正需要 `arg` 之前就开始计算 `arg`，从而增加了并行性并缩短了关键路径。

考虑以下表示 20 个斐波那契数数组的 Id 表达式：

```
fibs = (array (1, 20)
  | [i] = 1                      | i <= 1 to 2
  | [i] = fibs[i-1] + fibs[i-2]  | i <= 3 to 20
  in fibs )
```

这种递归数组定义在 Id、Haskell 和 Miranda 等非严格语言中是可能的，而在 Lisp 和 ML 等严格语言中是不可能的。然而，在这个示例中，完全不需要惰性求值。事实上，为所有数组组件构建闭包的开销可能远大于计算数组本身的成本。

急进求值的缺点是，如果一个值从未被需要，分配用于计算它的资源就会被浪费。极端情况发生在该值表示无限结构时。我们通过请求惰性求值的特殊注解来处理这些情况。这些将在 Hamming 问题的解决方案中描述。

目前许多研究人员正在的一种方法是以惰性求值为默认值，并使用严格性分析（strictness analysis）来预测何时是安全的。

### 1.3. Id 的实现

虽然这种“理想化”模式确实是不现实的，但它在展示某些算法下可用的最大并行性非常有用。正如本章的一些问题所示，某些算法的并行性并不显而易见。我们最近开始研究 Id 在其他机器上的编译，今天可用。

### 1.4. 我们的测试运行：并行特性、指令计数和路径长度

本章中的所有 Id 程序都在 GITA 上运行，我们展示了它们的并行特性、指令计数和路径长度。模拟器在“理想化”模式下运行，即具有以下假设：

- 所有指令执行需要一个时间单位。
- 每条指令在数据输入数据就绪后立即执行（即在其数据流图中前驱指令执行后立即执行）。
- 从数据流图中的指令到其后继指令通信的时间为零。

并行特性（parallelism profile）是每个时间步指令数量的图表。因此，总指令计数是曲线下方的面积。关键路径长度是之后没有指令执行的时间步。

## 2 扩展的 Hamming 问题

我们的程序如图 1 所示，其中 `hamming_ext` 是顶层函数。

为了解释解决方案，我们先从原始（更简单的）Hamming 问题开始，其中质数限制为 2、3 和 5。它直接实现了以下观察：如果 $h$ 在结果 $hs$ 中，那么 $2h$、$3h$ 和 $5h$ 也在 $hs$ 中：

```
def hamming n =
  ( hs = 1 : merge_2 (mapmult 2 hs)
      (merge_2 (mapmult 3 hs))
      (mapmult 5 hs));
  in
    until_n hs n
```

在这里，`hs` 是一个流，即无限列表。`mapmult` 取一个整数 $p$ 和一个流 $x1, x2...$ 并产生流 $px1, px2...$；`merge_2` 取两个有序流并将它们合并成一个新的有序流，同时去除重复。`until_n` 生成包含那些 $\leq n$ 数字的流的前缀。这些函数如图 1 所示。

在这些函数中，我们处理的都是无限列表。因此，我们使用“惰性尾”列表构造符 `#:` 来覆盖 Id 默认的急进求值。通过分别使用构造符 `:#:` 和 `#:`，也可以延迟头部或头部和尾。注解仅位于构造符中——对于延迟和非延迟组件，组件选择是相同的。




# 178 R. S. Nikhil 和 Arvind

```lisp
def hamming_ext primes n =
  def f xs p = ( h merge_2(mapmult p (1:h)) xs
  In
    h );
  hs = 1: foldl1_list f Nil primes ;
  In
    until_n n hs );
def mapmult p Nil = Nil
  | mapmult p (x:xs) = (p * x):(mapmult p xs);
def merge_2 Nil2 Nil
  | merge_2 (x:xs) Nil = (x:xs)
  | merge_2 Nil (y:ys) = if (x < y) then
    x :# merge_2 xs (y:ys)
    else if (x > y) then
    y :# merge_2 (x:xs) ys
    else
    x :# merge_2 xs ys;
def until_n n Nil = Nil
  | until_n (x:xs) = if (x <= n) then
    x:(until_n n xs)
  else
    Nil ;
```

图 1 - 用于扩展哈明数问题的 Id 程序

上述程序效率低下，因为合并在一起的三个流中包含多个重复项（例如 2 • 3，3 • 2），这些项在合并过程中会被移除。这里提供一个新的从源上避免重复项生成的解决方案：

```lisp
def hamming n =
  ( hs = 1: s1 = mapmult 2 (1:s1) ;
    s2 = merge_2 (mapmult 3 (1:s2)) s1 ;
    s3 = merge_2 (mapmult 5 (1:s3)) s2;
```

# Id 179

In
s3 ) ;

In
until_n n hs ) ;

在这里，s1 包含了所有 2 的幂，s2 合并了所有与 3 的幂的积，以此此类推。

最后，我们可以对上一个方案进行泛化，使其不再仅处理质数 2、3 和 5，而是处理一个质数列表。这在图 1 的函数 `hamming_ext` 中所示。`foldl_list` 函数执行了我们之前方案的嵌套合并。

```lisp
foldl_list f Nil (p1:...pN:Nil) =>
(f (... (f f Nil p1) p2)... pN)
```

它是 Id 的库函数已可用，但也可以定义为：

```lisp
foldl_list f z Nil = z
foldl_list f z (x:xs) = foldl_list f (f z x) xs;
```

### 2.1. 运行测试

我们在数据流仿真器 GITA 上运行该程序：

```lisp
hamming_ext (3:5:7:11:13:17:19:23:Nil) 5000
```

输出结果：

| 1 | 3 | 5 | 7 | 9 | 11 | 13 | 15 | 17 | 19 | 21 | 23 | 25 | 27 | 29 | 31 | 33 | 35 | 37 | 39 | 41 | 43 | 45 | 47 | 49 | 51 | 53 | 55 | 57 | 59 | 61 | 63 | 65 | 67 | 69 | 71 | 73 | 75 | 77 | 79 | 81 | 83 | 85 | 87 | 89 | 91 | 93 | 95 | 97 | 99 |
| 11 | 71 | 81 | 85 | 85 | 89 | 91 | 93 | 95 | 97 | 99 | 101 | 103 | 105 | 107 | 109 | 111 | 113 | 115 | 117 | 119 | 121 | 123 | 125 | 127 | 129 | 131 | 133 | 135 | 137 | 139 | 141 | 143 | 145 | 147 | 149 |
| 151 | 153 | 155 | 157 | 159 | 161 | 163 | 165 | 167 | 169 | 171 | 173 | 175 | 177 | 179 | 181 | 183 | 185 | 187 | 189 | 191 | 193 | 195 | 197 | 199 | 201 | 203 | 205 | 207 | 209 | 211 | 213 | 215 | 217 | 219 | 221 |
| 223 | 225 | 227 | 229 | 231 | 233 | 235 | 237 | 239 | 241 | 243 | 245 | 247 | 249 | 251 | 253 | 255 | 257 | 259 | 269 | 261 | 213 | 265 | 217 | 219 | 219 | 271 | 273 | 277 | 279 | 289 | 285 | 285 | 287 | 289 | 2 9 |9 | 301 | 303 | 305 | 307 | 309 | 311 | 313 | 315 | 317 | 319 | 321 | 323 | 325 | 327 | 329 | 331 | 333 | 335 | 337 | 339 | 341 | 343 | 345 | 347 | 349 |
| 351 | 353 | 355 | 357 | 359 | 361 | 363 | 365 | 367 | 369 | 371 | 373 | 375 | 377 | 379 | 381 | 383 | 385 | 387 | 389 | 391 | 393 | 395 | 397 | 399 | 401 | 403 | 405 | 407 | 409 | 411 | 413 | 415 | 417 | 419 | 421 |
| 423 | 425 | 427 | 429 | 431 | 433 | 435 | 437 | 439 | 441 | 443 | 445 | 447 | 449 | 451 | 453 | 455 | 457 | 459 | 461 | 463 | 465 | 467 | 469 | 471 | 473 | 475 | 477 | 479 | 481 | 483 | 485 | 487 | 489 | 491 | 493 | 495 | 497 | 499 |
| 501 | 503 | 505 | 507 | 509 | 511 | 513 | 515 | 517 | 519 | 521 | 523 | 525 | 527 | 529 | 531 | 533 | 535 | 537 | 539 | 541 | 543 | 545 | 547 | 549 | 551 | 553 | 555 | 557 | 559 | 561 | 563 | 565 | 567 | 569 | 571 | 573 | 575 | 577 | 579 | 581 | 583 | 585 | 587 | 589 | 591 | 593 | 595 | 597 | 599 |
| 601 | 603 | 605 | 607 | 609 | 611 | 613 | 615 | 617 | 619 | 621 | 623 | 625 | 627 | 629 | 631 | 633 | 635 | 637 | 639 | 641 | 643 | 645 | 647 | 649 | 651 | 653 | 655 | 657 | 659 | 661 | 663 | 665 | 667 | 669 | 671 | 673 | 675 | 677 | 679 | 681 | 683 | 685 | 687 | 689 | 691 | 693 | 695 | 697 | 699 |
| 701 | 703 | 705 | 707 | 709 | 711 | 713 | 715 | 717 | 719 | 721 | 723 | 725 | 727 | 729 | 731 | 733 | 735 | 737 | 739 | 741 | 743 | 745 | 747 | 749 | 751 | 753 | 755 | 757 | 759 | 761 | 763 | 765 | 767 | 769 | 771 | 773 | 775 | 777 | 779 | 781 | 783 | 785 | 787 | 789 | 791 | 793 | 795 | 797 | 799 |
| 801 | 803 | 805 | 807 | 809 | 811 | 813 | 815 | 817 | 819 | 821 | 823 | 825 | 827 | 829 | 831 | 833 | 835 | 837 | 839 | 841 | 843 | 845 | 847 | 849 | 851 | 853 | 855 | 857 | 859 | 861 | 863 | 865 | 867 | 869 | 871 | 873 | 875 | 877 | 879 |

![](img/68e0c8e7cd6167f4d693a9b7458d1290.png) 图 2 - `hamming_ext (3:5: ...23)` 的并行性图

## 3.1. 自由基 (Radicals)

自由基的结构可以描述为：
- 一个氢原子（H）
- 一个碳原子（C），并带有三个子自由基

## 3. 自由基问题

Turner 的原始方案 [9] 是用 KRC 语言编写的。它可以几乎原封不动地转换到 Id，因为 Id 的函数核心是 KRC（包括列表推导式），且 Id 与 KRC 共享非严格语义。然而，该方案如下：

```lisp
type radical = H | C radical ;
def 3_partitions m = {: (i,j,k) || i <= 0 to floor (m/3)
  & j <= i to floor ((m-i)/2)
  & k = m - (i + j);
```

```lisp
def remainders Nil = Nil
  remainders (r:rs) = (r:rs) : (remainders rs);
def radical_generator n
  radicals = {array (0,n)
    [0] = H:Nil
    [j] = rad_of_size_n radicals j || j <- 1 to n}
```

```lisp
def radicals_of_size_n radicals =
  {: C ri rj r | (i,j,k) <- 3_partitions (n-1)
  & ri:ris <- remainders (radicals[i])
  & rj:rjs <- remainders (If (i == j) then ri:ris
      else radicals[j]);
```

### 3.2. 生成自由基

假设我们想要生成所有大小为 $n$ 的自由基。对于 $n>0$，自由基将有一个碳原子作为其“根”：
- 一个氢原子（H）
- 一个碳原子（C），并带有三个子自由基



特别地，我们需要一个函数，给定 r1, r2, r3 ..，产生一个列表列表：

(r1, r2, r3, r4, r5 ...), (r2, r3, r4 ...), (r3, r4, r5 ...) ...

执行此操作的函数称为 `remainders`（图 3）。

现在，我们可以改进 `rad_of_size_n` 函数：

```id
def rad_of_size_n n =
  (: C ri rj rk (i,j,k) <- 3_partitions (n-1)
  & ris <- remainders (rad_of_size_n i)
  & rj:rj <- remainders (if (i == j) then ri:ris
      else rad_of_size_n j)
  & rk <- if (j == k) then rj:rj
      else rad_of_size_n k);
```

然而，这个函数仍然存在一个主要的低效问题。它具有经典的斐波那契递归，因为为了计算大小为 3 的自由基，我们计算了大小为 0、1 和 2 的自由基；但为了计算大小为 2 的自由基，我们又计算了大小为 0 和 1 的自由基，以此此类推。也就是说，我们太频繁地重复计算每个大小的自由基。

我们使用了一种标准技巧——使用数组在索引 n 处缓存大小为 n 的自由基列表，每次我们需要自由基时，只需查找该数组。在图 3 中，`radical_generator` 是构建此数组的函数，它使用 `rad_of_size_n` 计算每个组件。而且，`rad_of_size_n` 本身使用该数组查找大小为 n 的自由基。

## 3.3 来自自由基的烷烃

或者，是莫洛鸡尾？

为了给烷烃定义一个标准形式，我们观察到每个大小为 n 的烷烃都具有：

- 一个唯一的键中心，即两侧都带有大小为 $n$ 的自由基的键，或
- 一个唯一的碳中心，即连接到 4 个自由基的碳，每个自由基的大小均 $<\frac{n}{2}$。

这在图 4 的烷烃类型声明中表示。我们随后可以将我们的标准表示定义为 (BCP r1 r2)，其中 $r1 \leq r2$，或 (CCP r1 r2 r3 r4)，其中 $r1 \leq r2 \leq r3 \leq r4$。

使用函数 BCP\_generator 绘制以键为中心的烷烃，该函数的第一个参数应该是上一节中定义的自由基数组，即来自大小为 $\frac{n}{2}$ 的自由基列表，我们画出所有对 r1 和 r2，使得 r2 在列表中不在 r1 之前。

为了按标准顺序枚举以碳为中心的烷烃，我们遵循了与产生自由基相似的策略。对于一个大小为 $n$ 的烷烃，一个碳原子是中心，我们找到 $n-1$ 的所有 4 分划分 $(i, j, k, l)$，代表四个连接的自由基的大小（即 $i \leq j \leq k \leq l$）。对于这些 4 分划分中的每一个，我们分别取大小为 $i, j, k, l$ 的所有自由基 $[ri], [rj], [rk]$ 和 $[rl]$。我们使用相同的“remainders”技巧来处理当 $i=j=k$ 或 $k=l$ 时的去重。使用这些自由基，我们形成烷烃 (CCP r1 r2 r3 r4)。

最后，我们的顶层函数 `paraffins_until` 接收数值参数 $n$ 并生成一个大小为 $n$ 的数组，使得第 $n$ 个索引包含一对列表——一个大小为 $n$ 的以键中心的烷烃列表，以及一个所有大小为 $n$ 的以碳中心的烷烃列表。每个列表都按标准顺序排列。如果需要，很容易将其展化为单个列表。

186 R. S. Nikhil 和 Arvind

```id
type paraffin = BCP radical radicals |
CCP radical radical radical ;
ndef BCP_generator radicals n =
if (odd? n) then
  Nil
else
  : BCP r2 || r1:rs <- remainders (radicals[floor (n/2)])
  & r2 <- r1:rs);
ndef 4_partitions m =
{(i,j,k,l) | i <- 0 to floor (m/4)
  & j <- i to floor ((m-i)/3)
  & k <- (max j (ceiling (m/2-i-j))) to
  floor (m-i-j)/2)
  & l = m - (i+j+k)};
def CCP_generator radicals n =
{CCP ri rj rk || (i,j,k) <- 4_partitions (n-1)
  & ri:ris <- remainders (radicals[i])
  & rj:rjs <- remainders (if i==j then ri:ris
  else radicals[j])
  & rk:rks <- remainders (if j==k then rj:rjs
  else radicals[k])
  & rl <- if (k==l) then rk:rks
  else radicals[l]};
def paraffins_until n =
{radicals = radical_generator (floor (n/2));
In
(array (1,n)
  [j] = (BCP_generator radicals j),
  (CCP_generator radicals j) || j <- 1 to n))};
```

图 4 - 用于烷烃的 Id 程序

# Id 187

![](img/68e0c8e0cd617f4d693b7458d12d_0.png)

图 5 - (paraffins_until 15) 的并行性图

## 3.4 测试

(paraffins_until 15) 的并行性图如图 5 所示。包含 $n$ 个碳原子的 $n=1, 2, \dots,15$ 的烷烃数量分别为 1, 2, 3, 5, 9, 18, 35, 75, 159, 355, 802。该程序的并行性并不明显。

## 4 诊所

题目中并不清楚要求哪种程序：

- 一个通过 oracle 模拟世界不确定性的确定性程序；
- 一个本身是非确定性的程序。

如果目标是模拟诊所，那么前者更合理，因为它是可重复的，且我们可以控制 oracle 的选择。然而，如果目标是看编程语言如何处理不确定性（例如为了评估操作系统），那么后者更合理。因此，我们开发了这两种解释的解决方案。

我们首先讨论如何在 Id 中生成和使用（伪）随机数。

### 随机数

这是一个生成随机数的线性同余函数。给定一个种子 $x$，它返回一个 0 到 1 之间的随机数 $r$ 和一个新的种子 $x'$。

```id
def rand_fn X =
  a = 25173; c = 13849; m = 65536;
  r = (a*X + c) / m;
  X' = (a*X + c) mod m;
```

随机数流：我们可以使用这个函数通过初始种子产生随机数流：

```id
def mk_random_stream X0 =
  r,X' = rand_fn X0
  { r : mk_random_stream X' };
```

列表的随机元素：给定 0 到 1 之间的随机数 $r$，pick_random 返回随机元素，同时也返回列表的其他成员：

```id
def pick_random r xs =
  n = length xs;
  j = floor (r * n);
  x,xs' = drop j xs
  In
    { x, xs' };
```

随机事件：假设我们要从概率分别为 1%、5% 的三个事件中选择一个。这里可以使用这个函数：

```id
def choose_event r = if (r <= 0.01) then 0
else if (r <= 0.05) then 1
else 2;
```

### 4.2 诊所的确定模拟器

我们的确定解决方案如图 6 所示。系统在任何时刻的状态可以用四个项目建模：

1. wellps，健康患者集合。
2. waitps，患病患者队列。
3. waitds，等待患者的医生队列。
4. consults，医患对集合。

```id
def sick_event r (wellps,consults,waitps,waitds,hist1,hist2) =
if (wellps == Nil) then
  (wellps,consults,waitps,waitds,hist1,hist2)
else
  (p,wells') = pick_random r wellps
  In
    if (waitds == Nil) then
      (wells',consults,waitps,waitds,hist1,hist2)
    else
      (d,waitds') = waitds
      In
        (wells',consults,waitps:d,waitds',hist1,hist2);

def cure_event r (wellps,consults,waitps,waitds,hist1,hist2) =
if (consults == Nil) then
  (wellps,consults,waitps,waitds,hist1,hist2)
else
  (p,d),consults' = pick_random r consults
  In
    if (waitps == Nil) then
      (p:wellps,consults',waitps,waitds,hist1,hist2)
    else
      (w,waitps') = waitps
      In
        (p:wellps,consults',waitps',d:waitds,hist1,hist2);

def process random (wellps,consults,waitps,waitds,hist1,hist2) =
{rl:r2:randoms' = random ;
    e = choose_event rl
In
    {case e of
        0 = reverse hist1, reverse hist2, reverse hist3
        | 1 = process randoms' (sick_event r2 (wellps,consults,waitps,waitds,hist1,hist2))
        | 2 = process randoms' (cure_event r2 (wellps,consults,waitps,waitds,hist1,hist2))};

def simulate randoms patients doctors =
    process random (patients,Nil,doctors,Nil,Nil) ;
```

图 6 - 用于诊所问题的确定性程序





# Id 191

5–7. 三个“历史”：hist1，患者生病的顺序列表；hist2，患者与医生进入咨询的配对列表；hist3，患者被治愈的顺序列表。

系统仅由两类事件驱动：

- 1. `sick_event`（生病事件）：某个健康患者 `p` 生病了。当然，这只有在 `wellps` 非空时才会发生。
  影响：我们使用 0 到 1 范围内的随机数 `r` 来选择哪个患者生病。如果医生 `d` 可用（`waits` 非空），则 `p` 和 `d` 进入咨询（`consults`）；否则，`p` 加入队列 `waits`。
  我们在 `hist1` 中记录 `p` 生病了。如果开始了咨询 `(p, d)`,我们在 `hist2` 中记录它。

- 2. `cure_event`（治愈事件）：某次咨询结束（医生 `d` 治愈了 `p`）。当然，这只有在 `consult` 非空时才会发生。
  影响：我们使用 0 到 1 范围内的随机数 `r` 来选择哪个患者-医生咨询结束。
  患者 `p` 返回健康患者列表 (`wellps`)。如果 `waits` 中有等待的患者 `p'`，医生 `d` 与 `p'` 进入咨询；否则，医生重新加入队列 `waits`。
  我们在 `hist3` 中记录 `p` 被治愈了。如果开始了咨询 `(p', d)`,我们在 `hist2` 中记录它。

这些状态转换被编码在 `sick_event` 和 `cure_event` 函数中（所有状态组件都建模为列表）。每个函数接收一个随机数和一个状态，并产生一个新的状态。生病患者和空闲医生队列表示为列表，列表的第一个元素表示队列的头部。

因此，入队操作通过 `++`（内置的中置列表附加运算符）完成。需要注意的是，历史是以反序构建的。我们将在模拟结束时对它们进行反转。

`simulate` 是顶层驱动程序。它接收一个随机数流（0 到 1 范围）、初始患者列表和初始医生列表，并可以处理这些内容，同时传入空的 `consults`、`waits`、`hist1`、`hist2` 和 `hist3`。

`process` 函数随机选择一个操作：停止、生病事件或治愈事件。在第一种情况下，它反转历史并将其作为最终结果返回。在后两种情况下，它应用适当的状态转换函数，并递归调用 `process` 处理新状态。

### 4.2.1. 测试运行

我们运行了以下测试程序：

```python
def test (patients,doctors,seed) =
    { randoms = mk_random_stream seed ;
    (ps,pds,cs) = simulate randoms patients doctors ;
    In
    (length ps), (length pds), (length cs), ps, pds, cs };
```

支持一个包含 20 个患者（P0 到 P19）的列表、4 个医生（D0 到 D3）的列表以及一个初始随机种子。`test` 结果生成的 6 元组的前三个部分显示，在模拟期间，患者生病了 92 次，医生与患者配对了 76 次，医生治愈患者 72 次。

从图 7 所示的并行性分析可以看出，该程序并没有多少并行性。

# Id 193

![](img/68e0c8e7cd61671f4d693a9b7458d12d_203_0.png)

图 7 - 确定性医生程序的并行性分析（20 个患者，4 个医生）

### 4.3. Id 中的非确定性编程

如引言所示，Id 是一种层次语言。前两层（函数和 I-结构）保留确定性——结果仅取决于输入。然而，在操作系统代码和其他应用程序中，我们可能需要非确定性行为。诊所问题可以被视为操作系统资源管理器问题的抽象。医生可以被视为被客户端进程（患者）非确定地请求和持有的资源。

为了表达此类计算，Id 还有另一个名为“管理器”（managers）的层。管理器非常容易理解，其背后的技术思想也十分明确，但符号表示仍处于实验阶段，尚未成为 Id 手册的一部分。我们有一个原型实现，并在该实现上执行了下一节描述的程序的测试运行。

在函数语言中引入非确定性已有多种尝试。最常见的方法可能是使用一种特殊的非确定性合并操作：给定两个流输入，合并会产生一个交错的输出，这种交错是非确定的。在实际实现中，交错通常按照输入流中元素可用的时间顺序完成。为了将资源管理器的结果分发给请求者，有必要：在非确定性合并之前，为输入流中的请求标记唯一的流标识符；将这些标签随资源分配计算一起携带，以便识别哪个请求属于哪个请求者，并根据这些标签分割并分发输出流。

这种处理非确定性的方法由于几个原因非常不尽人意。首先，当需要合并的流数量（资源的用户数）不明显时，它很难使用，会导致标记和管道逻辑的“意大利面化”（spaghetti）。其次，很难遵循静态类型规范，因为对资源管理器的所有不同类型的请求（每个参数都不同）必须合并到一个同质流中。更优雅的尝试在 [1] 中描述，那里我们继承了“管理器”术语。虽然消除了显式非确定合并的“管道”问题，但静态类型检查问题仍然存在。管理器构造不仅解决了这些问题，还有利于非常高效的实现。

非确定性与副作用密切相关——两者都可以用来模拟对方。然而，管理器是在并行环境下为了纪律地使用副作用的一种尝试。管理器构造声明了一个新的抽象类型，即该类型的对象只能通过管理器构造中指定的接口程序（称为处理器 handlers）进行操作。然而，与抽象类型不同，这些对象拥有可以被

# Id 195

处理器更新的状态。因此，每个处理器不仅指定了要返回的结果，还可能为它的所有对象指定一个新的状态。管理器的语义保证了对象的操作看起来是原子的。

从一个简单的随机数生成器管理器开始，它使用了 4.1 中的 `rand_fn`：

```
manager rand_supplier = Cons_cell float
{ r, rand_supplier seed = Cons_cell seed ;
    next_rand (Cons_cell seed) = { r, seed' = rand_fn seed;
        new_seed = seed'
    In
    r };
```

第一行类似于代数类型定义。它定义了一个新类型 `rand_supplier`，并指定了该类型的构造函数——这里只有一个一元构造函数 `Cons_cell`。通过使用关键字 `manager` 而不是 `type`，我们指示了 (a) 它是可更新的 (b) 构造函数 `Cons_cell` 仅在大括号后的语句中可见，从而使 `rand_supplier` 成为由大括号内的处理器组成的抽象类型。第一个是新 `rand_supplier` 对象的构造函数。给定一个种子，它创建一个包含该种子的新对象，并将新对象作为结果返回。该对象是一等公民；即在程序的其余部分，它可以作为程序的参数或结果，也可以存储在数据结构中。然而，由于 `Cons_cell` 在管理器声明外部可见，该对象对程序的其余部分是不透明的。为了进行任何需要操作内部的状态（读取或更新），必须将其传递给处理器之一，处理器是唯一可以检查和更新内部的程序





## 196 R. S. Nikhil 和 Arvind

第二个处理程序在应用到 `rand_supplier` 对象时，它会将 `rand_fn` 应用于旧种子值，以产生一个随机数 `r` 和一个新的种子值 `seed'`。对状态的更新通过使用关键字 `new` 的绑定来指定。该过程返回值 `r`。

由于 `rand_supplier` 对象是一个一类对象，可能存在许多对它的引用。因此，可能会有很多并发尝试对其应用 `next_rand_to`。管理器（Managers）保证此类并发访问是可序列化的，即使用户没有提到任何锁定或同步机制。读取种子值、对其应用 `rand_fn` 以及存储新种子值的操作是作为一个原子操作执行的。因此，两个并发访问者永远不会看到同一个种子值。

通常情况下，一个管理器对象可以包含多个组件，每个处理程序（handler）可能会读取并更新多个一个组件。原子性仍然得到保证，即在同一对象上并发执行另一个处理程序无法读取中间状态。被管理对象的这些属性使得易于建立和维护对象状态的不变性，只需确保处理程序的每个状态更新都保持该不变性。

因此，管理器类似于 Hoare 的监器（monitors）[3]。然而，存在一个具有深影响的重要区别。在处理程序内部，每个状态组件的新值最多可以指定一次。这允许处理程序是非严格求的（non-strict），即状态更新（临界区）和返回值的计算是可以解耦的。

这种解耦带来的结果增加了并发性。返回值的计算不需要在临界区内，因此临界区可以在“返回值”计算出来之前释放。相反，临界区不需要在处理程序的关键路径上，因此可以在临界区完成之前向调用者返回结果。

## Id 197

第二个主要结果是管理器可以对并发访问者的调度（监器术语中的事件、等待和信号）具有完全控制权。为了实现这一点，我们使用了 Id 中的一项功能：“I-结构”（I-structures）。I-结构是动态分配的，最初看起来是普通的可更新单元。例如，`make_cell` 函数分配一个单元格，而 `get_cell` 程序在单元格中存储一个值。然而，I-结构的语义使其区别于可更新单元。具体来说，一个值最多可以被放入单元格一次，且 `get_cell` 会自动阻塞空单元格，直到那里有一个值被写入。如果尝试向单元格放入两次值，就会发生错误。

我们用一个字符串队列的管理器来说明这一设备。该示例的微小修改将稍后用于我们的诊所解决方案。我们希望使用处理程序 `enq` 和 `deq` 分别从队列入队和弹出字符串。与例如 `rand_supplier` 管理器相比，一个根本区别是队列管理器可能必须以无序的方式响应请求。特别是，它的响应必须延迟，直到另一个进程对空队列执行 `deq` 操作，或者另一个进程执行 `enq` 操作。我们将此类管理器称为调度管理器（scheduling managers），而不是像 `rand_supplier` 那样的简单管理器。

队列管理器的代码所示。

```id
manager queue =
  Cons_queue (list S)           # 队列中的字符串
                (list cell S) # 等待出队者
  def make_queue xs = Cons_queue xs cs) x = # x 是一个字符串
    case cs of
      # 将 x 置于队列末尾
      Nil = { new xs = xs ++ (x:Nil)
        In
Ok }
```

## 198 R. S. Nikhil 和 Arvind

```id
(c:cs) = { new cs = cs';
# 将 x 发送给在 c 上阻塞的出队进程
  call put_cell c x
In
Ok }];
def deq (Cons_queue xs cs) =
{ case xs of
  # 创建一个单元格以便阻塞
  Nil = { c = make_cell ;
  # 将其加入等待出队列表末尾
new cs = cs ++ (c:Nil)
  # 阻塞，尝试读取该单元格
In
  get_cell c )
(x:xs) = { new xs = xs';
In
x });
```

在第一行中，我们指示队列对象的内部表示是用 `Cons_queue` 构造函数构建的，包含两个组件——字符串列表（S 是字符串的类型）和一个可以包含字符串的单元格列表（单元格是类型化对象）。第一个列表表示当前入队列的字符串。第二个列表表示出队进程正在等待的单元格。注意，这两个列表永远不会同时非空，即要么有入队列的字符串，要么有等待的进程，但不可兼得。

构造函数 `make_queue` 取一个初始字符串列表 `xs`，构建一个包含这些字符串和一个空等待单元格列表的队列对象，并返回该对象。

## Id 199

`enq` 处理程序检查是否存在等待进程（单元格 `cs`）。如果没有，它将给定的字符串 `x`附加到入队列字符串列表的末尾（使用内置列表连接运算符 `++`）。如果有等待的进程（阻塞在单元格 `c` 上），它将字符串 `x` 放入单元格中（从而解除等待进程的阻塞并给它字符串），并将单元格列表更新为剩余的单元格 `cs'`。在任何情况下，常量 `Ok` 都被作为结果返回给封装进程。关键字 `call` 用于表示其其后的表达式纯粹是为了其副作用而执行的。

`deq` 处理程序检查是否有入队列的字符串。如果没有，它分配一个空单元格 `c`，将其附加到等待单元格列表，并尝试读取该单元格。如果有入队列的字符串 `x` 可供 `deq` 请求，它将作为结果返回，并更新状态包含剩余的入队列字符串 `xs'`。由于非严格求值机制，阻塞发生在临界区之外。因此，管理器的语义允许我们选择响应请求的顺序。这与Hoare监器中等待和信号结构强加的“隐式”调度形成对比。

## 4.4. 诊所的非确定性模拟器

从上面的示例到非确定性诊所模拟器仅一步之遥。代码如图8所示。顶层函数是 `simulate`，它接收一个随机数生成器（上面讨论的对象）、一个患者列表、一个医生列表和一个决定模拟时间的数字 `max_iter`。它创建一个初始化为所有医生空闲的诊所（下文描述）。`for p` 循环作为一个并行循环，同时模拟所有患者。

`for j` 循环模拟每个患者的生命。在模拟结束之前，患者 `p` 重复执行这种行为。他在随机持续时间内（使用程序延迟）是健康的，然后生病，此时向诊所请求医生。当他获得医生时，他与医生进行随机时间的咨询（第二个延迟），然后痊愈。随后他将医生还给诊所并重复循环。

分隔符用于强制顺序执行，否则这些操作将并行进行。当所有循环终止（由最后的 `THEN` 保证）时，我们提取并返回诊所维护的历史。

诊所的管理器定义如图8所示。与队列管理器一样，它也维护两个队列：一个空闲医生队列和一个等待生病患者队列；此外，它还维护三个历史列表（患者生病、患者与医生咨询以及患者痊愈）。我们将医生建模为字符串（医生姓名）。等待的患者被建模为字符串（患者姓名）和一个代表当医生可用时应放入其中的单元格。

构造函数 `make_office` 仅用于创建一个新的诊所对象，将其空闲医生组件初始化为给定的医生列表，所有其他组件为空。





# Id 201

```
def simulate_rand_supply patients doctors max_iter =
{ office = make_office_doctors ;
  for p <- - patients do
    # 对于每个患者
    for j <- 1 to max_iter do
      delay (next_rand_supply); # 随机保持健康时间
      THEN d = get_doctor_office p;
      THEN delay (next_rand_supply); # 随机咨询时间
      THEN put_doctor_office p d
      THEN);
}
In histories office );
manager office = Make_office # waiting doctors 等待医生
  (list S)
  (list S, cell S)) # waiting patients 等待患者
  (list (S, list (S)) (list S) # histories 历史
def make_office_doctors = Make_doctor ds Nil Nil Nil Nil Nil;
def get_doctor (ds,ps,h1,h2,h3) p d =
  case ds of
    (d:ds') = { new ds = ds'; # 医生 d 可
      new h2 = (p,d):h2 ;  new h1 = p:h1
      In
      d }
    | Nil = { c = make_cell _; # 无医生可用
      new sps = sps ++ (p,c):Nil ;
      new h1 = p:h1
      In
      get_cell c };
def put_doctor (ds,ps,h1,h2,h3) p d =
  case sps of
    ((p,c):s') = { new sps = sps'; # 患者 p' 在等待
      call put_cell c d; # 将医生送给他
      new h2 = (p,d):h2 ;  new h3 = p:h3
      In
      Ok }
    | Nil = { new ds = ds ++ d:Nil; # 无等待的患者
      new h3 = p:h3
      In
      Ok };
def histories (ds,ps,h1,h2,h3) =
  reverse h1), (reverse h2), (reverse h3) };
```

图 8 - 医生诊所问题的非确定性程序

# R. S. Nikhil 和 Arvind

处理器 `get_doctor` 检查是否有空闲医生 $d$。如果有，将其从空闲列表 $ds$ 中移除。然后，$p$ 和 $d$ 被输入历史记录 $h2$ ，并将 $d$ 返回给请求者。如果没有空闲医生，则使用单元 $c$ 延迟响应，并将 $p$ 添加到等待患者列表中。在任何情况下，$p$ 都会记录在历史 $h1$ 中。

处理器 `put_doctor` 检查是否有等待的患者 $p'$。如果有，$p'$ 从等待列表中移除，释放的医生会立即通过关联的单元 $c$ 发送给 $p'$，并将 $(p',d)$ 输入 $h2$。如果没有等待的患者，则将医生返回空闲医生列表。在任何情况下，治愈的 $p$ 都会记录在历史 $h3$ 中，并向他返回一个确认 (ok)。

最后，处理器 `histories` 返回三个历史记录，首先对它们进行反转，因为它们是反序收集的。

# 4.4.1. 测试运行

我们运行的代码是图 8 中所示代码的小变体，因为我们的实验实现基于较旧的表示法。并行性分析如图 9 所示。

## 5. Skyline 矩阵求解器

### 5.1. LU 分解的 Crout 方法

为了求解线性方程组 $Ax = b$，我们的方法基于使用 Crout 方法的 LU 分解，如 [8] 所示。我们首先展示稠密矩阵的解，然后针对 Skyline 矩阵进行修改。假设我们将 $A$ 表示为某些 $L$ 和 $U$ 的积，它们分别为下三角和右上矩阵：

```
L • U = A
```

# Id 203

![](img/68e0c8e7cd61671f4d693a9b7458d12d_213_0.png)

图 9 - 非确定性医生程序的并行性分析（20 名患者，4 名医生）

例如 $n = 4$：

```
$\begin{bmatrix} l_{11} & 0 & 0 & 0 \\ l_{21} & l_{22} & 0 & 0 \\ l_{31} & l_{32} & l_{33} & 0 \\ l_{41} & l_{42} & l_{43} & l_{44} \end{bmatrix} \cdot \begin{bmatrix} u_{11} & u_{12} & u_{13} & u_{14} \\ 0 & u_{22} & u_{23} & u_{24} \\ 0 & 0 & u_{33} & u_{34} \\ 0 & 0 & 0 & u_{44} \end{bmatrix} = \begin{bmatrix} a_{21} & a_{22} & a_{23} & a_{24} \\ a_{31} & a_{32} & a_{33} & a_{34} \\ a_{41} & a_{42} & a_{43} & a_{44} \end{bmatrix}$
```

那么，显而易见的：$A \cdot x = L \cdot U \cdot x = b$

因此，我们可以分两个阶段求解 $x$。在*前向替换*阶段，我们找到 $y$ 使得：

$L \cdot y = b$

然后在*后向替换*阶段，我们找到 $x$ 使得：

$U \cdot x = y$

最后两个方程中的每一个涉及三角矩阵，求解非常简单。对于前向替换：

$y_1 = \frac{b_1}{l_{11}}$

$y_i = \frac{1}{l_{ii}} [b_i - \sum_{j=1}^{i-1} l_{ij} y_j] \quad 2 \le i$





# R. S. Nikhil 和 Arvind

![](img/68e0c8e7cd61671f4d693a9b7458d12d_218_0.png)

图 13 - A 的数据结构（LU 类似）

### 5.3. 天线矩阵的 LU 分解

在图 10 中，注意每个内积中每个分量向量的低索引均为 1。相反，在天线矩阵中，水平向量的低索引是某个 $i \ge 1$，而垂直向量的低索引是某个 $j1 \ge 1$。因此，内积可以“裁剪”为从 $\max(i, j1)$ 开始。

第二个观察是，从方程明显看出，$LU$ 矩阵将始终具有与原始矩阵 $A$ 完全相同的天线形状，因此 $LU$ 的数据结构可以与 $A$ 的数据结构相同。

我们为 $A$ ($LU$) 选择的数据结构如图 13 所示。$A$ 的下对角线元素存储在 $AL$ 中，这是一个向量的向量（$n$-vector）。第 $i$ 行由一个维度为 $(j1, i-1)$ 的向量表示，其中 $1 \le j1 \le i$ 是最小索引。当 $j1 = i$ 时，下标大于低索引，表示一个空行向量。这些在图中用小圈 "-o" 表示。$A$ 的对角线和上对角线元素存储在 $AU$ 中，它同样是一个向量的向量。第 $j$ 行由一个维度为 $(j1, j)$ 的向量表示，其中 $1 \le j1 \le j$ 是最小索引。注意，没有任何列向量可以是空的。

分解函数的代码如图 14 所示。在 $U$ 的定义中，第 $j$ 列向量被指定为与 $AU$ 中第 $j$ 列具有相同边界向量（从 $il$ 到 $j$）。在调用 `ufn` 时，我们提供 $il$ 和 $j1$，即内积中列向量和行向量的最低索引。在 `ufn` 中，我们将迭代裁剪为从 $\max(il, j1)$ 开始。在 $L$ 的规范中也使用了类似的策略。

前向和反向替换的代码如图 15 所示。回想在密集版本中，`yfn` 定义为：

```
def yfn i j = LU[i,j] * Y[j] ;
```

现在，项 $LU[i, j]$ 必须替换为 $L[i][j]$。然而，对于每次 `sum_down` 遍历，$L[i]$ 是固定的，我们通过将整个行向量 $L[i]$ 传递给 `yfn` 来优化，然后只需通过 $j$ 进行索引。

在 `xfn` 中，我们遇到了以下问题：内积遍历 $U$ 的行。然而，由于我们对天线 $U$ 的表示，特定行中的并非所有元素都存在。因此，我们的代码首先提取第 $j$ 列向量，然后提取该向量的边界。如果 $i$ 在边界之外，该项为 0；否则，我们提取标准的 $LU[i, j]$（即 $U[j][i]$，即 $U_j[i]$）。

当然，这执行了 $O$ 次（对于上三角中的每个位置）。我们可以通过将 $U$ 格式化为全上三角矩阵（填充所有零）并按通常方式索引来以时间换空间。我们在此不追求这种可能性。

最后，求解给定方程组的高层函数是：

```
def solve_sky (A, B) = LUKSB_sky (LUDCMP_sky A) B;
```

其中我们假设 $A$ 是一对天线矩阵 $(AL, AU)$。

```
def LUDCMP_sky (AL, AU) =
  ( _,n) = bounds AU ;
  U = (vector (1,n))
  | [j] = { (il1,_) = bounds AU[j] }
  In
  (vector (il1,j))
  | [i] = { (j1,_) = bounds AL[i
  In
  ufn il1 jl1 i j) || i <- il1 to j);
  | || j <- 1 to n j);
  L = (vector (2,n))
  | [i] = { (j1,_) = bounds AL[i]}
  In
  (vector (j1,i-1))
  | [j] = { (il1,_) = bounds AU[j]}
  In
  lfn il1 jl1 i j) || j <- jl1 to (i-1))
  | || i <- 2 to n j);
def ufnn il1 jl1 i j =
  sum_down (max il jl1) (i-1) AU[j][i] (term i j);
def lfn il1 jl1 i j =
  (1/U[j][j]) * (sum_down max il jl1)
  (j-1) AL[i][j] (term i j));
def term i j k = L[i][k] * U[j][k];
  In
| [j] = { L, U };
```

图 14 - 天线矩阵的 LU 分解

## 5.4. 测试运行

我们生成了一个随机的 50 x 50 $A$ 矩阵（即选择一个随机包络并填充随机数），包含 1210 个元素，即密度约为 50%。我们还生成了一个大小为 50 的随机填充 $B$ 向量。

```
def LUKSB_sky (L,U) B =
  { (,n) = bounds B ;
  Y = { vector (1,n)
  | [1] = B[1]
  | [i] = {j1,_) = bounds L[i]
  In
  sum_down j1 (i-1) B[i] (yfn L[i])
  || i <- 2 to n);
  yfn Li i j = Li[j] * Y[j]
  X = { vector (1,n)
  | [n] = Y[n] / U[n][n]
  | [i] = (1/U[i]) * (sum_down (i+1) n Y[i]) (xfn i)
  || i <- (n-1) downto 1);
  def xn i j = { uj = U[j];
  (i1,_) = bounds uj ;
  In
  if (i < i1) then 0.0
  else Uj[i] * X[j]; }
```

图 15 - 天线矩阵的前向和反向替换

图 16 显示了当在这些输入上运行 solve_sky 时 GITA 生成的并行性分析。图 17 和 18 分别显示了 `lucmp_sky` 和 `lubksb_sky` 对复合并行分析的各自贡献。

显然，天线矩阵求解器中的所有并行性实际上都在 LU 分解阶段。如果分析 Crout 算法，这一点实际上非常明显，它表现出“波前”并行性。LU 矩阵中的每个元素只依赖于其上方和左侧的元素，因此可以并行计算垂直于对角线的边界。这条边界像波浪一样从左上到右下扫过整个矩阵。

在前向和反向替换阶段，由于 $y$ 和 $x$ 矩阵是使用线性递归填充的，几乎没有任何并行性。

在具有显式并行性的语言中，LU 分解的波前并行性对于密集矩阵只需少少努力即可实现。我们可以有一个遍历对角线的顺序循环，以及一个计算所有交叉对角线的并行循环。遗憾的是，将此类解决方案扩展到天线矩阵似乎并不容易，因为交叉对角线的形状是不规则的。另一方面，在 Id 中，隐式并行性为我们提供了生产者-消费者同步，使其能够动态适应此类结构。

# Id

![](img/68e0c8e7cd61671f4d693a9b7458d12d_223_0.png)

图 16 - solve_sky 的并行性分析 (50 x 50)

![](img/68e0c8e7cd61671f4d693a9b7458d12d_223_1.png)

图 17 - lucmp_sky 的并行性分析 (50 x 50)

![](img/68e0c8e7cd61671f4d693a9b7458d12d_223_2.png)

图 18 - lubksb_sky 的并行性分析 (50 x 50)

# 感谢

Steve Heller 主要负责我们 1988 年开发的并行性解决方案。

非确定性诊所程序是与 Paul Barth 讨论后开发的，他也负责实现和测试运行。

尽管我们的天线矩阵求解器使用了 Crout 方法，但我们从之前的线性方程求解工作中学习了很多。IBM 研究的 Eigenadhan 开发了优雅的矩阵 Id 程序，而 Javed Aslam、Christopher Colby 和 Ken Steele 开发了稀疏矩阵的 Id 程序。

本报告描述了马萨诸理工学院计算机实验室的研究。实验室的资金由国防部海军研究办公室的合同 N00014-89-J-1988 部分提供。

# 注释

+   1. Id 的第一个版本于 1978 年。自 1985 年以来，它经历了一系列修订，期间曾被称为 Id/83s、Id86、Id Noveau 等，最后恢复为“Id”。

+   2. 然而，Id 绝非特定于数据流机器。

+   3. 详细讨论请参见 [5]。

+   4. 我们采取这种不对称观点是因为问题陈述的措辞。如果医生在患者之间会随机离开，那么我们就有对称性。我们会把“咨询”建模为两类客户（医生和患者）请求的资源。

+   5. 我们将模拟持续建模为固定次数的迭代，因为问题陈述没有说明任何内容。





# 标识符 215

另一种可能性是咨询一个实时时钟（当然，它将被实现为一个管理器对象。）

# 参考文献

- 1. Arvind and J. Dean Brock. Resource Managers in Functional Programming. Journal of Parallel and Distributed Computing, 1(6), June 1984.
- 2. Arvind, S. K.. Heller, and R. S. Nikhil. Programming Generality and Parallel Computers. In Proc. of the Fourth International Symposium on Biological and Artificial Intelligence Systems, Trento, September 1988, pgs. 255–286.
- 3. Hoare, C. A. R. Monitors: an Operating System Structuring Concept. Communications of the ACM, 17(10), October 1974, pgs. 549–557.
- 4. Knuth, D. E. The Art of Computer Programming, Volume 1: Fundamental Algorithms. Addison Wesley, Reading, MA, 1973.
- 5. Knuth, D. E. The Art of Computer Programming, Volume 2: Semi-Numerical Algorithms. Addison Wesley, Reading, MA, 1973.
- 6. Nikhil, R. S. Id (Version 8.1) Reference Manual. CSG Memo 284, Laboratory for Computer Science, August 1998.
- 7. Nikhil, R. S. and Arvind. Programming in Id: a parallel programming language. Book in preparation.
- 8. W. H. Numerical Recipes: The Art of Scientific Computing. Cambridge University Press, Cambridge, London, 1986, pgs. 31–35.
- 9. Turner, D. A. Semantic Elegance of Applicative Languages. In Proc. ACM Conference on Functional Languages and Computer Architecture, Portsmouth, NH, October 1981, pgs. 85–92.

A Comparative Study of Parallel Programming Languages: The Feo (Editor) 1992 Elsevier Science Publishers B.V.

217

# OCCAM

Jean-Luc Gaudiot
Department of Electrical Engineering-Systems
University of Southern California
Los Angeles, CA

Dae Yoon
Computer Science Department
University of Southern California
Los Angeles, CA

## 1. 引言

## 1.1. 简史

Occam 语言自 1982 年起一直在 INMOS Ltd. 开发。它基于 David May 和 C. A. R. Hoare 的并发进程（CSP）[1,3]。David May 花了多年时间开发并发进程的想法。他将许多想法公式化为一种名为 EPL（实验编程语言）语言。从那时，David May 将这些原始想法发展成了如今的 Occam。

Occam 的第一个版本称为 proto-Occam 或 Occam 1，它提供了该语言的基础结构和机制。自从 1983 年 1 月发布 Occam 以来，该语言发展成了更完善的形式 Occam 2。在 Occam 2 中，除了通信协议方面的改进，还引入了强类型和缩写机制。多维数组和无副作用函数也得到了实现 [3, 4, 6]。

Occam 编程语言是一种高级语言，用于在处理器网络上实现并发程序。该语言旨在实现在任何通用计算机上，但在 transporter（传输器）上特别高效。Inmos transporter 的设计与 Occam 的开发密切相关。因此，transporter 可以被视为一台“Occam 机器” [2]。

### 1.2. 并发

顺序程序指定了语句列表的顺序执行，其执行被称为进程（process）。并发程序指定了两个或多个可以作为并行进程并发执行的顺序程序。考虑以下示例（见图1）：

```
process 1:
  do forever...
    produce data
    send data to process 2
    do some other stuff
```

```
process 2:
  do forever...
    do something
    receive data from process 1
    consume data and do some other stuff
```

上述示例存在许多相互进程的应用中。每个进程由顺序执行的语句组成，而进程 1 和进程 2 同时并行执行。在 Occam 中，顺序和并行进程的符号分别为 SEQ 和 PAR。因此，上述示例可以使用 Occam 结构编写如下：

# Occam

219

图 1 - 两个通信的进程

```
PAR
WHILE TRUE
SEQ
  produce data
  send data to process 2
  do some other stuff
WHILE TRUE
SEQ
  do something
  receive data from process 1
  consume data and do some other stuff
```

进程是 Occam 程序的字节实体。每个语句（或行）被视为一个进程，并可以通过结构组合成更大的进程。在上述示例中，两个循环是并发执行的独立进程。它们只在某些点通过交换数据进行相互作用。

### 1.3. 通信

进程之间的交互机制是并发编程的重要组成部分。Occam 提供了进程之间的路径，称为通道（channels），输入和输出进程分别用 ? 和 ! 表示。通道在进程之间作为全局对象可见。换句话说，两个进程通过共享通道进行通信。只有当输入和输出语句都准备绪时，才能通过通道进行通信。使用通道，我们之前的示例可以重写为：

```
CHAN OF ANY:
PAR
WHILE TRUE
SEQ
  produce data
  send data to process 2
  do some other stuff
WHILE TRUE
SEQ
  do something
  receive data from process 1
  consume data and do some other stuff
```

这简化了由竞态条件引起的许多问题。

### 1.4. 程序结构

Occam 程序是进程的集合。每个进程可以被视为一组形成块（block）的语句。与许多块结构语言不同，缩进不仅是为了可读性，还为了程序结构。变量在它们被使用的进程之前立即定义，并在进程（块）的执行期间保持有效。考虑以下 Occam 程序，它评估表达式：

```
(a - b) * (a*c + a/c)
```

并行执行。

230
J. Gaudiot and D. Yoon

```
CHAN OF INT in1,in2,in3,out:
CHAN OF INT ch1,ch2,ch4:
INT a,b,c:
SEQ
-- 获取 a,b 和 c 的输入
PAR
in1 ? a
in2 ? b
in3 ? c
-- 并行执行算术运算
PAR
ch1 ! a - b
ch2 ! a * c
ch3 ! a / c
-- 评估 a*c + c)
INT t1,t2: -- 注意 t1,t2 是局部变量
SEQ
PAR
ch2 ? t1
ch3 ? t2
ch4 ! t1 + t2
-- 评估 (a-b) * (a*c + a/c) 并输出结果
INT t1,t2:
SEQ
```
PAR
ch1 ? t1
ch4 ? t2
out ! t1 * t2 -- 输出结果
```在这个示例中，所有算术运算都是并行的。没有强制运算符之间的顺序控制。然而，仔细检查通道通信可以看出程序的某些部分将顺序执行。例如，通道 ch1、ch2、ch3 和 ch4 都有生产者和消费者。消费者必须等待生产者准备好输出。变量在使用的进程之前立即定义，并在进程执行期间保持有效。在我们的示例中，变量 a、b 和 c 在整个程序执行期间是全局的，而变量 t1 和 t2 局部于它们声明之后的进程。

与其他语言一样，Occam 允许注释。但请注意，当注释另行开始时，应该正确缩进。

# 2. 进程

## 2.1. 原始进程

三种类型的原始进程——赋值、输入/输出以及 SKIP/STOP——形成了 Occam 操作的基础。

赋值进程改变变量的值，就像大多数传统语言一样。赋值的符号为

```
<variable> := <expression>
```




也可以进行多重赋值，如下所示。

```
a, b, c := x, y * z, x - z
```

在表达式中可以使用运算符所示所示。

- + * +, -, *, /, \ : 数值运算符，其中 \ 是取模操作。
- /\, \<, <, << >> : 逻辑和二元运算符，分别表示不等于、与、小于、或、异或、非、左移和右移。
- =, <, >, >=, <> : 关系运算符。

表达式可以使用左括号和右括号。

输入和输出过程（?,, !) 可用于通信目的。它们仅作用于通道（channels）。输入和输出的表示法如下。

```
channel ? variable
channel ! expression
```

输入输出过程的通用形式将在本章稍后进行讨论。

存在特殊用途的进程，主要用于控制执行流。

- STOP：一旦启动，它永远不会终止。因此，如果如果在 SEQ 块中使用，STOP 之后的进程将永远不会执行。
- SKIP：等同于无操作。

### 2.2. 构造

较大的进程通过使用构造将较小的进程组合起来。Occam 中可以使用以下类型的构造。

- SEQ：顺序
- PAR：并行
- IF：条件
- WHILE：循环
- ALT：交替
- CASE：选择

顺序构造将要按顺序执行的进程组合在一起。我们已经见过这种构造的示例。顺序构造可以包含其他构造，形成分级结构。

并行构造是 Occam 语言中最重要的构造之一。它将若干要并行执行的进程分组。

条件求值中的每个进程都由一个布尔表达式保护。如果发现某个表达式为真，则执行表达式后面的进程，并终止条件构造。如果没有发现任何表达式为真，则条件构造的行为类似于 STOP。考虑以下示例：

```
IF
  x < y
  x := x + 1
```

如果 $x \ge y$，条件构造将停止（STOP）。为了防止终止，我们可以按照如下方式修改条件：

```
IF
 x < y
 x := x + 1
 x >= y
 SKIP
```

或者

```
IF
 x < y
 x := x + 1
TRUE
SKIP
```

上述程序段的行为类似于传统语言中的 if-then-else-endif 语句。条件可以嵌套以实现更复杂的控制流。

循环重复一个进程，直到关联的布尔表达式返回假。例如：

```
SEQ
 i := i < number.of.inputs
SEQ
 keyboard ? ch
 screen ! ch
 i := i + 1
```

交替根据通信通道的状态提供进程（或多个进程）的选择。这种构造与条件构造类似，后者根据布尔表达式的值提供进程的选择。交替检查所有输入通道，并执行与第一个响应的通道关联的进程。例如：

```
CHAN OF INT chan1, chan2, chan3 :
INT x:
ALT
  chan1 ? x
    process 1
  chan2 ? x
    process 2
  chan3 ? x
    process 3
```

如果只有 chan1 响应，则只执行 process 1。如果 chan1 和 chan2 都响应，则执行与第一个响应通道关联的进程。“守卫”（guards）可以包含一个布尔表达式。在这种情况下，只有当通道是第一个响应的且布尔表达式为真时，才会执行关联的进程。如下例所示：

```
CHAN OF INT chan1, chan2, chan3 :
INT x:
ALT
  (y < 0) & chan1 ? x
    process 1
  (y < 0) & chan2 ? x
    process 2
  (y < 0) & chan3 ? x
    process 3
```

选择（CASE）通过匹配选择器的值与一组常量表达式的值，从多个选项中进行。（类似于 C 语言中的 switch() 语句）。

```
CASE ch
'a'
screen ! 'A'
'A'
screen ! 'A'
'b'
screen ! 'B'
'B'
screen ! 'B'
```

我们可以将关联进程完全相同的常量表达式分在一起。

```
CASE ch
'a', 'A'
screen ! 'A'
'b', 'B'
screen ! 'B'
```

## 2.3. 复制器

在某些情况下，我们可能有若干行为相同或相似的进程。考虑以下示例：

```
INT x:
SEQ
input ? x
input ? x
input ? x
input ? x
input ? x
```

使用复制器编写的等效形式如下：

```
INT x:
SEQ i = 0 FOR 5
input ? x
```

创建了五个输入进程的副本并按顺序执行。复制器始终包含以下内容之一：SEQ, PAR, ALT, IF。

复制器的通用形式为：

```
REP index = base FOR count
process
```

其中，REP 是 SEQ、PAR、ALT 或 IF 之一。index 与数组结合使用，其值范围从 base 到 base + count - 1。每个索引值的实例都与对应的副本或进程关联。因此，创建了 count 个副本。

例如，基本的客户端-服务器模型可以这样实现：

```
[number.of.clients] CHAN OF INT request
[number.of.clients] CHAN OF BOOL acknowledge:
PAR
-- server process
INT service:
WHILE TRUE
SEQ i i = 0 FOR number.clients
  request[i] ? service
  acknowledge[i] ! TRUE
```

其他处理工作...

```
-- Create replicas of client
PAR i = 0 FOR number.clients
BOOL ack:
INT service:
WHILE TRUE
SEQ
  determine service
  request[i] ? service
  acknowledge[i] ! TRUE
```

在此示例中，我们定义了 client 的数组。因此，类型的数组。

## 3. 类型与变量

### 3.1. 变量

变量的声明格式如下：

```
<type> <name>
```

在 Occam 中，变量的声明与标量变量相同，只是数组的大小由类型说明符在前缀。数组声明的示例是：

```
[10]INT int.array;
```

### 3.2. 基本类型

Occam 提供了以下基本类型：

BOOL, BYTE, INT, INT16, INT32, INT64, REAL32, REAL64

字面量可以显式类型。这通常用于转换类型：

- 42 (BYTE)：字节值。
- 'T' (INT)：整数值。
- 42.0 (REAL64)：64位浮点值。

### 3.3. 数组

数组是相同类型对象的组合，连接到一个命名对象。在 Occam 中，数组变量的声明与任何类型的标量变量相同，只是数组的大小由类型说明符在前缀。数组声明的示例是：[10]INT.array。

数组可以作为参数传递给过程。在 Occam 中，我们不需要在过程声明中指定数组的大小；任何大小但数据类型正确的数组都可以作为实际参数传递。例如：

```
PROC proc(CHAN OF INT input, []INT array)
```

数组段表示为：

```
[ array FROM subscript FOR count ]
```

段可以在语句中进行输入、输出或赋值，只要左侧和右侧的类型相同。例如：

```
int.array FROM 10 FOR 5 := [int.array FROM 1 FOR 5]
int.array FROM 10 FOR 5 := other.array
```

在上述示例中，other.array 的声明应该是 [5]INT。

在 Occam 中生成数组值非常简单。例如：

```
[10, 21, x+4, y+z]
```

假设 x 和 y 是整数变量，这生成了一个类型为 [4]INT 的数组。



232 J. L. Gaudiot 和 D. K. Yoon

数组生成和数组段通常与缩写（abbreviation）结合使用。例如：

```
f IS [int.array FROM 1 FOR 5] VAL q IS [1, 3, 5, 7, 9]
```

如果前面有 VAL，则关联的变量不能被修改。

Occam 支持任意维数的数组，它们的声明方式与我们目前看到的波形保持一致。例如，一个二维数组可以定义为：

```
[20]REAL32 real.matrix:
```

每个元素或每行都可以被视为单个变量。例如，real.matrix[i][j] 指的是第 i 行的第 j 个元素，而 real.matrix[i] 指的是整个 i 行。

在 Occam 中，字符串被处理为字节 类型的数组。例如，"hello" 等于 ['h','e','l','l','o']。我们将在下一节中介绍字符串的输入和输出。

## 4 通道通信

Occam 编程的底层原理是进程之间的通信，而通道是进行这种通信的主要手段。Occam 提供了一种协议，定义了通道上传输的数据类型或一组数据类型。通道的声明形式如下：

```
CHAN OF protocol name:
```

### 4.1. 简单协议

最简单的协议由基本类型组成。例如：

```
CHAN OF INT comm:
CHAN OF [20]INT chan:
```

Occam 233

在上面的示例中，chan 始终携带好 20 个 INT 类型的元素。然而，我们可以通过通道发送数组的大小。例如，以下进程在同一个通道上输出两个不同大小的整数数组。

```
CHAN OF INT[:]BYTE comm : 
[20]BYTE a:
[40]BYTE b:
SEQ
  comm ! 20::a
  comm ! 40::b
```

对应的输入进程如下：

```
INT size:
[1000]BYTE string:
SEQ
  comm ? size::string
  ...
  comm ? size::string
```

上面的示例还说明了如何在同一个通道上输入和输出字符串。

### 4.2. 命名协议

协议可以被命名并在多个通道声明中使用。如果通道上的协议很复杂，这通常非常有用。例如，可以使用 `;` 定义一个顺序协议，如下所示：

```
PROTOCOL Message IS BYTE; INT; INT:
...
CHAN OF Message comm:
```

234 J. L. Gaudiot 和 D. K. Yoon

通道 comm 接收或发送一个 BYTE 类型的值，随后是两个 INT 类型的值。输出进程包含一个具有正确类型表达式表达式列表，例如：

```
comm ! 10(BYTE); 321; 833
```

对应的输入进程是

```
comm ? x; y; z
```

单个通道可以通过变体协议（variant protocol）携带数种不同格式的消息。变体协议是一组不同的协议，每个协议都与一个标签（tag）相关。以下定义定义了一个名为 Messages 的变体协议：

```
Protocol Messages
CASE
a;INT; INT
b;BYTE::[]BYTE :
:
```

a 和 b 是此示例中的标签。使用该协议的示例是：

```
CHAN OF Messages comm:
PAR
INT x, y:
BYTE size :
[256]BYTE v:
comm ? CASE
a; x; y
...
b; size::v
...
```

其他进程可以发送此类消息：

```
comm ! a; 100; 250
```

Occam 235

或者

```
comm ! b;5:"Hello World !!"
```

标签可以作为 ALT 构造中的守卫，我们可以定义一个仅由标签组成的协议。这种协议通常用于在同一个通道上输入或输出不同的信号。

# 5. 过程与函数

与许多其他传统语言一样，我们可以通过定义过程或函数来实现某种程度的程序抽象。

### 5.1. 过程

过程定义将名称与进程关联。程序中的过程调用被替换为过程体。考虑以下过程：

```
PROC procl1()
SEQ
num := num + 1
count := count - 1
```

在程序文中出现字符串 procl() 的地方，它会被替换为语句：

```
SEQ
num := num + 1
count := count - 1
```

过程定义可能包含形式参数，这些参数通过缩写进行展开。例如，考虑以下定义

236 J. L. Gaudiot 和 D. K. Yoon

```
PROC write.string(CHAN OF BYTE c, VAL []BYTE s)
SEQ i = 0 FOR SIZE s
c ! s[i]
```

那么调用

```
write.string(output,"Hello World!")
```

将展开为：

```
CHAN OF BYTE c output :
[]BYTE s "Hello World !!"
SEQ i = 0 FOR SIZE s
c ! s[i]
```

SIZE 是一个预定义过程，返回数组中的元素数量。

由于过程调用是通过内联展开实现的，因此不允许递归过程调用。

### 5.2. 函数

函数是一种特殊的进程，称为值过程（value process）。值过程返回一个基本数据类型类型的结果（即不是数组类型）。例如，考虑以下未名函数定义：

```
big := (INT max:
VALOF
IF
a >= b
max := a
TRUE
max := b
RESULT max
)
```

Occam

如果对值过程进行了命名，则该名称可以在程序的其他部分使用以引用该进程。例如，我们可以定义函数 max 为：

```
INT FUNCTION max(VAL INT a, b)

INT max:
VALOF
IF
  a >= b
  max := a
TRUE
  max := b
RESULT max :
```

现在，函数调用：

```
big := max(a,b)
```

将 a 和 b 的最大值赋值给 big。

# 6. 配置

# 6.1. 多处理器的分配

PAR 构造中的组件进程可以在不同的处理器上执行。这可以通过特殊的注解 `PLACED` 来指定，它将进程分配给指定的处理器。考虑以下示例：

```
PLACED PAR
PROCESS 1
proc1()
PROCESS 2
proc2()
```

在这里，进程 proc1 和 proc2 被放置在编号为 1 和 2 的处理器上。该注释也可以复制：

238 J. L. Gaudiot 和 D. K. Yoon

PLACED PAR

```
PLACED PAR i = 0 FOR n
PROCESSOR 2*i
evenproc()
PLACED PAR i = 0 FOR n
PROCESSOR 2*i+1
oddproc()
```

### 6.2. 硬通道

当硬件与程序紧密结合时，我们可能需要对硬件进行直接访问。当我们有多个传输器并需要在传输器之间进行通信时情况也是如此。这等同于外部通信。外部通信通过传输器之间的链路完成。这些通常通过内存映射 I/O 实现，并标记为直接映射到外部硬件的内存位置地址。考虑以下示例：

```
PLACE screen AT 1:
PLACE keyboard AT 2:
```

现在，每个通道、屏幕和键盘分别映射到输出（链路 1）和输入（链路 2）。

除了硬通道外，Occam 还可以声明像传统系统中那样使用的 I/O 端口。一个端口的示例是：

```
PORT OF BYTE serial:
```

### 6.3. 优先级

在单个处理器上，我们可以为 PAR 构造中的每个进程分配相对优先级。考虑示例：

Occam 249

```
PRI PAR
proc1()
proc2()
...
procn(),
```

此外，如果 $i < j$，则 $proc_i$ 的优先级高于 $proc_j$。因此，只有当 $proc_1$ ... $proc_{i-1}$ 未准备就绪时，$proc_i$ 才能执行。PRI PAR 也可以复制。

此外，交替构造中的输入进程也可能具有优先级。考虑以下示例：

```
PRI ALT
chan1 ? data
rocl()
chan2 ? data
proc2()
...
TRUE & SKIP
default.proc()
```

在这个示例中，只有当 $proc_n$ 准备就绪且 $chan_1$ ... $chan_{n-1}$ 未准备就绪时，才会选择 $proc_n$。如果没有输入准备就绪，则选择 $default.proc$ 作为默认进程。

### 6.4. 定器

为了提供实时编程环境，Occam 支持一种名为 TIMER 的特殊类型。一个简单的示例看起来如下：

```
TIMER clock:
INT time:
clock ? time
```

240 J. L. Gaudiot 和 D. K. Yoon

这个简单的定时器进程从实时钟读取输入，即时钟周期。你可以声明任意数量的定时器，这有时是有用的，但定时器的值可能不同。

作为一个实际但简单的示例，我们可以如下所示定义一个延迟过程：

```
PROC delay (VAL INT interval)
TIMER clock:
INT timenow:
SEQ
clock ? timenow
clock ? AFTER timenow PLUS interval
```

进程 c ? AFTER b 是一个延迟过程，像 SKIP 一样什么都不做（但进程可能会挂起），并且当对 c 的读取满足条件 AFTER b 时才会终止。a AFTER b 可以被读取为一个条件，就像 (a MINUS b) > 0 一样。因此，我们可以将程序的最后一行解释为“等待当前时间超过开始时间加上间隔时间”。

超时可以通过如下方式实现：

```
TIMER clock:
VAL timeout IS 1000:
INT timenow:
SEQ
clock ? timenow
INT x :
ALT
input ? x
..some process.
clock ? AFTER timenow PLUS timeout
screen ! (18:: "Timeout on input !")
```




在使用定时器（timer）编写程序时，意识到时间表示的细节至关重要。只有当两个时间差相对于整数所能表示的最大值足够小时，测试才具有意义。

## 7. 示例

每个问题的完整代码出现在附录中。建议读者先阅读一个章节，然后学习附录中列出的 Occam 代码。

## 7.1. 扩展的哈明问题

给定一组素数 $a, b, c, \dots$，生成形式如下的整数序列：

$a! \cdot b! \cdot c! \cdotcdot \dots \le n$

在 Occam 中，除了过程的形式参数外，所有结构的大小必须在编译时均确定。因此，我们被迫假设固定数量的素数，而不是无限（或未知）数量的素数。哈明数通过递归计算输出流生成。由于 Occam 不允许递归调用，我们被迫使用特殊技术（例如流水线进程或操作堆栈 [7]）来实现递归。在我们的解决方案中，我们选择了一个反馈通道。为了避免死锁，数字在回传时会被队列，且队列管理器仅在收到请求时才发布一个数字。程序结构如图 2 所示。

### 7.2. 石烷问题

该问题要求我们生成所有大小 $i \le n$ 的石烷分子，其中 $i$ 是碳原子的数量。这等同于生成所有不重复的大小为 $n$ 的树。枚举树在 [5] 中讨论。为了简单起见，我们将石烷结构表示为碳原子列表。在示例程序中，我们将每个石烷表示为字符串 `(` `)` 和 `c`。例如，石烷 C2H6 表示为 `(C(C))`。

我们对石烷问题的解决方案使用了固定大小的三维数组。然而，由于动态数组结构对这个问题非常有用，我们引入了一个分隔符 (`$#`) 来表示不存在的元素。在 Occam 中处理动态结构通常不是易事，需要额外的代码行。在我们的示例程序中，我们只使用了 SRQ 结构，因为 Occam 的当前实现不允许数量数量的并行进程，并且不允许在并行组件体内对全局数组进行索引，除非索引值在编译时是已知的。如果我们仔细设计一个进程通信网络（假设进程数量可以在编译时确定），我们可以利用某些有限的并行性。然而，我们将付出巨大的通信成本。

图 2 - 扩展的哈明问题的程序结构

图 3 - 诊室问题中进程之间的交互

### 7.3. 诊室

此示例了如何在 Occam 中模拟异步进程之间的交互。示例程序还阐明了使用 Timer 进行实时编程。程序的大部分负责处理并发进程的终止。负责模拟结束进程是超时（time-out）处理。当超时事件发生时，终止信号将传播到所有参与模拟的进程。进程之间的交互如图 3 所示。

## 7.4. 天际矩阵求解器

在这个问题中，我们通过仅计算天际矩阵（skyline matrix）的非零元素来求解线性方程组，已知矩阵天际线的两个轮廓向量。在石烷问题中，我们需要动态数组结构。然而，正如我们之前提到的，Occam 要求在编译时确定所有数组的大小，因此我们只能存储天际矩阵的非零元素。为了补偿，我们引入了错误值来表示零元素。然后通过在计算期间忽略错误值，我们消除了对零元素的考虑。尽管这个问题具有程度的并行性，但为了简单起见，我们没有使用任何并行结构。使用并行结构需要许多许多内容在编译时已知，导致解决方案不具有通用性。

## 参考文献

- 1. Hoare, C. S. Communicating sequential processes. Communications of the ACM, 21(8), August 1978.
- 2. Inmos. Transputer Development System 2.0. Inmos Ltd., 1987.
- 3. Inmos. Occam 2 Reference Manual. Prentice Hall, 1988.
- 4. Jones, G. and M. Goldsmith. Programming in Occam 2. Prentice Hall, 1988.
- 5. Knuth, D. The Art of Computer Programming, Vol. 1: Fundamental Algorithms. Addison-Wesley, 1987.
- 6. Poutain, R. and D. May. A Tutorial Introduction to Occam Programming – including a language definition. Inmos Ltd., 1987.
- 7. Redfern, S. Implementing data structures and recursion in occam. Inmos Ltd. Technical Report 38, Central Applications Group, Inmos Ltd., 1988.

## 附录

************************************
*** 扩展的哈明问题 ****
************************************

```
VAL N IS 1000:
VAL Nprime IS 10:
[Nprime] INT Primes:
[N+1] INT Hamming:

PROC Hamming()
CHAN OF INT Feedback, RequestNum, GrantNum, Output:
[Nprime] INT ToMult, FromMult:

-- Collector:
-- Proc collector gathers new numbers and eliminates duplicates.
-- This proc sends a new hamming number back to "QueueManager" in
-- order to generate a new number from this number.

PROC Collector ()
VAL delayunit IS 1000:
VAL nomereinput IS 20:
INT num, delaycnt:
BOOL continue:
SEQ

SEQ i = 0 FOR N
Hamming[i] := -1
Feedback ! 1 (INT) -- Send initial value
continue := TRUE
delaycnt := 0
WHILE continue
PRI ALT
-- An input from one of Multipliers
ALT j=0 FOR Nprime
FromMult[j] ? num
SEQ
delaycnt := 0
IF
Hamming[num] = -1 -- No duplicate
SEQ
hamming[num] := num
Feedback ! num -- duplicate
TRUE
SKIP
```

(注：原始文本中的代码块在源文中是碎片化的；上述代码是根据提供的片段重建的逻辑。)




## Occam

249

```oc
--
PROC OnedinCat(VAL []BYTE t1, VAL t2 []BYTE t2, []BYTE t)
  INT i1,i2:
  SEQ
  i1,i2 := 0,0
  WHILE t1[i1] <> '$'
    SEQ
    t[i1] := t1[i1]
    i1 := i1 + 1
  WHILE t2[i2] <> '$'
    SEQ
    t[i1] := t2[i2]
    i1, i2 := i1+1, i2+1
  t[i1] := '$'
```

--
TwodimArrayAdjust :
-- 调整二维数组的下界和上界。
-- 即：返回此边界内元素的数组。

```oc
PROC TwodimArrayAdjust(VAL []BYTE a, VAL INT l, VAL INT u,
  INT i:
  SEQ
  i := 0
  WHILE i < l
    SEQ
    a[i][0] := '$'
    i := i+1
  WHILE i <= u
    SEQ
    a[i][0] := a[i]
    i := i+1
  WHILE i < Maxtrees
    SEQ
    a[i][0] := '$'
    i := i+1
```

--
Xtrees :
-- 返回大小为 i,j,k 和 1 的树集合的笛卡尔积
--且无重复。

```oc
PROC Xtrees(VAL INT i, VAL INT j, VAL INT k, VAL INT l,
  VAL [][]BYTE trees, [][]BYTE ntree)
  Maxtrees[Maxsize]BYTE cross1, cross2:
  Maxtrees[Maxsize]BYTE tmp2:
  INT i1,i2,m,n,o:
```

## J. L. Gaudiot and D. K. Yoon

```oc
SEQ
IF
 i = j
SEQ
 n := 0
WHILE trees[j][n][0] = '$'
 n := n + 1
 i1 := 0
WHILE trees[j][n][0] <> '$'
SEQ
 TwodimArrayAdjust(trees[j], 1, n, tmp)
 m := 0
WHILE tmp[m][0] = '$'
 m := m + 1
WHILE tmp[m][0] <> '$'
SEQ
 Onedimcat(trees[j][n],tmp[m],crossl[il])
 m := m + 1
 n := n + 1
 i1 := i1 + 1
 crossl[il][0] := '$'
```

TRUE

```oc
SEQ
 n := 0
WHILE trees[j][n][0] = '$'
 n := n + 1
 i1 := 0
WHILE trees[j][n][0] <> '$'
SEQ
 m := 0
WHILE trees[i][m][0] = '$'
 m := m + 1
WHILE trees[i][m][0] <> '$'
SEQ
 Onedimcat(trees[j][n],trees[i][m],crossl[il])
 m := m + 1
 n := n + 1
 i1 := i1 + 1
 crossl[il][0] := '$'
```

IF

```oc
k := 1
SEQ
 n := 0
WHILE trees[k][n][0] = '$'
 n := n + 1
 i1 := 0
WHILE trees[k][n][0] <> '$'
SEQ
 TwodimArrayAdjust(trees[k], 1, n, tmp)
 m := 0
WHILE tmp[m][0] = '$'
```

## Occam

251

```oc
m := m + 1
WHILE tmp[m][0] <> '$$'
SEQ
OnedimCat(trees[k][n],tmp[m],cross2[il])
m := m + 1
n := n + 1
il := il + 1
cross2[il][0] := '$$'
```




# Occam

SEQ
SickList[SickSize] := pat
SickSize := SickSize + 1
pqueue[pr] := pat -- 将患者加入患者队列
pq, pr := npq1, (pr+1) REM 队列大小
IF
dq > 0 then -- 有空闲医生

```
SEQ
doc := dqueue[df] -- 从医生队列删除
dq, df := ndq-1, (df+1) REM 队列大小
pat := pqueue[pf] -- 从患者队列删除
pq, pf := npq-1, (pf+1) REM 队列大小
AssignedList[AssignedSize][0] := pat
AssignedList[AssignedSize][1] := doc
AssignedSize := AssignedSize + 1
RectDoc[doc-1] := ! pat -- 分配患者
```

```
SKIP
ALT i := 0 FOR NumDoc-1 -- 来自医生输入
DocToRec[i] := ! pat -- 医生释放了一个患者
```

```
SEQ
CuredList[CuredSize] := pat
CuredSize := CuredSize + 1
dqueue[dr] := i+1 -- 将医生加入队列
dq, dr := ndq-1, (dr+1) REM 队列大小
IF
RectToFat[pat-1] := ! pat -- 患者离开办公室
```

```
npq > 0 then -- 有正在等待的患者
SEQ
pat := pqueue[pf] -- 从患者队列删除
pq, pf := npq-1, (pf+1) REM 队列大小
doc := dqueue[df] -- 从医生队列删除
dq, df := ndq-1, (df+1) REM 队列大小
AssignedList[AssignedSize][0] := pat
AssignedList[AssignedSize][1] := doc
AssignedSize := AssignedSize + 1
RectDoc[doc-1] := ! pat -- 分配患者
```

```
TRUE
SKIP
TRUE & SKIP
SKIP -- 无输入
```

-- 终止所有医生和患者
continue := TRUE
WHILE continue

```
PRI ALT -- 读取待处理输入
i := 0 FOR NumDoc-1
DocToRec[i] := doc
SKIP
ALT i := 0 FOR NumPat-1
PatToRec[i] := ! pat
```

# 258 J. L. Gaudiot 和 D. K. Yoon

```
SKIP
TRUE & SKIP
delay(Interval)
retrydelay := retrydelay - Interval
IF
retrydelay < 0
continue := false
TRUE
skip
```

```
-- 向患者和医生发送终止信号
PAR i = 0 FOR NumDoc-1
RecToDoc[i] != -1
PAR i = 0 FOR NumPat-1
RecToPat[i] != -1
```

```
:
-- 在给定的间隔后生成超时信号
PROC TimeoutProc(VAL INT t)
BOOL continue,term:
INT timeout:
SEQ
continue := TRUE
timeout := t
WHILE continue
PRI ALT
ToTimeout ? term
continue := FALSE
TRUE & SKIP
IF
timeout < 0
SEQ
continue := FALSE
FromTimeout ! TRUE
TRUE
SEQ
delay(Interval)
timeout := timeout - Interval
```

```
:
-- 医生诊室的主体
PAR
Receptionist()
PAR i = 0 FOR NumDoc-1
Doctor(RecToDoc[i],DocToRec[i],10000,1000)
PAR i = 0 FOR NumPat-1
Patient(RecToPat[i],PatToRec[i],5) -- 生病概率 5%
TimeoutProc(Hotlong)
:
```

# Occam

************************************
**** Skyline 矩阵 ****
************************************

VAL error IS 999999.99
VAL N IS 20

```
-- Skyline
-- 接收一个整数、两个特征向量、一个二维数组和
-- 一个列向量作为输入。返回线性方程组的解集。
```

```
PROC Skyline(VAL INT n, VAL []INT pi, VAL []INR pjr,
              VAL []REAL32 ain, VAL []REAL32 bin, [[]REAL32 sol)
```

```
-- FormSkyline
-- 给定两个特征向量和一个 n*n 矩阵，返回 A 的
-- 三角和上三角的非零元素，存储在两个
-- 二维数组中。注意上三角是关于对角线对称的。
```

```
PROC FormSkyline(VAL INT n, VAL []INT I, VAL []INT J, VAL []REAL32 A,
                 VAL []REAL32 L, []REAL32 U)
```

```
SEQ
SEQ k=1 FOR n
SEQ l=1 FOR n
L[k][l], U[k][k] := error, error -- 填充错误值
L[k][1] := A[k][k]
SEQ k=1 FOR n
SEQ l=I[k] FOR k-I[k]+1
L[k][l] := A[k][1]
SEQ k=1 FOR n
SEQ l=J[k] FOR k-J[k]+1
U[k][l] := A[k][1]
```

```
-- ZeroFill
-- 如果 'b' 的下界小于 'a' 的下界，
-- 则在 'a' 前面补零。
```

```
ZeroFill(VAL []REAL32 a, VAL []REAL32 b, []REAL32 c)
INT la, lb :=
SEQ
la, lb := 1,
WHILE a[la] <> error
la := la + 1
la := la - 1
WHILE b[lb] <> error
lb := lb + 1
```

```
lb := lb - 1
C := a
IF
  lb < la
    SEQ i:=lb FOR la-lb
    c[i] := 0.0
  TRUE
  SKIP
```

-- 取 L 的第 j 行和增量矩阵，并返回
-- row := (delta 的第 j 行)。

```
ElimL(VAL INT j, []REAL32 row, VAL []REAL32 delta, []REAL32 res)
INT k:
  SEQ i:=0 FOR N
    res[i] := error -- 初始分配错误值
    k := 1
    WHILE row[k] := error
      k := k + 1
    WHILE row[k] <> error
      IF
        delta[j][k] := error
          res[k] := row[k]
        TRUE
          res[k] := row[k] - delta[j]
      k := 1
```

-- 取 U 的第 j 行和增量矩阵，并返回
-- row := (delta 的第 j 列)。

```
ElimU(VAL INT j, []REAL32 row, VAL []REAL32 delta, []REAL32 res)
INT k:
  SEQ i:=0 FOR N
    res[i] := error -- 初始分配错误值
    k := 1
    WHILE row[k] := error
      k := k + 1
    WHILE row[k] <> error
      IF
        delta[j][k] := error
          res[k] := row[k]

TRUE

res[k] := row[k] - delta[j][k]
k := 1
```

- Eliminate :
- 接收一个整数、一个下/上三角数组和
- 一个列向量。消除上三角数组，并返回
- 调整后的下三角数组和列向量。注意
-- U 的行是对角线以上的列。

```
PROC Eliminate (VAL INT n, VAL [][]REAL32 Lin, VAL [][]REAL32 Uin,
VAL [][]REAL32 bin, [][]REAL32 Lout, [][]REAL32 bout)
INT i,i1,i2:
[N]REAL32 U, delta:
[N]REAL32 b, L, U:
i := n
L, U, b := Lin, Uin, bin
SEQ o=0 FOR N
SEQ p=0 FOR N
delta[o][p] := error
WHILE i > 1
SEQ
i1 := 1
WHILE U[i][i1] = error
i1 := i1 + 1
WHILE U[i][i1+1] <> error
i2 := 1
WHILE L[i][i2] = error
i2 := i2 + 1
WHILE L[i][i2+1] <> error
delta[i1][i2] := x * L[i]
SEQ j=1 FOR i
SEQ p=0 FOR N
row, col := error, error
ZeroFill(L[j], L[i], row)
ZeroFill(U[j], U[i], row)
ElimL(j, row, delta)
ElimU(j, row, delta)
```

# Program Notation

K. Maniandy

## 1. Introduction

Program Composition Notation (PCN) is a notation for composing programs. The programs that are composed may be expressed in base languages (such as Fortran, Lisp, or Strand) or in PCN itself. The PCN research effort has a narrow focus; our goals are described next.

**Composition:** The traditional method of constructing programs is sequential composition. We are evaluating the systems that other forms of program composition are helpful, and that programmers should be able to define their own composition operators, and to evaluate their efficacy in reasoning.

**Concurrent Implementations:** We seek to develop programs that execute efficiently on multicomputers (i.e., distributed memory machines), shared memory multiprocessors, and SIMD machines. A project on implementing PCN is underway at Caltech. A variant of this notation has been developed and is being implemented on the Connection Machine at UCLA by Rajivroda.

**Methodology:** We seek to propose a unifying framework for developing numeric, symbolic and reactive programs. Our intent is to develop programs by stepwise refinement, starting with programs with simpler proofs and refining them if they are not adequately efficient. A goal is to use existing libraries of programs in different languages.

## 2 Data Types

PCN has the basic data types called sync: boolean, integer, single and double precision floating point, character, and string. The initial value of a variable of a basic data type is arbitrary.

# 2.1. The Synchronization Type

PCN has a data type called sync, for synchronization. The initial value of a synch variable is a special symbol, ϕ, that indicates that the variable is undefined. Programmers have the obligation of proving that a synch variable is assigned at most one value. Given such a proof, a synch variable is either undefined (ϕ), or it is defined (by its non-ϕ value) and its definition remains unchanged. A synch variable can be assigned a value of any type.

A variable that is not declared is assumed to be a synch type; the scope of the variable is the block in which it is named.





# 程序组合表示法 265

## 2.2. 元组数据类型

PCN 有一种名为“元组”（tuple）的数据类型，它是成对项 {...} 之间的序列。元组的元素可以是任意数据类型，包括元组本身。元组 x 的第 $i$ 个元素表示为 x[i]。访问元组的第 $i$ 个元素的时间与 $i$ 无关。元组与一维数组相同，但元组的元素不必都是同一种类型。应用于元组的函数 `sizeof` 返回其大小。元组可以通过枚举定义，例如 {5, 3, 4}，也可以通过后文描述的量化定义。

### 2.3. 量化

项序列可以使用量化来定义。量化形式的语法为：

```
« identifier in integer-expression .. integer-expression :: lexical-unit »
```

量化形式 «i in n..m :: exp» 是一个序列，其中对于每一个满足 $n \le i \le m$ 的 $i$ 实例，词法单元 exp 出现一次；在 exp 的第 $k$ 次出现时，所有的 $i exp$ 实例均被标记为 $k$。

### 示例 -

- «i in 0..2 :: x[i] + y[i]»是序列 x[0] + y[0], x[1] + y[1], x[2] + y[2]。
- «i in 0..2 :: 5»是序列 5, 5, 5。
- «i in 0..2 :: x[i] := y[i], u[i] := v[i]»是语句序列：

```
x[0] := y[0], u[0] := v[0],
x[1] := y[1], u[1] := v[1],
x[2] := y[2], u[2] := v[2].
```

元组可以通过大括号之间的量化形式定义；例如：{«i in [0..2] : x[i]»}是元组 (x[0], x[1], x[2])。

量化形式可以相互嵌套。符号 «i,j in n..m : exp»等价于

«i in n..m :: j in n..m :: exp»

而符号 «i in ni..mi, j in nj..mj : exp»等价于

«i in ni..mi :: j in nj..mj :: exp»

## **守卫表达式 (Guarded Expressions)**：守卫表达式的语法为：

guard → expression

其中 guard 是一个布尔表达式。守卫表达式 g → e 的值定义如下：如果 g 成立，则 g → e 的值为空，其中符号 empty 的含义是：如果 if → g，则 g → e 的值是连接操作（序列的拼接）中的单位元。例如

> ««i, j in 0..1 :: (i ≤ j) → l[i, j], (i > j) → u[i, j]»

是元组

```
{ 1[0,0], 1[0,1], u[1,0], 1[1,1] }
```

## **作用于量化表达式的二元运算符 (Dyadic Operators on Quantified Expressions)**：归约形式的语法为：

dyadic-operator over quantified-form

且量化形式中的语法单元必须是（守卫或未守卫的）布尔、算术或字符串表达式。如果量化形式为空序列，则归约形式为该二元运算符的单位元，否则为：

```
t[0] ∇ t[1] ∇ ... ∇ t[k]
```

其中由量化形式指定的序列为 t[0] ... t[k]，∇ 是二元运算符。

### 示例 -

- Σ^m_i=n A[i] = + over <<i in n..m>>
- Π^m_i=n A[i] = * over <<i in n..m>>
- V^m_i=n A[i] = v over <<i in n..m>>
- + over <<i in n..m>> 2,1].

## 2.4. 数组、记录与集合

复杂类型可以通过数组和记录（结构）从其他类型创建。

支持基本类型的集合以及基本类型的记录集合（但不包括集合的集合）。集合用于关系。PCN 还允许对集合进行量化。对集合的量化与对序列的量化语法相同，只是范围 n..m 被替换为集合标识符。在这种情况下，量化形式表示集合。作用于集合的二元运算符必须满足结合律和交换律。集合可以通过枚举或通过量化形式定义，方法与元组相同，但使用不同的括号包裹。集合通过哈希实现。本文不再讨论集合。

## 3 组合

程序通过组合块来构建。组合程序使用的运算符可以是原始运算符或用户定义的运算符。本文中我们关注四种原始程序组合运算符：顺序组合 (;)、并行 (||)、选择 (?) 和公平组合 (-)。

参数通过引用传递。程序包含声明和一个块，如 C。块可以包含局部变量声明，如 C。块有一个体，其语法在后文中用 BNF 描述。所有非终端符号使用斜体，终端符号使用正体或粗体。符号 <s>su（其中 su 是语法单元）表示零或多个语法单元的实例，多个实例之间用逗号分隔。

```
block :: assignment | procedure-call | guard -> block | {primitive-composition-operator <block>} | user-defined-composition-operator <argument>
```

### 3.1. 赋值

表达式：赋值右侧的表达式如命令式表示法，但表达式可以是元组，或者表达式可以包含归约表达式。赋值右侧元组元素的执行方式如下。考虑两种情况：

情况 1：x 是变量或 e 是元组。
情况 2：x 是普通变量或 e 是表达式。

### 3.2. 守卫块

语法为

```
guard → block

```的含义在后文中给出。guard 的语法为：

```
guard :: predicate |
match-list |
match-list, predicate |
match-list :: <match>
match :: <pattern-identifier> △ variable-identifier
```



# 程序组合符号 271

为真，则守卫条件评估为成功；如果谓词评估为假，则守卫条件评估为失败。

- 否则（即如果 $x$ 的评估值不是 $\phi$ 也不是一个 k 元组），$g$ 评估为失败，且 $g$ 的评估终止。

语法为 $g \rightarrow c$ 的块 $b$ 的执行如下。如果 $g$ 评估为：

- 成功则执行 $c$（当 $c$ 终止时块 $b$ 终止）
- 失败则跳过（$b$ 的执行终止）
- $\phi$ 则执行 $b$（再次执行该块）

直观地说，块 $b$ 的执行过程是：等待直到 $g$ 获得一个非 $\phi$ 的值；如果 $g$ 的值为成功，则执行 $c$ 并跳过。

无守卫块的含义与守卫条件始终评估为成功的守卫块含义相同。因此，块 $true \rightarrow c$ 以及块 $c$ 的证明规则是相同的。

## 3.3. 顺序组合

块 $\{<block>;\}$ 的执行如下：由顺序组合构成的块按顺序执行。当顺序组合块中其块列表的最后一个块 $<block>$ 终止时，该顺序组合块终止。

## 3.4. 并行组合

块 $\{|| <block>|\}$ 的执行如下：由并行组合组成的所有块都并行执行。一个并行 272 K. M. Chandy 和 S. Taylor -组合块在它所组成的所有块都终止时终止。

并行执行的块可能会读取和写入公共变量。读取或写入基本数据类型的一个项是一个原子操作。

使用交替语义来对并行组合进行推理。保证了以下步进条件：在计算的任何点，对于每个由并行组合构成的块，该块要么已经终止，要么块中的某条语句最终将被执行。

## 3.5. 选择组合

本节描述了块 $\{<block>\}$ 的执行。仅关注形式为如下的选择块：$(?$ $<guard \rightarrow block>)$。（无守卫块被视为具有真值守卫的守卫块。）

选择块的执行如下：

1. 如果选择块中至少有一个守卫评估为成功，则执行任何守卫评估为成功的块。
2. 如果选择块中的所有守卫都评估为失败，则跳过。
3. 否则（即如果选择块中没有守卫评估为成功，且至少有一个守卫评估为挂起），则重复执行该选择块。

如果守卫的评估成功且对应守卫的块终止，或者如果块列表中所有守卫的评估均失败，则选择块的执行终止。

# 程序组合符号

## 3.6. 公平组合

公平组合与选择组合相同，除非控制流从一个公平组合块流回自身无限次次，在这种情况下，由公平组合构成的块列表中的每个守卫都会被无限次评估。

考虑以下程序，它们是相同的，除了第一个由选择组合定义，第二个由公平组合定义。

```
p(x)
integer: x;
?
true -> {; q(x), p(x) }
true -> {; r(x), p(x) }
p(x)
integer: x;
{
true -> {; q(x), p(x) }
true -> {; r(x), p(x) }}
```

程序 p 执行 q 或 r 并递归地调用自己。

选择组合程序允许比公平组合程序更多的计算。在公平组合程序中，q 和 r 都被无限次地执行；因此，$q$ 最终会被执行，$r$ 也最终会被执行。在选择组合程序中，$q$ 被无限次执行或者 $r$ 被无限次执行。因此，选择组合也允许在程序的某个时间点之后，$q$ 或 $r$ 其中之一永远不被执行。注意，我们同时使用选择和公平组合操作的唯一原因是，使用选择组合实现的程序比使用公平组合的程序更高效。此外，对于许多程序，选择组合就足够。

从一个块到另一个块的控制流含义在附录中通过组合运算符定义。控制流具有命令式编程中而易见的直观含义：控制从顺序组合中的一个块流到下一个块，从 274 K. M. Chandy 和 S. Taylor -块流到并行组合产生的所有块，从选择或公平组合块流到被选择执行的块。

## 4. 示例

在本节中，开发了几个程序来阐明组合运算符。程序文本使用 courier 字体，而程序内部文档使用 bookman 字体。我们从一个简单的 `flip` 程序开始，它有两个整数参数，`flip` 修改其参数的值。程序的体是一个顺序组合块。

```
flip(u,v)
integer: u, v;
{
integer: w;
w := u; u := v; v := w
}
```

声明程序的参数。
开始顺序组合块。
声明块的局部变量。
块列表
结束顺序组合块并结束程序。

接下来考虑一个带有三个参数的程序 f$：一个整数 $n$，一个索引为 $\{0 \le i < n\}$ 的一维数组 $x$，以及一个 $0 < j < n$ 的索引 $j$。如果 $x[j-1]$ 和 $x[j]$ 不是升序的，程序将交换它们。

```
f(n,j,x)
integer: n, j;
array [0 .. n-1] of integer: x;
(x[j-1] > x[j]) -> flip(x[j-1],x[j])
```

单条语句。接下来我们写了程序 $s0, s1, s2$，每个程序都有两个参数：$n$ 和 $x$，其中 $x$ 是一个 $[0 .. n-1]$ 数组，且每个程序的先决条件是 $x$ 是互不同的。为了说明方便，285

# 程序组合符号

### 4.1. 简单排序

**选择组合：** 如 UNITY 中，最简单的排序程序是翻转 $x$ 中任何一对无序的元素，然后重复该排序。

```
s0(n,x)
integer: n;
array [0 .. n-1] of integer: x;
{ ? i in 1..n-1 :
  (x[i-1] > x[i]) -> flip(x[i-1],x[i])
}
```

**顺序组合：** 冒泡排序通过顺序组合组合的方式定义。

```
s1(n,x)
integer: n;
array [0 .. n-1] of integer: x;
{ << t in 1 .. n-1, i in 1 .. n : f(n,x) }
```

**并行组合：** 奇偶交换排序使用顺序和并行组合定义。在每一步中，对于所有奇数 $i$，如果 $x[i-1]$ 和 $x[i]$ 无序则进行翻转；在偶数步时也执行相同的操作。

```
s2(n,x)
integer: n;
array [0 .. n-1] of integer: x;
{ << t in 0 .. n :
  || i in 1 .. n : ((t-i) mod 2 = 0) -> f(n,i) }
}
```

接下来我们使用同步变量展示奇偶交换程序。程序的参数是 $n$ 和数组 $x, y$，索引为 $i$，其中 $0 \le i < n$。程序不修改 $n$ 或 276 K. M. Handy 和 S. Taylor - x。程序的后置条件是 $y$ 是 $x$ 的排序。程序使用一个索引为 $t$（$0 \le t < n+2$）的局部数组 $z$。

**规范：** 程序的规范是以下方程组：

- $V$ 其中 $0 \le i \le n-1$：$z[i], l = x[i]$

**程序：** 程序是规范的句法转换：

```
s3(n,x,y)
integer: n;
array [0 .. n-1] of integer: x, y;
(| array [0 .. n+1, 0] of synch integer: z;
« i in 0 .. n-1 :: z[0, i] := x[i],
y[i] := z[n+1, i],
«« t in 0 .. n ::
(i-t) mod 2 = 0 $\rightarrow$ min(z[t, i], z[t, i+1]),
(i-t) mod 2 = 0 $\rightarrow$ max(z[t, i], z[t, i-1])
}}
```





# 程序组合表示法

![](img/68e0c8e7cd61671f4d693a9b7458d12d_287_0.png)

图 1 - 扩展的汉明问题

数组 x 的元素以及变量 d、y 是表示列表的元组。

该程序是以下程序的并行组合（见图 1）：

- 程序 `mult`，将列表 `x[i]` 的一个元素定义为列表 z 的对应元素与 `p[i]` 的乘积。对于每个 `i` 都有一个 `mult` 程序。
- 程序 `merge`，合并 `x` 中的 `m` 个列表以生成列表 `y`。
- 列表 `d` 定义为数字 1 后跟列表 `y`，即 `d = {1,y}`。
- 程序 `firstn` 将输出序列 `z` 定义为列表 `d` 的前 `n` 个元素。

```
hamming(p,n, z)
{
  array [0 .. m-1] of synch: x;
  << i in 0 .. m-1 :: mult(z,p[i],x[i]) >>
  merge(x,m,0,m,y),
  d := {1,y}
  firstn(d,n, z)
}
```

# 278 K. M. Chandy 和 S. Taylor

**mult**: `mult` 的第一个参数是输入列表 `z`，第二个参数是输入整数 `q`；其输出参数是列表 `v`，通过将 `z` 的每个元素乘以 `q` 得到。

程序 `mult(z, q, v)` 中 `v` 的值定义如下：

- 1. 如果 `z` 是空列表，则 `v` 为空列表。
- 2. `z` 的头部和尾部分别为为 `hz` 和 `tz`。
  那么 `v = (w,tv)`，其中 `w = hz * q`，且 `tv` 由 `mult(tz, q,tv)` 定义。

```
mult(z,q,v)
integer: q;
(?) ▷ z → v := ()
(hz,tz) ▷ z → [1 | v := (w,tv), w := hz * q, mult(tz,q,tv)]
```

**merge**: 程序 `merge`（见图 2）具有以下输入参数：数组 `x`、整数 `m` 以及两个索引 `lo` 和 `hi`。程序 `merge` 合并列表 `x[lo],...,x[hi-1]`。它有一个单一输出参数 `q`，即合并后的列表。

程序 `merge` 实现为由 `m2` 程序组成的平衡二叉树。

程序 `merge` 的输出是其输入的函数。输出 `q` 定义如下：

- 1. 如果 `hi - lo = 1`，则输出列表 `q` 与输入列表 `x[lo]` 相同。
- 2. 如果 `hi - lo = 2`，则输出列表 `q` 由 `m2(x[lo],x[hi], q)` 定义，其中 `m2` 合并它的两个输入列表 `x[lo]` 和 `x[hi]` 以产生输出列表 `q`。
- 3. 如果 `hi - lo > 2`，则输出列表 `q` 定义如下：

# 程序组合表示法

# merge

![](img/68e0c8e7cd61671f4d693a9b7458d12d_289_0.png)

图 2 - 合并函数

定义 `mid` 为 `(lo + hi)/2`。注意：`lo < mid < hi`。
定义 `lopart` 为 `merge (x, m, lo, lopart)`。
定义 `hipart` 为 `merge (x, m, mid, hi, hipart)`。
定义 `q` 为 `m2(lopart, hipart, q)`。

输出 `q` 是 `lopart` 和 `hipart` 的合并，其中 `lopart` 和 `hipart` 分别是 `x[i]` 中对于 `lo ≤ i < mid` 和 `mid ≤ i < hi` 的列表的合并。

```
merge(x,m,lo,hi,q)
integer: m, lo, hi;
array [0 .. m-1] of synch tuple: x;
synch tuple: q;
  ? (hi - lo) = 1 -> q := x[lo]
  (hi - lo) = 2 -> m2(x[lo], x[lo+1], q)
  (hi - lo) > 2 -> (|| synch (lo + hi)
      mid := (lo + hi)/2
      merge (x,m,lo,mid, lopart)
      merge (x,m,mid, hi, hipart)
      m2(lopart, hipart, q)
```

# K. M. Chandy 和 S. Taylor

**m2:** 程序 `m2` 有两个输入元组 `u` 和 `v`，以及一个输出元组 `w`。元组 `u`、`v` 和 `w` 表示列表。输出 `w` 定义如下：

- 如果输入 `u` 或 `v` 是空列表，则 `w` 为空列表。
- 如果 `u = {hu,tu}` 且 `v = {hv,tv}`，则：
  如果 `hu < hv`，则 `w = {hu,tw}`，其中 `tw` 由 `m2(tu,tv)` 定义。
  如果 `hv < hu`，则 `w = {hv,tw}`，其中 `tw` 由 `m2(u,tv)` 定义。
  如果 `hu = hv`，则 `w = {hu,tw}`，其中 `tw` 由 `m2(tu,tv)` 定义。

```
m2 (tu,v,w)
() ▷ u -> w := {}
(hu,tu) ◁ u -> w := {}
(hv,tv) ◁ v -> w := {}
  hu < hv -> w := {hu,tw}, m2(tu,tv)
  hv < hu -> w := {hv,tw}, m2(u,tv)
  hu = hv -> w := {hu,tw}, m2(tu,tv)
```

**firstn:** 程序 `firstn` 有输入列表 `d` 和整数 `n`，输出 `z`。输出是 `d` 的前 `n` 个元素。输出定义如下：

- 如果 `n = 0` 或 `d` 为空，则 `z` 为空。
- 如果 `n > 0` 且 `d = {hd,td}`，则 `z = {hd,tz}`，其中 `tz` 由 `firstn(td,n)` 定义。

# 程序组合表示法

```
firstn(d,n,z)
integer: n;
? (n = 0) -> z := {}
(d = {}) -> z := {}
(hd,td) ▷ (n > 0) -> z := (hd,tz)
```

# 6. Paraffin (并行结构)

Paraffin 的连接结构形成一个每个节点最多有四个邻居的树。一个树有一个中心或两个中心（见图 3）：

- 1. 单中心连接到最多四个树，每个树的节点最多有 3 个儿子。
- 2. 两个中心，每个中心的节点最多有 3 个儿子。

因此，问题的核心是表示所有节点最多有 3 个儿子的根树。

6.1. 根树

在本节中，我们使用“根树”一术语指代节点最多有 3 个儿子的树。与其仅仅打印所有自由树，我们将使用一种简单的数据结构来存储给定大小的所有自由树。换句话说，我们将存储 paraffin 的表示并进行计算。

# K. M. Chandy 和 S. Taylor

![](img/68e0c8e7cd61671f4d693a9b7458d12d_292_0.png)

图 3 - 两个自由树及其根表示

下一个根树有 0 或 1 个节点，根有 3 个孩子。考虑一个具有 $m+1$ 个节点的树，其由元组 $(i, u, j, v, k, l)$ 表示。

**生成根树程序:** 程序输入参数 `n`——要生成最多 `n` 个节点的根树。程序有输出参数 `t`，序列数组。

![](img/68e0c8e7cd61671f4d693a9b7458d12d_293_0.png)

图 4 - 树的数据结构

考虑一个具有 $m+1$ 个节点的树的三个孩子，其中 $m > 0$。考虑由元组 $(i, u, j, v, k, l)$ 表示的树。

**第一个孩子:** 第一个孩子至少有 $m/3$ 个节点，因为第一个孩子的节点数至少等于另外两个孩子的和。第一个孩子最多有 $m$ 个节点。因此，$i$ 的取值范围从 $[m/3]$ 到 $m$。第一个孩子的索引 $u$ 范围从 $0$ 到 $s[l]-1$。

**第二个孩子:** 第二个孩子至少有 $(m-1)/2$ 个节点，因为它与第三孩子的节点数相同，且第二个和三个孩子共有 $m-1$ 个节点。第二个孩子最多有 $m-1$ 个节点。因此，$j$ 的取值范围从 $\{(m-1)/3\}$ 到 $m-1$。如果 $i < j$，第二个孩子的索引 $v$ 范围从 $0$ 到 $s[j]-1$。如果 $i = j$，为了确保 $(i, u)$ 在字典序上大于或等于 $(j, v)$，我们需要 $u \geq v$。我们可以通过多种方式实现此点——我们选择了通过守卫 $(i > j)$ 来确保字典序。

**第三个孩子:** 第三个孩子恰好有 $m-i-j$ 个节点。如果 $j > k$，第三个孩子的索引 $w$ 范围从 $0$ 到 $s[k]-1$。

# 284 K. M. Chandy 和 S. Taylor

j = k，为了确保 $(j, v)$ 在字典序上大于或等于 $(k, w)$，我们需要 $v \ge w$。

程序按照 $m \in 1 \dots n-1$ 的顺序为 $t[m+1]$ 分配一个元组。分配给 $t[m+1]$ 的元组是通过描述三个孩子的段落中 $i, j, k, u, v, w$ 的量定义的。

```
rt(n, t)
integer: n;
array [1 .. n] of tuple: t;
{
  s[0] := 1, s[1] := 1
  << m in 1 .. n-1 :: t[m+1] := << i in (m/3) .. m,
	j in (m-i)/2 .. min(i,m-i),
	k in (m-i-j) .. (m-i-j),
	u in 0 .. s[i]-1, v in 0 .. s[j]-1, w in 0 .. s[k]-1 :
	((i > j) v (u <= v)) ^ ((j > k) v (v <= w)) $\rightarrow$ {i, u, j, v, k, w}
  >>
  s[m] := sizeof(t[m])
}
```





# 程序组合表示法

```
{; print(`level`,1`,`son`,s`number of vertices`,i)
, (i > 1) -> { k in [0.2] ::
  p(t,t[i][u] [2*k],t[i][u] [1+2*k],l+1,k)}
}
```

接下来我们给出一个打印所有大小为 $m+1$ 且具有单个质点的无根树程序。它与构建所有根树的程序相似，因为它生成了最多有 4 个子节点的根树，且其他顶点最多有 3 个子节点。

```
single(m)
integer: m;
  << i in [(m/4) .. m],
    j in [(m-i)/3 .. min(i,m-i)],
    k in [(m-i)/2 .. min(j,m-j)],
    l in [(m-j-k) .. (m-j-k)]
    u in 0 .. s[i]-1, v in 0 .. s[j]-1
    w in 0 .. s[k]-1, x in 0 .. s[l]-1 ::
    ((i > j)) ^ (u > v)) ^ (w > k) v
    ((v > w)) ^ (k > l) v (w > x)) ->
    {; p(t,i,u,1,0), p(t,j,v,1,1), p(t,k,w,1,2), p(t,l,x,1,3)) >>
```

最后，我们给出一个打印所有具有双质点的无根树程序。

```
double(n)
integer: n;
mod 2 = 0 -> {; << u in [0 .. s[n/2]-1],
  v in [u .. s[n/2] - 1] ::
  -> {; p(t,n/2,u,1,0), p(t,n/2,v,1,0)}
}
```

打印所有大小最大到 $n$ 的无根树的程序，只需对于所有 $m \in [1 .. n]$ 将 `single(m)` 和 `double(m)` 进行顺序组合即可。

# 286 K. M. Chandy 和 S. Taylor

图 5 - 诊室问题

# 7. 诊室

让患者的索引为 $i$，其中 $0 \leq i < np$。令 $sick[i]$ 为第 $i$ 个患者去医院的路径（图 5）。所有病患都通过一扇门进入，因此为接待员形成了一个单一队列。等待接待员的病患列表称为 `admit`。入口门由程序 `merge` 建模，其输入参数为数组 `sick`，输出参数为列表 `admit`。`merge` 程序通过合并其输入列表（即其输入数组的元素）来产生输出列表。这里使用了公平合并（fair merge），因为每个到达入口的患者都会通过那扇门。

让医生的索引为 $j$，其中 $0 \leq j < nd$。接待台处可用医生列表称为 $d$；列表中的每个条目都是一个医生的 ID。

接待员处理 `admit` 中的元素，并生成一个 $\{sick-patient, doctor\}$ 键对列表。该列表称为 `spd`。

$\{sick-patient, doctor\}$ 键对列表通过一条通道，每个患者-医生对进入相应的诊室。进入第 $j$ 个医生诊室的 $\{patient, doctor\}$ 键对列表为 `office[j]`。通道由程序 `fork` 建模，其输入参数为列表 `spd`，输出参数为数组 `office`。`fork` 程序输入列表中的每个条目包含一个指向输出数组的索引；输入列表中的条目会被复制到指定的输出列表中。

离开诊室 $j$ 的患者-医生对列表称为 `happy[j]`。患者在任意（有限）时间内被治愈。医生 $j$ 治疗的过程由程序 `ran` 建模，该程序具有单一输入列表 `office[j]` 和单一输出列表 `happy[j]`。`ran` 程序输入列表中的元素在任意有限步数后被放入其输出列表。

离开每个诊室的患者-医生对通过一扇门并加入单一输出列表 `cured`。这扇门由程序 `merge` 建模，输入为 `happy`，输出为 `cured`。接待员处理 `cured` 中的元素。通过字段标识的医生加入已见过接待员的医生列表。可用医生的列表 $d$ 是初始医生队列，随后是 `fd`（治愈后离开医院的医生序列）。通过字段标识的患者加入返回回家的患者列表；令患者 $i$ 的路径为 `healthy[i]`。出口由程序 `fork` 建模，其输入为 `out`，输出为 `healthy`。健康人在任意时间内生病。因此，列表 `healthy[i]` 中的一个条目会在任意有限时间内变为列表 `sick[i]` 中的一个条目。

**初始条件：** 我们假设最初所有患者都是健康的，所有医生都是可用的。因此，`ran` 的输入是按 递增排列的序列（即从 0 到 $nd-1$ 的序列 $j$），随后是 `fd`，即治愈后离开医院的医生序列。

### 7.1. ran

程序 `ran` 有一个单一输入序列 $x$ 和单一输出序列 $y$。输入序列中的元素在任意（有限）步数后被放入输出中。在以下程序中，首先选择第一个守卫（guard），将来自 $x$ 的一个元素放入 $y$。如果选择了该守卫，$y$ 保持不变。第一个守卫最终会被选中，因为该程序是使用公平组合（fair composition）构建的。（如果我们要允许患者永远健康的可能性，将用选择组合（choice composition）代替公平组合。）如果输入为空列表，则输出为空列表。

```
ran(x,y)
- ((hx,tx) ◁ x) -> (|| ran(tx,ty), y := (hx, ty))
- ((hx,tx) ◁ x) -> ran(x,y)
- (◁ x) -> y := {}
```

### 7.2. merge

我们使用 `merge` 程序的树，类似于 Hamming 问题中的做法，但合并两个序列的程序不同。这里我们只给出合并两个序列的程序 `m2`，因为程序的其余部分与 Hamming 问题相同。

程序 `m2` 有两个列表 $u$ 和 $v$，以及一个单一输出列表 $w$。`m2` 程序通过给出满足 $u$ 和 $v$ 取值的关系的 $w$ 值，定义了 $u, v$ 与 $w$ 之间的关系。列表 $w$ 用 $u$ 和 $v$ 定义如下：

- 1. 如果 $u$ 和 $v$ 都是空列表，则 $w$ 为空列表。
- 2. 如果列表 $u$ 不空，令 $hu$ 和 $tu$ 分别为 $u$ 的头部和尾部；列表 $w$ 定义为 $(hu,tw)$，其中 $tw$ 由关系 $m2(tu,v,tw)$ 定义。
- 3. 如果列表 $v$ 不空，令 $hv$ 和 $tv$ 分别为 $v$ 的头部和尾部；列表 $w$ 定义为 $(hv,tw)$，其中 $tw$ 由关系 $m2(u,tv,tw)$ 定义。

```
m2 (u,v,w)
- ((◁ u), (◁ v)) -> w := {}
- ((hu,tu) ◁ u) -> (|| m2(tu,v,tw), w := (hu,tw))
- ((hv,tv) ◁ v) -> (|| m2(u,tv,tw), w := (hv,tw))
```

### 7.3. fork

程序 `fork` 有两个输入：元组 $x$ 和索引 $m$。其输出是一个元组数组 $y$；这些元组中的代表一个列表。数组 $y$ 的索引范围为 $0 \leq i < m$。输入 $x$ 代表一个 2-元组列表 $\{j, v\}$，其中 $0 \leq j < m$。

`fork` 程序将 $y$ 定义为输入的函数。输出 $y$ 定义如下：

- 1. 如果 $x$ 是空列表，则对于所有 $j$，$y[j]$均为空列表。
- 2. 如果 $x$ 的头部元素是 $\{hx, tx\}$，令 $hx = \{j, v\}$；对于除 $j$ 外的所有元素，$y[i]$ 定义为 $z[i]$，且 $y[j]$ 定义为 $w[z,m]$；其中 $z = fork(tx,m,z)$。

```
fork(x,m,z)
integer: m;
array [0 .. m-1] of synch: y;
{
  ((◁ x) -> (|| i in [0 .. np-1] :: y[i] := {} ))
  ((hx,tx) ◁ x), ((j,v) ◁ hx) ->
    || array [0 .. m-1] of synch: z;
    fork(tx,m,z);
    « i in [0 .. m-1]: (i != j) -> y[i] := z[i],
    (i = j) -> y[i] := {hx,z[i]}
n
}
```

### 7.4. Receptionist

`receptionist` 程序通过为给定的输入 `admit, d, cured` 值定义输出 `spd, out, fd` 的值，定义了其参数之间的关系，定义如下：

- 1. 如果任何一个输入为空列表，则所有输出均为空列表。





# 程序组合表示法

2. 如果 admit = {i,ta} 且 d = {j,td}, 则 spd = {{i,j},tspd}, 其中 tspd 由 receptionist (ta, td, tspd, d, out, fd) 定义。

3. 如果 cured 的头元素是 (i, j)，则 out = (i,tout) 且 fd = {j,tfd}, 其中 tout 和 tfd 由 receptionist (admit, d, tc, spd, tout, tfd, tfd) 定义，其中 tc 是 c 的尾。

```
receptionist(admit, d, cured, spd, out)
?(size(out) = 0) v (size(d) = 0) v (size(cured) = 0) ->
  || spd := {out, out}, fd := {}
  ,(i,ta) triangleleft admit, ({j,td} triangleleft) ->
    || receptionist(ta, td, cured, spd, out)
      spd := {(i,j},tspd)
  ((i,j),tc) triangleleft ->
    || receptionist(admit,d, tc, spd, tout, tfd)
      out := (i,tout)
      fd := (j,tfd)
```

# 7.5. makelist

程序 makelist 有两个输入参数 nd 和 fd，以及一个输出参数 d。参数 fd 和 d 是列表，nd 是一个整数。该程序将其输出定义为输入的函数如下：

- 1. 如果 nd = 0 则 d = {0,fd}
- 2. 如果 nd > 0 则 d 由 makelist (nd-1,d, {nd,fd}) 定义。

```
makelist(nd, fd)
integer: nd;
?( nd = 0 -> d := {0,fd}
  , nd ≠ 0 ->

```
{|| makelist(m,d,t), m := nd - l, t := {nd,fd}}
}
```

# 8. 天际线矩阵 (Skyline Matrix)

数据结构：我们将首先给出 [2] 中描述的算法，稍后对其修改（如 [2] 中所示）以避免存储零。问题是获取矩阵 a 的 LU 分解。设 L、U 和 a 为 [1 .. n, 1 ..] 的实数数组。设 d 为 [1 .. n] 的实数数组。分解的下三角数组存储在 L 中，上三角数组存储在 U 中，对角线元素（的 l）存储在 d 中。

设 r, c 为 [1 .. n] 的整数数组，其中：

- 1. r[i] ≤ i，且对于所有 j < r[i]: a[i,j] = 0
- 2. c[j] ≤ j，且对于所有 i < c[j], a[i,j] = 0。

因此 r 和 c 定义了数组中非零元素的天际线。

算法的原始描述如下。（见算法 2.1，第 5 页，[2]）。初始 L 包含 a 的下半部分，U 包含 a 的上半部分，d 包含 a 的对角线元素。

# 程序规范：

```
For i := 1 to n do
  For j := r[i] to i - 1 do
    L[i,j] := L[i,j] - ∑_{k=max(r[i],c[j])}^{j-1} (L[i,k] * U[k,j]);
  For j := c[i] to i - 1 do
    U[i,j] := U[i,j] - ∑_{k=max(r[j],c[i])}^{j-1} (L[i,j] * U[k,j]) / d[j];
  d[i] := d[i] - ∑_{k=max(r[i],c[i])}^{i-1} (L[i,k] * U[k,i])
```

# 程序组合表示法

# 内存优化：

设 l 为 [1 .. n] 的元组数组，其中 l[i] 是元素 a[i, j] 的元组，其中 r[i] ≤ j < i。因此 a 的行 i 中对角线左侧的所有非零元素都在元组 l[i] 中。因此，如果 r[i] ≤ j，则 a[i, j] = l[i][j - r[i]]。

类似，设 u 为 [1 .. n] 的元组数组，其中 u[j] 是元素 a[i, j] 的元组，其中 c[j] ≤ i < j。因此 a 的列 j 中对角线上方的所有非零元素都在元组 u[j] 中。因此，如果 c[j] ≤ i，则 a[i, j] = u[j][i - c[j]]。

PCN 中的程序通过以下语法变换从规范中获得。替换：

- high_k-low_exp 为 (+ over k in [low..high]) :: exp >>
- L[i,j] 为 l[i][j - r[i]],
- u[j,i] 为 u[i][j - c[i]]。

生成的程序是：

```
lu(1,u,d,r,c);
array [1 .. n] of integer: d,r,c;
array [1 .. n] of tuple: l,u;
{
  i in [1 .. n] ::
  j in [r[i] .. i-1] ::
    l[i][j - r[i]] := (l[i][j - r[i]] - (+ over k in [(max(r[i],c[j]))..j-1] (l[i][k - r[i]] * u[k][j - c[j]]))
  j in [c[i] .. i-1] ::
    u[i][j - c[i]] := (u[i][j - c[i]] - (+ over k in [(max(r[j],c[i]))..j-1] (l[i][j - r[i]] * u[k][j - c[i]])) / d[j])
  d[i] := (d[i] - (+ over k in [(max(r[i],c[i]))..i-1] (l[i][k - r[i]] * u[k][i - c[i]])))
}
```

solve 通过相同的语法变换从其规范中获得。

# 参考文献

- 1. Chandy, K. M. and Misra. Parallel Program Design. Addison Wesley, Reading, MA, 1988
- 2. Eisenstat, S. C. and Taylor, H. Subroutines for sparse linear systems. Research Report 35, Yale University, New Haven, CT, 1974
- 3. Foster, I. and Taylor, S. Strand: New Concepts in Parallel Programming. Prentice Hall, Englewood Cliffs, NJ, 1990
- 4. Hoare, C. Communicating Sequential Processes. Prentice Hall International, London, 1984

# 附录

从一个块到另一个块的控制流在附录的程序组合上下文中定义。为每个组合块分配一个唯一名称。在程序的执行过程中，一个块可能执行任意次。考虑给定的程序执行，并为程序中的每次执行给一个唯一名称。控制流从块 b 的执行到块 d 的执行：

- 1. b 是并行组合块且 d 是 b 的块列表之一，或
- 2. b 是顺序组合块且 d 是 d 的块列表中的第一个块，或
- 3. 执行了一个顺序组合块，其中 b 在块列表中的先于 d，或
- 4. b 是选择组合块或并行组合块，且 g 在 b 的块列表中，且在 b 的执行中，g 求值为成功，然后执行 d，或
- 5. 存在一个块 c，控制流从 b 流到 c，再从 c 流到 d。

# Scheme 编程语言

John Franco
计算机科学系
辛辛那大学
Mail Location 8
Cincinnati, OH 45221

Daniel P. Friedman
计算机科学系
印第安纳大学
Bloomington, IN 47405

Olivier Dancy
计算与信息科学系
堪萨斯州立大学
Manhattan, KS 66506

## 1. Scheme 的历史与特征

Scheme 由 Gerald J. Sussman 和 Guy Steele Jr 于 1975 年开发 [4]。他们的目标是构建 Carl Hewitt Actor 系统的类 Lisp 原型。令他们惊讶的是，在去除了几层语法和语义糖后，剩余的是一个支持状态和一阶延续的应用顺序 λ 演算的扩展。从那时起，语言定义有了四个版本，并一直在努力创建一个 Scheme 的扩展 IEEE 标准。如今的 Scheme 仍然是具有声明式和命令式组件的 λ 演算。它被许多大学和研究中心作为学生的第一门编程语言，或研究项目和软件产品的核心。Scheme 的完整描述可以在 [1.3] 中找到。

由于源自 Lisp，Scheme 的基本语法单元是全括号表达式。Scheme 的基本控制结构是过程应用。过程要么表示为 λ 表达式，要么是原始的，操作数字、字符串、符号、对、列表（由对构建）、向量和全局输入输出流。

除了应用于函数以外的数据类型外，Scheme 在三个方向上扩展了 λ 演算：

- 使用条件表达式；
- 使用顺序和通过延续对控制的一阶访问；
- 对变量、结构和外部世界的副作用。

Scheme 采用传值调用（call-by-value），即过程应用于其参数的值，这与 ALGOL 60 和惰性语言不同。定义表达式求值的一种方便方法是将其定义为无参数过程。对该过程应用无参数就意味着对延迟表达式进行求值。这使得流的定义变得简单，如扩展汉明问题的解决方案所示。




Scheme 的实现是适当尾递归的。因此，在许多情况下，递归会自动转换为迭代。结果是，该语言没有提供显式的循环结构。这一特性被应用于一个解决方案中，在其中患者、医生和接待员之间的通信以轮询（round-robin）的方式进行。

由于 Scheme 程序是完全括号化的，因此可以被表示为列表。这使得将程序视为数据对象变得简单，句法扩展（宏）可以在 Scheme 世界内直接表达，而无需诉助于外部的抽象语法。

Scheme 表达式是动态类型的，即类型检查是在运行时进行的。这使得编写没有类型的程序成为可能。

Scheme 目前没有显式地支持任何形式的并行。然而，通过要求应用中子表达式的求值顺序是任意的，Scheme 设计者为某种形式的协作评估留下了空间。

最后，Scheme 从 Lisp 继承了使用 cons 对的列表表示法、依赖垃圾回收的隐式内存管理，以及引用（quotation）机制。

## 2 Scheme 的语法

为了本章的目的，我们使用以下 Scheme 的 BNF。

```
<declaration> ::==
<expression>
| (define <variable> <expression>
(extend-syntax) <identifier> [(<identifier> <input-spec>
<expression>)]*
```

```
<expression> ::==
<constant>
| <variable>
| <application>
| <lambda (<variable>*) <expression>
| <lambda <variable> <expression>
| <if <test> <consequence> <alternative>]* [else <expression>]
| <case [[symbol>] <expression>]* [else <expression>]
| cond [<test> <expression>]* [else <expression>]
| (and <expression>*)
| (or <expression>*)
| let ([<variable> <value>*) <expression>
| letrec ([<variable> <value>*) <expression
| let* ([<variable> <value>*) <expression
| (begin <expression>*)
| (set! <variable> <expression>)
| (apply <expression> <expression>)
| 'S-expression
```

```
<application> ::= <expression> <expression>*
input-spec ::= <5-expression*
<consequent>, <alternative>, <value>, <tag> ::= <expression>
```

方括号代表普通括号——它们提高了程序的可读性。上标 `*` 表示前一个形式出现零次或多次；上标 `+` 表示前一个形式出现一次或多次；`<condition>` 表示一个布尔表达式。

声明有三种：全局变量的定义；句法扩展的定义；以及普通表达式。

### 2.1. 全局变量

全局变量定义在全局环境中。

### 2.2. 句法扩展

句法扩展提供了一种基于条件指定展开的宏机制，这种展开取决于通过模式匹配所选的句法上下文。虽然 Scheme 社区对此尚未达成共识，但它们提供了非常方便的表达能力，且足够易于理解，满足本章的需求。关于 extend-syntax 的完整描述可以在 [1,2] 中找到。

例如，现在让我们定义以下句法扩展 `rec`、`when` 和 `unless`，它们将在本章的剩余部分中使用。

```
(extend-syntax (rec)
  [(rec ide exp)
    (letrec ((ide exp))
     ide))]

(extend-syntax (when)
  [(when test exp)
    (if exp
      'undefined))]

(extend-syntax (unless)
  [(unless test exp)
    (if test
      'undefined
      exp))])
```

`rec` 是一个递归声明，求值为递归声明的过程。`when` 和 `unless` 实现了一种“单臂”条件表达式。

### 2.3. 表达式

表达式可以是一个 $\lambda$-演算的表达式，也可以是 $\lambda$-演算的声明式或命令式扩展。

### 2.3.1. 纯 Scheme 表达式

常量、变量、$\lambda$-表达式和应用赋予了 Scheme 作用的、弱类型的且应用应用顺序的 $\lambda$-演算的完整威力。常量（字符串、数字等）求值结果为基础值。变量由当前环境中的值表示。$\lambda$-表达式求值为一等类过程，其中自由变量在词法上被绑定。应用中出现的表达式以任何顺序求值。第一个表达式求值为一个过程。该过程被应用于剩余表达式的值上。

### 2.3.2. 条件和声明式扩展

Scheme 为 $\lambda$-演算提供了条件和声明式扩展。这些包括条件表达式（**if, case, cond**）、逻辑操作（**and, or**）和局部定义（**let, letrec**）。

`if` 求值其测试表达式。如果结果不是布尔值 `false`，则求值结果部分，否则求值替代部分。**case** 求值标签表达式，并返回第一个与其关联的符号与标签匹配的表达式的值。最后一个符号 **else** 匹配任何值。`cond` 具有与 Lisp 语义，如果它的任一个表达式求值为 **false**，则返回 **false**。`and`（对应 `or`）中的子表达式从左到右求值，直到发现 **false**（对应非 **false**）值或直到所有表达式都求值完毕。`and`（对应 `or`）表达式在某个表达式求值为 `false`（或所有表达式都求值为 `false`）时求值为 `false`，否则求值为最后一个（或第一个）非假值。`let` 声明并行绑定，而 `letrec` 声明互递归。

### 2.3.3. 命令式扩展

Scheme 为 $\lambda$-演算提供了命令式扩展。这些包括 `let*`、`begin` 和 `set!`。`let*` 声明局部绑定。`begin` 子表达式按顺序求值，并返回最后一个表达式的值。`set!` 将表达式的值赋值给变量，前提是该变量在词法环境中已声明。

### 2.3.4. 应用

`(apply <expression> <expression>)` 返回第一个表达式的值应用于第二个表达式的值的结果，其中第一个值是一等类过程，第二个值是用于该过程的参数列表。

### 2.3.5. 原生操作符

除了这些特殊形式外，Scheme 还提供了处理基础构造的原生过程。如果它们是谓词，则名称后加问号；如果它们执行副作用，则后加感叹号——Scheme 程序员在自己的程序中通常遵循这一约定。

例如，`zero?` 检查参数是否为数字 0，`null?` 检查参数是否为空列表。`eq?` 检查参数的值是否相同。`eq?` 检查参数是否为同一个对象。

`cons`、`car` 和 `cdr` 是常用的列表构建和分解操作。`set-car!` 和 `set-cdr` 更新 cons 对的两个字段。

此外，Scheme 还提供了结构化谓词。例如，`pair?` 测试参数是否为 cons 对，`number?` 测试参数是否为数字，依此类推。

最后，过程 `call-with-current-continuation` 被作为一个一元过程进行传递，并将其应用于当前延续的抽象。稍后将此延续应用于某个值将恢复当前延续并将该值传递过去。

### 2.3.6. 值的表示

布尔常量 `true` 和 `false` 分别由 `#t` 和 `#f` 表示。空列表由 `'()` 表示。与其祖先 Lisp 不同，Scheme 中 `false` 和空列表的表示并不要求一致。

### 2.3.7. 引用

Scheme 从 Lisp 继承了引用机制。这种元结构机制允许在程序正文中指定诸如数字、字符串、符号、向量——或它们的任何列表或向量。本课程强烈依赖于将程序直接表示为数据。与 Lisp 一样，引用 `'S-expression>` 是 `(quote <S-expression>)` 的简写。





# Scheme

### 2.4. 结论

本节介绍了 Scheme 的语法以及部分语义和设计原理。关于其语义的正式描述可以在 [3] 中找到。

## 3. 扩展汉明问题

设 $a, b, c, \dots$ 为质数的有序列表。汉明问题是产生一个有序的整数流，其乘积为：

> $a^i x b^j x c^k \dots$

其中 $i, j, k, \dots$ 是非负整数，且 $i, j, k, \dots$ 中至少有一个非零。

### 3.1. 修改后问题的分析

设 $T$ 为任意整数，假设汉明问题被修改为返回给定的有序流：

> $T x a^i x b^j x c^k \dots$

即原始汉明问题的解，但所有的输出标记都乘以了整数 $T$。该流等价于等于以下整数的有序流：

> $T x a x^i x b^j x c^k \dots$

或

> $T x b^j x c^k \dots$

其中 $i, j, k, \dots$ 是非负的，且 $i, j, k, \dots$ 中至少有一个非零；$j', k', \dots$ 是非负的，且 $j', k', \dots$ 中至少有一个非零。

这一观察是我们的解决扩展汉明问题的递归解决方案的基础。我们通过合并以下流的结果来构造输出流：

```
T x a x a' a' b/ x ck' ...
```

和

```
T x b' x ck' ...
```

到输出标记 $T x a$。

### 3.2. 解决方案所利用的 Scheme 特性

解决方案的实现需要对流的操作。特别是流必须被合并和组装。虽然 Scheme 没有原生的操作或创建流的能力，但我们可以通过延迟流尾部的构造来推导出它。

让我们首先定义视为惰性列表的流的标准操作。

```scheme
(extend-syntax (force)
  [(force e) (e)])

(extend-syntax (delay)
  [(delay e) (lambda () e)])

(extend-syntax (empty-stream)
  [(empty-stream) '()]])

(extend-syntax (null-stream?)
  [(null-stream? s) (null? s)])

(extend-syntax (car-stream))
  {(car-stream s) (car s)})

(extend-syntax (cdr-stream))
  {(cdr-stream s) let ([d s])
    if (procedure? (cdr d))
      (begin
        (set-cdr! d (force (cdr d))) (cdr d))
        (cdr d))]

(extend-syntax (cons-stream)
  {(cons-stream a d) (cons a (delay d))}
```

然后，有一个合并两个递增整数流的程序：

```scheme
(define merge-streams;; Stream(Int) x Stream(Int) -> Stream(Int)
  (lambda (s1 s2)
    (cond
      [null-stream? s1] s2]
      [null-stream? s2] s1]
      [else
        (let [(<= a1 a2) [a1 (car-stream s1)] [a2 (car-stream s2)]
          (if
            (cons-stream a1 (merge-streams (cdr-stream s1) s2))
            (cons-stream a2 (merge-streams s1 (cdr-stream s2))))))))
```

该解决方案直接利用了函数作为值，并通过将值表示为无参数过程来延迟值。通过使用语法扩展保持了程序的简单。

308 J. Franco, et. al

```scheme
(define hamming ;;; Int x List(Int) -> Stream(Int)
(lambda (T lp))
  (if (null? stream)
    (let ([new-T (* T (car lp)))
      (cons-stream new-T (merge-streams
        (hamming new-T lp)
        (hamming T (cdr lp))))))
```

图 1 - 解决扩展汉明问题的程序

### 3.3. 解决方案

该问题的解决方案涉及合并任意长度的列表。这些列表用流表示。

图 1 显示的程序 `hamming` 接收一个输出标记 $T$ 和一个递增的质数有序列表 $lp$。`hamming` 产生一个递增的整数流，等于

$T x d' x b' x ck \dots$

其中 $i, j, k, \dots$ 是非负整数，$i, j, k, \dots$ 中至少有一个非零，且 $a, b, c, \dots$ 是质数列表 $lp$ 中的元素。

图 2 显示了一组用于测试此解决方案的程序。这里重要的程序是 `print-stream!`，它接收一个整数 $m$ 指定要输出的最大流元素，以及一个整数 $n$ 指定要打印的流元素数量。

### 3.4. 我们在这一节中学了什么？

汉明问题的解决方案可以使用流递归地表示。虽然递归在 Scheme 中是自然的，但一个显式的

```scheme
(define test
  ;; Unit -> Unspecified
  (lambda ()
    (print-stream! (hamming 1 '(2 3 5 7)) 10)))

(define print-stream!
  ;; Stream(Int) x Int -> Unspecified
  (lambda (s n)
    (if (and (null-stream? s) (> n 0))
      (begin
        (display (car-stream s))
        (newline)
        (print-stream! (cdr-stream s) (- n 1))))))
```

```scheme
(define test
  ;; Unit -> Unspecified
  (lambda ()
    (print-stream! (hamming 1 '(2 3 5 7)) 10)))

(define print-stream!
  ;; Stream(Int) x Int -> Unspecified
  (lambda (s n)
    (if (and (null-stream? s) (> n 0))
      (begin
        (display (car-stream s))
        (newline)
        (print-stream! (cdr-stream s) (- n 1))))))
```

图 2 - 扩展问题的示例测试

石蜡问题 (Paraffin Problem)

问题是寻找 $carbonnH$ 的所有异构体。$nH$ 的组成是 $n$ 个碳原子和 $2n$ 个氢原子。问题是寻找 $nH$ 的所有异构体。问题是寻找 $nH$ 的所有异构体。问题是寻找 $nH$ 的所有异构体。问题是寻找 $nH$ 的所有异构体。问题是寻找 $nH$ 的所有异构体。碳原子必须连接起来。汉明问题的解决方案可以使用流递归地表示。

```scheme
(define test
  ;; Unit -> Unspecified
  (lambda ()
    (print-stream! (hamming 1 '(2 3 5 7)) 10)))

(define print-stream!
  ;; Stream(Int) x Int -> Unspecified
  (lambda (s n)
    (if (and (null-stream? s) (> n 0))
      (begin
        (display (car-stream s))
        (newline)
        (print-stream! (cdr-stream s) (- n 1))))))
```

图 2 - 扩展问题的示例测试

石蜡问题 (Paraffin Problem)

问题是寻找 $carbonnH$ 的所有异构体。$nH$ 的组成是 $n$ 个碳原子和 $2n$ 个氢原子。碳原子必须连接起来。

# 石蜡问题 (The Paraffin Problem)

问题是寻找 $nH$ 的所有异构体。$nH$ 的组成是 $n$ 个碳原子和 $2n$ 个氢原子。

### 4.1. 输入和输出规范

图 3 所示程序接收一个整数 $n$ 作为输入。输出是一个树的列表，具有最大度且列表中没有两个树是同构的。迭代过程 map 定义在附录中定义。

### 4.2. 树的表示

输出列表中的每个树实际上是两个或多个子树的集合。为了可读性，每个子树包含在角括号之间。所有子树的节点数为 $n$。最高子树之间的高度差始终为零。左边缘边界处的符号 `<()>` 表示这种分裂，并代表仅由中心节点组成的单元子树。当最长路径为奇数时（即路径上的节点数为偶数），存在一条中心边，分裂为由该边连接的两个子树。

子树本身按如下递归定义。单节点子树表示为 `()`。有一个子节点的子树表示为：

> *subtree of the child*)

有两个子节点的子树表示为：

> *subtree of the left child* *subtree of the right child*)

有三个子节点的子树表示为：

> *subtree left child* *subtree middle child* *subtree right child*)

因此，子树 `(()) (())` 是四节点树，其中一个度为三；而子树 `(((())))` 是所有节点都在直线的四节点树。

### 4.3. 收集子树

使用二维数组保存每对 $(n, h)$ 的高度为 $h$ 包含 $n$ 个节点的子树列表。每个列表包含重复树。

### 4.4. 子树的唯一性

石蜡树由子树集合组装，这些集合共同遵守以下限制。所有子树的节点之和为 $n$。排除左边缘特殊的 `<()>`，从左到右的子树高度是非增的，且前两个高度相同。所有可能的组合的





## 312 J. Franco, 等人

```lisp
(define split-t
  (lambda (A l x n)
    (if (null? l)
        ()
        (let* ((tree (car l)) [h (1+ (height tree))])
          (begin
            (when (< h (1+ (/ n 2)))
              (array-set! A x h (cons tree (array-ref A x h))))
            (split-t A l x n)))))
```

图 4 - 按高度拆分 n 节点树并保存到数组中

匹配每个高度规格的子树被组合成单独的**石蜡树（（paraffin trees**）。当子树的高度相同且节点数相同时，则对子树的组合进行排序，以防止石蜡树的重复。

### 4.5. 算法粗略描述

该算法包含两个阶段。第一阶段的目标是收集最大度为四、根最大度为三的唯一树列表，每种高度和大小（节点数）的组合对应一个列表。每个列表被保存为数组的一个元素：数组的 $i,j$ 位置包含大小为 $i$ 高度为 $j$ 的唯一树列表。第二阶段的目标是遍历数组，汇组成代表石蜡树的子树组。

第一阶段由过程 `split-t`（图 4）处理，该过程自包含恰 $n$ 个节点的 `para.list` 和数量 $n$。对于 $l$ 中的每棵树，`split-t` 确定其高度 $h$，并将其添加到具有 $n$ 个节点且高度 $h$ 的现有树列表中，该列表存储在数组的 $(n, h)$ 位置。输入列表 $l$ 获取自过程 `build-trees`，如下：

## Scheme 313

由 `trees` 调用。该过程输入数量 $n$，并产生一个最大度为四、根度为三的唯一树列表。此类树中的每个节点最多有三个孩子。使用每个三元组，在 `build-tree` 内部递归生成右、中、左子树的集合，分别为 `trees-a`、`trees-b` 和 `trees-c`。子树的合法尺寸由过程 `sizer` 返回。

子树通过 `assemble` 链接以创建一个完整的子树。该过程输入子树列表 (a,b,c,d) 以及实例化为 `cons` 和 `cdr` 的操作符。将子树组汇成代表另一个子树的列表，其中根的节点是输入子树的根。

第一阶段完成后，数组 $\lambda$ 包含了组装输出树所需的所有树列表。过程 `done`（图 5）被调用四次，以从数组中组装相应的树集合（实际上使用了图 3 中的 `construct-trees`）。其他调用处理最长路径上存在中心节点且该节点具有二、三、四个邻居的情况。`done` 过程从数组中检索合适的子树组合以组装成石蜡树。过程 `height-list` 和 `sizer` 计算石蜡树的高度和尺寸规格。这些过程根据高度规格和节点数 $n$， 产生所有总和为 $n-1$ 的三元组列表。`sizer` 过程用于选择组装成石蜡树的子树尺寸。三元组中的数字分别代表右、中、左子树的节点数。`trees` 产生的树的唯一性在部分由三元组相对于高度配置的唯一性得以保证。由 `printer-tree` 监督的过程 `assemble` 组装石蜡树，而过程 `bracket-parts` 处理输出格式。

314 J. Franco, 等人。

```lisp
(define done
  (lambda (type A hght-list size-list)
    (begin
      (let ([height-a (car hght-list)]
            [height-b (cadr hght-list)]
            [height-c (if (< length hght-list) 3)
                         0 (caddr hght-list) hght-list))]
            [height-d (if (< length hght-list) 4)
                         0 (caddr hght-list))])
        (map (lambda y)
          (let [[size-a (car y)]
                [size-b (cadr y)]
                [size-c (if (< length y) 3) 0 (cadr y))]
                [size-d (if (< length y) 4) 0 (caddr y))])
            (let [[tree-a (array-ref A size-a height-a)]
                  [tree-b (array-ref A size-b height-b)]
                  [tree-c (array-ref A size-c height-c)]
                  [tree-d (array-ref A size-d height-d)]]
              (when (and (not (null? tree-a))
                        (not (null? tree-b))
                        (or (not (null? tree-c)) (< (length y) 3))
                        (or (not (null? tree-d)) (< (length y) 4))))
                (let [[f1 if (and (= size-a size-b)
                            (= height-a height-b)) cdr id]
                      [f2 if (and (= size-b size-c)
                            (= height-b height-c)) cdr id]
                      [f3 if (and (= size-c size-d)
                            (= height-c height-d)) cdr id]])
                  (print-tree type tree-a tree-b tree-c tree-d f1 f2 f3))))
        size-list)) '())))
```

图 5 - 从高度列表、尺寸列表组装树

325

### 4.6. append 的问题

`append` 的问题在于它要求子树是相同的。然而，在我们的情况下，子树可以是不同的。因此，我们必须使用不同的方法来连接子树。

# 医生-患者问题

医生-患者问题是算法的关键部分。它涉及患者与医生之间的交互。患者被医生治疗，这种交互产生了石蜡树。

## 5.1. 主要组件

我们解决方案的主要组件是：患者制造者、医生制造者、接待员和事件管理器。每个过程在下文中详细描述。

### 5.1.1. 患者制造者

`patient-maker` 的代码如下：

```lisp
(define patient-maker
  (lambda (name)
    (let ([this-time 'infinity])
      (lambda msg)
        (case (1st msg)
          [(name) name]
          [(time) this-time]
          [(time!) (set! this-time (2nd msg))]
          [else (error "Error in patient-maker"))))))

(define patient-maker
  (lambda (name)
    (let ([person (person-maker name)])
      (rec patient
        (lambda msg)
          (case (1st msg)
            [(event) (receptionist 'enqueue-patient)]
            [(new-sick-patient)]
            (begin
              (patient 'time! (rand))
              (event-mgr 'record patient))]
            [else (apply person msg))))))))
```

327

## Scheme 317

每个患者过程有三个函数：生病时调用接待员、计算传递给事件管理器的新生存时间、以及向请求过程提供个人信息。函数的选择由作为参数传递给过程的消息决定。患者过程局部有名称和生存时间。患者名称在患者列表中指定，该列表由用户作为参数提供给启动过程 `doctors-patients-problem`。生存时间在启动过程中计算并传递给事件管理器。一个特殊的过程 `stop-patient` 被赋予一个对应仿真持续时间的生存时间。当轮到 `stop-patient` “病人”时，仿真终止。

### 5.1.2. 医生制造者

`doctor-maker` 的代码如下：

```lisp
(define doctor-maker
  (lambda (name)
    (let [(treated *) [person person-maker name])
      (rec doctor
        (lambda msg)
          (case (1st msg)
            (event)
            (begin
              (treated 'new-sick-patient)
              (receptionist 'release-patient doctor treated))]
            (assign-patient)
            (begin
              (doctor 'time! (rand))
              (set! treated (2nd msg))
              (event-mgr 'record doctor))]
            [else (apply person msg))))))))))))))))
```




318
J. Franco, et. al

每个医生程序都有三个功能：当其配对的患者即将释放时调用接待员；计算并传递给事件管理器（event-manager）一个新的释放时间；以及向请求的程序提供个人信息。消息会改变这些功能。医生程序的局部变量包括医生的姓名和释放时间。医生姓名在一个医生姓名列表中指定，该列表是启动过程的参数。

### 5.1.3. 接待员

接待员的代码如下：

```scheme
(define receptionist)
  (let ((p-Q queue) (doctor-list queue))
    (let ((p-empty?) (patient-Q 'empty?))
      (d-empty!) (doctor-list 'empty?))
      (p-dequeue! (patient-Q 'dequeue!))
      (d-dequeue! (doctor-list 'dequeue!))
      (p-enqueue! (patient-Q 'enqueue!))
      (d-enqueue! (doctor-list 'enqueue!)))
  (letrec [[treat-waiting-patients-if-docs-available
             (lambda ()
               (when (and (not (p-empty?)) (not (d-empty?)))
                 (let ((doctor (d-dequeue!)) (patient (p-dequeue!)))
                   (begin
                      (doctor 'assign-patient patient)
                      (SHOW-PAIR-DOC-PAT doctor patient)
                      treat-waiting-patients-if-docs-available))))))
            (lambda msg
              (begin
                (case (1st msg)
                  ((enqueue-patient)
                   (let ((patient (2nd msg))))))))))
```

```scheme
(begin
  (SHOW-PERSON-SICK patient)
  (if (d-empty?)
    (p-enqueue patient)
    (let ((doctor (d-dequeue!)))
      (begin
        (doctor 'assign-patient patient)
        (SHOW-PAIR-DOC-PAT doctor patient))))
  ((release-patient)
   (let ((doctor (2nd msg)) (patient (3rd msg)))
     (begin
       (SHOW-RELEASE patient doctor)
       (d-enqueue! doctor)
       (treat-waiting-patients-if-docs-available))))
  ((init) (for-each d-enqueue! (2nd msg)))
  (event-mgr 'next-event))))))
```

接待员负责医生-患者配对和释放所需的记账工作。使用一个医生列表和一个患者队列来辅助这种记账工作。当在特定时期无法再进行任何配对或释放时，接待员会调用事件管理器来启动下一个事件。

### 5.1.4. 事件管理器

事件管理器的代码如下：

```scheme
(define event-mgr
  (let ((event-Q (queue)))
    (let ((insert! (event-Q 'insert!))
          (dequeue! (event-Q 'dequeue!))
          (update-all! (event-Q 'update-all!)))
      (lambda msg
        (case (lst msg)
```

```scheme
 ((record) (insert! (2nd msg) 'time'))
 ((next-event)
 (let ([person (dequeue!)]
   (begin
     (update-all!)
     (let ((next-time (person 'time')))
       (lambda (p) (p 'time! (- (p 'time) next-time))))
     (unless (eq? person stop-patient)
       (person 'event')))))))]
```

事件管理器维护一个事件列表，并按照它们发生的顺序排列其发生的时间。事件管理器有两个功能：在事件列表中记录未来事件，以及在下一个事件到期时调用第一个程序。来自医生或程序的调用会导致该程序根据完成调用的时间被放置在事件列表中。事件列表中的医生程序代表其患者释放的未来事件。事件列表中的患者程序代表患者生病的未来事件。事件管理器在记录事件后会立即返回。当从接待员调用时，事件管理器会调用事件列表中的第一个程序。

## 5.2. 控制流

最初，调用启动过程 `doctors-patients-problem`，并将患者姓名列表和医生姓名列表作为参数。给 `stop-patient` 分配一个时间并由事件管理器记录在事件列表中。然后，对于患者列表中的每个患者姓名，都会创建一个患者程序，并用它将自身及其首次发病时间记录在事件列表中。通过调用接待员设置其医生列表，从而完成启动过程。在这种情况下，接待员的第二个参数是一个医生程序列表，医生姓名列表中的每个医生对应一个程序。接待员将这些医生程序存于其医生列表中。

模拟以轮询方式进行程序调用。对接待员的所有调用都会导致对事件管理器的调用。当从接待员调用时，事件管理器调用事件列表中的第一个程序。如果是患者程序，则表示患者已生病。因此，接待员被赋予指令，当有可用医生时将患者与其配对。如果是医生程序，则表示该医生正在治疗的患者已释放。因此，接待员被赋予指令释放该医生。

## 6. 天际线矩阵（Skyline-Matrix）

我们通过从右角到左上角对矩阵进行三角化，并从左上角到右上收集项来解决这个问题。

### 6.1. 输入规范

skyline 的输入是一个包含非零元素的行列表、一个行天际线列表、一个列天际线列表以及一个 b 列表。行列表中的行顺序从下到上，每个列表中的元素顺序是反转的。




## 324 J. Franco, 等人

```scheme
(define skyline
  (lambda row-list row-skyline col-skyline b-list n)
    (if null? row-list)
      '()
      (let* [row-len (- (addl n) (car row-skyline))]
             [col-len (- (addl n) (car col-skyline))]
             [z ((multiplier-list (caar row-list))]
             [subl col-len) (cdr row-list))]
             [new-sky ((fix-skyline (car col-skyline))
                       row-len col-skyline))]
             [new-sky ((fix-skyline (car row-skyline))
                       col-len row-skyline))]
             [new-row-list ((new-row (car row-list) col-skyline)
                            (subl col-len) (cdr row-list) z)]
             [new-b-list (cons (car b-list)
                          (new-b-list (car b-list))
                          (subl col-len) (cdr b-list) z))]
        (cons (car row-list) (skyline new-row-sky)
              (cons (car new-b-list)
                    (cdr new-row-sky)
                    (cdr new-col-sky)
                    (cdr new-b-list)
                    (subl n))))))

(define result
  (lambda (s-list)
    ((rec loop
       (lambda (sol s-list)
        (if null? s-list)
          sol
          (let [{sum-prod (dot-prod (cadadr s-list) sol)}]
            (loop (cons (/ - (car s-list) sum-prod)
                      (caadr s-list) sol))
            (cdr (cdr s-list))))))))
    '() (reverse s-list)))))
```

图 6 - 天际线矩阵问题的主程序

## Scheme 325

### 6.2. 输出规范

skyline 的输出是一个列表，其中包含了 b-list 数字列表与单个数字的交替。单个数字是 b-list 元素；它们可能因为行的加而发生变化。列表是连续的矩阵元素，按逆序排列，位于对角线左侧；它们也可能因为行的加而发生变化。从右到左，最后一行的 b-list 元素之后是最后一行的对角线元素（以单元素列表形式）。接着是倒数第二行的变化的 b-list 元素以及倒数第二行的非零元素列表，依此类推。

过程 result 递归地从 skyline 提供的输入构建解 X。假设 sol 是覆盖 X 的列表（变量）的部分解。我们按照如下方式将 sol 扩展为覆盖 X 的 $i+1$ 个变量的部分解：取 sol 与第 $i+1$ 个元素列表中的所有第一个矩阵元素（从右开始计数）的点积，并称之为 sumprod；让列表的第一个元素称为 diagelem，让第 $i+1$ 个数字称为 belem。那么，从底部开始的第 $i+1$ 个变量的值为 (belem - sumprod) / diagelem。过程 result 均以这种方式递归地构建一个解向量。

### 6.3. 程序描述

这里我们简要描述我们在解决天际线矩阵问题时使用的程序。具体代码见附录。skyline 递归地从逐渐减小的子矩阵和 b-list 构建矩阵元素对和 b-list 对的列表。这需要为 skyline 的递归调用计算以下新参数：row-list、row-extend、col-skyline 和 blist。在这四个参数中，b-list 和 row-list 都需要一个乘数列表，对应于右下对角线元素之上的每个非零矩阵元素，这些乘数将在最后一行加到其上方的行时被使用。

multiplier-list 由过程 multiplier-list 构建。列表的大小由 col-skyline 的第一个元素决定。令 $q$ 为右下角矩阵元素，令 $r_1, r_2...$ 为最右列中 $q$ 之上按顺序的非零元素。那么，产生的 multiplier-list 为 $(-r_1/q, r_2/q,...)$。当最后一行乘以 $r_i/q$ 并加到最后一行之上的第 $i$ 行时，该行的最右侧元素变为零。skyline 中对 multiplier-list 的调用产生列表 $l$。

new-list 和 b-list 同样通过 multiplier-list 以及旧 row-list 和 b-list 构建。区别在于，在 row-list 的情况下，添加的是列表；而在 b-list 的情况下，添加的是标量。我们抽象了共同部分并命名为 abstract-1。该过程接受另一个程序 $f$ 作为参数，并返回一个接受两个列表（list-1 和 list-2）和一个数字 $n$ 的程序。调用时，返回的程序按照 $n$ 指定步遍历 list-1 和 list-2，对遇到的每对 list-1 和 list-2 元素应用 $f$，并返回一个与 list-1 剩余部分连接起来的结果列表。

过程 new-b-list 通过调用 abstract-1 构建新的 b-list，其中程序 $f$ 将一个 b 值与 list-2 的元素（list-2 是 multiplier-list）相乘，并将结果加到 list-1 的元素上（list-1 是旧的 b-list）。

过程 new-row 通过调用 abstract-1 构建新的 row-list，其中程序 $f$ 将 add-row 程序应用于 list-2 的元素（再次是 multiplier-list）和 list-1 的元素（现在是行列表）。add-row 程序将 row-list 中第一行的所有乘数的乘积结果列表加到 row-list 剩余部分的元素上。由于 row-list 中的元素在给定矩阵中可能被零隔开，必须使用 col-skyline 来确定行加时的元素对齐。因此，旧的 col-skyline 是该程序的参数。在行元素出现零的意外情况下，程序不做任何特殊处理；此类元素被记录为零。

还需要说明如何构建新的 col-skyline 和 row-skyline。修复它们的程序是 fix-skyline。该程序调整旧 col-skyline 的元素。

## 7. 结论

正如本章所示，Scheme 本质上是简单、灵活且正交的。为了这一点，我们展示了延续计算的潜力。

## 致谢

John Franco 受空军研究办公室拨款 89 资助。Daniel Friedman 受国家基金拨款 CCR-217 资助。Olivier Danvy 在 1989 年秋季对本工作做出了贡献。

## 参考文献

- Dybvig, R. Scheme Language. Prentice-Hall, Englewood Cliffs, NJ, 1987.
- Kohlcker, E. Syntactic Extensions in Scheme. Ph.D. Dissertation, Department of Computer Science, Indiana University, Bloomington, 1986.
- Rees, J. and Clinger, W. C. (eds.). Revised Report on the Algorithmic Language. Sigplan Notices, 21(12), December 1986, pgs. 37-79.
- Sussman, G. J. and Steele, G. L. Scheme: an interpreter for extended lambda. Technical Report, Artificial Intelligence Laboratory, Massachusetts Institute of Technology, Cambridge, MA, 1975.





# 330 J. Franco, 等人。

assem-list)))

```lisp
(define list-max
(lambda (x) (if (null? x) 0 (max (car x) (list-max (cdr x)))))
```

```lisp
(define height
(lambda (x) (if (null? x) 0 (1+ (list-max (map height x)))))
```

```lisp
(define last-items
(lambda (x)
  (if (= 2 (length x)) 1 (last-items (cdr x)))))
```

```lisp
(define size
(lambda (n h-spec)
  let* ([items (last-items h-spec))
        [next-last (car items)]
        [last (cadr items)]
        [new-h-spec (cdr (reverse h-spec))]
    (if (= (length h-spec) 2
      (if (< x n)
        ()
        (cons x (list n)) (sizer (1+ n) (1- x) h-spec))
      (let ([bnd (if (<= next-last) n 1)])
        ()
        (append (map (lambda y) (append (list n))
          (sizer bnd (- x bnd) new-h-spec))
          (sizer (1+ n) (1- x) h-spec)))))
```

```lisp
(define id (lambda (x)))
```

```lisp
(define array-ref
(lambda (A n) (vector-ref A n))
```

```lisp
(define array-set!
(lambda (A n val) (vector-set A n val))
```

```lisp
(define create-array
(lambda (n))
  (let ((if (decr-ord-list (1+ n))) '() ())
    (apply vector (map (lambda (x) (make-vector (1+ n) '()))))))
```

```lisp
(define incr-ord-list
(lambda (n))
  ((rec up (lambda (acc x) (if (zero? x)
    acc (up (cons x acc) (1- x))))
    '()))))
```

# Scheme

331

```lisp
** (decr-ord-list 6) -> (6 5 4 3 2 1 0)
(define decr-ord-list
(lambda (n)
  (if (zero n) '(0) (cons n (decr-ord-list (1- n)))))

** (decr-ord-pair 4) -> ((3 3) (2 3) (1 0) (2 2))
(define decr-ord-pair
(lambda (n)
  (if (zero n)
    (list 0 0))
  (append (map (lambda x) (list x) (decr-ord-list n))
    (decr-ord-pair (1- n))))

(define decr-elements
(lambda (n)
  (map list (decr-ord-list n))))

(define height-proc
(lambda (n h)
  (cond
    [< n 0]
    '()
    [= h 2]
    (cons (list n) (height-proc (1- n) h)))
    [else
    (let ((map-list (if (= h n) elements n decr-ord-pair n)))
      (append (map (lambda y) (append list n y)) map-list)
      (height-proc (1- n) h))))

(define get-trees (lambda (B n) (vector-ref B n)))

(define build-trees
(lambda (B l)
  (if (null? l)
    '()
    (let* ([subtree-config (car l)]
           [nodes-c (car subtree-config)]
           [nodes-b (cadr subtree-config)]
           [nodes-a (caddr subtree-config)]
           [trees-c (get-trees B nodes-c)]
           [trees-b (get-trees B nodes-b)]
           [trees-a (get-trees B nodes-a)]
           [op1 (if (= nodes-a nodes-b) cdr id)]
           [op2 (if (= nodes-b nodes-c) cdr id)])
      (append assemble trees-c trees-b trees-a '() op1 id)
      (build-trees B (car l)))))

(define trees
(lambda (B n))
  (cond
    [(= n 1) (list '()))
    [(zero? n) '()]
    [else (build-trees B (sizer 0 (1- n) ('1 1 1)))]))
```

#*******************
**** 诊室 ****
********************

```lisp
(define stop-patient (patient-maker 'stop'))

(define for-each
  (lambda (p l)
    ((rec loop (lambda l1)
      (unless (null? l1))
        (begin
          (p car)
          (loop (cdr l1)))))))

(define doctors-patients-problem
  (lambda (patients doctors)
    (begin
      (stop-patient 'time! 100)
      (event-mgr 'record stop-patient)
      (for-each (lambda p) ((patient-maker p)
        'new-sick))
      (receptionist 'init (map doctor-maker doctors))))
```

```lisp
(define test
  (lambda ()
    (doctors-patients-problem
      ('John" "Jim" "Joy" "Grace" "Sam)))))
```

```lisp
(define queue
  (lambda ()
    (let ((front []) [rear []) [secure (lambda expr) 'done'])
      (rec enqueue
        (lambda item)
          (let ((list-of-item (cons item)))
            (if (null? front)
              (begin (set! front list-of-item)
                (set! rear (list-of-item))))
        [update-all! (lambda proc) (for-each front))
        [empty? (lambda () (null? front))]
        [dequeue
          (lambda ()
            (if (null? front)
              (begin (write "The queue is empty.") (newline))
                (let ((item car front)))))

# Scheme 333

```lisp
(begin set! front (cdr front))
  (when (null? front) (set! rear ')))
  item)))

(insert!
 (lambda (item)
  (let ((this-time (item)))
    (if (or (null? front) (< this-time (car front)))
      (if (null? front)
        (enqueue item)
        (let ((c (cons item)))
          (set! front c)))
      (rec loop (lambda before after)
        (cond
          [(null? after) (enqueue item)]
          [(< this-time (car after))]
            (let ((c (cons after)))
              (set! before c))]
          [else (error "Bad command to queue:" msg))]))
      front (cdr front))))

(lambda (msg)
  case msg
    [[update-all!] update-all!]
    [[enqueue!] enqueue!]
    [[dequeue!] dequeue!]
    [[insert!] insert!]
    [[empty?] empty?]
    [else (error "Bad command to queue:" msg))))
```

```lisp
(define rand
(let ((q 1))
  (lambda ()
    (if (eq? q 1) (set! q 1) (set! q (+ q 1))) q))))
```

```lisp
(define SHOW-RELEASE
(lambda (patient doctor)
  (display "Dr. ")
  (display (doctor))
  (display " releases ")
  (display (patient name))
  (display ".")
  (newline)))))
```

```lisp
(define SHOW-PERSON-SICK
(lambda (patient)
  (begin
    (display (patient name))
    (display " has gotten sick.")
    (newline)))))
```

```lisp
(define SHOW-PAIR-DOC-PAT
(lambda (doc patient)
  begin
  (display "Dr. ")
  (display (doc name))
  (( treats treats
  (( (patient))
  ((display Time to treatment end is ")
    (display ()) time))

(newline(```
```lisp
(define 1 car)
```

```lisp
( 2 cnd)
```

```lisp
( 3 caddr)
```

************************
**** Skyline 矩阵 ****
********************

```lisp
(define stop-patient (patient-maker 'stop))
(rec alpha (lambda (A B)
  (if null? A
  0
  (* (car A) (car B)) (alpha (cdr A) (cdr B)))))
```

```lisp
(define fix-skyline
(lambda (m))
  (rec alpha (lambda (n lst)
    (if zero? n
  lst
    (cons (min m (car lst))
    (alpha (sub1 n) (cdr lst))))
```

```lisp
(define multiplier-list
(lambda (q))
  (rec alpha (lambda (n lst))
    (if zero? n
      (cons (- 0 (/ (car lst) q))
      (alpha (sub1 n) (cdr lst)))))
```

```lisp
(define add-row
(lambda (row-numb mult))
  (rec alpha
  (lambda (t-row col old-row)
  (if null? t-row
old-row))
```

# Scheme 335

```lisp
(if (or (> (car col) row-num) (null? old-row))
    cons (+ (* mult (car t-row)) 0)
    (alpha (cdr t-row) (cdr col) old-row))
    (cons (+ (* mult (car t-row)) (car old-row))
    (alpha (cdr t-row) (cdr col) (cdr old-row))))))))
```

```lisp
(define abstract-1
(lambda (f))
  (rec alpha (lambda (n list-1 list-2))
    (if (zero? n)
      list-1
      (cons (f n (car list-1) (car list-2))
        (alpha (subl n) (cdr list-1) (cdr list-2))))))))
```

```lisp
(define new-b-list
(lambda (b-value))
  (abstract-1 (lambda (i x) (+ (* x b-value) z))))
```

```lisp
(define new-row
(lambda (a col-skyline))
  (abstract-1 (lambda (i x) (add-row ml)
    a col-skyline)))))
```

```lisp
(define main
(lambda ()
  (let ([rows ((4 2 6) (8 6 16) (2 10) (12 14))]
    [row-sky '(2 1 2)]
    [b-list '(10 4 2)]
    [col-sky '(3 1 2)]
    (let ([s-list skyline rows row-sky col-sky b-list (length rows))]
      (begin
        (display s-list) (newline)
        (result s-list))))))
```


- 5. 为了实现与命令式语言相当的执行性能，以及
- 6. 为了验证函数式编程在大规模科学应用中的性。

这些目标强调了可用性和性能。第四、五、六目标将 Sisal 与其他函数式语言项目区分开来。它们反映了洛伦斯利弗国家实验室和其他政府机构的计算环境。

函数式语言促进了正确、确定并行程序的开发。函数式程序没有别名、副作用和依赖于时间的错误。无论架构、操作系统或执行环境如何，结果都是确定的。与并行命令式语言不同，函数式语言减轻了编程负担。用户只需定义需要计算的内容，并仅对操作之间的数据依赖关系。编译器和运行时负责调度操作、通信数据值、同步操作以及管理内存。编写一个隐式并行的函数式程序与编写一个顺序命令式程序一样简单。通过从并行编程最困难的琐事中解脱出来，用户可以自由地专注于算法设计和应用开发。

第 2 节介绍了 Sisal，并讨论了后续章节中使用的那些语言特性。完整的语言定义请参阅 [5]。在第 3、4、5 和 6 节中，我们介绍了针对四个 Salishan 问题的解决方案。由于函数式编程所需的思维与命令式编程不同，我们描述了我们如何制定每个解决方案。在第 7 节中，我们对关于 Sisal 和函数式编程的一些性意见进行了总结。

# Sisal

## 2 语言定义

Sisal 是一种强类型的通用函数式语言，支持科学计算的数据类型和操作。为了缩短学习时间并增强可读性，Sisal 的创建者采用了类似于 Pascal 的、由关键字分隔的块语法。由于大多数科学程序只编写一次但维护多年，设计者尽可能地提高可读性。Sisal 程序稍微冗长，但易于阅读和理解。某些语言特性为了可读性而牺牲了优雅性。

Sisal 具有若干语义属性。首先，该语言在数学上是完备的——函数将输入映射到输出而没有副作用。其次，具有引用透明性；也就是说，它们代表值而不是内存位置。第三，该语言是单赋值的。在每个作用范围内，一个名称只能赋值一次值。Sisal 的一项原则（其函数语义未要求，但通过编译器强制执行以帮助可读性）是：所有名称在使用之前必须定义定义。

### 2.1 类型

Sisal 支持标准的标量数据类型：boolean、char、integer,real,double_real。它还包括聚合类型：array,record,stream 和 union。用户可以使用 `type` 语句定义聚合类型。例如：

```
type Instr = stream {integer};
type OneR = array [real];
type TwoR = array [OneR];
```

分别定义了一个整数流、一个实数数组和一个实数数组的数组。后者在数学上等同于一个实数值的二维数组。

在 Sisal 中，数组和流都是任何标准类型或用户定义类型的同质聚合句体。数组支持随机访问，而流的元素只能按先进先出（FIFO）顺序可用。也就是说，在消费第 (i + j) 个元素之前，必须先消费流的第 i 个元素。因此，Sisal 的流不会发生死锁。数组声明不包含大小或边界信息。数组的大小、下界和形状是在执行期间确定的。由于多维数组的组件是数组，每个组件可能有不同的长度和下界。我们称 Sisal 的数组是“参差不齐的”（ragged）。

名称的类型没有声明；相反，编译器从上下文推断每个名称的类型。两个例外是函数的正式参数和结果。这两个可以被推断，但是以牺牲可读性为代价的。类型在函数头中声明。

### 2.2 函数

函数可以接受零或多个参数，并必须返回一个或多个值。每个正式参数和结果值的类型在函数头中声明。例如，函数 `circle`

```
function circle(radius: real returns real, real)
  2.0 * 3.14 * radius * radius
end function
```

接受一个类型为 `real` 的正式参数 `radius`，并返回两个实数值，圆的周长和面积。函数或表达式返回的值的数量被称为函数或表达式的元数（arity）。函数只能访问其参数。没有全局值，函数在调用之间不保留状态。调用函数的影响仅限于它返回的值——没有副作用。

一个函数可以接受零或多个参数，并必须返回一个或多个值。每个正式参数和结果值的类型在函数头中声明。例如，函数 `circle`

```
function circle(radius: real returns real, real)
  2.0 * 3.14 * radius * radius
end function
```

接受一个类型为 `real` 的正式参数 `radius`，并返回两个实数值，圆的周长和面积。函数或表达式返回的值的数量被称为函数或表达式的元数。函数只能访问其参数。没有全局值，函数在调用之间不保留状态。调用函数的影响仅限于它返回的值——没有副作用。

一个函数可以接受零或多个参数，并必须返回一个或多个值。每个正式参数和结果值的类型在函数头中声明。例如，函数 `circle`

```
function circle(radius: real returns real, real)
  2.0 * 3.14 * radius * radius
end function
```

接受一个类型为 `real` 的正式参数 `radius`，并返回两个实数值，圆的周长和面积。函数或表达式返回的值的数量被称为函数或表达式的元数。函数只能访问其参数。没有全局值，函数在调用之间不保留状态。调用函数的影响仅限于它返回的值——没有副作用。

一个函数可以接受零或多个参数，并必须返回一个或多个值。每个正式参数和结果值的类型在函数头中声明。例如，函数 `circle`

```
function circle(radius: real returns real, real)
  2.0 * 3.14 * radius * radius
end function
```

接受一个类型为 `real` 的正式参数 `radius`，并返回两个实数值，圆的周长和面积。函数或表达式返回的值的数量被称为函数或表达式的元数。函数只能访问其参数。没有全局值，函数在调用之间不保留状态。调用函数的影响仅限于它返回的值——没有副作用。

一个函数可以接受零或多个参数，并必须返回一个或多个值。每个正式参数和结果值的类型在函数头中声明。例如，函数 `circle`

```
function circle(radius: real returns real, real)
  2.0 * 3.14 * radius * radius
end function
```

接受一个类型为 `real` 的正式参数 `radius`，并返回两个实数值，圆的周长和面积。函数或表达式返回的值的数量被称为函数或表达式的元数。函数只能访问其参数。没有全局值，函数在调用之间不保留状态。调用函数的影响仅限于它返回的值——没有副作用。

一个函数可以接受零或多个参数，并必须返回一个或多个值。每个正式参数和结果值的类型在函数头中声明。例如，函数 `circle`

```
function circle(radius: real returns real, real)
  2.0 * 3.14 * radius * radius
end function
```

接受一个类型为 `real` 的正式参数 `radius`，并返回两个实数值，圆的周长和面积。函数或表达式返回的值的数量被称为函数或表达式的元数。函数只能访问其参数。没有全局值，函数在调用之间不保留状态。调用函数的影响仅限于它返回的值——没有副作用。

一个函数可以接受零或多个参数，并必须返回一个或多个值。每个正式参数和结果值的类型在函数头中声明。例如，函数 `circle`

```
function circle(radius: real returns real, real)
  2.0 * 3.14 * radius * radius
end function
```

接受一个类型为 `real` 的正式参数 `radius`，并返回两个实数值，圆的周长和面积。函数或表达式返回的值的数量被称为函数或表达式的元数。函数只能访问其参数。没有全局值，函数在调用之间不保留状态。调用函数的影响仅限于它返回的值——没有副作用。

一个函数可以接受零或多个参数，并必须返回一个或多个值。每个正式参数和结果值的类型在函数头中声明。例如，函数 `circle`

```
function circle(radius: real returns real, real)
  2.0 * 3.14 * radius * radius
end function
```

接受一个类型为 `real` 的正式参数 `radius`，并返回两个实数值，圆的周长和面积。函数或表达式返回的值的数量被称为函数或表达式的元数。函数只能访问其参数。没有全局值，函数在调用之间不保留状态。调用函数的影响仅限于它返回的值——没有副作用。

一个函数可以接受零或多个参数，并必须返回一个或多个值。每个正式参数和结果值的类型在函数头中声明。例如，函数 `circle`

```
function circle(radius: real returns real, real)
  2.0 * 3.14 * radius * radius
end function
```

接受一个类型为 `real` 的正式参数 `radius`，并返回两个实数值，圆的周长和面积。函数或表达式返回的值的数量被称为函数或表达式的元数。函数只能访问其参数。没有全局值，函数在调用之间不保留状态。调用函数的影响仅限于它返回的值——没有副作用。

- 5. 为了实现与命令式语言相当的执行性能，以及
- 6. 为了验证函数式编程在大规模科学应用中的性。

这些目标强调了可用性和性能。第四、五、六目标将 Sisal 与其他函数式语言项目区分开来。它们反映了洛伦斯利弗国家实验室和其他政府机构的计算环境。

函数式语言促进了正确、确定并行程序的开发。函数式程序没有别名、副作用和依赖于时间的错误。无论架构、操作系统或执行环境如何，结果都是确定的。与并行命令式语言不同，函数式语言减轻了编程负担。用户只需定义需要计算的内容，并仅对操作之间的数据依赖关系。编译器和运行时负责调度操作、通信数据值、同步操作以及管理内存。编写一个隐式并行的函数式程序与编写一个顺序命令式程序一样简单。从并行编程最困难的琐事中解脱出来，用户可以自由地专注于算法设计和应用开发。

第 2 节介绍了 Sisal，并讨论了后续章节中使用的那些语言特性。完整的语言定义请参阅 [5]。在第 3、4、5 和 6 节中，我们介绍了针对四个 Salishan 问题的解决方案。由于函数式编程所需的思维与命令式编程不同，我们描述了我们如何制定每个解决方案。在第 7 节中，我们对关于 Sisal 和函数式编程的一些性意见进行了总结。

# Sisal

## 2 语言定义

Sisal 是一种强类型的通用函数式语言，支持科学计算的数据类型和操作。为了缩短学习时间并增强可读性，Sisal 的创建者采用了类似于 Pascal 的、由关键字分隔的块语法。由于大多数科学程序只编写一次但维护多年，设计者尽可能地提高可读性。Sisal 程序稍微冗长，但易于阅读和理解。某些语言特性为了可读性而牺牲了优雅性。

Sisal 具有若干语义属性。首先，该语言在数学上是完备的——函数将输入映射到输出而没有副作用。其次，具有引用透明性；也就是说，它们代表值而不是内存位置。第三，该语言是单赋值的。在每个作用范围内，一个名称只能赋值一次值。Sisal 的一项原则（其函数语义未要求，但通过编译器强制执行以帮助可读性）是：所有名称在使用之前必须定义。

### 2.1 类型

Sisal 支持标准的标量数据类型：boolean、char、integer,real,double_real。它还包括聚合类型：array,record,stream 和 union。用户可以使用 `type` 语句定义聚合类型。例如：

```
type Instr = stream {integer};
type OneR = array [real];
type TwoR = array [OneR];
```

分别定义了一个整数流、一个实数数组和一个实数数组的数组。后者在数学上等同于一个实数值的二维数组。

在 Sisal 中，数组和流都是任何标准类型或用户定义类型的同质聚合句体。数组支持随机访问，而流的元素只能按先进先出（FIFO）顺序可用。也就是说，在消费第 (i + j) 个元素之前，必须先消费流的第 i 个元素。因此，Sisal 的流不会发生死锁。数组声明不包含大小或边界信息。数组的大小、下界和形状是在执行期间确定的。由于多维数组的组件是数组，每个组件可能有不同的长度和下界。我们称 Sisal 的数组是“参差不齐的”（ragged）。

名称的类型没有声明；相反，编译器从上下文推断每个名称的类型。两个例外是函数的正式参数和结果。这两个可以被推断，但是以牺牲可读性为代价的。类型在函数头中声明。

### 2.2 函数

函数可以接受零或多个参数，并必须返回一个或多个值。每个正式参数和结果值的类型在函数头中声明。例如，函数 `circle`

```
function circle(radius: real returns real, real)
  2.0 * 3.14 * radius * radius
end function
```

接受一个类型为 `real` 的正式参数 `radius`，并返回两个实数值，圆的周长和面积。函数或表达式返回的值的数量被称为函数或表达式的元数（arity）。函数只能访问其参数。没有全局值，函数在调用之间不保留状态。调用函数的影响仅限于它返回的值——没有副作用。

一个函数可以接受零或多个参数，并必须返回一个或多个值。每个正式参数和结果值的类型在函数头中声明。例如，函数 `circle`

```
function circle(radius: real returns real, real)
  2.0 * 3.14 * radius * radius
end function
```

接受一个类型为 `real` 的正式参数 `radius`，并返回两个实数值，圆的周长和面积。函数或表达式返回的值的数量被称为函数或表达式的元数。函数只能访问其参数。没有全局值，函数在调用之间不保留状态。调用函数的影响仅限于它返回的值——没有副作用。

（此处省略重复的函数描述段落，遵循“不要重复输出原文”原则，但原文中确实存在重复，译文已按逻辑处理） 

...

```
function circle(radius: real returns real, real)
  2.0 * 3.14 * radius * radius
end function
```

继续...]

### 2.4 For 表达式

for 表达式，

```
for <range generator>
  loop body
  returns <returns clause>
end for
```

是 Sisal 中的并行形式。它包含三个部分：范围生成器、循环体和返回子句。范围生成器是序列或散点的点积（见图 1）。循环体为每个索引、值执行一次。范围生成器规定了归约顺序，并定义了生成对象的大小和结构。例如，该表达式返回一个行列列二维数组。

循环体是一组名称定义。Sisal 的语义防止循环体实例引用任何其他实例计算的值。因此，循环体的实例是数据独立的，可以并行执行。

返回子句定义了 for 表达式的元数、类型和值。每个结果都是循环体内定义的归约。归约顺序是确定的，等同于循环体的顺序执行。图 2 列出了 Sisal 支持的八种操作。参与归约的值可以通过包含 `when` 子句进行过滤。例如，

```
array of x when x > 0
```

返回一个只有正数的数组。如果没有值是正数，则返回一个与 x 类型相同的空数组。

### 2.3 Let 表达式

let 表达式由两个子句组成：let 子句和 in 子句。后者定义值。例如，

```
let pi = 3.14
in
pi * radius
```

返回圆的周长和面积。let 表达式定义了一组名称，然后使用 in 子句计算一个或多个值。

| 范围生成器 | 注释 |
|---|---|
| for x in A | 一个散点 (scatter) |
| for i in 1, n | 一个序列 (sequence) |
| for x in A dot y in B | 两个散点的点积 |
| for i in 1, n cross j in 1, n | 两个序列的交叉积 |

图 1 - 范围生成器的形式





344

J. T. Feo

| 返回子 | 注释 |
|---|---|
| value of x | 返回 x 的最后一个值 |
| array of x | 返回一个 x 值的数组 |
| stream of x | 返回一个 x 值的流 |
| value of sum x | 返回 x 值的和 |
| value of product x | 返回 x 值的乘积 |
| value of least x | 返回最小的 x 值 |
| value of greatest x | 返回最大的 x 值 |
| value of catenate x | 返回由连接 x 值形成的数组（注意 x 必须是一个数组） |

图 2 - 返回子

```
$$\sum_{k=1}^m a(i, k) \cdot b(k, j), \quad 1 \leq i, j \leq n \quad (2.1)$$
```

我们首先写下

```
function mmul(n,m: integer; a,b: TwoR returns TwoR
  ..
end function
```

这将 `mmul` 定义为一个具有四个输入的函数：类型为 integer 的 n 和 m，以及类型为 TwoR 的 a 和 b（之前定义）。该函数返回一个类型为 TwoR 的值，即 a 和 b 的乘积。

函数体是方程 2.1 的 Sisal 表达式。由于该方程计算了 $n^2$ 个独立的实数并将它们组合成一个数组，我们想要使用以下表达式：

```
for i in 1, n cross j in 1, n
  Cij := n returns array of Cij
end for
```

# Sisal

Cij 是 $a$ 的第 $i$ 行与 $b$ 的第 $j$ 列的内积。我们将两个 $m$ 元素向量的内积写为：

```
for k in 1, m
  returns value of sum a[i,k] * b[k,j]
end for
```

将所有内容结合，我们得到：

```
function mmul(n,m: integer; a,b: TwoR returns TwoR)
  for i in 1, n cross j in 1, n
    Cij := for k in 1, m
      returns value of sum a[i,k] * b[k,j]
    end for
  returns array of Cij
  end function
```

这里有三个重要的观察。首先，函数只表达了必要的数学计算。该函数的实现是 100% 并行的，并未指定。其次，该函数是动态的。执行它所需的资源完全取决于 $n$ 和 $m$。没有内存或处理器的静态分配。第三，与首先分配结果内存然后填充内存的命令式函数不同，Sisal 函数由单个表达式组成，该表达式既创建又定义了结果。

# 2.5. 初始表达式 (For Initial expressions)

对于 for initial 表达式，

```
for initial
<initialization>
while <test> repeat
<loop body>
returns <returns clause>
end for
for initial
<initialization>
repeat
<loop body>
until <test>
returns <returns clause>
end for
```

允许循环携带依赖（loop carried dependencies），但保留了单次赋值语义。它包含四个部分：初始化、测试、循环体和结果子。初始化部分定义了所有的循环常量，并为循环携带的名称分配初始值。它是循环的第一次迭代。

测试可以出现在循环体之前或之后。Sisal 支持两种形式：`while <test>` 和 `until <test>`。循环体为所有循环携带的名称计算新值。循环体的实例可以通过在名称前加上关键字 `old` 来引用上一个实例中定义的任何循环携带名称。因此，`old a` 指的是上一次迭代中 `a` 的值。注意，在当前迭代中定义一个值不会破坏旧值。循环携带名称对值的重新绑定是隐式的，发生在迭代之间。

for initial 表达式的返回子在语法和语义上与 for 表达式的返回子相同。

作为 for initial 表达式的示例，考虑函数 `first_sum`。设 $x$ 为长度为 $n$ 的实向量，则 $y(i)$

```
y(i) = ∑ⱼ=1ⁿ x(j), 1≤i≤n
```

虽然 $y$ 的元素是数据独立的，但使用 for 表达式将导致 $O(n^2)$ 次加法。使用 for initial 表达式可以获得更高效的算法。

# Sisal

首先，我们将方程 2 重写为

```
$y(i) = \begin{cases} x(1) \\ y(i-1) + x(i) \end{cases} \quad i = 1 \quad 2 \le i \le n \quad (2.3)$
```

然后用 Sisal 写下方程 2.3：

```
function first_sum(n: integer; x: OneR returns OneR
  for initial
    i := 1;
    y := x[1]
    while i < n repeat
      i := old y + 1;
      y := old y + x[i]
      returns array of y
    end for
end function
```

再次，从数学到 Sisal 的翻译是直观的。循环的“如何”（为结果分配内存并向位置赋值——是隐式的，由表达式的语义所暗示。

### 2.6. 数组和流操作

图 3 和图 4 列出了 Sisal 中的一些数组和流操作。重要的是记住，这些以及 Sisal 中的所有操作都保留了单次赋值。语句

```
A[1: 0, 1, 2]
```

并不是像命令式语言那样替换 A 的第一个、第二个和第三个元素，而是创建一个与 A 相同的新数组，其第一个、第二个和第三个元素被设置为 0、1 和 2。函数

```function
stream_first(A)
```

| 数组操作 | 注释 |
|---|---|
| array OneR | 创建一个空数组（需要类型） |
| array OneR | 创建一个实值数组（类型可选） |
| array_fill(1, n, 0) | 创建一个全 0 数组，下界为 1，上界为 |
| A[1: 0, 1, 2] | 创建一个与 A 相同的新数组，元素为 1、2 和 3 |
| A || B | 创建 A 和 B 的连接 |

| 流操作 | 注释 |
|---|---|
| stream_append(A, v) | 创建一个与 A 相同且追加了 v 的流 |
| stream_rest(A) | 创建一个与 A 相同且删除了第一个元素的流 |
| stream_first(A) | 返回 A 的第一个元素 |
| stream_empty(A) | 如果 A 为空且生产者已终止，则为真 |

通过仔细观察图 3 中列出的数组操作和上一节描述的循环结构，可能会得出结论：Sisal 的单次赋值语义以及这些操作隐含的拷贝和内存管理使得 Sisal 不适用于科学计算。然而，研究表明，编译时分析可以消除所有不必要的拷贝和内存管理操作。事实上，Sisal 的保守语义和式数组操作有助于分析。我们完全预计将达到与命令式语言相当的执行性能。

## 3. 哈明问题（扩展）

# 3.1. 理解哈明问题

给定一个整数 $n$ 和一个质数集合 $\{a, b, c...\}$，按顺序且不重复地生成所有形式如下的整数

```
a^l b^j c^k ... n
```

解决哈明问题的一种方法是计算集合的笛卡尔积

```
{a^l | l ≥ 0}, {b^j | j ≥ 0}, {c^k | k ≥ 0}, . .
```

形成形式如下的元组集

```
$(a^i, b^j, c^k, \dots) \quad i, j, k \geq 0$
```

将每个元组的元素相乘，按顺序排序并丢弃大于 $n$ 的整数，即可解决哈明问题。

例如，令 $n = 10$，质数集合为 $\{2, 3, 5\}$。我们首先形成三个集合 $\{1, 2, 4, 8\}, \{1, 3, 9\}, \{1\}$ 注意我们丢弃了大于 10 的整数。接下来形成这三个集合的笛卡尔积

```
{ (1,1,1), (1,1,5), (1,3,1), (1,3,5), (1,9,1), (1,9,5), (2,1,1), (2,1,5), (2,3,1), (2,3,5), (2,9,1), (2,9,5), (4,1,1), (4,1,5), (4,3,1), (4,3,5), (4,9,1), (4,9,5), (8,1,1), (8,1,5), (8,3,1), (8,3,5), (8,9,5) }
```

将每个元组的元素相乘，按顺序排序并丢弃大于 10 的值，得到集合

```
{ 1, 2, 3, 4, 5, 6, 8, 9, 10 }
```

图 5a 显示了一个计算 2 的幂次的任务图。它包含一个任务和两个边：$i, s$ 和 $b$。边作为零或多个值的 FIFO 队列。任务的指令集为：

+   1. 从边 $i$ 移除令牌，令其值为 $x$
2. repeat
3. 在边 $s$ 输出 $x$
4. 在边 $b$ 输出 2 次
5. 从边 $b$ 移除令牌，令其值为 $x$





# Sisal

图 5a - 计算 2 的幂次的任务图

图 5b - 计算 2^i 3^j 5^k 的任务图

图 5c - 任务图 5b 的快照

图 5b 展示了三个连接在一起的任务图实例。在最右侧 s 边发布的令牌（tokens）是质数集合 [2, 3, 5] 的汉明解。第二个和第三个任务的指令集需要略微修改。在每次迭代中（除第一次外），任务可以选择从入的 s 边或 b 边移除一个令牌。通过移除两个值中较小的一个，任务对输出到输出 s 边的值进行了排序。图 5c 显示了图 5b 中任务图的快照。

### 3.2. 一个 Sisal 解决方案

在本节中，我们将解释如何在 Sisal 中表示图 5b 所示的任务图。我们使用 `for initial` 表达式和流（streams）来为每个质数生成一个任务，并在任务 i 和 i+1（i ≥ 1）之间建立一个先进先出（FIFO）队列。Sisal 代码如下：

```
for initial
  i := 0;
  s_stream := array_size(primes) repeat
    i := old i + 1;
    s_stream := powers(n, primes[i], old s_stream)
  returns value of s_stream
end for
```

初始化子定义了 i 和 s_stream，后者是一个包含一个元素的整数流。循环体迭代执行，每个质数执行一次。循环体增加 i，并调用带有三个参数的函数 `powers`：n、第 i 个质数以及 `old s_stream`（上一次迭代时 s_stream 的值）。`for` 表达式的值是最后一次迭代中定义的 s_stream 的值（即由最后一次调用 `powers` 返回的值）。`for` 表达式为每个质数调用了一个 `powers` 实例，并在连续的实例之间建立了 FIFO 队列。如果流是惰性实现的（这正是我们的意图），这些实例将并发存在，利用任务图中的生产者/消费者并行性。

`powers` 函数实现了图 5a 所示的任务图。曾有人认为 Sisal 无法表达这种循环计算，但这种观点是不正确的。Sisal 在三个条件下可以表达循环计算：1) 输入边的初始条件是已知的（即计算有确定地开始），2) 循环计算可以展开为一系列任务，以及 3) 任务输出与任务输入同步（即任务在发布下一个输出之前始终等待下一个输入）。图 5a 中的任务图满足了所有三个要求。

`powers` 的 Sisal 代码见附录。`for initial` 表达式的每次迭代都会移除 `old s_stream` 和 `old b_stream` 头部较小的值（称之为令牌），将该令牌添加到输出流中，定义一个新的 `s_stream`，并定义一个在末尾附加了令牌 *乘以 质数* 的新 `b_stream`。由于任务可能会耗尽 s_stream，因此一个对 `stream_empty` 的测试是必要的。另一方面，任务永远不会耗尽 b_stream，因为在每次迭代中都会向流中添加一个新值。

注意函数式和命令式解决方案的处理过程有多么不同。函数式程序员首先在逻辑上指定计算过程，然后将规范翻译成代码。他以表达式的方式思考，这些表达式在执行时会绽变为所需的任务图。任务调度、内存分配和处理由编译器和运行时系统自动完成。对共享数据的同步访问是隐式的——细节由系统处理。命令式程序员在开始解决汉明问题时，可能首先定义 FIFO 队列、一组队列操作以及一个针对读取者和写入者的访问协议。在使用队列编写任务体代码后，必须小心不要违反操作语义或访问协议。确保正确性完全是他的责任。编译器和运行时系统提供的支持很少或没有支持。由于在命令式并行程序中很容易引入微妙的时间相关性错误，编程过程非常困难且容易出错。

# 乙烷、丙烷、异丁烷

图 6 - 大小为1, 2, 3, 4 的异构体

图 7 - 异构体

## 4. 烷烃

### 4.1. 基于有向树的 Sisal 解决方案

烷烃是一种含有 $n_2$ 的氢化合物。烷烃问题要求我们输出所有大小小于 $n$ 个原子的异构体。由于异构体的数量随着碳原子数量的增加而增加，这个问题是非常昂销的。图 8 显示了大小为 1, 2, 3, 4 的有向树。

函数式程序员首先在逻辑上指定计算过程，然后将规范翻译成代码。他以表达式的方式思考，这些表达式在执行时会绽变为所需的任务图。任务调度、内存分配和处理由编译器和运行时系统自动完成。





# Sisal

357

(0, 0, 3)

![](img/68e0c8e7cd61671f4d693a9b7458d12d_367_0.png)

(0, 0, 3)

![](img/68e0c8e7cd61671f4d693a9b7458d12d_367_1.png)

![](img/68e0c8e7cd61671f4d693a9b7458d12d_367_2.png)

(0, 1, 2)

(1, 1, 1)

![](img/68e0c8e7cd61671f4d693a9b7458d12d_367_3.png)

![](img/68e0c8e7cd61671f4d693a9b7458d12d_367_4.png)

图 9 - 构建大小为 4 的有向树

## 双质心：

1. 对 $b$ 和 $d$ 的所有选择重复
2. 选择两个有向树 $T_b^n$ 和 $T_d^n$
3. 将两棵树的根连接在一起。

图 10 展示了算法如何构建大小为 6 的烷烃。

构建过程必须使用有向树，因为必须对排列中的每个可区分节点集考虑一次每个节点排列方式。对于 $n=3$，有两组可区分节点：端节点和内部节点。有两种有向树：其中一个的根是端节点，另一个的根是内部节点。注意，大小为 3 的自由树只有一个（丙烷）。通过三种方式将两棵有向树的根连接在一起——端节点到端节点、端节点到内部节点、以及内部节点到内部节点——构建出三种大小为 6 的双质心异构体。

## 单质心：

(0, 1, 2, 2)

![](img/68e0c8e7cd61671f4d693a9b7458d12d_368_0.png)

(1, 1, 1, 1)

![](img/68e0c8e7cd61671f4d693a9b7458d12d_368_1.png)

## 双质心：

![](img/68e0c8e7cd61671f4d693a9b7458d12d_368_2.png)

图 10 - 构建大小为 6 的烷烃

### 4.2. 在 Sisal 中构建烷烃

编写 Sisal 函数来实现上一节描述的算法是非常直接的。我们将有向树和自由树（烷烃）都表示为字符字符串；即：

```
type trees = array[character]
```

对于前五个烷烃（图 6），我们的程序生成字符字符串：

(C) ((C) (C)) (C) (C)) ((C) (C) (C)) ((C) (C) (C) (C))

如果字符串是一个有向树，那么第一个 C 是树的根，同一层级的 C 的括号列表是子树。如果字符串是具有单质心的烷烃，则第一个 C 是质心。如果字符串是具有双质心的烷烃，则该字符串将分为两个具有相同数量 C 的字符串。质心是每个半部分的第一个 C。

我们将大小为 $i$ 的有向树和自由树（异构体）存储为树的数组：

```
type TreeArray = array[tree]
```

并将大小 $\le n$ 的有向树和自由树（烷烃分子）存储为树类型的数组数组：

```
type TreeArray2 = array[TreeArray]
```

主函数 Paraffins 接受一个整数参数 $n$，并返回一个 `TreeArray2` 类型的值。由于不同碳原子数的异构体数量也不同，结果数组将是不规则的。函数体是 `let` 表达式：

```
let Trees := OrientedTrees(n/2)
in for i in 1, n
    isomer := if mod(i, 2) = 1 then
        OneCentroid(i, Trees)
    else
        TwoCentroid(i, Trees)
    end
```

它定义了有向树并构建了大小从 1 到 $n$ 的烷烃。结果数组并行构建并按顺序返回。OrientedTrees 函数（见附录）实现了上一节描述的动态规划算法。该函数接受 $n$ 作为输入并返回大小为 $[0 ... n/2]$ 的数组，而体的第 $i$ 次迭代根据小于 $i$ 的树构建大小为 $i$ 的有向树。调用者保证 $a \le c \le e；在这种情况下，它们的集合交叉积是对称的。我们通过将交叉积结构化为 $(Trees[c] \times Trees[a]) \times (Trees[e] \times Trees[g])$ 并包含以下测试来消除对称性和重复：

1. 如果 $c = a$，则仅返回交叉积的下三角（图 1a）；否则返回整个乘积。
2. 如果 $e = g$，则仅返回交叉积的上三角（图 1b）；否则返回整个乘积。
3. 如果 $c = e$，则仅返回交叉积的下三角（图 1c）；否则返回整个乘积。

OneCentroid 函数（见附录）接受 $i$ 和有向树数组，返回具有单质心的大小为 $i$ 的自由树。三嵌套范围生成器：

```
for a in 0, (i - 1)/4 cross
  c in a, (i - 1 - a)/3 cross
  e in max(c, i/2 - a - c), (i - 1 - c)/2
```

为所有满足方程 4.1 的树大小组合创建一个函数体的实例（调用 XTrees）。由于 $c$ 和 $e$ 的值定义了 $g$ 的值，因此不需要第三个循环。TwoCentroid（见附录）接受 $i$ 和有向树数组，返回具有双质心的大小为 $i$ 的自由树。双嵌套范围生成器：

```
for b in 1, array_size(Trees/2) cross
d in b, array_size(Trees/2)
```

为每对大小为 $i/2$ 的有向树产生一个操作实例。这两个函数无重复地按顺序构建相应的树结构。图 1 - $a = c = e$ 时的表达式结果：

| (x,x) | (x,y) | (x,z) |
| :--- | :--- | :--- |
| (y,x) | (y,y) | (y,z) |
| (z,x) | (z,y) | (z,z) |

(a)

| (x,x) | (x,y) | (x,z) |
| :--- | :--- | :--- |
| (y,x) | (y,y) | (y,z) |
| (z,x) | (z,y) | (z,z) |

(b)

| (x,x,x,x) | (x,x,x,y) | (x,x,x,z) |
| :--- | :--- | :--- |
| (y,x,x,x) | (y,x,x,y) | (y,x,x,z) |
| (z,y,x,x) | (z,y,x,y) | (z,y,x,z) |
| (y,y,x,x) | (y,y,y,y) | (y,y,y,z) |
| (z,x,y,y) | (z,x,y,y) | (z,x,y,z) |
| (z,z,x,x) | (z,z,x,y) | (z,z,x,z) |
| (z,z,x,x) | (z,z,x,y) | (z,z,x,z) |
| (z,y,z,x) | (z,y,z,y) | (z,y,z,z) |
| (z,z,z,x) | (z,z,z,y) | (z,z,z,z) |

(c)

# 5. 诊室

## 5.1. 诊室的逻辑视图

给定一组患者和医生，模拟以下系统。最初，所有患者都是健康的，所有医生都是空闲的。医生在诊室的 FIFO 队列中等待患者。随机时间内，患者会生病、前往诊室并在医生 FIFO 队列中等待。护士将队列中的第一个患者和第一个医生配对，并为他们分配诊室。在诊室室内，医生在随机的时间内治愈患者。患者回到世界，医生回到护士站。图 12 显示了由三个任务和四条边组成的诊室逻辑视图。边作为零或多个值的 FIFO 队列。





正如汉明问题一样，我们面临着实现循环计算的问题。我们再次使用 `for initial` 表达式，并依赖表达式的循环语义来满足循环依赖。我们使用数组而不是流（streams）来实现先进先出（FIFO）队列，其原因很快就会显而易见。与汉明问题不同，3.2节中列出的三个条件仅满足了一个——即每条边的初始状态是已知的。

- Patients_In - 空
- Patient_Out - 患者列表
- Doctor_Out - 医生列表
- Patient_Doctor - 空

`for initial` 表达式的语义意味着任务的序列以及任务输入/输出的同步，这在精神上违背了规范，尽管它可能在字面上没有违背。理想情况下，这三个任务应该异步执行并通信，且没有任何任何限制。

遗憾的是，Sisal 排除了所有形式的异步性。它的函数是确定的。输出仅取决于输入，而与架构、操作系统、系统负载或程序状态无关。流的消费者无法测试流的数据可用性；如果是这样，消费者可以被程序为根据数据是否到达采取不同的行动。那么函数的输出将取决于生产者的执行速度、通信网络的速度和拥堵以及操作系统的调度策略。一旦消费者尝试读取下一个流值，它必须等待直到该值到达。为了从字面上解决“诊所”问题，这三个任务必须继续执行，无论它们的所有输入边是否到了数据。也就是说，无论治愈的患者是否从诊所返回，患者都必须处于病态；无论新患者或医生是否到达，患者-医生对都必须离开护士站；无论新的患者-医生对是否开始治疗，患者都必须被治愈。在5.3节中我们将解决这一困境并提出一个合理的解决方案。

## 5.2. 主函数

我们定义了两个新类型：

```
type queue = array[integer];
type queue2 = array[array[integer]];
```

并将 `main` 函数写写如下：

```
for initial
  seed := 0;
  patient_in := array queue [];
  patient_out := list_of_patients;
  doctor_out := list_of_doctors;
  patient_doctor := array queue2 [];
while true repeat
  seed := next_seed(old seed);
  patient_in := well_person(seed, old patient_out);
  patient_doctor := nurse(old patient_in, old doctor_out);
  patient_out, doctor_out := examinations(seed, old patient_doctor)
returns stream of patient_in
stream of doctor_out
end for
end function
```

`patient_in`、`patient_out` 和 `doctor_out` 是 `queue` 类型；`doctor_patient` 是 `queue2` 类型。初始化序列定义了四个数组和 `seed` 的初始值。后者被 `well_person` 和 `examinations` 用于驱动随机数生成器。体中的三个任务在执行时消耗在上一次迭代中定义的边值。该表达式返回患者队列的流和医生队列的流。

该表达式是不正确的。注意 `well_person` 接收 `old patient_out` 作为输入，即上一次迭代中被治愈的患者，他们现在重新加入健康患者数组。在上一次迭代中所有健康的患者都没有生病或丢失。状态并没有被保留。健康患者、在诊疗室等待的患者和医生是持久性数据集，它们不是在单次操作中创建和消耗的。由于 Sisal 函数是无副作用的且在调用之间不保留状态，我们必须显式地在迭代之间维护并传递状态。

因此，`well_person` 必须返回两个集合或数组：新的病患，以及仍然健康的患者数组。`nurse` 必须返回三个数组：新的患者-医生对、仍在等待医生的病患以及仍在等待患者的可用医生。`examinations` 必须返回三个数组：新治愈的患者、新可用的医生以及仍在诊疗室的患者-医生对。图13显示了新的边（数组）以及重新组状态所需的连接（catenate）操作。新的 `main` 函数是：

```
for initial
  seed           := 0;
  still_well      := list_of_patients;
  patient_out    := array queue [];
  still_sick      := array queue [];
  patient_in     := array queue [];
  still_available := list_of_doctors;
  doctor_out     := array queue [];
  still_examining := array queue2 [];
  patient_doctor := array queue2 []
while true repeat
    seed           := next_seed(old seed);
    still_well, patient_in :=
    person(seed, old still_well || old patient_out);
    still_sick, patient_doctor, still_available :=
    nurse(old still_sick || old patient_in,
    old still_available || old doctor_out);
    still_examining, patient_out, doctor_out :=
    examinations(seed, old still_examining || old patient_doctor)
returns stream of patient_in
    stream of doctor_out
```

为了简单起见，我们将连接操作推入了函数的参数列表中。

## 5.3. 三个任务

迭代 $i$ 的任务在迭代 $(i - 1)$ 的任务完成之前无法执行。循环携带依赖关系对迭代 $i$ 施加了约束。正如5.1节所述，迭代 $(i - 1)$ 的任务必须为迭代 $i$ 生成某些输出，使其能够执行。虽然我们对“诊所”问题的解决方案并不完美，由于 Sisal 显式排除了所有形式的异步性，我们永远无法希望完全解决该问题。我们所达的程度证明了 Sisal 的健壮性。`well_person` 的代码如下：

```
function well_person (seed: integer; old_patient_out: list)
returns array, array
let
    size := random(seed);
    still_well := old_still_well || old_patient_out;
    patient_in := array queue [];
    ...
    return patient_in, still_well
```_）
```

`nurse` 的代码类似：

```
function nurse (old still_sick: list; old patient_in: list; old still_available: list; old doctor_out: list)
returns array, array, array
let
    size := 0;
    still_sick := old_still_sick || old_patient_in;
    still_available := old_still_available || old_doctor_out;
    patient_doctor := array queue2 []
    ...
    return patient_doctor, still_sick, still_available
```

`examinations` 的代码为：

```
function examinations (seed: integer; old_still_examining: array2; old_patient_doctor: array2)
returns array, array, array
let
    size := 0;
    still_examining := old_still_examining || old_patient_doctor;
    patient_out := array queue [];
    doctor_out := array queue [];
    ...
    return patient_out, doctor_out, still_examining
```

## 6.0. 天际线问题 (Skyline Problem)

### 6.1. 无主元高斯消法

在这个问题中，我们被求解线性方程组

```
A x = b
```
(6.1)

线性方程组的传统求解方法是非主元高斯消法。该方法将 $A$ 转换为三角矩阵 $A'$，$b$ 转换为列向量 $b'$，使得：

```
$A' x = b'$
```
(6.2)

$A'$ 可以是上三角或下三角的。方程 6.2 然后通过称为回代法的方法求解。

6.3节开发的 Sisal 算法形成了一个下三角矩阵。归约在 $n-1$ 个步骤中进行，每行一步。为了消除上三角矩阵，我们从 $n$ 反向到 1。在步骤 $i$，我们按如下方式归约：

```
$A_{j,k} = A_{j,k} - (b_i * A_{i,k} / A_{i,t})$ $\quad 1 \le j < i, 1 \le k \le i$
```
(6.3.1)

以及

```
$b_j = b_j - (b_i * A_{i,j} / A_{i,t})$ $\quad 1 \le j < i$
```
(6.3.2)

第 $i$ 行到第 $n$ 行的元素





370

J. T. Feo

| 1 | 0 | 0 | 1 | 0 | 0 |
| 0 | 1 | 0 | 1 | 1 | 0 |
| 0 | 1 | 1 | 1 | 1 | 0 |
| 0 | 0 | 0 | 1 | 1 | 0 |
| 0 | 1 | 1 | 1 | 1 | 0 |
| 0 | 0 | 0 | 0 | 0 | 1 |

A

row = [1, 2, 2, 4, 2, 4, 7] column = [1, 2, 3, 1, 3, 2, 7]

图 14 - 天际线矩阵及相关的行、列向量

为了求解 $x$，我们首先求解 $x_1$

$x_1 = b'_1 / A'_{1,1}$ (6.4.1)

一旦有了 $x_1$，我们就可以求解 $x_2$

$x_2 = (b'_2 - A'_{2,1} x_1) / A'_{2,2}$ (6.4.2)

然后是 $x_3$

$x_3 = (b'_3 - A'_{3,1} x_1 - A'_{3,2} x_2) / A'_{3,3}$ (6.4.3)

依此类推。

### 6.2. Sisal 中天际线矩阵的高效表示

高效实现天际线矩阵问题的关键在于消除每行和每列开头的零元素，从而消除涉及这些零元素的计算。Sisal 的**不规则数组**（ragged array）结构非常适合解决这个问题。由于 Sisal 中的“二维”数组是“数组的数组”，且由于每个组件数组可以有不同的大小和下界，我们可以通过将组件 $i$ 的下界设置为 `row[i]` 来消除每行开头的零元素。回想 `row` 和 `column` 存储了每行每列中第一个非零元素的位置。由于组件数组必须是连续的，我们可以通过将每个组件数组的上界设置为该行中最后一个非零元素的索引位置，来消除对角线上的部分零元素。例如，图 14 所示数组中第一行第 5 到 7 列的零可以通过将行 1 的上界设置为 4 来消除；但第 2 和第 3 列的零仍然存在。

我们可以通过将 A 分为下三角和上三角子矩阵并转置上三角矩阵来消除所有的零。我们将前者称为 L，后者称为 U（尽管它实际上是 U 的转置）。在这种分解下，所有主导零都位于行首，可以通过将 L 和 U 的第 $i$ 个组件的下界分别设置为 `row[i]` 和 `column[i]` 来消除。图 15 显示了这种分解。构建这两个数组的 Sisal 代码为：

```
L := for i in 1, n cross j in row[i], i
    returns array of A[i, j]
    end for;
U := for i in 1, n cross j in column[i], i
    returns array of A[j, i]
    end for;
```

这两个表达式都返回一个具有 $n$ 行的“二维”数组。每行的下界是内部范围的第一个值（`row[i]` 或 `column[i]`），上界是 $i$；因此，每行只存储非零元素。形成 U 时的转置是通过反转读取操作中的 $i$ 和 $j$ 实现的。

372

J. T. Feo

| 1 0 0 1 0 0 0 |
| 0 1 0 1 0 1 0 |
| 0 1 1 1 1 1 0 |
| 0 0 0 1 1 1 0 |
| 0 1 1 1 1 1 0 |
| 0 0 0 1 1 1 0 |
| 0 0 0 0 0 0 1 |

| 1 |
| 1 |
| 1 1 1 |
| 1 1 1 |
| 1 1 1 1 |
| 1 |
U |

| 1 |
| 1 1 |
| 1 |
| 1 1 1 |
| 1 1 1 |
| 1 |
L |

图 15 - 分解为 L 和 U的天际线矩阵

### 6.3. 基于 Sisal 分解的高效算法

在消除了位于天际线之外的所有零之后，我们现在必须开发一种高效算法接收 L、U 和 b 并返回 A_prime 和 b_prime。消除 A 的下三角需要我们处理 L 和 U 的列。由于 Sisal 数组是按行优先的，按列优先的算法更复杂且效率较低。相反，如果我们消除 A 的上三角，就可以处理 L 和 U 的行，这是一个要容易得多且更直接的命题。

接下来的初始表达式实现了第 6.1 节描述的迭代算法。

373

Sisal

```
A_prime, b_prime :=
  initial
    i := n;
    pivot_b := b[n];
    pivot_A := L[n];
    U1, bl1 := reduce(n, L, U, b)
  while i > 1 repeat
    i := i - 1;
    pivot_b := bl[i];
    pivot_A := L[i];
    U1, bl1 := reduce(i, L, U, b)
  returns array of pivot_A
  array of pivot_b
```

该表达式从 n 到 1 倒退执行。每次迭代从数组之前的值定义 L1、U1 和 bl1 的新值，并为 A_prime 和 b_prime 贡献一个元素。贡献的值是：L1[i]（第 $i$ 行主元）和 bl1[i]（b 的第 $i$ 个主元元素）。新手 Sisal 程序员常见的一个错误是一次一个元素地构建 A_prime 和 b_prime，并在迭代之间传递部分数组。使用 `array_add` 将每次迭代的贡献添加到部分数组中。

```
A_prime := array_add(old A_prime, A_pivot);
b_prime := array_add(old b_prime, b_pivot);
```

这增加了表达式的复杂性，并且必要。新手没有理解 Sisal 表达式作为执行的结果会返回值（包括数组）。他们继续以命令式的方式思考，同时描述了计算的“什么”和“如何”。

374

J. T. Feo

`reduce` 函数实现了方程 6.3.1 和 6.3.2。用 L 和 U 重写这些表达式，我们得到：

```
L_{j,k} = L_{j,k} - (L_{i,k} * U_{i,j} / L_{i,i}) (6.3.1)
U_{j,k} = U_{j,k} - (L_{i,k} * U_{i,j} / L_{i,i}) (6.3.2)
b_j = b_j - (L_{i,j} * b_i / L_{i,i}) (6.3.3)
```

在 $j < i$ 且 $1 \le k \le j$ 时，我们可以用 Sisal 写出这些方程：

```
L1 := for i in 1, n cross j in row[i], i
    returns array of A[i, j]
    end for;
U1 := for i in 1, n cross j in column[i], i
    returns array of A[j, i]
    end for;
bl1 := for i in 1, n cross j in row[i], i
    returns array of b[j]
    end for;
```

由于 L1, U1 和 bl1 比原始数组更小，它们是压缩的。新手 Sisal 程序员常见的一个错误是一次一个元素地构建 A_prime 和 b_prime，并在迭代之间传递部分数组。使用 `array_add` 将每次迭代的贡献添加到部分数组中。（此处由于原文存在重复逻辑，翻译已根据逻辑衔接）

385

Sisal

如果 L1[i,j] 缺失（即主元元素为零），方程 6.3.1 和 6.3.2 简化为：

```
L_{j,k} = L_{j,k}
b_j = b_j
```

在 $j < i$ 且 $1 \le k \le j$ 时，我们在 `function reduce` 中重写 L1、U 和 bl1。

一旦有了 A_prime 和 b_prime，我们就可以根据方程 6.4 求解 $x$。Sisal 代码非常直观，我们将其留给读者作为练习（解决方案见附录）。

## 7. 结论

在本章中，我们展示了针对四个天际线问题的 Sisal 解决方案。所有解决方案都是并行的，初步研究表明编译时分析 [1, 6] 可以消除不必要的复制和内存操作。我们预计这些解决方案在传统的多处理器系统上的执行速度与命令式解决方案一样。我们在三个案例中满足了问题要求。在旧案例“医生诊所”中，由于问题的非确定性，我们无法完全按照规范实现。考虑到无意外的非确定性在开发正确的并行程序时造成的巨大破坏，我们不对 Sisal 的确定性这一“缺陷”道歉。




# 致谢

我谨向 Skedzielielewski 表示感谢，他与我一起设计了用于在1988年萨利什大会上展示的Sisal解决方案。同时也感谢 Tom DeBoni 对章节进行校对并提出了众多改进演算法呈现方式的建议。

这项工作部分得到了美国能源部（U.S. Department of Energy）应用数学程序（Applied Mathematics Program）在合同第W-7405-Eng-48号下支持给劳伦斯·利弗莫尔国家实验室。

## 声明

本报告是根据经由美国政府资助而编写的一份账目文件。  
无论是**美国**还是其任何领域，**能源部**（**Department Of Energy**）或任何员工和承包商均不做出关于是否具有准确性、完整性、**有效性**、信息、仪器、产品、过程揭露及使用权等暗示保证或接受相关责任之声明；这些未被视为侵犯知识产权公司名称仅作概约认可提议状态 **exclusion**，观点将作为官方美军政策除非文件注明「指定」(designated) докуменум则为例外引出特意说明后采取专属立场但仍受到该规定限制—此处省略更详尽细则务请参考原始函令规范。




## 384
## J. T. Feo

```pascal
still_sick := array queue [];
patient_in := array queue [];
still_available := list_of_doctors;
doctor_out := array queue [];
still_examining := array queue2 [];
patient_doctor := array queue2 [];
while true repeat
    seed := next_seed(old seed)
    still_well, patient_in :=
        well_persons(old, still_well || old patient_out)
    still_sick, patient_doctor, still_available :=
        nurse(old, still_sick || old patient_in,
            old_still_available, patient_out, doctor_out)
    still_examining, patient_out, doctor_out :=
        examinations(seed, old_still_examining || old patient_doctor)
returns stream of patient_in
    stream of doctor_out
```

```pascal
end function % doctors_office
```

```pascal
************************************
/** 天际线问题 (Skyline Problem) **/
************************************
```

定义 skyline

```pascal
type OneDim = array[real];
type TwoDim = array[OneDim];
type IntDim = array[integer];
```

```pascal
function form_skyline(n: integer; row, column: IntDim; A: TwoDim
returns TwoDim, TwoDim
```

```pascal
for i in 1, n cross j in row[i], i
returns array of A[i, j]
end for,
```

```pascal
for i in 1, n cross j in column[i], i
returns array of A[j, i]
end for
```

```pascal
end function % form_skyline
```

```pascal
function reduce(i: integer; TwoDim; L1, U1; bl: OneDim
returns TwoDim, TwoDim, OneDim
```

```pascal
% reduce L1
for j in 1, i - returns array of
```

## 385
# Sisal

```pascal
if is error(U1[i, j]) then
    L1[j]
else
    for k in min(array_liml(L1[i]), array_liml(L1[j])), j
        returns array of
        if is error(L1[i, k]) then
            L1[j, k]
        elseif is error(L1[j, k]) then
            (L1[i, k] * U1[i, j]) / L1[i, i]
        else
            L1[j, k] - (L1[i, k] * U1[i, j]) / L1[i, i]
        end if
    end for
end for
end for,
```

```pascal
% reduce U1
for j in 1, i - 1 returns array of
    if is error(L1[i, j]) then
        U1[j]
    else
        for k in min(array_liml(U1[i]), array_liml(U1[j])), j
            returns array of
            if is error(U1[i, k]) then
                U1[j, k]
            elseif is error(U1[j, k]) then
                (L1[i, j] * U1[i, k]) / L1[i, i]
            else
                U1[j, k] - (L1[i, j] * U1[i, k]) / L1[i, i]
            end if
        end for
    end if
end for,
```

```pascal
% reduce b1
for j in 1, i - 1 returns array of
    if is error(U1[i, j]) then
        b1[j]
    else
        b1[j] - (b1[i] * U1[i, j]) / L1[i, i]
    end if
end for,
```

```pascal
function eliminate(n: integer; L, U: TwoDim; b: OneDim)
    returns TwoDim, OneDim

for initial
```

```pascal
i
    := n;
    pivot_b    := b[n];
```

## 386
## J. T. Feo

```pascal
pivot_A := L[n];
Li, U1, b1 := reduce(n, L, U, b)
while i > 1 repeat
    i := old i - 1;
    pivot_b := old bl[i];
    pivot_A := old L[i];
    L1, U1, b1 := reduce(i, old L1, old U1, old b1)
returns array of pivot_A
    array of pivot_b
```

```pascal
end for
```

```pascal
function % eliminate
```

```pascal
function backsolve(n: integer; A_prime: TwoDim; b_prime: OneDim
returns OneDim
```

```pascal
for initial
i := n;
j := 1;
A := A_prime;
b := b_prime;
x := b[n] / A[n, 1]
nwhile i > 1 repeat
    i := old i - 1;
    j := old j + 1;
    b := for k in 1, i
        b_k := if error(A_prime[k, old j]) then
            old b[k]
        else
            old b[k] - old x * A_prime[k, old j]
    end if
    returns array of b_k
end for;
x := b[i] / A[i, j]
returns array of x
```

```pascal
end for
```

```pascal
function % backsolve
```

```pascal
function skyline(n: integer; row, column: IntDim;
A: TwoDim; b: OneDim
returns OneDim
```

```pascal
let
L, U := form_skyline(n, row, column, A);
A_prime, b_prime := eliminate(n, L, U, b)
in
    backsolve(n, A_prime, b_prime)
end let
```

```pascal
end function % skyline
```

