# LISTING 11-11 The command-handler switchboard has been simplified and will change less frequently.

```
class Program
{
    private delegate void CommandHandler(IEnumerable<string> parameters);
    private static ISensor CurrentSensor;

    static void Main(string[] args)
    {
        while (true)
        {
            Console.Write("> ");
            var input = Console.ReadLine() ?? string.Empty;
            var tokens = input.Split(' ');

            if (tokens.Length < 1)
            {
                Console.WriteLine("Please supply a command");
                continue;
            }

            var command = tokens.First();
            var parameters = tokens.Skip(1);

            var handlers = new Dictionary<string, CommandHandler>
            {
                {"select", SelectTool},
                {"move", Move},
                {"measure", Measure},
                {"rotate", Rotate},
                {"adjust-height", AdjustHeight},
                {"quit", Quit}
            };

            if (!handlers.ContainsKey(command))
            {
                Console.WriteLine($"Unrecognized command: {command}");
            }
            else
            {
                handlers[command].Invoke(parameters);
            }
        }
        // ...
    }
}
```