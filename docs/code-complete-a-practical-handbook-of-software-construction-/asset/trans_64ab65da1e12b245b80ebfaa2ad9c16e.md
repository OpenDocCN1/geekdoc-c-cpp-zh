

*IEEE Std 830-1998. IEEE Recommended Practice for Software Requirements Specifications.* Los Alamitos, CA: IEEE Computer Society Press. 本文是 IEEE-ANSI 编写软件需求规格说明书的指南。它描述了规格说明书中应包含的内容，并展示了几种备选大纲。

Abram, Alain, et al. *Swebok: Guide to the Software Engineering Body of Knowledge.* Los Alamitos, CA: IEEE Computer Society Press, 2001. 本文对软件需求知识体系进行了详细描述。也可从 *www.swebok.org* 下载。

其他不错的替代书籍包括以下：

Lauesen, Soren. *Software Requirements: Styles and Techniques.* Boston, MA: Addison-Wesley, 2002.

Kovitz, Benjamin L. *Practical Software Requirements: A Manual of Content and Style.* Manning Publications Company, 1998.

Cockburn, Alistair. *Writing Effective Use Cases.* Boston, MA: Addison-Wesley, 2000.

## Software Architecture

过去几年出版了大量关于软件架构的书籍。以下是其中最好的一些：

Bass, Len, Paul Clements, and Rick Kazman. *Software Architecture in Practice*, 2d ed. Boston, MA: Addison-Wesley, 2003.

Buschman, Frank, et al. *Pattern-Oriented Software Architecture, Volume 1: A System of Patterns.* New York, NY: John Wiley & Sons, 1996.

Clements, Paul, ed. *Documenting Software Architectures: Views and Beyond.* Boston, MA: Addison-Wesley, 2003.

Clements, Paul, Rick Kazman, and Mark Klein. *Evaluating Software Architectures: Methods and Case Studies.* Boston, MA: Addison-Wesley, 2002.

Fowler, Martin. *Patterns of Enterprise Application Architecture.* Boston, MA: Addison-Wesley, 2002.

Jacobson, Ivar, Grady Booch, and James Rumbaugh. *The Unified Software Development Process.* Reading, MA: Addison-Wesley, 1999.

*IEEE Std 1471-2000. Recommended Practice for Architectural Description of Software-Intensive Systems.* Los Alamitos, CA: IEEE Computer Society Press. 本文是 IEEE-ANSI 创建软件架构规格说明书的指南。

揭示章节：“A Typical Day using PSP/TSP,” “A Typical Day using Extreme Programming,” “A Crisis Day using PSP/TSP,” 和 “A Crisis Day using Extreme Programming。” 第 5 章论述如何利用风险平衡敏捷性，提供了在敏捷方法和计划驱动方法之间选择的精辟指导。第 6 章“Conclusions”也十分平衡，并提供了极佳的视角。附录 E 是关于敏捷实践的经验数据的宝库。

Larman, Craig. *Agile and Iterative Development: A Manager’s Guide*. Boston, MA: Addison Wesley, 2004. 这是一本关于灵活、演进式开发风格的深入研究入门。它概述了 Scrum、极限编程、统一过程和 Evo。

## Checklist: Upstream Prerequisites

- Have you identified the kind of software project you’re working on and tailored your approach appropriately?
- Are the requirements sufficiently well defined and stable enough to begin construction? (See the requirements checklist for details.)
- Is the architecture sufficiently well defined to begin construction? (See the architecture checklist for details.)
- Have other risks unique to your particular project been addressed, such that construction is not exposed to more risk than necessary?

## Key Points

- The overarching goal of preparing for construction is risk reduction. Be sure your preparation activities are reducing risks, not increasing them.
- If you want to develop high-quality software, attention to quality must be part of the software-development process from the beginning to the end. Attention to quality at the beginning has a greater influence on product quality than attention at the end.
- Part of a programmer’s job is to educate bosses and coworkers about the software-development process, including the importance of adequate preparation before programming begins.
- The kind of project you’re working on significantly affects construction prerequisites—many projects should be highly iterative, and some should be more sequential.
- If a good problem definition hasn’t been specified, you might be solving the wrong problem during construction.
- If good requirements work hasn’t been done, you might have missed important details of the problem. Requirements changes cost 20 to 100 times as much in the stages following construction as they do earlier, so be sure the requirements are right before you start programming.
- If a good architectural design hasn’t been done, you might be solving the right problem the wrong way during construction. The cost of architectural changes increases as more code is written for the wrong architecture, so be sure the architecture is right, too.
- Understand what approach has been taken to the construction prerequisites on your project, and choose your construction approach accordingly.

## Chapter 4

## Key Construction Decisions

### Contents

- 4.1 Choice of Programming Language: page 61
- 4.2 Programming Conventions: page 66
- 4.3 Your Location on the Technology Wave: page 66
- 4.4 Selection of Major Construction Practices: page 69

### Related Topics

- Upstream prerequisites: Chapter 3
- Determine the kind of software you’re working on: Section 3.2
- How program size affects construction: Chapter 27
- Managing construction: Chapter 28
- Software design: Chapter 5, and Chapters 6 through 9

一旦你确信为建设奠定了适当的基础，准备工作就会转向更具体的建设决策。第 3 章“Measure Twice, Cut Once: Upstream Prerequisites”讨论了蓝图和施工许可的软件等价物。你可能对这些准备工作没有太多控制权，因此该章的重点是评估建设开始时你所拥有的资源。本章重点关注个人程序员和技术负责人直接或间接负责的准备工作。它讨论了软件等价物，即如何为你的工具带选择特定工具，以及在前往工地之前如何装载卡车。

如果你觉得已经读够了关于建设准备的内容，可以跳到第 5 章“Design in Construction”。

### 4.1 Choice of Programming Language

> By relieving the brain of all unnecessary work, a good notation sets it free to concentrate on more advanced problems, and in effect increases the mental power of the race. Before the introduction of the Arabic notation, multiplication was difficult, and the division even of integers called into play the highest mathematical faculties. Probably nothing in the modern world would have more astonished a Greek mathematician than to learn that ... a huge proportion of the population
> 
> *of Western Europe could perform the operation of division for the largest numbers. This fact would have seemed to him a sheer impossibility.... Our modern power of easy reckoning with decimal fractions is the almost miraculous result of the gradual discovery of a perfect notation.*
> 
> –Alfred North Whitehead

系统将要实现的编程语言应该引起你的极大兴趣，因为你将从建设开始到结束都沉浸其中。

研究表明，编程语言的选择以多种方式影响生产率和代码质量。

程序员使用熟悉的语言比使用不熟悉的语言更有效率。来自 Cocomo II 估算模型的数据显示，使用过三年或更长时间的语言的程序员比具有同等经验但对语言不熟悉的程序员生产率高约 30%（Boehm et al. 2000）。IBM 的一项早期研究发现，对编程语言有丰富经验的程序员生产率超过经验最少者的三倍以上（Walston and Felix 1977）。（Cocomo II 更谨慎地分离了单个因素的影响，这解释了两项研究结果的不同。）

![](img/649c8eee28c38ca1e062691e45dc9883_98_0.png)

使用高级语言的程序员比使用低级语言的程序员实现更好的生产率和质量。诸如 C++、Java、Smalltalk 和 Visual Basic 等语言被认为将生产率、可靠性、简洁性和可理解性提高了 5 到 15 倍，相比之下低级语言如汇编和 C（Brooks 1987, Jones 1998, Boehm 2000）。当你不必每次 C 语句按预期工作时都举行颁奖典礼时，你就能节省时间。此外，高级语言比低级语言更具表达力。每行代码所表达的内容更多。表 4-1 显示了几种高级语言的源代码语句与等效 C 代码的典型比率。比率越高，表示所列语言中的每一行代码完成的工作就比 C 中的每一行代码更多。

## Table 4-1 Ratio of High-Level-Language Statements to Equivalent C Code

| Language | Level Relative to C |
|---|---|
| C | 1 |
| C++ | 2.5 |
| Fortran 95 | 2 |
| Java | 2.5 |
| Perl | 6 |
| Python | 6 |
| Smalltalk | 6 |
| Microsoft Visual Basic | 4.5 |
| Source: Adapted from *Estimating Software Costs* (Jones 1998), *Software Cost Estimation with Cocomo II* (Boehm 2000), and “An Empirical Comparison of Seven Programming Languages” (Prechelt 2000). |

