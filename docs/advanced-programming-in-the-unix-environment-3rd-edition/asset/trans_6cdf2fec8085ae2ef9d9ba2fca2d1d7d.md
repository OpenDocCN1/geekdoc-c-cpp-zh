

## 8.7 `waitid` 函数

Single UNIX Specification 包含一个额外的函数来检索进程的退出状态。`waitid` 函数与 `waitpid` 类似，但提供了额外的灵活性。

```c
#include <sys/wait.h>

int waitid(idtype_t idtype, id_t id, siginfo_t *infop, int options);
```

返回：成功时返回 0，错误时返回 −1

与 `waitpid` 一样，`waitid` 允许进程指定要等待的子进程。不是将此信息编码到与进程 ID 或进程组 ID 结合的单个参数中，而是使用两个独立的参数。`id` 参数的解释基于 `idtype` 的值。支持的类型总结在图 8.9 中。

| 常量 | 描述 |
|---|---|
| `P_PID` | 等待特定进程：`id` 包含要等待的子进程的进程 ID。 |
| `P_PGID` | 等待特定进程组中的任何子进程：`id` 包含要等待的子进程的进程组 ID。 |
| `P_ALL` | 等待任何子进程：`id` 被忽略。 |

**图 8.9** `waitid` 的 `idtype` 常量

`options` 参数是图 8.10 中所示标志的按位或。这些标志指示调用方感兴趣的状态更改。

| 常量 | 描述 |
|---|---|
| `WCONTINUED` | 等待之前停止且已被继续，并且其状态尚未报告的进程。 |
| `WEXITED` | 等待已退出的进程。 |
| `WNOHANG` | 如果没有可用的子进程退出状态，则立即返回而不是阻塞。 |
| `WNOWAIT` | 不要销毁子进程退出状态。子进程的退出状态可以通过后续调用 `wait`、`waitid` 或 `waitpid` 检索。 |
| `WSTOPPED` | 等待已停止且其状态尚未报告的进程。 |

**图 8.10** `waitid` 的 `options` 常量

`options` 参数中必须至少指定 `WCONTINUED`、`WEXITED` 或 `WSTOPPED` 中的一个。

`infop` 参数是指向 `siginfo` 结构的指针。此结构包含有关导致子进程状态更改而生成的信号的详细信息。`siginfo` 结构在第 10.14 节中进一步讨论。

> 在本书涵盖的四个平台中，只有 Linux 3.2.0、Mac OS X 10.6.8 和 Solaris 10 提供了对 `waitid` 的支持。需要注意的是，Mac OS X 10.6.8 并不会在 `siginfo` 结构中设置我们期望的所有信息。

## 8.8 `wait3` 和 `wait4` 函数

大多数 UNIX 系统实现提供了两个额外的函数：`wait3` 和 `wait4`。历史上，这两个变体源自 UNIX 系统的 BSD 分支。这两个函数提供的唯一特性是 `wait`、`waituid` 和 `waitpid` 函数未提供的额外参数，该参数允许内核返回已终止进程及其所有子进程使用的资源摘要。

```c
#include <sys/types.h>
#include <sys/wait.h>
#include <sys/time.h>
#include <sys/resource.h>

pid_t wait3(int *statloc, int options, struct rusage *rusage);

pid_t wait4(pid_t pid, int *statloc, int options, struct rusage *rusage);
```

两者返回：成功时返回进程 ID，0，或错误时返回 −1

资源信息包括用户 CPU 时间量、系统 CPU 时间量、页面错误数、接收到的信号数等统计信息。有关更多详细信息，请参阅 `getrusage(2)` 手册页。 （此资源信息与我们在第 7.11 节中描述的资源限制不同。）图 8.11 详细说明了 `wait` 函数支持的各种参数。

| 函数 | pid | options | rusage | POSIX.1 | FreeBSD 8.0 | Linux 3.2.0 | Mac OS X 10.6.8 | Solaris 10 |
|---|---|---|---|---|---|---|---|---|
| wait |  |  |  | • | • | • | • | • |
| waitid | • | • |  |  |  |  |  |  |
| waitpid | • | • |  | • | • | • | • | • |
| wait3 |  | • | • |  | • | • | • | • |
| wait4 | • | • | • |  | • | • | • | • |

**图 8.11** 各系统上 wait 函数支持的参数

`wait3` 函数包含在 Single UNIX Specification 的早期版本中。在第 2 版中，`wait3` 被移至遗留类别；在第 3 版中，`wait3` 从规范中删除。

## 8.9 竞态条件

就我们的目的而言，竞态条件发生在多个进程尝试对共享数据执行某些操作时，最终结果取决于进程运行的顺序。`fork` 函数是竞态条件的活跃温床，如果 `fork` 之后执行的任何逻辑在显式或隐式上依赖于 `fork` 后父进程或子进程先运行，则会发生这种情况。一般来说，我们无法预测哪个进程先运行。即使我们知道哪个进程会先运行，在该进程开始运行后发生的事情也取决于系统负载和内核的调度算法。

我们在图 8.8 中的程序中看到了一个潜在的竞态条件，当第二个子进程打印其父进程 ID 时。如果第二个子进程在第一个子进程之前运行，则其父进程将是第一个子进程。但如果第一个子进程先运行并且有足够的时间退出，则第二个子进程的父进程是 `init`。即使调用 `sleep`，如我们所做的那样，也不能保证任何事情。如果系统负载很重，第二个子进程可能在 `sleep` 返回后恢复，而第一个子进程还没有机会运行。此类问题很难调试，因为它们“大多数时候”都能正常工作。

想要等待子进程终止的进程必须调用其中一个 wait 函数。如果进程想要等待其父进程终止，如图 8.8 中的程序所示，可以使用以下形式的循环：

```c
while (getppid() != 1)
    sleep(1);
```

这种类型的循环称为 *轮询*，其问题在于浪费 CPU 时间，因为调用方每秒被唤醒一次以测试条件。

为了避免竞态条件并避免轮询，需要在多个进程之间进行某种形式的信号传递。信号可用于此目的，我们在第 10.16 节中描述了一种方法。各种形式的进程间通信 IPC 也可以使用。我们将在第 15 章和第 17 章中讨论这些选项中的一些。

对于父子关系，我们经常有以下场景。`fork` 之后，父进程和子进程都有事情要做。例如，父进程可以更新日志文件中的记录以包含子进程的进程 ID，而子进程可能必须为父进程创建一个文件。在此示例中，我们要求每个进程在完成初始操作集后通知另一个进程，并且每个进程等待另一个进程完成，然后再继续自己的工作。以下代码说明了此场景：

```c
#include "apue.h"

TELL_WAIT();    /* set things up for TELL_xxx & WAIT_xxx */

if ((pid = fork()) < 0) {
    err_sys("fork error");
} else if (pid == 0) {                 /* child */

    /* child does whatever is necessary ... */

    TELL_PARENT(getppid());      /* tell parent we're done */
    WAIT_PARENT();               /* and wait for parent */

    /* and the child continues on its way ... */

    exit(0);
}

/* parent does whatever is necessary ... */

TELL_CHILD(pid);                 /* tell child we're done */
WAIT_CHILD();                    /* and wait for child */

/* and the parent continues on its way ... */

exit(0);
```

我们假设头文件 `apue.h` 定义了所需的所有变量。五个例程 `TELL_WAIT`、`TELL_PARENT`、`TELL_CHILD`、`WAIT_PARENT` 和 `WAIT_CHILD` 可以是宏或函数。

我们将在后面的章节中展示实现这些 TELL 和 WAIT 例程的各种方法：第 10.16 节展示了使用信号的实现；图 15.7 展示了使用管道的实现。让我们看一个使用这五个例程的示例。

## 示例

图 8.12 中的程序输出两个字符串：一个来自子进程，一个来自父进程。该程序包含竞态条件，因为输出取决于内核运行进程的顺序以及每个进程运行的时间长度。

```c
#include "apue.h"

static void charatatime(char *);

int
main(void)
{
    pid_t   pid;

    if ((pid = fork()) < 0) {
        err_sys("fork error");
    } else if (pid == 0) {
        charatatime("output from child\n");
    } else {
        charatatime("output from parent\n");
    }
    exit(0);
}

static void
charatatime(char *str)
{
    char    *ptr;
    int     c;

    setbuf(stdout, NULL);          /* set unbuffered */
    for (ptr = str; (c = *ptr++) != 0; )
        putc(c, stdout);
}
```

**图 8.12** 具有竞态条件的程序

我们将标准输出设置为无缓冲，因此每次输出字符都会生成一次写入。此示例的目标是尽可能频繁地让内核在两个进程之间切换以演示竞态条件。 （如果我们不这样做，我们可能永远看不到以下类型的输出。看不到错误输出并不意味着

