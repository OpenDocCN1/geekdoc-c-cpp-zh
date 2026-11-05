
The IPAddress constructor is defined as follows,

```
public IPAddress(long newAddress);
```

It has only one parameter, a 32-bit value of the IP address. The class also contains the methods and properties described in the following table.

| Method | Description |
|---|---|
| HostToNetworkOrder() | Converts from host byte order to network byte order |
| IsLoopback() | Returns TRUE if the network address is the loopback adapter |
| NetworkToHostOrder() | Converts from network byte order to host byte order |
| Parse() | Converts a string to an IPAddress class |

| Property | Get/Set/Read-Only | Description |
|---|---|---|
| Address | Get/set | Value of the IP address |
| Any | Read-only field | Indicates that the IP address is used for all network adapters |
| Broadcast | Read-only field | Returns the IP broadcast address |
| Loopback | Read-only field | Returns the IP loopback address |
| None | Read-only field | Indicates that the IP address is not used for any network adapter |

Table 28.6.1 IPAddress class methods and properties

Widely used method in the IPAddress class is the Parse() method. It is used to construct a new IPAddress object using the standard dotted-notation Internet address, as shown below,

```
System.Net.IPAddress localIPAddress =
System.Net.IPAddress.Parse("127.0.0.1");
```

The IPAddress class is useful for managing an Internet address but most of the networking functions in the Compact Framework use the System.Net.IPEndPoint class to specify another machine on the network. An IPEndPoint class specifies the IP address of the remote connection as well as it contains information about the port that will be used to connect with the service running on the remote device. There are two ways to construct a new IPEndPoint class object. The first method takes the 32-bit value of the IP address and a port as shown below,

```
public IPEndPoint(long address, int port);
```

Another way to create a new IPEndPoint object is by passing in a previously created IPAddress object,

```
public IPEndPoint(IPAddress address, int port);
```

The following code shows how to create an IPEndPoint that represents a connection to the local machine on port 80,
System.Net.IPAddress localIPAddress =
System.Net.IPAddress.Parse("127.0.0.1");
System.Net.IPEndPoint localIPEndPoint = new
System.Net.IPEndPoint(localIPAddress, 80);

The IPEndPoint class consists of the methods and properties as described in the following table.

| Method | Description |
|---|---|
| Create() | Creates an IPEndPoint based on an IP address and port |
| Serialize() | Serializes IPEndPoint information into a SocketAddress instance |

| Property | Get/Set/Read-Only | Description |
|---|---|---|
| Address | Get/set | Value of the IP address |
| AddressFamily | Get | Gets the address family for the IP address |
| Port | Get/set | Value of the port |
| MaxPort | Read-only field | Specifies the maximum value for the port |
| MinPort | Read-only field | Specifies the minimum value for the port |

Table 28.6.2 IPEndPoint class methods and properties

## 28.6.3 Name Resolution

The resolution of a domain name (such as www.technicalpublications.org) or IP address is handled by the System.Net.Dns class. It contains the methods described in the following table.

| Method | Description |
|---|---|
| BeginGetHostByName() | Starts an asynchronous GetHostByName() request |
| BeginResolve() | Starts an asynchronous Resolve() request |
| EndGetHostByName() | Ends an asynchronous GetHostByName() request |
| EndResolve() | Ends an asynchronous Resolve() request |
| GetHostByAddress() | Gets host information based on the IP address |
| GetHostByName() | Gets host information based on the name |
| Resolve() | Resolves a host name or IP address to an IPHostEntry() class |

Table 28.6.3 Dns class methods

After the DNS resolution process has completed, information about the domain is stored in a new instance of the System.Net.IPHostEntry class. The class has the properties described in the following Table 28.6.4

| Property | Get/Set/Read-Only | Description |
|---|---|---|
| AddressList | Get/set | Gets or sets a list of IPAddress objects associated with the host |
| Aliases | Get/set | Gets or sets a list of aliases associated with the host |
| HostName | Get/set | Gets or sets the DNS host name |

Table 28.6.4 IPHostEntry class properties

The following code shows how to create an IPEndPoint that is associated with the Microsoft Web Server by using the System.Net.Dns class to first resolve the IP address.

```csharp
// Resolve the MS Web Server IP address
System.Net.IPHostEntry microsoftHost =
    System.Net.Dns.GetHostByName("www.microsoft.com");

// Copy the resolved IP address to a string
String msIP = microsoftHost.AddressList[0].ToString();

// Create the endpoint
System.Net.IPEndPoint microsoftEndPoint = new
    System.Net.IPEndPoint(microsoftHost.AddressList[0], 80);
```

## 28.6.4 Working with Winsock Connection

- The System.Net.Sockets namespace provides all of the classes that are needed to communicate over the Winsock interface when using the Compact Framework.
- The namespace provides four classes to work with Winsock connections,
  1. The System.Net.Sockets.Socket class is essentially a full wrapper around a traditional SOCKET handle. It provides all of the functionality for both connectionless and connection-based TCP and UDP communications.
  2. The System.Net.Sockets.TcpClient class provides all of the methods and properties for the client side of a TCP connection to a server.
  3. The System.Net.Sockets.TcpListener class provides all of the methods and properties for the server side of a TCP connection that will listen for incoming connections on a specific port.
  4. The System.Net.Sockets.UdpClient class provides all of the methods and properties for sending and receiving connectionless datagrams.

## 28.7 .NET Compact Framework - Mobile Devices and Pocket PC Platform

- The .NET Compact Framework has the ability to call into unmanaged code using Platform Invoke (P/Invoke). By using the P/Invoke service, one can access the APIs that are supported on a Pocket PC platform and exported by using dynamic link libraries (DLLs), from within a .NET application. This enables to integrate much of the functionality that is native to the Pocket PC, and not natively supported by the Compact Framework. For example, the Pocket PC Phone Edition supports the capability to send and receive SMS messages. P/Invoke enables the managed code to call into the unmanaged SMS API found in the cellcore.dll library.

To declare that a method in the application is going to use P/Invoke, DllImport attribute is used, which supports the fields described in the following table,

| Field | Description |
|---|---|
| EntryPoint | The function name that is to be called |
| CharSet | Specifies how the string arguments should be marshaled |
| CallingConvention | Specifies the calling convention to use when passing arguments |
| SetLastError | Set this value to TRUE to enable calling the Marshal.GetLastWin32Error method to check if an error occurred when invoking this method |

### Smart Device Wizard

Visual Studio .NET 2003 fully supports the development and deployment of .NET applications on mobile devices. It provides smart device wizard for mobile device applications.

![](img/3005a4307e6d8f3bb7e76eea28a92357_916_0.png)

Fig. 28.7.1 Smart device wizard

- The two platforms currently supported are Pocket PC and Windows CE. For each of these platforms, there are a number of project templates to choose from: Windows Application, Class Library, Non-graphical Application, or Empty Project.
- VS.NET uses the Smart Device Application Template to generate all the files necessary for the application and presents a blank form with a default menu attached to it. The controls can be dragged and dropped from the toolbox onto the form and code can be written that associates with events for these controls.
- The first time the emulator starts up, the .NET Compact Framework is installed. The .NET Compact Framework is less than 2 MB in size.
