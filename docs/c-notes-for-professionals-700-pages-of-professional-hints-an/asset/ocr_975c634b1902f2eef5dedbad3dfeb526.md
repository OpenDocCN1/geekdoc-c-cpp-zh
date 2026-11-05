```
```csharp
        }
    }
    catch
    {
        // if expetion is throw check if socket is connected because than you can startreive again else Disconnect
        if (!_receiveSocket.Connected)
        {
            Disconnect();
        }
        else
        {
            StartReceiving();
        }
    }
}

private void Disconnect()
{
    // Close connection
    _receiveSocket.Disconnect(true);
    // Next line only apply for the server side receive
    ClientController.RemoveClient(_clientId);
    // Next line only apply on the Client Side receive
    Here you want to run the method TryToConnect()
}
```
```

So we've setup a server that can receive and listen for incoming connections. When a clients connect it will be added to a list of clients and every client has his own receive class. To make the server listen:

```
```csharp
Listener listener = new Listener();
listener.StartListening();
```
```

# Some Classes I use in this example

```
```csharp
class Client
{
    public Socket _socket { get; set; }
    public ReceivePacket Receive { get; set; }
    public int Id { get; set; }

    public Client(Socket socket, int id)
    {
        Receive = new ReceivePacket(socket, id);
        Receive.StartReceiving();
        _socket = socket;
        Id = id;
    }
}

static class ClientController
{
    public static List<Client> Clients = new List<Client>();

    public static void AddClient(Socket socket)
    {
        Clients.Add(new Client(socket,Clients.Count));
    }

    public static void RemoveClient(int id)
    {
```
```