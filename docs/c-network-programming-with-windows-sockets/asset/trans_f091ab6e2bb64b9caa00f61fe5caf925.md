
## 清单 8.10. 用于 DBTST 的 SERVICE.CPP。

```cpp
// service.cpp : implementation file
//

#include "stdafx.h"
#include "dbtst.h"
#include "serviceDlg.h"

#ifdef _DEBUG
#undef THIS_FILE
static char BASED_CODE THIS_FILE[] = __FILE__;
#endif

//////////////////////////////////////////////////////////////////////
// CServiceDlg

CServiceDlg::CServiceDlg(CWnd* pParent /*=NULL*/)
    : CDialog(CServiceDlg::IDD, pParent)
{
    //{{AFX_DATA_INIT(CServiceDlg)
    m_stringService = "";
    m_stringProtocol = "";
    //}}AFX_DATA_INIT
}

void CServiceDlg::DoDataExchange(CDataExchange* pDX)
{
    CDialog::DoDataExchange(pDX);
    //{{AFX_DATA_MAP(CServiceDlg)
    DDX_Text(pDX, IDC_EDIT_SERVICE, m_stringService);
    DDX_Text(pDX, IDC_EDIT_PROTOCOL, m_stringProtocol);
    //}}AFX_DATA_MAP
}

BEGIN_MESSAGE_MAP(CServiceDlg, CDialog)
    //{{AFX_MSG_MAP(CServiceDlg)
    ON_BN_CLICKED(IDC_BUTTON_ASYNC, OnClickedButtonAsync)
    ON_BN_CLICKED(IDC_BUTTON_BLOCKING, OnClickedButtonBlocking)
    //}}AFX_MSG_MAP
END_MESSAGE_MAP()

//////////////////////////////////////////////////////////////////////
// CServiceDlg message handlers

void CServiceDlg::OnClickedButtonAsync()
{
    UpdateData(TRUE);
    EndDialog(IDC_BUTTON_ASYNC);
}

void CServiceDlg::OnClickedButtonBlocking()
{
    UpdateData(TRUE);
    EndDialog(IDC_BUTTON_BLOCKING);
}
```

在这个示例程序中，完成大部分工作的类是 CMainWindow，它派生自 MFC 类 CFrameWnd。正是这个类实际创建窗口、提供菜单，并调用 WinSock 数据库函数。其头文件如清单 8.11 所示。若干私有成员变量用于支持数据库查找。

## 清单 8.11. 用于 DBTST 的 MAINWND.H。

```cpp
#ifndef __MAINWND_H_
#define __MAINWND_H_

#define USER_INPUT_BUF_LEN    (100)

//////////////////////////////////////////////////////////////////////
// CMainWindow class declaration
//
class CMainWindow : public CFrameWnd
{
private:
    // variables to support host lookup
    HANDLE m_hAsyncHost;                        // async request handle
    char m_achHostEnt[MAXGETHOSTSTRUCT];        // hostent buffer for async call
    char m_lpszHost[USER_INPUT_BUF_LEN];        // host name or IP address
    PHOSTENT m_pHostEnt;                        // pointer to host entry structure
    IN_ADDR m_in;                               // Internet address structure
    u_long m_ulIPAddress;                       // Internet address

    // variables to support service lookup
    HANDLE m_hAsyncService;                     // async request handle
    char m_achServEnt[MAXGETHOSTSTRUCT];        // servent buffer for async call
    char m_lpszService[USER_INPUT_BUF_LEN];     // service name or port number
    char m_lpszProtocol[USER_INPUT_BUF_LEN];    // transport protocol
    PSERVENT m_pServEnt;                        // pointer to service entry structure
    short m_nPort;                              // port number

public:
    CMainWindow();

    //{{AFX_MSG(CMainWindow)
    afx_msg void OnHost();
    afx_msg LONG OnAsyncHost(WPARAM wParam, LPARAM lParam);
    afx_msg void OnCancelHost();
    afx_msg void OnService();
    afx_msg LONG OnAsyncService(WPARAM wParam, LPARAM lParam);
    afx_msg void OnCancelService();
    //}}AFX_MSG
    DECLARE_MESSAGE_MAP()
};

//////////////////////////////////////////////////////////////////////
// User defined messages used in CMainWindow's message map
//
#define WM_USER_ASYNC_HOST_LOOKUP       (WM_USER + 1)
#define WM_USER_ASYNC_SERVICE_LOOKUP    (WM_USER + 2)

#endif // __MAINWND_H_
```

## 清单 8.12. 续

```cpp
//
// Create the window with the appropriate style, size, menu, etc.
//
CMainWindow::CMainWindow()
{
    LoadAccelTable("MainAccelTable");

    Create(NULL, "WinSock Database Test Application",
        WS_OVERLAPPEDWINDOW, rectDefault, NULL, "MainMenu");

    // initialize the asynchronous request handles so we
    // know if there is any outstanding request
    m_hAsyncHost = m_hAsyncService = 0;
}

////////////////////////////////////////////////////////////////
// CMainWindow::OnHost
//
// Called when the Test | Host Lookup menu item is selected.
//
void CMainWindow::OnHost()
{
    char lpszMessage[100];    // informational message

    // prompt the user for host information
    CHostDlg dlg;
    int nStatus = dlg.DoModal();
    if (nStatus != IDCANCEL)
    {
        // copy the host information the user entered into a member variable
        if (dlg.m_strHost.GetLength() < USER_INPUT_BUF_LEN)
            lstrcpy(m_lpszHost, dlg.m_strHost);
        else
        {
            MessageBox("Host name or IP address was too long", "Host Lookup");
            return;
        }

        // see if the user entered a dotted-decimal IP address
        m_ulIPAddress = inet_addr(m_lpszHost);

        if (nStatus == IDC_BUTTON_ASYNC)
        {
            // do an asynchronous host lookup

            if (m_hAsyncHost != 0)
                MessageBox("Asynchronous host lookup already in progress", "Host Lookup");
            else
            {
                if (m_ulIPAddress == INADDR_NONE)
                    m_hAsyncHost = WSAAsyncGetHostByName(m_hWnd, WM_USER_ASYNC_HOST_LOOKUP,
                        m_lpszHost, m_achHostEnt, MAXGETHOSTSTRUCT);
                else
                    m_hAsyncHost = WSAAsyncGetHostByAddr(m_hWnd, WM_USER_ASYNC_HOST_LOOKUP,
                        (char *)&m_ulIPAddress, 4, PF_INET, m_achHostEnt, MAXGETHOSTSTRUCT);

                if (m_hAsyncHost == 0)
                {
                    wsprintf(lpszMessage, "Host lookup failed (WinSock error %d)",
                        WSAGetLastError());

                    MessageBox(lpszMessage, "Host Lookup");
                }
            }
        }
        else
        {
            // do a blocking host lookup

            if (m_ulIPAddress == INADDR_NONE)
                m_pHostEnt = gethostbyname(m_lpszHost);
            else
                m_pHostEnt = gethostbyaddr((char *)&m_ulIPAddress, 4, PF_INET);

            if (m_pHostEnt == NULL)
                wsprintf(lpszMessage, "Host lookup failed (WinSock error %d)",
                    WSAGetLastError());
            else
            {
                // copy the four byte IP address into an Internet address structure
                memcpy(&m_in, m_pHostEnt->h_addr, 4);

                // format the results, converting the IP address into a string
                wsprintf(lpszMessage, "Host %s has IP address %s",
                    m_pHostEnt->h_name, inet_ntoa(m_in));
            }

            MessageBox(lpszMessage, "Host Lookup");
        }
    }
}

/////////////////////////////////////////////////////////////////////////////
// CMainWindow::OnAsyncHost
//
// Called when the asynchronous lookup is done.
//
LONG CMainWindow::OnAsyncHost(WPARAM wParam, LPARAM lParam)
{
    char lpszMessage[100];  // informational message

    // check for an error
    if (WSAGETASYNCERROR(lParam) != 0)
        wsprintf(lpszMessage,
            "Host lookup failed (WinSock error %d)",
            WSAGETASYNCERROR(lParam));
    else
    {
        // assign a hostent host entry pointer to the buffer
        m_pHostEnt = (PHOSTENT)m_achHostEnt;

        // copy the four byte IP address into an Internet address structure
        memcpy(&m_in, m_pHostEnt->h_addr, 4);

        // format the results, converting the IP address into a string
        wsprintf(lpszMessage, "Host %s has IP address %s",
            m_pHostEnt->h_name, inet_ntoa(m_in));
    }

    m_hAsyncHost = 0;
    MessageBox(lpszMessage, "Host Lookup");

    return 0L;
}

///////////////////////////////////////////////////////////////
// CMainWindow::OnCancelHost
//
// Called when the Test | Cancel Host Lookup menu item is selected.
//
void CMainWindow::OnCancelHost()
{
    char lpszMessage[100];   // informational message

    // see if there is an outstanding asynchronous request
    if (m_hAsyncHost == 0)
        lstrcpy(lpszMessage, "No asynchronous host lookup in progress");
    else
    {
        // cancel the asynchronous request

        if (WSACancelAsyncRequest(m_hAsyncHost) != 0)
            wsprintf(lpszMessage, "Cancel asynchronous host lookup failed (WinSock error %d)",
                WSAGetLastError());
        else
            lstrcpy(lpszMessage, "Asynchronous host lookup canceled");

        m_hAsyncHost = 0;
    }

    MessageBox(lpszMessage, "Host Lookup");
}

///////////////////////////////////////////////////////////////
// CMainWindow::OnService
//
// Called when the Test | Service Lookup menu item is selected.
//
void CMainWindow::OnService()
{
    char lpszMessage[100];   // informational message

    // prompt the user for service information
    CServiceDlg dlg;
    int nStatus = dlg.DoModal();
    if (nStatus == IDCANCEL)
        return;
```

