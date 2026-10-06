

## 关于本书

## 编写目的

本书将教你如何访问 Medicare（美国医疗保险）数据，更重要的是，如何将这些数据应用于你的研究中。了解如何使用 Medicare 数据来回答常见的研究和业务问题，是许多 SAS 用户的一项关键技能。由于其复杂性，Medicare 数据需要特定的编程知识才能被准确应用。编程人员需要理解 Medicare 计划，以便正确地解释和使用其数据。通过这本书，你将学习使用 Medicare 数据进行编程的整个过程——从获取数据访问到衡量成本、利用率和质量，再到克服常见挑战。每一章都包含练习，挑战你将所学的概念应用于真实世界的编程任务。

## 这本书适合你吗？

对于任何感兴趣在 SAS 中进行 Medicare 数据编程的人来说，这本书都是必读的。这包括学生、专业研究人员以及联邦和州政府的员工。《Medicare 行政数据 SAS 编程》（SAS Programming with Medicare Administrative Data）为初学者提供了一个从头到尾可以遵循的编程模板。它包含了适合高级用户的复杂问题和讨论。

## 先决条件

本书没有先决条件，适用于所有水平的 SAS 用户，以及对 Medicare 计划和 Medicare 数据具有不同知识水平的读者。具有 SAS 经验但没有医疗或 Medicare 数据背景的读者可以更多关注第 1 章至第 5 章。在这些章节中，我们学习 Medicare 计划、该计划如何驱动数据内容，以及 Medicare 行政索赔和注册数据的获取。了解 Medicare 计划但不熟悉 Medicare 数据或 SAS 的读者可以更多关注第 3 章（我们在该章讨论了 Medicare 数据）以及第 6 章至第 10 章（我们在那里开发了大部分 SAS 代码）。

## 本书范围

Medicare 计划涵盖的主要主题包括：

- Medicare 计划简介；
- Medicare 数据的详细介绍；
- 关于如何规划研究编程计划的讨论；
- 获取 Medicare 数据的方法；
- 使用 Medicare 数据进行编程以衡量利用率、成本和质量的说明；
- 如何展示研究结果的演示；
- 关于如何结束研究编程项目的有用解释。

由于本书是基础性的，因此它不涵盖更复杂的处理或分析，例如风险调整或支付标准化算法。然而，它为读者提供了充足的背景信息，以独立处理这些主题。

## 关于示例

### 用于开发本书内容的软件

SAS 9.3

## 示例代码与数据

你可以通过链接到其作者页面 http://support.sas.com/publishing/authors/gillingham.html 来访问本书的示例代码和数据。所有提供示例代码和数据的书籍字母列表，请参阅 http://support.sas.com/bookcode。选择标题显示书籍的代码示例。

如果你无法通过网站访问代码，请发送电子邮件至 saspress@sas.com。

## 本书中使用的输出和图形

本书中的输出是使用 ODS 生成的。

## 练习答案

你可以通过链接到作者页面 http://support.sas.com/publishing/authors/gillingham.html 访问本书的练习答案。

## 保持联系

我们期待收到你的反馈。我们欢迎提问、意见和疑虑。如果你想就特定书籍与我们联系，请在给 saspress@sas.com 的信函中包含书名。

## 通过 SAS Press 联系作者

通过电子邮件：saspress@sas.com

通过网络：http://support.sas.com/author_feedback

## SAS 书籍

欲查看通过 SAS 提供的完整书籍列表，请访问 http://support.sas.com/bookstore。

电话：1-800-727-3228

传真：1-919-677-8166

电子邮件：sasbook@sas.com

## SAS 书籍报告

通过订阅 SAS Book Report 每月电子 {，通过电子邮件接收所有新 SAS 出版物的最新信息。访问 http://support.sas.com/sbr。

## 与 SAS 出版

SAS 正在招聘作者！你有兴趣写书吗？访问 http://support.sas.com/saspress 了解更多信息。

## 关于作者

Matthew Gillingham 是 Mathematica Policy Research 的健康研究系统总监。他的健康分析职业生涯始于 Mathematica。十多年来，他一直指导健康研究系统。通过访问他的页面 http://support.sas.com/publishing/authors/gillingham.html 了解更多关于这位作者的信息。

## 致谢

写这本书感觉更像是一种生活方式，而不是一个项目。我要感谢我在 Mathematica 的评审员：Sandy Nelson, Jeffrey Holt, Scott McCracken 和 Ken Peckham，他们让这本书比我最初的构想好得多。此外，我非常感谢 Scott Green, Patrick Wang, Ken Peckham，他们协助我创建数据，并感谢 Susie Clausen 在格式化我的材料方面做的出色工作。Mathematica 的传播部门在书籍的制作和设计中发挥了创意力量。我要感谢 SAS Publishing 的编辑 John West，感谢他的耐心和指导。重要的是，我还要感谢本书的技术评审员 Gerri Barosso, Russ Tyndall, John Shipway, Bernadette Johnston, Craig Dickstein 和 Deidra Peacock，感谢他们对我的手稿进行了详尽且周到的评审。

我的主管 Edward Coke 提供了性的指导和鼓励。无法想象他对我的生活产生了多大的影响。Mathematica 的高级领导层 D. Myles Maxwellfield, Craig Horton, Adam Coyne, Pam Tapscott, Tamara Barnes, Andrew Darling, Patricia Gurof 和 Mary Harrington 不仅提供了鼓励，还提供了有用的指导。最后，我在 Mathematica 安安办公室的同事（Dean Miller, Ken Peckham, Kelly Zidar, Kevin Brayden, Gregory Bee, Rachel Thompson, Gerry Skurski, Anne Harlow 和 Nate Darter）以及 Justin Oh 等同事提供了鼓励、支持和指导。

朋友和家人支持我并帮助我完成了项目。我的父母和姐姐教会我相信自己并远大。Anne 和 Lucy 为我提供了一个安全、充满爱且滋养的环境，以便在漫长的工作周后休息放松。特别是 Anne，她从没有让我忘记我可以完成这个项目。最后，我的好朋友 Thieme 不仅提供了鼓励，还教了我许多关于 SAS 的知识（尽管任何错误都是我的！）。他将是我认识的最熟练、最酷的 SAS 程序员。

