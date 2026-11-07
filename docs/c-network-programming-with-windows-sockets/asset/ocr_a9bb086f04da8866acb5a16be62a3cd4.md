configurable. This will ensure an easy fix to the problem of having several different servers hard-coded to use the same port number. If your server program must run on a computer with another server that was written to use a hard-coded port number, you can change the server and client configuration to use an unused port. With this information hard-coded, the change requires a recompile of the applications.

# Finding a Service’s Port Number

The `getservbyname()` function gets service information corresponding to a specific service name and protocol. Its function prototype looks like the following:

```
struct servent FAR * PASCAL FAR getservbyname(const char FAR * name,
        const char FAR * proto);
```

name is a pointer to a string that contains the service for which you are searching. The service name is either the official service name or an alias. proto is a pointer to a string that contains the transport protocol to use; it’s either “udp”, “tcp”, or NULL. A NULL proto will match on the first service in the services table that has the specified name, regardless of the protocol. The servent structure returned has the following format:

```
struct servent {
    char FAR * s_name;        // official service name
    char FAR * FAR * s_aliases; // alias list
    short s_port;              // port #
    char FAR * s_proto;        // protocol to use
};
```

A note on transport protocols: Protocol names are case sensitive. “TCP” is different from “tcp.” Ensure that you are using the exact format as listed in your services file.

The `getservbyname()` function returns a pointer to a servent structure on success and NULL on failure. On a return value of NULL, you can call `WSAGetLastError()` to determine the specifics of the problem. Possible error values include the following: WSANOTINITIALISED if WSAStartup() wasn’t called successfully; WSAENETDOWN if the network subsystem is failing; WSA_NO_RECOVERY if there was an unrecoverable error; WSANO_DATA if the service name is valid but no appropriate data could be found; WSAEINPROGRESS if a blocking WinSock operation is currently in progress; or WSAEINTR if the blocking call was canceled by WSACancelBlockingCall().

This code fragment searches for the time service on a UDP transport connection:

```
PSERVENT pservent;        // pointer to service entry structure
char lpszMessage[100];    // informational message
char lpszPort[6];         // port number string
```