![](bbox=[0.19, 0.06, 0.87, 0.33])

# Figure 31.9: Displaying the Output Without Using the Join() Method

In Figure 31.9, you can see that the Main() thread terminates rapidly after starting the FirstThread thread and the SecondThread thread. However, if you want the Main() thread to stay alive until the FirstThread thread is alive, then apply the Join() method to the FirstThread thread. To understand this more clearly, let’s implement the Join() method in the ThreadJoin project of the ThreadJoin application (also available on the CD), which shows the implementation of the Join() method.

Listing 31.10 shows the code for the ThreadJoin application:

# Listing 31.10: Showing the Code of the ThreadJoin Application

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
namespace ThreadJoin
{
class Program {
    static void Main(string[] args)
    {
        Thread FirstThread = new Thread(FirstFunction);
        Thread SecondThread = new Thread(SecondFunction);
        Thread ThirdThread = new Thread(ThirdFunction);
        Console.WriteLine("\nThreading Starts...\n");
        FirstThread.Start();
        SecondThread.Start();
        ThirdThread.Start();
        FirstThread.Join(); //Code to join the threads
        Console.WriteLine("\nThe Main() is Ending...\n");
    }
    public static void FirstFunction()
    {
        for (int number = 1; number <= 5; number++)
        {
            Console.WriteLine("First Thread Displays: " + number);
            Thread.Sleep(200);
        }
    }
    public static void SecondFunction()
    {
        for (int number = 1; number <= 5; number++)
```