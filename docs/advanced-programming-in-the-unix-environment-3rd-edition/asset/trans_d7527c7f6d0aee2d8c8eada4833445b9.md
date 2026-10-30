

#include <semaphore.h>
int sem_post(sem_t *sem);
返回：如果成功则为 0，错误时为 -1

如果在我们调用 sem_post 时有一个进程阻塞在 sem_wait（或 sem_timedwait）调用中，该进程将被唤醒，并且由 sem_post 刚刚递增的信号量计数会被 sem_wait（或 sem_timedwait）递减。

当我们想在单个进程内使用 POSIX 信号量时，使用无名信号量更容易。这只改变了我们创建和销毁信号量的方式。要创建无名信号量，我们调用 sem_init 函数。

```
#include <semaphore.h>
int sem_init(sem_t *sem, int pshared, unsigned int value);
Returns: 0 if OK, -1 on error
```

pshared 参数指示我们是否计划在多个进程中使用信号量。如果是，我们将其设为非零值。value 参数指定信号量的初始值。

与 sem_open 返回信号量的指针不同，我们需要声明一个类型为 sem_t 的变量并将其地址传递给 sem_init 以进行初始化。如果我们计划在两个进程之间使用信号量，我们需要确保 sem 参数指向进程之间共享的内存范围。

当我们完成对无名信号量的使用后，可以通过调用 sem_destroy 函数将其丢弃。

```
#include <semaphore.h>
int sem_destroy(sem_t *sem);
Returns: 0 if OK, -1 on error
```

调用 sem_destroy 后，除非我们再次调用 sem_init 重新初始化它，否则不能使用任何信号量函数与该 sem。

还有一个函数可用于检索信号量的值。我们为此目的调用 sem_getvalue 函数。

```
#include <semaphore.h>
int sem_getvalue(sem_t *restrict sem, int *restrict valp);
Returns: 0 if OK, -1 on error
```

成功时，valp 参数指向的整数将包含信号量的值。但请注意，信号量的值可能在我们尝试使用刚读取的值时发生变化。除非我们使用额外的同步机制来避免这种竞争，否则 sem_getvalue 函数仅用于调试。

## 示例

引入 POSIX 信号量接口的一个动机是它们可以比现有的 XSI 信号量接口性能显著更好。了解这一目标是否在现有系统中实现是有启发性的，即使这些系统并非设计用于支持实时应用程序。

在图 15.34 中，我们比较了使用 XSI 信号量（不带 SEM_UNDO）和 POSIX 信号量在两个平台（Linux 3.2.0 和 Solaris 10）上，3 个进程竞争分配和释放信号量 1,000,000 次时的性能。

| 操作 | Solaris 10 |  |  | Linux 3.2.0 |  |  |
|---|---|---|---|---|---|---|
|  | 用户 | 系统 | 时钟 | 用户 | 系统 | 时钟 |
| XSI 信号量 | 11.85 | 15.85 | 27.91 | 0.33 | 5.93 | 7.33 |
| POSIX 信号量 | 13.72 | 10.52 | 24.44 | 0.26 | 0.75 | 0.41 |

图 15.34 信号量实现的时间比较

在图 15.34 中，我们可以看到在 Solaris 上，POSIX 信号量仅比 XSI 信号量提高了 12%，但在 Linux 上，改进为 94%（快了近 18 倍）！如果我们跟踪程序，会发现 Linux 的 POSIX 信号量实现将文件映射到进程地址空间并在不使用系统调用的情况下执行单个信号量操作。

## 示例

回顾图 12.5，Single UNIX Specification 并未定义当一个线程锁定普通互斥锁而另一个线程尝试解锁它时会发生什么，但错误检查互斥锁和递归互斥锁会在这种情况下生成错误。由于二进制信号量可以像互斥锁一样使用，我们可以使用信号量来创建自己的锁定原语以提供互斥。

假设我们要创建一个可由一个线程锁定并由另一个线程解锁的锁，我们的锁结构可能如下所示

```
struct slock {
    sem_t *semp;
    char  name[_POSIX_NAME_MAX];
};
```

图 15.35 中的程序展示了基于信号量的互斥原语的实现。

```
#include "slock.h"
#include <stdlib.h>
#include <stdio.h>
#include <unistd.h>
#include <errno.h>
struct slock *
s_alloc()
{
    struct slock *sp;
    static int cnt;
    if ((sp = malloc(sizeof(struct slock))) == NULL)
        return(NULL);
    do {
        sprintf(sp->name, sizeof(sp->name), "%ld.%d", (long)getpid(),
            cnt++);
        sp->semp = sem_open(sp->name, O_CREAT|O_EXCL, S_IRWXU, 1);
    } while ((sp->semp == SEM_FAILED) && (errno == EEXIST));
    if (sp->semp == SEM_FAILED) {
        free(sp);
        return(NULL);
    }
    sem_unlink(sp->name);
    return(sp);
}
void
s_free(struct slock *sp)
{
    sem_close(sp->semp);
    free(sp);
}
int
s_lock(struct slock *sp)
{
    return(sem_wait(sp->semp));
}
int
s_trylock(struct slock *sp)
{
    return(sem_trywait(sp->semp));
}
int
s_unlock(struct slock *sp)
{
    return(sem_post(sp->semp));
}
```

# 图 15.35 使用 POSIX 信号量的互斥

我们基于进程 ID 和计数器创建一个名称。我们不费心用互斥锁保护计数器，因为如果两个竞争的线程同时调用 s_alloc 并最终得到相同的名称，使用 sem_open 调用中的 O_EXCL 标志会使一个成功而另一个以 errno 设为 EEXIST 失败，因此如果发生这种情况我们只需重试。请注意，我们在打开后取消链接信号量。这会销毁名称以便没有其他进程可以访问它，并在进程结束时简化清理。

## 15.11 客户端-服务器属性

让我们详细说明客户端和服务器的一些属性，这些属性受它们之间使用的各种 IPC 类型影响。最简单的关系是让客户端 fork 并 exec 所需的服务器。在 fork 之前可以创建两个半双工管道以允许在两个方向上传输数据。图 15.16 是这种安排的示例。被执行的服务器可以是 set-user-ID 程序，使其具有特殊权限。此外，服务器可以通过查看其真实用户 ID 来确定客户端的真实身份。（回顾第 8.10 节，真实用户 ID 和真实组 ID 在 exec 跨越时不会改变。）

通过这种安排，我们可以构建一个开放服务器。（我们在第 17.5 节展示了这种客户端-服务器机制的实现。）它为客户端打开文件，而不是客户端调用 open 函数。这样，可以在正常的 UNIX 系统用户/组/其他权限之上添加额外的权限检查。我们假设服务器是 set-user-ID 程序，使其具有额外的权限（可能是 root 权限）。服务器使用客户端的真实用户 ID 来确定是否允许其访问请求的文件。这样，我们可以构建一个服务器，允许某些用户拥有他们通常没有的权限。

在此示例中，由于服务器是父进程的子进程，服务器能做的全部就是将文件内容传回父进程。虽然这对于普通文件来说效果很好，但不能用于特殊设备文件等。我们希望服务器能够打开请求的文件并传回文件描述符。虽然父进程可以向子进程传递打开的描述符，但子进程不能将描述符传回父进程（除非使用我们在第 17 章中介绍的特殊编程技术）。

我们在图 15.23 中展示了下一类服务器。服务器是一个守护进程，所有客户端都通过某种形式的 IPC 与其联系。对于这种类型的客户端-服务器安排，不能使用管道。需要一种命名 IPC 形式，例如 FIFO 或消息队列。对于 FIFO，我们看到如果服务器要向客户端发送数据，则还需要每个客户端的单独 FIFO。如果客户端-服务器应用程序仅从客户端向服务器发送数据，则单个众所周知的 FIFO 就足够了。（System V 行式打印机 spooler 使用了这种形式的客户端-服务器安排。客户端是 lpr(1) 命令，服务器是 lpsched 守护进程。使用了单个 FIFO，因为数据流仅从客户端到服务器。没有向客户端发送任何内容。）

消息队列存在多种可能性。

- 1. 服务器和所有客户端之间可以使用单个队列，使用每条消息的类型字段来指示消息接收者。例如，客户端可以使用类型字段为 1 发送其请求。请求中必须包含客户端的进程 ID。然后服务器使用类型字段设置为客户端进程 ID 发送响应。服务器仅接收类型字段为 1 的消息（msgrcv 的第四个参数），客户端仅接收类型字段等于其进程 ID 的消息。
- 2. 或者，每个客户端可以使用单独的消息队列。在向服务器发送第一个请求之前，每个客户端创建自己的消息队列

