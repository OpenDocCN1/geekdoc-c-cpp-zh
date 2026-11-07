# Listing 8.10. SERVICE.CPP for DBTST.

```
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