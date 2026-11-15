Furthermore, anytime a method is long-running, it is probable that multithreaded programming is going to be required—invoking the long-running method asynchronously. As developers write more multithreaded code, a common set of scenarios and programming patterns for handling those scenarios emerges. The key scenarios relate to notifications of when a thread performing a long-running action completes.

One particularly prominent pattern established is the Asynchronous Programming Model (APM) pattern. Given a long-running synchronous method X(), APM uses a BeginX() method to start X() equivalent work asynchronously and an EndX() method to conclude it. (Henceforth we will name these methods X, BeginX, and EndX.)

# # Calling the APM

Listing 19.14 demonstrates the pattern using the System.Net.WebRequest class to download a Web page. Fulfilling Web requests is a relatively long-running task since they involve network I/O and they are very likely to go across the Internet. WebRequest supports the APM pattern with the methods BeginGetResponse() (BeginX) and EndGetResponse() (EndX)—asynchronous versions of the synchronous GetResponse() (X) method.

# ## LISTING 19.14: Calling the APM on WebRequest

```
using System;
using System.IO;
using System.Net;
using System.Linq;

public class Program
{
    public static void Main(string[] args)
    {
        string url = "http://www.intelliTecture.com";
        if (args.Length > 0)
        {
            url = args[0];
        }

        Console.WriteLine(url);
        WebRequest webRequest = WebRequest.Create(url);

        IAsyncResult asyncResult =
            webRequest.BeginGetResponse(null, null);
```