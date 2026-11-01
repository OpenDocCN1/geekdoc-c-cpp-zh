```
NetworkStream ns = tcpClient.GetStream();
FileStream fs = File.Open("form1.cs", FileMode.Open);

int data = fs.ReadByte();

while(data != -1)
{
    ns.WriteByte((byte)data);
    data = fs.ReadByte();
}

fs.Close();
ns.Close();
tcpClient.Close();
}
```

This example creates the TcpClient using a host name and a port number. Alternatively, if you have an instance of the IPEndPoint class, then you can pass the instance to the TcpClient constructor. After retrieving an instance of the NetworkStream class, you open the source code file and begin to read bytes. As with many of the binary streams, you need to check for the end of the stream by comparing the return value of the ReadByte() method to -1. After your loop has read all the bytes and sent them along to the network stream, you must close all the open files, connections, and streams.

On the other side of the connection, the TcpReceive application displays the received file after the transmission is finished (see Figure 24-12).

![](bbox=[0.2, 0.68, 0.7, 0.9])

# FIGURE 24-12

The form consists of a single TextBox control named txtDisplay. The TcpReceive application uses a TcpListener to wait for the incoming connection. To prevent freezing the application interface, you use a background thread to wait for and then read from the connection. Thus, you need to include the System.Threading namespace as well these other namespaces:

```
using System;
using System.IO;
```