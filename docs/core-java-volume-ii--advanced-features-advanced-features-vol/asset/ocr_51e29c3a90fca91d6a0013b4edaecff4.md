# **Listing 4.3 (Continued)**

```
~~~java
18  // establish server socket
19  try (var s = new ServerSocket(8189))
20  {
21      // wait for client connection
22      try (Socket incoming = s.accept())
23      {
24          InputStream inStream = incoming.getInputStream();
25          OutputStream outStream = incoming.getOutputStream();
26
27          try (var in = new Scanner(inStream, StandardCharsets.UTF_8))
28          {
29              var out = new PrintWriter(
30                  new OutputStreamWriter(outStream, StandardCharsets.UTF_8),
31                  true /* autoFlush */);
32
33              out.println("Hello! Enter BYE to exit.");
34
35              // echo client input
36              var done = false;
37              while (!done && in.hasNextLine())
38              {
39                  String line = in.nextLine();
40                  out.println("Echo: " + line);
41                  if (line.trim().equals("BYE")) done = true;
42              }
43          }
44      }
45  }
46
47 }
~~~
```

To try it out, compile and run the program. Then use telnet to connect to the server localhost (or IP address 127.0.0.1) and port 8189.

If you are connected directly to the Internet, anyone in the world can access your echo server, provided they know your IP address and the magic port number.

When you connect to the port, you will see the message shown in Figure 4.4:

Hello! Enter BYE to exit.

Type anything and watch the input echo on your screen. Type BYE (all uppercase letters) to disconnect. The server program will terminate as well.