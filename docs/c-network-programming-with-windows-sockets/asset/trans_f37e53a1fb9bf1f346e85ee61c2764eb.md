

## 清单 14.2（续）

```cpp
plb->InsertString(0, pszMessage);
free(pDataWritten);
break;

case CWINSOCK_ERROR_WRITING:
    // lParam = pointer to data that generated error sending
    pDataWritten = (LPVOID)lParam;
    wsprintf(pszMessage, "Error sending data (%s)", pDataWritten);
    plb->InsertString(0, pszMessage);
    free(pDataWritten);
    break;

case CWINSOCK_DONE_READING:
    // lParam = # data chunks in queue
    pDataRead = m_pDatagram->Read(&nLen, &sin);
    // display informational message (data must be NULL terminated)
    memcpy(&in, &sin.sin_addr.s_addr, 4);
    wsprintf(pszMessage, "Data received (%s) from %s, %d",
        pDataRead, inet_ntoa(in), ntohs(sin.sin_port));
    plb->InsertString(0, pszMessage);

    // echo the data back to the sender
    if (m_pDatagram->Write(nLen, pDataRead, &sin) != CWINSOCK_NOERROR)
    {
        wsprintf(pszMessage, "Error sending data (%s)", pDataRead);
        plb->InsertString(0, pszMessage);
        free(pDataRead);
    }

    break;

case CWINSOCK_ERROR_READING:
    break;

default:
    break;
}

return 0L;
}
```

## 数据报回显客户端 CDECLNT

数据报回显客户端 CDECLNT 是第 8 章中所述 DECLIENT 程序的重新实现。它使用一个从 CFormView 派生的对象作为其主界面。CMainView 对象的头文件如清单 14.3 所示，其实现如清单 14.4 所示。该对象完成了 CDECLNT 应用程序的大部分工作。在创建该对象后会很快调用 OnInitialUpdate()。此函数负责启动 WinSock 子系统、创建客户端数据报套接字、提示输入 CDESRV 数据报回显服务器的主机名或 IP 地址，并设置一个用于数据写入的五秒间隔计时器。当计时器到期时，会调用 OnTimer()。如果没有正在等待发送的数据（由发送缓冲区 m_pszBuf 的第一个字节包含 NULL 来表示），则会格式化一个发送数据流，并调用数据报套接字对象的 Write() 成员函数，将数据发送到指定服务器的 2000 端口。写入完成后，会调用 OnDatagram()，其 wParam 参数设置为 CWINSOCK_DONE_WRITING。m_pszBuf 的第一个字节会被设置为 NULL，以表示缓冲区可用。这种缓冲区使用方式与动态分配和释放内存的方法形成对比。CMainView 对象持续等待先前发送的数据被回显。当数据到达数据报套接字时，会触发 OnDatagram()，其 wParam 参数设置为 CWINSOCK_DONE_READING。读取数据后，读取缓冲区即被释放。当客户端应用程序关闭时，会调用 CMainView 的析构函数，销毁数据报套接字对象并关闭 WinSock 子系统。

## 清单 14.3：CDECLNT 的 MAINVIEW.H

```cpp
    // mainview.h : header file
    //

    /////////////////////////////////////////////////////////////////////////////
    // CMainView form view

    #ifndef __AFXEXT_H_
    #include <afxext.h>
    #endif

    #include "cwinsock.h"    // Windows Sockets classes

    class CMainView : public CFormView
    {
        DECLARE_DYNCREATE(CMainView)

    private:
        CWinSock * m_pWinSock;          // WinSock sub-system startup/.shutdown
        CDatagramSocket * m_pDatagram;  // Datagram socket to receive from
        char m_pszBuf[100];             // buffer to send
        char m_pszServer[100];          // host name or IP address of datagram server

    protected:
        CMainView();                    // protected constructor used by dynamic creation

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
    afx_msg LONG OnDatagram(WPARAM wParam, LPARAM lParam);
    afx_msg void OnTimer(UINT nIDEvent);
    //}}AFX_MSG
    DECLARE_MESSAGE_MAP()
};

///////////////////////////////////////////////////////////////

#define WM_USER_DATAGRAM (WM_USER + 1)
```

## 清单 14.4：CDECLNT 的 MAINVIEW.CPP

```cpp
// mainview.cpp : implementation file
//

#include "stdafx.h"
#include "cdeclnt.h"
#include "mainview.h"
#include "servdlg.h"

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

    // initialize class variables

    m_pWinSock = NULL;
    m_pDatagram = NULL;
    (*m_pszBuf) = '\0';
}

CMainView::~CMainView()
{
    // free the datagram and WinSock objects

    if (m_pDatagram)
    {
        m_pDatagram->DestroySocket();
        delete m_pDatagram;
        m_pDatagram = NULL;
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

void CMainView::OnInitialUpdate()
{
    // start the timer used to trigger the socket writes

    SetTimer(1, 5000, NULL);    // 5 second timer

    // get pointer to list box used for status messages

    CListBox *plb = (CListBox *)GetDlgItem(IDC_LIST_STATUS);

    // initialize the WinSock object

    m_pWinSock = new CWinSock;
    if (m_pWinSock->Startup() == CWINSOCK_NOERROR)
        plb->InsertString(0, "WinSock initialized");
    else
    {
        plb->InsertString(0, "WinSock initialization failed");
        delete m_pWinSock;
        m_pWinSock = NULL;
        return;
    }

    // prompt for server information
    // (host name or IP address of datagram server)

    while (1)
    {
        CServerDlg dlg;
        dlg.DoModal();
        if (dlg.m_stringServer.GetLength() < sizeof(m_pszServer))
        {
            lstrcpy(m_pszServer, dlg.m_stringServer);
            break;
        }
        else
            AfxMessageBox("Host name or IP address too long");
    }

    // initialize the datagram socket object

    m_pDatagram = new CDatagramSocket(this, WM_USER_DATAGRAM);
    if (m_pDatagram->CreateSocket() == CWINSOCK_NOERROR)
        plb->InsertString(0, "Datagram created");
    else
    {
        plb->InsertString(0, "Datagram creation failed");
        delete m_pDatagram;
        m_pDatagram = NULL;
    }
}

BEGIN_MESSAGE_MAP(CMainView, CFormView)
    //{{AFX_MSG_MAP(CMainView)
    ON_MESSAGE(WM_USER_DATAGRAM, OnDatagram)
    ON_WM_TIMER()
    //}}AFX_MSG_MAP
END_MESSAGE_MAP()

/////////////////////////////////////////////////////////////////////////////
// CMainView message handlers

/////////////////////////////////////////////////////////////////////////////
// CMainView::OnDatagram()
//
// Receives messages from the datagram object.
//
LONG CMainView::OnDatagram(WPARAM wParam, LPARAM lParam)
{
    LPVOID pDataWritten; // pointer to data that is completely written
    LPVOID pDataRead;    // pointer to data just read
    int nLen;            // length
    SOCKADDR_IN sin;     // Internet address of data's sender
    IN_ADDR in;          // IP address of data's sender
    char pszMessage[1000]; // informational message

    // get pointer to list box used for status messages
    CListBox *plb = (CListBox *)GetDlgItem(IDC_LIST_STATUS);

    switch (wParam)
    {
    case CWINSOCK_DONE_WRITING:
        // lParam = pointer to data that was sent
        pDataWritten = (LPVOID)lParam;
        wsprintf(pszMessage, "Data sent (%s)", pDataWritten);
        plb->InsertString(0, pszMessage);
        (*m_pszBuf) = '\0';   // same as (*pDataWritten) = '\0';
        break;

    case CWINSOCK_ERROR_WRITING:
        // lParam = pointer to data that generated error sending
        pDataWritten = (LPVOID)lParam;
        wsprintf(pszMessage, "Error sending data (%s)", pDataWritten);
        plb->InsertString(0, pszMessage);
        (*m_pszBuf) = '\0';   // same as (*pDataWritten) = '\0';
        break;

    case CWINSOCK_DONE_READING:
        // lParam = # data chunks in queue
        pDataRead = m_pDatagram->Read(&nLen, &sin);
        // display informational message (data must be NULL terminated)
        memcpy(&in, &sin.sin_addr.s_addr, 4);
        wsprintf(pszMessage, "Data received (%s) from %s, %d",
            pDataRead, inet_ntoa(in), ntohs(sin.sin_port));
        plb->InsertString(0, pszMessage);
        free(pDataRead);
        break;

    case CWINSOCK_ERROR_READING:
        break;

    default:
        break;
    }

    return 0L;
}

void CMainView::OnTimer(UINT nIDEvent)
{
    static int nSendCount = 1;  // used to generate unique message
    char pszMessage[1000];      // informational message

    // make sure we are not sending out of a bad datagram socket
    if (m_pDatagram == NULL)
        return;

    // get pointer to List box used for status messages
    CListBox *plb = (CListBox *)GetDlgItem(IDC_LIST_STATUS);

    // send the buffer unless the previous send hasn't completed yet
    if ((*m_pszBuf) == '\0')
    {
        wsprintf(m_pszBuf, "Hello %d", nSendCount);
        ++nSendCount;
        // be sure to send terminating NULL character
        if (m_pDatagram->Write(strlen(m_pszBuf) + 1, m_pszBuf,
            m_pszServer, 2000) != CWINSOCK_NOERROR)
        {
            (*m_pszBuf) = '\0';
```

