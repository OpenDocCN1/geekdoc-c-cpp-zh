
```cpp
//}}AFX_MSG_MAP
END_MESSAGE_MAP()

LONG CServerWindow::OnAsyncSelect(WPARAM wParam, LPARAM lParam)
{
    // wParam is the socket descriptor
    // lParam is a status or error indicator

    // check for an error
    if (WSAGETSELECTERROR(lParam) != 0)
        return 0;

    // what event are we being notified of?
    if (WSAGETSELECTEVENT(lParam) == FD_ACCEPT)
    {
        // m_clientS is defined as SOCKET in the CServerWindow class declaration
        m_clientS = accept(m_s, NULL, NULL);
        if (m_clientS == INVALID_SOCKET)
        {
            int nError = WSAGetLastError();
            if (nError == WSAEWOULDBLOCK)
            {
                // There really isn't a client ready to connect.
                // This error should never occur for the FD_ACCEPT event
                // so it should be treated just like this event
                // notification function hadn't been called.
                ;
            }
            else
                // some other error
                ;
        }
    }
}
```

Notice the call to `WSAGETSELECTERROR`. This is a macro provided in WINSOCK.H, which is called to determine whether there is an error in the asynchronous event. It returns 0 (zero) on success and an error value on failure. For the `FD_ACCEPT` event notification message, the error could be `WSAENETDOWN`, which means the network subsystem is down.

Also note that the `WSAGETSELECTEVENT` macro is called to determine the event that triggered this message handler even though the only way the `CServerWindow::OnAsyncSelect()` function is called is if the `FD_ACCEPT` event occurs. This macro will be used in later sample programs where the class’s member function handles several WinSock events for a particular socket.

If for some reason the `CServerWindow::OnAsyncSelect()` function is called with the `FD_ACCEPT` event but there is no client trying to connect to this server application, `accept()` returns `INVALID_SOCKET`. Calling `WSAGetLastError()` will return `WSAEWOULDBLOCK`, which tells you that this function is set up for nonblocking mode and if it weren’t, it would block.

## How Clients Connect to Servers

### Giving the Socket a Default Name

After the call to `socket()`, the `bind()` function may be used to give the socket a name. This step might be necessary because calling `socket()` simply reserves a socket descriptor. By naming the socket with `bind()`, you give the socket a port, out of which it communicates with a server.

The use of `bind()` to give a client socket a default name is shown here:

```c
SOCKET s;                    // socket descriptor
char lpszMessage[100];       // informational message
SOCKADDR_IN addr;            // Internet address

// create a stream socket
s = socket(AF_INET, SOCK_STREAM, 0);
if (s != INVALID_SOCKET)
{
    // fill out the socket's address information
    addr.sin_family = AF_INET;
    addr.sin_port = 0;       // let WinSock assign a port
    addr.sin_addr.s_addr = htonl(INADDR_ANY);

    // bind the socket to its address
    if (bind(s, (LPSOCKADDR)&addr, sizeof(addr)) == SOCKET_ERROR)
    {
        wsprintf(lpszMessage, "bind() generated error %d",
            WSAGetLastError());
        MessageBox(NULL, lpszMessage, "Info", MB_OK);
    }
    else
        ...
}
```

Note that `addr.sin_port` is assigned 0 (zero). This allows WinSock to assign any unused port it sees fit. This is in contrast to a server socket, which needs to listen for connections on a specific port. It really doesn’t matter which port a client uses. But if you do want to know which port a socket was assigned, you can use the `getsockname()` function. Its function prototype is as follows:

```c
int PASCAL FAR getsockname(SOCKET s,
  struct sockaddr FAR *name, int FAR * namelen);
```

It is used much like `getpeername()`. An example call to `getsockname()` is listed here:

```c
SOCKET s;                         // socket descriptor
char lpszMessage[100];             // informational message
SOCKADDR_IN addr;                  // Internet address used by bind()
SOCKADDR_IN nAddrAssigned;         // Internet address assigned by bind()
int nAddrAssignedLen = sizeof(nAddrAssigned);

// create a stream socket
s = socket(AF_INET, SOCK_STREAM, 0);
if (s != INVALID_SOCKET)
{
    // fill out the socket's address information

    addr.sin_family = AF_INET;
    addr.sin_port = 0;              // let WinSock assign a port
    addr.sin_addr.s_addr = htonl(INADDR_ANY);

    // bind the socket to its address
    if (bind(s, (LPSOCKADDR)&addr, sizeof(addr)) != SOCKET_ERROR)
    {
        // find out what port was assigned by WinSock
        if (getsockname(s, (LPSOCKADDR)&nAddrAssigned, &nAddrAssignedLen) == 0)
        // now nAddrAssigned.sin_port contains the port number
        // that WinSock assigned to this client
        ...
    }
}
```

In this example, as in the server example, the socket’s IP address is set to `INADDR_ANY`. This means that the socket can use any network interface the computer has. This use is fine for most instances. It may be necessary to specify a particular address if the computer on which the client application runs is connected to more than one network through more than one network interface. Figure 7.4 shows one possible scenario. The client computer in Figure 7.4 has two IP addresses; suppose that they are 166.12.34.101 and 166.12.34.102. If you want the client limited to going through only one network interface, you can do the following instead of using `INADDR_ANY`:

```c
addr.sin_addr.s_addr = inet_addr("166.12.34.101");
```

### Connecting to a Server

A client connects to a server using the `connect()` function. Its prototype is as follows:

```c
int PASCAL FAR connect(SOCKET s,
const struct sockaddr FAR *name, int namelen);
```

FIGURE 7.4. Client computer on two networks.

![](img/5e551abe6e0cb0588043ee757a235ddb_117_0.png)

s is the socket to use for the connection. name is the address of the server to connect to. It is always a `sockaddr_in` Internet address structure for WinSock 1.1. `namelen` is the length of the name parameter.

On success, `connect()` returns 0 (zero). On failure, it returns `SOCKET_ERROR` and `WSAGetLastError()` should be called to find out the cause of the error. Possible error values include the following: `WSANOTINITIALISED` if WinSock hasn’t been successfully initialized with a call to `WSAStartup()`; `WSAENETDOWN` if the network subsystem is failing; `WSAEADDRINUSE` if the address is already in use; `WSAEINTR` if the blocking call was canceled with `WSACancelBlockingCall()`; `WSAEINPROGRESS` if a blocking WinSock call is in progress; `WSAEADDRNOTAVAIL` if the address specified by `addr` isn’t available; `WSAEAFNOSUPPORT` if the addresses in the specified family can’t be used with this socket; `WSAECONNREFUSED` if the server forcefully refused the connection attempt; `WSAEDESTADDRREQ` if `name` isn’t specified; `WSAEFAULT` if `namelen` is invalid; `WSAEINVAL` if socket `s` isn’t bound to an address; `WSAEISCONN` if socket `s` is already connected; `WSAEMFILE` if there are no free file descriptors; `WSAENETUNREACH` if the network can’t be reached from this host at this time; `WSAENOBUFS` if no buffer space is available; `WSAENOTSOCK` if socket `s` isn’t a valid socket descriptor; `WSAETIMEDOUT` if the attempt to connect timed out; or `WSAEWOULDBLOCK` if socket `s` is marked as nonblocking and this connection can’t be completed immediately.

```cpp
// make the connection
if (connect(m_s, (LPSOCKADDR)&m_addrServer, sizeof(m_addrServer)) ==
    SOCKET_ERROR)
{
    int nError = WSAGetLastError();
    if (nError == WSAEWOULDBLOCK)
    {
        // this is ok...just wait for async notice
    }
    else
    {
        // some other error
    }
}
}
```

You also need a member function in `CClientWindow` to handle the `WM_USER + 1` message that’s generated when a client connection is completed:

```cpp
BEGIN_MESSAGE_MAP(CClientWindow, CFrameWnd)
    //{{AFX_MSG_MAP(CClientWindow)
    ...
    ON_MESSAGE(WM_USER + 1, OnAsyncSelect)
    ...
    //}}AFX_MSG_MAP
END_MESSAGE_MAP()
```

```cpp
LONG CClientWindow::OnAsyncSelect(WPARAM wParam, LPARAM lParam)
{
    // wParam is the socket descriptor
    // lParam is a status or error indicator

    // check for an error
    if (WSAGETSELECTERROR(lParam) != 0)
        return 0L;

    // what event are we being notified of?
    if (WSAGETSELECTEVENT(lParam) == FD_CONNECT)
    {
        // you now know that the m_s socket is connected to the server
    }
}
```

This message handler follows the same format as the `CServerWindow::OnAsyncSelect()` function. First, check for an error using the `WSAGETSELECTERROR` macro. Next, use `WSAGETSELECTEVENT` to determine which event caused this message to be called. The `FD_CONNECT` event tells us the client socket is connected to the server.

### Sending and Receiving Data on a Stream Socket

You have now seen how a server accepts a connection and how a client makes a connection. Once the client and server sockets are connected, data can be sent and received.
