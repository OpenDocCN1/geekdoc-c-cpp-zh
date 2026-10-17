
在 `process_udp4` 中，如果 `start_udp_proto` 返回成功，则会调用 `k_work_reschedule()` 来更新网络统计打印工作队列的任务，然后调用 `process_udp()` 来处理收到的 UDP 数据。因为 UDP 无论在 IPv4 还是 IPv6 之上的表现都是相同的，所以 `process_udp()` 也用于处理通过 IPv6 发送的 UDP 数据。

`process_udp()` 使用 `recvfrom` 来处理到达的 UDP 数据文，并使用 `sendto()`。`process_udp()` 函数实现了 UDP 回显服务器的行为。本质上，该函数将接收到的数据拷贝到缓冲区并将其发送回原始客户端，下方的 `process_udp()` 代码段展示了这一点：

```c
static int process_udp(struct data *data) {
    int ret = 0;
    int received;
    struct sockaddr client_addr_len;
    NET_INFO("Waiting for UDP packets on port %d (%s)...", MY_PORT, data->proto);
    do {
        client_addr_len = sizeof(client_addr);
        received = recvfrom(data->udp.sock,
```

```c
data->udp.recv_buffer,
sizeof(data->udp.recv_buffer), 0,
&client_addr, &client_addr_len);
if (received < 0) {
  /* Socket error */
  NET_ERR("%s): Connection error %d",
  data->proto, errno);
  ret = -errno;
  break;
} else if (received) {
  atomic_add(&data->udp.bytes_received,
  received);
}
ret = sendto(data->udp.sock, data->udp.recv_buffer,
  received, 0, &client_addr, client_addr_len);
if (ret < 0) {
  NET_ERR("%s): Failed to send %d",
  data->proto, errno);
  ret = -errno;
  break;
}
if (++data->udp.counter % 1000 == 0) {
  NET_INFO("%s UDP: Sent %u packets",
  data->proto,
  data->udp.counter);
}
NET_DBG("%s): Received and replied with %d bytes",
  data->proto, received);
```

```c
} while (true);
return ret;
}
```

可以通过在 PC 上运行如下简单的 Python 脚本来测试 UDP 回显服务器服务：

```python
import socket
testMessageStart = "Test message number"
serverAddressPort = ("192.0.2.1", 4242)
bufferSize = 1024
# Create a client side UDP socket
with socket.socket(family=socket.AF_INET, type=socket.SOCK_DGRAM) as UDPCClient:
    # Send a few test messages to the Echo Server
    for num in ("1","2","3","4","5","6","7","8","9") :
        message = testMessageStart + " " + num
        messageSize = str.encode(message)
        UDPCClient.sendto(messageSize, serverAddressPort)
        serverResponse = UDPCClient.recvfrom(bufferSize)
        response = "Echo from UDP Server"
        print(response[0].decode("utf-8"))
```

在 TCP 回显服务器代码中，`tcp.c` 文件中的 `process_tcp4()` 和 `process_tcp6()` 函数的模式与 `process_udp4()` 和 `process_udp6()` 相同，并最终会调用 TCP 处理函数 `process_tcp()`。由于 TCP 是一种面向连接的流协议，在 TCP 上进行数据读写类似于对文件的读写。`process_tcp()` 的代码与 `process_udp()` 的代码不同。

# 第 8 章 ZEPHYR RTOS 与以太网、Wi-Fi 和 TCP/IP

以下代码段展示了 `process_tcp()` 中处理基于 IPv4 的 TCP 请求和响应的代码。处理基于 IPv4 的 TCP 请求和响应的代码类似，可以参考原始源代码以查看细节。

```c
static int process_tcp(struct data *data) {
    int client;
    struct sockaddr_in client_addr;
    socklen_t client_addr_len = sizeof(client_addr);
    LOG_INF("Waiting for TCP connection on port %d (%s)...",
            MY_PORT, data->proto);
    int client = accept(data->tcp.sock,
                        struct sockaddr*)&client_addr, &client_addr_len);
    if (client < 0) {
        LOG_ERR("%s accept error (%d)", data->proto,
                errno);
        return 0;
    }
    int slot = get_free_slot(data);
    if (slot < 0) {
        LOG_ERR("Cannot accept more connections");
        close(client);
        return 0;
    }
    data->tcp.accepted[slot].sock = client;
    LOG_INF("TCP (%s) Accepted connection", data->proto);
#define MAX_NAME_LEN sizeof("tcp4[%d]")
    if (client_addr.sin_family == AF_INET) {
        tcp4_handler_in_use[slot] = true;
        k_thread_create(
            &tcp4_handler_thread[slot],
            tcp4_handler_stack[slot],
            (k_thread_entry_t)handle_data,
            POINTER(slot), data,
            &tcp4_handler_in_use[slot],
            THREAD_PRIORITY,
            IS_ENABLED(CONFIG_USERSPACE) ? K_USER_INHERIT_PERMS : 0,
            K_NO_WAIT);
        char name[MAX_NAME_LEN];
        snprintf(name, sizeof(name), "tcp4[%d]", slot);
        k_thread_name_set(&tcp4_handler_thread[slot], name);
    }
    return 0;
}
```

由于 TCP 是面向连接的，因此有跟踪活动连接的活动。与服务器关联的最大 TCP 连接数是可以配置的。跟踪连接的方法有：一种是单线程方法，由单个线程跟踪所有连接；另一种是为每个连接分配一个单独线程。示例回显服务器为每个连接分配一个单独线程，接下来将探讨该代码。

## 配置 TCP 服务器应用程序使用独立线程处理连接

首先需要理解在服务器端和客户端设置 TCP/IP 连接时涉及的各种数据结构和 API 函数。

### 与 TCP/IP 服务器端连接关联的数据结构

全局变量 `conf.ipv4.tcp` 元素的类型为：

```c
struct {
    int sock;
    atomic_t bytes_received;
    struct k_work delay stats_print;
    struct {
        int sock;
        char recv_buffer[RECV_BUFFER_SIZE];
        uint32_t counter;
    } accepted[CONFIG_NET_SAMPLE_HANDERS];
};
```

元素 `conf.ipv4.tcp.accepted` 是类型为元素的数组：

```c
struct {
    int sock;
    char recv_buffer[RECV_BUFFER_SIZE];
    uint32_t counter;
}
```

`accepted` 数组可以被看作槽位数组，每个槽位可能分配给特定的连接处理线程，或者未分配。`get_free_slot()` 函数遍历 `accepted` 数组，寻找 `sock` 值小于 0 的空槽位并返回它。

```c
static int get_free_slot(struct data *data) {
    int i;
    for (i = 0; i < CONFIG_NET_SAMPLE_HANDERS; i++) {
        if (data->tcp.accepted[i].sock < 0) {
            return i;
        }
    }
    return -1;
}
```

`accepted` 数组在 `start_tcp()` 函数中使用以下代码初始化：

```c
for (i = 0; i < CONFIG_NET_SAMPLE_HANDERS; i++) {
    conf.ipv6.tcp.accepted[i].sock = -1;
    conf.ipv4.tcp.accepted[i].sock = -1;
}
#if defined(CONFIG_NET_IPV4)
    tcp4_handler_in_use[i] = false;
#endif
```

## 用于 TCP/IP 服务器连接的线程结构池

处理线程的线程结构池在 `tcp.h` 中定义为全局变量数组 `struct k_thread` 元素；定义如下：

```c
static struct k_thread tcp4_handler_thread[CONFIG_NET_SAMPLE_HANDERS];
static bool tcp4_handler_in_use[CONFIG_NET_SAMPLE_HANDERS];
```

此数组中的元素被初始化，使得对于所有有效索引值 `tcp4_handler_in_use[i] = false;`

`start_tcp` 中在启用 `CONFIG_USERSPACE` 时处理权限的代码包含以下几行：

```c
#if defined(CONFIG_NET_IPV4)
#if defined(CONFIG_USERSPACE)
k_mem_domain_add_thread(&app_domain, tcp4_thread_id);
for (i = 0; i < CONFIG_NET_SAMPLE_HANDERS; i++) {
  k_mem_domain_add_thread(&app_domain, &tcp4_handler_thread[i]);
  k_thread_access_grant(tcp4_thread_id, &tcp4_handler_thread[i]);
  k_thread_access_grant(tcp4_thread_id, &tcp4_handler_stack[i]);
}
#endif
#endif
```

# 第 8 章 ZEPHYR RTOS 与以太网、Wi-Fi 以及 TCP/IP

在找到空槽位后，下一步是实际使用它来处理与该 TCP 连接相关的数据。以下是 `process_tcp()` 函数内部的相关代码，用于执行 IPv4 连接的处理。

```
slot = get_free_slot(data);
if (slot < 0) {
    LOG_ERR("Cannot accept more connections");
    close(client);
    return 0;
}
data->tcp.accepted[slot].sock = client;
LOG_INF("TCP (%s): Accepted connection", data->proto);
#if defined(CONFIG_NET_IP) == AF_INET) {
    if (client_addr.sin_family == AF_INET) {
        tcp4_handler_in_use[slot] = true;

        k_thread_create(
            &tcp4_handler_thread[slot],
            tcp4_handler_stack[slot],
            K_THREAD_STACK_SIZEOF(tcp4_handler_stack[slot]),
            (k_thread_entry_t)handle_data,
            INT_TO_POINTER(slot), data,
            &tcp4_handler_in_use[slot],
            THREAD_PRIORITY,
            IS_ENABLED(CONFIG_USERSPACE) ? K_USER | 
            K_INHERIT_PERMS : 0,
            K_NO_WAIT);
        if (IS_ENABLED(CONFIG_THREAD_NAME)) {
            char name[MAX_NAME_LEN];
            snprintf(name, sizeof(name),
            "tcp4[%d]", slot);
```

```
k_thread_name_set(&tcp4_handler_thread[slot], name);
}
#endif
```

需要注意的是动态创建一个线程来处理数据。该线程会在 `handle_data` 函数返回后终止。

以下是静态的（对 `tcp.h` 私有）`handle_data` 函数代码。省略了 TLS 代码，因为它在示例中没有被使用。

```
static void handle_data(void *ptr1, void *ptr2, void *ptr3) {
   int slot = POINTER_TO_INT(ptr1);
   struct data *data = ptr2;
   bool *in_use = ptr3;
   int offset = 0;
   int received;
   int client;
   int ret;
   client = data->tcp.accepted[slot].sock;
   do {
      received = recv(client,
         data->tcp.accepted[slot].recv_buffer
         + offset,
         sizeof(data->tcp.accepted[slot].recv_buffer) - offset,
         0);
      if (received == 0) {
         /* 连接关闭 */
         LOG_INF("TCP %s): Connection closed",
         data->proto);
```
