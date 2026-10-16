```
```csharp
{
    WriteLine("no IPv4 address");
    return;
}

using (var client = new Socket(AddressFamily.InterNetwork,
    SocketType.Stream, ProtocolType.Tcp))
{
    client.Connect(ipAddress, port);
    WriteLine("client successfully connected");
    var stream = new NetworkStream(client);
    var cts = new CancellationTokenSource();

    Task tSender = Sender(stream, cts);
    Task tReceiver = Receiver(stream, cts.Token);
    await Task.WhenAll(tSender, tReceiver);
}
}
catch (SocketException ex)
{
    WriteLine(ex.Message);
}
}
```
```

> **NOTE** *If you change the filtering of the address list to get an IPv6 address instead of a IPv4 address, you also need to change the `Socket` invocation to create a socket for the IPv6 address family.*

The `Sender` method asks the user for input and sends this data to the network stream with the `WriteAsync` method. The `Receiver` method receives data from the stream with the `ReadAsync` method. After the user enters the termination string, cancellation is sent from the `Sender` task via a `CancellationToken`:

```
```csharp
public static async Task Sender(NetworkStream stream,
    CancellationTokenSource cts)
{
    WriteLine("Sender task");
    while (true)
    {
        WriteLine("enter a string to send, shutdown to exit");
        string line = ReadLine();
        byte[] buffer = Encoding.UTF8.GetBytes($"{line}\r\n");
        await stream.WriteAsync(buffer, 0, buffer.Length);
        await stream.FlushAsync();
        if (string.Compare(line,"Shutdown", ignoreCase: true) == 0)
        {
            cts.Cancel();
            WriteLine("sender task closes");
            break;
        }
    }
}
```
```

```
```csharp
private const int ReadBufferSize = 1024;

public static async Task Receiver(NetworkStream stream,
    CancellationToken token)
{
    try
```
```