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

+   1. It receives a command from the client (“get me this information”) through an incoming data stream.
+   2. It decodes the client command.
+   3. It gathers the information that the client requested.
+   4. It sends the information to the client through the outgoing data stream.

Listing 4.3 is the complete program.

# Listing 4.3  `server/EchoServer.java`

```
package server;

import java.io.*;
import java.net.*;
import java.nio.charset.*;
import java.util.*;

/**
 * This program implements a simple server that listens to port 8189 and echoes back all
 * client input.
 * @version 1.22 2018-03-17
 * @author Cay Horstmann
 */
public class EchoServer
{
    public static void main(String[] args) throws IOException
    {
```

(Continues)