

```c
struct events[MAX_EVENTS];
int sockfd = socket(AF_INET, SOCK_STREAM, 0);
struct sockaddr_in serv_addr;
serv_addr.sin_family = AF_INET;
serv_addr.sin_addr.s_addr = INADDR_ANY;
serv_addr.sin_port = htons(portno);
bind(sockfd, (struct sockaddr *)&serv_addr, sizeof(serv_addr));
int epollfd = epoll_create1(0);
struct epoll_event ev;
ev.events = EPOLLIN;
ev.data.fd = sockfd;
if (epoll_ctl(epollfd, EPOLL_CTL_ADD, sockfd, &ev) == -1) {
    perror("epoll_ctl");
}
while ((n = epoll_wait(epollfd, events, MAX_EVENTS, -1)) > 0) {
    for (int i = 0; i < n; ++i) {
        if (events[i].data.fd == sockfd) {
            struct sockaddr_in cli_addr;
            socklen_t clilen = sizeof(cli_addr);
            int newsockfd = accept(sockfd, (struct sockaddr *)&cli_addr, &clilen);
            if (newsockfd != -1) {
                ev.events = EPOLLIN | EPOLLET;
                if (epoll_ctl(epollfd, EPOLL_CTL_ADD, newsockfd, &ev) == -1) {
                    perror("epoll_ctl");
                }
            }
        } else {
            // Handle read or write on events[i].data.fd
    }
}
```

该服务器监听端口 5003，并使用 `epoll` 高效地管理多个客户端连接。它将服务器套接字所有新的客户端套接字设置为非阻塞模式，以确保服务器在等待客户端数据时不会阻塞。

非阻塞 INET 套接字结合 `epoll` 等 I/O 多复用技术，为使用 C 开发高性能可扩展服务器提供了一种强有力的策略。通过结合这些技术，开发者可以创建能够处理大量并发连接的服务器，为更具响应性且健壮的网络应用程序铺平道路。

## 5.3

## 实现 HTTP 服务器和客户端

超文本传输协议（HTTP）是 Web 的基石，实现了 Web 服务器与客户端之间的通信。虽然许多高级编程语言都提供了库来抽象 HTTP 操作的复杂性，但在 C 中实现 HTTP 服务器和客户端可以深入理解该协议的底层原理。本节将介绍 HTTP 的基础知识，随后给出在 C 中实现简单 HTTP 服务器和客户端的详细示例。

理解 HTTP：HTTP 是客户端-服务器计算模型中的请求-响应协议。客户端（通常是网络浏览器或特殊的 HTTP 客户端）向服务器发送 HTTP 请求。存储内容和服务资源的服务器处理请求并返回 HTTP 响应。这种交互是无状态的，意味着每对请求-响应都是独立的，事务之间没有存储上下文。

HTTP 请求和响应由以下部分组成：

- 起始行：对于请求，定义请求方法、URI 和 HTTP 版本；对于响应，定义状态码和短语，它们携带了请求和响应消息的元数据。
- 可选的消息：包含传输的数据。

实现简单的 HTTP 服务器：可以使用 TCP 套接字实现基础的 HTTP 服务器，因为 HTTP 是运行在 TCP/IP 之上的应用层协议。服务器需要处理传入的客户端连接、解析 HTTP 请求并生成相应的 HTTP 响应。下面是一个演示最小 HTTP 服务器的简单 C 程序。

```c
#include <stdio.h>
#include <string.h>
#include <unistd.h>
#include <netinet/in.h>

int main() {
    int server_fd, client_fd;
    struct sockaddr_in server_addr, client_addr;
    socklen_t sin_len = sizeof(client_addr);
    char buf[2048];
    server_fd = socket(AF_INET, SOCK_STREAM, 0);
    server_addr.sin_family = AF_INET;
    server_addr.sin_addr.s_addr = INADDR_ANY;
    server_addr.sin_port = htons(8080);
    bind(server_fd, (struct sockaddr *)&server_addr, sizeof(server_addr));
    listen(server_fd, 5);
    if ((client_fd = accept(server_fd, (struct sockaddr *)&client_addr, &sin_len)) != -1) {
        read(client_fd, buf, 2047);
        char response[] = "HTTP/1.1 200 OK\r\nContent-Type: text/plain\r\n\r\nHello, world!";
        send(client_fd, response, strlen(response), 0);
        close(client_fd);
    }
    return 0;
}
```

该服务器监听端口 8080，并对每个 HTTP GET 请求返回简单的“Hello, world!” 消息。它演示了解析 HTTP 请求和构建响应的基础。然而，现实世界的 HTTP 服务器需要处理各种 HTTP 方法、解析头部头、支持并发连接并提供实际内容。

HTTP/1.1 200 OK
Content-Type: text/plain

Hello, world!

实现简单的 HTTP 客户端：C 中的 HTTP 客户端可以以类似的方式实现：与服务器建立 TCP 连接、发送 HTTP 请求并处理响应。下面是一个简单的 HTTP 客户端示例。

```c
#include <stdio.h>
#include <string.h>
#include <unistd.h>
#include <netdb.h>
#include <netinet/in.h>

int main() {
    struct addrinfo hints, *res;
    int sockfd;
    char buf[2048];
    memset(&hints, 0, sizeof(hints));
    hints.ai_family = AF_UNSPEC;
    hints.ai_socktype = SOCK_STREAM;
    getaddrinfo("example.com", "80", &hints, &res);
    sockfd = socket(res->ai_family, res->ai_socktype, res->ai_protocol);
    connect(sockfd, res->ai_addr, res->ai_addrlen);
    char http_request[] = "GET / HTTP/1.1\r\nHost: example.com\r\n\r\n";
    send(sockfd, http_request, strlen(http_request), 0);
    read(sockfd, buf, 2047);
    printf("%s", buf);
    close(sockfd);
    freeaddrinfo(res);
    return 0;
}
```

该客户端与 "example.com" 的 80 端口建立连接，发送简单的 HTTP GET 请求并打印响应。注意使用 `getaddrinfo` 获取地址结构，这抽象了 IPv4 和 IPv6 地址。

在 C 中实现 HTTP 服务器和客户端提供了丰富的体验，展示了 TCP/IP 与应用层之间的交互。虽然现代应用程序可能使用高级库和框架处理 HTTP 通信，但此处所示的原理是基础性的。

