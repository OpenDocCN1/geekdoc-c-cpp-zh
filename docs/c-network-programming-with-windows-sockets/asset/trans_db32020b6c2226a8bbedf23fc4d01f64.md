
```cpp
lstrcpy(pszError, "WinSock does not meet version requirements");
}
AfxMessageBox(pszError);
}
```

在编译和运行程序之前，唯一剩下要做的是更改链接器选项，以便为 16 位或 32 位版本分别链接 WINSOCK.LIB 或 WSOCK32.LIB。

图 8.1 显示即将选择 WinSock 信息菜单项。图 8.2 显示在 Windows NT 上使用 Microsoft 提供的 WinSock TCP/IP 协议栈运行的结果。

**图 8.1.**

*即将从“帮助”菜单中选择“WinSock 信息”。*

![](img/5e551abe6e0cb0588043ee757a235ddb_144_0.png)

**图 8.2.**

*Windows NT TCP/IP 协议栈的 WinSock 信息。*

![](img/5e551abe6e0cb0588043ee757a235ddb_144_1.png)

您可能希望在开发的应用程序中使用 CWinSockInfoDlg 类。它作为调试辅助工具可能非常有用。

## WinSock 数据库测试应用程序

此程序 DBTST 允许您对主机和服务执行 WinSock 数据库查找。它使用以下 WinSock 函数：`WSAStartup()`、`WSACleanup()`、`WSAGetLastError()`、`WSACancelAsyncRequest()`、`WSAAsyncGetHostByName()`、`WSAAsyncGetHostByAddr()`、`gethostbyname()`、`gethostbyaddr()`、`WSAAsyncGetServByName()`、`WSAAsyncGetServByPort()`、`getservbyname()`、`getservbyport()` 以及 `ntohs()`。此程序是从零开始创建的，没有借助 AppWizard。使用的是 Visual C++ 项目文件。

与让 AppWizard 完成繁琐工作相反，从零开始创建程序时必须采取额外步骤。从零开始创建程序的好处是，您不必处理可能不需要的功能，例如文档和视图。这种方法更接近旧的 SDK 做法，但仍然受益于 Microsoft Foundation Classes。

首先要查看的源文件是 STDAFX.H 和 STDAFX.CPP。这些文件支持预编译头功能。通过在每个实现文件（即 *.CPP）中包含 STDAFX.H，就不必在每个文件中包含必需的 Windows 和 MFC 头文件。STDAFX.H 和 STDAFX.CPP 分别如清单 8.3 和 8.4 所示。您必须配置编译器的预编译头编译选项才能使用此功能。

### 清单 8.3. DBTST 的 STDAFX.H。

```cpp
#include <afxwin.h>
#include <winsock.h>
```

### 清单 8.4. DBTST 的 STDAFX.CPP。

```cpp
#include "stdafx.h"
```

接下来关注的这些文件实现应用程序对象 `CTheApp`。`CTheApp` 派生自 MFC 类 `CWinApp`。类声明位于 DBTST.H 中，如清单 8.5 所示。该类在 DBTST.CPP 中实现，如清单 8.6 所示。请注意，这里的 WinSock 启动不如 WSINFO 示例中那样健壮；例如，出错时不会显示任何错误消息。相反，如果无法初始化 WinSock，应用程序会直接退出。

### 清单 8.5. DBTST 的 DBTST.H。

```cpp
#ifndef __DBTST_H__
#define __DBTST_H__

#include "resource.h"

///////////////////////////////////////////////////////////////
// CTheApp class declaration
//
class CTheApp : public CWinApp
{
private:
    WSADATA m_WsaData;  // WinSock data structure

public:
    BOOL InitInstance();
    int ExitInstance();
};

#endif // __DBTST_H
```

### 清单 8.6. DBTST 的 DBTST.CPP。

```cpp
///////////////////////////////////////////////////////////////
// CTheApp implementation file
//

#include "stdafx.h"
#include "dbtst.h"
#include "mainwindow.h"

///////////////////////////////////////////////////////////////
// Creating a CTheApp object starts the application running
//
CTheApp NEAR TheApp;

///////////////////////////////////////////////////////////////
// CTheApp::InitInstance
//
// When the CTheApp object is created, this member function is
// automatically called. WinSock is initiated here. The main window
// of the application is created and shown here.
//
BOOL CTheApp::InitInstance()
{
    if (WSAStartup(MAKEWORD(1, 1), &m_WsaData) != 0)
        return FALSE;

    m_pMainWnd = new CMainWindow();
    m_pMainWnd->ShowWindow(m_nCmdShow);
    m_pMainWnd->UpdateWindow();

    return TRUE;
}

///////////////////////////////////////////////////////////////
// CTheApp::ExitInstance
//
// When the application is closed, shutdown WinSock.
//
int CTheApp::ExitInstance()
{
    WSACleanup();

    return CWinApp::ExitInstance();
}
```

此应用程序可以查找主机或服务信息。为支持这一点，使用了两个对话框。主机对话框在 CHostDlg 类中实现。该类是使用 App Studio 和 ClassWizard 创建的。类声明文件（HOST.H）如清单 8.7 所示。清单 8.8 显示了类实现文件（HOST.CPP）。CHostDlg 有一个公共成员变量，即名为 m_strHost 的 CString 对象。此变量包含用户在对话框的单个 EDIT 控件中输入的字符串。该对话框有三个按钮：异步、阻塞和取消。如果用户按下“异步”按钮，则向调用方返回 IDC_BUTTON_ASYNC，表示用户希望异步执行数据库查找。同样，按下“阻塞”按钮时返回 IDC_BUTTON_BLOCKING。按下“取消”会中止查找。

### 清单 8.7. DBTST 的 HOST.H。

```cpp
///////////////////////////////////////////////////////////////
// CHostDlg dialog
//
class CHostDlg : public CDialog
{
// Construction
public:
    CHostDlg(CWnd* pParent = NULL);  // standard constructor

// Dialog Data
    //{{AFX_DATA(CHostDlg)
    enum { IDD = IDD_HOST };
    CString m_strHost;
    //}}AFX_DATA

// Implementation
protected:
    virtual void DoDataExchange(CDataExchange* pDX);  // DDX/DDV support

// Generated message map functions
    //{{AFX_MSG(CHostDlg)
    afx_msg void OnClickedButtonAsync();
    afx_msg void OnClickedButtonBlocking();
    //}}AFX_MSG
    DECLARE_MESSAGE_MAP()
};
```

### 清单 8.8. DBTST 的 HOST.CPP。

```cpp
// host.cpp : implementation file
//

#include "stdafx.h"
#include "dbtst.h"
#include "host.h"

#ifdef _DEBUG
#undef THIS_FILE
static char BASED_CODE THIS_FILE[] = __FILE__;
#endif

/////////////////////////////////////////////////////////////////////////////
// CHostDlg dialog

CHostDlg::CHostDlg(CWnd* pParent /*=NULL*/)
    : CDialog(CHostDlg::IDD, pParent)
{
    //{{AFX_DATA_INIT(CHostDlg)
    m_strHost = "";
    //}}AFX_DATA_INIT
}

void CHostDlg::DoDataExchange(CDataExchange* pDX)
{
    CDialog::DoDataExchange(pDX);
    //{{AFX_DATA_MAP(CHostDlg)
    DDX_Text(pDX, IDC_EDIT_HOST, m_strHost);
    //}}AFX_DATA_MAP
}

BEGIN_MESSAGE_MAP(CHostDlg, CDialog)
    //{{AFX_MSG_MAP(CHostDlg)
    ON_BN_CLICKED(IDC_BUTTON_ASYNC, OnClickedButtonAsync)
    ON_BN_CLICKED(IDC_BUTTON_BLOCKING, OnClickedButtonBlocking)
    //}}AFX_MSG_MAP
END_MESSAGE_MAP()

/////////////////////////////////////////////////////////////////////////////
// CHostDlg message handlers

void CHostDlg::OnClickedButtonAsync()
{
    UpdateData(TRUE);
    EndDialog(IDC_BUTTON_ASYNC);
}

void CHostDlg::OnClickedButtonBlocking()
{
    UpdateData(TRUE);
    EndDialog(IDC_BUTTON_BLOCKING);
}
```

用于提示要查找哪个服务的对话框实现为 CServiceDlg 类。此对话框的源代码位于 SERVICE.H 和 SERVICE.CPP 文件中，分别如清单 8.9 和 8.10 所示。该代码遵循与 CHostDlg 类相似的格式，不同之处在于服务对话框中有两个数据输入字段：服务和协议。

### 清单 8.9. DBTST 的 SERVICE.H。

```cpp
///////////////////////////////////////////////////////////////
// CServiceDlg dialog
///////////////////////////////////////////////////////////////
class CServiceDlg : public CDialog
{
// Construction
public:
    CServiceDlg(CWnd* pParent = NULL);   // standard constructor

// Dialog Data
    //{{AFX_DATA(CServiceDlg)
    enum { IDD = IDD_SERVICE };
    CString m_stringService;
    CString m_stringProtocol;
    //}}AFX_DATA

// Implementation
protected:
    virtual void DoDataExchange(CDataExchange* pDX);   // DDX/DDV support

    // Generated message map functions
    //{{AFX_MSG(CServiceDlg)
    afx_msg void OnClickedButtonAsync();
    afx_msg void OnClickedButtonBlocking();
    //}}AFX_MSG
    DECLARE_MESSAGE_MAP()
};
```
