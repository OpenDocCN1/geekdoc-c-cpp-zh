```
```cpp
// Implementation

//{{AFX_MSG(CWSinfoApp)
afx_msg void OnAppAbout();
}//}}AFX_MSG
DECLARE_MESSAGE_MAP()
};
```
```

Edit the WSINFO.CPP file to modify the InitInstance() and ExitInstance() CWSinfoApp class member functions. In InitInstance(), WSASStartUp() is called. When modifications to InitInstance() are completed, it looks like the following:

```
```cpp
BOOL CWSinfoApp::InitInstance()
{
    // WinSock startup
    // If WSASStartup() is successful, we still
    // need to check the version numbers.

    WORD wVersionRequired = MAKEWORD(1, 1);  // WinSock 1.1 required
    m_bWinSockOK = FALSE;                    // not OK
    m_nWinSockError = 0;                     // no WinSock error
    if (WSAStartup(wVersionRequired, &m_wsData) == 0)
    {
        if (wVersionRequired == m_wsData.wVersion)
            m_bWinSockOK = TRUE;
        else
            WSACleanup();
    }
    else
        m_nWinSockError = WSAGetLastError();

    // Standard initialization
    // If you are not using these features and wish to reduce the size
    // of your final executable, you should remove from the following
    // the specific initialization routines you do not need.

    SetDialogBkColor();          // set dialog background color to gray
    LoadStdProfileSettings();    // Load standard INI file options (including MRU)

    // Register the application's document templates.  Document templates
    // serve as the connection between documents, frame windows and views.

    AddDocTemplate(new CSingleDocTemplate(IDR_MAINFRAME,
                RUNTIME_CLASS(CWSinfoDoc),
                RUNTIME_CLASS(CMainFrame),    // main SDI frame window
                RUNTIME_CLASS(CWSinfoView)));

    // create a new (empty) document
    OnFileNew();

    if (m_lpCmdLine[0] != '\0')
    {
        // TODO: add command line processing here
    }

    return TRUE;
}
```
```