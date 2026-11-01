in a `try/catch` block to handle any exceptions that may occur during its execution.

# **Example:** Exception Handling in Chained Tasks

```
```csharp
using System;

using System.Threading.Tasks;

public class Program
{
    public static async Task Main()
    {
        try
        {
            int result1 = await Task1();
            int result2 = await Task2(result1);
            int finalResult = await Task3(result2);
            Console.WriteLine("Final Result: " + finalResult);
        }
        catch (Exception ex)
        {
            Console.WriteLine("Error: " + ex.Message);
        }
    }
}
```
```