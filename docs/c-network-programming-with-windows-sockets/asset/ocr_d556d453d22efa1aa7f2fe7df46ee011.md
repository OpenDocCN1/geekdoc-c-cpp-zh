This chapter discusses the last pieces of the WinSock class library, including a function to display a WinSock error message.

# CWinSockErrorBox()

One thing that is missing thus far is a function to display an error message with a textual description of the actual WinSock error. The `CWinSockErrorBox()` function does just that.

The first parameter to `CWinSockErrorBox()` is an integer representing the WinSock error as returned by `WSAGetLastError()`. The second parameter is an optional pointer to a string that contains additional information you would like to present to the user.

The prototype for the function is as follows:

```
```c
void CWinSockErrorBox(int nError, LPSTR pszMessage = NULL);
```
```

The `CWinSockErrorBox()` function is implemented as follows:

```
```c
///////////////////////////////////////////////////////////////////////
// CWinSockErrorBox
//
void CWinSockErrorBox(int nError, LPSTR pszMessage/*= NULL*/)
{
#define ERROR_BUF_LEN (1000)
  char pszError[ERROR_BUF_LEN];

  wsprintf(pszError, "WinSock error %d: ", nError);

  switch (nError)
  {
    case WSAEINTR:
      lstrcat(pszError, "Interrupted system call");
      break;
    case WSAEBADF:
      lstrcat(pszError, "Bad file number");
      break;
    case WSAEACCES:
      lstrcat(pszError, "Permission denied");
      break;
    case WSAEFAULT:
      lstrcat(pszError, "Bad address");
      break;
    case WSAEINVAL:
      lstrcat(pszError, "Invalid argument");
      break;
    case WSAEMFILE:
      lstrcat(pszError, "Too many open files");
      break;
    case WSAEWOULDBLOCK:
      lstrcat(pszError, "Operation would block");
      break;
```
```