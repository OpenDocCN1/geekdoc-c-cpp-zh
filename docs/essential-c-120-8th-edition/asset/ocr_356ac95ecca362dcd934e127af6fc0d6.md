Asynchronously Invoking a High-Latency Operation Using the TPL

# # Asynchronously Invoking a High-Latency Operation
Using the TPL

To address this problem of executing other work in parallel, Listing 20.2 takes a similar approach but instead we use task-based asynchrony with the TPL.

LISTING 20.2: An Asynchronous Web Request

```
using System;
using System.IO;
using System.Net;
using System.Runtime.ExceptionServices;
using System.Threading.Tasks;

public static class Program
{
    public static HttpClient HttpClient { get; set; } = new();
    public const string DefaultUrl = "https://IntelliTest.com";

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
        Console.WriteLine("Searching for '{findText}' at URL '{url}'.");

        Console.Write("Downloading...");
        Task task = HttpClient.GetByteArrayAsync(url)
            .ContinueWith(antecedent => {
                byte[] downloadData = antecedent.Result;
                Console.Write($"{Environment.NewLine}Searching...");
                return CountOccurrencesAsync(
downloadData, findText);
            });
    }
```