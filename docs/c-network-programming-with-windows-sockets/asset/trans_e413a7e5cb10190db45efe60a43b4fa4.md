

**图 6.1。**
*WinSock 使用本地文件查找。*

![](img/5e551abe6e0cb0588043ee757a235ddb_75_0.png)

使用目前介绍过的几个函数，你既可以显示网络互联中任意主机的 IP 地址，也可以查明本机的名称和 IP 地址。以下示例代码片段正是这样做的：

```c
#define HOST_NAME_LEN (50)
char lpszHostName[HOST_NAME_LEN];       // 将用于存放主机名
char lpszMessage[100];                  // 提示信息
char lpszIP[16];                        // IP 地址字符串
PHOSTENT phostent;                      // 指向主机条目结构的指针
IN_ADDR in;                             // Internet 地址结构

// 查找运行此程序的计算机名称
if (gethostname(lpszHostName, HOST_NAME_LEN) != 0)
    wsprintf(lpszMessage, "gethostname() generated error %d",
        WSAGetLastError());
else
{
    // 获取此计算机的主机条目结构
    if ((phostent = gethostbyname(lpszHostName)) == NULL)
        wsprintf(lpszMessage, "gethostbyname() generated error %d",
            WSAGetLastError());
    else
    {
        // 将四字节 IP 地址复制到 Internet 地址结构中
        memcpy(&in, phostent->h_addr, 4);

        // 格式化结果，将 IP 地址转换为字符串
        wsprintf(lpszMessage, "Host %s has IP address ", phostent->h_name);
        wsprintf(lpszIP, "%s", inet_ntoa(in));
    }
}
lstrcat(lpszMessage, lpszIP);
}
}

MessageBox(NULL, lpszMessage, "Info", MB_OK);
```

**图 6.2。**
*WinSock 使用联网的数据库服务器。*

![](img/5e551abe6e0cb0588043ee757a235ddb_76_0.png)

假设运行此程序的计算机名为“saturn”。调用 `gethostname()` 会将“saturn”设为主机名，并将该字符串复制到 `lpszHostName` 中。再假设这台计算机使用主机文件解析名称，而不是使用联网的名称服务器。该主机文件中的一行可能如下所示：

```
166.78.16.200        saturn
```

`gethostbyname()` 会在主机文件中查找“saturn”，找到它所在的行，并提取与之关联的 IP 地址。随后，它会将所有这些信息放入 `hostent` 主机条目结构中。最终，程序会生成格式化消息，说明“saturn”的 IP 地址为“166.78.16.200”。

### 注意

请注意，在这个示例中，仍然需要将 IP 地址复制到 `in_addr` 结构中，但这次源数据不是 `inet_ntoa()` 示例中的无符号长整数，而是 `hostent` 主机条目结构。`hostent` 结构的 `h_addr` 成员变量是一个指针，指向四字节 IP 地址的第一个字节；该地址已经以网络字节序存储。

## 异步查找主机的 IP 地址

在介绍 `gethostname()` 时，我提到过使用它有一个注意事项。在 `getXbyY` 函数中（其中之一就是 `gethostbyname()`），检索到的数据可能来自本地主机，也可能通过网络请求从某种服务器获取。一旦涉及网络通信，就必须考虑响应时间，以及网络请求进行期间应用程序对用户操作的响应能力。

`WSAAsyncGetHostByName()` 是 `gethostbyname()` 的异步版本。它被添加到 WinSock 中，用来配合 Berkeley 套接字函数，适应 Microsoft Windows 的消息传递体系结构。之所以称此函数为异步函数，是因为调用它不会暂停调用应用程序的执行，而是允许应用程序继续运行，直到 `WSAAsyncGetHostByName()` 发出的请求完成。调用 `gethostbyname()` 或任何其他 `getXbyY` 函数时，无法保证函数何时会返回结果。如果函数触发了网络操作，响应时间便无法确定。在请求尚未完成时，程序会停止运行；用户无法移动或关闭窗口，甚至无法取消操作。不仅如此，在 Windows 3.1 的非抢占式环境中，其他应用程序也会受到影响；整个系统似乎会暂时（甚至长时间）停滞。使用 `WSAAsyncGetHostByName()` 可以让应用程序响应用户输入，也不会对计算机上运行的其他应用程序造成不利影响。请求完成后，Windows 会向应用程序中的某个窗口发送一条消息。在请求仍未完成期间（例如，联网的域名服务器正在查找数据库并准备通过网络发回搜索结果时），调用应用程序以及计算机上其他应用程序的消息循环都会继续运行，因此所有程序都能响应用户操作。

> **注意**
>
> 实际上，如果你确定程序运行的环境使用本地主机文件解析主机名，就不必承担使用 `getXbyY` 函数异步版本所需的额外开销；阻塞函数完全够用，因为你知道它们会立即返回，不会导致任何正在运行的应用程序出现响应问题。

`WSAAsyncGetHostByName()` 的函数原型如下：

```c
HANDLE PASCAL FAR WSAAsyncGetHostByName(HWND hWnd, u_int wMsg,
    const char FAR * name, char FAR * buf, int buflen);
```

`hWnd` 是窗口句柄；`WSAAsyncGetHostByName()` 完成异步操作后，会向该窗口发送一条消息。`wMsg` 是异步操作完成后发送给 `hWnd` 的消息。`wMsg` 通常是用户定义的消息（即 `WM_USER + 1`）。`name` 是指向字符串的指针，该字符串包含要查询信息的主机名（例如 `"goober"` 或 `"goober.ping.com"`）。`buf` 是指向一块内存区域的指针；主机名查找成功后，该区域将包含目标主机的 `hostent` 结构。请注意，此缓冲区必须比 `hostent` 结构本身更大，因为 WinSock 还要用额外空间存储相关信息。WinSock 提供了一个名为 `MAXGETHOSTSTRUCT` 的已定义值，可将其用作缓冲区大小。此大小可以确保分配了足够的空间。`buflen` 是 `buf` 缓冲区的大小。为安全起见，它应设为 `MAXGETHOSTSTRUCT`。

如果成功启动异步操作，`WSAAsyncGetHostByName()` 的返回值就是异步任务的句柄。如果初始化失败，该函数会返回 0（零），此时应调用 `WSAGetLastError()` 来查明错误原因。可能的错误值包括：如果未成功调用 `WSAStartup()`，则为 `WSANOTINITIALIZED`；如果网络子系统发生故障，则为 `WSAENETDOWN`；如果由于特定 WinSock 实现内部的资源冲突，函数当前无法排入调度，则为 `WSAEWOULDBLOCK`；如果当前正在进行阻塞式 WinSock 操作，则为 `WSAEINPROGRESS`。请注意，该函数的返回值并不能告诉你请求的信息是否已成功检索；它只能说明函数是否已正常启动。

前面的示例代码用于显示运行程序的计算机名称和 IP 地址，现在可以改写为使用以下异步调用：

```c
// 全局变量
#define WM_USER_GETHOSTBYNAME (WM_USER + 1)
#define HOST_NAME_LEN (50)
```

```cpp
break;

default:
    break;
}
}
```

请注意，在 `WM_USER_GETHOSTBYNAME` 消息处理程序中，首先执行的是对 `WSAGETASYNCERROR()` 的调用。这是一个宏，用于确定 `WSAAsyncGetHostByName()` 请求是否成功。返回值为 0（零）表示一切正常。其他可能的值是 WINSOCK.H 中定义的各种错误代码。如果 `WSAGETASYNCERROR()` 返回错误 `WSAENOBUFS`，说明传递给 `WSAAsyncGetHostByName()` 的缓冲区太小。为确保安全，请使用至少有 `MAXGETHOSTSTRUCT` 字节的缓冲区。另外请注意，在 `WM_USER_GETHOSTBYNAME` 消息处理程序中，`wParam` 是当前返回操作的异步任务句柄。这意味着你可以对多个同时进行的异步请求使用同一个 `WM_USER` 消息。之后检查 `wParam`，即可确定当时返回的是哪项具体操作。

## 使用 Visual C++ 实现

本书介绍的是如何在 Microsoft Visual C++ 和 Microsoft 基础类库中使用 WinSock。前面的示例采用了“老式”的 SDK 风格，用来介绍第一个异步函数。本书其余示例主要基于 Visual C++ 和 MFC。使用 MFC 时，前面的示例代码可以按如下方式实现。

首先是类声明。本例中有一个名为 CMyWindow 的类，它派生自基类 CFrameWnd。CFrameWnd 是 MFC 提供的一个类。这个简单的类并未展示完整的类声明，只列出了重现前面 SDK 示例所需的部分：

```cpp
class CMyWindow : public CFrameWnd
{

...

    // 成员变量
#define HOST_NAME_LEN (50)
    char m_lpszHostName[HOST_NAME_LEN];      // 将用于存放主机名
    char m_lpszMessage[100];                 // 提示信息
    char m_lpszIP[16];                       // IP 地址字符串
    PHOSTENT m_phostent;                     // 指向主机条目结构的指针
    char m_lpszHostEntryBuffer[MAXGETHOSTSTRUCT]; // 主机条目结构
    IN_ADDR m_in;                            // Internet 地址结构
    HANDLE m_hGetHostByName;                 // 异步请求的句柄

    // 消息映射中的成员函数
    //{{AFX_MSG(CMyWindow)
    afx_msg void OnDoAsyncGetHostByName();
```

