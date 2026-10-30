

| 头文件 | FreeBSD 8.0 | Linux 3.2.0 | Mac OS X 10.6.8 | Solaris 10 | 描述 |
|---|---|---|---|---|---|
| \<aio.h\> | • | • | • | • | 异步 I/O |
| \<cpio.h\> | • | • | • | • | cpio 归档值 |
| \<dirent.h\> | • | • | • | • | 目录条目（第 4.22 节） |
| \<dlfcn.h\> | • | • | • | • | 动态链接 |
| \<fcntl.h\> | • | • | • | • | 文件控制（第 3.14 节） |
| \<fnmatch.h\> | • | • | • | • | 文件名匹配类型 |
| \<glob.h\> | • | • | • | • | 路径名模式匹配和生成 |
| \<grp.h\> | • | • | • | • | 组文件（第 6.4 节） |
| \<iconv.h\> | • | • | • | • | 编码转换实用程序 |
| \<langinfo.h\> | • | • | • | • | 语言信息常量 |
| \<monetary.h\> | • | • | • | • | 货币类型和函数 |
| \<netdb.h\> | • | • | • | • | 网络数据库操作 |
| \<nl_types.h\> | • | • | • | • | 消息目录 |
| \<poll.h\> | • | • | • | • | poll 函数（第 14.4.2 节） |
| \<pthread.h\> | • | • | • | • | 线程（第 11 章和第 12 章） |
| \<pwd.h\> | • | • | • | • | 密码文件（第 6.2 节） |
| \<regex.h\> | • | • | • | • | 正则表达式 |
| \<sched.h\> | • | • | • | • | 执行调度 |
| \<semaphore.h\> | • | • | • | • | 信号量 |
| \<strings.h\> | • | • | • | • | 字符串操作 |
| \<tar.h\> | • | • | • | • | tar 归档值 |
| \<termios.h\> | • | • | • | • | 终端 I/O（第 18 章） |
| \<unistd.h\> | • | • | • | • | 符号常量 |
| \<wordexp.h\> | • | • | • | • | 单词扩展定义 |
| \<arpa/inet.h\> | • | • | • | • | Internet 定义（第 16 章） |
| \<net/if.h\> | • | • | • | • | 套接字本地接口（第 16 章） |
| \<netinet/in.h\> | • | • | • | • | Internet 地址族（第 16.3 节） |
| \<netinet/tcp.h\> | • | • | • | • | 传输控制协议定义 |
| \<sys/mman.h\> | • | • | • | • | 内存管理声明 |
| \<sys/select.h\> | • | • | • | • | select 函数（第 14.4.1 节） |
| \<sys/socket.h\> | • | • | • | • | 套接字接口（第 16 章） |
| \<sys/stat.h\> | • | • | • | • | 文件状态（第 4 章） |
| \<sys/statvfs.h\> | • | • | • | • | 文件系统信息 |
| \<sys/times.h\> | • | • | • | • | 进程时间（第 8.17 节） |
| \<sys/types.h\> | • | • | • | • | 原始系统数据类型（第 2.8 节） |
| \<sys/un.h\> | • | • | • | • | UNIX 域套接字定义（第 17.2 节） |
| \<sys/utsname.h\> | • | • | • | • | 系统名称（第 6.9 节） |
| \<sys/wait.h\> | • | • | • | • | 进程控制（第 8.6 节） |

图 2.2 POSIX 标准定义所需的头文件

每个功能区域并突出显示描述标准各方面的文本，这些方面取决于特定选项的支持。许多选项涉及实时扩展。

POSIX.1 不包括超级用户的概念。相反，某些操作需要“适当的权限”，尽管 POSIX.1 将此术语的定义留给实现。符合美国国防部安全指南的 UNIX 系统具有多个安全级别。在本文中，我们使用传统的术语，并将需要超级用户权限的操作称为需要超级用户权限。

| 头文件 | FreeBSD 8.0 | Linux 3.2.0 | Mac OS X 10.6.8 | Solaris 10 | 描述 |
|---|---|---|---|---|---|
| \<fmtmsg.h\> | • | • | • | • | 消息显示结构 |
| \<ftw.h\> | • | • | • | • | 文件树遍历（第 4.22 节） |
| \<libgen.h\> | • | • | • | • | 路径名管理函数 |
| \<ndbm.h\> | • | • | • | • | 数据库操作 |
| \<search.h\> | • | • | • | • | 搜索表 |
| \<syslog.h\> | • | • | • | • | 系统错误日志（第 13.4 节） |
| \<utmpx.h\> | • | • | • | • | 用户记账数据库 |
| \<sys/ipc.h\> | • | • | • | • | IPC（第 15.6 节） |
| \<sys/msg.h\> | • | • | • | • | XSI 消息队列（第 15.7 节） |
| \<sys/resource.h\> | • | • | • | • | 资源操作（第 7.11 节） |
| \<sys/sem.h\> | • | • | • | • | XSI 信号量（第 15.8 节） |
| \<sys/shm.h\> | • | • | • | • | XSI 共享内存（第 15.9 节） |
| \<sys/time.h\> | • | • | • | • | 时间类型 |
| \<sys/uio.h\> | • | • | • | • | 向量 I/O 操作（第 14.6 节） |

图 2.3 POSIX 标准定义 XSI 选项头文件

经过二十多年的工作，标准已经成熟稳定。POSIX.1 标准由一个名为 Austin Group 的开放工作组维护（http://www.opengroup.org/austin）。为了确保它们仍然相关，标准需要不时更新或重新确认。

## 2.2.3 单一 UNIX 规范

单一 UNIX 规范是 POSIX.1 标准的超集，指定了扩展 POSIX.1 规范提供的功能的额外接口。POSIX.1 等同于单一 UNIX 规范的 Base Specifications 部分。

POSIX.1 中的 X/Open System Interfaces（XSI）选项描述了可选接口，并定义了实现要被视为 XSI 兼容必须支持的 POSIX.1 的可选部分。这些包括文件同步、线程栈地址和大小属性、线程进程共享同步以及 \_XOPEN_UNIX\_ 符号常量（在图 2.5 中标记为“SUS 强制”）。只有 XSI 兼容的实现才能称为 UNIX 系统。

> Open Group 拥有 UNIX 商标，并使用单一 UNIX 规范来定义实现必须支持的接口才能自称为 UNIX 系统。供应商必须提交符合性声明，通过测试套件验证符合性，并获得使用 UNIX 商标的许可。

| 头文件 | FreeBSD 8.0 | Linux 3.2.0 | Mac OS X 10.6.8 | Solaris 10 | 描述 |
|---|---|---|---|---|---|
| \<mqueue.h\> | • | • |  | • | 消息队列 |
| \<spawn.h\> | • | • | • | • | 实时 spawn 接口 |

图 2.4 POSIX 标准定义的可选头文件

单一 UNIX 规范的第一个版本由 X/Open 于 1994 年发布。它也被称为“Spec 1170”，因为它包含大约 1,170 个接口。它源于 Common Open Software Environment（COSE）倡议，其目标是提高 UNIX 操作系统所有实现之间的应用程序可移植性。COSE 组织——Sun、IBM、HP、Novell/USL 和 OSF——通过包含通用商业应用程序使用的接口，超越了认可标准。由此产生的 1,170 个接口选自这些应用程序，并还包括 X/Open Common Application Environment（CAE），Issue 4（历史上称为“XPG4”，是对其前身 X/Open Portability Guide 的历史参考）、System V Interface Definition（SVID），第 3 版，第 1 级接口，以及 OSF Application Environment Specification（AES）完整使用接口。

单一 UNIX 规范的第二个版本由 The Open Group 于 1997 年发布。新版本增加了对线程、实时接口、64 位处理、大文件和增强的多字节字符处理的支持。

单一 UNIX 规范的第三个版本（SUSv3）由 The Open Group 于 2001 年发布。SUSv3 的 Base Specifications 与 IEEE 标准 1003.1-2001 相同，并分为四个部分：Base Definitions、System Interfaces、Shell and Utilities 和 Rationale。SUSv3 还包括 X/Open Curses Issue 4，Version 2，但该规范不是 POSIX.1 的一部分。

2002 年，ISO 将 IEEE 标准 1003.1-2001 批准为国际标准 ISO/IEC 9945:2002。The Open Group 于 2003 年再次更新了 1003.1 标准以包含技术更正，ISO 将其批准为国际标准 ISO/IEC 9945:2003。2004 年 4 月，The Open Group 发布了单一 UNIX 规范，版本 3，2004 版。它将更多技术更正合并到标准正文中。

2008 年，单一 UNIX 规范进行了更新，包括更正和新接口，删除了过时接口，并将其他接口标记为过时以备将来删除。此外，一些以前可选的接口被提升为非可选状态，包括异步 I/O、屏障、时钟选择、内存映射文件、内存保护、读写锁、实时信号、POSIX 信号量、自旋锁、线程安全函数、线程、超时和计时器。由此产生的标准被称为 Base Specifications 的第 7 版，与 POSIX.1-2008 相同。The Open Group 将此版本与更新的 X/Open Curses 规范捆绑在一起，并于 2010 年作为单一 UNIX 规范的第 4 版发布。我们将其称为 SUSv4。

## 2.2.4 FIPS

FIPS 代表 Federal Information Processing Standard。它由美国政府发布，用于计算机系统的采购。FIPS 151-1（1989 年 4 月）基于 IEEE 标准 1003.1-1988 和 ANSI C 标准的草案。随后是 FIPS 151-2（1993 年 5 月），基于 IEEE 标准 1003.1-1990。FIPS 151-2 要求 POSIX.1 列为可选的一些功能。所有这些选项在 POSIX.1-2001 中都被列为强制。

