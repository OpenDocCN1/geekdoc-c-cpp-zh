```
else
{
    // try to make the connection
    // if it doesn't succeed it may still be ok as long
    // as the error was that the connection would block
    if (connect(m_s, (LPSOCKADDR)&m_addr, sizeof(m_addr)) == SOCKET_ERROR)
    {
        int nError = WSAGetLastError();
        if (nError != WSAEWOULDBLOCK)
            plb->InsertString(0, "Stream echo client could not connect");
        SetTimer(1, 5000, NULL);
    }
}

///////////////////////////////////////////////////////////////
// CMainView::OnAsyncSelect()
//
LONG CMainView::OnAsyncSelect(WPARAM wParam, LPARAM lParam)
{
    char pszMessage[100];        // informational message
    static char pBuf[101];       // send/recv buffer
    int nBytesRecv;              // number of bytes received
    int nBytesSent;              // number of bytes sent
    int nError;                  // WinSock error

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
        case FD_CONNECT:
            // the connection has been completed

            plb->InsertString(0, "Stream echo client connected");

            if (WSAAsyncSelect(m_s, m_hWnd, WM_USER_ASYNC_SELECT,
                FD_READ | FD_WRITE | FD_CLOSE) == SOCKET_ERROR)
                plb->InsertString(0, "Stream echo client could not do async select");
            break;

        case FD_CLOSE:
            // close the socket

            closesocket(m_s);
            m_s = INVALID_SOCKET;
```