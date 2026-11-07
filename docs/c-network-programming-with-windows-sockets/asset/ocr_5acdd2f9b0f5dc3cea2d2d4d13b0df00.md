As an example of a compromise that could be made, look at a sample server application. The two servers presented in the preceding chapter, DESERV and SESERV, didn’t specify which port they operated on. Instead, they let WinSock assign one dynamically. In this case, the matching client program needed to know this port number before it could communicate with the server. It’s much more common that the port to which a service is assigned is hard-coded or entered into the services file on the hosts, allowing the port number to be resolved by its name. With this in mind, a compromise could be made mandating that a server socket specify either a port number or a service name; letting WinSock decide whether the port number could be prevented. This compromise simplifies both the server and client, and hence the class library itself.

# Implementation Details

The entire WinSock class library, composed of several classes, is implemented in the CWINSOCK.CPP file with CWINSOCK.H containing the class declarations. This source file is simply added to each project that requires WinSock functionality. This is in contrast to creating a dynamic link library that is then linked to the application. If you want to create a DLL out of the WinSock classes, you have to use a Microsoft Foundation Class Extension DLL because some of the WinSock classes are derived from MFC classes. The creation of such a DLL is beyond the scope of this book, but documentation on how to do so is available from Microsoft sources such as the Developer Network CD.

The actual code for the WinSock class libraries follows the convention used in the Microsoft Foundation Class library. All class names begin with a capital C, as in:

```
class CWinSock
```

All class member variables begin with the m_ prefix. The Hungarian naming convention is appended after the m_ prefix but before the actual variable name. For example, an integer containing the length of a buffer might look like the following:

```
int m_nBufLen;
```

This naming convention should ensure quick, easy recognition and understanding of WinSock class references in your applications.

# Summary

This chapter introduces the notion of a WinSock class library, including its requirements and possible limitations. Chapters 10 through 13 describe several classes that compose the WinSock class library. These classes are then used in fully functional programs in Chapters 14 through 16.