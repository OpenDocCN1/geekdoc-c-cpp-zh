
通过讨论这些技术，开发者可以创建高效的多线程应用程序，能够充分利用底层硬件的能力。

# 第 5 章

# C 语言网络编程基础

本章介绍了 C 语言网络编程的基础知识，为读者构建和管理网络应用程序奠定坚实的基础。通过探索 C 网络编程的基石——Socket 编程，本章将引导读者学习 TCP 和 UDP 协议的创建、绑定、监听和接受连接。书中重点关注实际应用场景，展示了如何设计客户端-服务器架构、处理多个连接以及实现数据传输机制。通过详细的示例和清晰的解释，读者将获得应对网络通信复杂性所需的技能，使其能够使用 C 语言编写高效、健壮且可扩展的网络应用程序。

## 5.1 Socket 编程基础：TCP 和 UDP Socket

在网络编程领域，Socket（套接字）的概念上起着至关重要的作用。Socket 为不同进程（无论是在同一系统内还是跨网络）之间的数据交换提供了所需的通信端点。广而言之，有两种满足不同需求和协议的 Socket 类型：TCP（传输控制协议）Socket 和 UDP（用户数据报文协议）Socket。本节将深入探讨 Socket 编程的基础，涵盖 TCP 和 UDP Socket，并通过详细的代码示例演示它们的用法。

理解 Socket：从本质上，Socket 是两个进程之间通信的接口。将 Socket 想象成客户端和服务器之间双向通信链路的一端。每个 Socket 都有关联的 IP 地址和端口，它们共同工作以唯一标识通信端点。

TCP 提供了一种可靠的、面向连接的方式来发送和接收数据。通过 TCP 连接发送的数据保证按顺序到达且不重复，这使得 TCP Socket 适用于对可靠性交付至关重要的应用程序，例如 Web 服务器。

相反，UDP 是一种无连接的、不可靠的服务。通过 UDP 发送的数据包可能会乱序到达或完全丢失。然而，UDP 具有轻量级的特性，没有连接建立或销毁，且协议开销极小，这使其非常适合容忍丢失但需要快速、高效通信的应用程序，例如视频流媒体或在线游戏。

创建 TCP Socket：开始 TCP 通常涉及创建 socket、将其绑定到地址和端口、监听传入的连接、接受连接以及从 socket 读取或向其写入数据。下面是一个演示 TCP 服务器 Socket 的简单 C 程序。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>
#include <netinet/in.h>

int main(int argc, char *argv[]) {
    int sockfd, newsockfd, portno, clilen;
    char buffer[256];
    struct sockaddr_in serv_addr, cli_addr;
    int n;

    sockfd = socket(AF_INET, SOCK_STREAM, 0);
    if (sockfd < 0) return 1;

    memset(&serv_addr, 0, sizeof(serv_addr));
    serv_addr.sin_family = AF_INET;
    serv_addr.sin_addr.s_addr = INADDR_ANY;
    portno = 5001;
    serv_addr.sin_port = htons(portno);

    if (bind(sockfd, (struct sockaddr *)&serv_addr, sizeof(serv_addr)) < 0) return 1;

    listen(sockfd, 5);
    clilen = sizeof(cli_addr);
    newsockfd = accept(sockfd, (struct sockaddr *)&cli_addr, &clilen);
    if (newsockfd < 0) return 1;

    n = read(newsockfd, buffer, 255);
    if (n < 0) {
        buffer[n] = '\0';
        printf("Here is the message: %s\n", buffer);
        send(newsockfd, buffer, strlen(buffer), 0);
    }
    close(newsockfd);
    return 0;
}
```

这段代码段概述了一个在端口 5001 上监听的基础服务器设置。在接收到连接后，它读取客户端发送的消息，显示它，然后向客户端发送响应。

创建 UDP Socket：UDP Socket 编程要简单一些，因为不需要监听或接受连接。一旦创建并绑定 socket，就可以直接发送和接收数据。这是一个 UDP 服务器程序示例：

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>
#include <netinet/in.h>

int main() {
    int sockfd;
    struct sockaddr_in serv_addr, cli_addr;
    socklen_t addrlen = sizeof(cli_addr);
    char buffer[1024];
    int n;

    sockfd = socket(AF_INET, SOCK_DGRAM, 0);
    if (sockfd < 0) return 1;

    memset(&serv_addr, 0, sizeof(serv_addr));
    serv_addr.sin_family = AF_INET;
    serv_addr.sin_addr.s_addr = INADDR_ANY;
    serv_addr.sin_port = htons(5002);

    if (bind(sockfd, (struct sockaddr *)&serv_addr, sizeof(serv_addr)) < 0) return 1;

    while (1) {
        n = recvfrom(sockfd, buffer, 1024, MSG_WAITALL, (struct sockaddr *)&cli_addr, &addrlen);
        buffer[n] = '\0';
        printf("Received: %s\n", buffer);
        send(sockfd, buffer, strlen(buffer), 0, (struct sockaddr *)&cli_addr);
    }
    return 0;
}
```

C 语言中的 Socket 编程是开发网络应用程序的基础技能。通过 TCP 和 UDP Socket，程序员可以根据应用程序的需求实现可靠的面向连接通信和快速的无连接通信。这里提供的实际示例是深入研究网络编程世界的起点。

## 5.2 使用非阻塞 Socket 和 I/O 复用开发可扩展服务器

网络应用程序的可扩展性（特别是同时处理多个连接的服务器）取决于非阻塞 Socket 和 I/O 复用的有效使用。这些特性对于设计能够管理成千个并发连接而不受阻塞 I/O 限制的系统至关重要。本节介绍了非阻塞 Socket，深入探讨了 I/O 复用，并演示了如何在 C 语言中利用这些概念构建可扩展服务器。

阻塞 Socket：在传统的 Socket 编程中，Socket 默认是阻塞的。这意味着发送或接收数据的调用会直到操作完成。虽然这种模型对于低并发要求的应用程序良好，但对于阻塞 Socket，每个连接通常都需要一个专用线程或进程来处理 I/O 操作，这导致了资源的过度消耗和可扩展性瓶颈。

非阻塞 Socket：顾如名，非阻塞 Socket 允许操作立即返回，即使操作尚未完成。这允许应用程序在单个线程内继续其他任务或处理多个 Socket。要启用非阻塞模式，可以使用函数返回操作是否会阻塞的状态，允许应用程序决定如何继续。

I/O 复用：仅利用非阻塞 Socket 无法完全解决管理多个连接的问题。这就是 I/O 复用的用场，它允许单个线程监控多个文件描述符以执行 I/O 操作。select 和 epoll 等技术被用于 Unix 类系统的 I/O 复用。Linux 上的 epoll 比处理大量的 Socket 效率更高，因为它不需要每次调用时都重新构建 Socket 列表。

使用非阻塞 Socket 和 epoll 实现服务器：下面是一个利用非阻塞 Socket 配合 epoll 处理多个连接的简单回服务器示例。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>
#include <netinet/in.h>
#include <sys/epoll.h>

#define MAX_EVENTS 10

void set_nonblocking(int sockfd) {
    int opts = fcntl(sockfd, F_GETFL);
    if (opts < 0) return;
    fcntl(sockfd, F_SETFL, opts | O_NONBLOCK);
}

int main() {
    int sockfd, newsockfd, portno = 5003;
    struct sockaddr_in serv_addr, cli_addr;
    socklen_t clilen = sizeof(cli_addr);
    int epoll, nfds;
    struct epoll_event ev, events[MAX_EVENTS];

    sockfd = socket(AF_INET, SOCK_STREAM, 0);
    if (sockfd < 0) return 1;
    set_nonblocking(sockfd);

    memset(&serv_addr, 0, sizeof(serv_addr));
    serv_addr.sin_family = AF_INET;
    serv_addr.sin_addr.s_addr = INADDR_ANY;
    serv_addr.sin_port = htons(portno);

    if (bind(sockfd, (struct sockaddr *)&serv_addr, sizeof(serv_addr)) < 0) return 1;
    listen(sockfd, 5);

    epoll = epoll_create1(0);
    ev.events = EPOLLIN;
    ev.data.fd = sockfd;
    epoll_ctl(epoll, EPOLL_CTL_ADD, sockfd, &ev);

    while (1) {
        nfds = epoll_wait(epoll, events, MAX_EVENTS, -1);
        for (int i = 0; i < nfds; i++) {
            if (events[i].data.fd == sockfd) {
                newsockfd = accept(sockfd, (struct sockaddr *)&cli_addr, &clilen);
                if (newsockfd >= 0) {
                    set_nonblocking(newsockfd);
                    ev.events = EPOLLIN;
                    ev.data.fd = newsockfd;
                    epoll_ctl(epoll, EPOLL_CTL_ADD, newsockfd, &ev);
                }
            } else {
                char buffer[256];
                int n = read(events[i].data.fd, buffer, 255);
                if (n > 0) {
                    buffer[n] = '\0';
                    send(events[i].data.fd, buffer, strlen(buffer), 0);
                } else if (n == 0) {
                    epoll_ctl(epoll, EPOLL_CTL_DEL, events[i].data.fd, NULL);
                    close(events[i].data.fd);
                }
            }
        }
    }
    return 0;
}
```

