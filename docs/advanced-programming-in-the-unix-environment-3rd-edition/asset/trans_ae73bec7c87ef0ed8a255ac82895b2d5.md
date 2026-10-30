

## 示例 — 无连接服务器

图 16.20 中的程序是 uptime 服务器的数据报版本。

```
#include "apue.h"
#include <netdb.h>
#include <errno.h>
#include <syslog.h>
#include <sys/socket.h>

#define BUFLEN 128
#define MAXADDRLEN 256

#ifndef HOST_NAME_MAX
#define HOST_NAME_MAX 256
#endif

extern int initserver(int, const struct sockaddr *, socklen_t, int);
void
serve(int sockfd)
{
    int n;
    socklen_t alen;
    FILE *fp;
    char buf[BUFLEN];
    char abuf[MAXADDRLEN];
    struct sockaddr *addr = (struct sockaddr *)abuf;

    set_cloexec(sockfd);
    for (;;) {
        alen = MAXADDRLEN;
        if ((n = recvfrom(sockfd, buf, BUFLEN, 0, addr, &alen)) < 0) {
            syslog(LOG_ERR, "ruptimed: recvfrom error: %s", strerror(errno));
            exit(1);
        }
        if ((fp = popen("/usr/bin/uptime", "r")) == NULL) {
            sprintf(buf, "error: %s\n", strerror(errno));
            sendto(sockfd, buf, strlen(buf), 0, addr, alen);
        } else {
            if (fgets(buf, BUFLEN, fp) != NULL)
                sendto(sockfd, buf, strlen(buf), 0, addr, alen);
            pclose(fp);
        }
    }
}
int
main(int argc, char *argv[])
{
    struct addrinfo *ailist, *aip;
    struct addrinfo hint;
    int sockfd, err, n;
    char *host;
```
```
if (argc != 1)
    err_quit("usage: ruptime");
if ((n = sysconf(_SC_HOST_NAME_MAX)) < 0)
    n = HOST_NAME_MAX; /* best guess */
if ((host = malloc(n)) == NULL)
    err_sys("malloc error");
if (gethostname(host, n) < 0)
    err_sys("gethostname error");
daemonize("ruptimed");
memset(&hint, 0, sizeof(hint));
hint.ai_flags = AI_CANONNAME;
hint.ai_socktype = SOCK_DGRAM;
hint.ai_canonname = NULL;
hint.ai_addr = NULL;
hint.ai_next = NULL;
if ((err = getaddrinfo(host, "ruptime", &hint, &ailist)) != 0) {
    syslog(LOG_ERR, "ruptime: getaddrinfo error: %s",
        gai_strerror(err));
    exit(1);
}
for (aip = ailist; aip != NULL; aip = aip->ai_next) {
    if ((sockfd = initserver(SOCK_DGRAM, aip->ai_addr,
        aip->ai_addrlen, 0)) >= 0) {
        serve(sockfd);
        exit(0);
    }
}
exit(1);
}
```

# 图 16.20 通过数据报提供系统运行时间的服务器

服务器在 recvfrom 中阻塞以等待服务请求。当请求到达时，我们保存请求者的地址并使用 popen 运行 uptime 命令。我们使用 sendto 函数将输出发送回客户端，目标地址设置为请求者的地址。

## 16.6 套接字选项

套接字机制为我们提供了两个套接字选项接口来控制套接字的行为。一个接口用于设置选项，另一个接口允许我们查询选项的状态。我们可以获取和设置三种选项：

- 1. 适用于所有套接字类型的通用选项
- 2. 在套接字级别管理的选项，但依赖于底层协议的支持
- 3. 每个单独协议特有的协议特定选项

单一 UNIX 规范仅定义了套接字层选项（前述列表中的前两种选项类型）。

我们可以使用 setsockopt 函数设置套接字选项。

```
#include <sys/socket.h>
int setsockopt(int sockfd, int level, int option, const void *val,
    socklen_t len);
Returns: 0 if OK, -1 on error
```

level 参数标识选项适用的协议。如果选项是通用套接字级选项，则 level 设置为 SOL_SOCKET。否则，level 设置为控制该选项的协议的编号。示例为 TCP 选项的 IPPROTO_TCP 和 IP 选项的 IPPROTO_IP。图 16.21 总结了单一 UNIX 规范定义的通用套接字级选项。

| 选项 | val 参数的类型 | 描述 |
|---|---|---|
| SO_ACCEPTCONN | int | 返回套接字是否已启用监听（仅 getsockopt）。 |
| SO_BROADCAST | int | 如果 *val 非零则广播数据报。 |
| SO_DEBUG | int | 如果 *val 非零则在网络驱动中启用调试。 |
| SO_DONTROUTE | int | 如果 *val 非零则绕过正常路由。 |
| SO_ERROR | int | 返回并清除挂起的套接字错误（仅 getsockopt）。 |
| SO_KEEPALIVE | int | 如果 *val 非零则启用周期性保活消息。 |
| SO_LINGER | struct linger | 关闭套接字时存在未发送消息时的延迟时间。 |
| SO_OOBINLINE | int | 如果 *val 非零则带外数据与正常数据内联放置。 |
| SO_RCVBUF | int | 接收缓冲区的大小（字节）。 |
| SO_RCVLOWAT | int | 接收调用返回的最小数据量（字节）。 |
| SO_RCVTIMEO | struct timeval | 套接字接收调用的超时值。 |
| SO_REUSEADDR | int | 如果 *val 非零则在 bind 时重用地址。 |
| SO_SNDBUF | int | 发送缓冲区的大小（字节）。 |
| SO_SNDLOWAT | int | 发送调用中传输的最小数据量（字节）。 |
| SO_SNDTIMEO | struct timeval | 套接字发送调用的超时值。 |
| SO_TYPE | int | 标识套接字类型（仅 getsockopt）。 |

图 16.21 套接字选项

val 参数指向数据结构或整数，具体取决于选项。某些选项是开/关开关。如果整数非零，则启用该选项。如果整数为零，则禁用该选项。len 参数指定 val 指向的对象的大小。
我们可以使用 getsockopt 函数查找选项的当前值。

```
#include <sys/socket.h>
int getsockopt(int sockfd, int level, int option, void *restrict val,
    socklen_t *restrict lenp);
Returns: 0 if OK, -1 on error
```

lenp 参数是指向整数的指针。在调用 getsockopt 之前，我们将整数设置为选项将被复制到的缓冲区的大小。如果选项的实际大小大于此大小，则选项会被静默截断。如果选项的实际大小小于此大小，则在返回时整数将被更新为实际大小。

## 示例

图 16.12 中的函数在服务器终止后立即尝试重新启动时无法正常运行。通常，TCP 的实现会阻止我们在超时到期之前绑定相同的地址，该超时通常在数分钟量级。幸运的是，SO_REUSEADDR 套接字选项允许我们绕过此限制，如图 16.22 所示。

```
#include "apue.h"
#include <errno.h>
#include <sys/socket.h>

int
initserver(int type, const struct sockaddr *addr, socklen_t alen,
    int qlen)
{
    int fd, err;
    int reuse = 1;

    if ((fd = socket(addr->sa_family, type, 0)) < 0)
        return(-1);
    if (setsockopt(fd, SOL_SOCKET, SO_REUSEADDR, &reuse,
        sizeof(int)) < 0)
        goto err_out;
    if (bind(fd, addr, alen) < 0)
        goto err_out;
    if (type == SOCK_STREAM || type == SOCK_SEQPACKET)
        if (listen(fd, qlen) < 0)
            goto err_out;
    return(fd);

err_out:
    err = errno;
    close(fd);
    errno = err;
    return(-1);
}
```

图 16.22 使用地址重用初始化服务器的套接字端点

要启用 SO_REUSEADDR 选项，我们将一个整数设置为非零值并将整数的地址作为 val 参数传递给 setsockopt。我们将 len 参数设置为整数的大小以指示 val 指向的对象的大小。

## 16.7 带外数据

带外数据是某些通信协议支持的可选功能，允许比正常数据更高优先级的交付。带外数据会在任何已排队待传输的数据之前发送。TCP 支持带外数据，但 UDP 不支持。带外数据的套接字接口受 TCP 对带外数据的实现影响很大。

TCP 将带外数据称为“紧急”数据。TCP 仅支持一个字节的紧急数据，但允许紧急数据与正常数据交付机制分开交付。要生成紧急数据，我们为三个发送函数中的任何一个指定 MSG_OOB 标志。如果我们使用 MSG_OOB 标志发送超过一个字节，最后一个字节将被视为紧急数据字节。

当收到紧急数据时，如果我们已通过套接字安排信号生成，我们会收到 SIGURG 信号。在第 3.14 节和 14.5.2 节中，我们看到可以使用 F_SETOWN 命令对 fcntl 设置套接字的所有权。如果 fcntl 的第三个参数为正，则它指定进程 ID。如果它为负值且不为 -1，则表示进程组 ID。因此，我们可以通过调用来安排我们的进程从套接字接收信号

```
fcntl(sockfd, F_SETOWN, pid);
```

F_GETOWN 命令可用于检索当前套接字所有权。与 F_SETOWN 命令一样，负值表示进程组 ID，正值表示进程 ID。因此，调用

```
owner = fcntl(sockfd, F_GETOWN, 0);
```

将返回 owner 等于配置为从套接字接收信号的进程的 ID，如果 owner 为正；如果 owner 为负，则 owner 的绝对值等于配置为从套接字接收信号的进程组的 ID。

TCP 支持紧急标记的概念：正常数据流中紧急数据将要去的位置。我们可以选择使用 SO_OOBINLINE 套接字选项将紧急数据与正常数据内联接收。为了帮助我们识别何时到达紧急标记，我们可以使用 socketmark 函数。

```
#include <sys/socket.h>
int socketmark(int sockfd);
Returns: 1 if at mark, 0 if not at mark, -1 on error
```

当下一个要读取的字节位于紧急标记处时，socketmark 将返回 1。

当套接字的读取队列中存在带外数据时，select 函数（第 14.4.1 节）将返回文件描述符具有挂起的异常条件。我们可以选择将紧急数据与正常数据内联接收，或使用 MSG_OOB 标志与 recv 函数之一接收紧急数据，以优先于任何其他队列数据。TCP 仅排队一个字节的紧急数据。如果在我们接收当前字节之前到达另一个紧急字节，则现有字节将被丢弃。

