
# 第 6 章 特别主题：网络与消息传递

```c
struct tcp_info info;
int tisize = sizeof(struct tcp_info);
getsockopt(sockfd, SOL_TCP, TCP_INFO,
&info, (socklen_t *)&tisize);
int cgwin = info.tcpi_snd_cwnd;
```

这是一个大小为字节的结构体。这里的拥塞语法是调用 `getsockopt()`。它的第一个参数是一个套接字（socket）。它可以是服务器与客户端通信使用的 socket，也可以是客户端与服务器使用的 socket。第二个和第三个参数 `SOL_TCP` 和 `TCP_INFO` 要求向 `info` 填充正确类型的信息。当 `getsockopt()` 返回时，`info` 包含了关于丢包、已确认包、重传包等各种信息。在代码段中，拥塞窗口被提取并存储在 `cgwin` 中。

拥塞窗口的限制意味着互联网与带宽之间的连接。图 6.12 显示了两个附近的计算机之间连接的拥塞窗口。拥塞窗口迅速上升并保持在 85 左右。拥塞窗口的上限似乎约为 85。因为拥塞窗口是在传输中的，我们有：

带宽 ≤ 最大拥塞窗口 × MTU/(往返时间的一半)。

对于图 6.12 中附近计算机之间的连接，MTU 大约为 1.5 KB，往返时间为 0.23 毫秒。因此，110 MB/s 是带宽的上限。该网络运行速度接近其宣称的每秒 1 Gigabit比特的峰值。

**练习 6.4.1。** 使用 Pthreads 实现部分服务器的多线程版本。验证你的服务器能够同时为多个客户端服务。

**练习 6.4.2.**** 编写一个 TCP/IP 程序与中央数据库进行同步。假设中央数据库有若干数据项。为了简单起见，你可以禁止删除数据项。每个客户端程序将从客户端更新新的数据项以更新中央数据库，然后下载整个数据库（包括其他客户端推送的项）。

**练习 6.4.3.**** 编写一个去中心化的 TCP/IP 程序，其功能与上一个练习中的程序相似。为了实现去中心化，每个客户端都必须运行一个服务器，接受其他客户端查询其数据库的请求。

## 6.5 参考文献

![](img/2ae76787eef1fc62652846e2a52af15e_518_0.png)

图 6.12：在密歇根大学作者三楼办公室与同一大楼地下室计算机之间测得的拥塞窗口。记录的带宽超过了 100 MB/s。往返延迟似乎为 0.23 毫秒。

- Gropp, S. Huns-Lederman, A. Lumsdaine, E. Lusk, B. Nitberg, W. Saphir, and M. Snir. MPI—The Complete Reference The MPI Extensions, volume 2. MIT Press, Cambridge, Massachusetts, 1998.
- B.J. Hall. Bee’s Guide to Network Programming Using Internet Sockets. Lulu Marketplace, 2009.
- Kandalla, U., J. Keasler, T. Kolev, A. Moody, H. Subramoni, K. Tomko, J. Vienne, B.R. de Supinski, and D.K. Panda. Designing non-blocking allreduce with collective offload on Infiniband clusters: a case study with conjugate gradient solvers. IEEE 26th International Parallel and Distributed Processing Symposium, pages 1156–1167, 2012.
- C.E. Leiserson. Fat-trees: Universal networks for hardware-efficient supercomputing. IEEE Trans. on Computers, 34:892–901, 1985.
- J. Liu, J. Wu, S.P. Kini, P. Wyckoff, and D.K. Panda. High performance RDMA-based MPI implementation over infiniband. International Journal of Parallel Programming, 32:167–198, 2004.
- L.L. Peterson and B. Davie. Computer Networks: A Systems Approach. Morgan Kaufmann, San Francisco, 5th edition, 2010.
- M. Snir, S. Otto, S. Huss-Lederman, D. Walker, and J. Dongarra. MPI—The Complete Reference: The MPI Core, volume 1. MIT Press, Cambridge, Massachusetts, 2nd edition, 1998.
- A.S. Tanenbaum and D.J. Wetherall. Computer Networks. Prentice Hall, Upper Saddle River, 5th edition, 2010.
- T.S. Woodall, G.M. Shipman, G. Bosilca, and A.B. Maccabe. Recent Advances in Parallel Virtual Machine and Message Passing Interface. In Lecture Notes in Computer Science, volume 4192, pages 76–85. Springer, New York, 2006.

# 第 7 章 特别主题：Xeon Phi 处理器

Top 500 组织¹ 自 1993 年以来每年发布一份超级计算机排行榜。这份名单对科学计算做出了巨大贡献。计算机技术的可观利润在于娱乐、日常便利、创造新的热情、强化现有的热情以及商业。科学计算的利润几乎微乎其微。Top 500 带来的广泛关注确保了科学计算没有被大公司忽视。

Top 500 根据使用主元 LU 分解（LINPACK 基准）求解大型线性组时实现的浮点运算（flop）速率对计算机进行排名。计算必须是双精度的。flop 速率从 1993 年的 60 GFLOps/s（6 × 10¹⁰ flops/s）增加到 2015 年的 34 PFlops/s（3.4 × 10¹¹）。列表中列出了 500 台计算机。

科学计算与主流计算之间的关系是共生的，尽管后者占据主导地位。许多与网络、可视化等技术已从主流流向科学计算。

> ¹参见 www.top500.org。

# 第 7 章 特别主题：Xeon Phi 处理器

![](img/2ae76787eef1fc62652846e2a52af15e_521_0.png)

图 7.1：在密歇根大学作者三楼办公室与同一大楼地下室计算机之间测得的拥塞窗口。记录的带宽超过了 100 MB/s。往返延迟似乎为 0.23 毫秒。（注：图 7.1 的 OCR 文本与下方文本重复/根据提供的流进行修正）。*注：OCR 文本存在大量重复和重叠。我将重新处理全文。*

