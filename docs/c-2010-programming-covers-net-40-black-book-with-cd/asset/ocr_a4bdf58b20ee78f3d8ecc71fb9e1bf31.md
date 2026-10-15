![](bbox=[0.115, 0.056, 0.805, 0.265])

Figure 31.7: Setting a Thread's Priority

Let's learn how to determine the thread state.

# Determining State of a Thread

The thread state means the status of a thread. It is determined by the ThreadState property of the Thread class. Listing 31.8 shows the MyThreadsState application (also available on the CD) in which you learn to determine the status of a thread at various levels:

# Listing 31.8: Showing the Code of the MyThreadsState Application

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
namespace MyThreadsState
{
public class Program
{
    static Thread FirstThread;
    static Thread SecondThread;
    static Thread ThirdThread;
    public static void Main(string[] args)
    {
        FirstThread = new Thread(FirstFunction);
        SecondThread = new Thread(SecondFunction);
        ThirdThread = new Thread(ThirdFunction);
        FirstThread.Name = "First Thread";
        SecondThread.Name = "Second Thread";
        ThirdThread.Name = "Third Thread";
        StateOfThreads("Main() Before Starting the Threads..");
        FirstThread.Start();
        SecondThread.Start();
        ThirdThread.Start();
        StateOfThreads("Main() Before Ending the Threads...");
    }
    // writting a function for determining the state of the threads
    public static void StateOfThreads(string position)
    {
        Console.WriteLine("\r\nIn {0}", position);
        Console.WriteLine("Thread Name : {0}, Thread State : {1}", FirstThread.Name, FirstThread.ThreadState);
        Console.WriteLine("Thread Name : {0}, Thread State : {1}", SecondThread.Name, SecondThread.ThreadState);
        Console.WriteLine("Thread Name : {0}, Thread State : {1}\r\n", ThirdThread.Name, ThirdThread.ThreadState);
    }
}
```