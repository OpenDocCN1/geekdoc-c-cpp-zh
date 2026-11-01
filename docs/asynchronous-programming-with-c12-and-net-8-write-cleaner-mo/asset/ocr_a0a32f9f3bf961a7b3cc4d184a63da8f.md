In this example, the `Task.Run` operation throws an `InvalidOperationException`, which is caught and handled in the `catch` block of the `Main` method.

# 5. Using async/await for Asynchronous Code:

The `async/await` keywords in C# provide a more natural and readable way to write asynchronous code. `async` methods can await asynchronous operations without blocking the execution thread.

```
```csharp
using System;

using System.Threading.Tasks;

public class Program
{
    public static async Task Main()
    {
        int result = await CalculateSumAsync(10, 20);
        Console.WriteLine("Sum: " + result);
    }
    public static async Task<int> CalculateSumAsync(int a, int b)
    {
        await Task.Delay(1000); // Simulate asynchronous delay
```
```