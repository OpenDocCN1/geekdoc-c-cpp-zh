# Section 98.4: Basic UDP Client

This code example creates a UDP client then sends "Hello World" across the network to the intended recipient. A listener does not have to be active, as UDP Is connectionless and will broadcast the message regardless. Once the message is sent, the clients work is done.

```
byte[] data = Encoding.ASCII.GetBytes("Hello World");
string ipAddress = "192.168.1.141";
string sendPort = 55600;
try
{
    using (var client = new UdpClient())
    {
        IPEndPoint ep = new IPEndPoint(IPAddress.Parse(ipAddress), sendPort);
        client.Connect(ep);
        client.Send(data, data.Length);
    }
}
catch (Exception ex)
{
    Console.WriteLine(ex.ToString());
}
```

Below is an example of a UDP listener to complement the above client. It will constantly sit and listen for traffic on a given port and simply write that data to the console. This example contains a control flag 'done' that is not set internally and relies on something to set this to allow for ending the listener and exiting.

```
bool done = false;
int listenPort = 55600;
using(UdpClient listener = new UdpClient(listenPort))
{
    IPEndPoint listenEndPoint = new IPEndPoint(IPAddress.Any, listenPort);
    while(!done)
    {
        byte[] receivedData = listener.Receive(ref listenPort);

        Console.WriteLine("Received broadcast message from client {0}", listenEndPoint.ToString());

        Console.WriteLine("Decoded data is:");
        Console.WriteLine(Encoding.ASCII.GetString(receivedData)); //should be "Hello World" sent from above client
    }
}
```