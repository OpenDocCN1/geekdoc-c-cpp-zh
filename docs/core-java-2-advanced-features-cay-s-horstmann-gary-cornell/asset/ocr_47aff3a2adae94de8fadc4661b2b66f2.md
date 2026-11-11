Type anything and watch the input echo on your screen. Type **\n** (all uppercase letters) to disconnect. The server program will terminate as well.

| `java.net.ServerSocket` | 1.0 |
|---|---|
| `ServerSocket(int port)` | creates a server socket that monitors a port. |
| `Socket accept()` | waits for a connection. This method blocks (i.e., idles) the current thread until the connection is made. The method returns a `Socket` object through which the program can communicate with the connecting client. |
| `void close()` | closes the server socket. |

# 4.2.2 Serving Multiple Clients

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