

在标准发布后才开始进行新功能的工作的“等待期”。因此，对新语言特性的认真工作直到 2002 年才开始。其他原因包括现代语言及其基础库规模的增大。以标准文本页数计，语言增长了约 30%，标准库增长了约 100%。增幅很大程度上源于更详细的规范，而非新功能。此外，对新 C++ 标准的工作显然必须非常小心，不能通过不兼容的更改损害旧代码。委员会必须不破坏的 C++ 代码有数十亿行。

C++11 工作的总体目标为：

- 使 C++ 成为更好的系统编程和库构建语言。
- 使 C++ 更易于教学和学习。

目标已在 [Stroustrup,2007] 中记录并详细说明。

为使并发系统编程类型安全且可移植，投入了大量精力。这涉及内存模型 (§41.2) 和一组用于无锁编程的设施 (§41.3)，主要由 Hans Boehm、Brian McKnight 等人完成。在此基础上，我们添加了 **threads** 库。Pete Becker、Peter Dimov、Howard Hinnant、William Kempf、Anthony Williams 等人做了大量工作。为了提供在基本并发设施之上可以实现的内容示例，我提出了“在不显式使用锁的情况下在任务间交换信息的方式”的工作，这成为 **futures** 和 **async()** (§5.3.5)；Lawrence Crowl 和 Detlef Vollmann 完成了大部分工作。并发是一个需要非常长论文才能完整详细列出谁做了什么以及为什么的领域。在这里，我甚至无法尝试。

## 1.4.4.1 语言特性

将 C++98 扩展为 C++11 所添加的语言特性和标准库设施列表见 §44.2。除了并发支持外，语言的每项新增都可被视为“次要”，但这样做会忽略重点：语言特性旨在组合使用以编写更好的程序。所谓“更好”是指更易读、更易写、更优雅、更不易出错、更易维护、运行更快、消耗资源更少等。

以下是<|message|> 我认为最广泛有用的新“构建砖块”，影响 C++11 代码风格，并附上文本引用及其主要作者：

- 默认值控制：**=delete** 和 **=default**：§3.3.4, §17.6.1, §17.6.4；Lawrence Crowl 和 Bjarne Stroustrup。
- 从其初始化器推导对象类型，**auto**：§2.2.2, §6.3.6.1；Bjarne Stroustrup。我首次于 1983 年设计并实现 **auto**，但因 C 兼容性问题而不得不移除。
- 广义常量表达式求值（包括字面量类型），**constexpr**：§2.2.3, §10.4, §12.1.6；Gabriel Dos Reis 和 Bjarne Stroustrup [DosReis,2010]。
- 类内成员初始化器：§17.4.4；Michael Spertus 和 Bill Seymour。
- 继承构造函数：§20.3.5.1；Bjarne Stroustrup、Michael Wong 和 Michel Michaud。
- Lambda 表达式，即在表达式中使用时隐式定义函数对象的方式：§3.4.3, §11.4；Jaakko Jarvi。
- 移动语义，即在不复制的情况下传递信息的方式：§3.3.2, §17.5.2；Howard Hinnant。
- 声明函数可能不抛出异常的方式 **noexcept**：§13.5.1.1；David Abrahams、Rani Sharoni 和 Doug Gregor。
- 空指针的正式名称，§7.2.2；Herb Sutter 和 Bjarne Stroustrup。
- 范围 **for** 语句：§2.2.5, §9.5.1；Thorsten Ottosen 和 Bjarne Stroustrup。
- 重写控制：**final** 和 **override**：§20.3.4。Alisdair Meredith、Chris Uzdavinis 和 Ville Voutilainen。
- 类型别名，为类型或模板提供别名的机制。特别是，通过绑定另一个模板的一些参数来定义模板的方式：§3.4.5, §23.6；Bjarne Stroustrup 和 Gabriel Dos Reis。
- 具类型且作用域受限的枚举：**enum class**：§8.4.1；David E. Miller、Herb Sutter 和 Bjarne Stroustrup。
- 通用且统一的初始化（包括任意长度的初始化列表和防止窄化）：§2.2.2, §3.2.1.3, §6.3.5, §17.3.1, §17.3.4；Bjarne Stroustrup 和 Gabriel Dos Reis。
- 变参模板，即向模板传递任意数量任意类型参数的机制：§3.4.4, §28.6；Doug Gregor 和 Jaakko Jarvi。

还有许多人值得在此列出。提交给委员会的技术报告 [WG21] 和我的 C++11 FAQ [Stroustrup,2010a] 给出了许多名字。委员会工作组的会议记录中还提及更多。我的名字出现如此频繁（我希望）并非出于虚荣，而是因为我选择从事我认为重要的工作。这些特性将在优秀代码中无处不在。其主要作用是完善 C++ 特性集，以更好地支持编程风格 (§1.2.1)。它们是 C++11 综合的基石。

大量工作投入到一个未进入标准的提案中。“Concepts” 是用于指定和检查模板参数要求的设施 [Gregor,2006]，基于先前研究（例如，[Stroustrup,1994] [Siek,2000] [DosReis,2006]）和委员会的广泛工作。它已被设计、规范化、实现并测试，但委员会以压倒性多数决定该提案尚未准备就绪。如果我们能够完善“concepts”，它将是 C++11 中最重要的单一特性（其唯一竞争者是并发支持）。然而，委员会以复杂性、使用难度和编译时性能为由否决了“concepts” [Stroustrup,2010b]。我认为我们（委员会）对 C++11 的“concepts”做出了正确决定，但该特性确实是“溜走的那一个”。这目前是活跃的研究和设计领域 [Sutton,2011] [Stroustrup,2012a]。

## 1.4.4.2 标准库

成为 C++11 标准库的工作始于一个标准委员会技术报告（“TR1”）。最初，Matt Austern 是库工作组的负责人，后来 Howard Hinnant 接任，直到我们在 2011 年发布最终草案标准。

与语言特性一样，我只列出少数标准库组件，并附上文本引用和最密切相关的人员姓名。更详细的列表见 §44.2.2。一些组件，例如 unordered_map（哈希表），是我们未能及时完成以纳入 C++98 标准的东西。许多其他组件，例如 unique_ptr 和 function，是基于 Boost 库的技术报告（TR1）的一部分。Boost 是一个志愿者组织，旨在基于 STL 提供有用的库组件 [Boost]。

- 哈希容器，如 unordered_map：§31.4.3；Matt Austern。
- 基本并发库组件，如 thread、mutex 和 lock：§5.3, §42.2；Pete Becker、Peter Dimov、Howard Hinnant、William Kempf、Anthony Williams 等人。
- 启动异步计算并返回结果，future、promise 和 async()：§5.3.5, §42.4.6；Detlef Vollmann、Lawrence Crowl、Bjarne Stroustrup 和 Herb Sutter。
- 垃圾回收接口：§34.5；Michael Spertus 和 Hans Boehm。
- 正则表达式库，regexp：§5.5, 第 37 章；John Maddock。
- 随机数库：§5.6.3, §40.7；Jens Maurer 和 Walter Brown。终于到了。我在 1980 年随“C with Classes”发布了第一个随机数库。

一些实用组件在 Boost 中进行了尝试：

- 用于简单高效传递资源的指针，unique_ptr：§5.2.1, §34.3.1；Howard E. Hinnant。这最初称为 move_ptr，本应是 auto_ptr，如果我们在 C++98 时知道如何做的话。
- 用于表示共享所有权的指针，shared_ptr：§5.2.1, §34.3.2；Peter Dimov。这是 Greg Colvin 的 C++98 counted_ptr 提案的继任者。
- tuple 库：§5.4.3, §28.5, §34.2.4.2；Jaakko Jarvi 和 Gary Powell。他们感谢了包括 Doug Gregor、David Abrahams 和 Jeremy Siek 在内的长名单贡献者。
- 通用的 bind()：§33.5.1；Peter Dimov。他的致谢列出了 Boost 的真正名人堂（包括 Doug Gregor、John Maddock、Dave Abrahams 和 Jaakko Jarvi）。
- 用于保存可调用对象的 function 类型：§33.5.3；Doug Gregor。他感谢 William Kempf 等人的贡献。

## 1.4.5 C++ 用途是什么？

到目前为止（2013 年），C++ 无处不在：它在你的电脑、你的手机、你的汽车中，甚至可能在你的相机中。你通常看不到它。C++ 是一种系统编程语言，其最普遍的使用深藏在我们作为用户永远不会查看的基础设施中。

C++ 被数百万程序员在几乎每个应用领域使用。当前部署的 C++ 代码有数十亿行（数千百万行）。这种大规模使用由半打独立实现、数千个库、数百本教科书和数十个网站支持。各种层面的培训和教育广泛可用。

早期应用往往具有强烈的系统编程色彩。例如，

