

我希望这本书能成为你建立 C# 专业知识的宝贵资源，并且即使在你已经精通 C# 之后，你仍会继续参考其中那些你不经常使用的部分。

—Mark Michaelis

IntelliTect.com/mark

Twitter: @IntelliTect, @MarkMichaelis

> 在 InformIT 网站注册你的《Essential C# 7.0》副本，以便在更新和/或勘误表可用时方便地获取。要开始注册过程，请访问 informit.com/register 并登录或创建一个账户。输入产品 ISBN（9781509303588）并点击提交。在“已注册产品”选项卡上查看此产品旁边的“访问奖励内容”链接，并遵循该链接访问可用的奖励材料。如果你希望收到有关新版和更新的独家优惠通知，请勾选接收我们电子邮件的复选框。

## 致谢

一本书不可能仅靠作者独自出版，我对帮助我的众多人员表示极度感激。感谢顺序并不重要，除了那些排在前面的人。鉴于这是该书的第六版，你可以想象在过去 10 年里（更别说之前的书了）我的家人为我写作牺牲了多少。Benjamin、Hanna 和 Abigail 经常面对的是一个被这本书分心了的爸爸，但 Elisabeth 受的苦更多。她常常独自承担着照顾家庭的责任，维持着家庭的世界。（2017 年休假期间，我在室内花费数天写作，而他们更想去海滩。）巨大的抱歉和巨大的感谢！

多年来，许多技术编辑对每一章进行了细致的审查，以确保技术准确性。我经常惊讶于这些人仍然设法捕获的细微错误：Paul Bramsman、Kody Brown、Ian Davis、Doug Dechow、Gerard Frantz、Thomas Heavey、Anson Horton、Brian Jones、Shane K. Ercheval、Angelika Langer、Eric Lippert、John Michaelis、Jason Morse、Nicholas Paldino、Jon Skeet、Michael Stokesbary、Robert Stokesbary、John Timney、Neal Lundby、Andrew Comb、Jason Peterson、Andrew Scott、Dan Haley、Phil Spokas（他帮助完成了第 22 章部分的写作），以及 Kevin Bost。

当然，Eric Lippert 卓越非凡。他对 C# 的掌握令人惊叹，我非常感激他的编辑，尤其是当他在术语方面追求完美时。他对 C# 3.0 章节的改进意义非凡，而在第二版中，我唯一的遗憾是没有让他审查所有章节。然而，那个遗憾现在不再存在。Eric 仔细审查了每一章 *Essential C# 4.0*，甚至担任了 *Essential C# 5.0* 和 *Essential C# 6.0* 的合著者。我极度感激他在 *Essential C# 7.0* 中担任技术编辑的角色。谢谢你，Eric！我想象不出还有谁更适合这个职位。将标准从良好提升到卓越，所有的功劳都属于你。

就像 Eric 和 C# 一样，对 .NET 多线程了解得如此之好的人屈指可数，Stephen Toub 就是其中之一。因此，Stephen 专注于两章重写（第三次）的多线程章节，以及它们在 C# 5.0 中对异步支持的新重点。谢谢你，Stephen！

感谢 Pearson/Addison-Wesley 的每一位人员，尽管我经常关注手稿以外的一切，他们仍然耐心地与我合作。感谢 Trina Fletcher Macdonald、Anna Popick、Julie Nahil 和 Carol Lallier。Trina 理应获得一枚特别奖牌，因为她明显在处理众多其他更重要的事情的同时，忍受了我这样的人。此外，Carol 对细节的关注是无价的，她改进写作和红线潜在写作失误的能力（即使在代码列表中发现它们时也能捕捉到）非常令人感激。

### 作者简介

**Mark Michaelis** 是 IntelliTect 的创始人，这是一家高端软件工程和咨询公司，他在该公司担任首席技术架构师和培训师。Mark 在开发者大会上发表演讲，并撰写了众多文章和书籍。目前，他是 *MSDN Magazine* 的 Essential .NET 专栏作家。

自 1996 年以来，Mark 一直是 C#、Visual Studio Team System 和 Windows SDK 的 Microsoft MVP。2007 年，他被认可为 Microsoft 区域总监。他还担任多个 Microsoft 软件设计审查团队的成员，包括 C# 和 VSTS。

Mark 拥有伊利诺伊大学的哲学文学学士学位和伊利诺伊理工学院的计算机科学硕士学位。

当没有与电脑相处时，Mark 忙着照顾家人或玩壁球（自 2016 年起暂停参加铁人三项比赛）。Mark 和他的妻子 Elisabeth 以及三个孩子 Benjamin、Hanna 和 Abigail 住在华盛顿州斯波坎。

### 技术编辑简介

**Eric Lippert** 在 Facebook 从事开发者工具工作；他曾是 Microsoft C# 语言设计团队的前成员。在不回答 StackOverflow 上的 C# 问题或编辑编程书籍时，Eric 尽最大努力保持他那艘小帆船直立。他和妻子 Leah 住在华盛顿州西雅图。

## 1 介绍 C#

C# 现在是一种成熟稳定的语言，它建立在其前身 C 风格语言（C、C++ 和 Java）中的功能之上，使许多经验丰富的程序员立即感到熟悉。¹ 此外，C# 编程语言可用于构建在多种操作系统（平台）上运行的软件组件和应用。

![](img/ef6a8a417630b222bfb3f3b949facff0_37_0.png)

本章使用传统的 Hello World 程序介绍 C#。它专注于 C# 语法基础，包括定义 C# 程序的入口点，这将使你熟悉 C# 的语法风格和结构，并使你能够编写最简单的 C# 程序。在讨论 C# 语法基础之前，是对托管执行环境的概述，它解释了 C# 程序在运行时如何执行。本章以讨论变量声明、从控制台写入和检索数据以及 C# 中注释代码的基础知识结束。

### Hello, World

学习新编程语言的最佳方法是编写代码。第一个示例是经典的 Hello World 程序。在这个程序中，你将在屏幕上显示一些文本。

列表 1.1 显示了完整的 Hello World 程序；在以下部分中，你将编译并运行代码。

**列表 1.1: C# 中的 Hello World**²

```csharp
class HelloWorld
{
    static void Main()
    {
        System.Console.WriteLine("Hello. My name is Inigo Montoya.");
    }
}
```

> **注意**
> C# 是一种区分大小写的语言：错误的大小写会导致代码无法成功编译。

那些有 Java、C 或 C++ 编程经验的人会立即看到相似之处。与 Java 一样，C# 从 C 和 C++³ 继承了其基本语法，句法标点（如分号和花括号）、功能（如区分大小写）和关键字（如 class、public 和 void）对于这些语言有经验的程序员来说是熟悉的。初学者和其他语言的程序员会很快发现这些结构是直观的。

¹ 第一次 C# 设计会议于 1998 年举行。
² 如果你对在伊尼戈·蒙托亚的引用感到困惑，请参考电影《公主新娘》。
³ 在创建 C# 时，语言创建者审查了 C/C++ 的规范，字面上划掉了他们不喜欢的功能，并创建了一个他们喜欢的功能列表。该小组还包括在其他语言方面有强大背景的开发者。

### 创建、编辑、编译和运行 C# 源代码

一旦你编写了 C# 代码，就是编译和运行它的时候了。你可以选择使用哪个 .NET 实现——有时被称为 .NET 框架。通常，实现被打包成软件开发工具包（SDK）。SDK 包括编译器、运行时执行引擎、运行时可以访问的实用功能框架（见本章后面的“应用程序编程接口”），以及可能与 SDK 捆绑的任何额外工具（例如用于自动构建步骤的构建引擎）。鉴于 C# 自 2000 年以来已公开可用，有几种不同的 .NET 框架可供选择（见本章后面的“多个 .NET 框架”）。

对于每个 .NET 框架，安装说明因你正在开发所使用的操作系统和你选择的 .NET 框架而异。因此，我建议你访问 https://www.microsoft.com/net/download 获取下载和安装说明，首先选择 .NET 框架，然后根据你要开发的操作系统选择要下载的包。虽然我可以在此提供更多细节，但 .NET 下载站点拥有每个受支持组合的最新说明。

如果你不确定要使用哪个 .NET 框架，默认选择 .NET Core。它在 Linux、macOS 和 Microsoft Windows 上运行，是 .NET 开发团队将大部分投资应用于的实现。此外，由于跨平台能力，我将在章节中偏向使用 .NET Core 说明。

还有许多编辑源代码的方法，包括使用最基础的工具，如 Windows 上的记事本、Mac/macOS 上的文本编辑，或 Linux 上的 vi。但是，你很可能需要更高级的工具，至少使你的代码被着色。任何支持 C# 的编程编辑器都足够了。如果你还没有偏好，我建议你考虑开源编辑器 Visual Studio Code (https://code.visualstudio.com)。或者，如果你正在 Windows 或 Mac 上工作，考虑 Microsoft Visual Studio 2017（或更高版本）——参见 https://www.visualstudio.com。两者均可免费获得。

在接下来的两个部分中，我提供了两种编辑器的说明。对于 Visual Studio Code，我们依赖命令行（Dotnet CLI）来创建初始 C# 程序脚手架，除了编译和运行程序。对于 Windows 和 Mac，我们专注于使用 Visual Studio 2017。

