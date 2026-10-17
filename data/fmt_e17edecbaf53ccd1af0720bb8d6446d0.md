
`struct sockaddr_in` 包含了连接信息，包括 IP 和端口。它在 `bind()` 函数相当于电话号码。在详细层面，首先使用 `memset()` 函数对结构进行零值清空。这样做是为了确保结构中未使用的部分为零。然后向结构中填充关于如何使用 socket 的信息。`htons()` 函数是这类函数之一，用于确保字节顺序符合网络传输的要求。在 `bind()` 调用中，地址值 `INADDR_ANY` 表示 socket 应该绑定到当前执行进程的机器的 IP 上。在示例中，服务器将在自己的 IP 端口号 60000 上监听。

### 7.5.2.3 listen()

绑定后，服务器通常会调用 `listen()` 函数来等待通信：

```c
int i,sock;

/* socket 已创建并绑定 ... */

/* 监听 */
i=listen(sock,5);
if (i < 0)
    printf("listen failed\n");
```

`listen` 函数的第二个参数描述了当服务器处理另一个通信时可以队列多少连接。在示例中，操作系统将队列多五个连接尝试，然后再向尝试连接的客户端返回错误值。

### 7.5.2.4 connect()

客户端执行一个与绑定类似的步骤，但它不是在监听，而是主动拨号以建立连接。例如：

```c
int i,sock;
struct sockaddr_in addr_send;
char *server_ip="130.127.24.92";
unsigned short server_port=60000;
```

```c
/* socket 已创建 ... */
```

# 256 第 7 章 系统调用

```c
/* 创建用于连接的套接字地址结构 */
memset(&addr_send, 0, sizeof(addr_send)); /* 清空结构 */
addr_send.sin_family = AF_INET; /* 地址族 */
addr_send.sin_s_addr = inet_addr(server_ip);
addr_send.sin_port = htons(server_port);
```

```c
/* 连接到服务器 */
i=connect(sock, (struct sockaddr *) &addr_send,
sizeof(addr_send));
if (i < 0)
printf("connect failed\n");
```

在例示例中，`struct sockaddr_in` 结构体填充了客户端想要连接的服务器信息。`connect()` 函数用于调用服务器以尝试建立连接。

## 7.5.2.5 accept()

一旦服务器接收到传入的连接请求，它就可以接受该连接。例如：

```c
int                 i,sock,sock_recv,addr_size;
struct sockaddr_in   recv_addr;
```

```c
/* ... 套接字创建、绑定并监听 ... */
/* 传入的连接 -- 获取新的接收数据套接字 */
addr_size=sizeof(addr_recv);
sock_recv=accept(sock, (struct sockaddr *) &recv_addr,
&addr_size);
```

`accept()` 函数返回第二个套接字（在本例中为 `sock_recv`），数据将在该上面传输。这使得原始套接字（在本例中为 `sock`）能够继续监听额外的连接。

## 7.5.2.6 send() and recv()

在客户端和服务器建立连接后，就可以传输和接收数据。例如，客户端可以执行以下代码：

```c
int sock_bytes_sent;
char text[80];
/* ... 套接字已创建并连接 ... */
```

```c
/* 发送一些数据 */
printf("Send? ");
scanf("%s",text);
bytes_send=send(sock,text,strlen(text),0);
```

`send()` 函数接受四个参数：套接字标识符、指向数据的地址、要发送的字节数以及标志位设置。通常标志位的值设置为零。服务器执行类似的代码来接收数据。
例如：

```c
int sock_recv,bytes_received;
char text[80];
/* ... 套接字创建、绑定并接受 ... */
/* 接收一些数据 */
bytes_received=recv(sock_recv,text,80,0);
text[bytes_received]=\0';
printf("Received: %s\n",text);
```

`recv()` 函数调用的参数与 `send()` 类似，但第三个参数（在本例中为 80）表示可以接收的最大字节数。服务器和客户端都可以执行 `send()` 和 `recv()`；通信可以是双向的。同时注意，数据并不一定必须双向。`send()` 和 `recv()` 函数与 `fread()` 和 `fwrite()` 函数相似，它们的参数定义了一个地址和字节数，而不是给定地址处的数据类型。

## 7.5.2.7 close()

一旦通信完成，服务器和客户端都应该关闭各自的套接字。例如：

```c
int i,sock_recv;
/* ... 套接字通信完成 ... */
i=close(sock_recv);
if (i < 0)
    printf("close failed\n");
```

`close()` 系统调用会在操作系统内部启动一系列操作以终止连接。因此，套接字可能仍会在 `netstat` 列表中出现几秒钟，直到操作系统完成关闭操作。

## 7.5.3 示例

在节一节中，将发起网络通信与拨打电话进行了类比。然而，与电话通信（通信大多是人对人的）不同，在网络编程中，除了一对一的进程通信外，还有各种情况。呼叫者可能想要广播公告，同时调用整个子网的通信。呼叫者可能打开一个套接字并用它同时与多个远程进程进行通信。服务器一次只接受一个调用，也可以向多个并发调用开放。这些调用可以通过同一个端口进行所有管理，或者服务器可以在一个端口上接收多个传入的调用，并在不同的临时端口上为每个调用管理通信。这些只是可以使用套接字系统调用的一些情况。以下两个示例演示了两种特定情况，并为每种情况详细介绍了客户端和服务器程序。

### 7.5.3.1 单服务器-客户端连接

以下程序将第 7.5.2 节所有的思想整合到一个服务器程序和一个客户端程序中。服务器在端口 60000 上监听客户端，当客户端连接时，服务器读取任何传入的数据并一次打印一行。如果服务器接收到字符串 "shutdown"，那么它将关闭套接字并退出。

以下代码是用于服务器的：

```c
#include <stdio.h>
#include <sys/types.h> /* 系统类型定义 */
#include <sys/socket.h> /* 网络系统函数 */
#include <netinet/in.h> /* 协议与结构定义 */
#define BUF_SIZE      1024
#define LISTEN_PORT  60000
int main(int argc, char *argv[])
{
    int                 sock_listen,sock_recv;
    struct sockaddr_in   my_addr;
    struct sockaddr_in   recv_addr;
    int                 i,addr_size,bytes_received;
    char                buf[BUF_SIZE];
    fd_set              readfds;
    struct timeval      timeout={0,0};
    int                 incoming_len;
    struct sockaddr_in   remote_addr;
    int                 sock_listen;
    int                 sock_recv;
    int                 bytes_send,send_len,msg_size;
    int                 select_ret;
    /* ... 套接字创建、绑定并监听 ... */
    /* 传入的连接 -- 获取新的接收数据套接字 */
    addr_size=sizeof(recv_addr);
    sock_recv=accept(sock, (struct sockaddr *) &recv_addr,
    &addr_size);
    while (1)
    {
        FD_ZERO(&readfds);
        FD_SET(sock_recv, &readfds);
        if (select(sock_recv + 1, &readfds, NULL, NULL, &timeout) > 0)
        {
            bytes_received=recv(sock_recv,buf,80,0);
            buf[bytes_received]=\0;
            printf("Received: %s\n",buf);
            if (strcmp(buf,"shutdown") == 0)
                break;
        }
    }
    close(sock_recv);
    close(sock_listen);
}
```
*(注：由于原文提供的代码块在示例中存在严重的格式混乱和重复，翻译时根据逻辑对代码结构进行了对齐还原，以确保可读性并保留了所有逻辑含义)*

注意，服务器并不管理多个客户端。它允许一个客户端连接并与其通信。以下代码是用于客户端的：

```c
#include <stdio.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <string.h>
#include <unistd.h>
#define BUF_SIZE      1024
#define SERVER_IP "127.0.0.1"
#define SERVER_PORT 60000
int main(int argc, char *argv[])
{
    int sock_send;
    struct sockaddr_in addr_send;
    int i;
    char text[80],buf[BUF_SIZE];
    int bytes_sent,send_len;
    /* 创建用于发送数据的套接字 */
    sock_send=socket(PF_INET, SOCK_STREAM, 0);
    if (sock_send < 0)
    {
        printf("socket() failed\n");
        exit(0);
    }
    /* 创建用于连接的套接字地址结构 */
    memset(&addr_send, 0, sizeof(addr_send)); /* 清空结构 */
    addr_send.sin_family = AF_INET; /* 地址族 */
    addr_send.sin_s_addr = inet_addr(SERVER_IP);
    addr_send.sin_port = htons(SERVER_PORT);
    /* 连接到服务器 */
    i=connect(sock_send, (struct sockaddr *) &addr_send,
sizeof(addr_send));
    if (i < 0)
    {
        printf("connect failed\n");
        exit(0);
    }
    while (1)
    {
        /* 发送一些数据 */
        printf("Send? ");
        scanf("%s",text);
        if (strcmp(text,"quit") == 0)
            break;
        strcpy(buf,text);
        send_len=strlen(text);
        bytes_sent=send(sock_send,buf,send_len,0);
    }
    close(sock_send);
}
```

### 7.5.3.2 多个并发客户端

此示例的操作与上一个示例类似，但服务器在同一个端口上管理多个并发连接。服务器创建套接字并绑定的方式与上一个示例完全相同。然而，服务器不再使用 `listen()` 函数，而是使用 `select()` 函数来监听流量

## 第7 章 • 系统调用

该 socket。`select()` 函数被赋予一个零超时值，以便它不会阻塞。如果 socket 上没有接收到任何内容，程序将继续。如果接收到了内容，服务器将使用 `recvfrom()` 系统调用直接读取入站数据。它不会创建第二个 socket 来管理通信。这允许服务器能够在一个单一 socket 上接收来自任意数量客户端的数据。

以下是服务器的代码：

```c
#include <stdio.h>
#include <sys/types.h> /* 系统类型定义 */
#include <sys/socket.h> /* 网络系统函数 */
#include <netinet/in.h> /* 协议与结构体定义 */
#define BUF_SIZE 1024
#define LIST_PORT 60000
int main(int argc,char *argv[])
{
    int sock_recv;
    struct sockaddr_in my_addr;
    int i;
    fd_set readfds;
    struct timeval timeout={0,0};
    int incoming_len;
    struct sockaddr_in remote_addr;
    int recv_msg_size;
    char buf[BUF_SIZE];
    int select_ret;
    /* 创建接收用的 socket */
    sock_recv=socket(PF_INET, SOCK_DGRAM, IPPROTO_UDP);
    if (sock_recv < 0)
    {
        printf("socket() failed\n");
        exit(0);
    }
    /* 本地地址结构 */
    memset(&my_addr, 0, sizeof(my_addr)); /* 清空结构体 */
    my_addr.sin_family = AF_INET;      /* 地址族 */
    my_addr.sin_addr.s_addr = htonl(INADDR_ANY); /* 当前 IP * */
    my_addr.sin_port = htons((unsigned short)LIST_PORT);
    /* 将 socket 绑定到本地地址 */
    i=bind(sock_recv, (struct sockaddr *) &my_addr, sizeof (my_addr));
    if (i < 0)
    {
        printf("bind failed\n");
        exit(0);
    }
    /* 监听 ... */
    while (1)
    {
        do
            {
                FD_ZERO(&readfds);               /* 清空 socket 集合 */
                FD_SET(sock_recv,&readfds);      /* 将 socket 加入监听列表 */
                select_ret=select(sock_recv+1,&readfds,NULL,NULL,&timeout);
                if (select_ret > 0)              /* 任何 socket 有数据到达？ */
                {
                    incoming_len=sizeof(remote_addr); /* 谁发给我们的？ */
                    recv_msg_size=recvfrom(sock_recv,buf,BUF_SIZE,0,
                                            (struct sockaddr *)&remote_addr,&incoming_len);
                    if (recv_msg_size > 0)         /* 发送了什么？ */
                    {
                        buf[recv_msg_size]='\0';
