

## 43.12 崩溃恢复与日志

最后一个问题：如果系统在 LFS 向磁盘写入时发生崩溃会怎样？正如你在上一章关于日志（journaling）中所提到的，更新过程中的崩溃对于文件系统来说是非常棘手的，因此 LFS 也必须考虑这个问题。

在正常运行期间，LFS 在段（segment）中缓冲写入，然后（当段满，或经过了一段时间后）将该段写入磁盘。LFS 将这些组织在日志中，检查点区域（checkpoint region，CR）指向头部和尾部段，每个段指向下一个要写入的段。LFS还会定期更新检查点区域。崩溃显然可能发生在这些操作（写入段或写入磁盘）的期间。那么 LFS 是如何处理这些崩溃的呢？

让我们来看第二种情况。为了确保 CR 的更新是原子的，LFS 创建了两个 CR，分别位于磁盘的两个端，并交替写入它们。在更新带有 inode 映射和其他信息的 CR 时，LFS 实现了一套严谨的协议：首先写入头文件（带有时间戳），然后是 CR 的主体，最后是结尾（也带有时间戳）。如果系统在 CR 更新期间发生崩溃，LFS 可以通过发现时间戳不一致来检测到这一点。LFS 始终会选择时间戳一致的最新 CR，从而实现 CR 的一致更新。

现在让我们处理第一种情况。因为 LFS 每大约 30 秒就会崩溃一次，文件系统的快照可能非常旧。因此，在重启后，LFS 可以通过简单地读取检查点区域来恢复文件；然而，最后的更新将会丢失。

为了改进这一点，LFS 尝试通过一种名为“前滚”（roll forward）的技术来重建许多段。其基本思想是是从检查点区域开始，找到日志的末尾（包含在 CR 中），然后利用它读取后续段并查看是否有任何更新。如果有，LFS 就会相应地更新文件系统，并恢复自上次检查点以来写入的大部分数据和元数据。详情请参阅 Rosenblum 获奖的论文。

## 43.13 总结

LFS 引入了更新磁盘的新方法。LFS 不再在原地写入，而是始终写入磁盘的未使用部分，然后回收该空间。这种方法在数据库系统中被称为影子分页（shadow paging）[L77]，在文件系统术语中被称为写时复制（copy-on-write），它实现了高效写入，因为 LFS 可以将所有更新汇集在内存段中，然后顺序将它们写入。

### 提示：化缺陷为优势

每当你的系统存在缺陷时，看看是否能将其转化为有用的东西。NetApp 的 WAFL 在旧文件上就是这样做；通过让旧版本可用，WAFL 不再需要频繁担心清理（尽管它最终会在后台删除旧版本），并提供了一个酷炫的功能。还有其他例子吗？无疑是有的，但你必须自己思考，因为这一章已经彻底结束了（over with a capital “O”）。LFS 生成的大型写入对于许多不同设备的性能都是极佳的。在硬盘上，大写写入确保了寻道次数最小化；在基于校验的 RAID（如 RAID-4 和 RAID-5）上，它们完全避免了小写问题。最近关于闪存 SSD 的研究 [H17]；因此，令人的是，LFS 风格的文件系统可能是这些新介质的极佳选择。这种方法的缺点是会产生垃圾；数据的旧副本散落在整个磁盘上，如果想为后续使用留出空间，必须定期清理段。特别是，WAFL 通过在意外删除时通过快照提供文件系统的旧版本，将清理问题转化为一个功能得以解决。

## 参考文献

- [AD14] "Operating Systems: Three Easy Pieces"（章节：Flash-based State Drives），作者 Remzi Arpacci-Dousseau 和 Andrea Arpacci-Dousseau。Books, 2014。向你推荐这本书的其他章节可能略显生兀，但我们又凭什么判断呢？
- [B07] "ZFS: The Last Word in Files"，作者 Johnwick 和 Bill Moore。可用：http://www.ostep.org/citations/zfs_last.pdf。关于 ZFS 的幻灯片；没有免费的 ZFS 论文吗？（也许你会写一篇，到时候我们可以在这里引用它吗？）
- [H17] "The Unwritten Contract of State Drives"，作者 Jun He, Sudan Khanna, Andrea C. Arpacci-Dousseau, Remzi H. Arpacci-Dousseau，EuroSys 17, 2017。当写作者不努力从 SSD 中提取性能时，扩展性（或并行请求）和延迟最为重要。事态在变化——
- [HLM94] "File System for NFS Server"，作者 Dave Hines, James Lu, Michael Mahmood。USENIX 94。WAFL 吸取了 LFS 和 RAID 的许多思想，并将其应用于价值数十亿美元的公司 NetApp 的高速 NFS 中。
- [L77] "Physical Integrity in a Segmented Database"，作者 R. Lorie。ACM Transactions on Databases, 第 2 卷，1 (1977)。这里介绍了分页的原始想法。
- [M94] "A File System for UNIX"，作者 Robert K. McKusick, William N. Joy, Sam J. Lee, Robert S. Fabry，ACM TOC, 第 3 卷，1994 年 8 月。免费的 LFS 论文：更多细节请看 CFS。
- [MR97] "Improving the Performance of Log-Structured File Systems with Adaptive Methods"，作者 Jeanna Neefe Mathews, Remzi Dousseau, Adam M. Castro, Randolph Y. Wang, Thomas E. Anderson，SOSP '1997, 第 228–235 页，圣 Mayo，蒙特利尔。一篇较新的论文为 lfs 提供了更好的清理策略。
- [P98] "Hardware Trends and Database Opportunities"，作者 David D. Patterson。SIGMOD '98, Keynote, 5 月 4 日。幻灯片见：http://www.berkeley.edu/patterns/keynote.html。一组关于计算机系统趋势的精彩幻灯片。希望 Patterson 很快会创作另一一组。
- [R91] "Design and Implementation of the Log-Structured File System"，作者 Mendel Rosenblum 和 John Ousterhout。SOSP '91，加州太平洋园林，1991 年 10 月。关于 lfs 的原始 SOSP 论文已被数百篇其他论文引用，并启发了现代系统。
- [R92] "Design and Implementation of the Log-Structured File System"，作者 Mendel Rosenblum。http://www.berkeley.edu/Pubs/TechIPS/TechIPS-92-068.pdf。lfs 的获奖论文。
- [SS95] "File system using clustering: a performance comparison"，作者 Marco Selger, Keith A. Smith, Hari Balakrishnan, June Chang, Sara Menschae, Venkatesan Podabaman。USENIX 1995，路易斯安那州，1995 年。一篇显示 LFS 性能影响最严重的论文，特别是频繁调用 fsync() 时（例如数据库工作负载）。
- [S90] "Write-Disk Caching"，作者 James A. Sun, Susan Cyr, Cyril. Orji。SIGMOD '90，纽约，1990 年 5 月。关于软件缓存及其收益的早期研究。然而，缓存过久会有害：详见 [M94]。
- [Z12] "Deirection for Flash-based SSDs with Nameless Writes"，作者 Yiyang Zhang, Prash Prath Arul, Andrea C. Arpacci-Dousseau, Remzi H. Arpacci-Dousseau。FAST 13，加州圣何塞，2013 年 2 月。关于构建闪存存储设备的新方法的论文，以避免文件系统和 FTL 中冗余映射。其思想是由设备选择写入的物理位置，并将地址返回给文件系统，其中-

