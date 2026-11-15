
这些清单对读者仍然可用，本附录包含第 3、11、12、14 和 17 章的完整清单。

- 附录 C—System.Collections.Concurrent 中的并发类：本附录提供了添加到 .NET Framework 4 的并发集合的概览图。
- 附录 D-F：C# 2.0、C# 3.0、C# 4.0 主题：这些附录为任何 C# 2.0、C# 3.0 或 C# 4.0 内容提供快速参考。它们专门设计用于帮助程序员快速掌握 C# 功能。

我希望您能将本书视为建立 C# 专业知识的绝佳资源，并继续参考它来了解 C# 及其内部工作原理中较为晦涩的领域。

——Mark Michaelis

mark.michaelis.net

## 致谢

没有一本书能仅靠作者独自出版，我非常感谢所有帮助我完成此书的众多人士。

我感谢人们的顺序并不重要，除了那些排在最前面的人。毫无疑问，我的家人做出了最大的牺牲，才让我得以完成此书。Benjamin、Hanna 和 Abigail 经常有一个因这本书而心不在焉的爸爸，但 Elisabeth 承受得更多。她常常独自承担照顾家庭的责任，独自支撑起家庭的世界。我本想说每一版都会变得容易些，但唉，并非如此；随着孩子们长大，生活变得更加忙碌，没有我的 Elisabeth 几乎时时都处于濒临崩溃的边缘。深深的抱歉和巨大的谢谢！

许多技术编辑以极其细致的方式审阅了每一章，以确保技术准确性。我常常惊叹于这些人员仍能捕捉到的细微错误：Paul Bramsman、Kody Brown、Ian Davis、Doug Dechow、Gerard Frantz、Thomas Heyey、Anson Horton、Brian Jones、Shane Kercheval、Angelika Langer、Eric Lippert、John Michaelis、Jason Morse、Nicholas Paldino、Jon Skeet、Michael Stokesbary、Robert Stokesbary、John Timney 和 Stephen Toub。

特别是，Michael 在编辑技术内容方面提供了巨大帮助，并在我整理材料时充当了倾听者，更不用说他宝贵的友谊了。我也特别感谢 C# MVPs（Nicholas 和 John），他们在某些领域对语言的了解仅次于 C# 团队成员。

Eric 简直令人惊叹。他对 C# 词汇的掌握真的令人惊叹，我非常感激他的编辑工作，尤其是在他追求术语完美时。他对 C# 3.0 章节的改进非常重要，在第二版中，我唯一的遗憾是没有让他审阅所有章节。然而，这个遗憾不再存在。Eric 以惊人的细节和精度辛勤审阅了每一章 Essential C# 4.0。我对他为使本书比前两版更出色所做出的贡献表示极大的感谢。谢谢，Eric！我无法想象还有比他更适合这项工作的人。你应得所有功劳，将书本从优秀提升到了卓越。

就像 Eric 和 C# 一样，了解 .NET 多线程并不亚于 Stephen Toub 的人寥寥无几。因此，Stephen 专注于两个重写的多线程章节及其对并行编程的新关注。Stephen 的反馈以及 Beta 版本之间发生的变化，促使我要求他在我根据他第一次审阅意见更新章节后再次审阅——他接受了。我真的无法想象还有比他更适合审阅的人了。谢谢，Stephen！特别感谢你在我熟悉新 API 期间包容我。

Paul 和 Robert 是第二版的关键技术审阅人员，他们辛勤地重新编译并执行了每个清单。这是一项巨大的工作，你们发现的错误非常宝贵，你们的建议也是如此。

感谢 UCLA Extension 的 Scott Robertson 为本书创建了用于大学采用的教学材料。

感谢 Addison-Wesley 的所有人，尽管我经常专注于除手稿之外的一切，他们仍与我合作，耐心等待。感谢：Olivia Basagio、Sheri Cain、Curt Johnson、Joan Murray 和 Brandon Prebynski。

Joan，还要感谢你在第二版期间每周打电话让我保持专注——好吧，至少是在我不专注时让我感到内疚。还要感谢你愿意在第三版期间包容我。我希望能说这次我让你压力更小了，但我怀疑我做到了。谢谢！

感谢 Audrey Doyle。任何能引用《芝加哥格式手册》的人，都必定是担任你团队文字编辑的合适人选。她注意到并纠正的事情让我怀疑自己是否有资格使用电子邮件。特别感谢她在格式方面的所有帮助。

来自 Microsoft 开发人员部门的 Prashant Sridharan 是让我着手此书的人，他为材料提供了了不起的开端。谢谢，Prashant！

*此页故意留空*

## 关于作者

Mark Michaelis 最近创立了 IntelliTecture，这是一家在 Microsoft VSTS/TFS、BizTalk、SharePoint 和 .NET 方面拥有高端技能的软件工程和咨询公司。Mark 还担任 IDesign Inc. 的首席软件架构师和培训师。

Mark 拥有伊利诺伊大学的哲学学士学位和伊利诺伊理工学院的计算机科学硕士学位。2007 年，Mark 被评为 Microsoft 区域总监。自 1996 年以来，他一直是 C#、Visual Studio Team System 和 Windows SDK 的 Microsoft MVP。他担任多个 Microsoft 软件设计评审团队的成员，包括 C#、Connected Systems Division 和 VSTS。Mark 在开发者大会上发表演讲，并撰写了大量文章和书籍。

不与电脑亲密接触时，Mark 正忙于家庭事务或为另一场铁人三项训练（他于 2008 年完成了 Ironman 赛事）。Mark 与妻子 Elisabeth 以及三个孩子 Benjamin、Hanna 和 Abigail 住在华盛顿州斯波坎。

此页故意留空

## 1 C# 简介

C# 现在是一门成熟的语言，它建立在其前身 C 风格语言（C、C++ 和 Java）的特性之上，因此许多经验丰富的程序员都会觉得它非常熟悉。C# 是一种用于构建软件组件和应用程序的编程语言，属于名为公共语言基础结构 (CLI) 的更大、更复杂的执行平台的一部分。

![](img/ef1bd88b5fdf5fb56f8510479607fe66_49_0.png)

本章使用传统的 HelloWorld 程序介绍 C#。本章重点介绍 C# 语法基础，包括定义 C# 程序可执行文件的入口点。这将使您熟悉

- 1. 自第一次 C# 设计会议以来，现在已经过去十多年了。

C# 语法风格和结构，并使您能够编写最简单的 C# 程序。在讨论 C# 语法基础之前，首先概述了托管执行上下文，解释了 C# 程序在运行时如何执行。本章最后讨论了变量声明、从控制台写入和检索数据，以及 C# 中代码注释的基础知识。

### Hello, World

学习新编程语言的最佳方法是编写代码。第一个示例是经典的 HelloWorld 程序。在此程序中，您将向屏幕显示一些文本。

清单 11 显示了完整的 HelloWorld 程序；在以下部分中，您将编译代码。

```
LISTING 11: HelloWorld in C#

class HelloWorld
{
    static void Main()
    {
        System.Console.WriteLine("Hello. My name is Inigo Montoya.");
    }
}
```

> **注意**
> 
> C# 是区分大小写的语言：大小写不正确会阻止代码成功编译。

有 Java、C 或 C++ 编程经验的人会立即看到相似之处。与 Java 一样，C# 从 C 和 C++ 继承了其基本语法。语法标点（如分号和花括号）、特性（如区分大小写）和关键字（如 class、public 和 void）

- 2. 如果您对 Inigo Montoya 的引用感到困惑，请参考电影《公主新娘》。
- 3. 在创建 C# 时，语言创建者拿着 C/C++ 规范坐下来，字面上划掉了他们不喜欢的功能，并列出了他们喜欢的功能列表。该组还包括在其他语言方面有深厚背景的设计师。
