
类似地，当以下条件之一成立时，套接字变为可写：

- 套接字发送缓冲区中可用空间的字节数大于或等于该套接字发送缓冲区低水位标记的当前大小。
- 连接的写半部分已关闭。对该套接字的任何写操作都会产生 SIGPIPE。
- 有一个套接字错误待处理。对该套接字的写操作不会阻塞并继续；它将返回错误（-1），并将 errno 标志设置为特定值。

如果套接字存在带外数据，或者该套接字仍恰好处于带外标记状态，则该套接字有一个待处理的异常条件。当发生错误时，select 函数调用会认为该套接字既可读又可写。现在让我们看一下清单 22.14，其中我们修改了前面章节提到的客户端 TCP 程序，以适应新引入的 select 调用：

### 清单 22.14：展示使用 select() 函数进行 I/O 多路复用的用法

```c
#include <sys/socket.h>
#include <sys/types.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <netdb.h>
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <unistd.h>
#include <errno.h>
#include <stdio_ext.h>

#define SERV_TCP_PORT 15555
#define SERV_HOST_ADDR "127.0.0.1"  /* host addr for server */

int main()
{

    int sock, bytes_received;
    char choice;
    char send_data[2048],recv_data[2048];
    struct hostent *host;
    struct sockaddr_in server_addr;
    int maxfd1;
    fd_set    reset;

    host = gethostbyname(SERV_HOST_ADDR);

    if ((sock = socket(AF_INET, SOCK_STREAM, 0)) == -1) {
        perror("socket");
        exit(1);
    }

    bzero(&(server_addr.sin_zero), sizeof(server_addr.sin_zero));
    server_addr.sin_family = AF_INET;
    server_addr.sin_port = htons(SERV_TCP_PORT);
    inet_pton(AF_INET, SERV_HOST_ADDR, &(server_addr.sin_addr));

    if (connect(sock, (struct sockaddr *)&server_addr,
                sizeof(struct sockaddr)) == -1)
    {
```

## 第 22 章

### recv 和 recvfrom 函数

recv 和 recvfrom 函数的签名如下：

```c
ssize_t recv(int s, void *buf, size_t len, int flags);

ssize_t recvfrom(int s, void *buf, size_t len,
                int flags, struct sockaddr *from,
                socklen_t *fromlen);
```

我们需要包含头文件 <sys/types.h> 和 <sys/socket.h> 才能使用这两个函数。这些函数用于在套接字连接后从套接字读取数据。recv() 函数用于已连接的 TCP 套接字，recvfrom() 函数用于从 UDP 套接字读取信息。这两个函数有一些共同参数；两者都包含一个套接字描述符，由整数值 “s” 表示。一个指向缓冲区的指针，由 “buf” 表示，该缓冲区将包含正在读取的信息。另一个参数是字节大小，由参数 “len” 表示，参数 “flags” 控制这些函数的不同功能。除了所有这些参数之外，recvfrom 函数还接受一些额外参数，其中 “from” 参数指明信息来自何处。该函数调用还会给出数据来源的源套接字地址结构。“fromlen” 字段包含套接字地址结构的长度。表 22.3 列出了可提供给 “flags” 字段的不同值：

| 类型 | 描述 |
|---|---|
| **MSG_OOB** | 此标志表示“接收带外数据”。当设置 MSG_OOB 标志时，它表示应读取带外信息而不是普通信息。 |
| **MSG_PEEK** | 此标志帮助我们在不让系统丢弃信息的情况下查看可供读取的数据。 |
| **MSG_WAITALL** | 此标志告诉内核，在读取到请求的字节数之前不要从读操作返回。 |

这两个函数都返回实际接收的字节数。返回的值可能小于作为参数传入的长度。如果远程端关闭其连接端，则 recv() 函数返回零。

### send 和 sendto 函数

send 和 sendto 函数的签名如下：

```c
ssize_t send(int s, const void *buf, size_t len, int flags);

ssize_t sendto(int s, const void *buf, size_t len,
              int flags, const struct sockaddr *to,
              socklen_t tolen);
```

send 函数主要用于 TCP 连接，而 sendto 函数用于 UDP 无连接数据报套接字。对于无连接的情况，我们每次发送数据包时都需要指定目标地址。要指定目标地址，我们需要 sendto 函数调用的最后两个参数。参数 “s” 表示套接字，“buf” 是指向包含待发送数据的缓冲区的指针，“len” 是待发送的字节数。“flags” 参数告诉我们数据需要如何从客户端发送。如果该标志设置为零，则表示正常数据。让我们看看这些标志的一些值，如表 22.4 所示：

表 22.4：I/O 函数中使用的不同标志

| **类型** | **描述** |
|---|---|
| MSG_OOB | 对于 send 函数，此标志表示正在发送带外数据。这是一种告诉接收端该数据优先级高于普通数据的方式。 |
| MSG_DONTROUTE | 此标志告诉内核目标位于本地连接的网络中，我们无需执行路由表查找。此功能还作为 SO_DONTROUTE 的 setsockopt 选项获得了额外支持。 |
| MSG_DONTWAIT | 此标志表示非阻塞 I/O，而无需为套接字打开非阻塞标志。此选项执行 I/O 操作并关闭非阻塞标志。这就像仅为此发送启用非阻塞选项。 |
| MSG_NOSIGNAL | 当我们要发送到不再接收的远程主机时，需要此标志。在这种情况下，我们通常会收到 SIGPIPE 信号。此标志可防止此类信号被引发。 |

这些函数返回实际发送的字节数。可能出现我们已发送的字节数少于我们想要发送的字节数的情况。如果连接已关闭，则调用 send() 的进程将收到 SIGPIPE 信号。

### readv 和 writev 函数

readv 和 writev 函数的签名如下：

```c
int readv(int filedes, const struct iovec *iov, size_t count);

int writev(int filedes, const struct iovec *iov, size_t count);
```

我们需要包含头文件 <sys/uio.h> 才能使用 readv 和 writev 函数。这两个函数的参数与 read() 和 write() 几乎相同，但它们允许我们通过一次函数调用从多个不同缓冲区读取，或向多个不同缓冲区写入。这些函数通常称为分散读（因为输入数据被分散到多个应用程序缓冲区中）和聚集写操作（因为多个缓冲区被聚集在一起用于单次输出操作）。第一个参数是进行函数调用所需的文件描述符。这两个函数的第二个参数都是指向 “iovec” 结构数组的指针。该结构在头文件 <sys/uio.h> 中定义如下：

```c
struct iovec {
    void  *iov_base;    /* starting address of the buffer */
    size_t  iov_len;    /* size of the buffer */
};
```

对于 iovec 结构数组中的元素数量，实现允许的数量有一些限制。以 4.4BSD 为例，它允许 iovec 结构中最多 1024 个元素，而 Solaris 2.5 的上限是 16。readv 和 writev 函数可用于任何类型的描述符；它们不限于仅用于套接字。函数中提到的所有缓冲区都按数组顺序填充。这意味着 readv() 函数先填充 vector[0]，然后再继续处理 vector[1]。类似地，writev() 函数先写入 vector[0]，然后再转到 vector[1]。

### recvmsg 和 sendmsg 函数

还存在另一对读写函数，它们是所有 I/O 函数中最通用的。任何形式的读写操作都可以用这两个函数替代。recvmsg 和 sendmsg 函数的签名如下：

```c
ssize_t recvmsg(int socket, struct msghdr *message, int flags);
ssize_t sendmsg(int socket, struct msghdr *message, int flags);
```
