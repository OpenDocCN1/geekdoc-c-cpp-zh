

# Objective-C®

开发者参考

# Objective-C

# Objective-C

Jiva Devoe

![](img/aaee977487e7a3eefe7b1dd596e0f6fb_4_0.png)

Wiley Publishing, Inc.

献给我妻子 Dawn，以及我的孩子们 Robert、Alex 和 Izzy。
你们是我生命中最重要的人，永远都是。

## 关于作者

Jiva DeVoe 编写软件已有近 25 年的历史，从使用 BASIC 和汇编语言的 Commodore VIC-20 开始，逐步掌握了 C、C++、Python、Ruby、Java，最后是 Objective-C。2001 年，他创立了 Random Ideas, LLC，一家致力于为 Mac 打造优秀应用的软件公司。当 iPhone SDK 发布时，他很荣幸被选为最早获得 SDK 访问权限的开发者之一，并利用它开发了几款应用，这些应用在 2008 年 7 月 11 日 iTunes App Store 上线时即可使用。此后，他的 iPhone 应用获得了多项奖项，包括被选为 App Store 中排名前 100 的应用和游戏之一，并被评为 Apple 员工精选并出现在 Apple 广告中。如今，Jiva 继续全职为他的公司 Random Ideas 工作，开发优秀的 iPhone 和 Mac 应用。他与妻子、三个孩子和两只巴吉度猎犬一起生活在亚利桑那州尘土飞扬的沙漠中。

## 致谢

收购编辑
Aaron Black

执行编辑
Jody Lefevere

项目编辑
Beth Taylor

技术编辑
Brad Miller

校对编辑
Beth Taylor

编辑总监
Robyn Siesky

编辑经理
Rosemarie Graham

业务经理
Amy Knies

高级营销经理
Sandy Smith

副总裁兼执行集团出版人
Richard Swadley

副总裁兼执行出版人
Barry Pruett

项目协调员
Katherine Crocker

制作专员
Carrie A. Cesavice

质量控制技术员
Melissa Cossell

校对和索引
Laura Bowman, Evelyn Wellborn,
BIM Indexing & Proofreading Services

## 前言

Objective-C 在 IT 行业中得不到应有的待遇。尽管它是一种功能强大且动态的面向对象语言，但它获得的认可远不及 C++、Java 等语言。

当我撰写《Cocoa Touch for iPhone OS 3》时，我知道它需要一本配套书籍，帮助人们在进入更高层的框架 Cocoa 和 Cocoa Touch 之前，跨越学习 Objective-C 的障碍。

因此，当有机会撰写一本专门介绍 Objective-C 语言的书籍时，我欣然接受了！

最终，我觉得我有机会通过这本书为新 Mac、iPhone 和 iPad 开发者的知识基础做出贡献，我对此感到无比兴奋。我喜欢这个想法，即这本书可能成为催化剂，帮助 Objective-C 不仅在这些平台上，而且在许多其他平台上发展壮大。Objective-C 没有理由不能在 Unix、Windows 等平台上得到更多使用。

作为读者，您只需具备有限的计算机知识。我已尝试从最基本的要素入手，但您至少需要具备基本的计算机操作背景。

如果您已经了解一些编程语言，这对您不会有坏处。我讨论的一些内容对您来说可能是复习，但不用担心，这里有大量关于 Objective-C 的具体内容供您学习。

如果您已有 Objective-C 背景，我希望您能在本书中找到一些您不知道的信息。我已尝试以易于访问的形式呈现，以便您在需要时查找具体内容。您可能不会从头到尾阅读，但它应该能让您跳转到特定部分，了解如何完成您想要做的事情。

关于本书中使用的惯例，我已尽量保持一致，并在适当时通常遵循 Apple 的惯例。唯一值得注意的例外是我使用“方法”一词来表示实例和类上的函数。Apple 通常更喜欢“消息”一词。这在一定程度上是由于 Smalltalk 对 Objective-C 的影响。

在提及键盘快捷键时，我选择使用“Command-Key”一词来表示使用大多数 Apple 键盘上空格键左侧的键的键盘快捷键。您可能也知道这是“Apple”键，因为在几年前，它上面还印有小苹果标志。此外，Command-Key 旁边的键被称为“Option-Key”，再旁边的键被称为“Control-Key”。这些都应与 Apple 文档惯例保持一致。

在提及存储对象的变量时，我经常称它们为“实例变量”。一些书籍喜欢使用此术语，或其缩写“ivar”来指代类的一部分变量。对于这些变量，我更喜欢“成员变量”一词。对我来说，成员变量可以是实例变量，但并非所有实例变量都是成员变量。

在正文中引用方法时，我使用了标准的 Apple 惯例，即使用方法名引用它们，但不带参数。例如，方法：

```
-(void)someMethodUsingParam1:(NSString *)param1 andParam2:(NSString *)param2;
```

在正文中会写成：-someMethodUsingParam1:andParam2。如果是类方法，前面带连字符的符号会被 + 替换，就像您在类定义中编写方法一样。

关于示例代码，在我指导您构建特定完整项目的章节中，我通常会尽量包含代码的完整列表。在未包含的情况下，您始终可以从本书网站下载项目，其中包含艺术作品和其他支持文件。还有一些章节，制作完整项目来演示技术并不合适。在这些情况下，代码列表更多是您可以作为自己代码基础的片段。由于这些片段不构成完全可用的项目，网站上不会提供这些示例项目。

我希望您阅读本书的体验与我撰写本书一样愉快。对我来说，一本优秀的技术书籍的标志是它不会放在我的书架上。它在我的办公桌上或附近占据着荣誉的位置，因为我一次又一次地返回阅读它。我希望这本书在您的图书馆中享有同样的声望，并成为一本被翻阅、封面破损、页面上写满笔记的参考书，多年后仍对您有用。

Jiva DeVoe

book@random-ideas.net

## 致谢

撰写这本书既令人充实又充满挑战，但如果没有一些特定个人的帮助和支持，我是不可能完成的，我想向他们表示感谢。

首先，我要感谢 Cynical Peak Software 的 Brad Miller，他是业内最好的技术编辑之一。他对细节的关注以及他不懈地帮助我纠正错误，令人惊叹。感谢你的努力。你太棒了。

感谢他在 Wiley 的帮助和倡导，尽管道路有些坎坷，我要感谢 Aaron Black。你的赞助和帮助让我倍感珍惜。

感谢我的父亲 Robert A. DeVoe 教我惊叹于技术的奇迹，并鼓励我追求计算机梦想，我对此心存感激。

感谢我的儿子 Alex，他花费了许多小时排版这本书的页面，谢谢你。你的努力和帮助对于这本书的实现至关重要。

最后，也是最重要的是，我要感谢我的妻子，她在这项目中以及我所有的工作中给予了我坚定不移的支持。如果没有她，这本书就不可能完成。你在我精神低落、疲惫时提携我，并激励我不断追求新的成就和目标。我无法足够感谢你。

