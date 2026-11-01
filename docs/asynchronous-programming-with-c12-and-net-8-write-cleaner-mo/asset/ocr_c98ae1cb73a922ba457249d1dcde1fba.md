```
using System;
using System.Threading.Tasks;
public class Program
{
    public static async Task Main()
    {
        // Example of CPU-bound work offloaded to a background thread
        Task<int> task = Task.Run(() =>
        {
            return CalculateSum(10, 20);
        });
        // Continue asynchronously after the task completes
        int result = await task;
        Console.WriteLine("Sum: " + result);
    }
    public static int CalculateSum(int a, int b)
    {
        // Simulate CPU-bound work
        int sum = 0;
        for (int i = a; i <= b; i++)
```