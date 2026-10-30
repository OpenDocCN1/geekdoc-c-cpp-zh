

I/O 多路复用在 4.2BSD 中通过 select 函数提供。该函数一直以来都能与任何描述符一起工作，尽管其主要用途是终端 I/O 和网络 I/O。SVR3 在添加 STREAMS 机制时加入了 poll 函数。最初，poll 仅适用于 STREAMS 设备。在 SVR4 中，增加了支持以允许 poll 在任何描述符上工作。

## 14.4.1 select 和 pselect 函数

select 函数让我们在所有 POSIX 兼容平台下进行 I/O 多路复用。我们传递给 select 的参数告诉内核

- 我们感兴趣的描述符。
- 我们对每个描述符感兴趣的条件。 （我们想从给定描述符读取吗？我们想向给定描述符写入吗？我们对给定描述符的异常条件感兴趣吗？）
- 我们想等待多长时间。 （我们可以无限等待，等待固定时间，或根本不等待。）

select 返回时，内核告诉我们

- 就绪描述符的总数
- 哪些描述符对每种三种条件就绪（读、写或异常条件）

有了这些返回信息，我们可以调用适当的 I/O 函数（通常是 read 或 write），并且知道该函数不会阻塞。

```
#include <sys/select.h>

int select(int maxfdp1, fd_set *restrict readfds,
    fd_set *restrict writefds, fd_set *restrict exceptfds,
    struct timeval *restrict tvptr);

Returns: count of ready descriptors, 0 on timeout, -1 on error
```

让我们先看最后一个参数。它指定我们想以秒和微秒为单位等待多长时间（回顾第 4.20 节）。有三种情况。

tvptr == NULL

无限等待。此无限等待如果我们捕获到信号则会被中断。返回是在其中一个指定的描述符就绪时或捕获到信号时进行。如果捕获到信号，select 返回 -1 且 errno 设置为 EINTR。

tvptr->tv_sec == 0 && tvptr->tv_usec == 0

根本不等待。所有指定的描述符都会被测试，并立即返回。这是一种轮询系统以了解多个描述符状态而不阻塞在 select 函数中的方法。

tvptr->tv_sec != 0 || tvptr->tv_usec != 0

等待指定的秒数和微秒数。返回是在其中一个指定的描述符就绪时或超时值到期时进行。如果在任何描述符就绪之前超时到期，返回值是 0。 （如果系统不提供微秒分辨率，tvptr->tv_usec 值会向上舍入到最近支持的值。）与第一种情况一样，此等待也可以被捕获的信号中断。

> POSIX.1 允许实现修改 timeval 结构，因此 select 返回后，您不能依赖该结构包含调用 select 前的相同值。FreeBSD 8.0、Mac OS X 10.6.8 和 Solaris 10 都保持结构不变，但 Linux 3.2.0 如果 select 在超时值到期前返回，将用剩余时间更新它。

中间三个参数——readfds、writefds 和 exceptfds——是指向描述符集合的指针。这三个集合指定我们感兴趣的描述符以及针对哪些条件（可读、可写或异常条件）。描述符集合存储在 fd_set 数据类型中。此数据类型由实现选择，以便它可以为每个可能的描述符保存一个位。我们可以将其视为只是位的大数组，如图 14.15 所示。

![](img/244bf0c3b6d0288ae397336907e37851_536_0.png)

### Figure 14.15 Specifying the read, write, and exception descriptors for select

我们能对 fd_set 数据类型做的唯一事情是分配此类型变量，将此类型变量赋给同一类型的另一个变量，或对此类型变量使用以下四个函数之一。

```
#include <sys/select.h>

int FD_ISSET(int fd, fd_set *fdset);

Returns: nonzero if fd is in set, 0 otherwise

void FD_CLR(int fd, fd_set *fdset);
void FD_SET(int fd, fd_set *fdset);
void FD_ZERO(fd_set *fdset);
```

这些接口可以实现为宏或函数。通过调用 FD_ZERO 将 fd_set 设置为全零位。要打开集合中的单个位，我们使用 FD_SET。我们可以通过调用 FD_CLR 清除单个位。最后，我们可以用 FD_ISSET 测试集合中给定位是否打开。

声明描述符集合后，我们必须使用 FD_ZERO 清零集合。然后我们为我们感兴趣的每个描述符设置集合中的位，如下所示

```
fd_set rset;
int fd;

FD_ZERO(&rset);
FD_SET(fd, &rset);
FD_SET(STDIN_FILENO, &rset);
```

select 返回后，我们可以使用 FD_ISSET 测试集合中给定位是否仍打开：

```
if (FD_ISSET(fd, &rset)) {
    :
}
```

select 的中间三个参数（指向描述符集合的指针）中的任何一个（或全部）如果我们对该条件不感兴趣，可以为空指针。如果三个指针都为 NULL，那么我们就拥有比 sleep 提供的更高精度的计时器。 （回顾第 10.19 节，sleep 等待整数秒数。通过 select，我们可以等待小于一秒的时间间隔；实际分辨率取决于系统的时钟。）练习 14.5 显示了这样的函数。

select 的第一个参数 maxfdp1 代表“最大文件描述符加 1”。我们计算我们感兴趣的最高描述符，考虑全部三个描述符集合，加 1，那就是第一个参数。我们可以简单地将第一个参数设置为 FD_SETSIZE，<sys/select.h> 中的一个常量，指定最大描述符数（通常为 1,024），但该值对大多数应用程序来说太大。事实上，大多数应用程序可能使用 3 到 10 个描述符。 （一些应用程序需要更多描述符，但这些 UNIX 程序是不典型的。）通过指定我们感兴趣的最高描述符，我们可以防止内核遍历三个描述符集合中的数百个未使用位，寻找打开的位。

作为示例，图 14.16 显示了如果我们写下以下内容时两个描述符集合的样子

```
fd_set readset, writeset;

FD_ZERO(&readset);
FD_ZERO(&writeset);
FD_SET(0, &readset);
FD_SET(3, &readset);
FD_SET(1, &writeset);
FD_SET(2, &writeset);
select(4, &readset, &writeset, NULL, NULL);
```

重要的是要认识到描述符是阻塞还是非阻塞并不影响 select 是否阻塞。也就是说，如果我们有一个非阻塞描述符想从中读取，并且我们调用 select 超时值为 5 秒，select 将阻塞最多 5 秒。同样，如果我们指定无限超时，select 将阻塞直到描述符有数据准备好或直到捕获到信号。

如果我们在描述符上遇到文件结束，该描述符将被 select 视为可读。当调用 read 并返回 0 时——在 UNIX 系统上表示文件结束的方式。 （许多人错误地认为当文件结束时 select 会指示描述符的异常条件。）

POSIX.1 还定义了 select 的一个变体，称为 pselect。

```
#include <sys/select.h>

int pselect(int maxfd1, fd_set *restrict readfds,
            fd_set *restrict writefds, fd_set *restrict exceptfds,
            const struct timespec *restrict ts,
            const sigset_t *restrict sigmask);
```

Returns: count of ready descriptors, 0 on timeout, -1 on error

pselect 函数与 select 相同，但有以下例外。

- select 的超时值由 timeval 结构指定，但对于 pselect，使用 timespec 结构。 （回顾第 4.2 节中 timespec 结构的定义。）timespec 结构不是以秒和微秒表示超时值，而是以秒和纳秒表示。这提供了更高的分辨率超时，如果平台支持该精细的粒度。
- pselect 的超时值声明为 const，并且我们保证其值不会因调用 pselect 而改变。
- pselect 可选提供信号掩码参数。如果 sigmask 为 NULL，pselect 在信号方面表现得像 select。否则，sigmask 指向一个信号掩码，该掩码在调用 pselect 时原子地安装。返回时，之前的信号掩码将被恢复。

## 14.4.2 poll 函数

poll 函数与 select 类似，但程序员接口不同。该函数最初是在 System V 中引入以支持 STREAMS 子系统，但我们能够将其与任何类型的文件描述符一起使用。

```
#include <poll.h>

int poll(struct pollfd farray[], nfds_t nfds, int timeout);
```

Returns: count of ready descriptors, 0 on timeout, -1 on error

