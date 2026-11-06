```
public static void CallChild()
{
    Console.WriteLine("Start child thread");
}
static void Main(string[] args)
{
    ThreadStart child1 = new ThreadStart(CallChild);
    Console.WriteLine("Creating child thread");
    Thread child2 = new Thread(child1);
    child2.Start();
    Console.Read();
}
}
}
```

**On compiling and executing the code, the output is:**

Start child thread

Creating child thread

# Managing Threads

When there is a need to pause a thread for a period of time so that another thread can execute, the **Thread.Sleep()** method is used. The method takes a single argument stating time in milliseconds.

# Example:

```
using System;
using System.Threading;

namespace Multithreaded
{
```