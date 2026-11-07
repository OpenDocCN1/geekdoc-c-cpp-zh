
> 在没有先调用 htons() 转换例程的情况下连接到端口 427，它实际上是在尝试连接到十六进制端口 AB01，即十进制 43777。因此，客户端永远无法连接到在 Macintosh 上运行的服务器进程，或者至少不是预期的服务器进程。

要求其参数采用网络字节序的函数，会在每个函数说明的文字中注明。

## 转换 IP 地址

WinSock 提供了另一组转换函数，用于在点分十进制 IP 地址的 ASCII 表示与其他 WinSock 函数所需的内部 32 位、字节序数字之间进行转换。

### 将 IP 地址字符串转换为二进制

`inet_addr()` 将点分十进制 IP 地址字符串转换为适合用作 Internet 地址的数字。其函数原型如下：

```c
unsigned long PASCAL FAR inet_addr(const char FAR * cp);
```

`cp` 是指向以点分十进制表示法表示 IP 地址的字符串的指针。`inet_addr()` 函数返回给定 Internet 地址的二进制表示。该值已经是网络字节序，因此无需调用 `htonl()`。如果 `cp` 字符串不包含有效 IP 地址，`inet_addr()` 返回 INADDR_NONE。此类错误的一个可能原因是 IP 地址的某个组成部分大于 255。请记住，点分十进制 IP 地址的四个组成部分分别表示无符号长整型的四个字节之一，因此任何组成部分的值大于 255 都是非法的，因为一个字节的值必须介于 0 到 255（含）之间。

以下代码片段展示了对 `inet_addr()` 的典型调用。当然，实际程序不会硬编码 IP 地址；你很可能允许用户在配置应用程序时指定 IP 地址。

```c
u_long ulIPAddress = inet_addr("166.78.16.148");
```

此代码片段执行后，`ulIPAddress` 的值将是十六进制 A64E1094。`inet_addr()` 只是取 IP 地址的每个组成部分，并将其以二进制形式存储为四字节 IP 地址中的一个字节。不过，你不需要指定 IP 地址的全部四个部分。`inet_addr()` 可以接受以下任意一种点分十进制表示法的 IP 地址：a.b.c.d、a.b.c、a.b 或 a。a.b.c.d 值是前面代码示例中所示的典型 IP 地址。如果省略某个数量，最后一个已定义的数量将被简单地扩展以填充剩余字节，凑足总共四个字节。例如，如果传递给 `inet_addr()` 的字符串是“166.78.16”，采用 a.b.c 格式，则返回的无符号长整型为十六进制 A64E0010。

### 将二进制 IP 地址转换为字符串

`inet_ntoa()` 执行与 `inet_addr()` 相反的工作。其函数原型如下：

```c
char FAR * PASCAL FAR inet_ntoa(struct in_addr in);
```

`in` 是包含 Internet 主机地址的结构。你会看到有些 WinSock 函数将 IP 地址作为无符号长整型处理，另一些则作为 `in_addr` 结构处理。为弥补这一差异，需要进行一些字节复制。以下示例代码展示了这一点。成功时，`inet_ntoa()` 函数返回指向点分十进制 IP 地址字符串的指针。出错时，返回 `NULL`。NULL 值表示作为参数传入的 IP 地址无效。

以下是一段有点刻意构造的代码：

```c
// first get an unsigned long with a valid IP address
u_long ulIPAddress = inet_addr("166.78.16.148");

// copy the four bytes of the IP address into an in_addr structure
IN_ADDR in;
memcpy(&in, &ulIPAddress, 4);

// convert the IP address back into a string
char lpszIPAddress[16];
lstrcpy(lpszIPAddress, inet_ntoa(in));
```

我说前面的示例是刻意构造的，是因为二进制 IP 地址的获取方式。二进制 IP 地址 `ulIPAddress` 是通过使用 `inet_addr()` 转换 IP 地址字符串而获得的。在实际程序中，你希望对其使用 `inet_ntoa()` 的 IP 地址很可能来自另一个 WinSock 调用的结果，而不是用户输入或硬编码的；这部分代码仅用于演示目的。一旦有了这个无符号长整型，就需要将其存储在 `in_addr` 结构中，以供 `inet_ntoa()` 使用，因此使用了 `memcpy()`。接下来，调用转换函数。`inet_ntoa()` 返回的字符串指针只是临时的。在下一次调用 WinSock 函数后，它可能无效，因此最好将其复制到应用程序中的变量中。分配 16 字节缓冲区，因为这是有效的四字节 IP 地址可能达到的最长长度（即“255.255.255.255”加上终止 NULL 字符）。

## 我的名字是什么？

有些应用程序需要知道其运行所在计算机的名称。`gethostname()` 函数提供此功能。它被添加到 WinSock 1.1 规范中。该函数的原型如下：

```c
int PASCAL FAR gethostname(char FAR * name, int namelen);
```

`name` 是指向字符数组的远指针，该数组将接受以 null 结尾的主机名，`namelen` 是该字符数组的大小。`gethostname()` 函数成功时返回 0（零），失败时返回 SOCKET_ERROR。返回值为 SOCKET_ERROR 时，可以调用 `WSAGetLastError()` 确定具体问题。可能的错误值包括：如果缓冲区太小无法容纳主机名，则为 WSAEFAULT；如果 `WSAStartup()` 未成功调用，则为 WSANOTINITIALISED；如果网络子系统故障，则为 WSAENETDOWN；如果当前正在进行阻塞式 WinSock 操作，则为 WSAEINPROGRESS。

以下代码片段展示了对 `gethostname()` 的典型调用：

```c
#define HOST_NAME_LEN (50)
char lpszHostName[HOST_NAME_LEN];    // will accept the host name
char lpszMessage[100];               // informational message

if (gethostname(lpszHostName, HOST_NAME_LEN) == 0)
    wsprintf(lpszMessage, "This computer's name is %s", lpszHostName);
else
    wsprintf(lpszMessage, "gethostname() generated error %d",
        WSAGetLastError());

MessageBox(NULL, lpszMessage, "Info", MB_OK);
```

![](img/5e551abe6e0cb0588043ee757a235ddb_72_0.png)

> **注意**
>
> `gethostname()` 填充的名称可能是简单名称，也可能是完全限定域名。例如，我的计算机可能被识别为 goober 或 goober.ping.com。返回哪种格式由实现 WinSock 的人决定。关于 `name` 变量唯一保证的是，它可以被 `gethostbyname()` 函数解析，该函数将在后面讨论。

## 主机名解析

人类使用文本表示来指代程序连接的主机。计算机要求主机地址是一个 32 位整数，并以标准化方式存储，如上一节关于网络字节序所述。在你的程序能够连接到另一台计算机之前，该计算机的 IP 地址必须采用 32 位格式。为弥补这一差异，程序可以使用 `gethostbyname()` 或 `inet_addr()` 函数。如果你知道简单名称或完全限定域名，则使用 `gethostbyname()`。如果你知道 IP 地址，则使用 `inet_addr()`。

> **提示**
>
> 大多数带有配置以选择程序通信主机的程序，都允许用户输入主机名或 IP 地址。程序应首先用用户输入调用 `inet_addr()`。如果此函数成功返回，转换工作就完成了；否则，应假设用户输入的是主机名，并调用 `gethostbyname()`。

## 查找主机的 IP 地址

`gethostbyname()` 的主要职责是接收主机名并返回其 IP 地址。该函数及其名为 `WSAAsyncGetHostByName()` 的异步对应函数，可能会在程序运行所在计算机本地的主机文件上执行简单的表查找，也可能通过网络向名称服务器发送请求。图 6.1 和 6.2 展示了主机名解析的不同方式。应用程序员实际上并不知道使用哪种方法来解析主机名，而且这通常并不重要，但有一个注意事项，将在关于 `WSAAsyncGetHostByName()` 的章节中描述。该函数的原型如下：

```c
struct hostent FAR * PASCAL FAR gethostbyname(const char FAR * name);
```

`name` 是指向以 null 结尾的字符数组的远指针，该数组包含你希望获取主机信息的计算机名称。返回的 `hostent` 结构具有以下格式：

```c
struct hostent {
    char FAR * h_name;         // official name of host
    char FAR * FAR * h_aliases; // alias list
    short h_addrtype;           // host address type
    short h_length;             // length of address
    char FAR * FAR * h_addr_list; // list of addresses
#define h_addr h_addr_list[0]   // address, for backward compatibility
};
```

成功时，`gethostbyname()` 函数返回指向 `hostent` 结构的指针；失败时，该函数返回 NULL。返回值为 NULL 时，可以调用 `WSAGetLastError()` 确定具体问题。可能的错误值包括：如果 `WSAStartup()` 未成功调用，则为 WSANOTINITIALISED；如果网络子系统故障，则为 WSAENETDOWN；如果无法解析主机名，则为 WSAHOST_NOT_FOUND；如果失败原因可能是临时的，例如名称服务器宕机，则为 WSATRY_AGAIN；如果发生不可恢复错误，则为 WSANO_RECOVERY；如果主机名有效但找不到合适的数据，则为 WSANO_DATA；如果当前正在进行阻塞式 WinSock 操作，则为 WSAEINPROGRESS；或者如果阻塞调用被 `WSACancelBlockingCall()` 取消，则为 WSAEINTR。

