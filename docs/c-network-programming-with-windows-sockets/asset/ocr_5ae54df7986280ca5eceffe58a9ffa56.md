```
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
    afx_msg LONG OnDataGram(WPARAM wParam, LPARAM lParam);
    //}}AFX_MSG
    DECLARE_MESSAGE_MAP()
};

//////////////////////////////////////////////////////////////////////

#define WM_USER_DATAGRAM  (WM_USER + 1)

```

The implementation of the CMainView object is shown in Listing 14.2. This object performs most of the work for the CDESRV application. OnInitialUpdate() is called soon after the object is created. This function is responsible for starting the WinSock subsystem and creating a server datagram socket that waits for data to arrive on port 2000. When data is ready to be received on the socket, the OnDatagram() member function is triggered with wParam set to CWINSDOCK_DONE_READING. Data is read and a write attempt is made to echo the data back to the client. When the write finishes, OnDatagram() is called with wParam set to CWINSDOCK_DONE_WRITING. At this point, the data pointer is freed. When the server application is closed, CMainView’s destructor is called, destroying the datagram socket object and shutting down the WinSock subsystem.

# Listing 14.2. MAINVIEW.CPP FOR CDESRV.

```
// mainview.cpp : Implementation file
//

#include "stdafx.h"
#include "cdsrv.h"
#include "mainview.h"
```