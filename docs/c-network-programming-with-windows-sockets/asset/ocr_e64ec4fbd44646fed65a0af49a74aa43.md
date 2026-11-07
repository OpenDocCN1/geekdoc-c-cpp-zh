# Listing 14.8. continued

```
```cpp
    return 0L;
}

void CMainView::OnTimer(UINT nIDEvent)
{
    static int nSendCount = 1;  // used to generate unique message
    char pszMessage[1000];      // informational message

    // make sure we are not sending out of a bad stream socket
    if (m_pStream == NULL)
        return;

    // get pointer to list box used for status messages
    CListBox *plb = (CListBox *)GetDlgItem(IDC_LIST_STATUS);

    // send the buffer unless the previous send hasn't completed yet
    if ((*m_pszBuf) == '\0')
    {
        wsprintf(m_pszBuf, "Hello %d", nSendCount);
        ++nSendCount;
        // be sure to send terminating NULL character
        if (m_pStream->Write(lstrlen(m_pszBuf) + 1, m_pszBuf) != WINSOCK_NOERROR)
        {
            (*m_pszBuf) = '\0';
            wsprintf(pszMessage, "Error sending data (%s)", m_pszBuf);
            plb->InsertString(0, pszMessage);
        }
    }

    CFormView::OnTimer(nIDEvent);
}
```
```

# Running the Stream Echo Server and Client

Following is a sample sequence of events that occur when the stream echo client and server are run:

+   1. Run CSESRV.
+   2. Run CSECLNT on the same or a different computer. It prompts for the host name or IP address CSESRV is using. A connection to the server is attempted.
+   3. CSESRV’s `CMainView::OnStreamSrv()` is called with the `WINSOCK_READY_TO_ACCEPT_CONNECTION` event and, if the `m_pStream` socket is not yet connected to a client, a connection attempt is made.
+   4. When the server’s connection accept succeeds, `OnStream()` is called with `wParam` set to `WINSOCK_YOU_ARE_CONNECTED`.
+   5. CDECLNT’s `CMainView::OnStream()` is also called with the `WINSOCK_YOU_ARE_CONNECTED` event.