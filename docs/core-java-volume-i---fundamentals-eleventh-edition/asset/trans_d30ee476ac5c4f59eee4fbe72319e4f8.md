
## 致谢

写一本书始终是一项艰巨的工作，而重写这本书似乎也并不轻松多少，尤其是在 Java 技术不断变化的情况下。让一本书成为现实需要许多敬业的人，我非常高兴地感谢整个 Core Java 团队所作出的贡献。

Pearson 的许多人提供了宝贵的帮助，却甘居幕后。我想让他们都知道我非常感激他们的努力。一如既往，我衷心感谢我的编辑 Greg Doench，感谢他引导本书完成写作和制作过程，并让我得以幸福地对所有幕后人员的存在一无所知。我非常感谢 Julie Nahil 提供制作支持，感谢 Dmitry Kirsanov 和 Alina Kirsanova 对稿件进行文字编辑和排版。我还要感谢早期版本的合著者 Gary Cornell，他后来已转向其他事业。

感谢早期版本的许多读者，他们报告了令人尴尬的错误，并提出了许多深思熟虑的改进建议。我尤其感谢优秀的审阅团队，他们以惊人的细致审阅了稿件，使我避免了许多令人尴尬的错误。

本书及早期版本的审阅者包括：Chuck Allison（犹他谷大学）、Lance Andersen（甲骨文）、Paul Anderson（Anderson Software Group）、Alec Beaton（IBM）、Cliff Berg、Andrew Binstock（甲骨文）、Joshua Bloch、David Brown、Corky Cartwright、Frank Cohen（PushToTest）、Chris Crane（devXsolution）、Nicholas J. De Lillo 博士（曼哈顿学院）、Rakesh Dhoopar（甲骨文）、David Geary（Clarity Training）、Jim Gish（甲骨文）、Brian Goetz（甲骨文）、Angela Gordon、Dan Gordon（Electric Cloud）、Rob Gordon、John Gray（哈特福德大学）、Cameron Gregory（olabs.com）、Marty Hall（coreservlets.com, Inc.）、Vincent Hardy（Adobe Systems）、Dan Harkey（圣何塞州立大学）、William Higgins（IBM）、Vladimir Ivanovic（PointBase）、Jerry Jackson（CA Technologies）、Tim Kimmet（沃尔玛）、Chris Laffra、Charlie Lai（苹果）、Angelika Langer、Doug Langston、Hang Lau（麦吉尔大学）、Mark Lawrence、Doug Lea（纽约州立大学奥斯威戈分校）、Gregory Longshore、Bob Lynch（Lynch Associates）、Philip Milne（顾问）、Mark Morrissey（俄勒冈研究生院）、Mahesh Neelakanta（佛罗里达大西洋大学）、Hao Pham、Paul Philion、Blake Ragsdell、Stuart Reges（亚利桑那大学）、Simon Ritter（Azul Systems）、Rich Rosen（Interactive Data Corporation）、Peter Sanders（法国尼斯 ESSI 大学）、Paul Sanghera 博士（圣何塞州立大学和布鲁克斯学院）、Paul Sevinc（Teamp AG）、Devang Shah（Sun Microsystems）、Yoshiki Shibata、Bradley A. Smith、Steven Stelting（甲骨文）、Christopher Taylor、Luke Taylor（Valtech）、George Thiruvathukal、Kim Topley（StreamingEdge）、Janet Traub、Paul Tyma（顾问）、Peter van der Linden、Christian Ullenboom、Burt Walsh、Dan Xu（甲骨文）和 John Zavgren（甲骨文）。

*Cay Horstmann*
*加利福尼亚州旧金山*
*2018 年 6 月*

## 第 1 章：Java 简介

### 本章内容

- 1.1 Java 作为编程平台，第 1 页
- 1.2 Java“白皮书”中的流行术语，第 2 页
- 1.3 Java Applet 与互联网，第 9 页
- 1.4 Java 简史，第 10 页
- 1.5 关于 Java 的常见误解，第 13 页

1996 年 Java 的首次发布引起了极大的轰动，不仅是在计算机媒体上，也出现在 *纽约时报*、*华盛顿邮报* 和 *商业周刊* 等主流媒体上。Java 享有殊荣，成为第一种也是唯一一种在全国公共广播电台有十分钟专题报道的编程语言。曾有一笔 1 亿美元的创业投资基金专门用于支持使用*特定*计算机语言的产品。希望你会喜欢本章中 Java 的简史。

### 1.1 Java 作为编程平台

在本书第一版中，我和合著者 Gary Cornell 曾这样写 Java：

> “作为计算机语言，Java 的炒作有些过头：Java 当然是一门*好*编程语言。毫无疑问，对于严肃的程序员来说，它是可用的较好语言之一。我们认为它*本有可能*成为一门伟大的编程语言，但可能为时已晚。一门语言一旦投入实际使用，与现有代码兼容的丑陋现实就会随之而来。”

我们的编辑因为这段话，遭到了最初开发 Java 的 Sun Microsystems 公司某位高层人士的严厉批评。Java 语言有许多优良特性，我们将在本章后面详细探讨。它也有自己的瑕疵，而且由于兼容性要求，语言中一些较新的增补并不如原有特性那样优雅。

但是，正如我们在第一版中已经说过的，Java 从来就不只是一门语言。市面上有许多编程语言，但很少能引起很大反响。Java 是一个完整的平台，拥有庞大的库（其中包含大量可复用代码）以及一个执行环境，提供安全性、跨操作系统可移植性和自动垃圾回收等服务。

作为一名程序员，你会想要一门语法令人愉快、语义易于理解的语言（即，不是 C++）。Java 符合要求，其他几十种优秀语言也同样符合。有些语言提供了可移植性、垃圾回收等特性，但库不够丰富，如果你想实现图形、网络或数据库访问，就只能自己动手。而 Java 拥有一切——良好的语言、高质量的执行环境和庞大的库。正是这种组合，使 Java 成为对众多程序员难以抗拒的选择。

### 1.2 Java“白皮书”中的流行术语

Java 的作者们撰写了一份颇具影响力的白皮书，阐述了他们的设计目标和成果。他们还发布了一份较短的概述，按照以下 11 个流行术语组织：

1. 简单
2. 面向对象
3. 分布式
4. 健壮
5. 安全
6. 体系结构中立
7. 可移植
8. 解释型
9. 高性能
10. 多线程
11. 动态

在接下来的各小节中，你将看到一份摘要，其中包含白皮书摘录，说明 Java 设计者对每个流行术语的看法，以及基于我对当前 Java 版本的经验所作的评论。

![](img/127bccebb2cfadea3f02579edaad63c3_29_0.png)

**注意：** 白皮书可在 `www.oracle.com/technetwork/java/langenv-140151.html` 找到。你可以在 `http://horstmann.com/corejava/java-an-overview/7Goals.pdf` 获取包含这 11 个流行术语的概述。

### 1.2.1 简单

> 我们希望构建一个能够轻松编程的系统，无需大量深奥的训练，并且能利用当今的标准实践。因此，尽管我们发现 C++ 并不合适，我们还是尽可能让 Java 贴近 C++ 来设计，以使系统更易于理解。Java 省略了 C++ 中许多很少使用、不易理解且令人困惑的特性；根据我们的经验，这些特性带来的烦恼多于好处。

Java 的语法确实是 C++ 语法的清理版本。不需要头文件、指针运算（甚至不需要指针语法）、结构、联合、运算符重载、虚基类等。（有关 Java 与 C++ 差异的更多内容，请参阅全书中穿插的 C++ 注记。）然而，设计者并未试图修正 C++ 所有笨拙的特性。例如，switch 语句的语法在 Java 中保持不变。如果你懂 C++，你会发现过渡到 Java 语法很容易。

Java 发布时，C++ 实际上并不是最常用的编程语言。许多开发者使用 Visual Basic 及其拖放式编程环境。这些开发者并不觉得 Java 简单。Java 开发环境花了几年时间才赶上。如今，Java 开发环境已远远领先于大多数其他编程语言的开发环境。

> 简单的另一个方面是体积小。Java 的目标之一是能够构建可在小型机器上独立运行的软件。基本解释器和类支持的大小约为 40K；基本标准库和线程支持（本质上是一个自包含的微内核）又增加了 175K。

