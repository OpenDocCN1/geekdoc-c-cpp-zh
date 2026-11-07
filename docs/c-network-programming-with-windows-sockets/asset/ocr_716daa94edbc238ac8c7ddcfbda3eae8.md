```
```cpp
return;
}

if (m_stringUser.GetLength() >= MAXUSERLEN)
{
    AfxMessageBox("User name is too long");
    return;
}

// format the finger request

if (m_stringUser.Compare("*") == 0)
    lstrcpy(m_szUser, "\n\r");
else
{
    lstrcpy(m_szUser, m_stringUser);
    lstrcat(m_szUser, "\n\r");
}

// initialize the stream socket object

m_pStream = new CStreamSocket(this, WM_USER_STREAM);
if (m_pStream->CreateSocket() != CWINSOCK_ERROR)
{
    AfxMessageBox("Stream creation failed");
    delete m_pStream;
    m_pStream = NULL;
    return;
}

// connect the client to the finger server on port 79
// (the finger server usually listens on TCP port 79 but we
// could replace the hard-coded 79 with the "finger" string
// to do a service lookup)

if (m_pStream->Connect(szHost, 79) != CWINSOCK_ERROR)
{
    AfxMessageBox("Stream connect attempt failed");
    delete m_pStream;
    m_pStream = NULL;
    return;
}

GetDlgItem(IDC_BUTTON_FINGER)->EnableWindow(FALSE);
}

///////////////////////////////////////////////////////////////
// CMainView::DisplayData()
//
void CMainView::DisplayData(LPCSTR pDataRead, int nLen)
{
    char szBuf[2];       // buffer for a one byte string

    // get pointer to list box used for status messages
    CListBox* p1b = (CListBox *)GetDlgItem(IDC_LIST_OUTPUT);

    while (nLen > 0)
    {
```
```