

## 清单 15.2（续）

```cpp
if (nLen != sizeof(dbcmd))
{
    plb->InsertString(0, "This client cannot handle partial blocks");
    free(pDataRead);
    return;
}

// copy the data to a database command structure
memcpy(&dbcmd, pDataRead, sizeof(dbcmd));
free(pDataRead);

// display database command results
if (dbcmd.nCommand == DB_OK)
    wsprintf(pszMessage, "OK (ID %d, '%s')", dbcmd.nID, dbcmd.szValue);
else if (dbcmd.nCommand == DB_ERROR)
    wsprintf(pszMessage, "Error (ID %d, '%s')", dbcmd.nID, dbcmd.szValue);
else
    lstrcpy(pszMessage, "Invalid database response");
plb->InsertString(0, pszMessage);
}

//////////////////////////////////////////////////////////////
// CMainView::OnClickedButtonRead()
//////////////////////////////////////////////////////////////
void CMainView::OnClickedButtonRead()
{
    // get pointer to list box used for status messages
    CListBox *plb = (CListBox *)GetDlgItem(IDC_LIST_STATUS);

    // allocate memory for database command structure
    LPDBCOMMAND pdb = (LPDBCOMMAND)malloc(sizeof(DBCOMMAND));
    if (pdb == NULL)
        plb->InsertString(0, "Cannot allocate memory for command");
    else
    {
        memset(pdb, 0, sizeof(DBCOMMAND));
        UpdateData(TRUE);
        FillAndSendDBCmd(pdb, m_stringFile, m_stringSection, m_stringEntry);
    }
}

//////////////////////////////////////////////////////////////
// CMainView::OnClickedButtonWrite()
//////////////////////////////////////////////////////////////
void CMainView::OnClickedButtonWrite()
{
    // get pointer to list box used for status messages
    CListBox *plb = (CListBox *)GetDlgItem(IDC_LIST_STATUS);

    // allocate memory for database command structure
    LPDBCOMMAND pdb = (LPDBCOMMAND)malloc(sizeof(DBCOMMAND));
    if (pdb == NULL)
        plb->InsertString(0, "Cannot allocate memory for command");
    else
    {
        memset(pdb, 0, sizeof(DBCOMMAND));
        UpdateData(TRUE);
        FillAndSendDBCmd(pdb, m_stringFile, m_stringSection, m_stringEntry,
            m_stringValue);
    }
}

///////////////////////////////////////////////////////////////////////
// CMainView::FillAndSendDBCmd()
//
void CMainView::FillAndSendDBCmd(LPDBCOMMAND pdb, LPCSTR szFile,
    LPCSTR szSection, LPCSTR szEntry, LPCSTR szValue/* = NULL*/)
{
    char pszMessage[1000];    // informational message
    static int nID = 1;       // database command identifier

    // get pointer to list box used for status messages
    CListBox *plb = (CListBox *)GetDlgItem(IDC_LIST_STATUS);

    // fill out command parameters
    pdb->nID = nID;

    lstrcpy(pdb->szFile, szFile);
    lstrcpy(pdb->szSection, szSection);
    lstrcpy(pdb->szEntry, szEntry);

    if (szValue == NULL)
        pdb->nCommand = DB_READ;
    else
    {
        pdb->nCommand = DB_WRITE;
        lstrcpy(pdb->szValue, szValue);
    }

    // send the command to the server
    if (m_pStream->Write(sizeof(DBCOMMAND), pdb) == CWINSOCK_ERROR)
    {
        wsprintf(pszMessage, "Error sending data (ID %d)", pdb->nID);
        plb->InsertString(0, pszMessage);
        free(pdb);
    }
    else
        ++nID;
}

///////////////////////////////////////////////////////////////////////
// CMainView::OnDatagram()
//
// Receives messages from the heartbeat datagram object.
LONG CMainView::OnDatagram(WPARAM wParam, LPARAM lParam)
{
    LPVOID pDataWritten;    // pointer to data that is completely written
    LPVOID pDataRead;       // pointer to data just read
    int nLen;               // length
    char pszMessage[1000];  // informational message

    // get pointer to list box used for status messages
    CListBox *plb = (CListBox *)GetDlgItem(IDC_LIST_STATUS);

    switch (wParam)
    {
        case CWINSOCK_DONE_WRITING:
            // lParam = pointer to data that was sent
            // should never happen but make sure the memory is freed just in case
            pDataWritten = (LPVOID)lParam;
            free(pDataWritten);
            break;

        case CWINSOCK_ERROR_WRITING:
            // lParam = pointer to data that generated error sending
            // should never happen but make sure the memory is freed just in case
            pDataWritten = (LPVOID)lParam;
            free(pDataWritten);
            break;

        case CWINSOCK_DONE_READING:
            // lParam = # data chunks in queue
            pDataRead = m_pDataGram->Read(&nLen);
            lstrcpy(pszMessage, "Heartbeat received");
            plb->InsertString(0, pszMessage);
            free(pDataRead);
            m_nHeartbeat = 0;
            ((CStatic *)GetDlgItem(IDC_ICON_STATUS))->SetIcon(m_hGreen);
            break;

        case CWINSOCK_ERROR_READING:
            break;

        default:
            break;
    }

    return 0L;
}

///////////////////////////////////////////////////////////////////////
// CMainView::OnTimer()
//
// Receives timer messages
//
void CMainView::OnTimer(UINT nIDEvent)
{
    ++m_nHeartbeat;

    if (m_nHeartbeat > 1)
        ((CStatic *)GetDlgItem(IDC_ICON_STATUS))->SetIcon(m_hYellow);

    if (m_nHeartbeat > 2)
        ((CStatic *)GetDlgItem(IDC_ICON_STATUS))->SetIcon(m_hRed);

    CFormView::OnTimer(nIDEvent);
}
```

# INISRV 服务器

INISRV 程序使用多文档界面。该程序有两个派生自 `CFormView` 对象的视图。清单 15.3 和 15.4 中所示的 `CMainView` 显示服务器套接字的状态信息，该套接字等待来自客户端的连接请求。清单 15.5 和 15.6 中所示的 `CServerView` 显示已连接套接字的状态信息，该套接字处理客户端发送的数据库命令。

`CMainView` 的 `m_pWinSock` 成员变量控制该程序中 WinSock 子系统的启动和停止。`pStreamSrv` 是一个全局变量，指向等待客户端连接的服务器流套接字对象。

每当客户端请求连接时，用户定义的 `WM_USER_STREAMSRV` 消息就会触发 `CMainView::OnStreamSrv()` 成员函数，该函数接收服务器流套接字对象的状态信息。

`CMainView` 对象的实现如清单 15.4 所示。该对象负责执行 INISRV 应用程序的初始化工作。对象创建后不久就会调用 `CMainView` 的 `OnInitialUpdate()`。此函数负责启动 WinSock 子系统，并创建一个等待客户端连接请求到达的服务器流套接字。

## 多个视图

当客户端请求连接时，`OnStreamSrv()` 成员函数会被触发，同时将 `wParam` 设置为 `CWinSock::READY_TO_ACCEPT_CONNECTION`。随后会启动一个 `CServerView` 类型的新视图来接受客户端连接。通过两个文档模板来支持这一新视图，如清单 15.3 和 15.4 所示。其中一个模板使用 `CMainView`，另一个使用 `CServerView`。

### 清单 15.3。INISRV 的 MAINVIEW.H。

```cpp
// mainview.h : header file
//
//////////////////////////////////////////////////////////////////////
// CMainView form view

#ifndef _AFXEXT_H_
#include <afxext.h>
#endif

#include "cswinsock.h"   // Windows Sockets classes

class CMainView : public CFormView
{
DECLARE_DYNAMIC(CMainView)

private:
    CWinSock * m_pWinSock;          // WinSock sub-system startup/shutdown

protected:
    CMainView();        // protected constructor used by dynamic creation

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
    //}}AFX_MSG
    DECLARE_MESSAGE_MAP()
};

//////////////////////////////////////////////////////////////

#define WM_USER_STREAMSRV (WM_USER + 1)
```

### 清单 15.4。INISRV 的 MAINVIEW.CPP。

```cpp
// mainview.cpp : implementation file
//

#include "stdafx.h"
#include "inisrv.h"
#include "mainfrm.h"
#include "mainview.h"
#include "global.h"
#include "common.h"

#ifdef _DEBUG
#undef THIS_FILE
static char BASED_CODE THIS_FILE[] = __FILE__;
#endif
```

