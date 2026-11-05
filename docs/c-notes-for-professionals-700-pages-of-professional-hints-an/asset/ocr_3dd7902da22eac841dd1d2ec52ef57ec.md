```
Console.WriteLine("Starting a useless process...");
Stopwatch stopwatch = Stopwatch.StartNew();
int delay = await UselessProcessAsync(1000);
stopwatch.Stop();
Console.WriteLine("A useless process took {0} milliseconds to execute.",
stopwatch.ElapsedMilliseconds);
}
public async Task<int> UselessProcessAsync(int x)
{
    await Task.Delay(x);
    return x;
}
```

Output:

```
"Starting a useless process..."

**... 1 second delay...**

"A useless process took 1000 milliseconds to execute."
```

The keyword pairs async and await can be omitted if a Task or Task<T> returning method only returns a single asynchronous operation.

*Rather than this:*

```
public async Task PrintAndDelayAsync(string message, int delay)
{
    Debug.WriteLine(message);
    await Task.Delay(x);
}
```

*It is preferred to do this:*

```
public Task PrintAndDelayAsync(string message, int delay)
{
    Debug.WriteLine(message);
    return Task.Delay(x);
}
```

Version = 5.0

In C# 5.0 await cannot be used in catch and finally.

Version ≥ 6.0

With C# 6.0 await can be used in catch and finally.

# Section 52.10: for

Syntax: for (initializer; condition; iterator)

+   - The for loop is commonly used when the number of iterations is known.
+   - The statements in the initializer section run only once, before you enter the loop.
+   - The condition section contains a boolean expression that's evaluated at the end of every loop iteration to