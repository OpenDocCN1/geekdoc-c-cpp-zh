
我们已将代码升级（已按入门教材的适当程度）以符合各项 CERT 建议。如果你将在业界构建 C 系统，建议阅读 *CERT C安全编码标准（第2版）*（Robert Seacord，Addison-Wesley Professional，2014）和 *C和C++安全编码（第2版）*（Robert Seacord，Addison-Wesley Professional，2013）。CERT 指南可在 https://www.securecoding.cert.org/confluence/display/seccode/CERT+C+Coding+Standard 免费在线获取。

Seacord 先生是本书上一版 C 语言部分的技术审阅者，他为我们每个“安全 C 编程”章节提供了具体建议。Seacord 先生是卡内基梅隆大学软件工程研究所（SEI）CERT 的安全编码经理，也是卡内基梅隆大学计算机科学学院的兼职教授。

第 2–13 章末尾的“安全 C 编程”章节讨论了许多重要主题，包括：

- 测试算术溢出
- 防止缓冲区溢出
- 使用无符号整数类型
- 输入验证
- C 标准附录 K 中更安全的函数
- 避免未定义行为
- 检查标准库函数返回的状态信息的重要性
- 选择返回状态信息的函数，还是使用不返回状态信息的类似函数
- 范围检查
- 确保指针始终为 NULL 或包含有效地址
- 安全随机数生成
- 使用 C 函数还是使用预处理器宏，等等。
- 数组边界检查

## 网络资源

本书的开放访问配套网站（http://www.pearsonglobaleditions.com/deitel）包含所有代码示例的源代码以及以下 PDF 格式附录：

- 附录 F，使用 Visual Studio 调试器
- 附录 G，使用 GNU gdb 调试器
- 附录 H，使用 Xcode 调试器

## 依赖关系图

接下来两页的图 1 和图 2 展示了各章之间的依赖关系，以帮助教师规划教学大纲。*C语言程序设计（第8版）* 适合 CS1 和许多 CS2 课程，也适合中级 C 和 C++ 编程课程。本书的 C++ 部分假定你已学习 C 语言第 1–10 章。

## 教学方法

*C语言程序设计（第8版）* 包含丰富的示例集。我们关注良好的软件工程、程序清晰性、预防常见错误、程序可移植性和性能问题。

![](img/d0d3b7423c2d9e5650be79209ea1885d_27_0.png)

**图1 |** C语言各章依赖关系图

**语法着色。** 为便于阅读，我们对代码进行语法着色，类似于大多数 IDE 和代码编辑器给代码做语法配色的方式。我们的语法着色约定是：

```
comments appear like this in gray
keywords appear like this in dark blue
constants and literal values appear like this in light blue
all other code appears in black
```

![](img/d0d3b7423c2d9e5650be79209ea1885d_29_0.png)

## 性能提示

*这些提示强调让程序运行更快或尽量减少程序占用内存量的机会。*

![](img/d0d3b7423c2d9e5650be79209ea1885d_29_1.png)

## 可移植性提示

*这些可移植性提示帮助你编写可在多种平台上运行的代码。*

![](img/d0d3b7423c2d9e5650be79209ea1885d_29_2.png)

## 软件工程观察

*这些软件工程观察强调影响软件系统构建（尤其是大型系统）的架构和设计问题。*

**摘要要点。** 我们提供每章的详细逐节项目符号列表摘要，关键术语用**粗体**表示。为便于参考，大多数关键术语后面都跟有其定义出现处的页码。

**自测练习题与答案。** 包含大量自测练习题和答案，供自学使用。

**练习题。** 每章末尾都有大量练习题，包括：

- 简单回忆重要术语和概念
- 识别代码示例中的错误
- 编写单个程序语句
- 编写 C 函数（以及 C++ 成员函数和类）的小部分
- 编写完整程序
- 实现大型项目

**索引。** 我们提供了详尽的索引，当把本书作为参考书使用时尤其有帮助。关键术语的定义出现处在索引中以粗体彩色页码突出显示。

## *C语言程序设计（第8版）*中使用的软件

我们使用以下免费编译器测试了 *C语言程序设计（第8版）* 中的程序：

- GNU C 和 C++（http://gcc.gnu.org/install/binaries.html），它们已安装在大多数 Linux 系统上，也可安装在 OS X 和 Windows 系统上。
- 微软 Visual Studio 2013 Community 版中的 Visual C++，可从 http://go.microsoft.com/?linkid=9863608 下载
- Apple Xcode IDE 中的 LLVM，OS X 用户可从 Mac App Store 下载。

其他免费 C 和 C++ 编译器，请访问：

```
http://www.thefreecountry.com/compilers/cpp.shtml
http://www.compilers.net/Dir/Compilers/Cpp.htm
http://www.freebyte.com/programming/cpp/compilers
http://en.wikipedia.org/wiki/List_of_compilers#C.2B.2B_compilers
```

## 教师资源

以下补充材料*仅限合格教师*通过 Pearson Education 受密码保护的教师资源中心（www.pearsonglobaleditions.com/deitel）获取：

- *PowerPoint®幻灯片*，包含正文中的所有代码和插图，以及总结要点的项目符号条目。
- *测试题库*，包含多项选择题（大约每个书中顶级章节两道）
- *解答手册*，包含*大多数*（但不是全部）章末练习的解答。请查看教师资源中心以确定哪些练习有解答。

**请不要给我们写信**请求访问教师资源中心。访问权限仅限于使用本书授课的大学教师。教师只能通过其 Pearson 代表获得访问权限。如果你不是注册教师，请联系你的 Pearson 代表。

对于“项目”练习，*不提供*解答。请查看我们的编程项目资源中心，了解大量额外的练习和项目可能性（http://www.deitel.com/ProgrammingProjects/）。

## 致谢

我们感谢 Abbey Deitel 和 Barbara Deitel 为这个项目投入的长时间工作。Abbey 合著了第 1 章。我们很幸运能与 Pearson 敬业的出版专业团队合作。我们感谢计算机科学执行编辑 Tracy Johnson 的指导、专业见解和精力。Kelsey Loanes 和 Bob Engelhardt 分别出色地管理了评审和生产流程。

## *C语言程序设计（第8版）*审阅者

我们谨感谢审阅者们的努力。在紧迫的截止日期下，他们仔细审阅了正文和程序，并提供了无数改进呈现方式的建议：Brandon Invergo博士（GNU/欧洲生物信息研究所）、Danny Kalev（认证系统分析师、C专家、C++标准委员会前成员）、Jim Hogg（微软公司C/C++编译器团队项目经理）、José Antonio González Seco（安达卢西亚议会）、Sebnem Onsay（奥克兰大学工程与计算机科学学院特别讲师）、Alan Bunning（普渡大学）、Paul Clingan（俄亥俄州立大学）、Michael Geiger（马萨诸塞大学洛厄尔分校）、Jeonghwa Lee（希彭斯堡大学）、Susan Mengel（德克萨斯理工大学）、Judith O'Rourke（纽约州立大学奥尔巴尼分校）以及 Chen-Chih Radhord（河滨大学）。

## *其他近期版本的审阅者*

William Albrecht（南佛罗里达大学）、Ian Barland（拉德福德大学）、Ed James Beckham（Altera）、John Benito（Blue Pilot Consulting, Inc. 和 ISO WG14——负责C编程语言标准的工作组——召集人）、John F. Doyle博士（印第安纳大学东南分校）、Alireza Fazelpour（棕榈滩社区学院）、Mahesh Hariharan（微软）、Hemanth H.M.（SonicWALL软件工程师）、Kevin Mark Jones（惠普）、Lawrence Jones（UGS Corp.）、Don
