uses cooperative cancellation, a far more polite, robust, and reliable technique for safely canceling a task that is no longer needed. A task that supports cancellation monitors a CancellationToken object (found in the System.Threading namespace) by periodically polling it to see if a cancellation request has been issued. Listing 18.10 demonstrates both the cancellation request and the response to the request. Output 18.6 shows the results.

# LISTING 18.10: Canceling a Task Using CancellationToken

```
using System;
using System.Threading;
using System.Threading.Tasks;
using AddisonWesley.Michaelis.EssentialCSharp.Shared;

public class Program
{
    public static void Main()
    {
        string stars =
            "*".PadRight(Console.WindowWidth-1, '*');
        Console.WriteLine("Push ENTER to exit.");

        CancellationTokenSource cancellationTokenSource=
            new CancellationTokenSource();
        // Use Task.Factory.StartNew<string>() for
        // TPL prior to .NET 4.5
        Task task = Task.Run(
            () =>
                WritePi(cancellationTokenSource.Token),
                cancellationTokenSource.Token);

        // Wait for the user's input
        Console.ReadLine();

        cancellationTokenSource.Cancel();
        Console.WriteLine(stars);
        task.Wait();
        Console.WriteLine();
    }

    private static void WritePi(
        CancellationToken cancellationToken)
    {
        const int batchSize = 1;
        string piSection = string.Empty;
        int i = 0;

        while(!cancellationToken.IsCancellationRequested
            || i == int.MaxValue)
```