The implementation of the CMainView object is shown in Listing 8.15. This object performs most of the work for the DESERV application. CMainView::OnInitialUpdate() is called soon after the object is created. This function is responsible for creating a socket, binding it to a name (with the port assigned by WinSock), and waiting for data to arrive. When data is ready to be received or data can be sent, the CMainView::OnAsyncSelect() member function is called due to the message mapping of the user-defined message WM_USER_ASYNC_SELECT.

# Listing 8.15. MAINVIEW.CPP for DESERV.

```
```cpp
// mainview.cpp : implementation file
//

#include "stdafx.h"
#include "deserv.h"
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
	m_s = INVALID_SOCKET; // initialize socket to invalid handle

	//{{AFX_DATA_INIT(CMainView)
		// NOTE: the ClassWizard will add member initialization here
	//}}AFX_DATA_INIT
}

CMainView::~CMainView()
{
	// if the socket was opened successfully, close it

	if (m_s != INVALID_SOCKET)
	{
		closesocket(m_s);
		m_s = INVALID_SOCKET;
	}
}

void CMainView::DoDataExchange(CDataExchange* pDX)
{
	CFormView::DoDataExchange(pDX);
	//{{AFX_DATA_MAP(CMainView)
		// NOTE: the ClassWizard will add DDX and DDV calls here
	//}}AFX_DATA_MAP
}
```
```