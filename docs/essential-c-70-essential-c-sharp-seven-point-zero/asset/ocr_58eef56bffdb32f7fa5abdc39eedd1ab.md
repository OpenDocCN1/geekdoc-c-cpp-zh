# **LISTING 19.30: Canceling a Parallel Loop**

```
using System;
using System.Collections.Generic;
using System.IO;
using System.Threading;
using System.Threading.Tasks;

public class Program
{
    // ...

    static void EncryptFiles(
        string directoryPath, string searchPattern)
    {

        string stars =
            "*".PadRight(Console.WindowWidth-1, '*');

        IEnumerable<string> files = Directory.GetFiles(
            directoryPath, searchPattern,
            SearchOption.AllDirectories);

        CancellationTokenSource cts =
            new CancellationTokenSource();
        ParallelOptions parallelOptions =
            new ParallelOptions
                { CancellationToken = cts.Token };
        cts.Token.Register(
            () => Console.WriteLine("Canceling..."));

        Console.WriteLine("Push ENTER to exit.");

        Task task = Task.Run(() =>
        {
            try
            {
                Parallel.ForEach(
                    files, parallelOptions,
                    (fileName, loopState) =>
                    {
                        Encrypt(fileName);
                    });
            }
            catch(OperationCanceledException){}
        });

        // Wait for the user's input
        Console.Read();

```

![](bbox=[0.86, 0.55, 0.95, 0.6])