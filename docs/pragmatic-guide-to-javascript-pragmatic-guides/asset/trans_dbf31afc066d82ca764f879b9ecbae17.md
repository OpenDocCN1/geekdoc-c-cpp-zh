
SSD 驱动器让整体体验响应迅速。紧随这一现象之后，虚拟机在任何严肃的 Web 开发者的工具箱中都赢得了一席之地。虚拟机软件很便宜，有时甚至免费，可选方案也相当多：Parallels Desktop⁷（适用于 OS X、Windows 和 Linux）、VMware Fusion⁸（适用于 OS X）或 VMware Workstation⁹（适用于 Windows）、Sun 的 VirtualBox¹⁰（几乎适用于所有主流操作系统），以及更多其他选择。

虚拟机的这种商品化让我们能够设置独立的虚拟机，以复制我们需要测试的各种浏览器环境：从 IE6 到 IE9、各种版本的 Safari、Chrome、Firefox、Opera 等等。大多数浏览器不会允许你在单个操作系统上同时运行多个版本；即使允许，你也无法获得与该浏览器作为唯一安装版本时 100% 一致的行为（典型例子：Windows XP 上的第三方 MultipleIE 包）。虚拟机让你可以在不同的操作系统镜像中隔离各个后续版本。最棒的是，它们让你能在一台计算机上完成这一切。通常，首选的主机操作系统是 OS X；这源于许多因素，但对我而言最相关的一点是：在虚拟机中安装 Linux 或 Windows 很容易，但在非 Mac 平台上的虚拟机中运行 OS X 却非常困难。

所以，尽管去使用虚拟机吧！这比不得不使用多台机器或远程桌面要方便得多，在那些场景下你还会不断遇到同时使用这些资源、和你产生冲突的其他 Web 开发者。

## B.8 网络可能是你的敌人

有时你会遇到一些感觉像海森虫（heisenbugs）：¹¹ 的 bug，它们只在你没有盯着的时候出现。一旦你开始单步调试代码，或试图在开发机上重现时，这种难以捉摸的行为就消失得无影无踪。这是怎么回事？

这通常发生在涉及 Ajax 的操作，以及高延迟或不稳定的连接（例如拨号上网，或你的公司代理勉强支撑）时。要重现这类情况，你可以使用被称为慢代理（slow proxy）的软件。在这个领域我最喜欢的工具，也许也是最著名的，就是 Charles¹²，一个基于 Java 的工具（因此可以运行在所有主流平台上）。它不仅能让你限制感知带宽、调整延迟，并整体调节你感知到的网络行为，还可以记录和重放网络会话，并提供详细的 HTTP/HTTPS 监控。这样的工具真是天赐之物！

## JavaScript 框架

JavaScript 本身是一种很棒的语言。但当涉及到与其环境交互时——例如 DOM、CSS 或 XMLHttpRequest，仅举几个最常见的客户端例子——纯 JavaScript 开发就像用几把燧石斧和一堆滑溜溜的原木来建造摩天大楼。这主要是因为两个因素：原始的 DOM 接口缺少合理的高级特性，而且大多数浏览器都以各自非常特别的方式偏离 Web 标准。

正因为如此，涌现出了大量 JavaScript 框架。其中一些获得了足够的动力和追随者，变得非常成熟稳定，接下来我会在本附录中带你了解其中最著名的几个。

请立刻明白这一点：你非常应该使用框架，甚至可能要根据手头的项目或任务使用多个框架。这些框架的源代码很可能比你自己的代码更健壮、测试更充分、文档更完善，支持也更到位。而且它们本来就已存在，可以为你节省无数令人沮丧的开发时间。务实一点！

选择框架是一项重要任务，你应当关注一系列因素。下面这份清单可供参考：

- 它已经存在多久了？代码是否成熟稳定？是否经过了良好的测试？（也就是说，是否有维护完善的测试套件？）
- 它周围是否有强大且活跃的社区？我能轻松找到帮助吗？
- 是否有良好的文档，最好是官方文档？
- 它的 API 设计是否契合我自己的审美？当我使用这个框架时，最终写出的代码是否是我愿意阅读和编写的？
- 该框架是否服务于一组特定的目标？它是否面向特定的开发者群体？如果是，我的目标或我的情况是否吻合？

另一方面，有一个经常被吹捧的标准你其实不必在意：代码库大小。朋友，需要通过慢速方式提供 JavaScript 的时代已经过去了。如今，我们有众多技术可以用来以闪电般的速度提供

一个庞大且注释完善的代码库。这些技术包括去除注释、代码压缩、良好的 HTTP 响应头以帮助浏览器缓存、CDN 分发等等。

流行的框架会使用其中大部分或全部手段，以确保你的页面能瞬间加载它们，所以别再去纠结几 KB 的源代码大小了，好吗？

## C.1 Prototype、script.aculo.us 和 Scripty2

Prototype 是第一个广为人知的 JavaScript 框架。Sam Stephenson 于 2005 年 2 月在 37signals 创建了它，目的是为 DOM 操作、事件处理和 Ajax 提供一个统一、易用的 API。Thomas Fuchs 于 2005 年创建了 script.aculo.us，作为 Prototype 的配套 API，它从著名的 Yellow Fade Technique（黄色淡出技术）发展为一个全套的视觉效果、拖放以及少量基础 UI 控件套件。Scripty2 是 script.aculo.us 的完全重写和扩展版本，目前处于测试阶段，非常专注于视觉效果。

Prototype 背后的团队以一个约六名志愿者的核心层为中心而波动，其中最突出的是 Sam、Tobie Langel 和 Andrew Dupont。它基于 MIT 许可证发布（基本上就是开源且可随处使用），完整源代码可在 GitHub 上浏览、分叉和修改，并配有反馈邮件列表和 Bug 报告系统。

围绕 Prototype 已经形成了一个生态系统，包括 PDoc（一个代码内联文档系统）、Evidence（一个单元测试框架）、Sprockets（一个高级 JavaScript 处理和拼接工具）和 Scripteka（一个插件仓库）。社区活跃而富有生气，主要集中在 Google Groups 上。相关书籍已有不少；迄今为止，最新的是 Andrew Dupont 的 *Practical Prototype and script.aculo.us* [Dup08]，以及本人所著的 *Prototype and script.aculo.us* [Por07]。

虽然 Prototype 通常被认为是第一个广为人知的 JavaScript 框架，但在过去两年里，它的受欢迎程度已在缓慢下滑，显然是在向 jQuery 转移。不过，我相信这两个框架满足的是不同（尽管有重叠）的需求集（而且它们的代码美学当然也截然不同）。

Prototype 的架构、代码美学和连贯的 API 设计非常适合那些拥有健壮 API 的重要代码库，它把 Ruby 的许多优点（比如 Enumerable 模块）“移植”了过来，让大量算法密集型的代码易于编写。它是一个适合那些想拥抱 JavaScript 并用它写出精彩作品、随时间推移不断成长和维护

> 1. 不过要避免代码*混淆*，否则在其之上调试的人会恨你。

应用程序代码库的人。所以，对于只是想实现某个功能，或者在不怎么了解这门语言的情况下就用组件和插件拼凑一个网站的人来说，它很可能不是最佳选择。

以下是撰写本文时各版本的最新概况，以及你可能会用到的网址：

- Prototype 位于 [http://prototypejs.org/](http://prototypejs.org/)；其当前版本是 1.7。
- script.aculo.us 位于 [http://script.aculo.us/](http://script.aculo.us/)（显而易见！）；其当前版本是 1.8.3，开发基本上已冻结，因为重心已转向 Scriptaculous2。
- Scriptaculous2 可以在 [http://scriptly2.com/](http://scriptly2.com/) 找到。它目前处于 Alpha 6 版。
- PDoc 位于 [http://pdoc.org/](http://pdoc.org/)。
- Sprockets 位于 [http://getsprockets.org/](http://getsprockets.org/)。
- Scripteka 位于 [http://scripteka.com/](http://scripteka.com/)。
- 支持邮件列表位于 [http://groups.google.com/group/prototype-scriptaculous](http://groups.google.com/group/prototype-scriptaculous)。你也可以尝试 Freenode 上的 #prototype IRC 频道。
- 反馈邮件列表位于 [http://groups.google.com/group/prototype-core](http://groups.google.com/group/prototype-core)。请不要在那里寻求帮助——请使用支持列表！
- 官方仓库在 GitHub 上：[http://github.com/sstephenson/prototype](http://github.com/sstephenson/prototype)。
- 如果你要报告 Bug，请先阅读 [http://prototypejs.org/contribute](http://prototypejs.org/contribute) 上的指南，认真准备报告，然后前往 [https://prototype.lighthouseapp.com/](https://prototype.lighthouseapp.com/)。

## C.2 jQuery 与 jQuery UI

jQuery 起源于 2005 年 8 月。当时 John Resig 在使用 Prototype 之后，决定尽管他喜欢它的特性、API 和代码的整体感觉，但它并不完全符合自己的口味。于是，他开始尝试一些不同的东西。John 是 Mozilla 的一位友善的 JavaScript 大师，所以可以说，他开发一个框架是顺理成章的事。在 2006 年 6 月发布 1.0 版本之后，jQuery 得益于大量社区驱动的工作，在过去两年里迅速普及。jQuery 项目于 2009 年 9 月正式组建，其 1.4 版本于 2010 年 1 月发布，发布之际还举行了两周的在线庆祝和编程狂欢。（截至撰写本文时，当前版本是 1.4.2。）
