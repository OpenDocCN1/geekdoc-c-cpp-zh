

# 致谢

本书的出版，如果没有许多参加过我们课程的 MIT 学生的帮助是不可能的。他们实际上解决了书中的问题，并经常告诉我们我们所做的错误选择以及做错的事情！我们特别感谢那些担任助教的学生。Michael Blair, Alexey Radul, Pavel Panchekha, Robert L. McIntyre, Lars E. Johnson, Eli Davis, Micah Brodsky, Manushaqe Muco, Kenny Chen 和 Leilani Hendrina Gilpin 对我们提供了特别帮助。

这里介绍的许多想法都是在朋友和前学生的帮助下开发的。Richard Stallman, Jon Doyle, David McAllister, Ramin Zabih, Johan DeKler, Ken Forbus 和 Jeff Siskind 都对我们对依赖回溯（dependency-directed backtracking）的理解做出了贡献。而我们在第 7 章对传播（propagation）的理解，是与 Richard Stallman、Guy Lewis Steele Jr. 以及 Alex Radul 多年合作的结果。

特别感谢函数式编程社区的帮助和支持，特别是 Scheme Team。Guy Steele 在 20 世纪 70 年代与 Gerald Jay Sussman 共同创立了 Scheme，他几乎每年都会来我们的课程进行客座演讲。Arthur Gleckler, Guillermo Juan Rojas, Jose Marshall, James S. Miller 和 Henry Manyan Wu 对 MIT/GNU Scheme 的开发起了至关重要的作用。Taylor Campbell 和 Matt Birkholz 对这个古老的系统做出了重大贡献。我们还要感谢 Will Byrd 和 Michael Ballantyne 在帮助理解带分段变量（segment variables）的统一方面的协助。

Hal Abelson 和 Julie Sussman 与 Gerald Jay Sussman 合著了《计算机程序的构造与实现》（SICP），他们帮助我们形成了本书的理念。在许多方面，本书是 SICP 的高级续作。Dan Friedman 以及他那些优秀的学生和朋友对我们对编程的理解做出了深远贡献。我们与一些伟大的大师（如 William Kahan、Richard Stallman、Richard Greenblatt、Bill Gosper 和 Tom Knight）进行了许多关于编程艺术的对话。与 Jack Wisdom 合作多年数学动力学，有助于澄清我们在书中讨论的许多问题。

Sussman 特别感谢他的老师们的贡献：他与 Marvin Minsky、Seymour Paper、Jerome Lettvin、Joel Moses、Paul Penfield 和 Edward Fredkin 讨论的想法显著出现在书中。与 Minsky 和 Paper 同时代的 Carl Hewitt、David Waltz 和 Patrick Winston 的想法也收录在此。Jeff Siskind 和 Alexey Radul 指出并帮助消除了一些非常细微的错误。

Chris 在 Google 以及后来的 Datera 工作期间学习了大量大规模编程知识；这段经历影响了本书的部分。Arthur Gleckler 在每两周一次的午餐中对本书提供了有用的反馈。在 Google 的定期会议上，Mike Salisbury 总是对听到最新进展感到兴奋。黄洪涛（Hongtao Huang）和 Piyush Janwar 读了书的初稿。特别感谢 Rick Dukes，这位 MIT 的同学向 Chris 引入了 lambda 相关的论文，并让他开启了通往本书的漫漫道路。

我们感谢 MIT 电子工程与计算机科学系（Department of Electrical Engineering and Computer Science）以及 MIT 计算机科学与人工智能实验室（CSAIL）提供的款待和后勤支持。我们感谢松下电器公司（原松下电气工业公司）通过设立教授职位对 Gerald Jay Sussman 提供的支持。Chris 的这项工作也得到了 CSAIL 以及后期 Google 的部分支持。

Julie Sussman, PPA 提供了严谨的评审和严肃的批评，这迫使我们重新组织并重写了文本的大部分。多年来，她一直培养并维护着 Gerald Jay Sussman。

Elizabeth Vickers 作为多年的伴侣，为 Chris 和他们的孩子 Alan 和 Erica 提供了一个支持且稳定的环境。在缅因州漫长的工作期间，Elizabeth 还为两位作者准备了许多美味的饭菜。Alan 偶尔是初稿的充满热情的读者。

# 1

## 自然与设计中的灵活性

设计一种能够很好胜任任何特定任务的通用型机制是困难的，因此大多数工程系统都是为了执行特定任务设计的。通用型发明（如螺丝紧固件）非常罕见且具有重大意义。数字计算机就是这类突破，因为它是一个可以模拟任何其他信息处理机器的通用机器.¹¹ 我们编写软件来配置计算机，以便为所需的特定任务实现这种模拟。

作为过去工程实践的延伸，我们设计了能够很好完成特定任务的软件。每个软件的设计是为了完成一个相对狭的任务。当要解决的问题改变时，软件必须随之改变。但问题的微小变化往往并不只导致软件的微小变化。软件的设计过于紧凑，缺乏灵活性。结果就是系统无法优雅地演进。它们是脆弱的，当问题领域变化时，必须用全新的设计来替换²。这是既缓慢又昂贵的。

我们的工程系统不必是脆弱的。互联网已经从小系统扩展到了全球规模。我们的城市有机地演进，以适应新的业务模式、生活方式以及交通和通信手段。事实上，通过对生物系统的观察，我们可以构建能够适应环境变化的系统，无论是作为个体还是作为一个演化整体。为什么我们不这样设计和构建大多数软件呢？这有历史原因，但主原因是我们不知道如何通用地做到这一点。

目前，如果一个系统在面对需求变化时表现出健壮性，那是一种意外。

# 加法性编程（Additive programming）

本书的目标是研究如何构建计算系统，使其能够轻松适应变化的需求。人们不应该修改一个正在运行的程序。人们应该能够对其添加内容来实现新功能，或根据新需求调整旧函数。我们把这称为**加法性编程**（additive programming）。我们探索了在不破坏现有程序的情况下向其添加功能的技术。我们的技术并不能保证添加的内容是正确的：添加的内容本身需要经过调试；但它们不应该损害现有功能。

我们在书中探索的许多技术并非新颖；其中一些可以追溯到计算的早期！它们也不是一套完整的方案，而是我们发现实用的工具。我们的意图并不是推广这些技术的使用，而是鼓励一种关注灵活性的思维方式。

为了使加法性编程成为可能，必须尽量减少程序如何工作以及如何被使用的假设。在程序的设计和构建过程中所做的假设可能会减少程序未来的扩展空间。与其做此类假设，而是让程序根据运行的环境做出即时决策。我们将探索几种支持这种设计的技巧。

我们总是可以组合程序以获得每个程序所支持的行为并集。但我们希望整体大于部分之和；我们希望组合系统的部分能够相互协作，为系统提供任何部分都无法提供的能力。但这里存在权衡：我们组合以构建系统的部分必须严格分离关注点。如果一个部分在某方面做得非常好，它比结合了几个不同能力的部件更容易重用，也更容易调试。如果我们想以加法的方式进行构建，确保各个组件组合时产生的意外相互作用最少是关重要的。

