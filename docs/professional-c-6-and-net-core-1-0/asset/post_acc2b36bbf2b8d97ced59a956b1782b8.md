
```
}
}
catch (SocketException ex)
{
    WriteLine(ex.Message);
    return null;
}
}
```

When you pass a website to the program, you see a successful request with HTML content shown in the console.

Now it’s time to create a TCP listener with a custom protocol.

## Creating a TCP Listener

Creating your own protocol based on TCP needs requires some advance thought about the architecture. You can define your own binary protocol where every bit is saved on the data transfer, but it’s more complex to read; alternatively, you can use a text-based format such as HTTP or FTP. Should a session stay open or be closed with every request? Does the server need to keep state for a client, or is all the data sent with every request?

The custom server will support some simple functionality, such as echo and reverse a message that is sent. Another feature of the custom server is that the client can send state information and retrieve it again using another call. The state is stored temporarily in a session state. Although it’s a simple scenario, you get the idea of what’s needed to set this up.

The TcpServer sample code is implemented as a Console Application (Package) and makes use of the following dependencies and namespaces:

## Dependencies

```
NETStandard.Library
```

## Namespaces

```
System
System.Collections
System.Collections.Concurrent
System.Linq
System.Net.Sockets
System.Text
System.Threading
System.Threading.Tasks
static System.Console
static TcpServer.CustomProtocol
```

The custom TCP listener supports a few requests, as shown in the following table.

| Request | Description |
|---|---|
| HELO::v1.0 | This command needs to be sent after initiating the connection. Other commands will not be accepted. |
| ECHO::message | The ECHO command returns the message to the caller. |
| REV::message | The REV command reserves the message and returns it to the caller. |
| BYE | The BYE command closes the connection. |
| SET::key=value | The SET command sets the server-side state that can be retrieved with the GET command. |
| GET::key |  |

The first line of the request is a session-identifier prefixed by ID. This needs to be sent with every request except the HELO request. This is used as a state identifier.

All the constants of the protocol are defined in the static class CustomProtocol (code file TcpServer/CustomProtocol.cs):

```
public static class CustomProtocol
{
    public const string SESSIONID ="ID";
    public const string COMMANDHELO ="HELO";
    public const string COMMANDECHO ="ECHO";
    public const string COMMANDREV ="REV";
    public const string COMMAND BYE ="BYE";
    public const string COMMANDSET ="SET";
    public const string COMMANDGET ="GET";

    public const string STATUSOK ="OK";
    public const string STATUSCLOSED ="CLOSED";
    public const string STATUSINVALID ="INV";
    public const string STATUSUNKNOWN ="UNK";
    public const string STATUSNOTFOUND ="NOTFOUND";
    public const string STATUSTIMEOUT ="TIMEOUT";

    public const string SEPARATOR ="::";

    public static readonly TimeSpan SessionTimeout =
TimeSpan.FromMinutes(2);
}
```

The Run method (which is invoked from the Main method) starts a timer that cleans up all the session state every minute. The major functionality of the Run method is the start of the server by invoking the method RunServerAsync (code file TcpServer/Program.cs):

```
static void Main()
{
    var p = new Program();
    p.Run();
}

public void Run()
{
    using (var timer = new Timer(TimerSessionCleanup, null,
TimeSpan.FromMinutes(1), TimeSpan.FromMinutes(1))
{
    RunServerAsync().Wait();
}
```

The most important part of the server regarding the TcpListener class is in the method RunServerAsync. The TcpListener is instantiated using the constructor the IP address and port number where the listener can be accessed. Calling the Start method, the listener starts listening for client connections. The AcceptTcpClientAsync waits until a client connects. As soon as a client is connected, a TcpClient instance is returned that allows communication with the client. This instance is passed to the RunClientRequest method, where the request is dealt with.

```
private async Task RunServerAsync()
{
    try
    {
        var listener = new TcpListener(IPAddress.Any, portNumber);
        WriteLine($"listener started at port {portNumber}");
        listener.Start();

        while (true)
        {
            WriteLine("waiting for client...");
            TcpClient client = await listener.AcceptTcpClientAsync();
            Task t = RunClientRequest(client);
        }
    }
    catch (Exception ex)
    {
        WriteLine($"Exception of type {ex.GetType().Name}, Message: {ex.Message}");
    }
}
```

To read and write from and to the client, the GetStream method of the TcpClient returns a NetworkStream. First you need to read the request from the client. You do this by using the ReadAsync method. The ReadAsync method fills a byte array. This byte array is converted to a string using the Encoding class. The information received is written to the console and passed to the ParseRequest helper method. Depending on the result of the ParseRequest method, an answer for the client is created and returned to the client using the WriteAsync method.

```
private Task RunClientRequestAsync(TcpClient client)
{
    return Task.Run(async () =>
    {
        try
        {
            using (client)
            {
                WriteLine("client connected");

                using (NetworkStream stream = client.GetStream())
                {
bool completed = false;
do
{
    byte[] readBuffer = new byte[1024];
    int read = await stream.ReadAsync(
        readBuffer, 0, readBuffer.Length);
    string request =
Encoding.ASCII.GetString(readBuffer, 0, read);
    WriteLine($"received {request}");

    string sessionId;
    string result;
    byte[] writeBuffer = null;
    string response = string.Empty;

    ParseResponse resp = ParseRequest(
        request, out sessionId, out result);
    switch (resp)
    {
        case ParseResponse.OK:
            string content = $"{STATUSOK}::{SESSIONID}::
{sessionId}";
            if (!string.IsNullOrEmpty(result))
            {
                content += $"{SEPARATOR}{result}";
            }
            response = $"{STATUSOK}{SEPARATOR}{SESSIONID}
{SEPARATOR}" +
                $"{sessionId}{SEPARATOR}{content}";
            break;
        case ParseResponse.CLOSE:
            response = $"{STATUSCLOSED}";
            completed = true;
            break;
        case ParseResponse.TIMEOUT:
            response = $"{STATUSTIMEOUT}";
            break;
        case ParseResponse.ERROR:
            response = $"{STATUSINVALID}";
            break;
        default:
            break;
    }
    writeBuffer = Encoding.ASCII.GetBytes(response);
    await stream.WriteAsync(writeBuffer, 0,
writeBuffer.Length);
    await stream.FlushAsync();
    WriteLine($"returned {Encoding.ASCII.GetString(
        writeBuffer, 0, writeBuffer.Length)}");
    } while (!completed);
}
}
}
catch (Exception ex)
{
    WriteLine($"Exception in client request handling" +
        "of type {ex.GetType().Name}, Message: {ex.Message}");
}
WriteLine("client disconnected");
});
}
```

The ParseRequest method parses the request and filters out the session identifier. The first call to the server (HELO) is the only call where a session identifier is not passed from the client; here it is created using the SessionManager. With the second and later requests, requestColl[0] must contain ID, and requestColl[1] must contain the session identifier. Using this identifier, the TouchSession method updates the current time of the session identifier if the session is still valid. If it is not valid, a timeout is returned. For the functionality of the service, the ProcessRequest method is invoked:

```
private ParseResponse ParseRequest(string request, out string sessionId,
    out string response)
{
    sessionId = string.Empty;
    response = string.Empty;
    string[] requestColl = request.Split(
        new string[] { SEPARATOR },
StringSplitOptions.RemoveEmptyEntries);

    if (requestColl[0] == COMMANDHELO)  // first request
    {
        sessionId = _sessionManager.CreateSession();
    }
    else if (requestColl[0] == SESSIONID)  // any other valid request
    {
        sessionId = requestColl[1];

        if (!_sessionManager.TouchSession(sessionId))
        {
            return ParseResponse.TIMEOUT;
        }

        if (requestColl[2] == COMMAND BYE)
        {
            return ParseResponse.CLOSE;
        }
        if (requestColl.Length >= 4)
        {
            response = ProcessRequest(requestColl);
        }
    }
    else
    {
        return ParseResponse.ERROR;
    }
    return ParseResponse.OK;
}
```

The ProcessRequest method contains a switch statement to handle the different requests. This method in turn makes use of the CommandActions class to echo or reverse the message received. To store and retrieve the session state, the SessionManager is used:

```
private string ProcessRequest(string[] requestColl)
{
    if (requestColl.Length < 4)
        throw new ArgumentException("invalid length requestColl");

    string sessionId = requestColl[1];
    string response = string.Empty;
    string requestCommand = requestColl[2];
```
