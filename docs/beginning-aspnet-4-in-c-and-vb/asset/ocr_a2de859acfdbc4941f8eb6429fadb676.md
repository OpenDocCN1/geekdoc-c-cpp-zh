# The UDP Class

As you might expect, the UdpClient class features a smaller and simpler interface than TcpClient. This reflects the relatively simpler nature of the protocol. Although both TCP and UDP classes use a socket underneath the covers, the UdpClient class does not contain a method to return a network stream for reading and writing. Instead, the member function Send() accepts an array of bytes as a parameter, and the Receive() function returns an array of bytes. Also, because UDP is a connectionless protocol, you can wait to specify the endpoint for the communication as a parameter to the Send() and Receive() methods, instead of specifying it earlier in a constructor or Connect() method. You can also change the endpoint on each subsequent send or receive.

The following code fragment uses the UdpClient class to send a message to an echo service. A server with an echo service running accepts TCP or UDP connections on port 7. The echo service simply echoes any data sent to the server back to the client. This service is useful for diagnostics and testing, although many system administrators disable echo services for security reasons:

```
```csharp
using System;
using System.Text;
using System.Net;
using System.Net.Sockets;
namespace Nrox.ProCSharp.InternetAccess.UdpExample
{
    class Class1
    {
        [STAThread]
        static void Main(string[] args)
        {
            UdpClient udpClient = new UdpClient();
            string sendMsg = "Hello Echo Server";
            byte[] sendBytes = Encoding.ASCII.GetBytes(sendMsg);
            udpClient.Send(sendBytes, sendBytes.Length, "SomeEchoServer.net", 7);
            IPEndPoint endPoint = new IPEndPoint(0, 0);
            byte[] recvBytes = udpClient.Receive(ref endPoint);
            string rcvMessage = Encoding.ASCII.GetString(rcvBytes,
                                                        0,
                                                        rcvBytes.Length);
            // should print out "Hello Echo Server"
            Console.WriteLine(rcvMessage);
        }
    }
}
```
```

You make heavy use of the Encoding.ASCII class to translate strings into arrays of byte and vice versa. Also note that you pass an IPEndPoint by reference into the Receive() method. Because UDP is not a connection-oriented protocol, each call to Receive() might pick up data from a different endpoint, so Receive() populates this parameter with the IP address and port of the sending host.

Both UdpClient and TcpClient inherit from a layer of abstraction over the lowest of the low-level classes: the Socket.

# The Socket Class

The Socket class offers the highest level of control in network programming. One of the easiest ways to demonstrate the class is to rewrite the TcpReceive application with the Socket class. The updated Listen() method is listed in this example:

```
```csharp
public void Listen()
{
    Socket listener = new Socket(AddressFamily.InterNetwork,
```
```