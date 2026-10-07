# Chapter 22: Thread Synchronization

```
{
    if (args?.Length > 0) { _ = int.TryParse(args[0], out _Total); }
    Console.WriteLine("Increment and decrementing " + 
        $\${\_Total} times...");

    // Use Task.Factory.StartNew for .NET 4.0
    Task task = Task.Run(() => Decrement());

    // Increment
    for (int i = 0; i < _Total; i++)
    {
        lock (_Sync)
        {
            _Count++;
        }
    }
    task.Wait();
    Console.WriteLine("Count = {_Count}");
    return _Count;
}

public static void Decrement()
{
    for (int i = 0; i < _Total; i++)
    {
        lock (_Sync)
        {
            _Count--;
        }
    }
}
```

OUTPUT 22.3

Count = 0