

## 系统编程：进程管理和信号处理

```
/* Open file */
if (argc == 1) {
    printf("No file specified as command line argument.\n");
    exit(1);
}
if ((fd = open(argv[1], O_WRONLY|O_CREATE|O_TRUNC, S_IREAD|S_IWRITE)) == -1) {
    perror("File opening");
    exit(1);
}
/* Close standard output */
close(1);
/* Duplicate fd into file descriptor 1, i.e., stdout */
if (dup(fd) == -1) {
    perror("Duplicating file descriptor");
    exit(1);
}
/* Close fd in order to release the extra slot in the PPFD */
if (close(fd) == -1) {
    perror("File closing");
    exit(1);
}
/* Stdout redirected to the file passed as command line argument */
printf("Hello, world!\n");
    exit(0);
}
```

```
$ gcc -w dup.c -o dup
$ dup foo
$ cat foo
Hello, world!
```

在下面这个会话中，我们展示了 dup2.c 程序中使用 dup2() 来完成与 dup.c 程序相同的任务——即将标准输出重定向到作为命令行参数传给程序的文件。

```
#include <fcntl.h>
#include <sys/stat.h>

int main(int argc, char *argv[])
{
    int fd;
    /* Open file */
    if (argc == 1) {
        printf("No file specified as command line argument.\n");
        exit(1);
    }
    if ((fd = open(argv[1], O_WRONLY|O_CREATE|O_TRUNC, S_IREAD|S_IWRITE)) == -1) {
        perror("File opening");
        exit(1);
    }
    /* Duplicate fd into file descriptor 1, i.e., stdout */
    if (dup2(fd, 1) == -1) {
        perror("Duplicating file descriptor");
        exit(1);
    }
    /* Close fd in order to release the extra slot in the PPFD */
    if (close(fd) == -1) {
        perror("File closing");
        exit(1);
    }
}
```

```
/* Stdout redirected to the file passed as command line argument */
printf("Hello, world!\n");
exit(0);
}
```

```
$ gcc -w dup2.c -o dup2
$ dup2 foo
$ cat foo
Hello, world!
$
```

你可以按照讨论的相同方式重定向标准输入（或标准错误）。这三个标准文件可以重定向到一个文件或多个文件，分别为标准输入、标准输出和标准错误各重定向到一个文件。

## 练习 16.14

在你的系统上复现前面的会话。dup.c 和 dup2.c 程序是否按预期工作？

## 16.5 引起进程注意：Linux 信号

类似于外围设备可以使用中断来引起 CPU 注意并获得服务，你可以使用信号来引起进程的注意。我们在第 12 章中详细讨论了这个主题，以解释 shell 脚本中的信号/中断处理。这里，我们讨论 C 程序中的信号处理。

### 16.5.1 什么是信号？

如前所述，Linux 词汇中的信号是中断进程执行的事件。在讨论高级 Bourne shell 编程时，我们在 12.4 节中讨论了导致信号的事件。其中一些导致信号的事件列在表 12.1 中。我们在表 16.8 中复现了该表。

你可以通过查看 kill 命令或 kill() 系统调用的 man 页面来查看导致信号的完整事件列表。你也可以使用 kill -l 命令来显示信号列表。

## 表 16.8

常用信号、它们的编号及其用途

| 信号 | 编号 | 用途 |
|---|---|---|
| SIGHUP（挂断） | 1 | 当运行该进程的用户注销时通知进程，进程终止 |
| SIGINT（键盘中断） | 2 | 当用户按下 <Ctrl+C> 时通知进程，进程终止 |
| SIGQUIT（退出信号） | 3 | 当用户按下 <Ctrl+|> 或 <Ctrl+\> 时通知进程，进程终止 |
| SIGKILL（确定终止） | 9 | 当用户使用 kill -9 命令向进程发送该信号时，不再进行进一步处理（例如异常处理）就终止进程 |
| SIGSEGV（段错误） | 11 | 当进程尝试访问不属于它的内存空间时，发生内存错误，终止进程 |
| SIGTERM（软件终止） | 15 | 当 kill 命令不带任何信号编号使用时终止进程 |
| SIGTSTP（挂起/停止信号） | 18 | 挂起进程；通常是 <Ctrl+Z> |
| SIGCHLD（子进程执行完成） | 20 | 通知进程其某个子进程终止 |

## 系统编程 II：进程管理和信号处理

类似的列表也可以在 /usr/include/x86_64-linux-gnu/asm/signal.h、/usr/include/asm-generic/signal.h 和 /usr/src/linux-headers-4.4.0-21/include/uapi/asm-generic/signal.h 文件中找到。

你可以使用 kill 命令或 kill() 系统调用向进程发送信号。两者都需要两个参数：信号编号和接收信号的进程 PID。例如，kill -16 12345 命令将编号为 16 的信号发送给 PID 为 12345 的进程。

### 16.5.2 截获信号

进程可以使用 sigaction() 系统调用或 signal() 库调用来截获信号，并采取以下三种可能的动作之一：

- 1. 忽略信号
- 2. 采取内核定义的默认动作
- 3. 采取程序员定义的动作

默认动作列在 /usr/src/linux-headers-4.4.0-21/include/linux/signal.h 中。

sigaction() 系统调用的接口相当复杂。库调用 signal() 的接口简单得多。因此，程序员通常使用 signal() 来处理信号。以下是该调用的简要描述：

```
#include <signal.h>
sig_t signal(int sig, sig_t func);

Success: 0
Failure: -1 and kernel variable errno set to indicate the type of error
```

func 参数可以是 SIG_IGN（用于忽略信号）和 SIG_DFL（用于默认的内核定义动作）。调用 signal() 函数可能因两个原因而失败，如表 16.9 所示。

### 16.5.3 设置闹钟

库调用 alarm() 在指定秒数后向调用进程发送 SIGALRM 信号。因此，调用 alarm(10) 会在 10 秒后向调用者进程发送 SIGALRM 信号。以下是该调用的简要描述：

```
#include <unistd.h>
unsigned int alarm(unsigned int seconds);

Success: 0 if no alarm is currently set and the number of seconds left on the timer of the previous alarm()
Failure: -1 and kernel variable errno set to indicate the type of error
```

允许的最大秒数为 100,000,000。如果已经设置了闹钟但尚未触发（即信号尚未发送到进程），则另一次 alarm 调用将取代之前的调用。alarm(0) 调用取消当前闹钟，并且 SIGALRM 永远不会传递给调用进程。

| 失败原因 | errno 的值 |
|--------------------|----------------|
| sig 中指定的信号不是有效的信号编号 | EINVAL |
| 进程试图忽略 SIGKILL 或 SIGSTOP 信号或为其指定处理程序 | EINVAL |

```
[Output truncated]
16626 ?        00:00:00 sshd
16627 pts/0    00:00:00 bash
16647 pts/3    00:00:00 signals
16657 pts/0    00:00:00 ps
$ kill -1 16647
$ fg
signals
Waiting for alarm.
^CNice try! Sorry you cannot terminate me like this.
Waiting for alarm.
^Z
[1]+  Stopped                 signals
$ kill -9 16647
$ ps -U sarwar
PID TTY          TIME CMD
14466 ?        00:00:00 systemd
[Output truncated]
16626 ?        00:00:00 sshd
16627 pts/0    00:00:00 bash
16659 pts/3    00:00:00 ps
[1]+  Killed                 signals
$
```

在某些 Linux 系统上，使用 signal() 调用截获信号的设置仅在一次生效。当一个信号被截获并按照信号设置处理后，必须重新建立信号设置，信号处理才能正常工作。为此，相关的信号处理程序包含用于为未来信号处理重置信号的代码。为了让 signals.c 程序在此类系统上正常工作，你需要修改 nicetry() 函数（SIGINT 的处理程序），如下所示：

```
void nicetry(void)
{
    signal(SIGINT, nicetry);
    printf("Nice try! Sorry you cannot terminate me like this.\n");
}
```

## 练习 16.15

在你的系统上复现前面的会话。signals.c 程序是否按预期工作？

一些互联网服务（如 ftp）通过服务器进程提供，这些服务器进程通过多个从进程（每个客户端一个）向客户端进程提供服务。从进程是由主服务器预先创建和/或在需要时动态创建的。主服务器也称为主控服务器。这类服务器称为多进程服务器或并发服务器。并发服务器在无限循环中运行，代码结构如下：

```
while (1) {
    wait for a client request
    create a slave process when a client request arrives
    slave handles the client request
}
```

由于并发服务器在客户端请求到达时会不断创建从进程，因此在从进程为客户端进程提供服务后正确终止它并将其从系统中移除是很重要的。这是通过分别在从进程和主控进程中使用 exit() 和 wait() 调用来实现的。如果主服务器进程在从进程提供服务后没有移除这些从进程，

