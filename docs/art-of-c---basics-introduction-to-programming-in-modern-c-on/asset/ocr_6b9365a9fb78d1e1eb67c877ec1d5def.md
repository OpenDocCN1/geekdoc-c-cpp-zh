# key-value-store/Commands/Del.cs

```
namespace KV;
using System.CommandLine;
using System.CommandLine.Invocation;

public sealed class DelCommand : Command {
    private IServer<string> server;

    public DelCommand(IServer<string> server,
        string name = "del",
        string description = "Delete the entry for a given key") :
        base(name, description) {
        this.server = server;

        AddOption(new Option<string>[]{ "--key", "-k" }, "Key");
        Handler = CommandHandler.Create<string>(Del);
    }

    public void Del(string key) {
        var oldValue = server.Del(key);
        if (oldValue is not null) {
            Console.WriteLine($"Deleted {oldValue} for {key}.");
        } else {
            Console.WriteLine($"Item for {key} does not exist.");
        }
    }
}
```