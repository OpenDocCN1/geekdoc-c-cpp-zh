# **key-value-store/Program.cs**

```
```
using System.CommandLine;
using KV;

IServer<string> server = new Server();
var client = new Client(server);

var rootCommand = client.BuildRootCommand();
await rootCommand.InvokeAsync(args);
```
```