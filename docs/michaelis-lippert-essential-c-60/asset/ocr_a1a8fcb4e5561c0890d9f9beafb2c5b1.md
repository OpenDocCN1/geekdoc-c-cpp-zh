methods. As a result, if you have access to the TPL but are using APM-related APIs, you can still use the TPL to invoke them.

# APM with the TPL and CPS

The TPL includes a set of overloads on FromAsync for invoking APM methods. Listing C.4 provides an example. The same listing expands on the other APM examples to support downloading of multiple URLs; see Output C.2.

# LISTING C.4: Using the TPL to Call the APM

```
using System;
using System.IO;
using System.Net;
using System.Linq;
using System.Threading.Tasks;

public class Program
{
    static private object ConsoleSyncObject =
        new object();

    public static void Main(string[] args)
    {
        string[] urls = args;
        if (args.Length == 0)
        {
            urls = new string[]
            {
                "http://www.habitat-spokane.org",
                "http://www.partnersintl.org",
                "http://www.iassist.org",
                "http://www.fh.org",
                "http://www.worldvision.org"
            };
        }

        Task[] tasks = new Task[urls.Length];
        for (int line = 0; line < urls.Length; line++)
        {
            tasks[line] = DisplayPageSizeAsync(
                urls[line], line);
        }

        while (!Task.WaitAll(tasks, 50))
        {
            DisplayProgress(tasks);
        }
        Console.SetCursorPosition(0, urls.Length);
    }
}
```