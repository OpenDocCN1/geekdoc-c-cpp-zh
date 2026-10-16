# Creating a Listener Using Sockets

Let’s start with a server that listens to incoming requests. The server requires a port number that is expected with the program arguments. With this, it invokes the Listener method (code file SocketServer/Program.cs):

```
static void Main(string[] args)
{
    if (args.Length != 1)
    {
        ShowUsage();
        return;
    }
    int port;
    if (!int.TryParse(args[0], out port))
    {
        ShowUsage();
        return;
    }
    Listener(port);
    ReadLine();
}

private void ShowUsage()
{
    WriteLine("SocketServer port");
}
```

The most important code with regard to sockets is in the following code snippet. The listener creates a new Socket object. With the constructor, the AddressFamily, SocketType, and ProtocolType are supplied. The AddressFamily is a large enumeration that offers many different networks. Examples are DECnet, which was released 1975 by Digital Equipment and used as main network communication between PDP-11 systems; Banyan VINES, which was used to connect client machines; and, of course, InetnetWork for IPv4 and InternetWorkV6 for IPv6. As mentioned previously, you can use sockets for a large number of networking protocols. The second parameter SocketType specifies the kind of socket. Examples are Stream for TCP, Dgram for UDP, or Raw for raw sockets. The third parameter is an enumeration for the ProtocolType. Examples are IP, Ucmp, Udp, IPv6, and Raw. The settings you choose need to match. For example, using TCP with IPv4, the address family must be InterNetwork, the socket type Stream, and the protocol type Tcp. To create a UDP communication with IPv4, the address family needs to be set to InterNetwork, the socket type Dgram, and the protocol type Udp.

```
public static void Listener(int port)
{
    var listener = new Socket(AddressFamily.InterNetwork,
    SocketType.Stream,
        ProtocolType.Tcp);
    listener.ReceiveTimeout = 5000; // receive timout 5 seconds
    listener.SendTimeout = 5000; // send timeout 5 seconds
    // etc.
```