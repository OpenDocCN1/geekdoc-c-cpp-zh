

# 20

# 操作系统原理

# 参考文献

- [BS+09] "Tolerating File-System Mistakes with EnvyFS"由 L. Balairasundaram, S. Sundararaman, A. Apaci-Dusseau, R. Apaci-Dusseau 著。USENIX ’09, 加利福尼亚州圣地亚哥，2009年6月。关于同时使用文件系统来容忍其中一个错误的有趣论文。

- [BH100] "Computer Operating Systems"由 P. Brinch Hansen 著。『经典操作系统：从处理到分布式系统。』Springer-Verlag, 纽约，2000年。这篇文章为了一系列关于操作系统的精彩论文集提供了介绍。

- [B2+72] "A Paged Time Sharing System for the PDP-10"由 D. Dobson, J. Burchfield, D. Murphy, R. Tomlinson 著。CACM, 第15 卷，第3 期，1972年3月。TENEX 包含了现代操作系统中的许多机制；阅读它就可以看到 20 世纪 70 年代初已经有了多少创新。

- [B75] "The Mythical Man-Month"由 F. Brooks 著。Addison-Wesley, 1975年。软件工程的经典教材，非常值得一。

- [BH011] "Computer: A Programmer's Perspective"由 R. Bryant 和 D. O'Hallen 著。Addison-Wesley, 2010年。另一本关于计算机系统如何工作的极佳介绍。它与本书有些重叠——如果你喜欢它，可以跳过它的前几章，或者简单地阅读它们以获得某些材料的不同视角。毕竟，建立自己知识的良好方法之一是从许多角度听取意见，然后你对该问题形成自己的想法。你知道的，通过思考！

- [GS85] *The Mechanics of Unix*由 P. Maurice 著，1985年。www.gnu.org/gnu/manifesto.html。Linux 的成功无疑归于卓越的编译器 `gcc`、`acc` 以及其他免费软件的存在，虽然这书可能不是最好的读物。GNU 的 Stallman 在开源方面是一个远见者，这篇宣言阐述了他的希望和转折。

- [K+61] "One-Level Storage System"由 T. Killburn, B.D.G. Edwards, M. Ligan, F.H. Summer 著。IRE Transactions on Electronic Computers，1962年4月。Atlas 展示了你在现代系统中看到的许多内容。然而，如果只读一次，你需要阅读 [78] 的历史视角。

- [M78] "The Manchester Atlas: A Historical Perspective"由 S. H. Livingston 著。Communications of the ACM, 第21 卷:1，1978年1月。关于计算机系统早期发展和 Atlas 先驱性工作的一段精彩历史。当然，人们可以回去阅读 [78] 的论文，但这篇论文提供了良好的概述和历史视角。

- [O72] "The Multics System: An Examination"由 Elliott 著。MIT Press, 1972年。对许多优秀想法的极佳概述，它是一个过度设计的系统，追求触，而这实际上非常需要。Fred Brooks 的经典著作称之为“二要效应”（1973年）。

- [P03] "Introduction to Computing Systems: From Gates to C and Beyond"由 Yale N. Patt, Sananjay J. Patel 著。McGraw-Hill, 2003年。我们最喜欢的计算系统介绍书籍之一。从门电路开始，当你接触 C 语言时结束：材料其实非常简单。

- [RT74] "The Unix-Time Sharing System"由 Dennis M. Ritchie, Kevin Thompson 著。AC AC, 第17 卷:6，1974年7月。关于 Unix 分时系统的概论。

- [S68] "Time-Sharing System"由 Scientific Data 著。TECHNICAL MANUAL, 1968年8月。关于分时系统的技术手册，SDS 940 系统，1968年。

- [SS10] "Reliable Operating Systems"由 Balairasundaram, Sundararaman, Apaci-Dusseau, Apaci-Dusseau 著。圣地亚哥，加利福尼亚州，2010年2月。关于可靠操作系统的研究。

操作系统原理 版本1.0

# 操作系统原理

# 引言

# 参考文献

大部分我们最喜欢的计算系统介绍书籍之一。从门电路开始，当你接触 C 语言时结束：材料其实非常简单。

引言

# 引言

# 引言

大部分我们最喜欢的计算系统介绍书籍之一。从门电路开始，当你接触 C 语言时结束：材料其实非常简单。

引言

# 引言

# 引言

大部分我们最喜欢的计算系统介绍书籍之一。从门电路开始，当你接触 C 语言时结束：材料其实非常简单。为了完成这些作业，我们强烈建议你巩固你的技能。请查看此页面 (github.com/remzi-arpusseau/ostep-projects) 获取一些项目。为了完成这些作业，你可能需要一台基于 Unix 的机器，运行 Linux 或 macOS。它应该有一个 C 编译器（例如 gcc）以及 Python。你还应该学会用编辑器编写代码。

第一部分
## 虚拟化

### 关于虚拟化的对话

**教授：** 因此我们进入了操作系统的三个部分之一：**虚拟化**。

**学生：** *但是什么是虚拟化，尊敬的教授？*

**教授：** *想象我们有一个苹果。*

**学生：** *一个苹果？（怀疑地）*

**教授：** 是的，让我们把苹果称为*物理*苹果。但我们有许多想吃这个苹果的人。我们希望给每个人提供他们自己的苹果，这样他们就能开心。我们将创建的苹果称为**虚拟苹果**；我们通过某种方式从物理苹果创建许多虚拟苹果。重要的是：在这种幻象中，每个人看起来都拥有一个物理苹果，但实际上并没有。

**学生：** 所以你们在共享苹果，但你甚至并不知道？

**教授：** 正确！

**学生：** 嗯，如果我和别人共享苹果，我想我会注意到的。

**教授：** 噢！很好！但很多吃者的特点在于；他们大多数时间都在睡觉或做其他事情，因此，我们可以把苹果夺走，给别人用一会儿。我们我们创造了许多虚拟苹果的幻象，每个人一个苹果！

**学生：** 听起来像是个糟糕的竞选口号。你是在说计算机，对吧教授？

**教授：** 噢，年轻的弟子，你想一个更具体的例子。好主意！让我们来看看最基础的资源，CPU。假设系统中有一个物理 CPU（尽管通常有二、四或更多）。虚拟化所做的是将这一个 CPU 让运行系统上的应用程序看起来像许多虚拟 CPU。因此，虽然每个应用程序

