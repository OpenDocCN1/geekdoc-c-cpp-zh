

## 10.21 作业控制信号

图 10.1 所示的信号中，POSIX.1 将其中六个视为作业控制信号：

- `SIGCHLD`  子进程已停止或终止。
- `SIGCONT`  继续进程，如果已停止。
- `SIGSTOP`  停止信号（不能被捕获或忽略）。
- `SIGTSTP`  交互式停止信号。
- `SIGTTIN`  后台进程组成员从控制终端读取。
- `SIGTTOU`  后台进程组成员向控制终端写入。

除 `SIGCHLD` 外，大多数应用程序都不处理这些信号：交互式 shell 通常会执行处理它们所需的所有工作。当我们键入挂起字符（通常是 Control-Z）时，`SIGTSTP` 会发送给前台进程组中的所有进程。当我们告诉 shell 在前台或后台恢复作业时，shell 会向作业中的所有进程发送 `SIGCONT` 信号。同样，如果 `SIGTTIN` 或 `SIGTTOU` 被传递给进程，进程默认会被停止，而作业控制 shell 会识别到这一点并通知我们。

一个例外是管理终端的进程，例如 vi(1) 编辑器。它需要知道用户何时想挂起它，以便它可以将终端状态恢复到 vi 启动时的状态。此外，当它在前台恢复时，vi 编辑器需要将终端状态设置回它想要的状态，并且需要重绘终端屏幕。我们将在下面的示例中看到像 vi 这样的程序如何处理这个问题。

作业控制信号之间存在一些交互。当为进程生成四个停止信号之一（`SIGTSTP`、`SIGSTOP`、`SIGTTIN` 或 `SIGTTOU`）时，该进程的任何待处理的 `SIGCONT` 信号都会被丢弃。同样，当为进程生成 `SIGCONT` 信号时，该进程的任何待处理的停止信号都会被丢弃。

请注意，`SIGCONT` 的默认操作是如果进程已停止则继续进程；否则，信号将被忽略。通常，我们不必对该信号做任何事情。当 `SIGCONT` 为已停止的进程生成时，进程将被继续，即使信号被阻塞或忽略。

### 示例

图 10.31 中的程序演示了程序处理作业控制时使用的正常代码序列。该程序只是简单地将标准输入复制到标准输出，但信号处理程序中的注释给出了由管理屏幕的程序执行的典型操作。

```
#include "apue.h"
#define BUFFSIZE    1024
static void
sig_tstp(int signo) /* signal handler for SIGTSTP */
{
    sigset_t    mask;
    /* ... move cursor to lower left corner, reset tty mode ... */
    /*
     * Unblock SIGTSTP, since it’s blocked while we’re handling it.
     */
    sigemptyset(&mask);
    sigaddset(&mask, SIGTSTP);
    sigprocmask(SIG_UNBLOCK, &mask, NULL);
    signal(SIGTSTP, SIG_DFL);   /* reset disposition to default */
    kill(getpid(), SIGTSTP);    /* and send the signal to ourself */
    /* we won’t return from the kill until we’re continued */
    signal(SIGTSTP, sig_tstp);  /* reestablish signal handler */
    /* ... reset tty mode, redraw screen ... */
}
int
main(void)
{
    int     n;
    char    buf[BUFFSIZE];
    /*
     * Only catch SIGTSTP if we’re running with a job-control shell.
     */
    if ((signal(SIGTSTP, SIG_IGN) == SIG_DFL)
        signal(SIGTSTP, sig_tstp);
    while ((n = read(STDIN_FILENO, buf, BUFFSIZE)) > 0)
        if (write(STDOUT_FILENO, buf, n) != n)
            err_sys("write error");
    if (n < 0)
        err_sys("read error");
    exit(0);
}
```

### 图 10.31 如何处理 SIGTSTP

当图 10.31 中的程序启动时，它仅在信号的处置为 `SIG_DFL` 时才安排捕获 `SIGTSTP` 信号。原因在于当程序由不支持作业控制的 shell 启动时（例如 /bin/sh），信号的处置

应设置为 `SIG_IGN`。事实上，shell 并没有显式忽略该信号；init 将三个作业控制信号（`SIGTSTP`、`SIGTTIN` 和 `SIGTTOU`）的处置设置为 `SIG_IGN`。该处置随后被所有登录 shell 继承。只有作业控制 shell 才会将这三个信号的处置重置为 `SIG_DFL`。

当我们键入挂起字符时，进程会收到 `SIGTSTP` 信号并调用信号处理程序。此时，我们会执行任何与终端相关的处理：移动光标到左下角、恢复终端模式等。然后我们在将它的处置重置为默认值（停止进程）并解除信号阻塞后，向自己发送相同的信号 `SIGTSTP`。我们必须解除其阻塞，因为我们当前正在处理该信号，系统在捕获期间会自动阻塞它。此时，系统会停止进程。只有当它收到（通常来自作业控制 shell，对应于交互式 fg 命令）`SIGCONT` 信号时，才会被继续。我们不捕获 `SIGCONT`。它的默认处置是继续已停止的进程；当这种情况发生时，程序会继续执行，就好像它从 kill 函数返回一样。当程序被继续时，我们会重置 `SIGTSTP` 信号的处置并执行我们想要的任何终端处理（例如，我们可以重绘屏幕）。

## 10.22 信号名称和编号

在本节中，我们描述如何映射信号编号和名称。某些系统提供数组

```
extern char *sys_siglist[];
```

数组索引是信号编号，提供指向信号名称字符字符串的指针。

> FreeBSD 8.0、Linux 3.2.0 和 Mac OS X 10.6.8 都提供此信号名称数组。Solaris 10 也提供，但它使用名称 _sys_siglist。

为了以可移植的方式打印对应于信号编号的字符字符串，我们可以使用 psignal 函数。

```
#include <signal.h>
void psignal(int signo, const char *msg);
```

字符串 msg（通常包括程序名称）输出到标准错误，后跟冒号和空格，然后是信号的描述，然后是换行符。如果 msg 为 NULL，则仅将描述写入标准错误。此函数类似于 perror（第 1.7 节）。

如果您从替代 sigaction 信号处理程序获得 siginfo 结构，您可以使用 psiginfo 函数打印信号信息。

```
#include <signal.h>
void psiginfo(const siginfo_t *info, const char *msg);
```

它以与 psignal 函数类似的方式操作。尽管该函数可以访问的信息比仅信号编号更多，但平台在打印的额外信息方面各不相同。

如果您只需要信号的字符串描述，而不一定想将其写入标准错误（例如，您可能想将其写入日志文件），则可以使用 strsignal 函数。此函数类似于 strerror（也在第 1.7 节中描述）。

```
#include <string.h>
char *strsignal(int signo);

Returns: a pointer to a string describing the signal
```

给定信号编号，strsignal 将返回描述该信号的字符串。此字符串可由应用程序用于打印有关接收到的信号的错误消息。

本书讨论的所有平台都提供 psignal 和 strsignal 函数，但差异确实存在。在 Solaris 10 上，如果信号编号无效，strsignal 将返回空指针，而 FreeBSD 8.0、Linux 3.2.0 和 Mac OS X 10.6.8 则返回一个字符串，表明信号编号无法识别。

只有 Linux 3.2.0 和 Solaris 10 支持 psiginfo 函数。

Solaris 提供几个函数来将信号编号映射到信号名称，反之亦然。

```
#include <signal.h>

int sig2str(int signo, char *str);
int str2sig(const char *str, int *signop);

Both return: 0 if OK, -1 on error
```

当编写需要接受和打印信号名称和编号的交互式程序时，这些函数很有用。

## 10.23 摘要

信号在大多数非平凡的应用程序中使用。对信号处理的如何和为何的理解是高级 UNIX 系统编程必不可少的。本章对 UNIX 系统信号进行了长而彻底的探讨。我们首先研究了先前信号实现中的缺陷以及它们的表现方式。然后我们继续介绍 POSIX.1 可靠信号概念以及所有相关函数。一旦我们涵盖了所有这些细节，我们就能够提供 POSIX.1 abort、system 和 sleep 函数的实现。我们以对作业控制信号的介绍以及我们如何能在信号名称和编号之间转换作为结束。

## 练习

- 10.1 在图 10.2 中，删除 for (;;) 语句。会发生什么以及为什么？
- 10.2 实现第 10.22 节中描述的 sig2str 函数。
- 10.3 绘制运行图 10.9 程序时堆栈帧的图片。
- 10.4 在图 10.11 中，我们展示了一种经常使用的方法，使用 setjmp 和 longjmp 在 I/O 操作上设置超时。以下代码也曾出现过：

```
signal(SIGALRM, sig_alrm);
alarm(60);
if (setjmp(env_alrm) != 0) {
    /* handle timeout */
    ...
}
...
```

这个代码序列还有什么其他问题？
- 10.5 使用仅一个计时器（alarm 或更高精度的 setitimer），提供一组函数，允许进程设置任意数量的计时器。
- 10.6 编写以下程序以测试图 10.24 中的父子同步函数。进程创建一个文件并向文件中写入整数 0。进程然后调用 fork，父进程和子进程交替递增文件中的计数器。每次递增计数器时，打印哪个进程（父进程或子进程）正在执行递增。

