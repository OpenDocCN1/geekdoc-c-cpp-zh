

# 分段

177

## 参考文献

[CV65] "Introduction and Overview of the Multics System" 由 F. J. Corbalo, A. V. Vyssotsky. Fall Joint Computer Conference, 1968. 这是秋季联合计算机会议上关于 Multics 的五篇介绍论文之一；噢，真希望那时我是那房间里的一只苍蝇！

[DD68] "Virtual Memory, Processes, and Sharing in Multics" 由 Robert C. Daley 和 Jack B. Dennis 发表于 Communications of the ACM, Volume 11:5, May 1968. 一篇关于如何在 Multics 中实现动态链接的早期论文，其过程就像时间流动一样简单。随着共享库需求的出现，动态链接在约 20 年前进入系统。书中提到，这些早期的库是 Unix 早期用于动态链接的 retrieve 工具！

[Fac62] "Segment" 由 M. N. Greenfield. Proceedings of the SJCC, Volume 21, 1962. 另一篇关于分段的早期论文；早到它没有引用任何其他文献。

[Hol61] "Program Organization and Record Keeping for Dynamic Storage" 由 A. W. Holt. 发表于 Communications of the ACM, Volume 4:10. 一篇关于分段及其历史背景的令人惊讶且易于阅读的早期论文。

[In64] "86 and IA-32 Architecture Software Developer's Manual" Intel. 2009. 获取地址：http://www.intel.com/products/processors/manuals. 每一章都读到了分段（第3章标题：会让你头疼），像美酒一样需要细品。

[Ke68] "The Art of Computer Programming: Volume I" 由 Donald Knuth. Addison-Wesley, 1968. Knuth 不仅因其早期关于计算机程序艺术的书闻名，还因他在 1983 年 10 月引入的排版系统而闻名。这是关于构建系统的真正参考文献。输入这本书很难。他的著作一直是今天许多计算系统底层算法的极佳早期参考。

[LL83] "Hints for Computer Systems Design" 由 Butler Lamps 发表于 ACM Operating Systems Review，这是一份关于如何构建系统的卓越建议集。坐着很难读完，要像美酒或参考手册一样一次读一点。

[LV82] "Virtual Memory in the VAX/VMS Operating System" 由 Henry M. Levy, P. H. Lipman. 发表于 IEEE Computer, Volume 15:3; March 1982. 一个经典的内存管理系统，设计非常有理。我们将在稍后的章节中详细研究。

[RK68] "Dynamic Storage Allocation Systems" 由 B. Randell 和 J.C. Kuehner. 发表于 Communications of the ACM, Volume 11:5; May 1968. 对分页系统与其他系统之间差异的良好概述，并带有历史背景——

[R69] "A note on storage fragmentation and program segmentation" 由 Brian Randell. 发表于 Communications of the ACM, Volume 12:7; July 1969. 讨论碎片化的早期论文之一——

[W95] "Dynamic Storage Allocation: A Survey and Critical Review" 由 Paul R. Wilson, Mark S. Johnstone, Michael Neel, David Boles. International Workshop on Memory Management, Scotland, UK, September 1995. 一篇关于内存分配器的极佳综述论文。

© 2008-19, ARTIQUES-DUSEAU

三个简单部分

# 作业（模拟）

此程序允许你看到在分段的系统中是如何执行地址翻译的。详情请参见 README。

# 问题

- 1. 首先，让我们用一个微小的地址空间来翻译一些地址。这里有一组带有几个随机种子的简单参数；你能翻译出这些地址吗？

```
segmentation.py -a 128 -p 512 -b 0 -1 20 -B 512 -L 20 -s 0
segmentation.py -a 128 -p 512 -b 0 -1 20 -B 512 -L 20 -s 1
segmentation.py -a 128 -p 512 -b 0 -1 20 -B 512 -L 20 -s 2
```

- 2. 现在，让我们看看我们构建的这个微小地址空间（使用上述参数）。最高虚拟地址是多少？最低的非法地址又是哪里？最后，你如何使用 `-A` 标志运行 `segmentation.py` 来测试你是否正确？

- 3. 假设我们有 16 字节物理内存。为了让模拟器为指定的地址生成以下翻译结果：valid, valid, ..., violation, valid，你会设置什么样的基（base）和界（bounds）？假设参数如下：

```
segmentation.py -a 16 -p 128 -A 0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15 -b ? -s ?
```

- 4. 假设我们想生成一个大约 90% 虚拟地址都是有效的（非违规）的问题。你应该如何配置模拟器来实现这一点？哪些参数是重要的？

- 5. 你能运行模拟器使得没有虚拟地址是有效的吗？怎么做？

空闲空间管理

在本章中，我们将离开对内存虚拟化的讨论，去讨论任何内存管理系统的基本方面，无论是库（管理进程的堆）还是操作系统本身（管理地址空间部分）。具体而言，我们将讨论空闲空间管理。

管理空闲空间可以很简单，正如我们在讨论分页时将看到的那样。当你管理的空间被分为固定大小的单元时是很简单的；在这种情况下，你只需保留这些固定大小单元的列表；当客户端请求其中一个时，返回第一个条目即可。

空闲空间管理变得更加困难（且有趣）的情况是你管理的空闲空间由可变大小的单元组成；这出现在用户级内存分配库（如 `malloc()` 和 `free()`）以及管理物理内存的操作系统中。在任何情况下，存在的问题被称为外部碎片：空闲空间被切分成不同大小的碎片并因此碎片化；随后的请求可能会失败，因为没有单一的连续空间可以满足请求，即使空闲空间总量超过了请求的大小。

![](img/133d518e3f694caaead32569ae6c49_216_0.png)

该图展示了这个问题的例子。在这种情况下，可用的空闲空间为 20 字节；不幸的是，它被碎片化两个 10 字节的块。因此，15 字节的请求将失败。由此我们引出了本章讨论的问题。

# 核心：如何管理空闲空间

在满足可变大小请求时，应该如何管理空闲空间？可以使用哪些策略来减少碎片？其他方法的时间空间开销是什么？

## 17.1 假设

大部分讨论将集中在用户级分配器的历史。我们参考了 Wilson 的优秀综述 [W95]，但鼓励感兴趣的读者查阅原文获取详情：

我们假设有一个类似于 `malloc()` 和 `free()` 提供的基础接口。具体来说，`void malloc(size_t size)` 接收一个参数，即应用程序请求的字节数；它返回一个指向该大小区域的指针（无特定类型，在 C 语言中为空指针）。相应的程序 `free(void *ptr)` 接收指针并释放相应的块。注意这对用户的意义：在释放空间时，并不通知库其大小；库必须在仅收到指针时就能推断出内存块有多大。我们将在本章稍后部分讨论这样做。

该库管理的空间在历史上被称为堆（*heap*），而管理堆中空闲空间的通用数据结构是某种空闲列表（*free list*）。该结构包含受管理区域内所有块的引用。当然，这个数据结构本质上不需要列表，而是某种跟踪空闲空间的数据结构。

我们进一步假设我们关注的是**外部碎片**（external fragmentation），它与**内部碎片**（internal fragmentation）不同；如果分配器分出的内存块大于请求的，则此类块中任何多余（即未使用的）空间都被视为内部碎片（因为浪费发生在分配单元内部），它是空间浪费的另一个例子。为了简单起见，并由于两种碎片类型中外部更有趣，我们将主要关注外部碎片。

我们还假设一旦内存交付给客户端，就无法移动到内存中的另一个位置。例如，如果程序调用 `malloc()` 并获得一个指向堆内空间的指针，那么在程序通过相应的 `free()` 调用返回它之前，该内存区域实际上归程序“所有”（库无法移动它）。因此，空闲空间的压缩是不可能的，这

