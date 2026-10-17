
这里可能存在一些冗余。

### 6.4.1 IP 地址

对于普通人来说，互联网是新闻、商业和娱乐的场所。对于程序员来说，互联网是一个用于产生和消费 TCP/IP 数据包的软件接口。互联网上交换的各种信息最终转化为 TCP/IP 数据包。因此，观察 TCP/IP 数据包是一个很好的起点。

### TCP/IP 数据包

假设互联网上的某台服务器想向连接到它的台主机计算机发送数据。我们可以将数据视为一个比特流：

`$b_0, b_1, b_2, \dots$`

第一步是将比特流拆分为以下类型的传输控制协议（TCP）数据包：

`$b_0, b_1, \dots, b_k$` 源端口 + 目的端口 + 序列号 + 更多 TCP 信息。

一个 TCP 数据包的字节数可达 64 KB，但如此大的数据包并不常见。源端口识别服务器上发送数据的应用程序，而目的端口识别客户端上的应用程序。当 TCP 数据包到达时，操作系统内核会查看目的地址以将数据包路由到正确的应用程序。数据包持有发送者正在传输的比特流分段，可能会无序到达目的地。数据包可能从源地到目的地采取不同的路由。操作系统内核使用 32 位序列号对 TCP 分段进行排序。目的处的应用程序看到的与源地传输的相同的比特。

数据包在从源地到目的地的过程中会在路由器之间跳跃（hop）。路由由互联网协议（IP）信息决定。IP 数据包如下：

TCP 数据包 + 源地址 + 目的地址 + 更多 IP 信息。

路由器不查看 TCP/IP 数据包中 TCP 部分内部的数据。它们的工作是查看目的地址并将数据包发送到目的地或其他路由器。例如，如果服务器是 `www.xsede.org`，那么文本字符串 `www.xsede.org` 对应一个 IP 地址。客户端计算机也有一个 IP 地址。这两个 IP 地址都会出现在 IP 头部。

在大多数情况下，互联网可以等同于 TCP/IP 协议。TCP/IP 协议是一种软件标准。它对计算机之间传输数据包的硬件不做任何假设。当一个 IP 数据包准备好传输时，操作系统内核将其交给设备驱动程序。依赖硬件的信息由设备驱动程序处理，并超出 TCP/IP 协议的范畴。

作者的桌面电脑通过以太网连接到互联网。以太网是一种基于同轴光电缆的多接入网络。在多接入网络中，许多计算机使用同一根电缆进行通信（以太网是）。设备驱动程序将 TCP/IP 数据包转换为以太网包（frame）。

介质访问控制（MAC）地址识别通过以太网转发的数据包包。TCP/IP 数据包包含了目的地址，该地址可能在数英里之外。MAC 地址 识别位于同一建筑的路由器。地址解析协议（ARP）用于从 IP 地址推出 MAC 地址。MAC 地址是可以预测的，并存储在 ARP 缓存中。以太网数据包限制为 1500 字节，这是最大传输单元（MTU）在作者桌面上的配置（MTU 由 `ifconfig` 命令报告）。内核确保 TCP/IP 数据包适应单个 MTU。

在通过光纤连接的路由器之间，或者对于通过以太网以外的技术连接到互联网的主机，MTU 可能不是 1500 字节。即使是以太网连接也可以配置使用非 1500 字节的 MTU。MTU 对硬件的依赖性与 TCP/IP 的硬件无关性意味着 IP 数据包的分片不可避免。如果到达路由器的 IP 数据包对于下一跳来说太大，路由器必须对 IP 数据包进行分片，接收端必须进行重组。互联网流量中 IP 数据包分片的频率尚不明。

IP 地址对于互联网架构至关重要。数据以 TCP/IP 数据包的形式离开源计算机。TCP/IP 数据包从路由器传输到目的地。在每次跳跃中，都会检查目的地址以确定使用的硬件链路路由数据包。IP 地址对于应用程序和硬件链路都是可见的。

下面定义的函数接收如 `www.xdeorg` 的字符字符串作为唯一参数（`inaddr`），并返回网络栈各层可以理解的格式的 IP 地址。

```c
struct addrinfo *saddrlist(const char *inaddr){
    struct addrinfo hint;
    memset(&hint, 0, sizeof(hint));
    hint.ai_family = AF_UNSPEC;
    hint.ai_socktype = SOCK_STREAM;
    getaddrinfo(inaddr, NULL, &hint, &llist);
    return llist;
}
```

在第 2 行，该函数将 `hint` 定义为 `struct addrinfo` 类型。该函数返回指向 `struct addrinfo` 的指针。`sockets` API 不是互联网世界清洁设计的最佳示例。然而，`struct addrinfo` 让 API 变得更加易用。它的定义如下：

```c
struct addrinfo {
    int ai_flags;
    int ai_family;
    int ai_socktype;
    int ai_protocol;
    socklen_t ai_addrlen;
    struct sockaddr *ai_addr;
}
```

## 第 6 章 特殊主题：网络与消息传递

```c
char *ai_canonname;
struct addrinfo *ai_next;
```

最后一个字段 `ai_next` 是一个指针，链接到链表中的另一个 `struct addrinfo` 对象。我们将在其他字段出现时进行解释。在 `saddrlist()` 的第 3 行中，`memset()` 将提示对象的所有字段设置为零。第 4 行和第 5 行分别将 `ai_family` 和 `ai_socktype` 设置为 `AF_UNSPEC` 和 `SOCK_STREAM`。地址族可以是 IPv4 或 IPv6。通过指定 `AF_UNSPEC`，我们允许它是其中任何一种。套接类型 TCP 使用 `SOCK_STREAM`。对于数据报和控制消息还有其他类型。在很大程度上，互联网是由 TCP 套接驱动的。我们可以将其设置为特定值，以将提示限制为 TCP、UDP 或多播。

`getaddrinfo()` 的实际调用位于 `saddrlist()` 的第 7 行。`getaddrinfo()` 函数在成功时返回 0，否则返回各种错误代码。由于我们的目标仅仅是说明 TCP/IP，因此省略了所有的错误处理。第一个参数 `inaddr` 可以是 `NULL`、`www.xsede` 或其他互联网地址。第二个参数给为 `NULL`，但可以使用特定值来指定服务，如 `http` 或 `ssh`。第三个参数是指向提示的指针。最后一个参数是指向 `llist` 的指针。在 `saddrlist()` 的第 6 行中，变量 `llist` 定义为类型 `struct addrinfo *`。返回时，它是一个指向 `struct addrinfo` 对象链表的指针，每个对象都持有关于与 `inaddr` 参数对应并符合提示的套接字信息。

下文定义的函数 `printlist()` 遍历 `llist` 并打印链表每个节点中包含的部分信息。

```c
void printlist(struct addrinfo *llist){
    while(llist != NULL) {
        printinfo(llist);
        llist = llist->ai_next;
    }
}
```

实际的打印工作由 `printinfo()` 函数完成。

```c
1 void printinfo(struct addrinfo *p){
2     char ipver[200];
3  void *addr;
4  if(p->ai_family==AF_INET){
5      struct sockaddr_in *ipv4 =
6      (struct sockaddr_in *)p->ai_addr;
7      addr = &(ipv4->sin_addr);
8      strcpy(ipver, "IPv4");
9  } else if(p->ai_family==AF_INET6){
10      struct sockaddr_in6 *ipv6 =
11      (struct sockaddr_in6 *)p->ai_addr;
12      addr = &(ipv6->sin_addr);
13      strcpy(ipver, "IPv6");
14  } else
15      return;
16      char ipstr[INET_ADDRRLEN];
17      inet_ntop(p->ai_family, addr, ipstr, INET_ADDRRLEN);
18      cout << ipver << ": " << ipstr << endl;
19 }
```

该函数是本书中面向对象编程的唯一示例，且除某行外，它是纯 C 语言编写的。`struct addr *p` 可以是 IPv4 或 IPv6 地址。IPv4 地址在第 4 行到第 9 行的 `if` 块中处理，IPv6 地址在第 10 行到第 15 行的 `else` 块中处理。主要区别在于对 `p->ai_addr` 的解释（第 5/6和11/12 行）。在任何情况下，指针 `addr` 指向提取出的 IP 地址（第 7和13 行）。IPv4 地址为 32 位，IPv6 地址为 64 位。第 17 行的函数调用 `inet_ntop()` 将 IP 地址转换为更易读的格式。为了完整理解，我们将研究 `struct sockaddr`, `addr` 和 `sockaddr_in6`。我们只需提到前两个是存储地址族的短整型，而 `sockaddr_in6` 有两个额外的字节来适应更长的 IPv6 地址。

## 6.4. 互联网

IPv4 地址只有 32 位，可以取 40 亿不同的值（尽管并非所有值都是有效的）。通过台式机、笔记本电脑和移动设备，连接到互联网的节点非常多，以至于地址空间在 IPv6 中扩展到了 64 位。

### 6.4.2 发送与接收

每个网络接口都涉及数据的收发。我们使用以下函数发送数据：

```c
int block_send(int sockfd, void *buf, int len){
    int total_sent = 0;
    int num_sends = 0;
    while(total_sent < len){
        int ns = send(sockfd, buf, len-total_sent, 0);
        buf = (char *)buf+ns;
        total_sent += ns;
        num_sends += 1;
    }
    return num_sends;
}
```

该函数从缓冲区 `buf` 中发送 `len` 字节。发送目标由套接字文件描述符 `sockfd` 决定（第 1 行）。要以 TCP/IP 数据包的形式发送数据，Linux 内核需要目的地的 IP 地址以及源和目的的端口号。没有端口号就无法识别发送接收应用程序。尽管套接字文件描述符 `sockfd` 仅仅是一个 `int`，但 Linux 内核可以使用它来查找目的地的 IP 地址以及源和目的的端口号。这些信息对应用程序是隐藏的，尽管有方法获取它们。套接字文件描述符的设置方法稍后描述。

`block_send` 函数使用了 Linux 系统调用 `send()`（第 5 行）。第一个参数是套接字描述符，第二个参数是缓冲区，第三个参数是要发送的字节数。最后一个参数是标志，在第 5 行给出 0。其他标志值（如 `MSG_MORE`）可更改套接字行为。`send()` 可能不会传输所有数据。它返回传输的字节数，出错时返回 -1。（第 4 行到第 9 行）反复调用 `send()` 直到所有数据发送完毕。

接收函数非常相似。

```c
1 int block_recv(int sockfd, void *buf, int len){
2 int total_recv = 0;
3 int num_recv = 0;
4 while(total_recv < len){
5 int nr = recv(sockfd, buf, len-total_recv, 0);
6 if(nr==0){
7 num_recv=0;
8 break;
9 }
10 buf = (char *)buf+nr;
11 total_recv += nr;
12 num_recv += 1;
13 }
14 return num_recv;
15 }
```

### 6.4.3 服务器

服务器启动时打开套接字并将其绑定到端口。

```c
const char* PORTNUM="28537";
int bindport(const char* portnum){
  struct addrinfo hint;
  hint.ai_family = AF_UNSPEC;
  hint.ai_socktype = SOCK_STREAM;
  hint.ai_flags = AI_PASSIVE;
  struct addrinfo *list;
  getaddrinfo(NULL, portnum, &hint, &list);
  int socket = socket(list->ai_family, list->ai_socktype, list->ai_protocol);
  bind(socket, list->ai_addr, list->ai_addrlen);
  int backlog=10;
  listen(socket, backlog);
  int yes = 1;
  setsockopt(socket, SOL_SOCKET, SO_REUSEADDR, &yes, sizeof(int));
  return socket;
}
```

# 484 第 6 章 特别主题：网络与消息传递

作用是隐藏端口号从主机格式到网络格式的转换（最可能是从小端转换为大端端格式）。

第 13 行的系统调用 `listen()` 将 socket 标记为监听状态，队列长度为 10。系统套字 `socketport` 将保留最多 10 个等待连接的客户端，且不会更多。系统调用 `listen()` 是非阻塞的。它并不会真正开始监听。

第 15 行和 16 行使用 `setsockopt()` 确保服务器关闭后端口地址可以安全重用。此函数返回 socket 文件描述符 `socketport`（第 17 行）。

许多服务器都有防火墙，会阻止所有端口的入站连接，除了少数几个。为了让此程序运行，必须修改防火墙以接受端口 28537 的连接。

一旦 socket 绑定到端口并标记为监听，它就准备好接受连接了。

```c
int connect2(int socketport){
    int socketclient;
    socketclient = accept(socketport, NULL, NULL);
    return socketclient;
}
```

系统调用 `accept()` 的第一个参数是 socket 描述符。第二个参数可以是指向另一个 socket 地址的指针。在这里，`socketport` 已经绑定到本地端口并标记为监听。因此，第二个参数必须为 `NULL`。第三个参数是第二个参数所指向的结构体的大小，它也必须为 `NULL`。在默认情况下，系统调用 `accept()` 会阻塞直到连接建立。它在此处返回一个名为 `socketclient` 的 socket。操作系统内核可以使用此 socket 找到客户端的 IP 地址，以及该连接在客户端和服务器上的端口号。端口号 28537 被服务器用于监听连接。一旦连接建立，服务器端和客户端都将获得不同的端口号。端口号由 Linux 内核动态生成。如果服务器是多线程的，它在服务客户端时可能会接受新的连接。

在连接到客户端后，服务器运行以下函数：

```c
void partialsum_server(int socket2, int blocksize){
    double *recvbuf = new double[blocksize];
    double *sendbuf = new double[blocksize];
```

```c
4    double S=0;
5    while(1){
6        int ncrev=block_recv(sock2client, recvbuf,
7                               8*blocksize);
8        if(ncrev==0)
9            break;
10       for(int i=0; i < blocksize; i++){
11            S += recvbuf[i];
12            sendbuf[i] = S;
13       }
14       block_send(sock2client, sendbuf, 8*blocksize);
15   }
16   close(sock2client);
17   delete[] recvbuf;
18   delete[] sendbuf;
19 }
```

该函数使用第 4 行定义的变量 `S` 来跟踪部分和。在第 6 行，它在缓冲区 `recvbuf[]`（第 2 行分配）中接收 `blocksize` 个双精度浮点数。如果返回值 `ncrev` 为 0，则客户端已终止连接，服务器在第 9 行跳出 `while` 循环。如果接收到一组数字，它会更新部分和并将其存储在 `sendbuf[]` 中（第 11 行和 12 行）。部分和数组被发送回客户端（第 13 行）。

服务器调用以下函数：

```c
void server(int blocksize){
    int sock2port= bind2port(PORTNUM);
```
