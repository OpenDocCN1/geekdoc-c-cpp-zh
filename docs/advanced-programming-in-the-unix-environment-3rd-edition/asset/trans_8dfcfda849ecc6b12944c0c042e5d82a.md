

在示例 `ps` 输出中，内核守护进程以方括号中的名称出现。这个 Linux 版本使用一个特殊的内核进程 `kthreadd` 来创建其他内核进程，因此 `kthreadd` 作为其他内核守护进程的父进程出现。每个需要在进程上下文中执行工作、但并非从用户级进程的上下文调用的内核组件，通常都有自己的内核守护进程。例如，在 Linux 上

-   `kswapd` 守护进程也称为换页守护进程。它通过随时间将脏页缓慢写入磁盘来支持虚拟内存子系统，以便这些页面可以被回收。
-   当可用内存达到配置的最低阈值时，`flush` 守护进程会将脏页刷写到磁盘。它还会定期将脏页刷回磁盘，以减少系统故障时的数据丢失。可能存在多个 `flush` 守护进程——每个后备存储设备对应一个。示例输出显示了一个名为 `flush-8:0` 的刷写守护进程。在名称中，后备设备由其主设备号 (8) 和次设备号 (0) 标识。
-   `sync_supers` 守护进程定期将文件系统元数据刷写到磁盘。
-   `jbd` 守护进程帮助实现 ext4 文件系统中的日志。

进程 1 通常是 `init`（在 Mac OS X 上是 `launchd`），正如我们在 8.2 节中描述的那样。它是一个系统守护进程，除其他职责外，还负责启动特定于各种运行级别的系统服务。这些服务通常借助它们自己的守护进程来实现。

`rpcbind` 守护进程提供将 RPC（远程过程调用）程序号映射到网络端口号的服务。`syslogd` 守护进程可供任何程序使用，以便向管理员记录系统消息。这些消息可以打印在控制台设备上，也可以写入文件。（我们将在 13.4 节中描述 syslog 工具。）

我们在 9.3 节中讨论了 `inetd` 守护进程。它监听系统的网络接口，以接收对各种网络服务的传入请求。`nfsd`、`nfsiod`、`lockd`、`rpciod`、`rpc.idmapd`、`rpc.statd` 和 `rpc.mountd` 守护进程为网络文件系统（NFS）提供支持。请注意，前四个是内核守护进程，而后三个是用户级守护进程。

`cron` 守护进程按定期安排的日期和时间执行命令。许多系统管理任务由 `cron` 定期运行程序来处理。`atd` 守护进程与 `cron` 类似；它允许用户在指定时间执行作业，但每个作业只执行一次，而不是按定期安排的时间重复执行。`cups` 守护进程是一个打印假脱机程序；它处理系统上的打印请求。`sshd` 守护进程提供安全的远程登录和执行功能。

请注意，大多数守护进程以超级用户（root）权限运行。所有守护进程都没有控制终端：终端名称设置为问号。内核守护进程在启动时没有控制终端。用户级守护进程缺少控制终端可能是守护进程调用 `setsid` 的结果。大多数用户级守护进程是进程组组长和会话组长，并且是它们所在进程组和会话中的唯一进程。（唯一的例外是 `rsyslogd`。）最后，请注意用户级守护进程的父进程是 `init` 进程。

## 13.3 编码规则

守护进程编码的一些基本规则可防止发生不希望出现的交互。我们在此说明这些规则，然后展示一个实现这些规则的函数 `daemonize`。

-   1. 调用 `umask` 将文件模式创建屏蔽字设置为已知值，通常为 0。继承的文件模式创建屏蔽字可能被设置为拒绝某些权限。如果守护进程创建文件，它可能希望设置特定权限。例如，如果它以组读和组写权限创建文件，那么关闭其中任一权限的文件模式创建屏蔽字都会使其努力付诸东流。另一方面，如果守护进程调用的库函数会导致文件被创建，那么将文件模式创建屏蔽字设置为更严格的值（例如 007）可能是有意义的，因为库函数可能不允许调用者通过显式参数指定权限。

-   2. 调用 `fork` 并让父进程退出。这有几方面的作用。首先，如果守护进程是作为简单的 shell 命令启动的，那么父进程终止会让 shell 认为该命令已完成。其次，子进程继承父进程的进程组 ID，但获得新的进程 ID，因此我们可以保证子进程不是进程组组长。这是接下来调用 `setsid` 的先决条件。

-   3. 调用 `setsid` 创建一个新会话。9.5 节中列出的三个步骤会发生。该进程 (a) 成为新会话的组长，(b) 成为新进程组的组长，(c) 与控制终端脱离关联。

> 在基于 System V 的系统中，有些人建议此时再次调用 `fork`，终止父进程，并让子进程继续作为守护进程运行。这保证了守护进程不是会话组长，从而防止它根据 System V 规则（9.6 节）获得控制终端。或者，为了避免获得控制终端，请确保在打开终端设备时指定 `O_NOCTTY`。

-   4. 将当前工作目录更改为根目录。从父进程继承的当前工作目录可能位于已挂载的文件系统上。由于守护进程通常会一直存在到系统重新启动，如果守护进程停留在已挂载的文件系统上，则该文件系统无法被卸载。或者，某些守护进程可能会将当前工作目录更改为它们将执行所有工作的特定位置。例如，行式打印机假脱机守护进程可能会将其工作目录更改为其假脱机目录。

-   5. 应关闭不需要的文件描述符。这可以防止守护进程保持打开它可能从父进程（可能是 shell 或其他进程）继承的任何描述符。我们可以使用 `open_max` 函数（图 2.17）或 `getrlimit` 函数（7.11 节）来确定最高描述符，并关闭直到该值的所有描述符。

-   6. 某些守护进程将文件描述符 0、1 和 2 打开到 `/dev/null`，这样任何尝试从标准输入读取或写入标准输出或标准错误的库例程都不会产生效果。由于守护进程与终端设备没有关联，因此没有地方可以显示输出，也没有地方可以从交互式用户接收输入。即使守护进程是从交互式会话启动的，守护进程也在后台运行，登录会话可以终止而不影响守护进程。如果其他用户在同一终端设备上登录，我们不希望守护进程的输出显示在终端上，而且这些用户也不会期望他们的输入被守护进程读取。

## 示例

图 13.1 显示了一个函数，可以从想要将自己初始化为守护进程的程序中调用。

```
#include "apue.h"
#include <syslog.h>
#include <fcntl.h>
#include <sys/resource.h>

void
daemonize(const char *cmd)
{
    int             i, fd0, fd1, fd2;
    pid_t           pid;
    struct rlimit   rl;
    struct sigaction sa;

    /*
     * Clear file creation mask.
     */
    umask(0);

    /*
     * Get maximum number of file descriptors.
     */
    if (getrlimit(RLIMIT_NOFILE, &rl) < 0)
        err_quit("%s: can't get file limit", cmd);

    /*
     * Become a session leader to lose controlling TTY.
     */
    if ((pid = fork()) < 0)
        err_quit("%s: can't fork", cmd);
    else if (pid != 0) /* parent */
        exit(0);
    setsid();

    /*
     * Ensure future opens won't allocate controlling TTYs.
     */
    sa.sa_handler = SIG_IGN;
    sigemptyset(&sa.sa_mask);
```

```
sa.sa_flags = 0;
if (sigaction(SIGHUP, &sa, NULL) < 0)
    err_quit("%s: can't ignore SIGHUP", cmd);
if ((pid = fork()) < 0)
    err_quit("%s: can't fork", cmd);
else if (pid != 0) /* parent */
    exit(0);

/*
 * Change the current working directory to the root so
 * we won't prevent file systems from being unmounted.
 */
if (chdir("/") < 0)
    err_quit("%s: can't change directory to '/'", cmd);

/*
 * Close all open file descriptors.
 */
if (rl.rlim_max == RLIM_INFINITY)
    rl.rlim_max = 1024;
for (i = 0; i < rl.rlim_max; i++)
    close(i);

/*
 * Attach file descriptors 0, 1, and 2 to /dev/null.
 */
fd0 = open("/dev/null", O_RDWR);
fd1 = dup(0);
fd2 = dup(0);

/*
 * Initialize the log file.
 */
openlog(cmd, LOG_CONS, LOG_DAEMON);
if (fd0 != 0 || fd1 != 1 || fd2 != 2) {
    syslog(LOG_ERR, "unexpected file descriptors %d %d %d",
        fd0, fd1, fd2);
    exit(1);
}
```

# 图 13.1 初始化守护进程

如果从随后进入休眠的 `main` 程序中调用 `daemonize` 函数，我们可以使用 `ps` 命令检查守护进程的状态：

```
$ ./a.out
$ ps -efj
UID    PID  PPID  PGID  SID  TTY CMD
sar   13800     1 13799 13799  ?  ./a.out
$ ps -efj | grep 13799
sar   13800     1 13799 13799  ?  ./a.out
```

