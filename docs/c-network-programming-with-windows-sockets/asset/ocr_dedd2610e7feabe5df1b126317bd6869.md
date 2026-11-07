```
{
    nStatus = CWINSOCK_WINDOWS_ERROR;
    break;
}

// accept the client connection
pStreamSocket->m_s = accept(m_s, NULL, NULL);
if (pStreamSocket->m_s == INVALID_SOCKET)
{
    m_nLastError = WSAGetLastError();
    nStatus = CWINSOCK_WINDOWS_ERROR;
    pStreamSocket->DestroyWindow();
    break;
}

// start asynchronous event notification
long lEvent;
lEvent = FD_READ | FD_WRITE | FD_CONNECT | FD_CLOSE;
if (WSAAsyncSelect(pStreamSocket->m_s, pStreamSocket->m_hWnd,
    CWINSOCK_EVENT_NOTIFICATION, lEvent) == SOCKET_ERROR)
{
    m_nLastError = WSAGetLastError();
    nStatus = CWINSOCK_SOCKET_ERROR;
    closesocket(pStreamSocket->m_s);
    pStreamSocket->DestroySocket();
    break;
}

break;
}

// if anything failed in this function, set the
// socket variables appropriately
if (nStatus == CWINSOCK_ERROR)
    pStreamSocket->InitVars(FALSE);
else if (nStatus == CWINSOCK_ERROR)
    // notify the parent if the connection was accepted successfully
    pStreamSocket->m_pParentWnd->PostMessage(m_uMsg,
        CWINSOCK_YOU_ARE_CONNECTED);

return nStatus;
}
```

# CStreamSocket::GetPeerName()

The GetPeerName() member function is used to find the Internet address at the other end of a connected stream socket. This is a useful function for servers that may wish to log the names of the clients that use its services.

```
////////////////////////////////////////////////////////////
// CStreamSocket::GetPeerName()
//
// Copies the Internet address of the other end of the socket
// connection into the pointer provided.
//
// Useful for server's to use after an Accept().
//
```