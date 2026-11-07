
```c
break;
case WSANOTINITIALISED:
    lstrcat(pszError, "WinSock not initialized");
    break;
case WSAHOST_NOT_FOUND:
    lstrcat(pszError, "Host not found");
    break;
case WSATRY_AGAIN:
    lstrcat(pszError, "Non-authoritative host not found");
    break;
case WSANO_RECOVERY:
    lstrcat(pszError, "Non-recoverable error");
    break;
case WSANO_DATA:
    lstrcat(pszError, "Valid name, no data record of requested type");
    break;
default:
    lstrcpy(pszError, "Not a WinSock error");
    break;
}

lstrcat(pszError, "\n");

int n = lstrlen(pszError);
if (pszMessage != NULL)
    n += lstrlen(pszMessage);
if ((pszMessage != NULL) && (n < ERROR_BUF_LEN))
    lstrcat(pszError, pszMessage);

AfxMessageBox(pszError);
```

If the WinSock error is WSANOTINITIALISED, the result of the following code looks like Figure 13.1:

```c
if (...WinSock function fails...)
    CWinSockErrorBox(WSAGetLastError());
```

Supplying the second parameter to CWinSockErrorBox(), as in the following sample, results in that shown in Figure 13.2:

```c
if (...WinSock function fails...)
    CWinSockErrorBox(WSAGetLastError(),
      "Contact your software distributor for technical support");
```

**FIGURE 13.1.**  
*CWinSockErrorBox().*

![](img/5e551abe6e0cb0588043ee757a235ddb_246_0.png)

**FIGURE 13.2.**  
*CWinSockErrorBox()*  
*with second parameter.*

![](img/5e551abe6e0cb0588043ee757a235ddb_247_0.png)

### Implementation Details

The error message strings that are copied into pszError within the large switch statement consume a significant amount of DGROUP space in your application. If you get compiler errors referring to DGROUP space, consider moving these error message strings into the string table of your project’s resource file. You can then use the `LoadString()` function to retrieve the appropriate text.

As discussed in Chapter 9, “Design Goals,” the three classes (`CWinSock`, `CDatagramSocket`, and `CStreamSocket`) and the `CWinSockErrorBox()` function are implemented in the WINSOCK.CPP file. The class and function prototypes are contained in the WINSOCK.H file. The WINSOCK.CPP source file is simply added to each project that requires WinSock functionality.

### Summary

This chapter wraps up the WinSock class library. The remaining chapters of the book examine several sample programs that make use of the class library developed in Chapters 9 through 13.

![](img/5e551abe6e0cb0588043ee757a235ddb_248_0.png)

## Programming with the WinSock Class Library

- 14. Sample Applications Using the Class Library
- 15. Practical Client/Server Database Application
- 16. Finger Application in a Heterogeneous UNIX Environment

![](img/5e551abe6e0cb0588043ee757a235ddb_249_0.png)

## 14 Sample Applications

This chapter presents the reimplementation of two of the samples described in Chapter 8, “Sample Applications.” This time, the WinSock class library, developed in the preceding chapters, is used rather than the raw WinSock API. The two samples are composed of two programs each: a client that sends either datagrams or stream data, and a server that receives them and sends them back to the client.

### Datagram Echo Client and Server

These programs, CDESRV and CDECLNT, demonstrate the use of the `CDatagramSocket` object. The CDESRV server application receives data and sends it back to the client. The CDECLNT client application sends data to the server and receives the echoed reply. These programs are generated using Visual C++’s AppWizard feature.

### Datagram Echo Server CDESRV

As in the DESERV program described in Chapter 8, this sample uses a `CFormView`-derived object named `CMainView` as its primary user interface. The `CMainView` header file is shown in Listing 14.1. The `m_pWinSock` member variable controls the starting and stopping of the WinSock subsystem for this program. The `m_pDatagram` member variable is a pointer to the datagram socket object that receives data from clients. The `OnDatagram()` member function receives status information for the datagram socket object. It’s triggered by the `WM_USER_DATAGRAM` user-defined message.

### Listing 14.1. MAINVIEW.H for CDESRV.

```cpp
// mainview.h : header file
//

//////////////////////////////////////////////////////////////////////
// CMainView form view

#ifndef __AFXEXT_H__
#include <afxtempl.h>
#endif

#include "winsock.h"  // Windows Sockets classes

class CMainView : public CFormView
{
    DECLARE_DYNCREATE(CMainView)

private:
    CWinSock * m_pWinSock;          // WinSock sub-system startup/.shutdown
    CDatagramSocket * m_pDatagram; // Datagram socket to receive from

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
    virtual void DoDataExchange(CDataExchange* pDX);    // DDX/DDV support
    virtual void OnInitialUpdate();
    // Generated message map functions
    //{{AFX_MSG(CMainView)
    afx_msg LONG OnDatagram(WPARAM wParam, LPARAM lParam);
    //}}AFX_MSG
    DECLARE_MESSAGE_MAP()
};

//////////////////////////////////////////////////////////////////////

#define WM_USER_DATAGRAM  (WM_USER + 1)
```

The implementation of the CMainView object is shown in Listing 14.2. This object performs most of the work for the CDESRV application. OnInitialUpdate() is called soon after the object is created. This function is responsible for starting the WinSock subsystem and creating a server datagram socket that waits for data to arrive on port 2000. When data is ready to be received on the socket, the OnDatagram() member function is triggered with wParam set to CWINSOCK_DONE_READING. Data is read and a write attempt is made to echo the data back to the client. When the write finishes, OnDatagram() is called with wParam set to CWINSOCK_DONE_WRITING. At this point, the data pointer is freed. When the server application is closed, CMainView’s destructor is called, destroying the datagram socket object and shutting down the WinSock subsystem.

### Listing 14.2. MAINVIEW.CPP FOR CDESRV.

```cpp
// mainview.cpp : Implementation file
//

#include "stdafx.h"
#include "cdsrv.h"
#include "mainview.h"

#ifdef _DEBUG
#undef THIS_FILE
static char BASED_CODE THIS_FILE[] = __FILE__;
#endif

/////////////////////////////////////////////////////////////////////////////
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
    // get pointer to list box used for status messages

    CListBox *plb = (CListBox *)GetDlgItem(IDC_LIST_STATUS);

    // initialize the WinSock object
    m_pWinSock = new CWinSock;
    if (m_pWinSock->Startup() != WINSOCK_ERROR)
        plb->InsertString(0, "WinSock initialized");
    else
    {
        plb->InsertString(0, "WinSock initialization failed");
        delete m_pWinSock;
        m_pWinSock = NULL;
        return;
    }

    // initialize the datagram socket object
    m_pDatagram = new CDatagramSocket(this, WM_USER_DATAGRAM);
    if (m_pDatagram->CreateSocket(2000) != WINSOCK_ERROR)
        plb->InsertString(0, "Datagram created (port 2000)");
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
//}}AFX_MSG_MAP
END_MESSAGE_MAP()

/////////////////////////////////////////////////////////////////////
// CMainView message handlers

/////////////////////////////////////////////////////////////////////
// CMainView::OnDatagram()
//
// Receives messages from the datagram object.
//
LONG CMainView::OnDatagram(WPARAM wParam, LPARAM lParam)
{
    LPVOID pDataWritten;  // pointer to data that is completely written
    LPVOID pDataRead;     // pointer to data just read
    int nLen;              // length
    SOCKADDR_IN sin;       // Internet address of data's sender
    IN_ADDR in;            // IP address of data's sender
    char pszMessage[1000]; // informational message

    // get pointer to list box used for status messages
    CListBox *pLb = (CListBox *)GetDlgItem(IDC_LIST_STATUS);

    switch (wParam)
    {
        case CWINSOCK_DONE_WRITING:
            // lParam = pointer to data that was sent
            pDataWritten = (LPVOID)lParam;
            wsprintf(pszMessage, "Data sent (%s)", pDataWritten);
```
