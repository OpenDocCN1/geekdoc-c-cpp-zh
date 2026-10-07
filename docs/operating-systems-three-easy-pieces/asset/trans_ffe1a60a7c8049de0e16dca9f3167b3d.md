

旁注：伟大的工程师确实非常了不起
像 Jeff Bonwick 这样的工程师（他不仅编写了本文提到的 slab 分配器，还是惊人的文件系统 ZFS 的首席负责人）是硅谷的核心。在几乎任何伟大的产品或技术背后，都有一个（或一小群）他们，才华、能力和奉献精神其实非常平庸。马克·扎克伯格（Facebook 创始人）曾说：“在岗位上表现卓越的人，不仅仅是比表现优秀的人好一点点。他们要强出 100 倍。”这就是为什么直到今天，两个人也可以创立一家改变世界格局的公司（想想 Google、Apple 或 Facebook）。努力工作，你可能也会成为那样 100% 的优秀人才。即使失败了，你一天学到的东西也比大多数人一年的多。slab 分配器还通过将空对象保持在预初始化状态，超越了分离方法。Bonwick 表明，数据结构的初始化和销毁是昂昂的；通过将空对象保持在特定的列表中，slab 分配器避免了每个对象频繁的初始化和销毁周期，从而降低了开销。

## 伙伴分配 (Buddy Allocation)

由于合并（coalescing）对于分配器至关重要，某些方法的设计是围绕使合并简单化的。一个示例是在二进制分配器 [K65] 中。在这样的系统中，空闲内存概念上被认为是一个为 $2^n$ 的大空间。当提出内存请求时，对空闲空间的搜索会递归划分空间，直到找到足够容纳请求的块（进一步拆分将导致空间过小）。此时，请求的块被返回给用户。这里是系统中为 8KB 块划分空闲空间的示例（图 17.8）。在示例中，最左侧的 8KB 块被分配（用较深的灰色表示）并返回给用户；注意，这种方案可能会受到碎片化的影响，但我们允许分配 2 的幂大小的块。伙伴分配的妙之处在于块释放时发生的情况。当将 8KB 块返回空闲列表时，分配器会检查 8KB 的“伙伴”是否空闲；如果是，它会将这两个块合并成一个 16KB 的块。分配器随后检查 16KB 块的伙伴是否仍然空闲；如果是，它将合并这两个块。这种递归合并过程一直持续，直到树恢复了整个空闲空间，或者在发现伙伴被占用时停止。

![](img/13d518e3f694caaead32c569aec49.png)
图 17.8: 伙伴管理堆示例

伙伴分配之所以工作得很好，是因为确定特定块的伙伴非常简单。你问怎么做？想想上面块的地址。如果你想得足够仔细，你会发现每个伙伴的地址仅差一个位；该比特位由伙伴树中的级别决定。因此，你对伙伴分配方案的工作原理有了一个基本的概念。关于更多细节，请像往常一样，参阅 Wilson [W95]。

## 其他想法

上述方法的一个主要问题是它们缺乏可扩展性。具体来说，搜索列表可能非常慢。因此，高级分配器使用更复杂的数据结构来解决这些成本，用简单性换取性能。示例包括平衡二叉树、AVL 树或部分有序树 [W95]。

鉴于现代系统通常有多个处理器并运行多线程工作负载（你将在“并发”章节中详细学习这一点），并不意外人们投入了大量精力使分配器在多处理器系统上良好运行。两个极好的例子可以在 Berger 等人 [B00] 和 Evans [E06] 中找到；查看它们以获取细节。

这些人们随着时间推移对内存分配器提出的数千想法中的两个；如果你感兴趣，可以自行阅读。阅读 glibc 分配器是如何工作的 [S15]，让你对真实世界的情况有一个直观感受。

## 17.5 总结

在本章中，我们讨论了内存分配器的原始形式。此类分配器无处不在，连接到你编写的每一个 C 程序中，也存在于管理自身数据结构的底层操作系统中。对于许多系统来说，构建这样的系统需要进行许多权衡，你对分配器面临的精确工作负载越了解，越能对其进行调优以使其在该工作负载运行得更好。构建一个适用于广泛工作负载的快速、空间高效且可扩展的分配器，仍然是现代计算机系统中面临的持续挑战。

## 参考文献

[B00] "Hoard: A Scalable Memory Allocator for Multithreaded Applications" by Emery D. Berger, Kathryn S. McKinley, Robert D. Blumofe, Paul R. Wilson. ASPLOS IX, November 2000. Berger 等公司为多处理器系统设计的优秀分配器。不仅是一篇有趣的论文，在实践中也得到了使用！

[U94] "The Slab Allocator: An Object-Caching Kernel Memory Allocator" by Jeff Bonwick. USENIX. 94. 一关于如何为操作系统内核构建分配器的免费论文，以及如何针对特定对象大小进行特化的绝佳。

[E06] "A Concurrent Malloc: Implementation for FreeBSD" by Jason Evans, April, 2006. http://freebsd.org/jemalloc/jemalloc.pdf. 详细介绍了如何为多处理器构建现代分配器。它现在被广泛应用，如 FreeBSD、NetBSD、Mozilla Firefox 以及 Facebook 内部。

[K65] "A Fast Storage Allocator" by Knowton. Communications of the ACM, Volume 8, October 1965.

[S15] "Understanding glibc malloc" by sploftun. wordpress.com/2015/understanding-glibc-malloc/.

[W95] "Dynamic Allocation: A Survey and Critical Review" by Paul R. Wilson, Mark S. Johnston, Michael Neely. International Workshop on Memory Management, Scotland, UK, September 1995.

