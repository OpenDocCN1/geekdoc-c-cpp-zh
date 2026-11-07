# Listing 15.6. continued

```
```cpp
}
    }
}

void CServerView::DoDataExchange(CDataExchange* pDX)
{
    CFormView::DoDataExchange(pDX);
    //{{AFX_DATA_MAP(CServerView)
    // NOTE: the ClassWizard will add DDX and DDV calls here
    //}}AFX_DATA_MAP
}

void CServerView::OnInitialUpdate()
{
    // start the timer used to trigger the heartbeat writes

    SetTimer(1, HEARTBEAT_DELAY, NULL);

    // get pointer to list box used for status messages

    CListBox *pIb = (CListBox *)GetDlgItem(IDC_LIST_STATUS);

    // accept the client connection
    int nStatus;
    m_pStream = new CStreamSocket(this, WM_USER_STREAM);
    nStatus = g_pStreamSrv->Accept(m_pStream);
    if (nStatus != CWINSOCK_NOERROR)
    {
        pIb->InsertString(0, "Error accepting client connection");
        delete m_pStream;
        m_pStream = NULL;
        return;
    }

    pIb->InsertString(0, "Accepted client connection");

    // get address of client and convert it to be used for sending heartbeat
    if (m_pStream->GetPeerName(&m_sinClient) != CWINSOCK_NOERROR)
    {
        pIb->InsertString(0, "Cannot get name of client");
        m_pStream->DestroySocket();
        delete m_pStream;
        m_pStream = NULL;
        return;
    }
    m_sinClient.sin_port = htons(DATAGRAM_PORT);

    // create the heartbeat datagram
    m_pDatagram = new CDatagramSocket(this, WM_USER_DATAGRAM);
    nStatus = m_pDatagram->CreateSocket();
    if (nStatus != CWINSOCK_NOERROR)
    {
        delete m_pDatagram;
        m_pDatagram = NULL;
        pIb->InsertString(0, "Error creating heartbeat datagram");
```
```