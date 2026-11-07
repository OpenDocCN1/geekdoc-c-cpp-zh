

## 列表 14.6（续）

```cpp
case CWINSOCK_ERROR_WRITING:
    // lParam = 指向发送时产生错误的数据的指针
    pDataWritten = (LPVOID)lParam;
    wsprintf(pszMessage, "Error sending data (%s)", pDataWritten);
    pIb->InsertString(0, pszMessage);
    free(pDataWritten);
    break;

case CWINSOCK_DONE_READING:
    // lParam = 队列中的数据块数量
    pDataRead = m_pStream->Read(&len);
    wsprintf(pszMessage, "Data received (%s)", pDataRead);
    pIb->InsertString(0, pszMessage);

    // 将数据回显给发送方
    if (m_pStream->Write(nLen, pDataRead) != CWINSOCK_NOERROR)
    {
        wsprintf(pszMessage, "Error sending data (%s)", pDataRead);
        pIb->InsertString(0, pszMessage);
        free(pDataRead);
    }

    break;

case CWINSOCK_ERROR_READING:
    break;

case CWINSOCK_YOU_ARE_CONNECTED:
    // 输出客户端信息
    nStatus = m_pStream->GetPeerName(&sin);
    if (nStatus == CWINSOCK_NOERROR)
    {
        memcpy(&sin, &sin.sin_addr.s_addr, 4);
        wsprintf(pszMessage, "Connected to client %s, %d",
            inet_ntoa(sin), ntohs(sin.sin_port));
        pIb->InsertString(0, pszMessage);
    }
    else
        pIb->InsertString(0, "Error getting client name");
    break;

case CWINSOCK_LOST_CONNECTION:
    // 客户端关闭了连接
    m_pStream->DestroySocket();
    delete m_pStream;
    m_pStream = NULL;
    pIb->InsertString(0, "Client closed connection");
    break;

default:
    break;
}

return 0L;
```

## 流式回显客户端 CSECLNT

流式回显客户端 CSECLNT 是对第 8 章介绍的 SECLIENT 程序的重新实现。它使用一个派生自 CFormView 的对象作为主界面。CMainView 对象的头文件见列表 14.7，其实现见列表 14.8。该对象承担了 CSECLNT 应用程序的大部分工作。对象创建后不久便会调用 OnInitialUpdate()。此函数负责启动 WinSock 子系统、创建客户端流套接字、提示输入主机名或 IP 地址以连接到 CSESRV 流式回显服务器，并设置一个 5 秒间隔的计时器，用于触发数据写入。当服务器在端口 2000 上接受客户端的连接请求时，将调用 OnStream()，此时 wParam 设置为 CWINSocket_YOU_ARE_CONNECTED。5 秒计时器触发时，将调用 OnTimer()。如果没有等待发送的数据（即传出缓冲区 m_pszBuf 的第一个字节为 NULL），程序就会格式化一个传出数据流，并调用流套接字对象的 Write() 成员函数，将数据发送到指定服务器。写入完成后，将调用 OnStream()，此时 wParam 设置为 CWINSocket_DONE_WRITING。m_pszBuf 的第一个字节会被设为 NULL，以指示缓冲区可用。CMainView 对象会持续等待先前发送的数据回显。当数据到达流套接字时，将触发 OnStream()，此时 wParam 设置为 CWINSocket_DONE_READING。随后读取数据，并释放读取缓冲区。关闭客户端应用程序时，将调用 CMainView 的析构函数，销毁流套接字对象并关闭 WinSock 子系统。

## 列表 14.7 CSECLNT 的 MAINVIEW.H

```cpp
// MAINVIEW.H: 头文件
//

///////////////////////////////////////////////////////////////////////
// CMainView 表单视图

#ifndef __AFXEXT_H__
#include <afxext.h>
#endif

#include "winsock.h"    // Windows 套接字类

class CMainView : public CFormView
{
    DECLARE_DYNCREATE(CMainView)

private:
    CWinSock * m_pWinSock;          // WinSock 子系统的启动/关闭
    CStreamSocket * m_pStream;      // 用于接收数据的流套接字
    char m_pszBuf[100];             // 待发送缓冲区
    char m_pszServer[100];          // 流服务器的主机名或 IP 地址

protected:
    CMainView();        // 用于动态创建的受保护构造函数

// 表单数据
public:
    //{{AFX_DATA(CMainView)
    enum { IDD = IDD_DIALOG_MAIN };
    // NOTE: the ClassWizard will add data members here
    //}}AFX_DATA

// 属性
public:

// 操作
public:

// 实现
protected:
    virtual ~CMainView();
    virtual void DoDataExchange(CDataExchange* pDX);  // DDX/DDV 支持
    virtual void OnInitialUpdate();
    // 生成的消息映射函数
    //{{AFX_MSG(CMainView)
    afx_msg LONG OnStream(WPARAM wParam, LPARAM lParam);
    afx_msg void OnTimer(UINT nIDEvent);
    //}}AFX_MSG
    DECLARE_MESSAGE_MAP()
};

////////////////////////////////////////////////////////////

#define WM_USER_STREAM (WM_USER + 1)
```

## 列表 14.8 CSECLNT 的 MAINVIEW.CPP

```cpp
// mainview.cpp : 实现文件
//

#include "stdafx.h"
#include "csclnt.h"
#include "mainview.h"
#include "servdlg.h"

#ifdef _DEBUG
#undef THIS_FILE
static char BASED_CODE THIS_FILE[] = __FILE__;
#endif

////////////////////////////////////////////////////////////
// CMainView

IMPLEMENT_DYNCREATE(CMainView, CFormView)

CMainView::CMainView()
    : CFormView(CMainView::IDD)
{
    //{{AFX_DATA_INIT(CMainView)
    // NOTE: the ClassWizard will add member initialization here
    //}}AFX_DATA_INIT

    // 初始化类变量

    m_pWinSock = NULL;
    m_pStream = NULL;
    (*m_pszBuf) = '\0';
}

CMainView::~CMainView()
{
    // 释放流套接字和 WinSock 对象

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

void CMainView::OnInitialUpdate()
{
    // 启动用于触发套接字写入的计时器

    SetTimer(1, 5000, NULL);    // 5 秒计时器

    // 获取用于显示状态消息的列表框指针

    CListBox *plb = (CListBox *)GetDlgItem(IDC_LIST_STATUS);

    // 初始化 WinSock 对象

    m_pWinSock = new CWinSock;
    if (m_pWinSock->Startup() == WINSOCK_NOERROR)
        plb->InsertString(0, "WinSock initialized");
    else
    {
        plb->InsertString(0, "WinSock initialization failed");
        delete m_pWinSock;
        m_pWinSock = NULL;
        return;
    }

    // 提示输入服务器信息
    //（流服务器的主机名或 IP 地址）

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

    // 初始化流套接字对象

    m_pStream = new CStreamSocket(this, WM_USER_STREAM);
    if (m_pStream->CreateSocket() == CWIN_SOCK_NOERROR)
        plb->InsertString(0, "Stream created");
    else
    {
        plb->InsertString(0, "Stream creation failed");
        delete m_pStream;
        m_pStream = NULL;
    }

    // 将客户端连接到服务器
    if (m_pStream->Connect(m_pszServer, 2000) == CWINSOCK_NOERROR)
        plb->InsertString(0, "Stream connect attempt made");
    else
    {
        plb->InsertString(0, "Stream connect attempt failed");
        delete m_pStream;
        m_pStream = NULL;
    }

    BEGIN_MESSAGE_MAP(CMainView, CFormView)
        //{{AFX_MSG_MAP(CMainView)
        ON_MESSAGE(WM_USER_STREAM, OnStream)
        ON_WM_TIMER()
        //}}AFX_MSG_MAP
    END_MESSAGE_MAP()

    ////////////////////////////////////////////////////////////////
    // CMainView 消息处理程序

    ////////////////////////////////////////////////////////////////

    // CMainView::OnStream()
    //
    // 接收来自流对象的消息。
    //
    LONG CMainView::OnStream(WPARAM wParam, LPARAM lParam)
    {
        LPVOID pDataWritten;    // 指向已完全写入的数据的指针
        LPVOID pDataRead;       // 指向刚读取的数据的指针
        int nLen;               // 长度
        char pszMessage[1000];  // 信息消息

        // 获取用于显示状态消息的列表框指针
        CListBox *pLb = (CListBox *)GetDlgItem(IDC_LIST_STATUS);

        switch (wParam)
        {
            case CWINSOCK_DONE_WRITING:
                // lParam = 指向已发送数据的指针
                pDataWritten = (LPVOID)lParam;
                wsprintf(pszMessage, "Data sent (%s)", pDataWritten);
                pLb->InsertString(0, pszMessage);
                (*m_pszBuf) = '\0';  // 等同于 (*pDataWritten) = '\0';
                break;

            case CWINSOCK_ERROR_WRITING:
                // lParam = 指向发送时产生错误的数据的指针
                pDataWritten = (LPVOID)lParam;
                wsprintf(pszMessage, "Error sending data (%s)", pDataWritten);
                pLb->InsertString(0, pszMessage);
                (*m_pszBuf) = '\0';  // 等同于 (*pDataWritten) = '\0';
                break;

            case CWINSOCK_DONE_READING:
                // lParam = 队列中的数据块数量
                pDataRead = m_pStream->Read(&nLen);
                wsprintf(pszMessage, "Data received (%s)", pDataRead);
                pLb->InsertString(0, pszMessage);
                free(pDataRead);
                break;

            case CWINSOCK_ERROR_READING:
                break;

            case CWINSOCK_YOU_ARE_CONNECTED:
                pLb->InsertString(0, "Connected to server");
                break;

            case CWINSOCK_LOST_CONNECTION:
                // 服务器关闭了连接
                m_pStream->DestroySocket();
                delete m_pStream;
                m_pStream = NULL;
                pLb->InsertString(0, "Server closed connection");
                break;

            default:
                break;
        }
    }
```

