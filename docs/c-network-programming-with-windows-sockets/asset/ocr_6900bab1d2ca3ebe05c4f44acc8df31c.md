```
```c
// get the service entry structure for the time service using UDP
if ((pservnt = getservbyname("time", "udp")) == NULL)
    wsprintf(lpszMessage, "getservbyname() generated error %d",
        WSAGetLastError());
else
{
    // format the results
    wsprintf(lpszMessage, "Service %s using protocol %s has port ",
        pservnt->s_name, pservnt->s_proto);
    wsprintf(lpszPort, "%d", ntohs(pservnt->s_port));
    lstrcat(lpszMessage, lpszPort);
}

MessageBox(NULL, lpszMessage, "Info", MB_OK);
```
```

The end result is the formatted message describing that the “time” service using the “udp” protocol has port 37. Notice that the port number, `pservnt->s_port`, must be converted from network to host byte ordering.

If the sample was rewritten to not specify the transport protocol, the results would be different:

```
```c
Pservnt pservnt;             // pointer to service entry structure
char lpszMessage[100];       // informational message
char lpszPort[6];            // port number string

// get the service entry structure for the time service
if ((pservnt = getservbyname("time", NULL)) == NULL)
    wsprintf(lpszMessage, "getservbyname() generated error %d",
        WSAGetLastError());
else
{
    // format the results
    wsprintf(lpszMessage, "Service %s using protocol %s has port ",
        pservnt->s_name, pservnt->s_proto);
    wsprintf(lpszPort, "%d", ntohs(pservnt->s_port));
    lstrcat(lpszMessage, lpszPort);
}

MessageBox(NULL, lpszMessage, "Info", MB_OK);
```
```

The end result of this sample is the formatted message describing that the “time” service using the “tcp” protocol has port 37. The TCP result is given because that entry appears first in the services file.

# Asynchronously Finding a Service’s Port Number

`WSAAsyncGetServByName()` is the asynchronous counterpart to `getservbyname()`. Its function prototype is as follows:

```
```c
HANDLE PASCAL FAR WSAAsyncGetServByName(HWND hWnd, u_int wMsg,
    const char FAR * name, const char FAR * proto,
    char FAR * buf, u_int buflen);
```
```