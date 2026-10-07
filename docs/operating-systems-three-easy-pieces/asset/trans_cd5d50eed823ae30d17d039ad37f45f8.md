

# 调度：
# 多级反馈队列

94

> 提示：尽可能使用建议（ADVICE）
由于操作系统很少知道对于系统中的每一个进程来说什么是最好的，因此提供一些接口允许用户或管理员向操作系统提供一些提示，通常是很有用的。我们通常将此类提示称为“建议（advice）”，因为操作系统并不非要关注它，而是可能会考虑这些建议以做出更好的决策。此类提示在操作系统的许多部分都很有用，包括调度器（例如使用 `nice`）、内存管理器（例如 `madvise`）和文件系统（例如知性预取和缓存 [P-95]）。

# 8.6 MLFQ：总结

我们已经描述了一种名为多级反馈队列（MLFQ）的调度方法。希望你现在能理解它为什么叫这个名字：它具有多个级别的队列，并利用反馈来确定给定作业的优先级。历史是它的指南：关注作业随时间推移的行为以及如何处理它们。

经过精炼的 MLFQ 规则贯穿整个章节，在此列出供你参考：

- 规则 1：如果 Priority(A) > Priority(B)，则 A 运行（B 不运行）。
- 规则 2：如果 Priority(A) = Priority(B)，则 A 和 B 使用队列的时间片（量子长度）以轮询方式运行。
- 规则 3：当一个作业进入系统时，它被放置在最高优先级（最顶部的队列）。
- 规则 4：一旦一个作业在给定层级用完了它的配额（无论它放弃了 CPU 多少次），它的优先级就会降低（即它向下移动到队列）。
- 规则 5：经过一段时间 $S_j$ 后，将系统中的所有作业移动到最顶部的队列。

MLFQ 的趣味之处在于：它并不要求对作业的性质有先验知识，而是观察作业的执行情况并对其划分优先级。通过这种方式，它成功兼顾了这两者的优点：对于短运行的交互式作业提供卓越的性能（类似于 SJF/STCF），并且对于长时间的 CPU 密集型工作负载是公平的并能取得进展。由于这个原因，包括 BSD 衍生版 [LM+89, B86]、Solaris [M06] 以及 Windows NT 及后续的 Windows 操作系统 [CS97] 在内的许多系统使用某种形式的 MLFQ 作为它们的基础调度器。

操作系统
[版本 1.01]

WWW.OSTEP.ORG

# 调度：

# 多级反馈队列

95

# 参考文献

[AD09]Multilevel Feedback Scheduling in Solaris by Andrea Arpaci-Dousseau. Available：http://www.ostep.org/Citations/notes-solaris.pdf。由 Solaris 调度器作者之一编写的一组非常好的笔记。好吧，我们在描述中可能带有偏见，但这些笔记确实非常棒。

[B86]The Design of the UNIX Operating System by M.J. Bach. Prentice-Hall. 一本关于 UNIX 操作系统如何工作的经典老书之一：内核处理程序的必读之目。

[C62]"Experimental Time-Sharing System" by J. F. Corberto, M. D. Daggett, R. C. Daley. IFPRS 1962. 一本难读的书，但它是多级反馈调度中许多早期思想的来源。内存引入 Unix 较晚，有人可以认为它是所有操作系统中影响最大的。

[CS97>"Inside NT" by Helen Cutler and David A. Microsoft Press, 1997. 如果你想学习 Unix 以外的其他知识。当然，你为什么要学这个？好吧，我们在开玩笑；你知道的，你某天真的可能会为微软工作。

[ES95]"An Analysis of Decay-Scheduling in Multiprocessors" by D.H.J. Epema. SIG-METTER 1995。一篇不错的论文，回顾了 20 世纪 90 年代中期，包括对衰减使用调度基本方法的良好概述。

[LM89]"The Design and Implementation of the 4.3BSD Unix Operating System" by S.J. Leifer, M.K. McKus, M.J. Kernels, J.S. Quar. Addison-Wesley, 1989。另一本操作系统经典著作，由 BSD 背后的四位主要人物编写。这本书的其他版本虽然更更新，但无法比拟原版的美感。

[O11]"John Orouster's Home Page" by John Orouster. www.stanford.edu/bouncer/。著名的 Orouster 教授的主页。这本书的两位作者在研究生阶段从 Orouster 处学习了研究生操作系统；这就是他们两人离开学校、成家，甚至写出这本书的地方。因此，你真的可以怪 Orouster 导致了你现在所的困境。

[P95]"Informed Prefetching and Caching" by R.H. Preetch, G.A. Gibson, E. Gint, D. Stodolsky, J. Zelenka. SOSP 95, Copper Mountain, Colorado, October 1995。一篇关于文件系统中一些非常酷的想法的论文，包括应用程序如何向操作系统提供关于正在访问哪些文件以及如何进行规划的建议。

[Y18]"Principled Scalability Analysis for Distributed Storage Systems using Thread Architecture Models" by Suli Yang, Jing Liu, Andrea C. Arpaci-Dusseau, Remzi H. Arpaci-Dusseau. OSDI '18, San Diego, California。我们小组的近期工作展示了在现代分布式存储系统（如 Hive/HDFS, Cassandra, MongoDB 和 Risk）中调度 I/O 请求的困难。如果不加注意，单个用户可能会垄断系统资源。

© 2008-2019, ARPACI-DUSSEAU

三
三个简单的部分

# 课作业（模拟）

此程序 `mlfq.py` 允许你观察本章介绍的 MLFQ 调度器的行为。详情请参阅 README。

# 问题

1. 运行几个只有两个作业和两个队列的随机生成问题；为每个作业计算 MLFQ 执行轨迹。通过限制每个作业的长度并关闭 I/O 来让你的工作更轻松。
2. 你将如何运行调度器以重现章节中的每个示例？
3. 你将如何配置调度器参数使其表现得像一个轮询调度器？
4. 构造一个具有两个作业和调度器参数的工作负载，使得一个作业能够利用旧的规则 4a 和 4b。
5. 经过一段时间 $S_j$ 后，将系统中的所有作业移动到最顶部的队列。给定一个量子长度为 10 ms 的系统，你如何保证一个长时间饥饿的作业至少获得 5% 的 CPU？
6. 调度中的一个问题是将刚完成 I/O 的作业放在队列的哪一。尝试一些工作负载并观察效果。

# 调度：比例份额

在本章中，我们将检查一种不同的调度器类型，称为比例份额（proportional-share）调度器。比例份额基于一个简单的概念：与其优化周转时间或响应时间，调度器可能会保证每个作业获得特定百分比的 CPU 时间。

比例调度的一个卓越案例见于 Waldspurger 和 Weihl的研究 [WW94]，被称为彩票调度（lottery scheduling）；然而，这个想法无疑更老 [KL88]。基本思想非常简单：经常举行抽票以决定下一个运行哪个进程；运行更频繁的进程应该获得更多中奖机会。

但在核心问题之前：

| 如何按比例共享 CPU |
| :--- |
| 我们如何设计一个调度器来按比例方式共享 CPU？实现它的关键机制有哪些？它们效果如何？ |

# 9.1 基本概念：票代表你的份额

彩票调的底层是一个非常基础的概念：票（tickets），用于表示进程（或用户或其他）应该获得的资源份额。进程的票百分比代表了它对所涉及系统资源的份额。

让我们看一个例子。假设有两个进程 A 和 B，并且假设 A 有 75 张票，而 B 只有 25 张。因此，A 获得 75% 的 CPU 而 B 获得剩余 25% 是什么样的。

彩票调度通过概率性（而非确定性地）每隔（例如每个时间片）举行抽票来实现这一点。举行抽票非常简单：调度器必须知道有多少张票（在我们的例子中有 100 张）。调度器然后选取

