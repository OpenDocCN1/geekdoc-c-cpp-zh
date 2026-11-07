1.1 specification. The function’s prototype looks like the following:

```
int PASCAL FAR gethostname(char FAR * name, int namelen);
```

name is a far pointer to a character array that will accept the null-terminated host name, and namelen is the size of that character array. The gethostname() function returns 0 (zero) on success and SOCKET_ERROR on failure. On a return value of SOCKET_ERROR, you can call WSAGetLastError() to determine the specifics of the problem. Possible error values include WSAEFAULT if the buffer was too small to accept the host name, WSANOTINITIALISED if WSAStartup() wasn’t called successfully, WSAENETDOWN if the network subsystem is failing, or WSAEINPROGRESS if a blocking WinSock operation is currently in progress.

The following code fragment shows a typical call to gethostname():

```
```c
#define HOST_NAME_LEN (50)
char lpszHostName[HOST_NAME_LEN];    // will accept the host name
char lpszMessage[100];               // informational message

if (gethostname(lpszHostName, HOST_NAME_LEN) == 0)
    wsprintf(lpszMessage, 'This computer’s name is %s', lpszHostName);
else
    wsprintf(lpszMessage, 'gethostname() generated error %d',
        WSAGetLastError());

MessageBox(NULL, lpszMessage, 'Info', MB_OK);
```
```

![](bbox=[0.052, 0.545, 0.18, 0.599])

> **Note**
> 
> The name populated by gethostname() may be a simple name or a fully qualified domain name. For example, my computer, my computer may be recognized as goober or goober.ping.com. It’s up to those who implement WinSock to determine which format is returned. The only thing guaranteed about the name variable is that it can be parsed by the gethostbyname() function, which will be discussed later.

# Host Name Resolution

Humans use a textual representation for the hosts to which their programs connect. The computer requires a host’s address to be a 32-bit integer stored in a standardized way as described in the previous section on network byte ordering. Your program cannot connect to another computer until that computer’s IP address is in the 32-bit format. To remedy this difference, your program can use either the gethostbyname() or inet_addr() functions. gethostbyname() is used if you know either the simple name or the fully qualified domain name. inet_addr() is used if you know the IP address.