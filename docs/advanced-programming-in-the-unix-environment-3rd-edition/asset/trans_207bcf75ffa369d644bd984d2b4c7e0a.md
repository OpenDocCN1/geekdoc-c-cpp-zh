

对于这两个函数，参数 statloc 都是指向一个整数的指针。如果该参数不是空指针，则终止进程的终止状态将被存储在该参数所指向的位置。如果我们不关心终止状态，则只需将空指针作为该参数传递。

传统上，这两个函数返回的整数 status 是由实现定义的，其中某些位表示退出状态（对于正常返回），其他位表示信号编号（对于异常返回），一位表示是否生成了核心文件，等等。POSIX.1 规定终止状态应使用在 <sys/wait.h> 中定义的各种宏来查看。四个互斥的宏告诉我们进程是如何终止的，它们都以 WIF 开头。根据这四个宏中的哪一个为真，其他宏用于获取退出状态、信号编号等。这四个互斥的宏如 Figure 8.4 所示。

| Macro | Description |
|---|---|
| WIFEXITED(status) | True if status was returned for a child that terminated normally. In this case, we can execute WEXITSTATUS(status) to fetch the low-order 8 bits of the argument that the child passed to exit, _exit, or _Exit. |
| WIFSIGNALED(status) | True if status was returned for a child that terminated abnormally, by receipt of a signal that it didn’t catch. In this case, we can execute WTERMSIG(status) to fetch the signal number that caused the termination. Additionally, some implementations (but not the Single UNIX Specification) define the macro WCOREDUMP(status) that returns true if a core file of the terminated process was generated. |
| WIFSTOPPED(status) | True if status was returned for a child that is currently stopped. In this case, we can execute WSTOPSIG(status) to fetch the signal number that caused the child to stop. |
| WIFCONTINUED(status) | True if status was returned for a child that has been continued after a job control stop (XSI option; waitpid only). |

Figure 8.4 Macros to examine the termination status returned by wait and waitpid

我们将在第 9.8 节讨论进程如何被停止时讨论作业控制。

## Example

Figure 8.5 中的函数 pr_exit 使用 Figure 8.4 中的宏来打印终止状态的描述。我们将在文本中的许多程序中调用此函数。请注意，此函数会处理 WCOREDUMP 宏（如果已定义）。

```
#include "apue.h"
#include <sys/wait.h>

void
pr_exit(int status)
{
    if (WIFEXITED(status))
        printf("normal termination, exit status = %d\n",
               WEXITSTATUS(status));
    else if (WIFSIGNALED(status))
        printf("abnormal termination, signal number = %d%s\n",
               WTERMSIG(status),
#ifdef WCOREDUMP
               WCOREDUMP(status) ? " (core file generated)" : "");
#else
               "");
#endif
    else if (WIFSTOPPED(status))
        printf("child stopped, signal number = %d\n",
               WSTOPSIG(status));
}
```

*Figure 8.5* Print a description of the exit status

FreeBSD 8.0、Linux 3.2.0、Mac OS X 10.6.8 和 Solaris 10 都支持 WCOREDUMP 宏。然而，一些平台在定义了 _POSIX_C_SOURCE 常量时隐藏了其定义（请回顾第 2.7 节）。

Figure 8.6 所示的程序调用 `pr_exit` 函数，演示了终止状态的各种值。如果我们运行 Figure 8.6 中的程序，我们会得到

```
$ ./a.out
normal termination, exit status = 7
abnormal termination, signal number = 6 (core file generated)
abnormal termination, signal number = 8 (core file generated)
```

目前，我们打印来自 WTERMSIG 的信号编号。我们可以查看 <signal.h> 头文件以验证 SIGABRT 的值为 6，SIGFPE 的值为 8。我们将在第 10.22 节看到将信号编号映射到描述性名称的可移植方法。

正如我们提到的，如果我们有多个子进程，wait 会在任意一个子进程终止时返回。但如果我们想等待特定进程终止（假设我们知道要等待的进程 ID）会怎样？在旧版本的 UNIX 系统中，我们必须调用 wait 并将返回的进程 ID 与我们感兴趣的进程 ID 进行比较。如果终止的进程不是我们想要的进程，我们就需要保存进程 ID 和终止状态，然后再次调用 wait。我们需要继续这样做，直到期望的进程终止。下一次我们想等待特定进程时，我们会遍历已终止进程的列表，看看是否已经为其等待过，如果没有，则再次调用 wait。

```
#include "apue.h"
#include <sys/wait.h>

int
main(void)
{
    pid_t   pid;
    int     status;

    if ((pid = fork()) < 0)
        err_sys("fork error");
    else if (pid == 0)              /* child */
        exit(7);

    if (wait(&status) != pid)       /* wait for child */
        err_sys("wait error");
    pr_exit(status);                /* and print its status */

    if ((pid = fork()) < 0)
        err_sys("fork error");
    else if (pid == 0)              /* child */
        abort();                    /* generates SIGABRT */

    if (wait(&status) != pid)       /* wait for child */
        err_sys("wait error");
    pr_exit(status);                /* and print its status */

    if ((pid = fork()) < 0)
        err_sys("fork error");
    else if (pid == 0)              /* child */
        status /= 0;                /* divide by 0 generates SIGFPE */

    if (wait(&status) != pid)       /* wait for child */
        err_sys("wait error");
    pr_exit(status);                /* and print its status */

    exit(0);
}
```

Figure 8.6 Demonstrate various exit statuses

我们需要的是一个等待特定进程的函数。POSIX.1 waitpid 函数提供了此功能（以及更多功能）。

waitpid 对 pid 参数的解释取决于其值：

- **pid == -1** 等待任何子进程。在这方面，waitpid 等同于 wait。
- **pid > 0** 等待其进程 ID 等于 pid 的子进程。
- **pid == 0** 等待其进程组 ID 等于调用进程的任何子进程。（我们在第 9.4 节讨论进程组。）
- **pid < -1** 等待其进程组 ID 等于 pid 绝对值的任何子进程。

waitpid 函数返回终止的子进程的进程 ID，并将子进程的终止状态存储在 statloc 指向的内存位置。对于 wait，唯一的真正错误是调用进程没有子进程。（另一种错误返回是可能的，如果函数调用被信号中断。我们将在第 10 章讨论此问题。）对于 waitpid，如果指定的进程或进程组不存在或不是调用进程的子进程，也可能出现错误。

options 参数让我们进一步控制 waitpid 的操作。此参数要么为 0，要么由 Figure 8.7 中的常量的按位或构造而成。

FreeBSD 8.0 和 Solaris 10 支持一个额外的、但非标准的选项常量。WNOHANG 使系统保持 waitpid 返回终止状态的进程处于等待状态，以便可以再次等待它。

| Constant | Description |
|---|---|
| WCONTINUED | If the implementation supports job control, the status of any child specified by pid that has been continued after being stopped, but whose status has not yet been reported, is returned (XSI option). |
| WNO HANG | The waitpid function will not block if a child specified by pid is not immediately available. In this case, the return value is 0. |
| WUNTRACED | If the implementation supports job control, the status of any child specified by pid that has stopped, and whose status has not been reported since it has stopped, is returned. The WIFSTOPPED macro determines whether the return value corresponds to a stopped child process. |

Figure 8.7 The options constants for waitpid

waitpid 函数提供了 wait 函数未提供的三个功能。

- 1. waitpid 函数让我们等待某个特定进程，而 wait 函数返回任意已终止子进程的状态。我们将在讨论 popen 函数时回到此功能。
- 2. waitpid 函数提供了 wait 的非阻塞版本。有时我们想要获取子进程的状态，但又不想阻塞。
- 3. waitpid 函数通过 WUNTRACED 和 WCONTINUED 选项提供了作业控制支持。

## Example

回顾我们在第 8.5 节关于僵尸进程的讨论。如果我们想编写一个进程使其 fork 一个子进程，但我们不想等待子进程完成，并且我们也不希望子进程在我们终止之前成为僵尸，诀窍是调用两次 fork。Figure 8.8 中的程序就是这样做的。

