```
```cpp
// assign the address family
m_sinLocal.sin_family = AF_INET;

// assign the service port (may have to do a database lookup
// if a service port number was not specified)
m_sinLocal.sin_port = htons(atoi(pszLocalService));
if (m_sinLocal.sin_port == 0)
{
    LPSERVENT pSent = getservbyname(pszLocalService, "udp");
    if (pSent == NULL)
    {
        m_nLastError = WSASocketError();
        m_nStatus = C WINSOCK_ERROR;
        closesocket(m_s);
        DestroyWindow();
        break;
    }
    m_sinLocal.sin_port = pSent->s_port;
}

// assign the IP address
m_sinLocal.sin_addr.s_addr = htonl(INADDR_ANY);

// bind the server socket to the name containing the port
if (bind(m_s, (LPSOCKADDR)&m_sinLocal, sizeof(m_sinLocal)) == SOCKET_ERROR)
{
    m_nLastError = WSASocketError();
    m_nStatus = C WINSOCK_ERROR;
    closesocket(m_s);
    DestroyWindow();
    break;
}

// start asynchronous event notification
long lEvent = FD_READ | FD_WRITE;
if (WSAAsyncSelect(m_s, m_hWnd, WINSOCK_EVENT_NOTIFICATION, lEvent) ==
SOCKET_ERROR)
{
    m_nLastError = WSASocketError();
    m_nStatus = C WINSOCK_ERROR;
    closesocket(m_s);
    DestroyWindow();
    break;
}

break;
}

// if anything failed in this function, set the
// socket variable appropriately
if (nStatus != C WINSOCK_ERROR)
    InitVars(FALSE);

return nStatus;
}
```
```