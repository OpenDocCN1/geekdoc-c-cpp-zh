
```csharp
private void watch()
{
    // Create a new FileSystemWatcher and set its properties.
    watcher = new FileSystemWatcher();
    watcher.Path = path;

    /* Watch for changes in LastAccess and LastWrite times, and
       the renaming of files or directories. */
    watcher.NotifyFilter = NotifyFilters.LastAccess | NotifyFilters.LastWrite
        | NotifyFilters.FileName | NotifyFilters.DirectoryName;

    // Only watch text files.
    watcher.Filter = "*.txt*";

    // Add event handler.
    watcher.Changed += new FileSystemEventHandler(OnChanged);
    // Begin watching.
    watcher.EnableRaisingEvents = true;
}

// Define the event handler.
private void OnChanged(object source, FileSystemEventArgs e)
{
    //Copies file to another directory or another action.
    Console.WriteLine("File: " + e.FullPath + " " + e.ChangeType);
}
```

## Chapter 102: Access network shared folder with username and password

Accessing network share file using PInvoke.

### Section 102.1: Code to access network shared file

```csharp
public class NetworkConnection : IDisposable
{
    string _networkName;

    public NetworkConnection(string networkName,
        NetworkCredential credentials)
    {
        _networkName = networkName;

        var netResource = new NetResource()
        {
            Scope = ResourceScope.GlobalNetwork,
            ResourceType = ResourceType.Disk,
            DisplayType = ResourceDisplayType.Share,
            RemoteName = networkName
        };

        var userName = string.IsNullOrEmpty(credentials.Domain)
            ? credentials.UserName
            : string.Format(@"@{}\{}", credentials.Domain, credentials.UserName);

        var result = WNetAddConnection2(
            netResource,
            credentials.Password,
            userName,
            0);

        if (result != 0)
        {
            throw new Win32Exception(result);
        }
    }

    ~NetworkConnection()
    {
        Dispose(false);
    }

    public void Dispose()
    {
        Dispose(true);
        GC.SuppressFinalize(this);
    }

    protected virtual void Dispose(bool disposing)
    {
        WNetCancelConnection2(_networkName, 0, true);
    }

    [DllImport("mpr.dll")]
    private static extern int WNetAddConnection2(NetResource netResource,
        string password, string username, int flags);
    [DllImport("mpr.dll")]
    private static extern int WNetCancelConnection2(string name, int flags,
    bool force);
}
```

```csharp
[StructLayout(LayoutKind.Sequential)]
public class NetResource
{
    public ResourceScope Scope;
    public ResourceType ResourceType;
    public ResourceDisplaytype DisplayType;
    public int Usage;
    public string LocalName;
    public string RemoteName;
    public string Comment;
    public string Provider;
}

public enum ResourceScope : int
{
    Connected = 1,
    GlobalNetwork,
    Remembered,
    Recent,
    Context
};

public enum ResourceType : int
{
    Any = 0,
    Disk = 1,
    Print = 2,
    Reserved = 8,
}

public enum ResourceDisplaytype : int
{
    Generic = 0x0,
    Domain = 0x01,
    Server = 0x02,
    Share = 0x03,
    File = 0x04,
    Group = 0x05,
    Network = 0x06,
    Root = 0x07,
    Sharedadmin = 0x08,
    Directory = 0x09,
    Tree = 0x0a,
    Ndscontainer = 0x0b
}
```

## Chapter 103: Asynchronous Socket

By using asynchronous sockets a server can listen for incoming connections and do some other logic in the meantime in contrast to synchronous sockets when they are listening they block the main thread and the application becomes unresponsive and will freeze until a client connects.

### Section 103.1: Asynchronous Socket (Client / Server) example

### Server Side example

### Create Listener for server

Start off with creating a server that will handle clients that connect, and requests that will be sent. So create a Listener Class that will handle this.

```csharp
class Listener
{
    public Socket ListenerSocket; //This is the socket that will listen to any incoming connections
    public short Port = 1234; // on this port we will listen

    public Listener()
    {
        ListenerSocket = new Socket(AddressFamily.InterNetwork, SocketType.Stream,
ProtocolType.Tcp);
    }
}
```

First we need to initialize the Listener socket where we can listen on for any connections. We are going to use a Tcp Socket that is why we use SocketType.Stream. Also we specify to which port the server should listen to

Then we start listening for any incoming connections.

**The three methods we use here are:**

- 1. ListenerSocket.Bind():
- 
- This method binds the socket to an IPEndPoint. This class contains the host and local or remote port information needed by an application to connect to a service on a host.
- 
- 2. ListenerSocket.Listen(10):
- 
- The backlog parameter specifies the number of incoming connections that can be queued for acceptance.
- 
- 3. ListenerSocket.BeginAccept():
- 
- The server will start listening for incoming connections and will go on with other logic. When there is a connection the server switches back to this method and will run the AcceptCallback method

```csharp
public void StartListening()
{
try
{
    MessageBox.Show($"Listening started port:{Port} protocol type: {ProtocolType.Tcp}");
    ListenerSocket.Bind(new IPEndPoint(IPAddress.Any, Port));
    ListenerSocket.Listen(10);
    ListenerSocket.BeginAccept(AcceptCallback, ListenerSocket);
}
catch(Exception ex)
{
    throw new Exception("listening error" + ex);
}
}
```

So when a client connects we can accept them by this method:

### Three methods we use here are:

- 1. ListenerSocket.EndAccept()
- 
- We started the callback with Listener.BeginAccept() and now we have to end that callback. The EndAccept() method accepts an IAsyncResult parameter, this will store the state of the asynchronous method, From this state we can extract the socket where the incoming connection was coming from.
- 
- 2. ClientController.AddClient()
- 
- With the socket we got from EndAccept() we create an Client with an own made method (code ClientController below server example).
- 
- 3. ListenerSocket.BeginAccept()
- 
- We need to start listening again when the socket is done with handling the new connection. Pass in the method who will catch this callback. And also pass in the Listener socket so we can reuse this socket for upcoming connections.

```csharp
public void AcceptCallback(IAsyncResult ar)
{
    try
    {
        Console.WriteLine($"Accept CallBack port:{Port} protocol type: {ProtocolType.Tcp}");
        Socket acceptedSocket = ListenerSocket.EndAccept(ar);
        ClientController.AddClient(acceptedSocket);

        ListenerSocket.BeginAccept(AcceptCallback, ListenerSocket);
    }
    catch (Exception ex)
    {
        throw new Exception("Base Accept error"+ ex);
    }
}
```

Now we have a Listening Socket but how do we receive data sent by the client that is what the next code is showing.

### Create Server Receiver for each client

First create a receive class with a constructor that takes in a Socket as parameter:

```csharp
public class ReceivePacket
{
    private byte[] _buffer;
    private Socket _receiveSocket;

    public ReceivePacket(Socket receiveSocket)
    {
        _receiveSocket = receiveSocket;
    }
}
```

In the next method we first start off with giving the buffer a size of 4 bytes (Int32) or package contains two parts (length, actual data). So the first 4 bytes we reserve for the length of the data the rest for the actual data.

Next we use BeginReceive() method. This method is used to start receiving from connected clients and when it will receive data it will run the ReceiveCallback function.

```csharp
public void StartReceiving()
{
    try
    {
        _buffer = new byte[4];
        _receiveSocket.BeginReceive(_buffer, 0, _buffer.Length, SocketFlags.None,
ReceiveCallback, null);
    }
    catch {}
}

private void ReceiveCallback(IAsyncResult AR)
{
    try
    {
        // if bytes are less than 1 takes place when a client disconnect from the server.
        // So we run the Disconnect function on the current client
        if (_receiveSocket.EndReceive(AR) > 1)
        {
            // Convert the first 4 bytes (int 32) that we received and convert it to an Int32
(this is the size for the coming data).
            _buffer = new byte[BitConverter.ToInt32(_buffer, 0)];
            // Next receive this data into the buffer with size that we did receive before
            _receiveSocket.Receive(_buffer, _buffer.Length, SocketFlags.None);
            // When we received everything it's up to you to convert it into the data that you've
sent.
            // For example string, int etc... in this example I only use the implementation for
sending and receiving a string.

            // Convert the bytes to string and output it in a message box
            string data = Encoding.Default.GetString(_buffer);
            MessageBox.Show(data);
            // Now we have to start all over again with waiting for a data to come from the
socket.

            StartReceiving();
        }
        else
        {
            Disconnect();
        }
    }
    catch {}
}
```
