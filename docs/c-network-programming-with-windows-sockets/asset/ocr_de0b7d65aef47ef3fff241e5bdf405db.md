# Listing 8.8. continued

```
```cpp
EndDialog(IDC_BUTTON_ASYNC);
}

void CHostDlg::OnClickedButtonBlocking()
{
    UpdateData(TRUE);
    EndDialog(IDC_BUTTON_BLOCKING);
}
```
```

The dialog box to prompt for which service to look up is implemented as theCServiceDlg class. The source code for this dialog box is in the SERVICE.H and SERVICE.CPP files shown in Listings 8.9 and 8.10, respectively. The code follows a similar format as the CHostDlg class except that there are two data entry fields in the services dialog: service and protocol.

# Listing 8.9. SERVICE.H for DBTST.

```
```cpp
///////////////////////////////////////////////////////////////
// CServiceDlg dialog
///////////////////////////////////////////////////////////////
class CServiceDlg : public CDialog
{
// Construction
public:
    CServiceDlg(CWnd* pParent = NULL);   // standard constructor

// Dialog Data
    //{{AFX_DATA(CServiceDlg)
    enum { IDD = IDD_SERVICE };
    CString m_stringService;
    CString m_stringProtocol;
    //}}AFX_DATA

// Implementation
protected:
    virtual void DoDataExchange(CDataExchange* pDX);   // DDX/DDV support

    // Generated message map functions
    //{{AFX_MSG(CServiceDlg)
    afx_msg void OnClickedButtonAsync();
    afx_msg void OnClickedButtonBlocking();
    //}}AFX_MSG
    DECLARE_MESSAGE_MAP()
};
```
```