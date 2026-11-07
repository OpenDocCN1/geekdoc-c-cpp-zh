# Listing 14.8. continued

```
plb->InsertString(0, "WinSock initialization failed");
delete m_pWinSock;
m_pWinSock = NULL;
return;
}

// prompt for server information
// (host name or IP address of stream server)

while (1)
{
    CServerDlg dlg;
    dlg.DoModal();
    if (dlg.m_stringServer.GetLength() < sizeof(m_pszServer))
    {
        lstrcpy(m_pszServer, dlg.m_stringServer);
        break;
    }
    else
        AfxMessageBox("Host name or IP address too long");
}

// initialize the stream socket object

m_pStream = new CStreamSocket(this, WM_USER_STREAM);
if (m_pStream->CreateSocket() == CWIN_SOCK_NOERROR)
    plb->InsertString(0, "Stream created");
else
{
    plb->InsertString(0, "Stream creation failed");
    delete m_pStream;
    m_pStream = NULL;
}

// connect the client to the server
if (m_pStream->Connect(m_pszServer, 2000) == CWINSOCK_NOERROR)
    plb->InsertString(0, "Stream connect attempt made");
else
{
    plb->InsertString(0, "Stream connect attempt failed");
    delete m_pStream;
    m_pStream = NULL;
}

BEGIN_MESSAGE_MAP(CMainView, CFormView)
    //{{AFX_MSG_MAP(CMainView)
    ON_MESSAGE(WM_USER_STREAM, OnStream)
    ON_WM_TIMER()
    //}}AFX_MSG_MAP
END_MESSAGE_MAP()

////////////////////////////////////////////////////////////////
// CMainView message handlers

////////////////////////////////////////////////////////////////
```