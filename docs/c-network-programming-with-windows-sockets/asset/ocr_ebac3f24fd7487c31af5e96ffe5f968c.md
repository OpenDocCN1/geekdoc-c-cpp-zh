```
```cpp
CServerDlg dlg;
if (dlg.DoModal() == IDCANCEL)
    return;

plb->InsertString(0, "Initializing...");

// create the socket
m_s = socket(AF_INET, SOCK_DGRAM, 0);
if (m_s == INVALID_SOCKET)
    plb->InsertString(0, "Datagram echo client could not create socket");
else
{
    // fill out the server's address
    m_addr.sin_family = AF_INET;
    m_addr.sin_port = htons(atoi(dlg.m_stringPort));
    m_addr.sin_addr.s_addr = inet_addr(dlg.m_stringIP);

    // save sending client's IP address
    memcpy(&m_in, &m_addr.sin_addr.s_addr, 4);

    // do the asynchronous select to wait for data
    if (WSAAsyncSelect(m_s, m_hWnd, WM_USER_ASYNC_SELECT,
        FD_READ | FD_WRITE) == SOCKET_ERROR)
        plb->InsertString(0, "Datagram echo client could not do async select");
    else
        SetTimer(1, 5000, NULL);
}

/////////////////////////////////////////////////////////////////
// COnAsyncView::OnAsyncSelect
//
LONG COnAsyncView::OnAsyncSelect(WPARAM wParam, LPARAM lParam)
{
    char pszMessage[100];       // informational message
    static char pBuf[101];      // send/recv buffer
    int nBytesRecv;             // number of bytes received
    int nBytesSent;             // number of bytes sent
    int nError;                 // WinSock error

    // get pointer to list box used for status messages
    CListBox *plb = (CListBox *)GetDlgItem(IDC_LIST_STATUS);

    // check for an error
    if (WSAGETSELECTERROR(lParam) != 0)
    {
        wsprintf(pszMessage, "Datagram echo client async select got error %d",
            WSAGETSELECTERROR(lParam));
        plb->InsertString(0, pszMessage);
        return 0L;
    }

    // what event are we being notified of?
    switch (WSAGETSELECTEVENT(lParam))
    {
    case FD_WRITE:
        plb->InsertString(0, "FD_WRITE");
```
```