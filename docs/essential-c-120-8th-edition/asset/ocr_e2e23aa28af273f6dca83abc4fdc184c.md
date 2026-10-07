11. async/await with
the Windows UI

10. Task Schedulers and
the Synchronization Context

9. Asynchronous Lambdas
and Local Functions

8. Returning void from
an Asynchronous Method

7. Using LINQ with
IEnumerable

1. Synchronously Invoking
a High-Latency Operation

2. Asynchronously Invoking
a High-Latency Operation
Using the TPL

3. The Task-Based Asynchronous
Pattern with async and await

4. Introducing Asynchronous
Return of ValueTask

5. Asynchronous Streams

6. IDisposable and
the await
Declaration and Statement

# Programming the
Task Based Asynchronous
Pattern

LISTING 20.1: A Synchronous Web Request

```
using System;
using System.IO;
using System.Net;
```

```
public static class Programn{
    public static HttpClient HttpClient { get; set; } = new();
    public const string DefaultUrl = "https://IntelliTect.com";
}
```

```
public static void Main(string[] args)
{
    if (args.Length == 0)
    {
        Console.WriteLine("ERROR: No findText argument specified.");
        return;
    }
    string findText = args[0];

    string url = DefaultUrl;
    if (args.Length > 1)
    {
        url = args[1];
        // Ignore additional parameters
    }
    Console.WriteLine(
        $"Searching for {findText} at URL {url}.");
}
```