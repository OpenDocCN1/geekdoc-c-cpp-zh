

```include <stdio.h>
#include <stdlib.h>
#include <sys/time.h>
#include <sys/types.h>
#include <unistd.h>

int main(void) {
    // open and set up a bunch of sockets (not shown)
    // main loop
    while (1) {
        // initialize the fd_set to all zero
        fd_set readFDs;
        FD_ZERO(&readFDs);

        // set the bits for the descriptors
        // this server is interested in
        // (for simplicity, all of them from min to max)
        int fd;
        for (fd = minFD; fd < maxFD; fd++)
            FD_SET(fd, &readFDs);

        // do the select
        int rc = select(maxFD+1, &readFDs, NULL, NULL, NULL);

        // check which actually have data using FD_ISSET()
        for (fd = minFD; fd < maxFD; fd++)
            if (FD_ISSET(fd, &readFDs))
                processFD(fd);
    }
}
```

图 33.1: 使用 select 的简单代码

描述符集合可能代表（例如）服务器正在关注的所有网络套字。最后，服务器调用 `select()` 来查看哪些连接有可用数据。通过在循环中使用 `FD_ISSET()`，事件服务器可以查看哪些描述符的数据已就绪，并处理传入的数据。

当然，一个真实的服务器会比这复杂得多，并且需要处理发送消息、磁盘 I/O 以及许多其他细节的逻辑。如需更多信息，请参考 Stevens 和 Rago 的 [SR05] API 信息，或参考 Pai 等人或 Welsh 关于事件驱动服务器通用流程的良好概述 [PDZ99, WCB01]。

## 事件驱动并发（进阶）

> 提示：在事件驱动的服务器中不要阻塞
事件驱动的服务器能够对任务调度进行细粒度的控制。然而，为了维持这种控制，不能进行任何会阻塞调用者执行执行的调用；不遵守这一设计提示将导致事件驱动服务器阻塞、客户端感到沮丧，并引发对你是否真的读过书的这部分的严重质疑。

## 33.4 为什么更简单？不需要锁

在使用单个 CPU 和事件驱动应用程序时，并发程序中发现的问题将不再复存在。具体来说，一次只处理一个事件，不需要获取或释放锁；事件驱动的服务器不会被另一个线程中断，因为它是单线程的。因此，线程程序中常见的并发 Bug 在基础的事件驱动方法中并不会表现出来。

## 33.5 一个问题：阻塞系统调用

到目前为止，事件驱动编程听起来很棒，对吧？你编写一个简单的循环，并在事件发生时处理它们。你不需要考虑锁定！但存在一个问题：如果某个事件要求你发出一个可能会阻塞的系统调用怎么办？

例如，想象一个客户端向服务器请求从磁盘读取一个文件并将其内容返回给请求的客户端（类似于简单的 HTTP 请求）。为了处理此类请求，某些事件处理器必须发出 `open()` 调用来打开文件，紧接着是一系列 `read()` 调用来读取文件。当文件被读入内存后，服务器可能会开始将结果发送给客户端。

`open()` 和 `read()` 调用都可能向存储系统发出 I/O 请求（当元数据或数据不在内存中时），并且可能需要很长时间来处理。对于基于线程的服务器来说这不是问题；当发出 I/O 的线程挂起（等待 I/O 完成）时，其他线程可以运行，使服务器取得进展。事实上，这使得基于线程的编程对于 I/O 密集型任务非常自然直接。

然而，对于事件驱动的方法，没有其他线程可以运行：只有主循环。这意味着如果事件处理器发出了一个阻塞调用，整个服务器将只能：直到该调用完成。当事件循环阻塞时，系统就会处于闲置状态，从而造成资源的巨大浪费。在事件驱动系统中有一条必须遵守的规则：不要有阻塞调用。

## 33.6 解决方案：异步 I/O

为了克服这一局限性，许多操作系统引入了发出 I/O 的新方法，统称为异步 I/O。例如，某些系统提供了这样的结构：

```c
struct aiocb {
    int fildes;      // 文件描述符
    off_t offset;     // 偏移量
    void *aio_buf;    // 缓冲区
    size_t aio_bytes; // 传输长度
};
```

在事件驱动系统中，生活并不那么轻松。为了执行相同的任务，我们首先使用上面描述的 AIO 类异步发出读取。假设我们定期使用 `aio.error()` 调用检查读取的完成情况；当它通知我们读取已完成时，事件驱动服务器如何知道该做什么？

