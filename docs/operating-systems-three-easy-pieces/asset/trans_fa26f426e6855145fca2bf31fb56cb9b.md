

提示：理解持久性与性能的权衡
存储系统通常向用户呈现持久性与性能之间的权衡。如果用户希望写入的数据能够立即持久化，系统就必须야尽全力将新写入的数据提交到磁盘，这样写入速度就会很慢（尽管如此）。然而，如果用户可以忍受少量数据丢失，系统就可以在内存中缓存写入一段时间，并在稍后（在后台）将它们写入磁盘。这样做可以让写入操作看起来非常快，从而提高性能；但是，如果发生崩溃，未提交到磁盘的写入将将会丢失，这就是权衡的所在。要理解如何正确进行这种权衡，最好的办法是理解使用系统的应用程序需要什么；例如，丢失网页浏览器下载的最后几张图片可能是可以忍受的，但丢失部分向你的账户增加资金的数据库交易可能就不那么好忍受了。当然，除非你非常有钱；如果是那样，你为什么要那么在意积攒那最后的一分钱呢？

某些应用程序（如数据库）并不喜欢这种权衡。因此，为了避免缓存引起的意外丢失，它们简单地通过调用 `fsync()` 强制写入磁盘，通过使用绕过缓存的直接 I/O 接口，或者通过使用原始磁盘接口并完全跳过文件系统。由于系统所做的权衡，有足够的控制措施让系统执行你想要的操作，但默认设置将是不令人满意的。

## 40.8 总结

我们已经看到了构建文件系统所需的机制。每个文件都需要一些信息（元数据），这些信息通常存储在一个称为 `inode` 的结构中。目录只是某种特殊的文件，存储了“名称→inode”的映射。还需要其他结构；例如，文件系统经常使用类似位图（bitmap）的结构来跟踪哪些 `inode` 或数据块是空闲或已分配的。

文件设计的奇之处在于它的自由性；在接下来的章节中，我们将探索如何利用这种自由来优化文件系统的各个方面。显然，我们还有许多策略决策尚未探索。例如，当创建一个新文件时，它应该被放在磁盘的什么位置？这种策略以及其他策略也将是未来章节的主题。它们会吗？

> 去学一下数据库类，了解更多关于老派数据库以及它们过去坚持避免操作系统并控制一切的执念。但要注意！那些数据库类型总是试图坏化操作系统。真丢脸，你们数据库的人们。真丢脸。

伴随着神秘的音乐，让你对文件系统的话题更加感兴趣。

操作系统 [版本 1.01]
WWW.OSTEP.ORG

## 文件实现

## 参考文献

- [A07] "A Five-Year Study of File-System Metadata" Nitin Agrawal, William J. Boloski, John R. Dourcer, Jacob R. Lorch. FAT '07, 加州圣荷塞, 2007年2月。对实际使用的文件系统分析的极佳回顾。利用参考文献可以将文件分析论文的线索追溯到20 世纪 80 年代初。
- [B07] "ZFS: The Last Word in File Systems" Ben Bonwick and Bill Moore。访问地址：http://www.ostep.org/Citations/zfs_last.pdf。最重要的文件系统之一，充满了功能和进步。我们应该就它写一个章节，也许很快就会。
- [B02] "The FAT File System" Andrews Brouwer.2002年9月。在线获取：http://www.fune.net/tui/linux/fs/fat.html。对 FAT 文件系统的很好的描述，不是经典的那种。你必须承认，但 FAT 味道可能更好。
- [C94] "The Windows File System" Helen Custer. 微软出版社, 1994。关于 Windows 文件系统的简短介绍。
- [H88] "Scale and Performance in Distributed File System" David Howard, Michael L. Menees, Robert N. Subramanian, Michael J. West. ACM Transactions, 1988年。
- [P09] "The Unix Time-Sharing System: Internal Layout" Dave Portier.n2.com/papers/unix.
- [RT74] "The Unix Time-Sharing System: Internal Layout" C. Ritchie and D. Thompson. ACM Transactions, 第17卷，1974。
- [S00] "UBC: Unified Buffer Cache" Chuck Silver，2000。
- [S96] "Scalability in XFS" Adam Sweeney, Doug Courville, Wei Hu, Geoff Peck. USENIX '96, 加州圣迭戈。

## 作业（模拟）

使用此工具 `vsfs.py` 来研究随着操作的进行文件系统是如何变化的。模拟从空状态开始，只有根目录。

### 问题

- 1. 使用不同的种子（例如 17, 18, 19）运行模拟器，看看你可以发现什么。
- 2. 现在使用不同的种子（例如 21, 22, 23）并带有 `-r` 参数。
- 3. 现在减少文件系统中数据块的数量到非常低的水平（例如两个），并运行几百次请求。
- 4. 现在这样做，但使用 `inodes`。在 `inode` 很少的情况下，哪些操作可以成功？

## 局部性与快速文件系统

当 UNIX 操作系统首次引入时，Unix 大师 Ken Thompson 编写了第一个文件系统。我们称之为“旧 UNIX 文件系统”，它非常简单。基本上，它的数据结构在磁盘上如下：

| S | Inodes | Data |
|---|---|---|

块（S）包含了整个文件系统的信息：卷有多大、有多少个 `inode`、空闲块列表头的指针等。磁盘的 `inode` 区域包含了文件系统所有的 `inode`。最后，大部分数据由数据块占据。

旧文件系统的优点是它非常简单，并且支持文件系统试图提供的基本抽象：文件和目录层次结构。这套易于使用的系统是过去笨拙的记录存储系统迈出的一步，而目录层次结构也是更早简单的单级层次结构的真正进步。

