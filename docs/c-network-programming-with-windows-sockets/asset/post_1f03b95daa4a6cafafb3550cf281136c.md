
## Finding a Service Name When You Know Its Port Number

The getservbyport() function gets service information corresponding to a specific port and protocol. Its function prototype looks like the following:

```c
struct servent FAR * PASCAL FAR getservbyport(int port,
    const char FAR * proto);
```

port is the service port, in network byte order. proto is a pointer to a protocol name; it is "tcp", "udp", or NULL. If proto is NULL, the first matching service is returned. The getservbyport() function returns a pointer to a servent structure on success and NULL on failure. On a return value of NULL, you can call WSAGetLastError() to determine the specifics of the problem. Possible error values include the following: WSANOTINITIALIZED if WSAStartup() wasn’t called successfully; WSAENETDOWN if the network subsystem is failing; WSANO_RECOVERY if there was an unrecoverable error; WSANO_DATA if the port number is valid but no appropriate data could be found; WSAEINPROGRESS if a blocking WinSock operation is currently in progress; or WSAEINTR if the blocking call was canceled by WSACancelBlockingCall().

This code fragment searches for the service corresponding to port 37 on a UDP transport connection:

```c
PSERVENT pservent;             // pointer to service entry structure
char lpszMessage[100];         // informational message
char lpszPort[6];              // port number string

// get the service entry structure for the port 37 service using UDP
if ((pservent = getservbyport(htons(37), "udp")) == NULL)
    wsprintf(lpszMessage, "getservbyport() generated error %d",
        WSAGetLastError());
else
{
    // format the results
    wsprintf(lpszMessage, "Service %s using protocol %s has port ",
        pservent->s_name, pservent->s_proto);
    wsprintf(lpszPort, "%d", ntohs(pservent->s_port));
    lstrcat(lpszMessage, lpszPort);
}

MessageBox(NULL, lpszMessage, "Info", MB_OK);
```

Note that the port number is converted to network byte order before it is passed to getservbyport(). The end result is the formatted message describing that port 37 using the “udp” transport protocol corresponds to the “time” service. Note the similarity between this sample and the one presented for getservbyname().

### Asynchronously Finding a Service Name When You Know Its Port Number

WSAAsyncGetServByPort() is the asynchronous counterpart to getservbyport(). Its function prototype is as follows:

```c
HANDLE PASCAL FAR WSAAsyncGetServByPort(HWND hWnd, u_int wMsg,
    int port, const char FAR * proto, char FAR * buf, int buflen);
```

hWnd is the handle to the window to which a message will be sent when WSAAsyncGetServByPort() has completed its asynchronous operation. wMsg is the user-defined message that will be posted to hWnd when the asynchronous operation is complete. port is the service port, in network byte order, of the service about which you want information. proto is a pointer to a protocol name; it is "tcp", "udp", or NULL. If proto is NULL, the first matching service is returned. buf is a pointer to an area of memory that, on successful completion of the service lookup, will contain the servent structure for the desired service. This buffer must be large enough to store the servent structure as well as other referenced data; therefore, it should be at least MAXGETHOSTSTRUCT bytes long. buflen is the size of the buf buffer. It should be MAXGETHOSTSTRUCT for safety's sake.

If the asynchronous operation is initiated successfully, the return value of WSAAsyncGetServByPort() is a handle to the asynchronous task. On failure of initialization, the function returns 0 (zero) and WSAGetLastError() should be called to find out the reason for the error. Possible error values include the following: WSANOTINITIALIZED if WSAStartup() wasn't called successfully; WSAENETDOWN if the network subsystem is failing; WSAEWOULDBLOCK if the function cannot be scheduled at this time due to a resource conflict within the specific WinSock implementation; or WSAEINPROGRESS if a blocking WinSock operation is currently in progress. The function's return value doesn't tell you whether the requested information was retrieved successfully; all it tells you is whether the function was started properly.

This function is used much like the other asynchronous functions discussed thus far. Using an MFC implementation method to replicate the example given in the getservbyport() example would have a class declaration like the following:

```cpp
class CMyWindow : public CFrameWnd
{
    ...
    // member variables
    PSERVENT m_pservent;            // pointer to service entry structure
    char m_lpszMessage[100];        // informational message
    char m_lpszPort[6];             // port number string
    HANDLE m_hGetServByPort;        // handle of asynchronous request
    char m_lpszServEntryBuf[MAXGETHOSTSTRUCT]; // service entry structure

    // member functions in the message map
    //{{AFX_MSG(CMyWindow)
    afx_msg void OnDoAsyncGetServByPort();
    afx_msg LONG OnAsyncGetServByPort(WPARAM wParam, LPARAM lParam);
    //}}AFX_MSG
    DECLARE_MESSAGE_MAP()
};
```

Notice that the variables are now member variables of the class. The implementation of the CMyWindow class begins with the message map for the window:

```cpp
#define WM_USER_ASYNCGETSERVBYPORT (WM_USER + 4)
```

```cpp
BEGIN_MESSAGE_MAP(CMyWindow, CFrameWnd)
    //{{AFX_MSG_MAP(CMyWindow)
    ON_COMMAND(ID_TEST_ASYNCGETSERVBYPORT, OnDoAsyncGetServByPort)
    ON_MESSAGE(WM_USER_ASYNCGETSERVBYPORT, OnAsyncGetServByPort)
    //}}AFX_MSG_MAP
END_MESSAGE_MAP()
```

The first entry in the message map is for a menu item that will launch the search. That function is implemented as follows:

```cpp
void CMyWindow::OnDoAsyncGetServByPort()
{
    // get the service entry structure for the port 37 service using UDP
    if ((m_hGetServByPort = WSAAsyncGetServByPort(m_hWnd,
        WM_USER_ASYNCGETSERVBYPORT, htons(37), "udp",
        m_lpszServEntryBuf, MAXGETHOSTSTRUCT)) == 0)
    {
        wsprintf(m_lpszMessage, "WSAAsyncGetServByPort() generated error %d",
            WSAGetLastError());
        MessageBox(m_lpszMessage, "Info");
    }
}
```

The second entry in the message map is for the user-defined message that indicates the asynchronous function has completed. When the WM_USER_ASYNCGETSERVBYPORT message is generated by WinSock on completion of the asynchronous call, the OnAsyncGetServByPort() function is executed. That function is implemented as follows:

```cpp
LONG CMyWindow::OnAsyncGetServByPort(WPARAM wParam, LPARAM lParam)
{
    // check for an error
    if (WSAGETASYNCERROR(lParam) != 0)
        MessageBox("WSAAsyncGetServByPort() had an error", "Info");
    else
    {
        // assign a servent service entry pointer to the buffer
        m_pservent = (PSERVENT)m_lpszServEntryBuf;

        // format the results
        wsprintf(m_lpszMessage, "Service %s using protocol %s has port ",
            m_pservent->s_name, m_pservent->s_proto);
        wsprintf(m_lpszPort, "%d", ntohs(m_pservent->s_port));
        lstrcat(m_lpszMessage, m_lpszPort);
        MessageBox(m_lpszMessage, "Info");
    }

    return 0L;
}
```

## Summary

This chapter examined the many conversion and database functions provided by WinSock. There are more such functions but the most commonly used ones were presented here. Chapter 8, “Sample Applications,” contains a complete application that uses several of these functions.

The next chapter discusses the functions necessary for creating a socket, connecting through sockets, and sending data back and forth through a socket. With that knowledge, you’ll be ready to write fully functional WinSock applications.

![](img/5e551abe6e0cb0588043ee757a235ddb_98_0.png)

## 7
## Socket Functions

The preceding two chapters show how to initialize the WinSock library and how to resolve host names and services. This chapter discusses the remaining WinSock functions necessary to make a truly useful networked application. Among these functions are the following: `socket()` to create an end-point of communication, `bind()` to give the end-point a name, `listen()` to listen for incoming connections, `accept()` to accept a connection, `send()` and `sendto()` to send data, and `recv()` and `recvfrom()` to receive data.

Figure 7.1 shows the flow of WinSock function calls for a client and server using TCP. Figure 7.2 shows a similar flow of WinSock function calls, but this time for a client and server using UDP.

**Figure 7.1.** *Client/server WinSock function flow using TCP.*

![](img/5e551abe6e0cb0588043ee757a235ddb_99_0.png)
