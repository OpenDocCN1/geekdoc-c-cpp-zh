

## Notes

- 1. 关于BBS文化，我强烈推荐Jason Scott的《BBS：纪录片》（2005）。

- 2. Eliza并非第一个让观众产生与计算机进行有意义交流印象的系统。Matthew Kirschenbaum的《Mechanisms》（2008）提供了一个引人入胜的例子：“Professor RAMAC”——一台四吨重的IBM机器，在1958年世界博览会上被拟人化——它使用了当时革命性的硬盘驱动器，为访问一系列历史事实提供了问答功能。

- 3. Erik Loyer在为数字媒体期刊Vectors合作的一个项目中重新实现Eliza系统时指出，这次对话似乎经过编辑。除非Eliza系统有未记录的功能，否则它对“You are not very aggressive but I think you don't want to notice that”的回应应该是“WHAT MAKES YOU THINK I AM NOT VERY AGGRESSIVE BUT YOU THINK I DON'T WANT YOU TO NOTICE THAT”，而不是更简洁的“WHAT MAKES YOU THINK I AM NOT VERY AGGRESSIVE。”

- 4. 这篇文章不仅是解释Eliza过程的优秀、清晰来源（也是计算机科学文献中关于Eliza引用最多的出版物）。它还成为多年后全国各地计算中心创建的许多本地Eliza版本的基础。距离研究人员和爱好者能够轻松通过计算机网络相互传输软件，那时还相隔数十年——因此，《Communications of the ACM》（面向研究人员）和《Byte》（面向爱好者）等纸质出版物通常包含了在本地重新实现该软件所需的所有信息（例如，在Weizenbaum的文章中，包括完整的Doctor脚本）。

- 5. 虽然原始脚本文本全是大写，但我在此将其常规化。此外，此描述侧重于Eliza中运作的核心过程；若全部描述，本节将如Weizenbaum的论文般冗长。

- 6. 问号未被使用，因为在Weizenbaum使用的计算机系统上，它们被解释为“行删除”。

- 7. 这是Janet Murray在《Hamlet on the Holodeck》中报道的故事版本。除了这个版本，还有许多明显是伪造的版本流传，包括一个Weizenbaum作为事件参与者的版本。这个版本本身不可能是与Eliza的逐字对话，至少不是以Weizenbaum 1966年论文中系统存在时的形式。例如，该论文的Doctor脚本包含回应“YOU AREN'T SURE”和“WHY THE UNCERTAIN TONE”，但不包含“WHY AREN'T YOU SURE。”除了措辞差异外，还值得记住前一条注释：Weizenbaum使用的系统不支持问号，而问号贯穿于此记录中。

- 8. Mark J. Nelson在本书的基于博客的同行评审中敦促我澄清，这不仅适用于计算机系统——本章后面的一个例子就是证明：Harold Garfinkel的是/否治疗实验。

- 9. 公平地说，在Weizenbaum最初观察的时候，几乎没有人能够与Eliza Doctor进行持续的交互，因为计算资源有限。正如Weizenbaum所指出的，
"由于受试者无法探测*Eliza*能力的真实极限（毕竟，他只有有限的时间来玩弄它，而且它不断从他那里获取新素材），他不得不将比实际更大的力量归因于它"（1976, 191）。

- 10. Turkle评论道，“有些人会不遗余力地‘摸清’程序，以了解其结构，从而欺骗它并将其揭露为一台‘单纯的机器。’更多人则恰恰相反。……他们不会提出明知会‘混淆’程序、会让它‘胡言乱语’的问题。”（40）。Turkle将此归因于一种愿望，即“维持Eliza能够回应他们的幻觉。”然而，这也完全符合Murray将Eliza视为媒体体验的解读，观众塑造他们的互动，以帮助维持自愿的暂时怀疑。

- 11. Suchman认为，Garfinkel的实验支持Weizenbaum的观点，即与*Eliza Doctor*对话中的智能感来自观众的工作。此外，她主张，学生们强烈情境化的理解（他们基于假设的情境解释随机的是/否答案序列）不仅挑战社会科学的强结构导向假设，也挑战认知科学的假设。

- 12. 除了那少数可能希望探索其中一种效果的虚构作品之外。

## Chapter 3 Computer Game Fictions

### Digital Fictions and the Eliza Effect

想象你已经借出了书籍，穿过潮湿的黄昏，走到街对面的公交车站。它的荧光灯管已经闪烁亮起——你可以读取有机玻璃后面的时刻表和广告，以及散落在其上的贴纸。

一张矩形贴纸引起了你的注意。它上面没有任何乐队的名称，没有任何开锁师的电话号码，没有任何公司的标志，也没有Andre the Giant的图像。它只是一段文本。开头写着，“Why bomb libraries？”

这段文字摘自Implementation，这是一本以小块形式编写、排版适合通过标准激光打印机在邮寄标签上打印的小说。Implementation从某种意义上说是一种贴纸小说，也是一种数字小说。它的作者Nick Montfort和Scott Rettberg（2004）主要分发的不是贴纸。相反，他们分发数字文件，由他人将其打印在贴纸上并张贴在引人注目的位置。读者有时会遇到这些贴纸。但是，和大多数贴纸一样，它们往往会被迅速从长椅、门、卫生间隔间、雕像牌匾、路灯杆、保险杠以及其他张贴位置移除。更持久的是人们拍摄的Implementation贴纸在有趣位置的照片，大多数人正是通过这些图像体验Implementation，这些图像的文件大小远超Implementation网站上的其他内容。

遇到Implementation可能是一种神秘的体验。发现一张脱离上下文的文本贴纸，尤其是位置巧妙时，往往令人不安。而张贴贴纸的图像也有其自身的谜团：那是哪里？那是什么？但是，尽管数字技术对Implementation很重要，谜团从来不在于软件。Implementation依赖于数字过程——但却是我们每天都在使用的过程，以至于文件下载、激光打印和照片分享等过程不再吸引我们的注意力。

有人甚至可能认为，Implementation不适合作为“数字”小说来讨论，而应视为一种以数字方式分发和记录的小说。无论如何，在其使用数字过程方面，Implementation作为许多数字虚构作品中普遍存在的一种相对极端的例子：它们通过采用概念简单、熟悉且明确向观众展示的过程，避免了Eliza效应的困境。

不同的虚构作品以不同方式采用这种一般策略。有些与Implementation的方式相对接近，将自身嵌入熟悉的数字环境中。例如，Rob Wittig（2001, 2002）的电子邮件小说Blue Company依赖于电子邮件传输和阅读过程——但就像激光打印过程一样，这些过程对于许多有计算机访问权限的人来说已经完全自然化。同样，网页浏览器和网页服务器熟悉的链接跟踪功能使得可以从互连的网页网络中构建虚构作品，例如William Gillespie、Scott Rettberg、Dirk Stratton和Frank Marquardt（1999）的The Unknown。熟悉的过程也是Elan Lee、Sean Stewart、Jim Stewartson和Jane McGonigal（2004）的交替现实游戏I Love Bees等混合作品的主要数字组成部分，该游戏将玩家带入了由网页组成的虚构世界

