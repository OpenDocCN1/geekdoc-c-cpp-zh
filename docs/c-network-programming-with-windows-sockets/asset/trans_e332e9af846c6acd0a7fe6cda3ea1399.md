
### 清单16.1. 续

```cpp
////////////////////////////////////////////////////////////
// CMainView form view

#ifndef __AFXEXT_H__
#include <afxext.h>
#endif

#include "cwinsock.h"    // Windows Sockets classes

class CMainView : public CFormView
{
    DECLARE_DYNCREATE(CMainView)

private:
    void DisplayData(LPCSTR pDataRead, int nLen);
    CWinSock * m_pWinSock;    // WinSock sub-system startup/shutdown
    CStreamSocket * m_pStream;    // Stream socket
#define MAXUSERLEN (100)
    char m_szUser[MAXUSERLEN+1];    // user name to query finger with
#define MAXBUFLEN (200)
    char m_szBuf[MAXBUFLEN+1];    // one line of finger output

protected:
    CMainView();        // protected constructor used by dynamic creation

    // Form Data
public:
    //{{AFX_DATA(CMainView)
    enum { IDD = IDD_DIALOG_MAIN };
    CString m_stringHost;
    CString m_stringUser;
    //}}AFX_DATA

    // Attributes
public:

    // Operations
public:

    // Implementation
protected:
    virtual ~CMainView();
    virtual void DoDataExchange(CDataExchange* pDX);    // DDX/DDV support
    virtual void OnInitialUpdate();
    // Generated message map functions
    //{{AFX_MSG(CMainView)
    afx_msg LONG OnStream(WPARAM wParam, LPARAM lParam);
    afx_msg void OnClickedButtonFinger();
    //}}AFX_MSG
    DECLARE_MESSAGE_MAP()
};

////////////////////////////////////////////////////////////

#define WM_USER_STREAM (WM_USER + 1)
```

### 清单16.2. 续

```cpp
LONG CMainView::OnStream(WPARAM wParam, LPARAM lParam)
{
    LPCSTR pDataRead;       // pointer to data just read
    LPCSTR pOrigDataRead;   // pointer to data just read
    int nLen;               // length

    // get pointer to list box used for status messages

    CListBox *plb = (CListBox *)GetDlgItem(IDC_LIST_OUTPUT);

    // check for invalid stream socket object
    if (m_pStream == NULL)
    {
        plb->AddString("Invalid stream socket object");
        return 0L;
    }

    switch (wParam)
    {
        case CWINSOCK_DONE_WRITING:
            // lParam = pointer to data that was sent

            // lParam points to the static variable m_szUser
            // so it should not be freed

            // clear the list box
            while (plb->GetCount() > 0)
                plb->DeleteString(0);
            break;

        case CWINSOCK_ERROR_WRITING:
            // lParam = pointer to data that generated error sending

            // lParam points to the static variable m_szUser
            // so it should not be freed

            AfxMessageBox("Error sending finger request");
            break;

        case CWINSOCK_DONE_READING:
            // lParam = data chunks in queue
            pDataRead = pOrigDataRead = (LPCSTR)m_pStream->Read(&nLen);
            if (pDataRead != NULL)
            {
                DisplayData(pDataRead, nLen);
                free((LPVOID)pOrigDataRead);
            }
            break;

        case CWINSOCK_ERROR_READING:
            break;

        case CWINSOCK_YOU_ARE_CONNECTED:
            if (m_pStream->Write(lstrlen(m_szUser), m_szUser) !=
                CWINSOCK_NOERROR)
            {
                AfxMessageBox("Error sending finger request");
                m_pStream->DestroySocket();
            }
            delete m_pStream;
            m_pStream = NULL;
            GetDlgItem(IDC_BUTTON_FINGER)->EnableWindow(TRUE);
            break;

        case CWINSOCK_LOST_CONNECTION:
            // server closed the connection
            m_pStream->DestroySocket();
            delete m_pStream;
            m_pStream = NULL;
            GetDlgItem(IDC_BUTTON_FINGER)->EnableWindow(TRUE);
            break;

        default:
            break;
    }

    return 0L;
}

//////////////////////////////////////////////////////////////
// CMainView::OnClickedButtonFinger()
//
// Called when the Finger button is pressed.
// Creates a socket, and connects to a finger server, and send the request.
//
void CMainView::OnClickedButtonFinger()
{
    // initialize the buffer used to display the results
    m_szBuf[0] = '\0';

    // make sure the user entered something for the host

    UpdateData(TRUE);

    if (m_stringHost.GetLength() == 0)
    {
        AfxMessageBox("You must enter a host name or IP address");
        return;
    }

#define MAXHOSTLEN (100)
    char szHost[MAXHOSTLEN];
    if (m_stringHost.GetLength() >= MAXHOSTLEN)
    {
        AfxMessageBox("Host name or IP address is too long");
        return;
    }
    lstrcpy(szHost, m_stringHost);

    // make sure the user entered something for the user

    if (m_stringUser.GetLength() == 0)
    {
        AfxMessageBox("You must enter a user name or *");
        return;
    }

    if (m_stringUser.GetLength() >= MAXUSERLEN)
    {
        AfxMessageBox("User name is too long");
        return;
    }

    // format the finger request

    if (m_stringUser.Compare("*") == 0)
        lstrcpy(m_szUser, "\r\n");
    else
    {
        lstrcpy(m_szUser, m_stringUser);
        lstrcat(m_szUser, "\r\n");
    }

    // initialize the stream socket object

    m_pStream = new CStreamSocket(this, WM_USER_STREAM);
    if (m_pStream->CreateSocket() != CWINSOCK_ERROR)
    {
        AfxMessageBox("Stream creation failed");
        delete m_pStream;
        m_pStream = NULL;
        return;
    }

    // connect the client to the finger server on port 79
    // (the finger server usually listens on TCP port 79 but we
    // could replace the hard-coded 79 with the "finger" string
    // to do a service lookup)

    if (m_pStream->Connect(szHost, 79) != CWINSOCK_ERROR)
    {
        AfxMessageBox("Stream connect attempt failed");
        delete m_pStream;
        m_pStream = NULL;
        return;
    }

    GetDlgItem(IDC_BUTTON_FINGER)->EnableWindow(FALSE);
}

///////////////////////////////////////////////////////////////
// CMainView::DisplayData()
//
void CMainView::DisplayData(LPCSTR pDataRead, int nLen)
{
    char szBuf[2];       // buffer for a one byte string

    // get pointer to list box used for status messages
    CListBox* plb = (CListBox *)GetDlgItem(IDC_LIST_OUTPUT);

    while (nLen > 0)
    {
        // ignore linefeed
        if (*pDataRead != '\r')
        {
            // don't add carriage return to string
            if (*pDataRead != '\n')
            {
                szBuf[0] = *pDataRead;
                szBuf[1] = '\0';
                lstrcat(m_szBuf, szBuf);
            }
            if ((lstrlen(m_szBuf) >= MAXBUFLEN) || (*pDataRead == '\n'))
            {
                // check to see if the buffer has data in it
                if (m_szBuf[0] != '\0')
                {
                    plb->AddString(m_szBuf);
                    m_szBuf[0] = '\0';
                }
                // check to see if we should insert a blank line
                else if (*pDataRead == '\n')
                    plb->AddString(" ");
            }
        }
        --nLen;
        ++pDataRead;
    }
}
```

## 运行 Finger 客户端

图16.1展示了Finger客户端运行时的情形。用户只需输入运行Finger服务器（或守护进程）的计算机的主机名或IP地址。如果用户希望获取主机上所有用户的信息，则将用户字段保留为星号（*）；否则，输入特定用户的名称。只需按下Finger按钮即可开始请求。

**图16.1.**  
*Finger客户端。*

![](img/5e551abe6e0cb0588043ee757a235ddb_310_0.png)

## 小结

本章给出了使用第III部分开发的WinSock类库的最后一个示例。它展示了将Windows程序与运行相同或不同操作系统的计算机对接是多么容易。借助业界公认的协议，有些程序变得相当简单。

![](img/5e551abe6e0cb0588043ee757a235ddb_311_0.png)

## WINSOCK.H

### 文件清单

```c
/* WINSOCK.H—definitions to be used with the WINSOCK.DLL
 *
 * This header file corresponds to version 1.1 of the Windows Sockets specification.
 *
 * This file includes parts which are Copyright (c) 1982-1986 Regents
 * of the University of California. All rights reserved. The
 * Berkeley Software License Agreement specifies the terms and
 * conditions for redistribution.
 *
 * Change log:
 *
 * Fri Apr 23 16:31:01 1993  Mark Towfiq (towfiq@Microdyne.COM)
 *   New version from David Treadwell which adds extern "C" around
 *   __WSAFDIsSet() and removes 'const' from buf param of
 *   WSAAsyncGetHostByAddr(). Added change log.
 *
 * Sat May 15 10:55:00 1993 David Treadwell (davidtr@microsoft.com)
 *   Fix the IN_CLASSC macro to account for class-D multicasts.
 *   Add AF_INX == AF_NS.
 */

#ifndef _WINSOCKAPI_
#define _WINSOCKAPI_

/*
 * Pull in WINDOWS.H if necessary
 */
#ifndef _INC_WINDOWS
#include <windows.h>
#endif /* _INC_WINDOWS */

/*
 * Basic system type definitions, taken from the BSD file sys/types.h.
 */
typedef unsigned char   u_char;
typedef unsigned short  u_short;
typedef unsigned int    u_int;
typedef unsigned long   u_long;

/*
 * The new type to be used in all
 * instances which refer to sockets.
 */
typedef u_int           SOCKET;

/*
 * Select uses arrays of SOCKETs.  These macros manipulate such
 * arrays.  FD_SETSIZE may be defined by the user before including
 * this file, but the default here should be >= 64.
 *
 * CAVEAT IMPLEMENTOR and USER: THESE MACROS AND TYPES MUST BE
 * INCLUDED IN WINSOCK.H EXACTLY AS SHOWN HERE.
 */
#ifndef FD_SETSIZE
#define FD_SETSIZE      64
#endif /* FD_SETSIZE */
```
