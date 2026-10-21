
```csharp
public class ThreadExp
{
    public static int Main(String[] args)
    {
        Console.WriteLine("Example of Threading");
        AOne a = new AOne();
        Thread T1 = new Thread(new ThreadStart(a.First)); // Creating thread T1
        T1.Start(); // Starting thread T1
        Console.WriteLine("T1 thread started.");
        Thread T2 = new Thread(new ThreadStart(AOne.Second)); // Creating T2
        T2.Start(); // Starting thread T2
        Console.WriteLine("T2 thread started.");
        return 0;
    }
}
```

In the above C# program, two threads T1 and T2 have been created and started using the Start() method of the Thread class. In case of T1 thread, the execution starts from First method defined in the AOne class while in case of T2 thread the execution starts from Second method, which is a static method. The output of the above program is:

```text
Example of Threading
First method of AOne class is running on T1 thread.
T1 thread started.
Second method of AOne class is running on T2 thread.
T2 thread started.
The First method called by T1 thread has ended.
The Second method called by T2 thread has ended.
Press any key to continue . . .
```

We can also create a thread and attach a timer to it as illustrated by Program 19.2. Program 19.2 starts a thread and displays the thread information after every second. When the Enter key is pressed, the thread stops. On pressing the Enter key again, the thread resumes. On pressing the Enter key again, the thread is destroyed.

### Program 19.2 | USING TIMER

```csharp
using System;
using System.Collections.Generic;
using System.Text;
using System.Timers;

namespace ThreadTimers
{
    class Program
    {
        static void Main()
        {
            Timer time = new Timer();          // Doesn't require any args
            time.Interval = 1000;
            time.Elapsed += time_Elapsed;      // Uses an event
            time.Start();                      // Start the timer

            Console.ReadLine();
            time.Stop();
            Console.WriteLine("Timer Thread stopped. Enter again to start. (Twice entering would destroy the Thread.)"); // Pause the timer
            Console.ReadLine();
            time.Start(); // Resume the timer
            Console.ReadLine();
            Console.WriteLine("Timer destroyed!");
            time.Dispose(); // Destroy the Timer Thread
        }
        static void Display(object ObjTime)
        {
            // This runs on a pooled thread
            Console.WriteLine(ObjTime); // Writes "tick..."
        }
        static void time_Elapsed(object sender, EventArgs e)
        {
            Console.Write("The Time is passing by : ");
            Console.WriteLine(DateTime.Now);
        }
    }
}
```

In the above program, a thread with a timer is created. The Start and Stop methods of the timer are used to start and stop the timer and the thread. The output of Program 19.2 is:

```text
The Time is passing by : 7/25/2007 4:03:24 PM
The Time is passing by : 7/25/2007 4:03:25 PM
The Time is passing by : 7/25/2007 4:03:26 PM
The Time is passing by : 7/25/2007 4:03:27 PM
The Time is passing by : 7/25/2007 4:03:28 PM
The Time is passing by : 7/25/2007 4:03:29 PM
The Time is passing by : 7/25/2007 4:03:30 PM
The Time is passing by : 7/25/2007 4:03:31 PM
The Time is passing by : 7/25/2007 4:03:32 PM
The Time is passing by : 7/25/2007 4:03:33 PM
The Time is passing by : 7/25/2007 4:03:34 PM
The Time is passing by : 7/25/2007 4:03:35 PM
The Time is passing by : 7/25/2007 4:03:36 PM
The Time is passing by : 7/25/2007 4:03:37 PM
The Time is passing by : 7/25/2007 4:03:38 PM
The Time is passing by : 7/25/2007 4:03:39 PM
The Time is passing by : 7/25/2007 4:03:40 PM
The Time is passing by : 7/25/2007 4:03:41 PM
```

## 19.4 SCHEDULING A THREAD

In C#, threads can be scheduled by setting the priority of the thread using the Priority property of the Thread class. We can provide the following values for the Priority property of a specific thread:

- Highest
- Normal
- Lowest
- AboveNormal
- BelowNormal

For example, to set the priority of `tr1` thread as Lowest, we can use the code:
`tr1.Priority = ThreadPriority.Lowest;`

After a priority is set for a thread, the thread runs according to its priority. This means that a BelowNormal priority thread runs after the Normal priority thread but before the Lowest priority thread. Program 19.3 illustrated the use of Priority property.

### Program 19.3 | SETTING THREAD PRIORITY

```csharp
using System;
using System.Threading;
public class ABC
{
    public void A()
    {
        Console.WriteLine("Thread A");
        Console.WriteLine("Priority of Thread A is: " + Thread.CurrentThread.Priority.ToString());
        Console.WriteLine(" ");
        Thread.Sleep(5000);
        Console.WriteLine("Thread with " + Thread.CurrentThread.Priority.ToString() + " has run");
        Console.WriteLine(" ");
    }
    public void B()
    {
        Console.WriteLine("Thread B");
        Console.WriteLine("Priority of Thread B is: " + Thread.CurrentThread.Priority.ToString());
        Console.WriteLine(" ");
        Thread.Sleep(5000);
        Console.WriteLine("Thread with " + Thread.CurrentThread.Priority.ToString() + " has run");
        Console.WriteLine(" ");
    }
    public static void C()
    {
        Console.WriteLine("Thread C");
        Console.WriteLine("Priority of Thread C is: " + Thread.CurrentThread.Priority.ToString());
        Console.WriteLine(" ");
        Thread.Sleep(3000);
        Console.WriteLine("Thread with " + Thread.CurrentThread.Priority.ToString() + " has run");
        Console.WriteLine(" ");
    }
}
public class ScheduleExp
{
    public static int Main(String[] args)
    {
        Console.WriteLine("..........Scheduling Threads");
        Console.WriteLine(" ");
        ABC a1 = new ABC();
        Thread tr1 = new Thread(new ThreadStart(a1.A));
        Thread tr2 = new Thread(new ThreadStart(a1.B));
        Thread tr3 = new Thread(new ThreadStart(ABC.C));
        Console.WriteLine("Priority of Main method is: " + Thread.CurrentThread.Priority.ToString());
        Console.WriteLine(" ");
        tr1.Name = " Thread A";
        tr2.Name = " Thread B";
        tr3.Name = " Thread C";
        tr1.Priority = ThreadPriority.AboveNormal;
        tr2.Priority = ThreadPriority.BelowNormal;
        tr3.Priority = ThreadPriority.Lowest;
        tr1.Start();
        tr2.Start();
        tr3.Start();
        return 0;
    }
}
```

In the above C# program, the priorities of the three threads tr1, tr2, and tr3 have been set to AboveNormal, BelowNormal and Lowest. The priority of Main thread is also displayed using the Console.WriteLine() method. The output of the above program is:

```text
............Scheduling Threads
Priority of Main method is: Normal
Thread A
Priority of Thread A is: AboveNormal
Thread B
Priority of Thread B is: BelowNormal
Thread C
Priority of Thread C is: Lowest
Thread with Lowest has run
Thread with AboveNormal has run
Thread with BelowNormal has run
Press any key to continue . . .
```

## 19.5 SYNCHRONISING THREADS

In C#, threads can be synchronised by using methods such as Sleep and Join of the Thread class. We can use these methods to block a thread for a specific time period until another thread completes its processing. In a multithreading environment multiple threads are run for the execution of a program. These threads may run asynchronously. As a result, one thread can access the resources such as network connection and file handles that are being used by another thread. This may corrupt the data unpredictably. Therefore it is necessary to synchronise the access to resources by different threads.

Synchronisation of threads means coordinating the access to resources for different threads running for execution. To synchronise the threads, we can either block a thread till the time another thread has completed its tasks or lock access to a resource. The Thread class provides methods such as SpinWait and Suspend that help block a thread for a specific time period. In C#, we can use the lock keyword to lock access to a resource for a specific thread. The lock keyword marks a block of C# program statements as a critical section by first obtaining a mutually exclusive lock for an object. After obtaining the lock, the program statements are executed. When the program statements have been executed, the mutually exclusive lock is released. The syntax for using the lock keyword is:

```csharp
lock (obj) // obj is the object being synchronised
{
    // set of statements to be synchronised
}
```

Program 19.4 shows how to use the lock keyword and Sleep method for thread synchronisation.

### Program 19.4 SYNCHRONISING THREADS

```csharp
using System;
using System.Threading;

class ABC
{
    private object thislock = new object();
    public void A()
    {
        Console.WriteLine("Starting " + Thread.CurrentThread.Name.ToString());
        int x = 10, z = 30;
        int sum = 0;
        lock (thislock)
        {
            sum = x + z;
            Console.WriteLine(sum);
        }
        Thread.Sleep(5000);
        Console.WriteLine(Thread.CurrentThread.Name.ToString() + " is stopped");
    }
}

public class SyncExp
{
    public static void Main()
    {
        ABC a1 = new ABC();
        Thread t1 = new Thread(new ThreadStart(a1.A));
        Thread t2 = new Thread(new ThreadStart(a1.A));
        t1.Name = "T1";
        t2.Name = "T2";
        t1.Start();
        t2.Start();
    }
}
```
