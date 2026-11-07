```
```c
case WSAENOBUFS:
    lstrcat(pszError, "No buffer space available");
    break;
case WSAISCONN:
    lstrcat(pszError, "Socket is already connected");
    break;
case WSAENOTCONN:
    lstrcat(pszError, "Socket is not connected");
    break;
case WSAESHUTDOWN:
    lstrcat(pszError, "Can't send after socket shutdown");
    break;
case WSAETOOMANYREFS:
    lstrcat(pszError, "Too many references: can't splice");
    break;
case WSAETIMEDOUT:
    lstrcat(pszError, "Connection timed out");
    break;
case WSAECONNREFUSED:
    lstrcat(pszError, "Connection refused");
    break;
case WSAELOOP:
    lstrcat(pszError, "Too many levels of symbolic links");
    break;
case WSAENAMETOOLONG:
    lstrcat(pszError, "File name too long");
    break;
case WSAEHOSTDOWN:
    lstrcat(pszError, "Host is down");
    break;
case WSAEHOSTUNREACH:
    lstrcat(pszError, "No route to host");
    break;
case WSAENOTEMPTY:
    lstrcat(pszError, "Directory not empty");
    break;
case WSAEPROCLIM:
    lstrcat(pszError, "Too many processes");
    break;
case WSAEUSERS:
    lstrcat(pszError, "Too many users");
    break;
case WSAEDQUOT:
    lstrcat(pszError, "Disc quota exceeded");
    break;
case WSAESTALE:
    lstrcat(pszError, "Stale NFS file handle");
    break;
case WSAEREMOTE:
    lstrcat(pszError, "Too many levels of remote in path");
    break;
case WSAEDISCON:
    lstrcat(pszError, "Disconnect");
    break;
case WSASYSNOTREADY:
    lstrcat(pszError, "Network sub-system is unusable");
    break;
case WSAVERNOTSUPPORTED:
    lstrcat(pszError, "WinSock DLL cannot support this application");
```
```