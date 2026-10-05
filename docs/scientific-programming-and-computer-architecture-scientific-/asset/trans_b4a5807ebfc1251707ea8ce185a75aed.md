

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

该函数使用第 4 行定义的变量 S 来跟踪部分和。在第 6 行，它在缓冲区 `recvbuf[]`（第 2 行分配）中接收 `blocksize` 个双精度浮点数。如果返回值 `ncrev` 为 0，则客户端已终止连接，服务器在第 9 行跳出 `while` 循环。如果接收到一组数字，它会更新部分和并将其存储在 `sendbuf[]` 中（第 11 行和 12 行）。部分和数组被发送回客户端（第 13 行）。

服务器调用以下函数：

```c
void server(int blocksize){
    int sock2port= bind2port(PORTNUM);
    while(1){
        int sock2client = connectclient(sock2port);
        partialsum_server(sock2client, blocksize);
    }
}
```

此函数绑定到端口 28537（即 `PORTNUM` 的值）并监听连接。一旦它与客户端建立连接，就会调用 `partialsum_server()`。

## 6.4.4 客户端

客户端在某些方面与服务器镜像，但在另一些方面不同。客户端首先与服务器建立连接。

```c
1 int connect2server(const char *server,
2 const char *portnum){
3 struct addrinfo hint;
4 memset(&hint, 0, sizeof(hint));
5 hint.ai_family = AF_UNSPEC;
6 hint.ai_socktype = SOCK_STREAM;
7 struct addrinfo *list;
8 getaddrinfo(server, portnum, &hint, &list);
9 int sock2server = socket(list->ai_family,
10 list->ai_socktype,
11 list->ai_protocol);
12 connect(sock2server, list->ai_addr,
13 list->ai_addrlen);
14 freeaddrinfo(list);
15 return sock2server
16 }
```

参数 `server`（第 1 行）是运行服务器的机器名称。例如可以是 `login.univ.edu`。`hint`（第 3 行）指定了族但未指定地址。第 7 行的 `getaddrinfo()` 调用不仅提供了服务器名称，但也指定了端口号。指定的端口号是该函数的第二个参数。它在第 9、10 和 11 行打开一个 socket。socket `sock2server` 在第 12 和 13 行通过 `connect()` 连接到服务器。在互联网上建立和终止连接的方式存在一些微妙之处，此处未讨论。系统调用 `connect()` 是 `accept()` 的客户端对应项。`connect()` 的第二个参数是 `sockaddr*` 类型。它所指向的结构体 `(*list)` 包含了服务器的 IP 地址以及预期监听的端口号。这由 `getaddrinfo()`（第 8 行）构造。原则上，为了健壮性，必须遍历该列表，直到其中一个连接尝试成功。由于前面的原因，未尝试检测和处理错误。

为了找到 `series` 的部分和，客户端使用以下程序：

```c
void partialsum_client(int sock2server,
    double *series, int n,
    int blocksize,
    double *psum,
    StatVector& stat_ts,
    StatVector& stat_tr){
  assert(n%blocksize==0);
  int count = n/blocksize;
  double cycles;
  Timestamp clk;
  for(int i=0; i < count; i++){
    clk.tick();
    int nsend=block_send(sock2server, series,
        8*blocksize);
    cycles = clk.toc();
    stat_ts.insert(cycles);
    clk.tick();
    int nrecv=block_recv(sock2server, psum,
        8*blocksize);
    cycles = clk.toc();
    stat_tr.insert(cycles);
    series += blocksize;
    psum += blocksize;
  }
  close(sock2server);
}
```

这里没什么新可说的。客户端交替调用 `block_send()` 发送 `series[]` 块，调用 `block_recv()` 将部分和存储在 `psum[]` 中。`block_send()` 和 `block_recv()` 的调用被计时。发送和接收期间的循环统计使用 `StatVector` 对象收集。客户端程序的列表由以下函数定义完成：

```c
void client(const char* server, int blocksize){
    int n;
  if(blocksize < 1000)
    n = 1000*blocksize*10;
  else
    n=1000*1000*20;
    n = (n/blocksize)*blocksize;
    int sock2server = connect2server(server, PORTNUM);
    double *series= new double[n];
    for(int i=0; i < n; i++)
        series[i]=(i*2==0)?4.0/(2*i+1):-4.0/(2*i+1);
    double *psum=new double[n];
    int count = n/blocksize;
    StatVector stat_ts(count), stat_tr(count);
    Timestamp clk;
    clk.tic();
    partialsum_client(sock2server, series, n,
        blocksize, psum, stat_ts, stat_tr);
    double cycles = clk.toc();
    /* output code omitted */
    std::cout<<"bandwidth = " <<16.0*n/cycles*1e9*CPGHZ/1e3
        << "kbps"<<endl;
    delete[] series;
    delete[] psum;
}
```

第一个参数是服务器名称¹。`client()` 的第二个参数是 `blocksize`。为了让此程序正确运行，该参数必须与 `server()` 中的值相同。注意 `series` 中的项数总是块 大的偶整数倍数。`series[]` 数组用莱布尼茨级数初始化。

大部分输出代码被省略。但我们展示了带宽计算，其中包括发送和接收的字节。常量 `CPGHZ` 必须定义为 GHz 单位的 CPU 速度。

¹要运行此程序，需要知道运行服务器的计算机形式是 www.somewhere.org 还是 IP 地址。有很多网络服务可以查找你计算机的 IP 地址。

## 6.4. 互联网

## 6.4.5 互联网延迟

为了找到网络延迟，我们将块大小设置为 100 个双精度数字或 800 字节。这样的一个块可以舒适地放入小于 1.5 KB（以太网 MTU）的单个 TCP/IP 包中。因此，客户端发送单个 TCP/IP 包并等待部分和，后者以单个 TCP/IP 包到达。

所有测量都是通过在德克斯斯计算中心（TACC）运行服务器并在密歇根大学（UM）运行客户端完成的。在多次试验中，发送+接收的中位时间接近 55 毫秒。因此，认为 UM 和 TACC 之间的往返延迟为 55 毫秒，这是一个非常有趣的问题。

理解为什么延迟是 55 毫秒，从 UM 到 TACC 的距离超过 1000 英里。因此，光速似乎占了超过 10 毫秒的延迟。

事实上，情况更为复杂。Linux 命令 `traceroute` 显示数据包从 UM 到 TACC 以及返回的路径是不同的。一个从 UM 到 TACC 的数据包几乎立即从作者的桌面传输到位于 2.3 英处的路由器（经过几次跳数）。作者桌面以南 2.3 英处的路由器由 Merit Networks 管理。从该路由器开始，它跳转到 Lubbock 的一个路由器，单跳就覆盖了从 UM 到 TACC 的大部分距离。Lubbock 的路由器由 LEARN 管理。数据包从德克萨斯 Lubbock 经过几次快速跳转到达 TACC 路由器。大部分延迟

> ²²感谢 Barnar 在 2005 年 7 月在 Comcast 论坛上的一个帖子，解释了 traceroute 的一些微妙之处。

