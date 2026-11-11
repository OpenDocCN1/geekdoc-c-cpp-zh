
```java
catch (InterruptedIOException exception)
{
    react to timeout
}
```

There is one additional timeout issue that you need to address. The constructor

```
Socket(String host, int port)
```

can block indefinitely until an initial connection to the host is established.

You can overcome this problem by first constructing an unconnected socket and then connecting it with a timeout:

```
Socket s = new Socket();
s.connect(new InetSocketAddress(host, port), timeout);
```

See Section 4.3, “Interruptible Sockets,” on p. 250 for how to allow users to interrupt the socket connection at any time.

| Member | Description |
|---|---|
| `java.net.Socket` 1.0 |  |
| `Socket()` 1.1 | creates a socket that has not yet been connected. |
| `void connect(SocketAddress address)` 1.4 | connects this socket to the given address. |
| `void connect(SocketAddress address, int timeoutInMilliseconds)` 1.4 | connects this socket to the given address, or returns if the time interval expired. |
| `void setSoTimeout(int timeoutInMilliseconds)` 1.1 | sets the blocking time for read requests on this socket. If the timeout is reached, an InterruptedIOException is raised. |
| `boolean isConnected()` 1.4 | returns true if the socket is connected. |
| `boolean isClosed()` 1.4 | returns true if the socket is closed. |

### 4.1.4 Internet Addresses

Usually, you don’t have to worry too much about Internet addresses—the numerical host addresses that consist of 4 bytes (or, with IPv6, 16 bytes) such as 129.6.15.28. However, you can use the `InetAddress` class if you need to convert between host names and Internet addresses.

```java
public static void main(String[] args) throws IOException
{
    if (args.length > 0)
    {
        String host = args[0];
        InetAddress[] addresses = InetAddress.getAllByName(host);
        for (InetAddress a : addresses)
            System.out.println(a);
    }
    else
    {
        InetAddress localHostAddress = InetAddress.getLocalHost();
        System.out.println(localHostAddress);
    }
}
```

**java.net.InetAddress 1.0**

- `static InetAddress getByName(String host)` constructs an InetAddress, or an array of all Internet addresses, for the given host name.
- `static InetAddress[] getAllByName(String host)`
- `static InetAddress getLocalHost()` constructs an InetAddress for the local host.
- `byte[] getAddress()` returns an array of bytes that contains the numerical address.
- `String getHostAddress()` returns an IP address with decimal numbers, separated by periods, for example "129.6.15.28".
- `String getHostName()` returns the host name.

## 4.2 Implementing Servers

Now that we have implemented a basic network client that receives data from the Internet, let’s program a simple server that can send information to clients. In the previous section, we have implemented a basic network client that receives data from the Internet. In the following sections, we will program a simple server that can send information to clients.

### 4.2.1 Server Sockets

A server program, when started, waits for a client to attach to its port. For our example program, we chose port number 8189, which is not used by any of the standard services. The ServerSocket class establishes a socket. In our case, the command

```
ServerSocket s = new ServerSocket(8189);
```

establishes a server that monitors port 8189. The command

```
Socket incoming = s.accept();
```

tells the program to wait indefinitely until a client connects to that port. Once someone connects to this port by sending the correct request over the network, this method returns a Socket object that represents the connection that was made. You can use this object to get input and output streams, as is shown in the following code:

```
InputStream inStream = incoming.getInputStream();
OutputStream outStream = incoming.getOutputStream();
```

Everything that the server sends to the server output stream becomes the input of the client program, and all the output from the client program ends up in the server input stream.

In all the examples in this chapter, we transmit text through sockets. We therefore turn the streams into scanners and writers.

```
Scanner in = new Scanner(inStream, "UTF-8");
PrintWriter out = new PrintWriter(new OutputStreamWriter(outStream, "UTF-8"),
    true /* autoFlush */);
```

Let’s send the client a greeting:

```
out.println("Hello! Enter BYE to exit.");
```

When you use telnet to connect to this server program at port 8189, you will see this greeting on the terminal screen.

In this simple server, we just read the client’s input, a line at a time, and echo it. This demonstrates that the program receives the input. An actual server would obviously compute and return an answer depending on the input.

```
String line = in.nextLine();
out.println("Echo: " + line);
if (line.trim().equals("BYE")) done = true;
```

In the end, we close the incoming socket.

```
incoming.close();
```

That is all there is to it. Every server program, such as an HTTP web server, continues performing this loop:

- 1. It receives a command from the client (“get me this information”) through an incoming data stream.
- 2. It decodes the client command.
- 3. It gathers the information that the client requested.
- 4. It sends the information to the client through the outgoing data stream.

Listing 4.3 is the complete program.

**Listing 4.3  `server/EchoServer.java`**

```java
package server;

import java.io.*;
import java.net.*;
import java.util.*;

/**
 * This program implements a simple server that listens to port 8189 and echoes back all client
 * input.
 * @version 1.21 2012-05-19
 * @author Cay Horstmann
 */
public class EchoServer
{
    public static void main(String[] args) throws IOException
    {
        // establish server socket
        try (ServerSocket s = new ServerSocket(8189))
        {
            // wait for client connection
            try (Socket incoming = s.accept())
            {
                InputStream inStream = incoming.getInputStream();
                OutputStream outStream = incoming.getOutputStream();

                try (Scanner in = new Scanner(inStream, "UTF-8"))
                {
                    PrintWriter out = new PrintWriter(
                        new OutputStreamWriter(outStream, "UTF-8"),
                        true /* autoFlush */);

                    out.println("Hello! Enter BYE to exit.");

                    // echo client input
                    boolean done = false;
                    while (!done && in.hasNextLine())
                    {
                        String line = in.nextLine();
                        out.println("Echo: " + line);
                        if (line.trim().equals("BYE")) done = true;
                    }
                }
            }
        }
    }
}
```

To try it out, compile and run the program. Then use telnet to connect to the server localhost (or IP address 127.0.0.1) and port 8189.

If you are connected directly to the Internet, anyone in the world can access your echo server, provided they know your IP address and the magic port number.

When you connect to the port, you will see the message shown in Figure 4.4:

```
Hello! Enter BYE to exit.
```

![](img/7dd923a566750151a3aab0dacd0cdaa5_264_0.png)

**Figure 4.4** Accessing an echo server

Type anything and watch the input echo on your screen. Type **BYE** (all uppercase letters) to disconnect. The server program will terminate as well.

| Member | Description |
|---|---|
| `java.net.ServerSocket` 1.0 |  |
| `ServerSocket(int port)` | creates a server socket that monitors a port. |
| `Socket accept()` | waits for a connection. This method blocks (i.e., idles) the current thread until the connection is made. The method returns a `Socket` object through which the program can communicate with the connecting client. |
| `void close()` | closes the server socket. |

### 4.2.2 Serving Multiple Clients

There is one problem with the simple server in the preceding example. Suppose we want to allow multiple clients to connect to our server at the same time. Typically, a server runs constantly on a server computer, and clients from all over the Internet might want to use it at the same time. Rejecting multiple connections allows any one client to monopolize the service by connecting to it for a long time. We can do much better through the magic of threads.

Every time we know the program has established a new socket connection—that is, every time the call to `accept()` returns a socket—we will launch a new thread to take care of the connection between the server and that client. The main program will just go back and wait for the next connection. For this to happen, the main loop of the server should look like this:

```
while (true)
{
    Socket incoming = s.accept();
    Runnable r = new ThreadedEchoHandler(incoming);

    Thread t = new Thread(r);
    t.start();
}
```

The `ThreadedEchoHandler` class implements `Runnable` and contains the communication loop with the client in its run method.

```
class ThreadedEchoHandler implements Runnable
{
    . . .
}
```
