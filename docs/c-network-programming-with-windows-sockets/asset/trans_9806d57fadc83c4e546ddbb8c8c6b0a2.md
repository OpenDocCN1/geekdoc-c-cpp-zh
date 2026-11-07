

### 列表 14.4（续）

```cpp
    wsprintf(pszMessage, "Error sending data (%s)", m_pszBuf);
    plb->InsertString(0, pszMessage);
  }
}

CFormView::OnTimer(nIDEvent);
}
```

## 运行数据报回显服务器和客户端

以下是运行数据报回显客户端和服务器时发生的事件示例：

- 1. 运行 CDESRV。
- 2. 在同一台或另一台计算机上运行 CDECLNT。程序会提示输入 CDESRV 的主机名或 IP 地址。
- 3. 五秒后，CDECLNT 中的计时器触发，导致调用 `CMainView::OnTimer()`。此时发送缓冲区未被使用，因此会将数据填入发送缓冲区，并使用 `m_pDatagram` 的 `Write()` 成员函数写入数据。
- 4. 在 CDECLNT 中调用 `CMainView::OnDatagram()`，并收到 `CWINSOCK_DONE_WRITING` 通知。随后将发送缓冲区标记为未使用，以便在下一次 `CMainView::OnTimer()` 触发时使用。
- 5. 在 CDESRV 中调用 `CMainView::OnDatagram()`，并收到 `CWINSOCK_DONE_READING` 通知。程序读取数据，并立即将其回显给客户端。
- 6. 在 CDESRV 中调用 `CMainView::OnDatagram()`，并收到 `CWINSOCK_DONE_WRITING` 通知。随后释放数据。
- 7. 在 CDECLNT 中调用 `CMainView::OnDatagram()`，并收到 `CWINSOCK_DONE_READING` 通知。程序读取回显的数据，然后释放数据。
- 8. CDECLNT 中的另一个计时器触发，随后重复上述过程。

## 流式回显客户端和服务器

这些程序 CSESRV 和 CSECLNT 展示了 `CStreamSocket` 对象的用法。CSESRV 服务器应用程序接收数据并将其发送回客户端。CSECLNT 客户端应用程序向服务器发送数据，并接收回显的回复。

## 流式回显服务器 CSESRV

与第 8 章所述的 SESERV 程序一样，此示例使用一个名为 CMainView、派生自 CFormView 的对象作为主要用户界面。成员变量 m_pWinSock 控制此程序中 WinSock 子系统的启动和关闭。成员变量 m_pStreamSrv 是一个指向流式套接字对象的指针，该对象等待客户端连接。成员变量 m_pStream 是实际负责从客户端接收数据并向客户端发送数据的流式套接字。OnStreamSrv() 成员函数接收服务器流式套接字对象的状态信息。每当客户端请求连接服务器时，都会触发用户自定义消息 WM_USER_STREAMSRV，从而调用该函数。OnStream() 成员函数接收实际与客户端通信的流式套接字对象的状态信息。每当建立或断开客户端连接，以及有数据可供读取或数据写入完成时，都会触发用户自定义消息 WM_USER_STREAM，从而调用该函数。

### 列表 14.5：CSESRV 的 MAINVIEW.H

```cpp
// mainview.h : header file
//
//////////////////////////////////////////////////////////////////////
// CMainView form view

#ifndef __AFXEXT_H__
#include <afxext.h>
#endif

#include "winsock.h"    // Windows Sockets classes

class CMainView : public CFormView
{
    DECLARE_DYNCREATE(CMainView)

private:
    CWinSock * m_pWinSock;          // WinSock sub-system startup/shutdown
    CStreamSocket * m_pStreamSrv;   // Stream socket to wait for connections on
    CStreamSocket * m_pStream;      // Stream socket to receive from

protected:
    CMainView();       // protected constructor used by dynamic creation

// Form Data
public:
    //{{AFX_DATA(CMainView)
    enum { IDD = IDD_DIALOG_MAIN };
    // NOTE: the ClassWizard will add data members here
    //}}AFX_DATA

// Attributes

public:

// Operations
public:

// Implementation
protected:
  virtual ~CMainView();
  virtual void DoDataExchange(CDataExchange* pDX);  // DDX/DDV support
  virtual void OnInitialUpdate();
  // Generated message map functions
  //{{AFX_MSG(CMainView)
  afx_msg LONG OnStreamSrv(WPARAM wParam, LPARAM lParam);
  afx_msg LONG OnStream(WPARAM wParam, LPARAM lParam);
  //}}AFX_MSG
  DECLARE_MESSAGE_MAP()
};

/////////////////////////////////////////////////////////////////////

#define WM_USER_STREAMSRV (WM_USER + 1)
#define WM_USER_STREAM    (WM_USER + 2)
```

`CMainView` 对象的实现如列表 14.6 所示。该对象负责完成 CSESRV 应用程序的大部分工作。对象创建后不久就会调用 `OnInitialUpdate()`。此函数负责启动 WinSock 子系统，并创建一个服务器流式套接字，使其在端口 2000 上等待连接请求到达。客户端请求连接时，会触发 `OnStreamSrv()` 成员函数，此时 `wParam` 被设为 `CWINSOCK_READY_TO_ACCEPT_CONNECTION`。随后使用 `m_pStream` 对象接受客户端的连接请求。连接建立后，会调用 `OnStream()`，此时 `wParam` 被设为 `CWINSOCK_YOU_ARE_CONNECTED`。客户端数据到达时，会调用 `OnStream()`，此时 `wParam` 被设为 `CWINSOCK_DONE_READING`。程序读取数据，并尝试将数据写回客户端以完成回显。写入完成后，会调用 `OnStream()`，此时 `wParam` 被设为 `CWINSOCK_DONE_WRITING`。此时会释放数据指针。关闭服务器应用程序时，会调用 `CMainView` 的析构函数，销毁两个流式套接字对象并关闭 WinSock 子系统。

### 列表 14.6：CSESRV 的 MAINVIEW.CPP

```cpp
// mainview.cpp : implementation file
//

#include "stdafx.h"
#include "csesrv.h"
#include "mainview.h"

#ifdef _DEBUG
#undef THIS_FILE
static char BASED_CODE THIS_FILE[] = __FILE__;
#endif

///////////////////////////////////////////////////////////////
// CMainView

IMPLEMENT_DYNCREATE(CMainView, CFormView)

CMainView::CMainView()
    : CFormView(CMainView::IDD)
{
    //{{AFX_DATA_INIT(CMainView)
    // NOTE: the ClassWizard will add member initialization here
    //}}AFX_DATA_INIT

    // initialization class variables

    m_pWinSock = NULL;
    m_pStreamSrv = NULL;
    m_pStream = NULL;
}

CMainView::~CMainView()
{
    // free the stream and WinSock objects

    if (m_pStreamSrv)
    {
        m_pStreamSrv->DestroySocket();
        delete m_pStreamSrv;
        m_pStreamSrv = NULL;
    }

    if (m_pStream)
    {
        m_pStream->DestroySocket();
        delete m_pStream;
        m_pStream = NULL;
    }

    if (m_pWinSock)
    {
        m_pWinSock->Shutdown();
        delete m_pWinSock;
        m_pWinSock = NULL;
    }
}

void CMainView::DoDataExchange(CDataExchange* pDX)
{
    CFormView::DoDataExchange(pDX);
    //{{AFX_DATA_MAP(CMainView)
    // NOTE: the ClassWizard will add DDX and DDV calls here
    //}}AFX_DATA_MAP
}

case CWINSOCK_READY_TO_ACCEPT_CONNECTION:
    // make sure the server is not already servicing a client
    if (m_pStream != NULL)
    {
        plb->InsertString(0, "Already servicing a client");
        break;
    }

    // accept the client connection
    int nStatus;
    m_pStream = new CStreamSocket(this, WM_USER_STREAM);
    nStatus = m_pStreamSrv->Accept(m_pStream);
    if (nStatus != CWINSOCK_NOERROR)
    {
        delete m_pStream;
        m_pStream = NULL;
        plb->InsertString(0, "Error accepting client connection");
        break;
    }
    else
        plb->InsertString(0, "Accepted client connection");

    break;

default:
    break;
}

return 0L;
}

////////////////////////////////////////////////////////////
// CMainView::OnStream()
////////////////////////////////////////////////////////////
// Receives messages from the connected stream object.
//
LONG CMainView::OnStream(WPARAM wParam, LPARAM lParam)
{
    LPVOID pDataWritten;    // pointer to data that is completely written
    LPVOID pDataRead;       // pointer to data just read
    int nLen;               // length
    char szMessage[1000];   // information message
    SOCKADDR_IN sin;        // Internet address of client
    IN_ADDR in;             // IP address of client
    int nStatus;            // error status

    // get pointer to list box used for status messages
    CListBox *plb = (CListBox *)GetDlgItem(IDC_LIST_STATUS);

    switch (wParam)
    {
        case CWINSOCK_DONE_WRITING:
            // lParam = pointer to data that was sent
            pDataWritten = (LPVOID)lParam;
            wsprintf(szMessage, "Data sent (%s)", pDataWritten);
            plb->InsertString(0, szMessage);
            free(pDataWritten);
            break;
    }
}
```

