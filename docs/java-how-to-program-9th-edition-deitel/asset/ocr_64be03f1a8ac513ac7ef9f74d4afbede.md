# 27.5 Establishing a Simple Client Using Stream Sockets

Establishing a simple client in Java requires four steps.

# Step 1: Create a Socket to Connect to the Server

In Step 1, we create a Socket to connect to the server. The Socket constructor establishes the connection. For example, the statement

```
Socket connection = new Socket( serverAddress, port );
```

uses the Socket constructor with two arguments—the server’s address (serverAddress) and the port number. If the connection attempt is successful, this statement returns a Socket. A connection attempt that fails throws an instance of a subclass of IOException, so many programs simply catch IOException. An UnknownHostException occurs specifically when the system is unable to resolve the server name specified in the call to the Socket constructor to a corresponding IP address.

# Step 2: Get the Socket’s I/O Streams

In Step 2, the client uses Socket methods getInputStream and getOutputStream to obtain references to the Socket’s InputStream and OutputStream. As we mentioned in the preceding section, we can use the techniques of Chapter 17 to wrap other stream types around the InputStream and OutputStream associated with the Socket. If the server is sending information in the form of actual types, the client should receive the information in the same format. Thus, if the server sends values with an ObjectOutputStream, the client should read those values with an ObjectInputStream.

# Step 3: Perform the Processing

Step 3 is the processing phase in which the client and the server communicate via the InputStream and OutputStream objects.

# Step 4: Close the Connection

In Step 4, the client closes the connection when the transmission is complete by invoking the close method on the streams and on the Socket. The client must determine when the server is finished sending information so that it can call close to close the Socket connection. For example, the InputStream method read returns the value –1 when it detects end-of-stream (also called EOF—end-of-file). If an ObjectInputStream reads information from the server, an EOFException occurs when the client attempts to read a value from a stream on which end-of-stream is detected.

# 27.6 Client/Server Interaction with Stream Socket Connections

Figures 27.5 and 27.7 use stream sockets, ObjectInputStream and ObjectOutputStream to demonstrate a simple client/server chat application. The server waits for a client connection attempt. When a client connects to the server, the server application sends the client a String object (recall that Strings are Serializable objects) indicating that the connection was successful. Then the client displays the message. The client and server applications each provide text fields that allow the user to type a message and send it to the other application. When the client or the server sends the String "TERMINATE", the con-