
### 清单 8.12. 续

```cpp
    // copy the service name or port number if its format is legal
    int nServiceLen = dlg.m_stringService.GetLength();
    if ((nServiceLen > USER_INPUT_BUF_LEN) || (nServiceLen == 0))
    {
        MessageBox("Service name or port number is either too long or unspecified",
            "Service Lookup");
        return;
    }
    lstrcpy(m_lpszService, dlg.m_stringService);

    // see if the user entered a port number
    m_nPort = atoi(m_lpszService);
    m_nPort = htons(m_nPort);

    // copy the transport protocol
    static char *lpszProtocol;
    int nProtocolLen = dlg.m_stringProtocol.GetLength();
    if (nProtocolLen > USER_INPUT_BUF_LEN)
    {
        MessageBox("Protocol name is too long", "Service Lookup");
        return;
    }
    if (nProtocolLen > 0)
    {
        lstrcpy(m_lpszProtocol, dlg.m_stringProtocol);
        lpszProtocol = m_lpszProtocol;
    }
    else
        lpszProtocol = NULL;    // protocol wasn't specified, so NULL gets passed

    if (nStatus == IDC_BUTTON_ASYNC)
    {
        // do an asynchronous service lookup

        if (m_hAsyncService != 0)
            MessageBox("Asynchronous service lookup already in progress", "Service Lookup");
        else
        {
            if (m_nPort == 0)
                m_hAsyncService = WSAAsyncGetServByName(m_hWnd, WM_USER_ASYNC_SERVICE_LOOKUP,
                    m_lpszService, lpszProtocol, m_achServEnt, MAXGETHOSTSTRUCT);
            else
                m_hAsyncService = WSAAsyncGetServByPort(m_hWnd, WM_USER_ASYNC_SERVICE_LOOKUP,
                    m_nPort, lpszProtocol, m_achServEnt, MAXGETHOSTSTRUCT);

            if (m_hAsyncService == 0)
            {
                wsprintf(lpszMessage, "Service lookup failed (WinSock error %d)",
                    WSAGetLastError());

                MessageBox(lpszMessage, "Service Lookup");
            }
        }
    }
    else
    {
        // do a blocking service lookup
        if (m_nPort == 0)
            m_pServEnt = getservbyname(m_lpszService, lpszProtocol);
        else
            m_pServEnt = getservbyport(m_nPort, lpszProtocol);

        if (m_pServEnt == NULL)
            wsprintf(lpszMessage, "Service lookup failed (WinSock error %d)",
                WSAGetLastError());
        else
        {
            // format the results, converting the port to host byte order
            wsprintf(lpszMessage, "%s service using protocol %s has port %d",
                m_pServEnt->s_name, m_pServEnt->s_proto, ntohs(m_pServEnt->s_port));
        }
        MessageBox(lpszMessage, "Service Lookup");
    }
}

///////////////////////////////////////////////////////////////////
// CMainWindow::OnAsyncService
//
// Called when the asynchronous lookup is done.
LONG CMainWindow::OnAsyncService(WPARAM wParam, LPARAM lParam)
{
    char lpszMessage[100];   // informational message

    // check for an error
    if (WSAGETASYNCERROR(lParam) != 0)
        wsprintf(lpszMessage,
            "Service lookup failed (WinSock error %d)",
            WSAGETASYNCERROR(lParam));
    else
    {
        // assign a servent host entry pointer to the buffer
        m_pServEnt = (PSERVENT)m_achServEnt;

        // format the results, converting the port to host byte order
        wsprintf(lpszMessage, "%s service using protocol %s has port %d",
            m_pServEnt->s_name, m_pServEnt->s_proto, ntohs(m_pServEnt->s_port));
    }

    m_hAsyncService = 0;
    MessageBox(lpszMessage, "Service Lookup");

    return 0L;
}

///////////////////////////////////////////////////////////////////
// CMainWindow::OnCancelService
//
// Called when the Test | Cancel Service Lookup menu item is selected.
void CMainWindow::OnCancelService()
{
    char lpszMessage[100];   // informational message

    // see if there is an outstanding asynchronous request
    if (m_hAsyncService == 0)
        lstrcpy(lpszMessage, "No asynchronous service lookup in progress");
    else
    {
        // cancel the asynchronous request

        if (WSACancelAsyncRequest(m_hAsyncService) != 0)
            wsprintf(lpszMessage, "Cancel asynchronous service lookup failed (WinSock error %d)",
                WSAGetLastError());
        else
            lstrcpy(lpszMessage, "Asynchronous service lookup canceled");

        m_hAsyncService = 0;
    }

    MessageBox(lpszMessage, "Service Lookup");
}
```

DBTST 的一个示例执行过程如图 8.3 至图 8.7 所示。图 8.3 显示了 DBTST 应用程序的菜单。图 8.4 显示输入主机信息，图 8.5 显示主机查找的结果。图 8.6 显示输入服务信息，图 8.7 显示服务查找的结果。你可能想把这个应用程序放在手边，因为当你需要快速获知主机的 IP 地址时，它会非常方便。

**图 8.3.**
*DBTST 菜单项。*

![](img/5e551abe6e0cb0588043ee757a235ddb_158_0.png)

**图 8.4.**
*输入主机查找信息。*

![](img/5e551abe6e0cb0588043ee757a235ddb_159_0.png)

**图 8.5.**
*主机查找结果。*

![](img/5e551abe6e0cb0588043ee757a235ddb_159_1.png)

**图 8.6.**
*输入服务查找信息。*

![](img/5e551abe6e0cb0588043ee757a235ddb_159_2.png)

**图 8.7.**
*服务查找结果。*

![](img/5e551abe6e0cb0588043ee757a235ddb_160_0.png)

## 数据报回显客户端与服务器

这些程序 DESERV 和 DECLIENT 演示了非阻塞数据报套接字的使用。它们使用以下 WinSock 函数：`WSAStartup()`、`WSACleanup()`、`WSAGetLastError()`、`socket()`、`closesocket()`、`bind()`、`WSAAsyncSelect()`、`sendto()`、`recvfrom()`、`getsockname()`、`ntohs()` 和 `inet_ntoa()`。DESERV 服务器应用程序接收数据并将其发送回客户端。DECLIENT 客户端应用程序向服务器发送数据并接收回显的回复。

### 数据报回显服务器 DESERV

这些程序使用 Visual C++ 的 AppWizard 功能生成。WINSOCK.H 头文件包含在 STDAFX.H 预编译头文件中，如清单 8.13 所示。项目的源模块会包含 STDAFX.H，因此 WinSock 函数和结构始终可用。

**清单 8.13. 用于 DESERV 的 STDAFX.H。**

```cpp
// stdafx.h : include file for standard system include files,
//  or project specific include files that are used frequently, but
//  are changed infrequently
//

#include <afxwin.h>      // MFC core and standard components
#include <afxext.h>      // MFC extensions
#include <winsock.h>     // Windows Sockets
```

与 WSINFO 示例一样，DESERV 使用应用程序对象分别在 `CDeservApp::InitInstance()` 和 `CDeservApp::ExitInstance()` 中启动和停止 WinSock。

DESERV 使用单文档界面进行窗口管理。AppWizard 创建了一个派生自 MFC 类 `CView` 的默认视图类，但应用程序并未使用这个类。相反，它使用了一个派生自 `CFormView` 的对象。使用 `CFormView` 意味着首先使用 App Studio 创建对话框资源。创建了一个对话框，其中包含一个静态文本标签和一个用于显示状态消息的列表框。一般来说，会创建对话框资源，并使用 ClassWizard 创建派生自 `CDialog` 的类。由于你希望这个对话框资源成为程序的主界面，因此使用 ClassWizard 创建派生自 `CFormView` 的类。但首先，必须正确设置对话框资源的标志。具体来说，样式为 child，边框为 none，visible 标志未勾选，Caption 留空。图 8.8 显示了用作 DESERV 主窗口的对话框资源的对话框属性中的样式部分。

**图 8.8.**
*DESERV 主窗口对话框资源的样式属性。*

![](img/5e551abe6e0cb0588043ee757a235ddb_161_0.png)

对应用程序对象 `CDeservApp` 进行了修改，使其使用这个视图，而不是 AppWizard 生成的默认视图。`CDeservApp::InitInstance()` 的默认实现中有一个对 `AddDocTemplate()` 的调用，如下所示：

```cpp
AddDocTemplate(new CSingleDocTemplate(IDR_MAINFRAME,
    RUNTIME_CLASS(CDeservDoc),
    RUNTIME_CLASS(CMainFrame),       // main SDI frame window
    RUNTIME_CLASS(CDeservView)));
```

它需要如下所示：

```cpp
AddDocTemplate(new CSingleDocTemplate(IDR_MAINFRAME,
    RUNTIME_CLASS(CDeservDoc),
    RUNTIME_CLASS(CMainFrame),       // main SDI frame window
    RUNTIME_CLASS(CMainView)));
```

派生自 `CFormView` 的对象名为 `CMainView`，其头文件如清单 8.14 所示。注意成员变量 `m_s` 和 `m_addr`，以及函数 `OnAsyncSelect()`。`OnAsyncSelect()` 是手动添加到类中的，因为 ClassWizard 不支持用户自定义消息。
