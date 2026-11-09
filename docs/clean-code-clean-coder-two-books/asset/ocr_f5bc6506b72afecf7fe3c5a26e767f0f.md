talked about strategies for exposing concurrent problems by instrumenting your code.

# Tutorial: Full Code Examples

# Client/Server Nonthreaded

# Listing A-3 server.java

```
```java
package com.objectmentor.clientserver.nonth threaded;

import java.io.IOException;
import java.net.ServerSocket;
import java.net.Socket;
import java.net.SocketException;

import common.MessageUtils;

public class Server implements Runnable {
    ServerSocket serverSocket;
    volatile boolean keepProcessing = true;

    public Server(int port, int millisecondsTimeout) throws IOException {
        serverSocket = new ServerSocket(port);
        serverSocket.setSoTimeout(millisecondsTimeout);
    }

    public void run() {
        System.out.printf("Server Starting\\n");

        while (keepProcessing) {
            try {
                System.out.printf("accepting client\\n");
                Socket socket = serverSocket.accept();
                System.out.printf("got client\\n");
                process(socket);
            } catch (Exception e) {
                handle(e);
```
```