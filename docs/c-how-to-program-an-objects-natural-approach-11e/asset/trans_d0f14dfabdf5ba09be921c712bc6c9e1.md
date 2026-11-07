

## 7 编译器、Docker 和静态代码分析工具

### 工业级编译器

我们在 Windows、macOS 和 Linux 操作系统上，使用以下最新版本测试了所有代码的正确性：

- Windows® 上 Microsoft® Visual Studio® 社区版中的 Visual C++®，
- GNU® C++（g++），以及
- Clang C++（clang++）。

有关软件安装说明，请参见本前言之后的“开始之前”一节。

这些编译器现在已完整实现大多数 C++20 特性。我们会在适当之处指出例外情况。随着支持范围扩大，我们会将代码更新发布到本书的 GitHub 仓库：https://github.com/deitel/CPlusPlusHowToProgram11e，并将代码和文本更新发布到本书网站：https://www.deitel.com/books/cpphtp11

在撰写本书时，Apple 的 Xcode 集成开发环境（IDE）不支持我们使用的多项关键 C++20 特性。一旦这些特性在 Xcode 中可用，我们将在前述网站上发布 Xcode 使用说明。

### Docker

Docker 是一种将软件打包到容器中的工具，这些容器打包了跨平台便捷且可移植地执行该软件所需的一切。Docker 提供了一种简单方式，帮助你在台式机或笔记本电脑上快速、便捷且经济地开始使用新技术。我们展示如何安装并执行预配置了以下内容的 Docker 容器：

- GNU 编译器集合（GCC），其中包含 g++ 编译器，以及
- 最新版本的 Clang clang++ 编译器。

每种编译器都可以在 Windows、macOS 和 Linux 上的 Docker 中运行，使用户能够试用这些编译器的最新版本。第 1 章包含试用演练，展示如何编译程序并在跨平台 Docker 容器环境中运行它们。

### 静态代码分析工具

静态代码分析工具让你快速检查代码中的常见错误和安全问题，并提供代码改进的洞见。使用这些工具就像让世界级专家检查你的代码。为了帮助我们遵循 C++ 核心准则并总体改进代码，我们使用了以下静态代码分析器：

- `clang-tidy`—https://clang.llvm.org/extra/clang-tidy/
- `cppcheck`—https://cppcheck.sourceforge.io/
- Microsoft 的 C++ Core Guidelines 静态代码分析工具，这些工具内置于 Visual Studio 的静态代码分析器中

我们对本书所有代码示例使用了这三种工具，以检查：

- 是否遵循 C++ 核心准则，
- 是否遵循编码标准，
- 是否遵循现代 C++ 惯用法，
- 可能的安全问题，
- 常见缺陷，
- 可能的性能问题，
- 代码可读性，
- 等等。

我们还在 GNU g++ 和 LLVM clang++ 编译器中使用了编译器标志 -Wall，以启用所有编译器警告。我们的大多数程序编译时没有警告消息。有关在 Microsoft Visual C++ 中配置 C++ 核心准则检查器的信息，请参见本前言之后的“开始之前”一节。

## 8 像开发者一样思考——GitHub、StackOverflow 及更多

> *“准备[成为程序员]的最佳方式是编写程序，并研究其他人编写的优秀程序。就我而言，我曾去计算机科学中心的垃圾桶里，翻找出他们操作系统的代码清单。”*<sup>14</sup>—威廉·盖茨

你将使用 GitHub 和 StackOverflow 等热门网站，并进行大量互联网研究。

- StackOverflow 是最受欢迎的编程问答网站之一。你可能遇到的许多问题已经在这里讨论过。它是提出面向代码问题的好地方。在我们整个写作过程中，针对各种往往复杂的问题进行的许多 Google 搜索，其第一条结果都返回了 StackOverflow 帖子。
- GitHub 是寻找免费开源代码以探索并纳入你的项目的绝佳场所——如果你愿意，也可以向开源社区贡献你的代码。一亿开发者使用 GitHub。<sup>15</sup> 该网站托管着超过 3.3 亿个使用多种编程语言的代码仓库<sup>16</sup>——开发者们在 2022 年向仓库贡献了 4.13 亿次贡献。<sup>17</sup>

GitHub 是专业软件开发人员武器库中的关键要素，其版本控制工具帮助开发团队管理公共开源项目和私有项目。GitHub 上有一个庞大的 C++ 开源社区，开发者们向近 58,000 个 C++ 代码仓库贡献代码。我们鼓励你研究和执行大量开发者的开源 C++ 代码。这是一种很好的学习方式，也是我们实时编码教学方法的自然延伸。

- 14. William Gates，引自 Susan Lammers 的 *《工作中的程序员：与 19 位塑造计算机行业的程序员访谈》*。Microsoft Press，1986 年，第 83 页。
- 15. “Let’s build from here: The complete developer platform to build, scale, and deliver secure software.” 访问于 2023 年 3 月 8 日。https://github.com/about。
- 16. “Let’s build from here: The complete developer platform to build, scale, and deliver secure software.” 访问于 2023 年 3 月 8 日。https://github.com/about。
- 17. “OCTOVERSE 2022: The state of open source software.” 访问于 2023 年 3 月 8 日。https://octoverse.github.com。
- 18. “C++”。访问于 2023 年 3 月 8 日。https://github.com/topics/cpp。
- 19. 你需要熟悉 GitHub 上软件的各种开源许可证。

## 9 计算与数据科学课程体系

本书面向遵循以下一项或多项 ACM/IEEE 计算机科学及相关课程体系的课程，这些课程体系要求涵盖安全、数据科学、伦理、隐私和性能概念，并使用真实世界数据：

- 《计算机科学课程体系 2013》
- 《CC2020：计算课程体系愿景》
- 《计算课程体系 2020》建议
- 《信息技术课程体系 2017》
- 《网络安全课程体系 2017》
- 由 NSF 和高等研究院资助的教师小组制定的 2016 年数据科学倡议“数据科学本科项目课程指南”，以及
- ACM 数据科学任务组的《数据科学本科课程计算能力最终报告》。

![](img/7b5e2088e71c7f78681d4ddbcf104c06_39_0.png)

- 20. ACM/IEEE（计算机协会/电气与电子工程师协会，2013）。*《计算机科学课程体系 2013：计算机科学本科学位项目课程指南》*（纽约：ACM）。访问于 2023 年 3 月 8 日。http://ai.stanford.edu/users/sahami/CS2013/final-draft/CS2013-final-report.pdf。
- 21. A. Clear、A. Parrish、G. van der Veer 和 M. Zhang，“CC2020: A Vision on Computing Curricula。”访问于 2023 年 3 月 8 日。https://dl.acm.org/citation.cfm?id=3017690。
- 22. CC2020 任务组，*《计算课程体系 2020》*。访问于 2023 年 3 月 8 日。https://www.acm.org/binaries/content/assets/education/curricula-recommendations/cc2020.pdf。
- 23. *《信息技术课程体系 2017》*。访问于 2023 年 3 月 8 日。http://www.acm.org/binaries/content/assets/education/it2017.pdf。
- 24. *《网络安全课程体系 2017》*。访问于 2023 年 3 月 8 日。https://cybered.hosting.acm.org/wp-content/uploads/2018/02/newcover_csec2017.pdf。
- 25. “Curriculum Guidelines for Undergraduate Programs in Data Science。”访问于 2023 年 3 月 8 日。http://www.annualreviews.org/doi/full/10.1146/annurev-statistics-060116-053930。
- 26. ACM 数据科学任务组，*《数据科学本科课程计算能力》*。访问于 2023 年 3 月 8 日。https://dsf.acm.org/DSFT_Final_Report.pdf。

- 附录 A“字符集”包含 ASCII 字符集的字母、数字和符号。
- 附录 B“数制”概述二进制、八进制、十进制和十六进制数制。
- 附录 C“预处理器”讨论 C++ 预处理器的其他特性。模板元编程（第 15 章）和 C++20 模块（第 16 章）消除了对本附录许多特性的需要。
- 附录 D“位操作”讨论用于操作整型操作数各个位的按位运算符，以及用于紧凑表示整数数据的位字段。

## deitel.com 上的其他网络资源

本书网页还包含：

- 指向我们的 GitHub 仓库的链接，其中包含可下载的 C++ 源代码
- 博客文章——https://deitel.com/blog
- 图书更新

有关下载代码示例和设置 C++ 开发环境的更多信息，请参见本前言之后的“开始之前”一节。

## 12 C++ 核心准则

C++ Core Guidelines https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines 是“帮助人们有效使用现代 C++”的建议。<sup>32</sup> 它们由 Bjarne Stroustrup（C++ 的创造者）和 Herb Sutter（ISO C++ 标准委员会召集人）编辑。根据其概述：

> > “这些准则侧重于相对高层的问题，例如接口、资源管理、内存管理和并发。此类规则会影响应用程序架构和库设计。遵循这些规则将产生静态类型安全、无资源泄漏、并能比当今常见代码捕获更多编程逻辑错误的代码。而且它运行得很快——你完全有条件把事情做对。”<sup>33</sup>

在本书中，我们会在适当之处遵循这些准则。你会希望密切关注其中的智慧。我们用 CG 图标指出许多 C++ 核心准则建议。核心准则有数百条，分为数十个类别和子类别。尽管这看起来可能让人不知所措，但我们前面讨论的静态代码分析工具可以对照这些准则检查你的代码。

![](img/7b5e2088e71c7f78681d4ddbcf104c06_41_0.png)

- 32. C++ 核心准则，“摘要”。访问于 2023 年 3 月 8 日。https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#s-abstract。
- 33. C++ 核心准则，“摘要”。

