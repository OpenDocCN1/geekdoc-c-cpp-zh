```
namespace KV;
using System.CommandLine;
using System.CommandLine.Invocation;

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