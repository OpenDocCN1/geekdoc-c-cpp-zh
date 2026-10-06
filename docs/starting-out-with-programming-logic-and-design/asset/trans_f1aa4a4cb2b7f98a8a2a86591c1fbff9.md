

# 第 14 章：面向对象编程

本章比较了过程化编程和面向对象编程的实践。讨论了字段、方法、访问规范符、构造函数、访问器和变异器。学生将学习如何使用 UML 对类建模，以及如何在特定问题中寻找类。

# 第 15 章：GUI 应用与事件驱动编程

本章讨论了设计 GUI 应用的基本方面。讨论了如何使用视觉化工具（如 Visual Studio® 或 NetBeans™）构建图形用户界面。学生将学习如何在 GUI 应用中工作以及如何编写事件处理器。

# 附录 A：ASCII/Unicode 字符

本录列出了 ASCII 字符集，它与前 127 个 Unicode 字符编码相同。

# 附录 B：流程图符号

本录展示了书中使用的流程图符号。

# 附录 C：伪代码参考

本录为书中使用的伪代码语言提供了快速参考。

# 附录 D：十进制转二进制

本附录通过简单的教程演示了如何将十进制转换为二进制。

# 附录 E：检查点问题答案

本附录提供了书中出现的检查点（Checkpoint）问题的答案。

# 本书结构

本书以循序渐进的方式教授编程逻辑设计。每章涵盖一组主要主题，并随着学生阅读书籍不断构建知识。虽然章节可以按照现有顺序轻松教授，但具有一定的灵活性。P-1 显示了章节之间的依赖关系。每个框代表一个章节或一组章节。箭头指向的章节必须在箭头来源章节之前涵盖。虚线表示第 10 章的部分内容取决于第 8 章介绍的信息。

# 本书特点

概念陈述（Concept Statements）。书的每个主要章节都以一个概念陈述开头。该陈述简洁地总结了该节的核心观点。

![](img/c939132f78787c7f339c6977b3fc8c85_17_0.png)

示例程序。每章都有大量的完整和部分示例程序，旨在突出当前主题。示例程序使用了伪代码、流程图和其他设计工具。

**焦点关注（ Spotlight）。** 每章都有一个或多个“焦点关注”案例，对问题提供详细的逐步分析，并向学生展示如何解决问题。

**视频笔记（VideoNotes）。** 一系列专门为本书开发的在线视频可在 www.pearsonhigher.com/gaddis 观看。书中处处出现的图标提醒学生查看有关特定主题的视频。

> 注意（NOTE）：笔记出现在书中的多个地方。它们是对与当前主题相关的有趣或经常被误解的点的解释。

> 提示（TIP）：提示为学生提供处理不同编程或动画问题的最佳技术建议。

xviii 前言

> 警告！WARNING！警告学生注意可能导致程序故障或数据丢失的编程技术或实践。

**编程语言伙伴（Programming Language Companions）。** 书中许多伪代码程序也用 Java、Python 和 Visual Basic 编写。这些程序出现在可以在 www.pearsonhighered.com/gadis 获取的编程语言伴书中。在每个与语言伴书中同样出现的伪代码页面旁边都会出现相应的图标。

**检查点（Checkpoints）。** 检查点间隔分布在每章的各个部分。它们旨在学生在学习完新主题后快速查询其知识情况。

**复习题（Review Questions）。** 每章都提供了一套详尽且多样的复习题和练习。它们包括多选择、判断题、简答和算法工作站（Algorithm Workbench）。

**编程练习（Programming Exercises）。** 每章都提供一组编程练习，旨在巩固学生对当前所学主题的知识。

# 补充材料

# 学生在线资源

出版商为本书提供了许多学生资源。以下项目可以在 www.pearsonhighered.com/gadis 的 Gaddis 系列资源页面获取：

- 访问书籍的伴随视频笔记（VideoNotes）
  开发了一系列扩展的在线视频笔记以配合本书。在整书中，视频笔记提醒学生查看涵盖特定主题的视频。此外，每章末尾的一个编程练习都有附带的视频笔记，解释如何开发问题的解决方案。

- 访问 Python、Java、Visual Basic 和 C++ 的语言伴书
  专为配合本教材第四版设计的编程语言伴书供下载。伴书介绍了 Java™、Python*、Visual Basic 和 C++ 编程语言，并与教材逐章对应。书中许多伪代码程序也出现在伴侣书中，并用特定的编程语言实现。

- 下载 Flowalgorithm 流程图应用程序的链接
  Flowalgorithm 是由萨克拉门大学的 Devin Cook 开发的一款免费程序，允许你使用简单的流程图创建程序。它支持书中使用的流程图规范，以及其他几种标准规范。当你使用 Flowgorithm 创建流程图时，可以执行程序并生成 Gaddis 伪代码。你还可以生成 Java、Python、Ruby、JavaScript 以及其他几种语言的源代码。更多信息请参见 www.flowgorithm.org。

- 下载 RAPTOR 流程图环境的链接
  RAPTOR 是由美国空军学院计算机系开发的基于流程图的编程环境。

# 教师资源

以下补充材料仅供合格教师使用：

- 所有复习题的答案
- 编程练习的解
- 每章的 PowerPoint® 演示灯片
- 题库

访问 Pearson 教师中心 (http://www.pearsonhighered.com/irc) 或向 computing@aw.com 发送电子邮件获取如何访问的信息。

20

本页特留白

21

# 致谢

本书的开发和出版过程中有许多他者的帮助。我要感谢以下教职工评审员：

## 本版评审员

- Alan Anderson, Gwinnett Technical College
- Richard J. Davison, College of the Albemarle
- Sameer Dutta, Grambling State University
- Norman P. Hahn, Thomas Nelson Community College
- John Haley, Athens Technical College
- Dianne Hill, Jackson College
- J. Shawn Pope, Tulsa Community College
- Linda Reeser, Arizona Western College
- Homayoun Sharafi, Prince George's Community College
- Maryam Rahmnoonfar, Texas&M University
- Scott Vanselow, Edison State College

## 前版评审员

- Reni Abraham, Houston Community College
- Cherie Aukland, Thomas Nelson Community College
- Steve Browning, Freed Hardeman University

xxi

# 致谢

John P. Buerck, Saint Louis University
Jill Canine, Ivy Tech Community of Indiana
Steven D. Carver, Ivy Tech Community
Stephen Robert Cheskiewicz, Keystone College and Wilkes University
Katie Danko, Grand Rapids Community College
Ronald J. Harkins, Miami University, OH
Coronicca Oliver, Coastal Georgia Community College
Robert S. Overall, III, Nashville State Community College
Dale T. Pickett, Baker College of Clinton Township
Tonya Pierce, Ivy Tech Community
Larry Strain, Ivy Tech Community–Bloomington
Donald Stroup, Ivy Tech Community
John Thacher, Gwinnett Technical College
Jim Turney, Austin Community College
Scott Vanselow, Edison State College

我还要感谢 Pearson 的所有人，让 Starting Out With . . . 系列取得成功。我与 Pearson 团队密切合作，以至于我视他们为最好的朋友。我非常幸运有 Matt Goldstein 作为我的编辑，Kelsey Loanes 作为编辑助理。他们指导我修订这本书以及许多其他书。我非常幸运有 Demetrius Hall 和 Bram Van Kempen 担任营销经理。他们的努力非常鼓舞人心，并很好地将我的书推广到学术界。制作团队为了这本书的诞生付出了巨大的努力。感谢大家！

