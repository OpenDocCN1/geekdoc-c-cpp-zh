```
```csharp
namespace KV;
using System.CommandLine;
using System.CommandLine.Invocation;

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
```