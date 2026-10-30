

signal handler, write fails with errno set to EPIPE. With poll, however, the behavior varies by platform.

## 15.8

子进程写入标准错误的内容会出现在父进程的标准错误出现的地方。要将标准错误发送回父进程，请在 cmdstring 中包含 shell 重定向 2>&1。

## 15.9

popen 函数会 fork 一个子进程，子进程执行 shell。shell 又调用 fork，shell 的子进程执行命令字符串。当 cmdstring 终止时，shell 正在等待这种情况的发生。随后 shell 退出，这正是 pclose 中的 waitpid 正在等待的。

## 15.10

诀窍在于打开 FIFO 两次：一次用于读取，一次用于写入。我们从未使用打开用于写入的描述符，但保留该描述符打开可以防止客户端数量从 1 变为 0 时产生文件结束。打开 FIFO 两次需要谨慎，因为需要非阻塞打开。我们必须先进行非阻塞的只读打开，然后再进行阻塞的只写打开。 （如果我们先尝试非阻塞的只写打开，它会返回错误。）然后我们为读描述符关闭非阻塞。图 C.20 显示了此代码。

```
#include "apue.h"
#include <fcntl.h>
#define FIFO  "temp.fifo"
int
main(void)
{
    int fdread, fdwrite;
    unlink(FIFO);
    if (mkfifo(FIFO, FILE_MODE) < 0)
        err_sys("mkfifo error");
    if ((fdread = open(FIFO, O_RDONLY | O_NONBLOCK)) < 0)
        err_sys("open error for reading");
    if ((fdwrite = open(FIFO, O_WRONLY)) < 0)
        err_sys("open error for writing");
    clr_fl(fdread, O_NONBLOCK);
    exit(0);
}
```

图 C.20 以非阻塞方式打开 FIFO 用于读写

## 15.11

从活动队列中随机读取一条消息会干扰客户端-服务器协议，因为客户端请求或服务器的响应会被丢失。要读取队列，只需进程知道队列的标识符，并且队列允许世界可读访问即可。

## 15.13

我们从不在共享内存段中存储实际地址，因为服务器和所有客户端可能在不同地址附加该段。

相反，当在共享内存段中构建链表时，链表指针应存储为共享内存段中其他对象的偏移量。这些偏移量是通过从共享内存段的起始位置减去对象的实际地址形成的。

## 15.14

图 C.21 显示了相关事件。

| Parent i set to | Child i set to | Shared value set to | update returns | Comment |
|---|---|---|---|---|
| 0 | 1 | 0 |  | initialized by mmap
child runs first, then is blocked
parent runs |
|  |  | 1 |  |  |
|  |  | 2 | 0 | then parent is blocked
child resumes |
| 2 | 3 |  | 1 | then child is blocked
parent resumes |
|  |  | 3 |  |  |
|  |  | 4 | 2 | then parent is blocked |
| 4 | 5 |  | 3 | then child is blocked
parent resumes |

图 C.21 图 15.33 中父进程和子进程之间的交替

## Chapter 16

## 16.1

图 C.22 显示了一个打印系统字节顺序的程序。

```
#include <stdio.h>
#include <stdlib.h>
#include <inttypes.h>
int
main(void)
{
    uint32_t    i = 0x04030201;
    unsigned char    *cp = (unsigned char *) &i;
    if (*cp == 1)
        printf("little-endian\n");
    else if (*cp == 4)
        printf("big-endian\n");
    else
        printf("who knows?\n");
    exit(0);
}
```

图 C.22 确定系统上的字节顺序

## 16.3

对于我们将要监听的每个端点，我们需要绑定适当的地址并在 fd_set 结构中记录对应每个文件描述符的条目。我们将使用 select 等待多个端点上的连接请求到达。请回顾第 16.4 节，被动端点在连接请求到达时会表现为可读。当连接请求确实到达时，我们将接受请求并像以前一样处理它。

## 16.5

在主过程中，我们需要通过调用我们的信号函数（图 10.18）来安排捕获 SIGCHLD，该函数将使用 sigaction 安装处理程序并指定可重启系统调用选项。接下来，我们需要从 serve 函数中删除对 waitpid 的调用。fork 子进程为请求提供服务后，父进程关闭新的文件描述符并继续监听额外的连接请求。最后，我们需要一个 SIGCHLD 信号处理程序，如下所示：

```
void
sighchild(int signo)
{
    while (waitpid((pid_t)-1, NULL, WNOHANG) > 0)
        ;
}
```

## 16.6

要启用异步套接字 I/O，我们需要使用 F_SETOWN fcntl 命令建立套接字所有权，然后使用 FIOASYNC ioctl 命令启用异步信号。要禁用异步套接字 I/O，我们只需禁用异步信号即可。我们混合使用 fcntl 和 ioctl 命令的原因是为了找到最可移植的方法。代码显示在图 C.23 中。

```
#include "apue.h"
#include <errno.h>
#include <fcntl.h>
#include <sys/socket.h>
#include <sys/ioctl.h>
#if defined(BSD) || defined(MACOS) || defined(SOLARIS)
#include <sys/filio.h>
#endif

int
setasync(int sockfd)
{
    int n;

    if (fcntl(sockfd, F_SETOWN, getpid()) < 0)
        return(-1);
    n = 1;
    if (ioctl(sockfd, FIOASYNC, &n) < 0)
        return(-1);
    return(0);
}
```

```
int
clrasync(int sockfd)
{
    int n;
    n = 0;
    if (ioctl(sockfd, FIOASYNC, &n) < 0)
        return(-1);
    return(0);
}
```

图 C.23 启用和禁用异步套接字 I/O

## Chapter 17

## 17.1

常规管道提供字节流接口。要检测消息边界，我们必须为每条消息添加一个头来指示长度。但这仍然涉及两次额外的复制操作：一次写入管道，一次从管道读取。更有效的方法是仅使用管道来向主线程发出新消息可用信号。我们可以用一个字节来实现此目的。通过这种方法，我们需要将 mymesg 结构移动到 threadinfo 结构，并使用互斥锁和条件变量防止辅助线程在主线程完成处理之前重用 mymesg 结构。解决方案显示在图 C.24 中。

```
#include "apue.h"
#include <poll.h>
#include <pthread.h>
#include <sys/msg.h>
#include <sys/socket.h>

#define NQ      3      /* number of queues */
#define MAXMSZ  512    /* maximum message size */
#define KEY     0x123  /* key for first message queue */

struct mymesg {
    long    mtype;
    char    mtext[MAXMSZ+1];
};

struct threadinfo {
    int     qid;
    int     fd;
    int     len;
    pthread_mutex_t mutex;
    pthread_cond_t  ready;
    struct mymesg    m;
};
```

```
void *
helper(void *arg)
{
    int                 n;
    struct threadinfo   *tip = arg;

    for(;;) {
        memset(&tip->m, 0, sizeof(struct mymsg));
        if ((n = msgrcv(tip->qid, &tip->m, MAXMSZ, 0,
            MSG_NOERROR)) < 0)
            err_sys("msgrcv error");
        tip->len = n;
        pthread_mutex_lock(&tip->mutex);
        if (write(tip->fd, "a", sizeof(char)) < 0)
            err_sys("write error");
        pthread_cond_wait(&tip->ready, &tip->mutex);
        pthread_mutex_unlock(&tip->mutex);
    }

    int
main()
{
    char                c;
    int                 i, n, err;
    int                 fd[2];
    int                 qid[NQ];
    struct pollfd       pfd[NQ];
    struct threadinfo   ti[NQ];
    pthread_t           tid[NQ];

    for (i = 0; i < NQ; i++) {
        if ((qid[i] = msgget((KEY+1), IPC_CREAT|0666)) < 0)
            err_sys("msgget error");

        printf("queue ID %d is %d\n", i, qid[i]);

        if (socketpair(AF_UNIX, SOCK_DGRAM, 0, fd) < 0)
            err_sys("socketpair error");
        pfd[i].fd = fd[0];
        pfd[i].events = POLLIN;
        ti[i].qid = qid[i];
        ti[i].fd = fd[1];
        if (pthread_cond_init(&ti[i].ready, NULL) != 0)
            err_sys("pthread_cond_init error");
        if (pthread_mutex_init(&ti[i].mutex, NULL) != 0)
            err_sys("pthread_mutex_init error");
        if ((err = pthread_create(&tid[i], NULL, helper,
            &ti[i])) != 0)
            err_exit(err, "pthread_create error");
    }
}
```
