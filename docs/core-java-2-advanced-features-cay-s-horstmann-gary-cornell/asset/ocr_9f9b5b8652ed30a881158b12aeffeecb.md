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
```