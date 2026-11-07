```
```cpp
//
// Read data that has been received by the socket.
//
// This function takes a pointer to an integer that will be filled
// with the length of the data read and an optional pointer
// to an Internet address structure that will be filled with
// the address of the sender of the data.
//
// A pointer to the data is returned on success. The application
// using this object must free this pointer. NULL is returned on failure.
LPVOID CDatagramSocket::Read(LPINT pnLen, LPSOCKADDR_IN psinRemote/* = NULL*/)
{
    LPVOID pData = NULL;

    // check to see if there is data to retrieve
    if (!m_listRead.IsEmpty())
    {
        // remove the stream data from the list
        LPDATAGRAMDATA pDatagramData = (LPDATAGRAMDATA)m_listRead.RemoveHead();
        pData = pDatagramData->pData;
        *pnLen = pDatagramData->nLen;
        if (psinRemote != NULL)
            memcpy(psinRemote, &(pDatagramData->sin), sizeof(SOCKADDR_IN));
        delete pDatagramData;
    }

    return pData;
}
```
```

# CDatagramSocket::OnWinSockEvent()

The OnWinSockEvent() member function handles the asynchronous event notification messages sent by the WinSock subsystem. The WinSock events of interest are FD_READ and FD_WRITE. Interest in these events is registered by the call to WSAAsyncSelect() in the CreateSocket() member function. The Microsoft Foundation Class message map facility is used to map the CWIN SOCK_EVENT_NOTIFICATION message to the OnWinSockEvent() function. The message map looks like the following:

```
```cpp
// message map
BEGIN_MESSAGE_MAP(CDatagramSocket, CWnd)
//{{AFX_MSG_MAP(CDatagramSocket)
//}}AFX_MSG_MAP
ON_MESSAGE(CWINSOCK_EVENT_NOTIFICATION, OnWinSockEvent)
END_MESSAGE_MAP()
```
```

The code for OnWinSockEvent() follows. It simply checks for errors and, if there are none, calls an appropriate message handler.

```
```cpp
/////////////////////////////////////////////////////////////////////
// CDatagramSocket::OnWinSockEvent()
//
// Called when there is an asynchronous event on the socket.
//
```
```