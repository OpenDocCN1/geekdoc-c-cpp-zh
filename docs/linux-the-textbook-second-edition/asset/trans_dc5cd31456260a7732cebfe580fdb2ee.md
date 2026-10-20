

## 表 16.2

fork() 系统调用失败的原因

| 失败原因 | errno 的值 |
|---|---|
| 将超过系统上可同时运行的最大进程数限制 | EAGAIN |
| 将超过单个用户下可运行的最大进程数限制 | EAGAIN |
| 已达到为进程设置的资源限制 | EAGAIN |
| 新进程的交换空间不足 | ENOMEM |

任一进程在另一个进程中都是可见的。因此，如果任一进程从已打开的文件中读取 N 字节，文件指针将增加 N，父进程或子进程的下一次读取或写入操作将在文件指针的新位置执行。

fork() 调用可能因表 16.2 中列出的原因而失败。

vfork() 系统调用是 fork() 的一个轻量级版本。它像 fork() 一样创建子进程，但不会复制父进程的地址空间；它按需复制地址空间——即当需要子进程的内存映像时。vfork() 系统调用替代 fork() 使用，尤其是在子进程创建后立即使用 execve() 系统调用（或其变体）或 exec1() 库调用（或其变体）用另一个可执行代码覆盖自身的情况下。这常见于诸如 shell 程序之类的应用程序中，这些程序在 fork() 之后立即使用 exec() 调用（exec1()、execve()、fexecve() 等）来执行外部命令。exec() 调用将在本章后面介绍。

## 练习 16.9

如果你浏览 fork() 系统调用的手册页，会看到 vfork() 和 rfork() 调用的名称。这些调用各有什么用途？

## 16.3.3 向父进程报告状态

Linux 进程通过 _exit() 系统调用或 exit() 库调用向父进程报告其终止状态。由于大多数程序员使用 exit() 调用来终止进程，因此我们将在全书讨论它。进程通过 exit() 调用的唯一参数将其终止状态传递给父进程，通常为 0 或 1。值 0 用于表示进程成功完成，值 1 表示进程终止失败。

父进程通过使用 wait() 类的系统调用（参见 16.3.4 节）来接收此状态。实际上，终止进程的状态保存在该进程的 proc 结构中。分配给该进程的所有数据结构和资源都会被释放，除了其 proc 结构。在父进程读取了子进程的退出状态后，proc 结构才被释放回内核。如果进程未使用 exit() 调用终止自身，内核会自动将进程的终止状态发送给其父进程。

请注意，子进程和父进程通过 exit() 和 wait() 系统调用会合，父进程在此会合中接收子进程的退出状态及其终止原因。这是 Linux 中最简单的进程间通信形式。通过为 exit() 参数赋予不同的含义，子进程可以向父进程传递有意义的消息。我们将在第 W20 章详细讨论 Linux 进程之间的通信问题。

## 16.3.4 收集子进程的状态

进程可以使用 wait() 系统调用等待子进程终止并了解其终止原因。进程可以使用 waitpid() 系统调用等待特定子进程的终止。以下是这些系统调用的简要说明：

```
#include <sys/types.h>
#include <sys/wait.h>
pid_t wait(int *status);
pid_t waitpid(pid_t wpid, int *status, int options);

**成功：** 子进程的 PID
**失败：** -1，并且内核变量 errno 被设置为指示错误类型
```

wait() 调用可能因多种原因失败。表 16.3 列出了其中一些原因。

程序员可以通过检查 status 参数的值来解读子进程的终止状态及其终止相关的附加信息，例如进程是否因信号而终止。如图 16.7 所示，退出状态和进程终止的原因存储在 status 中。低字节包含进程终止的原因，高字节包含退出状态。如果进程在接收信号时终止，信号编号存储在 status 变量的低字节中。因此，例如，如果进程因 <Ctrl+C>（键盘中断）而终止，低字节包含 SIGINT（即值 2）。

随着时间的推移，Linux 设计者增加了许多 wait() 调用的变体。wait() 系统调用是最古老的，而 waitpid() 是这些调用中限制最严格的。最新且最广泛的接口是 wait6() 系统调用。对 wait3()、wait4() 和 wait6() 的详细讨论超出了本书的范围。以下是 wait3() 和 wait4() 调用的简要说明：

```
#include <sys/types.h>
#include <sys/wait.h>
#include <sys/time.h>
#include <sys/resource.h>
pid_t wait3(int *status, int options, struct rusage *rusage);
pid_t wait4(pid_t wpid, int *status, int options, struct rusage *rusage);

**成功：** 子进程的 PID
**失败：** -1，并且内核变量 errno 被设置为指示错误类型
```

wait4() 系统调用指示进程等待特定的子进程并检索其资源使用统计信息。如表 16.4 所示，wait4() 和 waitpid() 调用中的 wpid 参数决定了父进程等待哪个（或哪些）子进程。

wait3() 和 wait4() 中的 options 参数包含可用选项中任意几个的按位或。你可以通过查看这些调用的手册页以及浏览头文件 /usr/include/linux/wait.h 或 /usr/src/linux-headers-4.4.0-21/include/uapi/linux/wait.h 来查看这些选项及其含义。手册页还描述了几个宏，可用于确定已终止子进程的状态。例如，你可以判断子进程是否因信号的到达而终止，如果是，则可以确定导致进程终止的信号编号。这些宏定义在文件 /usr/include/x86_64-linux-gnu/sys/wait.h 和 /usr/include/x86_64-linux-gnu/bits/waitstatus.h 中。

当指定了 WNOHANG 选项且没有进程报告状态时，wait4() 和 wait3() 不会阻塞，而是返回 0 作为 PID。表 16.5 显示了 wait4() 调用与 wait() 类中其他调用的一些等价关系。

## 表 16.3

wait() 系统调用失败的部分原因

| 失败原因 | errno 的值 |
|---|---|
| 调用进程没有可等待的子进程 | ECHILD |
| 由于调用进程正在忽略 SIGCHLD 且系统正在丢弃此类状态，因此已终止子进程的状态不可用 | ECHILD |
| 调用被信号中断 | EINTR |
| 系统调用中指定了无效选项 | EINVAL |

| 低字节 | 高字节 |
|---|---|
| 系统对子进程终止原因的理解：普通终止为 0，异常终止为非 0 | exit() 调用的参数 |
| 0 7 | 8 15 |

图 16.7 status 参数值的两个字节中值的含义。

## 表 16.4

wait4() 和 waitpid() 系统调用的 wpid 参数值及等待的子进程

| wpid | 调用者等待 |
|------|------------|
| -1 | 任意子进程 |
| 0 | 调用者进程组中的任意子进程 |
| > 0 | PID 为 wpid 的子进程 |
| < -1 | 进程 GID 等于 wpid 绝对值的任意子进程 |

以下会话中的 fork.c 程序使用 fork() 系统调用创建一个子进程。子进程在显示其 PID 和父进程 PID 后终止。父进程等待子进程，并在显示其 PID 和子进程 PID 后终止。请注意，父进程显示的 PID 与子进程显示的父进程 PID 相同，这是符合预期的。

```
$ cat fork.c
#include <unistd.h>

extern int errno;

int main(void)
{
    int pid, status;

    pid = fork();
    if (pid == -1) {
        perror("Fork failed.");
        exit(1);
    }
    /* 子进程 */
    if (pid == 0) {
        printf("\nCHILD: Child here with PID = %d.\n", getpid());
        printf("CHILD: My Mom has PID = %d.\n", getppid());
        exit(0);
    }
    /* 父进程 */
    wait(&status);
    printf("\nPARENT: Mom here with PID = %d.\n", getpid());
    printf("PARENT: Well done, child!\n\n");
    exit(0);
}
$ gcc -w fork.c -o fork
```

## 表 16.5

wait4() 系统调用的等价关系

wait4(..., ..., ..., 0);    waitpid(..., ..., ...);
wait4(-1, ..., ..., ...);    wait3(..., ..., ...);
wait4(-1, ..., 0, 0);       wait(...);

