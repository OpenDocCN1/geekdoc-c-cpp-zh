```
afx_msg LONG OnDatagram(WPARAM wParam, LPARAM lParam);
afx_msg void OnTimer(UINT nIDEvent);
afx_msg void OnClickedButtonRead();
afx_msg void OnClickedButtonWrite();
//}}AFX_MSG
DECLARE_MESSAGE_MAP()
};

//////////////////////////////////////////////////////////////

#define WM_USER_STREAM    (WM_USER + 1)
#define WM_USER_DATAGRAM  (WM_USER + 2)
```

# Listing 15.2. MAINVIEW.CPP FOR INCLNT.

```
// mainview.cpp : implementation file
//

#include "stdafx.h"
#include "inclnt.h"
#include "mainview.h"
#include "servdlg.h"
#include "db.h"
#include "common.h"

#ifdef _DEBUG
#undef THIS_FILE
static char BASED_CODE THIS_FILE[] = __FILE__;
#endif

//////////////////////////////////////////////////////////////
// CMainView

IMPLEMENT_DYNCREATE(CMainView, CFormView)

CMainView::CMainView()
    : CFormView(CMainView::IDD)
{
    //{{AFX_DATA_INIT(CMainView)
    m_stringFile = "";
    m_stringSection = "";
    m_stringValue = "";
    m_stringEntry = "";
    //}}AFX_DATA_INIT

    // initialize class variables

    m_pWinSock = NULL;
    m_pStream = NULL;
    m_pDatagram = NULL;
    m_nHeartbeat = 0;

    // load link status icons
    m_hRed = AfxGetApp()->LoadIcon(IDI_ICON_RED);
```