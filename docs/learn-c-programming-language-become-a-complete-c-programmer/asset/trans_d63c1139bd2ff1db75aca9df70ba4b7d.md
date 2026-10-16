

一些早期的操作系统是用 C++ 编写的：[Campbell,1987]（学术），[Rozier,1988]（实时），[Berg,1995]（高吞吐量 I/O）。许多当前的操作系统（例如 Windows、Apple 的 OS、Linux 以及大多数便携设备操作系统）都有关键部分是用 C++ 实现的。你的手机和互联网路由器很可能就是用 C++ 编写的。我认为 C++ 对于无妥协的底层效率至关重要。这使我们能够用 C++ 编写设备驱动程序和其他依赖于在实时约束下直接操作硬件的软件。在此类代码中，性能的可预测性至少与原始速度一样重要。往往，结果系统的紧凑性也很重要。C++ 的设计使得每个语言特性都可以在严苛的时间和空间约束下的代码中使用（§1.2.4）[Stroustrup,1994,§4.5]。

当今最显眼且广泛使用的系统中的关键部分是用 C++ 编写的。例子有 Amadeus（航空票务）、Amazon（网络商务）、Bloomberg（金融信息）、Google（网络搜索）和 Facebook（社交媒体）。许多其他编程语言和技术在实现上严重依赖 C++ 的性能和可靠性。例子包括最广泛使用的 Java 虚拟机（例如 Oracle 的 HotSpot）、JavaScript 解释器（例如 Google 的 V8）、浏览器（例如 Microsoft 的 Internet Explorer、Mozilla 的 Firefox、Apple 的 Safari 和 Google 的 Chrome）以及应用程序框架（例如 Microsoft 的 .NET Web 服务框架）。我认为 C++ 在基础设施软件领域具有独特的优势 [Stroustrup,2012a]。

大多数应用程序都有对可接受性能至关重要的代码段。然而，最大的代码量并不在这些段中。对于大多数代码而言，可维护性、易于扩展和易于测试是关键。C++ 对这些问题的支持使其在可靠性至关重要且需求随时间显著变化的领域得到广泛使用。例子有金融系统、电信、设备控制和军事应用。几十年来，美国长途电话系统的中央控制一直依赖 C++，每一次 800 电话（即由被叫方付费的电话）都由 C++ 程序路由 [Kamath,1993]。许多此类应用程序都很大且寿命很长。因此，稳定性、兼容性和可扩展性一直是 C++ 开发中的主要关注点。数百万行 C++ 程序很常见。

## Section 1.4.5 What is C++ used for?

游戏是另一个需要多种语言和工具共存且需要提供无妥协效率的语言（通常在“不寻常”的硬件上）的领域。因此，游戏一直是 C++ 的另一个主要应用领域。

过去所称的系统编程广泛存在于嵌入式系统中，因此在要求苛刻的嵌入式系统项目中大量使用 C++ 并不令人惊讶，包括计算机断层扫描（CAT 扫描仪）、飞行控制软件（例如 Lockheed-Martin）、火箭控制、船舶发动机（例如来自 MAN 的世界上最大的船用柴油发动机的控制）、汽车软件（例如 BMW）以及风力涡轮机控制（例如 Vesta）。

C++ 并不是专门为数值计算而设计的。然而，大量的数值、科学和工程计算是用 C++ 完成的。这主要原因是传统的数值工作通常必须与图形结合，并且与不符合传统 Fortran 模式的数据结构相关的计算结合（例如 [Root,1995]）。我特别高兴看到 C++ 被用于重大的科学事业中，例如人类基因组计划、NASA 的火星探测车、CERN 对宇宙基本原理的探索，以及许多其他项目。

C++ 能够有效地用于需要在多种应用领域工作的应用程序，这是一个重要的优势。涉及本地和广域网络、数值、图形、用户交互和数据库访问的应用程序很常见。传统上，这些应用领域被认为是不同的，并由使用多种编程语言的不同技术社区服务。然而，C++ 在所有这些领域以及更多领域中被广泛使用。它被设计成 C++ 代码可以与用其他语言编写的代码共存。在这里，C++ 几十年来的稳定性也很重要。此外，没有真正的大型系统是 100% 用单一语言编写的。因此，C++ 最初的设计目标——互操作性——变得很重要。

大型应用程序并不是仅用原始语言编写的。C++ 由多种库（超出 ISO C++ 标准库）和工具集支持，例如 Boost [Boost]（可移植基础库）、POCO（Web 开发）、QT（跨平台应用程序开发）、wxWidgets（跨平台 GUI 库）、WebKit（Web 浏览器布局引擎库）、CGAL（计算几何）、QuickFix（金融信息交换）、OpenCV（实时图像处理）以及 Root [Root,1995]（高能物理）。C++ 库有成千上万个，因此不可能全部跟上。

## 1.5 Advice

每一章都包含一个“Advice”部分，其中包含与其内容相关的具体建议。这样的建议是粗略的经验法则，而不是不可改变的法律。建议应仅在合理的情况下应用。没有什么是能替代智力、经验、常识和良好的品味的。

我发现“永远不要这样做”形式的规则没有帮助。因此，大多数建议都表述为做什么的建议。负面建议往往不表述为绝对禁止，我会尝试提出替代方案。我不知道 C++ 的任何主要特性是我没有看到被很好地利用的。“Advice”部分不包含解释。相反，每条建议都附有指向本书相应部分的引用。

首先，这里有一些从 C++ 的设计、学习和历史部分得出的高层次建议：

- [1] 直接在代码中表示思想（概念），例如作为函数、类或枚举；§1.2。
- [2] 目标是让你的代码既优雅又高效；§1.2。
- [3] 不要过度抽象；§1.2。
- [4] 将设计重点放在提供优雅和高效的抽象上，可能以库的形式呈现；§1.2。
- [5] 直接在代码中表示思想之间的关系，例如通过
- [6] 在代码中单独表示独立的思想，例如避免类之间的相互依赖；§1.2.1。
- [7] C++ 不仅仅是面向对象的；§1.2.1。
- [8] C++ 不仅仅是用于泛型编程；§1.2.1。
- [9] 优先选择可以静态检查的解决方案；§1.2.1。
- [10] 使资源显式化（将它们表示为类对象）；§1.2.1, §1.4.2.1。
- [11] 简单的思想要简单地表达；§1.2.1。
- [12] 使用库，尤其是标准库，而不是试图从头开始构建一切；§1.2.1。
- [13] 使用类型丰富的编程风格；§1.2.2。
- [14] 底层代码不一定高效；不要因担心性能问题而避免使用类、模板和标准库组件；§1.2.4, §1.3.3。
- [15] 如果数据有不变式，就封装它；§1.3.2。
- [16] C++ 不仅仅是带少量扩展的 C；§1.3.3。

总的来说：写一个好的程序需要智力、品味和耐心。你不可能第一次就做对。尝试！

## 1.6 References

- [Austern,2003]
- [Barron,1963]
- [Barton,1994]
- [Berg,1995]
- [Boehm,2008]

- [Boost]
- [Budge,1992] Matt Austern et al.: *Untangling the Balancing and Searching of Balanced Binary Search Trees*. Software – Practice & Experience. Vol 33, Issue 13. November 2003.
- D. W. Barron et al.: *The main features of CPL*. The Computer Journal. 6 (2): 134. (1963). comjnl.oxfordjournals.org/content/6/2/134.full.pdf+html.
- J. J. Barton and L. R. Nackman: *Scientific and Engineering C++: An Introduction with Advanced Techniques and Examples*. Addison-Wesley. Reading, Massachusetts. 1994. ISBN 0-201-53393-6.
- William Berg, Marshall Cline, and Mike Girou: *Lessons Learned from the OS/400 OO Project*. CACM. Vol. 38, No. 10. October 1995.
- Hans-J. Boehm and Sarita V. Adve: *Foundations of the C++ concurrency memory model*. ACM PLDI’08.
- The Boost library collection. www.boost.org.
- Kent Budge, J. S. Perry, and A. C. Robinson: *High-Performance Scientific Computation Using C++*. Proc. USENIX C++ Conference. Portland, Oregon. August 1992.

- [C,1990]
- [C,1999]
- [C,2011]
- [C++,1998]
- [C++Math,2010]

