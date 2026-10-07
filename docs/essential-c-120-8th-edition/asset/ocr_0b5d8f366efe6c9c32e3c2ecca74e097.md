# Chapter 21: Iterating in Parallel

runs on another thread that the current thread can cancel it if necessary—the same solution used in Listing 21.5.

LISTING 21.10: Canceling a PLLinq Query

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading;
using System.Threading.Tasks;

public static class Program
{
    public static List<string> ParallelEncrypt(
        List<string> data,
        Cancellation cancellationToken)
    {
        int governor = 0;
        return data.AsParallel().WithCancellation(
            cancellationToken).Select(
            (item) =>
            {
                if (Interlocked.CompareExchange(
                    ref governor, 0, 100) == 0)
                {
                    Console.Write('.');
                }
                Interlocked.Increment(ref governor);
                return Encrypt(item);
            })
        ).ToList();
    }

public static async Task Main()
{
    Console originalColor = Console.ForegroundColor;
    List<string> data = Utility.GetData(100000).ToList();

    using CancellationTokenSource cts = new();

    Task task = Task.Run(() =>
    {
        data = ParallelEncrypt(data, cts.Token);
    }, cts.Token);

    Console.WriteLine("Press any key to Exit.");
    Task<int> cancelTask = Console.ReadKeyAsync(cts.Token);
```