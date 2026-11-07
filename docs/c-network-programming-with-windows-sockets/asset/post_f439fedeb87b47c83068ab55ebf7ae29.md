
## CStreamSocket::HandleRead()

The HandleRead() member function handles the asynchronous FD_READ event notification messages sent by the WinSock subsystem. This function is called when WinSock thinks a read from the socket will succeed. The first portion of this function allocates memory for the data and the data’s length. A recv() is then attempted. If the receive is successful, the data is added to the read queue. If everything goes OK, the m_uMsg message is posted to the application window that owns this stream socket object, with wParam set to CWIN_SOCK_DONE_READING and lParam set to the number of data buffers waiting to be read. When the application receives this message, it should call the Read() member function. If there is an error in receiving the data, wParam is set to CWIN_SOCK_ERROR_READING. If data is received and the CWIN_SOCK_DONE_READING message is sent to the application, a 1 is returned by HandleRead(), otherwise, 0 is returned. This differentiation is used by OnWinSockEvent()’s FD_CLOSE handler to let it know when all data received on the socket is completely processed.

```cpp
////////////////////////////////////////////////////////////
// CStreamSocket::HandleRead()
//
// Called when there is an asynchronous read event on the socket.
//
// If the read was successful, the data and its length are stored
// in the read queue.  Upon a successful read, the application
// window using this object is then notified with the m_uMsg message
// (wParam set to CWIN_SOCK_DONE_READING; lParam set to the number of
// data chunks in the read queue).  At this point, the application
// should call Read().  If the read fails for some reason, the m_uMsg
// is sent with wParam set to CWIN_SOCK_ERROR_READING.
//
LONG CStreamSocket::HandleRead(WPARAM wParam, LPARAM lParam)
{
    while (1)
    {
        // allocate memory for incoming data
        LPVOID pData = malloc(READ_BUF_LEN);
        LPSTREAMDATA pStreamData = new STREAMDATA;
        if ((pData == NULL) || (pStreamData == NULL))
        {
            // free anything that was allocated
            if (pData != NULL)
                free(pData);
            pData = NULL;
            if (pStreamData != NULL)
                delete pStreamData;
            pStreamData = NULL;

            // tell the parent that a possible data read failed
            m_pParentWnd->PostMessage(m_uMsg, CWIN_SOCK_ERROR_READING);

            // fake the event to try again
            PostMessage(CWIN_SOCK_EVENT_NOTIFICATION, m_s,
                WSAMAKESELECTREPLY(FD_READ, 0));
m_pParentWnd->PostMessage(m_uMsg, CWIN_SOCK_DONE_READING,
    (LPARAM)m_listRead.GetCount());

// 1 is returned if there is data so CStreamSocket::OnWinSockEvent()'s
// FD_CLOSE handler will know when the socket can really be closed
return 1L;

break;
}

return 0L;
}
```

## CStreamSocket::HandleWrite()

The HandleWrite() member function handles the asynchronous FD_WRITE event notification messages sent by the WinSock subsystem. This function is called when WinSock thinks a write out of the socket will succeed. The first portion of this socket checks to see whether there is any data waiting to be sent from the write queue. This queue is added to by the application calling the Write() member function. If there is data in the write queue, a send() is attempted. If the send() would block, the data is retained to have another send attempted at a later time. If the send() fails with an error other than WSAEWOULDBLOCK, the data is removed from the write queue and the m_uMsg message is sent to the application window with wParam set to CWIN_SOCK_ERROR_WRITING and lParam the pointer to the data that was unsuccessfully sent. If the send() succeeds but not all of the bytes are sent, a pointer into the buffer is retained until the next time HandleWrite() is executed. When the entire buffer is successfully sent, wParam is set to CWIN_SOCK_DONE_WRITING and lParam is the data pointer. When the application receives this message notification, it's safe to free or reuse the storage space pointed to by the pointer returned in lParam.

```cpp
////////////////////////////////////////////////////////////////
// CStreamSocket::HandleWrite()
//
// Called when there is an asynchronous write event on the socket.
//
// If there is data in the write queue waiting to be sent,
// a WinSock send is attempted. If the send is successful,
// a m_uMsg message is sent to the application window with
// wParam set to CWIN_SOCK_DONE_WRITING and lParam set to the
// address of the data that was sent. On send failure,
// wParam is set to CWIN_SOCK_ERROR_WRITING and lParam set to
// the address of the data which couldn't be sent. In either
// case, the application may free the pointer pointing to
// the data. In no case should the buffer be considered to
// be empty: the entire amount of data to not be sent in one call to send().
// In this case, an attempt is made to send the remaining portion
// of that block of data the next time HandleWrite() is invoked.
//
//
LONG CStreamSocket::HandleWrite(WPARAM wParam, LPARAM lParam)
{
    LPSTREAMDATA pStreamData;             // pointer to stream data structure
    LPVOID pData;                          // pointer to buffer to send
    int nLen;                              // total length of buffer to send
    static LPVOID pDataRemaining = NULL;   // pointer into buffer to send
    static int nLenRemaining = 0;          // number of bytes left to send

    while (1)
    {
        // check to see if there is any data to send
        if (m_listWrite.IsEmpty())
            break;

        // if we are not in the middle of another buffer send,
        // get data and data length from the write queue
        pStreamData = (LPSTREAMDATA)m_listWrite.GetHead(); // not RemoveHead()
        pData = pStreamData->pData;
        nLen = pStreamData->nLen;
        if (pDataRemaining == NULL)
        {
            pDataRemaining = pData;
            nLenRemaining = nLen;
        }

        // send the data
        BOOL bRemove = FALSE;      // remove data from queue?
        int nBytesSent = send(m_s, (LPCSTR)pDataRemaining, nLenRemaining, 0);
        if (nBytesSent == SOCKET_ERROR)
        {
            // if the error is just that the send would block,
            // don't do anything; we'll get another FD_WRITE soon
            m_nLastError = WSAGetLastError();
            if (m_nLastError == WSAEWOULDBLOCK)
                m_nLastError = 0;
            else
            {
                bRemove = TRUE;
                m_pParentWnd->PostMessage(m_uMsg, WSA...);
            }
        }
        else
        {
            // if data was sent, we must still check to see
            // if all the bytes were sent
            if (nBytesSent == nLenRemaining)
            {
                bRemove = TRUE;
                m_pParentWnd->PostMessage(m_uMsg, C...);
            }
            else
            {
                // the complete buffer was not sent so adjust
                // the values accordingly
                pDataRemaining = (LPVOID)((LPCSTR)pDataRemaining + nBytesSent);
                nLenRemaining = nLenRemaining - nBytesSent;
            }
        }
    }
}
```

```cpp
// remove any data in the read queue
while (!m_listRead.IsEmpty())
{
    LPSTREAMDATA pStreamData = (LPSTREAMDATA)m_listRead.RemoveHead();
    free(pStreamData->pData);
    delete pStreamData;
}

// close the socket and initialize variables
closesocket(m_s);
InitVars();

// destroy the hidden window
DestroyWindow();
}

return nStatus;
}
```

## CStreamSocket::LastError()

The LastError() member function is implemented as an in-line function. It simply returns the m_nLastError value that contains the last WinSock error message generated by the CStreamSocket object. This function should be called whenever a CStreamSocket member function returns WINSOCK_ERROR.

## Application Responsibility

The goal of this object is to enable the rapid development of a networked application using stream sockets. The public interface to the CStreamSocket object consists of the following functions: CreateSocket(), DestroySocket(), Read(), Write(), Connect(), Accept(), GetPeerName(), and LastError().

The application must provide a certain level of support for the stream object. The application must provide a message handler to receive messages sent from the object. Also, the stream object’s constructor requires a pointer to the application window object and a message. A sample call to a stream object constructor looks like the following:

```cpp
ps = new CStreamSocket(this, WM_USER + 1);
```

An entry must be made in the message map to associate the WM_USER + 1 message to an application member function.

```cpp
BEGIN_MESSAGE_MAP(CMainFrame, CFrameWnd)
    //{{AFX_MSG_MAP(CMainFrame)
    //}}AFX_MSG_MAP
    ON_MESSAGE(WM_USER + 1, OnWinSockEvent)
END_MESSAGE_MAP()
```
