# Chapter 22: Thread Synchronization

```
readonly static object _Sync = new();
static int _Total = int.MaxValue;
static int _Count = 0;
```

```
public static async Task<int> Main(string[] args)
{
    if (args.Length > 0) { _Total = int.TryParse(args[0], out _Total); }
    Console.WriteLine("Increment and decrementing " + 
        $\$\{\_Total} times...");

    // Use Task.Factory.StartNew for .NET 4.0
    Task task = Task.Run(() => Decrement());

    // Increment
    for(int i = 0; i < _Total; i++)
    {
        lock(_Sync)
        {
            _Count++;
        }
    }
    await task;
    Console.WriteLine($$\{\_Count}");
    return _Count;
}
```

```
static void Decrement()
{
    for(int i = 0; i < _Total; i++)
    {
        lock(_Sync)
        {
            _Count--;
        }
    }
    Task.Run();
}
```

# Choosing a lock Object

Whether or not the lock keyword or the Monitor class is explicitly used, it is crucial that programmers carefully select the lock object.