+   - TCP
+   - HTTP
+   - IPC

Let’s discuss these in detail, one by one.

# The TCP Channel

The TCP channel is a socket-based transport channel that uses the TCP protocol to transport the serialized message stream across boundaries. It uses the TcpChannel class to setup a remoting server and its client. The TcpChannel class is defined in the System.Runtime.Remoting.Channels.Tcp namespace and implements the IChannel, IChannelSender, and IChannelReceiver interfaces, which means the TcpChannel class supports both sending and receiving data across .NET remoting boundaries. By default, the TcpChannel class uses the binary formatter to serialize messages; however, it can also use the SOAP formatter.

The class hierarchy of the TcpChannel class is shown as follows:

```
System.Object
  System.Runtime.Remoting.Channels.Tcp.TcpChannel
```

Table 35.9 lists the noteworthy public properties of the TcpChannel class:

| Table 35.9: Noteworthy Public Properties of the TcpChannel Class |
| Property | Description |
| ChannelData | Gets the channel-specific data |
| ChannelName | Gets the name of the current channel |
| ChannelPriority | Returns the priority of the current channel |

Table 35.10 lists the noteworthy public methods of the TcpChannel class:

| Table 35.10: Noteworthy Public Methods of the TcpChannel Class |
| Method | Description |
| CreateMessageSink() | Returns a channel message sink that delivers messages to the specified URL or channel data object |
| GetUrlsForUri() | Returns an array of all the URLs for an object with the specified URI, hosted on the current TcpChannel |
| Parse() | Extracts the channel URI and the remote well-known object URI from the specified URL |
| StartListening() | Instructs the current channel to start listening to requests |
| StopListening() | Instructs the current channel to stop listening to requests |

# The HTTP Channel

The HTTP channel uses the HTTP protocol to transfer messages over the Internet. You can specify an HTTP channel for remote calls to a client by using the HttpChannel class. This class can be used over the Internet because firewalls generally do not block HTTP communication. The HttpChannel class is defined in the System.Runtime.Remoting.Channels.Http namespace and implements the HTTP transport functionality. Similar to the TcpChannel class, the HttpChannel class can also send and receive messages across boundaries. By default, the HttpChannel class uses the SOAP formatter to serialize messages; however, it can also use the binary formatter. The class hierarchy of the HttpChannel class is shown as follows:

```
System.Object
  System.Runtime.Remoting.Channels.BaseChannelObjectWithProperties
    System.Runtime.Remoting.Channels.BaseChannelWithProperties
      System.Runtime.Remoting.Channels.Http.HttpChannel
```

Table 35.11 lists the noteworthy public properties of HttpChannel class: