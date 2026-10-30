

你可能需要定义一个额外的符号，例如在 FreeBSD 上使用 __BSD_VISIBLE 或在 Linux 上使用 __USE_BSD。

大多数 syslog 实现会将消息排队一段时间。如果在此期间到达重复消息，syslog 守护进程不会将其写入日志。相反，守护进程会打印类似“last message repeated N times.”的消息。

## 13.5 单实例守护进程

某些守护进程的实现方式是同一时间只能运行一个副本才能正常运行。例如，这样的守护进程可能需要独占访问某个设备。在 cron 守护进程的情况下，如果运行多个实例，每个副本都可能尝试启动同一个计划操作，导致重复操作并可能出现错误。

如果守护进程需要访问设备，设备驱动程序有时会阻止多次尝试打开 /dev 中的对应设备节点。这限制了同一时间只能运行一个守护进程副本。如果没有此类设备可用，则我们需要自己完成这项工作。

文件和记录锁定机制提供了确保只有一个守护进程副本运行的一种方式的基础。（我们在第 14.3 节讨论文件和记录锁定。）如果每个守护进程都创建一个具有固定名称的文件并对整个文件放置写锁，则只允许创建一个这样的写锁。后续创建写锁的尝试将失败，作为后续守护进程副本的指示，表明另一个实例已在运行。

文件和记录锁定提供了一个方便的互斥机制。如果守护进程对整个文件获得写锁，当守护进程退出时锁将自动移除。这简化了恢复，消除了我们需要从守护进程的先前实例清理的需要。

### Example

图 13.6 所示的函数说明了如何使用文件和记录锁定来确保只有一个守护进程副本在运行。

```
#include <unistd.h>
#include <stdlib.h>
#include <fcntl.h>
#include <syslog.h>
#include <string.h>
#include <errno.h>
#include <stdio.h>
#include <sys/stat.h>

#define LOCKFILE "/var/run/daemon.pid"
#define LOCKMODE (S_IRUSR|S_IWUSR|S_IRGRP|S_IROTH)

extern int lockfile(int);
```

```
int
already_running(void)
{
    int     fd;
    char    buf[16];
    fd = open(LOCKFILE, O_RDWR|O_CREAT, LOCKMODE);
    if (fd < 0) {
        syslog(LOG_ERR, "can't open %s: %s", LOCKFILE, strerror(errno));
        exit(1);
    }
    if (lockfile(fd) < 0) {
        if (errno == EACCES || errno == EAGAIN) {
            close(fd);
            return(1);
        }
        syslog(LOG_ERR, "can't lock %s: %s", LOCKFILE, strerror(errno));
        exit(1);
    }
    ftruncate(fd, 0);
    sprintf(buf, "%ld", (long)getpid());
    write(fd, buf, strlen(buf)+1);
    return(0);
}
```

### Figure 13.6 Ensure that only one copy of a daemon is running

每个守护进程副本都会尝试创建一个文件并在其中写入其进程 ID。这将允许管理员轻松识别该进程。如果文件已被锁定，lockfile 函数将失败并将 errno 设置为 EACCES 或 EAGAIN，因此我们返回 1，表示守护进程已在运行。否则，我们截断文件，将我们的进程 ID 写入其中，并返回 0。

我们需要截断文件，因为守护进程的先前实例可能具有比我们更大的进程 ID，且字符串长度更大。例如，如果守护进程的先前实例是进程 ID 12345，而新实例是进程 ID 9999，当我们将进程 ID 写入文件时，文件中会留下 99995。截断文件可防止来自先前守护进程的数据似乎适用于当前守护进程。

## 13.6 守护进程约定

UNIX 系统中的守护进程遵循几种常见约定。

- 如果守护进程使用锁文件，该文件通常存储在 /var/run 中。注意，然而，守护进程可能需要超级用户权限在此处创建文件。文件的名称通常为 name.pid，其中 name 是守护进程或服务的名称。例如，在 Linux 上，cron 守护进程的锁文件名为 /var/run/crond.pid。

```
}

switch (signo) {
case SIGHUP:
    syslog(LOG_INFO, "Re-reading configuration file");
    reread();
    break;

case SIGTERM:
    syslog(LOG_INFO, "got SIGTERM; exiting");
    exit(0);

default:
    syslog(LOG_INFO, "unexpected signal %d\n", signo);
}
    return(0);
}

int
main(int argc, char *argv[])
{
    int             err;
    pthread_t       tid;
    char            *cmd;
    struct sigaction sa;

    if ((cmd = strchr(argv[0], '/')) == NULL)
        cmd = argv[0];
    else
        cmd++;

    /*
     * Become a daemon.
     */
    daemonize(cmd);

    /*
     * Make sure only one copy of the daemon is running.
     */
    if (already_running()) {
        syslog(LOG_ERR, "daemon already running");
        exit(1);
    }

    /*
     * Restore SIGHUP default and block all signals.
     */
    sa.sa_handler = SIG_DFL;
    sigemptyset(&sa.sa_mask);
    sa.sa_flags = 0;
    if (sigaction(SIGHUP, &sa, NULL) < 0)
        err_quit("%s: can't restore SIGHUP default");
```

```
sigfillset(&mask);
if ((err = pthread_sigmask(SIG_BLOCK, &mask, NULL)) != 0)
    err_exit(err, "SIG_BLOCK error");

/*
 * Create a thread to handle SIGHUP and SIGTERM.
 */
err = pthread_create(&tid, NULL, thr_fn, 0);
if (err != 0)
    err_exit(err, "can't create thread");

/*
 * Proceed with the rest of the daemon.
 */
/* ... */
exit(0);
}
```

### Figure 13.7 Daemon rereading configuration files

我们调用图 13.1 中的 daemonize 来初始化守护进程。当它返回时，我们调用图 13.6 中的 already_running 来确保只有一个守护进程副本在运行。此时，SIGHUP 仍被忽略，因此我们需要将处置重置为默认行为；否则，调用 sigwait 的线程可能永远看不到该信号。

我们阻塞所有信号，这是多线程程序推荐的做法，并创建一个线程来处理信号。该线程的唯一工作是等待 SIGHUP 和 SIGTERM。当它收到 SIGHUP 时，线程调用 reread 重新读取其配置文件。当它收到 SIGTERM 时，线程记录一条消息并退出。

回想图 10.1，SIGHUP 和 SIGTERM 的默认操作是终止进程。由于我们阻塞了这些信号，当其中一个信号发送到进程时，守护进程不会死亡。相反，调用 sigwait 的线程将返回并指示已收到信号。

### Example

并非所有守护进程都是多线程的。图 13.8 中的程序展示了单线程守护进程如何捕获 SIGHUP 并重新读取其配置文件。

```
#include "apue.h"
#include <syslog.h>
#include <errno.h>

extern int lockfile(int);
extern int already_running(void);

void
reread(void)
{
    /* ... */
```

```
sigaddset(&sa.sa_mask, SIGTERM);
 sa.sa_flags = 0;
 if (sigaction(SIGHUP, &sa, NULL) < 0) {
  syslog(LOG_ERR, "can't catch SIGHUP: %s", strerror(errno));
  exit(1);
 }

 /*
  * Proceed with the rest of the daemon.
  */
 /* ... */
 exit(0);
}
```

### Figure 13.8 Alternative implementation of daemon rereading configuration files

在初始化守护进程后，我们为 SIGHUP 和 SIGTERM 安装信号处理程序。我们可以将 reread 逻辑放在信号处理程序中，也只在处理程序中设置一个标志，让守护进程的主线程来完成所有工作。

## 13.7 客户端-服务器模型

守护进程的常见用途之一是作为服务器进程。事实上，在图 13.2 中，我们可以将 syslogd 进程称为服务器，它通过 UNIX 域数据报套接字接收来自用户进程（客户端）的消息。

一般来说，服务器是一个等待客户端联系它以请求某种服务的进程。在图 13.2 中，syslogd 服务器提供的服务是记录错误消息。

在图 13.2 中，客户端和服务器之间的通信是单向的。客户端向服务器发送服务请求；服务器不会向客户端发送任何回复。在接下来的章节中，我们将看到客户端和服务器之间双向通信的众多示例——客户端向服务器发送请求，服务器向客户端发送回复。

