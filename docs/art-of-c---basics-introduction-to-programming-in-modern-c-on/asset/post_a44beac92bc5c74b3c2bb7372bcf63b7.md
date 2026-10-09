
Regardless of how you add the package reference, the project XML file ends up getting the following line:

```xml
<ItemGroup>
    <PackageReference Include="System.CommandLine" Version="2.0.0-beta1.21216.1" />
</ItemGroup>
```

> The version number of the library might be different when you read this book. Check the most recent version from the official NuGet website.

For our key-value store project, we will borrow some CLI commands from Redis, redis.io/commands, for inspiration.

In particular, we will try to implement the following methods:

- ping
- keys
- get key
- set key value
- del key
- exists key

Note that Redis is based on the client-server architecture. That is, a client program and a server program run in separate processes, possibly on different machines, and they communicate over the network, e.g., over the local network or over the Internet.

For the project in this lesson, however, we will create a single program that includes both "client" and "server" components.

In theory, we can refactor the code to create two separate programs, one for the client and the other for the server. In order to do that, we will need to add a network communication layer between the client and the server. For the sample code, we merely use the internal API calls.

## 29.3. Sample Code Snippets - key-value-store

Note that we set the command name to `kvstore` in the project XML file for this program:

```xml
<PropertyGroup>
  <AssemblyName>kvstore</AssemblyName>
</PropertyGroup>
```

Here's the main (client) program:

```csharp
// key-value-store/Program.cs (lines 4-8)
4 IServer<string> server = new Server();
5 var client = new Client(server);
7 var rootCommand = client.BuildRootCommand();
8 await rootCommand.InvokeAsync(args);
```

It reads the command line argument, and passes it to the "client".

Note that this program has a rather similar structure as the sample code of the previous lesson. We use an abstraction for the "server" component using an interface, `IServer<string>`.

A "client" instance is constructed by taking a concrete implementation of this interface type `IServer<string>` as an argument.

Although it is beyond the scope of this book, this kind of pattern can be used for "dependency injection" (or, DI for short), if needed. The readers are encouraged to look up on this topic, if interested.

![](img/25af69ec45b3c0b589a8dccd0c2a88be_469_0.png)

As stated, software development requires a lot of different skills and knowledge beyond mere "programming".

The `Client` encapsulates the functionalities of the "CLI client".

The `System.CommandLine` library more or less requires the program to start as follows:

```csharp
await rootCommand.InvokeAsync(args);
```

We are using the async version of the `Invoke()` method here. As stated, the generated `Main()` method of this program will be an async version. The `rootCommand` is a variable for type `System.CommandLine.RootCommand`.

The client supports a number of different "sub-commands" below the root command.

### key-value-store/Client.cs (lines 5-33)

```csharp
public sealed class Client {
    private IServer<string> server;

    public Client(IServer<string> server) => this.server = server;

    public RootCommand BuildRootCommand() {
        var rootCommand = new RootCommand(description:
                "A demo app to store key-value data.")
        {
                new Option<bool>(new string[]{"--reset-all"}, "Delete all data and start fresh"),

                new PingCommand(server),
                new GetCommand(server),
                new SetCommand(server),
                new KeysCommand(server),
                new ExistsCommand(server),
                new DelCommand(server),
        };
        rootCommand.Handler = CommandHandler.Create<bool>(RootCommandHandler);

        return rootCommand;
    }

    private void RootCommandHandler(bool resetAll) {
        // Placeholder for now.
        Console.WriteLine($"resetAll: {resetAll}");
    }
}
```

A series of sample commands:

### key-value-store/Commands/Ping.cs (lines 5-20)

```csharp
public sealed class PingCommand : Command {
    private IServer<string> server;

    public PingCommand(IServer<string> server,
        string name = "ping",
        string description = "Ping the server") : base(name, description) {
        this.server = server;

        Handler = CommandHandler.Create(Ping);
    }

    public void Ping() {
        var result = server.Ping();
        Console.WriteLine($"Ping: {result}");
    }
}
```

### key-value-store/Commands/Get.cs (lines 5-26)

```csharp
public sealed class GetCommand : Command {
    private IServer<string> server;

    public GetCommand(IServer<string> server,
        string name = "get",
        string description = "Get the value of a key")
        : base(name, description) {
        this.server = server;

        AddOption(new Option<string>(new[] { "--key", "-k" }, "Key"));
        Handler = CommandHandler.Create<string>(Get);
    }

    public void Get(string key) {
        var value = server.Get(key);
        if (value is not null) {
            Console.WriteLine($"Value {value} for {key}");
        } else {
            Console.WriteLine($"Item for {key} does not exist.");
        }
    }
}
```

### key-value-store/Commands/Set.cs (lines 5-26)

```csharp
public sealed class SetCommand : Command {
    private IServer<string> server;

    public SetCommand(IServer<string> server,
                string name = "set",
                string description = "Set the value of a key to the given value") : base(name, description) {
        this.server = server;

        AddOption(new Option<string>(new[] { "--key", "-k" }, "Key"));
        AddOption(new Option<string>(new[] { "--value", "-v" }, "Value as a string"));
        Handler = CommandHandler.Create<string, string>(Set);
    }

    public void Set(string key, string value) {
        var oldValue = server.Set(key, value);
        if (oldValue is not null) {
            Console.WriteLine($"Replaced {oldValue} with {value} for {key}.");
        } else {
            Console.WriteLine($"Created a new item for {key} with value {value}.");
        }
    }
}
```

### key-value-store/Commands/Keys.cs (lines 5-20)

```csharp
public sealed class KeysCommand : Command {
    private IServer<string> server;

    public KeysCommand(IServer<string> server,
        string name = "keys",
        string description = "List all keys") : base(name,
        description) {
        this.server = server;

        Handler = CommandHandler.Create(Keys);
    }

    public void Keys() {
        var keys = server.Keys();
        Console.WriteLine($"All keys: {string.Join(", ", keys)}");
    }
}
```

### key-value-store/Commands/Exists.cs (lines 5-24)

```csharp
public sealed class ExistsCommand : Command {
    private IServer<string> server;

    public ExistsCommand(IServer<string> server,
                        string name = "exists",
                        string description = "Returns true if a key exists, false otherwise") : base(name, description) {
        this.server = server;

        AddOption(new Option<string>(new[] { "--key", "-k" }, "Key"));
        Handler = CommandHandler.Create<string>(Exists);
    }

    public void Exists(string key) {
        if (server.Exists(key)) {
            Console.WriteLine($"{key} exists");
        } else {
            Console.WriteLine($"{key} does not exist");
        }
    }
}
```

### key-value-store/Commands/Del.cs (lines 5-25)

```csharp
public sealed class DelCommand : Command {
    private IServer<string> server;

    public DelCommand(IServer<string> server, 
        string name = "del",
        string description = "Delete the entry for a given key") :
        base (name, description) {
            this . server = server ;

            AddOption(new Option <string>(new[] { "--key" , "-k" }, "Key"));
            Handler = CommandHandler.Create <string>(Del);
        }

    public void Del (string key) {
        var oldValue = server . Del(key) ;
        if (oldValue is not null) {
            Console.WriteLine($"Deleted {oldValue} for {key}." );
        } else {
            Console.WriteLine($"Item for {key} does not exist." );
        }
    }
}
```

Note that the "client" commands rely on the server implementations. That is, the Server class provides the actual implementations for these commands:
