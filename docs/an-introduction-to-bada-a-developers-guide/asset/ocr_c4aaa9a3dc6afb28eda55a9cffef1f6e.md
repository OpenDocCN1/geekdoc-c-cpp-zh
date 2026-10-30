Like the rest of the communications features of bada, HTTP requests are dealt with asynchronously, so to receive responses to a HTTP request, and to upload messages which are divided into chunks, you need to implement a IHttpTransactionEventListener.

For those web sites that require a name and password, you can specify this information when you open a HttpTransaction by wrapping the login information up in an HttpAuthentication object.

```
Osp::Net::Sockets
```

# Declared In:

```
FNetSockets.h
```

# Privileges Required:

You will need the following privilege to make use of the features of the Sockets sub-namespace:

| Privilege group | Privilege level | Description |
|---|---|---|
| SOCKET | NORMAL | Creating a socket connection, sending and receiving data |

# Summary

Selected important classes:

+   - SecureSocket
+   - Socket

Sockets implements socket data communications protocols, similar to the standard BSD socket library. A socket is described as an endpoint, one side of the communication between two applications running on a network. bada supports TCP/IP, UDP, and secure sockets, and the stream and datagram protocols. Applications should implement the ISocketEventListener to process socket events asynchronously.

The various classes for implementing socket functionality are shown in Figure 6.22. Notice that both standard and secure sockets are supported in bada.

```
Osp::Net::Wifi
```

# Declared In:

```
FNetWifi.h
```