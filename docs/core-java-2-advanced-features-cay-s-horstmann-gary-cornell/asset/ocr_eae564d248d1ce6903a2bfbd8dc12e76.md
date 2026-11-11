**NOTE:** In network parlance, a port is not a physical device, but an abstraction facilitating communication between a server and a client (see Figure 4.2).

![](bbox=[0.126, 0.229, 0.789, 0.451])

**Figure 4.2** A client connecting to a server port

The server software is continuously running on the remote machine, waiting for any network traffic that wants to chat with port 13. When the operating system on the remote computer receives a network package that contains a request to connect to port number 13, it wakes up the listening server process and establishes the connection. The connection stays up until it is terminated by one of the parties.

When you began the telnet session with `time-a.nist.gov` at port 13, a piece of network software knew enough to convert the string `"time-a.nist.gov"` to its correct Internet Protocol (IP) address, 129.6.15.28. The telnet software then sent a connection request to that address, asking for a connection to port 13. Once the connection was established, the remote program sent back a line of data and closed the connection. In general, of course, clients and servers engage in a more extensive dialog before one or the other closes the connection.

Here is another experiment along the same lines—but a bit more interesting. Type

```
```text
telnet horstmann.com 80
```
```

Then type very carefully the following:

```
```http
GET / HTTP/1.1
Host: horstmann.com

```
```

That is, hit the Enter key twice at the end.