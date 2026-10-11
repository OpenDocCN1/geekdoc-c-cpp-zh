
# WPF 程序员参考指南：CA 2010 和 .NET 4 的 Windows Presentation Foundation

## 从 wrox.com 获取更多内容

### 互动
通过参与 `@p2p.wrox.com` 的 P2P 论坛，在网上发挥积极作用

### 加入社区
在 `newsletter.wrox.com` 订阅我们的免费每月新闻邮件

### Wrox 在线图书馆
我们的数百种书籍已通过 `Books24x7.com` 可提供

### 浏览
准备好学习 Wrox 吗？我们提供了关于 .NET、SQL Server、Java、XML、Visual Basic、C#/ C++ 及等领域的书籍和电子书！

### Wrox Blox
下载简短的信息片段和代码，让您与时同步并避免陷阱！

### 联系我们
我们总是欢迎来自读者的反馈。有书的书的想法吗？需要社区支持吗？请发送电子邮件至 `wrox-partnerwithus@wrox.com` 告诉我们

书号: `978-0-470-47722-9`

## 关于作者

`ROD STEPHENS` 在 MIT 求读期间开始一名数学家，他发现了编程的乐趣，从那以后一直从事专业编程。在职业生涯中，他参与了多个领域的应用，如电话交换、计费、维修调度、税务处理、废水处理、演唱会门票销售、地图绘制以及职业运动员的训练。

`Rod` 是微软 Visual Basic 最优秀专业人士 (MVP) 和 ITT 兼职教师。他编写了 20 多本书，这些书籍已被翻译成全球各种语言，并发表了 250 多篇涵盖 Visual Basic、C#、VBA、Delphi 和 Java 的杂志文章。他是 `DevX` (`www.DevX.com`) 的定期贡献者。

`Rod` 著名的 VB Helper 网站 `www.vb-helper.com` 每月拥有数百万访问量，包含了数千页针对 Visual Basic 程序员的提示、技巧和示例代码，以及本书的示例代码。

## 鸣谢

执行编辑
`Bob Elliott`

副总裁及执行集团出版经理
`Richard Swadle`

高级项目编辑
`Adaobi Obi Tuton`

副总裁及执行出版经理
`Barry Pruett`

技术编辑
`John Mueller`

助理出版
`Jim Minateli`

高级制作编辑
`Debra Banninger`

封面协调员
`Lynsey Stanford`

拷贝
`Cate Caffery`

排版
`James D. Kramer, Happenstance Type-O-Ramer`

编辑总监
`Robyn B. Siesky`

校对
`Nancy Carrasco`

编辑经理
`Mary Beth Wakefield`

索引
`J & J Indexing`

营销经理
`Ashley Zurcher`

封面设计师
`Michael E. Trent`

制作经理
`Tim Tate`

封面图片
© Ben Blankenburg / istockphoto

## 致谢

感谢 `Bob Elliott`、`Adaobi Obi Tulton`、`Kristin Vorce`、`Cate Caffery` 以及所有为本书这本书付出巨大努力的人。

同样感谢 `John Mueller` 为我提供了另一个视角以及他丰富的专业知识。访问 `www.mwt.net/~mueller` 了解 John 的书籍并订阅他的免费邮件 .NET Tips, Trends & Technology eEXTRA。

- 新控件 17
- 分隔符 (`Separator`) 97
- 矩形 (`Rectangle`) 151
+ 第 11 章：事件与后台代码 179
- 示例代码 181

## 第 19 章：控制 347
控制概念 348
带操作的预定义命令 349
不带操作的预定义命令 352
自定义命令 355
总结 358

## 第 20 章：变换与效果 359
总结 416
`DockPanel` 附加属性 423
`GroupBox` 431
线性渐变画刷 500
`SolidBrush` 502
选择表达式 516
显示表达式 517
+ 绑定组件 519
绑定到 `RelativeSource` 520
绑定到 XAML 代码中的类 521
XAML 代码中的集合 522
后台代码中的集合 522
`ComponentCommands` 526
编辑命令 527
`MediaCommands` 530
导航命令 531
XAML 中的命令 531
后台代码中的命令 532
命名样式 535
未命名样式 536
`CheckBox` 540
`RadioButton` 541
定向进度条 542
修改的滚动条 445

# 引言

`WINDOWS PRESENTATION Foundation` (`WPF`) 是微软在用户界面 (`UI`) 开发方面的下一步。虽然 `WPF` 允许开发者像多年来那样投放控件，但 `WPF` 提供了一次跨越式的飞跃。

`WPF` lets you drop controls as developers have been doing for years, but `WPF` provides a quantum leap.

`WPF` allows you to drop controls as developers have been doing for years, but `WPF` provides a quantum leap.

and content, as shown in Figure 0-1.

`WPF` lets you drop controls as developers have been doing for years, but `WPF` provides a quantum leap.

`WPF` lets you drop controls as developers have been doing for years, but `WPF` provides a quantum leap.

`WPF` allows you to rearrange their content, and needed, as shown in Figure 0-2.

`WPF` lets you drop controls as developers have been doing for years, but `WPF` provides a quantum leap.

`WPF` lets you drop controls as developers have been doing for years, but `WPF` provides a quantum leap.

such- and effects, as shown in Figure 0-3.

`WPF` lets you drop controls as developers have been doing for years, but `WPF` provides a quantum leap.

`WPF` allows you to drop controls as developers have been doing for years, but `WPF` provides a quantum leap.

and effects, as shown in Figure 0-4.

`WPF` lets you drop controls as developers have been doing for years, but `WPF` provides a quantum leap.

`WPF` allows you to drop controls as developers have been doing for years, but `WPF` provides a quantum leap.

and effects, as shown in Figure 0-5.

`WPF` lets you drop controls as developers have been doing for years, but `WPF` provides a quantum leap.

`WPF` allows you to drop controls as developers have been doing for years, but `WPF` provides a quantum leap.

and- effects, as shown in Figure 0-6.

`WPF` lets you drop controls as developers have been doing for years, but `WPF` provides a quantum leap.

`WPF` allows you to drop controls as developers have been doing for years, but `WPF` provides a quantum leap.

and- effects, as shown in Figure 0-7.

`WPF` lets you drop controls as developers have been doing for years, but `WPF` provides a quantum leap.

`WPF` allows you to drop controls as developers have been doing for years, but `WPF` provides a quantum leap.

and- effects, as shown in Figure 0-8.

`WPF` lets you drop controls as developers have been doing for years, but `WPF` provides a quantum leap.

Unfortunately, to use `WPF`, you must overcome a steep learning curve. Many of the fundamental concepts in modern UI design are different from those used by `WPF`. Concepts as basic as how events are handled and how program code is attached to the user interface are different in `WPF`. Many of these new concepts are unified, elegant, and simple. Such as declarative building an interface in Extensible Markup Language (`XAML`), value inheritance, and allowing controls to contain any type of content make it simple yet powerful.

This book provides an introduction to `WPF` development. It explains fundamental concepts so you can start applications quickly and easily. As it progresses, the book covers more complex topics, explaining how to handle the extras and shortcuts built into `WPF`.

The book finishes with a series of appendices summarizing `WPF` concepts and syntax for easy reference. You can use these appendices to refresh your memory of `WPF`'s intricate and sometimes intuitive syntax.

Of course, many future applications will be written without `WPF`. Many will be written using clunky old technologies like command-line interfaces and pure HTML. Others will be written with competing technologies like Java and Flash. Finally, developers will continue using old familiar Windows Forms in C# or Visual Basic. There's a lot to be said for sticking with what you know, but the future of development in the Windows environment is `WPF`.

## 谁适合这本书

This book is for anyone who wants to use or better understand `WPF`. In particular, it is intended for:

- Specialized UI designers who build user interfaces but don't write program code
- Programmers who write the code behind the user interface
- Jack-of-all-trades developers who create user interfaces and write the code behind them
- Web developers who want to learn how to use `WPF` in loose web pages, browser-applications, and Silverlight applications
- Project managers who want a better understanding of what `WPF` is and what kinds of features it can provide

## 引言

几十年来，优秀的开发者一直将 UI 构建与用户界面背后的代码（code behind）分开。保持这种分离有利于在不同的开发者之间分配工作，并更便于独立地构建每个部分。`WPF` 延续了这一哲学，它让用户界面与后台代码之间的分离比以往任何时候都更加清晰。

事实上，微软最初的愿景是：由专业的图形设计师构建用户界面，而程序员则完全负责添加后台代码。

虽然许多开发项目无法负担同时雇佣独立图形设计师和程序员的费用，但将这两项任务分开仍然很有价值。本书专门为负责其中任一任务的人士而编写。

本书提供了对 `WPF` 的介绍，不需要你具备任何相关经验。事实上，它甚至不需要你具备任何先前的编程或 UI 设计经验。

> 我不想收到一大堆抱怨某些内容太基础的“喷火式”邮件，所以我现在就警告你！如果你对入门级材料感到受到了极大的冒犯，欢迎跳过前几章，直接阅读更高级的内容。

尽管本书不需要先前的编程经验，但它涵盖了大量内容，并涉及了一些高级主题。当你读完这本书时，无论你开始时的经验如何，都应该学到很多。

## 本书涵盖的内容（以及未涵盖的内容）

本书解释了 `WPF` 开发。它解释了如何使用微软的 `Expression Blend` 工具、`Visual Studio` 和 `XAML` 语言来构建用户界面。它还解释了如何使用 `Visual Studio` 将代码附加到界面。

`WPF` 是一个非常灵活的工具，你可以用它制作出惊叹的用户界面。遗憾的是，它通常也很复杂，有时令人困惑，有时又令人生畏。你可以利用它完成非凡的 UI 幻术，但这样做可能是一场充满实验和浏览的英雄式冒险。

这种开发行为违背了微软的愿景——即由专业图形设计师构建用户界面，然后由程序员将其附加到代码中。我可能混错了圈子，但我遇到的设计师并没有技能或兴趣花费时间去构建复杂的 UI 界面。相反，他们更关注界面的外观和易用性。

本书的哲学是：用户界面是应用程序的前端，而不是应用程序本身。构建一个数据输入表单不需要多年的经验和 `WPF` 博士学位。
