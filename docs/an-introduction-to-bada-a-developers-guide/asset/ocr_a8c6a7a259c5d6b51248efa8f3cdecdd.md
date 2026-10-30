```
{
    AppLog("AsyncSelectByListener Failed %d",r);
}

//NetEndPoint holds the IP address and Port number
Ip4Address peerAddr(NET_SOCKET_INADDR_ANY);
unsigned short peerPort = 9000;
NetEndPoint peerEndPoint(peerAddr, peerPort);

//The socket will bind to a port, on which it will listen for
//connection
r = pServerSocket->Bind(peerEndPoint);
if (E_SUCCESS!= r)
{
    AppLog("CreateServerSocket Bind Failed %d",r);
}

//The socket will listen to the incoming connections, the maximum
//number of incoming connections that can be queued for acceptance
//can be specified as argument to this function
r = pServerSocket->Listen(1);

if (E_SUCCESS!= r)
{
    AppLog("CreateServerSocket Listen Failed %d",r);
}
```

# 3. Create a client socket as follows:

+   a. Create a socket instance.
+   b. As with a client socket, in the construct method for the TCP socket provide NET_SOCKET_TYPE_STREAM as the net socket type and NET_SOCKET_PROTOCOL_TCP as the net socket protocol.
+   c. To create a non-blocking socket, register with ISocketEventListener by calling AddSocketListener.
+   d. Set the socket in async mode by calling AsyncSelectByListener.
+   e. Call the Connect function and specify the NetEndPoint of the server to which this client is going to connect.

```
void
MyClass::CreateClientSocket(String serverIP)
{
    result r = E_SUCCESS;

    //Create socket instance
```